# WTD-SOP-MFG-005 Workstation Readiness And Environment Control

## Objective

Make workstation and environment readiness visible in ERP before controlled manufacturing work starts, using the existing workstation, maintenance, and HRMS shift structures as the base evidence layer.

## Minimal ERP Changes

- Mark quality-critical workstations, areas, and supporting assets.
- Add a pre-start readiness checklist tied to workstation, shift, or `Job Card`.
- Add environment or cleanliness status fields for processes that require them.
- Add a blocked state and reason when the workstation or environment is not ready.
- Add a deviation route for contamination, line-clearance failure, or readiness failure.

## Workflow And Automation

- Surface readiness status on `Job Card` and prevent start or completion where policy requires a ready state.
- Pull supporting asset-maintenance status into the readiness decision for critical workstations.
- Use HRMS shift assignment or check-in context to confirm assigned coverage where required.
- Create guided actions for `Raise Readiness Deviation`, `Open Maintenance`, or `Open NCR`.
- Keep contamination-specific controls parameterized so they can remain inactive where product scope does not require them.

## Reports And Views

- workstation readiness board
- blocked workstation log
- overdue supporting-maintenance list for quality-critical workstations
- shift coverage vs workstation readiness report
- environment or cleanliness deviation trend

## Acceptance Criteria

- Users can show which workstation and supporting assets were ready at the time of work.
- Required pre-start checks become visible records instead of verbal checks.
- Blocked or non-ready conditions are visible and auditable.
- Contamination or cleanliness-sensitive processes can be layered in without inventing a separate manual system.
