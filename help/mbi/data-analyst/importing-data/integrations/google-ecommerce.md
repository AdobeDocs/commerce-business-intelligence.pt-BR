---
title: Conectar o Google Commerce
description: Saiba mais sobre os seus canais de referência mais importantes.
exl-id: c80f52f3-894a-4084-8c0e-aee618ed77f5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# Conectar [!DNL Google ECommerce]

>[!NOTE]
>
>Requer [permissões de administrador](../../../administrator/user-management/user-management.md).

![Logotipo do Google eCommerce](../../../assets/google-ecommerce-logo.png)

Você tem fluxo constante de tráfego e pedidos, o que significa que está efetivamente atingindo e adquirindo clientes. Mas quais são seus canais de indicação mais valiosos? Qual é o valor médio de vida útil dos clientes adquiridos de uma origem em relação a outra? Conectando seus dados de origem da indicação de pedido de [!DNL Google ECommerce] a [!DNL Commerce Intelligence], você poderá criar análises que ajudarão a identificar seus [canais de marketing mais valiosos](../../../data-analyst/analysis/most-value-source-channel.md).

Comece digitando suas credenciais do [!DNL Google ECommerce] em [!DNL Commerce Intelligence]:

1. Vá para a página `Connections` em **[!UICONTROL Admin** > **Connections]**.

1. Clique em **[!UICONTROL Add a New Source]**, localizado no lado direito da tela acima da tabela `Data Sources`.

1. Clique no ícone [!DNL Google ECommerce]. Isso abre a página de credenciais do [!DNL Google ECommerce].

1. Insira suas credenciais do [!DNL Google Analytics]. Ao concluir o processo de autorização, você será redirecionado de volta para [!DNL Commerce Intelligence].

1. Uma lista de IDs de perfil é exibida. Verifique os perfis aos quais você deseja se conectar [!DNL Commerce Intelligence].

   Se você tiver vários perfis e precisar de ajuda para identificar qual é qual, consulte a seção **Conectando vários perfis do [!DNL Google Analytics] abaixo.

   ![Formulário que mostra opções para conectar vários perfis do Google Analytics](../../../assets/conn-mult-ga-profiles.png)<!--{: width="500"}-->

1. As alterações são salvas automaticamente, portanto, clique em **[!UICONTROL Back to Connections]** quando terminar.

## Conectando vários perfis do [!DNL Google Analytics] a [!DNL Commerce Intelligence]

Você pode ter vários sites conectados a uma única conta do [!DNL Google Analytics], identificados pela própria ID de perfil do [!DNL Google Analytics]. Nesse caso, você tem a opção de incluir todas as IDs de perfil em [!DNL Commerce Intelligence]. Marque as IDs de perfil que você deseja incluir durante a etapa de seleção de perfil.

Para identificar a ID de perfil do [!DNL Google Analytics] de um site específico:

1. Faça logon em [!DNL Google Analytics].
1. Vá para o painel [!DNL Google Analytics] do site específico.
1. Examine a URL - a ID do Perfil corresponde aos oito números que seguem `p` no final da linha.

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Desconectando [!DNL Google ECommerce] de [!DNL Commerce Intelligence] {#disconnect}

1. Visite a página [!DNL Google Analytics] [configurações da conta](https://www.google.com/account/about/?hl=en).
1. Na seção `Security`, clique em **[!UICONTROL edit]** ao lado de `Authorizing` aplicativos e sites.
1. Clique em **[!UICONTROL revoke access]** ao lado de [!DNL Commerce Intelligence].

## Relacionados:

* [Dados  [!DNL Google ECommerce]  esperados](../integrations/google-ecommerce-data.md)
* [Reautenticando integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=pt-BR)
* [Configurando [!DNL Google ECommerce] rastreamento](https://support.google.com/analytics/answer/1009612?hl=en)
* [Descubra as fontes e os canais de aquisição mais valiosos](../../analysis/most-value-source-channel.md)
* [Aumente o ROI em suas campanhas publicitárias](../../analysis/roi-ad-camp.md)
