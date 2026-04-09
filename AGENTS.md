# ERPNext Docs Guidelines

This file governs documentation work under:

- `/home/prince/frappe-bench-15/apps/erpnext/docs`

Use it to continue the ISO 13485, ERPNext, `qms`, and HRMS research in a consistent way.

## 1. Folder Contract

Organize by purpose, not by the history of the investigation.

- `existing_sop/`
  - regulatory-approved source documents
  - approved SOPs, forms, checklists, logs, lists, agreements, and original office files
  - do not rewrite or reorganize approved originals unless explicitly requested
- `iso13485/`
  - active ISO-facing deliverables
  - ERP/qms/HRMS workflow SOPs
  - enhancement-assumed SOPs
  - `work_to_be_done/` implementation packets
- `reference/`
  - internal research, architecture notes, baseline explorations, presentation notes, and next-iteration planning
  - use this folder for material that helps write SOPs but is not itself an SOP deliverable

Do not create new history folders such as:

- `*_end_state`
- `*_phase2`
- `*_final2`

unless explicitly requested.

## 2. Source Of Truth Order

When the sources disagree, use this order:

1. local repo code and DocType JSON
2. current approved source documents in `existing_sop/`
3. active SOP deliverables in `iso13485/`
4. reference material in `reference/`
5. older README or marketing text

Rules:

- repo truth beats remembered assumptions
- approved source documents beat draft interpretation
- if a custom app doc differs from actual app surface, say so explicitly

## 3. Required Skills

Use these skills when their trigger condition applies.

### `frappe-arch-hunter`

Use when:

- tracing ERPNext, `qms`, or HRMS workflows
- mapping DocType ownership
- reconstructing transaction, quality, training, or approval flows
- producing Mermaid flow notes from code evidence

Default output shape:

1. scope and assumptions
2. ownership graph
3. write paths and side effects
4. reconstructed flows
5. Mermaid diagram
6. unresolved gaps and next probes

### `doc`

Use when:

- reading or reviewing `.docx` approved SOPs or forms
- preserving layout matters
- extracting structured content from regulatory-approved documents

### `spreadsheet`

Use when:

- reading or reviewing `.xlsx`, `.csv`, or `.tsv` source artifacts
- checking controlled lists, trackers, or matrices
- preserving formulas or formatting matters

### `acpx`

Use when:

- you want headless delegated review through ACP
- you want named persistent sessions for long-running ISO/QMS analysis threads

If `acpx` runtime fails, record it in the relevant prompt log and fall back to built-in subagents.

## 4. Research Modes

Use one of these modes deliberately.

### Approved SOP Review

Goal:

- assess what the approved source documents already establish
- identify what still remains manual, undefined, or outside ERP/qms/HRMS

Typical outputs:

- approved-SOP alignment notes
- research verdict
- presentation-safe wording
- next-iteration queue

### ERPNext Baseline

Goal:

- understand built-in ERPNext behavior without custom apps

Store outputs under:

- `reference/erpnext_baseline/`

### Cross-App Architecture

Goal:

- map ERPNext + `qms` + HRMS + bridge logic into one operating model

Store outputs under:

- `reference/erp_qms_hrms_architecture/`

### SOP Drafting

Goal:

- turn repo truth plus approved policy into employee-usable SOPs

Store outputs under:

- `iso13485/sops/current_erp/`
- `iso13485/sops/enhancement_assumed/`

### Work-To-Be-Done Drafting

Goal:

- define the minimum ERP/qms/HRMS or bridge changes needed for an enhancement-assumed SOP

Store outputs under:

- `iso13485/work_to_be_done/`

## 5. Delegation Patterns

Prefer narrow, bounded delegation.

### Built-in subagent split patterns

Use domain slices such as:

- document control
- record control
- supplier control
- training and competence
- complaint and CAPA
- audit and management review

Use app slices such as:

- ERPNext baseline
- `qms` surface
- HRMS surface
- bridge or exception design

Subagent prompt rules:

- specify the exact files or folders to inspect
- ask for evidence-backed output
- say `No edits` unless implementation is requested
- ask for concise findings, not generic ISO explanations

### `acpx` session patterns

If using persistent `acpx` sessions, prefer names like:

- `approved-sop-review`
- `erpnext-baseline`
- `cross-app-architecture`
- `supplier-control`
- `training-and-competence`
- `complaint-capa`
- `audit-and-management-review`

Notes from this workspace:

- put global options before `exec` or `prompt`
- example:
  - `acpx --approve-all --timeout 180 exec '...'`
- if ACP runtime returns quota or internal errors, stop retry loops and use built-in subagents instead

## 6. Office-File Extraction Pattern

When reviewing approved `.docx` or spreadsheet files:

1. do not edit originals in `existing_sop/`
2. extract working text or tabular views into `/tmp/...`
3. keep those extracts ephemeral unless the user explicitly wants them preserved

Recommended temporary paths:

- `/tmp/existing_sop_extracts/`
- `/tmp/docs/`
- `/tmp/spreadsheets/`

Environment note for this bench:

- prefer `/home/prince/.pyenv/versions/3.14.2/bin/python` for office-file extraction
- `python3` on `PATH` may not have the same installed packages

If required packages are missing, prefer:

- `uv pip install --system python-docx openpyxl pandas`

## 7. Output Patterns

### For reference architecture docs

Prefer numbered files like:

- `00_...`
- `01_...`
- `02_...`

These belong in:

- `reference/erp_qms_hrms_architecture/`
- `reference/erpnext_baseline/`

### For SOP deliverables

Use:

- `SOP-<DOMAIN>-<NNN>_<slug>.md`

Examples:

- `SOP-QMS-001_document_and_record_control.md`
- `SOP-PUR-002_supplier_qualification_and_release.md`

### For implementation packets

Use:

- `WTD-SOP-<DOMAIN>-<NNN>_<slug>.md`

### For prompt history

Keep one prompt log per packet area:

- `PROMPT_LOG.md` in the relevant folder

Prompt logs should preserve:

- user brief
- working assumptions
- subagent or `acpx` attempts
- notable runtime limitations

## 8. Readme Discipline

Whenever the structure changes:

- update `iso13485/README.md`
- update `reference/README.md`
- update the local packet `README.md`

Do not leave stale folder names or old read paths in active README files.

## 9. How To Turn Research Into More SOPs

Follow this sequence:

1. read the approved source documents in `existing_sop/`
2. confirm actual repo truth in ERPNext, `qms`, and HRMS
3. decide whether the SOP is:
   - current ERP
   - enhancement-assumed
4. draft the SOP under `iso13485/sops/...`
5. if enhancement-assumed, draft the matching `WTD-SOP-*`
6. update the relevant README and prompt log

Do not place presentation notes, authority summaries, or planning documents inside `iso13485/` unless they are directly part of the SOP deliverable set.

## 10. Completion Rule

Do not say the research is fully closed unless:

1. approved source documents for the in-scope domains have been reviewed
2. ERPNext, `qms`, and HRMS mappings are evidence-backed
3. unresolved items are implementation gaps, not discovery gaps
4. the presentation wording does not overclaim approval or implementation status
