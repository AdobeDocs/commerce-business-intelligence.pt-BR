---
title: Conectar Google Analytics Armazenados
description: Saiba como rastrear como os visitantes usam seu site, qual conteúdo é atraente, onde os visitantes saem e muito mais.
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# Conectar [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>Requer [ permissões ](../../../administrator/user-management/user-management.md) de administrador.

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] é o serviço de análise da web mais amplamente usado na Internet. A implementação [!DNL Google Analytics] em seu site permite faixa como os visitantes usam o site, o que conteúdo é atraente, onde os visitantes saem e muito mais. [!DNL Google Analytics Warehoused] é uma integração separada da integração existente [!DNL Google Analytics] . Isso permite um melhor análise devido à existência dos [!DNL Google Analytics] dados no data warehouse, que é diferente do feed ao vivo da integração existente [!DNL Google Analytics] . A análise dessas métricas em [!DNL Commerce Intelligence] , juntamente com outras partes de dados, melhora a integridade e a usabilidade geral do site.

## Diferença entre a integração do GA em depósito e ao vivo

O principal diferencial é que uma integração é armazenada ([!DNL Google Analytics Warehoused]), e o outro não ([!DNL Google Analytics Live]). No caso de [!DNL Google Analytics Warehoused], isso permite a manipulação do [!DNL Google Analytics] dados e oferece a capacidade de combinar [!DNL Google Analytics] e outras fontes de dados para criar relatórios relevantes.

Examinar [!DNL Google Analytics] Adicione campanhas para obter um exemplo do que pode ser feito do ponto de vista da manipulação. Suponha que você tenha várias campanhas de anúncios para o quarto trimestre com nomes diferentes. As campanhas foram resultado de uma iniciativa de marketing específica. Com dados armazenados, você pode criar uma coluna que localize os nomes de campanha em questão e retorne o nome da iniciativa do quarto trimestre de `Operation Dumbo`.

O aspecto de combinação permite [!DNL Google Analytics] dados a serem unidos a outros dados para realizar análises. Por exemplo, use `Total Time On Site By Ad Campaign` dados de [!DNL Google Analytics] e Junte-se a eles `Total Spent Per Campaign` a partir de [!DNL Facebook Ads] dados para obter uma imagem completa do quanto envolvimento está demorando.

Com a [!DNL Google Analytics Live] integração por outro lado, todos [!DNL Google Analytics] os gráficos são curtir um pequeno silo que não está armazenado em seu data warehouse.

## Conectar [!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused] é uma `Premium` integração. [Entre em contato com o suporte ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) se tiver uma interesse de adicionar essa integração à sua assinatura.

1. Vá para o `Connections` página em **[!UICONTROL Admin** > **Integrations]** .
1. Clique em **[!UICONTROL Add an Integration]**, localizado no lado direito.
1. Clique em [!DNL Google Analytics Warehoused] ícone. Isso abre o [!DNL Google Analytics] página de credenciais.
1. Insira seu [!DNL Google Analytics] credenciais. Após a conclusão do processo de autorização, você será redirecionado de volta para [!DNL Commerce Intelligence].
1. Uma lista de IDs de perfil é exibida. Marque os perfis aos quais deseja se conectar [!DNL Commerce Intelligence]. Se você tiver vários perfis e precisar de ajuda para identificar qual é qual, consulte o tópico sobre Conexão de vários [!DNL Google Analytics] seção de perfis abaixo.

## Conexão de vários [!DNL Google Analytics] perfis

Você pode ter vários sites conectados a uma única [!DNL Google Analytics] conta, identificados por sua própria [!DNL Google Analytics] ID de perfil. Nesse caso, você tem a opção de incluir todas as suas perfil IDs no [!DNL Commerce Intelligence] . Verifique os perfil IDs que você curtir para incluir durante a etapa de seleção de perfil.

Para identificar a ID de perfil de [!DNL Google Analytics] um site específico:

1. Faça logon em [!DNL Google Analytics]
1. Ir para o site específico [!DNL Google Analytics] painel
1. Examine o URL - a ID do perfil corresponde aos oito números seguintes `p` no final da linha

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Desconectando [!DNL Google Analytics Warehoused] de [!DNL Commerce Intelligence] {#disconnect}

1. Visite seu [!DNL Google Analytics] [configurações da conta](https://myaccount.google.com/intro) página.
1. No `Security` e clique em **[!UICONTROL edit]** ao lado de `Authorizing` aplicativos e sites.
1. Clique em **[!UICONTROL revoke access]** ao lado de [!DNL Commerce Intelligence].

## Documentação relacionada

* [Reautenticando integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Conectar [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Análise de atividade de site e taxas de conversão do cliente](../../analysis/web-act-cust-conversion.md)
* [Rastrear usuário atração dados usando  [!DNL Google Analytics]  cookies](../../analysis/google-track-user-acq.md)
