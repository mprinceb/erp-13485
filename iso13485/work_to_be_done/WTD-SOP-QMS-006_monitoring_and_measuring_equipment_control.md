# WTD-SOP-QMS-006 Monitoring And Measuring Equipment Control

## Objective

Turn ERPNext asset-maintenance records into a quality-critical equipment-control model that can support calibration or verification evidence and block invalid equipment from controlled use.

## Minimal ERP Changes

- Flag quality-critical and inspection-critical assets.
- Add calibration or verification status, next due date, and current release or block flag.
- Make certificate attachment mandatory where the maintenance task requires it.
- Add product-impact assessment when equipment is out of tolerance or invalid.
- Add a usage check for controlled inspection or release actions.

## Workflow And Automation

- Auto-mark overdue quality-critical tasks as blocked for controlled use.
- Prevent controlled inspection or release when assigned equipment is blocked or overdue.
- Route out-of-tolerance events into NCR, CAPA, or change review when product impact is possible.

## Reports And Views

- quality-critical equipment due and overdue list
- blocked-equipment report
- calibration certificate completeness report
- out-of-tolerance impact assessment register

## Acceptance Criteria

- Users can identify which equipment is currently valid for controlled quality use.
- Overdue or invalid equipment is blocked from controlled inspection or release.
- Maintenance, certificate, and product-impact evidence is retrievable in one chain.
