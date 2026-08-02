---
name: Reconcile an InfinitePay payment webhook
description: Receive, verify and reconcile the InfinitePay payment_approved webhook against a merchant order.
api: openapi/cloudwalk-infinitepay-checkout-openapi.yml
operations: [onPaymentApproved, checkPaymentStatus]
generated: '2026-08-01'
method: generated
---

# Reconcile an InfinitePay payment webhook

Use this when building the receiving end of an InfinitePay checkout integration. InfinitePay
sends exactly one event type — payment approved — to the `webhook_url` supplied on each
checkout link.

## The contract

- Transport: HTTPS `POST`, `application/json`, to the `webhook_url` you set on the link.
- Subscription is **per link**. There is no webhook registration endpoint and no account-wide
  endpoint configuration.
- Respond **fast** — the provider asks for under about one second.
  - `200 OK` — acknowledged, no retry.
  - `400 Bad Request` — InfinitePay will attempt delivery again.
- No retry schedule, attempt cap or backoff is published. Treat delivery as **at-least-once**.

## Payload

```json
{
  "invoice_slug": "abc123",
  "amount": 1000,
  "paid_amount": 1010,
  "installments": 1,
  "capture_method": "credit_card",
  "transaction_nsu": "UUID",
  "order_nsu": "UUID-do-pedido",
  "receipt_url": "https://comprovante.com/123",
  "items": [ { "quantity": 1, "price": 1000, "description": "Produto de Exemplo" } ]
}
```

Note the name drift: the link you created returned `slug`; the webhook calls the same value
`invoice_slug`. They are one identifier.

## Step 1 — Acknowledge first, process second

Write the raw body to durable storage, return `200`, then process asynchronously. Do not do
order fulfilment inside the request — you will blow the ~1s budget and trigger redeliveries.
Return `400` only when you genuinely want the notification re-sent.

## Step 2 — De-duplicate

**There is no signature and no idempotency guarantee.** De-duplicate on `transaction_nsu`
(UUID). If you have already processed that `transaction_nsu`, acknowledge with `200` and stop.

## Step 3 — Verify before you trust

The webhook is unauthenticated: anyone who learns your endpoint can POST to it. The
provider's own guidance is to validate `order_nsu` against a real order in your system. Do
that, and then independently confirm with **`checkPaymentStatus`** (`POST /payment_check`),
sending `handle`, `order_nsu`, `transaction_nsu` and `slug` (= `invoice_slug`). Only ship
goods or mark the order paid once that call returns `paid: true`.

## Step 4 — Reconcile the money

- Match on `order_nsu` → your order; store `transaction_nsu` and `receipt_url` on it.
- Compare `amount` (in cents) against your order total. **Do not compare against
  `paid_amount`** — that can be higher when installment fees are passed to the buyer.
- Record `capture_method` (`credit_card` or `pix`) and `installments` for settlement
  expectations: credit installments settle differently from Pix.

## Rules

- Never treat the `redirect_url` query parameters (`receipt_url`, `order_nsu`, `slug`,
  `capture_method`, `transaction_nsu`) as authoritative — they come through the buyer's
  browser.
- There is no refund, chargeback, dispute or settlement event. Absence of a webhook is not
  evidence of non-payment; fall back to `checkPaymentStatus`.
- Serve the endpoint over HTTPS only, and keep the URL unguessable.
- See `asyncapi/cloudwalk-infinitepay-webhooks.yml` for the full catalogue and
  `conventions/cloudwalk-conventions.yml` for the cross-cutting semantics.
