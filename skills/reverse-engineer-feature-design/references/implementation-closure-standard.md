# Implementation Closure Standard

## Purpose

This standard prevents a source-code tour from being mislabeled as a reproducible detailed design.

## Mandatory rule

First enumerate the implementation surface, then close every applicable item with exact contracts and pinned evidence. Unknown or absent evidence is never silently converted into design.

## Closure units

### Frontend closure

A frontend surface is closed only when the document identifies:

- route/page/component ownership;
- controls, inputs, defaults, validation, and actions;
- client state, server state, cache, and transitions;
- all loading/empty/partial/error/unauthorized/retry/refresh states;
- outbound and inbound field mapping;
- permission, feature-flag, responsive, accessibility, and telemetry behavior;
- tests or explicit test absence.

### Backend closure

A backend surface is closed only when it identifies:

- entry handler and authorization;
- exact input/output/error contracts;
- orchestration and method ownership;
- repository/external calls;
- transaction, concurrency, idempotency, timeout, and retry;
- failure and recovery branches;
- configuration and observability.

### Contract closure

A synchronous contract needs method/path/headers/path-query-body fields/auth/success/error/versioning/idempotency.
An asynchronous contract needs channel/direction/producer/consumer/payload/order/retry/dedupe/DLQ/replay.
Both require field lineage to domain and persistence.

### Persistence closure

For every persistent object, record:

| Required | Minimum evidence |
|---|---|
| Object identity | physical schema and table/collection/view name |
| Columns | name, exact type, null, default/generated, meaning |
| Primary key | columns/order/generation |
| Foreign keys | local/ref columns and update/delete/deferrability |
| Invariants | unique/check/exclusion/application-only constraints |
| Indexes | keys/order/include/predicate/expression and access rationale |
| Database behavior | sequences/enums/domains/triggers/views |
| Scale and ownership | tenant/partition/shard/retention/sensitivity |
| Provenance | migration/schema/ORM/DDL locator and version |
| Construction | prerequisites and empty-DB build order |
| Evolution | migration, seed, backfill, compatibility, rollback/restore |
| Usage | query/repository plus DTO/field lineage |

If persistence is applicable and any material row is missing, the status cannot be COMPLETE.

### Delivery closure

Record startup registration, config/default precedence, code generation, build commands, dependency services, deployment order, migrations, feature flags, rollback, backup/restore, and operational signals.

## Inventory accounting

Each inventory item is included, excluded-with-evidence, generated, third-party, or unknown. Unknown material items force PARTIAL or BLOCKED.

Every BEH must have at least one entry, implementation path, state/data effect, output, failure evidence, and test/negative-evidence result.

## Counterfactual reproduction test

A second engineer should be able to:

1. construct the schema from an empty database;
2. implement the backend contracts and state transitions;
3. implement the frontend states and field mappings;
4. reproduce failures and concurrency behavior;
5. build, configure, deploy, observe, and roll back the feature.

If they must reopen the repository to choose a table column, key, error contract, state transition, or build/migration order, that unit is not closed.
