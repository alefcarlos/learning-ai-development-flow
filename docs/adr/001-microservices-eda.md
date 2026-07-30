# ADR 001: Microservices com Event-Driven Architecture

* Status: Accepted
* Date: 2026-07-29

## Context and Problem Statement

O desafio exige que o serviço de controle de lançamentos não fique indisponível se o sistema de consolidação diária cair. Em dias de pico, o serviço de consolidação recebe 50 requisições por segundo, com no máximo 5% de perda. Como arquitetar o sistema para atender aos requisitos de resiliência e escala, mantendo o desacoplamento entre os domínios de lançamentos e consolidação?

## Decision Drivers

* Resiliência: falha no consolidador não pode afetar lançamentos
* Escala: capacidade de escalar cada domínio independentemente
* Desacoplamento: lançamentos e consolidação são bounded contexts distintos
* Observabilidade: necessidade de monitorar fluxos assíncronos

## Considered Options

* **Modular Monolith** - Único processo com módulos separados por pastas/projetos
* **Microservices com EDA** - Serviços independentes comunicando-se via eventos assíncronos
* **SOA** - Serviços maiores com comunicação síncrona via ESB

## Decision Outcome

Chosen option: **Microservices com Event-Driven Architecture (EDA)**

Cada bounded context (Transactions e Consolidated) torna-se um microservice independente. A comunicação entre eles é puramente assíncrona via RabbitMQ, garantindo que falhas no consolidador não impactem o serviço de lançamentos.

### Positive Consequences

* Resiliência: o serviço de lançamentos continua operando mesmo que o consolidador esteja fora
* Escala independente: é possível escalar horizontalmente apenas Transactions API ou Worker conforme necessidade
* Desacoplamento: bounded contexts evoluem independentemente com seus próprios deploys
* Tolerância a picos: o RabbitMQ atua como buffer, suavizando picos de 50 req/s

### Negative Consequences

* Complexidade operacional: gerenciar múltiplos serviços (deploy, monitoramento, logging)
* Consistência eventual: o saldo consolidado pode ter delay em relação aos lançamentos
* Overhead de infraestrutura: necessário gerenciar RabbitMQ e bancos de dados separados

## Estrutura de Serviços

```
CashFlow.Service.Transactions  (WebApi - ASP.NET Core)
CashFlow.Service.Consolidated  (WebApi - ASP.NET Core)
CashFlow.Worker.Consolidation  (Worker - .NET)
CashFlow.Shared                (Biblioteca compartilhada - contratos, result pattern)
```

## Fluxo de Eventos

1. Transactions API recebe lançamento via HTTP
2. Transactions API persiste no TransactionsDB
3. Transactions API publica `TransactionCreatedEvent` no RabbitMQ
4. Worker consome o evento do RabbitMQ
5. Worker processa e atualiza o ConsolidatedDB
6. Consolidated API retorna o saldo consolidado para consulta
