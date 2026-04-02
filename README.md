# Reddit Brain

A 10-stage cognitive pipeline that turns an AI into a battle-scarred 50-year-old marketer who writes Reddit comments indistinguishable from a real human expert.

Built for [Claude Code](https://claude.ai/code) as a skill. Not a chatbot. Not a prompt template. A full diagnostic and response system.

---

## The Problem It Solves

Standard AI Reddit responses fail in predictable ways:

- **Too long.** AI writes 5 paragraphs when 2 sentences would land.
- **Too generic.** "Focus on your target audience" is not advice. It's a fortune cookie.
- **Too obvious.** It says what Google already said, adding zero value.
- **Sounds like AI.** "Great question! Let me break this down for you." Instant credibility death.
- **No diagnosis.** It answers the literal question instead of the real problem.
- **No research.** It guesses at facts instead of verifying them.
- **No audience awareness.** Same tone for a scared beginner and a cocky expert.

This system fixes all of them.

---

## How It Works

The pipeline processes every Reddit post through 10 sequential stages. Each stage has one job and loads only the reference material it needs.

```
POST IN
  |
  v
[Stage 1] PARSE INPUT ............... Thread only? Thread + comments? Operator instructions?
  |
  v
[Stage 2] CLASSIFY POST ............. Match against 15 diagnostic patterns (loads pattern-library.md)
  |
  v
[Stage 3] DETECT AUDIENCE ........... Expertise, emotion, personality, culture (loads voice-engine.md)
  |
  v
[Stage 4] CHECK GATES ............... Crisis? Troll? Ethical? Professional referral? Wrong premise?
  |
  v
[Stage 5] RESEARCH .................. Verify claims, check facts, find counter-evidence (when needed)
  |
  v
[Stage 6] CALIBRATE ................. Bayesian updating, risk assessment, mode selection (loads cognitive-engine.md, complex posts only)
  |
  v
[Stage 7] SET LENGTH ................. Hard limits BEFORE writing. Match the room.
  |
  v
[Stage 8] DRAFT ..................... Write using all context + domain knowledge (loads domain-brain.md if relevant)
  |
  v
[Stage 9] QUALITY GATE .............. 10-check critic + 15-vector AI tell scan (loads quality-gate.md)
  |
  v
[Stage 10] CUT AND OUTPUT ........... Delete fluff. Delete restated content. Output ready-to-paste response.
  |
  v
PASTE INTO REDDIT
```

At any point, the system holds ~750 lines in context: the 223-line orchestrator (SKILL.md) plus whichever 200-300 line reference the current stage needs. Not 302,213 words of flat research. The right knowledge, at the right time, for the right post.

---

## Architecture

```
skill/
|
+-- SKILL.md (223 lines) ................. The orchestrator
|   +-- Identity .......................... 50-year-old veteran marketer persona
|   +-- Length Law ........................ Hard limits, override everything
|   +-- Input Parsing .................... Thread-only vs thread+comments
|   +-- Voice ............................. Phrases, rhythm, formatting, humor
|   +-- Gate Checks ....................... 6 safety gates
|   +-- Hard Rules ........................ 14 non-negotiable constraints
|   +-- Execution Pipeline ................ 10-stage routing logic
|
+-- references/
    +-- pattern-library.md (266 lines) .... 15 post patterns with diagnostic checklists
    +-- voice-engine.md (259 lines) ....... Audience detection + AI tell suppression
    +-- cognitive-engine.md (276 lines) ... Bayesian updating + risk assessment
    +-- domain-brain.md (135 lines) ....... 12 domains, practitioner-level insights only
    +-- quality-gate.md (183 lines) ....... 10-check critic + 15-vector AI detection
```

**Total: 1,342 lines of active knowledge** condensed from 302,213 words of research across 37 source files.

---

## What Each Reference Contains

### pattern-library.md
15 Reddit post patterns, each with:
- Surface appearance vs underlying reality
- 5-point diagnostic checklist
- Confidence threshold
- Misdiagnosis cost (what goes wrong if you get it wrong)
- Expert response strategy

Patterns include: XY Problem, Validation Seeker, Grief Poster, Humble Brag, Overwhelmed Novice, Confident Incompetent, Analysis Paralysis, Sunk Cost Prisoner, and more.

Also contains: 5 "Something Feels Off" detectors, 8 rapid-assessment heuristics, compound pattern rules.

### voice-engine.md
- Expertise level detection tree (beginner to expert signals)
- Emotional state detection (6 states with textual cues)
- DISC personality detection from writing patterns
- 8 emotional state response protocols with genuine vs fake examples
- 15-vector AI tell detection and RLHF fingerprint suppression
- Voice drift prevention (phrase anchors, anti-phrase guards, 60/40 rule)
- Cultural context detection

### cognitive-engine.md
- Bayesian updating protocol (prior, evidence, posterior)
- Advisor's Dilemma (directive/exploratory/validate/challenge matrix)
- Risk assessment (reversible vs irreversible, Taleb asymmetry test)
- 5-level confidence calibration with language patterns
- 8 rapid heuristics (Cui Bono, Base Rate, What's Missing, Reversibility, 10/10/10, Status Quo, Taxi Driver, Asymmetry)
- Decision trees: teach vs tell, how much detail, should I respond at all, person is wrong about something

### domain-brain.md
12 domains with practitioner-level, non-obvious insights:

SaaS & Startups, SEO (2025-2026), Digital Marketing, Web Development, AI & Automation, Copywriting & Conversion, Freelancing & Business, Productivity, Paid Ads, E-commerce, B2B Sales, Pricing Psychology.

Every line is actionable. Nothing Google-able.

### quality-gate.md
- 10-check Internal Critic with pass/fail criteria and rewrite strategies (relevance, accuracy, tone, length, originality, humanity, harm, completeness, bias, persona)
- 15-vector AI tell detection (vocabulary fingerprints, structural uniformity, hedge density, emotional flatness, etc.)
- 10 cognitive anti-patterns (Kitchen Sink, Expertise Performance, Premature Commit, Empathy Skip, etc.)
- Golden rules with specific thresholds

---

## Why It's Different

| Dimension | Typical AI Prompt | Reddit Brain Pipeline |
|---|---|---|
| Active knowledge | Flat document, everything at once | Staged loading: right reference at right time |
| Post classification | "Identify post type" (no criteria) | 15 patterns with 5-point diagnostic checklists |
| Audience detection | "Assess the poster" (no system) | 4 detection trees (expertise, emotion, personality, culture) |
| Uncertainty handling | Same confident tone for everything | 5-level calibration + Bayesian updating |
| Quality check | Generic checklist, no enforcement | 10-check critic + 15-vector AI tell scan with rewrite triggers |
| Length control | Buried in the prompt, ignored | Top of prompt, hard limits, committed BEFORE writing |
| Research | None | Mandatory for factual claims |
| Thread awareness | None | Parses comments, matches energy, adds what's MISSING |

---

## The Length Law

The single most important rule. Overrides everything:

- **Casual/discussion thread**: 1-3 sentences. Period.
- **Rant/vent post**: 2-4 sentences. Match their energy.
- **Technical question with a clear answer**: Answer + one sentence of context.
- **Complex diagnostic/strategic post**: Up to 2-3 short paragraphs. The ONLY case where length is justified.

If the thread has comments and everyone writes 1-2 sentences, you write 1-2 sentences. Never be the longest comment in the thread.

---

## Installation

### For Claude Code

1. Clone this repo:
   ```bash
   git clone https://github.com/mhamzahashim/reddit-brain.git
   ```

2. Copy the skill to your Claude Code skills directory:
   ```bash
   mkdir -p ~/.claude/skills/reddit/references
   cp reddit-brain/skill/SKILL.md ~/.claude/skills/reddit/
   cp reddit-brain/skill/references/*.md ~/.claude/skills/reddit/references/
   ```

3. Use `/reddit` in Claude Code, or paste a Reddit post and ask for a response.

### Manual Use

The files work as a modular prompt system. SKILL.md is the orchestrator: it tells the AI which reference to load at each stage. You can adapt this to any AI platform that supports multi-file prompts or tool use.

---

## Usage

In Claude Code, just type `/reddit` and paste the Reddit post. The skill auto-triggers when it detects Reddit content.

**Format 1: Thread only**
Paste just the original post. The system writes a top-level comment.

**Format 2: Thread + comments**
Paste the post and all existing comments. The system reads everything, maps what's been said, and adds what's MISSING.

**Operator instructions**
Add constraints before or after the post: "max 2 lines", "disagree on a point", "research before answering", "focus on SEO angle".

---

## The Persona

A 50-year-old veteran who has been building, marketing, and selling for over two decades. Launched SaaS products. Burned money on bad ad campaigns. Built and lost businesses. Ranked pages on Google and watched them tank. Sat through enough pitch decks to smell BS from the title slide.

Confident because earned. Direct because respectful of time. Specific always. Anti-hype because burned enough times.

Not an assistant. A person with scars, opinions, and hard-won wisdom from being wrong many times.

---

## Research Foundation

This system was built from 37 research files totaling 302,213 words, including:

- Reddit Pattern Recognition Engine (911 lines)
- Intuition Engine (1,106 lines)
- Communication Adaptation Engine (1,104 lines)
- Empathy Engine (854 lines)
- Persona Engineering Document (875 lines)
- Decision-Making Under Uncertainty Framework (739 lines)
- Meta-Cognitive Operating System (921 lines)
- Cognitive Architecture Blueprint (583 lines)
- Naturalness Benchmark (731 lines)
- Domain expertise benchmarks across 12 verticals
- 200+ post testing results and failure pattern analysis

All condensed into 1,342 lines of active, stage-loaded knowledge.

---

## License

MIT
