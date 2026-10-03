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

## 2026-09-30 — Global skill wired to the repo, not just copied

Follow-up to the relocation above: `~/.claude/skills/squarespace-site/` (the global,
always-discovered copy) is no longer an independent copy that could silently drift from this
repo. It's now:

- `assets/`, `references/`, `private/` — real Windows directory **junctions** into
  `<repo>/.claude/skills/squarespace-site/`. A `git pull` in the repo clone
  (`C:\Users\beggi\source\meltglassart.com\`) is immediately visible at the global location
  too — same files on disk, no separate sync step.
- `SKILL.md` — **not** linked; it's a plain copy. Windows blocked a true file symlink
  ("Administrator privilege required" — junctions only work for directories, and this account
  doesn't have Developer Mode enabled). This one file will drift from the repo's copy if
  either side is edited without the other being updated to match. Fix options, either: enable
  Developer Mode (Settings → For developers) so a real symlink can replace the copy, or keep
  manually re-copying `SKILL.md` after edits on either side.
- The pre-relocation original at `~/.claude/skills/squarespace-site/` couldn't be fully
  deleted — Windows reports the directory itself "busy" (this session has had it pinned as
  its active working directory the entire time). All of its *contents* were removed first, so
  what's left is an empty, harmless directory entry; full removal needs a session restart to
  release the lock. A complete backup of the pre-relocation content was copied to
  `~/.claude/skills/backup/squarespace-site/` before any of this, independent of that lock
  issue.

## 2026-10-01 — SKILL.md gap closed

Developer Mode enabled (user action, Windows Settings → Update & Security → For developers),
then a sign-out/sign-in to refresh the shell's security token — Windows doesn't grant the
symlink privilege to already-running processes just because the setting changed. After that,
`SKILL.md` was successfully relinked as a real symlink, same as the other three items. The
global skill location (`~/.claude/skills/squarespace-site/`) is now **fully** link-based —
`SKILL.md`, `assets/`, `references/`, `private/` all point back into this repo's clone with
no plain copies left anywhere. The drift risk noted in the previous entry no longer applies.

## 2026-10-02 — Security review added to the skill; README made the living workflow doc

- `SKILL.md` — added a new **Phase 5 — Security review**, required before publishing anything
  that touches Code Injection, forms, or third-party embeds, and re-run whenever those change
  (not just once). Covers: verified script sources, no secrets in client-visible code, no
  unverified `eval`/`document.write` in copied snippets, form submission-destination checks,
  official embed code only, `rel="noopener noreferrer"` on external links, and tracking/cookie
  consent matching. The former Phase 5 (Pre-launch check) is renumbered **Phase 6**, with a new
  first checklist item requiring the Phase 5 review to be complete.
- `README.md` — the three-bullet "Workflow" section is replaced with a full numbered procedure
  covering editing/committing the skill content, applying a change live (Phase 4), the new
  security review (Phase 5), the pre-launch check (Phase 6), and CHANGELOG logging. Adds an
  explicit standing rule: this section must be updated in the same commit as any change to the
  skill's phases or the commit/review process — it's documented as a living doc, not a
  one-time write.

## 2026-10-02 — Write-access test: custom.css applied live

Requested test that Claude Code can actually write to the Squarespace platform (not just
prepare content specs). Applied the already-finalized `assets/custom.css` into the live
prototype's Custom CSS panel (Website → Pages → Custom Code → Custom CSS, found at
`/config/pages/custom-css` — not under "Website → Styles" as SKILL.md's "Website Tools"
wording suggested; SKILL.md should be corrected to match the actual 7.1 location next time
it's touched).

- Typing the CSS via the browser-automation `type` action triggered CodeMirror's
  auto-close-brackets feature, duplicating a closing `}` for each of the 4 opening braces in
  the file (4 stray `}` appended at the end, breaking the stylesheet). Caught via the editor's
  own "Syntax error on line 49" indicator before saving; fixed by selecting from the intended
  end of file to the document end and deleting the duplicates. **Note for future automated
  edits to this (or any CodeMirror-based) Squarespace code panel: verify line count / check
  for a trailing syntax-error indicator before saving, don't assume typed content landed
  verbatim.**
- After the fix, saved successfully (editor returned to non-dirty state, no error shown).
- **Verified live**, not just saved: queried `getComputedStyle` on the actual rendered Home
  page DOM inside the admin preview iframe — all 5 brand color tokens and the mobile
  section-spacing token are present with the exact values written
  (`--brand-primary:#3e7ab5`, `--brand-secondary:#e76d18`, `--brand-accent:#f37920`,
  `--brand-bg:#faf3ec`, `--brand-text:#823038`, `--space-section-mobile:3rem`).
- **One rule isn't visually effective**: `.sqs-block-button-element { border-radius: 0; }` is
  present in the saved CSS but a higher-specificity or later-loading native Squarespace rule
  still renders buttons at `border-radius: 300px` (pill-shaped). This is the exact risk the
  file's own "FRAGILE ZONE" comment warns about for selectors like this — not a write failure,
  but square-cornered buttons are **not yet actually achieved** and need a more specific
  selector (or a native Squarespace button-shape setting) to actually take effect.

