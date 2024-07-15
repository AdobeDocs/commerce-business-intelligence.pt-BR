---
title: Restringir acesso às métricas
description: Saiba como trabalhar com acesso e restrições de métricas.
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
role: Admin, User
feature: User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# Gerenciar usuários de métricas

Além de definir níveis de permissão de usuário, você também pode restringir o acesso às métricas individualmente. Por exemplo, se você quiser que o departamento de contabilidade tenha acesso a métricas relacionadas à receita, mas não a métricas de aquisição de usuário, poderá restringir o acesso a essas métricas.

Em casos como esses, o Adobe recomenda configurar a conta desse usuário como **[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)**. **[!UICONTROL Standard]** permissões devem ser concedidas a usuários que não precisam criar ou alterar métricas, colunas calculadas, integrações ou usuários, mas que precisam de acesso aos dados na Data Warehouse. Se quiser restringir totalmente o acesso aos dados, use as permissões de **[!UICONTROL Read Only]**.

Depois de definir o nível de permissão, você pode selecionar as métricas que um usuário **[!UICONTROL Standard]** pode acessar fazendo o seguinte:

1. Vá para **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**.
1. Selecione a conta de usuário desejada.
1. A guia **[!UICONTROL Metrics]** exibe uma lista de métricas disponíveis. Marque as métricas às quais você deseja que o usuário tenha acesso e desmarque as às quais ele não deve ter acesso.
1. [!DNL Adobe Commerce Intelligence] salva as alterações automaticamente. Se a alteração for bem-sucedida, [!DNL Commerce Intelligence] exibirá **[!UICONTROL Saved!]** na parte superior da página.

>[!NOTE]
>
>Todos os usuários com permissões **[!UICONTROL Standard]** podem acessar todos os dados na Data Warehouse por meio da Exportação de Dados, além de todas as métricas do [!DNL Google Analytics].

Você também pode restringir o acesso a uma métrica editando a métrica e **[!UICONTROL Standard]** selecionando usuários na seção **[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)**.

>[!NOTE]
>
>Se você duplicar uma métrica, [!DNL Commerce Intelligence] copiará as permissões de usuário definidas na métrica original.
