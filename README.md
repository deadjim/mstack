# GTMstack

AI marketing team for Claude Code.

gstack gave Claude Code a virtual engineering team. GTMstack gives it a virtual marketing team — CMO, copywriter, SEO strategist, email marketer, ad writer — all as slash commands in your terminal.

**The insight:** every existing AI marketing tool is a SaaS dashboard built for marketers. GTMstack lives in the terminal because it's built for founders who live in the terminal. A `/mlaunch` command run next to `git push` is a fundamentally different product.

## Install

```bash
git clone --single-branch --depth 1 https://github.com/deadjim/GTMstack.git \
  ~/.claude/skills/GTMstack && cd ~/.claude/skills/GTMstack && ./setup
```

## Skills

| Command | What it does |
|---------|-------------|
| `/mlaunch` | Reads your README + CHANGELOG → generates landing page copy, email announcement, social posts, ad copy |
| `/mbrand` | Infers your brand voice → writes `marketing/BRAND.md` |
| `/mcmo` | Produces a one-page positioning brief and channel strategy |
| `/mcopy` | Rewrites any file with brand voice |
| `/memail` | Generates email sequences (onboarding, launch, re-engagement) |
| `/mads` | Generates ad copy variants for Google, Meta, LinkedIn |
| `/mseo` | SEO audit from URL or markdown |
| `/maudit` | Full marketing gap analysis |
| `/mretro` | Weekly marketing retrospective |

## Usage

Run from inside any git repo:

```bash
/mlaunch                          # reads README + CHANGELOG
/mlaunch "My product does X for Y" # with explicit description
/mbrand                           # run this first on a new project
/mcopy landing.md                 # rewrite a specific file
/memail onboarding --emails 5     # 5-email onboarding sequence
```

Output goes to `marketing/` in your repo. Never overwrites source files.

## How it works

1. Reads `README.md`, `CHANGELOG.md`, and `marketing/BRAND.md` for context
2. Calls Claude once per command (single API call, ~$0.02)
3. Writes markdown files to `marketing/{skill}/{date}/`

## Works great with gstack

GTMstack and gstack are independent installs that compose naturally:
- Use gstack to build and ship your feature
- Use GTMstack to launch it

## Requirements

- [Claude Code](https://claude.ai/code)
- Git

## License

MIT
