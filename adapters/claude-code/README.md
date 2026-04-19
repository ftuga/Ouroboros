# claude code adapter

default target. `install.sh` at repo root does everything:

1. copies `hooks/evolve.sh`, `self-check.sh`, `session-start.sh`, `session-end.sh` → `~/.claude/`
2. copies `hooks/decay.sh`, `session-exit-hook.sh` → `~/.claude/helpers/`
3. seeds `~/.claude/CLAUDE.md` (from `templates/CLAUDE.md.template`, only if absent)
4. seeds `~/.claude/memory/active-rules.md`
5. creates `~/.local/bin/ouroboros` dispatcher
6. registers `session-exit-hook.sh` in `settings.json` (SessionEnd event)

## manual install

```bash
mkdir -p ~/.claude/helpers ~/.claude/memory/topics ~/.local/bin
cp hooks/{evolve,self-check,session-start,session-end}.sh ~/.claude/
cp hooks/{decay,session-exit-hook}.sh ~/.claude/helpers/
chmod +x ~/.claude/*.sh ~/.claude/helpers/*.sh

# optional: seed CLAUDE.md and active-rules if absent
[ ! -f ~/.claude/CLAUDE.md ] && cp templates/CLAUDE.md.template ~/.claude/CLAUDE.md
[ ! -f ~/.claude/memory/active-rules.md ] && cp templates/active-rules.template.md ~/.claude/memory/active-rules.md

# add to ~/.claude/settings.json under "hooks":
#   SessionEnd → ".*" → session-exit-hook.sh
```
