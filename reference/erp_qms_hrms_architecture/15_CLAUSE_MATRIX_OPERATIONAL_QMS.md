# Clause Matrix For Operational QMS

This matrix turns ISO 13485 clause intent into an ERP, `qms`, and HRMS operating model.

Scope choice for this pass:

- optimize for operational QMS
- keep design-control, DHF, DMR, risk, and regulatory-reporting clauses visible
- give lighter workflow depth to clauses that do not drive day-to-day operational execution

Source priority used here:

1. local repo code and DocType surfaces
2. approved source corpus under `erpnext/docs/existing_sop/`
3. active SOP deliverables under `erpnext/docs/iso13485/`
4. reference architecture docs in this folder

## Legend

- `Baseline`: status in the approved-source tracking baseline
- `Workflow fit`: how the clause should land in software
  - `Current` = already supportable with current app behavior
  - `Light adapt` = small configuration or low-risk customization
  - `Extend qms` = natural extension of the current `qms` app
  - `New bridge/module` = cross-app enforcement or new quality surface needed
  - `Deferred` = keep visible, but outside the first operational-QMS delivery slice

## Clause 4: Quality Management System

| Clause | Intent | SOP baseline | Workflow fit | Primary system | Daily workflow and evidence | Gap and next move |
| --- | --- | --- | --- | --- | --- | --- |
| 4.1 | Define the QMS process map, interfaces, controls, and outsourced-process governance | Approved core only: `TCR-COD-SOP-1`, `TCR-COR-SOP-2`; `TCR-CHM-SOP-3` under final review; active enhancement pack `SOP-QMS-011` | `Extend qms` + `New bridge/module` | `qms` + bridge | Controlled docs, change records, gate logs, and management-review packs define the live operating system | No executable cross-app control plan yet; software-validation evidence and cross-app gate governance still need implementation |
| 4.2.1 | Maintain the required documented QMS set | `TCR-COD-SOP-1` approved, `TCR-COR-SOP-2` approved, `QMM-QM-43` tracked only | `Extend qms` | `qms` | `QMS Document`, master lists, document distribution, obsolete list, and record registry | Quality manual and document applicability are not yet enforced in-app |
| 4.2.2 | Maintain a quality manual and its governed appendices | `QMM-QM-43` tracked only; `TCR-QMM-ANNEX-001` approved; `TCR-QMM-ANNEX-002` draft | `Extend qms` | `qms` | Quality manual, organizational annexes, and authority appendices should live as controlled released documents | Manual exists only as tracked artifact today; link quality manual to current process map and authority overlay |
| 4.2.3 | Maintain medical-device-file style product records | `TCR-MDF-SOP-39` tracked only | `Deferred` | new module | Product-family file, linked specs, IFU, traceability set, release dossier, and change links | No MDF/DMR-style assembly layer yet; keep clause visible and defer beyond operational execution slice |
| 4.2.4 | Control document creation, review, approval, release, revision, distribution, and obsolescence | `TCR-COD-SOP-1` approved; active enhancement pack `SOP-QMS-001` | `Extend qms` | `qms` | `QMS Document` already supports status transitions, release metadata, archive behavior, and distribution logs | Revision-specific acknowledgment, ERP context display, and training generation still missing |
| 4.2.5 | Control records, retention, disposition, and retrieval | `TCR-COR-SOP-2` approved; active enhancement pack `SOP-QMS-001` | `Extend qms` + `Light adapt` | ERPNext + `qms` | ERP transactions create execution records; `qms` should hold record master lists, retention rules, and disposition logs | Record tracking sheet is largely not populated; retention metadata must be attached to real ERP and qms records |

## Clause 5: Management Responsibility

