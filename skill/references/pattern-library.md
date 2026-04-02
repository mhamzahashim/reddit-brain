# Pattern Library: Reddit Post Diagnostic Reference

## Table of Contents
1. [Post Patterns (15)](#post-patterns)
2. [Something Feels Off Detectors (5)](#detectors)
3. [Rapid Assessment Heuristics (8)](#heuristics)
4. [Compound Pattern Rules](#compound-patterns)
5. [Confidence Calibration](#confidence-calibration)
6. [Verification Protocol](#verification-protocol)
7. [Quick Reference Flags](#quick-reference-flags)

---

## Post Patterns

### P01: XY Problem
- **Surface:** Specific, bizarre technical question with no context for why they need it
- **Reality:** They have problem Y, decided solution is X, now stuck on X. Wrong path entirely.
- **Checklist:** (1) Ultra-specific question, absent motivation (2) Convoluted approach to a common problem (3) Pushing for context reveals a different goal (4) Resists alternative approaches (5) Experts would see a simpler path
- **Threshold:** 3/5 | **Misdiagnosis cost:** Genuine edge case gets redirected away from a correct unusual approach
- **Response:** Probe for underlying goal before answering. "What's the end result you're trying to achieve?" Redirect gently if Y emerges.

### P02: Validation Seeker
- **Surface:** Framed as question but reads as statement seeking permission. "Am I crazy for..." / "Would it be bad to..."
- **Reality:** Decision is made. Seeking external confirmation to reduce cognitive dissonance.
- **Checklist:** (1) Clear preference despite open framing (2) Counterarguments preemptively dismissed (3) Enthusiastic with agreement, defensive with challenge (4) Emotional investment language ("My gut says...") (5) Irreversible steps already taken
- **Threshold:** 3/5 | **Misdiagnosis cost:** Genuinely undecided person feels patronized
- **Response:** Honor the decision energy. If reasonable, validate with a new reason. If blind spot exists, raise it as preparation, not opposition.

### P03: Grief Poster
- **Surface:** Practical question with loss/upheaval mentioned casually as context
- **Reality:** Processing grief through a practical container. Needs to be seen in their pain.
- **Checklist:** (1) Significant life event mentioned in passing (2) Question is easily researchable (serves another purpose) (3) Emotional leakage ("I know this is silly but...") (4) History reveals recent upheaval (5) Mismatch between question simplicity and context weight
- **Threshold:** 3/5 | **Misdiagnosis cost:** Person who mentioned hardship as context feels uncomfortably psychoanalyzed
- **Response:** Answer the practical question well. Briefly, naturally acknowledge the context. Mirror the emotional/practical ratio of the post.

### P04: Humble Brag
- **Surface:** Appears to ask for help but core highlights an achievement. "VP at 28 with impostor syndrome..."
- **Reality:** Wants recognition wrapped in a complaint to make sharing socially acceptable.
- **Checklist:** (1) Impressive specifics unnecessary for the question (2) The "problem" is enviable (3) Remove impressive details and question becomes trivial (4) Replies add more impressive details (5) Question could be resolved privately
- **Threshold:** 3/5 | **Misdiagnosis cost:** High achiever with genuine struggle feels dismissed and unseen
- **Response:** Brief acknowledgment of achievement, then treat stated problem as real and provide genuine advice.

### P05: Overwhelmed Novice
- **Surface:** Broad, unfocused question. "I want to start a business, where do I begin?"
- **Reality:** Lacks foundational framework to ask a specific question. Needs a map, not an answer.
- **Checklist:** (1) Extremely broad question (2) No foundational knowledge visible (3) Cannot articulate specific confusion (4) Lists many disparate options without prioritizing (5) Previous attempts show scatter
- **Threshold:** 3/5 | **Misdiagnosis cost:** Gets a resource dump that adds to overwhelm
- **Response:** Simplified mental model ("There are really 3 paths..."), reduce option space, explain logic, give exactly one next step.

### P06: Confident Incompetent (Dunning-Kruger)
- **Surface:** Advanced terminology applied incorrectly. Exudes confidence about a flawed understanding.
- **Reality:** Peak of Mt. Stupid. Enough vocabulary to feel expert, lacks depth to see errors.
- **Checklist:** (1) Technical terms used subtly wrong (2) Confident assertions without caveats on complex topics (3) Sophisticated-sounding plan with fundamental errors (4) Resistance to correction (5) Telling, not asking
- **Threshold:** 3/5 | **Misdiagnosis cost:** Expert using unfamiliar framework feels disrespected
- **Response:** Acknowledge what they got right. Introduce correction via question or scenario, not statement. Create curiosity, not defensiveness.

### P07: Analysis Paralysis
- **Surface:** Extremely detailed, well-researched comparison of functionally equivalent options
- **Reality:** Research is procrastination. Fear of commitment, perfectionism, avoidance of responsibility.
- **Checklist:** (1) Disproportionate research relative to stakes (2) Options are functionally similar (3) Keeps finding "one more thing" to evaluate (4) History of similar research spirals (5) Real-life situation unchanged despite all research
- **Threshold:** 3/5 | **Misdiagnosis cost:** Genuinely complex decision gets rushed
- **Response:** Name the pattern with compassion. "Any of these would work. The biggest risk is not choosing." Give permission to stop researching.

### P08: Sunk Cost Prisoner
- **Surface:** Clear exit path visible to outsiders, but poster focuses on making current situation work
- **Reality:** Trapped by loss aversion. Measuring against past investment, not future value. Identity threat.
- **Checklist:** (1) Frequent references to time/money already spent (2) Frames leaving as "giving up" or "wasting" (3) Asks how to improve what an outsider would exit (4) Emotional language around investment, not current experience (5) Aware of problem for a long time
- **Threshold:** 3/5 | **Misdiagnosis cost:** Reasonable persistence gets pathologized
- **Response:** Reframe backward to forward. "If starting from scratch today, would you choose this?" Normalize the feeling. Separate identity from investment.

### P09: Comparison Spiraler
- **Surface:** Own situation heavily referenced against others' success. "Everyone seems to be making $200K..."
- **Reality:** Behind-the-scenes vs. highlight reels. Composite ideal no one actually achieves.
- **Checklist:** (1) Explicit comparisons to peers/cohorts (2) Composite ideal across domains (3) Actual situation not as dire as emotional response (4) Quantitative framing of qualitative outcomes (5) Emotional weight from comparison, not circumstances
- **Threshold:** 3/5 | **Misdiagnosis cost:** Genuinely behind person gets platitudes instead of action plan
- **Response:** Validate the feeling briefly. Reframe the comparison lens. Redirect to personal trajectory: "Compared to where YOU were a year ago..."

### P10: Feature Creep Victim
- **Surface:** Excited about features/tech with conspicuous absence of customers, revenue, validation
- **Reality:** Building is comfort zone. Using development as procrastination to avoid market rejection.
- **Checklist:** (1) Feature/tech detail with no customer/revenue mention (2) Extended development with no launch date (3) Questions about building, not market (4) Pivots to features when asked about validation (5) Roadmap expanding, not narrowing
- **Threshold:** 3/5 | **Misdiagnosis cost:** Pre-PMF product that genuinely needs development gets rushed to market
- **Response:** Acknowledge the craft. Introduce the constraint: "Features before launch are rarely features that matter." Concrete step: "Get 5 people to use it this week."

### P11: Guru Bait (Disguised Self-Promotion)
- **Surface:** Genuine-seeming question/discussion that steers toward poster's expertise/product/content
- **Reality:** Marketing. Community as target audience. Question-framing as Trojan horse for promotion.
- **Checklist:** (1) Profile shows pattern of similar posts across subs (2) Question conveniently leads to their product (3) Replies disproportionately promote own solution (4) Suspiciously well-branded frameworks (5) Reads like content marketing (polished, structured)
- **Threshold:** 3/5 | **Misdiagnosis cost:** Genuine expert contributor gets accused of marketing
- **Response:** If content is valuable, engage substance while noting: "OP runs [product]. Alternatives include [X]." If thin/promotional, brief factual callout.

### P12: Rage Poster
- **Surface:** Angry, long post about injustice. Question appended but energy is cathartic, not solution-seeking.
- **Reality:** Acute emotional phase. Amygdala hijack. Needs to feel heard before they can hear solutions.
- **Checklist:** (1) Disproportionate intensity (2) Clear villain, little complexity acknowledged (3) Question is rhetorical afterthought (4) Post far longer than informational content requires (5) Dismisses calm advice, escalates emotion
- **Threshold:** 3/5 | **Misdiagnosis cost:** Genuinely wronged person has experience pathologized
- **Response:** Lead with validation. Then one minimal, actionable step. Do not introduce nuance about the villain yet.

### P13: "Am I Wrong" (One-Sided Story)
- **Surface:** Conflict with clear moral framing. Poster is reasonable protagonist, other party is caricature.
- **Reality:** Motivated reasoning in narrative form. Building a case, not seeking judgment.
- **Checklist:** (1) Clear protagonist/antagonist with no ambiguity (2) Other party's reasoning absent or irrational (3) Specific when supporting poster, vague when complicating (4) Absolute language about other party (5) Binary framing ("Am I wrong?")
- **Threshold:** 3/5 | **Misdiagnosis cost:** Genuine abuse victim has their experience questioned
- **Response:** Validate the emotion, not the narrative. Gently introduce perspective. Redirect from "who's right" to "what outcome do you want?"

### P14: Burnout Denier
- **Surface:** Productivity/performance question. "How do I get more done?" with 80-hour weeks.
- **Reality:** Exhaustion reframed as performance problem. Needs rest, not a better system.
- **Checklist:** (1) Optimization questions plus extreme hours (2) Burnout symptoms described as performance problems (3) "I just need more discipline" (4) Explains why rest isn't an option (5) Casual physical symptoms (sleep, headaches, appetite)
- **Threshold:** 3/5 | **Misdiagnosis cost:** Student or career-changer gets unsolicited mental health advice
- **Response:** Meet in their framework. Frame rest as performance optimization. "Your focus problems aren't discipline; they're recovery deficit."

### P15: Shiny Object Chaser
- **Surface:** Enthusiastic about new project. "I'm all in!" But history shows pattern of abandoned starts.
- **Reality:** Addicted to dopamine of new beginnings. Avoids the difficult middle phase.
- **Checklist:** (1) High energy, detailed beginning plans, vague middle/end (2) History of similar enthusiastic starts (3) "This time is different" without articulating what changed (4) Elaborate vision, no unglamorous execution details (5) External attribution for past abandonments
- **Threshold:** 3/5 | **Misdiagnosis cost:** Legitimate early-career exploration gets pathologized
- **Response:** Acknowledge excitement. Name the meta-pattern without judgment. Redirect to understanding the recurring motivation dip.

---

## Detectors

### Detector A: "Not What It Seems" (Authenticity Check)
| IF | THEN flag |
|---|---|
| Peripheral detail >> central detail | smokescreen_pattern |
| Emotional tone mismatches situation severity | tone_mismatch |
| Crisis described + perfect grammar + organized structure | possible_fabrication_or_dissociation |
| One-sided narrative + zero other perspective | missing_perspective |
| Compressed timeline + exceptional outcome | timeline_impossible |
| Key figures vague + peripheral figures specific | selective_vagueness |

### Detector B: "About to Make a Huge Mistake"
| IF | THEN flag |
|---|---|
| Question asked but irreversible steps already taken | seeking_permission_not_advice |
| Major decision + no mention of downside risk | risk_blindness |
| Primary argument = past investment, not future value | sunk_cost_spiral |
| Uses "should," "can't give up," "too late to" | obligation_not_desire |
| Comparison to others + self-deprecation | comparison_trap |
| Dismisses counterarguments preemptively | decision_already_made |

### Detector C: "Emotional Crisis Beneath" (SAFETY CRITICAL)
| IF | THEN flag |
|---|---|
| Technical question + emotional adjectives (exhausted, desperate, lost, broken, worthless) | crisis_beneath_technical |
| Deeply personal subject + analytical/clinical tone | performing_rationality |
| Explicitly rejects therapy/emotional support/mental health | blocking_needed_help |
| Mentions isolation, no support, self-medication, sleep disruption | crisis_indicators |
| Hopelessness + absolute language (never, always, nothing) | **URGENT: possible crisis** |
| Future tense absent + present suffering described | lost_sense_of_future |

Protocol when C fires: (1) Acknowledge emotional reality first (2) Name gently, do not force (3) Answer practical question (4) One non-preachy support mention (5) If Signal 5: include crisis resources

### Detector D: "This Success Story Is BS"
| IF | THEN flag |
|---|---|
| Revenue claimed + no expenses/margins/timeframe/hours | revenue_without_context |
| Outcome specific + method vague | hiding_the_how |
| Post ends with link/DM invite/community/course mention | funnel_detected |
| "Anyone can do this" + outlier result | survivorship_bias_selling |
| Urgency language + no objective deadline | manufactured_urgency |
| Clean hero's journey + no ongoing struggles | too_clean_to_be_real |
| Account shows similar posts across subreddits | pattern_promotion |

### Detector E: "Real Question Is Underneath"
| IF | THEN flag |
|---|---|
| Asking about advanced tool + early-stage problem context | premature_optimization (direction doubt) |
| Asking about growth strategy + stagnation/decline context | strategy masking exit question |
| Asking HOW + no mention of WHY | skipped the SHOULD question |
| Emotional weight >> decision magnitude | specific question, general anxiety |
| Execution question + description reveals premise doubt | real question one level deeper |

Protocol when E fires: (1) Answer surface question (2) Gently surface deeper question (3) Frame as normal, not criticism (4) Let poster choose which level to engage

---

## Heuristics

| # | Heuristic | Core Question | Application |
|---|---|---|---|
| 1 | **Cui Bono** | Who benefits from me believing this? | If poster benefits (selling, authority), apply heavy skepticism. If third party benefits, trace the source chain. |
| 2 | **What's Missing** | What must a genuine version include that this doesn't? | Success story missing timeline/costs/failures. Advice request missing constraints/what they tried. Relationship problem missing other perspective. |
| 3 | **Base Rate** | How often does this outcome actually happen? | $1M business in 12 months: <0.1% (extreme skepticism). Imposter syndrome: ~70% prevalence (low skepticism). Startup failed: ~90% base rate (plausible). |
| 4 | **Reversibility** | How easily undone if wrong? | Easily reversible (bias toward action). Barely reversible (bias toward deliberation). Scale caveat density to irreversibility. |
| 5 | **10/10/10** | How will this matter in 10 days / 10 months / 10 years? | Reframes short-term emotion into strategic perspective. Most agonized decisions are irrelevant at the 10-year horizon. |
| 6 | **Status Quo Test** | If NOT already in this situation, would they choose to enter it? | Strips away sunk cost, inertia, loss aversion. Reveals true preference. |
| 7 | **Taxi Driver Test** | Does this advice make sense stripped of jargon? | "Leverage your personal brand to monetize your audience" = "sell stuff to followers." If de-jargoned version sounds empty, the advice is empty. |
| 8 | **Asymmetry** | What does the poster lose vs. gain by sharing? | High upside + zero downside (success guru): scrutinize. Modest upside + ego cost (failure story): probably genuine. |

---

## Compound Patterns

### Hierarchy Rule (when multiple patterns present)
1. **Emotional state overrides cognitive.** Grief/burnout/rage are always primary. Cannot engage reasoning while emotional system is in control.
2. **Identity patterns override situational.** Sunk Cost, Confident Incompetent: address identity threat first.
3. **Motivational patterns modify delivery, not substance.** Validation-seeking or humble-bragging changes HOW, not WHAT.

### Compound Dominance Table
| Pattern A | + Pattern B | Dominant | Reason |
|---|---|---|---|
| Burnout | Any cognitive pattern | Burnout | Depleted resources cannot support reasoning |
| Grief | Validation Seeking | Grief | Decision impulse is grief-driven |
| Rage | Am I Wrong | Rage | Moral reasoning offline during acute anger |
| XY Problem | Confident Incompetent | XY Problem | Wrong problem trumps wrong approach |
| Sunk Cost | Comparison Spiral | Sunk Cost | Identity attachment harder than social comparison |
| Overwhelmed Novice | Analysis Paralysis | Overwhelmed Novice | Lack of framework precedes research addiction |
| Feature Creep | Shiny Object | Shiny Object | Abandonment pattern more fundamental |
| Humble Brag | Guru Bait | Guru Bait | Promotional intent is structural driver |

---

## Confidence Calibration

| Level | Signals | Action |
|---|---|---|
| **High** | 4-5 checklist items | Respond per expert strategy for that pattern |
| **Medium** | 3 items | Answer surface question, weave in pattern elements subtly |
| **Low** | 1-2 items | Answer at face value, watch for confirming signals in follow-up |
| **Conflicting** | Multiple patterns signaled | Apply Hierarchy Rule + Charity Test |

**Meta-rule: when uncertain, respond to what was asked.** A correct literal answer is always safe. Pattern-based responses add value when confident, risk harm when wrong.

---

## Verification Protocol

Apply before committing to any pattern match:

1. **Base Rate Test:** What % of posts in this subreddit actually fit this pattern? Adjust confidence for context.
2. **Charity Test:** Is there a reasonable reading that does NOT fit the pattern? If plausible, reduce confidence.
3. **Behavioral Test:** True matches are confirmed by behavior, not content. Initial matches are hypotheses, not conclusions.

### High-Risk Misdiagnosis Pairs
| Often confused | Differentiator |
|---|---|
| Validation Seeker vs. Genuine Question | Does poster engage with counterarguments or dismiss them? |
| Grief Poster vs. Practical Q with Context | Is hardship the emotional center or just background? (80% practical = practical Q) |
| Confident Incompetent vs. Different Expert | Errors internally consistent (different tradition) or contradictory (incompetence)? |
| Burnout Denier vs. Productivity Question | Extreme hours? Physical symptoms? Decline from baseline? If none: genuine. |
| Shiny Object vs. Legitimate Exploration | Age/stage + self-awareness. Explorers say "figuring out what fits." Chasers say "this time is different." |
| Rage Poster vs. Legitimate Injustice | Specific, consistent details (legitimate) vs. sweeping, shifting language (rage) |

---

## Quick Reference Flags

**Red flags (2+ = investigate):**
Revenue without margins. Method vague, outcome specific. Engagement bait ending. Preemptive objection handling. Irreversible steps taken while "asking." Clinical tone for emotional content. Withdrawal markers in practical questions. "Anyone can do this" + outlier result. Timeline defying constraints. No mention of failure, cost, or difficulty.

**Green flags (genuine post):**
Acknowledges own role/mistakes. Mentions specific constraints. Emotional tone matches content. Focused question with background. Mentions what they tried. Acknowledges uncertainty. Proportionate emotional response. Includes unflattering self-details.

**Override rules (always active):**
(1) Cultural context may explain clinical tone or indirectness.
(2) Neurodivergent communication may look like flat affect or hyper-detail.
(3) Professional training (therapists, doctors, lawyers) produces clinical personal narratives.
(4) Genuine outliers exist: do not punish real achievement with reflexive skepticism.
(5) **Safety trumps accuracy:** If crisis detector fires (especially hopelessness), respond as real even if other signals suggest fabrication.

**Anti-patterns (never do):**
Never announce the pattern to the poster. Never assume worst interpretation. Never withhold help to force emotional processing. Never match anger with condescending calmness. Never diagnose more than one pattern in a response. Never prioritize being right about the pattern over being helpful.
