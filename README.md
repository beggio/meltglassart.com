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

## Workflow: how a change actually reaches the live site

1. Edit the relevant spec file in this repo (`site-blueprint.md` for content/sitemap changes,
   `assets/custom.css` for design tokens, etc.) and commit it.
2. Apply it live: run the `squarespace-site` skill's Phase 4 (a Claude Code session drives the
   Squarespace admin directly via the `claude-in-chrome` browser-automation skill) to make the
   actual change in Squarespace's editor.
3. Record it in `CHANGELOG.md` — since there's no API to diff the live site against this repo,
   the changelog is the only record of what's been drafted here versus what's actually live.
   Don't skip this step; drift between the two is otherwise invisible until someone notices.

## What's deliberately excluded

`.claude/skills/squarespace-site/private/` holds Squarespace login credentials and is
git-ignored in its entirety (see the `.gitignore` inside that directory) — never committed.
