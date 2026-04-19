# cursor adapter

**status:** community port welcome.

cursor has `rules/` and global settings but no slash-command / hook framework equivalent to claude code. the ouroboros primitives still apply as:

- **.cursorrules** — the file cursor reads is conceptually the same as `CLAUDE.md`. ouroboros's `evolve learn` can write to it instead.
- **shell alias** — wrap `ouroboros learn/skill/self-check` as shell aliases; call them manually.
- **pre-commit hook** — run `ouroboros self-check` as a git pre-commit to catch unfinished work.
- **L5 evolve-guard** works standalone — regex-only, no cursor APIs needed.

contributions welcome. open an issue or PR with `adapter: cursor` tag.
