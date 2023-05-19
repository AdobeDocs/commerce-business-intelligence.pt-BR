---
title: Conectar o Google Commerce
description: Saiba mais sobre os seus canais de referência mais importantes.
exl-id: c80f52f3-894a-4084-8c0e-aee618ed77f5
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Conectar [!DNL Google ECommerce]

>[!NOTE]
>
>Exige [Permissões de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/google-ecommerce-logo.png)

Você tem fluxo constante de tráfego e pedidos, o que significa que está efetivamente atingindo e adquirindo clientes. Mas quais são seus canais de indicação mais valiosos? Qual é o valor médio de vida útil dos clientes adquiridos de uma origem em relação a outra? Conectando seus dados de origem de referência de pedido do [!DNL Google ECommerce] para [!DNL Commerce Intelligence], você pode criar análises que ajudam a identificar [canais de marketing mais valiosos](../../../data-analyst/analysis/most-value-source-channel.md).

Comece digitando seu [!DNL Google ECommerce] credenciais para [!DNL Commerce Intelligence]:

1. Vá para a `Connections` página abaixo **[!UICONTROL Admin** > **Connections]**.

1. Clique em **[!UICONTROL Add a New Source]**, localizado no lado direito da tela acima da `Data Sources` tabela.

1. Clique em [!DNL Google ECommerce] ícone. Isso abre o [!DNL Google ECommerce] página de credenciais.

1. Insira seu [!DNL Google Analytics] credenciais. Ao concluir o processo de autorização, você será redirecionado de volta para [!DNL Commerce Intelligence].

1. Uma lista de IDs de perfil é exibida. Marque os perfis aos quais deseja se conectar [!DNL Commerce Intelligence].

   Se você tiver vários perfis e precisar de ajuda para identificar qual é qual, consulte o **Conectando vários [!DNL Google Analytics] seção de perfis abaixo.

   ![](../../../assets/conn-mult-ga-profiles.png)<!--{: width="500"}-->

1. As alterações são salvas automaticamente, portanto, clique em **[!UICONTROL Back to Connections]** quando terminar.

## Conectando vários [!DNL Google Analytics] perfis para [!DNL Commerce Intelligence]

Você pode ter vários sites conectados a um único [!DNL Google Analytics] conta, identificada pelos seus próprios [!DNL Google Analytics] ID do perfil. Nesse caso, você tem a opção de incluir todas as IDs de perfil no [!DNL Commerce Intelligence]. Marque as IDs de perfil que você deseja incluir durante a etapa de seleção de perfil.

Para identificar o de um site específico [!DNL Google Analytics] ID do perfil:

1. Efetue logon no [!DNL Google Analytics].
1. Ir para o site específico [!DNL Google Analytics] painel.
1. Examine o URL - a ID do perfil corresponde aos oito números seguintes `p` no final da linha.

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Desconectando [!DNL Google ECommerce] de [!DNL Commerce Intelligence] {#disconnect}

1. Visite seu [!DNL Google Analytics] [configurações da conta](https://www.google.com/account/about/?hl=en) página.
1. No `Security` clique em **[!UICONTROL edit]** ao lado de `Authorizing` aplicativos e sites.
1. Clique em **[!UICONTROL revoke access]** ao lado de [!DNL Commerce Intelligence].

## Relacionados:

* [Esperado [!DNL Google ECommerce] dados](../integrations/google-ecommerce-data.md)
* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Configuração [!DNL Google ECommerce] rastreamento](https://support.google.com/analytics/answer/1009612?hl=en)
* [Descubra as fontes e os canais de aquisição mais valiosos](../../analysis/most-value-source-channel.md)
* [Aumente o ROI em suas campanhas publicitárias](../../analysis/roi-ad-camp.md)
