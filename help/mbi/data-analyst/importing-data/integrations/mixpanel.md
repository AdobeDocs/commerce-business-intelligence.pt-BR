---
title: Conectar Mixpanel
description: Saiba como analisar como os usuários navegam e usam seus sites e aplicativos.
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: 'https://experienceleague.adobe.com/ap-nWiPVnPSpvUT4uiimZ7iC4fiuKvKH0ZMVkOTDcK8'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
  - id: 4d217dbe-2c9a-5839-94d7-471fd31623b7
    internal-label: Data Integration
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%
---
# Conectar [!DNL Mixpanel]

>[!NOTE]
>
>Requer [permissões de administrador](../../../administrator/user-management/user-management.md).

![Logotipo do Mixpanel](../../../assets/Mixpanel_logo.png)

Com o [!DNL Mixpanel], você pode analisar como os usuários navegam e usam seus sites e aplicativos. Analisar de perto os dados de comportamento do usuário leva a decisões de design e desenvolvimento mais inteligentes, o que significa um produto melhor em geral. Conectar [!DNL Mixpanel] a [!DNL Commerce Intelligence] permite que você analise como seus usuários se comportam e como esse comportamento se traduz em receita.

Conectando seus dados do [!DNL Mixpanel] ao [!DNL Commerce Intelligence] um processo simples de três etapas:

1. [Abrir a página  [!DNL Mixpanel] credenciais [!DNL Commerce Intelligence]](#stepone)
1. [Recupere suas credenciais de API do  [!DNL Mixpanel] &#x200B;](#steptwo)
1. [Insira suas  [!DNL Mixpanel] credenciais de API em  [!DNL Commerce Intelligence]](#stepthree)

Para concluir esse processo, é necessário abrir duas janelas ou guias do navegador, uma para [!DNL Commerce Intelligence] e outra para sua conta do [!DNL Mixpanel].

## Abrindo a página de credenciais do [!DNL Mixpanel] {#stepone}

Introdução:

1. Vá para a página `Connections` em **[!DNL Manage Data** > **Connections]**.

1. Clique em **[!UICONTROL Add a New Source]**, localizado no lado direito da tela acima da tabela `Data Sources`.

1. Clique no ícone [!DNL Mixpanel] e a página de credenciais será aberta.

Deixe esta página aberta por enquanto e alterne para a janela do navegador com sua conta do [!DNL Mixpanel].

## Recuperando suas credenciais de API do [!DNL Mixpanel] {#steptwo}

Se você ainda não fez logon na sua conta do [!DNL Mixpanel], faça isso e faça o seguinte:

1. Clique em **[!UICONTROL Account]** no canto superior direito.

1. No diálogo exibido, clique em **[!UICONTROL Projects]**.

1. Suas credenciais de API são exibidas:

![Recuperando credenciais de API do Mixpanel](../../../assets/Mixpanel_API_creds.png)

Mantenha isso aberto, você precisa para encerrar isso.

## Inserindo suas credenciais de API do [!DNL Mixpanel] em [!DNL Commerce Intelligence] {#stepthree}

1. Copie o `API Key` e `Secret` na página de credenciais [!DNL Mixpanel] em [!DNL Commerce Intelligence].
1. Clique em **[!UICONTROL Connect to Mixpanel]** para concluir a instalação.

Se a conexão for bem-sucedida, um _Sucesso!_ é exibida na parte superior da página.

### Relacionados

* [Dados  [!DNL Mixpanel]  esperados](../integrations/mixpanel-data.md)
* [Reautenticação de integrações](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations)
