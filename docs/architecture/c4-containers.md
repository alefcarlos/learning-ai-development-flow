# Diagrama de Container - CashFlow System

## Propósito

Este diagrama C4 de Container (nível 2) mostra a decomposição do CashFlow System em microservices, bancos de dados, message broker e provedor de identidade.

## Diagrama

```mermaid
C4Container
  title Diagrama de Container - CashFlow

  Person(comerciante, "Comerciante")

  Container_Boundary(cashflow, "CashFlow System") {
    Container(transactions, "Transactions API", "ASP.NET Core", "CRUD de lançamentos e emite eventos")
    Container(consolidated, "Consolidated API", "ASP.NET Core", "Consulta saldo consolidado diário")
    Container(worker, "Consolidation Worker", ".NET Worker", "Consome eventos e processa consolidação")
    ContainerDb(txDb, "TransactionsDB", "PostgreSQL", "Armazena lançamentos")
    ContainerDb(consDb, "ConsolidatedDB", "PostgreSQL", "Armazena saldos consolidados")
    ContainerQueue(rabbit, "RabbitMQ", "Message Broker", "Barramento de eventos")
  }

  Container_Ext(keycloak, "Keycloak", "Identity Provider")

  Rel(comerciante, transactions, "Gerencia lançamentos", "HTTPS")
  Rel(comerciante, consolidated, "Consulta saldo", "HTTPS")
  Rel(transactions, rabbit, "Publica TransactionCreatedEvent", "AMQP")
  Rel(rabbit, worker, "Entrega evento", "AMQP")
  Rel(worker, consDb, "Atualiza consolidação", "TCP/5432")
  Rel(transactions, txDb, "CRUD", "TCP/5432")
  Rel(consolidated, consDb, "Read", "TCP/5432")
  Rel(transactions, keycloak, "Obtém chave pública JWKS", "HTTPS")
  Rel(consolidated, keycloak, "Obtém chave pública JWKS", "HTTPS")

  UpdateLayoutConfig($c4ShapeInRow="1", $c4BoundaryInRow="1")

  UpdateLayoutConfig($c4ShapeInRow="3", $c4BoundaryInRow="1")
```

## Containers

| Container | Tecnologia | Responsabilidade |
|-----------|-----------|------------------|
| **Transactions API** | ASP.NET Core | CRUD de lançamentos (débito/crédito), autenticação JWT, emissão de eventos |
| **Consolidated API** | ASP.NET Core | Consulta de saldo consolidado diário, autenticação JWT (read-only) |
| **Consolidation Worker** | .NET Worker | Consumer RabbitMQ, lógica de agregação e consolidação diária |
| **TransactionsDB** | PostgreSQL | Armazenamento de lançamentos financeiros |
| **ConsolidatedDB** | PostgreSQL | Armazenamento de saldos consolidados por dia |
| **RabbitMQ** | Message Broker | Barramento assíncrono para eventos de transação |

## Comunicação entre Containers

| Origem | Destino | Protocolo | Descrição |
|--------|---------|-----------|-----------|
| Comerciante | Transactions API | HTTPS | CRUD de lançamentos |
| Comerciante | Consolidated API | HTTPS | Consulta de saldo |
| Transactions API | RabbitMQ | AMQP | Publicação de `TransactionCreatedEvent` |
| RabbitMQ | Worker | AMQP | Entrega de evento para processamento |
| Worker | ConsolidatedDB | TCP/5432 | Inserção/atualização de consolidação |
| Transactions API | TransactionsDB | TCP/5432 | Leitura/escrita de lançamentos |
| Consolidated API | ConsolidatedDB | TCP/5432 | Leitura de saldos consolidados |
| Transactions API | Keycloak | HTTPS | Obtenção de chave pública JWKS (offline) |
| Consolidated API | Keycloak | HTTPS | Obtenção de chave pública JWKS (offline) |
