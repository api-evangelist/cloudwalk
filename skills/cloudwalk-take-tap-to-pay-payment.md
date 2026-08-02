---
name: Take an in-person Tap to Pay payment with InfiniteTap
description: Hand a card payment from a third-party POS app to the InfinitePay mobile app over the InfiniteTap deeplink and reconcile the result.
api: conventions/cloudwalk-conventions.yml
operations: []
generated: '2026-08-01'
method: generated
---

# Take an in-person Tap to Pay payment with InfiniteTap

Use this when a point-of-sale or field-service app needs to take a contactless card payment
on the merchant's own phone. This is **not an HTTP API** — it is a URI-scheme handoff to the
InfinitePay mobile app, documented at <https://www.infinitepay.io/checkout-tap>. Every
parameter below is quoted from that page; do not invent others.

## Requirements

- Android 11 or later with NFC, or iOS with Apple Tap to Pay.
- The merchant must be logged into the InfinitePay app on that device.
- On iOS, the operator accepts Apple's Tap to Pay terms on first use, binding their iCloud
  account to the merchant account.
- Your app must be able to **receive** a deeplink, so InfinitePay can hand control back.
- No API key is needed. There is no credential to provision.

## Step 1 — Build the deeplink

Base: `infinitepaydash://infinitetap-app`

| Parameter | Required | Notes |
|---|---|---|
| `amount` | yes | Integer cents as a string. **Minimum `100`** (R$ 1,00). |
| `payment_method` | yes | `credit` or `debit`. |
| `installments` | credit only | Max `12`. **Each installment must be at least R$ 1,00** — 10x R$ 10,00 is fine, 12x of the same total is not. |
| `order_id` | yes | Your order identifier, so you can link the transaction back. |
| `result_url` | yes | Your own return deeplink. Use an internal scheme for a seamless handback. URL-encode it. |
| `app_client_referrer` | yes | Your app's referrer string. **Always send the identical value.** |
| `handle` | optional | Merchant InfiniteTag — asserts the app is logged into the expected account. |
| `doc_number` | optional | Merchant document number, digits only — same assertion. |
| `af_force_deeplink` | iOS | Send `true` on iOS. |

Example:

```
infinitepaydash://infinitetap-app?amount=100&payment_method=credit&installments=1&order_id=3262&result_url=mypocapp%3A%2F%2Fexample%2Ftap_result&app_client_referrer=POCApp&handle=merchant_dev_4&doc_number=27346981000144&af_force_deeplink=true
```

Validate `amount`, `installments` and the per-installment minimum **before** you open the
link. There is no error response to parse — a malformed request just fails in the other app.

## Step 2 — Handle the return

InfinitePay calls your `result_url` with query parameters:

`order_id`, `nsu` (transaction identifier, UUID), `aut` (authorization code, may contain
letters), `card_brand`, `user_id`, `access_id`, `handle`, `merchant_document`.

On failure the same parameters come back plus **`warning`** (e.g. `order_id is empty`) when a
field was missing or malformed. **Presence of `warning` is your failure signal** — there is
no status code.

## Step 3 — Reconcile

- Match on `order_id` — and confirm it is one of *your* orders before marking anything paid.
- Persist `nsu` and `aut`. These are what InfinitePay support asks for about a specific sale.
- Record `card_brand` and `merchant_document` for your own reconciliation.

## Rules

- **Test with a real low-value transaction and cancel it afterwards** — this is the
  provider's own guidance. There is no simulator, no test mode and no magic test values.
- Never derive a payment status from the fact that your app was reopened. Only the returned
  parameters, with no `warning`, indicate success.
- Keep `app_client_referrer` stable across releases; it is how CloudWalk attributes traffic
  from your app.
- InfiniteTap is free to integrate; standard InfinitePay card fees apply per sale
  (<https://www.infinitepay.io/taxas>).
- Integration questions go to parcerias@cloudwalk.io.
