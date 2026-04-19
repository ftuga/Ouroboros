# the evolution loop

```
┌──────────────────────────────────────────────────────────────────┐
│                                                                  │
│   session-start                                                  │
│      ├─ load ~/.claude/memory/active-rules.md                    │
│      ├─ check ~/.claude/memory/helix-alerta.md                   │
│      └─ emit [HELIX-SUGGEST-ANALYSIS] if no baseline             │
│      ▼                                                           │
│   [ agent works on task ]                                        │
│      │                                                           │
│      ├─ error happens                                            │
│      │    └─ /learn <category> "<lesson>" "<trigger>"            │
│      │         ├─ L5 evolve-guard scans lesson                   │
│      │         │    └─ reject if jailbreak/pipe/eval/zero-width  │
│      │         ├─ append to ~/.claude/CLAUDE.md § <category>     │
│      │         ├─ append to ~/.claude/memory/active-rules.md     │
│      │         └─ increment category counter                     │
│      │                                                           │
│      ├─ pattern repeated 2+ times                                │
│      │    └─ /skill <name> "<description>"                       │
│      │         └─ creates ~/.claude/skills/<name>/SKILL.md       │
│      │                                                           │
│      └─ before declaring task done                               │
│           └─ /self-check                                         │
│                ├─ DB model changes propagated?                   │
│                ├─ endpoints registered?                          │
│                ├─ env vars in .env.example?                      │
│                ├─ independent Reads/Greps parallelized?          │
│                └─ patterns ≥2 times have a skill?                │
│                                                                  │
│   session-end "<summary>"                                        │
│      ├─ append session row to ## 📋 SESIONES                     │
│      ├─ decay.sh: lower priority of unfired rules                │
│      ├─ archive rules < priority 20                              │
│      └─ save retrospective                                       │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

## why this works

the crux: **the system prompt is the cheapest place to store policy.** every retrieval-based memory system pays a tool call (latency + tokens). writing to `CLAUDE.md` pays once, at session-start, and applies to every turn for free.

the trade-off: `CLAUDE.md` grows. decay solves growth.

## decay

every rule has a priority score (0–100) and a `last_fired` timestamp. decay:

1. runs at session-end
2. reduces priority by 5 for rules that didn't fire this session
3. archives rules at priority ≤ 20 to `memory/topics/decayed-rules.md`
4. keeps the 3 highest-priority rules per category regardless of fire-rate (anchor rules)

in practice: lesson-learning is additive, but the hot set stays bounded. on the reference helix deployment, `CLAUDE.md` grew from 120 → 482 lines over 4 months, then decay brought it back to 305 and held it there.

## active-rules.md format

```markdown
| priority | category | rule | trigger | last fired |
|---|---|---|---|---|
| 92 | seguridad | endpoints /debug deben eliminarse antes de prod | staging leak 2026-04-12 | 2026-04-12 |
| 87 | testing   | todo bug debe tener test que lo reproduzca      | regression #142       | 2026-04-15 |
| 45 | operatividad | reads/greps independientes en paralelo       | serial-antipattern    | 2026-03-28 |
```

one file. one sort key. grep-friendly.
