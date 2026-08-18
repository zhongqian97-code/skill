# Detailed design review standard

## 1. Entry minimum

Every review requires a stable artifact and the CORE evidence. Additional evidence is triggered by applicability and risk. Do not require arbitrary document length or a specific notation.

The non-negotiable minimum is:

- scope, goals, non-goals, baseline, owner, version, assumptions, constraints, and open decisions;
- requirements or acceptance criteria with stable identifiers;
- system context, boundaries, dependencies, and affected components;
- interface, core data, behavior, failure, security-minimum, verification, rollout, rollback, and observability evidence;
- an explicit tailoring table for omitted areas.

A referenced shared baseline is acceptable only when its version, link, applicability, and deviations are recorded.

## 2. Hard gates

### G1 — Scope and baseline

Require:

- current capability and target capability;
- exact in-scope and out-of-scope behavior;
- stakeholders, owners, reviewers, version, and lifecycle state;
- assumptions, business and technical constraints, dependencies, and compatibility boundaries;
- open decisions listed separately with owner and due date.

Fail when scope depends on an unconfirmed critical assumption or the review object cannot be reproduced.

### G2 — Bidirectional traceability

Require reversible navigation across:

```text
requirement / acceptance criterion
→ design element
→ UI / API / event / data / state
→ risk and quality attribute
→ test
→ runtime evidence
```

Fail for an orphan critical requirement, a critical design element with no source, or a critical requirement with no verification target.

### G3 — Executable interaction contracts

For every affected UI, API, event, job, webhook, and external dependency, require applicable details:

- direction, protocol, method/path/topic, ownership, producer, and consumer;
- request/response/event schema, types, required/null/default rules, ranges, units, time zones, precision, and examples;
- authentication, function/object/property/tenant authorization, and visibility;
- status codes, machine-readable error codes, failure semantics, and caller behavior;
- safe/idempotent/non-idempotent classification, idempotency key semantics, deduplication, ordering, timeout, retry, backoff/jitter, cancellation, and rate limits;
- pagination stable order, filtering/sorting allowlists, maximum payload, versioning, compatibility, and deprecation;
- OpenAPI, AsyncAPI, protobuf, JSON Schema, or an equivalent versioned contract when practical;
- UI initial/loading/empty/success/partial/stale/error/unauthorized/offline/submitting/duplicate-submit states, refresh/back/deep-link behavior, races, cancellation, optimistic rollback, keyboard/focus, and accessibility when applicable.

Fail when implementers must choose a critical field, state, error, retry, duplicate, ordering, or compatibility behavior.

### G4 — Data, state, consistency, and migration

Require:

- entities, fields, ownership, keys, relations, constraints, null semantics, units, sensitivity, retention, archive, deletion, and audit requirements;
- access patterns, index rationale, cardinality, growth, hot keys, partitioning, and tenant isolation;
- explicit state machines with legal/illegal transitions, preconditions, postconditions, and invariants;
- atomic boundaries, isolation level, locks or conditional updates, optimistic versions, deadlock/serialization retry, and final concurrent outcomes;
- cache source of truth, key/tenant dimension, TTL or freshness bound, read/write/invalidation ordering, stampede/penetration strategy, stale/miss/outage behavior, capacity, and eviction;
- forward migration, compatibility window, backfill, validation, lock/performance impact, recovery, and the effect of rolling back code after schema change;
- expand–migrate–contract or an equivalent safe process for breaking changes;
- backup, restore evidence, and explicit approval for irreversible changes.

Fail when a data change lacks a safe migration and recovery path or when a critical invariant is not protected.

### G5 — Critical flows and recovery

For each critical journey, require:

- happy path;
- expected business rejection;
- dependency timeout or outage;
- partial success;
- duplicate, delayed, out-of-order, and concurrent execution;
- process restart or task resume;
- retry exhaustion, compensation, reconciliation, manual repair, and final state;
- observable signals and operator action.

For cross-service writes, require the selected consistency model, Saga/outbox or equivalent, compensable/pivot/retryable steps, replay and deduplication. Treat “exactly once” as unproven unless the end-to-end guarantee is demonstrated.

For messages, require schema/version, partition/order key, delivery semantics, retry, DLQ, retention, replay isolation, poison handling, backlog alerting, and idempotent side effects.

