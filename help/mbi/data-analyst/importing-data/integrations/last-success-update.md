---
title: Entender os resultados entre o banco de dados e o editor SQL
description: Saiba como entender os resultados entre o banco de dados e o editor SQL.
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 5e80ff8f8ec76996b88a22b115be696b110581be
workflow-type: tm+mt
source-wordcount: '257'
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
- Se os valores `MAX(timestamp)` forem iguais ou anteriores a `Last Data Point Received`, isso significa que o ciclo de atualização da conta foi afetado. Nesta situação, [envie um tíquete de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=pt-BR).
