# Detailed design authoring methodology

## Purpose

A detailed design is an executable agreement among product, engineering, security, data, QA, and operations. Its goal is not length. Its goal is to close critical decisions and make them traceable and verifiable.

The required depth is: low-level units, interfaces, data, behavior, resources, failure handling, and verification must be specific enough to code, integrate, and test.

## 1. Input and evidence inventory

Start with a source index:

- product requirements and acceptance criteria;
- existing architecture and design decisions;
- current code, configuration, database schemas, API/event specifications, and feature flags;
- current tests and coverage;
- deployment topology, infrastructure, telemetry, alerts, runbooks, incident history, and SLOs;
- legal, privacy, security, accessibility, and compatibility constraints.

For every source, record version/commit, owner, date, link/path, and applicability.

Label statements CONFIRMED, INFERRED, PROPOSED, or OPEN. An inference must cite its inputs. A proposal must record alternatives and consequences. An open item must have an owner, due date, impact, and whether it blocks review.

## 2. Scope, baseline, and target

Write:

- problem and business outcome;
- current supported and unsupported capability;
- system-of-interest and boundary;
- exact in-scope and out-of-scope behavior;
- target capability and measurable acceptance criteria;
- stakeholders and concerns;
- assumptions, constraints, dependencies, compatibility obligations, and approval authority.

Avoid scope verbs without objects. “Support Docker” is ambiguous; name which services, environments, persistent data, networking, secrets, build, release, and operations are included.

## 3. Stable identifiers and traceability

Use stable prefixes, for example:

- `REQ-`: requirement;
- `AC-`: acceptance criterion;
- `FLOW-`: journey or failure flow;
- `UI-`, `API-`, `EVT-`, `DATA-`: contracts;
- `INV-`: invariant;
- `QA-`: quality-attribute scenario;
- `DEC-`: decision;
- `RISK-`: risk;
- `TEST-`: verification;
- `OPS-`: runtime check or procedure.

Build the traceability matrix before deep prose. Missing destinations expose design work early.

Require forward and reverse navigation. A feature without a source is scope creep; a requirement without a design/test destination is incomplete.

## 4. Views selected by concern

Select views because a stakeholder concern requires them:

- context view: actors, external systems, trust and ownership boundaries;
- static decomposition: modules, responsibilities, dependencies, allowed directions;
- runtime interaction: critical sequences, async boundaries, timeouts, and failure propagation;
- deployment view: processes, nodes, networks, fault domains, secrets, and scaling;
- information view: data ownership, schemas, lifecycle, movement, and sensitivity;
- state view: legal/illegal transitions, guards, terminal states, and recovery;
- resource view: CPU, memory, storage, connections, queues, bandwidth, quotas;
- security/threat view: assets, attackers, entry points, abuse paths, and controls.

Keep names, boundaries, ownership, and directions consistent across all views. Record correspondence rules where representations differ.

## 5. Current-to-target gap closure

For every gap, write:

- current evidence;
- target requirement and acceptance IDs;
- consequence if unresolved;
- affected modules and code landing points;
- UI/API/event/data/state changes;
- dependency, configuration, infrastructure, and operational changes;
- migration and compatibility;
- verification and runtime evidence;
- decision, risk, owner, and sequence.

This preserves the original strength of current-state/target/gap analysis while extending it into an implementation contract.

## 6. Behavior and cross-layer flows

For each critical journey, describe:

1. trigger, actor, preconditions, and authorization;
2. UI or caller state;
3. API/event interaction;
4. domain decisions and invariants;
5. data reads/writes and transaction boundary;
6. messages, caches, and external dependencies;
7. response and final state;
8. logs, metrics, traces, audit, and reconciliation.

Add variations as applicable:

- business rejection and validation failure;
- unauthorized/forbidden;
- empty, partial, stale, offline, or degraded result;
- timeout, dependency outage, and retry exhaustion;
- duplicate, delayed, out-of-order, and concurrent execution;
- cancellation, client disconnect, process restart, and task resume;
- partial commit, compensation, manual repair, and final consistency.

State the final user-visible, data, and operational outcome for every branch.

## 7. Contract writing

### UI

Define state source of truth and initial/loading/empty/success/partial/stale/error/unauthorized/offline/submitting states. Specify duplicate-submit, cancellation, navigation, refresh, deep-link, multi-tab, race, optimistic rollback, keyboard/focus, responsiveness, and accessibility where applicable.

### API/RPC

