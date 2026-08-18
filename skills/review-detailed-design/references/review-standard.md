# Detailed Design Review Standard

## 1. Mode discipline

| Mode | Question | Inputs | Verdict | Can authorize implementation? |
|---|---|---|---|---|
| AS-IS reconstruction audit | Does the document faithfully and completely represent the pinned implementation so it can be equivalently reproduced? | BEH, INV, source evidence, schema/migrations, conflict/unknown ledgers | COMPLETE / PARTIAL / BLOCKED | No |
| TO-BE implementation authorization | Is the proposed target design sufficiently decided, testable, safe, and operable to begin implementation? | REQ/AC, target design, traceability, owners, tests, rollout | PASS / CONDITIONAL PASS / FAIL | PASS only |

Do not fail AS-IS merely for lacking target owners, acceptance approval, or rollout decisions. Do not pass TO-BE because it accurately describes current code.

## 2. Shared hard gates

### S1 Scope, behavior, and implementation census

Pass requires:

- stable scope and observable behavior IDs;
- actor/trigger/success/failure/concurrency variants;
- inventory of frontend, contract, backend, persistence, async, build/config/deploy, and test artifacts;
- every material item included, excluded-with-evidence, generated, third-party, or unknown;
- no unexplained material unknown.

### S2 Frontend states and client design

When applicable, pass requires:

- routes/pages/components and ownership;
- controls/fields/defaults/validation/visibility/enablement/actions;
- local/server/cache state and transitions;
- loading/empty/partial/stale/error/unauthorized/retry/refresh/navigation states;
- request/response mapping;
- permissions, flags, responsive/accessibility/localization/telemetry where material;
- frontend verification.

A component list or screenshot is insufficient.

### S3 Interaction contracts and field lineage

Pass requires exact applicable contracts.

Synchronous:

- method/path/auth;
- header/path/query/body fields with type/null/default/validation/encoding;
- success and error responses/codes;
- pagination/order/versioning;
- idempotency/timeout/retry/cancellation/rate limits.

Asynchronous:

- channel/direction/producer/consumer;
- complete payload schema: every JSON key, exact type, required/omitempty, zero-value and legacy compatibility;
- queue, timeout, MaxRetry/backoff and whether completion consumes a parent counter;
- order, retry, dedupe, DLQ, replay, poison-message behavior.

A table of “core fields” is a hard failure when an implementer still needs source to construct a compatible payload.

Field lineage:

`UI/client ↔ request/event ↔ domain/service ↔ repository ↔ DB/external field ↔ response/client/display`.

For every sensitive field, audit request, DTO/domain, serialization, persistence/config, logs, list/detail/export responses, encryption and masking. Raw persistence or response exposure omitted from the design is at least S1 when it can leak credentials or private data.

A sequence diagram without exact schemas is insufficient.

### S4 Backend responsibilities and executable flows

Pass requires:

- handler/controller/resolver/consumer ownership;
- validators and authorization;
- service/use-case/domain responsibilities;
- repository/external dependencies;
- method signatures or exact input/output contracts where decisions otherwise remain;
- numbered success and all material failure flows;
- side effects and state outcomes;
- tests or explicit negative evidence.

### S5 Database schema and empty-database reconstruction

If persistence applies, every object must have:

- exact schema/table/collection/view name;
- every column/field with exact type/parameters, nullability, default/generated behavior, meaning/sensitivity;
- primary key including composite order and generation strategy;
- foreign keys with referenced columns, update/delete action, and deferrability;
- unique/check/exclusion/application invariants;
- indexes with keys/order/include/predicate/expression and access rationale;
- sequences, enums/domains, triggers, generated columns, views;
- tenant/partition/shard keys, retention and audit/encryption where relevant;
- migration/schema/ORM/DDL source and version;
- explicit distinction among physical database DEFAULT, migration-only backfill, and application-assigned default;
- engine/extensions/prerequisites;
- empty-database construction order;
- seeds/reference data, backfill, compatibility, rollback/restore, irreversible steps;
- mapping from queries/repositories and DTO fields to physical columns.

Hard fail examples:

- only an entity list or ERD;
- table names without columns;
- columns without PK/FK/constraints/indexes;
- current schema without how it is constructed;
- migration names without ordering, backfill, or rollback;
- database applicability marked N/A despite repository/data access evidence;
- “see source” in place of a reproducible schema.

The reviewer must be able to answer: can a clean database be built and verified without making a new schema decision?

