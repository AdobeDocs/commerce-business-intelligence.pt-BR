---
title: Replicação de canais Google Analytics usando fontes de aquisição
description: Saiba como replicar canais Google Analytics usando fontes de aquisição.
exl-id: e7248fe4-94db-4cdf-8f58-1f65061a207d
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# Google Analytics usando fontes de aquisição

## O que são Canais? {#channels}

Criação de segmentos personalizados para ver o desempenho de tráfego diferente e observar tendências (para melhor ou pior!) é um dos usos mais eficientes para  [!DNL Google Analytics ]. Uma classe de segmentos que existe por padrão em [!DNL Google Analytics ] são `Channels`. Os canais são um agrupamento de maneiras comuns que as pessoas visitam seu site.  [!DNL Google Analytics ] O classifica automaticamente as várias maneiras de adquirir um usuário, seja em redes sociais, no pagamento por clique, no email ou em links de referência, e os agrupa em um bucket ou Canal.

## Por que não vejo meu `channels` na IMM? {#nochannels}

`Channels` são compartimentos de dados simples e agregados. Para classificar suas aquisições em buckets de canal, a Google define regras e definições distintas usando parâmetros específicos: uma combinação de aquisição [Origem](https://support.google.com/analytics/answer/1033173?hl=en) (a origem do seu tráfego) e aquisição [Médio](https://support.google.com/analytics/answer/6099206?hl=en) (categoria geral da fonte).

Embora esses compartimentos possam ajudá-lo a entender de onde seu tráfego vem, esses dados não são marcados por canal, mas por uma combinação de Origem e Médio. Como o Google envia informações de canal como dois pontos de dados separados, os agrupamentos de canais não são exibidos automaticamente em [!DNL MBI].

## Quais são os agrupamentos de canais padrão? Como eles são criados?

Por padrão, o Google configura você com 8 canais diferentes. Vamos analisar as regras que determinam como elas são criadas:

| Canal | O que é? | Como é criado? |
|---|---|---|
| Direta | Qualquer pessoa que entre diretamente no seu site. | Origem = `Direct`<br>E Médio = `(not set); OR Medium = (none)` |
| Pesquisa orgânica | Tráfego que foi classificado organicamente em mecanismos de pesquisa não pagos. | Médio = `organic` |
| Consulta | Tráfego que vem de um link externo que não é Pesquisa orgânica ou de sites que não são redes sociais. | Médio = `referral` |
| Pesquisa paga | Tráfego que tem um código de rastreamento de UTM, onde a mídia é &quot;cpc&quot;, &quot;ppc&quot; ou &quot;paidsearch&quot; E é uma rede de distribuição de anúncios que não corresponde a &quot;Conteúdo&quot;. | Médio = `^(cpc|ppc|paidsearch)$`<br>E Rede de Distribuição de Anúncios ≠ `Content` |
| Social | Tráfego de referência proveniente de qualquer um de aproximadamente [400 redes sociais](https://www.annielytics.com/blog/analytics/sites-google-analytics-includes-in-social-reports/) e não são marcados como anúncios. | Referência da fonte social = `Yes`<br>OU Médio = `^(social|social-network|social-media|sm|social network|social media)$` |
| Email | Tráfego de sessões que são marcadas com um meio de &quot;email&quot;. | Código de rastreamento de UTM de Médio = `email` |
| Exibir | Tráfego que tem um código de rastreamento de UTM, onde a mídia é exibida ou cpm. Também inclui a interação do AdWords, onde a rede de distribuição de anúncios corresponde a &quot;Conteúdo&quot; | Médio = `^(display|cpm|banner)$`<br>OU Rede de distribuição de anúncios = `Content`<br>Formato de anúncio E ≠ `Text` |
| Outras | Sessões de outros canais de publicidade, não incluindo Pesquisa paga, que são marcadas com um meio de &quot;cpc&quot;, &quot;ppc&quot;, &quot;cpm&quot;, &quot;cpv&quot;, &quot;cpa&quot;, &quot;cpp&quot;, &quot;afiliado&quot;. | Médio = `^(cpv|cpa|cpp|content-text)$` |

{style=&quot;table-layout:auto&quot;}

## Como posso recriar esses agrupamentos de canais na minha Data Warehouse? {#recreate}

Agora que você sabe que os canais são apenas combinações de fontes e mídias, é um processo fácil de três etapas para recriar esses agrupamentos em sua Data Warehouse.

1. **Ative o[!DNL Google ECommerce]integração**

   [Uma vez ativado](../importing-data/integrations/google-ecommerce.md), certifique-se de [sincronizar](../{{ site.baseurl }}/data-analyst/data-warehouse-mgr/tour-dwm.html#sincronização) a **medium** e **source** em sua Data Warehouse. Depois que isso for concluído, os dados de aquisição de mídia e fonte serão trazidos para a Data Warehouse.

1. **Fazer upload de um mapeamento de agrupamentos de canais do Google**

   Para economizar tempo, o Commerce já criou uma tabela com os agrupamentos padrão mapeados como um arquivo que você pode [download](../../assets/ga-channel-mapping.csv).

   Se você for um Google Analytics pro e tiver criado seus próprios canais, será necessário adicionar suas regras específicas à tabela de mapeamento antes de fazer upload do arquivo para [!DNL MBI].

   Traga-o para a sua Data Warehouse como um [Upload de arquivo](../importing-data/connecting-data/using-file-uploader.md).

   ![](../../assets/Setting_Primary_Keys.png)

1. **Estabelecer uma relação entre[!DNL Google ECommerce]Upload de arquivo de mapeamentos e**

   Para estabelecer uma relação entre a[!DNL Google ECommerce]e a tabela de mapeamento, [enviar um pedido de apoio](../../guide-overview.md) para nossa equipe de Analistas de dados e consulte este artigo. O analista criará uma nova coluna calculada chamada **Canal** na tabela comércio eletrônico. **Após um ciclo completo de atualização**, essa coluna estará pronta para ser usada em Filtrar ou Agrupar por.

Parabéns! Agora você tem agrupamentos de Canal Google Analytics em sua Data Warehouse, o que significa que é possível analisar seus dados de uma nova perspectiva:

![Segmentação da métrica Número de pedidos por canal](../../assets/GA_Channel_Gif.gif)

Neste exemplo, começamos a ser simples - segmentando o **Número de pedidos** métrica por **Canal**. Agora é a sua vez - teste sua nova coluna e veja quais tendências você pode identificar nos dados do seu canal Google Analytics!

## Documentação relacionada

* [Uso do Report Builder](../../tutorials/using-visual-report-builder.md)
* [Esperado[!DNL Google ECommerce]dados](../importing-data/integrations/google-ecommerce-data.md)
* [Construção[!DNL Google ECommerce]dimensões com dados de pedido e cliente](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [Quais são suas fontes e canais de aquisição mais valiosos?](../analysis/most-value-source-channel.md)
