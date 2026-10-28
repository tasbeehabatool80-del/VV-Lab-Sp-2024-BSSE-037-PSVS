# Defect Log for PSVS-REQ-v1.0

**Artifact inspected:** `requirements/PSVS-REQ-v1.0.md` (S1-S12)
**Method:** Manual inspection, requirement by requirement, then cross-checking requirements that talk about the same thing.
**Total defects:** 47  |  **Cross-requirement defects:** 12  |  **Categories used:** 8 of 8

Taxonomy and severity definitions: `defect-taxonomy.md`.

| Defect ID | Req ID | Category | Description | Evidence | Severity | Suggested fix | Status |
|-----------|--------|----------|-------------|----------|----------|---------------|--------|
| D01 | S1 | Incompleteness | 'Registered' is never defined. No requirement says who registers a depositor, what record is kept, or how the vault checks registration. | S1: "...only from registered depositors." | High | Add a requirement defining registration (approving body, registry record) and require the vault to check the registry on every deposit. | Open |
| D02 | S1 | Incompleteness | No behaviour is given for a depositor who is deregistered or suspended after depositing. It is unclear whether their boxes stay, and whether they may still withdraw them. | S1 only constrains acceptance of new boxes; S4 says the depositor owns the box for good. | Medium | State that deregistration never changes ownership of stored boxes, and say whether withdrawal is still allowed. | Open |
| D03 | S1 | Ambiguity | 'Accept ... from' does not say whether it also covers redeposits (S11), or boxes delivered by a courier or staff member on behalf of a registered depositor. | S1: "accept seed boxes only from registered depositors"; S11 talks about redeposit. | Medium | Define 'deposit request' with an explicit depositor identity, and state that S1 applies to Deposit and Redeposit. | Open |
| D04 | S2 | Vagueness | 'A large number of boxes' has no numeric value. | S2: "Each chamber can hold a large number of boxes." | Medium | Delete S2 (S3 already gives numbers) or replace it with a numeric minimum. | Open |
| D05 | S2 | Non-verifiability | No test can decide whether S2 is satisfied, because 'large' has no threshold. | S2: "a large number" | Medium | Rewrite as a measurable statement, e.g. 'Each chamber shall have a capacity of at least 20,000 boxes'. | Open |
| D06 | S2, S3 | Redundancy | S2 is already covered by the exact capacities in S3. Keeping both risks divergence, e.g. is Chamber 4 (20,000) 'large'? | S2: 'large number'; S3: 'at most 50,000 ... at most 20,000'. | Low | Merge S2 into S3 and remove S2. | Open |
| D07 | S2 | Untraceability | S2 has no stated source, rationale, or linked test or design element. Nothing can be traced back to it. | S2 is a bare sentence with no rationale or reference. | Low | Record source and rationale for each requirement in the requirements table. | Open |
| D08 | S3 | Ambiguity | It is unclear what counts toward a chamber's load: only stored boxes, or also withdrawn boxes awaiting re-inspection or quarantined boxes. | S3: "hold at most 50,000 boxes"; S11 implies boxes can be in states other than stored. | Medium | Define 'chamber load' = number of boxes whose status is stored (or stored+quarantined) and located in that chamber. | Open |
| D09 | S3 | Incompleteness | No behaviour is given when a chamber is full: is the deposit rejected, or sent to another chamber? | S3 gives upper bounds but no consequence for reaching them. | High | Add: a deposit into a full chamber shall be rejected with a 'chamber full' report. | Open |
| D10 | S3 | Incompleteness | Nothing says who or what chooses the chamber for a new box, or whether boxes can be moved between chambers (MoveBox). | S3 describes chambers but no requirement assigns boxes to chambers. | Medium | Add requirements for chamber assignment (by staff, as a deposit input) and for MoveBox. | Open |
| D11 | S3 | Incompleteness | Only Chambers 1-4 have limits, but the scenario says the vault has 'several' chambers. Any other chamber has no capacity. | S3: "Chambers 1-3 ... Chamber 4"; scenario: "several freezer chambers". | Medium | State that the vault has exactly four chambers, or give a default capacity for any other chamber. | Open |
| D12 | S3, S11 | Incompleteness | When a box is withdrawn, its slot may be taken by another deposit. A later redeposit could then find the chamber full, and no requirement says what happens. | S3 sets a hard limit; S11 allows redeposit but says nothing about space. | Medium | State whether a slot is reserved on withdrawal, or that redeposit is subject to the same capacity check as Deposit. | Open |
| D13 | S3, S8 | Infeasibility | Maintenance on a full chamber means moving up to 50,000 boxes, but the other chambers may have no spare room (170,000 total capacity). | S3: capacities; S8: chamber may be warmed (boxes would warm too). | Medium | Require a pre-maintenance check that the boxes can be relocated, or allow boxes to stay and add a maximum warming time. | Open |
| D14 | S4 | Incompleteness | No way to transfer ownership (merger, closure or renaming of an institution). 'Exactly one depositor' is permanent. | S4: "belongs to exactly one depositor" | Medium | Add a TransferOwnership operation, or state explicitly that ownership never changes. | Open |
| D15 | S4 | Incompleteness | Nothing says how the vault checks that a requester is the owning depositor (identity, authority to act for the institution). | S4: "only that depositor may withdraw it" | Medium | Add an authentication requirement; each request carries a depositor identity checked against the box owner. | Open |
| D16 | S4, S5 | Contradiction | S4 says only the owner may withdraw a box. S5 lets the authority release any box to any party in an emergency. Both cannot hold at once. | S4: "only that depositor may withdraw it"; S5: "release any box to any requesting party". | High | Make S4 'except under S5' and state a priority rule: during a declared emergency, S5 overrides S4. | Open |
| D17 | S5 | Ambiguity | 'Emergency' is not defined: which events qualify, who declares it, when it starts and ends. | S5: "In an emergency..." | High | Define emergency as a state declared by the vault authority (DeclareEmergency) and ended by EndEmergency. | Open |
| D18 | S5 | Ambiguity | 'Vault authority' is not defined: who it is, how it is identified, and whether one person is enough. | S5: "the vault authority may release..." | High | Define the vault authority as a named role and require its identity on DeclareEmergency and release requests. | Open |
| D19 | S5 | Ambiguity | 'Release' is not defined and differs from 'withdraw' in S4. Is it a withdrawal, a loan, or a transfer of ownership? | S4: "withdraw"; S5: "release". | Medium | Define 'release' as a withdrawal under S5 that keeps the original owner in the record. | Open |
| D20 | S5 | Vagueness | 'Any requesting party' is unbounded. It could be unregistered, hostile, or demand every box, and no limits or conditions are given. | S5: "any box to any requesting party" | High | Require the authority to approve each release, and name allowed recipient classes (e.g. registered depositors, national governments). | Open |
| D21 | S5, S10 | Ambiguity | Unclear whether an emergency release counts toward the 20% yearly quota or is exempt from it. | S5: "any box"; S10: "at most 20% ... per year". | Medium | State that emergency releases are exempt from S10 and are not counted against the quota. | Open |
| D22 | S5, S12 | Incompleteness | Emergency releases are the most sensitive actions, yet nothing says they must be logged with who approved them and why. | S5 has no logging statement; S12 only says 'a good audit trail'. | Medium | Require every emergency action to be logged with authority identity, recipient, timestamp, and reason. | Open |
| D23 | S6 | Vagueness | 'Safe temperature' has no value or range. | S6: "Boxes shall be stored at a safe temperature." | High | Define safe temperature numerically, e.g. 'at most -18 C' (link to S7). | Open |
| D24 | S6 | Non-verifiability | S6 cannot be tested or monitored, because 'safe' is undefined. | S6: "a safe temperature" | Medium | Express it as a measurable condition on chamber temperature (see S7). | Open |
| D25 | S6, S7 | Redundancy | S6 states the goal and S7 the concrete limit for the same concern. Two statements can drift apart (what if -18 C is not 'safe'?). | S6: "safe temperature"; S7: "never rise above -18 C". | Low | Keep S7 as the testable rule and make S6 its rationale. | Open |
| D26 | S6, S8 | Contradiction | S8 lets a chamber warm to 0 C. That is unlikely to be a 'safe' storage temperature, so S8 may break S6 while boxes are inside. | S6: "safe temperature"; S8: "warmed to 0 C". | Medium | Say that S6 applies outside maintenance windows, and define what happens to boxes during maintenance. | Open |
| D27 | S7 | Ambiguity | 'Temperature' is not defined: the chamber average, a single sensor, or the box. Measurement frequency, tolerance, and any lower limit are missing. | S7: "Chamber temperature shall never rise above -18 C." | Medium | Define temperature as the chamber sensor reading sampled at a fixed interval, and state if there is a lower bound. | Open |
| D28 | S7, S8 | Contradiction | S7 says the chamber must never be above -18 C. S8 allows warming up to 0 C. Both cannot be true. | S7: "never rise above -18 C"; S8: "may be warmed to 0 C". | High | Make S7 conditional: temp <= -18 C unless the chamber is in maintenance mode, in which case temp <= 0 C. | Open |
| D29 | S8 | Incompleteness | Maintenance has no controls: who authorises it, maximum duration, what happens to boxes inside, whether deposits or withdrawals are allowed, and what happens if an emergency starts during maintenance. | S8: "During maintenance, a chamber may be warmed to 0 C." | High | Add StartMaintenance/EndMaintenance with authorisation and maximum duration. Reject Deposit and Withdraw on a chamber in maintenance (except S5). | Open |
| D30 | S8 | Ambiguity | 'May be warmed to 0 C': is 0 C an upper limit or a required target? Can it go above 0 C? | S8: "may be warmed to 0 C" | Medium | State that temperature during maintenance shall not exceed 0 C. | Open |
| D31 | S9 | Vagueness | 'Low viability' has no threshold (e.g. germination below some percentage). | S9: "Seed samples with low viability..." | High | Define a viability threshold (e.g. germination rate below 85%); mark it as a configurable value. | Open |
| D32 | S9 | Non-verifiability | 'Promptly' has no time limit, so timeliness cannot be tested. | S9: "flagged promptly" | Medium | Set a limit, e.g. 'within 24 hours of the test result being recorded'. | Open |
| D33 | S9 | Incompleteness | Missing: who tests viability and how often, who is notified of a flag, what status a flagged box gets, and who does the regeneration. | S9: "flagged ... for regeneration" | High | Add requirements for periodic viability tests, notification to the owner, and a 'flagged' state of the box. | Open |
| D34 | S9 | Untraceability | S9 depends on viability testing and regeneration processes that no other requirement defines, so S9 cannot be traced to any operation. | No S-requirement mentions viability testing or regeneration. | Medium | Add the missing process requirements and link them to S9 in the traceability table. | Open |
| D35 | S9, S10 | Incompleteness | Regeneration needs seeds taken from a box. It is unclear whether that is a withdrawal (subject to S4 owner-only and S10 quota) and who authorises it. | S9: 'regeneration'; S4: 'only that depositor may withdraw'; S10: 'at most 20%'. | Medium | State whether regeneration is a special withdrawal, and whether it counts against the quota. | Open |
| D36 | S10 | Ambiguity | 'Per year' could be a calendar year, a rolling 12 months, or a fiscal year. | S10: "at most 20% ... per year" | High | Choose one time model (e.g. calendar year Jan 1 - Dec 31) and state it. | Open |
| D37 | S10 | Ambiguity | The base for '20% of its boxes' is unclear: boxes held at the start of the year, held now, or ever deposited. Mid-year deposits also change it. | S10: "20% of its boxes of a species" | Medium | Define the base as the number of boxes of that species held by the depositor at the start of the year. | Open |
| D38 | S10 | Infeasibility | A depositor with fewer than 5 boxes of a species can never withdraw one box (20% of 4 = 0.8), since fractions of a box do not exist. | S10: "at most 20%" | Medium | Add a rounding rule: allowance = max(1, floor(20% x base)), or state that small depositors are exempt. | Open |
| D39 | S10 | Incompleteness | Nothing says that boxes must be tagged with a species, or how species is recorded, though S10 depends on it (the scenario says it, S1-S12 do not). | S10: "boxes of a species" | Medium | Add a requirement that every box records exactly one species at deposit. | Open |
| D40 | S10, S11 | Incompleteness | After a withdrawn box is redeposited, it is unclear whether the quota is restored. | S10: yearly limit on withdrawals; S11: redeposit after re-inspection. | Medium | State that withdrawals count for the year even if the box is redeposited. | Open |
| D41 | S11 | Ambiguity | 'Re-inspection' is not defined: who inspects, what is checked, what counts as pass or fail. | S11: "only after re-inspection" | High | Define re-inspection as a recorded check by vault staff with a pass/fail result. | Open |
| D42 | S11 | Incompleteness | No outcome is given for a failed re-inspection (quarantine, discard, return), no time limit, and it is not stated who may redeposit. | S11 only covers the allowed case. | Medium | State that a failed box becomes quarantined and may not be stored, and that only the original owner may redeposit. | Open |
| D43 | S5, S11 | Ambiguity | It is unclear whether a box released in an emergency counts as 'withdrawn' under S11, and who may redeposit it. | S5: "release"; S11: "A withdrawn box". | Medium | State that S11 applies to emergency-released boxes and that only the original depositor or the authority may redeposit. | Open |
| D44 | S12 | Vagueness | 'Good audit trail' is subjective. No measurable quality is given. | S12: "a good audit trail" | High | Define the audit record fields (who, what, when, outcome) and make every action produce one. | Open |
| D45 | S12 | Ambiguity | 'All actions' is unclear: does it include failed or rejected attempts, read-only queries, sensor readings, or staff actions? | S12: "all actions" | Medium | List the logged action types explicitly, including rejected requests. | Open |
| D46 | S12 | Incompleteness | Missing: log contents, retention period, protection against tampering, and who may read the log. | S12 is one sentence. | Medium | Add requirements for log fields, retention (e.g. 10 years), append-only storage, and access control. | Open |
| D47 | S12 | Non-verifiability | 'Good' cannot be tested, so no one can show that S12 is met. | S12: "good audit trail" | Medium | Replace with a testable check such as 'for every state-changing operation there is exactly one log entry'. | Open |

## Cross-requirement defects (index)

| Defect ID | Requirements | Category |
|---|---|---|
| D06 | S2, S3 | Redundancy |
| D12 | S3, S11 | Incompleteness |
| D13 | S3, S8 | Infeasibility |
| D16 | S4, S5 | Contradiction |
| D21 | S5, S10 | Ambiguity |
| D22 | S5, S12 | Incompleteness |
| D25 | S6, S7 | Redundancy |
| D26 | S6, S8 | Contradiction |
| D28 | S7, S8 | Contradiction |
| D35 | S9, S10 | Incompleteness |
| D40 | S10, S11 | Incompleteness |
| D43 | S5, S11 | Ambiguity |

## Notes

- Status is **Open** for every entry. Entries are closed with evidence in Task 6 (PSVS-REQ-v3.0).
- Evidence quotes come from `PSVS-REQ-v1.0.md`. Where the evidence is the *absence* of a statement, this is said explicitly.
