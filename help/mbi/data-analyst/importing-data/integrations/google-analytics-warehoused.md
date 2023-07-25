---
title: Conectar Google Analytics Armazenados
description: Saiba como rastrear como os visitantes usam seu site, qual conteúdo é atraente, onde os visitantes saem e muito mais.
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# Conectar [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>Exige [Permissões de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] O é o serviço de análise da web mais usado na Internet. Implementação [!DNL Google Analytics] no seu site permite rastrear como os visitantes usam o site, qual conteúdo é atraente, onde os visitantes saem e muito mais. [!DNL Google Analytics Warehoused] O é uma integração separada do seu [!DNL Google Analytics] integração. Permite uma melhor análise devido à necessidade de [!DNL Google Analytics] dados na sua Data Warehouse, que é diferente do feed ativo do existente [!DNL Google Analytics] integração. Análise dessas métricas no [!DNL Commerce Intelligence], juntamente com outros dados, melhora a integridade e a usabilidade geral do site.

## Diferença entre GA Warehouse e Integração em tempo real

O principal diferencial é que uma integração é armazenada ([!DNL Google Analytics Warehoused]), e o outro não ([!DNL Google Analytics Live]). No caso de [!DNL Google Analytics Warehoused], isso permite a manipulação do [!DNL Google Analytics] dados e oferece a capacidade de combinar [!DNL Google Analytics] e outras fontes de dados para criar relatórios relevantes.

Examinar [!DNL Google Analytics] Adicione campanhas para obter um exemplo do que pode ser feito do ponto de vista da manipulação. Suponha que você tenha várias campanhas de anúncios para o quarto trimestre com nomes diferentes. As campanhas foram resultado de uma iniciativa de marketing específica. Com dados armazenados, você pode criar uma coluna que localize os nomes de campanha em questão e retorne o nome da iniciativa do quarto trimestre de `Operation Dumbo`.

O aspecto de combinação permite [!DNL Google Analytics] dados a serem unidos a outros dados para realizar análises. Por exemplo, considere `Total Time On Site By Ad Campaign` dados de [!DNL Google Analytics] e uni-lo contra `Total Spent Per Campaign` dados de [!DNL Facebook Ads] para obter uma visão completa de quanto o engajamento está custando a você.

Com o [!DNL Google Analytics Live] integração, por outro lado, cada [!DNL Google Analytics] O gráfico é como um pequeno silo que não é armazenado em sua Data Warehouse.

## Conectando [!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused] é um `Premium` Integração. [Entrar em contato com o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) se você tiver interesse em adicionar essa integração à sua assinatura.

1. Vá para a `Connections` página abaixo **[!UICONTROL Admin** > **Integrations]**.
1. Clique em **[!UICONTROL Add an Integration]**, localizado no lado direito.
1. Clique em [!DNL Google Analytics Warehoused] ícone. Isso abre o [!DNL Google Analytics] página de credenciais.
1. Insira seu [!DNL Google Analytics] credenciais. Após a conclusão do processo de autorização, você será redirecionado de volta para [!DNL Commerce Intelligence].
1. Uma lista de IDs de perfil é exibida. Marque os perfis aos quais deseja se conectar [!DNL Commerce Intelligence]. Se você tiver vários perfis e precisar de ajuda para identificar qual é qual, consulte o tópico sobre Conexão de vários [!DNL Google Analytics] seção de perfis abaixo.

## Conectando vários [!DNL Google Analytics] perfis

Você pode ter vários sites conectados a um único [!DNL Google Analytics] conta, identificada pelos seus próprios [!DNL Google Analytics] ID do perfil. Nesse caso, você tem a opção de incluir todas as IDs de perfil no [!DNL Commerce Intelligence]. Marque as IDs de perfil que você deseja incluir durante a etapa de seleção de perfil.

Para identificar o de um site específico [!DNL Google Analytics] ID do perfil:

1. Efetue logon no [!DNL Google Analytics]
1. Ir para o site específico [!DNL Google Analytics] painel
1. Examine o URL - a ID do perfil corresponde aos oito números seguintes `p` no final da linha

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Desconectando [!DNL Google Analytics Warehoused] de [!DNL Commerce Intelligence] {#disconnect}

1. Visite seu [!DNL Google Analytics] [configurações da conta](https://myaccount.google.com/intro) página.
1. No `Security` e clique em **[!UICONTROL edit]** ao lado de `Authorizing` aplicativos e sites.
1. Clique em **[!UICONTROL revoke access]** ao lado de [!DNL Commerce Intelligence].

## Documentação relacionada

* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Conectando [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Análise da atividade do site e das taxas de conversão do cliente](../../analysis/web-act-cust-conversion.md)
* [Rastrear dados de aquisição de usuário usando [!DNL Google Analytics] cookies](../../analysis/google-track-user-acq.md)
