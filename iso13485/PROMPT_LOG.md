# Prompt Log

## Purpose

Keep a durable log of the working brief, assumptions, and delegated prompts for this ERPNext and ISO 13485 exploration.

## User brief

Date: `2026-04-06`

Original goal:

> Explore the ERPNext app from the point of view of ISO 13485, especially its quality module. For purchase, sales, accounting, manufacturing, and other modules, identify flows and workflows and how quality is managed as per ERP. Produce Markdown with charts and diagrams so the architecture and SOP direction are clear. Use subagents and keep notes of prompts in a file.

Follow-on goal:

> Assess which SOPs can run fully in ERPNext as-is, which SOPs can run if small ERP enhancements are assumed, write those SOPs, and create work-to-be-done files for the enhancement-assumed set. Use the added ISO 13485 source files at `erpnext/docs/ISO 13485.pdf` and `erpnext/docs/iso_13485.md`.

## Working assumptions

- Primary scope is built-in `erpnext`, not the separate `qms` app.
- The target output is an architecture and SOP-baseline packet, not a custom code implementation.
- The packet must separate direct ERPNext behavior from inferred compliance controls.

## Main working prompt

Create an evidence-backed architecture packet that:

- maps ERPNext quality-related records and workflows
- shows how quality gates interact with buying, stock, manufacturing, selling, and accounts
- explains what employees must do in ERPNext to preserve auditable evidence
- highlights where SOP is required because ERPNext does not enforce the control itself

## Delegated subagent prompts

### Subagent A: core quality

Analyze the local codebase and produce an evidence-backed summary of ERPNext core quality features relevant to ISO 13485, limited to built-in ERPNext modules. Focus on `quality_management` plus stock and manufacturing quality inspection doctypes and reports. Identify:

1. core DocTypes and their purpose
2. main workflows and state changes
3. write paths, automation, schedulers, hooks
4. integration points into other ERPNext modules
5. gaps from an ISO 13485 auditable-process perspective
6. Mermaid-ready flow ideas

### Subagent B: procurement and inbound

Map ERPNext procurement, inventory, subcontracting, and accounting touchpoints from an ISO 13485 auditable-record perspective. Focus on purchase flow documents, stock receipt inspection controls, supplier-facing checkpoints, nonconformance-relevant points, and accounting evidence created by these flows.

### Subagent C: manufacturing and outbound

Map ERPNext sales, distribution, and manufacturing quality-related workflows from an ISO 13485 auditable-record perspective. Focus on order-to-delivery flow, production planning, work order, job card, in-process and final inspection points, traceability-related records, and where quality documents attach or block progression.

### Subagent D: ISO clauses 4, 5, and 8 against core ERP quality

Using the local `iso_13485.md` text and built-in ERPNext code only, classify candidate SOPs into:

1. workable today in ERPNext
2. workable with light customization
3. not a good fit without a larger system layer

Focus on document control, management review, feedback, complaints, nonconformance, CAPA, record control, and internal audit boundaries.

### Subagent E: ISO clause 7 operational SOP classification

Using the local `iso_13485.md` text and built-in ERPNext code only, classify operational SOP candidates across purchasing, manufacturing, installation, delivery, traceability, preservation, and service. Be explicit about what is truly native and what needs light customization.

## Notes to preserve

- `StockController.validate_inspection()` is the main transactional gate for required inspections.
- `Quality Inspection` is the cross-module record that links quality release to operational documents.
- The built-in `quality_management` module acts more like a quality register than a full procedural enforcement engine.
- `Job Card` supports in-process inspection, but current evidence suggests the gate is not server-enforced.
- A separate `qms` app exists in the bench and may be worth a later pass if the target architecture needs stronger complaint/CAPA/process controls.
- `A` class SOPs only remain defensible if inspection settings stay hardened to `Stop` and post-facto inspection bypass is not used.
- `B` class SOPs in this packet are intentionally limited to light ERP enhancements that can plausibly live inside core ERPNext customizations.

## Follow-on SOP Drafting Wave

Date: `2026-04-09`

Goal:

> Continue the research so it produces ERP-oriented SOP drafts that can be sent to the regulatory team for validation, with the real target operating model being ERPNext + HRMS + qms rather than ERPNext alone.

Outputs added in this wave:

- `SOP-QMS-005` and `WTD-SOP-QMS-005` for controlled-role training, competence, and authority
- `SOP-SAL-002` and `WTD-SOP-SAL-002` for customer requirement review and order acceptance
- `SOP-QMS-006` and `WTD-SOP-QMS-006` for monitoring and measuring equipment control
- `SOP-QMS-007` and `WTD-SOP-QMS-007` for internal quality audit and finding escalation

