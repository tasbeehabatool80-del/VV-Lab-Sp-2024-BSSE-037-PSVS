# Polar Seed Vault System (PSVS): Requirements Verification

> Configuration-managed requirements baseline and defect analysis for a polar seed vault, prepared for the Verification and Validation lab.

![Scope](https://img.shields.io/badge/scope-requirements%20analysis-blue)
![Baseline](https://img.shields.io/badge/baseline-PSVS--REQ--v1.0-green)
![Defects](https://img.shields.io/badge/defects%20logged-47-orange)
![Cross-requirement](https://img.shields.io/badge/cross--requirement-12-red)

---

## Table of Contents

1. [Overview](#1-overview)
2. [The Scenario](#2-the-scenario)
3. [Baseline Requirements](#3-baseline-requirements)
4. [Repository Structure](#4-repository-structure)
5. [Deliverables](#5-deliverables)
6. [Defect Analysis Method](#6-defect-analysis-method)
7. [Results](#7-results)
8. [Key Findings](#8-key-findings)
9. [Configuration Management](#9-configuration-management)
10. [How to Use This Repository](#10-how-to-use-this-repository)
11. [Scope and Roadmap](#11-scope-and-roadmap)

---

## 1. Overview

This repository holds the first stage of a verification and validation exercise on the **Polar Seed Vault System (PSVS)**. It contains:

- **Configuration management:** a frozen requirements baseline, a tagged release, a branch-and-merge workflow, and a change-request process.
- **Defect analysis:** a defect taxonomy and a defect log recording every problem found in the twelve informal requirements (S1-S12).

The goal of this stage is to find, classify and record the weaknesses in the informal requirements **before** any formal modelling begins. Fixing a requirement defect early is far cheaper than fixing it after a design has been built on it.

## 2. The Scenario

A polar vault stores sealed boxes of crop seeds deposited by registered institutions (gene banks, universities, governments). Each box holds seed samples of one species. The vault has several freezer chambers, and staff handle deposits, withdrawals, and monitoring. Depositors keep ownership of their boxes. The vault is a **custodian**, not an owner.

| Term | Meaning in this project |
|------|-------------------------|
| **Depositor** | A registered institution that sends seed boxes to the vault and owns them |
| **Box** | A sealed container holding seed samples of one species |
| **Chamber** | One freezer room in the vault, with its own capacity and temperature |
| **Custodian** | The vault's role: it looks after boxes but never owns them |
| **Vault authority** | The body that can act in an emergency |

## 3. Baseline Requirements

The baseline is **`PSVS-REQ-v1.0`** (tag `baseline-1`). It is kept exactly as given and is never edited.

| ID | Requirement |
|----|-------------|
| S1 | The system shall accept seed boxes only from registered depositors. |
| S2 | Each chamber can hold a large number of boxes. |
| S3 | Chambers 1-3 hold at most 50,000 boxes each; Chamber 4 holds at most 20,000. |
| S4 | A box belongs to exactly one depositor, and only that depositor may withdraw it. |
| S5 | In an emergency, the vault authority may release any box to any requesting party. |
| S6 | Boxes shall be stored at a safe temperature. |
| S7 | Chamber temperature shall never rise above -18°C. |
| S8 | During maintenance, a chamber may be warmed to 0°C. |
| S9 | Seed samples with low viability shall be flagged promptly for regeneration. |
| S10 | A depositor may withdraw at most 20% of its boxes of a species per year. |
| S11 | A withdrawn box may be redeposited only after re-inspection. |
| S12 | The system shall keep a good audit trail of all actions. |

Full document: [`requirements/PSVS-REQ-v1.0.md`](requirements/PSVS-REQ-v1.0.md)

## 4. Repository Structure

```
.
├── README.md
├── requirements/
│   ├── README.md
│   ├── PSVS-REQ-v1.0.md               # frozen baseline (tag: baseline-1)
│   └── change-request-template.md     # ID, artifact, reason, impact, approver
├── defect-logs/
│   ├── README.md
│   ├── defect-taxonomy.md             # 8 categories, severity scale, status values
│   ├── defect-log.md                  # 47 defects with evidence and suggested fixes
│   └── peer-review-comparison.md      # classmate comparison and detection rate
├── reports/
│   ├── README.md
│   ├── defect-summary.md              # counts by category and severity
│   └── defect-summary-chart.png       # chart
├── abstractions/                      # reserved for later lab stages
├── models/                            # reserved for later lab stages
├── operations/                        # reserved for later lab stages
├── constraints/                       # reserved for later lab stages
└── proofs/                            # reserved for later lab stages
```

| Folder | Purpose | Status |
|--------|---------|--------|
| [`requirements/`](requirements/) | Requirement versions and change-control template | Active |
| [`defect-logs/`](defect-logs/) | Taxonomy, defect log, peer review | Active |
| [`reports/`](reports/) | Summary tables and charts | Active |
| `abstractions/`, `models/`, `operations/`, `constraints/`, `proofs/` | Later lab stages | Reserved |

## 5. Deliverables

| # | Deliverable | Location |
|---|-------------|----------|
| 1 | Baseline requirements `PSVS-REQ-v1.0`, tagged `baseline-1` | [`requirements/PSVS-REQ-v1.0.md`](requirements/PSVS-REQ-v1.0.md) |
| 2 | Change-request template | [`requirements/change-request-template.md`](requirements/change-request-template.md) |
| 3 | Defect taxonomy (8 categories) | [`defect-logs/defect-taxonomy.md`](defect-logs/defect-taxonomy.md) |
| 4 | Defect log (47 defects) | [`defect-logs/defect-log.md`](defect-logs/defect-log.md) |
| 5 | Peer-review comparison and detection rate | [`defect-logs/peer-review-comparison.md`](defect-logs/peer-review-comparison.md) |
| 6 | Summary table and chart | [`reports/defect-summary.md`](reports/defect-summary.md) |

## 6. Defect Analysis Method

### 6.1 Inspection approach

1. **Single-requirement pass:** each of S1-S12 was read on its own and checked against every category in the taxonomy.
2. **Cross-requirement pass:** requirements that discuss the same concept (temperature, ownership and withdrawal, capacity, quota, logging) were read together to find conflicts and gaps that a single-requirement pass cannot see.
3. **Recording:** every defect was logged with evidence quoted from the baseline and a suggested fix.
4. **Peer review:** the log is compared with a classmate's log to measure detection rate.

### 6.2 Taxonomy

| Category | Definition (short) |
|----------|--------------------|
| **Ambiguity** | Can be read in more than one way |
| **Vagueness** | Uses an imprecise term with no clear boundary |
| **Incompleteness** | A needed case, actor, condition or requirement is missing |
| **Contradiction** | Two statements cannot both be true |
| **Non-verifiability** | No practical test can show it is met |
| **Redundancy** | The same information is stated more than once |
| **Infeasibility** | Cannot be met in practice as written |
| **Untraceability** | No source, rationale or link to other artifacts |

Definitions and examples: [`defect-logs/defect-taxonomy.md`](defect-logs/defect-taxonomy.md)

### 6.3 Severity scale

| Severity | Meaning |
|----------|---------|
| **High** | Could lead to an unsafe or wrong system, or blocks implementation. Must be resolved before modelling. |
| **Medium** | Different readers would build different behaviour, or an important case is missing. |
| **Low** | Style or maintainability issue. |

### 6.4 Defect log columns

`Defect ID | Req ID | Category | Description | Evidence | Severity | Suggested fix | Status`

A defect is **cross-requirement** when its *Req ID* names two or more requirements (for example `S4, S5`).

## 7. Results

### 7.1 Summary

| Measure | Value |
|---------|------:|
| Requirements inspected | 12 |
| Defects logged | **47** |
| Cross-requirement defects | **12** |
| Taxonomy categories used | 8 of 8 |
| High / Medium / Low severity | 14 / 30 / 3 |
| Defects currently open | 47 |

### 7.2 Defects by category and severity

| Category | High | Medium | Low | **Total** |
|----------|-----:|-------:|----:|----------:|
| Ambiguity | 4 | 9 | 0 | **13** |
| Vagueness | 4 | 1 | 0 | **5** |
| Incompleteness | 4 | 12 | 0 | **16** |
| Contradiction | 2 | 1 | 0 | **3** |
| Non-verifiability | 0 | 4 | 0 | **4** |
| Redundancy | 0 | 0 | 2 | **2** |
| Infeasibility | 0 | 2 | 0 | **2** |
| Untraceability | 0 | 1 | 1 | **2** |
| **Total** | **14** | **30** | **3** | **47** |

![Defects by category and severity](reports/defect-summary-chart.png)

### 7.3 Defects per requirement

A cross-requirement defect is counted once for each requirement it names.

| S1 | S2 | S3 | S4 | S5 | S6 | S7 | S8 | S9 | S10 | S11 | S12 |
|---:|---:|---:|---:|---:|---:|---:|---:|---:|----:|----:|----:|
| 3 | 4 | 7 | 3 | 8 | 4 | 3 | 5 | 5 | 7 | 5 | 5 |

## 8. Key Findings

### 8.1 Contradictions between requirements

| Defect | Requirements | Problem | Proposed resolution |
|--------|--------------|---------|---------------------|
| D16 | S4 vs. S5 | Only the owner may withdraw (S4), yet the authority may release any box to anyone in an emergency (S5). | State that S5 overrides S4 during a declared emergency. |
| D28 | S7 vs. S8 | Temperature must never exceed -18°C (S7), yet maintenance allows 0°C (S8). | Temperature is at most -18°C unless the chamber is in maintenance mode. |
| D26 | S6 vs. S8 | Warming to 0°C may not be a "safe temperature" (S6). | Apply S6 outside maintenance windows and define handling of boxes during maintenance. |

### 8.2 Highest-risk gaps

- **Undefined emergency (D17, D18, D20):** nothing says what an emergency is, who declares it, or who may receive boxes. This is the largest security and ownership risk.
- **Unbounded maintenance (D29):** no authorisation, duration limit or rule for boxes inside a warming chamber.
- **No full-chamber behaviour (D09):** capacity is stated, but the response to a deposit into a full chamber is not.
- **Unmeasurable terms (D23, D31, D44):** "safe temperature", "low viability" and "good audit trail" have no numeric or testable definition.
- **Undefined time and quota basis (D36, D37, D38):** "per year" and "20% of its boxes" are ambiguous, and small depositors can never withdraw a box under a literal reading.

### 8.3 Most affected requirements

**S5** has the most defects (8) and the most High-severity ones. **S3** and **S10** follow with 7 each. Incompleteness and ambiguity make up most defects, so the requirements mainly lack detail rather than being factually wrong.

## 9. Configuration Management

### 9.1 Branching model

- **`main`** holds stable, reviewed work.
- Work is done on a **topic branch** and merged with a merge commit (`--no-ff`), so history shows where each piece of work came from.
- The defect analysis was done on the **`defect-analysis`** branch and merged into `main`.

### 9.2 Tags and baselines

| Tag | Meaning |
|-----|---------|
| `baseline-1` | `PSVS-REQ-v1.0`: the original informal requirements, frozen |

A tagged baseline is never edited. Any change produces a new version file.

### 9.3 Commit convention

```
<artifact or area>: <what changed>
```

Examples: `defect-logs: add defect taxonomy`, `requirements: add change-request template`.

### 9.4 Change control

All changes to a baselined artifact need a change request recording these fields. Template: [`requirements/change-request-template.md`](requirements/change-request-template.md)

| Field | Purpose |
|-------|---------|
| **ID** | Unique, sequential identifier (CR-001, CR-002, ...) |
| **Artifact** | The exact file and item being changed |
| **Reason** | Why, with the related defect IDs |
| **Impact** | What else is affected, with effort and risk |
| **Approver** | Who authorises the change |

### 9.5 Commit history

```
*   Merge branch 'defect-analysis' into main
|\
| * reports: add defect summary table, chart and peer-review template
| * defect-logs: add defect log for PSVS-REQ-v1.0 (47 defects, 12 cross-requirement)
| * defect-logs: add defect taxonomy (8 categories, severity scale)
|/
* requirements: add change-request template
* PSVS-REQ-v1.0: add baseline informal requirements S1-S12   (tag: baseline-1)
* Initial commit: project structure, folder READMEs and main README
```

## 10. How to Use This Repository

**Read the work in this order:**

1. [`requirements/PSVS-REQ-v1.0.md`](requirements/PSVS-REQ-v1.0.md): what is being analysed
2. [`defect-logs/defect-taxonomy.md`](defect-logs/defect-taxonomy.md): how defects are classified
3. [`defect-logs/defect-log.md`](defect-logs/defect-log.md): the defects themselves
4. [`reports/defect-summary.md`](reports/defect-summary.md): the totals and chart

**Inspect the history:**

```bash
git log --oneline --graph --all --decorate   # full history with branch and merge
git tag -n                                   # list baselines
git show baseline-1                          # inspect the frozen baseline
git diff baseline-1 main --stat              # everything added since the baseline
```

**Check out the baseline exactly as frozen:**

```bash
git checkout baseline-1
```

## 11. Scope and Roadmap

This repository currently covers **repository setup and configuration management** and **requirements defect analysis**. The folders `abstractions/`, `models/`, `operations/`, `constraints/` and `proofs/` are reserved and will be filled in later lab stages, which will clarify the requirements and then specify and verify them formally. When a later stage resolves a logged defect, its status changes from **Open** to **Closed** with evidence.
