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
- Vertical stems 124px, except the I's stem at 150px (a lone vertical needs
  extra width for equal optical mass — the Adobe equal-mass rule);
  horizontals 112px (horizontals read heavier than verticals — cut thinner
  for equal apparent weight).
- Per-letter optical balance: F shifted +8px right (open lower-right); I gets
  I-beam caps plus the wider stem for equal optical mass; R's bowl reaches
  x=742, overshooting the flat right edges of E (x=732) by 10px and of the
  right-shifted F (x=740) by 2px — curves must overshoot flats to look equal.
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

## In-app color system — Flame

Decided 2026-08-11 (research: HIG icon/tint coordination; Stripe's
shift-the-shade accessibility method; WCAG 2.1 contrast). Shipped in
FIRE Biz 1.13.0 and FIRE Mileage 1.12.0; implementation spec in FIRE-Biz-iOS
`docs/superpowers/specs/2026-08-11-app-color-theme-design.md`.

Every app ships the **Flame** treatment: neutral system chrome with the
app's flame hue as the accent — vivid fills on primary CTAs, toggles, and
selection marks; the text-safe cut on links, nav buttons, and tab
selection. The home-screen icon is untouched by any in-app choice.

**Revision, same day:** the first cut shipped this as a two-theme system —
a neutral "Classic" default plus Flame behind a Settings App Color picker.
On-device inspection showed the two looks read too close (the only visible
difference was the CTA fill), so the setting was removed (Biz #48,
Mileage #63) and Flame is the one look. The Classic/Mono scheme below
remains fully specified as a designed option for future use:

- **Classic/Mono (designed, not shipped)** — a warm ink-and-paper scheme in
  the tone of the Claude app: light paper `#F7F5F1` ground, white cards,
  ink `#211D19`; dark ground `#1E1B18`, cards `#262220`, text `#ECE7E0`;
  primary buttons ink-with-paper-label (inverted in dark); the flame hue
  only where it carries meaning — links, tab selection, toggles, selection
  marks, one key data highlight per screen. Worth revisiting if a future
  app (or a suite restyle) wants the accent scarce; pair it with warm
  custom surfaces (not just system backgrounds) so the difference from
  Flame is unmistakable — that surface work is what the first cut lacked.

Two accent roles per app, both asset-catalog colorsets with Any + Dark:

| App | AccentText (links; ≥4.5:1) | AccentFill (fills; vivid icon hue) |
|---|---|---|
| FIRE Finance | `#9E1B2E` / `#EC4B59` | `#9E1B2E` / `#EC4B59` (same) |
| FIRE Mileage | `#D2401E` / `#F2632E` | same as text |
| FIRE Realty | `#B25F0A` / `#F79F1E` | `#EE7F0E` / `#F79F1E` |
| FIRE Biz | `#9C6B07` / `#F6C232` | `#E8A00B` / `#F6C232` |

`AccentColor` (the app-wide tint) carries the AccentText values, so anything
rendering the accent *as text* passes WCAG; `AccentFill` exists because the
vivid Realty/Biz hues are 2.7:1 / 2.2:1 on white — fill roles only. Finance
and Mileage hues pass as-is, but the two-asset structure is kept in every
app so the siblings stay identical. Classic/Mono neutrals (for future use):
ink `#211D19`, paper `#F7F5F1`, dark ground `#1E1B18`, dark card `#262220`,
dark text `#ECE7E0`.

Standing rules:

1. **Fill labels are white suite-wide** — a deliberate brand call accepted
   below strict WCAG on the gold fills (Apple's own toggle green is 2.2:1);
   button shape and weight carry recognition.
2. **Data/category palettes never use hues adjacent to the app's flame
   accent** (Biz retired amber for sienna). Selection is marked by an
   accent ring + check — shape first — never by recoloring the item.
3. **Semantic colors stay system** (destructive red, success green), and
   pending/attention states in the gold-adjacent apps (Realty, Biz) use a
   neutral badge + SF Symbol, never amber.
4. Print/PDF surfaces use the light-mode AccentText value (Mileage's tax
   report replaced its violet rule with flame orange).

### Settings screens — colour rule and section spine

Decided 2026-08-12 after on-device inspection of FIRE Mileage 1.12.0.
Implementation spec: FIRE-Mileage-iOS
`docs/superpowers/specs/2026-08-12-settings-standard-design.md`.
Shipped in FIRE Mileage 1.13.0 and FIRE Biz 1.14.0.

The trigger: Settings rows rendered in a mix of `.primary` and the flame
accent with no rule behind it. Inside a `List`, SwiftUI tints a `Button`'s
entire label with the accent while leaving a `NavigationLink`'s at
`.primary` — so the colour reported *which SwiftUI type a row used*, which
no user can interpret. `Export Tax Report (PDF)` (dark) sat directly above
`Export Data (CSV)` (orange) in the same section doing the same job.

1. **Row labels are always `.primary`.** Every app, every row. In a Settings
   list the accent appears **only** in the leading SF Symbol — a uniform
   column of flame marks down the left edge.
2. **Settings row icons use `AccentColor`, never `AccentFill`.** A thin
   monochrome symbol behaves like text, and the vivid fill hues fall below
   the WCAG text-contrast gate in Realty and Biz (see the AccentFill table
   above).
3. **Row kind is signalled by a trailing glyph, never by colour:**
   `›` pushes a screen · nothing acts now (sheet, share, compose) ·
   `↗` leaves the app · grey value text is read-only status.
4. **Semantic state colour is still allowed** on a status *value* line
   (green ok / red failed). Colour must mean something.
5. **Fixed section order: Setup · Data · Help · About.** Every app fills
   these four in order, skipping any it doesn't need. Slot 1 may be renamed
   when the app has a single coherent subject (Biz → `Business`); slots 2–4
   keep their names. Ordering is descending by how often that slot is the
   reason someone opened Settings.
6. **About shows the marketing version only**, no build number — but the
   feedback payload must keep the build, since it is the only handle tying a
   TestFlight report to the build that produced it.
7. **Icons stay monochrome symbols, not filled chips.** iOS-Settings-style
   colour chips were considered and rejected: they need a chip palette
   Settings doesn't have. Revisit only if a future app needs one.
8. **`foregroundStyle` on both `Label` slots is necessary but not
   sufficient — the row also needs `.tint(.primary)`.** Observed on iOS
   26.5 (simulator, FIRE Mileage, 2026-08-12): a `Button` inside a `List`
   still tints its whole label with the accent unless the row itself also
   carries `.tint(.primary)`.
   - `.buttonStyle(.plain)` also stops the bleed but was rejected: it strips
     the row's system press-highlight, and it only works where applied — a
     per-call-site fix, the trap the shared primitive exists to avoid.
   - `.tint(.primary)` then suppresses the system's automatic dimming of a
     **disabled** `Button` row, while a disabled `NavigationLink` still
     greys correctly — the shared row type must read
     `@Environment(\.isEnabled)` and de-emphasise both slots itself. A real
     regression, caught only by screenshotting the empty-data state (zero
     vehicles, which is what disables those rows) — missed by review passes
     that only screenshotted the enabled state.
   - None of this is testable from Swift Testing or XCTest — SwiftUI's
     resolved `foregroundStyle`/`tint` isn't inspectable. Device
     screenshots in both appearances, including the disabled state, are
     the only check; re-verify after any Xcode or iOS SDK bump touching
     `List` or `Button`.
   - Reference implementation: `Shared/SettingsRow.swift` in FIRE Mileage
     and FIRE Biz.

A sync **toolbar indicator** (glanceable cloud glyph opening a Sync sheet and
a Diagnostics screen) is designed but deferred to a follow-up spec. Two
findings from its feasibility pass, recorded so they aren't re-derived:
`NSPersistentCloudKitContainer` exposes no public queue depth, so a "pending
changes" count cannot be built honestly; and SwiftData cannot toggle CloudKit
at runtime without rebuilding the `ModelContainer`, so no in-app sync toggle.

## Website implications

- The flame ramp is the site's palette; the F·I·R·E row is the hero image.
- The journey story above is the narrative spine for the landing page.
- Blue-hot flame may appear in website storytelling only (the "what burns
  next" moment), never on icons.
