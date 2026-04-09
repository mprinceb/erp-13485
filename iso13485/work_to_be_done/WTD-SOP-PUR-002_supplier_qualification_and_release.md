# WTD-SOP-PUR-002 Supplier Qualification And Approved Supplier Release

## Objective

Implement approved-supplier-by-item release control as an early compliance slice using existing ERP buying and stock transactions plus a small new bridge record, without waiting for the full complaint or CAPA program.

## Target Behavior

- Buyers can source controlled items only from approved suppliers in the released scope.
- Receipt users cannot release controlled incoming material if the supplier approval is invalid, expired, suspended, or outside scope.
- Supplier qualification evidence is linked from qms controlled external documents instead of being re-entered into multiple apps.
- Temporary concession use is explicit, permissioned, time-bounded, and auditable.

## Minimal Data Model

- New DocType: `Approved Supplier`
  - `supplier`
  - `company`
  - `status`
  - `effective_from`
  - `review_due_date`
  - `risk_class`
  - `change_notification_required`
  - `approved_by`
  - `reviewed_by`
  - link to qms change or review record
  - optional concession reference
- New child table: `Approved Supplier Scope`
  - `item`
  - `item_group`
  - `purpose` such as `Purchase`, `Subcontract`, or `Both`
  - optional site or company qualifier if needed
- Optional generic `Gate Log` reuse or new quality gate log entry for blocked and allowed release decisions

## Enforcement Points

- `Supplier Quotation.validate`
  - preferred initial mode: warning or guided prompt for controlled items
- `Purchase Order.validate` or `before_submit`
  - required mode: hard stop for controlled items outside approved scope
- `Purchase Receipt.validate` and `before_submit`
  - hard stop when supplier approval is invalid even if PO already exists
- `Subcontracting Receipt.validate` and `before_submit`
  - same hard stop behavior as normal receipt
- `Quality Inspection.on_submit`
  - on rejection, offer or create supplier deviation or NCR seed and update supplier-quality trend inputs
- daily scheduler
  - notify on `review_due_date`
  - expire overdue approvals where policy requires it

## User Guidance And Teaching

- Show approved-supplier state on `Supplier Quotation`, `Purchase Order`, and `Purchase Receipt`.
- Add guided buttons for:
  - `Open Approved Supplier`
  - `Open Supplier Documents`
  - `Request Temporary Concession`
- Add a short submit checklist on PO for controlled items:
  - supplier is approved for scope
  - required supplier document set is linked
  - no open suspension or expired review exists

## System Ownership

- ERPNext owns transactional sourcing, order, receipt, and inspection evidence.
- qms owns the governed supplier-document attachments and linked change-control context.
- HRMS owns the employee and approver identity used to prove who approved or reviewed supplier release.
- The new bridge layer owns approved-supplier release logic and cross-app validation.

## Reports And Views

- approved supplier list by item and item group
- qualification due and overdue report
- blocked PO and blocked receipt attempts
- supplier defect trend from rejected incoming inspections
- temporary concession register

## Parallel Implementation Note

This slice should be pulled forward immediately after Phase 0 and can run in parallel with training and authority work:

- it uses existing ERP gate points in `Purchase Order` and receipt flows
- qms only needs supplier-document linkage, not a full new complaint framework
- HRMS dependency is light and limited to approver identity and authority

## Acceptance Criteria

- Controlled items cannot be released on PO when supplier scope is not approved.
- Controlled items cannot be released on receipt when supplier scope is not approved.
- Approval status, approving authority, due date, and scope are visible from the transaction.
- Supplier qualification evidence and supplier-quality history can be reviewed together.
- Temporary exceptions are explicit and time-bounded, never silent.