| Clause | Intent | SOP baseline | Workflow fit | Primary system | Daily workflow and evidence | Gap and next move |
| --- | --- | --- | --- | --- | --- | --- |
| 5.1 | Show management commitment through assigned governance and review activity | `TCR-MGR-SOP-4` under 2nd review; `TCR-QMM-ANNEX-001` approved | `Extend qms` | `qms` | Management review agenda, action closure, authority assignments, and resource decisions provide evidence | Management oversight exists conceptually, but review-pack assembly is still manual |
| 5.2 | Maintain customer focus in requirement review, complaint handling, and feedback loops | `TCR-CRP-SOP-11` draft, `TCR-CFB-SOP-23` draft, `TCR-CHL-SOP-24` draft | `New bridge/module` | ERPNext + `qms` | Customer interactions in `Issue`, `Warranty Claim`, sales docs, and service docs should feed complaint and feedback evidence | No closed-loop complaint/feedback layer is enforced today |
| 5.3 | Maintain and communicate quality policy | `QMM-QM-43` tracked only; active enhancement pack `SOP-QMS-010` | `Extend qms` | `qms` | Released quality-policy document, acknowledgment, and training assignment | The SOP pack now exists, but role-based applicability and enforced acknowledgment are still missing |
| 5.4.1 | Set and monitor quality objectives | `TCR-MGR-SOP-4` under 2nd review; `TCR-PRL-SOP-9` under 1st review | `Current` + `Extend qms` | ERPNext + `qms` | `Quality Goal`, `Quality Review`, and review packs can hold objectives and status evidence | Objectives exist in ERPNext, but not yet tied into the governed review cadence |
| 5.4.2 | Plan QMS changes without breaking controls | `TCR-CHM-SOP-3` under final review; active enhancement pack `SOP-QMS-011` | `Extend qms` | `qms` | `Change Request Ticket` and `Change Management` can define change reason, impact, and implementation evidence | Need ERP impact mapping, software-validation evidence, retraining generation, and formal release criteria |
| 5.5.1 | Define responsibility and authority | `TCR-QMM-ANNEX-001` approved; `TCR-QMM-ANNEX-002` draft; `TCR-CAT-SOP-7` under 1st review | `Extend qms` + `Light adapt` | HRMS + `qms` | HRMS gives person, department, designation, reporting line; qms should overlay quality authority and controlled-role logic | Quality authority is not yet a live governed layer |
| 5.5.2 | Define management representative responsibilities | `TCR-QMM-ANNEX-001` approved; roles annex still draft | `Extend qms` | `qms` + HRMS | Named MR role, effective dates, delegated authority, and review ownership | No explicit MR/PRRC authority overlay in current app surface |
| 5.5.3 | Maintain internal communication | `TCR-ICM-SOP-5` under 1st review; active enhancement pack `SOP-QMS-010` | `Light adapt` + `Extend qms` | HRMS + `qms` | HRMS assignments, qms distribution logs, and review-action routing should create communication evidence | The SOP pack now exists, but governed applicability and completion tracking still need implementation |
| 5.6.1 | Hold management review at defined intervals | `TCR-MGR-SOP-4` under 2nd review; active pack `SOP-QMS-002` | `Extend qms` | `qms` | Review schedule, agenda, attendees, input pack, minutes, and actions | Review pack still needs automated assembly from ERP, qms, and HRMS |
| 5.6.2 | Feed the required inputs into management review | same baseline as 5.6.1 | `Extend qms` + `New bridge/module` | `qms` | Complaints, supplier metrics, training status, NCR/CAPA, and change state should flow into one governed packet | Inputs exist across systems, but aggregation is mostly manual today |
| 5.6.3 | Capture review outputs and follow-up actions | same baseline as 5.6.1 | `Extend qms` | `qms` | Action list, owners, due dates, and effectiveness status | Need a formal management-review action object or disciplined reuse of tasks/actions |

## Clause 6: Resource Management

