# FIRE Suite — Design Rationale

The visual identity of the FIRE app suite, and the reasoning behind every
choice. Decided 2026-08-11 after research into icon geometry, Apple's 2026
production requirements, and how famous app suites (Office, Adobe, iWork,
Omni — and Google Workspace's famous failure) achieve family harmony.
Design principles are codified in the reusable `app-icon-design` skill.

## The story the icons tell

The suite is a set of tools for the FIRE journey — **F**inancial
**I**ndependence, **R**etire **E**arly. The proven sequence: iron out your
personal finances and understand your goal; use everyday discipline tools;
house-hack real estate to cut expenses and grow income; and let that anchor
multiply into a small business. Four apps, four letters, four stages of one
fire.

## Letter assignment — each app owns one letter of F·I·R·E

| Letter | App | Why this letter |
|---|---|---|
| **F** | FIRE Finance | The flagship letter for the flagship subject. Personal finance is where the journey starts — F is the ember that lights the rest. |
| **I** | FIRE Mileage | m**I**leage. Deliberately NOT "Investment": naming an app Investment would box the suite into investment products and cancel the everyday-tools line (like mileage tracking) that actually carries people to FIRE. The capital I is also the strongest visual letter for the job — a straight vertical stroke that reads as a road. |
| **R** | FIRE Realty | **R**eal estate — the most literal fit, and the house-hacking stage of the journey. |
| **E** | FIRE Biz | **E**xpenses — what the app tracks. "Biz" names the audience; E names the job. The business stage burns hottest. |

## Display names

`FIRE Finance · FIRE Mileage · FIRE Realty · FIRE Biz` — the family prefix on
every home screen, every name ≤ 12 characters so iOS never truncates.
("FIRE Business" is 13 characters and truncates; "Biz" reads friendlier.)
App Store listing names may append a descriptive suffix (docs/TODO.md).

## Color system — the flame ramp

Each app owns one hue of a single flame, ordered by rising temperature
F → I → R → E:

| App | Light bg | Dark-variant glyph | Stage |
|---|---|---|---|
| FIRE Finance | `#9E1B2E` deep ember | `#E8404F` | the ember — where the fire starts |
| FIRE Mileage | `#D2401E` flame orange | `#F2632E` | catching — everyday tools |
| FIRE Realty | `#EE7F0E` bright amber | `#F79F1E` | burning — house-hacking |
| FIRE Biz | `#E8A00B` hot gold | `#F6C232` | hottest — the business stage |

**Why a ramp and not four contrasting hues** (the Office/iWork pattern, which
pure findability research favors): the ramp makes the brand BE the palette —
four icons in a home-screen row literally spell the word and form the flame,
something no famous suite can do. It stays safe because the two identity
channels cover each other's blind spots: where color is weakest (I vs R,
neighboring hues) the letterforms are maximally distinct (bar vs bowl+leg);
where letters are weakest (F vs E, near-identical skeletons) color is
maximally distinct (opposite ends of the ramp). Every icon pair has at least
one strong channel — the "redundant coding" rule whose violation sank Google
Workspace 2020 (peer-reviewed studies measure ~12× slower icon-finding when
neighbors share color AND style).

**Temperature direction, honestly:** this is the *cultural* fire scale —
red glow → hot gold, the fire everyone recognizes. Real combustion continues
to white- and blue-hot; we considered a blue E (physically true, and blue is
the business color) and rejected it because a blue tile reads as
water/tech, breaking the flame at a glance. Chosen deliberately: warmth
rises F → E the way the journey compounds. The ramp is also monotonic in
brightness, so the four stay ordered even in iOS's grayscale tinted mode.

## Icon style — Solid Signal (light) + Ember Tile (dark)

Two finalist directions both won, because Apple's appearance-variant system
IS the pair:

- **Light/default — "Solid Signal":** white letter on solid flame hue.
  Everything constant except hue (the iWork/Office harmony formula):
  same geometric letterforms, same cap height, same baseline, same white.
- **Dark — "Ember Tile":** the same letter in its flame hue on a transparent
  background; iOS composites the system dark gradient behind it — the
  colored-letter-on-black look of the suite's original TestFlight icons,
  shipped the canonical way.
- **Tinted/mono:** opaque grayscale masters (white glyph on black), as the
  spec requires; letterforms carry identity when hue vanishes.

A "function cut" direction (FedEx-style negative-space meaning per letter)
was explored and rejected in favor of clean letters.

## Letterform construction

Geometric slab letters built on the suite grid, per the app-icon-design
skill's numbers:

- Cap height 580px on the 1024 canvas (≈57%, in the 55–62% monogram band);
  baseline zone y 207–787 with a ~15px visual-center lift.
- Vertical stems 124px; horizontals 112px (horizontals read heavier than
  verticals — cut thinner for equal apparent weight).
- Per-letter optical balance: F shifted +8px right (open lower-right); I gets
  I-beam caps for equal optical mass with its siblings; R's bowl overshoots
  its siblings' right edge by 10px (curves must overshoot to look equal).
- All four letters share one baseline and margin system so the home-row
  reads as typesetting: **F I R E**.
- Full-bleed square masters — the system applies the mask (never pre-round).

## Assets (masters live here; app repos receive copies)

```
brand/svg/<app>-{light,dark,tinted}.svg     flattened vector masters
brand/svg/<app>-glyph.svg                   letter-only layer (transparent) for Icon Composer
brand/png/<app>-{light,dark,tinted}-1024.png  1024px exports
brand/web/favicon.svg                       suite mark: 2×2 flame quadrants, clockwise F→I→R→E
brand/web/apple-touch-icon.png              180px full-bleed suite mark
brand/web/og-image.png                      1200×630 social-share card
```

Light and tinted PNGs are alpha-free (App Store requirement); dark PNGs keep
required transparency. `<app>` ∈ finance, mileage, realty, biz.

**Icon Composer recipe** (when building each app's `.icon`): background =
native solid fill in the app's light hue; foreground = `<app>-glyph.svg`
(white); Dark mode = glyph recolored to the dark-variant hue on no
background; Mono derives tinted/clear automatically. Everything else
(all rendered sizes, clear variants, App Store icon) is generated by the
system — do not hand-author it.

## Website implications

- The flame ramp is the site's palette; the F·I·R·E row is the hero image.
- The journey story above is the narrative spine for the landing page.
- Blue-hot flame may appear in website storytelling only (the "what burns
  next" moment), never on icons.
