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
"MeltyCheese") on 2026-09-30 — Home/Shop/Barn & Banter/About/Contact are the actual Main
Navigation and page order already built in Squarespace. Calendar and Map from the earlier
draft do **not** exist on the prototype yet (no such pages, linked or unlinked) — kept here
as planned/not-yet-built pages rather than dropped; still need to be created.

```
/                    Home           — navigation to other pages, short summary of Melt, several images of work
/shop                Shop           — listing of all products available for sale
/barn-banter         Barn & Banter  — client based creative workshops (linked in nav, page is empty — no sections built yet)
/calendar            Calendar       — Barn & Banter events (not yet built on the prototype)
/map                 Map            — customer map corkboard (not yet built on the prototype)
/about               About          — bio of artist, history of work and practice
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
Section 1 — Hero: image-left / text-right + full-bleed title / "MELT: A GLASS ART STUDIO" / placeholder subhead ("Lorem ipsum dolor sit amet...") / — / studio photo of Brooke
Section 2 — About the artist: split, dark bg / "About the artist" / placeholder bio teaser ("Born at the crossroads of curiosity and code...") / "More About Brooke" → /about / studio photo
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
Status: EMPTY on the prototype — linked in nav but zero sections built ("Create a
beautiful page by adding and combining sections."). Needs the full build from scratch;
carrying forward the original draft shape below as the starting point, pending approval:
Section 1 — Hero: split-L / "Barn & Banter" / short workshop pitch / "Book a session" → <!-- FILL: booking destination — Acuity link? Contact? --> / workshop photo
Section 2 — What to expect: grid-3 / "How it works" / 3 short steps / — / 3 icons
Section 3 — Gallery: carousel / — / — / — / past workshop photos
SEO title (<60):
SEO description (<160):

## Calendar  (/calendar)
Purpose: display calendar of events for 12 months
Status: NOT BUILT on the prototype — no /calendar page exists yet, linked or unlinked.
Section 1 — <name>: Hero:
Section 2 — <name>:
SEO title (<60):
SEO description (<160):

## Map  (/map)
Purpose: customer map corkboard
Status: NOT BUILT on the prototype — no /map page exists yet, linked or unlinked.
Section 1 — <name>:  layout / headline / body / CTA / image
Section 2 — <name>:  ...
SEO title (<60):
SEO description (<160):

## About  (/about)
Purpose: bio of artist, history of work and practice
Section 1 — Hero: split / "Art in Motion: Shaping Tomorrow's Creativity" (placeholder — needs Brooke/Melt-specific headline) / "Pioneering the Future of Art" placeholder body / "Learn More" / —
Section 2 — Connect and Create with Us: form / — / inquiry form (First/Last Name, Email, Phone, Project Details) / "Submit" / — <!-- FILL: confirm with Brooke whether an inquiry form belongs on About, or should move to Contact only -->
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
