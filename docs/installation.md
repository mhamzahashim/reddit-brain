# Installation

Detailed setup instructions for Reddit Brain across different environments.

---

## Claude Code (Recommended)

### Quick Install

```bash
git clone https://github.com/mhamzahashim/reddit-brain.git
mkdir -p ~/.claude/skills/reddit/references
cp reddit-brain/skill/SKILL.md ~/.claude/skills/reddit/
cp reddit-brain/skill/references/*.md ~/.claude/skills/reddit/references/
```

### Verify Installation

```bash
ls -la ~/.claude/skills/reddit/
# Should show:
# SKILL.md
# references/

ls -la ~/.claude/skills/reddit/references/
# Should show:
# cognitive-engine.md
# domain-brain.md
# pattern-library.md
# quality-gate.md
# voice-engine.md
```

### Usage

In Claude Code, type `/reddit` and paste the Reddit post. The skill auto-detects Reddit content and triggers the pipeline.

### Updating

```bash
cd reddit-brain
git pull origin main
cp skill/SKILL.md ~/.claude/skills/reddit/
cp skill/references/*.md ~/.claude/skills/reddit/references/
```

---

## One-Line Install Script

```bash
git clone https://github.com/mhamzahashim/reddit-brain.git /tmp/reddit-brain && mkdir -p ~/.claude/skills/reddit/references && cp /tmp/reddit-brain/skill/SKILL.md ~/.claude/skills/reddit/ && cp /tmp/reddit-brain/skill/references/*.md ~/.claude/skills/reddit/references/ && echo "Reddit Brain installed." && rm -rf /tmp/reddit-brain
```

---

## Manual Setup (Any AI Platform)

Reddit Brain works as a modular prompt system. You can adapt it to any AI that supports multi-file context or tool use.

### Minimum Viable Setup

1. Use `skill/SKILL.md` as your system prompt
2. When the pipeline says "load references/X.md," include that file's contents in the context

### Recommended Setup

1. Load `skill/SKILL.md` as the persistent system prompt
2. Create a tool/function that reads reference files on demand
3. Configure the tool to be called at the pipeline stages specified in SKILL.md

### Reference Loading Map

| Stage | Reference File | When to Load |
|---|---|---|
| Stage 2 | `references/pattern-library.md` | Every post |
| Stage 3 | `references/voice-engine.md` | Every post (can skip for casual) |
| Stage 6 | `references/cognitive-engine.md` | Complex/strategic posts only |
| Stage 8 | `references/domain-brain.md` | When post touches a specific domain |
| Stage 9 | `references/quality-gate.md` | Every post (can skip for casual) |

---

## File Structure

```
~/.claude/skills/reddit/
├── SKILL.md (223 lines, ~3.5K tokens)
└── references/
    ├── pattern-library.md (266 lines, ~4.2K tokens)
    ├── voice-engine.md (259 lines, ~4.1K tokens)
    ├── cognitive-engine.md (276 lines, ~4.3K tokens)
    ├── domain-brain.md (135 lines, ~2.1K tokens)
    └── quality-gate.md (183 lines, ~2.9K tokens)

Total: 1,342 lines, ~21K tokens
Max concurrent: ~750 lines, ~12K tokens
```

---

## Troubleshooting

### Skill Not Triggering

- Verify files are in `~/.claude/skills/reddit/` (not a subdirectory)
- Check SKILL.md has valid frontmatter (name: reddit)
- Try explicit trigger: type `/reddit` before pasting

### References Not Loading

- Verify all 5 files exist in `~/.claude/skills/reddit/references/`
- File names must match exactly (case-sensitive)
- Check file permissions: must be readable

### Responses Too Long

- The Length Law in SKILL.md should be at the top of the operational sections
- If it's been moved or modified, length compliance drops
- Verify lines 17-41 of SKILL.md contain the Length Law section

### AI-Sounding Output

- Verify quality-gate.md is intact (not truncated)
- Check that voice-engine.md's banned phrases section is complete
- The 15-vector AI tell scan runs at Stage 9: if quality-gate.md is missing, it's skipped
