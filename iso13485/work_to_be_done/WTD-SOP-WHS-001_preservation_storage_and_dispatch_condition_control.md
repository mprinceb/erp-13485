# WTD-SOP-WHS-001 Preservation, Storage, And Dispatch Condition Control

## Objective

Turn native warehouse, batch, serial, and dispatch transactions into a controlled preservation model that distinguishes released stock from held stock and captures shipment-condition evidence where required.

## Minimal ERP Changes

- Add storage-condition class and approved-warehouse mapping for controlled items or warehouses.
- Add a dispatch-condition or packaging checklist before final shipment release.
- Add explicit hold or quarantine reason tracking for condition failures.
- Add an excursion path from storage or dispatch failure into NCR handling.
- Add near-expiry and storage-condition exception reporting for controlled stock.

## Workflow And Automation

- Default rejected or suspect material into the correct hold or rejected warehouse.
- Warn or block dispatch when required condition checks are incomplete.
- Prevent release of stock that is expired, quarantined, or under unresolved condition deviation.
- Create NCR review automatically when storage or dispatch-condition failures affect released or releasable product.

## Reports And Views

- held and rejected stock by warehouse
- near-expiry controlled material list
- dispatch-condition checklist completeness report
- storage and dispatch excursion register

## Acceptance Criteria

- Users can distinguish released, held, rejected, and transit stock inside ERP.
- Expired or held product cannot be shipped through the normal path.
- Packaging and dispatch-condition evidence is retrievable for controlled shipments.
