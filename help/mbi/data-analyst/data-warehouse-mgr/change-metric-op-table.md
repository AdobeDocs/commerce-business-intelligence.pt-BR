---
title: Alterar a tabela operacional de uma métrica
description: Saiba como alterar a tabela de dados que uma métrica usa para executar sua operação.
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Alterar a tabela operacional de uma métrica

Em determinados casos, você pode decidir alterar a tabela de dados que uma métrica usa para executar sua operação. Por exemplo, se você tiver uma nova tabela de usuários, será necessário migrar as métricas relacionadas ao usuário da tabela &quot;Usuários\_Antigo&quot; para usar a tabela &quot;Usuários\_Novo&quot;.

1. Ir para **[!UICONTROL Data]** > **[!UICONTROL Metrics]**
1. Clique em **[!UICONTROL Edit]** ao lado da métrica para a qual você deseja alternar a variável `operational` tabela.
1. No editor, clique em **[!UICONTROL Change]**.

   ![](../../assets/change-metrics-1.png)
1. Agora selecione a nova tabela na qual deseja basear essa métrica.
1. Em seguida, será necessário corresponder as dimensões dos dados existentes às correspondentes na nova tabela. Por exemplo, se você tiver uma coluna chamada `User's registration date`, basta selecionar qual coluna na nova tabela registra os mesmos dados de data. (Veja a próxima etapa se você não tiver colunas correspondentes na nova tabela)

   ![](../../assets/change-metrics-2.png)

1. Se você não tiver uma coluna correspondente na nova tabela, poderá **criar na tabela de dados** ou [entrar em contato com o suporte](../../guide-overview.md) se for uma coluna ou dimensão de cálculo feita por [!DNL MBI]), ou simplesmente **excluir a dimensão da métrica**. Para excluir uma dimensão que não é mais necessária, retorne ao editor da métrica e selecione em quais dimensões excluir `Dimensions`.

   ![](../../assets/change-metrics-3.png)
