# dev-mastery — Index

Five-year curriculum: React → .NET → Distributed Systems/Go →
Cloud/K8s → Security/SRE → Leadership, with continuous
architecture and infrastructure-foundations tracks.

**Owner:** 15+ yrs coding, professionally frontend (JavaScript,
not TS). Company runs .NET 8 he doesn't touch. Strong intuition,
weak explicit theory. Target: senior/staff depth, then technical
leadership. 8–15 hrs/week, newborn at home, fragmented sittings.

**Total estimated effort:** ~2,800 hours (~4–5.5 years).
**Orchestration:** Cursor / Claude Code, driven by `CLAUDE.md`.
**v1 scope:** markdown only. No scripts.

## Read order for an AI joining cold

1. `NOW.md` — where I stopped
2. `CLAUDE.md` — rules, rails, boot sequence
3. `docs/01-ARCHITECTURE.md` — how the system works
4. `CURRICULUM.yaml` — the dependency graph
5. `PROGRESS.md` — tail 40 lines
6. `docs/04-AGENTS.md` — mode behaviours

## Files

| File | Written by | Purpose |
|---|---|---|
| `CLAUDE.md` | manual | Canonical rules. Auto-loaded by both tools. |
| `.cursor/rules/000-boot.mdc` | manual | Redirect to `CLAUDE.md` |
| `NOW.md` | agent | Current state. Rewritten every sitting. |
| `PROGRESS.md` | agent | Append-only log. Source of truth. |
| `CURRICULUM.yaml` | `build graph` | Dependency graph |
| `CALIBRATION.md` | `gate` | Skill ratings over time |
| `00-INDEX.md` | manual | This file |
| `docs/01-ARCHITECTURE.md` | manual | Session/sitting model, formats |
| `docs/02-PHASES.md` | manual | Phase and node reference |
| `docs/03-SCHEMA.md` | manual | `CURRICULUM.yaml` schema |
| `docs/04-AGENTS.md` | manual | Mode behaviours |
| `docs/06-BOOTSTRAP.md` | manual | One-time setup order |

## Triggers

Plain keywords, no slash needed, works in Cursor and Claude Code:

`start` · `pause` · `wrap up` / `done` · `maintenance` · `gate` ·
`quiz` · `build graph`

## Tracks

| Track | Share | Content |
|---|---|---|
| Primary | 50% | Current phase focus |
| Secondary | 25% | Linux, HTTP, git, Docker, TS, SQL, observability |
| Architecture | 15% | Patterns, SOLID, DDD, refactoring, ADRs |
| Maintenance | 10% | Spaced review |

Secondary and architecture run continuously alongside every phase,
not sequentially.

## Current state

Phase: 0 (bootstrap)
Nodes complete: 0
Next: `docs/06-BOOTSTRAP.md` step 3 — Phase 1 graph sign-off
  (primary awaiting sign-off; secondary and architecture still stubs)
