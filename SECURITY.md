# Security Policy

## Reporting Security Issues

Report suspected vulnerabilities privately to the repository owner. Do not open a public issue containing exploit details, credentials, access tokens, personal data, merchant information, or sensitive operational details.

Configure a monitored private security contact before production or public commercial launch.

## Public Repository Rules

Never commit:

- `.env` files or production configuration
- API keys, passwords, tokens, certificates, or private keys
- Marketplace, payment, logistics, email, or social-channel credentials
- Customer or merchant personal data
- Production database exports
- Private prompts, internal agent instructions, scoring logic, or retrieval content
- Private infrastructure addresses or deployment secrets

## Supported Release

Only the latest tagged public preview is supported for security review. Prototype and preview releases are not represented as production-ready systems.

## Security Boundaries

The production architecture must enforce:

- Verified tenant context for every request and background job
- Tenant isolation across database, search, cache, storage, analytics, retrieval, and agent execution
- Role-based and resource-level authorization
- Multi-factor authentication for privileged users
- Encryption in transit and at rest
- Secret management, rotation, and revocation
- Human approval for configured financial and publishing actions
- Idempotency and post-action verification for external side effects
- Audit logs, monitoring, backup, restoration, and incident response
- Prompt-injection, cross-tenant, and authorization-negative testing

## Third-Party Dependencies

All dependencies must undergo license review, version pinning, vulnerability scanning, and software-bill-of-materials generation before production release.

## Disclosure

Do not test against merchant accounts, customer data, or third-party platforms without explicit authorization and an agreed scope.
