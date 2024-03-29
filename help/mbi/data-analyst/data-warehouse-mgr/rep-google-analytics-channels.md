---
title: Replicação de canais do Google Analytics usando fontes de aquisição
description: Saiba como replicar canais do Google Analytics usando fontes de aquisição.
exl-id: e7248fe4-94db-4cdf-8f58-1f65061a207d
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 0%

---

# [!DNL Google Analytics] uso de Fontes de aquisição

## O que são canais? {#channels}

Criar segmentos personalizados para ver como diferentes tráfegos funcionam e observar tendências é um dos usos mais eficientes do [!DNL Google Analytics]. Uma classe de segmentos que existe por padrão no [!DNL Google Analytics] são `Channels`. Os canais são um agrupamento de maneiras comuns de as pessoas acessarem o site.  [!DNL Google Analytics] O classifica automaticamente as várias maneiras de adquirir um usuário (redes sociais, pay-per-click, email ou links de referência) e os agrupa em um bucket ou canal.

## Por que não vejo meu `channels` no Commerce Intelligence? {#nochannels}

`Channels` são compartimentos de dados simples e agregados. Para classificar as aquisições em compartimentos de canal, [!DNL Google] O define regras e definições distintas usando parâmetros específicos: uma combinação de aquisição [Origem](https://support.google.com/analytics/answer/1033173?hl=en) (a origem do seu tráfego) e aquisição [Medium](https://support.google.com/analytics/answer/6099206?hl=en) (a categoria geral da fonte).

Embora ter esses buckets possa ajudar a entender de onde seu tráfego vem, esses dados não são marcados por canal, mas por uma combinação de Origem e Meio. Porque [!DNL Google] O envia informações do canal como dois pontos de dados separados. Os agrupamentos de canal não são exibidos automaticamente no [!DNL Commerce Intelligence].

## Quais são os agrupamentos de canal padrão? Como eles são criados?

Por padrão, [!DNL Google] O configura oito canais diferentes. As regras que determinam como os canais são criados estão abaixo.

| **Canal** | **O que é?** | **Como ele é criado?** |
|---|---|---|
| Direto | Qualquer pessoa que entre diretamente no seu site. | Origem = `Direct`<br>E Médio = `(not set); OR Medium = (none)` |
| Pesquisa orgânica | Tráfego que foi classificado organicamente em mecanismos de pesquisa não pagos. | Médio = `organic` |
| Referência | Tráfego que vem de um link externo que não é Pesquisa orgânica ou de sites que não são redes sociais. | Médio = `referral` |
| Pesquisa paga | Tráfego que tem um Código de rastreamento UTM em que a mídia é &quot;cpc&quot;, &quot;ppc&quot; ou &quot;paidsearch&quot; E é uma rede de distribuição de anúncios que não corresponde a &quot;Conteúdo&quot;. | Médio = `^(cpc|ppc|paidsearch)$`<br>AND Rede de distribuição de anúncios ≠ `Content` |
| Social | Tráfego de referência que vem de qualquer um de aproximadamente [400 redes sociais](https://www.annielytics.com/blog/analytics/sites-google-analytics-includes-in-social-reports/) e não são marcados como anúncios. | Referência de origem social = `Yes`<br>OU Médio = `^(social|social-network|social-media|sm|social network|social media)$` |
| E-mail | Tráfego de sessões que são marcadas com uma mídia de &quot;email&quot;. | Código de rastreamento UTM de Médio = `email` |
| Exibir | Tráfego que tem um Código de rastreamento UTM em que a mídia é exibição ou cpm. Também inclui a interação do AdWords em que a rede de distribuição de anúncios corresponde a &quot;Conteúdo&quot; | Médio = `^(display|cpm|banner)$`<br>OU Rede de distribuição de anúncios = `Content`<br>E Formato Ad ≠ `Text` |
| Outro | Sessões de outros canais de publicidade (sem incluir Pesquisa paga) marcadas com uma mídia &quot;cpc&quot;, &quot;ppc&quot;, &quot;cpm&quot;, &quot;cpv&quot;, &quot;cpa&quot;, &quot;cpp&quot;, &quot;afiliate&quot;. | Médio = `^(cpv|cpa|cpp|content-text)$` |

{style="table-layout:auto"}

## Como posso recriar esses agrupamentos de canais na minha Data Warehouse? {#recreate}

Agora que você sabe que os canais são apenas combinações de fontes e meios, é fácil executar o processo de 3 etapas para recriar esses agrupamentos na Data Warehouse.

1. **Ativar o[!DNL Google ECommerce]integração**

   [Quando ativado](../importing-data/integrations/google-ecommerce.md), verifique se [sincronizar](../{{ site.baseurl }}/data-analyst/data-warehouse-mgr/tour-dwm.html#syncing) o **médio** e **origem** campos na Data Warehouse. Após concluir, os dados de aquisição de mídia e fonte serão trazidos para a Data Warehouse.

1. **Fazer upload de um mapeamento dos agrupamentos de canal do Google**

   O Adobe Commerce cria uma tabela com os agrupamentos padrão mapeados como um arquivo que você pode [baixar](../../assets/ga-channel-mapping.csv).

   Se você é um [!DNL Google Analytics] pro e criou seus próprios canais, é necessário adicionar regras específicas à tabela de mapeamento antes de fazer upload do arquivo no [!DNL Commerce Intelligence].

   Traga-o para sua Data Warehouse como um [Upload de arquivo](../importing-data/connecting-data/using-file-uploader.md).

   ![](../../assets/Setting_Primary_Keys.png)

1. **Estabelecer uma relação entre[!DNL Google ECommerce]Upload do arquivo de mapeamento e**

   Para estabelecer uma relação entre a[!DNL Google ECommerce] e a tabela de mapeamento, [enviar uma solicitação de suporte](../../guide-overview.md#Submitting-a-Support-Ticket) à sua equipe de Data Analyst e referencie este tópico. O analista cria uma nova coluna calculada chamada **Canal** na tabela ECommerce. **Após um ciclo completo de atualização**, esta coluna estará pronta para uso em um `Filter` ou `Group by`.

Agora você tem [!DNL Google Analytics Channel] agrupamentos na Data Warehouse, o que significa que você pode analisar seus dados de uma nova perspectiva:

![Segmentação da métrica Número de pedidos por canal](../../assets/GA_Channel_Gif.gif)

Neste exemplo, você começou simples com a segmentação do **Número de pedidos** métrica por **Canal**. Teste a nova coluna e veja quais tendências você pode identificar em sua [!DNL Google Analytics Channel] dados!

## Documentação relacionada

* [Uso do Report Builder](../../tutorials/using-visual-report-builder.md)
* [Esperado[!DNL Google ECommerce]dados](../importing-data/integrations/google-ecommerce-data.md)
* [Criação[!DNL Google ECommerce]dimensões com dados de pedido e cliente](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [Quais são suas fontes e canais de aquisição mais valiosos?](../analysis/most-value-source-channel.md)
