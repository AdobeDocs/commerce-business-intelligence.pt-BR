---
title: Conectar o Zendesk
description: Saiba como consolidar os relatórios do suporte técnico em [!DNL MBI].
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 0%

---

# Connect [!DNL Zendesk]

>[!NOTE]
>
>Exige [Permissões de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/Zendesk_logo.png)

Conectar seu [!DNL Zendesk] Os dados do permitem consolidar os relatórios do suporte técnico no [!DNL MBI]. Isso permite otimizar o suporte ao cliente e monitorar o desempenho do suporte técnico junto com a receita.

Conectar seu [!DNL Zendesk] os dados são um processo simples de três etapas:

1. [Abra o [!DNL Zendesk] página credenciais em [!DNL MBI]](#stepone)
1. [Recupere seu [!DNL Zendesk] Token de API](#steptwo)
1. [Insira seu [!DNL Zendesk] informações de logon e token em [!DNL MBI]](#stepthree)

Para concluir esse processo, você precisará abrir duas janelas ou guias do navegador - uma para [!DNL MBI], o outro para o seu [!DNL Zendesk] conta.

## Abra o [!DNL Zendesk] página credenciais em [!DNL MBI] {#stepone}

1. Vá para o `Integrations` página abaixo **[!UICONTROL Manage Data** > ** Fontes de dados **> **Integrações]**.
1. Clique em **[!UICONTROL Add Integration]**, localizado no lado direito da tela.
1. Clique no botão [!DNL Zendesk] ícone . Isso abrirá o [!DNL Zendesk] credenciais.

## Recupere seu [!DNL Zendesk] Token de API {#steptwo}

1. Na janela/guia em que você está conectado ao [!DNL Zendesk] , clique no ícone Configurações (engrenagem) no canto inferior esquerdo da tela.
1. Quando a variável `Settings` for exibido, localize a variável `Channels` seção. Clique em **[!UICONTROL API]** nesta seção.
1. No `Token Access` nessa página, clique na caixa de seleção ao lado de `Enabled`. Uma lista de tokens de API ativos será exibida.
1. Clique em **[!UICONTROL Add New Token]**.
1. Quando solicitado, insira um rótulo para o token. Recomendamos usar `MBI`, para que você saiba, rapidamente, qual aplicativo está usando o token.
1. Clique em **[!UICONTROL Create]**.
1. Um token de API será criado. Copiar este token; ele será usado na próxima etapa.

## Enter [!DNL Zendesk] informações de logon e token da API em [!DNL MBI] {#stepthree}

1. Insira seu [!DNL Zendesk] prefixo do site e email de logon na [!DNL Zendesk] página credenciais em [!DNL MBI].
1. Insira o token da API.
1. Clique em **[!UICONTROL Save & Connect]**. Se a conexão for bem-sucedida, uma *Conexão bem-sucedida!* será exibida na parte superior da tela.

## Relacionadas:

* [Esperado [!DNL Zendesk] dados](../integrations/exp-zendesk-data.md)
* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
