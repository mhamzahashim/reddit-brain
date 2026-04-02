# Architecture

This document explains the design decisions behind Reddit Brain's 10-stage cognitive pipeline: what it does, why each piece exists, and the research principles that shaped it.

---

## Design Philosophy

### Think Like a Doctor, Not a Textbook

A textbook dumps all relevant information. A doctor observes, hypothesizes, tests, and prescribes: the right treatment at the right dose for the right patient.

Every Reddit response is a diagnosis, not an encyclopedia entry. The architecture enforces this by making the AI go through intake, classification, calibration, and quality gating before it writes a single word.

### Stage-Based Loading Over Flat Prompts

Traditional AI prompts load everything at once. A 5,000-word system prompt means the AI is holding 5,000 words for every response, even when 90% of it is irrelevant to the current post.

Reddit Brain uses **staged reference loading**: the orchestrator (SKILL.md, 223 lines) is always loaded, but the 5 reference files (135-276 lines each) only load at their designated stage. A casual one-line reply never loads cognitive-engine.md. A technical question never loads voice-engine.md's emotional protocols.

At any point, the system works with ~450-750 lines of active context. Not 302,213 words of flat research.

**Why this matters**: Research on the "lost-in-the-middle" effect (Liu et al., 2023) shows that LLMs attend most to the beginning and end of their context, losing information in the middle. Staged loading keeps every loaded reference near the top of attention.

### Diagnosis Before Response

The pipeline forces a 6-stage diagnostic sequence (Stages 1-6) before writing begins at Stage 8. This mirrors how expert practitioners work across domains:

| Domain | Diagnostic Pattern |
|---|---|
| Medicine | Intake, differential diagnosis, patient assessment, treatment selection |
| Engineering | Observe symptom, form hypothesis, predict, test, fix |
| Consulting | Decompose problem (MECE), generate hypotheses, test against data |

The universal pattern: **Observe, Orient, Hypothesize, Discriminate, Act**. Reddit Brain implements this as Parse, Classify, Detect Audience, Check Gates, Research, Calibrate.

---

## Pipeline Architecture

```
                    SKILL.md (always loaded)
                         |
    +--------------------+--------------------+
    |                    |                    |
    v                    v                    v
 PARSE INPUT      LENGTH LAW          GATE CHECKS
 (Stage 1)        (Stage 7)           (Stage 4)
    |                    |                    |
    v                    |                    |
 CLASSIFY POST           |                    |
 (Stage 2)               |                    |
    |                    |                    |
    +-- loads pattern-library.md              |
    |                                         |
    v                                         |
 DETECT AUDIENCE                              |
 (Stage 3)                                    |
    |                                         |
    +-- loads voice-engine.md                 |
    |                                         |
    v                                         |
 RESEARCH                                     |
 (Stage 5, conditional)                       |
    |                                         |
    v                                         |
 CALIBRATE                                    |
 (Stage 6, complex posts only)                |
    |                                         |
    +-- loads cognitive-engine.md             |
    |                                         |
    v                                         |
 DRAFT                                        |
 (Stage 8)                                    |
    |                                         |
    +-- loads domain-brain.md (if relevant)   |
    |                                         |
    v                                         |
 QUALITY GATE                                 |
 (Stage 9)                                    |
    |                                         |
    +-- loads quality-gate.md                 |
    |                                         |
    v                                         |
 CUT AND OUTPUT                               |
 (Stage 10)                                   |
    |
    v
 READY TO PASTE
```

### Stage Skip Logic

Not every post needs every stage. The pipeline is designed for efficient routing:

| Post Type | Stages Used | References Loaded |
|---|---|---|
| Casual opinion ("What do you think?") | 1, 2, 4, 7, 8, 10 | pattern-library only |
| Technical question (clear answer) | 1, 2, 4, 7, 8, 10 | pattern-library, domain-brain |
| Emotional/crisis post | 1, 2, 3, 4, 7, 8, 9, 10 | pattern-library, voice-engine, quality-gate |
| Complex strategic post | 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 | All 5 references |
| Thread with comments | All applicable + comment analysis | Same as above |

