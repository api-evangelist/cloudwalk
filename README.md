# CloudWalk

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
