---
title: Conectar o Google Analytics
description: Saiba como conectar o Google Analytics ao  [!DNL Commerce Intelligence].
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/wSR5SWYSfmNZkzp5QxTUwv6QSsynXYofmRkKbvMsohs
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 283
ht-degree: 0%

---

# Conectar [!DNL Google Analytics]

>[!NOTE]
>
>Requer [permissões de administrador](../../../administrator/user-management/user-management.md).

![logotipo do Google Analytics](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] é o serviço de análise da web mais usado na Internet. A implementação do [!DNL Google Analytics] no seu site permite que você acompanhe como os visitantes usam o seu site, qual conteúdo é atraente, onde os visitantes saem e muito mais. A análise dessas métricas no [!DNL Commerce Intelligence], juntamente com outros dados, melhora a integridade e a usabilidade geral do site.

Comece digitando suas credenciais do [!DNL Google Analytics] em [!DNL Commerce Intelligence]:

1. Ir para **[!UICONTROL Manage Data** > **Integrations]**.

1. Clique em **[!UICONTROL Add Integration]**, localizado no lado direito da tela.

1. Clique no ícone [!DNL Google Analytics]. Isso abre a página de credenciais do [!DNL Google Analytics].

1. Insira suas credenciais do [!DNL Google Analytics]. Ao concluir o processo de autorização, você será redirecionado de volta para [!DNL Commerce Intelligence].

1. Uma lista de IDs de perfil é exibida. Verifique os perfis aos quais você deseja se conectar [!DNL Commerce Intelligence]. Se você tiver vários perfis e precisar de ajuda para identificar qual é qual, consulte a seção Conectando Vários Perfis [!DNL Google Analytics] abaixo.

   ![Página de administrador do Google Analytics mostrando a ID do perfil na URL](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

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
