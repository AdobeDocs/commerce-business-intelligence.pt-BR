---
title: Conectar o Stripe
description: Saiba como gerenciar e rastrear os dados de pagamento e fatura de sua empresa.
exl-id: c038f2a9-b2bd-4e45-93f9-12d2e5077b31
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/S6-otAlCeS8aKQ6K-xZH2ZaqEjZ-ZZ6fMWXtFFafu6c
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 151
ht-degree: 0%

---

# Conectar [!DNL Stripe]

>[!NOTE]
>
>Requer [permissões de administrador](../../../administrator/user-management/user-management.md).

![logotipo do Stripe](../../../assets/stripe-logo.png)

O [!DNL Stripe] permite gerenciar e controlar os dados de pagamento e fatura da sua empresa. A conexão da conta do [!DNL Stripe] com o [!DNL Commerce Intelligence] é um processo simples de duas etapas:

1. [Adicionar [!DNL Stripe] como uma fonte de dados em [!DNL Commerce Intelligence]](#stepone)
1. [Permitir [!DNL Commerce Intelligence] acesso aos seus [!DNL Stripe] Dados](#steptwo)

## Adicionar [!DNL Stripe] como uma fonte de dados {#stepone}

1. Vá para a página `Connections` em **[!UICONTROL Admin** > **Connections]**.
1. Clique em **[!UICONTROL Add a Data Source]**, localizado no lado direito da tela acima da tabela `Data Sources`.
1. Clique no ícone [!DNL Stripe]. Isso exibe a página `[!DNL Stripe] authorization`.
1. Clique em **[!UICONTROL Connect with Stripe]**.

## Permitir que [!DNL Commerce Intelligence] acesse seus dados de [!DNL Stripe] {#steptwo}

Depois de clicar em **[!UICONTROL Connect with Stripe]**, uma página de solicitação de acesso é exibida.

1. Clique em **[!UICONTROL Sign in with Stripe to Continue]**.

1. Insira suas credenciais e clique em **[!UICONTROL Sign in to your account]**.

1. Suas credenciais serão validadas e você será direcionado de volta a [!DNL Commerce Intelligence].

1. Se a conexão for bem-sucedida, uma *Conexão bem-sucedida!* mensagem aparece na parte superior da tela.

## Relacionados:

A [[!DNL Stripe] Documentação da API](https://stripe.com/docs/api) pode ser um recurso útil para saber mais sobre como o [!DNL Stripe] é integrado ao [!DNL Commerce Intelligence].

* [Dados  [!DNL Stripe]  esperados](../integrations/stripe-data.md)
* [Reautenticando integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
