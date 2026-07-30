---
id: TASK-005
title: 'ADR: Autenticação e Autorização'
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
Registrar ADR documentando a estrategia de autenticacao via Keycloak com public client e audit trail de usuario.

### Contexto
- Endpoints consumidos por usuarios logados (pessoas reais, nao maquinas)
- Qualquer usuario autenticado do cliente publico pode emitir transacoes
- Necessario rastrear quem fez cada lancamento (audit trail)

### Decisao
- **Client type:** Public (sem client secret) - Authorization Code + PKCE
- **Token:** JWT Bearer com claims sub, email, name
- **Validacao:** AddJwtBearer() em cada WebApi (issuer + audience)
- **Audit:** Extrair email claim do token e armazenar em Transaction.CreatedBy
- **RBAC:** Nao teremos - todo usuario autenticado do realm pode operar
- **Terraform:** Realm + public client apenas

### Consequencias
- Res - Simplicidade: sem gerenciamento de roles/permissões
- Res - Audit trail: toda transacao tem o email do autor
- Res - Seguranca: PKCE protege o fluxo Authorization Code
- Neg - Sem autorizacao granular (qualquer usuario pode tudo)

### Passos para executar:
1. Descrever fluxo de autenticacao (Authorization Code + PKCE)
2. Definir claims necessarias no token (email, name, sub)
3. Modelar Transaction.CreatedBy como string (email do usuario)
4. Configurar Terraform: realm + public client
5. Salvar como docs/adr/003-autenticacao-autorizacao.md
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Salvo como docs/adr/003-autenticacao-autorizacao.md
- [ ] #2 Fluxo Authorization Code + PKCE documentado
- [ ] #3 Claims do token definidas (sub, email, name)
- [ ] #4 Transaction.CreatedBy modelado para audit trail
- [ ] #5 Terraform simplificado: realm + public client
<!-- AC:END -->

## Implementation Plan

<!-- SECTION:PLAN:BEGIN -->
$1. Criar docs/adr/003-autenticacao-autorizacao.md\n2. Documentar fluxo de autenticação com diagrama de sequence\n3. Definir estrutura de claims e extração no backend\n4. Criar Terraform para realm + public client\n5. Atualizar modelo Transaction com CreatedBy
<!-- SECTION:PLAN:END -->
