---
name: mlaunch
version: 0.2.0
description: |
  Generate 3 positioning hypotheses from synthetic user research — not just your
  README. Scrapes Reddit, HN, G2/Trustpilot, and competitor pages to find real
  human language before writing a word of copy.
---

# /mlaunch

Most launch copy fails because it's written from the founder's perspective, not the
user's. /mlaunch fixes that by doing synthetic user research before generating anything.

The output is not one polished campaign. It's 3 cheap positioning hypotheses with
meaningfully different ICPs, pain hooks, and wedges — ready to test in parallel.
Let data pick the winner before you scale.

## Preamble

```bash
_BRAND_REPO="marketing/BRAND.md"
_BRAND_GLOBAL="$HOME/.mstack/BRAND.md"
_README="README.md"
_CHANGELOG="CHANGELOG.md"
_DATE=$(date +%Y-%m-%d)
_OUT="marketing/launch/$_DATE"
mkdir -p "$_OUT"
echo "Output dir: $_OUT"

[ -f "$_BRAND_REPO" ] && echo "BRAND: repo" || { [ -f "$_BRAND_GLOBAL" ] && echo "BRAND: global" || echo "BRAND: none"; }
[ -f "$_README" ] && echo "README: found ($(wc -w < $_README) words)" || echo "README: missing"

# Check browse binary for research phase
B=""
[ -x "$HOME/.claude/skills/gstack/browse/dist/browse" ] && B="$HOME/.claude/skills/gstack/browse/dist/browse"
[ -n "$B" ] && echo "BROWSE: ready" || echo "BROWSE: unavailable (research phase will use WebSearch fallback)"
```

## Phase 1: Product Context

Gather what you know about the product:

1. **README.md** — product name (H1), description (first paragraph), target user
   (section with "who", "for", "audience"), key features. Max 8KB.
2. **CHANGELOG.md** — first version entry only. Max 2KB.
3. **Tech stack** — `package.json`, `go.mod`, `pyproject.toml`. One line.
4. **Inline arg** — `/mlaunch "description"` overrides README description.
5. **Interactive fallback** — if README < 50 words and no inline arg, ask:
   "What does your product do, and who is it for?"

Extract and state clearly:
- Product name
- One-sentence description of what it does
- Who it's for (best guess from README — this will be challenged in Phase 2)
- 3-5 key features or facts
- What it costs or how it's distributed

## Phase 2: Synthetic User Research

**Goal:** Find how real people describe this problem in their own words — before
you describe your solution in yours.

Run the following searches. Use WebSearch (or `$B goto` + `$B text` if browse is
available for richer scraping). Adapt search terms to the actual product.

### 2a. Reddit — problem language

Search: `site:reddit.com "[problem space]" frustration OR "wish there was" OR "how do you"`

Read the top 3-5 results. Extract:
- Exact phrases people use to describe the pain (quote them)
- What workarounds they're using
- What they've tried and why it failed
- Emotional language: frustration, embarrassment, wasted time, cost

### 2b. HN — technical buyer language

Search: `site:news.ycombinator.com "Ask HN" [problem space]`

Read the top 2-3 threads. Extract:
- How technical users frame the problem
- What solutions they've evaluated and rejected
- Price sensitivity signals
- "I wish X would just..." statements

### 2c. Competitor reviews — G2 / Trustpilot / App Store

Identify 1-2 closest competitors from the product context. Search:
`site:g2.com "[competitor]" reviews` or `site:trustpilot.com "[competitor]"`

Extract:
- 1-star and 2-star reviews: what breaks, what's missing, what's overpriced
- 5-star reviews: what they love (this is what you must match or beat)
- Exact phrases that appear in multiple reviews (these are resonant)

### 2d. Job postings — operational pain

Search: `"[job title most likely to buy this]" job posting [related workflow]`

Extract:
- How companies describe the problem in hiring language
- What skills/tools they list (reveals the current status quo)
- What outcomes they promise to whoever solves it

### 2e. Competitor landing pages — what's been said to death

