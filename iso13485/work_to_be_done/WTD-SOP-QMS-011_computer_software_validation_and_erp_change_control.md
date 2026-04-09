# WTD-SOP-QMS-011 Computer Software Validation And ERP Change Control

## Objective

Extend the current `qms` document and change skeleton into a defensible software-validation workflow for ERPNext, `qms`, HRMS, integrations, and quality-critical customizations.

## Minimal ERP Changes

- Add a software-application register with owner, scope, risk, and quality relevance.
- Add software-validation fields and child tables to the change package for protocol, test result, defect, approval, rollback, and post-implementation review.
- Create software-focused `Change Type` and `Questionnaire` templates.
- Require deployment approval and validation evidence before software change closure.
- Link software changes to revised SOPs, training, and acknowledgment where user behavior changes.

## Workflow And Automation

- Start all quality-relevant software change through `Change Request Ticket`.
- Expand impact questions automatically from the chosen software change type.
- Block `Change Management` close until required validation evidence and new controlled document versions are present.
- Trigger document distribution and training impact generation when the software change updates controlled instructions.
- Add a post-implementation review checkpoint for production changes affecting QMS records or release logic.

## Reports And Views

- software application register
- open software changes by risk or status
- validation evidence missing report
- deployed changes awaiting post-implementation review
- software changes requiring retraining or document release

## Acceptance Criteria

- Every quality-relevant software change has a controlled request, impact review, validation evidence, and close decision.
- Document changes and software behavior changes remain linked.
- Deployment cannot be treated as closed on narrative remarks alone.
- The organization can retrieve a software-change evidence pack for audit without reconstructing it manually.
