# WTD-SOP-TRC-003 Identifier, Barcode, And Label Governance

## Objective

Turn ERPNext item barcodes and scan-enabled stock flows into a governed identifier and label-control model suitable for regulated traceability use.

## Minimal ERP Changes

- Add controlled identifier classification at `Item` level for regulated products.
- Add released label template and print-revision linkage for regulated identifier printing.
- Add label issuance and reprint logs by item, batch, serial range, user, and template revision.
- Add print authorization for regulated labels.
- Add hold and exception routes for missing, duplicate, or unreadable identifiers.

## Workflow And Automation

- Validate identifier uniqueness and code structure at item setup.
- Force regulated label printing through the approved template route.
- Record every label print or reprint event.
- Add scan verification at selected stock, packing, or shipment checkpoints.

## Reports And Views

- regulated identifier master list
- label issuance and reprint log
- identifier discrepancy register
- scan-verification exception report

## Acceptance Criteria

- Users can prove which approved identifier and label revision was used for a product lot or serial range.
- Unauthorized or uncontrolled reprints are visible.
- Barcode scanning and released traceability records use the same governed identifier set.
