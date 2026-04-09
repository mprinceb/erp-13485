# WTD-SOP-QMS-004 Complaint Handling And Escalation

## Objective

Turn the existing support and service records in ERPNext into one governed complaint workflow that can drive investigation, service action, NCR, CAPA, and management-review trend evidence.

## Target Behavior

- All complaints enter one canonical record type.
- Product traceability, service action, and quality escalation stay linked without duplicate data entry.
- Serious, recurrent, or nonconforming complaints route into NCR or CAPA automatically or by governed prompt.
- Complaint closure is blocked until required triage, investigation, and escalation steps are complete.

## Minimal Data Model

- Extend `Issue` with:
  - complaint class
  - severity
  - reportability assessment
  - investigation required
  - item
  - serial number
  - batch
  - delivery note
  - warranty claim link
  - maintenance visit link
  - NCR link
  - CAPA link
  - closure code
  - complaint owner and supervisor
- Optional bridge record: `Complaint Assessment`
  - if the organization wants classification and reportability review separated from the raw intake ticket

## Enforcement Points

- `Issue.validate` or workflow transition
  - require complaint-classification fields before leaving intake or triage
- `Issue` close transition
  - hard-stop closure when required service, investigation, or escalation fields are incomplete
- `Warranty Claim` creation from complaint
  - map complaint traceability and narrative forward, do not re-enter manually
- `Maintenance Visit.on_submit`
  - write the actual service outcome back into the linked complaint path
- complaint severity or recurrence rule
  - prompt or auto-create NCR seed and notify quality owner

## User Guidance And Teaching

- Add guided buttons on the complaint record for:
  - `Create Warranty Claim`
  - `Create Maintenance Visit`
  - `Create NCR`
  - `Open Complaint Traceability`
- Show the complaint workflow step and missing-required-field checklist on the form.
- Use role-based prompts so support users can triage without needing deep quality knowledge, while QA sees the escalation decision points.

## System Ownership

- ERPNext owns the complaint intake, product traceability, service transaction, and linked customer evidence.
- HRMS owns owner, supervisor, and department resolution for assignment and escalation.
- `qms` owns the governed exception, CAPA, and management-review linkage once the complaint crosses into formal quality handling.
- The bridge layer owns severity rules, reportability prompts, and complaint-to-NCR/CAPA routing.

## Reports And Views

- complaint aging and backlog
- complaints by item, serial, batch, and customer
- severity and recurrence trend
- complaint-to-NCR or CAPA conversion
- open serious complaint escalation report

## Priority And Sequencing Note

This slice should start at the front of Phase 3 because it creates the first formal exception intake path from daily operational use:

- the intake and service records already exist
- the current gap is governed quality routing and closure control
- it becomes the main doorway into NCR and CAPA

## Acceptance Criteria

- Each complaint can be traced to customer and affected product context.
- Service actions stay linked to the complaint without duplicate entry.
- Complaint closure is blocked when required investigation or escalation is incomplete.
- Quality can trend complaint severity, recurrence, and escalation outcome from the system.
