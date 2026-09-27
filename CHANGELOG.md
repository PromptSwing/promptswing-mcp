# Changelog

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
