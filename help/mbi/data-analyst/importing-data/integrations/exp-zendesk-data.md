---
title: Dados esperados do Zendesk
description: Saiba mais sobre as principais tabelas de dados que você pode importar do Zendesk para o Commerce Intelligence, incluindo links para documentação adicional sobre dados do Zendesk.
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/0p4SOrpj7wM-y5j3CMpHTs7HpysB5znJu3jSNiVJ2YY
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 362
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
