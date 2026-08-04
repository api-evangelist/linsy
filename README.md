# Linsy

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

Linsy (LINSY HOME) is a direct-to-consumer modular furniture brand founded in 2007, selling True Modular sofas, sectionals, reclining couches, modular storage cabinets, replacement covers and accessories from U.S. warehouse fulfillment.

Linsy has no developer program, but both of its storefronts — [www.linsyhome.com](https://www.linsyhome.com/) and [linsy.com](https://linsy.com/) — publish a real machine-readable agent surface:

- **`llms.txt` / `agents.md`** — agent instructions, read-only browsing endpoints, and the buyer-approval rules.
- **UCP merchant profile** at `/.well-known/ucp` — Universal Commerce Protocol `2026-04-08` (and `2026-01-23`), with cart, checkout, discount, fulfillment, order and catalog capabilities.
- **MCP endpoint** at `/api/ucp/mcp` — JSON-RPC transport for `search_catalog`, `create_cart`, `create_checkout`, `update_checkout`, `complete_checkout`.
- **OpenID Connect discovery** at `/.well-known/openid-configuration` — Shopify customer accounts, authorization code + PKCE (S256).

Artifacts in this repo: `well-known/`, `llms/`, `mcp/`, `authentication/`, `scopes/`, `conformance/`, `conventions/`, `lifecycle/`, `security/`, `skills/`.

Backed by: hongshan
