# fal

## Role

fal provides execution for supported image and video generation paths. Mosaify owns the user contract, job state, persistence, and durable result delivery; fal owns provider execution.

The integration is active in `mosaify-api` and the local `mosaify-cli`. The browser must never call fal directly. Current production account, model enablement, provider retention, and alert configuration are unconfirmed.

## Credential boundary

- Keep provider credentials in the approved secret manager or a local ignored environment file.
- Never expose provider credentials to the browser, commit them, paste them into documentation, or include them in logs and analytics.
- Use separate credentials or scoped accounts for development and production when the provider supports them.

## Request boundary

- Validate supported model, media, duration, aspect ratio, and reference combinations before provider submission.
- Treat provider acceptance as different from a completed durable render.
- Persist result media under Mosaify ownership rather than relying on expiring provider URLs.
- Keep provider task identifiers first-party and out of analytics and error-monitoring payloads.
- Make retries idempotent so recovery cannot create accidental paid duplicate jobs.

Permitted data is limited to the requested prompt, generation settings, selected reference media or provider-readable URLs, provider task state, and generated results. Unrelated customer records, authentication/billing data, Mosaify credentials, and provider task payloads in analytics or error monitoring are prohibited.

Configuration names are `FAL_KEY`, `FAL_BASE_URL`, `FAL_PLATFORM_URL`, `FAL_RUN_BASE_URL`, `FAL_IMAGE_MODEL`, and `FAL_SEEDANCE_VIDEO_MODEL`.

## Rollout, rollback, cost, and alerting

Paid provider canaries must be narrowly scoped, intentionally authorized, and recorded with expected cost and cleanup behavior. Validate the exact model, reference combination, duration, aspect ratio, output decoding, queue polling, timeout, and durable-ingestion path before changing a default.

Roll back a model change to the previously validated endpoint. Roll back fal video routing to a validated alternate provider only if already-submitted fal jobs continue to reconcile. Never retry a paid submission without the same first-party idempotency and credit-reservation boundary.

Alert on sustained submission/polling failures, invalid output, cost anomalies, and first-party ingestion failure using sanitized first-party job IDs. Do not include prompts, reference URLs, provider payloads, or private result URLs. Confirm provider-side retention and production alert settings in the restricted operating record before production use.
