# Marketing Assumptions — GTMstack — 2026-03-28

These are the beliefs this launch is betting on. Run `/mretro` after 2 weeks to score each one.

## ICP assumptions

- [ ] **A1:** The primary user is a solo technical founder with 0-to-1 products (no users yet), not a post-traction growth engineer.
      Evidence: Reddit/IH data shows "0 users" pain is expressed acutely and repeatedly; gstack users skew technical founder.
      Test: Check GitHub star-to-issue ratio. Issues from post-traction founders = A1 wrong.

- [ ] **A2:** The user is already comfortable with CLI tools (can run `git clone` and `./setup` without friction).
      Evidence: gstack has this audience; GTMstack targets the same community.
      Test: Any "how do I install this?" issues = friction at the install step = A2 wrong or onboarding needs work.

- [ ] **A3:** The user does their own marketing (no marketing hire or co-founder).
      Evidence: Pain language consistently comes from solo operators wearing every hat.
      Test: Survey first 10 users — do they have a marketing person? If >30% do, A3 wrong.

## Pain assumptions

- [ ] **B1:** The primary pain is not "writing copy is hard" — it's "I don't know who my user is or what to say to them." Research-first is the right wedge, not faster copy generation.
      Evidence: "If your indie project is stuck, it's probably because no one knows how it helps them." Research-first is the differentiated feature vs. every competitor.
      Test: Do users engage with RESEARCH.md and ASSUMPTIONS.md, or do they only look at hypothesis copy? If they ignore the research, B1 is wrong.

- [ ] **B2:** The user is more motivated by "test cheap" positioning than "launch polished."
      Evidence: 37 launches with no traction → founder explicitly said they need a different approach. Polished = risky; cheap test = low stakes.
      Test: Does the "3 hypotheses" framing generate discussion, or do users say "I just want one good campaign"?

- [ ] **B3:** The gstack community is the right launch channel — they're already context-aware on Claude Code skills.
      Evidence: Shared architecture, shared install pattern, shared audience of technical founders.
      Test: GitHub stars in first 2 weeks from gstack Discussions post. Target: 25+.

## Channel assumptions

- [ ] **C1:** GitHub Discussions on garrytan/gstack is the highest-leverage first channel.
      Evidence: Built-in audience with exactly the right profile. Zero paid spend.
      Test: Stars and installs in the first week. Baseline: 10+ stars from one post = confirmed.

- [ ] **C2:** HN Show HH is a viable second channel (not first — timing matters).
      Evidence: GTMstack is technical, open source, solves a real developer problem. HN reward these.
      Test: Front page = confirmed. <20 upvotes in first hour = wrong day/time, retry.

- [ ] **C3:** Hypothesis A (the crickets problem) will outperform B and C on the IH/Reddit channel.
      Evidence: Language match — "crickets" is their exact language.
      Test: Post all 3 hooks as different threads or A/B test. Measure replies and click-through.

## Pricing/conversion assumptions

- [ ] **D1:** "Free, open source, $0.02/run" is a meaningful advantage over Jasper/Copy.ai for this audience.
      Evidence: Billing horror stories are extensively documented. Trust is broken with incumbents.
      Test: Do users mention cost/pricing in installs or issues? If nobody mentions it, it's not the wedge.

- [ ] **D2:** The install friction (git clone + ./setup) will not materially reduce conversion for this audience.
      Evidence: gstack uses the same pattern and has significant adoption.
      Test: GitHub clone count vs. star count. Ratio <0.3 = friction is real.

## Competitive assumptions

- [ ] **E1:** "Jasper refugee" (Hypothesis C) is a smaller audience than "crickets founder" (Hypothesis A) for this product.
      Evidence: Jasper users skew non-technical; GTMstack requires CLI comfort. The overlap may be thin.
      Test: If Hypothesis C generates more engagement than A in the first week, E1 is wrong — pivot messaging.

- [ ] **E2:** The research-first approach (Phase 2 of /mlaunch) is what makes GTMstack meaningfully different — not just the CLI interface.
      Evidence: Multiple "devs who hate marketing" tools exist. The gap is the approach, not the interface.
      Test: Do users mention RESEARCH.md or the hypothesis framework in reviews/discussions? If they only talk about "terminal-native," E2 is wrong and the interface is the real wedge.

---
*Score each assumption after 2 weeks: CONFIRMED / REFUTED / UNCLEAR + evidence.*
*Run `/mretro` to structure the scoring.*
