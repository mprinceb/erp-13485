# WTD-SOP-MFG-001 In-Process Inspection And Hold Points

## Objective

Convert existing job-card-linked in-process inspection into an enforced manufacturing hold-point control using the ERP manufacturing documents that already exist.

## Target Behavior

- Routing can declare which operations are true manufacturing hold points.
- A hold-point `Job Card` cannot be completed without accepted in-process inspection evidence linked to that `Job Card`.
- Manufacture posting cannot release finished output while required hold points remain open or rejected.
- Failed in-process checks lead users into a visible corrective job card or NCR path instead of informal offline correction.

## Minimal Data Model

- Add field on `BOM Operation`
  - `hold_point_required`
  - optional `ncr_on_reject_required`
- Copy the effective hold-point state to `Work Order Operation` and `Job Card`
  - `hold_point_required`
  - `hold_point_status`
- Reuse existing `quality_inspection_template` and `quality_inspection` linkage on `Job Card`
- Reuse existing `Quality Inspection`
  - require `inspection_type = In Process`
  - require `reference_type = Job Card`
  - make job-card or routing template precedence explicit for hold-point inspections
- Optional shared `Qualification Gate Log` reuse from `SOP-QMS-005`

## Enforcement Points

- Work-order creation or job-card generation
  - copy hold-point requirement from the approved routing
- `Job Card.validate` or controlled status-transition method
  - hard-stop completion when `hold_point_required = 1` and no accepted in-process `Quality Inspection` exists
- `Quality Inspection.on_submit`
  - update the effective hold-point status; on reject, surface corrective job card and NCR actions
- manufacturing `Stock Entry.validate` or `before_submit`
  - hard-stop finished-goods posting while required hold points for the completed quantity are unresolved

## User Guidance And Teaching

- Show hold-point badges on `Work Order` and `Job Card`.
- Add direct guided buttons on `Job Card`:
  - `Create In Process Quality Inspection`
  - `Open Existing Inspection`
  - `Create Corrective Job Card`
  - `Open NCR`
- Show the missing inspection reason in the block message when completion is denied.
- Show supervisor views for:
  - blocked work orders
  - rejected in-process inspections
  - open re-inspection actions

## System Ownership

- ERPNext owns routing, work execution, job-card completion, in-process inspection evidence, and manufacture release gates.
- `qms` owns the controlled instructions, checklists, and formal exception workflow linked from rejected inspections.
- HRMS only supports this slice where operator or inspector qualification is also gated.
- A small bridge is only needed if qualification from `SOP-QMS-005` is enforced at the same hold point.

## Reports And Views

- open hold-point blockers by work order
- hold-point completion status by operation
- in-process inspection pass or fail trend
- corrective job card and rework history
- rejected hold points awaiting NCR or re-inspection

## Priority And Sequencing Note

This slice should follow immediately after the first shared gate-service foundation and can run alongside other early transaction hardening work:

- most of the process already lives inside ERP manufacturing
- the missing gap is a narrow server-side control, not a large new module
- it gives a high-value manufacturing hard stop early in the program

## Acceptance Criteria

- Operators cannot complete a configured hold-point `Job Card` without accepted in-process inspection evidence.
- Manufacture posting cannot release finished goods while required hold points are unresolved.
- Rejected in-process inspections lead users into a traceable corrective path.
- Supervisors can identify blocked and failed hold points from standard manufacturing views.