| Clause | Intent | SOP baseline | Workflow fit | Primary system | Daily workflow and evidence | Gap and next move |
| --- | --- | --- | --- | --- | --- | --- |
| 6.1 | Provide the needed people, infrastructure, and supporting resources | `TCR-RSM-SOP-6` under 1st review | `Light adapt` | HRMS + ERPNext | Employee assignments, equipment lists, and resource planning records | Resource need tracking is not yet connected to quality-review obligations |
| 6.2 | Ensure competence, awareness, training, and qualification | `TCR-CAT-SOP-7` under 1st review; record list includes job-role descriptions, training records, annual calendar, and training evaluation forms | `Extend qms` + `Light adapt` | HRMS + `qms` | HRMS onboarding, transfer, `Training Event`, `Training Result`, and qms acknowledgment/competency should create the evidence set | HRMS has lifecycle and training-event surfaces, but revision acknowledgment and qualification gates are missing |
| 6.3 | Control infrastructure needed for product quality | `TCR-RSM-SOP-6` under 1st review; record list includes equipment and maintenance records; active enhancement pack `SOP-MFG-005` | `Light adapt` | ERPNext + HRMS | Equipment master, maintenance records, workspace ownership, and workstation state | Infrastructure is not yet connected to hard release gates, audit packs, or readiness checks by default |
| 6.4.1 | Maintain suitable work environment | `TCR-WEM-SOP-8` draft; `TCR-WEM-WI-001` draft; active enhancement pack `SOP-MFG-005` | `Light adapt` | ERPNext + HRMS | Cleaning, readiness, shift, and environment records should attach to production and facility workflows | The SOP path is now drafted, but structured readiness and environment logs still need implementation |
| 6.4.2 | Maintain contamination-control arrangements where relevant | same baseline as 6.4.1; active enhancement pack `SOP-MFG-005` for the non-sterile readiness layer | `Deferred` unless product scope requires it | ERPNext + `qms` | Environment logs, cleaning records, batch linkage, and deviation records | Keep visible; the drafted readiness slice helps, but true contamination control still depends on confirmed product scope and extra records |

## Clause 7: Product Realization

