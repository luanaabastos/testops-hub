# TestOps Hub — interview talk track

Respostas em primeira pessoa, pensadas como guias de 30–60 segundos. Devem soar naturais; não precisam ser memorizadas literalmente.

## “O que é o TestOps Hub?”

TestOps Hub é uma plataforma TestOps de portfólio que transforma relatórios de testes gerados na CI em histórico, métricas e sinais de regressão. Cypress e Playwright rodam em browsers reais no GitHub Actions, os reports são enviados para uma API autenticada, adapters convertem formatos diferentes para um modelo comum e o PostgreSQL persiste as execuções. O dashboard mostra tanto o resultado quanto a origem da evidência. Todos os produtos e dados são fictícios, mas o fluxo técnico demonstrado é real.

## “Qual problema você quis resolver?”

Eu quis explorar a fragmentação da evidência de testes. O status fica no CI, o detalhe no report, o arquivo em um artifact, o contexto em logs e a comparação depende de execuções anteriores. Para QA, um job vermelho isolado não diz se a falha é funcional, de infraestrutura, nova ou persistente. A proposta foi reunir esses elementos em um histórico rastreável, mantendo links para a fonte e sem apagar as diferenças entre os frameworks.

## “Por que não simplesmente olhar o GitHub Actions?”

GitHub Actions é a fonte de execução e continua sendo parte essencial da rastreabilidade. O que ele não oferece neste projeto é um modelo unificado entre frameworks nem uma visão de produto que compare execuções equivalentes. No TestOps Hub eu consigo ver Cypress e Playwright com as mesmas semânticas de contagem, separar falha funcional de erro de infraestrutura e calcular Regression Delta. Cada tela ainda aponta para workflow, artifact, branch e commit, então a plataforma complementa o CI em vez de substituí-lo.

## “Por que normalizar reports?”

Mochawesome e Playwright JSON representam suites, testes, estados, duração e erros de formas diferentes. Se o dashboard entendesse cada formato diretamente, parsing, métricas e interface ficariam acoplados. Usei adapters versionados na borda: cada um valida e interpreta seu formato, depois devolve uma execução normalizada. Assim, o domínio calcula histórico e regressão de forma consistente, enquanto framework e formato originais continuam registrados para auditoria.

## “Como Cypress e Playwright convivem?”

Eles compartilham o contrato de ingestão, não o report bruto. ShopSphere roda Cypress e gera Mochawesome; ServiceDesk roda Playwright e gera o JSON versionado do projeto. Em ambos os workflows, o browser roda primeiro, o artifact é preservado e o envelope autenticado é enviado à API. O adapter correto produz o mesmo modelo de execução. Isso permite métricas comparáveis sem fingir que os frameworks geram a mesma estrutura ou têm o mesmo runner.

## “O que é Regression Delta?”

Regression Delta compara a execução atual com a execução anterior comparável do mesmo produto e fonte de evidência. Em vez de olhar apenas o total de falhas, ele associa identidades de testes e classifica mudanças: novas falhas, recuperados, falhas persistentes, testes novos e removidos. Na prova pública, ShopSphere passou de 5/5 para 4/5; o dashboard detectou uma nova falha. Isso traz para a interface a mudança que normalmente exigiria comparar dois reports manualmente.

## “Como você diferencia dado real e demo?”

Eu modelei origem e evidência explicitamente. Official CI significa browser real no GitHub Actions com ingestão autenticada e origem `EXTERNAL_CI`; somente esse grupo entra nas métricas oficiais. Demo Data é histórico sintético para explicar a interface. Local Demo existe para desenvolvimento. Hosted Preview mostra as etapas do fluxo, mas não abre browser, não cria execução e não altera métricas. PocketWallet também é rotulado como Mobile Harness Demo, nunca como teste real de Android.

## “Por que os browsers não rodam no Render?”

Foi uma decisão de arquitetura compatível com o escopo e o plano gratuito. O Render serve bem a aplicação React e a API Fastify, mas eu não quis representar esse serviço como um worker de browser. GitHub Actions já oferece um ambiente reproduzível, logs públicos e artifacts para Cypress e Playwright. Assim, o browser roda no CI externo, o report é ingerido no Render e o histórico fica no Neon. O Pipeline Lab hospedado permanece uma prévia segura e claramente rotulada.

## “Como você tratou segurança?”

A ingestão usa tokens por produto e o banco armazena somente hashes com salt usando scrypt. O corpo tem limite, o schema é validado e as queries são parametrizadas dentro de transações. Diagnósticos são sanitizados antes da persistência. Reenvio idêntico é idempotente e conteúdo conflitante na mesma identidade recebe HTTP 409. No Pipeline Lab, o usuário escolhe enums mapeados para runners fixos; não há construção de comandos, URLs ou paths. Também mantenho scans para secrets, histórico, paths, assets, identidade Git e referências públicas.

## “O que faria numa versão empresarial?”

Eu começaria por identidade e isolamento: autenticação de usuários, RBAC, multi-tenancy e trilha de auditoria. Depois moveria relatórios brutos para object storage com retenção, usaria uma fila distribuída com workers recuperáveis e rate limiting compartilhado. Também acrescentaria observabilidade, backup e restauração testados, SLOs e uma política de migração. Flaky Test Radar e integrações adicionais viriam depois que a governança da evidência estivesse definida. Nada disso é apresentado como funcionalidade atual.

## “Qual foi o maior desafio técnico?”

O maior desafio foi preservar a fronteira entre demonstração e evidência. Eu precisava de dados suficientes para explicar a interface, mas seed e preview não poderiam alterar métricas oficiais. Ao mesmo tempo, um workflow com falha funcional precisava guardar o report e ingeri-lo antes de terminar vermelho. A solução combinou origem explícita, filtro de evidência oficial e ordem controlada no workflow. Isso permitiu demonstrar uma regressão real sem transformar preview em prova.

## “O que você aprendeu?”

Aprendi que um dashboard de qualidade só é confiável quando identidade, origem, semântica de erro e rastreabilidade são definidas antes dos gráficos. Também vi na prática como adapters reduzem o acoplamento entre frameworks e domínio, e como idempotência precisa fazer parte do desenho de uma API consumida por CI. Por fim, as limitações de hosting ajudaram a separar responsabilidades: browser no GitHub Actions, aplicação no Render, persistência no Neon e preview sem evidência oficial.
