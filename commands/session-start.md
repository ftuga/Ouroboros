---
description: Load active-rules + surface any session alerts
allowed-tools: Bash(bash:*)
---

Load `active-rules.md` summary, check for pending alerts (`helix-alerta.md`), suggest `/analiza` if no baseline. Call at the start of a session or on resume.

Run:
```bash
bash ~/.claude/session-start.sh
```
