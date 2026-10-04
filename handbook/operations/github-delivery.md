# GitHub delivery

## Role and current state

GitHub is active for source control, pull-request review, CI checks, releases, and the public organization profile. Jira is the authoritative planning, backlog, and work-tracking system; GitHub Issues and organization Projects are disabled.

CI is owned by `mosaify-workspace`, `mosaify-studio`, `mosaify-platform`, `mosaify-cinema`, `mosaify-skills`, `mosaify-cli`, and active `Ava`. Studio checks and deploys its API, web, and MCP from one repository; Platform deploys its company and Accounts frontends. The public `.github` repository contains handbook and organization-profile content.

The retired standalone API, web, and MCP repositories are not deployment owners. Their deployment workflows are disabled. Current workflows check out Studio or Platform, use immutable container images or direct Cloudflare Pages uploads, and retain cloud resource identities independently of the source repository names. Source-repository deletion must never remove ECR images, ECS services, Pages projects, databases, media, runtime secrets, or retained rollback artifacts.

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
