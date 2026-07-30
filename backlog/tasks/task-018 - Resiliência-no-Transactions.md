---
id: TASK-018
title: Resiliência no Transactions
status: To Do
assignee: []
created_date: '2026-07-30 01:45'
labels:
  - transactions resiliencia infra
dependencies: []
priority: medium
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Implementar Polly: circuit breaker para RabbitMQ (se broker cair, não derrubar o serviço), retry policy para falhas transientes, timeout policy. Garantir NF: serviço de lançamentos não pode ficar indisponível se o consolidador cair.
<!-- SECTION:DESCRIPTION:END -->
