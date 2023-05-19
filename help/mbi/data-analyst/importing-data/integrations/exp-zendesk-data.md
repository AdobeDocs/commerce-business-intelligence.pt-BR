---
title: Dados esperados do Zendesk
description: Saiba mais sobre as principais tabelas de dados que você pode importar do Zendesk para o Commerce Intelligence, incluindo links para documentação adicional sobre dados do Zendesk.
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# Esperado [!DNL Zendesk] dados

Depois [você conectou o [!DNL Zendesk] account](../integrations/zendesk.md), você pode usar o [Gerenciador de Data Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear facilmente campos de dados relevantes para análise.

Este tópico explora as principais tabelas de dados das quais você pode importar [!DNL Zendesk] em [!DNL Adobe Commerce Intelligence], incluindo links para a documentação adicional sobre [!DNL Zendesk] dados.

| Nome da tabela | Descrição |
|-----|-----|
| [`Audits`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | A variável `Audits` a tabela registra a atividade associada a um ticket, incluindo alterações de status e respostas do cliente e do agente. Essa tabela inclui uma ID de tíquete vinculada à `Tickets` tabela, que permite analisar o tempo até a primeira resposta e o tempo até a resolução para cada ticket. |
| [`Audit_~\_Events`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | A variável `audit_~\_events` a tabela é filha do `audits` tabela e registra detalhes adicionais de um evento de ticket. |
| [`Organizations`](https://developer.zendesk.com/rest_api/docs/core/organizations) | A variável `Organizations` A tabela registra informações da empresa sobre seus usuários finais, como nome, ID, nomes de domínio associados, tags e campos personalizados. |
| [`Tickets`](https://developer.zendesk.com/rest_api/docs/core/tickets) | A variável `Tickets` A tabela registra todos os detalhes do ticket, incluindo o `created_at` carimbo de data e hora e o `requester\_id` e `assignee\_id`, que permite vincular um ticket a um usuário final e agente na `Users` tabela, respectivamente. |
| [`Ticket_~\_Fields`](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | A variável `ticket fields` A tabela contém informações sobre os campos de texto básico e campos de tíquete personalizados da sua conta. Os atributos desta tabela incluem o campo `ID`, `URL`, `type`, `title`, `description`, `position`, `requirement setting`informações específicas do agente e do usuário final e informações de criação e atualização. |
| [`Users`](https://developer.zendesk.com/rest_api/docs/core/users) | A variável `Users` A tabela inclui todos os detalhes sobre usuários finais e agentes, incluindo o nome e e-mail do indivíduo. Isso permite analisar o engajamento dos usuários finais e o desempenho dos agentes. |
| [`Zendesk\_Groups`](https://developer.zendesk.com/rest_api/docs/core/groups) | Grupos são como os agentes são organizados em sua conta do Zendesk. A variável `Groups` a tabela registra informações como `group ID`, `URL`, `name`e criação e atualização de informações. |
| [`Zendesk\_Macro`](https://developer.zendesk.com/rest_api/docs/core/macros) | As macros são ações definidas por você que modificam os valores dos campos de um tíquete. Esta tabela contém atributos como título, ID, ações, restrições e informações de criação e atualização da macro. |
| [`Zendesk\_Tags`](https://developer.zendesk.com/rest_api/docs/core/tags) | A variável `Tags` A tabela contém uma lista de todas as tags da sua conta. |
| [`Zendesk\_Ticket\_Metrics`](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | Esta tabela contém dados sobre métricas de tíquete. Os campos incluem `ticket ID`, `URL`e o número de grupos, responsáveis, reaberturas, respostas, tempo de resposta (em minutos), tempo de resolução total e informações da última atualização (por exemplo, status, responsável ou solicitante). |

{style="table-layout:auto"}

## Relacionados

* [Conectar o Zendesk](../integrations/zendesk.md)
* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
