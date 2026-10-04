# Architecture Audit and Upgrade Report

Audit date: 2026-10-05

## Overall verdict

The CommerceOS concept is viable as a service-led, multi-tenant merchant operations product, but the previous blueprint was not complete enough to be called implementation-ready. The v2 blueprint closes the main architecture gaps below.

## Gaps found and upgrades applied

### 1. Commerce core selection was unresolved
Upgrade: adopt Vendure as the preferred commerce substrate because Channels, channel-scoped roles, custom entities, permissions, and plugins map well to merchant workspaces. Keep a proof-of-concept gate before final lock-in.

### 2. Tenant isolation depended too much on the phrase “tenant-aware”
Upgrade: require verified tenant context across HTTP requests, database rows, job payloads, events, object-storage keys, search documents, caches, exports, analytics, RAG documents, agent runs, and audit records. Add cross-tenant tests to CI and use PostgreSQL row-level security where appropriate.

### 3. Authentication and authorization were conflated
Upgrade: Keycloak authenticates users and manages organization identity; OpenFGA decides resource permissions. Application services still enforce business policy and tenant database boundaries.

### 4. Workflow technology was over-specified
Upgrade: start MVP with Postgres-backed jobs and explicit idempotency. Introduce Temporal only for workflows that demonstrably need durable timers, long approval waits, state replay, or multi-day recovery.

### 5. Agent observability lacked a concrete implementation
Upgrade: standardize telemetry with OpenTelemetry and use Langfuse when TindaBot touches real merchant workflows. Redact credentials, secrets, and unnecessary customer content.

### 6. Connector reliability was incomplete
Upgrade: every connector needs versioned schemas, scoped credentials, rate limiting, signed-webhook validation, replay defense, idempotency keys, cursor checkpoints, dead-letter handling, reconciliation, and merchant-visible health.

### 7. Analytics risked becoming another source of truth
Upgrade: analytics, search, and warehouse records are derived. Order, inventory, customer, catalog, approval, and payment state remain authoritative in domain services/PostgreSQL.

### 8. Governance Agent had enforcement language
Upgrade: the Governance/Audit Agent is read-only assurance. Keycloak/OpenFGA/application policy gates enforce access and side effects.

### 9. MVP scope still risked too many services
Upgrade: define a minimum deployment: Next.js, Vendure/CommerceOS API, PostgreSQL, Keycloak, OpenFGA for sensitive resources, simple jobs, OpenTelemetry. Everything else waits for an explicit trigger.

### 10. Licensing needed stricter treatment
Upgrade: add a license gate for every dependency. Permissive licenses are preferred for embedded components. AGPL, fair-code, source-available, community-edition restrictions, trademarks, and hosted-service limitations require recorded legal review.

## Remaining external gates

- Marketplace developer approval and per-market API availability
- Data Privacy Act / NPC professional review
- BIR invoicing and recordkeeping design
- DTI and consumer-protection review
- Payment-provider merchant onboarding and PCI responsibility mapping
- Commercial software license review
- Merchant discovery and willingness-to-pay evidence

## Release gate

Do not begin broad multi-channel implementation until:

1. Fifteen merchant interviews are completed.
2. Three design partners are secured.
3. At least one merchant pays for a setup or workflow improvement.
4. One channel or CSV workflow is selected.
5. Tenant-isolation tests pass.
6. Backup restore is tested.
7. The exact dependency licenses are recorded and approved.
