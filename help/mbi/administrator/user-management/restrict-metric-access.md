---
title: Restringir acesso às métricas
description: Saiba como trabalhar com acesso e restrições de métricas.
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# Gerenciar usuários de métricas

Além de definir níveis de permissão de usuário, você também pode restringir o acesso às métricas individualmente. Por exemplo, se você quiser que o departamento de contabilidade tenha acesso a métricas relacionadas à receita, mas não a métricas de aquisição de usuário, poderá restringir o acesso a essas métricas.

Em casos como esses, o Adobe recomenda configurar a conta desse usuário para **[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)**. **[!UICONTROL Standard]** permissões devem ser fornecidas a usuários que não precisam criar ou alterar métricas, colunas calculadas, integrações ou usuários, mas que precisam de acesso aos dados na Data Warehouse. Se quiser restringir totalmente o acesso aos dados, use o **[!UICONTROL Read Only]** permissões.

Depois de definir o nível de permissão, é possível selecionar as métricas a **[!UICONTROL Standard]** O usuário pode acessar o fazendo o seguinte:

1. Ir para **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**.
1. Selecione a conta de usuário desejada.
1. A variável **[!UICONTROL Metrics]** exibe uma lista de métricas disponíveis. Marque as métricas às quais você deseja que o usuário tenha acesso e desmarque as às quais ele não deve ter acesso.
1. [!DNL Adobe Commerce Intelligence] O salva as alterações automaticamente. Se a alteração for bem-sucedida, [!DNL Commerce Intelligence] exibições **[!UICONTROL Saved!]** na parte superior da página.

>[!NOTE]
>
>Todos os usuários com **[!UICONTROL Standard]** As permissões do podem acessar todos os dados na Data Warehouse por meio da Exportação de dados, além de todas as métricas do [!DNL Google Analytics].

Também é possível restringir o acesso a uma métrica editando a métrica e **[!UICONTROL Standard]** seleção de usuários na **[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)** seção.

>[!NOTE]
>
>Se você duplicar uma métrica, [!DNL Commerce Intelligence] copia as permissões do usuário definidas na métrica original.
