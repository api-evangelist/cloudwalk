# CloudWalk

CloudWalk, Inc. is a payments and financial-infrastructure company (Sunnyvale, CA and São
Paulo, Brazil) building an AI-native transaction layer for small businesses. It operates
three brands: **InfinitePay** (Brazilian acquiring, digital banking, Tap to Pay, hosted
checkout, Pix, credit), **JIM** (phone-as-POS for self-employed workers in the US) and
**Pierre** (personal-finance intelligence on Brazilian Open Finance).

- https://www.cloudwalk.io/
- Developers: https://www.infinitepay.io/desenvolvedores

## Public API surface

| Surface | What it is |
|---|---|
| **InfinitePay Checkout API** — `https://api.checkout.infinitepay.io` | Two JSON operations: `POST /links` creates a hosted checkout payment link, `POST /payment_check` returns its payment status. [Reference](https://www.infinitepay.io/checkout-documentacao) |
| **`payment_approved` webhook** | One event, POSTed to the `webhook_url` set on a link. Answer `200` to acknowledge, `400` to be retried. |
| **InfiniteTap deeplink** — `infinitepaydash://infinitetap-app` | Hands a Tap-to-Pay card transaction from a third-party POS app to the InfinitePay mobile app and back. [Reference](https://www.infinitepay.io/checkout-tap) |

## What CloudWalk publishes — and does not

- **No OpenAPI, Swagger, AsyncAPI or GraphQL.** Every candidate spec path was probed on every
  API and docs host (`/openapi.json`, `/openapi.yaml`, `/swagger.json`, `/api-docs`, `/docs`,
  `/redoc`) and all missed; `/api-docs` returns `401`, an access-controlled internal surface.
  The former documentation host `docs.infinitepay.io` no longer resolves in DNS.
- **No `/.well-known/` documents at all** — no `security.txt`, OIDC/OAuth metadata,
  `api-catalog`, `ai-plugin.json`, or A2A agent card at either the canonical or legacy path.
- **No MCP server** and **no `llms.txt`**.
- **No authentication** on the public API. The merchant is identified by its public
  InfiniteTag `handle` in the request body — no key, token, OAuth or webhook signature.
- **No versioning, deprecation policy, changelog, SLA, rate-limit documentation, error
  reference or sandbox.**
- It **does** run a live status page (https://status.infinitepay.io/), a named
  responsible-disclosure program (security@cloudwalk.io, one-business-day acknowledgement),
  and the full BACEN-mandated regulatory policy set for a supervised Brazilian payment
  institution.

## Artifacts in this repo

Everything below was produced by the API Evangelist enrichment pipeline (2026-08-01), not
published by CloudWalk. The OpenAPI is a faithful transcription of CloudWalk's own live
public reference, with live probe evidence recorded in `x-evidence`.

| Path | What |
|---|---|
| `openapi/` | OpenAPI 3.1 for the Checkout API (2 operations + 1 webhook) |
| `overlays/` | The API Evangelist enhancements over that spec |
| `asyncapi/` | The webhook catalogue (no AsyncAPI is published) |
| `conventions/` | Auth style, money units, error envelope, versioning, and the full InfiniteTap deeplink parameter contract |
| `authentication/` | The (absent) auth model, plus the undocumented `/v2/cards/tokenize` endpoint observed on `authorizer.infinitepay.io` |
| `errors/` | Error responses observed live; CloudWalk publishes no error reference |
| `lifecycle/` | Status page, the `api.infinitepay.io` → `api.checkout.infinitepay.io` host migration, and the missing policies |
| `data-model/` | The entity graph |
| `components/` | Hosted checkout and app-hosted Tap surfaces |
| `conformance/` | Standards conformance plus the BACEN regulatory compliance set |
| `packages/` | First-party POS/plugin libraries and community SDKs |
| `security/` | Domain security probe, and the responsible-disclosure program |
| `well-known/` | The verified-empty discovery surface |
| `agentic-access/` | Recommended `x-agentic-access` contracts per operation |
| `skills/` | Three packaged agent skills grounded in real operationIds |
| `mcp/` | Candidate tool surface only — CloudWalk operates no MCP server, so no `MCPServer` pointer is wired |
| `llms/` | Generated `llms.txt` |