| Clause | Intent | SOP baseline | Workflow fit | Primary system | Daily workflow and evidence | Gap and next move |
| --- | --- | --- | --- | --- | --- | --- |
| 7.1 | Plan product realization and quality controls before execution | `TCR-PRL-SOP-9` under 1st review; active pack `SOP-MFG-003` | `Current` + `Light adapt` | ERPNext | BOM, routing, work order, operation, inspection template, and release planning evidence | Planning exists in ERPNext, but qms-driven release and exception overlays are missing |
| 7.2.1 | Capture product and customer requirements | `TCR-CRP-SOP-11` draft | `Light adapt` | ERPNext | Quotation, sales order, item spec, and controlled requirement-review fields | Customer requirement review is not yet formalized in ERP workflows |
| 7.2.2 | Review requirements before commitment | `TCR-CRP-SOP-11` draft | `Light adapt` | ERPNext + `qms` | Approval trail on quotation/order plus any concession/change review evidence | Need a controlled review checklist for regulated orders or product variants |
| 7.2.3 | Maintain customer communication | `TCR-CRP-SOP-11` draft; `TCR-CFB-SOP-23` draft; `TCR-CHL-SOP-24` draft | `Current` + `New bridge/module` | ERPNext | Sales, support, service, warranty, and issue records | Complaint-quality escalation and formal communication records are not yet layered on top |
| 7.3.1 | Control design and development at the system level | `TCR-DND-SOP-12` under 1st review | `Deferred` | new module | Design plan, review, verification, validation, transfer, and file records | Design controls remain outside the first operational-QMS delivery slice |
| 7.3.2 | Plan design and development work | `TCR-DND-SD-001` under 1st review | `Deferred` | new module | Design plans, milestones, and review gates | No design-control module yet |
| 7.3.3 | Maintain controlled design inputs | multiple `TCR-DND-*-001/002` records under review or draft | `Deferred` | new module | Approved inputs and review trace | Outside first slice |
| 7.3.4 | Maintain controlled design outputs | multiple `TCR-DND-*-003/004` records under review or draft | `Deferred` | new module | Released outputs and trace to inputs | Outside first slice |
| 7.3.5 | Perform design reviews | multiple `TCR-DND-*` review records under review or draft | `Deferred` | new module | Design review minutes and approvals | Outside first slice |
| 7.3.6 | Perform design verification | multiple `TCR-DND-*-005/006` records draft or blank | `Deferred` | new module | Verification protocols, results, and closures | Outside first slice |
| 7.3.7 | Perform design validation | multiple `TCR-DND-*-007/008` records draft or blank | `Deferred` | new module | Validation protocols, reports, and approvals | Outside first slice |
| 7.3.8 | Control design transfer | `TCR-DND-SOP-12` under 1st review | `Deferred` | new module + ERPNext | Transfer approvals, BOM/routing release, and manufacturing readiness evidence | Needs a later design-to-manufacturing bridge |
| 7.3.9 | Control design changes | `TCR-CHM-SOP-3` under final review; `TCR-DND-SOP-12` under 1st review | `Deferred` | new module + `qms` | Design change package and affected-document map | Keep visible; use current change-control model only for document/process changes in first slice |
| 7.3.10 | Maintain design-and-development files | `TCR-MDF-SOP-39` tracked only plus design-file entries | `Deferred` | new module | DHF/DMR-like assembled file | Outside first slice |
| 7.4.1 | Control supplier qualification and purchasing process | `TCR-SCP-SOP-13` approved; active packs `SOP-PUR-003`, `SOP-PUR-002` | `Current` + `New bridge/module` | ERPNext + new supplier-control module | Supplier master, scorecard, assessment, approved scope, PO approval | ERPNext supports sourcing and scorecards, but approved-supplier-by-item release control is missing |
| 7.4.2 | Define purchasing information | `TCR-SCP-SOP-13` approved; active pack `SOP-PUR-004` | `Current` | ERPNext | Supplier quotation, PO terms, item specs, attachments, and controlled supplier communication | Need stronger linkage between controlled specs and PO/inspection templates |
| 7.4.3 | Verify purchased product before release | `TCR-SCP-SOP-13` approved; active packs `SOP-PUR-001`, `SOP-PUR-002` | `Current` + `Light adapt` | ERPNext | `Purchase Receipt`, `Quality Inspection`, batch/serial, release result, supplier performance evidence | Core hard gate exists, but approved-supplier control and automatic NCR routing do not |
| 7.5.1 | Control production and service provision | `TCR-PRL-SOP-9` under 1st review; `TCR-COP-SOP-10` draft; `TCR-CASM-SOP-15` draft; `TCR-AASM-SOP-16` tracked | `Current` + `Light adapt` | ERPNext | Work order, job card, stock entry, final inspection, release, and service records | ERP execution exists, but SOP guidance and hold-point gating are incomplete |
| 7.5.2 | Control cleanliness where it affects product | `TCR-WEM-SOP-8` draft and multiple cartridge-assembly work instructions draft; active enhancement pack `SOP-MFG-005` | `Light adapt` | ERPNext | Cleaning and environment checks tied to workstation, shift, batch, or work order | The SOP path is now drafted, but structured ERP evidence still needs implementation |
| 7.5.3 | Control installation activities | `TCR-ISD-SOP-14` draft; active enhancement pack `SOP-SRV-002` | `Light adapt` | ERPNext | Installation, acceptance, and site records | ERP service tools support installation records, and the SOP pack now exists, but controlled acceptance and escalation still need implementation |
| 7.5.4 | Control servicing activities | `TCR-ISD-SOP-14` draft; active pack `SOP-SRV-001` | `Current` + `Light adapt` | ERPNext | Maintenance visit, warranty claim, return, service history, complaint linkage | Works as service evidence today, but feedback/complaint escalation needs a quality layer |
| 7.5.5 | Add sterile-medical-device controls where applicable | no approved baseline; `TCR-VLP-SOP-17` draft may contribute | `Deferred` | new module | Sterile-process records, batch trace, and validation evidence | Implement only if sterile scope is confirmed |
| 7.5.6 | Validate production and service processes where output cannot be fully verified later | `TCR-VLP-SOP-17` draft; `TCR-SWV-SOP-18` draft | `Deferred` in first slice | ERPNext + `qms` | Validation protocols, reports, trained-authority approvals, and change impact | Keep visible; add when process validation becomes active implementation scope |
| 7.5.7 | Validate sterilization and sterile-barrier processes where applicable | no practical baseline in current packet | `Deferred` | new module | Sterilization validation file and cycle evidence | Out of first slice unless product scope requires it |
| 7.5.8 | Identify product and status throughout realization | `TCR-IDT-SOP-19` under 1st review; active packs `SOP-TRC-001`, `SOP-TRC-003` | `Current` + `Light adapt` | ERPNext | Item, batch, serial, warehouse, label, inspection status, and stock movement evidence | Current ERP traceability is strong; regulated label issuance and identifier-governance controls still need implementation |
| 7.5.9 | Maintain traceability to the required depth | same baseline as 7.5.8; active enhancement pack `SOP-TRC-002` | `Current` + `New bridge/module` | ERPNext + new DHR/release module | Work order to batch/serial to delivery/service chain; release dossier should assemble it | Need one assembled DHR/release dossier for audit retrieval |
| 7.5.10 | Control customer property | `TCR-HCP-SOP-20` draft; active enhancement pack `SOP-SRV-003` | `Light adapt` | ERPNext | Customer-owned asset, serial, service, custody, and disposition records | The SOP path is now drafted, but governed intake, condition, loss, and disposition controls still need implementation |
| 7.5.11 | Preserve product during internal handling, storage, and shipment | `TCR-HSPP-SOP-21` draft; active enhancement pack `SOP-WHS-001` | `Light adapt` | ERPNext | Warehousing, packaging, labelling, dispatch, and storage-condition records | The SOP pack now exists, but storage-condition evidence and dispatch-condition controls still need implementation |
| 7.6 | Control monitoring and measuring equipment | `TCR-CMME-SOP-22` draft; active enhancement pack `SOP-QMS-006` | `Light adapt` | ERPNext + `qms` | Equipment master, calibration/maintenance records, usage restriction, and training linkage | The operating model is now drafted, but quality-critical equipment release and block logic are still not implemented |

