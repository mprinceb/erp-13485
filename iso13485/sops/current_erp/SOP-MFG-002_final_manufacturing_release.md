# SOP-MFG-002 Final Manufacturing Release

## Status

- ERP fit: `A` current ERPNext
- ISO clauses: `7.5.1`, `7.5.8`, `7.5.9`, `8.2.6`
- Primary ERP records: `BOM`, `Work Order`, `Stock Entry`, `Quality Inspection`, `Batch`, `Serial No`

## Purpose

Define how finished goods are inspected and released from manufacturing in ERPNext.

## Preconditions

- The BOM defines whether inspection is required.
- The BOM or item defines the correct inspection template.
- Traceability settings for batch or serial control are correctly configured for the product class.

## Procedure

1. Create and release the `Work Order`.
2. Execute manufacturing operations per route and record production progress.
3. Before finished-goods posting, create the manufacturing `Stock Entry`.
4. If the BOM requires inspection, create and complete the linked `Quality Inspection`.
5. Submit the `Quality Inspection`.
6. Submit the manufacturing `Stock Entry` only after accepted inspection.
7. Confirm that batch or serial records were created or linked correctly for the finished good.
8. If final inspection is rejected, stop release and route the event into nonconformance handling.

## Records To Retain

- `BOM`
- `Work Order`
- manufacturing `Stock Entry`
- linked `Quality Inspection`
- batch and serial records

## ERP Control Notes

- This SOP works in current ERPNext because final release is gated through stock-entry validation.
- It does not cover mandatory in-process hold points on each operation. That belongs in `SOP-MFG-001`.

