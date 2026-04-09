# WTD-SOP-SRV-003 Customer Property And Customer-Owned Product Control

## Objective

Turn existing asset, service, and complaint records into a governed customer-property control flow so the organization can prove identification, custody, condition, and disposition of customer-owned property without separate spreadsheets.

## Minimal ERP Changes

- Add a customer-property flag or classification on the relevant receipt or service intake path.
- Add mandatory condition-on-receipt and disposition fields for customer-owned property.
- Add a controlled linkage from service or complaint records to the customer-owned `Asset`, serialized unit, or customer-property receipt record.
- Add explicit lost, damaged, unsuitable, and returned states with escalation guidance.
- Add a dashboard or list for customer property currently in-house and awaiting action.

## Workflow And Automation

- Guide users to create or link a customer-owned `Asset` or equivalent receipt record at intake.
- Require location or custodian updates through `Asset Movement` whenever responsibility changes.
- Surface guided actions from service records such as `Create Customer Property NCR` or `Record Damage / Loss`.
- Route damaged, lost, or unsuitable customer property into complaint, NCR, or concession review.
- Keep final return or disposition visible so customer-owned property cannot remain orphaned in the system.

## Reports And Views

- customer property in-house register
- customer property by custodian or location
- damaged or unsuitable customer property log
- customer property awaiting return or disposition
- customer property linked to complaint or NCR

## Acceptance Criteria

- Users can prove what customer-owned property is currently in-house and who is responsible for it.
- Service and complaint records link back to the specific customer property involved.
- Loss, damage, or unsuitable condition cannot be hidden in remarks alone.
- Final disposition or return is visible and auditable.
