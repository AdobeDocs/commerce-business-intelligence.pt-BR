---
title: Conectar anúncios do Facebook
description: Saiba como analisar os dados de gastos com anúncios e ver se o dinheiro está sendo gasto de maneira eficaz.
exl-id: 219a868b-f17c-4299-9e29-94db9156c9b6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---

# Conectar [!DNL Facebook Ads]

>[!NOTE]
>
>Requer [permissões de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/facebook-ads-logo.png)

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

![](../../../assets/Facebook_Access_Popup.png)

Siga uma série de etapas para permitir que o [!DNL Commerce Intelligence] acesse dados do seu Perfil Público, [!DNL Facebook Ads] e estatísticas relacionadas. Clique em **[!UICONTROL OK]** nessas etapas para continuar.

## Selecione contas do [!DNL Facebook Ads] para obter dados {#stepthree}

1. Após a conclusão da autenticação, você será solicitado a selecionar as [!DNL Facebook Ads] contas das quais deseja extrair dados. Selecione as contas desejadas clicando na caixa de seleção na coluna `Connect`.

   ![](../../../assets/Facebook_Ad_Accounts.png)

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
