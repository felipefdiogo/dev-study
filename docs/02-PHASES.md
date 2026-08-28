# Phases and nodes

Reference table. Effort is hours to `depth_2_solid` unless noted.
Architecture and secondary tracks run **alongside** every phase, not
after it.

Gate G-1 (and later gates) require the **primary** nodes of that
phase at `depth_2_solid`. Secondary and architecture nodes are not
gate blockers unless a primary node `requires` them.

**Ledger denominator:** `NOW.md` currently reads `N/24 Phase 1
nodes`. That 24 is the Phase 1 *window* (9 primary + 8 secondary +
the architecture nodes expected to be started in Phase 1, not all
10). The architecture track is 10 nodes across the whole
curriculum. Do not treat 24 as “must finish every architecture
node before G-1”.

---

## Capstones

| Capstone | Node | When |
|---|---|---|
| mini-React | P1-M02 | Phase 1 |
| Forge (quiz app, quiz-only v1) | C-01 | Phase 0 / ongoing tool |
| headless-ui (6 components vs Radix) | P1-M09 | Phase 1 |
| distributed system | P3-M09 | Phase 3 |
| full platform | P4-M12 | Phase 4 |

---

## Phase 0 — Bootstrap

Not a learning phase. Operating files, graph seed, diagnostic,
first sitting loop. See `docs/06-BOOTSTRAP.md`.

| Id | Title | Scope | Effort |
|---|---|---|---|
| C-01 | Forge: quiz app with spaced repetition (quiz-only v1) | Ship a local quiz tool you will actually use. Quiz-only; no lesson engine. | 20–35h |

Remedial nodes `S-99-*` are invented when a Phase 1 node’s
`stuck_fallbacks` point at a missing prerequisite. They are not
picked by the recommender except via stuck detection.

---

## Phase 1 — React (primary, 9 nodes)

Gate **G-1**: all nine at `depth_2_solid`. Unlocks Phase 2.

| Id | Title | Scope | Effort |
|---|---|---|---|
| P1-M01 | JavaScript substrate beneath React | Event loop, closures, task vs microtask, where React’s scheduler sits. | 25–40h |
| P1-M02 | Build a mini-React | Reconciler, fibers, keys, hooks rules from implementation. **Capstone.** | 50–80h |
| P1-M03 | Rendering cost model — measured not folklore | Profiler, memo/useMemo/context split from measured thresholds. | 30–45h |
| P1-M04 | State architecture — one app five ways | Same app, multiple state models; derived vs stored; blast radius. | 35–50h |
| P1-M05 | Concurrent React: lanes, Suspense, transitions, tearing | Urgent vs transition work; Suspense as constraint; tearing. | 30–45h |
| P1-M06 | RSC and the framework layer | Server/client boundary, serialisation, caching, what Next (etc.) adds. | 35–50h |
| P1-M07 | Testing React without waste | Behaviour vs implementation; async; what not to test. | 30–40h |
| P1-M08 | Performance: bundles, Web Vitals, memory, CI budgets | Load vs runtime vs memory; budgets that fail CI. | 35–50h |
| P1-M09 | Component API design — 6 headless components vs Radix | Compound/headless APIs, a11y, compare to Radix. **Capstone.** | 45–65h |

---

## Secondary track (8 nodes)

Infrastructure foundations. Spans Phase 1–2. Counts toward the
track-balance rail.

| Id | Title | Scope | Effort |
|---|---|---|---|
| S1-01 | Linux fundamentals: processes, fds, signals, `/proc` | What a process is; inspect live systems without a GUI. | 25–40h |
| S1-02 | Shell competence: bash properly, 5 tools I keep | Pipelines, quoting, job control; a small personal toolkit. | 15–25h |
| S1-03 | Git internals: objects, refs, DAG; build a mini-git | Object model, not GUI fluency. | 20–30h |
| S1-04 | HTTP & networking: TCP, TLS 1.3, H2/H3, caching, CORS | Packets to cookies; caching that actually works. | 30–45h |
| S1-05 | Docker: namespaces, cgroups, layers; toy runtime | Containers as Linux features, not as a Dockerfile hobby. | 25–40h |
| S1-06 | TypeScript: generics through conditional types | Read and write types at Radix/library level. | 30–45h |
| S1-07 | Observability basics: structured logs, OTel, RUM, source maps | Signals you can debug from; frontend and backend. | 20–30h |
| S1-08 | SQL fundamentals: modelling, indexes, query plans | Schema, indexes, `EXPLAIN`; enough to talk to a DBA. | 30–45h |

---

## Architecture track (10 nodes)

Continuous. Every node critiques a **real** codebase (work app or
capstones). Pattern study without a subject is cargo cult.

For 8 weeks after **A-01**, the anti-pattern rail is on: challenge
every pattern introduced.

