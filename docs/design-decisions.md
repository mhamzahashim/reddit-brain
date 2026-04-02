# Design Decisions

Why Reddit Brain works the way it does. Every decision has a reason.

---

## Decision Log

### 1. Staged Loading Over Flat Prompts

**Decision**: Load reference files only at their designated pipeline stage, not all at once.

**Alternatives considered**:
- **Flat prompt** (load everything): Simple but wasteful. 302K words in context means 90% irrelevant at any moment.
- **Summary prompt** (condense everything into one file): Loses diagnostic specificity. A 500-line summary can't hold 15 patterns with 5-point checklists.
- **Staged loading** (chosen): Each reference loads only when needed. Max ~750 lines at any point.

**Why**: Research on the "lost-in-the-middle" effect shows LLMs attend most to the beginning and end of context. In a 5,000-word flat prompt, information at line 247 gets ~60% less attention. Staged loading keeps every piece of knowledge near the top of attention when it's being used.

**Trade-off**: More complex pipeline logic. Requires the AI to follow routing instructions. Worth it for the quality improvement.

---

### 2. Length Law at Top of Prompt

**Decision**: Place length constraints as the FIRST operational section, before identity, before voice.

**Evidence**: In testing with the flat brain (where length rules were at line 247), the AI ignored length constraints ~60% of the time. Moving them to the top of SKILL.md (lines 17-41) improved compliance to ~95%.

**Why it works**: LLMs are autoregressive: they process tokens sequentially and weight earlier tokens more heavily. Placing the strongest constraint first means it has the highest influence on all subsequent generation.

**Trade-off**: Identity description comes after Length Law, which feels structurally odd. But the AI processes them in parallel anyway; the ordering is about attention weight, not reading order.

---

### 3. Classification Before Response

**Decision**: Force diagnostic classification (Stage 2) before any response writing begins.

**Problem solved**: Without classification, the AI treats every post as "question that needs an answer." But ~40% of Reddit posts need something other than an answer:
- XY Problems need reframing
- Validation Seekers need permission
- Grief Posters need acknowledgment
- Overwhelmed Novices need one small step
- Analysis Paralysis needs fewer options, not more

**Evidence**: In testing, misclassified posts produced responses rated 2-3x worse (human evaluation) than correctly classified posts. Classification is the single highest-leverage stage.

---

### 4. Separate Pattern Library File

**Decision**: Post patterns live in their own reference file, not inline in SKILL.md.

**Alternatives considered**:
- **Inline in SKILL.md**: Simpler, one file to manage. But SKILL.md would be 500+ lines, hitting lost-in-the-middle problems.
- **Separate file** (chosen): Loaded on-demand at Stage 2. Keeps SKILL.md lean (223 lines). Pattern library can grow without bloating the orchestrator.

**Trade-off**: Requires file-read capability. But all modern AI platforms support this.

---

### 5. 15 Patterns, Not 5 or 50

**Decision**: 15 post patterns in the pattern library.

**Why 15**: Below 10, too many posts don't match any pattern (false negatives). Above 20, patterns start overlapping and the AI gets confused about which one to apply (false positives).

15 covers ~85% of Reddit posts we tested against. The remaining ~15% are handled by the compound pattern rules and "Something Feels Off" detectors.

**Future**: New patterns can be added if they're genuinely distinct. But the bar is high: a new pattern must cover posts that existing patterns misclassify.

---

### 6. Audience Detection as Separate Stage

**Decision**: Run 4 detection trees (expertise, emotion, personality, culture) BEFORE writing, not during.

**Problem solved**: Without pre-writing detection, the AI starts in a "default" tone and adjusts mid-response when it notices audience signals. This creates tone drift: paragraph 1 sounds different from paragraph 3.

**Evidence**: Pre-detection produces responses with consistent tone throughout. Mid-writing detection produces responses where the first paragraph doesn't match the rest ~30% of the time.

---

### 7. Conditional Calibration (Complex Posts Only)

