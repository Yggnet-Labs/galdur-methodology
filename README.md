# GALDUR

**A methodology for hybrid teams of people and AI agents.**

GALDUR is a governance methodology for building and operating software when part of
the delivery is done by autonomous AI agents. Where Scrum, SAFe or Waterfall treat AI
as just another tool, GALDUR treats agents as *acting participants* — and gives teams
the intent contracts, autonomy levels, hard locks and audit trail to stay in control.

- **7 principles · autonomy levels L0–L3 · 11 domains**
- **Current release: v0.95** — seven amendments since v0.9 (AM-1 Loop Execution Mode, AM-2 tamper-resistant acceptance, AM-3 machine pre-gate, AM-4 longitudinal drift in loops, AM-5 five separate Spec Health indicators, AM-6/AM-7 record patches). Full changelog and amendment log are at the end of the methodology.
- Web & methodology (buy / download / community): **https://getgaldur.com**
- Author: Vladimír Šedivý · **Yggnet Labs s.r.o.**

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

Appendices A–C of the methodology are strict subsets of `intent-spec-dev.yaml`,
`intent-spec-ops.yaml` and `governance-levels-quick-ref.md`: every field printed in the
book exists in the template under the same name, so a spec written from the book
validates against the template and vice versa.

## Community

Questions, feedback and contributions are welcome via GitHub Discussions and at
[getgaldur.com](https://getgaldur.com). Contributions to the methodology are credited in
the next release.

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
