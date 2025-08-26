# Study Guide: GitHub Actions CI/CD (From Zero to Pro)

Learning approach:
- Learn concepts, then immediately run the corresponding workflow in this repo.
- Use the Actions tab to read logs; modify a workflow and re-run to see the effect.

1) Core concepts (1–2 hours)
- Workflow structure: on, jobs, steps, runs-on
- Runners and runner images (hosted vs self-hosted)
- Actions vs shell steps
- Contexts: github, job, steps, runner, matrix, secrets, env, inputs
- Expressions: ${{ ... }}, if:, contains, startsWith
Hands-on:
- Open .github/workflows/ci-node.yml and ci-python.yml
- Push a branch; open a PR; watch both run

2) Environment variables and secrets (1 hour)
- env at workflow/job/step precedence
- Passing env to steps
- Masking secrets; never echo raw secrets
- Repository variables vs environment variables vs default env
Hands-on:
- Edit ci-node.yml env values; print them in steps
- Add a repo secret API_KEY; consume it in a step (don’t echo it)
Docs:
- https://docs.github.com/actions/learn-github-actions/variables
- https://docs.github.com/actions/security-guides/using-secrets-in-github-actions

3) Job orchestration and control (1–2 hours)
- needs: controlling order
- Job outputs; passing data between jobs
- Conditionals: if:, success(), failure(), cancelled(), always()
- concurrency to avoid overlapping runs
- strategy: matrix, fail-fast, include/exclude
Hands-on:
- Explore ci-node.yml and conditional-and-matrix examples inside it
- Purposefully break tests to see fail-fast behavior
Docs:
- https://docs.github.com/actions/using-jobs/using-concurrency
- https://docs.github.com/actions/using-jobs/using-jobs-in-a-workflow

4) Caching, artifacts, and summaries (1 hour)
- actions/cache for dependencies
- upload-artifact/download-artifact for build outputs
- Job summaries (GITHUB_STEP_SUMMARY)
Hands-on:
- See caches in ci-node.yml / ci-python.yml
- Upload coverage and view in run’s artifacts
Docs:
- https://docs.github.com/actions/using-workflows/caching-dependencies
- https://docs.github.com/actions/using-workflows/storing-workflow-data-as-artifacts

5) Containers and services (1–2 hours)
- Running a job inside a container (jobs.<id>.container)
- Service containers (databases, queues), health checks, ports
Hands-on:
- Run container-and-services.yml; connect to Postgres service
Docs:
- https://docs.github.com/actions/using-jobs/running-jobs-in-a-container
- https://docs.github.com/actions/using-containerized-services

6) Building and publishing images (1–2 hours)
- docker/login-action + build-push-action
- Using GITHUB_TOKEN for GHCR (packages: write)
- Tagging strategies
Hands-on:
- Trigger docker-ghcr.yml via workflow_dispatch or tags
Docs:
- https://docs.github.com/packages/working-with-a-github-packages-registry/working-with-the-container-registry
- https://github.com/docker/build-push-action

7) Deployments and environments (1–2 hours)
- environments with reviewers/approvals and environment-scoped secrets/vars
- Using environment: staging/production
- Promotion from staging to prod (workflow_run or manual)
Hands-on:
- Configure environment “production” with required reviewers
- Run docker-ghcr.yml deploy job that targets production
Docs:
- https://docs.github.com/actions/deployment/targeting-different-environments/using-environments-for-deployment

8) Reusable workflows and composite actions (1 hour)
- workflow_call inputs/outputs/secrets
- .github/actions composite actions to share logic
Hands-on:
- Inspect reusable.yml and caller.yml
- See .github/actions/setup-python composite
Docs:
- https://docs.github.com/actions/using-workflows/reusing-workflows
- https://docs.github.com/actions/creating-actions/creating-a-composite-action

9) Security best practices (ongoing)
- Least-privilege permissions: permissions: block at workflow
- Pin actions to SHAs (not just v4) in production
- OIDC (id-token: write) for cloud deploys; avoid long-lived cloud keys
- Protect main with required PR reviews + required status checks
- Dependabot for actions/npm/pip; CodeQL for code scanning
Hands-on:
- Review permissions in workflows
- Enable Code scanning alerts; Dependabot updates
Docs:
- https://docs.github.com/actions/security-guides/security-hardening-for-github-actions
- https://docs.github.com/code-security/code-scanning

10) Troubleshooting and debugging
- Add actions/setup-node/python with detailed logs
- Use run: env to print env keys (avoid secrets)
- Use step timeouts and continue-on-error for experiments
- Re-run failed jobs; enable debug logging via repository secrets ACTIONS_STEP_DEBUG=true
Docs:
- https://docs.github.com/actions/monitoring-and-troubleshooting-workflows/enabling-debug-logging