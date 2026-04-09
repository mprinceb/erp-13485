# Current State Inventory

This inventory now uses local repo code as source of truth across:

- `/home/prince/frappe-bench-15/apps/erpnext`
- `/home/prince/frappe-bench-15/apps/qms`
- `/home/prince/frappe-bench-15/apps/hrms`

## 1. ERPNext Transaction Baseline Already Available

The earlier ERP packet remains the baseline for transaction truth:

- `Quality Inspection` and `StockController.validate_inspection()` already gate receipt, stock posting, manufacture output, and delivery release.
- `Job Card` already exposes an in-process QI launch path, but not a server-enforced hold point.
- `Supplier Scorecard` already updates supplier standing and can warn or block RFQs and POs through supplier flags.
- `Issue`, `Warranty Claim`, `Maintenance Visit`, and `Installation Note` already provide support and service evidence.
- `Quality Review`, `Quality Meeting`, `Quality Goal`, `Quality Action`, and `Non Conformance` exist, but the exception loop is lightweight.

## 2. Actual qms App Surface In Code

The local `qms` app is broader than its top-level docs imply.

### Existing doctypes in repo

| Area | Actual surface in code | Notes |
| --- | --- | --- |
| Document control | `QMS Document`, `QMS Document Distribution`, `External Origin Document`, `Obsolete Document` | Real controllers and reports exist |
| Change control | `Change Request Ticket`, `Change Management`, `Change Request Document`, `Change Request Change Type`, `Change Management Document`, `Change Management Question`, `Change Type`, `Questionnaire`, `Questionnaire Question` | This is a meaningful partial workflow already |
| Distribution | `Distribution List`, `Distribution List Member`, `Distribution Log`, `Distribution Log User` | Separate from the child-table distribution model on `QMS Document` |
| People / authority | `Organization Chart` | Tree structure exists, but it overlaps with HRMS org data unless repurposed |
| File trace | `QMS Document Activity` | Viewer logs view, download, print, and edit events |
| Basic records | `Records` | Only title, file, and document number; too shallow for controlled quality records |
| Master data | `QMS Document-Record Type`, `QMS Process Abbreviation` | Main document flow uses these |
| Legacy duplicates | `Document Types`, `Process Abbreviations` | Present, but not the primary doctypes used by `QMS Document` |

### Existing pages, reports, and workspace

| Surface | Repo truth | Notes |
| --- | --- | --- |
| Workspace | `qms/qms/qms/workspace/qms/qms.json` | Exists, but only links a subset of actual doctypes |
| Pages | `qms_explorer`, `qms_viewer` | Not prominent in `qms/docs/*`, but they are real and useful |
| Reports | Master lists plus tracking report | Document-control oriented only |
| API | Zoho editor session, callback, attachment listing, download block helper | Real integration point for in-app controlled editing |

## 3. What qms Really Does Today

### Strongest current capabilities

- `QMS Document` has guarded status transition methods for review, approve, release, and archive.
- `QMS Document` auto-archives prior versions and creates `Obsolete Document` records.
- `Change Request Ticket` can create `Change Management` records and inject questionnaire-based impact questions.
- `Distribution List` plus `Distribution Log` can snapshot who received a distributed document set.
- `QMS Explorer` and `QMS Viewer` already support a more guided in-app document experience than standard file attachments.
- `QMS Document Activity` logs file access events.

### Partial capabilities

- `Organization Chart` exists, but is not tied to approval authority, HR reporting lines, or training requirements.
- `Records` exists, but does not support retention, linkage, approval, or classification.
- Document distribution exists in two models:
  - child-table `QMS Document Distribution`
  - standalone `Distribution List` plus `Distribution Log`
  This is not yet a single coherent controlled-distribution model.

## 4. Actual HRMS App Surface In Code

The local `hrms` app is a live workflow layer, not just master-data forms.

### Evidence examined

- `hrms/hrms/hooks.py`
- `hrms/overrides/employee_master.py`
- `hrms/controllers/employee_boarding_controller.py`
- `hrms/hr/doctype/employee_onboarding/employee_onboarding.py`
- `hrms/hr/doctype/employee_separation/employee_separation.py`
- `hrms/hr/doctype/employee_transfer/employee_transfer.py`
- `hrms/hr/doctype/training_event/training_event.py`
- `hrms/hr/doctype/training_result/training_result.py`
- `hrms/hr/doctype/department_approver/department_approver.py`

### Existing doctypes and constructs in repo

