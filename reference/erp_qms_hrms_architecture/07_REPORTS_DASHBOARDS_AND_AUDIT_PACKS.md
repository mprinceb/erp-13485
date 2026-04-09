# Reports, Dashboards, And Audit Packs

The end-state should make audit retrieval and management visibility a normal system behavior, not a manual scramble.

## 1. Operational Dashboards

| Dashboard | Primary system | Sources | Main users |
| --- | --- | --- | --- |
| Incoming inspection blockers | ERPNext plus bridge | `Purchase Receipt`, `Subcontracting Receipt`, `Quality Inspection`, qualification gate result | stores, incoming QC, buyers |
| Supplier quality status | ERPNext plus approved-supplier module | `Supplier Scorecard`, `Approved Supplier`, NCR trend | buyers, supplier quality |
| Manufacturing hold-point blockers | ERPNext plus bridge | `Work Order`, `Job Card`, in-process QI, gate result, NCR | production, QA |
| Finished-goods release queue | new release module | `Release Dossier`, final QI, unresolved exceptions, authority result | QA release, warehouse |
| Complaint and service queue | ERPNext | `Issue`, `Warranty Claim`, `Maintenance Visit` | support, service, QA |
| NCR / CAPA aging | ERPNext quality extensions | NCR and CAPA workflow states | QA, process owners |

## 2. HRMS And qms Dashboards

| Dashboard | Primary system | Sources | Notes |
| --- | --- | --- | --- |
| Effective documents dashboard | `qms` | `QMS Document`, `Obsolete Document` | current released docs, pending reviews, overdue reviews |
| Revision acknowledgment dashboard | `qms` | `Training Assignment`, `Training Acknowledgment`, `Distribution Log` | overdue and not-yet-read users by revision |
| Controlled-role onboarding dashboard | HRMS plus qms | `Employee Onboarding`, training assignments, authority setup tasks | new hires not yet released into controlled work |
| Competency and recertification dashboard | qms plus HRMS | competency records, training results, employee status | expiring or failed qualifications |
| Authority and approval dashboard | qms plus HRMS | authority matrix, employee active status, delegations | approval bottlenecks and coverage gaps |
| External document dashboard | `qms` | `External Origin Document` | expiring regulatory and supplier docs |
| Role change and offboarding review dashboard | HRMS plus qms | `Employee Transfer`, `Employee Separation`, open authority or training tasks | pending revocation or reassignment actions |

## 3. Management Review Pack

Recommended pack sections:

1. Document control
   - overdue reviews
   - recently released documents
   - obsolete documents pending disposal
2. Training and competency
   - overdue assignments
   - blocked critical users
   - failed competency assessments
   - recertification due
3. Organization and authority
   - open authority gaps
   - delegated authority nearing expiry
   - controlled-role onboarding backlog
4. Supplier and incoming quality
   - scorecard standings
   - approved-supplier expiries
   - incoming rejection trend
5. Production and release
   - hold-point failures
   - final release holds
   - release dossier backlog
6. Complaints and post-delivery
   - complaint aging
   - recurring product issues
   - field correction trends
7. NCR / CAPA
   - open NCRs
   - CAPA aging
   - effectiveness overdue
8. Change and audit
   - open change actions
   - audit findings by severity
   - recurring finding themes

## 4. Audit Packs

### Document-control audit pack

- current master list of documents
- obsolete document register
- sample release and acknowledgment logs
- sample change package linked to superseded document

### Training and qualification audit pack

- role-to-document training matrix
- overdue training list
- acknowledgment record sample
- competency assessment sample
- training event and training result sample from HRMS
- evidence of who was qualified at time of action

### Supplier and incoming-quality audit pack

- approved supplier list
- supplier scorecard trend
- sample PO release with supplier approval evidence
- sample receipt with QI and NCR escalation
- evidence that the inspector or release authority was qualified

### Manufacturing and release audit pack

- sample work order trace
- sample hold-point inspection evidence
- qualification gate result for the operator
- sample release dossier / DHR
- sample shipment trace to customer

### Complaint and CAPA audit pack

- sample complaint intake
- linked service record
- assigned owner and supervisor evidence from HRMS
- linked NCR
- linked CAPA with effectiveness verification

### Employee lifecycle and authority audit pack

- controlled-role onboarding sample
- role-change requalification sample
- separation-driven authority revocation sample
- delegated authority sample with effective dates

## 5. Current Repo Truth Vs End-State Reporting

| Area | Exists today | Missing today |
| --- | --- | --- |
| Document master lists | Yes in `qms` | acknowledgment and competency rollups |
| HR lifecycle and training reports | Yes in HRMS | QMS-linked qualification and controlled-role views |
| ERP operational quality views | Partially through ERP reports and lists | assembled cross-domain review pack |
| Authority and qualification-at-time-of-action evidence | No coherent set | requires bridge log and authority model |
| Complaint, NCR, CAPA, audit dashboards | No coherent set | requires new models and reports |
| Release dossier retrieval | No | requires new release module |

## 6. Report Design Rules

Each pack should be generated from linked source records.

Do not:

- copy transaction values into presentation-only tables
- maintain manual audit spreadsheets after the record already exists in ERP
- maintain a second employee hierarchy in qms when HRMS already stores the people truth

Every sensitive quality action should be able to answer:

- who performed it
- whether they were active and qualified
- who approved it
- whether that approver held valid authority at the time
