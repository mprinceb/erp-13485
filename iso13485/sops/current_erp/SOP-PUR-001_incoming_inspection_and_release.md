# SOP-PUR-001 Incoming Inspection And Release

## Status

- ERP fit: `A` current ERPNext
- ISO clauses: `7.4.3`, `7.5.11`, `8.2.6`, `8.3.2`
- Primary ERP records: `Item`, `Purchase Receipt`, `Subcontracting Receipt`, `Purchase Invoice`, `Quality Inspection`

## Purpose

Define how purchased and subcontracted product is received, inspected, accepted, rejected, and released in ERPNext.

## Preconditions

- Controlled items have `inspection_required_before_purchase` enabled where needed.
- Controlled items have the correct `quality_inspection_template`.
- `Stock Settings` related to inspection are configured to `Stop` unless an approved exception policy exists.

## Procedure

1. Create the `Purchase Receipt` or `Subcontracting Receipt`.
2. Record item, lot, serial, quantity, and warehouse details accurately on each line.
3. If any quantity is visibly nonconforming, record rejected quantity and segregation-related details on the receipt line.
4. Create the linked `Quality Inspection` from the inbound transaction.
5. Complete sample size, lot or serial references, and all required readings.
6. Submit the `Quality Inspection`.
7. If the inspection is accepted, submit the receipt.
8. If the inspection is rejected, hold the receipt from release and follow the NCR/CAPA procedure.
9. If finance uses stock-updating `Purchase Invoice`, do not bypass the same quality logic.

## Records To Retain

- `Item` inspection settings
- `Purchase Receipt` or `Subcontracting Receipt`
- linked `Quality Inspection`
- batch and serial evidence
- rejected-quantity and segregation evidence
- retained-sample evidence when applicable

## ERP Control Notes

- This SOP works because ERPNext already blocks or warns on missing, unsubmitted, or rejected inspection for inbound controlled items.
- Supplier approval status is not part of this SOP because built-in inbound blocking is item/QI driven, not supplier-quality driven.

