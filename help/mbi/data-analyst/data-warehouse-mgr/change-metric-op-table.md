---
title: Alterar a tabela operacional de uma métrica
description: Saiba como alterar a tabela de dados que uma métrica usa para executar sua operação.
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '231'
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

1. Se você não tiver uma coluna correspondente na nova tabela, poderá **criá-la na tabela de dados** ou [contatar o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) se for uma coluna de cálculo ou uma dimensão criada por [!DNL Commerce Intelligence]. Você também pode **excluir a dimensão da métrica**. Para excluir uma dimensão que não é mais necessária, retorne ao editor da métrica e selecione quais dimensões serão excluídas em `Dimensions`.

   ![Menu suspenso de seleção de coluna operacional](../../assets/change-metrics-3.png)
