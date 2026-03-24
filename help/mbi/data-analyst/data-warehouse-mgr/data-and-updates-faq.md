---
title: Informações de Dados e Atualizações
description: Saiba como verificar o status do ciclo de atualização.
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/qT3lojSuve8jHgNVKoJCUW82cN2QK497wFX8NVbptWI
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 481
ht-degree: 0%

---

# Informações de Dados e Atualizações

* [Por que meus dados foram alterados?](#datachange)
* [Qual é a diferença entre uma atualização regular e forçada?](#regularforcedupdates)
* [Por que o ciclo de atualização leva muito tempo?](#updatecycletime)
* [Posso ser notificado quando um ciclo de atualização for concluído?](#notifyupdate)
* [Por que os dados do  [!DNL Google ECommerce]  são diferentes do meu banco de dados?](#ecommdatabase)
* [Como solucionar problemas de discrepância de dados?](#datadiscrepancy)

## Por que meus dados foram alterados? {#datachange}

Os valores do gráfico podem mudar durante o dia devido aos novos dados que estão sendo sincronizados com sua Data Warehouse. Além disso, os valores para colunas de dados existentes podem mudar devido a [reverificações](../data-warehouse-mgr/cfg-data-rechecks.md). Uma nova verificação é um processo que procura valores alterados em colunas de dados, como um status de pedido movendo de `open` para `shipped`.

Há algumas maneiras diferentes [de verificar o status do ciclo de atualizações](../../best-practices/check-update-cycle.md), dependendo das configurações de permissões do usuário:

* **[!UICONTROL Read-Only]e [!UICONTROL Standard] Usuários** - Podem passar o mouse sobre o ícone na parte superior direita da página para ver quando o último ponto de dados foi extraído.
* **[!UICONTROL Admin]Usuários** - Podem exibir o último ponto de dados e ícone de status de integrações de contas. Para obter mais detalhes, navegue até **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]** para ver o status da atualização atual e a hora da última atualização concluída.
* **Método de API** - Pode recuperar o ciclo de atualização concluído mais recentemente usando a API de Status do Ciclo de Atualização.

Para obter detalhes completos sobre a verificação do status do ciclo de atualização, consulte [Verificando o Status do Ciclo de Atualização](../../best-practices/check-update-cycle.md).

## Qual é a diferença entre uma atualização regular e forçada? {#regularforcedupdates}

As atualizações regulares são **processos agendados**, enquanto as atualizações forçadas são **processos manuais iniciados por você**. Se você tiver horas de blecaute (ou um período em que [!DNL Commerce Intelligence] não deve atualizar seus dados), forçar uma atualização inicia um ciclo que não respeita as limitações do período de blecaute.

## Por que o ciclo de atualização leva muito tempo? {#updatecycletime}

Vários fatores podem aumentar um tempo de atualização já longo. Determinados [métodos de replicação](../data-warehouse-mgr/cfg-replication-methods.md), [frequências de reverificação mais altas](../data-warehouse-mgr/cfg-data-rechecks.md) e o número de painéis e gráficos são apenas alguns colaboradores. A Adobe recomenda [redefinir algumas de suas configurações](../../best-practices/reduce-update-cycle-time.md) e [otimizar o banco de dados para análise](../../best-practices/opt-db-analysis.md) para reduzir os tempos de atualização.

## Posso ser notificado quando um ciclo de atualização for concluído? {#notifyupdate}

Se uma atualização estiver em andamento, há um link na página **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]** que você pode usar para solicitar uma notificação por email após a conclusão do ciclo. Se uma atualização não estiver em andamento, você verá um link para forçar o início de uma atualização.

## Por que os dados do [!DNL Google ECommerce] são diferentes do meu banco de dados? {#ecommdatabase}

Discrepâncias entre [!DNL Google Analytics] e seu banco de dados podem surgir por vários motivos. O rastreamento não está ativado corretamente, os usuários que visitam de forma incógnita e os eventos de clique que não estão funcionando corretamente são apenas alguns exemplos. Se a receita e os pedidos não parecerem corretos, [consulte este tópico](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html) para diagnosticar um problema.

## Como solucionar problemas de discrepância de dados? {#datadiscrepancy}

A Adobe sabe que ver dados inconsistentes pode ser uma experiência frustrante. Tente usar o [tutorial de Lista de Verificação de Discrepância de Dados](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html) ou [de Exportações de Dados](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html) para diagnosticar o problema. Se você ainda estiver com problemas, [contate o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
