---
description: Extract a repeated pattern into a reusable skill under ~/.claude/skills/
allowed-tools: Bash(bash:*)
---

Create a new skill from a repeated pattern. Skills live in `~/.claude/skills/<name>/SKILL.md` and are loaded on-demand (not every session).

**usage:** `/skill <name> "<description>"`

Run:
```bash
bash ~/.claude/evolve.sh skill $ARGUMENTS
```
