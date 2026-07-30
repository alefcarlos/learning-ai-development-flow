# Diagrama de Contexto - CashFlow System

## Propósito

Este diagrama C4 de Contexto (nível 1) mostra o sistema CashFlow e suas interações com atores externos e sistemas adjacentes.

## Diagrama

```mermaid
C4Context
  title Diagrama de Contexto - CashFlow

  Person(comerciante, "Comerciante", "Usuário que gerencia fluxo de caixa")

  System(cashflow, "CashFlow System", "Sistema de controle de lançamentos e consolidação diária")

  System_Ext(keycloak, "Keycloak", "Identity Provider - SSO e JWT")

  Rel(comerciante, cashflow, "Gerencia lançamentos e consulta saldo", "HTTPS")
  Rel(comerciante, keycloak, "Autentica-se", "HTTPS")
  Rel(cashflow, keycloak, "Obtém chave pública JWKS", "HTTPS")

  UpdateLayoutConfig($c4ShapeInRow="1", $c4BoundaryInRow="1")

  UpdateLayoutConfig($c4ShapeInRow="1", $c4BoundaryInRow="1")
```

## Atores e Sistemas

| Elemento | Tipo | Descrição |
|----------|------|-----------|
| **Comerciante** | Person | Usuário que gerencia o fluxo de caixa diário, realiza lançamentos e consulta saldos |
| **CashFlow System** | System | Sistema principal composto por 3 microservices que controla lançamentos financeiros e consolidação diária |
| **Keycloak** | External System | Identity Provider responsável por autenticação e emissão de tokens JWT |

## Fluxos Principais

1. Comerciante autentica-se no Keycloak (Authorization Code + PKCE)
2. Comerciante gerencia lançamentos via CashFlow System (com token JWT)
3. CashFlow System obtém chave pública JWKS do Keycloak e valida o token offline
4. Comerciante consulta saldo consolidado via CashFlow System
