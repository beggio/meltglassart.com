# Squarespace platform capabilities

Verified against squarespace.com developer docs and help center, September 2026.
Re-verify before relying on any line here — Squarespace changes this surface.

## APIs that exist

From the Developer Platform and the "Developer Tools APIs" help article:

| API | Writes what |
|---|---|
| Orders, Products, Inventory, Transactions (Commerce) | store data |
| Discounts | promo codes |
| Contacts / Profiles | customer records |
| Domains Search, Domains Management | domains |
| Acuity | scheduling |
| Scripts, UI Component Registrations | extension surfaces |
| Webhook Subscriptions, Incoming Webhooks | event delivery |
| Reseller | site + domain provisioning (partner-gated) |

## What has no API

**Page and content creation/editing.** There is no documented endpoint that creates a
page, adds a section, or sets body content. Third-party blog posts and AI summaries
sometimes claim a "Pages endpoint" or "Sites endpoint" — that claim does not appear in
Squarespace's own documentation and should be treated as false until seen there.

Consequence: building a site means the editor UI, by a human or a browser agent.

## Version differences

- **7.0** — multiple template families, each with its own options. Supports Developer
  Mode: Git access to a JSON-T/LESS template. Legacy; not offered for new sites.
- **7.1** — one unified codebase, all templates share features. **No Developer Mode.**
  Customization is site styles, Custom CSS, Code Injection, Code Blocks, Fluid Engine.

Assume 7.1 unless the site is old and the user confirms otherwise.

## Customization surfaces on 7.1

- **Site styles** — fonts, colors, spacing, button shapes. Prefer these; they survive updates.
- **Custom CSS** (`Website → Website Tools → Custom CSS`) — sitewide. Paid plans.
- **Code Injection** — header, footer, and per-page. Paid plans. Use for analytics,
  meta tags, third-party embeds.
- **Code Blocks** — HTML/markdown inside a single section.
- **Fluid Engine** — drag-and-drop grid, with **separate desktop and mobile layouts**.

## Fragility warning

CSS that targets Squarespace's generated class names breaks when Squarespace ships
changes. Prefer, in order: native setting → semantic/stable selector → generated class
name as a last resort, commented with what it was for so it can be repaired.