### S6 State, transactions, concurrency, failures, recovery

Pass requires:

- state machines/invariants;
- exact cross-store side-effect order for create/update/delete/reparse/cleanup; error aggregation, partial commits, retry/re-entry, double-apply risk, quota/accounting drift and reconciliation;
- transaction boundaries and isolation/locks/version checks;
- duplicate/idempotency behavior;
- concurrent modification and race outcomes;
- timeouts/retries/cancellation;
- partial failure/compensation;
- crash/restart and recovery;
- migration/job interruption behavior.

### S7 Security and boundaries

Pass requires applicable authn/authz, tenant isolation, input/content validation, injection defenses, secrets, encryption, sensitive logging, privacy/retention, external trust boundaries, abuse/rate controls, and auditable events.

### S8 Delivery and operations

Pass requires applicable:

- build and code generation;
- runtime configuration/default precedence;
- dependency/startup registration;
- migration/deployment order;
- feature flags and compatibility;
- metrics/logs/traces/audit/alerts;
- capacity/latency limits;
- rollback, backup, restore, disaster recovery, and verification.

### S9 Verification, traceability, evidence, closure

Pass requires:

- every behavior or requirement maps to implementation units and verification;
- contract/schema/failure branches have tests or explicit negative evidence;
- coverage matrix totals reconcile;
- conflicts and unknowns have impact/disposition;
- cited evidence is specific and reproducible;
- no claim exceeds its evidence strength.

## 3. AS-IS fidelity gates

### A1 Source pinning and integrity

Full commit, dirty/submodule state, schema head, generated artifacts, and executed evidence are recorded.

### A2 Bidirectional trace

Every behavior has forward and backward traces through all applicable layers. Material outputs/persisted fields can be traced to writers and inputs.

### A3 Source arbitration

Conflicting docs/types/runtime validators/schema/migrations are recorded. The runtime winner is claimed only with evidence.

### A4 Defect/omission classification

| Situation | Classification | Treatment |
|---|---|---|
| Source artifacts contradict each other and design documents contradiction | Source defect | Appendix/conflict ledger; does not by itself fail fidelity |
| Source behavior/schema exists but design omits it | Reconstruction omission | Fail relevant shared gate |
| Source lacks a required capability and design accurately says so | Source limitation | Appendix; may still allow COMPLETE if the observed behavior is fully reconstructed |
| Evidence unavailable | Evidence blocker | PARTIAL or BLOCKED |

### A5 Equivalent reproduction

A second engineer can reconstruct:

- all user-visible frontend states;
- all backend decisions and side effects;
- exact sync/async contracts;
- an empty database with the same schema/invariants/access paths;
- state, concurrency, failures and recovery;
- build/config/deploy/observe/rollback behavior.

Needing source access to choose any material contract makes the relevant gate fail.

## 4. TO-BE authorization gates

### T1 Requirements and traceability

Stable REQ/AC map forward to design/test/operations and backward from implementation units.

### T2 Decision closure

Owners/approvers, selected options, constraints, dependencies, defaults, and unresolved decisions are explicit. No critical TBD/TODO.

### T3 Verification-ready acceptance

Tests are observable, bounded, and cover normal, validation, boundary, concurrency, failure, recovery, security, migration, and rollback as applicable.

### T4 Release feasibility

Migration/backfill/compatibility/deploy/rollback/restore steps are sequenced, owned, observable, and rehearsable.

### T5 Independent implementer convergence

Two competent engineers should not choose materially different UI behavior, contracts, schema, algorithms, state transitions, concurrency, security, recovery, or acceptance.

## 5. Scoring and verdict

Scoring is explanatory, never compensatory. A high aggregate cannot offset a failed hard gate.

For each applicable gate record PASS/FAIL/N/A-with-evidence and confidence.

- S0/S1/S2 block COMPLETE and PASS.
- AS-IS: all S and A gates pass for COMPLETE.
- TO-BE: all S and T gates pass for PASS.
- CONDITIONAL PASS cannot contain an implementation-affecting open item.

## 6. Reviewer evidence procedure

For each missing item:

1. cite the reviewed document location;
2. search cited source/evidence when AS-IS;
3. determine whether the detail exists in source;
4. classify it as source defect, reconstruction omission, or unavailable evidence;
5. state the minimal correction.

This step prevents blaming the source for a shallow document or demanding a TO-BE invention from an AS-IS reconstruction.
