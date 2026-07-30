---
name: linsy-buy-modular-sofa
description: Search the LINSY HOME catalog, build a cart, and drive a buyer-approved checkout through
  Linsy's Universal Commerce Protocol MCP endpoint.
generated: '2026-07-19'
method: generated
source: https://www.linsyhome.com/llms.txt
api: linsy:linsy-home-ucp
endpoint: https://www.linsyhome.com/api/ucp/mcp
operations:
- search_catalog
- create_cart
- create_checkout
- update_checkout
- complete_checkout
---

# Buy from LINSY HOME as an agent

LINSY HOME sells modular sofas, sectionals, reclining couches and modular storage cabinets. The store
exposes a Universal Commerce Protocol (UCP) shopping service over MCP, so an agent can go from intent to
a buyer-approved purchase without scraping the storefront.

Every tool name below is taken verbatim from the store's published `/llms.txt`. Do not invent tools —
call `tools/list` on the MCP endpoint to confirm the live schema before you rely on any argument shape.

## Before you start

- **Discovery first.** `GET https://www.linsyhome.com/.well-known/ucp` and read `ucp.version` plus
  `ucp.capabilities`. The store currently declares `2026-04-08` (latest stable) and `2026-01-23`.
- **Agent profile is required.** The MCP endpoint rejects calls that carry no UCP agent profile URI with
  JSON-RPC error `-32001` / `invalid_profile_url`. Establish your profile before calling tools.
- **Buyer context.** Pass `context.address_country` and `context.currency` so pricing, availability and
  shipping are accurate.

## Steps

1. **Discover** — `GET /.well-known/ucp` to confirm the protocol version and that
   `dev.ucp.shopping.checkout`, `dev.ucp.shopping.cart` and `dev.ucp.shopping.fulfillment` are present.
2. **Search** — call `search_catalog` with the buyer's intent (for example a modular sectional with
   storage, in a given size or fabric). Confirm the match with the buyer before spending money.
3. **Cart** — call `create_cart` with the chosen items. Modules are cross-compatible within a
   collection, so confirm the configuration (seats, chaise side, storage modules) with the buyer rather
   than assuming a layout.
4. **Checkout** — call `create_checkout` to start the purchase flow.
5. **Fulfill** — call `update_checkout` to set the shipping address and shipping method. The store's UCP
   fulfillment capability declares `allows_multi_destination.shipping: false`, so a single checkout ships
   to one destination; split the order if the buyer needs two addresses.
6. **Complete** — call `complete_checkout`. **The buyer must approve payment.** Never complete a payment
   on a buyer's behalf without contemporaneous, explicit consent.

## Rules and error handling

- **Payment approval is an invariant.** If you cannot get buyer approval at the moment of payment, do
  not complete the checkout — route the purchase through Shop Pay via `https://shop.app/SKILL.md`
  instead.
- **Rate limits.** The MCP endpoint is rate limited per IP. Back off on `429`.
- **Errors are JSON-RPC 2.0 objects**, not RFC 9457 problem documents. Read `error.code`,
  `error.message` and `error.data.code`; `invalid_profile_url` means your agent profile is missing or
  unfetchable, not that the store is down.
- **No idempotency keys.** Linsy publishes no idempotency header, so a blind retry of
  `create_checkout` or `complete_checkout` is not safe. Re-read state before retrying.

## Read-only alternative

If the buyer only wants to browse, skip MCP entirely — these need no authentication:
`GET /collections/all`, `GET /products/{handle}.json`,
`GET /collections/{handle}/products.json`, `GET /search?q={query}&type=product`.

## Related

- Conventions: `conventions/linsy-conventions.yml`
- Authentication and scopes: `authentication/linsy-authentication.yml`, `scopes/linsy-scopes.yml`
- MCP profile: `mcp/linsy-mcp.yml`