Repo-truth anchors used in this wave:

- HRMS onboarding, transfer, separation, training, and skill surfaces
- ERPNext quotation and sales-order records for customer requirement review
- ERPNext asset, asset maintenance, and asset maintenance log records for equipment control
- explicit absence of a first-class audit workflow in inspected ERPNext and `qms` surfaces

## Continuation SOP Drafting Wave

Date: `2026-04-09`

Goal:

> Continue the clause-wise SOP drafting so employees can follow ERP-oriented procedures directly inside ERPNext, HRMS, and qms-linked flows, with the next focus on installation acceptance, preservation or storage control, and process-monitoring evidence.

Outputs added in this wave:

- `SOP-SRV-002` and `WTD-SOP-SRV-002` for installation verification and acceptance
- `SOP-WHS-001` and `WTD-SOP-WHS-001` for preservation, storage, and dispatch-condition control
- `SOP-QMS-008` and `WTD-SOP-QMS-008` for process monitoring and trend escalation

Repo-truth anchors used in this wave:

- `Installation Note` validates serial numbers against the delivery record and prevents installation dates earlier than delivery
- `Installation Note` updates delivery-item installation status on submit
- `Maintenance Visit` records work done, completion status, customer feedback, and warranty-follow-up state
- `Warehouse` supports warehouse type and rejected-warehouse designation
- `Batch` enforces expiry-date setup for expiry-controlled items and ERP stock paths already prevent expired-batch use
- `Serial No` maintains product, location, employee, warranty, and maintenance-status context
- `Quality Goal`, scheduled `Quality Review`, and `Quality Action` already exist, but KPI harvesting and escalation routing remain lightweight

## Rework And Feedback SOP Drafting Wave

Date: `2026-04-09`

Goal:

> Continue the ERP-oriented SOP set with the next strongest repo-backed operational gaps, focusing on manufacturing rework and routine feedback capture that should feed trend review and exception escalation.

Outputs added in this wave:

- `SOP-MFG-004` and `WTD-SOP-MFG-004` for rework, re-inspection, and rerelease
- `SOP-QMS-009` and `WTD-SOP-QMS-009` for feedback capture and trend triage

Repo-truth anchors used in this wave:

- ERPNext `Job Card` supports corrective job card creation from a submitted job card
- ERPNext `Work Order` costing already includes corrective operation cost when configured
- ERPNext provides a `Cost of Poor Quality Report` driven by submitted corrective job cards
- ERPNext `Issue`, `Warranty Claim`, and `Maintenance Visit` already capture service and customer-quality signals
- ERPNext `Quality Feedback`, `Quality Goal`, `Quality Review`, and `Quality Action` provide the lightweight native trend and action chain

## Communication And Identifier SOP Drafting Wave

Date: `2026-04-09`

Goal:

> Continue the operational SOP set with the next defensible local surfaces, specifically controlled internal communication or policy awareness through `qms`, and regulated identifier or label governance through ERP item barcode and scan flows.

Outputs added in this wave:

- `SOP-QMS-010` and `WTD-SOP-QMS-010` for quality policy, internal communication, and controlled awareness
- `SOP-TRC-003` and `WTD-SOP-TRC-003` for identifier, barcode, and label governance

Repo-truth anchors used in this wave:

- `QMS Document` already supports guarded review, approval, release, archival, and released-document distribution
- `Distribution List` and `Distribution Log` already create auditable recipient snapshots for controlled communications
- `Organization Chart` already exists in the local `qms` app as a governed hierarchy
- ERPNext `Item Barcode` already validates uniqueness and code validity and supports barcode types including `GS1` and `GTIN`
- ERPNext `scan_barcode()` already resolves item barcodes, serial numbers, and batch numbers into stock-usable scan results
- ERPNext stock transactions already expose barcode-scanning fields in operational forms such as `Delivery Note` and `Stock Reconciliation`

## Approved Supplier Priority Wave

Date: `2026-04-09`

Goal:

> Revisit approved-supplier control as an implementation priority, verify the exact ERP gate points in local code, and decide whether the supplier-control slice should move earlier and run in parallel with other enhancement work.

Delegation used in this wave:

- `acpx` session `supplier-control`
- `acpx` session `cross-app-architecture`

Repo-truth anchors used in this wave:

