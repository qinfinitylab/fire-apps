# FIRE Suite — Design Rationale

> Working document. The icon system is being designed (2026-08-11); decisions
> land here as they are made, with the reasoning that made them.

## Decided

### Letter assignment — each app owns one letter of F·I·R·E

| Letter | App | Why this letter |
|---|---|---|
| **F** | FIRE Finance | The flagship letter for the flagship subject: **F**inance. Personal finance is the center of the FIRE journey; it gets the word the acronym starts with. |
| **I** | FIRE Mileage | m**I**leage — and the capital *I* is the strongest *visual* letter for this app: a straight vertical stroke reads naturally as a road / lane marker, a visual pun the icon design can exploit. |
| **R** | FIRE Realty | **R**eal estate / **R**ealty — the most literal fit in the set. |
| **E** | FIRE Biz | **E**xpenses — what the app actually tracks. "Biz" names the audience; *E* names the job. |

### Display names

`FIRE Finance · FIRE Mileage · FIRE Realty · FIRE Biz` — the family prefix on
every home screen, every name ≤ 12 characters so iOS never truncates it.
("FIRE Business" is 13 characters and truncates; "Biz" also reads friendlier.)
App Store listing names may append a descriptive suffix (tracked in docs/TODO.md).

## In progress

- **Color system** — shortlisted: flame-spectrum ramp (each app one hue of a
  fire gradient) vs one brand color with letter-only variation. Decision
  pending design research.
- **Icon geometry/style** — direction to be chosen from mocked alternatives
  after research.

## Assets

Production icon masters will live in this folder as `icon-<app>-1024.png`
(+ source SVGs). App repos receive copies; this folder is the master.
