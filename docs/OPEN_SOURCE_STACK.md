# Open-Source Tool Decision Record

Research date: 2026-10-05

## Adopt for the core plan

### Vendure
Role: commerce substrate for catalog, orders, inventory, channels, administrators, roles, permissions, and plugins.
Decision: preferred over building the commerce domain from scratch. Vendure's Channels and channel-scoped roles directly match merchant workspaces, but CommerceOS must still enforce tenant context across custom entities, jobs, search, caches, object storage, analytics, and agents.

### PostgreSQL
Role: authoritative transactional database.
Decision: required. Every tenant-owned row carries tenant_id. Use composite uniqueness, foreign-key consistency, query middleware, database roles, and row-level security as defense in depth. Do not rely on application filters alone.

### Keycloak
Role: authentication and identity lifecycle.
Decision: use OIDC, MFA, sessions, organizations, and organization groups. Avoid encoding all object permissions into large JWTs.

### OpenFGA
Role: resource-level and relationship-based authorization.
Decision: use for organization/workspace/member relationships, custom merchant roles, approval rights, resource access, and support access. Database tenant filtering remains mandatory.

### OpenTelemetry
Role: common telemetry vocabulary and propagation.
Decision: instrument HTTP, database, queue, workflow, connector, agent, approval, and audit correlation identifiers from the first production pilot.

## Adopt when triggered by measured need

### Temporal
Trigger: long-running workflows, approval waits, connector outages, reconciliation, resumable imports, or multi-day fulfillment processes become difficult to manage with simple jobs.
Decision: approved future durable-execution runtime. Do not make it an MVP dependency unless the first paid workflow demands it.

### Typesense
Trigger: PostgreSQL search is insufficient for typo tolerance, facets, recommendation, semantic search, or search analytics.
Decision: approved derived index. PostgreSQL remains authoritative; enforce tenant-scoped collections or mandatory tenant filters/scoped keys.

### Langfuse
Trigger: TindaBot handles real merchant data or more than controlled prototype flows.
Decision: approved for agent traces, datasets, experiments, evaluations, tool-call analysis, cost, latency, and human feedback. Redaction and retention rules are mandatory.

### Novu
Trigger: multiple notification channels and merchant-managed preferences create recurring engineering load.
Decision: approved optional communication layer. CommerceOS owns business events and delivery intent.

### Metabase
Trigger: internal merchant-success and product analytics require self-service BI.
Decision: approved internal BI tool behind governed models/views. Do not allow unrestricted customer access to shared schemas.

## Hold pending license or commercial review

### Windmill
The repository uses AGPL and Apache licensing plus proprietary enterprise/community terms. Internal developer use may be useful, but embedding, wrapping, reselling, or exposing it as a managed CommerceOS capability requires explicit license review.

### n8n
Useful for internal integration experiments, but its fair-code model is not equivalent to a permissive open-source license for all commercial SaaS patterns. Keep internal-only unless legal review clears the exact use.

## Deliberately deferred

- Kubernetes before operational scale warrants it
- Dedicated data warehouse before analytics volume warrants it
- Separate vector database while PostgreSQL/approved retrieval is sufficient
- Multiple marketplace adapters before one integration proves value
- Autonomous financial execution
- Browser automation as a generic customer capability
