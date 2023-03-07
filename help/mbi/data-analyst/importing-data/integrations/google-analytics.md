---
title: Conectar o Google Analytics
description: Saiba como conectar o Google Analytics com [!DNL MBI].
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
source-git-commit: 8de036e2717aedef95a8bb908898fd9b9bc9c3fa
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Conectar [!DNL Google Analytics]

>[!NOTE]
>
>Exige [Permissões de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] O é o serviço de análise da web mais usado na Internet. Implementação [!DNL Google Analytics] no seu site permite rastrear como os visitantes usam o site, qual conteúdo é atraente, onde os visitantes saem e muito mais. Análise dessas métricas no [!DNL MBI], juntamente com outros dados, melhora a integridade e a usabilidade geral do site.

Comece digitando seu [!DNL Google Analytics] credenciais para [!DNL MBI]:

1. Vá para a **[!UICONTROL Manage Data** > **Integrations]** página.
1. Clique em **[!UICONTROL Add Integration]**, localizado no lado direito da tela.
1. Clique em [!DNL Google Analytics] ícone. Isso abre o [!DNL Google Analytics] página de credenciais.
1. Insira seu [!DNL Google Analytics] credenciais. Ao concluir o processo de autorização, você será redirecionado de volta para [!DNL MBI].
1. Uma lista de IDs de perfil é exibida. Marque os perfis aos quais deseja se conectar [!DNL MBI]. Se você tiver vários perfis e precisar de ajuda para identificar qual é qual, consulte o tópico sobre Conexão de vários [!DNL Google Analytics] seção de perfis abaixo.

   ![](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

1. As alterações são salvas automaticamente, portanto, clique em **Voltar para Conexões** quando terminar.

## Conectando vários [!DNL Google Analytics] perfis

Você pode ter vários sites conectados a um único [!DNL Google Analytics] conta, identificada pelos seus próprios [!DNL Google Analytics] ID do perfil. Nesse caso, você tem a opção de incluir todas as IDs de perfil no [!DNL MBI]. Marque as IDs de perfil que você deseja incluir durante a etapa de seleção de perfil.

Para identificar o de um site específico [!DNL Google Analytics] ID do perfil:

1. Efetue logon no [!DNL Google Analytics]
1. Ir para o site específico [!DNL Google Analytics] painel
1. Examine o URL - a ID do perfil corresponde aos oito números seguintes `p` no final da linha:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Desconectando [!DNL Google Analytics] de [!DNL MBI] {#disconnect}

1. Visite seu [!DNL Google Analytics] [configurações da conta](https://accounts.google.com/) página.
1. No `Security` e clique em **[!UICONTROL edit]** ao lado de `Authorizing` aplicativos e sites.
1. Clique em **[!UICONTROL revoke access]** ao lado de [!DNL MBI].

## Relacionados:

* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
* [Conectando [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Análise da atividade do site e das taxas de conversão do cliente](../../analysis/web-act-cust-conversion.md)
* [Rastrear dados de aquisição de usuário usando [!DNL Google Analytics] cookies](../../analysis/google-track-user-acq.md)
