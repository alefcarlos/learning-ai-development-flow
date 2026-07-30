---
id: TASK-004
title: 'ADR: Tech Stack'
status: To Do
assignee: []
created_date: '2026-07-30 01:44'
updated_date: '2026-07-30 01:57'
labels:
  - documentacao arquitetura adr
dependencies: []
priority: high
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Registrar ADR documentando a escolha de cada tecnologia do stack.

### Decisoes

| Tecnologia | Justificativa |
|------------|---------------|
| .NET 8+ LTS | Ecossistema maduro, performance, requisito do desafio |
| ASP.NET Core | Framework web padrao para APIs REST |
| PostgreSQL | Robusto, relacional, otimo para dados financeiros |
| EF Core | ORM maduro, migrations, LINQ |
| RabbitMQ | Mensageria madura, suporte .NET, facil setup Docker |
| xUnit + MTP | Testes modernos com Aspire testing integration |
| Keycloak | SSO open source, suporte OIDC/OAuth2 |
| Aspire | Observabilidade, health checks, orquestracao dev |
| Terraform | Infrastructure as Code para Keycloak |

### Passos para executar:
1. Para cada tecnologia, documentar: nome, versao, proposito
2. Justificar cada escolha contra alternativas
3. Registrar implicacoes (licenciamento, custo, curva de aprendizado)
4. Salvar como docs/adr/002-tech-stack.md
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Salvo como docs/adr/002-tech-stack.md
- [ ] #2 Todas as tecnologias listadas com versoes
- [ ] #3 Justificativas contra alternativas registradas
- [ ] #4 Implicacoes documentadas
<!-- AC:END -->

## Implementation Plan

<!-- SECTION:PLAN:BEGIN -->
$1. Criar docs/adr/002-tech-stack.md\n2. Listar cada tecnologia com versão e propósito\n3. Para cada uma, justificar contra alternativas\n4. Documentar implicações
<!-- SECTION:PLAN:END -->
