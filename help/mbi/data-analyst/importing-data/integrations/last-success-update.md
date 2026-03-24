---
title: Entender os resultados entre o banco de dados e o editor SQL
description: Saiba como entender os resultados entre o banco de dados e o editor SQL.
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/pScH-yKW8hbSNZzsJ537CN7rxhcuygaLmCu3fdVaYgk
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 257
ht-degree: 0%

---

# Resultados do Banco de Dados vs [!DNL SQL Editor] Resultados

Você pode estar curioso sobre qual é o campo `Last successful update began` dentro da página `Integrations`:

![Última_atualização_bem-sucedida.png](../../../assets/Last_successful_update.png)

## Entender o campo `timestamp`

Ele mostra o início `timestamp` (no fuso horário definido em sua conta) do _último ciclo de atualização bem-sucedido_ em sua conta.

- Se qualquer uma das tabelas sincronizadas encontrou um problema durante o último ciclo de atualização, esse carimbo de data/hora será *não atualizado*.
- Portanto, pode haver casos em que os relatórios tenham sido atualizados com dados novos, mas a *Última atualização bem-sucedida iniciada* ainda está atrasada.

## Identificação do último ponto de dados &quot;real&quot;

O ponto de dados mais recente de uma integração específica é determinado pelo carimbo de data e hora `Last Data Point Received`, localizado à direita de cada integração. Esse carimbo de data e hora se refere ao último ponto em que o Data Warehouse recebeu com êxito pontos de dados dessa fonte, seja um banco de dados, API ou integração de terceiros.

Para verificar a atualização dos dados de *tabelas específicas*, a Adobe recomenda criar um [[!DNL SQL] relatório](../../dev-reports/sql-rpt-bldr.md) rápido que execute um `MAX(timestamp)` na tabela mais importante da sua conta. Comparar esse carimbo de data/hora com `Last Data Point` indica se o problema afetou toda a conta ou um subconjunto das tabelas. A Adobe recomenda fazer isso para três a quatro tabelas importantes e usadas com frequência.

- Se os valores `MAX(timestamp)` forem mais recentes que `Last Data Point Received`, isso significa que um subconjunto das tabelas foi afetado, mas o ciclo de atualização da conta geral é estável.
- Se os valores `MAX(timestamp)` forem iguais ou anteriores a `Last Data Point Received`, isso significa que o ciclo de atualização da conta foi afetado. Nesta situação, [envie um tíquete de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
