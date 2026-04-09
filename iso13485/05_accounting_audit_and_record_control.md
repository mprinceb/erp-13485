# Accounting, Audit Evidence, and Record Control

## Direct ERPNext behavior

- `Quality Inspection` is not a stock or GL posting document.
  - In the traced controller, its write paths mainly update source-document links and child-row references (`erpnext/erpnext/stock/doctype/quality_inspection/quality_inspection.py:114`, `erpnext/erpnext/stock/doctype/quality_inspection/quality_inspection.py:233`).
- `Purchase Invoice` and `Sales Invoice` can carry `quality_inspection` at item level (`erpnext/erpnext/accounts/doctype/purchase_invoice_item/purchase_invoice_item.json:440`, `erpnext/erpnext/accounts/doctype/sales_invoice_item/sales_invoice_item.json:605`).
- The inspection gate on invoices only matters when the invoice affects stock.
  - `StockController.validate_inspection()` exits early for `Sales Invoice` and `Purchase Invoice` when `update_stock` is false (`erpnext/erpnext/controllers/stock_controller.py:1024`).
- On inbound posting, `Purchase Receipt` is still the main release-and-accounting hinge.
  - In the traced inbound path, receipt submission is where stock and accounting consequences proceed after the inspection gate.
- This means the financial record is supporting evidence for released material movement, not a substitute for the operational quality-release record.

## Audit chain to preserve

| Event | Quality release record | Operational record | Financial or stock evidence |
| --- | --- | --- | --- |
| Receive controlled material | `Quality Inspection` | `Purchase Receipt` or stock-affecting `Purchase Invoice` | stock movement, payable posting |
| Receive subcontracted FG | `Quality Inspection` | `Subcontracting Receipt` | stock movement and downstream invoice |
| Post finished goods | `Quality Inspection` | manufacturing `Stock Entry` | stock movement, valuation impact |
| Ship controlled material | `Quality Inspection` | `Delivery Note` or stock-affecting `Sales Invoice` | stock movement, receivable posting |

## SOP-ready accounting rules

1. Treat the operational document as the release anchor.
   - Finance should not treat a commercial invoice as proof of quality release.
2. Reconcile by document chain, not by amount alone.
   - For each controlled lot or serial, the auditable chain should be:
     - item master and inspection policy
     - source transaction
     - linked `Quality Inspection`
     - resulting stock and finance posting
3. If invoices update stock:
   - Enforce the same quality rule on invoices as on receipts or deliveries.
4. If invoices do not update stock:
   - Keep quality release tied to the delivery or receipt document and make that mandatory in the SOP.

## Inferred ISO 13485 gaps

- A pure financial invoice is not a quality gate.
  - If `update_stock` is false, invoice submission does not enforce inspection (`erpnext/erpnext/controllers/stock_controller.py:1024`).
- ERPNext does not assemble a retention packet automatically.
  - Audit readiness depends on the organization defining a retained record set and retention schedule.
- There is no built-in automatic bridge from rejected inspection to finance hold.
  - The business must define whether rejected material blocks invoicing, credit release, or revenue recognition.
