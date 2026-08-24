# Lançamento no LinkedIn — PT-BR

Resultados de testes automatizados costumam ficar espalhados entre pipelines, logs, artifacts e relatórios de frameworks diferentes. Quando algo falha, entender o contexto e comparar com a execução anterior exige abrir várias fontes.

Criei o **TestOps Hub** para explorar esse problema: uma plataforma de portfólio que transforma execuções de CI em histórico rastreável, métricas de qualidade e sinais de regressão.

O fluxo é real:

GitHub Actions → Cypress / Playwright → reports → API de ingestão autenticada → normalização → PostgreSQL → dashboard.

A evidência pública inclui:

- ShopSphere SUCCESS: 5/5 testes aprovados;
- ServiceDesk SUCCESS: 5/5 testes aprovados;
- ShopSphere FUNCTIONAL_FAILURE: 4/5 aprovados e 1 falha funcional;
- Regression Delta: 1 nova falha detectada.

Em vez de reconciliar manualmente pipelines, artifacts e reports para esses cenários, a plataforma reúne origem, framework, branch, commit, resultado, diagnóstico e comparação em uma visão consolidada.

Stack: TypeScript, React, Fastify, Cypress, Playwright, PostgreSQL/Neon, Render, Docker e GitHub Actions.

Live Demo: https://qualityops-hub.onrender.com<br>
Repositório e evidências: https://github.com/luanaabastos/testops-hub

Todos os produtos, testes e dados apresentados são fictícios e sintéticos. As execuções de browser, reports, ingestão e persistência demonstradas são evidências técnicas reais do projeto.

#QualityEngineering #TestAutomation #TestOps #SDET #CICD #Playwright #Cypress
