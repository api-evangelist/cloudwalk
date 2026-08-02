---
name: Collect a payment with an InfinitePay checkout link
description: Create an InfinitePay-hosted checkout link for a basket of items, send the buyer to it, and confirm the payment.
api: openapi/cloudwalk-infinitepay-checkout-openapi.yml
operations: [createCheckoutLink, checkPaymentStatus]
generated: '2026-08-01'
method: generated
---

# Collect a payment with an InfinitePay checkout link

Use this when a Brazilian merchant on InfinitePay needs to be paid for a specific order and
the buyer is not physically present. InfinitePay hosts the payment page; you never render or
handle card data.

## Before you start

- You need the merchant's **InfiniteTag** (`handle`) — their username in the InfinitePay app,
  **without** the leading `$`. This is the only merchant identifier the API takes.
- There is **no API key, token or Authorization header**. See
  `authentication/cloudwalk-authentication.yml`. Because link creation is unauthenticated and
  moves money, get explicit human confirmation of the amount and the handle before calling.
- **All amounts are integers in Brazilian cents.** R$ 10,00 is `1000`. Getting this wrong
  charges the buyer 100x or 1/100x.
- Base URL: `https://api.checkout.infinitepay.io`. Content-Type: `application/json`.

## Step 1 — Create the checkout link

Call **`createCheckoutLink`** (`POST /links`).

Required:
- `handle` — the merchant's InfiniteTag without `$`.
- `items` — at least one `{quantity, price, description}`. `price` is the **unit** price in
  cents.

Strongly recommended:
- `order_nsu` — your own order identifier. If you omit it, InfinitePay generates a random
  value and you lose the correlation back to your system. **This is a correlation key, not an
  idempotency key** — re-calling with the same `order_nsu` creates a *second* link, it does
  not replay the first. Never retry this call blindly.
- `webhook_url` — where InfinitePay POSTs the approval event (see the reconcile skill).
- `redirect_url` — where the buyer lands after paying.

Optional pre-fill: `customer` (`name`, `email`, `phone_number`) and `address`
(`cep`, `street`, `neighborhood`, `number`, `complement`).

```json
{
  "handle": "colakids",
  "items": [
    { "quantity": 1, "price": 1000, "description": "Produto de Exemplo" }
  ],
  "order_nsu": "order-nsu-123",
  "redirect_url": "https://seusite.com/pagamento-concluido",
  "webhook_url": "https://seusite.com/webhook-infinitepay"
}
```

Take `checkout_url` (the provider's reference also shows `link` + `slug` in one place — read
whichever key is present) and send the buyer there. **Persist `order_nsu` and `slug` before
you show the link to anyone**; without them you cannot query the payment later.

## Step 2 — Confirm the payment

Prefer the webhook. Poll only when you cannot receive one.

Call **`checkPaymentStatus`** (`POST /payment_check`) with all four of `handle`,
`order_nsu`, `transaction_nsu` and `slug`. `transaction_nsu` comes back on the webhook or on
the `redirect_url` query string.

A `200` returns `{success, paid, amount, paid_amount, installments, capture_method}`.
Treat the payment as complete only when `paid` is `true`.

`paid_amount` may be **greater** than `amount` when installment fees are passed to the buyer.
Reconcile against `amount`, not `paid_amount`.

## Rules

- **Never trust the browser redirect as proof of payment.** Its parameters are
  buyer-supplied. Confirm with the webhook or `checkPaymentStatus`.
- **Do not retry `createCheckoutLink` on timeout.** There is no idempotency. Query
  `checkPaymentStatus` or ask the merchant before creating another link.
- `capture_method` is `credit_card` or `pix`. Credit supports up to 12 installments.
- Errors are `{"success": false, "message": "..."}` — free text, no error codes. A `400`
  names the offending parameter (`param is missing or the value is empty or invalid: handle`);
  validation is ordered, so fix and re-read the message rather than guessing. See
  `errors/cloudwalk-problem-types.yml`.
- There is no refund, cancel or dispute operation in the public API. Escalate those to the
  merchant in the InfinitePay app.
- There is no published sandbox and no test handle. Do not "try it out" against a real
  InfiniteTag.