- `Supplier Scorecard.update_standing()` writes supplier-level warn and prevent flags back to `Supplier`
- `Purchase Order.validate_supplier()` already blocks on `prevent_pos` and warns on `warn_pos`
- `StockController.validate_inspection()` already hard-gates incoming inspection at receipt time when settings are hardened
- `Item Supplier` is only a passive item child table and does not represent approved-supplier scope
- qms has no approved-supplier record today; it only contributes external supplier-document control

Outputs updated in this wave:

- `SOP-PUR-002`
- `WTD-SOP-PUR-002`
- `07_sop_portfolio_and_assessment.md`
- `README.md`

## Training, Authority, And Hold-Point Deepening Wave

Date: `2026-04-09`

Goal:

> Continue the documentation-only research pass after approved supplier by tightening the next two concrete operating slices: controlled-role training and authority, and manufacturing in-process hold points.

Delegation used in this wave:

- `acpx` session `training-and-competence`
- `acpx` session `mfg-hold-points`

Repo-truth anchors used in this wave:

- `QMS Document` already performs review, approval, release, archival, and distribution, but `qms` app-wide hooks are still mostly commented out
- `Organization Chart` is descriptive and free-text today, so HRMS remains the employee and role source of truth
- HRMS `Employee Onboarding` blocks employee creation until mandatory onboarding tasks are complete
- HRMS `Training Event`, `Training Result`, and `Training Feedback` already provide training evidence, but do not yet create revision-specific acknowledgment or governed authority
- ERP manufacturing already supports `Job Card`, in-process `Quality Inspection`, and corrective job cards
- ERP manufacturing `Stock Entry` already blocks manufacture when operations are incomplete, but not yet when a configured hold-point inspection is missing

Outputs updated in this wave:

- `SOP-QMS-005`
- `WTD-SOP-QMS-005`
- `SOP-MFG-001`
- `WTD-SOP-MFG-001`
- `07_sop_portfolio_and_assessment.md`
- `README.md`

## Complaint, NCR, And Release-Dossier Deepening Wave

Date: `2026-04-09`

Goal:

> Continue the ERP-oriented SOP set by turning the next exception and release-evidence slices into employee-facing SOPs: complaint handling, NCR/CAPA, and release dossier or DHR assembly.

Delegation used in this wave:

- `acpx` session `complaint-exception`
- `acpx` session `release-dossier`

Repo-truth anchors used in this wave:

- ERPNext `Issue` is the strongest current complaint intake shell, with ownering, communications, status, and closure behavior already present
- ERPNext `Warranty Claim` and `Maintenance Visit` already preserve product-service facts and service-resolution linkage
- ERPNext `Non Conformance` is present but very shallow
- ERPNext `Quality Action` and `Quality Action Resolution` provide partial CAPA structure, but not full closed-loop closure and effectiveness
- ERPNext `Stock Entry`, `Quality Inspection`, `Batch`, `Serial No`, and `Delivery Note` already hold most release evidence needed for a DHR-like packet

Outputs updated in this wave:

- `SOP-QMS-004`
- `WTD-SOP-QMS-004`
- `SOP-QMS-003`
- `WTD-SOP-QMS-003`
- `SOP-TRC-002`
- `WTD-SOP-TRC-002`
- `07_sop_portfolio_and_assessment.md`
- `README.md`

## Customer Property, Environment, And Software Validation Wave

Date: `2026-04-09`

Goal:

> Continue the ERP-oriented SOP set into the weaker but still important operational clauses: customer property control, workstation or environment readiness, and computer software validation or ERP change control.

Delegation used in this wave:

- `acpx` lane `customer-property`
- `acpx` lane `env-readiness`
- `acpx` lane `software-validation`

Repo-truth anchors used in this wave:

- ERPNext `Asset` already supports `asset_owner = Customer`, plus customer, custodian, location, and maintenance context
- ERPNext `Asset Movement` already updates location and custodian and writes `Asset Activity`
- ERPNext `Asset Maintenance`, `Asset Maintenance Log`, and `Asset Repair` already provide upkeep and repair evidence
- ERPNext `Workstation`, `Job Card`, and HRMS `Shift Assignment` and `Employee Checkin` already provide the base evidence for workstation readiness and assigned presence
- local `qms` already provides real `QMS Document`, `Change Request Ticket`, `Change Management`, `Questionnaire`, `Distribution Log`, `External Origin Document`, and `Obsolete Document` surfaces for software-change governance

Outputs updated in this wave:

- `SOP-SRV-003`
- `WTD-SOP-SRV-003`
- `SOP-MFG-005`
- `WTD-SOP-MFG-005`
- `SOP-QMS-011`
- `WTD-SOP-QMS-011`
- `07_sop_portfolio_and_assessment.md`
- `README.md`
