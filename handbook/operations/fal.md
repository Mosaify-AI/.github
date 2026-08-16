# fal

## Role

fal provides execution for supported image and video generation paths. Mosaify owns the user contract, job state, persistence, and durable result delivery; fal owns provider execution.

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

Paid provider canaries must be narrowly scoped, intentionally authorized, and recorded with expected cost and cleanup behavior.
