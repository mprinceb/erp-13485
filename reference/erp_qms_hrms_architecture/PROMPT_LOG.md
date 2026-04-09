# Prompt Log

## Purpose

Keep a durable record of the second-pass end-state architecture brief, assumptions, and delegated probes for ISO 13485 execution across ERPNext, qms, and HRMS.

Location note:

- this packet is now maintained under `erpnext/docs/reference/erp_qms_hrms_architecture/*`
- quoted user briefs below retain the original requested path where the work first started

## User Brief 1

Date: `2026-04-09`

Goal:

> Continue the existing ISO 13485 / ERPNext exploration from the existing outputs under `erpnext/docs/iso13485/*`. Do not redo the ERPNext-core baseline. Design the real end-state QMS architecture across built-in ERPNext, the local custom `qms` app, and any required new modules / doctypes / workflows. Use repo truth from both apps as source of truth. Create a new packet under `qms/docs/iso13485_end_state/`.

## Working Assumptions For Brief 1

- The earlier ERP packet remains the baseline for ERP transaction truth.
- This pass is about end-state architecture, not implementation code.
- Repo truth overrides `qms/docs/*` and `qms/README.md` if they diverge.
- The target state should minimize duplicate entry and keep operational evidence in ERP transactions.

## Main Working Prompt For Brief 1

Design an architecture that clearly separates:

1. what can be done right now
2. what should be extended in the existing `qms` app
3. what still requires new modules or workflows

and for each major business flow define:

- trigger
- roles
- ERP documents
- QMS documents
- evidence
- gates
- exception path
- reporting outputs

## User Brief 2

Date: `2026-04-09`

Goal:

> Continue the same ISO 13485 architecture thread and extend the existing packet under `qms/docs/iso13485_end_state/` to include the local `hrms` app in the same evidence-driven manner already used for ERPNext and qms. Do not restart from scratch. Keep repo truth as source of truth. Explicitly inspect HRMS and answer what HRMS actually contributes today, which capability areas it should own or strongly support, where it should be system of record versus qms versus ERPNext, how employee lifecycle and training flow across the apps, and what HRMS-linked events should update QMS records and enforcement state.

## Working Assumptions For Brief 2

- The `qms/docs/iso13485_end_state/*` packet created in brief 1 remains the base.
- HRMS should be assessed as the people, authority, qualification, and assignment layer where appropriate.
- ERPNext remains the transaction execution and release-evidence layer.
- qms remains the governance, document, change, and exception-governance layer.
- Bridge logic should stay as small as possible and only exist where cross-app enforcement is required.

## Main Working Prompt For Brief 2

Update the packet so it clearly shows:

1. what HRMS already gives now
2. what needs light adaptation in HRMS
3. what belongs in qms extension
4. what still requires a small new bridge or module

and make these flows concrete:

- employee onboarding into controlled roles
- training assignment and completion
- SOP acknowledgment after revision
- competency approval for sensitive operations
- authority mapping for release and approval roles
- role change, department transfer, and exit causing access or qualification review
- escalation ownership for complaints, NCR, CAPA, and audit findings

## Delegated Probes Used

### Probe A

Scope:

- inspect local HRMS doctypes, hooks, and workflow code for lifecycle, training, approver, and qualification-relevant behavior
- identify what is real in code versus assumed from generic Frappe knowledge

### Probe B

Scope:

- inspect cross-app ownership and integration touchpoints across ERPNext, qms, and HRMS
- focus on system-of-record boundaries, event triggers, and the smallest bridge needed for qualification enforcement

## Notes To Preserve

- ERPNext remains the system of action for receipt, manufacture, shipment, and service.
- The local `qms` app is materially broader than its top-level docs describe.
- `qms` contains real change-control and file-governance surfaces, but almost no live ERP transaction integration.
- qms automation claims are overstated unless hooks and scheduler wiring are explicitly activated.
- HRMS is already a live workflow layer for onboarding, transfer, separation, training events, and approver-role handling.
- HRMS should own employee and reporting structure truth; qms should not keep a competing free-standing org tree.
- The best implementation path is to extend qms for governed content, acknowledgment, competency, and authority; use HRMS for people and lifecycle truth; extend ERP for transactional exceptions; and add a small bridge for lifecycle sync and qualification gates.

## User Brief 3

Date: `2026-04-09`

Goal:

> Review the currently approved SOP and related documents under `erpnext/docs/existing_sop`, using the relevant document and spreadsheet workflows and delegated agents. Decide whether the research is finished, and if yes produce the final documents and architecture for authority presentation. If not, define the next iteration plan.

