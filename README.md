# GitHub Actions CI/CD Lab

Hands-on repository to learn GitHub Actions by example:
- CI for Node.js and Python with matrices, caching, artifacts
- Environment variables at workflow, job, and step scope
- Secrets and environments (protected deployments)
- Job control: needs, outputs, conditionals, concurrency, strategy
- Containers and service containers (Postgres)
- Docker build and publish to GHCR
- Reusable workflows (workflow_call)
- Pages deployment, CodeQL, Dependabot

Start here:
1) Read STUDY_GUIDE.md
2) Try projects in PRACTICE_PROJECTS.md
3) Open Actions tab to watch runs on your forks/branches

Requirements:
- Fork or create this repo
- Optional: configure GitHub Environments (staging/production) under Settings > Environments for approval gates and env-scoped secrets/vars
- Optional: publish packages to GHCR (no PAT needed; uses GITHUB_TOKEN)

Secrets/Vars you can add (Settings > Secrets and variables):
- Repository secrets (example): API_KEY
- Environment secrets (example): PROD_API_URL on environment “production”
- Repository variables (example): EXAMPLE_VAR

Useful docs:
- Actions docs: https://docs.github.com/actions
- Contexts: https://docs.github.com/actions/learn-github-actions/contexts
- Expressions: https://docs.github.com/actions/learn-github-actions/expressions

---

Note: If this repo is private, GitHub Pages deployments won’t publish unless your plan allows it. You can still run the workflow to learn.