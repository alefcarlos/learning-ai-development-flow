---
id: TASK-022
title: Consumer RabbitMQ - Worker
status: To Do
assignee: []
created_date: '2026-07-30 01:45'
labels:
  - worker eda mensageria
dependencies: []
priority: high
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Implementar consumer do TransactionCreatedEvent no Worker. Configurar fila transaction.created.queue vinculada à exchange transactions. Processar mensagens em lote para eficiência. Atualizar/inserir DailyConsolidation no banco Consolidated.
<!-- SECTION:DESCRIPTION:END -->
