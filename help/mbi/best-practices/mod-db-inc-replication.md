---
title: Modificar seu banco de dados para oferecer suporte à replicação incremental
description: Saiba como modificar seu banco de dados para oferecer suporte à replicação incremental.
exl-id: c9a38892-6096-4eb5-8a53-35b8b7b083dc
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# Suporte para replicação incremental

Se as tabelas atualmente não permitem replicação incremental, consulte as seguintes recomendações para possíveis soluções.

## Modificações para Modificado em

O `Modified At` , que é o método de replicação mais ideal, usa um `datetime` para detectar dados novos e/ou atualizados. Lembre-se de que a variável `datetime` nas tabelas que usam esse método devem ser indexadas e não podem conter valores nulos a qualquer momento.

Se sua tabela não tiver uma `datetime` , é possível adicionar um índice `modified at` coluna. Valores nulos não são permitidos em um `modified at` coluna. Verifique se a coluna está preenchida para cada linha.

Para garantir que `Modified At` O método funciona conforme o esperado, não é possível excluir linhas da tabela. Em vez disso, você deve marcar a linha como inválida ao adicionar um `deleted` para a tabela. Essa coluna retornará uma `1` se a linha for inválida e `0` caso contrário. Em seguida, você pode usar essa coluna para filtrar linhas inválidas ao criar métricas e relatórios.

## Modificações para Incrementação automática única da chave primária

Se a variável `Modified At` não pode ser ativado, então a Chave primária de incremento automático único é a melhor opção a seguir. Novos dados são descobertos nas tabelas usando este método, procurando por valores de chave primária que são maiores que o valor mais alto atual na Data Warehouse.

Lembre-se, as tabelas que usam esse método são colunas únicas com números inteiros incrementando automaticamente as chaves primárias. Para usar esse método no banco de dados, faça as seguintes modificações:

* Se a chave primária for uma chave composta ou um número não inteiro, altere a chave primária para um número inteiro incrementado automaticamente
* Se a chave primária for uma única coluna inteira, mas as chaves puderem ser atribuídas de forma não sequencial, altere a chave primária para incremento automático

## Quebra de linha

Ao fazer pequenas modificações nas tabelas, você pode aproveitar os Métodos de replicação incremental mais rápidos e eficientes; no entanto, se isso ainda não for possível, você ainda poderá tomar outras medidas para [reduzir o tempo de atualização](../best-practices/reduce-update-cycle-time.md) e [otimizar seu banco de dados](../best-practices/opt-db-analysis.md).
