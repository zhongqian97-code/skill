---
name: "review-detailed-design"
description: "以全栈、数据库、图文可用性和单文档合稿硬门禁审查 AS-IS/TO-BE 设计。"
---

# Review Detailed Design

Review in one explicit mode:

1. AS-IS RECONSTRUCTION AUDIT: fidelity and equivalent reproduction.
2. TO-BE IMPLEMENTATION AUTHORIZATION: readiness to implement.

Never mix their inputs, verdicts, or authority. Read references/review-standard.md and references/usability-and-synthesis-gates.md completely. Use templates/review-report.md.

## Core principles

- Review content, findability, diagrams, cross-view consistency, and evidence.
- A design is not usable because every fact exists somewhere.
- Exact tables and contracts are mandatory; diagrams supplement them.
- A full-stack feature needs an early system summary and visual coverage for every F-ID.
- Multiple-agent work must be semantically integrated by one editor, not concatenated.
- A source defect belongs in the AS-IS defect register; a source detail missing from the design is a reconstruction omission.
- AS-IS never grants implementation authorization; only TO-BE PASS does.

## 1. Select mode and run readiness

AS-IS inputs: pinned source, feature boundary, F/BEH catalog, implementation census, evidence/conflict/unknown ledgers, claimed status.

Verdicts: COMPLETE, PARTIAL, BLOCKED. Authorization: NOT APPLICABLE.

TO-BE inputs: frozen scope/REQ/AC, owners/approvers, target design, traceability, verification, migration/release/rollback.

Verdicts: PASS, CONDITIONAL PASS, FAIL/FAIL not ready. Only PASS authorizes implementation.

Readiness must not hide visible severe findings.

## 2. Determine applicability

Mark frontend, sync, async, backend, persistence, dependencies, build/config/deploy, security/ops, migration/recovery, and visual views applicable/N/A-with-evidence/unknown.

## 3. Run implementation-completeness gates

S1 Scope/behaviors/census
S2 Frontend controls and all client states
S3 Sync/async contracts and field lineage
S4 Backend ownership and executable flows
S5 Physical schema and empty-database reconstruction
S6 State/transactions/concurrency/failure/recovery
S7 Security/tenancy/privacy/external boundaries
S8 Build/config/deploy/observability/rollback/restore
S9 Verification/traceability/evidence/closure

Immediate failure when applicable exact fields, schemas, states, failures, migration/build steps, or evidence are absent. ER diagrams and sequence diagrams do not replace normative contracts.

Precision extensions:

- every sensitive field must trace request → DTO/domain → serialization → persistence/config → logs and list/detail/export responses; record actual encryption, masking, omission, or raw exposure;
- every async contract must enumerate all JSON keys/types/required-or-omitempty/zero-value compatibility, producer, consumer, queue, timeout, retry, and counter semantics;
- database review distinguishes physical DEFAULT from migration backfill and application defaults;
- cross-store cleanup/reparse review preserves side-effect order and checks error aggregation, partial commit, retry/double-apply, accounting drift, reconciliation, and repair.

## 4. Run document-usability and visual gates

### U1 Single-document integrity

Require exactly one formal Markdown deliverable, one H1, one status/source block, one table of contents, one continuous hierarchy, and one canonical glossary.

Fail for appended standalone reports, repeated H1/introduction/conclusion, numbering restarts, duplicated normative API/table/state definitions, abrupt terminology/voice changes, or dependencies on companion files.

### U2 Dual-reader information architecture

Require explicit learner, implementer, and reviewer paths. The first 15–20% establishes scope, vocabulary, system shape, lifecycle, and feature map.

From any F-ID, API/event, backend, DB, failure, test, and evidence must be reachable within two navigational jumps.

### V1 System visual model

Require an early Mermaid system summary covering applicable actors, frontend, API, domain/backend, async, persistence/storage, external dependencies, and trust/runtime boundaries.

Require triggered component/context, state, physical ER, sequence/flow, and deployment views, or N/A with evidence.

### V2 Feature visual coverage

Every F-ID must map to at least one renderable primary Mermaid behavior diagram from trigger to observable result. Shared diagrams need explicit path coverage.

