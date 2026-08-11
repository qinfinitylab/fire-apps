# fire-apps — FIRE suite website + brand

Customer-facing repo for the FIRE app suite (FIRE Finance · FIRE Mileage ·
FIRE Realty · FIRE Biz): the marketing/story website (GitHub Pages, not built
yet) and the suite's brand assets. **This repo is PUBLIC** — never commit
secrets, API keys, TestFlight redemption codes meant to be limited, or
personal data.

## Source of truth

- **[docs/mission.md](docs/mission.md)** — what the site is and v1 acceptance.
- **[brand/DESIGN-RATIONALE.md](brand/DESIGN-RATIONALE.md)** — the icon/brand
  system and the *why* behind every choice. The site and the app repos both
  follow it; change the rationale doc in the same PR as any brand change.
- **[docs/TODO.md](docs/TODO.md)** — deferred work.

## Non-negotiables

1. Public repo: no secrets, ever.
2. Brand changes update `brand/DESIGN-RATIONALE.md` in the same change —
   assets and rationale must not drift.
3. Icon masters live here (`brand/`); app repos receive **copies**. Edit the
   master here first.
4. Site (when built) is static, GitHub Pages-hosted; keep it dependency-light.

## Git workflow

- Branch per feature, PR into `main`, squash merge, never push `main` directly.
- Review PRs with the local `codex` CLI before merging (qinfinitylab repo — no
  auto Codex review).
- Conventional Commits.

## Skill routing

- Icon/brand design work → `/app-icon-design` (once created), `/frontend-design`
- Site visual design → `/design-consultation`, `/frontend-design`
- Ship / open PR → `/ship`
