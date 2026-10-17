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

## 2026-10-03 — Fixes from client review: location, socials, heading, shop hero image

Client review of the previous entry's build caught several issues; all applied live in the
Squarespace editor and verified via screenshot after each change.

- **Location corrected.** "Edgewood, New Mexico" (the old site's stale location) replaced with
  "Hazel Green, Alabama" everywhere it appeared: the global site footer, the Contact page's
  Location sidebar block, and the About page's bio paragraph.
- **Social links fixed.** Footer Facebook now links to
  `facebook.com/Melt-A-glass-art-studio-192573367419544` (reliably — an earlier attempt
  silently reverted to Squarespace's placeholder URL because the fix didn't press Enter to
  commit the link edit; redone with Enter and reverified). Footer Instagram added, linking to
  `instagram.com/meltstudionm` — this didn't exist before; the prior entry's claim that no
  Instagram existed anywhere was about the old Square site, not a final answer.
- **Barn & Banter heading fixed.** The hero "Barn & Banter" text block had lost its Heading 1
  styling (flagged as a known rough edge in the previous entry) and was rendering as small
  Paragraph 2 body text. Reset to Heading 1; now matches the large hero-title size used on
  other pages.
- **Shop page hero image replaced.** The generic Squarespace stock photo (unrelated person at
  a pottery wheel) swapped for a real photo of Brooke's own work: the "Open Spaces" marbled
  platter (`assets/shop/platter-open-spaces.jpg`).
- **About page texture image removed.** `assets/textures.jpg` — a brand color/texture
  moodboard meant only as a styling reference for palette/texture decisions — had been placed
  as literal page content at the bottom of the About page's "Have a Question?" section in the
  previous build. Removed; the file stays in `assets/` for its intended styling-reference use,
  not as site content.

**Not re-verified in this pass:** the footer's location and social-link fixes were spot-checked
on the Contact, About, and Barn & Banter pages at the time each was made, but not re-confirmed
against every page in this same session due to the Squarespace editor's scroll/navigation
quirks (clicking a nav link while in page-edit mode selects the nav block instead of
navigating, and mouse-wheel scroll is frequently a no-op). Worth a full footer sweep next
session before publishing.

## 2026-10-03 — Second texture-image removal: it was also on the Home page

The previous entry's "About page texture image removed" fix was incomplete — the client
caught a second placement of the same moodboard crop that the first pass missed: the Home
page's main hero section had a swirled pink/orange/yellow image (`orangeglass.png`, a crop of
`assets/textures.jpg`) sitting behind Brooke's portrait photo as a second, separate image
block in the same section — not something that showed up when checking the About page alone.

- Removed the `orangeglass.png` image block from the Home page hero. Brooke's portrait photo
  (a separate, overlapping block in the same section) was confirmed intact immediately after
  — an early attempt to delete the emptied block itself briefly removed the portrait too;
  caught via preview and undone before saving, then redone correctly (content-only removal,
  block left in place and empty).
- Swept all five pages (Home, Shop, Barn & Banter, About, Contact) plus the global footer for
  any other stray use of this texture crop. None found. Footer confirmed showing "Hazel Green,
  Alabama," both Facebook and Instagram links (`instagram.com/meltstudionm/`), and the restored
  logo — all still correct from the previous entry's fixes.
- **Lesson for next time:** a styling-reference asset like `textures.jpg` can get reused as
  literal content in more than one place during a build pass. When removing one instance,
  check all pages that share a section layout or were built in the same pass, not just the
  page the issue was reported on.

## 2026-10-03 — Third texture-image removal: full textures.jpg in the Home page's Barn & Banter preview

