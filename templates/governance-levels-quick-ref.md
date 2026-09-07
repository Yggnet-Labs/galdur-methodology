# Governance Levels — Quick Reference

*GALDUR v0.95 · one level per spec, chosen explicitly and justified in `governance_level_reason`.*

## L0 — Autonomous

**Agent executes, logs, continues. Human is notified async.**

When to use:
- Read-only operations (queries, analysis, monitoring)
- Isolated changes (single file, test, log)
- Easily reversible (undone in < 5 minutes, no side effects)
- Low blast radius

Examples: unit tests, README, isolated bug fix, log rotation, read-only analysis, reporting

Human touchpoint: Drift Signal — async, does not stop flow.

---

## L1 — Supervised

**Agent executes → output passes Validation Gate before deploy.**

When to use:
- Changes affecting multiple modules or dependencies
- Staging deployments
- Additive operations (new features, additive DB migrations)
- Changes reviewable before they go live

Examples: new feature, staging deploy, additive DB migration, OS patch (non-prod), documentation

Human touchpoint: Curator reviews and approves — or returns for revision.

---

## L2 — Collaborative

**Agent plans → human approves the plan → agent executes.**

When to use:
- Production environment changes
- Changes with significant blast radius
- External parties involved (customer, partner)
- Partially reversible or high-impact actions

Examples: prod deploy with a verified rollback, internal API breaking change, non-destructive prod config change, migration with tested rollback

*Not L2:* destructive DB migrations, prod firewall changes, customer-facing e-mail — these sit in the domain hard minima / Hard Locks below and are human-executed (L3/HARD).

Human touchpoint: Approval required BEFORE execution.

---

## L3 — Manual

**Human executes, agent assists.**

When to use:
- Hard Lock categories (see hard-locks-quick-ref.md)
- Irreversible actions
- Legal or financial commitments
- Security-critical operations

Examples: IAM changes, payment/billing logic, cryptography, incident containment, signing contracts

Human touchpoint: Every step must be explicitly triggered by the human.

---

## HARD — Absolute Locks

**Cannot be reduced by anything in the Intent Spec.** A locked action is always executed by a human; approval unlocks the *continuation of the spec*, it does not free the agent's hands (v0.95).  
See [hard-locks-quick-ref.md](hard-locks-quick-ref.md) for the complete list.

---

## v0.95 rules that change how you pick a level

- **Per-spec, not per-task.** One spec = one governance level for all its tasks. Mixed sensitivity (docs + DB migration)? Split into two specs linked with `depends_on`. There is no per-task `governance_override` in v0.95 (roadmap v1.x).
- **Untrusted inputs raise the level by one.** A spec that consumes e-mail, web content, uploads or another agent's output declares `trust_boundary: external` → L0 becomes L1, L1 becomes L2 (prompt-injection defence, ch. 10).
- **Loops (AM-1).** `execution_mode: loop` needs the runtime contract (max_iterations, completion_promise, evaluator ≠ worker, loop_budget); a separate evaluator is mandatory from L1 upward.
- **Acceptance is read-only for the agent (AM-2).** Changing criteria or tests is a drift event `constraint_breach`; in a loop it suspends the spec.

---

## Decision Tree — Which Level? (Appendix C of the methodology)

**First check the domain governance matrix and the Hard Locks (ch. 06 and 10) — their minimum takes precedence over this orientation tree.**

```
Is the action reversible within 60 minutes without data loss?
├── NO  → L3 (Manual), unless the domain matrix names a Hard Lock or explicitly another level
└── YES → Does the blast radius reach beyond a single spec / service?
          ├── YES → L2 (Collaborative) — a human approves the plan
          └── NO  → Does the action touch the production environment?
                    ├── YES → at least the level set by the domain matrix (ch. 06)
                    └── NO  → Is the agent calibrated (< 15 drift events / 100 specs)?
                              ├── YES → L0 (Autonomous) — async Drift Signal
                              └── NO  → L1 (Supervised) — Validation Gate before deploy
```

The tree mirrors the calibration logic of ch. 06; per-domain thresholds, multi-layer escalation and level-specific policies are in ch. 06 and ch. 10.

**When in doubt: choose higher.** The drift log will show if you were too strict — that is correctable. An incident from too low a level may not be.

---

## CANNOT BE REDUCED (domain defaults)

| Domain | Hard Locks (human-executed, cannot be reduced) |
|---|---|
| Dev | DB destructive · Auth · Cryptography · Payments · External communication |
| Infra | Restore to prod · Decommission without backup verification · Prod SSL/TLS without downtime coordination |
| Database | Prod restore · UPDATE without WHERE > 10K rows · Replication config |
| Network | DNS prod (A, MX, NS) · Core switch · VPN prod config |
| Security | Incident containment · Audit log manipulation · Prod firewall |
| Sales | Sending offers to customers · Accepting commitments (prices, deadlines) |
| Legal | Sending contracts · Signing, accepting or rejecting · Regulatory filing |
| Finance | Any payment · Banking or payment system access |

Hard Locks cannot be reduced by any `governance_override` or Amendment. The agent never executes a locked action — after an explicit real-time approval by the Intent Architect, a human performs it; the approval unlocks the continuation of the spec, not the agent's execution. Every such use is a Hard Lock incident with a mandatory Trace Audit (ch. 10).

---

*GALDUR v0.95 · © 2026 Yggnet Labs s.r.o. · getgaldur.com · MIT License (templates)*