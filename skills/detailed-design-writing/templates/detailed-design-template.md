# Detailed Design — <system / feature>

> Status: DRAFT — NOT READY FOR FORMAL REVIEW / READY FOR INDEPENDENT REVIEW
> Version / commit:
> Author / owner:
> Required reviewers:
> Approval authority:
> Last updated:
> Supersedes / previous review:

## 0. Applicability and evidence status

### 0.1 Applicability

| Domain | Applicable | Rationale / evidence | Confirmed by |
| --- | --- | --- | --- |
| CORE | Yes | | |
| UI | Yes/No | | |
| API | Yes/No | | |
| EVENT | Yes/No | | |
| DATA | Yes/No | | |
| SECURITY | Yes/No | | |
| OPS | Yes/No | | |

### 0.2 Source index

| Source | Version / commit | Owner | Used for | Status |
| --- | --- | --- | --- | --- |

### 0.3 Statement status

Use `CONFIRMED`, `INFERRED`, `PROPOSED`, or `OPEN` on material claims and decisions.

## 1. Executive summary and scope

### 1.1 Problem and outcome

- Problem:
- Business/user outcome:
- Success measures:

### 1.2 Goals and non-goals

- In scope:
- Out of scope:
- Explicitly unchanged:

### 1.3 Ownership and boundaries

- System of interest:
- Owners:
- Upstream/downstream systems:
- Compatibility boundary:
- Approval authority:

### 1.4 Assumptions, constraints, and dependencies

| ID | Type | Statement | Evidence / owner | Impact if false |
| --- | --- | --- | --- | --- |

## 2. Current state, target, and gap analysis

### 2.1 Current capability and limits

Describe confirmed behavior, unsupported behavior, constraints, topology, contracts, data, tests, and operations. Cite versioned evidence.

### 2.2 Target capability

Define observable target behavior and measurable acceptance criteria.

### 2.3 Gap-to-implementation map

| Gap ID | Current evidence | Target REQ/AC | Consequence | Modules / landing points | Contract/data/ops change | Verification |
| --- | --- | --- | --- | --- | --- | --- |

## 3. Requirements and acceptance baseline

| REQ ID | Requirement | Priority | Source | AC IDs | Owner |
| --- | --- | --- | --- | --- | --- |

| AC ID | Given / precondition | When / stimulus | Then / measurable result | Verification ID |
| --- | --- | --- | --- | --- |

## 4. Stakeholders, concerns, and views

| Stakeholder | Concern | Required view/evidence | Location | Status |
| --- | --- | --- | --- | --- |

### 4.1 System context and trust boundaries

Include actors, external systems, ownership, protocols, data movement, and trust boundaries.

### 4.2 Static decomposition

For each module: responsibility, owned data, public contracts, dependencies, forbidden dependencies, scaling/failure unit, and code landing point.

### 4.3 Runtime interactions

Provide sequences for critical flows, async boundaries, timeout, retry, cancellation, and failure propagation.

### 4.4 Deployment and resource view

Include processes/nodes, networks, fault domains, storage, secrets, CPU/memory/connections/queues/bandwidth, scaling, and environment differences.

### 4.5 Cross-view consistency rules

State canonical names, ownership, allowed directions, and how representations correspond.

## 5. Critical flows and state behavior

For each flow use this structure.

### FLOW-<id> — <name>

- Requirement/AC:
- Actor and trigger:
- Preconditions and authorization:
- Main sequence:
- UI/caller state:
- API/event interactions:
- Domain decisions and invariants:
- Data/message/cache effects:
- Final user/data/operational state:
- Logs/metrics/traces/audit:

| Branch | Trigger | Expected behavior | Final state | Recovery/operator action | Verification |
| --- | --- | --- | --- | --- | --- |
| Business rejection | | | | | |
| Unauthorized | | | | | |
| Timeout/outage | | | | | |
| Retry exhausted | | | | | |
| Duplicate/concurrent | | | | | |
| Delayed/out-of-order | | | | | |
| Cancellation/disconnect | | | | | |
| Partial success | | | | | |
| Restart/resume | | | | | |

## 6. UI and client-state design

Delete only when UI is validly N/A and recorded in section 0.

- State source of truth:
- URL/navigation state:
- Server/cache state:
- Form/draft state:
- Local UI state:
- Race/cancellation rules:
- Optimistic update and rollback:
- Refresh/back/deep-link/multi-tab/reconnect:
- Keyboard/focus/responsive/accessibility target:

| UI ID | Initial | Loading | Empty | Success | Partial/stale | Error | Unauthorized | Offline | Submitting/duplicate |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |

## 7. API/RPC contracts

Reference a versioned OpenAPI/protobuf/JSON Schema artifact when practical.

### API-<id> — <method/path/name>

- Owner / consumers:
- Authentication and authorization:
- Request schema and example:
- Response schema and example:
- Required/null/default/range/unit/time-zone/precision:
- Status and machine-readable errors; caller behavior:
- Safe/idempotent classification:
- Idempotency-key scope/storage/mismatch/replay/expiry/late request:
- Timeout/retry/backoff/jitter/cancellation:
- Pagination/order/filter/sort/payload limits:
- Rate/quota:
- Version/compatibility/deprecation:
- Contract tests:

## 8. Events, jobs, streams, and webhooks

### EVT-<id> — <name>

- Producer / consumers:
- Topic/job/trigger:
- Schema and version:
- Partition/order key:
- Delivery semantics:
- Dedupe/idempotent side effects:
- Retry/backoff/DLQ/retention:
- Replay/late/out-of-order/poison behavior:
- DB-write/publish atomicity:
- Backlog/lag monitoring:
- Recovery/reconciliation/manual repair:
- Verification:

