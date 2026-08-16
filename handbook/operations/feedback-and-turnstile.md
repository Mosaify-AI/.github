# Feedback and Turnstile

## Role and current state

Public contact, authenticated contextual reports, PostgreSQL-backed rate limiting, and Cloudflare Turnstile verification are adoption-in-progress. They exist on coordinated open API/web branches and are not established as production-enabled.

`mosaify-web` owns the form, accessibility, challenge widget, and user intent. `mosaify-api` owns validation, trusted proxy handling, rate limits, Turnstile verification, persistence, and optional email notification. A report must be persisted before notification; notification failure must not erase accepted feedback.

## Data boundary

The system may process contact details and feedback text intentionally submitted by the user, plus the minimal authenticated context allowed by the report contract. Turnstile receives a short-lived challenge token and verification context, not the feedback body.

Never accept or encourage credentials, authentication tokens, payment data, private keys, unnecessary prompts or media, or sensitive incident evidence in ordinary feedback. Never copy feedback text, email addresses, IP addresses, Turnstile tokens, private links, or report bodies into PostHog or Sentry.

Configuration names are `SUPPORT_INBOX_EMAIL`, `TURNSTILE_SECRET_KEY`, `TRUST_PROXY`, and `VITE_TURNSTILE_SITE_KEY`.

## Retention and abuse controls

The proposed first-party feedback retention target is 12 months; counsel and production configuration must confirm it before rollout. Keep only the minimum rate-limit and abuse evidence needed for the control. Do not publish the support destination or provider dashboard.

## Rollout and rollback

1. Confirm privacy copy and report categories with counsel.
2. Apply additive feedback/rate-limit schema changes and deploy the API before the web form.
3. Canary anonymous and authenticated submission, invalid/expired challenge, proxy parsing, rate-limit boundaries, persistence, notification failure, and accessibility.
4. Verify that feedback and challenge data do not enter analytics or error payloads.

Rollback by hiding/disabling submission entry points and rejecting new writes while retaining already-accepted records according to policy. Turnstile failure should fail closed for the protected public submission path, not degrade unrelated authenticated product access. Alert on sustained verification failures, rate-limit anomalies, persistence failures, and notification backlog without including report contents.
