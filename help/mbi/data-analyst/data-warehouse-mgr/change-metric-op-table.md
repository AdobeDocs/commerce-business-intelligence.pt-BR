---
title: Alterar a tabela operacional de uma métrica
description: Saiba como alterar a tabela de dados que uma métrica usa para executar sua operação.
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/9yJ1Zc2NLDvXYO16UvDkeWE0hD1jx0-Ne3AyFFHX5ns
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
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 231
ht-degree: 0%

---

# Alterar a tabela operacional de uma métrica

Em certos casos, você pode decidir alterar a tabela de dados que uma métrica usa para executar sua operação. Por exemplo, se você tiver uma nova tabela de usuários, desejará migrar suas métricas relacionadas ao usuário da tabela `Users\_Old` para usar a tabela `Users\_New`.

1. Ir para **[!UICONTROL Data]** > **[!UICONTROL Metrics]**
1. Clique em **[!UICONTROL Edit]** ao lado da métrica para a qual você deseja alternar a tabela `operational`.
1. No editor, clique em **[!UICONTROL Change]**.

   ![Página de definição de métrica mostrando a configuração de tabela operacional](../../assets/change-metrics-1.png)
1. Selecione a nova tabela na qual você deseja basear essa métrica.
1. Faça a correspondência das dimensões de dados existentes com as correspondentes na nova tabela. Por exemplo, se você tiver uma coluna chamada `User's registration date`, basta selecionar qual coluna na nova tabela registra os mesmos dados de data. (Consulte a próxima etapa se você não tiver colunas correspondentes na nova tabela)

   ![Lista suspensa de seleção de tabela mostrando as tabelas disponíveis](../../assets/change-metrics-2.png)

1. Se você não tiver uma coluna correspondente na nova tabela, poderá **criá-la na tabela de dados** ou [contatar o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=pt-BR) se for uma coluna de cálculo ou uma dimensão criada por [!DNL Commerce Intelligence]. Você também pode **excluir a dimensão da métrica**. Para excluir uma dimensão que não é mais necessária, retorne ao editor da métrica e selecione quais dimensões serão excluídas em `Dimensions`.

   ![Menu suspenso de seleção de coluna operacional](../../assets/change-metrics-3.png)
