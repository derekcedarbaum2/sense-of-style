# AGENTS.md — `sense-of-style`

Operating protocol for agents installing this skill for an operator.

## What this repo provides

A single Claude Code skill — `sense-of-style`. Diagnoses and rewrites prose using Steven Pinker's *Sense of Style* principles. Scores writing on 8 style dimensions, flags line-level problems (nominalizations, passive voice, hedges, broken topic chains, clichés), and produces a rewrite that preserves voice while killing bloat.

## Read order

1. `README.md` — human overview, the 8 dimensions, when to use vs. when not to.
2. `SKILL.md` — the skill itself.
3. `examples/` — annotated before-and-after rewrites.

## Trust boundary

- This skill changes *prose* — it should preserve voice and intent. The 8-dimension scoring is the audit trail.
- The skill does NOT fix arguments, structure, or claims. For that, pair with [`qa-loop`](https://github.com/derekcedarbaum2/qa-loop).
- Pinker's principles are opinionated. If the operator's voice is intentionally unconventional (poetry, intentional repetition, distinctive cadence), the skill may over-correct. Check examples first.

## Install

```bash
mkdir -p ~/.claude/skills/sense-of-style
cp -r SKILL.md examples/ ~/.claude/skills/sense-of-style/
```

## Adaptation checklist

- [ ] Operator's voice is documented somewhere the skill can reference (e.g., a `derek-voice.md` shared file). The skill should preserve that voice, not impose Pinker's.
- [ ] Skill registers — verify by invoking `/sense-of-style`.

## Common tasks

| Task | Command |
|---|---|
| Diagnose + rewrite a prose document | `/sense-of-style /path/to/doc.md` |
| Diagnose only (no rewrite) | `/sense-of-style /path/to/doc.md --score-only` (if supported by the SKILL.md) |

## When to use this vs. `qa-loop`

- **`sense-of-style`** — content is right but the writing is soft. The argument works; the sentences don't sing.
- **`qa-loop`** — argument has gaps, claims are weak, or structure is off. Fix the substance first.
- **Both** — apply qa-loop first, then sense-of-style. The order matters: rewriting prose around a broken argument just polishes the wrong thing.

## Related repos

- [`qa-loop`](https://github.com/derekcedarbaum2/qa-loop) — the substance/argument loop. Pair with sense-of-style.
- [`adversarial-agent-pattern`](https://github.com/derekcedarbaum2/adversarial-agent-pattern) — meta-pattern documentation for qa-loop and siblings.
