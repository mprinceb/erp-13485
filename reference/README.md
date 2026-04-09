# Reference Docs

This folder contains internal reference material used to write and extend SOPs.

These are not the approved SOP set itself.

## Folder Purpose

| Folder | Purpose | Use it for |
| --- | --- | --- |
| `erpnext_baseline/` | First-pass ERPNext-only discovery notes | understanding built-in ERPNext behavior before adding `qms` and HRMS |
| `erp_qms_hrms_architecture/` | Cross-app architecture, research verdict, presentation notes, and next-iteration planning | writing future SOPs and workflow packs across ERPNext, `qms`, and HRMS |

## Why This Exists

The earlier structure preserved the history of the work:

- `iso13485_erpnext` meant the early ERPNext-only reasoning pass
- `iso13485_end_state` meant the later cross-app architecture pass

That structure was useful while the work was evolving, but not for long-term use.

The current rule is:

- approved and working ISO/SOP deliverables stay under `docs/iso13485/`
- approved source documents stay under `docs/existing_sop/`
- internal architecture, research, and presentation material stays under `docs/reference/`

## Read Order For New SOP Work

1. `erpnext_baseline/README.md`
2. `erp_qms_hrms_architecture/README.md`
3. `../iso13485/README.md`

Use that sequence when drafting additional SOPs with ERP/qms/HRMS workflows.
