---
id: TASK-005
title: 'ADR: Autenticação e Autorização'
status: To Do
assignee: []
created_date: '2026-07-30 01:44'
labels:
  - documentacao arquitetura adr
dependencies: []
priority: high
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Registrar decisão de usar Keycloak como SSO com JWT Bearer token. Fluxo: client credentials grant para machine-to-machine. Configurar RBAC com roles admin/operator. Proteger todos os endpoints das WebAPIs com [Authorize].
<!-- SECTION:DESCRIPTION:END -->