## Working Assumptions For Brief 3

- The approved corpus in `existing_sop` is now the authoritative baseline for what has actually been prepared and approved by regulatory.
- The earlier ERPNext and end-state packets remain the architecture baseline.
- The question is not only “what is approved” but also “is the wider research closed enough to present honestly.”

## Notes For Brief 3

- 18 DOCX artifacts were found in `erpnext/docs/existing_sop`.
- No Excel workbook was found in that folder during this pass.
- Text extracts were generated from the DOCX files under `/tmp/existing_sop_extracts` for review.
- An `acpx` attempt was made for delegated review, but the local codex ACP adapter failed with `Quota exceeded`, so the review continued with built-in subagents.
- The approved SOP set strongly covers document control, record control, and supplier control, but the approved tracking list still shows a much wider QMS library in draft or review.

## User Brief 4

Date: `2026-04-09`

Goal:

> Continue the research by going clause-wise through ISO 13485, identify which SOPs are needed, and determine how much of each clause can be implemented through ERPNext, qms, and HRMS workflows so that user work itself creates the required compliance records.

## Working Assumptions For Brief 4

- Optimize for operational QMS first.
- Use the clause matrix as the main output before drafting more SOPs.
- Keep design controls, risk, DHF, DMR, and regulatory reporting visible, but with lighter depth unless they directly affect daily operational execution.
- Use the approved source tracking list as the baseline for what is actually approved versus draft.

## Main Working Prompt For Brief 4

Build the next operational-QMS reference layer by producing:

1. a clause matrix
2. an operational clause-to-system map
3. a Frappe event and automation blueprint

so the next SOP drafting pass can turn the architecture into employee-usable ERP workflows.

## Evidence Notes For Brief 4

- The clause source for this pass was `erpnext/docs/iso_13485.md`.
- The approved baseline came primarily from:
  - `/tmp/existing_sop_extracts/SOP-1_Control_of_Documents_LST-004_QMS_Documents_Tracking_List.docx.md`
  - `/tmp/existing_sop_extracts/SOP-2_Control_of_Records_LST-004_QMS_Records_Tracking_List.docx.md`
- ERPNext repo truth for hard inspection gates is in `erpnext/erpnext/controllers/stock_controller.py`.
- ERPNext manufacturing repo truth for in-process inspection is present in `Job Card` and BOM surfaces, but not yet as a hard server-side hold point.
- `qms` repo truth shows active document and change-control logic in controllers, but most app-wide hooks and schedulers remain commented out in `qms/hooks.py`.
- HRMS repo truth shows real lifecycle and training surfaces through onboarding, transfer, separation, employee hooks, training events, and training results.

## Outputs Created For Brief 4

- `15_CLAUSE_MATRIX_OPERATIONAL_QMS.md`
- `16_OPERATIONAL_CLAUSE_TO_SYSTEM_MAP.md`
- `17_FRAPPE_EVENT_AND_AUTOMATION_BLUEPRINT.md`

## Approved Supplier Priority Follow-On

Date: `2026-04-09`

Goal:

> Re-check approved-supplier control as a potentially earlier implementation slice, use named `acpx` sessions for parallel supplier-control review, and fold the result back into the roadmap, event matrix, and ERP-oriented supplier SOP.

Named `acpx` sessions used:

- `supplier-control`
- `cross-app-architecture`

Key repo-truth confirmations:

- ERPNext already contains supplier-level PO gating in `Purchase Order.validate_supplier()`
- ERPNext already contains receipt-side incoming inspection gates in `StockController.validate_inspection()`
- qms does not currently contain an approved-supplier register
- qms can still hold controlled supplier evidence through `External Origin Document` with source `Supplier Document`
- HRMS contributes approver and training context, but not supplier approval itself

Outputs updated in this wave:

- `04_EVENT_AND_INTEGRATION_MATRIX.md`
- `09_PHASED_IMPLEMENTATION_ROADMAP.md`
- `10_IMPLEMENT_NOW_VS_EXTEND_QMS_VS_NEW_MODULES.md`
- `17_FRAPPE_EVENT_AND_AUTOMATION_BLUEPRINT.md`
- `18_APPROVED_SUPPLIER_CONTROL_ARCHITECTURE.md`

Naming note:

- these files follow the existing numbered-uppercase pattern already used by the rest of this packet
- duplicate lowercase filenames created during drafting were removed so only one canonical set remains

## Training And Hold-Point Follow-On

Date: `2026-04-09`

Goal:

