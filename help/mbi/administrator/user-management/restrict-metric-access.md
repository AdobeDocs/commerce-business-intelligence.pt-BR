---
title: Restringir o acesso às métricas
description: Saiba como trabalhar com restrições e acesso a métricas.
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Gerenciar usuários de métricas

Além de definir os níveis de permissão do usuário, também é possível restringir o acesso às métricas individualmente. Por exemplo, se você quiser que seu departamento de contabilidade tenha acesso a métricas relacionadas à receita, mas não a métricas de aquisição de usuários, poderá restringir o acesso a essas métricas.

Em casos como esse, recomendamos configurar a conta desse usuário para **[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)**. **[!UICONTROL Standard]** permissões devem ser fornecidas a usuários que não precisam criar ou alterar métricas, colunas calculadas, integrações ou usuários, mas que precisam acessar os dados na Data Warehouse. Se quiser restringir totalmente o acesso aos dados, use a **[!UICONTROL Read Only]** permissões em vez disso.

Após definir o nível de permissão, você pode selecionar as métricas como **[!UICONTROL Standard]** O usuário pode acessar fazendo o seguinte:

1. Ir para **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**.
1. Selecione a conta de usuário desejada.
1. O **[!UICONTROL Metrics]** exibirá uma lista de métricas disponíveis. Verifique as métricas que você deseja que o usuário tenha acesso; desmarque aqueles aos quais o usuário não deve ter acesso.
1. [!DNL MBI] salva as alterações automaticamente. Se a alteração for bem-sucedida, [!DNL MBI] exibições **[!UICONTROL Saved!]** na parte superior da página.

>[!NOTE]
>
>Todos os usuários com **[!UICONTROL Standard]** As permissões do podem acessar todos os dados no data warehouse por meio da Exportação de dados, além de todas as métricas do [!DNL Google Analytics].

Também é possível restringir o acesso a uma métrica ao editar a métrica e **[!UICONTROL Standard]** selecionar usuários na **[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)** seção.

>[!NOTE]
>
>Se você duplicar uma métrica, [!DNL MBI] copia as permissões do usuário definidas na métrica original.
