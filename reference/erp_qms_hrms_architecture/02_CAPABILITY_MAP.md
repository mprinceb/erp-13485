# Capability Map

Status labels used here:

- `Exists now`: usable from repo truth today
- `Partial`: there is a real starting point but not enough for ISO 13485-style operation
- `Missing`: not meaningfully present

Decision labels:

- `ERP`: stay primarily in ERPNext transaction flow
- `qms extension`: extend existing `qms` app surface
- `HRMS`: use HRMS as the primary record
- `Bridge`: small cross-app orchestration and enforcement layer
- `New module`: add new doctypes and workflows not present today
- `Out of scope now`: defer

| Capability area | Current state | Evidence today | System of record in end state | Required action |
| --- | --- | --- | --- | --- |
| Document control | `Partial` | `QMS Document`, `Obsolete Document`, explorer/viewer, transition methods | `qms extension` | Activate wiring, normalize models, add controlled revision + acknowledgment |
| External document control | `Partial` | `External Origin Document` and report exist | `qms extension` | Add owner, expiry, impact, and linked change behavior |
| Change control | `Partial` | `Change Request Ticket`, `Change Management`, questionnaires, version-copy logic | `qms extension` | Add workflow authority, ERP impact links, implementation evidence |
| Organization / authority mapping | `Partial` | HRMS employee structure, department hierarchy, approver fields, and qms `Organization Chart` all exist, but are disconnected | `HRMS` for people structure plus `qms extension` for quality authority rules | Make HRMS the source for people and reporting lines; repurpose qms org model into a quality authority overlay |
| Training assignment | `Partial` | HRMS `Training Event` and `Training Result` exist; qms has no assignment model | `qms extension` plus `HRMS` | qms should own required training; HRMS should own event attendance and completion evidence |
| Read-and-understand acknowledgment | `Missing` | qms has activity logging only | `qms extension` | Add explicit acknowledgment records tied to document revision |
| Competency / qualification / recertification | `Partial` | HRMS `Skill` and `Skill Assessment` exist, but are not tied to controlled work or expiry | `qms extension` plus `HRMS` plus `Bridge` | Add competency requirements and qualification validity rules; optionally reuse HRMS skill evidence |
| Role gating for sensitive actions | `Missing` | No submit-time cross-app check today | `Bridge` read by `ERP` | Add one gate service that checks employee status, authority, training, and competency before sensitive actions |
| Supervisor / approver mapping | `Partial` | HRMS employee `reports_to`, approver fields, and `Department Approver` exist | `HRMS` | Reuse existing supervisor and department patterns; map quality approval roles in qms against HRMS persons or positions |
| Audit of who was qualified, current, or expired at the time of action | `Missing` | HRMS has lifecycle and shift history; ERP has transaction history; no qualification snapshot | `Bridge` plus `ERP` | Add immutable qualification check log or embed gate result snapshots on sensitive transactions |
| Onboarding / role change / offboarding impacts on training and authority | `Partial` | `Employee Onboarding`, `Employee Transfer`, and `Employee Separation` are real workflows | `HRMS` plus `Bridge` plus `qms extension` | Trigger training reassignment, authority review, and access revocation from lifecycle events |
| Supplier qualification / approved supplier control | `Partial` | ERPNext `Supplier Scorecard` and PO warn or block behavior exist | `ERP` plus `New module` | Add approved-supplier register and item-scope validation |
| Incoming inspection and receipt release | `Exists now` | ERPNext `Quality Inspection` and stock validation | `ERP` | Harden settings and add QMS links only where useful |
| In-process inspection / manufacturing hold points | `Partial` | `Job Card` launches in-process QI, not server-enforced | `ERP` plus `Bridge` | Add hold-point validation and operator-qualification checks |
| Final release / outgoing release | `Exists now` for transaction gating, `Partial` for authority and dossier | ERPNext stock and delivery release gates exist | `ERP` plus `Bridge` plus `New module` | Keep release in transactions; add authority check and release dossier packaging |
| Complaints | `Partial` | ERPNext `Issue`, `Warranty Claim`, `Maintenance Visit` exist | `ERP` plus `New module` | Extend intake fields and route into quality exceptions |
| Nonconformance | `Partial` | ERPNext `Non Conformance` exists but is lightweight | `ERP` plus `New module` | Expand NCR workflow and source-linkage |
| CAPA | `Partial` | ERPNext `Quality Action` exists but is lightweight | `ERP` plus `New module` | Add root cause, action ownership, effectiveness, closure rules |
| Traceability / DHR-like evidence assembly | `Partial` | ERPNext stores the chain, but not one assembled packet | `New module` | Add release dossier / DHR assembler |
| Service / post-delivery feedback | `Exists now` for trace, `Partial` for escalation | Warranty and maintenance traces exist | `ERP` plus `New module` | Keep service in ERP; route quality signals into complaint/NCR/CAPA |
| Internal audit | `Missing` | No audit doctypes in ERPNext or `qms` | `New module` | Add audit program, checklist, findings, follow-up |
| Management review | `Partial` | ERPNext quality review and meetings exist; qms has reports; HRMS has people and training data | `ERP` plus `qms extension` plus `HRMS` | Aggregate cross-domain metrics and produce one evidence pack |
| Design controls / DHF / DMR | `Missing` | No realistic design-control model in inspected apps | `Out of scope now` or `New module later` | Defer unless product-development scope is explicitly included |
| Risk / regulatory / RAE review touchpoints | `Partial` | Change questionnaires, external docs, support traces, organization data exist | `qms extension` plus `New module later` | Add review checkpoints; keep full risk/regulatory system out of phase 1 |

## Immediate Interpretation

- Keep release-critical transaction control in ERPNext.
- Make HRMS the authoritative people layer for active employees, org placement, reporting lines, and training event attendance.
- Turn `qms` into the governed knowledge, acknowledgment, competency-rule, and authority layer.
- Add a small bridge so HRMS lifecycle changes and qms qualification status can actually enforce ERP behavior.
