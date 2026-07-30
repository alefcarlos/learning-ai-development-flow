---
id: TASK-003
title: 'ADR: Microservices + EDA'
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
Registrar ADR (Architecture Decision Record) documentando a decisao de usar microservices com Event-Driven Architecture.

### Contexto
- Desafio exige que servico de lancamentos nao fique indisponivel se o consolidador cair
- Picos de 50 req/s no consolidado com max 5% de perda
- Necessidade de escalar independentemente cada dominio

### Decisao
- Microservices: cada bounded context vira um servico independente
- EDA: comunicacao assincrona via RabbitMQ entre lancamentos e consolidacao

### Alternativas consideradas
- Modular Monolith: mais simples, mas nao atende requisito de escala independente
- SOA: muito pesado para o cenario

### Consequencias
- Res - Resiliencia: falha no consolidado nao afeta lancamentos
- Res - Escala independente por servico
- Res - Desacoplamento entre dominios
- Neg - Complexidade operacional (N servicos vs 1 monolito)
- Neg - Consistencia eventual

### Passos para executar:
1. Seguir template MADR (Michael Nygard)
2. Escrever contexto e drivers da decisao
3. Listar alternativas consideradas e seus trade-offs
4. Registrar consequencias positivas e negativas
5. Salvar como docs/adr/001-microservices-eda.md
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Salvo como docs/adr/001-microservices-eda.md
- [ ] #2 Contexto e drivers documentados
- [ ] #3 Alternativas consideradas (Modular Monolith, SOA)
- [ ] #4 Trade-offs e consequencias registrados
- [ ] #5 Template MADR seguido
<!-- AC:END -->

## Implementation Plan

<!-- SECTION:PLAN:BEGIN -->
$1. Criar diretorio docs/adr/\n2. Criar arquivo docs/adr/001-microservices-eda.md seguindo template MADR\n3. Preencher contexto, decisão, alternativas, consequências\n4. Revisar com o time
<!-- SECTION:PLAN:END -->
