# PROGRESS

Append-only. Never edit or reorder past entries. One entry per
completed session (= one node depth reached), regardless of how
many sittings it took.

Newest entries go at the **bottom**.

## Entry format

```markdown
## YYYY-MM-DD — {node-id} — {node title}
**Node:** {node-id} → {depth} reached
**Hours:** {n} ({m} sittings)
**Track:** primary | secondary | architecture | maintenance
**Done:** {concrete artifacts, not topics covered}
**Learned:** {the insight, in my own words}
**Confused about:** {open questions — never blank unless truly none}
**Confidence 1-5:** {n}
**Quiz:** {n}/10
**Next:** {specific next node or objective}
```

Non-session entries use these shapes:

```markdown
## YYYY-MM-DD — MAINTENANCE
**Hours:** 1
**Reviewed:** {topics}
**Decayed:** {what I'd forgotten}
**Resolved:** {open questions closed}
**Steer:** {pattern the agent called out}
**Next week:** {3 objectives}
```

```markdown
## YYYY-MM-DD — GATE G-{n}
**Result:** pass | conditional | fail
**Rounds:** written {n}/5 · debug {n}/5 · design {n}/5 · teach-back {n}/5
**Weighted:** {n}/5
**Misconceptions found:** {list}
**Remediation:** {nodes to redo, if any}
**Unlocked:** Phase {n}
```

---

<!-- entries begin below this line -->
