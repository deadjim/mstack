# Changelog

## [0.1.0] - 2026-03-28 — Initial Release

### Added

- `/mlaunch` — generate a complete launch campaign from your repo
- `/mbrand` — infer brand voice and write `marketing/BRAND.md`
- `/mcmo` — one-page positioning and channel strategy
- `/mcopy` — rewrite any copy with brand voice
- `/memail` — generate email sequences from a goal
- `/mads` — generate ad copy variants
- `/mseo` — SEO audit from URL or markdown
- `/maudit` — full marketing gap analysis
- `/mretro` — weekly marketing retrospective

## [0.1.1] - 2026-03-28 — Sprint 1 Tests Pass

### Tested

- `/mlaunch` on mstack itself (338-word README) — all quality gates pass
- `/mlaunch` on actual-ai (1234-word README, no CHANGELOG) — all gates pass, 1 subject line trimmed
- `/mlaunch` on sparse README (6 words) — interactive fallback works, all gates pass

## [0.2.0] - 2026-03-28 — Research-First Positioning

Major redesign of /mlaunch based on feedback: confident output for a zero-user
product is the wrong goal.

### Changed

- `/mlaunch` now runs synthetic user research before generating any copy:
  Reddit threads, HN discussions, G2/Trustpilot reviews, job postings, competitor
  landing pages. Real human language beats README-derived copy every time.
- Output changes from 1 campaign to **3 positioning hypotheses** with different
  ICPs, pains, and wedges. Each hypothesis includes a cheap test strategy.
- Added `RESEARCH.md` — the research brief that grounds all copy decisions.
- Added `ASSUMPTIONS.md` — 5+ falsifiable beliefs with defined test signals.
  `/mretro` will score these post-launch.
- Competitor analysis now surfaces "what's been said to death" so your wedge
  is the gap, not a repeat of existing positioning.
