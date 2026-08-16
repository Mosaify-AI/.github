# BytePlus ModelArk

## Role and current state

BytePlus ModelArk is an active alternate direct Seedance video-provider path in `mosaify-api`, selected with `VIDEO_PROVIDER=seedance`. The default checked-in provider choice remains fal, and current production use of the direct BytePlus path is unconfirmed.

## Data boundary

The API may send the requested prompt, supported generation settings, and selected reference image/video/audio URLs needed for a job. It may process provider task state and result URLs long enough to reconcile and ingest the result. Never send Mosaify credentials, authentication/billing records, unrelated customer records, or provider task payloads to analytics/error monitoring.

Configuration names are `VIDEO_PROVIDER`, `ARK_API_KEY`, `SEEDANCE_BASE_URL`, and `SEEDANCE_VIDEO_MODEL`.

## Rollout and rollback

Validate account access, model identifier, reference compatibility, duration/aspect-ratio handling, output decoding, timeout behavior, and estimated cost with a controlled paid canary. Enable the path for a narrow cohort or operator-controlled job before changing the general default. A job is complete only after first-party persistence and durable media ingestion.

Roll back by restoring `VIDEO_PROVIDER=fal` or the previously validated model, while continuing to reconcile already-submitted BytePlus tasks. Retries must remain idempotent and credit reservations must not double-charge.

Provider retention, regional processing, alert configuration, and production account enablement are unconfirmed. Record confirmed private settings only in the restricted supplement. Public alerts should contain sanitized first-party job IDs, not prompts, reference URLs, or provider payloads.
