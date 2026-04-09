# WTD-SOP-TRC-002 Device History Record And Release Dossier

## Objective

Assemble native ERP manufacturing, inspection, traceability, and shipment evidence into one governed release-ready packet for each batch, lot, or serialized device scope.

## Target Behavior

- A reviewer can open one release-dossier record and see the full release evidence chain.
- Missing inspections, missing traceability links, or unresolved exceptions are visible before sign-off.
- Release approval is attributable to a named authority and timestamp.
- The approved packet is frozen as an audit snapshot instead of being rebuilt live each time.

## Minimal Data Model

- New record: `Release Dossier`
  - item
  - company
  - work order
  - finished-goods stock entry
  - batch
  - serial scope
  - delivery note or shipment link
  - release status
  - completeness status
  - unresolved exception status
  - release authority
  - approval date and time
  - frozen snapshot reference
- Optional child table: `Release Dossier Evidence`
  - evidence type
  - linked doctype
  - linked name
  - required flag
  - present flag

## Enforcement Points

- generate from `Stock Entry`, `Batch`, `Serial No`, or `Delivery Note`
  - gather the evidence chain automatically
- dossier approve or release action
  - hard-stop if required evidence is missing or linked exceptions remain unresolved
- shipment release check
  - verify a current approved dossier exists where policy requires it

## User Guidance And Teaching

- Add direct guided actions on manufacturing and shipment forms:
  - `Generate Release Dossier`
  - `Open Existing Dossier`
  - `Open Missing Evidence`
  - `Open Linked NCR/CAPA`
- Show the completeness checklist and unresolved-exception summary on the dossier form.
- When approval is blocked, show the exact missing evidence instead of a generic release failure.

## System Ownership

- ERPNext owns manufacturing, quality inspection, lot or serial traceability, and shipment evidence.
- `qms` owns the governed document, checklist, and approval context that defines what must be present.
- HRMS plus the authority bridge own who is allowed to approve or release the dossier.
- The new release-dossier layer owns evidence assembly, freeze, and retrieval.

## Reports And Views

- pending release dossiers
- dossiers with missing evidence
- dossiers blocked by open NCR or CAPA
- released lots or serial scopes by approver and date
- audit retrieval by item, batch, serial, or shipment

## Priority And Sequencing Note

This slice should start at the front of Phase 4 after the release-critical transaction gates and exception backbone are stable:

- the evidence chain already exists in ERP
- the missing gap is governed assembly and freeze
- the packet becomes defensible only when complaint, NCR, CAPA, and release-gate data are already trustworthy

## Acceptance Criteria

- One dossier record can present the full release evidence chain for the scoped lot or serials.
- Missing inspections or unresolved deviations block release approval.
- Release approval is attributable to a named authority and timestamp.
- Audit users can retrieve the frozen packet quickly by batch, serial, work order, or shipment.