| Id | Title | Scope | Effort |
|---|---|---|---|
| A-01 | GoF patterns — taught as when NOT to use them | Catalogue plus cost; what breaks without each pattern. | 25–40h |
| A-02 | SOLID, coupling/cohesion, dependency direction | Package and module direction; not poster SOLID. | 20–30h |
| A-03 | Domain-driven design (tactical + bounded contexts) | Ubiquitous language, aggregates, where DDD is too much. | 25–40h |
| A-04 | Application architecture | Layers vs features vs hexagonal; pick one for a real app and defend it. | 20–35h |
| A-05 | Enterprise patterns (PoEAA-scale) | Unit of Work, Identity Map, etc. — only where the app already has the problem. | 25–40h |
| A-06 | Refactoring: smells to transformations, under test | Refactoring as a discipline, not a rewrite. | 25–40h |
| A-07 | Working with existing code | Seams, characterisation tests, change without understanding everything. **Half-node.** | 10–18h |
| A-08 | Distributed-systems patterns | Outbox, sagas, idempotency, circuit breakers — as patterns, on a real or capstone system. | 25–40h |
| A-09 | ADR and C4 practice | Decisions you would actually file; C4 on the work app or a capstone. | 12–20h |
| A-10 | Anti-patterns | Name the failure modes you have shipped; cost of the “clean” alternative. | 15–25h |

---

## Phase 2 — .NET (primary, 12 nodes)

Company stack is .NET 8. Goal: enough genuine backend depth to
take production work.

**Non-optional, month 6 of Phase 2:** volunteer for a real
production backend ticket at work. This is not a study node and
it is not optional. If `PROGRESS.md` shows deep Phase 2 hours
without that ticket, the agent reminds you. Everything else is
study; that ticket is the career-changing move.

Gate **G-2**: all twelve primary at `depth_2_solid`. Unlocks Phase 3.

Nodes below are titles and scope only. Full `CURRICULUM.yaml`
specs are generated at G-1, not now.

| Id | Title | Scope | Effort |
|---|---|---|---|
| P2-M01 | C# and the CLR | Types, memory, generics, spans; not “C# for JS devs” tourism. | 30–45h |
| P2-M02 | ASP.NET Core pipeline | Host, middleware, DI, request lifetime. | 25–40h |
| P2-M03 | Async in .NET | `async`/`await`, sync-over-async, channels, vs the JS event loop. | 25–40h |
| P2-M04 | EF Core and data access | Change tracking, queries, migrations; pair with S1-08. | 30–45h |
| P2-M05 | Configuration, Options, secrets | `IOptions`, environments, what must never be in source. | 15–25h |
| P2-M06 | Testing .NET | xUnit, TestServer, integration vs unit; contract tests. | 25–40h |
| P2-M07 | AuthN / AuthZ | Cookies, JWT, policies, the work app’s actual scheme. | 25–40h |
| P2-M08 | HTTP APIs | Minimal APIs, versioning, validation, problem details. | 20–35h |
| P2-M09 | Background work and messaging | Hosted services, queues, outbox; delivery guarantees. | 25–40h |
| P2-M10 | Diagnostics and performance | `dotnet-trace`/`dump`, allocations, thread pool. | 25–40h |
| P2-M11 | Production hardening | Health, shutdown, config, observability hooks. | 20–30h |
| P2-M12 | Read and change the work backend | Navigate the real solution; a change you could PR. | 30–50h |

---

## Phase 3 — Distributed systems + Go (primary, 10 nodes)

Gate **G-3**. Unlocks Phase 4.

| Id | Title | Scope | Effort |
|---|---|---|---|
| P3-M01 | Go language | Idiomatic Go; modules, interfaces, errors. | 30–45h |
| P3-M02 | Go concurrency | Goroutines, channels, memory model; vs JS and .NET. | 30–45h |
| P3-M03 | Networking in Go | HTTP, gRPC, context cancellation. | 20–35h |
| P3-M04 | Failure, time, and consistency | Partial failure, retries, clocks, what “consistent” meant. | 25–40h |
| P3-M05 | Coordination | Leader election, leases, consensus at a usable level. | 25–40h |
| P3-M06 | Delivery guarantees | At-least/at-most/exactly-once; idempotency; outbox. | 20–35h |
| P3-M07 | Data for distributed systems | Replication, partitioning, what your DB already does. | 25–40h |
| P3-M08 | Observability under failure | Trace across services; debug from signals only. | 20–30h |
| P3-M09 | Capstone: a small distributed system | Real processes, real failure, tests that catch it. **Capstone.** | 50–80h |
| P3-M10 | Load and correctness | Fault injection, invariants, when to stop. | 20–35h |

---

## Phase 4 — Cloud / K8s / AWS (primary, 12 nodes)

AWS budget **$10/mo max**; LocalStack otherwise.