> Continue the next-slice documentation after approved supplier by deepening controlled-role training and authority, and by defining the first manufacturing hard-stop architecture around in-process hold points.

Named `acpx` sessions used:

- `training-and-competence`
- `mfg-hold-points`

Key repo-truth confirmations:

- `QMS Document` already has release and distribution behavior, but `qms` hook and scheduler wiring remains mostly commented out
- `Organization Chart` is descriptive and not suitable as the primary employee authority truth
- HRMS onboarding, transfer, separation, training-event, and training-result surfaces are real, but revision-specific acknowledgment and governed authority are still missing
- ERPNext `Job Card` already exposes an in-process `Quality Inspection` route and corrective job card creation
- ERPNext `Stock Entry` already blocks manufacture when operations are incomplete, but no current server-side gate requires accepted in-process inspection on a hold-point operation

Outputs updated in this wave:

- `19_CONTROLLED_ROLE_TRAINING_AND_AUTHORITY_ARCHITECTURE.md`
- `20_IN_PROCESS_HOLD_POINT_ARCHITECTURE.md`
- `04_EVENT_AND_INTEGRATION_MATRIX.md`
- `09_PHASED_IMPLEMENTATION_ROADMAP.md`
- `10_IMPLEMENT_NOW_VS_EXTEND_QMS_VS_NEW_MODULES.md`
- `17_FRAPPE_EVENT_AND_AUTOMATION_BLUEPRINT.md`
- `README.md`

## Exception Backbone And Release-Dossier Follow-On

Date: `2026-04-09`

Goal:

> Continue the architecture packet after the foundation-gate slices by defining the next operational exception backbone: complaint intake and service escalation, NCR/CAPA depth, and release dossier or DHR assembly.

Named `acpx` sessions used:

- `complaint-exception`
- `release-dossier`

Key repo-truth confirmations:

- ERPNext `Issue` already provides the best local complaint intake shell, but quality classification, severity, reportability, and governed close rules are still missing
- ERPNext `Warranty Claim` and `Maintenance Visit` already preserve product, serial, service, and resolution context that should feed the complaint workflow
- ERPNext `Non Conformance` is too shallow on its own, while `Quality Action` and `Quality Action Resolution` provide only partial CAPA structure
- ERPNext execution and release evidence already exists across `Work Order`, `Job Card`, `Stock Entry`, `Quality Inspection`, `Batch`, `Serial No`, and `Delivery Note`, but no governed DHR or release-dossier freeze exists today

Outputs updated in this wave:

- `21_COMPLAINT_HANDLING_AND_SERVICE_ESCALATION_ARCHITECTURE.md`
- `22_NONCONFORMANCE_CAPA_AND_EFFECTIVENESS_ARCHITECTURE.md`
- `23_RELEASE_DOSSIER_AND_DHR_ARCHITECTURE.md`
- `04_EVENT_AND_INTEGRATION_MATRIX.md`
- `09_PHASED_IMPLEMENTATION_ROADMAP.md`
- `10_IMPLEMENT_NOW_VS_EXTEND_QMS_VS_NEW_MODULES.md`
- `17_FRAPPE_EVENT_AND_AUTOMATION_BLUEPRINT.md`
- `README.md`

## Customer Property, Environment, And Software Validation Follow-On

Date: `2026-04-09`

Goal:

> Continue the architecture packet into the lighter operational clauses that still need repo-truth framing: customer property, workstation or environment readiness, and software validation or ERP change control.

Named `acpx` lanes used:

- `customer-property`
- `env-readiness`
- `software-validation`

Key repo-truth confirmations:

- ERPNext already supports customer-owned assets, asset movement, asset activity, service, and repair history strongly enough to draft a customer-property control slice
- ERPNext `Workstation`, `Job Card`, supporting asset-maintenance records, and HRMS shift or presence records are strong enough for readiness control, but not for full contamination-control rigor
- local `qms` already has a real document and change backbone, but software-validation-specific evidence, deployment approval, and post-change rigor are still missing

Outputs updated in this wave:

- `24_CUSTOMER_PROPERTY_AND_CUSTOMER_OWNED_PRODUCT_CONTROL_ARCHITECTURE.md`
- `25_WORK_ENVIRONMENT_AND_WORKSTATION_READINESS_ARCHITECTURE.md`
- `26_COMPUTER_SOFTWARE_VALIDATION_AND_ERP_CHANGE_CONTROL_ARCHITECTURE.md`
- `15_CLAUSE_MATRIX_OPERATIONAL_QMS.md`
- `16_OPERATIONAL_CLAUSE_TO_SYSTEM_MAP.md`
- `README.md`
