---
title: Conectar Zendesk
description: Saiba como consolidar seus relatórios de suporte técnico no [!DNL Commerce Intelligence].
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 1%

---

# Conectar [!DNL Zendesk]

>[!NOTE]
>
>Exige [Permissões de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/Zendesk_logo.png)

Conectar o [!DNL Zendesk] permite consolidar seus relatórios de suporte técnico no [!DNL Commerce Intelligence]. Isso permite otimizar o suporte ao cliente e monitorar o desempenho do help desk junto com sua receita.

Conectar o [!DNL Zendesk] os dados são um processo simples de três etapas:

1. [Abra o [!DNL Zendesk] página de credenciais em [!DNL Commerce Intelligence]](#stepone)
1. [Recupere seu [!DNL Zendesk] Token de API](#steptwo)
1. [Insira seu [!DNL Zendesk] informações de logon e token no [!DNL Commerce Intelligence]](#stepthree)

Para concluir esse processo, é necessário abrir duas janelas ou guias do navegador - uma para [!DNL Commerce Intelligence], o outro para o [!DNL Zendesk] conta.

## Abra o [!DNL Zendesk] página de credenciais em [!DNL Commerce Intelligence] {#stepone}

1. Vá para a `Integrations` página abaixo **[!UICONTROL Manage Data** > ** Fontes de dados **> **Integrações]**.
1. Clique em **[!UICONTROL Add Integration]**, localizado no lado direito da tela.
1. Clique em [!DNL Zendesk] ícone. Isso abre o [!DNL Zendesk] página de credenciais.

## Recupere seu [!DNL Zendesk] Token de API {#steptwo}

1. Na janela/guia onde você está conectado no [!DNL Zendesk] clique no ícone Configurações (engrenagem) no canto inferior esquerdo da tela.
1. Quando a variável `Settings` for exibido, localize a variável `Channels` seção. Clique em **[!UICONTROL API]** nesta seção.
1. No `Token Access` desta página, clique na caixa de seleção ao lado de `Enabled`. Uma lista de Tokens de API ativos é exibida.
1. Clique em **[!UICONTROL Add New Token]**.
1. Quando solicitado, insira um rótulo para o token. O Adobe recomenda usar `Commerce Intelligence`, para que você saiba, rapidamente, qual aplicativo está usando o token.
1. Clique em **[!UICONTROL Create]**.
1. Um token de API é criado. Copie este token; ele será usado na próxima etapa.

## Enter [!DNL Zendesk] informações de logon e token de API em [!DNL Commerce Intelligence] {#stepthree}

1. Insira seu [!DNL Zendesk] prefixo do site e email de logon na [!DNL Zendesk] página de credenciais em [!DNL Commerce Intelligence].
1. Insira o token da API.
1. Clique em **[!UICONTROL Save & Connect]**. Se a conexão for bem-sucedida, uma variável *Conexão bem sucedida!* é exibida na parte superior da tela.

## Relacionados:

* [Esperado [!DNL Zendesk] dados](../integrations/exp-zendesk-data.md)
* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
