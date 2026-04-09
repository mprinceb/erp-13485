# Scope And Method

## Scope

- Codebase: `erpnext` app in the current bench
- ERP focus: built-in modules, built-in Quality Management module, built-in Quality Inspection controls
- Compliance viewpoint: ISO 13485-style documented processes, traceability, review, inspection, CAPA-like follow-up, and auditable records

## Important Boundaries

- This is a code and workflow architecture packet, not legal certification advice.
- ERPNext provides transaction controls and records; it does not by itself satisfy every ISO 13485 requirement.
- Several controls still need SOP, role assignment, approval policy, training, and retention rules outside the code.

## Analysis Method

1. Inventory ERPNext modules and quality-related DocTypes.
2. Trace server-side validation and write paths.
3. Separate direct code evidence from compliance inference.
4. Translate flows into SOP-oriented module notes and diagrams.

## Architecture Lens

The practical question for each module is:

- What record starts the flow?
- What downstream records are created?
- Where can quality be required, linked, or blocked?
- What evidence remains after submission or cancellation?
- What employee SOP steps are necessary so auditors can reconstruct the process?

## Reading Key

- `Direct evidence`: behavior visible in local code.
- `Inference`: likely compliance implication or SOP need based on that behavior.
