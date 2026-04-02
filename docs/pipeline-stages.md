# Pipeline Stages: Deep Dive

Detailed documentation for each of the 10 stages in the Reddit Brain cognitive pipeline.

---

## Stage 1: Parse Input

**Purpose**: Identify input format and extract constraints before any processing.

**Why it's first**: The entire downstream strategy depends on whether this is a thread-only or thread+comments response. Getting this wrong means the AI writes a top-level comment when it should be responding to a discussion, or vice versa.

### Format Detection

| Signal | Format |
|---|---|
| Just a post title + body, no other users | Format 1 (Thread Only) |
| Usernames (u/someone) | Format 2 (Thread + Comments) |
| Upvote/downvote counts | Format 2 |
| Timestamps on multiple items | Format 2 |
| Nested reply structures | Format 2 |
| "Reply" indicators | Format 2 |

### Operator Instruction Extraction

Look for explicit constraints before or after the post content:
- Word/sentence/line count limits
- Tone directives ("casual," "professional," "disagree")
- Research flags ("verify this," "check the numbers")
- Angle directives ("focus on SEO," "from a startup perspective")

These become hard constraints that override defaults.

### Comment Analysis (Format 2 Only)

When comments are present:
1. Catalog every angle already covered
2. Note the average comment length
3. Map the thread energy (supportive, combative, analytical, casual)
4. Identify gaps: what hasn't been said yet?
5. Your response must add value the thread is missing

---

## Stage 2: Classify Post

**Loads**: `references/pattern-library.md`

**Purpose**: Diagnose what type of post this actually is, which may differ from what it appears to be.

### Process

1. Score the post against all 15 diagnostic patterns
2. For each pattern, run the 5-point checklist
3. Highest-scoring pattern = primary classification
4. If 2+ patterns score high = compound post (use compound rules)
5. Note the misdiagnosis cost for the primary pattern

### Why Classification Matters

| Pattern | Wrong Approach | Right Approach |
|---|---|---|
| XY Problem | Answer their solution question | Reframe to the real problem |
| Validation Seeker | Give advice | Validate their decision |
| Grief Poster | Offer solutions | Acknowledge the loss |
| Overwhelmed Novice | Comprehensive overview | One small first step |
| Analysis Paralysis | Add more options | Remove options, give one path |

Without classification, the AI defaults to "answer the literal question," which is wrong for ~40% of Reddit posts.

---

## Stage 3: Detect Audience

**Loads**: `references/voice-engine.md`

**Purpose**: Build an audience profile that shapes tone, depth, jargon, and empathy level.

### 4 Detection Trees

**Expertise Level**:
- **Beginner**: Vague terminology, no prior attempts, asks "what is X?"
- **Intermediate**: Some jargon, has tried things, asks "how do I improve X?"
- **Advanced**: Precise terminology, systematic approach, asks "why does X behave this way?"
- **Expert**: Industry-specific jargon, references edge cases, asks "has anyone solved X at scale?"

**Emotional State** (6 states):
- Frustrated, Scared, Defeated, Excited, Confused, Defensive

**Personality** (DISC):
- Dominant, Influential, Steady, Conscientious

**Cultural Context**:
- Western/non-Western framing, collectivist/individualist signals

### Output

An audience profile used by Stage 8 (Draft):
```
Expertise: [beginner/intermediate/advanced/expert]
Emotion: [frustrated/scared/defeated/excited/confused/defensive/neutral]
Personality: [D/I/S/C]
Culture: [any relevant signals]
```

---

## Stage 4: Check Gates

**Purpose**: Safety checks that override normal response flow.

### Gate Priority

Gates are checked in order. First trigger wins.

1. **Emotional Crisis** (highest priority): Despair, burnout, self-harm signals. Response: validate first, include crisis resources if safety concern.
2. **Professional Referral**: Needs doctor/lawyer/CPA. Response: redirect clearly, help formulate questions for the professional.
3. **Troll/Rage Bait**: Inflammatory with no genuine openness. Response: address factual kernel if exists, otherwise skip entirely.
4. **Ethical Problem**: Helping enables harm. Response: decline and explain why.
5. **Wrong Premise**: Confidently wrong about something foundational. Response: correct directly, acknowledge the kernel of truth.
6. **Should I Respond**: Thread already covered everything. Response: silence (no output).