Fail a happy-path-only design.

### G6 — Measurable quality attributes

For each important quality attribute, require a scenario:

```text
source + stimulus + affected artifact + environment + response + response measure
```

Cover applicable performance, reliability, availability, security, compatibility, usability/accessibility, maintainability, portability/flexibility, and safety concerns.

Require numeric workload, latency percentile, throughput, error, saturation, availability, capacity margin, RTO/RPO, or equivalent thresholds and a verification method. Record sensitivity and tradeoff points.

Fail qualitative claims such as “high performance,” “high availability,” “scalable,” or “secure” without measurable scenarios.

### G7 — Security, privacy, and compliance

Require:

- assets, data classification, trust boundaries, attackers, entry points, third parties, threats or abuse cases, mitigations, and negative verification;
- deny by default, least privilege, and per-request function/object/property/tenant authorization;
- session/token issue, storage, TTL, refresh, revocation, rotation, logout, multi-device behavior, reauthentication, and MFA triggers where applicable;
- input validation, output encoding, CSRF, XSS/CSP, CORS allowlist, SSRF/egress, injection, upload, secrets, encryption, masking, logging, auditing, enumeration, brute force, and rate controls as applicable;
- privacy purpose, minimization, retention, deletion, export, residency, and consent obligations;
- security requirement → control → test traceability;
- exception owner, approver, rationale, compensating control, expiry, and re-review.

Public systems, PII, money, administration, and multi-tenant systems require an explicit threat model. Fail applicable designs without it.

### G8 — Verification and acceptance

Require:

- every requirement, invariant, failure mode, authorization rule, migration, and quality target mapped to a test or runtime check;
- unit, integration/contract, and a small set of critical end-to-end tests chosen by risk;
- concurrent, duplicate/out-of-order, timeout/retry, failure-injection, migration compatibility, rollback, restore, load/capacity, and security-negative tests when triggered;
- test inputs, environment, dependency strategy, expected result or oracle, measurable threshold, data handling, repeatability, and failure disposition;
- post-release validation through metrics, logs, traces, alerts, and business reconciliation;
- owner for non-automated verification.

Fail “test after implementation” or test names without deterministic expected results.

### G9 — Decisions, operations, and delivery

Require:

- key decisions, alternatives, rationale, costs, and positive/negative quality impacts;
- known risks with trigger, impact, likelihood, mitigation, owner, due date, and approver;
- immutable artifact/version linkage, configuration and secret changes, rollout strategy, health gates, stop conditions, and automatic/manual rollback triggers;
- correct readiness/liveness/startup semantics where applicable;
- rollback compatibility across application, schema, message schema, cache, and feature flags;
- feature flag owner, default, permission, audit, expiry, and removal plan;
- SLI/SLO, measurement point, window, error budget, owner, and budget-exhaustion action for critical journeys;
- latency including p95/p99, traffic, explicit and implicit errors, saturation, correlation/request/idempotency/saga identifiers, and secret-safe telemetry;
- capacity assumptions, peak/growth/burst model, bottlenecks, quotas, backpressure, load shedding, degradation, and autoscaling delay;
- actionable alerts tied to user symptoms, thresholds, runbook, and owner;
- RTO/RPO, backup scope/frequency/encryption/retention/fault domain, restore order, traffic switch, and recent exercise evidence when disaster recovery is applicable;
- synchronization rules between the design and code, schemas, generated specifications, tests, and runbooks.

Fail when the design is not observable, cannot be safely rolled back/recovered, or hides a critical tradeoff.

## 3. Risk-triggered checks

Always apply CORE. Activate additional checks when these triggers exist:

- write or billable side effect → concurrency, idempotency, retry, duplicate-submit;
- multiple data sources or cross-service writes → Saga/outbox, compensation, reconciliation;
- cache → freshness, invalidation, stampede, sensitive isolation;
- message/event/job/webhook → delivery, ordering, dedupe, DLQ, replay;
- schema/data change → compatibility, backfill, validation, rollback;
- public network, PII, money, admin, or multi-tenant → threat model, strong authorization, audit, security-negative testing;
- 24×7 or business critical → formal SLO, error budget, capacity, RTO/RPO, recovery exercise;
- high or bursty load → quota, backpressure, load shedding, load testing;
- SSR, offline, multiple tabs, or optimistic UI → hydration, synchronization, race, conflict recovery;
- zero downtime → rolling/blue-green/canary, readiness, compatibility window;
- non-trivial algorithm → pseudocode, rule/decision table, complexity, preconditions, postconditions, invariants;
- accessibility requirement → target WCAG level and testable success criteria.

