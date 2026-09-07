# Hard Locks — Quick Reference

Hard Locks are categories of actions that **an agent never performs**, regardless of any instructions in the Intent Spec. When such an action is needed, a human performs it after explicit real-time approval by the Intent Architect.

These locks are implemented in the governance engine — the agent cannot override them, the curator cannot delegate them.

**Semantics (v0.95, unified):** a locked action is executed by a human, never by the agent. A human *approval* unlocks the continuation of the spec — it does not hand the locked action back to the agent. Editing acceptance criteria or tests is **not** a Hard Lock but a drift event `constraint_breach` (AM-2); in loops it suspends the spec.

---

## Universal Hard Locks — all domains, no exceptions

| Category | Specific Prohibitions |
|---|---|
| **Credentials & Secrets** | Handling private keys/passwords/API keys in plain-text · Writing secrets to logs or DB without encryption · Rotating prod credentials without rollback plan |
| **Destructive DB Operations** | DELETE without WHERE on production DB · DROP TABLE/DATABASE in production · TRUNCATE prod tables · Overwriting production backups |
| **Identity & Access** | Any IAM/permissions change without human approval · Creating or deleting admin/root account · SSH key into authorized_keys on prod server |
| **Critical Infrastructure** | Changing core routing tables or BGP · Changing prod firewall rules (allow or deny) · Shutdown/restart of critical prod server without change window |
| **External Communication** | Email/notification to >10 recipients · Webhook to external system with PII · Communication implying organisational commitment |
| **Payments & Compliance** | Manipulating payment logic or billing data · Exporting PII without GDPR audit trail · Deleting data subject to retention policy |

---

## Infrastructure Hard Locks

```
🔴 Restore from backup to production
🔴 Server decommission without data backup verification
🔴 Production SSL/TLS config change without downtime coordination
```

## Database Hard Locks

```
🔴 Restore backup to production DB
🔴 Any UPDATE without WHERE on prod table > 10K rows
🔴 DB replication configuration change
```

## Network Hard Locks

```
🔴 DNS record change/deletion for prod domains (A, MX, NS)
🔴 Core switch configuration change
🔴 Any VPN config change affecting prod traffic
```

## Security Hard Locks

```
🔴 Incident response containment (system isolation, IP blocking)
🔴 Deletion or modification of audit logs
🔴 Any exploit attempt (including authorised pen test without explicit spec)
```

## Knowledge Domain Hard Locks (Sales, Marketing, Legal, Finance)

```
🔴 Any communication to external party containing prices, deadlines, or commitments
🔴 Signing, accepting or rejecting a contract
🔴 Sending contract to counterparty
🔴 Any regulatory filing
🔴 Initiating a payment of any amount
🔴 Accessing banking or payment systems
🔴 Press release, crisis communication
🔴 Any HR communication regarding offers, rejections, terminations
```

## Physical Agent Hard Locks (Robotics)

```
🔴 Movement when person detected in safety zone (without explicit override)
🔴 Exceeding force limit (hardware)
🔴 Disabling emergency stop
🔴 Handling biological/chemical/radioactive materials without L3 + certified protocol
🔴 Restricting movement or exit of a person from space (anti-trapping)
```

---

## What happens when a Hard Lock is triggered

1. Agent **immediately stops** execution
2. Spec transitions to `ESCALATED:hard_lock` state
3. Governance Steward receives **immediate notification** (not async Drift Signal)
4. Incident written to separate Hard Lock Incident Log
5. Spec **cannot continue** without explicit Intent Architect approval
6. Hard Lock incident **always reviewed** at next Trace Audit

---

## Hard Lock incident is not a failure

The purpose of Hard Locks is to protect the system **and** the Curator. An agent triggering a Hard Lock means the system is working correctly. The postmortem question is always: "Where did the system fail?" — not "Who failed?"

---

*GALDUR v0.95 · © 2026 Yggnet Labs s.r.o. · getgaldur.com · MIT License (templates)*