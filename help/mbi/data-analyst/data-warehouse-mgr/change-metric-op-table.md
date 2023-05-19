---
title: Alterar a tabela operacional de uma métrica
description: Saiba como alterar a tabela de dados que uma métrica usa para executar sua operação.
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# Alterar a tabela operacional de uma métrica

Em certos casos, você pode decidir alterar a tabela de dados que uma métrica usa para executar sua operação. Por exemplo, se você tiver uma nova tabela de usuários, desejará migrar suas métricas relacionadas ao usuário do  `Users\_Old` tabela para usar o `Users\_New` tabela em vez disso.

1. Ir para **[!UICONTROL Data]** > **[!UICONTROL Metrics]**
1. Clique em **[!UICONTROL Edit]** ao lado da métrica para a qual você deseja alternar a variável `operational` tabela.
1. No editor, clique em **[!UICONTROL Change]**.

   ![](../../assets/change-metrics-1.png)
1. Selecione a nova tabela na qual você deseja basear essa métrica.
1. Faça a correspondência das dimensões de dados existentes com as correspondentes na nova tabela. Por exemplo, se você tiver uma coluna chamada `User's registration date`, basta selecionar qual coluna na nova tabela registra os mesmos dados de data. (Consulte a próxima etapa se você não tiver colunas correspondentes na nova tabela)

   ![](../../assets/change-metrics-2.png)

1. Se você não tiver uma coluna correspondente na nova tabela, poderá **criar na tabela de dados** ou [entre em contato com o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) se for uma coluna de cálculo ou dimensão feita por [!DNL Commerce Intelligence]. Também é possível **excluir a dimensão da métrica**. Para excluir uma dimensão que não é mais necessária, retorne ao editor da métrica e selecione em quais dimensões serão excluídas `Dimensions`.

   ![](../../assets/change-metrics-3.png)
