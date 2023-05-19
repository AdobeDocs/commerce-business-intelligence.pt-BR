---
title: Dados esperados do Facebook Ads
description: Saiba mais sobre uma breve visão geral das tabelas recomendadas para sincronização com a Data Warehouse
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# Esperado [!DNL Facebook Ads] dados

Depois de ter [conectou o [!DNL Facebook Ads] account](../integrations/facebook-ads.md), você pode usar o [Gerenciador de Data Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear facilmente campos de dados relevantes para análise.

Este tópico fornece uma breve visão geral das tabelas que a Adobe recomenda que você sincronize com a Data Warehouse. Isso apenas destaca as tabelas principais, pois há algumas subtabelas.

## Tabelas de campanha de publicidade principais

Essas tabelas contêm dados sobre os componentes principais dos anúncios.

### [`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group)

Esta tabela é a tabela principal das campanhas em uma [!DNL Facebook Ads] conta. As colunas incluem `campaign id`, `name`, `status (active/paused)`, `objective`.

### [`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

Este registro de tabela é a tabela principal de [!DNL Facebook Ads] Conjuntos em um [!DNL Facebook Ads] conta. As colunas incluem o anúncio `Campaign id/name` o Conjunto de anúncios pertence a, o orçamento, tipo de oferta, programação e informações de direcionamento de público-alvo.

### [`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/adgroup)

Esta tabela registra todos os anúncios em um [!DNL Facebook Ads] conta. As colunas incluem as informações do anúncio, incluindo o Conjunto de anúncios e a Campanha publicitária à qual ele pertence, o lance do anúncio, o direcionamento do anúncio e a referência ao criativo específico (imagem/texto) que o anúncio usa.

### [`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-creative)

Esta tabela registra criações usadas em [!DNL Facebook Ads]. A seção Criativos inclui nome criativo, descrição e urls de imagem relevantes, quando apropriado.

## Tabelas de campanha segmentadas

As tabelas a seguir contêm uma entrada para cada combinação de campanha/conjunto/anúncio para cada dia, segmentada por dimensões como idade, gênero e país.

### `facebook _ads insights_ (account-id)`

Esta tabela inclui uma entrada para cada combinação de campanha/conjunto/anúncio para cada dia, juntamente com estatísticas, incluindo impressões, cliques, custo, cpc, cpm, cpp, ctr, alcance, alcance social e gasto.

### `facebook _ads insights_ (account-id)_~\_actions`

Esta é uma subtabela de `facebook_ads_insights_{account_id}` tabela. Ele inclui dados de conversão para ações que ocorrem com base em campanhas diferentes.

### `facebook _ads insights country_ (account-id)`

Esta tabela inclui as mesmas informações que a variável `facebook_ads_insights_{account_id}` tabela e a segmenta por país.

### `facebook ads insights age and gender (account-id)`

Esta tabela inclui as mesmas informações que a variável `facebook_ads_insights_{account_id}` tabela e a segmenta por idade e gênero.

## Relacionados

* [Conectando [!DNL Facebook Ads]](../integrations/facebook-ads.md)
* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
