---
name: "detailed-design-writing"
description: "Implementation-ready detailed design authoring with traceable requirements, executable contracts, failure behavior, verification, and review handoff."
---

# Write implementation-ready detailed designs

Produce a detailed design that another qualified engineer can code, integrate, test, operate, and recover without inventing critical behavior.

Read [references/methodology.md](references/methodology.md) completely before writing a full design. Read [references/evidence-catalog.md](references/evidence-catalog.md) to select risk-triggered evidence. Use [templates/detailed-design-template.md](templates/detailed-design-template.md) for a new document and [templates/traceability-matrix.md](templates/traceability-matrix.md) for coverage.

Match the user's language. Preserve identifiers, code, paths, schemas, and quoted evidence.

## Relationship to formal review

This skill authors and improves designs. It never grants implementation authorization.

After writing:

1. hand the versioned artifact to an independent `review-detailed-design` pass;
2. implement only after that review returns `PASS`;
3. treat `CONDITIONAL PASS` as not authorized until every condition is closed and rechecked;
4. revise and re-review after changes to scope, contracts, data, state, security, quality targets, migration, rollout, rollback, or recovery.

Do not silently weaken content to make review easier.

## Workflow

### 1. Establish the evidence baseline

Inspect the available requirements, current code and configuration, schemas, APIs, tests, deployment files, runbooks, prior decisions, and production evidence.

Record each material statement as:

- `CONFIRMED`: supported by a versioned source;
- `INFERRED`: derived from evidence and explicitly labeled;
- `PROPOSED`: a new design decision;
- `OPEN`: unresolved, with owner, due date, impact, and blocking status.

Never convert missing facts into confident prose. Critical OPEN items mean the document is not review-ready.

### 2. Declare scope and applicability

Define goals, non-goals, current baseline, target capability, boundaries, assumptions, constraints, dependencies, owners, version, and approval authority.

Classify `CORE` plus applicable `UI`, `API`, `EVENT`, `DATA`, `SECURITY`, and `OPS`. Every N/A requires a reason and evidence.

### 3. Create stable IDs and evidence maps

Assign stable IDs to requirements, acceptance criteria, flows, contracts, decisions, risks, quality scenarios, tests, and operational checks.

Maintain:

```text
requirement / acceptance criterion
→ design element
→ UI / API / event / data / state
→ risk and quality scenario
→ test
→ runtime evidence
```

Also map stakeholder/concern → view and decision → alternatives/rationale/tradeoff.

### 4. Write current state, target, and gaps

Describe what exists, what does not, and where the present capability boundary lies. Define the target behavior. List each gap and consequence, then map it to concrete modules, contracts, data/configuration, migration, tests, rollout, and code landing points.

Do not stop at a feature list or file list.

### 5. Close cross-layer semantics

For every critical journey, specify UI/state → API/event → domain action → data/message → runtime signal.

Define applicable schemas, errors, authorization, idempotency, ordering, timeouts, retries, cancellation, concurrency, transactions, state transitions, invariants, partial failure, compensation, recovery, and operator action.

Use OpenAPI, AsyncAPI, protobuf, JSON Schema, DDL, state machines, sequence diagrams, decision tables, or pseudocode when they express the contract more precisely than prose.

### 6. Quantify quality and verification

Turn “fast,” “available,” “secure,” “scalable,” and similar claims into scenarios with source, stimulus, artifact, environment, response, measure, and verification.

Map every requirement, invariant, failure mode, authorization rule, migration, and quality target to deterministic tests or runtime checks with inputs, environment, expected result, threshold, and owner.

### 7. Design delivery and recovery

Specify version compatibility, migration/backfill, rollout, health gates, stop conditions, observability, alerting, runbook, rollback, backup/restore, RTO/RPO, reconciliation, and support ownership as applicable.

A deployment sequence without a failure and recovery sequence is incomplete.

### 8. Run the author readiness check

Before handoff, confirm:

- the artifact and evidence are versioned and reproducible;
- all applicable template sections contain resolved decisions or justified N/A;
- no critical `TODO/TBD/TBC/OPEN` remains;
- cross-view names, boundaries, ownership, schemas, and directions agree;
- every critical requirement has design and verification targets;
- failure, concurrency, security, migration, rollout, and recovery semantics are explicit;
- two qualified engineers would not make different critical choices.

If the check fails, label the output `DRAFT — NOT READY FOR FORMAL REVIEW` and give the shortest completion list. Do not self-score or declare PASS.

### 9. Prepare review handoff

Freeze a document version and provide:

- applicability and tailoring table;
- evidence/source index;
- traceability matrix;
- open-decision and accepted-risk register;
- changed sections since the previous review;
- requested reviewers by domain;
- explicit statement: `Ready for independent review` or `Not ready`.

## Precision rules

- Prefer exact schemas, state tables, sequences, invariants, thresholds, and examples over adjectives.
- Describe normal, boundary, rejected, timeout, retry, duplicate, concurrent, partial-success, restart, and recovery behavior when applicable.
- Allow local code organization to remain an implementation choice; close all cross-module and risk-bearing semantics.
- Use diagrams only when they resolve a concern. A diagram count is never a quality metric.
- Do not duplicate production code into the design. Specify behavior, contracts, invariants, and landing points.
- Do not cite “framework defaults,” “industry standard,” or undocumented team knowledge as design evidence.
- Do not return an empty generic template when project evidence is available; fill confirmed sections and expose missing evidence precisely.

## Completion test

Ask:

> If two qualified engineers independently implement this document, could they choose different critical interfaces, data rules, states, errors, concurrency behavior, security controls, quality thresholds, migration, rollback, or acceptance criteria?

If yes, continue designing. The document is not ready for formal review.
