---
title: Conectar Zendesk
description: Saiba como consolidar seus relatórios de suporte técnico no [!DNL MBI].
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# Conectar [!DNL Zendesk]

>[!NOTE]
>
>Exige [Permissões de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/Zendesk_logo.png)

Conectar o [!DNL Zendesk] permite consolidar seus relatórios de suporte técnico no [!DNL MBI]. Isso permite otimizar o suporte ao cliente e monitorar o desempenho do help desk junto com sua receita.

Conectar o [!DNL Zendesk] os dados são um processo simples de três etapas:

1. [Abra o [!DNL Zendesk] página de credenciais em [!DNL MBI]](#stepone)
1. [Recupere seu [!DNL Zendesk] Token de API](#steptwo)
1. [Insira seu [!DNL Zendesk] informações de logon e token no [!DNL MBI]](#stepthree)

Para concluir esse processo, é necessário abrir duas janelas ou guias do navegador - uma para [!DNL MBI], o outro para o [!DNL Zendesk] conta.

## Abra o [!DNL Zendesk] página de credenciais em [!DNL MBI] {#stepone}

1. Vá para a `Integrations` página abaixo **[!UICONTROL Manage Data** > ** Fontes de dados **> **Integrações]**.
1. Clique em **[!UICONTROL Add Integration]**, localizado no lado direito da tela.
1. Clique em [!DNL Zendesk] ícone. Isso abre o [!DNL Zendesk] página de credenciais.

## Recupere seu [!DNL Zendesk] Token de API {#steptwo}

1. Na janela/guia onde você está conectado no [!DNL Zendesk] clique no ícone Configurações (engrenagem) no canto inferior esquerdo da tela.
1. Quando a variável `Settings` for exibido, localize a variável `Channels` seção. Clique em **[!UICONTROL API]** nesta seção.
1. No `Token Access` desta página, clique na caixa de seleção ao lado de `Enabled`. Uma lista de Tokens de API ativos é exibida.
1. Clique em **[!UICONTROL Add New Token]**.
1. Quando solicitado, insira um rótulo para o token. O Adobe recomenda usar `MBI`, para que você saiba, rapidamente, qual aplicativo está usando o token.
1. Clique em **[!UICONTROL Create]**.
1. Um token de API é criado. Copie este token; ele será usado na próxima etapa.

## Enter [!DNL Zendesk] informações de logon e token de API em [!DNL MBI] {#stepthree}

1. Insira seu [!DNL Zendesk] prefixo do site e email de logon na [!DNL Zendesk] página de credenciais em [!DNL MBI].
1. Insira o token da API.
1. Clique em **[!UICONTROL Save & Connect]**. Se a conexão for bem-sucedida, uma variável *Conexão bem sucedida!* é exibida na parte superior da tela.

## Relacionados:

* [Esperado [!DNL Zendesk] dados](../integrations/exp-zendesk-data.md)
* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
