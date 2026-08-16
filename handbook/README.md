# Mosaify handbook

This handbook records the public knowledge that should survive individual projects, vendor dashboards, and any one person's memory.

## Start here

| Area | Purpose |
| --- | --- |
| [Product thesis](company/product-thesis.md) | The durable product boundary and language used across Mosaify. |
| [System map](engineering/system-map.md) | Repository ownership, runtime boundaries, and cross-system dependencies. |
| [Service catalog](operations/service-catalog.md) | Operational systems, data boundaries, and rollout state. |
| [PostHog](operations/posthog.md) | Consented product analytics and separately consented session replay. |
| [Sentry](operations/sentry.md) | Minimized operational error monitoring. |
| [fal](operations/fal.md) | Provider execution, credential boundary, and failure handling. |
| [Incident response](operations/incident-response.md) | A small, repeatable process for detecting, containing, and learning from incidents. |
| [Access and secrets](security/access-and-secrets.md) | How access is granted and how secret references are documented safely. |
| [Decision records](decisions/README.md) | How durable cross-repository decisions are recorded. |

## Documentation rules

1. Keep a single owner and one canonical source of truth for every consequential decision.
2. Put repository-specific behavior next to the code. Link to it here instead of duplicating it.
3. Document current state separately from intended state. An open pull request or configured vendor account is not a production deployment.
4. Never commit credentials, tokens, customer content, private media URLs, or copied production payloads.
5. Record access instructions using the approved secret-manager entry name and owning role, not the secret value.
6. Review privacy, retention, alerting, rollback, and canary requirements before enabling a new external service.
7. Update the relevant runbook in the same pull request that changes an operational contract.

## Ownership

This repository owns the public handbook. Private operating detail belongs in access-controlled systems, while implementation details, tests, contracts, migrations, and deployment requirements remain with the repository that owns them.
