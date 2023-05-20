---
title: Conectar Google Analytics
description: Aprenda a se conectar Google Analytics com  [!DNL Commerce Intelligence] o.
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Conectar [!DNL Google Analytics]

>[!NOTE]
>
>Requer [ permissões ](../../../administrator/user-management/user-management.md) de administrador.

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] é o serviço de análise da web mais amplamente usado na Internet. A implementação [!DNL Google Analytics] em seu site permite faixa como os visitantes usam o site, o que conteúdo é atraente, onde os visitantes saem e muito mais. A análise dessas métricas em [!DNL Commerce Intelligence] , juntamente com outras partes de dados, melhora a integridade e a usabilidade geral do site.

Comece inserindo suas [!DNL Google Analytics] credenciais em [!DNL Commerce Intelligence] :

1. Vá para **[!UICONTROL Manage Data** > **Integrations]** .

1. Clique **[!UICONTROL Add Integration]** em, localizado no lado direito da tela.

1. Clique no [!DNL Google Analytics] ícone. Isso abre as [!DNL Google Analytics] credenciais página.

1. Insira suas [!DNL Google Analytics] credenciais. Ao concluir o processo de autorização, você é redirecionado para [!DNL Commerce Intelligence] .

1. Uma lista de perfil IDs é exibida. Verifique os perfis aos [!DNL Commerce Intelligence] quais você deseja se conectar. Se você tiver vários perfis e precisar de ajuda para identificar qual deles, consulte a seção conectando vários [!DNL Google Analytics] perfis abaixo.

   ![](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

1. As alterações são salvas automaticamente, portanto, clique em **anterior para conexões** quando você terminar.

## Conexão de vários [!DNL Google Analytics] perfis

Você pode ter vários sites conectados a uma única [!DNL Google Analytics] conta, identificados por sua própria [!DNL Google Analytics] ID de perfil. Nesse caso, você tem a opção de incluir todas as suas perfil IDs no [!DNL Commerce Intelligence] . Verifique os perfil IDs que você curtir para incluir durante a etapa de seleção de perfil.

Para identificar a ID de perfil de [!DNL Google Analytics] um site específico:

1. Faça logon em [!DNL Google Analytics]
1. Vá para a painel do [!DNL Google Analytics] site específico
1. Look na URL-a ID do perfil corresponde aos oito números após `p` o final da linha:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Desconectar-se [!DNL Google Analytics] de [!DNL Commerce Intelligence] {#disconnect}

1. Visite as configurações ](https://accounts.google.com/) do [!DNL Google Analytics] [ conta página.
1. `Security`Na seção e clique em **[!UICONTROL edit]** próximo a `Authorizing` aplicativos e sites.
1. Clique em **[!UICONTROL revoke access]** próximo a [!DNL Commerce Intelligence] .

## Relacionadas:

* [Reautenticando integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Conectar [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Análise de atividade de site e taxas de conversão do cliente](../../analysis/web-act-cust-conversion.md)
* [Rastrear usuário atração dados usando  [!DNL Google Analytics]  cookies](../../analysis/google-track-user-acq.md)
