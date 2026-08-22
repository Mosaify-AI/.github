# GitHub delivery

## Role and current state

GitHub is active for source control, pull-request review, CI checks, releases, and the public organization profile. Jira is the authoritative planning, backlog, and work-tracking system; GitHub Issues and organization Projects are disabled.

CI exists in `mosaify-workspace`, `mosaify-api`, `mosaify-web`, `mosaify-cli`, and archived `Ava`. `mosaify-mcp` and the public `.github` repository have no workflow checks.

## Data boundary

Repository code, pull-request discussion, test results, and sanitized CI logs may be processed according to repository visibility. Do not put credentials, private environment files, customer data, prompts, private media URLs, authenticated dashboard URLs, copied production payloads, or private incident evidence in GitHub content or logs.

## Delivery controls

- Keep each repository's branch, commit, check, and release lifecycle independent.
- Require repository-local checks before publishing and verify remote checks to a terminal result.
- Use pinned action revisions where elevated permissions are required; otherwise prefer stable official actions with least privilege.
- Treat forked or third-party pull requests as untrusted input and do not expose write credentials to them.

## Rollout, rollback, and alerting

Canary workflow changes with `workflow_dispatch` or a narrow pull request before relying on them broadly. Roll back a faulty check by reverting the workflow change. Contain a compromised automation path by disabling the affected workflow and revoking or rotating its credential. Failed required checks remain visible in the pull request; the owning engineer is responsible for triage. Private alert destinations belong in the restricted supplement.

Git history is durable and difficult to purge completely. If a secret is committed, rotate it immediately even if the commit is later removed.
