---
name: mlaunch
version: 0.1.0
description: |
  Generate a complete launch campaign from your repo. Reads README, CHANGELOG,
  and brand voice to produce landing page copy, email announcement, social posts,
  and ad copy in one command.
---

# /mlaunch

Generate a complete launch kit from your repo in under 60 seconds.

## Preamble

```bash
_BRAND_REPO="marketing/BRAND.md"
_BRAND_GLOBAL="$HOME/.mstack/BRAND.md"
_README="README.md"
_CHANGELOG="CHANGELOG.md"
_OUT="marketing/launch/$(date +%Y-%m-%d)"
mkdir -p "$_OUT"
echo "Output dir: $_OUT"

# Detect brand voice source
if [ -f "$_BRAND_REPO" ]; then
  echo "BRAND: repo (marketing/BRAND.md)"
elif [ -f "$_BRAND_GLOBAL" ]; then
  echo "BRAND: global (~/.mstack/BRAND.md)"
else
  echo "BRAND: none (will infer)"
fi

# Detect context sources
[ -f "$_README" ] && echo "README: found" || echo "README: missing"
[ -f "$_CHANGELOG" ] && echo "CHANGELOG: found" || echo "CHANGELOG: missing"
```

## Input Resolution

Gather context in this order:

1. **Inline arg:** If the user ran `/mlaunch "description here"`, use that as the
   primary product description. Skip README extraction for description.

2. **README.md:** Read up to 8KB.
   - Product name: the H1 heading
   - Description: first paragraph after H1
   - Target user: content under a heading containing "who", "for", or "audience"
   - If README missing or < 50 words: proceed to interactive fallback

3. **CHANGELOG.md:** Read the first version entry only (content until the second
   `## [` or EOF). Max 2KB. This is "what's new."

4. **Tech stack:** Check for `package.json` (read `name` + `description` fields),
   `go.mod` (module name), `pyproject.toml` (name + description). One line of
   context max.

5. **BRAND.md:** If found (repo > global), prepend to prompt as voice constraints.

6. **Interactive fallback** (if README missing or < 50 words and no inline arg):
   Ask ONE question: "What does your product do, and who is it for?" Wait for
   the answer before proceeding.

## Generation

Using the gathered context, generate all four assets now. You are the copywriter.

**Voice and tone:**
- Write like a founder talking to a peer, not a marketer talking to a prospect
- Specific beats vague. If the README says "reduces build time by 40%", use that number.
  If there's no number, find the most concrete fact available.
- Short sentences. Active voice. No throat-clearing.
- Banned words (replace if generated): unlock, revolutionize, game-changer, powerful,
  seamless, robust, comprehensive, leverage, synergy, cutting-edge, innovative,
  streamline, empower, transformative

**Rules per asset:**
- Twitter/X posts: each tweet ≤280 characters, no emojis unless brand uses them
- Headlines: ≤10 words, start with a verb or the product name
- Email subjects: ≤50 characters, no ALL CAPS, no clickbait ("You won't believe...")
- Google headlines: ≤30 characters each (count carefully)
- Meta primary text: ≤125 characters

**Grounding rule:** At least one specific number, feature name, or concrete fact from
the repo context must appear somewhere in each output file. If the context is thin,
use the product name and what it does — not generic benefits.

Generate all four files now, following the output formats below exactly.

## Output

Write four files to `marketing/launch/{YYYY-MM-DD}/`:

**hero.md** — landing page copy
```
# [Headline — ≤10 words]
## [Subheadline — one sentence, what it does and for whom]

### [Feature 1 — 3 words max]
[One sentence description]

### [Feature 2]
[One sentence]

### [Feature 3]
[One sentence]

**[CTA button text]** — [URL placeholder]
```

**announcement.md** — email announcement
```
Subject: [Option 1]
Subject: [Option 2]
Subject: [Option 3]
Preview: [Preview text, ≤90 chars]

---

[Email body — 150-200 words, conversational, ends with single CTA]
```

**social.md** — social posts
```
## Twitter/X Thread
1/ [Tweet 1 — the hook]
2/ [Tweet 2 — the problem]
3/ [Tweet 3 — the solution]
4/ [Tweet 4 — the proof/feature]
5/ [Tweet 5 — the CTA]

## LinkedIn
[150-200 word post, professional but not corporate]

## Hacker News (Show HN)
Show HN: [Product name] — [one-line description]
[2-3 sentences: what it is, who built it, why now]
```

**ads.md** — ad copy
```
## Google Search Ads
Headline 1: [≤30 chars]
Headline 2: [≤30 chars]
Description: [≤90 chars]

Headline 1: [variant 2]
Headline 2: [variant 2]
Description: [variant 2]

## Meta/Social Ads
Primary text: [≤125 chars]
Headline: [≤40 chars]

Primary text: [variant 2]
Headline: [variant 2]
```

## Quality Check

After writing files, verify each against quality gates:
- [ ] No banned words in any file
- [ ] All Twitter posts ≤280 chars
- [ ] All Google headlines ≤30 chars
- [ ] All email subjects ≤50 chars
- [ ] At least one number or specific fact appears across the output

If a gate fails: fix inline without re-calling Claude (simple word substitution
or length trim). If a fix would change meaning, flag it to the user.

## Completion

```bash
echo ""
echo "✦ Launch kit ready: $_OUT"
echo "  hero.md          — landing page copy"
echo "  announcement.md  — email announcement (3 subject variants)"
echo "  social.md        — Twitter thread, LinkedIn, HN Show HH"
echo "  ads.md           — Google + Meta ad copy"
echo ""
echo "Next: review and edit, then /mretro after your launch to capture what worked."
```

Report: DONE if all 4 files written and quality gates passed.
Report: DONE_WITH_CONCERNS if any quality gate had to be manually fixed.
