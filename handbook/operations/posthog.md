# PostHog

## Role

PostHog provides product analytics only after Product Analytics consent. Session Replay is a separate choice and must never be inferred from analytics consent.

The integration is rollout-gated. A configured account, installed package, or merged pull request does not establish production readiness.

Current repository evidence places the API and web implementation on coordinated open branches. It is therefore **adoption in progress**, not confirmed production telemetry.

## Ownership boundary

- `mosaify-web` owns consent presentation, browser-local consent state, lazy SDK initialization, replay gating, route normalization, and browser event sanitization.
- `mosaify-api` owns authoritative generation and credit-purchase lifecycle events and validates current consent before capture.
- Analytics transport failures are non-fatal to product behavior.
- Unknown events or unsafe properties must be rejected before transport.

## Prohibited data

Do not send prompts, chat or feedback text, names, email addresses, authentication data, project or media titles, copied values, uploads, generated media, canvas contents, private URLs, cookies, headers, request or response bodies, console logs, billing session IDs, provider task IDs, or arbitrary DOM text and attributes.

Do not create an advertising pixel, retargeting audience, or conversion API from this integration without a separate product, privacy, and legal decision.

## Consent invariants

1. Declining analytics leaves product access unchanged and produces no analytics initialization or traffic.
2. Analytics and replay choices are independent and equally available.
3. Withdrawal stops later ingestion, resets identity, and disables SDK persistence.
4. Server events require the latest accepted, unexpired, correctly associated consent receipt.
5. Replay remains fully masked and excludes authentication, prompts, feedback, billing, media, canvas, network, console, and cross-origin content.

If prohibited data is observed, disable the affected capture path immediately, preserve only the minimum incident evidence, start the incident process, and follow the provider's deletion procedure.

## Configuration

`mosaify-web` uses `VITE_POSTHOG_PROJECT_TOKEN` and `VITE_POSTHOG_HOST`. `mosaify-api` uses `POSTHOG_PROJECT_TOKEN` and `POSTHOG_HOST`. These identifiers may be documented, but values, account names, project names, and dashboard URLs must not be published.

## Retention, rollout, and rollback

The proposed production targets are 24 months for curated events, 90 days for raw autocapture/heatmap data, and 30 days for replay. Counsel approval and provider-side verification are required before rollout; repository code cannot prove configured retention.

Canary in this order: decline all consent and verify zero SDK/network activity; enable analytics without replay; withdraw and verify reset/no later ingestion; enable replay separately on a controlled account; validate server events against valid, expired, and withdrawn consent receipts. Inspect payloads at the network boundary, not only the UI.

Rollback by removing the client token/host and server token/host or disabling the initialization path. Product behavior must remain available when PostHog is absent or failing. Alert on prohibited payloads, unexpected ingestion after withdrawal, and sustained transport failures without copying event contents into the alert.
