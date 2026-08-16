# Sentry

## Role

Sentry is an essential operational error-monitoring service. The current Mosaify contract is deliberately minimized: error monitoring with PII redaction, without Session Replay or performance tracing.

Current API/web implementation is on coordinated open branches. The service is therefore **adoption in progress** and is not confirmed production-enabled.

## Data boundary

Do not send prompts, messages, feedback text, names, email addresses, authentication secrets, cookies, headers, request or response bodies, private media URLs, billing content, provider payloads, or arbitrary application state.

Scrubbing must happen before transport where possible. Provider-side redaction is a second control, not the only control.

## Operating principles

- Separate development and production environments consistently.
- Resolve production errors to releases and source maps without capturing user content.
- Keep Session Replay and performance tracing disabled until separately reviewed and approved.
- Route actionable alerts to a named engineering owner without duplicate noise.
- Validate enablement with an intentional, content-free error canary.
- Keep an independent rollback path that cannot block the application.

If a sensitive field reaches Sentry, narrow or disable the affected capture path, preserve only the minimum incident evidence, delete the event according to provider procedure, and add a scrubber regression test before re-enabling it.

## Configuration

`mosaify-web` runtime variables are `VITE_SENTRY_DSN`, `VITE_SENTRY_ENVIRONMENT`, and `VITE_APP_RELEASE`. Source-map upload uses build-only `SENTRY_ORG`, `SENTRY_PROJECT`, and `SENTRY_AUTH_TOKEN`; the auth token must never use the `VITE_` prefix or enter a browser bundle. `mosaify-api` uses `SENTRY_DSN`, `SENTRY_ENVIRONMENT`, and `APP_RELEASE`.

## Retention, rollout, and rollback

The proposed production event-retention ceiling is 90 days. Confirm the actual provider configuration before rollout; code cannot establish it.

Canary a content-free client error and server error in the target environment, verify release/source-map resolution, and inspect the complete outbound payload for prohibited fields. Confirm that no event is sent without a DSN and that transport failure cannot fail the product request.

Rollback by removing the relevant DSN or disabling initialization independently on web and API. Retain an application-level error path that works without Sentry. Alerts should identify release, environment, error class, and sanitized route only; destinations and escalation contacts belong in the restricted supplement.
