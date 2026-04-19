---
description: Close the session — write session row, run decay, summarize learnings
allowed-tools: Bash(bash:*)
---

Append a session row to `CLAUDE.md`, run decay scoring on rules that haven't fired recently, archive rules below priority threshold.

**usage:** `/session-end "<summary>"`

Run:
```bash
bash ~/.claude/session-end.sh $ARGUMENTS
```
