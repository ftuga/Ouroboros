---
description: Validate the pre-close checklist before declaring a task complete
allowed-tools: Bash(bash:*)
---

Run the pre-close validation. Checks: session-start ran, DB model changes propagated, endpoints registered, env vars in `.env.example`, repeated patterns → skill, independent Reads/Greps parallelized.

Run:
```bash
bash ~/.claude/self-check.sh
```
