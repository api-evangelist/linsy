# Linsy

Linsy (LINSY HOME) is a direct-to-consumer modular furniture brand founded in 2007, selling True Modular sofas, sectionals, reclining couches, modular storage cabinets, replacement covers and accessories from U.S. warehouse fulfillment.

Linsy has no developer program, but both of its storefronts — [www.linsyhome.com](https://www.linsyhome.com/) and [linsy.com](https://linsy.com/) — publish a real machine-readable agent surface:

- **`llms.txt` / `agents.md`** — agent instructions, read-only browsing endpoints, and the buyer-approval rules.
- **UCP merchant profile** at `/.well-known/ucp` — Universal Commerce Protocol `2026-04-08` (and `2026-01-23`), with cart, checkout, discount, fulfillment, order and catalog capabilities.
- **MCP endpoint** at `/api/ucp/mcp` — JSON-RPC transport for `search_catalog`, `create_cart`, `create_checkout`, `update_checkout`, `complete_checkout`.
- **OpenID Connect discovery** at `/.well-known/openid-configuration` — Shopify customer accounts, authorization code + PKCE (S256).

Artifacts in this repo: `well-known/`, `llms/`, `mcp/`, `authentication/`, `scopes/`, `conformance/`, `conventions/`, `lifecycle/`, `security/`, `skills/`.

Backed by: hongshan
