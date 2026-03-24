---
title: Replicação de canais da Google Analytics usando fontes de aquisição
description: Saiba como replicar canais da Google Analytics usando fontes de aquisição.
exl-id: e7248fe4-94db-4cdf-8f58-1f65061a207d
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/5UBZqrRg-eiDLvcGe93qEX5KQKWc63eTQOLQ9pnprkI
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 688
ht-degree: 0%

---

# [!DNL Google Analytics] usando fontes de aquisição

## O que são canais? {#channels}

Criar segmentos personalizados para ver como tráfego diferente funciona e observar tendências é um dos usos mais eficientes do [!DNL Google Analytics]. Uma classe de segmentos que existe por padrão em [!DNL Google Analytics] é `Channels`. Os canais são um agrupamento de maneiras comuns de as pessoas acessarem o site.  O [!DNL Google Analytics] classifica automaticamente as várias formas pelas quais você adquire um usuário - seja redes sociais, pay-per-click, email ou links de referência - e os agrupa em um balde ou Canal.

## Por que não vejo meu `channels` no Commerce Intelligence? {#nochannels}

`Channels` são compartimentos de dados simples e agregados. Para classificar suas aquisições em compartimentos de canal, o [!DNL Google] define regras e definições distintas usando parâmetros específicos: uma combinação de aquisição [Source](https://support.google.com/analytics/answer/1033173?hl=en) (a origem do tráfego) e aquisição [Medium](https://support.google.com/analytics/answer/6099206?hl=en) (a categoria geral da origem).

Embora ter esses buckets possa ajudar a entender de onde seu tráfego vem, esses dados não são marcados por canal, mas por uma combinação de Source e Medium. Como [!DNL Google] envia informações de canal como dois pontos de dados separados, os agrupamentos de canal não aparecem automaticamente em [!DNL Commerce Intelligence].

## Quais são os agrupamentos de canal padrão? Como eles são criados?

Por padrão, o [!DNL Google] configura oito canais diferentes. As regras que determinam como os canais são criados estão abaixo.

| **Canal** | **O que é?** | **Como ele é criado?** |
|---|---|---|
| Direto | Qualquer pessoa que entre diretamente no seu site. | Source = `Direct`<br>E Medium = `(not set); OR Medium = (none)` |
| Pesquisa orgânica | Tráfego que foi classificado organicamente em mecanismos de pesquisa não pagos. | Medium = `organic` |
| Referência | Tráfego que vem de um link externo que não é Pesquisa orgânica ou de sites que não são redes sociais. | Medium = `referral` |
| Pesquisa paga | Tráfego que tem um Código de rastreamento UTM em que a mídia é &quot;cpc&quot;, &quot;ppc&quot; ou &quot;paidsearch&quot; E é uma rede de distribuição de anúncios que não corresponde a &quot;Conteúdo&quot;. | Medium = `^(cpc`\|`ppc`\|`paidsearch)$`<br>AND Ad Distribution Network ≠ `Content` |
| Social | Tráfego de referência que vem de qualquer uma das aproximadamente 400 redes sociais e não são marcadas como anúncios. | Referência do Social Source = `Yes`<br>OU Medium = `^(social`\|`social-network`\|`social-media`\|`sm`\|`social network`\|`social media)$` |
| Email | Tráfego de sessões que são marcadas com uma mídia de &quot;email&quot;. | Código de rastreamento UTM do Medium = `email` |
| Exibir | Tráfego que tem um Código de rastreamento UTM em que a mídia é exibição ou cpm. Também inclui a interação do AdWords em que a rede de distribuição de anúncios corresponde a &quot;Conteúdo&quot; | Medium = `^(display`\|`cpm`\|`banner)$`<br>OU Rede de Distribuição de Anúncios = `Content`<br>E Formato de Anúncios ≠ `Text` |
| Outro | Sessões de outros canais de publicidade (sem incluir Pesquisa paga) marcadas com uma mídia &quot;cpc&quot;, &quot;ppc&quot;, &quot;cpm&quot;, &quot;cpv&quot;, &quot;cpa&quot;, &quot;cpp&quot;, &quot;afiliate&quot;. | Medium = `^(cpv`\|`cpa`\|`cpp`\|`content-text)$` |

{style="table-layout:auto"}

## Como posso recriar esses agrupamentos de canal no meu Data Warehouse? {#recreate}

Agora que você sabe que os canais são apenas combinações de fontes e mídias, é um processo fácil de 3 etapas para recriar esses agrupamentos no Data Warehouse.

1. **Habilitar sua[!DNL Google ECommerce]integração**

   [Quando habilitado](../importing-data/integrations/google-ecommerce.md), certifique-se de [sincronizar](tour-dwm.md#syncing) os campos **mídia** e **origem** em sua Data Warehouse. Depois que isso for concluído, os dados de aquisição de mídia e fonte serão trazidos para a Data Warehouse.

1. **Carregar um mapeamento dos agrupamentos de canais da Google**

   O Adobe Commerce cria uma tabela com os agrupamentos padrão mapeados como um arquivo que você pode [baixar](../../assets/ga-channel-mapping.csv).

   Se você é um profissional do [!DNL Google Analytics] e criou seus próprios canais, deseja adicionar suas regras específicas à tabela de mapeamento antes de carregar o arquivo no [!DNL Commerce Intelligence].

   Traga-o para sua Data Warehouse como um [Upload de arquivo](../importing-data/connecting-data/using-file-uploader.md).

   ![Interface do Data Warehouse Manager mostrando configurações de chave primária](../../assets/Setting_Primary_Keys.png)

1. **Estabelecer uma relação entre[!DNL Google ECommerce]e o Carregamento de Arquivo de Mapeamentos**

   Para estabelecer uma relação entre o [!DNL Google ECommerce] e a tabela de mapeamento, [envie uma solicitação de suporte](../../guide-overview.md#Submitting-a-Support-Ticket) para sua equipe de Data Analyst e faça referência a este tópico. O analista cria uma nova coluna calculada chamada **Canal** na tabela ECommerce. **Após um ciclo completo de atualização**, esta coluna estará pronta para uso em um `Filter` ou `Group by`.

Agora você tem [!DNL Google Analytics Channel] agrupamentos em sua Data Warehouse, o que significa que você pode analisar seus dados de uma nova perspectiva:

![Segmentando a métrica Número de Pedidos por Canal](../../assets/GA_Channel_Gif.gif)

Neste exemplo, você começou simples com a segmentação da métrica **Número de pedidos** pelo **Canal**. Teste a nova coluna e veja quais tendências você pode identificar nos dados do [!DNL Google Analytics Channel]!

## Documentação relacionada

* [Uso do Report Builder](../../tutorials/using-visual-report-builder.md)
* [Dados [!DNL Google ECommerce] esperados](../importing-data/integrations/google-ecommerce-data.md)
* [Compilando [!DNL Google ECommerce]dimensões com dados de ordem e cliente](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [Quais são suas fontes e canais de aquisição mais valiosos?](../analysis/most-value-source-channel.md)
