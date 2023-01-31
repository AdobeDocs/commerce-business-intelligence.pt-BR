---
title: Conectar Google Analytics Warehouse
description: Saiba como os visitantes usam seu site, qual conteúdo é atraente, onde os visitantes saem e muito mais.
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---

# Connect [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>Exige [Permissões de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] O é o serviço de análise da Web mais usado na Internet. Implementação [!DNL Google Analytics] em seu site, você pode acompanhar como os visitantes usam seu site, qual conteúdo é atraente, onde os visitantes saem e muito mais. [!DNL Google Analytics Warehoused] é uma integração separada da existente [!DNL Google Analytics] integração. Isso permitirá uma melhor análise devido à [!DNL Google Analytics] dados na sua Data Warehouse, que é diferente do feed ao vivo do [!DNL Google Analytics] integração. Análise dessas métricas no [!DNL MBI], juntamente com outros dados, melhorarão a integridade e a usabilidade geral do site.

## Diferença entre o GA Warehouse e a integração ao vivo

O principal diferencial é que uma integração é armazenada ([!DNL Google Analytics Warehoused]) e o outro não é ([!DNL Google Analytics Live]). No caso de [!DNL Google Analytics Warehoused], isso permite a manipulação do [!DNL Google Analytics] e oferece a capacidade de combinar [!DNL Google Analytics] e outras fontes de dados para criar relatórios esclarecedores.

Vamos olhar para [!DNL Google Analytics] campanhas de publicidade para obter um exemplo do que pode ser feito de um ponto de vista de manipulação. Suponha que você tenha várias campanhas publicitárias para o quarto trimestre com nomes diferentes. As campanhas foram resultado de uma iniciativa de marketing específica. Com dados armazenados no , podemos criar uma nova coluna que localiza os nomes de campanha em questão e retorna o nome da iniciativa do T4 de `Operation Dumbo`.

O aspecto de combinação permite [!DNL Google Analytics] dados a juntar a outros dados para realizar análises. Por exemplo, considere `Total Time On Site By Ad Campaign` dados de [!DNL Google Analytics] e junte-se a isso `Total Spent Per Campaign` dados de [!DNL Facebook Ads] para obter uma imagem completa de quanto de envolvimento está lhe custando.

Com o [!DNL Google Analytics Live] integração, por outro lado, a cada [!DNL Google Analytics] é como um silo pequeno que não está armazenado em seu [!DNL MBI] data warehouse.

## Conexão [!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused] é um `Premium` Integração. [Entre em contato com o suporte](../../../guide-overview.md) se você tiver interesse em adicionar essa integração à sua assinatura.

1. Vá para o `Connections` página abaixo **[!UICONTROL Admin** > **Integrations]**.
1. Clique em **[!UICONTROL Add a Add Integration]**, localizado no lado direito da tela.
1. Clique no botão [!DNL Google Analytics Warehoused] ícone . Isso abrirá o [!DNL Google Analytics] credenciais.
1. Insira seu [!DNL Google Analytics] credenciais. Após a conclusão do processo de autorização, você será redirecionado para [!DNL MBI].
1. Uma lista de IDs de perfil será exibida. Verifique os perfis aos quais deseja se conectar [!DNL MBI]. Se você tiver vários perfis e precisar de ajuda para identificar qual, consulte Conexão de vários [!DNL Google Analytics] seção de perfis abaixo.

## Conexão múltipla [!DNL Google Analytics] perfis

Você pode ter vários sites conectados a um único [!DNL Google Analytics] , identificada por sua própria conta [!DNL Google Analytics] ID do perfil. Nesse caso, você terá a opção de incluir todas as IDs de perfil no [!DNL MBI]. Basta verificar as IDs de perfil que você deseja incluir durante a etapa de seleção de perfil.

Para identificar um site específico [!DNL Google Analytics] ID do perfil:

1. Faça logon [!DNL Google Analytics]
1. Vá para o site específico [!DNL Google Analytics] painel
1. Examine o URL - a ID de perfil corresponde aos 8 números que seguem `p` no final da linha

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Desconectar [!DNL Google Analytics Warehoused] from [!DNL MBI] {#disconnect}

1. Visite seu [!DNL Google Analytics] [configurações da conta](https://www.google.com/accounts/) página.
1. Em `Security` e clique em **[!UICONTROL edit]** ao lado de `Authorizing` aplicativos e sites.
1. Clique em **[!UICONTROL revoke access]** ao lado de [!DNL MBI].

## Documentação relacionada

* [Reautenticação de integrações](https://support.magento.com/hc/en-us/articles/360016733151)
* [Conexão [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Análise da atividade do site e das taxas de conversão do cliente](../../analysis/web-act-cust-conversion.md)
* [Rastrear dados de aquisição do usuário usando [!DNL Google Analytics] cookies](../../analysis/google-track-user-acq.md)
* [Rastrear os dados do dispositivo e do navegador do usuário usando [!DNL Google Analytics] cookies](https://support.magento.com/hc/en-us/articles/360016732911)
