---
title: Dados esperados do Zendesk
description: Saiba mais sobre as principais tabelas de dados que você pode importar do Zendesk para o Commerce Intelligence, incluindo links para documentação adicional sobre dados do Zendesk.
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Dados [!DNL Zendesk] esperados

Depois de [conectar sua [!DNL Zendesk] conta](../integrations/zendesk.md), você poderá usar o [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear facilmente campos de dados relevantes para análise.

Este tópico explora as principais tabelas de dados que você pode importar de [!DNL Zendesk] para [!DNL Adobe Commerce Intelligence], incluindo links para documentação adicional sobre dados de [!DNL Zendesk].

| Nome da tabela | Descrição |
|-----|-----|
| [`Audits`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | A tabela `Audits` registra a atividade associada a um tíquete, incluindo alterações de status e respostas do cliente e do agente. Esta tabela inclui uma ID de tíquete vinculada à tabela `Tickets`, que permite analisar o tempo até a primeira resposta e o tempo até a resolução para cada tíquete. |
| [`Audit_~\_Events`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | A tabela `audit_~\_events` é filha da tabela `audits` e registra detalhes adicionais de um evento de tíquete. |
| [`Organizations`](https://developer.zendesk.com/rest_api/docs/core/organizations) | A tabela `Organizations` registra informações da empresa sobre seus usuários finais, como nome, ID, nomes de domínio associados, marcas e campos personalizados. |
| [`Tickets`](https://developer.zendesk.com/rest_api/docs/core/tickets) | A tabela `Tickets` registra todos os detalhes do tíquete, incluindo o carimbo de data e hora `created_at` e `requester\_id` e `assignee\_id`, que permitem vincular um tíquete a um usuário final e agente na tabela `Users`, respectivamente. |
| [`Ticket_~\_Fields`](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | A tabela `ticket fields` contém informações sobre os campos de texto básico e campos de tíquete personalizados da sua conta. Os atributos desta tabela incluem o campo `ID`, `URL`, `type`, `title`, `description`, `position`, `requirement setting`, informações específicas do agente e do usuário final e informações de criação e atualização. |
| [`Users`](https://developer.zendesk.com/rest_api/docs/core/users) | A tabela `Users` inclui todos os detalhes sobre usuários finais e agentes, incluindo o nome e email do indivíduo. Isso permite analisar o engajamento dos usuários finais e o desempenho dos agentes. |
| [`Zendesk\_Groups`](https://developer.zendesk.com/rest_api/docs/core/groups) | Grupos são como os agentes são organizados em sua conta do Zendesk. A tabela `Groups` registra informações como `group ID`, `URL`, `name` e informações de criação e atualização. |
| [`Zendesk\_Macro`](https://developer.zendesk.com/rest_api/docs/core/macros) | As macros são ações definidas por você que modificam os valores dos campos de um tíquete. Esta tabela contém atributos como título, ID, ações, restrições e informações de criação e atualização da macro. |
| [`Zendesk\_Tags`](https://developer.zendesk.com/rest_api/docs/core/tags) | A tabela `Tags` contém uma lista de todas as tags da sua conta. |
| [`Zendesk\_Ticket\_Metrics`](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | Esta tabela contém dados sobre métricas de tíquete. Os campos incluem `ticket ID`, `URL`, e o número de grupos, responsáveis, reaberturas, respostas, tempo de resposta (em minutos), tempo de resolução total e informações da última atualização (por exemplo, status, responsável ou solicitante). |

{style="table-layout:auto"}

## Relacionados

* [Conectar o Zendesk](../integrations/zendesk.md)
* [Reautenticando integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=pt-BR)