| Area | Actual surface in code | Notes |
| --- | --- | --- |
| Employee master and org placement | ERPNext `Employee` overridden by HRMS; fields such as `department`, `designation`, `reports_to`, `branch`, `leave_approver`, and `expense_approver` exist on the employee master | HRMS extends the employee lifecycle rather than replacing the master doctype |
| Lifecycle workflows | `Employee Onboarding`, `Employee Onboarding Template`, `Employee Separation`, `Employee Separation Template`, `Employee Transfer`, `Employee Promotion`, `Exit Interview` | Real process engines; they create projects and tasks for boarding activities and track role or exit changes |
| Authority helpers | `Department Approver` plus employee approver fields | Current logic resolves HR approvers through department hierarchy |
| Training | `Training Program`, `Training Event`, `Training Result`, `Training Feedback` | Real attendance and completion evidence exists |
| Competency and skills | `Skill`, `Skill Assessment`, `Employee Skill Map` | Present, but thin and not tied to controlled operations |
| Performance and goals | `Appraisal`, `Goal` | Useful as supporting evidence, not quality gating |
| Work timing and assignment | `Shift Assignment`, `Shift Schedule Assignment`, `Shift Type`, `Employee Checkin` | Useful for qualification-at-time-of-action and controlled-work windows |
| People issue / escalation context | `Employee Grievance` | Not a quality record, but demonstrates supervisor and resolver links |

### What HRMS really does today

- `Employee Onboarding` and `Employee Separation` use `Employee Boarding Controller` to create `Project` and `Task` records from onboarding or separation activities.
- `Employee Onboarding.validate_employee_creation()` can block employee creation until mandatory onboarding tasks are complete.
- `Employee Transfer` can move a user, update history, or create a new employee ID when organizational placement changes.
- `Employee Promotion` updates work history and role progression, which makes it a useful trigger for authority review where designation changes matter.
- `Exit Interview` and related exit records provide additional evidence around relieving date and end-of-employment workflow.
- `update_approver_role()` in the HRMS employee override actively manages approver roles on user accounts.
- `Training Event` and `Training Result` create a real submitted record of attendance and completion.
- `Department Approver.get_approvers()` already contains a reusable pattern for department-tree-based authority resolution.

## 5. What HRMS Contributes Today To An ISO-13485-Oriented Operating Model

HRMS is already the best source of truth today for:

- whether a person is an active employee
- which department, designation, company, branch, and reporting line they belong to
- onboarding, transfer, and separation state
- scheduled and completed training events
- shift and assignment context for who was expected to perform controlled work
- supervisor or department-approver context that can be reused for escalation and authority

This means HRMS already materially supports:

- employee onboarding into controlled roles
- role-change and offboarding reviews
- assignment of classroom or instructor-led training
- audit reconstruction of who was employed, where they sat in the organization, and who they reported to at the time

## 6. What HRMS Does Not Yet Provide

HRMS does not currently provide:

- revision-specific SOP acknowledgment
- controlled-document applicability rules
- competency expiry or recertification logic tied to sensitive ERP actions
- quality-specific authority mapping for release, approval, concession, or CAPA closure
- complaint, NCR, CAPA, audit, or supplier-quality workflows
- direct enforcement over ERP transaction submission

`Training Program`, `Training Event`, and `Training Result` are useful, but they are generic training records, not a governed QMS training engine by themselves.

Also note:

- `Employee`, `Department`, `Designation`, and `Branch` remain core ERPNext masters in this bench
- HRMS extends and operationalizes them through hooks, overrides, and linked lifecycle doctypes rather than redefining them locally

## 7. Repo Mismatches Between qms Docs And App Truth

| Claim in docs / README | Repo truth | Assessment |
| --- | --- | --- |
| QMS app mainly has five core doctypes | Actual repo includes distribution lists/logs, org chart, questionnaire, change ticket, records, and activity logging | Docs understate the real surface |
| Daily reminders, weekly reports, monthly cleanup, and notifications are built automation | Functions exist in `qms/qms/qms/tasks.py`, `events.py`, and `notifications.py`, but hooks wiring in `qms/qms/hooks.py` is commented out | Automation code exists but is not active by default |
| Workspace has quick shortcuts and complete navigation | Actual workspace JSON has no shortcuts and exposes only a subset of doctypes | Docs overstate workspace completeness |
| QMS is a complete document management solution | Current app is document and change control centric, not a full ISO 13485 execution layer | Marketing statement, not architecture truth |

## 8. Biggest Capability Gaps Across ERPNext + qms + HRMS Today

| Capability | Current state |
| --- | --- |
| Document control | Partial in `qms`, but missing activation wiring and read-and-understand |
| Employee and authority source data | Exists in HRMS and ERP employee master, but not connected to quality authority rules |
| Training assignment and revision-specific acknowledgment | Missing as a governed cross-app flow |
| Competency / qualification / recertification | Missing as a controlled model |
| Supplier approval by item scope | Missing |
| Complaint-to-quality escalation | Missing |
| NCR / CAPA loop | Partial only in ERPNext, not closed-loop |
| In-process manufacturing hold points | Partial only in ERPNext UI |
| Release dossier / DHR | Missing |
| Internal audit | Missing |
| Design control / DHF / DMR | Missing |

## 9. Current-State Conclusion

Today the repo supports:

- ERPNext as the operational evidence engine
- `qms` as a partially implemented document and change-control app
- HRMS as the people, assignment, and generic training record layer

It does not yet support:

- compliance-by-default through normal ERP use
- training-gated execution
- quality authority based on real employee lifecycle data
- integrated quality exception routing
- one coherent management review evidence layer across transactions, documents, and people