Visit 1-2 competitor homepages. Extract:
- Their headline and subheadline (this is what's already been said)
- Their top 3 claimed benefits
- Their CTA

**The gap is your wedge.** If every competitor says "save time," you don't say
"save time." You find what they're not saying.

### Research synthesis

After gathering, produce a **Research Brief** written to `marketing/launch/{date}/RESEARCH.md`:

```markdown
# Research Brief — [Product Name] — [Date]

## Real user language (direct quotes)
- "[quote from Reddit/HN/review]" — source
- "[quote]" — source
...

## Current workarounds
- [what people do today instead]

## Competitor positioning (what's already been said)
- [Competitor 1]: "[their headline]" — claims: [list]
- [Competitor 2]: "[their headline]" — claims: [list]

## The gap
[1-2 sentences: what every competitor says vs. what nobody is saying]

## Resonant phrases to steal (use verbatim or close)
- "[phrase from reviews/Reddit]"
- "[phrase]"

## Signals about who hurts most
[Which segment of potential users expressed the most acute pain? Quote evidence.]
```

## Phase 3: 3 Positioning Hypotheses

Using the research brief, generate 3 meaningfully different campaign directions.
These are not variations of the same campaign — they bet on different things.

**Each hypothesis must differ on at least 2 of these axes:**
- ICP (who is it for — be specific: "ops manager at 20-person SaaS" not "businesses")
- Primary pain (speed vs. cost vs. embarrassment vs. reliability vs. status)
- Wedge (what makes this different from the thing they're already using)
- Hook (the single sentence that earns the next sentence)

For each hypothesis, write to `marketing/launch/{date}/hypothesis-[A|B|C].md`:

```markdown
# Hypothesis [A|B|C]: [Name — 3 words describing the bet]

## The bet
ICP: [Specific person — title, company size, context]
Primary pain: [One pain, stated as the user would state it]
Wedge: [Why this, why now, vs. what they're doing today]
Hook: [The single opening line that earns the next]

## Confidence level: [Low|Medium|High]
## Evidence from research: [1-2 quotes or signals that support this bet]
## What would prove this wrong: [Falsifiable signal]

---

## Hero copy
### [Headline — ≤10 words, active voice, no banned words]
#### [Subheadline — one sentence]

**[Feature 1 — 3 words]**
[One sentence]

**[Feature 2]**
[One sentence]

**[Feature 3]**
[One sentence]

**[CTA]** — [URL placeholder]

---

## Email subject lines (3 variants)
- Subject: [≤50 chars]
- Subject: [≤50 chars]
- Subject: [≤50 chars]
Preview: [≤90 chars]

---

## Tweet hook
[Single tweet ≤280 chars — the one you'd post to test this positioning]

---

## How to test this hypothesis cheap
[Specific: post to which subreddit, which HN thread to comment on, which
community to share in, what ad to run at $5/day and what click = signal]
```

**Banned words across all copy:** unlock, revolutionize, game-changer, powerful,
seamless, robust, comprehensive, leverage, synergy, cutting-edge, innovative,
streamline, empower, transformative, excited to announce, proud to share.

**Grounding rule:** Every hypothesis must use at least one phrase lifted directly
from the research (quotes from users, reviews, or job postings). Real language
beats founder language every time.

## Phase 4: Assumption Log

Write `marketing/launch/{date}/ASSUMPTIONS.md`:

```markdown
# Marketing Assumptions — [Product Name] — [Date]

These are the beliefs this launch is betting on. /mretro will score each one
after you have data.

## ICP assumptions
- [ ] **A1:** [Specific belief about who the primary buyer is]
      Evidence: [what made us think this]
      Test: [what signal would confirm or deny]

- [ ] **A2:** [Another ICP belief]
      ...

## Pain assumptions
- [ ] **B1:** [Belief about what pain matters most]
      Evidence:
      Test:

- [ ] **B2:** ...

## Channel assumptions
- [ ] **C1:** [Where this person hangs out / how they discover tools]
      Evidence:
      Test:

## Pricing/conversion assumptions
- [ ] **D1:** [Belief about willingness to pay or convert]
      Evidence:
      Test:

## Competitive assumptions
- [ ] **E1:** [Belief about why they'd switch from current solution]
      Evidence:
      Test:

---
*Scored by /mretro after launch. Update each assumption with: CONFIRMED /
REFUTED / UNCLEAR + evidence.*
```

## Phase 5: Quality Gates

Check all hypothesis files:
- [ ] No banned words
- [ ] All tweet hooks ≤280 chars
- [ ] All email subjects ≤50 chars
- [ ] All headlines ≤10 words
- [ ] Each hypothesis uses ≥1 direct quote or phrase from research
- [ ] Each hypothesis has a falsifiable "what would prove this wrong" statement
- [ ] ASSUMPTIONS.md has ≥5 assumptions with tests defined

Fix inline if possible. Flag to user if a fix would change meaning.

## Completion

```bash
echo ""
echo "✦ /mlaunch complete: $_OUT"
echo ""
echo "  RESEARCH.md          — synthetic user research brief"
echo "  hypothesis-A.md      — positioning bet A"
echo "  hypothesis-B.md      — positioning bet B"
echo "  hypothesis-C.md      — positioning bet C"
echo "  ASSUMPTIONS.md       — what this launch is betting on"
echo ""
echo "Next: pick one hypothesis to test first, or run all 3 cheap in parallel."
echo "Run /mretro after 2 weeks to score your assumptions."
```

**This is not a launch. It's a test.** The goal is to learn which hypothesis
resonates before spending real money or reputation on any of them.

Report: DONE if all 5 files written and quality gates passed.
Report: DONE_WITH_CONCERNS if research phase was limited (search unavailable, etc.)