A third instance of the same asset, found by the client via a direct CDN link after the
second fix above. This time it was the full, uncropped `textures.jpg` (not a crop like
`orangeglass.png`), placed as a standalone image block in the Home page's "Barn & Banter"
preview section (the teaser block below "Shop Fine Art," next to Brooke's portrait photo) —
below where the previous sweep's manual scroll-through had stopped, which is why it was missed
then.

- Removed the `textures.jpg` image block from that section. It was a standalone block (no
  other content layered on it), so it came out cleanly in one step — unlike the Home hero fix
  above, there was no risk of also deleting Brooke's portrait, which is a separate block.
- Verified via direct fetch of each live page's rendered HTML (`textures.jpg` string search)
  rather than a manual editor scroll-through this time: Home, Shop, Barn & Banter, About, and
  Contact all confirmed clean.
- **Standing rule, now saved to persistent memory (not just this changelog):** `textures.jpg`
  and any crop/derivative of it is a styling-reference asset only — palette and texture cues
  for CSS/design decisions — and must never appear as rendered content on the live site, on
  any page, permanently. Three separate instances turned up across two review passes, so this
  is now checked by direct page-source search (`textures.jpg` string match) rather than relying
  on a manual scroll-through, which has proven to miss instances below the fold.

## 2026-10-15 — Home hero swapped to a studio work photo; new photo library added

Brooke added a batch of real photos (market booth shots, product shots, and one genuine
studio work-in-progress shot) to a new `assets/images/` folder, reorganized `assets/` into
`images/` and `logo/` subfolders, and updated `site-blueprint.md`'s Home page spec: the Hero
should show "image of work in studio" instead of a portrait, and "About the artist" should
show "photo of Brooke" instead of a generic "studio photo."

**Applied live** (`lute-bagpipe-ehkr.squarespace.com`, Home page):
- Hero image replaced with `87480861_...jpg` — a genuine studio work-in-progress shot (glass
  cutter, ruler, a piece being laid out on the bench). The previous Hero image was actually
  Brooke's portrait, mislabeled in spec as generic "studio photo"; moving it out of the Hero
  matches the blueprint's new "image of work in studio" instruction.
- Hero subhead copy replaced: "Fused glass is the way I communicate my soul. Thank you for
  visiting." → "The fusion of glass, heat, and passion" (per the blueprint edit).
- "About the artist" section: no change needed — it already used the real Brooke portrait
  (`brooke-studio-portrait.jpg` in Squarespace's library), which already satisfies the
  blueprint's "photo of Brooke" instruction.
- Verified live via the page editor's published preview (not just Save confirmation).

**Not applied — blocked:**
- About page Section 3, "Experience my work in action - links to working videos contained in
  assets directory" (added to the blueprint this round) — the video files it refers to were
  removed from the repo in the 2026-10-13 size-limit revert (see git history) and no longer
  exist anywhere in `assets/`. Needs real video assets (hosted outside this repo, given
  GitHub's size limits) before this section can be built.

**Data-quality note:** the newly added `assets/images/brooke-studio-portrait.jpg` (added
2026-10-15) is, despite its filename, a photo of a market display table — not a portrait of
Brooke. The actual portrait is `assets/images/brooke-studio-hero-clean.jpg`. Flagged for a
filename fix; not renamed in this pass to avoid touching files mid-review.

## 2026-10-15 — About the artist image replaced; zoomed-in portrait retired

The "About the artist" section's image (`brooke-studio-hero-clean.jpg`) was too tightly
zoomed/cropped to read well as a section image — it was the same close-up used in the Home
hero before the previous entry's swap. Client asked for it to be replaced and removed from
the repo entirely.

**Applied live** (`lute-bagpipe-ehkr.squarespace.com`, Home page):
- "About the artist" section image replaced with `468787199_...jpg` — a market-booth photo
  showing Brooke clearly at the Melt table — the only remaining new photo with a clear,
  unambiguous shot of her face.
- Verified live via the page editor's published preview.

**Repo:**
- `assets/images/brooke-studio-hero-clean.jpg` removed (`git rm`).
- `references/site-blueprint.md` Section 1 updated with a standing exclusion, mirroring the
  `textures.jpg` rule: this file must never be re-added or used on the site.

## 2026-10-15 — Same over-zoomed image was live on three more pages

Client reported the just-removed image was still showing on the Barn & Banter page. A full
sweep (not just a spot-fix — see the `textures.jpg` lesson from 2026-10-03) turned up the same
photo in **four** places total, not one: it had been uploaded to Squarespace's media library
multiple times under reused filenames (`brooke-studio-portrait.jpg` in Squarespace's own
library is not one file — at least two separate uploads share that label), so removing the
repo source file didn't touch any of the copies already placed on live pages.

**Applied live, all on `lute-bagpipe-ehkr.squarespace.com`:**
- Barn & Banter — hero image block replaced with `468840146_...jpg` (glass Zia-symbol tiles
  in progress — fits a hands-on-workshop page).
- About page — **two** separate instances, both missed in the earlier pass:
  - Hero section background (behind "Breathe. Strength. Nature.") replaced with the same
    market-booth photo of Brooke used on Home's About section (`468787199_...jpg`).
  - "In the Studio" image block replaced with the studio work-in-progress bench shot
    (`87480861_...jpg`) — matches that section's own heading.
- Verified clean via full scroll-through of Contact and Shop (no instance found on either).

**Process note:** checked every page by eye this time, not just by filename — Squarespace's
displayed "filename" for an asset is just a label, not a unique identifier, so two visually
different images (or two copies of the same one) can carry the same name in its library.
Filename alone is not reliable evidence that an image is or isn't the retired photo.

## 2026-10-15 — Still on the Home page: the Barn & Banter teaser section was missed

Client reported the photo was *still* live, specifically on "the Barn & Banter section of the
Home page." A server-side fetch check (searching rendered HTML for `hero-clean` across all 5
routes) had come back clean, which was true for the four spots already fixed — but missed a
**fifth** placement: the same image was also the card photo in the Home page's own "Barn &
Banter" teaser section (the 3-up section below "Shop Fine Art"), a page section distinct from
the actual `/barn-banter` page. This exact section was already called out by name in the
2026-10-03 textures.jpg entry above as a previous hiding spot for a retired image — it should
have been checked automatically this time without being told twice.

**Applied live** (`lute-bagpipe-ehkr.squarespace.com`, Home page):
- Barn & Banter teaser section image replaced with `IMG_1504.jpeg` — a new photo of the actual
  barn/studio exterior, added uncommitted to the repo by the client for this purpose.
- Re-verified via the same server-side fetch check used earlier, across all 5 routes: `0`
  matches for `hero-clean` and `0` for `brooke-studio-portrait` this time.

**Repo:** `assets/images/IMG_1504.jpeg` added and committed.

**Lesson:** a page can host the same image in more than one distinct section, and a general
sweep has to check *every section of every page*, not stop at the sections already known to
have held content before (Hero, About). When a project's own history already names a specific
section as a past hiding spot for a stale asset (see the 2026-10-03 entry), check that named
section explicitly on the next sweep rather than re-discovering it by a third report.

## 2026-10-15 — Calendar and Map pages built; sitemap finalized

The two remaining planned-but-unbuilt pages from the original sitemap draft. Scoped with the
client first rather than guessing: Barn & Banter already says workshop dates aren't set yet,
so Calendar needed to stay honest (no invented events), and "customer map corkboard" was too
vague to build without asking what it should actually be.

**Decisions (client-confirmed):**
- Calendar: a simple "coming soon" page in Barn & Banter's own honest tone — no fake dates,
  links to Contact. Revisit once real workshop dates exist.
- Map: a literal interactive map. Starts with just the studio's own pin (Hazel Green, AL,
  city-level only — no street address exists publicly); no customer locations invented. Uses
  Squarespace's native Map block, so no third-party account or API key is needed. Real
  collector pins can be added later as that data comes in.

**Applied live** (`lute-bagpipe-ehkr.squarespace.com`):
- `/calendar` — built: "Calendar" heading, honest body copy, "Get in Touch" → /contact. SEO
  title/description set.
- `/map` — built: "Find Us" intro section with body copy, "Share Your Spot" → /contact, plus a
  native Google Map block geocoded to "Hazel Green, AL" (confirmed via the block's address
  autocomplete — typing into the City/State field alone did not trigger geocoding; the
  Address field's autocomplete selection did). SEO title/description set.
- Main Navigation reordered by the client directly in the Squarespace editor (drag-and-drop
  reordering did not respond to browser-automation input — flagged and left for the client
  rather than fought further). Final live order: Home, About, Calendar, Barn & Banter, Shop,
  Map, Contact.

**Repo:** `references/site-blueprint.md` Sections 5 and 6 updated to match: sitemap order now
reflects the live nav, Barn & Banter's stale "EMPTY" status note removed (it's been built for
a while), and Calendar/Map's "NOT BUILT" placeholders replaced with their actual shipped
content specs.

## 2026-10-15 — Real calendar grid, world-view map, and a duplicate-page recovery

Follow-up to the entry above: client asked for the Calendar page to show an actual empty
calendar of the current month (not just text) with month-to-month navigation, and the Map
page's map to be a zoomed-out world view with Hazel Green, AL as the only pin, matching the
original sitemap intent.

**Calendar — applied live:**
- Added Squarespace's native Calendar block (always shows the current month, with prev/next
  arrows — confirmed this is a platform feature, not something built here).
