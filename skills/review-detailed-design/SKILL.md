---
name: "review-detailed-design"
description: "Review detailed designs with hard gates, evidence scoring, severity, and implementation authorization."
---

# Review detailed designs

Review a detailed design independently before implementation. Approve only when another qualified engineer can implement and verify the design without inventing critical behavior.

Read [references/review-standard.md](references/review-standard.md) completely for every formal review. Read [references/sources.md](references/sources.md) when the user asks for rationale, standards, or source verification. Use [templates/review-report.md](templates/review-report.md) as the required report structure.

Match the user's language. Preserve identifiers, code, paths, schema names, and quoted evidence.

## Authority rule

Treat the verdict as an implementation gate:

- `PASS`: authorize implementation.
- `CONDITIONAL PASS`: do not authorize implementation yet. Close every condition and perform the stated recheck before converting to `PASS`.
- `FAIL`: return the design for revision and re-review.

Never let a score offset a failed hard gate or an open S0, S1, or S2 finding.

## Review workflow

### 1. Establish the review baseline

Record:

- document name, stable version, commit, or timestamp;
- system or feature and change scope;
- author, owners, reviewers, and intended approval authority;
- referenced requirements, specifications, diagrams, schemas, and code baseline;
- assumptions, constraints, dependencies, out-of-scope items, and open decisions.

If the review object or version cannot be reproduced, report an S0 and `FAIL`.

### 2. Declare applicability

Classify the design using:

- `CORE`: always applicable;
- `UI`: pages or user interaction;
- `API`: synchronous APIs or RPC;
- `EVENT`: messages, jobs, webhooks, or asynchronous workflows;
- `DATA`: persistent data, caches, indexes, files, or migrations;
- `SECURITY`: identity, permissions, sensitive data, money, tenants, or trust boundaries;
- `OPS`: release, capacity, availability, recovery, or external dependencies.

For every excluded area, require a specific `N/A` rationale and evidence. Treat an invalid `N/A` as a hard-gate failure.

### 3. Run the readiness gate

Before scoring, verify that the document contains:

1. scope, goals, non-goals, baseline, assumptions, constraints, and owners;
2. stable requirement or acceptance IDs and their design targets;
3. at least one end-to-end main flow plus relevant failure, timeout, retry, cancellation, concurrency, and recovery flows;
4. cross-layer contracts from UI/state through API/event, domain operation, data/message, and runtime signal;
5. data ownership, trust boundaries, transaction/consistency boundaries, and critical invariants;
6. measurable acceptance criteria, test mapping, rollout, observability, rollback, and recovery.

If any applicable item is absent or a critical item remains `TBD/TBC/TODO`, stop the formal review. Produce `FAIL (not ready)`, list the shortest concrete completion set, and do not invent missing design.

Early advisory feedback is allowed, but it cannot produce `PASS` or implementation authorization.

When readiness fails, use an abbreviated report: metadata, executive conclusion, applicability, readiness result, directly supported findings, and re-review scope. In the hard-gate table, record gates directly proven to fail and mark every unexamined applicable gate `NOT EVALUATED — readiness stop`. Do not misuse `N/A` and do not score.

### 4. Build evidence maps

Create these maps before judging quality:

- stakeholder/concern → section, view, or artifact;
- requirement/acceptance criterion → design element → contract/data/state → test → runtime evidence;
- decision → alternatives → rationale → quality/risk impact;
- critical flow → failure modes → recovery → operator action.

Flag orphan requirements, unmotivated design elements, missing verification targets, and cross-view contradictions.

### 5. Evaluate all applicable hard gates

After readiness passes, evaluate G1–G9 from the review standard. Each formal gate result is only:

- `PASS`;
- `FAIL`;
- `N/A — <rationale and evidence>`.

Every result must cite a document section, diagram, table, schema, specification, or other versioned artifact. A heading without resolved design content is not evidence.

### 6. Apply the two-engineer counterfactual

Ask:

> If two qualified engineers independently implemented this document, could they make different critical choices about interfaces, data, state transitions, errors, concurrency, security, quality thresholds, migration, rollback, or acceptance?

If yes, rate the affected dimension at most 2/4, create at least one S2 finding, and return `FAIL`.

Local code organization may remain an implementation choice. Cross-module semantics and risk-bearing behavior may not.

### 7. Score only after all gates pass

Use the weights and 0–4 anchors in the review standard. Cite evidence for every rating.

Do not score a document with a failed gate as if it were eligible for approval. You may include diagnostic ratings, clearly marked non-authoritative, only when they help the author revise.

### 8. Classify findings and determine the verdict

Classify every finding S0–S4 by impact, not scheduling priority. Apply the verdict rules exactly.

Do not downgrade severity because a team does not plan to fix an issue soon. Do not accept high or critical risk without the required authority, owner, expiry, mitigation, and verification.

### 9. Produce the report

Use the report template. At minimum include:

- final verdict and explicit implementation authorization;
- artifact and version reviewed;
- applicability profile and N/A rationales;
- hard-gate table with evidence;
- traceability and quality-attribute evidence;
- score, only when eligible;
- findings with severity, impact, exact remediation, owner, due date, and verification;
- accepted risks, conditions, and re-review scope.

A finding must say what evidence is missing or contradictory and the exact design change required. Do not rewrite the design inside the review and then approve your own addition.

## Re-review rules

Invalidate the prior `PASS` when changes affect:

- scope or acceptance criteria;
- API, event, data, or state contracts;
- transaction, concurrency, retry, or failure semantics;
- security or trust boundaries;
- quality targets, capacity assumptions, migration, rollout, rollback, or recovery.

Use a delta review only when unchanged evidence is versioned and still valid. Otherwise perform a full review.

## Prohibited shortcuts

Never approve based on:

- page count, word count, number of diagrams, UML usage, or apparent polish;
- “the framework handles it,” “industry standard,” or undocumented team knowledge;
- happy-path-only narratives;
- totals or averages that hide a weak dimension;
- reviewer-supplied core design decisions;
- inaccessible, unversioned, or stale evidence;
- a list of tests without inputs, expected results, thresholds, or traceability.

The decisive test is evidence closure: the design must be specific enough to code, integrate, test, operate, recover, and review without moving critical design decisions into implementation.