Define method/path, ownership, authentication/authorization, request/response schemas, types, required/null/default rules, range/unit/time zone/precision, status and machine error codes, paging/order/filtering, payload limits, safe/idempotent semantics, idempotency-key behavior, timeout/retry/backoff, cancellation, rate limits, versioning, compatibility, and deprecation.

### Event/job/webhook

Define producer/consumer, topic, schema/version, partition/order key, delivery semantics, dedupe, idempotent side effects, retry/backoff, DLQ, retention, replay, late/out-of-order behavior, poison handling, backlog alert, and recovery.

### External dependency

Define trust, authentication, quota, timeout, retry, circuit/degradation policy, data exposure, contract version, sandbox/test strategy, outage behavior, and ownership.

## 8. Data, state, and consistency

Define:

- entities, fields, keys, relations, constraints, null semantics, units, time zones, precision, and sensitive classification;
- source of truth, ownership, retention, archival, deletion, export, audit, and legal holds;
- access patterns, indexes, cardinality, growth, hot keys, partitioning, and tenant isolation;
- invariants and legal/illegal state transitions;
- atomic boundary, isolation, lock/order, conditional update, optimistic version, deadlock/serialization retry;
- concurrent outcomes for duplicate or competing writes;
- cache keys, TTL/freshness, invalidation order, stampede controls, stale/miss/outage behavior;
- migration, expand–migrate–contract, backfill, validation, compatibility window, performance/lock impact, code rollback after schema change, backup, restore, and irreversible-change approval.

Never write only “use a transaction,” “use Redis,” or “add an index.” Explain the correctness contract and evidence.

## 9. Security, privacy, and compliance

Identify assets, data classification, trust boundaries, attackers, entry points, third parties, threats/abuse cases, controls, and negative tests.

Define deny-by-default authorization across function, object, property, and tenant; session/token lifecycle; reauthentication/MFA triggers; input/output controls; CSRF, XSS/CSP, CORS, SSRF/egress, injection, upload, secrets, encryption, masking, logs, audit, enumeration, brute force, and rate controls as applicable.

Map security requirement → control → test/runtime evidence. Record exception approver, compensating control, expiry, and re-review date.

## 10. Quality attributes and capacity

Write priority scenarios as:

```text
source + stimulus + artifact + environment + response + response measure
```

Use system-specific numbers for workload, latency percentiles, throughput, error rate, saturation, availability, capacity margin, scale delay, RTO/RPO, accessibility, compatibility, or maintainability.

Record alternatives, sensitivity points, tradeoff points, measurement location, test method, and owner. A category name from a quality model is not a threshold.

## 11. Verification design

For every requirement, invariant, failure, authorization rule, migration, and quality target, specify:

- test level and ID;
- setup, input, environment, dependency behavior, and test data;
- action/stimulus;
- expected result/oracle and numeric threshold;
- cleanup and repeatability;
- owner and failure disposition;
- post-release runtime evidence.

Choose unit, integration/contract, and critical E2E tests by risk. Add concurrency, duplicate/out-of-order, timeout/retry, failure-injection, migration compatibility, rollback, restore, load, and security-negative tests when triggered.

## 12. Delivery, operations, and recovery

Define:

- immutable artifact and version linkage;
- configuration and secret migration;
- rolling, blue/green, canary, or other rollout sequence;
- feature flag owner/default/access/audit/expiry/removal;
- readiness, liveness, startup, health gates, stop conditions, and rollback triggers;
- application/schema/event/cache compatibility during forward and rollback paths;
- SLI/SLO, window, error budget, telemetry fields, correlation IDs, dashboard, alert, runbook, and owner;
- peak/growth/burst assumptions, quotas, backpressure, load shedding, degradation, and autoscaling delay;
- RTO/RPO, backup scope/frequency/encryption/retention/fault domains, restore order, traffic switch, dependency recovery, and exercise evidence;
- reconciliation and manual repair.

## 13. Decision and risk closure

For every key decision, record alternatives, rationale, rejected options, cost, positive/negative quality impact, approver, and invalidation trigger.

For every risk, record trigger, impact, likelihood, mitigation, detection, contingency, owner, due date, residual risk, and approver.

Critical open decisions about interfaces, data, state, consistency, security, quality thresholds, migration, rollback, or acceptance block formal review readiness.

## 14. Author readiness and handoff

Run consistency checks across views and evidence maps. Search for TODO/TBD/TBC, ambiguous adjectives, unowned risks, missing IDs, and inaccessible references.

Apply the two-engineer counterfactual. If critical choices can diverge, continue designing.

Freeze the artifact version. Attach the applicability table, source index, traceability matrix, decision/risk register, changed-section list, and requested reviewers. The independent reviewer—not the authoring skill—decides PASS.
