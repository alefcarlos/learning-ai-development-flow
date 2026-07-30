# ADR 002: Tech Stack

* Status: Accepted
* Date: 2026-07-29

## Context and Problem Statement

Selecionar as tecnologias para implementar o CashFlow System, considerando os requisitos do desafio (C#, boas práticas, padrões de arquitetura), a necessidade de resiliência, e o ecossistema .NET moderno.

## Decision Drivers

* Stack obrigatória: C# conforme requisito do desafio
* Maturidade e suporte da comunidade
* Performance e capacidade de atender 50 req/s com <5% de perda
* Facilidade de setup local para desenvolvimento

## Considered Options

For each technology category, alternatives were evaluated:

### Linguagem e Runtime
* **C# com .NET 8+ LTS** vs Java, Python, Node.js
* Justificativa: requisito do desafio, performance, ecossistema maduro

### Framework Web
* **ASP.NET Core** vs Minimal APIs vs FastEndpoints
* Justificativa: padrão do mercado, suporte oficial, maturidade

### ORM
* **EF Core** vs Dapper vs ADO.NET
* Justificativa: migrations nativas, LINQ, bom para cenário CRUD

### Database
* **PostgreSQL** vs SQL Server vs SQLite
* Justificativa: robustez, relacional, adequado para dados financeiros, sem lock-in

### Message Broker
* **RabbitMQ** vs Azure Service Bus vs Kafka
* Justificativa: maturidade, suporte .NET via MassTransit/Raw, fácil setup Docker

### Test Framework
* **xUnit + Microsoft.Testing.Platform** vs NUnit vs MSTest
* Justificativa: moderno, integração com Aspire testing, ecossistema ativo

### Identity Provider
* **Keycloak** vs Azure AD vs IdentityServer vs Duende
* Justificativa: open source, suporte OIDC/OAuth2, sem custo de licenciamento

### Orchestration/Dev
* **Aspire** vs docker-compose puro vs Tye
* Justificativa: observabilidade integrada, health checks, service discovery

### Infrastructure as Code
* **Terraform** vs Pulumi vs Bicep
* Justificativa: multi-cloud, open source, ideal para provisionar Keycloak

## Decision Outcome

Chosen option: **Stack completa combinando as tecnologias listadas acima**.

### Tecnologias Selecionadas

| Tecnologia | Versão | Propósito |
|------------|--------|-----------|
| .NET | 10.0 (LTS) | Runtime e SDK |
| ASP.NET Core | 10.0 | APIs REST |
| EF Core | 10.0 | ORM com PostgreSQL |
| PostgreSQL | 17 | Banco relacional |
| RabbitMQ | 4.3 | Message broker |
| xUnit | 3.x | Testes unitários/integração |
| Microsoft.Testing.Platform | 1.x | Plataforma de testes |
| Keycloak | 26.7 | Identity Provider |
| Aspire | 13.x | Observabilidade e orquestração |
| Terraform | 1.15 | IaC para Keycloak |

### Positive Consequences

* Stack coesa: todas as tecnologias têm boa integração com .NET
* Custo zero de licenciamento: todas as ferramentas são open source
* Documentação abundante: tecnologias maduras com comunidades ativas

### Negative Consequences

* Complexidade operacional: múltiplas tecnologias para gerenciar (PostgreSQL, RabbitMQ, Keycloak)
* Consumo de recursos: containers Docker para cada dependência durante desenvolvimento
