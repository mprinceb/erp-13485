# SOP-SAL-001 Outgoing Inspection And Shipment Release

## Status

- ERP fit: `A` current ERPNext
- ISO clauses: `7.5.8`, `7.5.9`, `8.2.6`, `8.3.2`
- Primary ERP records: `Item`, `Sales Order`, `Pick List`, `Delivery Note`, `Sales Invoice`, `Quality Inspection`

## Purpose

Define how controlled product is inspected before shipment and released to the customer in ERPNext.

## Preconditions

- Controlled items have `inspection_required_before_delivery` enabled.
- Shipping teams use `Delivery Note` or stock-affecting `Sales Invoice` as the release record.
- Lot and serial selection is under warehouse control.

## Procedure

1. Review the `Sales Order` and prepare the shipment through `Pick List` or `Delivery Note`.
2. Confirm that the exact batch or serial to be shipped is identified.
3. Create the linked outgoing `Quality Inspection` from the outbound line.
4. Complete the inspection readings and confirm traceability data.
5. Submit the `Quality Inspection`.
6. Submit the `Delivery Note` or stock-affecting `Sales Invoice` only after accepted inspection.
7. If the inspection is rejected, hold shipment and route the event into nonconformance handling.

## Records To Retain

- `Sales Order`
- `Pick List` when used
- `Delivery Note` or stock-affecting `Sales Invoice`
- linked `Quality Inspection`
- batch and serial shipment evidence

## ERP Control Notes

- This SOP works because outbound stock-affecting documents can already be gated by `Quality Inspection`.
- The quality gate is not at sales-order approval level. Shipment release is where control becomes enforceable.

