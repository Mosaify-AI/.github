# PostHog

## Role

PostHog provides product analytics only after Product Analytics consent. Session Replay is a separate choice and must never be inferred from analytics consent.

The integration is rollout-gated. A configured account, installed package, or merged pull request does not establish production readiness.

## Ownership boundary

- `mosaic-web` owns consent presentation, browser-local consent state, lazy SDK initialization, replay gating, route normalization, and browser event sanitization.
- `mosaic-api` owns authoritative generation and credit-purchase lifecycle events and validates current consent before capture.
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
