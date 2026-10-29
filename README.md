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
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

CloudWalk, Inc. is a Sunnyvale- and São Paulo-based payments and financial-infrastructure company that builds an AI-native transaction layer for small businesses. It operates three consumer-facing brands: InfinitePay, its Brazilian acquirer and digital-banking platform (card machines, Tap to Pay, hosted checkout, payment links, Pix, PJ accounts, credit and CDB); JIM, a phone-as-POS operating system for self-employed workers in the United States; and Pierre, a personal-finance intelligence product built on Brazilian Open Finance. Its public developer surface is deliberately small and integration-shaped rather than platform-shaped: an Integrated Checkout REST API on api.checkout.infinitepay.io that creates hosted payment links and checks their status, an approved-payment webhook, and an InfiniteTap deeplink contract that hands a Tap-to-Pay transaction from a third-party POS app to the InfinitePay mobile app and back. CloudWalk publishes no OpenAPI, no machine-readable discovery documents and no MCP or agent surface. The legal entity behind InfinitePay is CLOUDWALK INSTITUIÇÃO DE PAGAMENTO E SERVIÇOS LTDA (CNPJ 18.189.547/0001-42), a Brazilian payment institution supervised by the Banco Central do Brasil.

**Areas:** Company · Payments · Financial Services · Fintech · Checkout · Point-of-Sale · Acquiring · Pix · Brazil · Banking · Webhook · Tap to Pay

## CloudWalk on APIs.io

Everything profiled for CloudWalk is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/cloudwalk/](https://apis.io/providers/cloudwalk/)** — or go straight to one of the APIs or properties below.

### APIs (3)

- [CloudWalk Checkout Links API](https://apis.io/apis/cloudwalk/cloudwalk-checkout-links-api/) — Create InfinitePay-hosted checkout payment links.
- [CloudWalk InfinitePay Checkout API](https://apis.io/apis/cloudwalk/cloudwalk-infinitepay-checkout-api-api/) — The InfinitePay Checkout API API from CloudWalk — 0 operation(s) for infinitepay checkout api.
- [CloudWalk Payments API](https://apis.io/apis/cloudwalk/cloudwalk-payments-api/) — Query the payment status of a checkout link.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Cloudwalk Infinitepay Webhooks](https://apis.io/asyncapis/cloudwalk/cloudwalk-infinitepay-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [infinitepay-checkout](https://apis.io/servers/cloudwalk/infinitepay-checkout/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Cloudwalk Agentic Access](https://apis.io/agentic-access/cloudwalk/cloudwalk-agentic-access/)

#### Collections (1)

Postman and Open Collection request collections.

- [InfinitePay Checkout API](https://apis.io/collections/cloudwalk/open-cloudwalk-infinitepay-checkout/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Cloudwalk Infinitepay Checkout Overlay](https://apis.io/overlays/cloudwalk/cloudwalk-infinitepay-checkout-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Cloudwalk Authentication](https://apis.io/security/cloudwalk/cloudwalk-authentication/)
- [Cloudwalk Domain Security](https://apis.io/security/cloudwalk/cloudwalk-domain-security/)
- [Cloudwalk Vulnerability Disclosure](https://apis.io/security/cloudwalk/cloudwalk-vulnerability-disclosure/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Cloudwalk Plans Pricing](https://apis.io/plans/cloudwalk/cloudwalk-plans-pricing/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.cloudwalk.io/)
- [Documentation](https://www.infinitepay.io/checkout-documentacao)
- [Getting started](https://www.infinitepay.io/checkout)
- [API reference](https://www.infinitepay.io/checkout-documentacao)
- [Pricing](https://www.infinitepay.io/taxas)
- [Sign up](https://app.infinitepay.io)
- [Support](https://ajuda.infinitepay.io/pt-BR/)
- [Blog](https://www.infinitepay.io/blog)
- [Security](https://www.infinitepay.io/security)
- [Compliance](https://www.infinitepay.io/legal/politica-de-seguranca-cibernetica)
- [Terms of service](https://www.infinitepay.io/legal/termos-de-uso)
- [Privacy policy](https://www.infinitepay.io/legal/aviso-de-privacidade)
- [GitHub](https://github.com/cloudwalk)
- [Status](https://status.infinitepay.io/)

## API Evangelist rating

**Kin Score 55.7** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 74.1 |
| Contract quality | 57.2 |
| Contract governance | 4.5 |
| Operational transparency | 36.8 |
| Developer ergonomics | 66.1 |
| Access clarity | 71.1 |

**Agent readiness 30.4** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | verified |
| Rate Limit Signal | — |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | na |

**Regulatory alignment 32.1** — Payments

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/cloudwalk/](https://apis.io/providers/cloudwalk/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for CloudWalk: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/cloudwalk/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
