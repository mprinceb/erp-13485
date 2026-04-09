# Implement Now Vs Extend QMS Vs New Modules

## Implement Now With Current Repo Truth

| Action | Why now |
| --- | --- |
| Harden ERP quality settings to hard-stop release behavior | immediate compliance improvement without code expansion |
| Use ERPNext transaction docs as the canonical execution evidence layer | avoids duplicate entry from day one |
| Use current `QMS Document`, `External Origin Document`, `Obsolete Document`, `Change Request Ticket`, and `Change Management` as the document/change baseline | these are real and already coded |
| Use HRMS `Employee Onboarding`, `Employee Transfer`, `Employee Separation`, `Training Event`, and `Training Result` as the current people and lifecycle evidence layer | these are real workflows with real history |
| Use HRMS employee structure, `reports_to`, department, designation, branch, and approver fields as the current people source of truth | best available source for authority and assignment context |
| Use `Supplier Scorecard`, `Issue`, `Warranty Claim`, `Maintenance Visit`, and ERP quality review docs consistently | strong immediate operational signals already exist |
| Use `QMS Explorer` and `QMS Viewer` as the current controlled document access pattern | better than unmanaged attachment download behavior |

## Priority Parallel Slice After Phase 0

| Slice | Why pull it forward |
| --- | --- |
| Approved supplier control from `SOP-PUR-002` | ERP already has supplier-level PO gating and receipt inspection gates, so item-scope approval can be added with a small bridge and gives immediate procurement compliance value |
| Controlled-role training and authority from `SOP-QMS-005` | it determines who is allowed to act, and pairs well with form guidance and release gating |
| Manufacturing hold points from `SOP-MFG-001` | ERP manufacturing already has the execution records and in-process inspection hook point, so the remaining gap is a narrow server-side hard stop |

## Priority Next Slice After The Foundation Gates

| Slice | Why it comes next |
| --- | --- |
| Complaint intake and escalation from `SOP-QMS-004` | `Issue` is already a strong intake shell, and `Warranty Claim` plus `Maintenance Visit` already capture service facts; the missing layer is governed classification, escalation, and closure |
| NCR / CAPA depth from `SOP-QMS-003` | `Non Conformance` and `Quality Action` already exist, so closed-loop containment, disposition, root cause, and effectiveness can be layered without inventing a new exception universe |
| Release dossier / DHR from `SOP-TRC-002` | ERP already holds the evidence in execution documents; the missing step is governed assembly, approval, and freeze |

## Light Adaptation In HRMS

| Adaptation | Why it belongs in HRMS |
| --- | --- |
| Mark controlled roles or controlled departments and designations | onboarding and transfer already run there |
| Add quality-impact flags or callbacks on onboarding, transfer, and separation | HRMS is the natural event source |
| Reuse training events and results for instructor-led or scheduled training evidence | already implemented and familiar to HR users |
| Reuse supervisor and department-approver resolution patterns for escalation ownership | current HRMS logic already traverses the department hierarchy |

## Extend Existing qms App

| Extension | Why it belongs in qms |
| --- | --- |
| Activate intentional hooks, notifications, and review reminders | code already exists in qms |
| Add training assignment, acknowledgment, and competency | naturally tied to document release and controlled procedures |
| Extend `Organization Chart` into a quality authority overlay backed by HRMS references, or replace it cleanly | qms should own authority rules, not raw employee master data |
| Extend document release with impact preview and training generation | fits current qms document workflow |
| Extend change control with ERP impact mapping and implementation evidence | current change workflow is real but incomplete |
| Build management review packs for documents, training, authority, and change status | qms is the right aggregation layer for governed content |

## New Bridge / New Workflow Surfaces

| Module or workflow | Why new |
| --- | --- |
| HRMS to qms lifecycle sync and qualification gate service | no current app owns cross-app enforcement cleanly |
| Qualification gate log for sensitive actions | needed for audit evidence of who was current or expired at time of action |
| Approved supplier register and item-scope approval | neither ERPNext nor current qms models this cleanly |
| Hold-point state propagation and server-side manufacturing gate | ERP has manufacturing records, but no current cross-document hold-point enforcement model |
| Complaint quality workflow on top of `Issue` and `Warranty Claim` | intake exists, but quality logic does not |
| Extended NCR / CAPA closure model | ERP quality doctypes need a deeper lifecycle than they have today |
| Release dossier / DHR | missing entirely |
| Internal audit program and findings | missing entirely |

## Keep In ERPNext, Do Not Move Into qms Or HRMS

| Domain | Reason |
| --- | --- |
| Incoming inspection and receipt release | the stock transaction is already the source of truth |
| Manufacturing execution and in-process inspection evidence | operators already work in ERP manufacturing docs |
| Final release and shipment release | release gates are tied to stock and delivery docs |
| Service and warranty activity | customer and serial context already exists in ERP service records |

## Out Of Scope For The First Delivery Slice

| Area | Reason |
| --- | --- |
| Full design control system | too large and not needed to make daily execution compliant-by-default |
| Full risk file / FMEA platform | no current base model in inspected apps |
| Regulatory reporting engine | depends on jurisdiction-specific requirements outside this repo baseline |
| Full LMS replacement | not needed while HRMS training events plus qms acknowledgment cover the first operating model |
