# Site blueprint — <!-- FILL: client/site name -->

Fill this in with the user before building. Approve the sitemap before writing copy.

## 1. Situation
- Existing site URL: www.meltglassart.com
- New site URL: lute-bagpipe-ehkr.squarespace.com
- Squarespace version (7.0 / 7.1), verified how: 7.1, new site
- Plan tier: core plan
- Who clicks: browser agent
- Deadline: 11/30/26
- repo: https://github.com/beggio/meltglassart.com.git
- assets/textures.jpg is a reference only and must be excluded as content everywhere on the site.
- assets/images/brooke-studio-hero-clean.jpg (too tightly zoomed/cropped to use as a section
  image) was removed from the repo 2026-10-15 and must never be re-added or used on the site.
- "Events (data source)" is a deliberately unlinked Events-collection page (Not Linked group)
  with zero events, kept only so the Calendar page's Calendar block has a genuinely empty
  source to point to. Do not add real events to it, delete it, or link it in nav — if it needs
  real events someday, that's a separate decision, not an incidental edit.

## 2. Goal
- The **one** action a visitor should take: view products
- How success is measured: views to sales conversion
- What happens today that shouldn't: short visits

## 3. Audience
- Who they are: fused glass collectors
- What they already believe: that they have all the glass
- What objection must be answered before they act: will it break? is it food safe?

## 4. Brand
- Logo file: assets/logo.jpg
## - Palette: primary `#` / secondary `#` / accent `#` / bg `#` / text `#`
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

## - Fonts: heading / body
- Fonts:
    - H1 heading: helvetica world
    - H2 subheading: inclusive sans light all caps
    - H3 notes: generic g10-fr slim
    - P1 body: inclusive sans semibold
    - buttons: intro rust all caps

- Voice in three adjectives: artistic, colorful, natural
- Words to never use:
- Reference sites they like, and *what specifically* they like about each:

## 5. Sitemap

Mark each page's job. Keep top-level nav to 5-7 items.

Verified against the live prototype (lute-bagpipe-ehkr.squarespace.com, password
"MeltyCheese") on 2026-10-15 — Calendar and Map are now built (see Section 6) and the client
set the final Main Navigation order directly in the Squarespace editor. Current actual order:

Note: the Main Navigation "Map" entry is a **Link item** pointing to `/map`, not a direct page
pick — a duplicate blank page got created under the same name during this build, got linked in
nav by mistake, and was deleted; relinking the real page directly wasn't possible (page
drag-reorder between the Main Navigation and Not Linked groups didn't respond to automation),
so a Link item routing to `/map` was used instead. Functionally identical for visitors.

```
/                    Home           — navigation to other pages, short summary of Melt, several images of work
/about               About          — bio of artist, history of work and practice
/calendar            Calendar       — honest "coming soon" page; no fake events, links to Contact
/barn-banter         Barn & Banter  — client based creative workshops
/shop                Shop           — listing of all products available for sale
/map                 Map            — studio location (Hazel Green, AL) + invitation for collectors to share theirs
/contact             Contact        — contact information for artist, links to social network pages
```

Not in nav: <!-- FILL: legal, thank-you, 404 -->. The prototype's "Not Linked" group only
holds duplicate unused template stub pages (Home/About/Contact/Shop repeated ~16x) — these
are Squarespace onboarding leftovers, not intentional pages; flag for cleanup/deletion before
launch (confirm with the user first, since deleting pages is a destructive action).

## 6. Per-page sections

Repeat per page. Sections are the build unit.

Below is the ACTUAL section structure already built on the prototype (checked 2026-09-30),
not an aspirational draft. Every page is still running Squarespace's default AI-generated
placeholder copy (Lorem ipsum, generic "art hub"/"next-generation" boilerplate, demo
products, a fake address and social links) — none of it is Melt- or Brooke-specific yet.
Phase 2 copywriting replaces the placeholder text in place of these section shapes; don't
invent new section shapes unless a page's purpose genuinely needs one.

