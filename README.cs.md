# GALDUR

[English](README.md) · **Čeština**

[![Vydání](https://img.shields.io/github/v/release/Yggnet-Labs/galdur-methodology?display_name=tag)](https://github.com/Yggnet-Labs/galdur-methodology/releases)
[![Šablony: MIT](https://img.shields.io/badge/%C5%A1ablony-MIT-blue.svg)](LICENSE)
[![Metodika: CC BY 4.0](https://img.shields.io/badge/metodika-CC%20BY%204.0-lightgrey.svg)](LICENSE-DOCS)
[![Diskuse](https://img.shields.io/github/discussions/Yggnet-Labs/galdur-methodology)](https://github.com/Yggnet-Labs/galdur-methodology/discussions)

**Metodika pro hybridní týmy lidí a AI agentů.**

GALDUR je governance metodika pro vývoj a provoz softwaru, na kterém se podílejí
autonomní AI agenti. Zatímco Scrum, SAFe nebo Waterfall zacházejí s AI jako s
nástrojem, GALDUR pracuje s agenty jako s *jednajícími účastníky*. Týmům dává
kontrakty záměru, úrovně autonomie, tvrdé zákazy a auditní stopu, aby si udržely
kontrolu.

- **7 principů · úrovně autonomie L0–L3 · 11 domén**
- **Aktuální vydání: v0.95** — sedm dodatků od v0.9; úplný changelog a registr
  dodatků jsou na konci metodiky.
- Web, metodika a komunita: **https://getgaldur.com**
- Autor: Vladimír Šedivý · **Yggnet Labs s.r.o.**

## Začněte za 10 minut

1. Přečtěte si [sedm principů a úrovně governance](docs/index.html).
2. Zvolte nejnižší úroveň autonomie, která odpovídá riziku práce.
3. Zkopírujte do svého repozitáře Intent Spec z `templates/` (`dev`, `ops`
   nebo `loop`).
4. Vyplňte cíl, akceptační důkazy, povolené akce, Hard Locks a evaluátora.
5. Proveďte práci, uložte důkazy a po dokončení použijte šablonu Trace Audit.

Pokud si nejste jistí, začněte na L1 nebo L2. Hard Locks nejsou přepínače,
které lze schválením vypnout: agent zamčenou akci nikdy neprovede; po výslovném
schválení ji provede člověk.

## Co je v repozitáři

| Cesta | Obsah |
|---|---|
| `index.html` | Úvodní stránka GALDUR |
| `docs/` | Metodika česky (`docs/index.html`) a anglicky (`docs/en/index.html`) |
| `templates/` | Šablony v0.95: Intent Spec (dev / ops / loop), rychlé přehledy Governance Levels a Hard Locks, Trace Audit |
| `community/` | Komunitní rozcestník |
| `legal/` | Provozovatel a právní informace |
| `branding/` | Veřejné grafické podklady stránek |

## Použití šablon

Soubory v `templates/` jsou určené ke zkopírování do vlastních repozitářů a
přizpůsobení týmu. Přílohy A a B metodiky používají stejné názvy polí jako
`intent-spec-dev.yaml` a `intent-spec-ops.yaml`. Příloha C odpovídá
`governance-levels-quick-ref.md`.

## Komunita a příspěvky

Otázky a zkušenosti patří do [GitHub Discussions](https://github.com/Yggnet-Labs/galdur-methodology/discussions).
Konkrétní chyby nebo chybějící obsah hlaste přes issue šablony. Před příspěvkem
si přečtěte [CONTRIBUTING.md](CONTRIBUTING.md), [Code of Conduct](CODE_OF_CONDUCT.md)
a [SECURITY.md](SECURITY.md). Změny vydání shrnuje [CHANGELOG.md](CHANGELOG.md).

## Licence

Repozitář používá dvě licence podle druhu obsahu:

| Obsah | Licence |
|---|---|
| **Šablony** (`templates/*`) | **MIT** — viz [LICENSE](LICENSE). Lze používat, upravovat a šířit i komerčně. |
| **Metodika a dokumentace** (`docs/`, landing, community a legal stránky) | **CC BY 4.0** — viz [LICENSE-DOCS](LICENSE-DOCS). Při sdílení a úpravách je nutné uvést autora. |
| **Název a loga GALDUR** | Ochranné známky / duševní vlastnictví Yggnet Labs s.r.o.; licence výše se na ně nevztahují. |

Požadovaná citace dokumentace: *„Yggnet Labs s.r.o., getgaldur.com — Licensed
under CC BY 4.0“.* Autoritativní znění je v
[podmínkách užití](https://getgaldur.com/terms.html).

---

© 2026 Yggnet Labs s.r.o. · getgaldur.com