**Net result: write access to Squarespace confirmed working.** `custom.css` is applied live
for its 5 color tokens and the mobile spacing rule; the button-radius rule needs a follow-up
fix to actually render square corners.

## 2026-10-02 — Button border-radius fixed; root cause documented

Followed up on the prior entry's open finding (button radius saved but not visually
effective). Investigated properly before guessing at a fix:

- Tried to inspect which native Squarespace rule was winning via `document.styleSheets` /
  `cssRules` from the page — every real theme stylesheet is served from
  `assets.squarespace.com` / `sqspcdn.com`, cross-origin from the site's own domain, so
  `cssRules` throws (`Cannot access rules`) on all of them. There's no way to read the actual
  competing selector or specificity from the page — confirmed by testing, this isn't
  speculation.
- Fix: added `!important` to the button border-radius rule, and widened the selector list to
  cover the actual classes observed on real buttons (`.sqs-block-button-element--small/medium
  /large`, `.sqs-button-element--primary/secondary/tertiary`) rather than the single base
  class alone.
- Re-typed the full `custom.css` into the live Custom CSS panel (same CodeMirror
  auto-close-brackets issue recurred — 4 stray trailing `}` for the file's 4 opening braces,
  same fix as before: delete from intended end-of-file to actual document end, verify, then
  save).
- **Verified live**: `getComputedStyle` on the actual button element in the rendered DOM now
  reports `border-radius: 0px` (previously `300px`). Fix confirmed working, not just saved.

**Findings captured as durable platform knowledge, not just here:**
- `references/platform-capabilities.md` — new note under "Fragility warning": Custom CSS
  rules meant to override a native element style usually need `!important`, because the
  compiled theme CSS is cross-origin and unreadable from the page; a saved, syntax-valid rule
  can have zero visual effect with no error shown, so the live *computed* style must be
  checked, not just "saved without error." Also corrected the Custom CSS panel's actual
  location (`Website → Pages → Custom Code → Custom CSS`, not "Website Tools" as previously
  written — verified live, not assumed).
- `SKILL.md` Phase 3 — same two corrections (actual panel location; `!important` guidance and
  the "verify computed style after saving" rule) added to the skill's own instructions, so
  this isn't knowledge that only lives in a changelog entry.

## 2026-10-03 — Shop catalog migration started; Nightlights prototype live

Began the shop catalog migration (the largest remaining content chunk in the project) and
built a working end-to-end prototype, per the user's request to "start the shop catalog
migration and create the new shop page from the skill and template as a prototype."

- **Authoritative category data**: visited all 8 category pages on the live Square site
  individually (not inferred from product names) to get exact per-category product lists.
  Found Dichroic Glass Trees has 0 products currently. Found 2 products
  ("A Little Bird Told Me So", "Open Spaces Serving Platter") have no category on Square at
  all — assigned to Plates and Platters for the new catalog, flagged as a judgment call.
- **`references/shop-inventory.md` created**: complete working source-of-truth for all 29
  products — name, verified category, price, and a rewritten description in Melt's brand
  voice (first-person as Brooke, per SKILL.md) for every item. Old Square descriptions were
  sampled (2 products) rather than captured verbatim for all 29 — confirmed generic
  AI-marketing boilerplate, being replaced not ported, so capturing all 29 was judged
  low-value versus spending the effort on real rewrites.
- **Squarespace Shop structure rebuilt**:
  - Found 36 duplicate placeholder demo products in the admin (6 names × 6 copies each) —
    more than the "6" assumed in the original migration plan, same duplication pattern as
    the page stubs found earlier in the project. Confirmed with the user before bulk-deleting
    all 36.
  - Created all 7 active product categories in Squarespace (Nightlights, Serving Pieces,
    Plates and Platters, Wine Bottles Reimagined, 4x4s for Everywhere, Sandia Bowls, Sterling
    Silver & Dichroic Glass Earrings) — ready to receive the remaining 24 products.
- **Nightlights category built as the full prototype** (5 of 29 products): saved real
  product photos from the Square site via browser screenshot-capture (the only available
  method — Square has no bulk export; ~199×199px, below the 2500px hero-image spec but fine
  for shop thumbnails), uploaded each via Squarespace's file-upload flow, wrote real prices
  and the rewritten descriptions, assigned the Nightlights category.
- **Verified live**, not just saved: read the actual rendered `/shop` page — all 7 categories
  appear as real filters, the 5 Nightlights products show with correct names/prices, and the
  36 placeholder products are gone from both admin and storefront.

**Scope note**: 24 of 29 products remain — fully specified (name, category, price,
description) in `shop-inventory.md`, but no photos saved and nothing built in Squarespace yet
for those. Categories are already in place for all of them.

## 2026-10-03 — "Unnamed product" with no price noted, excluded from catalog

