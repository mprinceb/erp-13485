# WTD-SOP-QMS-005 Controlled-Role Training, Competence, And Authority

## Objective

Turn HRMS lifecycle events, qms document release, and sensitive ERP or qms actions into one governed training, acknowledgment, competence, and authority model with auditable gate results.

## Target Behavior

- A user entering a controlled role receives the correct training and acknowledgment assignments automatically.
- A released SOP revision creates revision-specific obligations for the affected users instead of relying on external circulation only.
- Practical competence and release authority are explicit records with scope and expiry, not informal knowledge.
- Sensitive actions are allowed only when the acting user is active, current, and authorized for that action.
- Every allowed or blocked decision is retrievable later as audit evidence.

## Minimal Data Model

- New record: `Controlled Role Requirement`
  - department, designation, process, operation, inspection role, or release role
  - required SOP or work instruction
  - required training type
  - practical competency required flag
  - authority required flag
- New record: `Training Assignment`
  - employee
  - source such as onboarding, transfer, released document, or recertification
  - linked `QMS Document`
  - due date
  - status
- New record: `Training Acknowledgment`
  - employee
  - `QMS Document`
  - revision
  - acknowledgment timestamp
- New record: `Competency Requirement`
  - controlled action
  - required assessor type
  - validity period
- New record: `Competency Assessment`
  - employee
  - controlled action
  - assessor
  - result
  - valid until
- New record: `Authority Grant`
  - employee
  - authority type such as review, release, inspection, concession, shipment release
  - scope
  - effective dates
  - approver
- New record: `Qualification Gate Log`
  - acting user
  - action
  - source transaction
  - allowed or blocked
  - missing prerequisite or justification

## Enforcement Points

- `QMS Document.on_update`
  - when status becomes `Released`, generate applicability-based assignments and revision acknowledgments
- HRMS `Employee Onboarding.on_submit` and `on_update_after_submit`
  - create the initial controlled-role obligations after onboarding tasks are in place
- HRMS `Employee.on_update`
  - refresh authority state when department, designation, reports-to, or status changes
- HRMS `Employee Transfer.on_submit`
  - revoke old role authority and create new assignments
- HRMS `Employee Separation.on_submit`
  - disable future approval or release authority and reassign open quality work
- HRMS `Training Result.on_submit`
  - close linked assignments and refresh competence or authority state
- shared qualification gate
  - callable first from `QMS Document` review or release actions and then from selected ERP sensitive actions

## User Guidance And Teaching

- Show the current effective SOP and assignment status on sensitive ERP and qms forms.
- Add guided buttons for:
  - `Open Current SOP`
  - `Acknowledge Revision`
  - `Open Training Assignment`
  - `Request Assessment`
- Show a pre-submit checklist on sensitive forms when authority or training is required.
- When blocked, tell the user exactly which training, acknowledgment, competence, or authority record is missing or expired.

## System Ownership

- HRMS owns employee lifecycle, department, designation, reporting line, and instructor-led training-event evidence.
- `qms` owns controlled-document release, applicability, revision acknowledgment rules, and authority policy.
- ERPNext owns the transaction where the sensitive work is actually executed.
- The bridge layer owns cross-app assignment generation, authority evaluation, and gate logging.

## Reports And Views

- controlled-role requirement matrix
- pending onboarding qualification queue
- overdue training and acknowledgment report
- expired competence and authority report
- blocked and allowed qualification gate log
- qualified-at-time-of-action retrieval report

## Priority And Sequencing Note

This slice should start immediately after Phase 0 and run in parallel with approved-supplier control:

- it determines who is allowed to act in every later quality gate
- it reuses real HRMS lifecycle and training surfaces that already exist
- it gives the shortest path to compliance-by-default once one shared gate service exists

Before relying on HRMS training completion for authority, fix or replace the current `Training Result` completion handoff so it updates the real `Training Event` completion field cleanly.

## Acceptance Criteria

- A new or transferred controlled-role user receives the right assignments without duplicate entry.
- A released controlled document can create revision-specific obligations automatically.
- A configured sensitive action can be blocked when the acting user is not current or not authorized.
- Supervisors and QA can see why a user was blocked and what is needed to clear the gate.
- Audit users can retrieve who was qualified and authorized at the time of action.
