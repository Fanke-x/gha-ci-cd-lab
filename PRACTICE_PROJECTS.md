# Practice Projects

Each project lists goals, steps, and acceptance criteria.

1) Node CI with matrix, cache, artifacts
- Goals: matrix across OS + Node versions; npm cache; test artifact
- Steps: modify src/node-app; open PR; read matrix logs
- Accept: All matrix jobs pass; coverage artifact uploaded

2) Python CI with cache and artifacts
- Goals: run pytest across Python versions; cache pip
- Steps: modify src/python-app; open PR
- Accept: Tests pass on all versions; JUnit/coverage artifact uploaded

3) Docker build and publish to GHCR
- Goals: build image from infra/docker/Dockerfile and push to ghcr.io
- Steps: run docker-ghcr via workflow_dispatch; tag latest + sha
- Accept: Image appears under Packages in repo

4) Reusable workflow library
- Goals: Call reusable.yml from caller.yml with inputs
- Steps: dispatch caller.yml; pass path to run tests
- Accept: Reusable workflow executes with input

5) Container job with Postgres service
- Goals: spin up service container and connect from app container
- Steps: run container-and-services.yml
- Accept: Healthcheck passes; psql query succeeds

6) Protected production deployment
- Goals: require approval before deploy job runs
- Steps: configure environment “production” with reviewer; run docker-ghcr deploy path
- Accept: Job waits for approval; after approval deploy step runs

7) Code scanning + Dependabot
- Goals: enable CodeQL workflow; review alerts; open Dependabot PR
- Steps: push code; wait for scans; manually run CodeQL once if needed
- Accept: At least one CodeQL run; Dependabot PR created

8) GitHub Pages Deploy
- Goals: deploy static site/site to Pages
- Steps: run pages.yml
- Accept: Pages site becomes available under repo’s Pages URL