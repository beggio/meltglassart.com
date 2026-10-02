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
