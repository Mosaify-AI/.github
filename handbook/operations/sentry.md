# Sentry

## Role

Sentry is an essential operational error-monitoring service. The current Mosaify contract is deliberately minimized: error monitoring with PII redaction, without Session Replay or performance tracing.

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