- The block's default/unconnected state renders Squarespace's own fake demo events live on the
  site (confirmed via both a server-side HTML fetch and the editor's own Preview mode, which
  showed the fake events even though they don't appear in page source — the block is
  client-rendered). Connecting it to the Shop/products collection was considered and rejected:
  that would show real products as fake "events."
- Fix: created a new, deliberately unlinked Events-collection page, "Events (data source)"
  (Not Linked group), deleted its 5 auto-generated demo events, and pointed the Calendar
  block at it. Result: a genuinely empty grid for the current month.

**Map — applied live:**
- Zoomed the native Map block out to 0.01x, which renders a full world view (all continents
  visible) with the Hazel Green, AL pin as the only marker, per the original sitemap
  ("customer map corkboard" → literal interactive map, starting with just the studio pin).

**Incident — duplicate Map page:** mid-session, a second blank page also named "Map" was found
linked in Main Navigation, shadowing the real content page (which still held everything built
2026-10-15 earlier, confirmed intact via direct HTML fetch). Likely created accidentally while
adding the Calendar's data-source page. Fixed by deleting the blank duplicate and adding a
Main Navigation **Link item** pointing to `/map`, since dragging the real page from "Not
Linked" into "Main Navigation" didn't respond to browser-automation input (same limitation as
the earlier nav-reorder issue — see the 2026-10-15 "still on the Home page" entry above).
Functionally identical for visitors; flagged in the blueprint so this isn't mistaken for a bug
later.

