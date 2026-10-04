# MVP Implementation Cut Line

## Build now
1. Merchant organization and member onboarding.
2. Keycloak OIDC login and MFA-ready configuration.
3. Merchant roles and OpenFGA authorization model.
4. Vendure-based catalog with tenant/channel boundaries.
5. CSV import with validation, preview, idempotency, and error report.
6. Catalog completeness analysis and content drafts.
7. Merchant approval and export.
8. Basic order, inventory, customer, and audit views.
9. Daily action report driven by deterministic queries.
10. OpenTelemetry correlation across request, job, approval, and agent draft.

## Build after one paid workflow
- First official marketplace adapter.
- Typesense catalog search.
- Novu multi-channel notifications.
- Langfuse production agent observability.
- Temporal durable workflows.
- Metabase internal BI.

## Do not build in MVP
- Autonomous refunds, purchasing, or price changes.
- All marketplaces simultaneously.
- Generic browser control for merchants.
- Cross-merchant benchmark products using identifiable data.
- Lending or financing promises.
- Complex forecasting before sufficient history exists.
- Kubernetes solely for appearance of scale.
