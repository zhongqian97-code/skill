---
name: "review-detailed-design"
description: "Audit AS-IS reconstruction or authorize TO-BE implementation with hard full-stack and database gates."
---

# Review Detailed Design

Review a detailed design using one of two explicit modes:

1. **AS-IS RECONSTRUCTION AUDIT** — determine whether a source-derived design faithfully and completely reconstructs the pinned implementation for equivalent reproduction.
2. **TO-BE IMPLEMENTATION AUTHORIZATION** — determine whether a proposed design is ready to authorize implementation.

Never mix their inputs, verdicts, or authority.

## Core principles

- Review contracts and evidence, not page count or polish.
- Select the mode before the readiness gate.
- Frontend, backend, interaction contracts, and persistence are first-class implementation surfaces.
- If persistent state is applicable, names or an ER diagram are not a database design.
- If a UI and backend are applicable, component and endpoint lists are not an interaction design; require field-level round trips and state transitions.
- A defect in the source implementation belongs in an AS-IS appendix/conflict ledger. An implementation detail present in source but missing from the document is a reconstruction defect.
- Do not lower the standard because a document calls itself a draft.
- Never authorize implementation from an AS-IS document.

Read `references/review-standard.md` completely before reviewing.

## 1. Select review mode

### AS-IS RECONSTRUCTION AUDIT

Use when the document was derived from an existing codebase and is intended for learning, comparison, or reuse baseline.

Required inputs:

- repository and full pinned commit;
- feature boundary and behavior IDs;
- implementation-surface census;
- AS-IS design;
- evidence, coverage, conflict, and unknown ledgers;
- access to the pinned source or sufficient immutable evidence.

Verdicts:

- `COMPLETE RECONSTRUCTION`;
- `PARTIAL RECONSTRUCTION`;
- `BLOCKED RECONSTRUCTION`.

These verdicts describe reconstruction quality only and never authorize implementation.

### TO-BE IMPLEMENTATION AUTHORIZATION

Use when the document proposes a target implementation.

Required inputs:

- frozen scope and stable requirement/acceptance IDs;
- implementation-ready design;
- traceability matrix;
- test/verification and release/rollback plans;
- owners and approvers;
- baseline/version/change history.

Verdicts:

- `PASS`;
- `CONDITIONAL PASS`;
- `FAIL`;
- readiness failure is reported as `FAIL (not ready)`.

Only unconditional `PASS` authorizes implementation.

If mode is ambiguous, stop with `FAIL (not ready — review mode and artifact intent are ambiguous)`.

## 2. Run the mode-specific readiness gate

### AS-IS readiness

Do not score until all exist:

- pinned source identity;
- explicit feature boundary;
- behavior catalog;
- implementation census;
- evidence coordinates;
- conflict/unknown ledger;
- reconstruction status claimed by the author.

If unavailable, report `BLOCKED RECONSTRUCTION` or `PARTIAL RECONSTRUCTION` depending on whether a meaningful audit is possible. Do not ask for REQ/AC, approvers, rollout, or TO-BE acceptance criteria as AS-IS readiness inputs.

### TO-BE readiness

Do not score until all required TO-BE inputs exist and are internally readable. Missing scope, REQ/AC, baseline, owners/approvers, traceability, or verification/release artifacts yields `FAIL (not ready)`.

Readiness controls whether scoring is meaningful; it must not hide obvious severe findings. Record any immediately visible critical issue even when stopping.

## 3. Determine applicability

For each surface mark `applicable`, `not applicable with evidence`, or `unknown`:

- frontend;
- synchronous contracts;
- asynchronous contracts;
- backend/domain;
- database/persistence;
- external dependencies;
- build/config/deployment;
- security/operations;
- migration/rollback/restore.

A bare “N/A” is not evidence. Unknown material applicability fails the relevant gate.

## 4. Run shared implementation-completeness gates

Use the gate definitions in `references/review-standard.md`.

