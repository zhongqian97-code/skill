# Risk-triggered evidence catalog

Use CORE for every detailed design. Add domains and triggered evidence based on actual risk. Never delete an applicable concern merely to shorten the document.

## CORE — always required

- stable artifact version, owner, reviewers, approval authority, status;
- goals, non-goals, current baseline, target, boundaries, assumptions, constraints, dependencies;
- stable requirement and acceptance IDs;
- context, affected components, ownership, and current-to-target gaps;
- at least one end-to-end main flow plus applicable rejection/failure/recovery;
- contracts for every changed boundary;
- core data/state, invariants, and consistency boundary;
- security minimum: identity, authorization, sensitive data, trust boundary, input/output;
- deterministic verification mapping;
- rollout, observability, rollback/recovery minimum;
- decisions, risks, open items, tailoring/N/A evidence, and review handoff.

## UI trigger

Use when pages, user interaction, or local/client state changes.

Require:

- state ownership and state transition model;
- initial/loading/empty/success/partial/stale/error/unauthorized/offline/submitting;
- disabled/duplicate action, cancellation, race, optimistic rollback;
- refresh, back/forward, deep link, multi-tab, reconnect;
- error placement, focus, keyboard, responsive behavior;
- accessibility target and testable criteria where applicable.

## API trigger

Use for synchronous API/RPC or changed consumer/provider contracts.

Require:

- executable versioned schema;
- authn, function/object/property/tenant authz;
- input/output constraints and examples;
- status/machine error codes and caller behavior;
- pagination stable order, filters/sorts, payload limits;
- safe/idempotent classification, idempotency-key lifecycle;
- timeout, retry/backoff/jitter, cancellation, rate/quota;
- compatibility, versioning, deprecation, consumer/provider contract tests.

## EVENT trigger

Use for messages, streams, background jobs, schedules, webhooks, or async workflows.

Require:

- producer, consumer, topic/job, schema/version;
- partition/order key and delivery semantics;
- dedupe and idempotent side effects;
- retry/backoff, DLQ, retention, replay;
- duplicate, delayed, out-of-order, poison, backlog;
- DB-write/publish atomicity such as outbox when needed;
- compensation, reconciliation, manual repair, monitoring.

## DATA trigger

Use for persistence, cache, indexes, files, search, migrations, or concurrent writes.

Require:

- source of truth, ownership, schema, constraints, null/unit/time/precision;
- invariants and state machine;
- transactions, isolation, locking/versioning, concurrent outcomes;
- indexes, access patterns, cardinality, growth, partition/tenant isolation;
- cache freshness, keys, invalidation, stampede, outage;
- retention, archive, deletion, export, audit;
- forward migration, compatibility, backfill, validation, rollback/recovery;
- backup/restore and irreversible-change approval.

Additional triggers:

- money/inventory/quota → atomic conditional change, exact invariant, idempotency, reconciliation;
- multiple services/data sources → Saga/outbox/compensation/pivot/retryable step;
- high volume → workload model, hot keys, query/plan evidence, capacity/load test.

## SECURITY trigger

Use for identity, permissions, secrets, PII, money, admin, public ingress, tenant boundaries, or untrusted third parties.

Require:

- data-flow/trust-boundary diagram and threat/abuse model;
- asset and sensitive-data classification;
- deny by default and least privilege;
- session/token/key lifecycle, revocation/rotation;
- tenant and object/property authorization;
- CSRF/XSS/CSP/CORS/SSRF/injection/upload/egress controls as applicable;
- encryption, secret storage, masking, safe logs, audit;
- privacy purpose, minimization, retention/deletion/export/residency/consent;
- negative security tests and detection/response;
- exceptions with authority, compensating control, expiry.

## OPS trigger

Use for production delivery, external dependencies, availability, capacity, recovery, or zero downtime.

Require:

- versioned artifact, config/secret changes, release sequence;
- rolling/blue-green/canary, flags, health gates, stop/rollback triggers;
- readiness/liveness/startup semantics;
- compatibility across app/schema/event/cache during rollout and rollback;
- SLI/SLO, error budget, latency/traffic/errors/saturation;
- correlation IDs, dashboard, actionable alerts, runbook, owner;
- capacity, peak/growth/burst, quota, backpressure, load shedding, degradation;
- external dependency quota/outage/fallback;
- RTO/RPO, backups, restore order, traffic switch, recovery exercise.

Additional triggers:

- 24×7 or business critical → formal SLO, error budget policy, RTO/RPO, exercise;
- zero downtime → compatibility window and progressive delivery;
- burst/high load → load model, headroom, overload isolation, autoscaling delay.

## Non-trivial algorithm trigger

Require:

- inputs, outputs, data structures, preconditions, postconditions, invariants;
- precise pseudocode, rule table, or mathematical definition;
- complexity and resource budget;
- boundary/degenerate cases, numerical precision, determinism;
- test oracle and property/invariant tests.

## Valid tailoring

A valid N/A says:

1. why the risk does not exist in this change;
2. which versioned evidence supports that conclusion;
3. who confirms the tailoring;
4. what change would invalidate the N/A.

Invalid tailoring examples:

- “handled by framework” without exact behavior/evidence;
- “existing behavior” without version/link and unchanged-boundary proof;
- “not needed for MVP” when correctness or safety still depends on it;
- blank sections or deleted headings.