Gate **G-4**. Unlocks Phase 5.

| Id | Title | Scope | Effort |
|---|---|---|---|
| P4-M01 | AWS account, IAM, budget alarms | Org/account shape; never a surprise bill. | 15–25h |
| P4-M02 | VPC and networking | Subnets, routing, security groups, what TLS does not solve. | 25–40h |
| P4-M03 | Compute: ECS and/or Lambda | Run something cheap; know the trade. | 20–35h |
| P4-M04 | Storage: S3, RDS, backups | Durability vs availability; restore tested. | 20–35h |
| P4-M05 | Kubernetes fundamentals | Pod, ReplicaSet, Deployment, Service — by building, not clicking. | 30–45h |
| P4-M06 | K8s networking and ingress | DNS, kube-proxy, ingress, NetworkPolicy. | 25–40h |
| P4-M07 | Workloads, config, secrets | Probes, resources, ConfigMap/Secret, rolling updates. | 20–35h |
| P4-M08 | GitOps / CD onto the cluster | A pipeline you trust; rollback. | 20–35h |
| P4-M09 | Cloud observability | Metrics, logs, traces on the cheap. | 20–30h |
| P4-M10 | Cost and capacity | Rightsizing; the $10 constraint as a design rule. | 12–20h |
| P4-M11 | Cloud security baseline | IAM least privilege, public exposure, supply chain at deploy time. | 20–35h |
| P4-M12 | Capstone: full platform | App + data + deploy + observe, budget-honest. **Capstone.** | 50–80h |

---

## Phase 5 — Security / SRE (primary, 10 nodes)

Gate **G-5**. Unlocks Phase 6.

| Id | Title | Scope | Effort |
|---|---|---|---|
| P5-M01 | Threat modelling | STRIDE (or equivalent) on a system you own. | 15–25h |
| P5-M02 | Application security | OWASP-class bugs in JS and .NET you can actually exploit-then-fix in a lab. | 30–45h |
| P5-M03 | Auth protocols | OAuth/OIDC, cookies vs bearer, confusion attacks at a conceptual level. | 25–40h |
| P5-M04 | Secrets and supply chain | Signing, SBOMs, dependency risk. | 20–30h |
| P5-M05 | SLOs and error budgets | SLI/SLO on something with real traffic or a honest simulation. | 20–30h |
| P5-M06 | Incident response | Roles, comms, severity; a game-day. | 15–25h |
| P5-M07 | On-call and runbooks | A runbook you would follow half-asleep. | 15–25h |
| P5-M08 | Load, capacity, degradation | Load tests; what you shed first. | 20–35h |
| P5-M09 | Chaos and resilience | Inject failure; assert invariants. | 20–35h |
| P5-M10 | Postmortems and reliability culture | Blameless write-up of a real or staged incident. | 12–20h |

---

## Phase 6 — Leadership (primary, 6 nodes)

Gate **G-6** (curriculum complete, not “done learning”).

| Id | Title | Scope | Effort |
|---|---|---|---|
| P6-M01 | Staff-shaped scope | What you own vs what you influence; a real proposal at work. | 20–35h |
| P6-M02 | Technical strategy | Multi-quarter bets; killing work. | 20–30h |
| P6-M03 | Mentoring and review | Review as teaching; one person measurably better. | 20–30h |
| P6-M04 | Writing and talks | ADRs, RFCs, one external or internal talk. | 15–25h |
| P6-M05 | Influence without authority | Aligning teams; the meeting after the meeting. | 15–25h |
| P6-M06 | Hiring and levelling (as interviewee *and* interviewer) | Rubrics; the interview you wish you’d had. | 15–25h |

---

## Gates

| Gate | After | Pass requirement | Unlocks |
|---|---|---|---|
| G-1 | Phase 1 | P1-M01…P1-M09 all at `depth_2_solid`; exam in `docs/04-AGENTS.md` | Phase 2 graph + study |
| G-2 | Phase 2 | Twelve primary at `depth_2_solid`; same exam shape | Phase 3 |
| G-3 | Phase 3 | Ten primary at `depth_2_solid` | Phase 4 |
| G-4 | Phase 4 | Twelve primary at `depth_2_solid` | Phase 5 |
| G-5 | Phase 5 | Ten primary at `depth_2_solid` | Phase 6 |
| G-6 | Phase 6 | Six primary at `depth_2_solid` | — |

Exam shape (every gate): four rounds, weighted 25 / 30 / 25 / 20.
Pass = weighted ≥ 4.0 **and** no round < 3. See `docs/04-AGENTS.md`.

Phases 2–6 node specs are **not** in `CURRICULUM.yaml` until the
previous gate passes. Titles above are the intended shape so Phase 1
planning has a horizon; they will be rewritten by the version of you
that just passed the previous gate.
