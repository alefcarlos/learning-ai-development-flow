---
id: TASK-017
title: Emissão de eventos - RabbitMQ
status: To Do
assignee: []
created_date: '2026-07-30 01:45'
labels:
  - transactions eda mensageria
dependencies: []
priority: high
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Após criar transação, publicar TransactionCreatedEvent no RabbitMQ. Usar MassTransit ou Raw RabbitMQ. Evento deve conter: TransactionId, Amount, Type, Date, Timestamp. Configurar exchange transactions, routing key transaction.created.
<!-- SECTION:DESCRIPTION:END -->
