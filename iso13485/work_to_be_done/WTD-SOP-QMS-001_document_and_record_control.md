# WTD-SOP-QMS-001 Document And Record Control

## Objective

Enable revision-controlled SOP and record management inside ERPNext using the existing `Quality Procedure` hierarchy as the parent structure.

## Minimal ERP Changes

- Add a `Controlled Document Revision` DocType linked to `Quality Procedure`.
- Add fields for document type, revision, effective date, superseded revision, reviewer, approver, retention period, and status.
- Add workflow states: `Draft`, `In Review`, `Approved`, `Effective`, `Obsolete`.
- Add a training acknowledgment child table or assignment model for affected employees.
- Add validation so only one revision per procedure can be `Effective`.

## Workflow And Automation

- Route revisions for review and approval before release.
- Auto-mark the previous effective revision obsolete when a new one becomes effective.
- Notify affected users of new or revised effective documents.
- Track overdue acknowledgments and periodic document review due dates.

## Reports And Views

- Effective controlled document register
- Obsolete document register
- Overdue acknowledgment report
- Documents due for periodic review

## Acceptance Criteria

- Users can retrieve the current effective SOP for any procedure.
- Review and approval history is retained in ERP.
- Obsolete revisions are visible but clearly segregated from current use.
- Training acknowledgment evidence can be shown during audit.
