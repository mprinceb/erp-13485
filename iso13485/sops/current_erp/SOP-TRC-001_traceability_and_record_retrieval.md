# SOP-TRC-001 Traceability And Record Retrieval

## Status

- ERP fit: `A` current ERPNext
- ISO clauses: `4.2.5`, `7.5.8`, `7.5.9`
- Primary ERP records: `Item`, `Batch`, `Serial No`, `Quality Inspection`, `Purchase Receipt`, `Stock Entry`, `Delivery Note`

## Purpose

Define how traceability and record retrieval is performed for controlled product in ERPNext.

## Preconditions

- Controlled products use the correct batch or serial configuration.
- All inspection-related transactions are linked through `Quality Inspection`.

## Procedure

1. Identify the batch or serial number under investigation.
2. Retrieve the inbound receipt records tied to that batch or serial.
3. Retrieve the related `Quality Inspection` records for incoming, in-process, or outgoing control.
4. Retrieve manufacturing records when the batch or serial was produced internally.
5. Retrieve outbound shipment records tied to the same batch or serial.
6. Assemble the evidence chain for audit, investigation, or recall review.

## Records To Retain

- `Batch`
- `Serial No`
- linked receipts, stock entries, delivery notes, and quality inspections
- any action or nonconformance records tied to the same product history

## ERP Control Notes

- ERPNext already stores the underlying chain.
- This SOP is about disciplined retrieval, not automatic dossier assembly.
- If the organization wants one-click release packets, use `SOP-TRC-002`.

