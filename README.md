# meltglassart.com

Source-of-truth content for Melt Glass Art Studio's website, currently being rebuilt on
Squarespace (migrating off Square Online) under this same domain, `www.meltglassart.com`.

## What's actually in this repo

**There is no literal website code here.** Squarespace has no code export and no API for
page content — the live site exists only inside Squarespace's hosted editor. What this repo
holds instead is the *content that drives that build*:

- `.claude/skills/squarespace-site/` — a Claude Code project skill, dedicated to this site.
  It contains the workflow (`SKILL.md`), the brand/content blueprint
  (`references/site-blueprint.md`), platform constraints
  (`references/platform-capabilities.md`), and brand assets (`assets/`) — logo, texture
  moodboard, and the CSS custom-property tokens used for Squarespace Custom CSS.

Cloning this repo into a Claude Code project and running `claude` from its root auto-discovers
`squarespace-site` as a project skill — no separate setup needed.

## Workflow: maintaining the skill and shipping a change to the live site

This section documents the full process end to end — editing and committing the skill/content
specs, applying a change in Squarespace, reviewing it, and logging it. **Keep this section
current.** Whenever the skill's phases change (renumbered, a step added or removed) or the
commit/review process itself changes, update this section in the *same commit* as that change.
A workflow doc that's drifted from reality is worse than none — don't let this become one.

### 1. Edit and commit the skill/content specs
Everything under `.claude/skills/squarespace-site/` (except `private/`, see below) is plain
version-controlled content: `SKILL.md` (the workflow itself), `references/site-blueprint.md`
(goal, audience, sitemap, per-page section copy), `references/platform-capabilities.md`
(platform constraints), and `assets/` (brand images, `custom.css` tokens). Edit the relevant
file directly in this repo, commit with a message describing the *content* change (not just
"update blueprint"), and push. Nothing here is live yet — this is the source, not the site.

### 2. Apply the change live in Squarespace
Run the `squarespace-site` skill's **Phase 4** (a Claude Code session drives the Squarespace
admin directly via the `claude-in-chrome` browser-automation skill) to make the actual change
in Squarespace's editor, following its build order: site styles → page/nav structure →
sections per page → Custom CSS → SEO titles/descriptions → mobile pass. Confirm with the user
before anything outward-facing or hard to undo (publishing, domain/DNS, deleting pages,
checkout settings).

### 3. Security review (Phase 5) — required before publishing
Run the skill's **Phase 5** whenever a change touches Code Injection, a form, or a third-party
embed — not just once at project end. Squarespace's Code Injection runs with full page
privileges in every visitor's browser, so a pasted-in script, embed, or form is reviewed like
someone else's pull request: verified source, no secrets in client-visible code, no
unverified `eval`/`document.write`, forms checked for their real submission destination,
`rel="noopener noreferrer"` on external `target="_blank"` links. See `SKILL.md` Phase 5 for
the full checklist.

### 4. Pre-launch check (Phase 6)
Before a full launch or a significant batch of changes, run the skill's **Phase 6** checklist
(nav links, CTAs, mobile layout, SEO, forms, favicon/social image/404, image compression,
domain+SSL, analytics) — its first item is confirming the Phase 5 security review is done.

### 5. Log it in `CHANGELOG.md`
Record what changed: what's now true in this repo (drafted) versus what's actually been built
live in Squarespace (applied). There's no Squarespace API to diff the repo against the live
site, so this changelog is the *only* record of that distinction — don't skip it, drift
between drafted and live is otherwise invisible until someone notices the hard way.

## What's deliberately excluded

`.claude/skills/squarespace-site/private/` holds Squarespace login credentials and is
git-ignored in its entirety (see the `.gitignore` inside that directory) — never committed.
