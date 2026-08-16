# Identity and email

## Role and current state

Mosaify has active merged support for first-party HttpOnly cookie sessions, email one-time codes, Google OAuth, and Sign in with Apple. The production OAuth credentials, SMTP vendor, and production enablement of each optional provider are unconfirmed.

`mosaify-api` owns identity verification, session issuance, workspace grants, and authorization. `mosaify-web` presents only the providers the API reports as enabled.

## Data boundary

Permitted data is limited to normalized email, provider subject, verification state, one-time-code state, OAuth state/nonce, session records, and the workspace/actor relationship required for authorization. OAuth access or identity tokens are transient exchange material and must not be copied into analytics, logs, public documentation, or long-lived product records unless a separately reviewed contract requires it.

Never send prompts, project content, media, billing data, session cookies, one-time codes, OAuth tokens, SMTP credentials, or unrelated product activity to an identity or email provider.

Configuration names are `AUTH_SECRET`, legacy fallback `SESSION_SECRET`, `AUTH_COOKIE_SECURE`, `PUBLIC_API_BASE_URL`, `WEB_APP_URL`, `GOOGLE_CLIENT_ID`, `GOOGLE_CLIENT_SECRET`, `GOOGLE_REDIRECT_URI`, `APPLE_CLIENT_ID`, `APPLE_CLIENT_SECRET`, `APPLE_REDIRECT_URI`, `SMTP_HOST`, `SMTP_PORT`, `SMTP_SECURE`, `SMTP_USER`, `SMTP_PASS`, and `SMTP_FROM`.

## Rollout and rollback

1. Apply identity/session schema changes before enabling a provider.
2. Verify exact callback origins, secure-cookie behavior, state/nonce rejection, account linking, logout, and a cross-workspace authorization denial.
3. Canary each provider with a controlled non-customer identity in the target environment.
4. Enable provider presentation only when the server configuration is complete.

Disable one optional OAuth provider by removing its server configuration and confirming it no longer appears in discovery. If email delivery fails, keep OAuth access available where safe and disable new email-code issuance rather than accepting unverifiable codes. Rotate `AUTH_SECRET` only with a deliberate session-invalidation plan.

Authentication failures should alert on rate or availability, not on email address or token contents. One-time-code and session retention must be bounded by their expiration/revocation purpose; provider and SMTP account retention settings remain unconfirmed.
