---
title: Dados esperados do Facebook Ads
description: Saiba mais sobre uma breve visão geral das tabelas recomendadas para sincronização com o Data Warehouse
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# Dados [!DNL Facebook Ads] esperados

Depois de [conectar sua [!DNL Facebook Ads] conta](../integrations/facebook-ads.md), você poderá usar o [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear facilmente campos de dados relevantes para análise.

Este tópico fornece uma breve visão geral das tabelas que a Adobe recomenda que você sincronize com o Data Warehouse. Isso apenas destaca as tabelas principais, pois há algumas subtabelas.

## Tabelas de campanha de publicidade principais

Essas tabelas contêm dados sobre os componentes principais dos anúncios.

### [`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group)

Esta tabela é a tabela principal das campanhas em uma conta do [!DNL Facebook Ads]. As colunas incluem `campaign id`, `name`, `status (active/paused)`, `objective`.

### [`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

Este registro de tabela é a tabela principal dos Conjuntos [!DNL Facebook Ads] em uma conta [!DNL Facebook Ads]. As colunas incluem o Anúncio `Campaign id/name` ao qual o Conjunto de Anúncios pertence, o orçamento, o tipo de oferta, o agendamento e as informações de direcionamento de público.

### [`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/adgroup)

Esta tabela registra todos os anúncios em uma conta [!DNL Facebook Ads]. As colunas incluem as informações do anúncio, incluindo o Conjunto de anúncios e a Campanha publicitária à qual ele pertence, o lance do anúncio, o direcionamento do anúncio e a referência ao criativo específico (imagem/texto) que o anúncio usa.

### [`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-creative)

Esta tabela registra as criações usadas em [!DNL Facebook Ads]. A seção Criativos inclui nome criativo, descrição e urls de imagem relevantes, quando apropriado.

## Tabelas de campanha segmentadas

As tabelas a seguir contêm uma entrada para cada combinação de campanha/conjunto/anúncio para cada dia, segmentada por dimensões como idade, gênero e país.

### `facebook _ads insights_ (account-id)`

Esta tabela inclui uma entrada para cada combinação de campanha/conjunto/anúncio para cada dia, juntamente com estatísticas, incluindo impressões, cliques, custo, cpc, cpm, cpp, ctr, alcance, alcance social e gasto.

### `facebook _ads insights_ (account-id)_~\_actions`

Esta é uma subtabela da tabela `facebook_ads_insights_{account_id}`. Ele inclui dados de conversão para ações que ocorrem com base em campanhas diferentes.

### `facebook _ads insights country_ (account-id)`

Esta tabela inclui as mesmas informações que a tabela `facebook_ads_insights_{account_id}` e a segmenta por país.

### `facebook ads insights age and gender (account-id)`

Esta tabela inclui as mesmas informações que a tabela `facebook_ads_insights_{account_id}` e as segmenta por idade e sexo.

## Relacionados

* [Conectando [!DNL Facebook Ads]](../integrations/facebook-ads.md)
* [Reautenticando integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
