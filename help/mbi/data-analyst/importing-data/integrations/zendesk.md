---
title: Conectar Zendesk
description: Saiba como consolidar seus relatórios de suporte técnico no [!DNL Commerce Intelligence].
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# Conectar [!DNL Zendesk]

>[!NOTE]
>
>Requer [permissões de administrador](../../../administrator/user-management/user-management.md).

![Logotipo do Zendesk](../../../assets/Zendesk_logo.png)

Conectar os dados do [!DNL Zendesk] permite consolidar os relatórios do suporte técnico no [!DNL Commerce Intelligence]. Isso permite otimizar o suporte ao cliente e monitorar o desempenho do help desk junto com sua receita.

A conexão de dados do [!DNL Zendesk] é um processo simples de três etapas:

1. [Abrir a página  [!DNL Zendesk] credenciais [!DNL Commerce Intelligence]](#stepone)
1. [Recuperar o token de API  [!DNL Zendesk] ](#steptwo)
1. [Insira suas  [!DNL Zendesk] informações de logon e o token em  [!DNL Commerce Intelligence]](#stepthree)

Para concluir esse processo, é necessário abrir duas janelas ou guias do navegador: uma para [!DNL Commerce Intelligence] e outra para sua conta do [!DNL Zendesk].

## Abrir a página de credenciais do [!DNL Zendesk] em [!DNL Commerce Intelligence] {#stepone}

1. Vá para a página `Integrations` em **[!UICONTROL Manage Data** > ** Fontes de Dados **> **Integrações]**.
1. Clique em **[!UICONTROL Add Integration]**, localizado no lado direito da tela.
1. Clique no ícone [!DNL Zendesk]. Isso abre a página de credenciais do [!DNL Zendesk].

## Recupere o token de API [!DNL Zendesk] {#steptwo}

1. Na janela/guia onde você está conectado à sua conta do [!DNL Zendesk], clique no ícone Configurações (engrenagem) no canto inferior esquerdo da tela.
1. Quando o menu `Settings` for exibido, localize a seção `Channels`. Clique em **[!UICONTROL API]** nesta seção.
1. Na seção `Token Access` desta página, clique na caixa de seleção ao lado de `Enabled`. Uma lista de Tokens de API ativos é exibida.
1. Clique em **[!UICONTROL Add New Token]**.
1. Quando solicitado, insira um rótulo para o token. A Adobe recomenda usar o `Commerce Intelligence`, para que você saiba rapidamente qual aplicativo está usando o token.
1. Clique em **[!UICONTROL Create]**.
1. Um token de API é criado. Copie este token; ele será usado na próxima etapa.

## Inserir informações de logon e token de API do [!DNL Zendesk] em [!DNL Commerce Intelligence] {#stepthree}

1. Insira o prefixo do site [!DNL Zendesk] e o email de logon na página de credenciais do [!DNL Zendesk] em [!DNL Commerce Intelligence].
1. Insira o token da API.
1. Clique em **[!UICONTROL Save & Connect]**. Se a conexão for bem-sucedida, uma *Conexão bem-sucedida!* mensagem é exibida na parte superior da tela.

## Relacionados:

* [Dados  [!DNL Zendesk]  esperados](../integrations/exp-zendesk-data.md)
* [Reautenticando integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
