# Standards and source notes

Use these sources to explain why a gate exists. Do not claim that a source certifies the reviewed system.

## Traditional design and architecture

- [NASA NPR 7150.2D](https://nodis3.gsfc.nasa.gov/displayDir.cfm?t=NPR&c=7150&s=2D): §4.3 requires lower-level units to be described so they can be coded, compiled, and tested; §3.12 covers bidirectional traceability.
- [IEEE 1016-2009](https://standards.ieee.org/ieee/1016/4502/): software design descriptions organized around stakeholders, concerns, viewpoints, views, design elements, relationships, constraints, and rationale.
- [ISO/IEC/IEEE 42010:2022](https://www.iso.org/standard/74393.html): architecture descriptions, stakeholders, concerns, viewpoints, views, correspondences, and decisions.
- [ISO/IEC/IEEE 29148:2018](https://www.iso.org/standard/72089.html): requirements quality and traceability.
- [ISO/IEC 25010:2023](https://www.iso.org/standard/78176.html): product quality model; use it to select quality concerns, then define system-specific measurable targets.
- [SEI ATAM](https://www.sei.cmu.edu/library/atam-method-for-architecture-evaluation/): quality-attribute scenarios, risks, sensitivity points, and tradeoff points.
- [NIST SP 800-218 SSDF](https://csrc.nist.gov/pubs/sp/800/218/final): threat modeling, traceable security decisions, independent design review, and finding remediation.
- [OWASP ASVS](https://owasp.org/www-project-application-security-verification-standard/): cumulative application-security verification requirements.
- [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119): normative MUST/SHOULD/MAY vocabulary.

## Modern Web contracts and operations

- [OpenAPI 3.1.1](https://spec.openapis.org/oas/v3.1.1.html): versioned API paths, operations, schemas, responses, and security requirements.
- [RFC 9110 idempotency](https://www.rfc-editor.org/rfc/rfc9110.html#section-9.2.2): HTTP idempotent semantics and retry constraints.
- [AWS safe retries](https://aws.amazon.com/builders-library/making-retries-safe-with-idempotent-APIs/): caller request IDs, atomic idempotency records, parameter mismatch, retention, and late requests.
- [PostgreSQL transaction isolation](https://www.postgresql.org/docs/current/transaction-iso.html): isolation behavior and serialization retry requirements.
- [Azure Saga](https://learn.microsoft.com/en-us/azure/architecture/patterns/saga): local transactions, compensation, pivot/retryable steps, and workflow tracking.
- [Azure Transactional Outbox](https://learn.microsoft.com/en-us/azure/architecture/databases/guide/transactional-out-box-cosmos): remove the business-write/message-publish loss window while handling duplicates and order.
- [Azure Cache-Aside](https://learn.microsoft.com/en-us/azure/architecture/patterns/cache-aside): freshness, eviction, failure, and local-cache inconsistency tradeoffs.
- [OWASP API Security Top 10 2023](https://owasp.org/API-Security/editions/2023/en/0x11-t10/): object authorization, resource consumption, SSRF, inventory, configuration, and unsafe third-party API risks.
- [OWASP Authorization Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html): least privilege, deny by default, and validation on every request.
- [Google SRE: Implementing SLOs](https://sre.google/workbook/implementing-slos/): SLI/SLO definitions, windows, ownership, error budgets, and budget actions.
- [Google SRE: Monitoring Distributed Systems](https://sre.google/sre-book/monitoring-distributed-systems/): latency, traffic, errors, saturation, tail latency, and actionable symptom-based alerts.
- [Kubernetes Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/): rolling-update controls, progress detection, revision history, and rollback.
- [Kubernetes probes](https://kubernetes.io/docs/concepts/configuration/liveness-readiness-startup-probes/): readiness, liveness, startup, and cascade risks.
- [AWS RTO and RPO](https://docs.aws.amazon.com/whitepapers/latest/disaster-recovery-workloads-on-aws/recovery-time-objective-and-recovery-point-objective.html): quantified recovery time and data-loss objectives.
- [Google Testing Blog: test pyramid](https://testing.googleblog.com/2015/04/just-say-no-to-more-end-to-end-tests.html): many unit tests, fewer integration tests, and few critical E2E tests; use risk rather than a mechanical ratio.
- [WCAG 2.2](https://www.w3.org/WAI/standards-guidelines/wcag/): testable accessibility principles and success criteria.

## Interpretation boundaries

- Standards define information, process, quality, or evaluation concerns; they do not prescribe a universal page count, diagram count, UML usage, or function-by-function pseudocode.
- ATAM reveals architectural risks and tradeoffs; it does not replace load, security, recovery, or acceptance testing.
- Quality models classify concerns; they do not supply the reviewed system's thresholds.
- Cloud well-architected guidance is a prompt set, not proof that a specific design is safe.
- A linked specification counts only when versioned, accessible, applicable, and consistent with the reviewed document.
