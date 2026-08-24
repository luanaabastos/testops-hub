# TestOps Hub — public evidence index

Only public project links are listed here. No credentials, environment values, or private resources are required to review the evidence.

## Project

- [Live Demo](https://qualityops-hub.onrender.com)
- [GitHub repository](https://github.com/luanaabastos/testops-hub)
- [Platform CI workflow](https://github.com/luanaabastos/testops-hub/actions/workflows/platform.yml)
- [Verified Platform CI run](https://github.com/luanaabastos/testops-hub/actions/runs/32546395494)
- [Published historical v1.0.0 release](https://github.com/luanaabastos/testops-hub/releases/tag/v1.0.0)

## Real browser workflows and reports

| Scenario | Workflow | Retained report artifact | Normalized execution |
|---|---|---|---|
| ShopSphere SUCCESS — Cypress, 5/5 passed | [Run 32431118788](https://github.com/luanaabastos/testops-hub/actions/runs/32431118788) | [Mochawesome artifact](https://github.com/luanaabastos/testops-hub/actions/runs/32431118788/artifacts/9429101193) | [Dashboard execution](https://qualityops-hub.onrender.com/executions/a8a65b5d-17b2-4714-b3c1-d2192b945963) |
| ServiceDesk SUCCESS — Playwright, 5/5 passed | [Run 32431321053](https://github.com/luanaabastos/testops-hub/actions/runs/32431321053) | [Playwright artifact](https://github.com/luanaabastos/testops-hub/actions/runs/32431321053/artifacts/9429173727) | [Dashboard execution](https://qualityops-hub.onrender.com/executions/6899dec4-d7d6-4fe9-ba89-7edf30b88d1c) |
| ShopSphere FUNCTIONAL_FAILURE — Cypress, 4/5 passed | [Expected failed run 32431559619](https://github.com/luanaabastos/testops-hub/actions/runs/32431559619) | [Mochawesome artifact](https://github.com/luanaabastos/testops-hub/actions/runs/32431559619/artifacts/9429251422) | [Execution with Regression Delta](https://qualityops-hub.onrender.com/executions/af12fdee-6860-4916-a35c-9fce60022556) |

The functional-failure workflow retains and ingests its report before ending red. Its dashboard execution compares against the successful ShopSphere run and shows **1 new failure**.

## Architecture and contracts

- [Architecture](https://github.com/luanaabastos/testops-hub/blob/main/docs/architecture.md)
- [Versioned report adapters](https://github.com/luanaabastos/testops-hub/blob/main/docs/adapters.md)
- [Test report contract](https://github.com/luanaabastos/testops-hub/blob/main/docs/test-report-contract.md)
- [GitHub Actions ingestion](https://github.com/luanaabastos/testops-hub/blob/main/docs/github-actions.md)
- [Hosting boundaries](https://github.com/luanaabastos/testops-hub/blob/main/docs/hosting.md)
- [Security design](https://github.com/luanaabastos/testops-hub/blob/main/docs/security.md)
- [Technical case study](https://github.com/luanaabastos/testops-hub/blob/main/docs/portfolio/case-study.md)

GitHub Actions artifacts follow GitHub's retention policy and may expire independently of the repository documentation and persisted normalized executions.
