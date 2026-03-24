---
title: Conectar o Google Commerce
description: Saiba mais sobre os seus canais de referência mais importantes.
exl-id: c80f52f3-894a-4084-8c0e-aee618ed77f5
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/iBVf-dkbm1NbELZUYjLp1TzypO7Cu55tIzd93lQ1zo0
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 305
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
* [Reautenticando integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Configurando [!DNL Google ECommerce] rastreamento](https://support.google.com/analytics/answer/1009612?hl=en)
* [Descubra as fontes e os canais de aquisição mais valiosos](../../analysis/most-value-source-channel.md)
* [Aumente o ROI em suas campanhas publicitárias](../../analysis/roi-ad-camp.md)