Per the client's report: Square's inventory has an entry showing as "Unnamed product" with no
price set. Not visible anywhere in the public `/s/shop` storefront grid — confirmed by
re-checking the full "All Items" view, still exactly the 29 named, priced products already in
`shop-inventory.md`. This is presumably a draft/incomplete listing only visible in Square's
admin, which this project has no access to (browsing has only ever been as a public visitor,
per the migration's content-source decision).

**Decision**: documented here as a build-log note only. Not added to `shop-inventory.md` or
the 29-product migration count — an unnamed, unpriced entry isn't a real catalog item to
migrate. If it turns out to represent a real product the client wants carried over, she'd need
to give it a name and price in Square (or just describe it) for it to be added properly.

## 2026-10-03 — Catalog hand-off: Brooke manages products directly in Squarespace

The client asked for a way for Brooke to add, remove, or hide shop products herself, without
needing a developer or a Claude Code session for routine catalog changes.

**Finding**: Squarespace's native product admin already covers all three needs — no custom
tooling needed. Confirmed directly by using the same admin screens this migration has been
using all along:
- **Add**: `Products & Services → Products → Add Product`, same flow already used to build
  the 5 live Nightlights products.
- **Remove**: select a product (or products) on the list → **Delete** — permanent.
- **Hide/show**: not part of the creation-time Save dropdown (that only appears when creating
  a new product) — it's a persistent **Visibility** combobox (Public / Hidden / Scheduled)
  inside each existing product's **Organization** tab. This is the real mechanism; worth
  calling out since it's not where a first guess would look.

**Delivered**: `SHOP-MANAGEMENT-GUIDE.md` (repo root) — a screenshot-illustrated, plain-
language guide for Brooke covering all three actions, with 4 screenshots saved to
`.claude/skills/squarespace-site/assets/guide/`.

**Decision — `shop-inventory.md` frozen as a migration baseline**: now that Brooke owns the
live catalog directly in Squarespace, `shop-inventory.md` stops being kept in sync with it.
It documents the initial 29-product migration (5 verified live, 24 specified but not yet
built) as a point-in-time record. Squarespace's own admin is the live source of truth for the
catalog going forward — this project does not try to resync the two. The remaining 24-product
build-out is unaffected and can still be resumed as a project task if asked; only Brooke's
independent day-to-day edits fall outside this file's scope now.

## 2026-10-03 — Home, About, Contact, Barn & Banter built with real content

Replaced Squarespace's default placeholder copy (Lorem ipsum, generic "next-generation art
hub" AI-marketing text, stock photos of unrelated people) on all four remaining pages. Per
the user's direction, content was pulled from the live old site (`www.meltglassart.com`,
still on Square) rather than invented, with the skill's existing section layouts kept as-is.

**Real content found on the old site and reused:**
- Home hero tagline: "Fused glass is the way I communicate my soul. Thank you for visiting."
  (old site's actual homepage copy).
- About page: Brooke's full artist statement, verbatim from `/artistbio` on the old site
  (first-person, her own words) — covers her process, influences, and that she lives and
  works in Edgewood, New Mexico.
- Real Facebook page: `facebook.com/Melt-A-glass-art-studio-192573367419544` — the only
  social link that exists; no Instagram/Twitter found anywhere, so those placeholder links
  were removed rather than left pointing nowhere.
- A real photo of Brooke at the torch, captured from the old site's artist-bio hero banner
  (screenshot crop, not a full-res source — flagged below) — saved to
  `assets/brooke-studio-hero-clean.jpg` and `assets/brooke-studio-portrait.jpg`, reused
  across Home, About, and Barn & Banter in place of Squarespace's stock photography.

**No real source existed for, so deliberately left honest rather than fabricated:**
- **Phone, street address, business hours** — the old site never published any of these
  (just a contact form). Squarespace's default Contact/footer templates assume a phone
  number and "Mon–Fri 10am–6pm" style hours; both were replaced with "No walk-in hours —
  reach out through the contact form" and the one confirmed fact (Edgewood, New Mexico)
  rather than inventing a schedule or number.
- **Barn & Banter specifics** — the old site has no workshop content at all (it's a new
  offering). Built as a single honest hero section only: what it is in one sentence, no
  invented pricing, schedule, or "how it works" steps, with a note that details are still
  coming together. The blueprint's fuller draft (3-step "how it works" grid, photo gallery)
  was **not** built — there's nothing true to put in it yet. Needs real input from Brooke
  before expanding.
- **About page's inquiry form** ("Connect and Create with Us," retitled "Have a Question?")
  — left in place and re-copied honestly rather than removed; the blueprint flagged this as
  an open question (does an inquiry form belong on About, or Contact only?) still worth
  settling with the client.

**Known rough edges, flagged rather than silently shipped:**
- The reused photo of Brooke is a browser screenshot crop of a small banner image on the old
  site (~199–611px source), not a full-resolution original — visibly soft/low-res up close.
  Real source photos from Brooke would look much better; same caveat already on record for
  the Nightlights product photos.
- Barn & Banter's hero section heading lost its large Heading-1 styling during a text edit
  and renders smaller than the other pages' hero titles — cosmetic, not re-fixed due to an
  editor quirk where re-selecting the block kept landing on the whole section instead of the
  text. Worth a quick pass in the Squarespace editor directly.
- None of these four pages have been re-verified against the live rendered site the way the
  shop products were — each was checked via the editor's own preview after saving, not a
  separate pass.
