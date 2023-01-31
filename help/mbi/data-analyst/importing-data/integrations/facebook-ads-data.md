---
title: Dados de anúncios do Facebook esperados
description: Saiba uma breve visão geral das tabelas que recomendamos que você sincronize com seu data warehouse
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# Esperado [!DNL Facebook Ads] dados

![](../../../assets/Facebook_Logo.png)

Depois de [conectou seu [!DNL Facebook Ads] account](../integrations/facebook-ads.md), você pode usar o [Gerenciador de Datas Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear facilmente os campos de dados relevantes para análise.

Neste artigo, fornecemos uma breve visão geral das tabelas que recomendamos que você sincronize com seu data warehouse. Esta não é uma lista completa, pois há alguns subquadros. Estamos apenas a destacar as principais tabelas.

## Tabelas de campanha de publicidade principal

Essas tabelas contêm dados sobre os componentes principais de campanha publicitária.

### [`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/reference/ads-api/adcampaign/)

Esta tabela é a tabela principal de campanhas em uma [!DNL Facebook Ads] conta. As colunas incluem `campaign id`, `name`, `status (active/paused)`, `objective`.

### [`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

Os registros desta tabela são a tabela principal de [!DNL Facebook Ads] Define em um [!DNL Facebook Ads] conta. As colunas incluem o anúncio `Campaign id/name` o Conjunto de anúncios pertence a, o orçamento, o tipo de lance, o agendamento e as informações de direcionamento do público-alvo.

### [`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/reference/ads-api/adgroup/)

Esta tabela registra todos os anúncios em uma [!DNL Facebook Ads] conta. As colunas incluem as informações do anúncio, incluindo o Conjunto de anúncios e a Campanha de publicidade à qual pertence, o lance do anúncio, o direcionamento do anúncio e a referência para anúncios específicos (imagem/texto) usados pelo anúncio.

### [`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/reference/ads-api/adcreative/)

Esta tabela registra todas as criações usadas em [!DNL Facebook Ads]. Isso inclui nome criativo, descrição e urls de imagem relevantes, quando apropriado.

## Tabelas de campanha segmentadas

As tabelas a seguir contêm uma entrada para cada combinação de campanha/conjunto/anúncio para cada dia, segmentada por dimensões como idade, gênero e país.

### `facebook _ads insights_ (account-id)`

Esta tabela inclui uma entrada para cada combinação de campanha/conjunto/anúncio para cada dia, juntamente com estatísticas que incluem impressões, cliques, custo, cpc, cpm, cpp, ctr, alcance, alcance social e gasto.

### `facebook _ads insights_ (account-id)_~\_actions`

Esta é uma subtabela da variável `facebook_ads_insights_{account_id}` tabela. Inclui dados de conversão para ações que acontecem com base em campanhas diferentes.

### `facebook _ads insights country_ (account-id)`

Esta tabela inclui as mesmas informações que o `facebook_ads_insights_{account_id}` e a segmenta por país.

### `facebook ads insights age and gender (account-id)`

Esta tabela inclui as mesmas informações que o `facebook_ads_insights_{account_id}` e a segmenta por idade e sexo.

## Relacionado

* [Conexão [!DNL Facebook Ads]](../integrations/facebook-ads.md)
* [Reautenticação de integrações](https://support.magento.com/hc/en-us/articles/360016733151-Reauthenticating-integrations)
