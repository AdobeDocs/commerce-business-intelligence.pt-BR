---
title: Entender os resultados entre o banco de dados e o editor SQL
description: Saiba como entender os resultados entre o banco de dados e o editor SQL.
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# Resultados do Banco de Dados vs `SQL Editor` Resultados

Você pode estar curioso para saber o que `Last successful update began` o campo está dentro de seu `Integrations` página:

![Last_successful_update.png](../../../assets/Last_successful_update.png)

## Compreender o `timestamp` campo

Ele mostra o início `timestamp` (no fuso horário definido em sua conta) da _último ciclo de atualização bem-sucedido_ em sua conta.

- Se qualquer uma das tabelas sincronizadas encontrar um problema durante o último ciclo de atualização, esse carimbo de data e hora será *não atualizado*.
- Por conseguinte, pode haver casos em que os relatórios tenham sido atualizados com *Última atualização bem-sucedida iniciada* O ainda está atrasado.

## Identificação do último ponto de dados &quot;real&quot;

O ponto de dados mais recente para uma integração específica é determinado pela variável `Last Data Point Received` `timestamp` localizado à direita de cada integração. Esse carimbo de data e hora se refere ao último ponto em que sua Data Warehouse recebeu pontos de dados com êxito dessa fonte, seja um banco de dados, uma API ou uma integração de terceiros.

Para verificar a atualização dos dados do *tabelas específicas*, o Adobe recomenda criar uma [Relatório SQL](../../dev-reports/sql-rpt-bldr.md) que executa um `MAX(timestamp)` na tabela mais importante da sua conta. Comparar esse carimbo de data e hora com o `Last Data Point` indica se o problema afetou toda a conta ou um subconjunto das tabelas. A Adobe recomenda fazer isso para três a quatro tabelas importantes, comumente usadas.

- Se a variável `MAX(timestamp)` os valores são mais recentes do que `Last Data Point Received`Portanto, significa que um subconjunto das tabelas foi afetado, mas o ciclo de atualização da conta geral é estável.
- Se a variável `MAX(timestamp)` os valores são iguais ou anteriores a `Last Data Point Received`, significa que o ciclo de atualização da conta foi afetado. Nesta situação, [enviar um tíquete de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