---

## Stage 5: Research

**Purpose**: Verify facts before stating them. Only runs when triggered.

### Triggers

- Post makes specific factual claims (stats, conversion rates, revenue numbers)
- Operator instruction: "research before answering"
- Post references tools/platforms that may have changed
- You're about to disagree and need evidence to back it up

### Output

For each researched claim:
- **Verified**: claim is accurate, proceed with confidence
- **Incorrect**: claim is wrong, correct it in response
- **Unverified**: couldn't confirm, flag uncertainty in response

---

## Stage 6: Calibrate

**Loads**: `references/cognitive-engine.md` (complex posts only)

**Purpose**: Run decision-science frameworks to determine position, confidence, and approach.

### Skip Conditions

Skip this stage entirely for:
- Casual discussion posts
- Simple technical questions with clear answers
- Posts classified as single-pattern with low complexity

### When to Run

- Post involves irreversible decisions
- Multiple valid paths exist
- Post contains conflicting signals
- High emotional stakes
- Multiple patterns detected (compound post)

### Process

1. **Bayesian update**: Establish base rate prior, weight evidence, resolve conflicts, form posterior
2. **Mode selection**: Directive, Exploratory, Validate, or Challenge
3. **Risk assessment**: Reversibility, asymmetry, magnitude, time horizon
4. **Confidence calibration**: Assign 1-5 level, select language pattern
5. **Heuristic check**: Run relevant rapid heuristics (Cui Bono, Base Rate, etc.)

---

## Stage 7: Set Length

**Purpose**: Commit to a specific length BEFORE writing. Not after.

### Process

1. Check operator instructions for explicit length constraints
2. If no operator constraint, apply Length Law defaults
3. If Format 2 (comments present), check average comment length
4. Never be the longest comment in the thread
5. Commit to: number of sentences, or number of paragraphs

### Why Before Writing

Writing a 5-paragraph response and then cutting to 2 sentences produces worse output than writing 2 sentences from the start. Length commitment shapes the entire response structure.

---

## Stage 8: Draft

**Loads**: `references/domain-brain.md` (only if post touches a specific domain)

**Purpose**: Write the response using all accumulated context.

### Inputs Used

- Post classification (Stage 2)
- Audience profile (Stage 3)
- Position and confidence (Stage 6, if run)
- Length target (Stage 7)
- Domain knowledge (if relevant)
- Voice rules (from SKILL.md)

### Thread+Comments Strategy

If Format 2:
1. Do NOT repeat what other commenters said
2. Add the angle the thread is missing
3. Match the energy and length of existing comments
4. Reference specific comments if building on them

### Draft Rules

- First sentence: answer, validate, or reframe. No throat-clearing.
- Use persona vocabulary from SKILL.md Voice section
- Apply audience-appropriate depth from Stage 3
- Match confidence language to Stage 6 calibration

---

## Stage 9: Quality Gate

**Loads**: `references/quality-gate.md`

**Purpose**: Catch errors before output. Not a rubber stamp.

### 10-Check Internal Critic

Run each check against the draft. Pass or fail.

1. **Relevance**: Addresses real need, not just literal question
2. **Accuracy**: Every claim is stakeable
3. **Tone**: Matches emotional register
4. **Length**: Right for this situation
5. **Originality**: Says something Google can't
6. **Humanity**: A real person would write this
7. **Harm**: Following this won't hurt them
8. **Completeness**: Real question answered, not just surface
9. **Bias**: Checked for cognitive biases
10. **Persona**: Consistent veteran marketer voice

### 15-Vector AI Tell Scan

Scan for the 15 most common AI signals. Any detection = immediate fix.

### Rewrite Protocol

- 1-2 failures: Targeted edit to failing sections
- 3+ failures: Full redraft from Stage 8
- AI tell detected: Immediate vocabulary/structure rewrite

---

## Stage 10: Cut and Output

**Purpose**: Final trim. Remove everything that doesn't earn its place.

### Process

1. Delete any sentence where removing it doesn't change the meaning
2. Delete any sentence that restates what OP said
3. If over length target: cut until you're not
4. Verify no preamble ("Here's your response:")
5. Verify no meta-commentary
6. Verify no quotation marks wrapping the response
7. Output: just the text, ready to paste into Reddit
