# PSVS-REQ-v1.0: Polar Seed Vault System, Informal Requirements

**Version:** 1.0 (baseline, tag `baseline-1`)
**Status:** Frozen. These are the original informal requirements exactly as given in the lab handout. They are **not edited** here. Later versions (v2.0, v3.0) are separate files.

## Scenario

A polar vault stores sealed boxes of crop seeds deposited by registered institutions (gene banks, universities, governments). Each box holds seed samples of one species. The vault has several freezer chambers, and staff handle deposits, withdrawals, and monitoring. Depositors keep ownership of their boxes. The vault is a custodian, not an owner.

## Requirements

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

## Change control

This file is the baseline. It must not be modified after tagging. Any change goes through a change request (see `change-request-template.md`) and produces a new version file.
