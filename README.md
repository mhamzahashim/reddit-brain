# Reddit Brain

Persistent cognitive pipeline for writing Reddit comments that are indistinguishable from a real human expert. Built as a [Claude Code](https://claude.ai/code) skill.

Not a chatbot. Not a prompt template. A 10-stage diagnostic system that classifies posts, detects audiences, calibrates confidence, checks for AI tells, and outputs ready-to-paste responses.

---

## Quick Start

```bash
# Clone
git clone https://github.com/mhamzahashim/reddit-brain.git

# Install to Claude Code
mkdir -p ~/.claude/skills/reddit/references
cp reddit-brain/skill/SKILL.md ~/.claude/skills/reddit/
cp reddit-brain/skill/references/*.md ~/.claude/skills/reddit/references/

# Use
# Type /reddit in Claude Code, paste a Reddit post
```

---

## How It Works

```
Reddit Post → PARSE → CLASSIFY → DETECT AUDIENCE → GATE CHECK → RESEARCH
                                                                    ↓
                         Ready-to-Paste ← CUT ← QUALITY GATE ← DRAFT ← CALIBRATE
```

Each stage has one job. Each reference file loads only when its stage runs. At any point, the system holds ~750 lines of active context: not 302,213 words of flat research.

| Stage | Job | Reference Loaded |
|---|---|---|
| 1. Parse Input | Format 1 (thread) or Format 2 (thread+comments)? | None |
| 2. Classify Post | Match against 15 diagnostic patterns | `pattern-library.md` |
| 3. Detect Audience | Expertise, emotion, personality, culture | `voice-engine.md` |
| 4. Check Gates | Crisis? Troll? Ethical? Wrong premise? | None |
| 5. Research | Verify facts, find counter-evidence | None (uses web tools) |
| 6. Calibrate | Bayesian updating, risk, confidence (complex only) | `cognitive-engine.md` |
| 7. Set Length | Hard limits BEFORE writing | None |
| 8. Draft | Write using all accumulated context | `domain-brain.md` (if relevant) |
| 9. Quality Gate | 10-check critic + 15-vector AI tell scan | `quality-gate.md` |
| 10. Cut & Output | Remove fluff, output ready-to-paste | None |

For a casual 1-sentence reply: stages 1, 2, 4, 7, 8, 10 (~7.7K tokens).
For a complex strategic post: all 10 stages (~11.8K tokens).

---

## Architecture

### Repository Structure

```
reddit-brain/
│
├── README.md ························ You are here
├── ARCHITECTURE.md ·················· Design decisions + pipeline deep dive
├── DOCS.md ·························· Full technical reference (all components)
├── CONTRIBUTING.md ·················· How to add patterns, domains, voice rules
├── CHANGELOG.md ····················· Version history
├── LICENSE ·························· MIT
│
├── skill/ ··························· The actual skill (install this)
│   ├── SKILL.md (303 lines) ········ Orchestrator + critical inlines
│   │   ├── Identity ················· 50-year-old veteran marketer persona
│   │   ├── Length Law ··············· Hard limits (overrides everything)
│   │   ├── Input Parsing ············ Thread-only vs thread+comments
│   │   ├── Voice ···················· Phrases, banned phrases, rhythm, humor
│   │   ├── Gate Checks ·············· 6 safety gates
│   │   ├── Hard Rules ··············· 14 non-negotiable constraints
│   │   ├── Execution Pipeline ······· 10-stage routing with reference loading
│   │   ├── Critical Patterns ········ Top 5 patterns (always loaded)
│   │   ├── Critical AI Tells ········ Top 5 tells (always loaded)
│   │   └── Golden Examples ·········· 4 annotated correct outputs
│   │
│   └── references/
│       ├── pattern-library.md (266)   15 patterns + diagnostic checklists
│       ├── voice-engine.md (227) ···· Audience detection + voice drift
│       ├── cognitive-engine.md (252)  Bayesian updating + risk assessment
│       ├── domain-brain.md (145) ···· 12 domains, practitioner insights
│       └── quality-gate.md (189) ···· 10-check critic + 15-vector AI scan
│
├── docs/
│   ├── installation.md ·············· Setup for Claude Code + other platforms
│   ├── pipeline-stages.md ··········· Deep dive into all 10 stages
│   ├── customization.md ············· Change persona, add domains/patterns
│   └── design-decisions.md ·········· 14 decisions with evidence + tradeoffs
│
├── examples/
│   └── README.md ···················· 5 examples with full pipeline traces
│
└── .github/
    ├── ISSUE_TEMPLATE/
    │   ├── bug_report.md ············ Stage-specific bug reporting
    │   ├── feature_request.md ······· Component-tagged requests
    │   └── pattern_request.md ······· New pattern proposals
    ├── PULL_REQUEST_TEMPLATE.md ····· Testing table + checklist
    └── labels.yml ··················· Type, status, component, priority labels
```

### Skill File Breakdown

```
skill/
├── SKILL.md (303 lines) ·············· Orchestrator + critical inlines
└── references/
    ├── pattern-library.md (266 lines)  Stage 2: post classification
    ├── voice-engine.md (227 lines) ··· Stage 3: audience detection
    ├── cognitive-engine.md (252 lines)  Stage 6: calibration (complex only)
    ├── domain-brain.md (145 lines) ··· Stage 8: domain knowledge (if relevant)
    └── quality-gate.md (189 lines) ··· Stage 9: quality checks
```

**1,382 lines total.** Condensed from 37 research files (302,213 words). Zero duplication between files.

---

## The Problem It Solves

Standard AI Reddit responses fail in 7 predictable ways:

| Failure | Why It Happens | How Reddit Brain Fixes It |
|---|---|---|
| **Too long** | No length commitment before writing | Length Law at top of prompt, committed at Stage 7 |
| **Too generic** | No audience detection | 4 detection trees: expertise, emotion, personality, culture |
| **Too obvious** | No originality check | Quality gate Check E: "Can you Google this in 30 seconds?" |
| **Sounds like AI** | No tell detection | 15-vector AI scan + 40+ banned phrases |
| **Wrong diagnosis** | No classification | 15 patterns with 5-point diagnostic checklists |
| **No research** | No verification step | Stage 5 triggers for factual claims |
| **Ignores context** | No thread awareness | Format 2 parsing: reads all comments, adds what's missing |

---

## Reference Files

### pattern-library.md

15 post patterns, each with surface appearance, underlying reality, 5-point diagnostic checklist, confidence threshold, misdiagnosis cost, and expert response strategy.

**Patterns**: XY Problem, Validation Seeker, Grief Poster, Humble Brag, Overwhelmed Novice, Confident Incompetent, Analysis Paralysis, Sunk Cost Prisoner, Comparison Spiraler, Feature Creep Victim, Guru Bait, Rage Poster, Am I Wrong, Burnout Denier, Shiny Object Chaser.

Plus: 5 "Something Feels Off" detectors, 8 rapid heuristics, compound pattern rules.

### voice-engine.md

4 audience detection trees (expertise level, emotional state, DISC personality, cultural context). 8 emotional state response protocols with genuine vs fake empathy examples. Voice drift prevention with phrase anchors, anti-phrase guards, and the 60/40 rule. (AI tell detection lives in quality-gate.md to avoid duplication.)

### cognitive-engine.md

Loaded only for complex/strategic posts (explicit complexity test in SKILL.md). Bayesian updating (prior, evidence, posterior). Advisor's Dilemma: 4-mode matrix (directive/exploratory/validate/challenge). Risk assessment (Bezos Type 1/2, Taleb asymmetry). 5-level confidence calibration. 4 decision trees. Premortem check. Signal vs noise analysis. (Rapid heuristics live in pattern-library.md to avoid duplication.)

### domain-brain.md

12 domains with practitioner-level, non-obvious insights: SaaS, SEO (2025-2026), Digital Marketing, Web Dev, AI/Automation, Copywriting, Freelancing, Productivity, Paid Ads, E-commerce, B2B Sales, Pricing Psychology. Every line actionable. Nothing Google-able.

### quality-gate.md

10-check Internal Critic (relevance, accuracy, tone, length, originality, humanity, harm, completeness, bias, persona) with pass/fail criteria and specific rewrite strategies. 15-vector AI tell detection. 10 cognitive anti-patterns. Rewrite escalation: 1-2 failures = targeted edit, 3+ = full redraft.

---

## Usage

### Format 1: Thread Only

Paste just the original post. The system writes a top-level comment.

```
/reddit

r/Entrepreneur
Title: Is $5K enough to start a SaaS?
Body: I have $5K saved up and want to build a SaaS product...
```

### Format 2: Thread + Comments

Paste the post and all existing comments. The system reads everything, maps what's been said, and adds what's MISSING.

```
/reddit

r/SaaS
Title: My SaaS has been stuck at $3K MRR...
Body: ...
---
u/saas_veteran (142 upvotes): Have you talked to churned customers?
u/growthguy (89 upvotes): What's your pricing?
```

### Operator Instructions

Add constraints before or after the post:

| Instruction | Effect |
|---|---|
| `max 2 lines` | Hard length constraint |
| `disagree on a point` | Forces contrarian angle |
| `research before answering` | Forces Stage 5 |
| `focus on SEO angle` | Loads domain-brain, prioritizes SEO |
| `50 words` | Exact word count |

### Output

Always: just the response text, ready to paste. No preamble, no quotes, no meta-commentary.

---

## The Persona

A 50-year-old veteran who has been building, marketing, and selling for 20+ years. Launched SaaS products. Burned money on bad ad campaigns. Built and lost businesses. Ranked pages on Google and watched them tank. Sat through enough pitch decks to smell BS from the title slide.

**Vocabulary**: "Ship it." / "Run the numbers." / "I've seen this movie before." / "The boring answer is usually the right one."

**Banned vocabulary** (40+ phrases, absolute ban): "Great question!" / "Let me break this down" / "Hope this helps!" / "Leverage" / "Game-changer" / "Holistic" / "Delve" / "Navigate" / all corporate jargon.

---

## Comparison

| Dimension | Flat System Prompt | Reddit Brain |
|---|---|---|
| Context loaded | Everything, always (~5K words) | Staged: right reference at right time (~750 lines max) |
| Post classification | "Identify post type" (no criteria) | 15 patterns, 5-point checklists, misdiagnosis costs |
| Audience detection | "Assess the poster" (no system) | 4 trees: expertise, emotion, personality, culture |
| Uncertainty | Same confident tone for everything | 5-level calibration + Bayesian updating |
| Quality control | Generic checklist | 10-check critic + 15-vector AI tell scan + rewrite strategies |
| Length control | Rule buried at line 247, ignored ~60% | Top of prompt, hard limits, committed before writing |
| Research | None | Mandatory for factual claims |
| Thread awareness | None | Reads comments, matches energy, adds what's missing |
| Token cost (casual) | ~8K tokens (all loaded) | ~4.8K tokens (SKILL.md with critical inlines) |
| Token cost (complex) | ~8K tokens (all loaded) | ~12K tokens (targeted loading) |

---

## Documentation

| Document | Content |
|---|---|
| [ARCHITECTURE.md](ARCHITECTURE.md) | Design decisions, pipeline architecture, research foundation |
| [DOCS.md](DOCS.md) | Full technical reference for all components |
| [CONTRIBUTING.md](CONTRIBUTING.md) | How to add patterns, domains, voice rules |
| [CHANGELOG.md](CHANGELOG.md) | Version history |
| [docs/installation.md](docs/installation.md) | Detailed setup for Claude Code and other platforms |
| [docs/pipeline-stages.md](docs/pipeline-stages.md) | Deep dive into each of the 10 stages |
| [docs/customization.md](docs/customization.md) | How to change persona, add domains, adjust settings |
| [docs/design-decisions.md](docs/design-decisions.md) | Why every decision was made |
| [examples/](examples/) | Real input/output examples with pipeline traces |

---

## Research Foundation

Condensed from 37 files totaling 302,213 words:

| Source Document | Lines | Condensed Into |
|---|---|---|
| Reddit Pattern Recognition Engine | 911 | pattern-library.md |
| Intuition Engine | 1,106 | pattern-library.md |
| Communication Adaptation Engine | 1,104 | voice-engine.md |
| Empathy Engine | 854 | voice-engine.md |
| Persona Engineering Document | 875 | voice-engine.md |
| Decision-Making Under Uncertainty | 739 | cognitive-engine.md |
| Meta-Cognitive Operating System | 921 | cognitive-engine.md |
| Cognitive Architecture Blueprint | 583 | cognitive-engine.md |
| Naturalness Benchmark | 731 | quality-gate.md |
| Domain expertise benchmarks (12) | ~3,000 | domain-brain.md |
| 200+ post test results | ~2,000 | quality-gate.md |

Draws from peer-reviewed research in expert cognition, clinical reasoning, decision science, Bayesian inference, metacognition, motivational interviewing, and writing process theory. Full bibliography in [ARCHITECTURE.md](ARCHITECTURE.md#research-foundation).

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). All changes start with an issue. Patterns need 5+ real Reddit posts for validation. Voice changes need 10+ diverse post tests.

---

## License

[MIT](LICENSE)