**Lesson:** before trusting an "Empty Page" or any other admin-panel state after a long gap
mid-session, verify against the actual published HTML (fetch) rather than the editor's visual
state — it can be stale or, as here, pointing at the wrong page entirely.

## 2026-10-15 — Map layout: moved the map directly under the heading

Client reported the map was visible on desktop (so the earlier "blank space" report was
something else — likely a stale cache/extension on their end, not a build issue) but
positioned wrong: it had landed in its own section below the body copy and button instead of
right under the "Find Us" heading.

**Applied live, both desktop and mobile:**
- Removed the old Map block (which lived in its own section near the bottom of the page).
- Added a new Map block directly into the intro section, in the empty space below the
  heading, and resized/repositioned it so it sits immediately under "Find Us" with no overlap
  — body copy and the "Share Your Spot" button now flow naturally below it.
- Reconfigured it identically to before: geocoded to "Hazel Green, AL", zoom 0.01x (world
  view).
- Deleted the now-empty old section.
- Checked independently in both Desktop View and Mobile View (Fluid Engine keeps these as
  separate layouts) — confirmed correct in both before saving.

## 2026-10-16 — Calendar layout: moved the calendar directly under the heading

Follow-up to the Map layout fix above: client asked for the same treatment on the Calendar
page — the Calendar block should follow directly under the "Calendar" heading and be
centered, matching the Map-page pattern.

