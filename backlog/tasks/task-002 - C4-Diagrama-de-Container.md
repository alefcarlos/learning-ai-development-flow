---
id: TASK-002
title: C4 - Diagrama de Container
status: To Do
assignee: []
created_date: '2026-07-30 01:44'
updated_date: '2026-07-30 01:57'
labels:
  - documentacao arquitetura
dependencies: []
priority: high
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Criar diagrama C4 de Container (nivel 2) decompondo o CashFlow System em 3 microservices + infraestrutura.

### Containers:
- **CashFlow.Service.Transactions** - WebApi (ASP.NET Core) - CRUD + eventos
- **CashFlow.Service.Consolidated** - WebApi (ASP.NET Core) - consulta saldo
- **CashFlow.Worker.Consolidation** - Worker (.NET) - consumer RabbitMQ
- **RabbitMQ** - Message Broker
- **PostgreSQL (TransactionsDB)** - Banco transacional
- **PostgreSQL (ConsolidatedDB)** - Banco de consolidacao
- **Keycloak** - Identity Provider

### Passos para executar:
1. Listar todos os containers com tecnologias e responsabilidades
2. Mapear protocolos de comunicacao entre containers
3. Desenhar relacionamentos entre containers
4. Validar alinhamento com requisitos NF (resiliencia, escala)
5. Salvar como docs/c4/container-diagram.md

### Implementacao

```mermaid
C4Container
  title Diagrama de Container - CashFlow
  Person(comerciante, "Comerciante")
  Container_Boundary(cashflow, "CashFlow System") {
    Container(transactions, "Transactions API", "ASP.NET Core", "CRUD lancamentos e emite eventos")
    Container(consolidated, "Consolidated API", "ASP.NET Core", "Consulta saldo diario")
    Container(worker, "Consolidation Worker", ".NET Worker", "Consome eventos e processa consolidacao")
    ContainerDb(txDb, "TransactionsDB", "PostgreSQL", "Armazena lancamentos")
    ContainerDb(consDb, "ConsolidatedDB", "PostgreSQL", "Armazena saldos consolidados")
    ContainerQueue(rabbit, "RabbitMQ", "Message Broker", "Barramento de eventos")
  }
  Container_Ext(keycloak, "Keycloak", "Identity Provider")
  Rel(comerciante, transactions, "Gerencia lancamentos", "HTTPS")
  Rel(comerciante, consolidated, "Consulta saldo", "HTTPS")
  Rel(transactions, rabbit, "Publica TransactionCreatedEvent", "AMQP")
  Rel(rabbit, worker, "Entrega evento", "AMQP")
  Rel(worker, consDb, "Atualiza consolidacao", "TCP/5432")
  Rel(transactions, txDb, "CRUD", "TCP/5432")
  Rel(consolidated, consDb, "Read", "TCP/5432")
  Rel(transactions, keycloak, "Valida JWT", "HTTPS")
  Rel(consolidated, keycloak, "Valida JWT", "HTTPS")
```
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Diagrama salvo em docs/c4/container-diagram.md
- [ ] #2 3 microservices representados
- [ ] #3 Infraestrutura (RabbitMQ, PostgreSQL, Keycloak) incluida
- [ ] #4 Protocolos de comunicacao mapeados
- [ ] #5 Formato Mermaid validado
<!-- AC:END -->
