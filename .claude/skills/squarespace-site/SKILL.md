---
name: squarespace-site
description: Build, redesign, or launch a website on Squarespace — client intake, sitemap, per-page section blueprints, section-by-section copy, custom CSS and code injection, and driving the Squarespace editor in the browser. Use when the user mentions Squarespace or asks to build/redesign/audit/launch a site on it. Squarespace has no page-content API, so this skill works through the editor UI and code injection, not REST calls.
---

# Squarespace site builder

This skill instance is dedicated to **Melt Glass Art Studio** — Brooke's fused-glass studio,
selling handmade serving pieces, wine-bottle art, nightlights, and sterling silver/dichroic
glass jewelry directly to collectors, plus (planned) "Barn & Banter" creative workshops. The
site is migrating from Square Online to Squarespace under the same domain,
`www.meltglassart.com`. **Single conversion goal: get a visitor into the Shop and buying a
piece** (see `references/site-blueprint.md` Section 2).

## Ground truth about the platform

Read this before promising anything. It is the constraint that shapes every workflow below.

- **There is no API for creating or editing pages, sections, or content.** The public
  Developer Platform is Commerce (orders, products, inventory, transactions), Domains,
  Profiles/Contacts, Discounts, Scripts, Webhooks, and Reseller provisioning. Nothing
  writes page content. Never plan a build around a "pages endpoint" — it does not exist.
- **Developer Mode (Git-based custom templates, JSON-T/LESS) is 7.0 only** and is not
  available for new sites. Assume any site built today is **7.1**.
- **7.1 customization happens through:** the editor UI, Custom CSS, Code Injection
  (header/footer/per-page), Code Blocks, and the Fluid Engine drag layout.
- Therefore this skill produces **(a) prepared content a human or browser agent pastes in**
  and **(b) code to inject** — not a programmatic site build.

Details and the current API list: `references/platform-capabilities.md`.

## Phase 0 — Establish the situation

Do not start writing copy before these are answered. Ask the user; do not assume.

1. New site, or changes to an existing one? If existing, get the URL.
2. **7.0 or 7.1?** Ask the user directly, or check `Design` in the site's admin — a
   `Template` panel with Developer Mode means 7.0. Verify rather than guess; the answer
   changes what customization is available.
3. Plan tier — Commerce features, code injection, and CSS availability differ by plan.
   Code Injection requires a paid plan.
4. Who executes the changes: the user clicking, or a browser agent (see Phase 4)?
5. Is there existing brand material — logo, fonts, palette, copy deck?

## Phase 1 — Blueprint before building

- reference site: www.meltglassart.com

Fill in `references/site-blueprint.md` with the user. It is the single source of truth
for the build: goal, audience, sitemap, per-page sections, and the conversion path.

Get the sitemap approved before writing a word of copy. Reworking a sitemap after copy
exists wastes the copy.

## Phase 2 — Content, page by page

For each page in the approved sitemap, produce a section-by-section spec:

```
## <Page name>  (/url-slug)
Purpose:        <the one job this page does>
Section 1 — <Hero>
  Layout:       <full-bleed image, left-aligned text>
  Headline:     <exact text>
  Body:         <exact text>
  CTA:          <button label> -> <destination>
  Image:        <what it shows; 2500px wide, <500KB, JPG>
Section 2 — ...
SEO title:      <under 60 chars>
SEO description:<under 160 chars>
```

Rules that keep this usable in the editor:

- Write **final text**, not descriptions of text. The person pasting should never write.
- One idea per section. Squarespace sections are the unit of layout.
- Name every image's subject and give dimensions — do not say "hero image here".
- Slugs lowercase-hyphenated, no dates, stable (changing them later breaks links).

