---
title: Conectar o Google Analytics warehouse
description: Saiba como rastrear como os visitantes usam seu site, qual conteúdo é atraente, onde os visitantes saem e muito mais.
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/fmI-RG3Ba7s--6-Qve8xzcBLAKcbAqfaMAb7hNiKciU
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: ba9e5be9-7de1-4f71-a5d2-baead0e425eeid: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: c1579802-ddd4-4214-8a91-97b2066abe11id: d095671a-1355-40aa-8b5f-06c33c68080bid: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 489
ht-degree: 0%

---

# Conectar [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>Requer [permissões de administrador](../../../administrator/user-management/user-management.md).

![logotipo do Google Analytics](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] é o serviço de análise da web mais usado na Internet. A implementação do [!DNL Google Analytics] no seu site permite que você acompanhe como os visitantes usam o seu site, qual conteúdo é atraente, onde os visitantes saem e muito mais. O [!DNL Google Analytics Warehoused] é uma integração separada da sua integração existente do [!DNL Google Analytics]. Isso permite uma melhor análise devido aos dados do [!DNL Google Analytics] em sua Data Warehouse, que é diferente do feed ao vivo da integração existente do [!DNL Google Analytics]. A análise dessas métricas no [!DNL Commerce Intelligence], juntamente com outros dados, melhora a integridade e a usabilidade geral do site.

## Diferença entre GA Warehouse e Integração em tempo real

O principal diferencial é que uma integração é armazenada ([!DNL Google Analytics Warehoused]) e a outra não é ([!DNL Google Analytics Live]). No caso do [!DNL Google Analytics Warehoused], isso permite a manipulação de seus dados do [!DNL Google Analytics] e oferece a capacidade de combinar o [!DNL Google Analytics] e outras fontes de dados para criar relatórios bem-sucedidos.

Veja as campanhas de anúncios [!DNL Google Analytics] para ver um exemplo do que pode ser feito do ponto de vista da manipulação. Suponha que você tenha várias campanhas de anúncios para o quarto trimestre com nomes diferentes. As campanhas foram resultado de uma iniciativa de marketing específica. Com dados armazenados, você pode criar uma coluna que localize os nomes de campanha em questão e retorne o nome da iniciativa do quarto trimestre de `Operation Dumbo`.

O aspecto de combinação permite que dados [!DNL Google Analytics] sejam unidos a outros dados para realizar análises. Por exemplo, pegue os dados de `Total Time On Site By Ad Campaign` de [!DNL Google Analytics] e junte-os aos dados de `Total Spent Per Campaign` de [!DNL Facebook Ads] para obter uma visão completa de quanto o engajamento está lhe custando.

Por outro lado, com a integração do [!DNL Google Analytics Live], cada gráfico do [!DNL Google Analytics] é como um pequeno silo que não é armazenado no Data Warehouse.

## Conectando [!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused] é uma Integração de `Premium`. [Contate o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) se tiver interesse em adicionar essa integração à sua assinatura.

1. Vá para a página `Connections` em **[!UICONTROL Admin** > **Integrations]**.
1. Clique em **[!UICONTROL Add an Integration]**, localizado no lado direito.
1. Clique no ícone [!DNL Google Analytics Warehoused]. Isso abre a página de credenciais do [!DNL Google Analytics].
1. Insira suas credenciais do [!DNL Google Analytics]. Após a conclusão do processo de autorização, você será redirecionado de volta para [!DNL Commerce Intelligence].
1. Uma lista de IDs de perfil é exibida. Verifique os perfis aos quais você deseja se conectar [!DNL Commerce Intelligence]. Se você tiver vários perfis e precisar de ajuda para identificar qual é qual, consulte a seção Conectando Vários Perfis [!DNL Google Analytics] abaixo.

## Conectando vários perfis [!DNL Google Analytics]

Você pode ter vários sites conectados a uma única conta do [!DNL Google Analytics], identificados pela própria ID de perfil do [!DNL Google Analytics]. Nesse caso, você tem a opção de incluir todas as IDs de perfil em [!DNL Commerce Intelligence]. Marque as IDs de perfil que você deseja incluir durante a etapa de seleção de perfil.

Para identificar a ID de perfil do [!DNL Google Analytics] de um site específico:

1. Fazer logon em [!DNL Google Analytics]
1. Ir para o painel do site específico [!DNL Google Analytics]
1. Examine a URL - a ID do Perfil corresponde aos oito números que seguem `p` no final da linha

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Desconectando [!DNL Google Analytics Warehoused] de [!DNL Commerce Intelligence] {#disconnect}

1. Visite a página [!DNL Google Analytics] [configurações da conta](https://myaccount.google.com/intro).
1. Na seção `Security` e clique em **[!UICONTROL edit]** ao lado de `Authorizing` aplicativos e sites.
1. Clique em **[!UICONTROL revoke access]** ao lado de [!DNL Commerce Intelligence].

## Documentação relacionada

* [Reautenticando integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Conectando [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Análise da atividade do site e das taxas de conversão do cliente](../../analysis/web-act-cust-conversion.md)
* [Rastrear dados de aquisição de usuário usando  [!DNL Google Analytics] cookies](../../analysis/google-track-user-acq.md)
