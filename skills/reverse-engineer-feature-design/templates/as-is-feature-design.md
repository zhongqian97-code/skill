# AS-IS Reconstructed Detailed Design: <feature>

> Status: PARTIAL RECONSTRUCTION — NOT COMPLETE
> This document reconstructs observed implementation at a pinned revision. It is not the original authors' design document.

## 0. Provenance and safety

- Repository / license:
- Requested ref / full commit:
- Retrieval time / clone mode:
- Submodule / LFS / sparse / symlink / dirty state:
- Selected platform, build profile, flags, toolchain:
- Unexamined variants:
- Allowed execution/network:
- Tools and versions:
- Source snapshot / analysis output locations:

## 1. Scope card

- Feature and aliases:
- Observable triggers:
- Inputs:
- Outputs and side effects:
- Included:
- Excluded:
- External/shared boundaries:
- Closure statement:

## 2. Observable behaviors

| ID | Trigger | Preconditions | Observable result | Failure result | Evidence | Status |
|---|---|---|---|---|---|---|

## 3. Evidence summary

- Evidence ledger:
- Search log:
- Conflict ledger:
- Critical UNKNOWNs:
- Reproduction commands:

## 4. Context and architecture

Describe context, containers/processes, components/modules, code entities, ownership, and trust boundaries. Bind every material node/edge to evidence IDs.

## 5. End-to-end implementation flows

For each behavior: trigger → entry → dispatch → core logic → data/state → side effects → output/error.

Cover normal, rejection, timeout, cancellation, retry, duplicate, concurrency, partial failure, restart, and recovery where applicable.

## 6. Implementation map

| Behavior | Entry/symbol | Components | Data/state | Side effects | Output/error | Evidence |
|---|---|---|---|---|---|---|

## 7. Interfaces and contracts

When applicable, provide separate **source-resolution order** and **conflict/arbitration order** decision tables. Document UI states, API/RPC/CLI schemas, events, errors, auth, ordering, idempotency, timeout, retry, cancellation, limits, and compatibility.

## 8. Data, state, and consistency

Document source of truth, schema, ownership, legal states/transitions, invariants, transactions, cache/index synchronization, concurrency, crash windows, migration, retention, backup, restore, and reconciliation.

## 9. Errors, concurrency, and recovery

Document creation and propagation of failures, race/ordering behavior, locks/tasks/channels, lifecycle, duplicate handling, retries/fallback/compensation, restart, and operator recovery.

## 10. Security and privacy

Document identities, authorization, trust boundaries, secrets, sensitive data flows, logs/telemetry, external calls, attack surfaces, and negative evidence.

## 11. Configuration, build, generated code, and dependencies

Show the selected variant and generator/schema/template → output → consumer chain. List excluded variants and external implementation boundaries.

## 12. Quality and operations

Record observed or declared performance/resource behavior, limits, telemetry, health, deployment, compatibility, rollback, recovery, and any UNKNOWN quality targets.

## 13. Tests and reproduced observations

| Scenario | Test/command | Input/environment | Assertion/observation | Output hash | Limitation | Evidence |
|---|---|---|---|---|---|---|

## 14. History and rationale

Separate current behavior from evidence-backed historical rationale. Record incomplete history and alternative explanations.

## 15. Reflexion audit

| Item | Observed AS-IS | Hypothesized intent | Convergence / divergence / absence | Evidence / confidence |
|---|---|---|---|---|

## 16. Unknowns, conflicts, and open frontier

| ID | Unknown/conflict | Impact | Why unresolved | Evidence needed | Owner/source |
|---|---|---|---|---|---|

## 17. Reusable lessons and optional TO-BE ideas

Keep this section separate from AS-IS. For each lesson/idea state the problem it solves, prerequisites, tradeoffs, license constraints, and when not to copy it.

## 18. Traceability and closure

| Behavior | Design sections | Implementation evidence | Test/runtime evidence | Unknowns | Status |
|---|---|---|---|---|---|

- Two-engineer counterfactual:
- Closure criteria result:
- Final status:
- Dynamic-evidence necessity: required / not required, with rationale
- Label crosswalk: AS-IS→CONFIRMED, INFERRED→INFERRED, UNKNOWN→OPEN, TO-BE→PROPOSED
- Handoff path: learning/comparison evidence audit | target-project reuse planning
- Evidence/closure audit reviewer and result (no implementation authorization):
- Target TO-BE design path, if reuse is intended:
- `detailed-design-writing` handoff status, if reuse is intended:
- `review-detailed-design` is requested only for the separate target TO-BE design
