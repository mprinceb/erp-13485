# WTD-SOP-QMS-007 Internal Quality Audit And Finding Escalation

## Objective

Create a small audit layer that plans audits, records findings, links evidence, escalates serious findings into NCR or CAPA, and feeds management review.

## Minimal ERP Changes

- Add `Internal Audit`, `Audit Checklist`, and `Audit Finding` records.
- Add finding severity, clause, process, evidence, owner, due date, and closure fields.
- Add links from findings to `Non Conformance`, `Quality Action`, retraining, and change records.
- Add management-review reporting over audit status and recurrence.

## Workflow And Automation

- Schedule audits and assign auditors and auditees.
- Require objective evidence on each finding.
- Escalate major or systemic findings into NCR or CAPA.
- Block audit closure until required findings and linked actions are complete.

## Reports And Views

- audit schedule and completion status
- open findings aging report
- audit finding recurrence report
- audit-to-CAPA escalation report

## Acceptance Criteria

- The organization can plan and execute internal audits in-system.
- Findings, evidence, and closure actions are retrievable without manual spreadsheet stitching.
- Major findings route into the same governed quality-exception backbone used elsewhere in the architecture.
