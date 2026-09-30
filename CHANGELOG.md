# Changelog

Tracks what's true in this repo's content specs versus what's actually been applied live on
the Squarespace site. Squarespace has no API, so there's no automatic way to diff the two —
this file is the only record. Add an entry whenever a spec change is drafted, and update it
once that change has actually been built in the Squarespace editor.

## 2026-09-30 — Repo created, existing work captured

**Drafted (in this repo), not yet applied live:**
- `references/site-blueprint.md` — Situation, Goal, Audience, Brand (palette/fonts) filled in.
  Sitemap drafted (Home, Shop, Barn & Banter, About, Contact, plus planned-but-unbuilt
  Calendar and Map) and verified against the live Squarespace prototype
  (`lute-bagpipe-ehkr.squarespace.com`) — not yet approved as final.
- `references/site-blueprint.md` Section 6 — per-page section specs captured from the
  Squarespace prototype's actual current state; still running Squarespace's default
  placeholder copy (Lorem ipsum, generic template text), not yet rewritten in Melt's voice.
- Shop catalog migration (Square "Shop Now" → Squarespace "Shop") — reviewed the live Square
  catalog (29 products, 8 categories) and confirmed scope (migrate all 29, rewrite
  descriptions in Melt's voice) with the client. **Not started**: no `shop-inventory.md` built
  yet, no product photos saved, no products created in Squarespace.
- `assets/custom.css` — real Melt brand tokens written (palette, contrast-checked body text).
  **Not yet pasted into Squarespace's Custom CSS panel** — exists only in this repo so far.
- `SKILL.md` — dedicated to Melt (opening paragraph, brand-voice section filled in). This is
  workflow documentation, not itself something that gets "applied live."

**Already true on the live Squarespace prototype** (observed, not changed by this repo):
- Site is on Squarespace 7.1, "Core" plan tier.
- Main Navigation already built: Home, Shop, Barn & Banter (empty, no sections), About,
  Contact — matches the drafted sitemap above.
- Shop page still has Squarespace's 6 placeholder demo products (not the real Melt catalog).

**Infrastructure (this entry):**
- Repo access scoped to a dedicated GitHub Deploy Key (not the account owner's personal SSH
  key) — read-write, bound to this repo only.
- `squarespace-site` skill relocated here from `~/.claude/skills/` as a project-scoped skill.
