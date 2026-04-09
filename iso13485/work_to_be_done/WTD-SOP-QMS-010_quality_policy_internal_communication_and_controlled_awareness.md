# WTD-SOP-QMS-010 Quality Policy, Internal Communication, And Controlled Awareness

## Objective

Turn qms document release and distribution into a controlled awareness system that knows who must receive, acknowledge, and stay current on quality-policy and critical internal communication documents.

## Minimal ERP Changes

- Add document applicability rules based on department, role, controlled function, or organization-chart node.
- Add revision-specific acknowledgment records for released policy and critical communication documents.
- Add onboarding and transfer triggers from HRMS into qms awareness assignment.
- Add overdue-awareness dashboards and manager follow-up queues.
- Show current effective policy or required communication links inside affected ERP transactions where useful.

## Workflow And Automation

- On `QMS Document` release, generate recipient sets from the controlled distribution and applicability rules.
- Create or refresh acknowledgment tasks for affected users.
- On HRMS onboarding or transfer, evaluate whether new policy or communication awareness is required.
- Escalate overdue acknowledgments to line managers or quality owners.

## Reports And Views

- released document distribution history
- overdue awareness or acknowledgment list
- onboarding and transfer awareness gap report
- critical communication completion dashboard

## Acceptance Criteria

- Users can prove who received and acknowledged each controlled quality-policy or critical communication revision.
- HRMS role changes automatically trigger a communication or awareness review.
- Controlled communications do not depend on informal announcements alone.
