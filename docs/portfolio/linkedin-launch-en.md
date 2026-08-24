# LinkedIn launch — English

Automated test results often end up scattered across pipelines, logs, artifacts, and framework-specific reports. When something fails, understanding the context and comparing it with the previous run means navigating several separate sources.

I built **TestOps Hub** to explore that problem: a portfolio platform that turns CI executions into traceable history, quality metrics, and regression signals.

The flow is real:

GitHub Actions → Cypress / Playwright → reports → authenticated ingestion API → normalization → PostgreSQL → dashboard.

The public evidence includes:

- ShopSphere SUCCESS: 5/5 tests passed;
- ServiceDesk SUCCESS: 5/5 tests passed;
- ShopSphere FUNCTIONAL_FAILURE: 4/5 passed and 1 functional failure;
- Regression Delta: 1 new failure detected.

For these scenarios, the platform brings origin, framework, branch, commit, outcome, diagnostics, and comparison into one view instead of requiring manual reconciliation across pipelines, artifacts, and reports.

Stack: TypeScript, React, Fastify, Cypress, Playwright, PostgreSQL/Neon, Render, Docker, and GitHub Actions.

Live Demo: https://qualityops-hub.onrender.com<br>
Repository and evidence: https://github.com/luanaabastos/testops-hub

Every product, test, and data point shown is fictional and synthetic. The demonstrated browser runs, reports, ingestion, and persistence are real technical evidence from the project.

#QualityEngineering #TestAutomation #TestOps #SDET #CICD #Playwright #Cypress
