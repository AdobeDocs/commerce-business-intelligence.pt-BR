---
title: Conectar o Facebook Ads
description: Saiba como analisar os dados de gastos com anúncios e ver se o dinheiro está sendo gasto de maneira eficaz.
exl-id: 219a868b-f17c-4299-9e29-94db9156c9b6
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Conectar [!DNL Facebook Ads]

>[!NOTE]
>
>Exige [Permissões de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/Facebook_Logo.png)

Você fez sua pesquisa, criou seus anúncios, lançou sua campanha em [!DNL Facebook]. Agora é hora de analisar seus dados de gastos com anúncios e ver se seu dinheiro está sendo gasto de maneira eficaz. Usando seus dados de gastos com anúncios, você pode [meça o ROI da campanha casando seu custo de publicidade com o valor vitalício do cliente (CLV)](../../../data-analyst/analysis/roi-ad-camp.md) de usuários adquiridos de suas campanhas.

Conectar os dados de anúncios do Facebook ao [!DNL MBI] O é um processo simples de três etapas:

1. [Adicionar [!DNL Facebook] como fonte de dados no [!DNL MBI]](#stepone)
1. [Permitir [!DNL MBI] acesso ao seu [!DNL Facebook Ads] dados](#steptwo)
1. [Selecionar [!DNL Facebook Ads] Contas para obtenção de dados](#stepthree)

## Adicionar [!DNL Facebook] como fonte de dados no [!DNL MBI] {#stepone}

1. Para adicionar o [!DNL Facebook] integração com sua conta, navegue até o `Connections` página abaixo **[!UICONTROL Manage Data** > **Integrations]**.
1. Clique em **[!UICONTROL Add Integration]**, localizado no lado direito da tela acima da tela Data `Sources` tabela.
1. Clique em [!DNL Facebook] ícone. Isso exibe o [!DNL Facebook] página de autorização.
1. Clique em **[!UICONTROL Authorize]**.

## Permitir [!DNL MBI] acesso ao seu [!DNL Facebook Ads] dados {#steptwo}

Depois de clicar em **[!DNL Facebook Authorize]**, uma pequena janela pop-up será exibida:

![](../../../assets/Facebook_Access_Popup.png)

Siga uma série de etapas para permitir [!DNL MBI] para acessar dados do seu Perfil público, [!DNL Facebook Ads] e estatísticas relacionadas. Clique em **[!UICONTROL OK]** nessas etapas para continuar.

## Selecionar [!DNL Facebook Ads] Contas para obtenção de dados {#stepthree}

1. Após a conclusão da autenticação, você será solicitado a selecionar o [!DNL Facebook Ads] Contas das quais você deseja extrair dados. Selecione as contas desejadas clicando na caixa de seleção na `Connect` coluna.

   ![](../../../assets/Facebook_Ad_Accounts.png)

1. Clique em **[!UICONTROL Save Connections]**.

   Se a conexão for bem-sucedida, uma variável *Conexão bem sucedida!* é exibida na parte superior da página.

## O que vem a seguir? {#next}

Verifique se você está rastreando [!DNL Facebook] campanhas no [!DNL Google Analytics]. Isso garante que a `utm\_campaign` campo em [!DNL Google Analytics] está preenchido corretamente para [!DNL Facebook] campanhas.

## Relacionados

* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
* [Conecte seu [!DNL Google Adwords] account](../integrations/google-ecommerce.md)
* [Rastrear origem de referência de ordem via [!DNL Google eCommerce]](../integrations/google-ecommerce.md)
* [Rastrear a fonte de referência do usuário no banco de dados](../../analysis/google-track-user-acq.md)
* [Rastrear o dispositivo do usuário, o navegador e os dados do sistema operacional no banco de dados](../../analysis/track-usr-dev-browser.md)
* [Descubra as fontes e os canais de aquisição mais valiosos](../../analysis/most-value-source-channel.md)
* [Aumente o ROI em suas campanhas publicitárias](../../analysis/roi-ad-camp.md)
* [Como o [!DNL Google Analytics] A atribuição UTM funciona?](../../analysis/utm-attributes.md)
