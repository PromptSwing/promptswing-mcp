# Changelog

## 0.1.5 — 2026-10-04

- A FOUND BY AI pack is also sold to a person in Japan, Switzerland, Singapore and India.

## 0.1.4 — 2026-10-04

- FOUND BY AI: ten full audits with ready-to-paste fixes are $5, a pack held by a key with no account, bought by a
  person by card through Paddle at https://app.promptswing.com/found. The per-call payment over x402 is removed.
  An AI agent cannot buy a pack yet. The free score is unchanged: `GET https://api.promptswing.com/api/found`.
- States where PromptSwing is offered: the United States (with its territories), Canada except Quebec,
  Australia and New Zealand.

## 0.1.2 — 2026-09-27

- FOUND BY AI: score any website free for how AI search and agents read it; the full audit ($0.01), fixes ($0.02)
  and re-measure ($0.01) are bought per call over x402 with no account — on the Base Sepolia test network until
  the live rail is configured. `GET https://api.promptswing.com/api/found`.

## 0.1.1 — 2026-09-27

- Connect section names the apps observed connecting: Claude, VS Code with GitHub Copilot, and Cursor desktop.
- Capabilities name three more reads: the store's own insights, whether it is live, and its front-page
  sections (`get_insights`, `check_status`, `get_sections`).

## 0.1.0 — 2026-09-11

First publishable set. Licensed Apache-2.0 — see LICENSE and NOTICE.

- Remote MCP server: land a site, read it back, change a page, restore a version,
  read and write the catalogue, read orders, reviews and the change record.
- Free public assessment at `POST /api/assess` — no account, keeps nothing.
- Public shelf search and order quote, with an OpenAPI contract. A quote reserves
  nothing and cannot yet be paid for through this path.
