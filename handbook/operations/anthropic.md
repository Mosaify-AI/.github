# Anthropic

## Role and current state

Anthropic is an active optional assistant path in the local `mosaify-cli` GUI when a user explicitly selects it. It is not a dependency of the browser application or `mosaify-api`, and no production deployment is evidenced. The local mock remains the CLI assistant default.

## Data and credential boundary

The local process may send the user's assistant message and the minimum direction/shot context needed for that request. Do not send fal credentials, unrelated local files, customer datasets, authentication or billing records, hidden background context, or Mosaify operational metadata. Keep the API key in the user's environment or ignored local `.env`; never copy it into project state, output, logs, or documentation.

Configuration names are `MOSAIFY_LLM_PROVIDER`, `ANTHROPIC_API_KEY`, `ANTHROPIC_BASE_URL`, `MOSAIFY_LLM_API_KEY`, `MOSAIFY_LLM_BASE_URL`, `MOSAIFY_LLM_MODEL`, and `MOSAIFY_LLM_MAX_TOKENS`.

## Cost, reliability, retention, and rollback

Canary with synthetic content and verify model selection, bounded output, timeout/error behavior, and the confirmation boundary before allowing any paid generation action. The assistant may prepare actions, but fal generation still requires explicit user confirmation.

Roll back by returning `MOSAIFY_LLM_PROVIDER` to the local mock or removing provider configuration. Provider-side retention/training settings and account alerting are unconfirmed; a local user must verify them before sending private material. Avoid automatic retries that can multiply cost, and keep provider errors free of request content.
