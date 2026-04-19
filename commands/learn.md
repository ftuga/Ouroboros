---
description: Persist a lesson into CLAUDE.md and active-rules — the agent will apply it next session
allowed-tools: Bash(bash:*)
---

Teach the harness a lesson. The lesson is persisted into `~/.claude/CLAUDE.md` under the matching category and added to `~/.claude/memory/active-rules.md`. The L5 evolve-guard rejects attack patterns before persistence.

**usage:** `/learn <category> "<lesson>" "<trigger>"`

**categories:** `seguridad` · `interfaz` · `funcionalidad` · `operatividad` · `arquitectura` · `performance` · `testing` · `datos` · `celery` · `auth` · `docker`

Run:
```bash
bash ~/.claude/evolve.sh learn $ARGUMENTS
```
