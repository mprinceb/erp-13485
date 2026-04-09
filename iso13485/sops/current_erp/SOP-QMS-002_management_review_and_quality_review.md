# SOP-QMS-002 Management Review And Quality Review

## Status

- ERP fit: `A` current ERPNext
- ISO clauses: `5.4.1`, `5.6`, `8.4`, `8.5`
- Primary ERP records: `Quality Procedure`, `Quality Goal`, `Quality Review`, `Quality Meeting`, `Quality Action`

## Purpose

Define how management review is planned, recorded, actioned, and retained inside ERPNext.

## Preconditions

- Each controlled business process exists in `Quality Procedure`.
- Each process that requires periodic oversight has a `Quality Goal` with frequency and objectives.
- Responsible users have access to quality records but submit authority is limited by role.

## Procedure

1. Create or maintain the process structure in `Quality Procedure`.
2. For each procedure that needs periodic review, define a `Quality Goal`.
3. Set the review frequency and measurable objectives on the goal.
4. Let the ERP scheduler create due `Quality Review` records from the goal.
5. Before the review meeting, process owners update the review rows with actual values and pass/fail status.
6. Hold the review meeting and record the discussion in `Quality Meeting`.
7. If any review objective fails or requires action, open `Quality Action` records.
8. Keep the review open until all child review rows are complete.
9. Keep the action open until all child resolution rows are closed.
10. At the next meeting, confirm status of prior actions and record that follow-up in meeting minutes.

## Records To Retain

- `Quality Procedure`
- `Quality Goal`
- auto-created and completed `Quality Review`
- `Quality Meeting`
- `Quality Action`

## ERP Control Notes

- This SOP works in current ERPNext because reviews can be scheduled from goals and actions can be tracked to closure.
- This SOP does not replace a document-control SOP.
- If the organization needs formal review approval, signature, or escalation workflow, that belongs in a separate enhancement.

