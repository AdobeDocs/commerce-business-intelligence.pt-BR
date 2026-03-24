---
title: Conectar Zendesk
description: Saiba como consolidar seus relatórios de suporte técnico no [!DNL Commerce Intelligence].
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/KBUuqTDD9s3qXDktcV3RzLx4zxtAFwAkKPbsQE2YGtI
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 261
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
1. [Recuperar o token de API  [!DNL Zendesk] &#x200B;](#steptwo)
1. [Insira suas  [!DNL Zendesk] informações de logon e o token em  [!DNL Commerce Intelligence]](#stepthree)

Para concluir esse processo, é necessário abrir duas janelas ou guias do navegador: uma para [!DNL Commerce Intelligence] e outra para sua conta do [!DNL Zendesk].

## Abrir a página de credenciais do [!DNL Zendesk] em [!DNL Commerce Intelligence] {#stepone}

1. Vá para a página `Integrations` em **[!UICONTROL Manage Data** > **&#x200B; Fontes de Dados &#x200B;**> **Integrações]**.
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
