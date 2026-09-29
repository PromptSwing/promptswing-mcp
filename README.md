# PromptSwing

> Publish a site your AI built to live hosting, then keep editing it: an MCP server for landing a store, reading it back, changing a page, and restoring any earlier version.

PromptSwing hosts storefronts that AI assistants build. Connect over MCP, land the files your assistant generated, and the store is live on its own address. From then on you can read it back, change one page without touching the rest, and restore any earlier version in a call — plus its catalogue, its orders, its reviews and its record, from the same conversation. Cart recovery, reviews and order signals run wherever the site calls the documented signal endpoints — assess_site reports which of those calls are missing before you land. Hosting is a paid subscription.

## What it does

- Land a site your assistant built onto live hosting (land_site).
- Read the live site back, so an edit changes what is there rather than replacing it (read_site).
- Add, change or delete ONE page without touching the rest (add_page, update_page, delete_page).
- Publish as a patch that cannot delete what it was not shown, or as a full replace that names every file it would drop.
- Restore any earlier version in one call — every publish is kept (revert_site).
- Read and write the catalogue (get_product, add_product, update_product).
- Read what sold, what customers said, and what changed and when (get_orders, get_reviews, get_record).
- Read the store's own insights (on a plan that includes them), whether it is live, and its front-page sections (get_insights, check_status, get_sections).
- Check before you land: which documented signal calls are missing, which contrast pairs fail, whether prices are hardcoded (assess_site).
- Score any website free for how AI search engines and AI agents read it, then buy the full audit ($0.01), ready-to-paste fixes ($0.02) or a re-measure ($0.01) per call over x402, with no account (GET https://api.promptswing.com/api/found).

## What it requires — read this before you depend on it

- Hosting requires an active PromptSwing subscription. A connector is a surface, never a way to get a store without buying one.
- A landed page emits signals only where its own call sites exist. PromptSwing injects the library; whether the page calls it is the author's choice, and assess_site reports which calls are absent.
- FOUND BY AI's paid calls run on the Base Sepolia test network until the live rail is configured; no payment has yet settled on chain. The free score works now.
- This server does not reach Captain, PromptSwing's own AI. Captain builds a store and changes it when its owner asks, on a Captain plan, from the Captain app.

## Connect

PromptSwing runs a **remote** MCP server. There is nothing to install and nothing
to run locally. A merchant authorizes it from their own PromptSwing account, in a
browser, and the app is authorized — never a model.

**Claude** (desktop and claude.ai) — add a custom connector with this URL:

    https://api.promptswing.com/api/connector

**VS Code with GitHub Copilot** — add it as an HTTP MCP server in `settings.json`:

```json
{
  "mcp": {
    "servers": {
      "promptswing": {
        "type": "http",
        "url": "https://api.promptswing.com/api/connector"
      }
    }
  }
}
```

In a workspace `mcp.json` the same entry goes in without the outer `"mcp"` key.

VS Code releases before 1.101 do not read a client metadata document and cannot
sign in; updating VS Code fixes it.

**Cursor desktop** — Cursor publishes no client document of its own, so name the
one PromptSwing hosts for it in `mcp.json`:

```json
{
  "mcpServers": {
    "promptswing": {
      "url": "https://api.promptswing.com/api/connector",
      "auth": { "CLIENT_ID": "https://app.promptswing.com/oauth/clients/cursor.json" }
    }
  }
}
```

**Any other client** takes the plain server entry:

```json
{
  "mcpServers": {
    "promptswing": {
      "url": "https://api.promptswing.com/api/connector"
    }
  }
}
```

Each app above was observed connecting and calling tools. **Cursor's cloud agents
and its browser drop the client id and cannot sign in**, and no app outside this
list has been observed connecting.

Authorization is OAuth 2.1 with PKCE, discovered through RFC 9728 protected-resource
metadata at:

    https://api.promptswing.com/.well-known/oauth-protected-resource/api/connector

Protocol revisions supported: 2025-06-18, 2025-03-26, 2024-11-05.

## Before you connect anything — a free check

If you have just built a site and want to know what happens when it goes live,
you can ask without an account, an authorization or a payment:

```bash
curl -X POST https://api.promptswing.com/api/assess \
  -H 'content-type: application/json' \
  -d '{"files":[{"path":"index.html","content":"<html>…</html>"}]}'
```

It reports which of the documented signal calls are absent, whether the checkout
has policy links, whether contrast pairs fall below the floor, and whether prices
are written into the page rather than read from a catalogue.

**Nothing is fetched, nothing is published, and nothing you send is kept.** It is
not an opinion on whether the site is good — a check that could not run is
reported as not-run rather than as a pass, and no model composes the verdict.

## Two ways a site arrives

A worked example of each is in [`examples/`](./examples):

- **[Land it over the connector](./examples/land-over-mcp.md)** — your assistant
  holds the files and publishes them directly.
- **[Import it over GitHub](./examples/import-over-github.md)** — connect a
  repository and every push goes live.

## The public endpoints

Three surfaces need no client, no account and no authorization. The full
contract is at
[`/.well-known/openapi.json`](https://api.promptswing.com/.well-known/openapi.json).

| endpoint | what it does |
|---|---|
| `POST /api/assess` | Check a site before publishing it anywhere. Keeps nothing. |
| `GET /api/shelf?q=` | Search products across hosted stores. |
| `POST /api/buy/quote` | Price an order from one of them. Reserves nothing. **It cannot yet be paid for through this path** — buy on the store's own checkout. |

## Links

- Publishing a site your AI built, answered: https://www.promptswing.com/publish-from-your-ai
- Machine-readable summary: https://www.promptswing.com/llms.txt
- Hosting: https://www.promptswing.com/hosting
- Pricing: https://app.promptswing.com/pricing

---

Run by Bergen Ridge LLC. Subscriptions are billed by Paddle as merchant of record.
Storefront sales settle to each merchant's own connected Stripe account —
PromptSwing is never merchant of record for a merchant's sales and takes no
commission on them.
