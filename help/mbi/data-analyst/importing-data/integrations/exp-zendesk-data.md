---
title: Dados esperados do Zendesk
description: Saiba mais sobre as principais tabelas de dados que você pode importar do Zendesk para o MBI, incluindo links para a documentação adicional sobre os dados do Zendesk.
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---

# Dados esperados do Zendesk

Depois [você conectou seu [!DNL Zendesk] account](../integrations/zendesk.md), você pode usar o [Gerenciador de Datas Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear facilmente os campos de dados relevantes para análise.

Neste artigo, exploramos as principais tabelas de dados que podem ser importadas de [!DNL Zendesk] em [!DNL MBI], incluindo links para documentação adicional sobre [!DNL Zendesk] dados.

| Nome da tabela | Descrição |
|-----|-----|
| [`Audits`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | O `Audits` a tabela registra a atividade associada a um tíquete, incluindo alterações de status e respostas de cliente e agente. Esta tabela inclui uma ID de tíquete que se vincula ao `Tickets` , que permite analisar o tempo da primeira resposta e o tempo da resolução para cada tíquete. |
| [`Audit_~\_Events`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | O `audit_~\_events` a tabela é filha do `audits` e registra detalhes adicionais de um evento de tíquete. |
| [`Organizations`](https://developer.zendesk.com/rest_api/docs/core/organizations) | O `Organizations` A tabela registra as informações da empresa sobre os usuários finais, como o nome, a ID, os nomes de domínio associados, as tags e quaisquer campos personalizados. |
| [`Tickets`](https://developer.zendesk.com/rest_api/docs/core/tickets) | O `Tickets` a tabela registra todos os detalhes do tíquete, incluindo o `created_at` carimbo de data e hora, bem como `requester\_id` e `assignee\_id`, que permite vincular um tíquete a um usuário final e agente no `Users` , respectivamente. |
| [`Ticket_~\_Fields`](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | O `ticket fields` a tabela contém informações sobre os campos de texto básicos, bem como campos de tíquete personalizados na sua conta. Os atributos desta tabela incluem o campo `ID`, `URL`, `type`, `title`, `description`, `position`, `requirement setting`, informações específicas do agente e do usuário final e informações de criação e atualização. |
| [`Users`](https://developer.zendesk.com/rest_api/docs/core/users) | O `Users` A tabela inclui todos os detalhes sobre usuários finais e agentes, incluindo o nome e email de cada indivíduo. Isso permite analisar o envolvimento de seus usuários finais e o desempenho de seus agentes. |
| [`Zendesk\_Groups`](https://developer.zendesk.com/rest_api/docs/core/groups) | Grupos são como os agentes são organizados em sua conta do Zendesk. O `Groups` a tabela registra informações como `group ID`, `URL`, `name`, bem como informações de criação e atualização. |
| [`Zendesk\_Macro`](https://developer.zendesk.com/rest_api/docs/core/macros) | Macros são ações definidas por você que modificam os valores dos campos de um tíquete. Esta tabela contém atributos como título da macro, ID, ações, restrições e informações de criação e atualização. |
| [`Zendesk\_Tags`](https://developer.zendesk.com/rest_api/docs/core/tags) | O `Tags` contém uma lista de todas as tags em sua conta. |
| [`Zendesk\_Ticket\_Metrics`](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | Esta tabela contém dados sobre métricas de tíquete. Os campos incluem o `ticket ID`, `URL`e o número de grupos, destinatários, reaberturas, respostas, tempo de resposta (em minutos), tempo de resolução completo e informações da última atualização (por exemplo, status, destinatário ou solicitante). |

{style=&quot;table-layout:auto&quot;}

## Relacionado

* [Conectando o Zendesk](../integrations/zendesk.md)
* [Reautenticação de integrações](https://support.magento.com/hc/en-us/articles/360016733151-Reauthenticating-integrations)
