# LinkedIn carousel plan

Five slides, one message per slide, with minimal copy over the existing screenshots.

## Slide 1 — TestOps Hub

**Headline:** Automated test results, in one place.<br>
**Support:** From CI test execution to actionable quality insights.<br>
**Visual:** [`overview.png`](../assets/overview.png), cropped to keep the product statement and official metrics visible.

## Slide 2 — The problem

**Headline:** Quality evidence is often scattered across different tools.<br>
**Visual:** A simple text flow using only `CI · Reports · Artifacts · Logs`. Do not add a fifth application screenshot; keep the problem legible and uncluttered.

## Slide 3 — The solution

**Headline:** Trace every execution from CI to the dashboard.<br>
**Flow:** GitHub Actions → Cypress / Playwright → TestOps Hub.<br>
**Visual:** [`executions.png`](../assets/executions.png), cropped around the three official CI rows while retaining framework, source, result, and evidence columns.

## Slide 4 — Regression evidence

**Headline:** Detect the change, not only the red status.<br>
**Copy:** Previous: 5/5 passed · Current: 4/5 passed · Detected: 1 new failure.<br>
**Visual:** [`regression-delta.png`](../assets/regression-delta.png), emphasizing the execution summary and Regression Delta. Avoid enlarging diagnostic text unnecessarily.

## Slide 5 — Explore the project

**Headline:** See the complete evidence flow.<br>
**Visual:** [`pipeline-lab.png`](../assets/pipeline-lab.png), keeping the Hosted Preview and Official CI boundary visible.<br>
**Links:** `qualityops-hub.onrender.com` · `github.com/luanaabastos/testops-hub`<br>
**Footer:** Portfolio project · fictional and synthetic data.

## Selected screenshots

1. **Overview** — strongest opening; explains the product and shows official metrics.
2. **Executions** — strongest traceability view; shows frameworks, GitHub Actions, results, and evidence labels.
3. **Regression Delta** — strongest technical proof; connects 5/5 to 4/5 and 1 new failure.
4. **Pipeline Lab** — strongest boundary explanation; makes clear that Hosted Preview is not Official CI.

Automation Coverage and Integrations remain optional supporting images. The six reviewed screenshots contain no terminal, editor, personal path, notification, raw token, or credential.