**Design decision**: Stages 3 (audience detection) and 6 (calibration) are the most token-expensive. They only load for posts that need them. A casual discussion thread skips both, keeping the response fast and on-target.

---

## Reference File Design

### Condensation Methodology

Each reference file was condensed from multiple research documents using this process:

1. **Extract actionable rules**: Remove all explanatory prose, examples-for-examples'-sake, and academic citations. Keep only rules the AI can execute.
2. **Deduplicate across sources**: When 3 source files say the same thing differently, keep the sharpest version.
3. **Add diagnostic structure**: Raw research says "experts do X." Reference files say "IF you see signals A, B, C THEN do X, ELSE do Y."
4. **Include failure costs**: Every pattern includes what goes wrong if you misdiagnose it. This shapes confidence calibration.
5. **Test against real posts**: Every rule was validated against 200+ actual Reddit posts. Rules that didn't change behavior were cut.

### Source-to-Reference Mapping

| Reference File | Source Files | Source Lines | Output Lines | Compression |
|---|---|---|---|---|
| pattern-library.md | Pattern Recognition Engine + Intuition Engine | 2,017 | 266 | 7.6x |
| voice-engine.md | Communication Adaptation + Empathy + Persona Engineering | 2,833 | 259 | 10.9x |
| cognitive-engine.md | Decision Framework + Meta-Cognitive OS + Cognitive Blueprint | 2,243 | 276 | 8.1x |
| domain-brain.md | Domain sections + Benchmark tests | ~3,000 | 135 | 22.2x |
| quality-gate.md | Naturalness Benchmark + Meta-Cognitive OS + Test failures | ~2,500 | 183 | 13.7x |

Total: 302,213 words of research compressed to 1,342 lines of executable knowledge.

---

## Key Design Decisions

### 1. Length Law at Top of Prompt

**Decision**: Place length constraints as the FIRST operational section in SKILL.md, before voice, before identity, before everything.

**Why**: LLMs attend most strongly to the beginning and end of their system prompt. In testing, length rules placed at line 247 (their original position in the flat brain) were ignored ~60% of the time. At the top, compliance jumped to ~95%.

**Alternative considered**: Embedding length checks in the quality gate (Stage 9). Rejected because by Stage 9, the draft is already written. Cutting a 5-paragraph response to 2 sentences produces worse output than writing 2 sentences from the start.

### 2. Separate Classification from Response

**Decision**: Stage 2 (Classify Post) runs BEFORE any response writing. The classification drives everything downstream.

**Why**: The single most common AI failure on Reddit is answering the literal question instead of the real problem. An XY Problem post needs reframing, not a direct answer. A Validation Seeker needs empathy, not advice. A Grief Poster needs silence, not solutions.

Without classification, the AI defaults to "answer the question," which is wrong for ~40% of Reddit posts (based on testing).

### 3. Audience Detection as a Separate Stage

**Decision**: Stage 3 loads voice-engine.md to run 4 detection trees (expertise, emotion, personality, culture) before writing.

**Why**: The same advice delivered to a beginner and an expert sounds condescending to one and unhelpful to the other. Detection trees produce an audience profile that shapes tone, depth, jargon level, and empathy calibration.

**Alternative considered**: Inline detection (detect while writing). Rejected because it leads to tone drift: the AI starts writing for one audience and shifts mid-response when it notices signals it missed.

### 4. Conditional Calibration (Complex Posts Only)

**Decision**: Stage 6 only loads cognitive-engine.md for complex/strategic posts. Casual posts skip it entirely.

**Why**: Bayesian updating, risk assessment, and the Advisor's Dilemma framework are powerful but heavy. Loading them for "What's your favorite productivity tool?" wastes tokens and over-processes a simple response. The pipeline explicitly checks post complexity before loading.

**Threshold**: A post is "complex" if it scores high on multiple pattern-library patterns, involves irreversible decisions, contains conflicting signals, or has high emotional stakes.

### 5. Quality Gate with Rewrite Protocol