Persistence requires ER; non-trivial lifecycle requires state; cross-boundary/async behavior requires sequence; complex branching requires flow.

Any uncovered F-ID is a hard S2 finding.

### V3 Diagram quality and truth

Every diagram needs stable D-ID, purpose, text alternative or accTitle/accDescr, guided reading, canonical names, and mappings to F/BEH/API/EVT/DB/TEST/E.

Edges must represent evidenced calls/messages/data writes. Sequence and flow views must preserve evidenced side-effect order and explicitly show queue/worker concurrency or partial ordering; a diagram that serializes a race, moves a write across enqueue, bypasses API/service layers, or lets a failed branch continue into success is a hard contradiction. Sync/async direction, states, and failure branches must agree with exact contracts. Mermaid must render or be explicitly marked rendering-unverified; syntax or semantic contradictions fail.

A diagram that merely decorates prose does not satisfy coverage.

### P1 Vertical Feature Packet closure

Every F-ID closes:

```text
intent/trigger → UI/state → API/event → backend → DB/queue/external
→ response/result → failure/recovery → security/ops → test/evidence
```

N/A requires evidence.

### M1 Multi-agent editorial synthesis

When multiple agents contributed, require evidence that:

- scope, F/BEH IDs, glossary, outline, and evidence/diagram conventions were frozen;
- agents returned structured packets/domain audits, not independent final chapters;
- one integrator resolved conflicts and rewrote the document;
- duplicate facts were replaced by cross-references;
- terminology, diagram nodes, directions, and IDs were normalized.

Hard-splice evidence is a blocking documentation defect even if component facts are individually correct.

### C1 Cross-view consistency

Require bidirectional mapping:

```text
F/BEH ↔ diagram node/edge ↔ UI/API/EVT ↔ backend symbol
↔ table/column/index ↔ failure/test ↔ evidence
```

Orphan diagrams, contracts, data objects, tests, and evidence fail the relevant gate.

## 5. Run mode-specific gates

AS-IS: A1 pinning/integrity; A2 forward/backward trace; A3 source arbitration; A4 source defect versus document omission; A5 equivalent reproduction; A6 learner and implementer usability.

TO-BE: T1 REQ/AC traceability; T2 decision closure/owners; T3 deterministic verification; T4 release/migration feasibility; T5 independent implementer convergence; T6 learner and implementer usability.

For AS-IS, a documented source defect does not fail fidelity by itself. Missing source behavior in the document does.

## 6. Perform two blind-read tests

Learner blind read:

- in ten minutes, use only the first understanding layer and one feature section;
- explain system purpose/boundary and one feature's trigger, processing, persistence, result, and important failure;
- every unfamiliar canonical term must be findable.

Implementer blind task:

- select one F-ID without author guidance;
- locate its diagram, UI, exact contract, backend, DB fields/indexes, async/failure behavior, tests, and evidence in at most two jumps;
- determine whether a critical design choice remains.

Record evidence and failure points; do not merely claim the tests passed.

## 7. Findings and severity

Every finding includes ID, severity, gate, location, evidence/missing artifact, impact, minimal closure, and classification.

S0 catastrophic; S1 material fidelity/production blocker; S2 hard completeness/usability blocker; S3 important non-blocker; S4 editorial.

Treat missing summary diagram, uncovered F-ID diagram, missing vertical slice, non-reconstructable DB, hard-spliced document, diagram/contract contradiction, or failed implementer blind task as at least S2. Escalate to S1 where it hides security/data-loss/integrity behavior.

Any S0/S1/S2 blocks COMPLETE and PASS.

## 8. Verdict

AS-IS COMPLETE requires S1–S9, U1–U2, V1–V3, P1, M1 when applicable, C1, A1–A6, no material unknowns, and no S0–S2.

TO-BE PASS requires the same shared/usability gates plus T1–T6 and no S0–S2. CONDITIONAL PASS cannot contain implementation-affecting conditions and does not authorize implementation until re-review.

## 9. Correction set

Separate:

- document/reconstruction omissions;
- source defects;
- unavailable external/runtime evidence;
- visual/editorial/synthesis defects;
- optional improvements.

Do not modify the reviewed document unless separately asked.