**Brand voice**: artistic, colorful, natural (per `references/site-blueprint.md` Section 4).
Plain, conversational, no jargon. Person: first-person as Brooke on personal pages (About,
product descriptions) — third-person ("Melt", "the studio") on structural pages (nav, footer,
policies). Avoid generic AI-marketing clichés ("elevate your space", "discover the perfect
blend of elegance and artistry") — the current live Square catalog copy already leans this
way and is being rewritten, not reused, for exactly this reason (see the shop-migration plan).
<!-- Assumption, not yet confirmed with the client: person and reading level above are a
     first draft inferred from the blueprint's three voice adjectives. Flag for confirmation. -->

## Phase 3 — Design system and code

Define tokens once, then apply them everywhere:

<!-- FILL: replace with the real brand values. -->
## - Palette: primary / secondary / accent / background / text, each as hex, checked for
##  4.5:1 contrast on body text.
- Palette:  
    - Logo:
            Orange: #F37920
            Blue: #3786C6
    - Content:
            #3E7AB5
            #D9F1FF
            #D1D5DE
            #FAF3EC
            #FFFFFF
            #DBD56E
            #E76D18
            #823038
    - Color pairings:
            #3E7AB5, #D1D5DE
            #3E7AB5, #DBD56E
            #D9F1FF, #DBD56E
            #3E7AB5, #823038
            #FAF3EC, #E76D18
            #FFFFFF, #E76D18
            #FFFFFF, #823038
            

## - Fonts: heading family, body family, base size, scale.
- Fonts: 
    - H1 heading: helvetica world
    - H2 subheading: inclusive sans light all caps
    - H3 notes: generic g10-fr slim
    - P1 body: inclusive sans semibold
    - buttons: intro rust all caps
- Spacing: section padding top/bottom at desktop and mobile.

- Textures: assets/textures.jpg

- Logo: assets/logo.jpg

Put reusable CSS in `assets/custom.css` and paste it into
`Website → Pages → Custom Code → Custom CSS` (verified live on 7.1, 2026-10-02 — not
"Website Tools", which doesn't have a Custom CSS panel on this version). Keep injection
minimal and commented — every rule is something a future editor cannot see in the UI and
will be confused by.

Before writing custom CSS, check whether a native Squarespace setting already does it.
Native settings survive Squarespace updates; CSS selectors targeting generated class
names do not.

A rule meant to override a native element style (buttons, nav, built-in sections) usually
needs `!important` to actually take effect — Squarespace's compiled theme CSS loads from a
cross-origin CDN, so there's no reliable way to inspect its specificity from the page to beat
it without `!important`. A saved, syntax-valid Custom CSS rule can have **zero visual
effect** and give no error — always verify the live *computed* style after saving, don't
trust that "saved without error" means "applied." See `references/platform-capabilities.md`.

## Phase 4 — Executing in the editor

If a browser agent is doing the work, invoke the `claude-in-chrome` skill and drive the
Squarespace admin directly. The user must be logged in already — do not ask for
credentials, and do not attempt to log in on their behalf.

Sequence that avoids rework:
1. Site styles (fonts, colors, spacing) — global, so do it first.
2. Page and navigation structure — create every page as a stub.
3. Sections per page, top to bottom.
4. Custom CSS.
5. SEO titles/descriptions.
6. Mobile pass — Fluid Engine keeps separate mobile layouts; desktop edits do not
   fully propagate. Check every page at mobile width.

Confirm with the user before anything outward-facing or hard to undo: publishing,
connecting a domain, changing DNS, deleting pages, or altering checkout/payment settings.
Run the Phase 5 security review before any of those, not after.

## Phase 5 — Security review

Run this before the Phase 6 pre-launch check — and again any time Code Injection, a form, or
a third-party embed changes, not just once at the end. Most of a Squarespace site's security
surface isn't code we write; it's code we're pasting in on the client's behalf, so review it
like it's someone else's pull request.

- **Code Injection (header/footer/per-page)** — read every line before pasting it in. This
  runs with full page privileges in every visitor's browser: a mistake here isn't a bug, it's
  a vulnerability live on the site.
  - Source every script to a named, trusted vendor (analytics, booking widget, etc.). Never
    paste an unverified snippet found in a template, scraped from another site, or suggested
    by an AI tool without reading what it actually does.
  - Never put API keys, tokens, or other secrets in Code Injection — it's visible to anyone
    who views page source. A third-party integration that needs a secret belongs in that
    vendor's own dashboard/server side, not in Squarespace.
  - Treat inline `eval`, `document.write`, or dynamically-constructed `<script>` tags in a
    copied snippet as a red flag worth stopping on, not pasting past.
- **Forms** — confirm each form's actual submission destination (not just what the UI implies)
  is an address the client controls, and that it isn't collecting more than it needs (payment
  or ID-number fields belong in Squarespace Commerce's own checkout, never a generic form).
- **Third-party embeds / iframes** — use only the vendor's own official embed code, never a
  copy found elsewhere, and confirm the embedded origin matches that vendor's real domain.
- **External links** — `target="_blank"` links need `rel="noopener noreferrer"`; don't link to
  an unverified or look-alike domain.
- **Copied content generally** — anything pulled from the old Square site, a competitor site,
  or a template is untrusted input. Page copy and images are low-risk; embedded `<script>` or
  `<iframe>` tags from an unverified source are not — read before pasting.
- **Cookie/tracking consent** — if a tracker or ad pixel goes in via Code Injection, confirm it
  matches whatever the site's privacy policy (if any) actually discloses.

Flag anything uncertain to the user rather than guessing — this phase exists specifically
because Code Injection is the one place in Squarespace where a mistake has real security
consequences, not just a design one.

## Phase 6 — Pre-launch check

- [ ] Phase 5 security review completed and any findings resolved
- [ ] Every nav link resolves; no orphan pages
- [ ] Every CTA points somewhere correct
- [ ] Mobile layout checked per page
- [ ] SEO title + description on every page
- [ ] Forms submit and deliver to the right address
- [ ] Favicon, social share image, 404 page
- [ ] Images compressed
- [ ] Domain connected and SSL active
- [ ] Analytics installed
<!-- FILL: add commerce checks (tax, shipping, payment) if this is a store. -->

## Reference files

- `references/platform-capabilities.md` — what the platform does and does not allow
- `references/site-blueprint.md` — intake + sitemap template to fill in
- `assets/custom.css` — starter CSS with the token block
- `private/credentials.md` — login credentials (see security note below)

**Security note on `private/credentials.md`**: a plaintext credentials file sitting in a
skill folder is a real risk if this folder is ever committed to git, zipped up, or shared —
`references/site-blueprint.md` Section 1 already references a live GitHub repo
(`github.com/beggio/meltglassart.com.git`) for this project. This folder isn't a git repo
today, so nothing has leaked yet, but the file should move to a password manager (or at
minimum get a `.gitignore` entry) before this folder goes anywhere near source control.
Flagged for the user to action — not read or moved by this skill.
