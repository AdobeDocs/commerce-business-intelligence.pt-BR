---
title: Conectar Google Analytics
description: Saiba como conectar o Google Analytics com [!DNL MBI].
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# Connect [!DNL Google Analytics]

>[!NOTE]
>
>Exige [Permissões de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] O é o serviço de análise da Web mais usado na Internet. Implementação [!DNL Google Analytics] em seu site, você pode acompanhar como os visitantes usam seu site, qual conteúdo é atraente, onde os visitantes saem e muito mais. Análise dessas métricas no [!DNL MBI], juntamente com outros dados, melhorarão a integridade e a usabilidade geral do site.

Vamos começar entrando em nosso [!DNL Google Analytics] credenciais em [!DNL MBI]:

1. Vá para o **[!UICONTROL Manage Data** > **Integrations]** página.
1. Clique em **[!UICONTROL Add Integration]**, localizado no lado direito da tela.
1. Clique no botão [!DNL Google Analytics] ícone . Isso abrirá o [!DNL Google Analytics] credenciais.
1. Insira seu [!DNL Google Analytics] credenciais. Ao concluir o processo de autorização, você será redirecionado para [!DNL MBI].
1. Uma lista de IDs de perfil será exibida. Verifique os perfis aos quais deseja se conectar [!DNL MBI]. Se você tiver vários perfis e precisar de ajuda para identificar qual, consulte Conexão de vários [!DNL Google Analytics] seção de perfis abaixo.

   ![](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

1. As alterações são salvas automaticamente, portanto, clique em **Voltar para Conexões** quando terminar.

## Conexão múltipla [!DNL Google Analytics] perfis

Você pode ter vários sites conectados a um único [!DNL Google Analytics] , identificada por sua própria conta [!DNL Google Analytics] ID do perfil. Nesse caso, você terá a opção de incluir todas as IDs de perfil no [!DNL MBI]. Basta verificar as IDs de perfil que você deseja incluir durante a etapa de seleção de perfil.

Para identificar um site específico [!DNL Google Analytics] ID do perfil:

1. Faça logon [!DNL Google Analytics]
1. Vá para o site específico [!DNL Google Analytics] painel
1. Examine o URL - a ID de perfil corresponde aos 8 números que seguem `p` no final da linha:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Desconectar [!DNL Google Analytics] from [!DNL MBI] {#disconnect}

1. Visite seu [!DNL Google Analytics] [configurações da conta](https://www.google.com/accounts/) página.
1. Em `Security` e clique em **[!UICONTROL edit]** ao lado de `Authorizing` aplicativos e sites.
1. Clique em **[!UICONTROL revoke access]** ao lado de [!DNL MBI].

## Relacionadas:

* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
* [Conexão [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Análise da atividade do site e das taxas de conversão do cliente](../../analysis/web-act-cust-conversion.md)
* [Rastrear dados de aquisição do usuário usando [!DNL Google Analytics] cookies](../../analysis/google-track-user-acq.md)
