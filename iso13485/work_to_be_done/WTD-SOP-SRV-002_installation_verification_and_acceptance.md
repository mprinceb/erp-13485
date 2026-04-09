# WTD-SOP-SRV-002 Installation Verification And Acceptance

## Objective

Turn `Installation Note` into a controlled installation-acceptance record that captures site verification, customer acceptance, and quality escalation without forcing teams into external spreadsheets.

## Minimal ERP Changes

- Add installation checklist, acceptance result, and customer sign-off fields to `Installation Note`.
- Make acceptance evidence mandatory before submit for installation-controlled products.
- Add explicit result values such as accepted, partial, and failed.
- Add a follow-up creation path into `Maintenance Visit`, complaint, or NCR based on the installation result.
- Add overdue-installation and pending-acceptance views from delivered items.

## Workflow And Automation

- Create `Installation Note` from the shipped transaction with delivered item and serial context prefilled.
- Block submission when checklist completion or acceptance evidence is missing.
- Auto-create follow-up service work for partial or failed installations.
- Auto-route installation failures with potential product-quality impact into complaint or NCR review.

## Reports And Views

- delivered but not installed list
- installed but not customer-accepted list
- failed or partial installation register
- installation exceptions by item, customer, and service owner

## Acceptance Criteria

- Users can prove which delivered serialized units were successfully installed and accepted.
- Installation failures cannot disappear into remarks alone; they create visible follow-up work.
- Quality-significant installation failures can be traced into complaint or NCR handling.
