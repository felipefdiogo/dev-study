# System Architecture

## Sessions vs sittings

**Session** = one learning objective, one node depth (2–6h).
**Sitting** = one physical block of time (20 min – 3h).

A session spans arbitrarily many sittings across arbitrarily many
days. `NOW.md` holds the open session. `PROGRESS.md` gets one entry
per *session*, written at wrap-up, so the log stays coherent even
though the calendar doesn't.

This split exists because of a newborn. Nothing in the system may
assume a sitting finishes anything.

## The loop

**Starting any sitting**

```bash
cd dev-mastery && git pull && claude .    # or: cursor .
```

Type anything. The agent boots automatically per `CLAUDE.md`,
prints the status block, and asks how long you have.

- `NOW.md` has an active node → resume. Echoes objective and
  "Next action" verbatim, under 50 words. No re-summarising.
- Node is `none` → graph traversal, rails first, then one
  recommendation.

**During**

Same thread all sitting. Commit as you go:

```bash
git commit -am "P1-M03: memo benchmark, 3 strategies"
```

**Ending a sitting, objective incomplete**

Say `pause`. The agent rewrites `NOW.md`: bumps hours, rewrites
"Next action" imperatively, updates open questions. No
`PROGRESS.md` write.

```bash
git commit -am "pause: P1-M03 sitting 3" && git push
```

**Ending a session, node depth reached**

Say `wrap up`. Quiz → grade → depth check → interview →
`PROGRESS.md` append → `NOW.md` reset → Forge questions exported.

```bash
git commit -am "session: P1-M03 depth_2" && git push
```

**Weekly** — say `maintenance`, ~1h.
**Phase boundary** — say `gate`.

## Graph, not a list

`CURRICULUM.yaml` is a DAG. It encodes what's genuinely *blocked*
versus merely *enriched* — most numeric module ordering is
enrichment, not dependency.

But the agent always surfaces **exactly one** recommended next
node. Branching stays hidden unless asked for, because visible
linear progress is what keeps me engaged.

## Three exit depths

Every node has:

- `depth_1_working` — genuinely sufficient to move on. Not a
  consolation prize.
- `depth_2_solid` — the target for the current phase.
- `depth_3_deep` — plausibly revisited years later.

Shipping at depth 1 and returning later is the intended pattern,
not a compromise. It's what stops perfectionism from becoming
abandonment.

## Track balance

Counted in **nodes, not hours** — verifiable by eye, no rolling
windows, no arithmetic the agent can fudge.

**Rule:** of the last 6 completed nodes, at least 1 secondary and
at least 1 architecture. If a track is absent, the next node must
come from it.

## Progress visibility

One ledger line at the top of `NOW.md`, updated at wrap-up:

```
> 4/24 Phase 1 nodes · 11 sessions · 62h logged
```

Three integers. Plus `PROGRESS.md`, which only ever grows. No XP,
no levels, no streaks in v1 — add them later if the append-only
log stops feeling like progress.

## NOW.md format

```markdown
> 4/24 Phase 1 nodes · 11 sessions · 62h logged

# NOW

**Node:** P1-M03 — Rendering cost model
**Target:** depth_2_solid
**Objective:** Measure the memo/useMemo crossover thresholds
**Session hours so far:** 4.5 (3 sittings)

## Next action
Open `phase-1-react/03-rendering/bench/context-split.jsx`.
Run `npm run bench:ctx` — expect ~40ms baseline.
Split the provider in two, re-measure.
Hypothesis: no change, because the consumer reads both halves.

## Open questions
- Does React 19 bail out earlier on same-reference context values?
- Is the React Compiler making manual memo obsolete or just
  usually-unnecessary?

## Recently completed
- P1-M02 mini-React — depth_2 — 2026-09-08
- P1-M01 JS substrate — depth_2 — 2026-08-24
- S1-01 Linux fundamentals — depth_1 — 2026-08-11

## Track balance (last 6 nodes)
primary 4 · secondary 1 · architecture 1
→ architecture is thin, pick A-01 next
```

Two states only: `Node: none — session closed`, or populated.
That's the entire state machine.

**"Next action" is the highest-value field in the repo.** Always
imperative — open X, run Y, expect Z. With 20-minute sittings,
cold-start cost is the dominant failure mode.

## PROGRESS.md entry format

```markdown
## 2026-09-16 — P1-M03 — Rendering cost model
**Node:** P1-M03 → depth_2_solid reached
**Hours:** 4.5 (3 sittings)
**Track:** primary
**Done:** 8 benchmarks; memoization decision flowchart derived
  from measured thresholds
**Learned:** memo() compares props before the render phase;
  children-as-JSX creates a new object every render, which is why
  memo "does nothing" on layout wrappers
**Confused about:** exact batching behaviour across await
  boundaries in React 18+
**Confidence 1-5:** 4
**Quiz:** 8/10
**Next:** P1-M04
```

Append-only. Never edited. `git log -p NOW.md` is the backup if a
sitting ends without a `NOW.md` rewrite.

## Directory layout

```text
dev-study/
├── CLAUDE.md
├── 00-INDEX.md
├── NOW.md
├── PROGRESS.md
├── CURRICULUM.yaml
├── CALIBRATION.md
├── .cursor/rules/000-boot.mdc
├── docs/
│   ├── 01-ARCHITECTURE.md
│   ├── 02-PHASES.md
│   ├── 03-SCHEMA.md
│   ├── 04-AGENTS.md
│   └── 06-BOOTSTRAP.md
├── phase-1-react/
│   └── 01-js-substrate/
│       ├── NOTES.md
│       ├── drills/
│       └── RETRO.md
├── phase-2-dotnet/
├── phase-3-distributed/
├── phase-4-cloud/
├── phase-5-security-sre/
├── secondary/
├── architecture/
├── capstones/
│   ├── 01-mini-react/
│   ├── 02-forge/
│   └── 03-headless-ui/
├── assessments/
│   └── 2026-XX-gate-1/
└── notes/
    ├── concepts/
    └── book-notes/
```
