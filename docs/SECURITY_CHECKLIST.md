# Tenant Isolation and Security Checklist

## Every request
- Validate session/token signature, issuer, audience, expiry, and authentication strength.
- Resolve an active tenant context independently of user-provided object identifiers.
- Check OpenFGA/resource permission for sensitive objects.
- Apply application policy for plan, state, amount, approval, and rate limits.

## Every data path
- tenant_id on tenant-owned authoritative tables.
- Composite keys and uniqueness include tenant_id where appropriate.
- Row-level security or equivalent database boundaries for sensitive tables.
- Tenant-prefixed object-storage paths and signed URLs.
- Tenant filter/scoped key on every search query.
- Tenant namespace on caches, jobs, traces, RAG documents, exports, and metrics.

## Every side effect
- Idempotency key and operation identifier.
- Expected object version / stale-state check.
- Human approval for financial or publishing actions as configured.
- Verify external result after execution.
- Reconcile unknown outcomes instead of blind retry.
- Emit immutable audit evidence.

## Every agent run
- Minimum context only.
- Approved tenant-scoped retrieval.
- Typed tools with explicit scopes.
- No direct database mutation.
- Secret and personal-data redaction.
- Trace, model, prompt, tool, latency, cost, and evaluation metadata.
- Prompt-injection and cross-tenant tests.

## Every release
- Dependency license scan.
- Secret scan and SBOM.
- SAST, dependency vulnerability scan, and container scan.
- Migration test and rollback rehearsal.
- Backup restore test.
- Cross-tenant negative tests.
- Public/private IP leakage scan.