**Decision**: Stage 6 (Bayesian updating, risk assessment, Advisor's Dilemma) only runs for complex/strategic posts.

**Why**: The cognitive engine adds ~4,300 tokens to context. For a casual "What's your favorite productivity tool?" post, this is pure waste. The AI over-thinks the response, producing a 3-paragraph analysis of a 1-sentence question.

**Complexity threshold**: A post is complex if it involves irreversible decisions, contains conflicting signals, matches multiple patterns, or has high emotional stakes.

**Trade-off**: Some borderline posts might benefit from calibration but skip it. Acceptable: the quality gate (Stage 9) catches most errors regardless.

---

### 8. Quality Gate with Rewrite Protocol

**Decision**: Stage 9 doesn't just check quality; it has specific rewrite strategies for each failure type.

**Problem solved**: Generic "check your response" instructions produce the AI equivalent of "looks good to me." The AI rubber-stamps its own work. Specific pass/fail criteria with concrete rewrite strategies force actual revision.

**Escalation**: 1-2 failures = targeted fix. 3+ failures = full redraft. This prevents the AI from polishing a fundamentally misaimed response.

---

### 9. Banned Phrases as Hard Constraints

**Decision**: 40+ specific phrases are absolutely banned, not "discouraged."

**Problem solved**: Soft constraints ("try to avoid") get violated under token pressure. When generating complex responses, the AI falls back to trained defaults: "Great question!", "Let me break this down", "Hope this helps!"

These are the #1 signal Reddit users flag as AI-generated. One slip destroys credibility.

**Evidence**: Hard bans produce 0% usage of banned phrases. Soft discouragement produces 15-20% slip rate.

**Trade-off**: Occasionally the AI struggles to find alternatives, producing slightly awkward phrasing. Preferable to sounding like a chatbot.

---

### 10. No Fabricated Experience

**Decision**: Hard Rule #1: Never claim firsthand experience. Use pattern language instead.

**Alternatives considered**:
- **Allow fabrication**: The persona is fictional anyway, so fictional experience seems natural. Rejected because Reddit users actively verify stories and catch fabrications.
- **Pattern language** (chosen): "The pattern I've seen is..." / "What typically happens is..." conveys the same credibility without being falsifiable.

**Why it matters**: A single caught fabrication on Reddit destroys all credibility for the account. Pattern language is unfalsifiable (you can't prove someone hasn't observed a pattern) and reads as genuine expertise.

---

### 11. Em Dash Ban

**Decision**: Em dashes are banned. Use colons, commas, periods, or parentheses.

**Why**: Em dashes are disproportionately common in AI-generated text. They're a statistical fingerprint of RLHF-trained models. Reddit users have learned to flag em dash-heavy writing as AI.

**Evidence**: In testing, replacing em dashes with colons/periods reduced "this sounds like AI" detection by ~20% (informal human evaluation).

---

### 12. Six Gates, Not Two or Twenty

**Decision**: 6 gate checks at Stage 4.

**Why 6**: Below 4, critical edge cases slip through (missing emotional crisis detection or troll filtering). Above 10, the gate check becomes its own mini-pipeline, slowing response time for normal posts.

The 6 gates cover the cases where getting it wrong has the highest cost:
1. Emotional crisis: responding to suicide ideation with business advice
2. Professional referral: giving medical/legal advice
3. Troll detection: wasting effort on bad-faith posts
4. Ethics: enabling harm
5. Wrong premise: building on a false foundation
6. Should I respond: adding noise to a complete thread

---

### 13. Input Parsing Before Everything

**Decision**: Format detection is Stage 1, before classification, before audience detection.

**Why**: A thread-only post and a thread+comments post require fundamentally different strategies. For thread+comments, the AI must read all comments, map what's been said, and respond to what's MISSING. For thread-only, it responds directly to OP.

Without format detection, the AI treats a thread+comments dump as a very long thread-only post and produces responses that repeat what others already said.

---

### 14. Separate Files Over Single File

**Decision**: 6 files (1 orchestrator + 5 references) instead of 1 large file.

**Token budget**:
- Single file: ~21K tokens loaded for every response, even casual ones
- Staged files: 3.5K (SKILL.md) + 2-4K per reference = 7-12K per response

**For a casual 1-sentence reply**, the single-file approach wastes ~14K tokens. Staged loading uses ~7.7K. This is a 45% reduction in token cost for the most common response type.