- S1 Scope, behavior, and complete implementation census
- S2 Frontend states and client design
- S3 Synchronous/asynchronous contracts and field lineage
- S4 Backend responsibilities and executable flows
- S5 Database schema and empty-database reconstruction
- S6 State, transactions, concurrency, failures, and recovery
- S7 Security, tenancy, privacy, and external boundaries
- S8 Build, configuration, deployment, observability, rollback, and restore
- S9 Verification, traceability, evidence, and closure

### Immediate hard failures

The relevant gate fails immediately when:

- persistence is applicable but exact physical objects, columns, keys/constraints/indexes, schema source, or construction/migration order are missing;
- a database can not be built from empty state using the document and cited artifacts;
- frontend and backend are applicable but request/response and field-level round trips are missing;
- UI states or backend failure paths are reduced to a happy path;
- transaction, concurrency, retry/idempotency, or recovery behavior is material but unspecified;
- an inventory item, behavior, contract, or database object is material and unexplained;
- the document relies on inference while claiming an exact contract;
- build/deploy/migration/rollback steps are necessary but absent.

## 5. Apply mode-specific gates

### AS-IS fidelity gates

- A1 Source pinning and evidence integrity
- A2 Forward and backward implementation trace
- A3 Source-of-truth arbitration and conflict handling
- A4 Source defects separated from document omissions
- A5 Equivalent-reproduction counterfactual

For A5, ask whether a second engineer can reproduce the frontend, backend, interaction contracts, persistent schema, failures, and clean-environment build without reopening the source except to verify cited locations.

A source defect does not fail reconstruction if the document accurately records the observed defect, its evidence, and effect. It belongs in the appendix. The same behavior or schema existing in source but absent from the document is a reconstruction omission and fails the relevant shared gate.

### TO-BE authorization gates

- T1 Stable REQ/AC and bidirectional traceability
- T2 Decision closure and accountable owners
- T3 Verification-ready acceptance and tests
- T4 Migration/release/rollback feasibility
- T5 Independent implementer convergence

Two competent implementers should not have to make materially different decisions about UI, contracts, data schema, state, concurrency, security, migration, recovery, or acceptance.

## 6. Record findings

Each finding includes:

- stable ID;
- severity;
- shared/mode-specific gate;
- exact document location;
- evidence or missing artifact;
- why it affects fidelity or implementation;
- minimal closure action;
- owner and status when applicable.

Severity:

- `S0`: catastrophic safety, security, data-loss, or irreversible integrity risk;
- `S1`: material authorization/fidelity blocker with likely severe production impact;
- `S2`: hard-gate completeness blocker;
- `S3`: important improvement that does not independently block;
- `S4`: editorial or optional improvement.

Any S0/S1/S2 means a TO-BE design cannot pass and an AS-IS reconstruction cannot be complete.

## 7. Produce the verdict

### AS-IS

- `COMPLETE RECONSTRUCTION`: all applicable shared and A gates pass; no S0/S1/S2; no material unknowns.
- `PARTIAL RECONSTRUCTION`: useful reconstruction exists but any applicable gate remains open.
- `BLOCKED RECONSTRUCTION`: trustworthy audit cannot proceed because source, scope, generated artifacts, dependencies, or evidence are unavailable.

State clearly: `Implementation authorization: NOT APPLICABLE / NOT GRANTED`.

### TO-BE

- `PASS`: all shared and T gates pass; no S0/S1/S2; independent implementation is authorized.
- `CONDITIONAL PASS`: only non-implementation-affecting pre-start administrative conditions remain. It does not authorize implementation until conditions close and are re-reviewed.
- `FAIL`: any hard gate fails or any S0/S1/S2 remains.

Use `templates/review-report.md`. Do not modify the reviewed document unless the user separately asks for revisions.

## 8. Minimum correction set

List the shortest concrete changes required to reach the next verdict. Separate:

- defects in the reviewed document;
- defects/inconsistencies in the source implementation;
- unavailable evidence or external blockers;
- optional improvements.

This separation is mandatory in AS-IS mode.

## Handoff

For an AS-IS result, hand the completed baseline to `detailed-design-writing` only if the user wants a separate TO-BE design. Then review that TO-BE document in authorization mode.

For a TO-BE result, only unconditional PASS may be used as implementation authorization.
