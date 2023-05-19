---
title: Verificando o Status do Ciclo de Atualização
description: Saiba como verificar o status do ciclo de atualização.
exl-id: bd65f2bb-86c1-4e83-a132-797694ddb086
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Atualizar progresso do ciclo

Ao fazer logon no [!DNL Adobe Commerce Intelligence] há várias maneiras de verificar o status do seu último ciclo de atualização. Tudo depende do tipo de [permissões de usuário](../administrator/user-management/user-management.md) que você tem.

## Por que devo verificar o status do ciclo de atualização?

A verificação do ciclo de atualização de status é útil quando você está auditando os dados em seu [!DNL Commerce Intelligence] conta. Se você vir [resultados que não atendem às suas expectativas](../data-analyst/data-warehouse-mgr/data-and-updates-faq.md), por exemplo, vendas diárias em [!DNL Commerce Intelligence] não correspondem ao que você está vendo na sua plataforma de comércio eletrônico ou no seu [[!DNL Google] receita de comércio eletrônico](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html) você pode verificar o último ponto de dados para ver se o problema é resolvido depois que uma atualização é concluída.

## [!UICONTROL Read-Only] e [!UICONTROL Standard] Usuários

`Read-only` os usuários podem fazer logon no painel e ver como os dados foram atualizados recentemente, passando o mouse sobre o ícone na parte superior direita da página. Isso mostra quando o último ponto de dados foi extraído.

![](../../mbi/assets/last-success-data.png)

## [!UICONTROL Admin] Usuários

`Admin` os usuários podem fazer logon no painel e ver o último ponto de dados acima, juntamente com um breve ícone de status das integrações de conta.

Para obter mais detalhes, os usuários administradores podem clicar em **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]**.

![](../../mbi/assets/detail-manage-data-integrations.png)

Esta página mostra o status da atualização atual e a hora da última atualização concluída.

Se uma atualização estiver em andamento, você verá um link para solicitar uma notificação por email após a conclusão da atualização.

Se uma atualização não estiver em andamento, você verá um link para forçar o início de uma atualização.

>[!NOTE]
>
>Se você tiver horas de blecaute (horário em que não deseja [!DNL Commerce Intelligence] para atualizar seus dados), forçar uma atualização inicia um ciclo de atualização que não respeita as limitações dessas horas de blecaute.
