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
