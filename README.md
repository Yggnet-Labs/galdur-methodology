# GALDUR

**English** · [Čeština](README.cs.md)

[![Release](https://img.shields.io/github/v/release/Yggnet-Labs/galdur-methodology?display_name=tag)](https://github.com/Yggnet-Labs/galdur-methodology/releases)
[![Templates: MIT](https://img.shields.io/badge/templates-MIT-blue.svg)](LICENSE)
[![Methodology: CC BY 4.0](https://img.shields.io/badge/methodology-CC%20BY%204.0-lightgrey.svg)](LICENSE-DOCS)
[![Discussions](https://img.shields.io/github/discussions/Yggnet-Labs/galdur-methodology)](https://github.com/Yggnet-Labs/galdur-methodology/discussions)

**A methodology for hybrid teams of people and AI agents.**

GALDUR is a governance methodology for building and operating software when part of
the delivery is done by autonomous AI agents. Where Scrum, SAFe or Waterfall treat AI
as just another tool, GALDUR treats agents as *acting participants* — and gives teams
the intent contracts, autonomy levels, hard locks and audit trail to stay in control.

- **7 principles · autonomy levels L0–L3 · 11 domains**
- **Current release: v0.95** — seven amendments since v0.9 (AM-1 Loop Execution Mode, AM-2 tamper-resistant acceptance, AM-3 machine pre-gate, AM-4 longitudinal drift in loops, AM-5 five separate Spec Health indicators, AM-6/AM-7 record patches). Full changelog and amendment log are at the end of the methodology.
- Web & methodology (buy / download / community): **https://getgaldur.com**
- Author: Vladimír Šedivý · **Yggnet Labs s.r.o.**

## Start in 10 minutes

1. Read the [seven principles and governance levels](docs/en/index.html).
2. Choose the lowest autonomy level that matches the risk of the task.
3. Copy an Intent Spec from `templates/` (`dev`, `ops`, or `loop`) into your repository.
4. Fill in the objective, acceptance evidence, allowed actions, Hard Locks, and evaluator.
5. Run the work, capture the evidence, and use the Trace Audit template after completion.

Start with L1 or L2 if you are unsure. Hard Locks are not override switches: the agent
never performs a locked action; after explicit approval, a human performs it.

## What's in this repository

This is the public, community-facing bundle:

| Path | Content |
|------|---------|
| `index.html` | GALDUR landing page |
| `docs/` | GALDUR methodology — Czech (`docs/index.html`) and English (`docs/en/index.html`) |
| `templates/` | Ready-to-use templates (v0.95): Intent Spec (dev / ops / loop), Governance Levels & Hard Locks quick-refs, Trace Audit |
| `community/` | Community hub |
| `legal/` | Operator & legal information |
| `branding/` | Brand assets used by the pages |

## Using the templates

The files in `templates/` are meant to be copied into your own repositories and adapted
to your team — intent specs, hard-lock references and the trace-audit template. Fork,
adapt, and share back what works.

Appendices A and B of the methodology use the same field names as `intent-spec-dev.yaml`
and `intent-spec-ops.yaml`: every field printed in the book exists in the template under
the same name; the templates add optional fields (identification, task details; risk assessment is optional for dev and mandatory for ops, post-actions for ops).
Appendix C (the reference card) is harmonised with `governance-levels-quick-ref.md`. There is
no validation schema — the match is by field names, checked when the release is prepared.

## Community

Questions, feedback and contributions are welcome via GitHub Discussions and at
[getgaldur.com](https://getgaldur.com). Contributions to the methodology are credited in
the next release.

Before contributing, read [CONTRIBUTING.md](CONTRIBUTING.md), the
[Code of Conduct](CODE_OF_CONDUCT.md), and [SECURITY.md](SECURITY.md). Release changes
are summarized in [CHANGELOG.md](CHANGELOG.md).

## Licensing

GALDUR uses the same licensing as getgaldur.com — see the
[Terms of Use](https://getgaldur.com/terms.html) for the authoritative wording:

| What | License |
|------|---------|
| **Template payloads** (`templates/*` — Intent Spec, Governance Levels & Hard Locks quick refs, Trace Audit) | **MIT** — see [`LICENSE`](LICENSE). Free to use, adapt and redistribute, including commercially. |
| **Methodology & documentation** (`docs/`, landing, community and legal pages) | **CC BY 4.0** — see [`LICENSE-DOCS`](LICENSE-DOCS). Free to share and adapt with attribution: *"Yggnet Labs s.r.o., getgaldur.com — Licensed under CC BY 4.0"*. |
| **The GALDUR name and logos** | Trademarks / IP of Yggnet Labs s.r.o. — see the [Trademark Policy](https://getgaldur.com/trademark.html). Not covered by the licenses above. |

---

© 2026 Yggnet Labs s.r.o. · getgaldur.com
