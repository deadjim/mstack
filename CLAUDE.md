# mstack — AI Marketing Team for Claude Code

mstack gives Claude Code a virtual marketing team. Same install pattern as gstack,
but the specialists are marketers: CMO, copywriter, SEO strategist, email marketer,
ad writer.

## Available Skills

- `/mdiscover` — synthetic user research before you've decided what to build
- `/mlaunch` — generate a complete launch campaign from your repo (reads /mdiscover output)
- `/mbrand` — infer brand voice, write `marketing/BRAND.md`
- `/mcmo` — one-page positioning and channel strategy
- `/mcopy` — rewrite any file with brand voice
- `/memail` — generate email sequences
- `/mads` — generate ad copy variants
- `/mseo` — SEO audit from URL or markdown
- `/maudit` — full marketing gap analysis
- `/mretro` — score marketing assumptions against real signal after launch

## Marketing Principles

- Read `marketing/BRAND.md` before generating any copy (repo-scoped).
  Fall back to `~/.mstack/BRAND.md` (global). Infer from repo if neither exists.
- Specificity beats adjectives. Numbers beat claims.
- Never use: unlock, revolutionize, game-changer, powerful, seamless, robust,
  comprehensive, leverage, synergy, cutting-edge.
- Match the product stage: pre-launch copy differs from growth copy.
- Output lives in `marketing/` — never overwrite source files.

## Context Reading Order

1. `marketing/BRAND.md` (repo-scoped brand voice)
2. `~/.mstack/BRAND.md` (global brand voice fallback)
3. `README.md` — product name (H1), description (first paragraph), target user
4. `CHANGELOG.md` — latest version entry as "what's new"
5. Tech stack detection: `package.json`, `go.mod`, `pyproject.toml`

## Context Budget

Max 8KB from README + 2KB from CHANGELOG latest entry + 200 chars tech stack.
Files larger than budget are truncated. Pass `--full-context` to disable.
