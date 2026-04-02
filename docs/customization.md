# Customization Guide

How to adapt Reddit Brain for different personas, domains, and use cases.

---

## Changing the Persona

The persona is defined across 4 touch points. All must be updated together.

### 1. Identity (SKILL.md, lines 9-12)

Replace the veteran marketer description with your persona:

```markdown
You are the ghostwriter behind a Reddit account run by a [your persona].
You have [their experience]. You have [their scars]. You have [their wisdom].
```

### 2. Voice (SKILL.md, lines 62-107)

Update these sections:
- **Natural phrases**: Replace with vocabulary your persona would actually use
- **Banned phrases**: Keep the AI-tell bans, add persona-specific bans
- **Reasoning style**: How does your persona explain things? Stories? Data? Analogies?
- **Humor style**: Dry? Self-deprecating? Absurdist? None?
- **Disagreement style**: How does your persona push back?

### 3. Domain Brain (references/domain-brain.md)

Replace the 12 domains with domains your persona is an expert in. Keep the format:
- Non-obvious insights only
- Actionable (reader can do something with it)
- Include specific thresholds/numbers
- Nothing Google-able

### 4. Quality Gate Check J (references/quality-gate.md)

Update the "Persona" check to match your new persona's voice characteristics.

---

## Adding Custom Domains

Open `skill/references/domain-brain.md` and add a new section:

```markdown
## Your Domain Name

- Insight 1: specific, non-obvious, includes numbers where possible
- Insight 2: actionable, not a general principle
- Insight 3: practitioner-level (5+ years of experience)
- ...5-8 insights total
```

### Quality Checklist for Domain Entries

- [ ] Would someone with 1 year of experience already know this? (If yes, cut it)
- [ ] Can someone ACT on this? (If not, rewrite to be actionable)
- [ ] Does this include specific numbers/thresholds? (Add them)
- [ ] Is this still current? (Domain knowledge expires)

---

## Adding Custom Patterns

Open `skill/references/pattern-library.md` and add:

```markdown
### Pattern Name

**Surface**: What the post looks like
**Reality**: What's actually happening
**Diagnostic checklist**:
1. Specific observable signal
2. Specific observable signal
3. Specific observable signal
4. Specific observable signal
5. Specific observable signal
**Confidence threshold**: X of 5 = confirmed
**Misdiagnosis cost**: What goes wrong if you're wrong
**Response strategy**: What to do when confirmed
```

### Validation

Test your pattern against 5+ real Reddit posts before adding it. Verify:
- The checklist correctly identifies the pattern
- Existing patterns don't already cover this
- The misdiagnosis cost is real and specific

---

## Adjusting Length Defaults

The Length Law (SKILL.md, lines 17-41) controls response length. To adjust:

```markdown
## LENGTH LAW (OVERRIDES EVERYTHING BELOW)

**Hard limits by context:**
- Casual/discussion: [your limit]
- Rant/vent: [your limit]
- Technical: [your limit]
- Complex: [your limit]
```

Keep it at the top of the operational sections. Moving it lower reduces compliance.

---

## Adjusting Confidence Calibration

The cognitive engine (references/cognitive-engine.md) has a 5-level system. To adjust:

| Level | Default Language | Your Adjustment |
|---|---|---|
| Established fact | Direct statement | Keep as-is |
| Strong inference | "In most cases..." | Change to match persona voice |
| Reasonable judgment | "Based on what you've described..." | Change to match persona voice |
| Informed speculation | "One possibility is..." | Change to match persona voice |
| Outside competence | "You need a [professional]" | Change to match persona voice |

---

## Removing Stages

For simpler use cases, you can remove stages from the pipeline:

| Stage | Safe to Remove? | Impact |
|---|---|---|
| Stage 1: Parse | No | Breaks format detection |
| Stage 2: Classify | Not recommended | Removes diagnostic capability |
| Stage 3: Detect Audience | Yes, for fixed audience | Removes tone adaptation |
| Stage 4: Gates | Not recommended | Removes safety checks |
| Stage 5: Research | Yes | Removes fact verification |
| Stage 6: Calibrate | Yes, for simple posts | Removes decision frameworks |
| Stage 7: Set Length | No | Responses will be too long |
| Stage 8: Draft | No | Core writing stage |
| Stage 9: Quality Gate | Not recommended | Removes quality control |
| Stage 10: Cut | No | Final output stage |

To remove a stage: delete its entry from the Execution Pipeline section in SKILL.md. Also remove the "loads reference" instruction and the reference file if no longer needed.

---

## Using for Non-Reddit Platforms

The system works for any text-based platform. To adapt:

1. **Update trigger rules** in SKILL.md frontmatter (replace "Reddit" references)
2. **Update voice** for platform norms (Twitter is shorter, LinkedIn is more professional, forums vary)
3. **Update Length Law** for platform expectations
4. **Update input parsing** for platform-specific formats
5. **Update quality gate** AI tells section for platform-specific detection patterns

The core diagnostic pipeline (classify, detect audience, calibrate, quality gate) works across platforms.
