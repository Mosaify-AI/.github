# OpenAI

## Role and current state

The OpenAI API is an active server-side integration for chat, title generation, image generation/editing, duration advice, and compatibility classification. `mosaify-cli` may also use an OpenAI or OpenAI-compatible assistant when a local user explicitly configures it. Production account and model enablement are unconfirmed.

## Data boundary

Send only the prompt, selected project context, generation settings, or selected image content needed for the requested operation. Credentials, unrelated project/customer records, authentication or billing data, private operational metadata, and full database records are prohibited.

Compatibility classification estimates provider suitability only. It must not identify a person, infer identity, build a biometric profile, or store biometric templates. Cache keys and decisions must remain versioned, minimized, and first-party.

Configuration names consumed by current source are `OPENAI_API_KEY`, `OPENAI_CHAT_MODEL`, `OPENAI_CHAT_MAX_OUTPUT_TOKENS`, `OPENAI_TITLE_MODEL`, `OPENAI_RESPONSES_URL`, `OPENAI_BASE_URL`, `OPENAI_IMAGE_MODEL`, `OPENAI_IMAGE_QUALITY`, `OPENAI_VIDEO_DURATION_MODEL`, `MOSAIFY_LLM_API_KEY`, and `MOSAIFY_LLM_BASE_URL`. Compatibility routing uses `HUMAN_LIKENESS_ROUTING_MODE`, `HUMAN_LIKENESS_ROUTING_POLICY_VERSION`, `HUMAN_LIKENESS_CLASSIFIER_MODEL`, `HUMAN_LIKENESS_IMAGE_MODEL`, `HUMAN_LIKENESS_VIDEO_MODEL`, `HUMAN_LIKENESS_COMPATIBLE_IMAGE_MODELS`, and `HUMAN_LIKENESS_COMPATIBLE_VIDEO_MODELS`. The CLI additionally uses `MOSAIFY_LLM_PROVIDER`, `MOSAIFY_LLM_MODEL`, and `MOSAIFY_LLM_MAX_TOKENS`.

## Reliability, cost, and rollout

- Validate model capability, request shape, output decoding, safety behavior, timeouts, and bounded output before switching defaults.
- Keep consequential routing server-authoritative and version both classifier and routing policy.
- Roll compatibility routing from `off` to `shadow`, review sanitized evidence, run a controlled provider canary, then move to `enforce`.
- Roll back routing to `shadow` or `off`; roll back model changes by restoring the prior configured model/endpoint.
- Use idempotency and credit reservations so retries cannot create uncontrolled paid duplication.
- Alert on sustained provider failures, invalid output, timeout rate, cost anomalies, and durable-ingestion failures using sanitized request/job identifiers only.

Provider-side retention and training controls for the production account are unconfirmed. Confirm them in the restricted operating record before production use; never copy account names or dashboard URLs here.
