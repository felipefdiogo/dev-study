# CURRICULUM.yaml schema

Derived from the fully specified nodes `P1-M01` and `P1-M02`.
v1 is markdown + YAML only. No scripts. Validate by hand (checklist
at the bottom).

The file is a **DAG**. Numeric ids (`P1-M03` before `P1-M04`) are
labels, not order. Most numbering is enrichment.

```yaml
meta:
  version: 1
  total_estimated_hours: 2800
  phase_gates_hard: true
  track_balance_rule: "of last 6 completed nodes, >=1 secondary and >=1 architecture"
  staleness_force_months: 3
  current_phase: 1
  graph_built_through_phase: 1

nodes: [ ... ]

gates: [ ... ]
```

`graph_built_through_phase: N` means nodes for phases `> N` must
not exist yet. They are authored at gate `G-N`.

---

## Node fields

Every non-stub node has all of the following.

### `id` (string, required)

Stable id. Patterns:

- `P{phase}-M{nn}` — primary, current phase
- `S1-{nn}` — secondary (foundations; spans phases)
- `A-{nn}` — architecture (continuous)
- `C-{nn}` — capstone / tool (e.g. Forge)
- `S-99-{topic}` — remedial prerequisite, created when a node’s
  `stuck_fallbacks` need a target that does not exist yet

Ids are referenced from `requires`, `unlocks`, `stuck_fallbacks.goto`,
`review_triggers.on_complete`, and `gates.nodes`. All must resolve.

### `title` (string, required)

Human title. Matches `docs/02-PHASES.md`.

### `phase` (integer, optional)

Primary nodes set this. Secondary and architecture omit it when they
span phases. Remedial `S-99-*` use `phase: 0`.

### `track` (enum, required)

`primary` | `secondary` | `architecture`

Maintenance is not a node track; it is a sitting mode.

`S-99-*` use `track: secondary` so they have a home, but they are
**not** a valid way to satisfy the track-balance rail. Rails look at
the last 6 *chosen* completions; if stuck-detection routed you to
`S-99-*`, say so in `PROGRESS.md` and do not count it as “I did a
secondary node” for balance.

### `effort_hours` (pair `[min, max]`, required)

Hours to reach `depth_2_solid`, not to finish `depth_3_deep`.
If the range looks wrong at authoring time, flag it in the PR/session
rather than silently keeping a round number.

### `requires` (list of node refs, required — may be `[]`)

**Hard dependencies only.** A ref is `ID` or `ID@depth_*`.

Use a depth suffix when `depth_1_working` on the dependency is not
enough. Example: `P1-M02` requires `P1-M01@depth_1_working`.

Do **not** put a node in `requires` because:

- it has a lower number
- it would be “nice to have first”
- it makes the graph look linear
- you studied it that way historically

Those belong in `unlocks` as `ID@enriched` on the *source* node.

If B is only richer after A, then A `unlocks: [B@enriched]` and B
does **not** `require` A.

### `unlocks` (list of node refs, required — may be `[]`)

Nodes that become available, or richer, when this node is done.

- `P1-M02` — hard unlock (the target also `requires` this node)
- `P1-M03@enriched` — not a blocker; later work is better with this
  behind you

### `entry_criteria` (list of strings, required)

What must already be true **before** starting. These are skills and
setup, not other curriculum nodes (those go in `requires`).

Example: “Can write a React app with hooks unaided”.

### `exit_criteria` (object, required)

Exactly three keys:

```yaml
exit_criteria:
  depth_1_working: [...]
  depth_2_solid: [...]
  depth_3_deep: [...]
```

| Depth | Meaning |
|---|---|
| `depth_1_working` | Genuinely sufficient to move on. A defensible stopping point, not a consolation prize. Shipping here and returning later is the intended pattern. |
| `depth_2_solid` | Target for the current phase. Gate exams assume this. |
| `depth_3_deep` | Plausibly revisited years later. Not required to proceed. |

Authoring test for `depth_1_working`: if someone stopped here, would
you argue they are blocked on later nodes, or merely less enriched?
If blocked, the criterion is too weak or belongs in `requires` of
the later node. If you are embarrassed to call it “done”, you have
written a consolation prize — raise it.

### `resources` (object, required)

```yaml
resources:
  essential: [...]   # do these
  optional: [...]    # only if stuck or going to depth_3
```

Short names a future sitting can find. No dump of every blog post.

### `breakpoints` (list, required — may be `[]`)

Safe pause points inside a 2–6h session that may span weeks.

```yaml
- after: "stage 5 (reconciliation and keys)"
  note: "Natural pause — highest value per hour is behind me"
```

### `review_triggers` (list, required — may be `[]`)

Spaced review: when a *later* node completes, this node is due
again because the later context rewrites the earlier one.

```yaml
- on_complete: [P2-M03, P3-M01]
  reason: >
    async/await state machines and goroutines both
    recontextualise the event loop
```

