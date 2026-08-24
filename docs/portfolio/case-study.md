# TestOps Hub — technical portfolio case study

## The problem

Automated-test evidence is commonly split across CI conclusions, framework reports, retained artifacts, logs, and historical runs. Each source answers only part of the investigation: a red job does not explain whether the cause was functional or infrastructural, and a standalone report does not show whether a failure is new, persistent, or recovered.

This matters to QA and Quality Engineering because trustworthy decisions depend on context. A team needs to know what ran, where the evidence came from, how it compares with the previous equivalent execution, and whether the result belongs in official metrics. Reconstructing that context manually across tools adds analysis steps and makes different frameworks harder to compare.

## The solution

TestOps Hub is an open-source portfolio platform that turns CI test reports into a normalized, traceable execution history. It receives product-authenticated reports, validates their contracts, converts framework-specific structures into one domain model, persists the result, and presents quality metrics, execution details, and regression signals in a React dashboard.

All products, users, tests, executions, and planning data are fictional and synthetic. The public GitHub Actions workflows, browser sessions, generated reports, authenticated ingestion, and PostgreSQL persistence are real technical evidence created for this portfolio project.

## Architecture

```text
GitHub Actions
→ Cypress / Playwright in real browsers
→ retained Mochawesome / Playwright JSON report
→ authenticated Fastify ingestion API on Render
→ versioned adapter and normalized execution
→ Neon PostgreSQL
→ React dashboard on Render
```

Browser automation runs in GitHub Actions. Render serves the application and API from one origin, while Neon provides managed PostgreSQL persistence. This keeps browser-heavy execution outside the hosted free-tier service and makes the workflow run and artifact independently inspectable.

## Cypress and Playwright in the same flow

ShopSphere uses Cypress and produces Mochawesome. ServiceDesk uses Playwright and produces the project's versioned Playwright JSON contract. Both workflows run real browser tests, retain the raw framework report as a GitHub Actions artifact, and then send an authenticated envelope to the same ingestion endpoint.

The workflow does not hide a functional failure. In the ShopSphere failure scenario, it preserves and ingests the report before propagating the failed test result and ending the job red.

## Report normalization

The API validates the envelope and selects an adapter by report format and version. Adapters understand framework-specific nesting, states, durations, and error fields, then return the same normalized structure: product, pipeline metadata, suites, test cases, counts, duration, outcome, and sanitized diagnostics.

This boundary lets Cypress/Mochawesome and Playwright results be compared without presenting them as identical raw formats. Traceability back to the original workflow, job, artifact, branch, commit, framework, and format remains attached to each execution.

## Persistence and delivery safety

The normalized execution graph is written transactionally to PostgreSQL. Product-scoped integration tokens authenticate ingestion and are stored only as salted scrypt hashes. A stable execution identity and content hash make retries deterministic: an identical replay returns the existing execution, while different content submitted for the same identity receives HTTP 409.

Only authenticated `GITHUB_ACTIONS` executions with `EXTERNAL_CI` origin contribute to official aggregates. Synthetic seed data, local demo runs, and Hosted Preview remain explicitly labeled and cannot replace or inflate official evidence.

## Regression Delta

Regression Delta compares an execution with the previous comparable execution for the same product and evidence source. Test identities are matched and classified as new failures, recovered tests, persistent failures, new tests, or removed tests.

The public ShopSphere proof moves from 5/5 passed to 4/5 passed with one functional failure. The dashboard identifies that change as **1 new failure**, rather than showing only two unrelated totals.

## Public proof

| Scenario | Framework | Executed | Passed | Failed | Result |
|---|---|---:|---:|---:|---|
| ShopSphere success | Cypress / Mochawesome | 5 | 5 | 0 | Passed |
| ServiceDesk success | Playwright / JSON | 5 | 5 | 0 | Passed |
| ShopSphere functional failure | Cypress / Mochawesome | 5 | 4 | 1 | Expected failed workflow |

The latest official result per external-CI product produces an aggregate of 10 executed, 9 passed, 1 failed, 0 infrastructure errors, a 90% Approval Rate, and a 90% Quality Score. The evidence is linked in the [public evidence index](evidence-index.md).

## How it supports analysis

TestOps Hub consolidates outcome, framework, origin, branch, commit, report link, test-level diagnostics, and regression comparison in one navigation path. This removes the need to manually reconcile those fields across several pipeline pages for the demonstrated scenarios. The project does not claim a measured time reduction; it demonstrates a smaller and more explicit investigation surface.

## Technical decisions

- **Versioned adapters** isolate parsing changes from HTTP routes and domain metrics.
- **One normalized execution model** supports comparison while retaining raw-format provenance.
- **Functional failures and infrastructure errors** remain separate quality semantics.
- **External browser CI** provides real browser evidence without requiring browser workers on Render.
- **Official-origin filtering** prevents preview or seeded data from affecting public metrics.
- **Transactional idempotent ingestion** handles normal CI retries without duplicating history.
- **Fixed, allow-listed Pipeline Lab inputs** avoid constructing commands, URLs, or paths from visitor input.
- **Stable internal identifiers** avoid an unnecessary migration after the public product and repository rename.

## Limitations

- PocketWallet is a deterministic Mobile Harness Demo, not an Android device or Appium run.
- Render Free can cold-start and has no availability commitment.
- Raw external-CI report retention depends on GitHub Actions; object storage is not enabled.
- There is no user authentication, role model, multi-tenancy, or tenant isolation.
- Background demo work uses an in-process queue without distributed recovery.
- Rate limiting is instance-local rather than distributed.
- Video Evidence is a labeled concept preview; recordings are not stored.
- Automation Coverage represents mapped fictional quality scenarios, not code coverage.

## What I learned

The main lesson was that useful quality reporting starts with evidence boundaries, not charts. Origin, identity, replay behavior, error semantics, and traceability need to be explicit before an aggregate can be trusted. The project also reinforced the value of keeping framework parsing at the edge: once results share a stable domain model, history and regression logic can remain independent of the runner that produced them.

Finally, hosting constraints can lead to a clearer architecture when they are visible. Separating external browser execution, hosted ingestion, durable persistence, and non-persisting preview behavior made the public demonstration more honest and auditable.

## Links

- [Live Demo](https://qualityops-hub.onrender.com)
- [GitHub repository](https://github.com/luanaabastos/testops-hub)
- [Architecture documentation](../architecture.md)
- [Public evidence index](evidence-index.md)
