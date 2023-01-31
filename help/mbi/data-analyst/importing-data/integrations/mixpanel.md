---
title: Conectar painel misto
description: Saiba como analisar como os usuários navegam e utilizam seus sites e aplicativos.
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Connect [!DNL Mixpanel]

>[!NOTE]
>
>Exige [Permissões de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/Mixpanel_logo.png)

Com [!DNL Mixpanel], é possível analisar como os usuários navegam e utilizam seus sites e aplicativos. Analisar os dados de comportamento do usuário leva a decisões mais inteligentes de design e desenvolvimento, o que significa um produto melhor em geral. Conexão [!DNL Mixpanel] para [!DNL MBI] permite analisar como seus usuários se comportam e como esse comportamento se traduz na receita.

Conectar seu [!DNL Mixpanel] para [!DNL MBI] um processo simples em três etapas:

1. [Abra o [!DNL Mixpanel] página credenciais em [!DNL MBI]](#stepone)
1. [Recupere seu [!DNL Mixpanel] Credenciais da API](#steptwo)
1. [Insira seu [!DNL Mixpanel] Credenciais da API no MBI](#stepthree)

Para concluir esse processo, você precisará abrir duas janelas ou guias do navegador - uma para [!DNL MBI], o outro para o seu [!DNL Mixpanel] conta.

## Abrir o [!DNL Mixpanel] página credenciais {#stepone}

Vamos começar:

1. Vá para o `Connections` página abaixo **[!DNL Manage Data** > **Connections]**.
1. Clique em **[!UICONTROL Add a New Source]**, localizado no lado direito do ecrã acima da `Data Sources` tabela.
1. Clique no botão [!DNL Mixpanel] e a página de credenciais será aberta.

Deixe essa página aberta por enquanto e alterne para a janela do navegador com seu [!DNL Mixpanel] conta.

## Recuperar seu [!DNL Mixpanel] Credenciais da API {#steptwo}

Se você não tiver feito logon no [!DNL Mixpanel] ainda assim, faça isso e faça o seguinte:

1. Clique em **[!UICONTROL Account]** no canto superior direito.
1. Na caixa de diálogo exibida, clique em **[!UICONTROL Projects]**.
1. As credenciais da API exibirão:

![Recuperar credenciais da API do Mixpanel](../../../assets/Mixpanel_API_creds.png)

Mantenha isto aberto - precisamos que termine isto.

## Inserir seu [!DNL Mixpanel] Credenciais da API em [!DNL MBI] {#stepthree}

1. Copie o `API Key` e `Secret` na [!DNL Mixpanel] página credenciais em [!DNL MBI].
1. Clique em **[!UICONTROL Connect to Mixpanel]** para concluir a configuração.

Pronto! Se a conexão for bem-sucedida, uma _Sucesso!_ será exibida na parte superior da página.

### Relacionado

* [Esperado [!DNL Mixpanel] dados](../integrations/mixpanel-data.md)
* [Reautenticação de integrações](https://support.magento.com/hc/en-us/articles/360016733151)
