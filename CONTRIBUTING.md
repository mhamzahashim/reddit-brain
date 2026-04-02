# Contributing to Reddit Brain

Thanks for your interest in improving Reddit Brain. This document covers how to contribute patterns, domains, voice rules, and documentation.

---

## What You Can Contribute

| Type | Where | Difficulty |
|---|---|---|
| New post pattern | `skill/references/pattern-library.md` | Medium |
| New domain | `skill/references/domain-brain.md` | Medium |
| New AI tell detection | `skill/references/quality-gate.md` | Easy |
| Voice improvements | `skill/references/voice-engine.md` | Hard |
| Pipeline improvements | `skill/SKILL.md` | Hard |
| Documentation | `docs/`, `README.md`, `DOCS.md` | Easy |
| Examples | `examples/` | Easy |
| Bug reports | GitHub Issues | Easy |

---

## Workflow

### Issue-First

Every change starts with an issue. This ensures alignment before work begins.

1. **Open an issue** describing what you want to change and why
2. **Wait for maintainer review** (within 2 business days)
3. **Once approved**: fork, branch, make changes, open PR
4. **PR must reference the issue** ("Closes #N" in the PR body)

### For Small Changes

Typos, documentation fixes, and single-line corrections can skip the issue step. Open a PR directly.

### Branch Naming

```
<type>/<short-description>

Examples:
pattern/add-perfectionist-pattern
domain/add-cybersecurity
fix/voice-engine-typo
docs/add-usage-examples
```

### Commit Messages

Follow conventional commit format:

```
<type>(<scope>): <description>

Types: feat, fix, docs, refactor, test, chore
Scopes: pattern, voice, cognitive, domain, quality, pipeline, docs
```

Examples:
```
feat(pattern): add perfectionist pattern with diagnostic checklist
fix(voice): remove duplicate banned phrase
docs(examples): add SaaS pricing thread example
```

---

## Contribution Standards

### Adding a New Pattern

Every pattern MUST include all 6 components:

```markdown
### Pattern Name

**Surface**: What the post appears to be about
**Reality**: What's actually happening underneath
**Diagnostic checklist** (all 5 must be present):
1. Signal one (specific, observable in text)
2. Signal two
3. Signal three
4. Signal four
5. Signal five
**Confidence threshold**: X of 5 signals = confirmed
**Misdiagnosis cost**: What goes wrong if you get this wrong
**Response strategy**: How to respond when this pattern is confirmed
```

Requirements:
- Must be validated against 5+ real Reddit posts
- Must be distinct from existing patterns (not a variant)
- Must include misdiagnosis cost (what happens if you wrongly apply this pattern)
- Diagnostic signals must be observable from text alone (no assumptions about poster's mental state)

### Adding a New Domain

Every domain entry MUST follow this structure:

```markdown
## Domain Name

- Insight 1 (specific, actionable, includes threshold/number)
- Insight 2
- ...5-8 insights total
```

Requirements:
- Every insight must be non-obvious (not findable in the first page of Google results)
- Every insight must be actionable (the reader can do something with it)
- Include specific numbers/thresholds where possible ("If X is below Y, do Z")
- Practitioner-level only (5+ years of domain experience)

### Adding an AI Tell

```markdown
**Vector N: Name**
- What it looks like: (specific example)
- Detection: (how to spot it in draft)
- Suppression: (how to fix it)
```

Requirements:
- Must be a pattern that real Reddit users actually flag as AI
- Must include both detection method AND fix strategy
- Must not overlap with existing tells (check the 15-vector list)

### Voice Contributions

Voice changes are the highest-risk modifications. A single change can break persona consistency across all responses.

Requirements:
- Must be tested against 10+ diverse Reddit posts
- Must not conflict with existing voice rules
- Must preserve the core persona (veteran marketer, direct, anti-hype)
- Banned phrase additions must include rationale

---

## Testing Your Changes

Reddit Brain doesn't have automated tests (it's a prompt system, not code). Testing is manual:

### Pattern Testing

1. Find 5+ real Reddit posts that match your proposed pattern
2. Verify the diagnostic checklist correctly identifies the pattern in each post
3. Verify existing patterns don't already cover this case
4. Document the test posts in your PR

### Domain Testing

1. Find 5+ real Reddit posts asking questions in the domain
2. Verify the insights produce useful, non-obvious responses
3. Verify the insights are accurate and current
4. Document the test posts in your PR

### Voice Testing

1. Run `/reddit` on 10+ diverse posts (casual, technical, emotional, complex)
2. Verify persona consistency across all responses
3. Verify no AI tells introduced
4. Compare before/after response quality
5. Document all test posts and results in your PR

---

## PR Template

When opening a PR, include:

```markdown
## What Changed

[Brief description]

## Why

[Motivation: what problem does this solve?]

## Testing

[List of Reddit posts tested against, with results]

## Checklist

- [ ] Follows contribution standards for this type of change
- [ ] Tested against 5+ real Reddit posts
- [ ] Does not conflict with existing patterns/rules
- [ ] Updated line counts in ARCHITECTURE.md if file sizes changed
- [ ] Documentation updated if needed

Closes #[issue number]
```

---

## Code of Conduct

- Be constructive. Critique ideas, not people.
- Back claims with evidence (real Reddit posts, not hypotheticals).
- Respect the persona. Changes that break the veteran marketer voice need strong justification.
- Don't add complexity without proven value. Every line in a reference file costs tokens.

---

## Questions?

Open a discussion issue with the `question` label.
