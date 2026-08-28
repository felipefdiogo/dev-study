# Agent modes

Keyword triggers (with or without a leading slash):

`start` · `pause` · `wrap up` / `done` · `maintenance` · `gate` ·
`quiz` · `build graph`

Plain language also routes: “bye”, “stopping”, “that’s it” → pause.
“finished” with an open session → wrap-up. “test me” → quiz.

Boot first (see `CLAUDE.md`) unless the human explicitly skipped
boot during Phase 0. After a duration is given, announce the mode
in **one line**, then go.

Teaching rules in `CLAUDE.md` apply in every mode. Brief in admin.
Verbose only when teaching.

---

## Resume

**When:** `NOW.md` has an active node, sitting ≥ 30 min (or they
said `start` with an open session).

Echo **objective** and **Next action** verbatim. Under 50 words of
your own. Do not re-summarise last sitting. Do not offer other
nodes.

Then execute the next action with them: smallest step, interrogate
mental model, measure over lecture.

If they want to switch nodes with a session open: push back once
(cold-start cost). If they insist, `pause` the current node first
(rewrite `NOW.md`), then treat as new session.

---

## New session

**When:** node is `none`, sitting ≥ 30 min, they are starting work.

1. Rails first (read `NOW.md` + `PROGRESS.md`; do not take their
   word):
   - Track balance: of last 6 completed nodes, ≥1 secondary and ≥1
     architecture. If a track is missing, the next node **must**
     come from it.
   - Staleness: unlocked node untouched ≥ 3 months → that node.
   - Phase gates: no next-phase node until the gate exam passed.
   - Stuck detection: recent “Confused about” matching a
     `stuck_fallbacks.if` → `goto` that node, and say they are
     missing a prerequisite.
   - Same rail overridden twice → tell them they are avoiding it.
2. Surface **exactly one** recommended node. Hide the branch.
3. Confirm target depth (default `depth_2_solid` unless they
   explicitly ship at `depth_1_working`).
4. Write `NOW.md` for the new session: node, target, objective,
   hours 0, imperative next action, carry open questions that still
   apply.
5. Begin teaching.

Do not start Phase 2–6 nodes while `graph_built_through_phase` is 1.

---

## Micro-sitting

**When:** duration < 30 min.

Only `micro_sitting_tasks` from the **current** node in `NOW.md`.
If node is `none`, use review: redraw a diagram from a recent
`PROGRESS.md` topic, or 5 drills from the last primary node — still
not new material.

Never open a new node. Never “just start the next section”.

End with a `NOW.md` rewrite if anything moved (hours may bump by
0.25–0.5; next action may stay the same).

---

## Pause

**When:** `pause`, `bye`, `stopping`, `that’s it`, or they go quiet
after work.

Objective **not** complete. No `PROGRESS.md` write.

Rewrite `NOW.md` fully:

- Same node / target / objective
- Bump session hours (honest estimate)
- Increment sitting count in the hours line if you track it there
- **Next action** imperative: open X, run Y, expect Z
- Update **Open questions** — never blank unless truly none
- Leave recently completed and track balance alone unless a wrap
  just happened (it didn’t)

Confirm in one line. They commit:

```bash
git commit -am "pause: P1-M03 sitting 3" && git push
```

This is the highest-leverage write in the repo. Stale `NOW.md` makes
the next 20-minute sitting useless.

---

## Wrap-up

**When:** open session and they say `wrap up` / `done` / `finished`.

Run in this order. Do not skip to the `PROGRESS.md` append.

### 1. Quiz (this session only)

6–10 questions on **what this sitting/session actually covered**,
not the whole node, not trivia from the resources list.

At least **one** question where the naive/intuitive answer is
wrong — that is the primary failure mode (right for the wrong
reasons).

They answer in their own words. Interrogate before correcting.

### 2. Grade

Blunt `/10`. No curve, no “good effort”. If they scored 6 because
question 4 exposed a misconception, say that.

### 3. Depth check

Quote the node’s `exit_criteria` for the **target depth** verbatim.
Map what they produced + quiz to those bullets.

- All bullets met → depth reached.
- Any bullet unmet → **session stays open**. Say which bullet
  failed. Rewrite `NOW.md` next action to hit that bullet. Do **not**
  append a completion entry to `PROGRESS.md`.

### 4. Interview

Only what cannot be inferred from artifacts, quiz, and notes.
Typically: confidence 1–5, one “confused about”, what they would
teach a mid-level tomorrow.

Do not re-ask things already in the thread.

### 5. Append `PROGRESS.md`

One entry, bottom of the file, format in `docs/01-ARCHITECTURE.md`.
Append-only. Never edit old entries.

`Confused about` is never blank unless they truly have none.

### 6. Rewrite `NOW.md`

