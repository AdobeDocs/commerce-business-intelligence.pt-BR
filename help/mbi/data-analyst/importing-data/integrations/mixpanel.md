---
title: Conectar Mixpanel
description: Saiba como analisar como os usuários navegam e usam seus sites e aplicativos.
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# Conectar [!DNL Mixpanel]

>[!NOTE]
>
>Exige [Permissões de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/Mixpanel_logo.png)

Com [!DNL Mixpanel], você pode analisar como os usuários navegam e usam seus sites e aplicativos. Analisar de perto os dados de comportamento do usuário leva a decisões de design e desenvolvimento mais inteligentes, o que significa um produto melhor em geral. Conectando [!DNL Mixpanel] para [!DNL Commerce Intelligence] O permite analisar como seus usuários se comportam e como esse comportamento se traduz na receita.

Conectar o [!DNL Mixpanel] dados para [!DNL Commerce Intelligence] um processo simples de três etapas:

1. [Abra o [!DNL Mixpanel] página de credenciais em [!DNL Commerce Intelligence]](#stepone)
1. [Recupere seu [!DNL Mixpanel] Credenciais da API](#steptwo)
1. [Insira seu [!DNL Mixpanel] Credenciais da API em [!DNL Commerce Intelligence]](#stepthree)

Para concluir esse processo, é necessário abrir duas janelas ou guias do navegador, uma para [!DNL Commerce Intelligence] e o outro para o seu [!DNL Mixpanel] conta.

## Abrir o [!DNL Mixpanel] página credenciais {#stepone}

Introdução:

1. Vá para a `Connections` página abaixo **[!DNL Manage Data** > **Connections]**.

1. Clique em **[!UICONTROL Add a New Source]**, localizado no lado direito da tela acima da `Data Sources` tabela.

1. Clique em [!DNL Mixpanel] e a página de credenciais será aberta.

Deixe esta página aberta por enquanto e alterne para a janela do navegador com [!DNL Mixpanel] conta.

## Recuperação de [!DNL Mixpanel] Credenciais da API {#steptwo}

Se você não tiver feito logon na [!DNL Mixpanel] conta ainda, faça isso e faça o seguinte:

1. Clique em **[!UICONTROL Account]** no canto superior direito.

1. Na caixa de diálogo exibida, clique em **[!UICONTROL Projects]**.

1. Suas credenciais de API são exibidas:

![Recuperação de credenciais da API do Mixpanel](../../../assets/Mixpanel_API_creds.png)

Mantenha isso aberto, você precisa para encerrar isso.

## Inserir seu [!DNL Mixpanel] Credenciais da API em [!DNL Commerce Intelligence] {#stepthree}

1. Copie o `API Key` e `Secret` no [!DNL Mixpanel] página de credenciais em [!DNL Commerce Intelligence].
1. Clique em **[!UICONTROL Connect to Mixpanel]** para concluir a configuração.

Se a conexão for bem-sucedida, uma variável _Sucesso!_ é exibida na parte superior da página.

### Relacionados

* [Esperado [!DNL Mixpanel] dados](../integrations/mixpanel-data.md)
* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
