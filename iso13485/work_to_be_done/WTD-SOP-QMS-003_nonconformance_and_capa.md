# WTD-SOP-QMS-003 Nonconformance And CAPA

## Objective

Turn the native `Non Conformance`, `Quality Action`, and `Quality Action Resolution` doctypes into a closed-loop NCR and CAPA process tied to real ERP exception events.

## Target Behavior

- A complaint, rejected inspection, audit finding, or other exception can open one governed NCR chain.
- Containment, disposition, root cause, actions, and effectiveness remain visible in one connected record set.
- CAPA tasks are assigned and tracked in-system with responsible user and due date.
- NCR and CAPA closure are blocked until required stages are complete.

## Minimal Data Model

- Extend `Non Conformance` with:
  - source doctype and source name
  - item
  - quantity
  - serial number
  - batch
  - containment
  - disposition
  - concession
  - root cause
  - owner
  - effectiveness due date
  - effectiveness result
  - closure approved by
- Extend `Quality Action` with:
  - NCR link
  - complaint link
  - effectiveness review fields
  - closure approval fields
- Reuse `Quality Action Resolution` as the action-task table, with optional light extension for evidence attachment or effectiveness note

## Enforcement Points

- `Quality Inspection` reject path
  - prompt or auto-create NCR seed
- complaint escalation path
  - create NCR from complaint severity or recurrence rule
- `Non Conformance` workflow transition
  - block disposition approval until containment exists
- NCR close transition
  - block closure until required `Quality Action` items and effectiveness review are complete
- `Quality Action` validation or workflow transition
  - block closure when open resolution rows remain

## User Guidance And Teaching

- Add guided buttons from source transactions for `Create NCR` and `Open CAPA`.
- Show the NCR stage and required next fields on the form.
- Show open action owners and due dates directly in the NCR record.
- When an NCR is blocked, show whether the blocker is containment, disposition, open action, or missing effectiveness review.

## System Ownership

- ERPNext owns the originating transaction and the NCR/CAPA execution records.
- HRMS owns owner, supervisor, and department resolution for action accountability.
- `qms` owns downstream document, training, and change-control impact where the NCR drives those governed actions.
- The bridge layer owns cross-linking between source event, NCR, complaint, CAPA, and management-review aggregation.

## Reports And Views

- open NCR aging
- open CAPA action due report
- NCR by source, item, supplier, customer, and process
- effectiveness verification due or overdue
- recurrence and repeated-failure trend

## Priority And Sequencing Note

This slice should follow immediately after complaint intake is governed in Phase 3:

- the complaint path is one of the main sources of NCR creation
- rejected inspection and supplier-deviation routing can reuse the same backbone
- effectiveness and recurrence reporting become meaningful only when NCR intake is consistent

## Acceptance Criteria

- A complaint or rejected inspection can be escalated into one traceable NCR chain.
- Users can see containment, disposition, CAPA tasks, and effectiveness evidence together.
- NCR or CAPA closure is prevented when mandatory quality steps are incomplete.
- Management can trend recurrence and overdue effectiveness from the system.
