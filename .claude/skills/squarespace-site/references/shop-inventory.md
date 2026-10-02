# Shop inventory — Square "Shop Now" → Squarespace "Shop"

**Frozen migration baseline — not a live mirror.** This file documents the initial 29-product
migration from Square (what was ported, its rewritten copy, and its status as of that
migration) as of 2026-10-02. From that point on, Brooke manages the live catalog directly in
Squarespace's own product admin — see `SHOP-MANAGEMENT-GUIDE.md` at the repo root — and this
file does **not** get updated for her day-to-day adds/removals/hides. Squarespace's admin is
the live source of truth for the catalog, not this table. This file only gets revisited if the
remaining migration work below is resumed as a project task.

Working source-of-truth for the shop catalog migration. See `SKILL.md` and
`site-blueprint.md` Section 6 (Shop page) for the broader build context.

**Category data verified live** against `www.meltglassart.com/s/shop` on 2026-10-03 by
visiting each of the 8 category pages individually (not inferred from product names) —
URLs and counts below are exact. **"Current description" is not captured per-product.**
Two products were sampled earlier in this project (Clock Pattern Night Light, Copper
sterling silver dichroic earrings- posts) and both read as generic AI-marketing boilerplate
("Illuminate your nights with our exquisite...", "Discover the perfect blend of elegance and
artistry...") — confirming the pattern flagged when this migration was scoped. Capturing all
29 old descriptions verbatim was judged low-value (they're being replaced, not ported) and
skipped to spend the effort on real rewrites instead. If verbatim old copy is ever needed,
each product page is at `www.meltglassart.com/product/<slug>/<id>`.

**Rewritten descriptions** are below, in Melt's brand voice (artistic, colorful, natural;
first-person as Brooke, per `SKILL.md` Phase 2) — first draft, not yet reviewed with the
client. Grounded in actual technique terms (fused, slumped, dichroic, kiln) where I'm
confident they're accurate; flag anything that reads wrong to an actual glass artist.

**Two products have no category on the live Square site** — "A Little Bird Told Me So" and
"Open Spaces Serving Platter" appear only in the unfiltered "All Items" view, in none of the
8 category pages. Assigned both to Plates and Platters below (closest fit among the 8
categories we're carrying forward) — a judgment call, not a verified fact; confirm with the
client if it matters which category they land in.

**Dichroic Glass Trees category is empty** on the live Square site (0 products) — not
included in the table below; nothing to migrate for it.

## Status legend
- `not started` — nothing done yet
- `photo saved` — product photo(s) saved to `assets/shop/`
- `built` — product created live in Squarespace with photo, price, category, description
- `verified` — built AND confirmed live via the actual rendered page, not just "saved without error"

## Nightlights (5 products) — `/shop/nightlights/10`

Photos saved 2026-10-03 via browser screenshot-capture of the live Square product grid
(zoom + save_to_disk on each thumbnail) — there's no bulk-export or direct-download path
from Square, so this is a screen capture, not the original source file. Resolution is
~199×199px, well under the 2500px-wide spec `SKILL.md` Phase 2 sets for hero images — fine
for a shop thumbnail, but flag to the client that real source photos (if she has them) would
look sharper than a re-screenshotted capture.

All 5 built live in Squarespace and verified 2026-10-03 — confirmed via the actual rendered
`/shop` page (not just "saved without error"): all 7 categories now appear as real category
filters, these 5 products show with correct name/price, and the old 36 duplicate placeholder
demo products are gone from both admin and storefront.

| Product | Price | Rewritten description | Photo | Status |
|---|---|---|---|---|
| Clock Pattern Night Light | $22.00 | I fused this piece around an etched clock motif — the kind of detail that only comes alive once the light's behind it. Plug it into any room that wants a little warmth after dark. | `nightlight-clock.png` | verified |
| Gear Pattern Night Light | $22.00 | Interlocking gears cut into the glass, caught mid-turn. I like how industrial patterns soften once they're lit from behind. | `nightlight-gear.png` | verified |
| El Dia de los Muertos Night Light | $22.00 | A sugar-skull silhouette in black against warm orange glass, made for Día de los Muertos but at home on a shelf year-round. Glows deep amber once it's plugged in. | `nightlight-dia-de-los-muertos.png` | verified |
| Zia Night Light | $22.00 | New Mexico's Zia sun symbol, fused in red on amber glass. This one's close to home — it glows gold wherever you put it. | `nightlight-zia.png` | verified |
| Mandala Night Light | $22.00 | A hand-cut mandala pattern on pale blue glass, more lace than light fixture once it's plugged in. | `nightlight-mandala.png` | verified |

## Serving Pieces (1 product) — `/shop/serving-pieces/9`

| Product | Price | Rewritten description | Photo | Status |
|---|---|---|---|---|
| Pick Up Stick Serving Platter | $125.00 | Dozens of thin glass rods fused at odd angles — it really does look like a game of pick-up sticks frozen mid-toss. One of the more labor-intensive pieces I make, and worth every hour at the table. | `serving-pick-up-stick.jpg` | not started |

## Plates and Platters (6 products) — `/shop/plates-and-platters/3`

| Product | Price | Rewritten description | Photo | Status |
|---|---|---|---|---|
| Ride Around Town Platter | $125.00 | Fused from scrap-glass stringers in a loose grid, this platter has the restless energy of a city map. Every piece runs a slightly different pattern — no two come out quite alike. | `platter-ride-around-town.jpg` | not started |
| Catch a Wave Plate | $45.00 | Deep blues and grays swirled together like water caught mid-motion. Good for serving, better for just leaving out where the light can hit it. | `plate-catch-a-wave.jpg` | not started |
| Circles Platter | $60.00 | Rings of color fused edge to edge — simple geometry, but it never looks the same twice depending on what's sitting on it. | `platter-circles.jpg` | not started |
| On-edge Construction Platter | $95.00 | Strips of glass stood on edge and fused flat, so the pattern runs straight through instead of sitting on the surface. One of my favorite techniques — and one of the more fragile ones to pull off. | `platter-on-edge-construction.jpg` | not started |
| Open Spaces Serving Platter | $125.00 | *(no category on Square — assigned here, see note above)* Marbled glass in warm grays and golds, fused loose and open like weather moving across a field. Big enough to actually serve from, pretty enough that you won't want to put food on it. | `platter-open-spaces.jpg` | not started |
| A Little Bird Told Me So | $50.00 | *(no category on Square — assigned here, see note above)* A bird on a branch, etched into pale blue-green glass — quiet, a little old-fashioned, the kind of piece that looks right propped on a windowsill. | `plate-a-little-bird-told-me-so.jpg` | not started |

## Wine Bottles Reimagined (4 products) — `/shop/wine-bottles-reimagined/5`

| Product | Price | Rewritten description | Photo | Status |
|---|---|---|---|---|
| Wine Bottle Cheese Tray - Green | $16.00 | A real wine bottle, slumped flat in the kiln until it's a tray instead of a bottle. Green glass keeps its curve at the neck — still unmistakably a bottle, just lying down. | `winebottle-tray-green.jpg` | not started |
| Wine Bottle Cheese Tray - Blue | $22.00 | Same idea, cobalt glass — a wine bottle melted flat into a cheese tray, neck and all. Nothing wasted, nothing added. | `winebottle-tray-blue.jpg` | not started |
| Limoncello wine bottle cheese tray | $22.00 | Made from an actual Limoncello bottle, slumped flat with the label's ghost still faintly visible in the glass. A good conversation piece before it's even holding cheese. | `winebottle-tray-limoncello.jpg` | not started |
| Wine Bottle Cheese Tray - Clear | $16.00 | Clear glass, so whatever the bottle held shows through — color, light, whatever's underneath. The simplest version, and sometimes the one people reach for first. | `winebottle-tray-clear.jpg` | not started |

## 4x4s for Everywhere (3 products) — `/shop/4x4s-for-everywhere/6`

| Product | Price | Rewritten description | Photo | Status |
|---|---|---|---|---|
| Candy Apple Red 4x4 | $14.00 | Four inches square, candy-apple red straight through. Small enough to prop anywhere — a shelf, a windowsill, a stack of books that needed some color. | `4x4-candy-apple-red.jpg` | not started |
| Small dish- Black and White | $14.00 | A small dish in bold black and white — good for rings, loose change, anything that needs a place to land. | `4x4-small-dish-black-white.jpg` | not started |
| Small Dish- Blueberry | $14.00 | Deep blueberry blue, small enough to tuck into a bathroom or a nightstand. One of the easiest ways to bring a little color into a room. | `4x4-small-dish-blueberry.jpg` | not started |

## Sandia Bowls (1 product) — `/shop/sandia-bowls/8`

| Product | Price | Rewritten description | Photo | Status |
|---|---|---|---|---|
| Sandia Sunrise bowl | $150.00 | Named for the Sandia Mountains at sunrise — the color runs from deep rose into gold, the way the mountains do most mornings here. The biggest, most involved bowl I make. | `bowl-sandia-sunrise.jpg` | not started |

## Sterling Silver & Dichroic Glass Earrings (9 products) — `/shop/sterling-silver-dichroic-glass-earrings/7`

| Product | Price | Rewritten description | Photo | Status |
|---|---|---|---|---|
| Dichroic cool sterling silver earrings- dangles | $36.00 | Dichroic glass shifts color depending on the light — these read cool blue-green most of the time, something else entirely in direct sun. Sterling silver ear wires. | `earrings-cool-dangles.jpg` | not started |
| Ocean green dichroic sterling silver earrings- posts | $28.00 | Ocean-green dichroic glass on sterling silver posts — small, everyday earrings with a little shimmer built in. | `earrings-ocean-green-posts.jpg` | not started |
| Ocean green dichroic sterling silver earrings- dangles | $36.00 | Same ocean-green dichroic glass as the posts, but on dangles that catch the light with every turn of your head. | `earrings-ocean-green-dangles.jpg` | not started |
| Copper sterling silver dichroic earrings- posts | $28.00 | Dichroic glass with a warm copper shift, set simply on sterling silver posts. | `earrings-copper-posts.jpg` | not started |
| Copper sterling silver dichroic earrings- dangles | $36.00 | The copper dichroic glass on dangles — more movement, more light catching the color shift as they swing. | `earrings-copper-dangles.jpg` | not started |
| Sterling silver and dichroic glass passion purple earrings-posts | $28.00 | A deep, almost electric purple dichroic glass — "passion purple" is the only name that ever fit it. Set on sterling silver posts. | `earrings-passion-purple-posts.jpg` | not started |
| Crinkle blue dichroic sterling silver earrings- dangles | $36.00 | Dichroic glass with a crinkled, textured surface that scatters the light instead of just reflecting it — blue shifting toward teal depending on the angle. | `earrings-crinkle-blue-dangles.jpg` | not started |
| Sterling silver and dichroic glass passion purple earrings- dangles | $36.00 | The passion-purple dichroic glass on dangles, swinging just enough to keep catching new light. | `earrings-passion-purple-dangles.jpg` | not started |
| Sterling silver, dichroic magic blue earrings- dangles | $36.00 | A shifting, almost iridescent blue dichroic glass I've nicknamed "magic blue" — it genuinely looks different depending on where you're standing. | `earrings-magic-blue-dangles.jpg` | not started |

## Totals
- 29 products across 7 active categories (Dichroic Glass Trees empty, not counted)
- **5 of 29 verified live** (Nightlights, complete). **24 of 29 remaining**: Serving Pieces
  (1), Plates and Platters (6), Wine Bottles Reimagined (4), 4x4s for Everywhere (3), Sandia
  Bowls (1), Sterling Silver & Dichroic Glass Earrings (9) — all have rewritten descriptions
  drafted above, none have photos saved or are built in Squarespace yet.
- All 7 Squarespace product categories exist (created during the Nightlights batch), ready
  to receive the remaining products — no category-creation work left, only products.
