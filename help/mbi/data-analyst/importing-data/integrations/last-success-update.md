---
title: Entender os resultados entre o Database e o SQL Editor
description: Saiba mais sobre como entender os resultados entre o banco de dados e o editor SQL.
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# Resultados do Banco de Dados vs `SQL Editor` Resultados

Você pode estar curioso sobre o que `Last successful update began` está dentro do seu `Integrations` página:

![Last_success_update.png](../../../assets/Last_successful_update.png)

## Entenda o `timestamp` campo

Mostra o início `timestamp` (no fuso horário definido em sua conta) da variável _último ciclo de atualização bem-sucedido_ por sua conta.

- Se qualquer uma das tabelas sincronizadas encontrar um problema durante o último ciclo de atualização, esse carimbo de data e hora será *não atualizado*.
- Portanto, pode haver casos em que os relatórios tenham sido atualizados com novos dados, mas a variável *Última atualização bem-sucedida iniciada* ainda está atrasado.

## Identificar o último ponto de dados &quot;real&quot;

O último ponto de dados para uma integração específica é determinado pela variável `Last Data Point Received` `timestamp` localizada à direita de cada integração. Esse carimbo de data e hora se refere ao último ponto em que o data warehouse recebeu com êxito pontos de dados dessa fonte, seja um banco de dados, uma API ou integração de terceiros.

Para verificar a atualização dos dados do *tabelas específicas*, recomendamos criar um [Relatório SQL](../../dev-reports/sql-rpt-bldr.md) que executa um `MAX(timestamp)` na tabela mais importante da sua conta. Comparação desse carimbo de data e hora com a `Last Data Point` indicará se o problema afetou a conta inteira ou um subconjunto das tabelas. Recomendamos fazer isso para três a quatro tabelas importantes e de uso comum.

- Se a variável `MAX(timestamp)` são mais recentes que `Last Data Point Received`, significa que um subconjunto das tabelas foi afetado, mas o ciclo de atualização geral da conta é estável.
- Se a variável `MAX(timestamp)` são iguais a ou anteriores `Last Data Point Received`, significa que o ciclo de atualização da conta foi afetado. Nesta situação, [enviar um tíquete de suporte](../../../guide-overview.md).