`on_complete` ids must resolve (they may be in a future phase —
record the intent; the later graph must keep the id).

### `stuck_fallbacks` (list, required, ≥1)

This is what makes traversal **adaptive** rather than a reorder of
a list. Each entry is a failure mode you are likely to hit, and the
node that actually fixes it.

```yaml
- if: "Can't predict microtask ordering after 15 drills"
  goto: S-99-js-prerequisites
  note: "Needs scope/hoisting/prototype refresher first"
```

Rules:

- `goto` must resolve
- If the real fix is not in the graph, **invent** `S-99-{topic}`
  and add it as a full node (or a stub with a one-line why)
- `if` is observable (“after N drills”, “can’t draw X”), not mood
- Do not `goto` the same node

When recent `PROGRESS.md` “Confused about” lines match an `if`,
the agent routes there and says plainly that a prerequisite is
missing.

### `micro_sitting_tasks` (list, required, ≥2)

Used when a sitting is **< 30 minutes**. Never new material.

Each task must need **zero context load**: no “open the half-finished
app and remember where I was”. Examples that qualify:

- 5 prediction drills
- Redraw a diagram from memory, compare to notes
- Re-read one failed drill and write why it was wrong
- Re-read *your own* code and add comments
- Write one failing test for the next stage (test file only)

Examples that do **not** qualify:

- “Continue stage 6 of mini-React”
- “Debug the benchmark from last sitting”
- Anything that requires reconstructing a mental stack

---

## Depth-qualified refs

`NODE_ID` or `NODE_ID@qualifier` where qualifier is:

- `depth_1_working`
- `depth_2_solid`
- `depth_3_deep`
- `enriched`

`enriched` is only valid in `unlocks`, never in `requires`.

---

## Gate fields

```yaml
gates:
  - id: G-1
    after_phase: 1
    requires_all_at: depth_2_solid
    nodes: [P1-M01, P1-M02, ...]
    unlocks_phase: 2
```

| Field | Meaning |
|---|---|
| `id` | `G-{n}` |
| `after_phase` | Phase just finished |
| `requires_all_at` | Depth every listed node must have reached |
| `nodes` | Primary nodes of that phase (not the whole secondary/architecture tracks) |
| `unlocks_phase` | Next phase; agent may then `build graph` for that phase |

Gates are hard. No next-phase node until the exam in
`docs/04-AGENTS.md` also passes.

---

## Authoring rules

1. **`requires` is a blocker test.** Delete the edge. Can the node
   still be done, just worse? Then it was enrichment — move it to
   `unlocks: [X@enriched]` on the other node.
2. **`depth_1_working` is a stopping point.** Write it first. Then
   write `depth_2` as “what Phase N actually owes”. Then `depth_3`
   as “come back in three years”.
3. **`stuck_fallbacks` are the adaptive engine.** A graph with empty
   fallbacks only reorders. Name the *likely* stuck, not a generic
   “if confused, review”.
4. **Micro-tasks are mandatory** and context-free. If you cannot
   invent two, the node is too project-shaped — split a drill
   surface out of it.
5. **Architecture nodes name a subject codebase** in
   `entry_criteria` or `exit_criteria` (work app or a capstone).
6. **Do not author phases ahead of the gate.** Phase 2–6 full specs
   are written after G-1, G-2, … by the person who just passed.
7. **Invent `S-99-*` instead of pretending a primary node teaches
   the missing substrate.** Tell the human why you added it.
8. **One recommended next node at runtime.** The graph may branch;
   the agent does not dump the branch.

---

## Manual validation checklist

Run this whenever `CURRICULUM.yaml` changes.

- [ ] Every `id` unique
- [ ] Every ref in `requires`, `unlocks`, `goto`, `on_complete`,
      `gates.nodes` resolves to an `id` (future-phase ids in
      `review_triggers` are allowed as stated intent; note them)
- [ ] No cycles in the **hard** graph (`requires` only; ignore
      `@enriched`)
- [ ] `requires` contains no `@enriched`
- [ ] Every non-stub node has all three `exit_criteria` depths
- [ ] `depth_1_working` would be a defensible place to stop
- [ ] ≥2 `micro_sitting_tasks` per non-stub node, all zero-context
- [ ] ≥1 `stuck_fallbacks` per non-stub node; every `goto` resolves
- [ ] `effort_hours` is a two-integer range
- [ ] `track` is one of the three enums
- [ ] Gate node lists match `docs/02-PHASES.md` primary lists
- [ ] `graph_built_through_phase` matches which phases have
      non-stub primary nodes
- [ ] Stub nodes (id/title/track/effort/`requires` only) exist only
      as placeholders you are about to expand, never as “done”

No automated validator in v1. The agent runs this list during
`build graph` and at wrap-up if the yaml changed.
