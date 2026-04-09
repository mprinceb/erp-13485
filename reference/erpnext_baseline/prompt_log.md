# Prompt Log

This file keeps the working prompts and delegation prompts used for this architecture packet.

## User Prompt

> we have to explore erpnext app from the point of view of iso 13485. and quality module of it's.
> it have purchase, sales, accounting, manufacturing etc and many more, for which an organisation have to define SOP. as the workflows are already there in erpnextm thus we should have actionable sop which tells employees how to do things in erp, so to have auditable records while being compliant.
> so for this purpose, take each module, identify flows and workflows and how quality is managed as per erp. produce markdowns with charts/diagrams so to purpose the architecture of how things will go.
> Use Subagents, required skill, ask me for anything. keep notes of our prompts in a file as well to not forget anything

## Skills Used

- `frappe-arch-hunter`: workflow tracing across DocTypes, controllers, and linked records
- `frappe-staff-engineer`: decomposition, architecture packet structure, and risk framing
- `frappe-helper`: reserved for official docs cross-checks where needed

## Assumptions Logged

- Primary scope is core ERPNext, not the separate custom `qms` app.
- The packet will focus deeply on ISO 13485-relevant operational modules, and provide a relevance map for the rest.
- The output is architecture-plus-SOP guidance, not legal certification advice.

## Subagent Prompts

### Core Quality

> You are analyzing the local codebase at /home/prince/frappe-bench-15/apps. Task: produce an evidence-backed summary of ERPNext core quality features relevant to ISO 13485, limited to built-in ERPNext modules. Focus on `erpnext/erpnext/quality_management` plus stock/manufacturing quality inspection doctypes and reports. Identify:
> 1. Core DocTypes and their purpose
> 2. Main workflows and state changes
> 3. Write paths / automation / schedulers / hooks
> 4. Integration points into other ERPNext modules
> 5. Gaps from an ISO 13485 auditable-process perspective (inference clearly marked)
> 6. Mermaid-ready flow ideas.
> Give file references with line numbers where practical. Do not edit files.

### Procurement / Inventory

> You are analyzing the local codebase at /home/prince/frappe-bench-15/apps. Task: map ERPNext procurement/inventory/accounting workflows from an ISO 13485 auditable-record perspective. Focus on `buying`, `stock`, `subcontracting`, and accounts touchpoints only where they affect purchasing/receipt quality evidence. Identify purchase flow documents, stock receipt/inspection controls, supplier-facing checkpoints, nonconformance-relevant points, and accounting evidence created by these flows. Include how Quality Inspection is enforced or linked. Provide concise evidence with file references and note inferred compliance implications separately. Do not edit files.

### Sales / Manufacturing

> You are analyzing the local codebase at /home/prince/frappe-bench-15/apps. Task: map ERPNext sales/distribution/manufacturing quality-related workflows from an ISO 13485 auditable-record perspective. Focus on `selling`, `stock` delivery, and `manufacturing` modules. Identify order-to-delivery flow, production planning/work order/job card flow, in-process/final inspection points, traceability-related records, and where quality documents attach or block progression. Include file references and clearly separate direct evidence from inference. Do not edit files.
