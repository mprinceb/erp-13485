# WTD-SOP-SAL-002 Customer Requirement Review And Order Acceptance

## Objective

Add a controlled review and approval layer to quotation and sales-order acceptance so ERP stores the accepted requirement set, any clarifications, and the approval decision.

## Minimal ERP Changes

- Add a requirement-review checklist to `Quotation` or `Sales Order`.
- Add mandatory fields or flags for controlled products, customer-specific requirements, labeling constraints, and exception review.
- Add approval routing for orders that need regulated review, deviation, or change.
- Add links from the commercial record to concession, change, or complaint records where needed.

## Workflow And Automation

- Require review completion before conversion from quotation to sales order for controlled cases.
- Block order acceptance when required attachments, clarifications, or approvals are missing.
- Keep revised requirement sets versioned through the ERP communication trail and linked records.

## Reports And Views

- orders pending requirement review
- orders accepted with deviation or concession
- customer-specific requirement exception report
- requirement-review aging report

## Acceptance Criteria

- Controlled orders cannot be accepted without a completed review.
- The accepted customer and product requirement set is visible and auditable in ERP.
- Review exceptions route into formal change or concession handling instead of email-only decisions.