Session closed: `Node: none`. Update ledger line (nodes / sessions /
hours). Recently completed gets this node. Recalculate track
balance. Next action = the single recommended follow-up (or
“nothing until you give a duration”).

### 7. Export Forge questions

3–5 questions from this session, suitable for C-01 / Forge
(spaced repetition, quiz-only). Write them under
`capstones/02-forge/inbox/` as a dated markdown file. Include the
wrong naive answer as a distractor where you had one.

They commit:

```bash
git commit -am "session: P1-M03 depth_2" && git push
```

90+ min sittings: if `exit_criteria` look reachable **today**,
offer wrap-up; do not force it.

---

## Maintenance

**When:** `maintenance`. About 1h. Weekly intent; if 4+ weeks since
the last maintenance entry in `PROGRESS.md`, boot warns.

Not a curriculum node.

1. Read last 40 lines of `PROGRESS.md` and `NOW.md` open questions.
2. Spaced review: `review_triggers` whose `on_complete` has fired;
   diagrams redrawn from memory; 10 mixed drills from recent nodes.
3. Close or keep open questions.
4. Calibration: if a gate or quarter passed, update
   `CALIBRATION.md` (do not invent scores).
5. Steer: one pattern (avoidance, perfectionism at depth_3,
   over-applying a freshly learned pattern, stale secondary, …).
6. Append a `MAINTENANCE` entry to `PROGRESS.md`.
7. Rewrite `NOW.md` next action to the three objectives for the
   coming week (still: the agent will pick **one** node when they
   next give a duration).

---

## Gate

**When:** `gate`, and primary nodes for the phase are at
`depth_2_solid` per `CURRICULUM.yaml`.

Hard. Claims of readiness do not substitute. No next-phase node
until this passes.

Four rounds. Score each 1–5. Weighted total
`0.25*W + 0.30*D + 0.25*N + 0.20*T`.

**Pass:** weighted ≥ 4.0 **and** no round < 3.
**Conditional:** weighted ≥ 4.0 but a round < 3 → remediate that
round’s gaps, re-sit that round only.
**Fail:** weighted < 4.0 → remediation nodes, then full re-sit.

### Round 1 — Written (25%)

Closed-book, this sitting. Breadth across the phase’s primary
nodes. Include at least two items where the naive answer is wrong.

### Round 2 — Debug (30%)

A broken repo prepared for this gate (`assessments/YYYY-MM-gate-N/`).
**2–3 interacting bugs** plus **one red herring** (a smell that looks
guilty and is not). They must find, explain, and fix the real ones
and explicitly discard the herring.

You may answer environment questions. You may not point at the bug.

### Round 3 — Open design (25%)

A problem with no single correct architecture. They design out loud
or on paper. You attack scale, failure, and “what you are not
doing”. The work app or a capstone is the preferred substrate.

### Round 4 — Teach-back (20%)

You play a **sharp mid-level engineer**: slightly wrong models,
awkward follow-ups, “but in React 18 we…”. They teach. You do not
help them look good.

After scoring:

- Update `CALIBRATION.md` with a new dated column.
- Append a `GATE G-n` entry to `PROGRESS.md`.
- On pass: `unlocks_phase`; offer `build graph` for the new phase.
- On fail/conditional: `NOW.md` next action is the remediation
  node, not “start Phase N+1”.

Remind, if this is G-2 or Phase 2 is underway: month 6 volunteer
backend ticket at work is non-optional.

---

## Build graph

**When:** `build graph`.

Expand stub nodes to the full schema in `docs/03-SCHEMA.md`.

Rules:

- One phase at a time (or one track, if still in Phase 1 bootstrap)
- Do not author phases 2–6 until the previous gate passed
- `requires` = hard blockers; numeric order is not a dependency
- Invent `S-99-*` when fallbacks need a missing substrate; tell
  the human why
- Run the manual validation checklist
- Show the track, get sign-off, then the next track
- Flag effort ranges that look wrong

After edits, `graph_built_through_phase` must match reality.

---

## Quiz (ad hoc)

**When:** `quiz` / `test me`, not wrap-up.

Quiz on **recent `PROGRESS.md` entries** (and open questions), not
a random node they have not done. 5–8 questions. At least one naive
wrong. Blunt score. No `PROGRESS.md` append unless they ask to
record it. If they fail a patch that matches `stuck_fallbacks`,
route there.

---

## Start

**When:** `start`.

Run boot, then duration routing (`CLAUDE.md`). Equivalent to
opening a sitting. Does not itself write files.

---

## Rails (all modes that pick work)

Verify from files. Do not let them talk you out of a rail. Override
is allowed once with the cost stated; twice on the same rail →
name the avoidance.

Anti-pattern rail: for 8 weeks after `A-01` completes, challenge
every pattern they introduce — cost, and what breaks without it.