For N/A, require: “why the risk does not exist,” referenced evidence, and reviewer confirmation.

## 4. Scoring

Score only after all applicable hard gates pass.

| Dimension | Weight |
| --- | ---: |
| Scope, requirements, and traceability | 14 |
| Functional flows, UI behavior, and state coverage | 12 |
| Architecture, dependencies, and decision rationale | 12 |
| UI/API/event/external contracts | 14 |
| Data, state, consistency, and concurrency | 14 |
| Quality attributes and capacity | 12 |
| Failure recovery, operations, and delivery | 10 |
| Security, privacy, and compliance | 7 |
| Verification and acceptance evidence | 5 |
| Total | 100 |

Calculate each weighted contribution as `rating / 4 × weight`.

Anchors:

- `0 — Missing`: no evidence or an undeclared omission.
- `1 — Intent`: goals, principles, names, or TODOs only; not implementable.
- `2 — Partial design`: a direction exists, but implementers must make critical choices or verification is incomplete.
- `3 — Implementation ready`: normal, exceptional, boundary, and contract behavior is clear; only local coding choices remain; verification is defined.
- `4 — Evidence complete`: level 3 plus bidirectional traceability, quantitative rationale, tradeoff analysis, and prototype/test/migration/failure evidence as appropriate.

Every rating must cite evidence. Repeated prose does not increase a rating.

## 5. Finding severity

- `S0 — Blocker`: artifact/version/scope unavailable; critical inputs inaccessible or contradictory; readiness gate fails; many critical TBD/TBC/TODO items. Stop and return FAIL.
- `S1 — Critical`: plausible authorization bypass, sensitive-data disclosure, money/data corruption, unrecoverable outage, legal/contract breach, unsafe migration/rollback, or critical invariant violation. FAIL.
- `S2 — Major`: implementers must decide critical contracts, state, transactions, consistency, idempotency, concurrency, quality thresholds, recovery, security, or acceptance; or a likely cross-team conflict/rework remains. FAIL.
- `S3 — Minor`: localized ambiguity or missing auxiliary evidence that does not alter critical behavior. May be a condition.
- `S4 — Suggestion`: optional readability, maintainability, or future optimization. Does not affect the verdict.

Severity is impact. Priority is schedule. Do not conflate them.

## 6. Verdict

### PASS

Require all:

- every applicable hard gate passes;
- score is at least 85;
- every applicable dimension rates at least 3;
- no open S0, S1, or S2;
- S3 items are closed or explicitly accepted without changing implementation, test, or rollout;
- evidence, reviewers, and approval authority are recorded.

Authorize implementation.

### CONDITIONAL PASS

Require all:

- every applicable hard gate passes;
- score is 75–84;
- every applicable dimension rates at least 3;
- no open S0, S1, or S2;
- only a limited set of S3 items remains;
- each condition has an owner, due date, exact document change, and mechanical recheck.

Do not authorize implementation until all conditions are closed and rechecked, converting the verdict to PASS.

### FAIL

Return FAIL if any applies:

- an applicable hard gate fails;
- an open S0, S1, or S2 exists;
- score is below 75;
- an applicable dimension rates below 3;
- critical evidence contradicts;
- the reviewer must guess author intent;
- a condition lacks owner, due date, or verification.

## 7. Anti-gaming rules

- Gates precede scoring.
- Every score and gate cites evidence.
- Each dimension has its own minimum.
- Every N/A requires rationale and approval.
- More prose, diagrams, or duplicated content do not earn points.
- Evidence may be linked OpenAPI, DDL, schemas, state machines, tests, or runbooks only when versioned and accessible.
- The reviewer must not supply missing core design and then approve it.
- Accepted risk requires an authorized approver and expiry.
- Changes to interface, data, state, security, quality target, migration, rollout, rollback, or recovery invalidate the prior PASS.
- Automated checks cannot replace independent tradeoff and risk judgment.
