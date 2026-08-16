# Access and secrets

## Principles

- Grant the least privilege needed for a person's role and current responsibility.
- Prefer organization-owned accounts over personal accounts.
- Require multi-factor authentication wherever supported.
- Keep production and development access separate where the provider supports it.
- Review access after role changes, offboarding, suspected compromise, and at a regular cadence.
- Give every credential a named owner, purpose, scope, storage location, and rotation expectation.

## What belongs in Git

Safe public documentation includes vendor names, configuration variable names, data boundaries, and rollback principles.

Never publish passwords, API keys, OAuth tokens, private keys, recovery codes, webhook secrets, copied environment files, session cookies, authenticated URLs, customer identifiers, prompts, media, production payloads, account names, secret-manager references, or screenshots exposing private data.

Client-visible ingestion identifiers are not authentication credentials, but they should still be configured through the normal environment contract rather than copied casually through documentation.

## Rotation response

When a credential is exposed or suspected exposed:

1. revoke or rotate it at the provider;
2. update the approved secret store and deployment reference;
3. invalidate sessions or derived credentials where applicable;
4. inspect sanitized audit logs for misuse;
5. verify recovery with a narrow canary; and
6. start an incident if production, private data, billing, or provider spend may have been affected.