```
## Home  (/)
Purpose: navigation to other pages, short summary of Melt, several images of work
Section 1 — Hero: image-left / text-right + full-bleed title / "MELT: A GLASS ART STUDIO" / placeholder subhead ("The fusion of glass, heat, and passion") / — / image of work in studio 
Section 2 — About the artist: split, dark bg / "About the artist" / placeholder bio teaser ("Born at the crossroads of curiosity and code...") / "More About Brooke" → /about / photo of artist with work
Section 3 — Shop Fine Art: 4-up product grid / "Shop Fine Art" / — / "Shop All" → /shop / 4 placeholder products ($25 each)
Section 4 — Barn & Banter teaser: 3-up card grid / "Barn & Banter" / 3 placeholder blurbs / "Get Started" → /barn-banter / placeholder cards
SEO title (<60):
SEO description (<160):

## Shop  (/shop)
Purpose: listing of all products available for sale
Section 1 — Hero: banner / "Discover Next-Generation Art Services" (placeholder — needs a Melt-specific headline) / — / — / —
Section 2 — Product grid: 6-up / — / — / — / 6 demo products (Iridescent Oil Paint, Soft Pastels, Palette Knife, Linen Canvas Roll, Sculpting Clay, Copper Etching Plate — replace with real Melt glass pieces + prices)
Section 3 — FAQ: accordion / "Frequently Asked Questions" / 6 generic placeholder questions (what services/pricing/how to start/etc.) / — / —
Section 4 — Social CTA: banner / "Join the Movement: Follow Us for the Latest in Art Innovation" (placeholder) / — / — / —
SEO title (<60):
SEO description (<160):

## Barn & Banter  (/barn-banter)
Purpose: client based creative workshops
Section 1 — Hero: split / "Barn & Banter" / "Hands-on creative workshops with Brooke, hosted
right in the studio. Details and dates are still coming together — reach out if you'd like to
hear when they're set." / "Get In Touch" → /contact / studio work-in-progress photo
SEO title (<60):
SEO description (<160):

## Calendar  (/calendar)
Purpose: honest placeholder until real workshop/event dates exist — no fabricated events
Single section, in order: "Calendar" heading, centered / native Squarespace Calendar block
(always shows the current month with prev/next navigation), positioned immediately under the
heading and centered horizontally / "Get in Touch" → /contact / body copy ("Workshop and
event dates are still coming together. Want to be the first to know when something's on the
calendar? Get in touch below."). Note: body copy currently sits *below* the button rather
than above it (blueprint originally called for heading → calendar → body copy → button) — a
block-drag limitation in the editor during the 2026-10-16 layout fix meant the body-copy
block could only be landed below the button, not between the calendar and it. Functionally
complete; revisit if the editor's drag behavior improves.
Calendar block connected to an empty, unlinked Events collection ("Events (data
source)" — see Section 1 note) rather than left unconnected, since an unconnected Calendar
block falls back to showing Squarespace's own fake demo events on the live site, not a blank
state. Never connect this block to Shop/products — it would show real products as "events."
This connection can silently reset during heavy layout editing — re-verify it (Content →
Events: Stacked) after any extended drag/undo troubleshooting on this page.
SEO title (<60): Calendar | Melt Glass Art Studio
SEO description (<160): Workshop dates are still coming together. Reach out to be the first to know when something's on the calendar.

## Map  (/map)
Purpose: studio location now; grows into a collector map over time as real locations come in
Single section, one layout, no sub-sections — in order: "Find Us" heading / native Squarespace
Map block, geocoded to "Hazel Green, AL" (city-level only — no street address exists publicly,
consistent with the "no walk-in hours" footer note), zoom set to 0.01x (world view) per client
request, placed immediately under the heading / body copy ("Melt is based in Hazel Green,
Alabama. We're building a map of where our pieces — and the people who collect them — call
home. If you've got a piece of Melt glass, let us know where it landed.") / "Share Your Spot"
→ /contact. The map must stay directly under the heading, above the body copy, on both
desktop and mobile (Fluid Engine keeps these as separate layouts — check both after any edit).
SEO title (<60): Find Us | Melt Glass Art Studio
SEO description (<160): Melt is based in Hazel Green, Alabama. See where our glass pieces and collectors call home.

## About  (/about)
Purpose: bio of artist, history of work and practice
Section 1 — Hero: split / "Art in Motion: Shaping Tomorrow's Creativity" (placeholder — needs Brooke/Melt-specific headline) / "Pioneering the Future of Art" placeholder body / "Learn More" / —
Section 2 — Connect and Create with Us: form / — / inquiry form (First/Last Name, Email, Phone, Project Details) / "Submit" / — <!-- FILL: confirm with Brooke whether an inquiry form belongs on About, or should move to Contact only -->
Section 3 - Experience my work in action - links to working videos contained in assets directory
SEO title (<60):
SEO description (<160):

## Contact  (/contact)
Purpose: contact information for artist, links to social network pages
Section 1 — Hero + form: — / "Start Your Creative Journey Today" (placeholder) / contact form (Name, Email, newsletter opt-in, Subject, Message) / "Submit Inquiry" / —
Section 2 — Details: — / "Hours" + "Phone" blocks / placeholder Mon–Fri 10am–6pm, (555) 555-5555 <!-- FILL: real hours/phone --> / — / —
Section 3 — Social: — / "Follow Melt On Social" / — / — / —
SEO title (<60):
SEO description (<160):

## Footer (all pages)
Find Us: placeholder address "123 Example Road, New York, NY 12345" <!-- FILL: real address or "by appointment" -->
Hours: placeholder Mon–Fri 10am–6pm
Follow: placeholder Facebook/Instagram/Twitter links <!-- FILL: real social URLs -->
```

## 7. Functionality
- [ ] Contact form → delivers to:
- [ ] Newsletter → provider:
- [ ] Commerce → products, tax, shipping:
- [ ] Scheduling (Acuity):
- [ ] Members area:
- [ ] Blog:
- [ ] Third-party embeds:

## 8. Assets still needed
| Asset | Who provides | Spec | Status |
|---|---|---|---|
| Hero image | client | 2500px wide, <500KB | missing |

## 9. Decisions log
Record choices the user made so they are not relitigated.
| Date | Decision | Why |
|---|---|---|