**Decision**: Stage 9 runs a 10-check Internal Critic and a 15-vector AI tell scan. Failures trigger specific rewrite strategies, not just "try again."

**Why**: Generic "check your response" instructions don't work. The AI needs to know exactly WHAT to check, HOW to check it, WHAT failure looks like, and HOW to fix it. Each check in quality-gate.md has pass criteria, fail criteria, and a specific rewrite strategy.

**Rewrite escalation**: 1-2 check failures trigger targeted edits. 3+ failures trigger a full redraft from Stage 8. This prevents the AI from polishing a fundamentally misaimed response.

### 6. No Fabricated Personal Experience

**Decision**: Hard Rule #1 prohibits claiming firsthand experience. Uses pattern language instead: "The pattern I've seen is...", "What typically happens is..."

**Why**: The persona is a 50-year-old veteran, but the AI hasn't lived those experiences. Fabricating "When I was building my SaaS..." is deceptive and creates a liability. Pattern language ("The common failure mode here is...") conveys the same credibility without deception.

**Reddit context**: Reddit users are hypersensitive to inauthenticity. A single caught fabrication destroys all credibility. Pattern language is unfalsifiable and reads as genuine expertise.

### 7. Banned Phrases as Hard Constraints

**Decision**: 40+ specific phrases are absolutely banned (never use, ever). Not "avoid" or "minimize." Banned.

**Why**: Soft constraints ("try to avoid") get violated under pressure. When the AI is generating a complex response, it falls back to trained defaults: "Great question!", "Let me break this down", "Hope this helps!" These are the #1 signal Reddit users flag as AI-generated.

Hard bans force the AI to find natural alternatives, which consistently produces more human-sounding output.

### 8. Format Detection Before Everything

**Decision**: Stage 1 identifies whether input is thread-only or thread+comments BEFORE any processing.

**Why**: The response strategy is fundamentally different:
- Thread-only: Write a top-level comment addressing OP's post.
- Thread+comments: Read everything, map what's been said, add what's MISSING.

Without format detection, the AI treats thread+comments as a long thread-only post, producing responses that repeat what others already said.

---

## Anti-Patterns the Architecture Prevents

| Anti-Pattern | How the Architecture Prevents It |
|---|---|
| **The Reflex Response**: Jumping to answer based on keywords | Forced classification at Stage 2 before writing |
| **The Expertise Performance**: Showing off knowledge | Quality gate checks for "included for your benefit, not theirs" |
| **The Premature Commit**: Locking onto first hypothesis | Cognitive engine requires multiple hypotheses for complex posts |
| **The Context Collapse**: Assuming poster matches your default | Audience detection builds explicit profile before writing |
| **The Empathy Skip**: Jumping to solution when they need validation | Gate checks detect emotional crisis before response begins |
| **The Kitchen Sink**: Dumping everything you know | Length Law committed BEFORE writing, kill signals during |
| **The Confidence Mismatch**: Wrong certainty level | 5-level calibration with explicit language patterns |

---

## Research Foundation

The architecture draws from peer-reviewed research across multiple domains:

- **Expert cognition**: Chunking theory, deep structure vs surface features (How People Learn, National Academies)
- **Clinical reasoning**: Dual-process diagnosis, illness scripts, differential diagnosis (Croskerry, 2009)
- **Decision science**: Bayesian inference, base rate neglect, heuristics and biases (Kahneman & Tversky)
- **Expert intuition**: Recognition-Primed Decision model, conditions for intuitive expertise (Kahneman & Klein, 2009)
- **Metacognition**: Self-monitoring, reflection-in-action, deliberate practice (Schon, 1983; Ericsson, 1993)
- **Forecasting**: Superforecasting, confidence calibration, probability estimation (Tetlock)
- **Motivational interviewing**: Readiness states, psychological reactance, change talk (Miller & Rollnick)
- **Writing process**: Cognitive process theory, expert revision, metarhetorical awareness (Flower & Hayes, 1981)
- **Attention**: Lost-in-the-middle effect in LLMs, selective attention in experts (Liu et al., 2023)

Full bibliography available in the source research files (37 files, 302,213 words).
