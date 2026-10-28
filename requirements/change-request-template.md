# Change Request Template

Copy this file to `requirements/change-requests/CR-<nnn>.md` for each change, and fill in every field.

| Field | Entry |
|-------|-------|
| **ID** | CR-001 *(unique, sequential)* |
| **Artifact** | *The exact file and item to change, e.g. `requirements/PSVS-REQ-v1.0.md`, requirement S7* |
| **Reason** | *Why the change is needed, e.g. defect D28 (S7 contradicts S8)* |
| **Impact** | *What else is affected: other requirements, models, proofs, tests, reports. Give the effort and risk (Low/Medium/High).* |
| **Approver** | *Name and role of the person who approves, e.g. Course instructor / Team lead* |

## Additional tracking (recommended)

| Field | Entry |
|-------|-------|
| Requested by | *name* |
| Date submitted | *YYYY-MM-DD* |
| Decision | *Approved / Rejected / Deferred* |
| Date decided | *YYYY-MM-DD* |
| New version created | *e.g. PSVS-REQ-v2.0* |
| Linked defect IDs | *e.g. D16, D28* |

## Worked example

| Field | Entry |
|-------|-------|
| **ID** | CR-001 |
| **Artifact** | `requirements/PSVS-REQ-v1.0.md`, requirement S7 |
| **Reason** | Defect D28: S7 ("never above -18 C") contradicts S8 ("may be warmed to 0 C") |
| **Impact** | Affects S7 and S8, the VaultState temperature invariant (Task 4) and StartMaintenance (Task 5). Risk: Medium. |
| **Approver** | Course instructor |
| Decision | Approved |
