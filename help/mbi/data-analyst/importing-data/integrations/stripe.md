---
title: Conectar o Stripe
description: Saiba como gerenciar e rastrear os dados de pagamento e fatura de sua empresa.
exl-id: c038f2a9-b2bd-4e45-93f9-12d2e5077b31
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '151'
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
* [Reautenticando integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=pt-BR)
