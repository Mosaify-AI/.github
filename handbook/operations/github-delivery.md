# GitHub delivery

## Role and current state

GitHub is active for source control, pull-request review, issues, the organization Delivery project, CI checks, and the public organization profile. GitHub Actions is not currently a production deployment system: no checked-in production deployment workflow or provider-specific manifest was found.

CI exists in `mosaify-workspace`, `mosaify-api`, `mosaify-web`, `mosaify-cli`, and archived `Ava`. `mosaify-mcp` and the public `.github` repository have no workflow checks.

## Data boundary

Repository code, pull-request discussion, issue metadata, test results, and sanitized CI logs may be processed according to repository visibility. Do not put credentials, private environment files, customer data, prompts, private media URLs, authenticated dashboard URLs, copied production payloads, or private incident evidence in GitHub content or logs.

## Delivery controls

- Keep each repository's branch, commit, check, and release lifecycle independent.
- Require repository-local checks before publishing and verify remote checks to a terminal result.
- Use pinned action revisions where elevated permissions are required; otherwise prefer stable official actions with least privilege.
- Treat forked or third-party pull requests as untrusted input and do not expose write credentials to them.
- The Delivery board automation may read issues and update organization-project status only.
- `MOSAIC_PROJECT_AUTOMATION_APP_ID` and `MOSAIC_PROJECT_AUTOMATION_PRIVATE_KEY` are deprecated naming retained solely for credential compatibility. Rename them only through a coordinated credential rotation; never duplicate their values into public docs.

## Rollout, rollback, and alerting

Canary workflow changes with `workflow_dispatch` or a narrow pull request before relying on them broadly. Roll back a faulty check by reverting the workflow change. Contain a compromised automation path by disabling the workflow and revoking or rotating the GitHub App credential. Failed required checks remain visible in the pull request; the owning engineer is responsible for triage. Private alert destinations belong in the restricted supplement.

Git history is durable and difficult to purge completely. If a secret is committed, rotate it immediately even if the commit is later removed.
