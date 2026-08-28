# Bootstrap

One-time. After step 7, every sitting uses the `CLAUDE.md` boot
sequence with no skip.

Estimated total: a few fragmented sittings, not a weekend.

---

## Step 1 — Operating files

**Done.**

`CLAUDE.md`, `.cursor/rules/000-boot.mdc`, `00-INDEX.md`, `NOW.md`,
`PROGRESS.md`, `docs/01-ARCHITECTURE.md`.

These are the rules, the state machine, and the read order.

---

## Step 2 — Seed the graph

**Done.**

`CURRICULUM.yaml` exists with `meta`, fully specified templates
`P1-M01` and `P1-M02`, stubs for the rest of Phase 1, and gate
`G-1`. Phases 2–6 are **not** in the yaml; they wait for gates.

---

## Step 3 — Remaining docs + Phase 1 full specs

Write `docs/02-PHASES.md`, `docs/03-SCHEMA.md`, `docs/04-AGENTS.md`,
this file. Skeleton `CALIBRATION.md`. Scaffold directories.

Expand every Phase 1 stub (primary, then secondary, then
architecture) to the full schema. Sign-off per track. Invent
`S-99-*` where the plan is missing a substrate.

Do not generate phases 2–6.

When this step is finished, `NOW.md` points at step 4.

---

## Step 4 — Diagnostic exam

No studying first. The point is a baseline, not a grade.

Across the ten `CALIBRATION.md` axes, mix of:

- Predict-the-output / “what happens if”
- Explain-back of something they already ship at work
- At least one question per axis where the naive answer is wrong

Agent scores 1–5 per axis (see `CALIBRATION.md` legend), writes the
first dated column, and notes two or three likely first nodes —
then recommends **exactly one** (step 5).

This is not gate G-1. Failing hard is useful data.

---

## Step 5 — First-node pick

Rails are empty (no last-6). Diagnostic + `entry_criteria` decide.

Default gravity is `P1-M01` unless the diagnostic says the JS
substrate is already `depth_1` and something else is the real
hole (Linux, HTTP, or “cannot explain hooks from first
principles” → still M01/M02).

Write `NOW.md` for that session. Do not open two nodes.

---

## Step 6 — Prove the sitting loop

One real sitting on the chosen node. Work. Then `pause`.

Check:

- `NOW.md` fully rewritten
- Next action is imperative (open X, run Y, expect Z)
- Open questions not blank
- `PROGRESS.md` untouched
- A commit happened

If `NOW.md` was not rewritten, fix the agent behaviour before
doing more curriculum. Cold-start cost is the failure mode this
repo exists to kill.

---

## Step 7 — Enable boot

From the next sitting: no “skip the boot sequence”. First message
of every session runs the status block in `CLAUDE.md` and waits
for a duration.

Optional: add a `MAINTENANCE` reminder date; create the first
Forge inbox file if C-01 has not shipped yet (export format still
stands).

Bootstrap is complete when step 6 has been proven once.
