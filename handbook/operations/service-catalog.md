# Service catalog

This catalog records why each external system exists, the boundary it is allowed to cross, and what must be true before it is treated as production-ready.

| System | Purpose | Data boundary | Current state |
| --- | --- | --- | --- |
| GitHub | Source control, review, issues, delivery automation, and organization profile | Code and repository metadata according to repository visibility and app permissions | Active |
| PostHog | Consented product analytics and separately consented session replay | Explicit event/property allowlists; no prompts, messages, private identifiers, media, billing content, or arbitrary DOM/network content | Adoption in progress; rollout gated |
| Sentry | Essential error monitoring | Minimized errors with PII redaction; no replay or tracing in the current contract | Adoption in progress; rollout gated |
| fal | Image and video provider execution | Server or local-client requests only; provider credentials and task identifiers stay out of browser and analytics payloads | Active in supported generation paths |
| Stripe | Credit-purchase checkout and webhook settlement | Provider identifiers remain first-party; the API owns authoritative purchase state | Integration in progress |

## Catalog requirements

Every active service must have a private operating record for account names, owning roles, dashboard links, secret references, data classification, retention, alerting, enablement, rollback, canaries, and its owning integration repository.

Missing details are work to complete, not permission to publish private configuration or production payloads.
