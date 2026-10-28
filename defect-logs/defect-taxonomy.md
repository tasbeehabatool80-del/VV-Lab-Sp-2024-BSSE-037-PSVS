# Defect Taxonomy

This taxonomy classifies the defects found in the informal requirements S1-S12 (PSVS-REQ-v1.0). It has **8 categories**, each with a definition and an example from the Polar Seed Vault System.

## Categories

| # | Category | Definition | Example (from S1-S12) |
|---|----------|-----------|-----------------------|
| 1 | **Ambiguity** | A statement that can reasonably be read in **two or more different ways**, so different readers build different systems. | S10: "per year" can mean a calendar year, a rolling 12 months, or a fiscal year. |
| 2 | **Vagueness** | A statement that uses an **imprecise term with no numeric or clear boundary**, so the requirement has no exact meaning. | S6: "safe temperature" (which temperature?). |
| 3 | **Incompleteness** | Something **necessary is missing**: an unstated case, condition, actor, error behaviour, or a needed requirement. | S3 gives capacity limits but never says what happens when a chamber is full. |
| 4 | **Contradiction** | Two requirements (or two parts of one) **cannot both be true** at the same time. | S7 ("never above -18 C") and S8 ("may be warmed to 0 C"). |
| 5 | **Non-verifiability** | A requirement for which **no practical test or measurement** can show it is met or not met. | S12: "a good audit trail" (no test can prove "good"). |
| 6 | **Redundancy** | The **same information is stated more than once** (or one statement is fully covered by another), creating a risk that the copies drift apart. | S2 ("a large number of boxes") is covered by the exact figures in S3. |
| 7 | **Infeasibility** | A requirement that **cannot be met in practice** (physically, logically, or with the other requirements) as written. | S10: 20% of 4 boxes is 0.8 of a box, so a small depositor can never withdraw anything. |
| 8 | **Untraceability** | A requirement with **no identifiable source, rationale, or link** to other requirements, design, or tests, so it cannot be followed forwards or backwards. | S9 needs viability testing and regeneration, but no requirement defines them. |

## How to spot each category (inspection hints)

- **Ambiguity:** Ask: "Could two engineers read this differently?"
- **Vagueness:** Look for words like safe, large, good, prompt, low, adequate.
- **Incompleteness:** Ask: "What if this fails or the limit is reached? Who does it? What is the outcome?"
- **Contradiction:** Compare requirements that talk about the same thing (temperature, withdrawal, ownership).
- **Non-verifiability:** Ask: "What test would I write? What is the pass/fail condition?"
- **Redundancy:** Look for statements that add no new constraint beyond another.
- **Infeasibility:** Try small, large, and extreme numbers; try doing all requirements at once.
- **Untraceability:** Ask: "Where does this come from? What implements it? What tests it?"

## Severity scale

| Severity | Meaning |
|----------|---------|
| **High** | Can cause a wrong or unsafe system (lost ownership control, seeds damaged, security hole), makes two requirements impossible together, or blocks implementation. Must be resolved before modelling. |
| **Medium** | Different readers would build different behaviour, or an important case is missing, but it does not by itself break safety. Should be resolved or recorded as an assumption. |
| **Low** | Style or maintainability issue (duplication, missing rationale). Fix when convenient. |

## Status values

| Status | Meaning |
|--------|---------|
| Open | Defect found, not yet resolved |
| In Progress | Clarification or change request under way |
| Closed | Resolved in a later requirements version, with evidence |
| Assumption | Cannot be answered; recorded as ASSUMPTION-n in v2.0 |

## Cross-requirement defects

A defect is **cross-requirement** when it only appears by reading two or more requirements together (for example S4 vs. S5, S7 vs. S8). In the defect log these have more than one ID in the *Req ID* column, such as `S4, S5`.
