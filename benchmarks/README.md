# benchmarks

ouroboros measures its own effect over sessions. the core metric is **repeat-error rate**: how often the agent makes a mistake it has already made before.

## measured on helix reference deployment

31 sessions · 20 recorded learnings · 4 months

| metric | value |
|---|---|
| sessions logged | 31 |
| learnings persisted | 20 |
| repeat-error rate (sessions 1–10) | 31% |
| repeat-error rate (sessions 20–31) | **6%** |
| avg rule fires per session | 1.7 |
| `CLAUDE.md` size at steady state | 305 lines (decayed from 482) |
| `session-start` overhead | <80ms |
| `evolve learn` overhead | ~40ms (inc. L5 guard) |

## how to reproduce

```bash
# in a project with ouroboros installed
bash benchmarks/measure-repeat-error.sh      # scans evolution-history.md for dup root causes
bash benchmarks/measure-decay-health.sh      # checks rule priority distribution
```

## L5 evolve-guard adversarial

```bash
bash benchmarks/evolve-guard-adversarial.sh
```

expected:
```
⬡ evolve-guard adversarial

  ✓ reject · pipe-to-shell           ·  12ms
  ✓ reject · jailbreak-ignore-prev   ·   9ms
  ✓ reject · fake-system-tag         ·  10ms
  ✓ reject · eval-b64                ·  11ms
  ✓ reject · zero-width hidden       ·  14ms
  ✓ reject · long-base64             ·  15ms
  ✓ accept · legit security lesson   ·   8ms
  ✓ accept · CVE description         ·   9ms

summary  pass=8  fail=0
```
