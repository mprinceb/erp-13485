# Gap Register and SOP Backlog

## Priority gaps

| Priority | Gap | Why it matters | Required action |
| --- | --- | --- | --- |
| High | `Warn` settings can let missing, draft, or rejected inspections pass | Weakens objective evidence and release control | Lock all quality-related stock settings to `Stop` unless a formal exception process exists |
| High | `Quality Procedure` is not a controlled-document module | Procedure control, approval, effective date, and training are not enforced | Add document-control SOP and, if needed, custom DocType or separate document system |
| High | Rejected inspection does not auto-open nonconformance or CAPA | Rejection can stop a transaction but not trigger closed-loop quality action | Define mandatory NCR/CAPA SOP and consider automation |
| High | In-process `Job Card` inspection is scaffolded but not mandatory | Shop-floor release can depend on user discipline | Define mandatory job-card inspection steps and consider customization |
| High | ERPNext does not assemble one device-history-style packet | Audit evidence remains fragmented | Define a release dossier or DHR assembly SOP |
| Medium | Outbound quality gate starts at delivery, not sales order | Commercial approval and quality release are separated | Define sales-order review vs shipment-release responsibilities in SOP |
| Medium | Feedback intake is limited to `User` or `Customer` | Complaint, service, supplier, and field feedback paths are not modeled directly | Extend SOP or model custom feedback sources |
| Medium | Repo search found no direct quality integration in `support`, `maintenance`, `assets`, or `crm` | Complaint handling, service feedback, and post-market servicing are not naturally tied into quality records | Decide whether to extend ERPNext or use the separate `qms` app for those processes |

## Suggested SOP library

- `SOP-QMS-001` Procedure control, approval, and training acknowledgment
- `SOP-QMS-002` Management review in ERPNext using goals, reviews, meetings, and actions
- `SOP-QMS-003` Nonconformance, disposition, CAPA, and effectiveness check
- `SOP-PUR-001` Incoming inspection for purchased and subcontracted items
- `SOP-MFG-001` In-process inspection on job cards
- `SOP-MFG-002` Final inspection and finished-good release on stock entry
- `SOP-SAL-001` Outgoing inspection and shipment release
- `SOP-TRC-001` Batch, serial, and release dossier retention
- `SOP-FIN-001` Finance reconciliation for controlled material movements

## Recommended next engineering passes

1. Decide whether the separate `qms` app should become part of the target architecture.
2. Trace complaint handling and servicing flows.
   - Current ERPNext quality records do not show direct code links into `support`, `maintenance`, `assets`, or `crm`.
3. Decide whether in-process release must be mandatory.
   - If yes, add server-side job-card enforcement.
4. Decide whether lot-release or DHR assembly should be automated.
   - If yes, create a custom summary record or print format that assembles the evidence chain.

