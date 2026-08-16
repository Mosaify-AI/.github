# Data and media

## Role and current state

`mosaify-api` actively uses PostgreSQL for authoritative relational state and an S3-compatible adapter for durable media. The production vendors, regions, backup systems, and configured retention policies are not established by public repository evidence.

`mosaify-workspace` runs PostgreSQL 16 and MinIO locally through Docker Compose. MinIO is development-only and must not be described as the production storage provider.

## Ownership and data boundary

PostgreSQL may store identities, sessions, workspaces, projects, scenes, render jobs, media metadata, provider-job state, credits, idempotency records, and billing state. Consent and feedback records join that boundary only when the adoption-in-progress implementation is deployed.

S3-compatible storage may contain intentional uploads, generated media, thumbnails, and other product-owned media artifacts. Provider result URLs are transient inputs to ingestion, not durable delivery. Credentials, raw card data, arbitrary telemetry payloads, and unrelated provider responses are prohibited. Biometric identification and biometric-profile storage are outside the current compatibility-routing contract.

Configuration names are `DATABASE_URL`, `TEST_DATABASE_URL`, `MEDIA_STORAGE_ENDPOINT`, `MEDIA_STORAGE_REGION`, `MEDIA_STORAGE_BUCKET`, `MEDIA_STORAGE_ACCESS_KEY_ID`, `MEDIA_STORAGE_SECRET_ACCESS_KEY`, `MEDIA_STORAGE_FORCE_PATH_STYLE`, and the local-reset guard `MOSAIFY_ALLOW_DEVELOPMENT_RESET`.

## Production boundary

- Use separate development/test and production databases, buckets, credentials, and endpoints.
- Never run `dev:reset` against a non-local endpoint. The checked-in guard permits only local database and media targets.
- Serve media through authenticated first-party routes or appropriately short-lived signed URLs.
- Keep database rows and media objects reconcilable; a provider success is not complete until durable ingestion succeeds.
- Document production vendor, region, encryption, backup, restore, lifecycle, deletion, and access-control settings only after they are confirmed. Private account and dashboard references belong in the restricted supplement.

## Retention, recovery, and canaries

Retention follows the product record's purpose and deletion contract; no blanket production duration is asserted here. Feedback and consent targets are defined in their own rollout runbooks. Generated media must not be silently expired while first-party metadata still promises availability.

Before a production change, test migration compatibility, create/read/delete a synthetic record, upload/read/delete a synthetic media object, and verify authorization through the application route. Roll back application code independently where schema compatibility permits; use additive migrations and restore drills for data recovery. A database or storage alarm must identify the owning environment without including customer content or private URLs.
