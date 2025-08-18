---
title: Conectar o Google Analytics
description: Saiba como conectar o Google Analytics ao  [!DNL Commerce Intelligence].
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# Conectar [!DNL Google Analytics]

>[!NOTE]
>
>Requer [permissões de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] é o serviço de análise da web mais usado na Internet. A implementação do [!DNL Google Analytics] no seu site permite que você acompanhe como os visitantes usam o seu site, qual conteúdo é atraente, onde os visitantes saem e muito mais. A análise dessas métricas no [!DNL Commerce Intelligence], juntamente com outros dados, melhora a integridade e a usabilidade geral do site.

Comece digitando suas credenciais do [!DNL Google Analytics] em [!DNL Commerce Intelligence]:

1. Ir para **[!UICONTROL Manage Data** > **Integrations]**.

1. Clique em **[!UICONTROL Add Integration]**, localizado no lado direito da tela.

1. Clique no ícone [!DNL Google Analytics]. Isso abre a página de credenciais do [!DNL Google Analytics].

1. Insira suas credenciais do [!DNL Google Analytics]. Ao concluir o processo de autorização, você será redirecionado de volta para [!DNL Commerce Intelligence].

1. Uma lista de IDs de perfil é exibida. Verifique os perfis aos quais você deseja se conectar [!DNL Commerce Intelligence]. Se você tiver vários perfis e precisar de ajuda para identificar qual é qual, consulte a seção Conectando Vários Perfis [!DNL Google Analytics] abaixo.

   ![](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

1. As alterações são salvas automaticamente, portanto, clique em **Voltar às Conexões** quando terminar.

## Conectando vários perfis [!DNL Google Analytics]

Você pode ter vários sites conectados a uma única conta do [!DNL Google Analytics], identificados pela própria ID de perfil do [!DNL Google Analytics]. Nesse caso, você tem a opção de incluir todas as IDs de perfil em [!DNL Commerce Intelligence]. Marque as IDs de perfil que você deseja incluir durante a etapa de seleção de perfil.

Para identificar a ID de perfil do [!DNL Google Analytics] de um site específico:

1. Fazer logon em [!DNL Google Analytics]
1. Ir para o painel do site específico [!DNL Google Analytics]
1. Examine a URL - a ID do Perfil corresponde aos oito números que seguem `p` no final da linha:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Desconectando [!DNL Google Analytics] de [!DNL Commerce Intelligence] {#disconnect}

1. Visite a página [!DNL Google Analytics] [configurações da conta](https://accounts.google.com/).
1. Na seção `Security` e clique em **[!UICONTROL edit]** ao lado de `Authorizing` aplicativos e sites.
1. Clique em **[!UICONTROL revoke access]** ao lado de [!DNL Commerce Intelligence].

## Relacionados:

* [Reautenticando integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Conectando [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Análise da atividade do site e das taxas de conversão do cliente](../../analysis/web-act-cust-conversion.md)
* [Rastrear dados de aquisição de usuário usando  [!DNL Google Analytics] cookies](../../analysis/google-track-user-acq.md)