**Applied live, both desktop and mobile:**
- Repositioned the Calendar block so it sits immediately under the "Calendar" heading
  (previously there was a large vertical gap) and centered it horizontally (previously
  offset ~46px left of center).
- In the process of earlier troubleshooting this session, the pre-existing body-copy text
  block ("Workshop and event dates are still coming together...") had been deleted and the
  Calendar block's data source had become disconnected from "Events (data source)" (it was
  rendering Squarespace's fake demo events — stock photos and "Porta"/"Pellentesque Risus
  Ridiculus" lorem text — again in the editor canvas). Both were fixed: reconnected the block
  to "Events (data source)", and re-added the body-copy text block with its original copy.
- Could not get the body-copy block to drag-reposition between the calendar and the "Get in
  Touch" button (same block-drag resistance as prior sessions) — landed it below the button
  instead, so the live order is now heading → calendar → button → body copy, not matching the
  blueprint's original heading → calendar → body copy → button order. Functionally complete,
  not a layout bug, but flagged here since it diverges from spec.
- Checked independently in both Desktop View and Mobile View — confirmed no overlap and no
  stray demo-event content in either, and reconfirmed via an authenticated fetch of the live
  `/calendar` HTML that no "Porta"/"Pellentesque" text is present before saving.

**Lesson:** a Calendar block's data-source connection can get silently reset by heavy
drag/undo churn during layout troubleshooting — re-check Content → Events: Stacked source
after any extended fight with a page's layout, not just the thing being visibly moved.

## 2026-10-16 — Footer logo replaced with the real brand mark

Client reported the logo image next to the "Follow" social links in the site footer needed
to be removed and replaced with the actual logo file from the repo.

**Applied live (global site footer, so this affects every page):**
- The footer's image block held an old placeholder logo (`logo.jpg` — "Melt" script text on a
  solid beige square, not the real brand mark).
- Replaced it with `Melt_logo-RGB.png` from
  `.claude/skills/squarespace-site/assets/` (transparent background, brand orange/blue —
  matches `references/site-blueprint.md` Section 4's logo spec) via the block's Content →
  Replace → Upload file flow.
- The image block's display mode was set to "Fill", which cropped the new logo's tagline
  ("a glass art studio") off its right edge since the new image's aspect ratio differs from
  the old square placeholder's. Switched the block to "Fit" so the full logo displays
  uncropped.
- Checked independently in both Desktop View and Mobile View, then confirmed live via an
  authenticated fetch of the Home page HTML (`logo.jpg` absent, `Melt_logo-RGB` present)
  before considering this done.

## 2026-10-17 — About page hero image recropped so Brooke's head isn't cut off

Client reported the top (hero) image on the About page still had Brooke's head cut off, and
asked for it to be replaced and recropped so the crop removes the bottom of the image instead
of the top.

**Applied live:**
- The hero is a full-bleed background-image section (`Fill Screen`), not a Fluid Engine image
  block, so there's no separate crop file — the live frame is a focal-point crop of the
  existing source photo (market-booth photo of Brooke at a show, filename
  `468787199_180528317873111..._81_n.jpg`). The photo itself already contains her full head;
  the section's focal point was just centered too low (on her torso), so the top of the frame
  cropped her head off.
- No need to replace the source file — confirmed via the image's own crop/edit tool that the
  full photo (head included) was already there. Fixed it by dragging the focal-point indicator
  on the background image's thumbnail (Background tab → Image → the small circle on the
  thumbnail) upward to center on her head instead of her torso. Squarespace's "Fill Screen"
  crop now keeps the top of the frame and crops from the bottom (her boots/legs are now out of
  frame) instead of the top.
- Checked independently in both Desktop View and Mobile View — her head, sunglasses, and
  beanie are fully visible with clean margin above in both.

**Lesson:** for a full-bleed background-image section (not a Fluid Engine image block), "crop"
is controlled by the focal-point indicator on the small thumbnail in Background → Image, not
by the destructive "Edit image" → Crop tool (which permanently re-crops the source file). Drag
that focal point toward the subject that must stay in frame rather than reaching for the crop
tool first.
