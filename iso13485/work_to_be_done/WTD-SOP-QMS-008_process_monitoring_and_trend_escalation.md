# WTD-SOP-QMS-008 Process Monitoring And Trend Escalation

## Objective

Turn `Quality Goal` and `Quality Review` from a manual quality register into an operating review layer that consumes ERP evidence and escalates failures automatically.

## Minimal ERP Changes

- Add KPI source mapping, owner, threshold, and escalation rule to monitored objectives.
- Prefill or assist review values from ERP reports or transaction summaries.
- Add repeated-trend and failed-review escalation into `Quality Action`, NCR, CAPA, complaint, or management review.
- Add overdue-review and repeated-failure dashboards.
- Add governed linkage between review findings and cross-app exception records.

## Workflow And Automation

- Use the existing scheduled `Quality Review` creation as the review trigger.
- Auto-populate known metrics where the report source is deterministic.
- Require owner commentary when objectives fail or deteriorate materially.
- Open follow-up action records automatically for failed objectives according to the configured escalation rule.

## Reports And Views

- overdue quality reviews
- failed objectives and repeated-trend dashboard
- process KPI review completion report
- open quality actions by originating review

## Acceptance Criteria

- Process metrics are reviewed inside ERP using live transaction evidence rather than duplicate external trackers.
- Failed or adverse trends create visible, owned follow-up records.
- Management review can retrieve current process-monitoring evidence directly from the ERP and QMS record chain.