## 9. Data, state, consistency, and migration

### 9.1 Data model

| DATA ID | Entity/field | Owner/source of truth | Type/constraints/null/unit/time | Sensitivity | Lifecycle |
| --- | --- | --- | --- | --- | --- |

Include relations, keys, unique/check constraints, access patterns, indexes, cardinality, growth, hot keys, partitioning, and tenant isolation.

### 9.2 Invariants and state machine

| INV ID | Invariant | Enforcement point | Concurrent behavior | Verification |
| --- | --- | --- | --- | --- |

| Current state | Event/command | Guard | Action | Next state | Illegal/duplicate behavior |
| --- | --- | --- | --- | --- | --- |

### 9.3 Transactions and concurrency

- Atomic boundary:
- Isolation:
- Lock/conditional update/optimistic version:
- Lock order/deadlock/serialization retry:
- Competing-write outcome:
- Cross-service consistency/Saga/outbox:
- Compensation/reconciliation:

### 9.4 Cache

- Source of truth/key/tenant:
- TTL/freshness:
- Read/write/invalidation order:
- Stampede/penetration controls:
- Stale/miss/outage behavior:
- Capacity/eviction/sensitive isolation:

### 9.5 Migration and recovery

- Forward migration:
- Expand–migrate–contract / compatibility window:
- Backfill and validation:
- Lock/performance impact:
- Failure recovery:
- Code rollback after schema change:
- Backup/restore:
- Irreversible-change approver:

## 10. Security, privacy, and compliance

### 10.1 Threat and abuse model

- Assets and sensitive data:
- Trust boundaries and entry points:
- Attackers/abuse cases:
- Third parties and data exposure:

| Threat/abuse ID | Scenario | Control | Detection | Negative test | Residual risk |
| --- | --- | --- | --- | --- | --- |

### 10.2 Identity and access

- Deny-by-default authorization:
- Function/object/property/tenant rules:
- Session/token/key issue, storage, TTL, refresh, revoke, rotate:
- Reauthentication/MFA:
- Audit:

### 10.3 Application and data controls

Cover applicable validation/encoding, CSRF, XSS/CSP, CORS, SSRF/egress, injection, upload, secrets, encryption, masking, safe logging, brute-force/rate controls, privacy minimization/retention/deletion/export/residency/consent.

## 11. Quality attributes and capacity

| QA ID | Source | Stimulus | Artifact | Environment | Response | Measure/threshold | Verification |
| --- | --- | --- | --- | --- | --- | --- | --- |

- Workload/traffic model:
- Peak/growth/burst:
- Bottlenecks and capacity margin:
- Quota/backpressure/load shedding/degradation:
- Scaling trigger and delay:
- Sensitivity/tradeoff points:

## 12. Observability and operational ownership

| OPS ID | Journey/failure | Signal and fields | SLI/SLO/threshold | Dashboard/alert | Runbook/action | Owner |
| --- | --- | --- | --- | --- | --- | --- |

- Correlation/request/idempotency/saga IDs:
- Latency p50/p95/p99:
- Traffic/errors/saturation:
- Secret/PII-safe telemetry:
- Error-budget action:
- Reconciliation/audit:

## 13. Verification and acceptance design

| TEST ID | REQ/AC/INV/RISK/QA | Level | Setup/input/environment | Dependency behavior | Expected result/oracle | Threshold | Owner |
| --- | --- | --- | --- | --- | --- | --- | --- |

Cover applicable unit, contract, integration, critical E2E, concurrency, duplicate/out-of-order, timeout/retry, failure injection, migration compatibility, rollback, restore, load/capacity, accessibility, and security-negative tests.

- Test data and privacy:
- Repeatability/flaky handling:
- Cleanup:
- Failure disposition:
- Post-release verification:

## 14. Delivery, rollback, and disaster recovery

### 14.1 Release plan

- Immutable artifact/version:
- Configuration/secrets:
- Rollout strategy and sequence:
- Feature flags:
- Health/readiness/liveness/startup gates:
- Stop conditions:
- Automatic/manual rollback triggers:

### 14.2 Compatibility and rollback matrix

| Component | Forward compatibility | Mixed-version window | Rollback behavior | Verification |
| --- | --- | --- | --- | --- |
| Application | | | | |
| Database/schema | | | | |
| Event schema | | | | |
| Cache | | | | |
| Configuration/flag | | | | |

### 14.3 Recovery

- RTO/RPO:
- Backup scope/frequency/encryption/retention/fault domain:
- Restore order and dependencies:
- Traffic/DNS switch:
- Reconciliation/manual repair:
- Exercise evidence:

## 15. Decisions, alternatives, risks, and open items

### 15.1 Decision log

| DEC ID | Decision | Alternatives | Rationale | Positive/negative tradeoff | Approver | Invalidation trigger |
| --- | --- | --- | --- | --- | --- | --- |

### 15.2 Risk register

| RISK ID | Trigger | Impact/likelihood | Mitigation/detection | Contingency | Owner/due | Residual approver |
| --- | --- | --- | --- | --- | --- | --- |

### 15.3 Open items

| OPEN ID | Question | Critical behavior affected | Owner | Due | Blocks review? | Resolution location |
| --- | --- | --- | --- | --- | --- | --- |

No critical open item may remain when status is READY FOR INDEPENDENT REVIEW.

## 16. Traceability and review handoff

Attach or complete [traceability-matrix.md](traceability-matrix.md).

- Document version frozen:
- Evidence links accessible:
- Cross-view consistency checked:
- Critical TODO/TBD/TBC/OPEN count:
- Changed sections since previous review:
- Requested domain reviewers:
- Author readiness result:
- Handoff statement: Ready / Not ready for independent review
