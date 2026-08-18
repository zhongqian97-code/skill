---
name: "detailed-design-writing"
description: "编写一份图文统一、双读者可用且可直接实施的全栈详细设计。"
---

# Write Implementation-Ready Detailed Designs

Produce one coherent detailed design that a learner can understand and a qualified engineer can implement, integrate, test, operate, and recover without inventing critical behavior.

Read references/methodology.md, references/evidence-catalog.md, and references/visual-and-editorial-standard.md before a full design. Use templates/detailed-design-template.md.

This skill authors designs but never grants implementation authorization. Independent review-detailed-design must return PASS before TO-BE implementation.

## Output and reader contract

The formal deliverable is exactly one Markdown document unless the user explicitly requests another packaging format.

Require:

- one H1, one status/version block, one table of contents, one continuous hierarchy;
- a five-minute understanding layer, feature implementation packets, and a normative reference layer;
- learner, implementer, and reviewer reading paths;
- one canonical glossary and identifier system;
- one fact in one canonical home, with cross-references elsewhere;
- no concatenated subdocuments, duplicate introductions/conclusions, restarted numbering, or companion-file dependencies.

A long document is not complete merely because facts exist somewhere. Important information must be findable and related.

## Stable identifiers

Use REQ/AC/FLOW plus F-### for user-observable features. Use D-F###-* for diagrams and UI/API/EVT/DATA/INV/QA/DEC/RISK/TEST/OPS for contracts and checks.

## Workflow

### 1. Establish baseline, scope, readers, and applicability

Inventory requirements, current code/config/schema/contracts/tests/deployment/runbooks and label claims CONFIRMED, INFERRED, PROPOSED, or OPEN.

Define current state, target, gap, owners, constraints, dependencies, non-goals, and CORE/UI/API/EVENT/DATA/SECURITY/OPS applicability. Critical OPEN items mean Not Ready. A subsystem may be out of scope internally, but its exact boundary contract remains in scope whenever the designed feature depends on its payload, state, counter, persistence, security, completion, failure, or recovery behavior.

### 2. Freeze information architecture before parallel work

Freeze:

- dual-reader paths and document outline;
- F-ID/REQ/AC catalog;
- canonical glossary and naming;
- diagram legend and D-ID convention;
- traceability/evidence format;
- canonical home for API, event, DB, state, and decision definitions.

When parallel agents are authorized for a large design, they return structured FeaturePackets or domain audits. They do not write final standalone chapters. One primary editor synthesizes the final document and owns terminology, ordering, deduplication, and cross-view consistency.

### 3. Build a five-minute mental model

Within the first 15% include:

- problem, outcome, scope, non-scope;
- canonical glossary;
- one system summary Mermaid diagram;
- feature map F-ID → primary diagram → UI/API/event/data/test;
- core lifecycle and major boundaries.

### 4. Design by vertical feature packets

Each F-ID contains:

1. purpose, actor, trigger, preconditions, permissions, measurable result;
2. at least one primary Mermaid diagram from trigger to result;
3. guided diagram reading and text alternative;
4. frontend controls, validation, and all client states;
5. exact sync/async contracts and field mappings; async schemas enumerate every wire key/type/required-or-omitempty/zero-value rule plus producer, consumer, queue, retry and timeout;
6. backend orchestration, modules, transactions, and side effects;
7. physical data reads/writes, fields, indexes, invariants, and migrations; distinguish physical DEFAULT, migration backfill, and application default;
8. state, concurrency, idempotency, timeout, retry, cancellation, failure, compensation, restart, and recovery, including cross-store partial commits, repeated cleanup/double-apply, quota/accounting drift, reconciliation, and exact side-effect order;
9. security, observability, quality targets; every sensitive field traces request → serialization/domain → persistence/config → response/log/export, with encryption/masking/raw exposure stated explicitly;
10. deterministic verification and acceptance mapping.

Use shared normative references instead of duplicating schemas.

### 5. Apply visual closure

Mandatory:

- one early system summary diagram;
- one primary Mermaid behavior diagram for every F-ID;
- ER when persistence applies;
- state diagram for non-trivial lifecycles;
- sequence diagram across client/API/async/external boundaries;
- flowchart for complex branching;
- deployment view when topology affects behavior.

Each diagram has a stable D-ID, purpose, text alternative/accTitle/accDescr, “read 1→N” guide, canonical names, and mappings to requirements/contracts/data/tests. Sequence diagrams preserve actual side-effect order and mark queue/worker concurrency or partial ordering explicitly; they may not serialize a race or reorder a source write for readability. Diagrams never replace exact schemas, DDL, error tables, state tables, or pseudocode.

Prefer focused diagrams: approximately 12 top-level nodes for summaries, 8 participants/20 messages for sequences, 15 nodes for flowcharts, and 10 entities for focused ER views unless the document explains a different budget. Render Mermaid blocks or mark rendering unverified.

### 6. Close exact contracts, data, failures, and operations

Specify UI state; API/event schemas; backend ownership; data columns/constraints/indexes; transactions/concurrency; security/privacy; quality thresholds; build/config/deploy; migration/backfill; observability; rollback/backup/restore; and tests.

For every critical journey trace:

```text
UI/state → API/event → domain → repository/external → data/message
→ response/state → user and operator result
```

### 7. Integrate rather than concatenate

After research:

1. resolve terminology and conflicts;
2. synthesize the outline around F-IDs and reader journeys;
3. define each shared contract once;
4. rewrite every accepted packet into the same voice and section rhythm;
5. remove repeated facts and replace them with links;
6. unify diagram participants and directions;
7. verify every cross-reference and identifier;
8. run Mermaid and document-structure checks.

Hard-splice signals are blocking defects: multiple H1s/status blocks/TOCs, duplicated normative definitions, repeated conclusion sections, numbering restarts, embedded standalone reports, and abrupt voice or terminology changes.

### 8. Run author readiness

Learner blind read: can a reader explain the summary and one full feature path in ten minutes?

Implementer blind task: can an engineer choose any F-ID and find its diagram, contracts, backend, data, failures, tests, and evidence within two jumps, then implement without a new critical design decision?

Also verify no critical OPEN/TODO/TBD, all diagrams render, exact tables agree with ER/state/sequence views, and requirement→design→test→runtime traceability closes.

If any hard gate fails, mark DRAFT — NOT READY FOR FORMAL REVIEW. Do not self-score or declare PASS.

## Required information architecture

1. Identity/status/readers/how to read
2. Executive summary, scope, glossary, summary diagram, feature map
3. Context/components/deployment/core lifecycle
4. F-ID feature implementation packets
5. Shared API/event contracts
6. Backend/runtime cross-cutting mechanisms
7. Physical database/data/migration reference
8. Security/quality/operations/recovery
9. Verification/traceability/review handoff
10. Decisions/risks/open items/evidence

## Precision rules

- diagrams answer structure, sequence, state, relationship, or deployment questions;
- every F-ID needs visual coverage, but methods and headings do not receive decorative diagrams;
- exact schemas, states, errors, thresholds, invariants, and examples outrank adjectives;
- never cite framework defaults or undocumented team knowledge as evidence;
- keep AS-IS, PROPOSED, and UNKNOWN visually and textually distinct.
