# Governance Levels — Quick Reference

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

**These cannot be reduced by any governance_override in the Intent Spec.**  
See [hard-locks.md](hard-locks.md) for the complete list.

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

*GALDUR v0.9 · © 2026 Yggnet Labs s.r.o. · getgaldur.com · MIT License (templates)*