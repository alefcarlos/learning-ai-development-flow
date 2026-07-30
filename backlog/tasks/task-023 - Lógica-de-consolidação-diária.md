---
id: TASK-023
title: Lógica de consolidação diária
status: To Do
assignee: []
created_date: '2026-07-30 01:45'
labels:
  - worker dominio
dependencies: []
priority: high
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Implementar lógica: ao receber TransactionCreatedEvent, buscar/ criar DailyConsolidation da data, atualizar totalCredits/totalDebits, recalcular balance. Garantir idempotência (mesmo evento processado múltiplas vezes não duplica).
<!-- SECTION:DESCRIPTION:END -->
