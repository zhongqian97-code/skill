# <Project> — <Feature> AS-IS Full-Stack Detailed Design

> Reconstruction status: COMPLETE | PARTIAL | BLOCKED
> Purpose: learning / comparison / reuse baseline
> This AS-IS document describes pinned source behavior. It does not authorize implementation in another product.

## 0. Source fingerprint

| Item | Value | Evidence |
|---|---|---|
| Repository | | |
| Full commit SHA | | |
| Dirty/submodule state | | |
| Package/lock versions | | |
| Schema/migration head | | |
| Generated artifacts | | |
| Execution authorization | | |

## 1. Scope and observed behaviors

### 1.1 Included / excluded boundary

### 1.2 Behavior catalog

| BEH ID | Trigger/actor | Success result | Validation/failure/concurrency variants | Evidence | Status |
|---|---|---|---|---|---|

## 2. Implementation-surface census

| INV ID | Layer | File/object and symbol | Role | Status | Exclusion or evidence |
|---|---|---|---|---|---|
| | Frontend | | | included/excluded/generated/third-party/unknown | |
| | API/contract | | | | |
| | Backend | | | | |
| | Persistence/migration | | | | |
| | Async/job | | | | |
| | Build/config/deploy | | | | |
| | Tests | | | | |

State census totals and all material unknowns.

## 3. System context and runtime topology

Include actors, containers/services, external dependencies, trust boundaries, deployment nodes, startup registration, and feature flags.

## 4. Frontend detailed design

### 4.1 Routes, pages, components

| Route/entry | Page/component | Parent/child ownership | Guard/flag | Evidence |
|---|---|---|---|---|

### 4.2 Controls and fields

| UI field/control | Type | Default | Validation | Enabled/visible rule | Action | Evidence |
|---|---|---|---|---|---|---|

### 4.3 State model

| State | Entry condition | Visible result | Allowed action | Transition | Failure/recovery | Evidence |
|---|---|---|---|---|---|---|

Cover loading, empty, partial, stale, error, unauthorized, retry, refresh, navigation, responsive, accessibility, localization, and analytics where applicable.

### 4.4 Client data and cache

Document stores/hooks/queries, cache keys, invalidation, optimistic updates, refresh/reload behavior, and client tests.

## 5. Frontend/backend interaction contracts

### 5.1 Synchronous APIs

| Contract ID | Method/path | Auth | Request schema | Success schema | Errors | Idempotency/timeout/version | Evidence |
|---|---|---|---|---|---|---|---|

Give field-level request and response tables, including type, nullability, default, validation, encoding, and semantic meaning.

### 5.2 Events, queues, jobs, webhooks

| Contract ID | Channel/direction | Producer | Consumer | Payload schema | Ordering/retry/dedupe/DLQ/replay | Evidence |
|---|---|---|---|---|---|---|

### 5.3 End-to-end field lineage

| Field ID | UI/client field | Request/event field | Domain/service field | Repository parameter | DB column/external field | Response/client/display | Evidence |
|---|---|---|---|---|---|---|---|

## 6. Backend detailed design

### 6.1 Modules and responsibilities

| Module/class/function | Inputs/outputs | Responsibility | Dependencies | Transaction/error behavior | Evidence |
|---|---|---|---|---|---|

### 6.2 Main flows

For each BEH provide numbered success and failure steps from entry through persistence/side effects and back to the rendered/output result.

### 6.3 Transactions, concurrency, idempotency

Specify transaction boundaries, isolation/locks, optimistic versions, uniqueness races, duplicate handling, timeout/retry/cancellation, compensation, and crash recovery.

## 7. Database and persistence reconstruction

If persistence is not applicable, prove that conclusion with source-search evidence. Otherwise complete every subsection.

### 7.1 Database topology and source of truth

State database engine/version, schemas, extensions, migration framework, ORM/codegen, schema head, and precedence when representations conflict.

### 7.2 Table/object catalog

| Object | Kind | Purpose/owner | Read/write paths | Source migration/schema | Evidence |
|---|---|---|---|---|---|

### 7.3 Complete schema per object

Repeat for every table/collection/view:

#### <schema.object>

| Column/field | Exact type | Null | Default/generated | Meaning/sensitivity | Writer/readers | Evidence |
|---|---|---|---|---|---|---|

| Constraint/index | Exact definition | Columns/order/ref | Update/delete/deferrable or predicate/include | Rationale/invariant | Evidence |
|---|---|---|---|---|---|

Record PK generation, FK actions, unique/check/exclusion constraints, sequences, enums/domains, triggers, views, tenant/partition/shard keys, retention, and encryption/audit behavior.

### 7.4 Relationship diagram

The diagram supplements, but does not replace, exact table definitions.

### 7.5 Empty-database construction

| Order | Prerequisite/migration/DDL | Objects created or changed | Transaction/lock | Failure/retry | Evidence |
|---|---|---|---|---|---|

Include extensions, seeds/reference data, application startup assumptions, schema-version detection, and verification commands.

### 7.6 Evolution, backfill, rollback, restore

Document compatibility windows, online/offline migration behavior, backfills, irreversible steps, rollback, backup/restore, and schema drift checks.

### 7.7 Query and access-path mapping

| Repository/query | SQL/ORM behavior | Tables/columns | Expected index | Lock/consistency | Evidence |
|---|---|---|---|---|---|

## 8. Failure, security, and operations

| Scenario | Detection | Observed behavior | State/data outcome | Recovery/compensation | Telemetry | Evidence |
|---|---|---|---|---|---|---|

Cover authn/authz, tenant isolation, injection/content validation, secrets/logging, capacity/latency, metrics/logs/traces/audit/alerts, deployment, feature flags, rollback, backup/restore.

## 9. Build, configuration, and deployment

Provide exact build/codegen/migration/start commands only when evidenced, configuration/default precedence, dependency services, deployment order, health checks, and rollback.

## 10. Verification and tests

| BEH/contract/object | Test or runtime evidence | Branches covered | Missing branch/negative evidence | Result |
|---|---|---|---|---|

## 11. Conflicts, unknowns, and source defects

| ID | Type | Conflicting/absent artifacts | Runtime winner or unknown | Impact on reproduction | Disposition |
|---|---|---|---|---|---|

Source defects belong here and do not become documentation omissions, provided the observed behavior and impact are documented.

## 12. Coverage and equivalent-reproduction audit

| Unit | Applicable | Inventory total | Closed | Unknown | Evidence gaps | Verdict |
|---|---:|---:|---:|---:|---|---|
| Behaviors | | | | | | |
| Frontend | | | | | | |
| API/async contracts | | | | | | |
| Backend | | | | | | |
| Database/persistence | | | | | | |
| Failure/security/ops | | | | | | |
| Build/deploy/tests | | | | | | |

Answer explicitly whether a second engineer can construct an empty database and reproduce the full feature without reopening the source.

## 13. Final status

- Status: COMPLETE RECONSTRUCTION | PARTIAL RECONSTRUCTION | BLOCKED RECONSTRUCTION
- Material open items:
- Recommended next evidence:
- AS-IS baseline suitability for a separate TO-BE design:
