# Third-party web assets

## Current state

`mosaify-web` currently makes two unauthenticated browser-side asset requests that are separate from the API and telemetry systems:

- Google Fonts CSS/font delivery for Space Grotesk and Plus Jakarta Sans;
- Simple Icons CDN requests for technology/brand icons in a marketing animation.

These are active in both development and production bundles unless deployment policy rewrites or blocks them.

## Data boundary

Only the asset URL and ordinary browser network metadata should reach these services. Mosaify must not append user, workspace, project, prompt, media, authentication, billing, analytics, or support identifiers. These requests must not be treated as consent for product analytics or advertising.

## Reliability, privacy, and rollback

- Keep the page usable if either service is unavailable or blocked.
- Review content-security policy and privacy disclosure before production launch.
- Canary a production build with the external requests allowed and blocked; verify layout, caching, and fallbacks.
- Roll back by self-hosting approved font/icon assets or removing the affected presentation.
- Do not use remote icon requests for user-derived slugs or data.

Neither service has a Mosaify configuration variable. Provider-side log retention is unconfirmed. No customer payload should be present to retain.
