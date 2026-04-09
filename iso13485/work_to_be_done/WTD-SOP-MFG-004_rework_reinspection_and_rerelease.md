# WTD-SOP-MFG-004 Rework, Re-Inspection, And Re-Release

## Objective

Turn ERPNext corrective job cards into a governed rework flow that blocks rerelease until corrected product has passed the required repeat inspection.

## Minimal ERP Changes

- Add source-defect, disposition, and affected-quantity fields to corrective `Job Card`.
- Require linkage from corrective work to the originating failed inspection or defect source.
- Require repeat `Quality Inspection` before the affected quantity can be released.
- Add hold or block logic on affected lot, batch, serial, or work-order quantity during rework.
- Add escalation from repeated or critical rework failures into NCR or CAPA.

## Workflow And Automation

- Create corrective `Job Card` directly from failed inspection or job-card context.
- Auto-mark the affected quantity as on hold when rework begins.
- Prevent release or downstream shipment until repeat inspection passes.
- Add dashboards for open rework, failed re-inspection, and recurring corrective operations.

## Reports And Views

- open corrective job cards
- rework awaiting repeat inspection
- failed re-inspection register
- poor-quality or rework cost trend by item, operation, and workstation

## Acceptance Criteria

- Users can trace every reworked quantity back to the original defect and forward to the repeat inspection result.
- Reworked product cannot silently return to released status without verification.
- Recurring rework patterns are visible and can trigger NCR or CAPA action.
