---
title: Dados esperados do Facebook Ads
description: Saiba mais sobre uma breve visão geral das tabelas recomendadas para sincronização com o Data Warehouse
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/LBpqIMm4nGx-Vu-zxw-iPLgNg1yfDsYi0yDyFHCyxvA
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 303
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
