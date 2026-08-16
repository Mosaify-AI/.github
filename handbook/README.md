# Mosaify handbook

This handbook records the public knowledge that should survive individual projects, vendor dashboards, and any one person's memory.

## Start here

| Area | Purpose |
| --- | --- |
| [Product thesis](company/product-thesis.md) | The durable product boundary and language used across Mosaify. |
| [System map](engineering/system-map.md) | Repository ownership, runtime boundaries, and cross-system dependencies. |
| [Tools and services catalog](operations/service-catalog.md) | Complete evidenced inventory, ownership, data boundaries, configuration names, and lifecycle state. |
| [GitHub delivery](operations/github-delivery.md) | Source control, Projects, CI, automation permissions, and rollback. |
| [Data and media](operations/data-and-media.md) | PostgreSQL, durable S3-compatible storage, and local MinIO boundaries. |
| [Identity and email](operations/identity-and-email.md) | Sessions, email codes, Google/Apple sign-in, and SMTP. |
| [Stripe](operations/stripe.md) | Billing authority, webhook settlement, rollout, and enforcement rollback. |
| [OpenAI](operations/openai.md) | Language/image operations and compatibility-classification boundaries. |
| [Anthropic](operations/anthropic.md) | Optional local CLI assistant boundary and rollback. |
| [PostHog](operations/posthog.md) | Consented product analytics and separately consented session replay. |
| [Sentry](operations/sentry.md) | Minimized operational error monitoring. |
| [fal](operations/fal.md) | Provider execution, credential boundary, and failure handling. |
| [BytePlus](operations/byteplus.md) | Alternate direct Seedance execution and provider rollback. |
| [Feedback and Turnstile](operations/feedback-and-turnstile.md) | Feedback persistence, abuse protection, retention, and rollout. |
| [Third-party web assets](operations/third-party-web-assets.md) | Google Fonts and Simple Icons browser-request boundaries. |
| [Content provenance](operations/content-provenance.md) | Pexels and original-asset evidence, promotion, and removal controls. |
| [Incident response](operations/incident-response.md) | A small, repeatable process for detecting, containing, and learning from incidents. |
| [Access and secrets](security/access-and-secrets.md) | How access is granted and how secret references are documented safely. |
| [Decision records](decisions/README.md) | How durable cross-repository decisions are recorded. |

## Documentation rules

1. Keep a single owner and one canonical source of truth for every consequential decision.
2. Put repository-specific behavior next to the code. Link to it here instead of duplicating it.
3. Document current state separately from intended state. An open pull request or configured vendor account is not a production deployment.
4. Never commit credentials, tokens, customer content, private media URLs, or copied production payloads.
5. Keep account names, dashboard links, secret-manager references, alert destinations, and access instructions in the private coordination supplement; public pages describe roles and controls only.
6. Review privacy, retention, alerting, rollback, and canary requirements before enabling a new external service.
7. Update the relevant runbook in the same pull request that changes an operational contract.

## Ownership

This repository owns the public handbook. Private operating detail belongs in access-controlled systems, while implementation details, tests, contracts, migrations, and deployment requirements remain with the repository that owns them.
