# Gap Register

## High Priority Gaps

| Gap | Current evidence | End-state decision | Owner |
| --- | --- | --- | --- |
| qms automation is coded but not wired | hooks for scheduler, notifications, and doc events are commented | activate only the needed hooks and remove stale claims | `qms` extension |
| No governed training or read-and-understand control | qms has no training doctypes; HRMS training is generic | add training assignment, acknowledgment, competency, and revision-specific applicability | `qms` extension |
| No HRMS to qms lifecycle bridge | onboarding, transfer, separation, and training completion do not create quality state changes | add event-driven sync and review tasks | `Bridge` |
| qms `Organization Chart` risks duplicating HRMS org truth | qms has its own tree; HRMS already stores employee structure and reporting lines | convert qms org model into a quality authority overlay only | `qms` extension plus `Bridge` |
| No quality authority matrix tied to real employees | HRMS approver logic is HR-only; qms hierarchy is not quality-aware | add authority mapping linked to HRMS persons, positions, and effective dates | `qms` extension |
| No qualification-at-time-of-action evidence | ERP has transactions and HRMS has people history, but no gate snapshot | add qualification gate log or equivalent immutable check result | `Bridge` |
| No approved supplier by item scope | ERP has scorecard only | add approved-supplier register and PO validation | new module plus ERP validation |
| No complaint-quality escalation layer | `Issue` and `Warranty Claim` exist, but not quality-classified | extend intake records and route to NCR/CAPA | ERP extension plus new workflow |
| NCR and CAPA are not closed-loop | ERPNext quality doctypes are lightweight | extend NCR and CAPA fields and workflow | ERP extension |
| In-process hold points are not hard-gated | Job Card QI launch is UI-level | enforce hold-point validations on job card and manufacture output | ERP extension plus `Bridge` |
| No DHR / release dossier | ERP stores evidence but no assembled packet | add release dossier module | new module |
| No internal audit module | none in ERPNext, qms, or HRMS | add audit program, audit, findings | new module |
| qms has duplicate master doctypes and duplicate distribution models | duplicate doctypes and overlapping distribution patterns exist | consolidate before broader rollout | `qms` extension |
| qms report-model mismatch exists | document master list queries a field not defined in QMS Document JSON | fix model and report alignment early | `qms` extension |

## Medium Priority Gaps

| Gap | Current evidence | Decision |
| --- | --- | --- |
| HRMS training does not carry SOP revision identity | `Training Event` and `Training Result` are generic training records | keep HRMS for event evidence; keep revision-specific acknowledgment in qms |
| HRMS `Skill` and `Skill Assessment` are too light for regulated qualification | doctype exists but no expiry or process linkage | reuse only if helpful; do not make it the sole qualification engine |
| Department approver logic is HR-process-specific | current helper supports leave, expense, and shift flows | reuse the pattern, not the exact rule set |
| Shift and attendance data are not tied to controlled transactions | HRMS stores the records, ERP does not consume them for quality gating | use for audit support and optional shift-based checks later |
| Management review is fragmented across ERP, qms, and HRMS | each app has part of the data | add aggregated management review pack |
| External docs are controlled but not impact-linked | external docs exist, but process impact is thin | extend with owner, expiry action, and linked change |
| Change control is document-centric, not product-impact centric | change workflows exist but do not reach ERP objects cleanly | extend change records with ERP impact mapping |

## Out Of Scope For Early Phases

| Area | Reason |
| --- | --- |
| Full design controls / DHF / DMR | no current model in inspected apps; better as later dedicated module |
| Full risk-management file / FMEA loop | no current risk model in inspected apps |
| Regulatory reporting engine | jurisdiction-specific and not needed for first compliance-by-default slice |
| Full LMS replacement | HRMS already provides basic training-event capability; broader learning platform is not phase-1 critical |
| Sterilization / special-process validation package | domain-specific and broader than current repo scope |

## Hardening Items To Implement Before Architecture Growth

1. Lock ERP quality settings to hard-stop release behavior where applicable.
2. Declare HRMS as the system of record for employee structure and lifecycle events.
3. Decide whether `Organization Chart` becomes a quality overlay or is replaced by a cleaner authority model.
4. Decide the one master source for document type and process abbreviation in qms.
5. Decide the one distribution model in qms.
6. Fix qms workspace and docs so they match actual app truth.
7. Turn inactive qms automation code into either active hooks or remove it from the narrative.
