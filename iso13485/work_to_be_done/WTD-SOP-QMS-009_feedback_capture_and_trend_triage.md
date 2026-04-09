# WTD-SOP-QMS-009 Feedback Capture And Trend Triage

## Objective

Turn ERP support, service, and quality-feedback records into one governed signal-capture layer that distinguishes routine feedback from complaints and escalates repeated adverse trends.

## Minimal ERP Changes

- Add complaint-vs-feedback triage at intake for service and support records.
- Add source-product and source-transaction linkage on `Quality Feedback`.
- Add category, severity, owner, and escalation-rule fields for feedback review.
- Add trend thresholds that open `Quality Action` or route into complaint, NCR, or CAPA.
- Add dashboards for repeated negative themes, unresolved feedback, and service-derived quality signals.

## Workflow And Automation

- Prompt service and support users to classify new signals as complaint or feedback.
- Create `Quality Feedback` automatically or through guided action from `Issue`, `Warranty Claim`, or `Maintenance Visit`.
- Feed categorized feedback into scheduled `Quality Review`.
- Open follow-up actions automatically when trend thresholds or severity rules are reached.

## Reports And Views

- open quality feedback by source
- recurring feedback theme dashboard
- service-derived feedback trend report
- feedback escalated to complaint, NCR, or CAPA

## Acceptance Criteria

- Users can capture quality-relevant feedback without duplicate entry outside ERP.
- Formal complaints are separated from routine feedback but remain linked where escalation occurs.
- Repeated adverse feedback cannot remain passive history; it produces visible trend review and owned follow-up.
