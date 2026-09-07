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

Examples: prod deploy, destructive DB migration, firewall changes, API breaking change, sending email to customer

Human touchpoint: Approval required BEFORE execution.

---

## L3 — Manual

**Human executes, agent assists.**

When to use:
- Hard Lock categories (see hard-locks.md)
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

## Decision Tree — Which Level?

```
Is the action reversible within 5 minutes without side effects?
├── YES → L0 candidate
│         Does it affect multiple modules or staging?
│         ├── YES → L1
│         └── NO  → L0
└── NO  → L2 candidate minimum
          Does it touch production or an external party?
          ├── YES + irreversible consequences → L3
          ├── YES                             → L2
          └── NO                             → back to reversibility check
                Is it a Hard Lock category?
                └── YES → L3/HARD — always human, no exceptions
```

**When in doubt: choose higher.** The drift log will show if you were too strict — that is correctable. An incident from too low a level may not be.

---

## CANNOT BE REDUCED (domain defaults)

| Domain | Hard minimum |
|---|---|
| Dev | DB destructive, Auth/session, Cryptography, Payments, External comms |
| Infra | Prod firewall, IAM changes, Prod data delete, Backup restore to prod |
| Network | DNS prod, Core routing, VPN prod config |
| Security | Incident containment, Audit log manipulation |
| Sales | Sending to customer, Accepting commitments |
| Legal | Sending contracts, Signing, Regulatory filing |
| Finance | Any payment, Banking system access |

---

*GALDUR v0.95 · © 2026 Yggnet Labs s.r.o. · getgaldur.com · MIT License (templates)*