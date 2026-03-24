---
title: Conectar anúncios do Facebook
description: Saiba como analisar os dados de gastos com anúncios e ver se o dinheiro está sendo gasto de maneira eficaz.
exl-id: 219a868b-f17c-4299-9e29-94db9156c9b6
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/6TR559YyeTHT3KWl3oA4Bdnpr-HCowTXTTkvmP0I0tg
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: bd989d82-1e15-4534-88db-f1f51dd77ffa
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 313
ht-degree: 0%

---

# Conectar [!DNL Facebook Ads]

>[!NOTE]
>
>Requer [permissões de administrador](../../../administrator/user-management/user-management.md).

![Logotipo do Facebook Ads](../../../assets/facebook-ads-logo.png)

Você fez sua pesquisa, criou seus anúncios, iniciou sua campanha em [!DNL Facebook]. Agora é hora de analisar seus dados de gastos com anúncios e ver se seu dinheiro está sendo gasto de maneira eficaz. Usando seus dados de gastos com anúncios, você pode [medir o ROI da campanha ao casar seu custo de publicidade com o valor vitalício do cliente (CLV)](../../../data-analyst/analysis/roi-ad-camp.md) dos usuários adquiridos de suas campanhas.

A conexão dos dados do [!DNL Facebook Ad] com o [!DNL Commerce Intelligence] é um processo simples de três etapas:

1. [Adicionar [!DNL Facebook] como uma fonte de dados em [!DNL Commerce Intelligence]](#stepone)
1. [Permitir [!DNL Commerce Intelligence] acesso aos seus [!DNL Facebook Ads] dados](#steptwo)
1. [Selecione [!DNL Facebook Ads] Contas para obter dados](#stepthree)

## Adicionar [!DNL Facebook] como uma fonte de dados em [!DNL Commerce Intelligence] {#stepone}

1. Para adicionar a integração do [!DNL Facebook] à sua conta do [!DNL Commerce Intelligence], navegue até a página `Connections` em **[!UICONTROL Manage Data** > **Integrations]**.
1. Clique em **[!UICONTROL Add Integration]**, localizado à direita.
1. Clique no ícone [!DNL Facebook]. Isso exibe a página de autorização [!DNL Facebook].
1. Clique em **[!UICONTROL Authorize]**.

## Permitir que [!DNL Commerce Intelligence] acesse seus dados de [!DNL Facebook Ads] {#steptwo}

Depois de clicar em **[!DNL Facebook Authorize]**, uma pequena janela pop-up será exibida:

![Caixa de diálogo de permissão de acesso do Facebook para o Commerce Intelligence](../../../assets/Facebook_Access_Popup.png)

Siga uma série de etapas para permitir que o [!DNL Commerce Intelligence] acesse dados do seu Perfil Público, [!DNL Facebook Ads] e estatísticas relacionadas. Clique em **[!UICONTROL OK]** nessas etapas para continuar.

## Selecione contas do [!DNL Facebook Ads] para obter dados {#stepthree}

1. Após a conclusão da autenticação, você será solicitado a selecionar as [!DNL Facebook Ads] contas das quais deseja extrair dados. Selecione as contas desejadas clicando na caixa de seleção na coluna `Connect`.

   ![Interface de seleção de contas de anúncio do Facebook](../../../assets/Facebook_Ad_Accounts.png)

1. Clique em **[!UICONTROL Save Connections]**.

   Se a conexão for bem-sucedida, uma *Conexão bem-sucedida!* mensagem é exibida na parte superior da página.

## O que vem a seguir? {#next}

Verifique se você está rastreando campanhas de [!DNL Facebook] em [!DNL Google Analytics]. Isso garante que o campo `utm\_campaign` em [!DNL Google Analytics] seja preenchido corretamente para suas campanhas [!DNL Facebook].

## Relacionados

* [Reautenticando integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Conectar sua conta  [!DNL Google Adwords] ](../integrations/google-ecommerce.md)
* [Rastrear origem da referência de ordem via [!DNL Google eCommerce]](../integrations/google-ecommerce.md)
* [Rastrear a fonte de referência do usuário no banco de dados](../../analysis/google-track-user-acq.md)
* [Rastrear o dispositivo do usuário, o navegador e os dados do sistema operacional no banco de dados](../../analysis/track-usr-dev-browser.md)
* [Descubra as fontes e os canais de aquisição mais valiosos](../../analysis/most-value-source-channel.md)
* [Aumente o ROI em suas campanhas publicitárias](../../analysis/roi-ad-camp.md)
* [Como funciona a atribuição  [!DNL Google Analytics] UTM?](../../analysis/utm-attributes.md)
