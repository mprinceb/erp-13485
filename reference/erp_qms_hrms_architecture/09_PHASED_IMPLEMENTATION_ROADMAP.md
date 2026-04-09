# Phased Implementation Roadmap

## Phase 0: Hardening And Alignment

Goal:

- make current ERP, qms, and HRMS behavior trustworthy before adding new modules

Scope:

- harden ERP quality-release settings to `Stop`
- align qms docs with actual repo truth
- activate only the qms hooks that are intentionally required
- declare HRMS the people source of truth
- choose the primary master doctypes and the primary distribution model
- decide whether `Organization Chart` becomes the quality authority overlay or is replaced
- fix qms report-model mismatches

Expected win:

- clearer current-state operation with fewer hidden bypasses and no ambiguity about where people data comes from

## Priority Parallel Lane: Approved Supplier Control

Goal:

- close the approved-supplier-by-item gap early, without waiting for the whole exception layer

Scope:

- add the `Approved Supplier` register and scope model
- link supplier qualification evidence to qms external supplier documents
- validate supplier scope on `Supplier Quotation`, `Purchase Order`, `Purchase Receipt`, and `Subcontracting Receipt`
- make temporary concession explicit and auditable
- add requalification-due reminders and blocked-sourcing reports

Expected win:

- one of the largest procurement compliance gaps closes early using ERP insertion points that already exist today

## Phase 1: Controlled Documents, Training, And Authority

Goal:

- make document control, onboarding impact, and training visible in daily work

Scope:

- extend `QMS Document` release flow with assignment generation
- add training assignment, acknowledgment, and competency doctypes
- extend qms authority mapping against HRMS employees, departments, and designations
- connect HRMS onboarding and transfer events to initial assignment generation
- add form banners for current effective SOP on key ERP transactions
- add training and authority prerequisite service for sensitive actions
- treat `SOP-QMS-005` as the concrete first operating slice for this phase

Expected win:

- users see what instruction applies, who owns the work, and whether they are allowed to perform the action

## Phase 2: Lifecycle Sync And Transaction Release Controls

Goal:

- make employee lifecycle changes automatically affect ERP qualification and release behavior

Scope:

- add HRMS to qms sync for onboarding, transfer, separation, and training-completion events
- revoke or re-evaluate authority on department or designation change
- enforce job-card hold points server-side
- add unresolved-exception and release-authority checks to finished-goods and shipment release
- add guided buttons for NCR, complaint escalation, and release dossier creation
- treat `SOP-MFG-001` as the first manufacturing hard-stop slice in this phase

Expected win:

- operational release becomes compliance-by-default instead of person-dependent

## Phase 3: Exception Layer

Goal:

- make deviations first-class controlled records with the right owner and supervisor context

Scope:

- extend ERPNext `Issue`, `Non Conformance`, and `Quality Action`
- implement closed-loop complaint, NCR, and CAPA flow
- derive owner, supervisor, and department context from HRMS
- add complaint-quality dashboards
- route QI rejects, serious complaints, supplier deviations, and audit findings into the same exception framework
- treat `SOP-QMS-004` as the first intake-and-escalation slice, then deepen closure and effectiveness through `SOP-QMS-003`

Expected win:

- one reusable quality-exception model across receipt, production, shipment, and service

## Phase 4: Review, Audit, And DHR

Goal:

- reduce manual audit and review preparation

Scope:

- add release dossier / DHR module
- add qualification gate log retrieval and qualified-at-time-of-action evidence
- add audit program, audit plan, and findings
- add management review pack assembly
- build cross-domain dashboards for management
- treat `SOP-TRC-002` as the first aggregation-and-freeze slice in this phase

Expected win:

- audit retrieval and management review become report-driven instead of manual compilation

## Phase 5: Optional Product-Development Layer

Goal:

- only if product-development scope really requires it

Scope:

- design controls
- DHF / DMR package assembly
- risk management and regulatory package extensions

Expected win:

- broader lifecycle coverage without contaminating the earlier, execution-focused phases

## Recommended Sequence

1. Phase 0
2. Approved Supplier parallel lane plus the `SOP-QMS-005` foundation slice
3. `SOP-MFG-001` plus the remaining Phase 2 controls
4. `SOP-QMS-004`, then `SOP-QMS-003`, then the rest of Phase 3
5. `SOP-TRC-002`, then the rest of Phase 4
6. Phase 5 only if explicitly in scope

## Dependency Notes

- Do not build training gates before defining authority and document applicability.
- Do not delay approved-supplier control until complaint/CAPA is complete; it can stand on existing ERP buying and receipt gate points.
- Do not enforce manufacturing hold points through client-side buttons alone; the decisive gate must be server-side.
- Do not treat `Issue` or `Warranty Claim` as a compliant complaint system until classification, escalation, and closure rules are explicit.
- Do not let qms maintain a second employee hierarchy that diverges from HRMS.
- Do not build DHR before release-critical transaction gates are stable.
- Do not freeze a release dossier while linked complaint, NCR, CAPA, or concession state is unresolved unless that override is explicit and auditable.
- Do not build audit packs before complaint, NCR, CAPA, training, and authority datasets are trustworthy.
- Do not rely on HRMS `Training Result` alone when revision-specific acknowledgment is required.