## Clause 8: Measurement, Analysis, And Improvement

| Clause | Intent | SOP baseline | Workflow fit | Primary system | Daily workflow and evidence | Gap and next move |
| --- | --- | --- | --- | --- | --- | --- |
| 8.1 | Define the measurement, analysis, and improvement framework | `TCR-PRL-SOP-9` under 1st review; `TCR-DAN-SOP-31` draft | `Extend qms` | `qms` + ERPNext | KPI packs, review metrics, NCR/CAPA status, supplier and complaint trends | Need one governed analytics and review model |
| 8.2.1 | Gather and analyze feedback | `TCR-CFB-SOP-23` draft; active enhancement pack `SOP-QMS-009` | `Light adapt` + `New bridge/module` | ERPNext | `Issue`, service history, returns, feedback notes, and customer interactions | The SOP pack now exists, but governed feedback-vs-complaint triage and trend escalation are still missing |
| 8.2.2 | Handle complaints formally | `TCR-CHL-SOP-24` draft; active enhancement pack `SOP-QMS-004` | `New bridge/module` | ERPNext + new exception layer | Intake in `Issue`/`Warranty Claim`, quality classification, investigation, owner, escalation, and closure | Complaint lifecycle is one of the biggest current gaps |
| 8.2.3 | Report to regulatory authorities when required | `TCR-CRB-SOP-25` draft; `TCR-VGL-SOP-26` draft | `Deferred` | new module | Regulatory incident assessment, field action, authority communication logs | Keep visible; not part of first operational-QMS implementation slice |
| 8.2.4 | Perform internal audits | `TCR-IQA-SOP-27` under 2nd review; active enhancement pack `SOP-QMS-007` | `New bridge/module` | new audit module + `qms` | Audit plan, schedule, checklist, findings, NCs, and closure actions | The SOP pack now exists, but no audit program module exists in inspected apps |
| 8.2.5 | Monitor and measure processes | `TCR-CMMPR-SOP-29` draft; active enhancement pack `SOP-QMS-008` | `Extend qms` + `Light adapt` | ERPNext + `qms` | Process KPIs, yield, hold-point results, overdue training, and review metrics | The SOP pack now exists, but governed thresholds and automated escalation are still missing |
| 8.2.6 | Monitor and measure product | `TCR-CMMPD-SOP-28` draft; active packs `SOP-PUR-001`, `SOP-MFG-001`, `SOP-MFG-002`, `SOP-SAL-001` | `Current` + `Light adapt` | ERPNext | Incoming, in-process, and final `Quality Inspection` plus release records | In-process hold points still need server-side enforcement |
| 8.3.1 | Control nonconforming product through a formal system | `TCR-NCPR-SOP-30` draft; active enhancement pack `SOP-QMS-003` | `New bridge/module` | ERPNext quality module + new exception layer | Source transaction, disposition, owner, root cause, and closure evidence | ERPNext `Non Conformance` is too shallow for the target operating model |
| 8.3.2 | Control nonconforming product before delivery | same baseline as 8.3.1 | `Current` + `New bridge/module` | ERPNext | QI reject, hold, block shipment, corrective job card, concession, or NCR | Transactional block paths exist only partially; auto-routing to NCR is missing |
| 8.3.3 | Control nonconforming product detected after delivery | same baseline as 8.3.1 | `New bridge/module` | ERPNext + complaint layer | Complaint, return, field failure, service finding, and post-delivery disposition | Needs closed-loop complaint-to-NCR flow |
| 8.3.4 | Control rework | same baseline as 8.3.1; active enhancement pack `SOP-MFG-004` | `Light adapt` + `New bridge/module` | ERPNext | Corrective job card, re-inspection, and re-release evidence | The SOP pack now exists, but ERP still lacks governed rework-to-rerelease enforcement |
| 8.4 | Analyze data and use it in review and improvement | `TCR-DAN-SOP-31` draft | `Extend qms` | `qms` + ERPNext + HRMS | KPI trends, supplier metrics, training compliance, NCR/CAPA, and complaint trends | Management-review analytics remain manual today |
| 8.5.1 | Drive improvement through the QMS | `TCR-CAPA-SOP-32` draft; `TCR-CHM-SOP-3` under final review | `New bridge/module` + `Extend qms` | ERPNext + `qms` | CAPA, change implementation, training updates, and review follow-up actions | No closed improvement system yet |
| 8.5.2 | Execute corrective action | `TCR-CAPA-SOP-32` draft; active enhancement pack `SOP-QMS-003` | `New bridge/module` | ERPNext quality module + `qms` | Root cause, action plan, implementation, effectiveness, closure approval | Current `Quality Action` is too shallow and not linked tightly enough to source events |
| 8.5.3 | Execute preventive action | same baseline as 8.5.2 | `New bridge/module` + `Extend qms` | ERPNext + `qms` | Trend-driven actions, change packages, retraining, and review follow-up | Preventive action should reuse the same exception and change backbone as CAPA |

## Immediate Reading Of The Matrix

### Already strongest in current repo truth

- 4.2.4 and 4.2.5 through the existing `qms` document stack plus approved document and record-control baseline
- 7.4.2 and 7.4.3 through ERP purchasing, receipt, and quality inspection behavior
- 7.5.8 and 7.5.9 through ERPNext identification and traceability fields
- 8.2.6 through incoming and final inspection scaffolding in ERPNext

### Strong on policy baseline but weak in live workflow

- 5.5 responsibility and authority
- 6.2 competence, awareness, and training
- 5.6 management review
- 8.2.4 internal audit

### Biggest operational software gaps

- 8.2.2 complaint handling
- 8.3 nonconforming product lifecycle depth
- 8.5 CAPA and effectiveness closure
- 7.4.1 approved-supplier-by-item release control
- 7.5.1 / 8.2.6 server-side in-process hold points
- 7.5.9 DHR / release dossier assembly
