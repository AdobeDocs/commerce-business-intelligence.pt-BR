---
title: Modificando o Banco de Dados para Suporte à Replicação Incremental
description: Saiba como modificar seu banco de dados para oferecer suporte à replicação incremental.
exl-id: c9a38892-6096-4eb5-8a53-35b8b7b083dc
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---

# Suporte para replicação incremental

Se as tabelas não permitirem replicação incremental no momento, consulte as seguintes recomendações para obter possíveis soluções.

## Modificações de Modificado em

A variável `Modified At` que é o método de replicação mais ideal, usa um `datetime` para detectar dados novos e/ou atualizados. Lembre-se de que a variável `datetime` a coluna nas tabelas que usam este método deve ser indexada e não pode conter valores nulos a qualquer momento.

Se a tabela não tiver um `datetime` , é possível adicionar um índice `modified at` coluna. Valores nulos não são permitidos em uma `modified at` coluna. Verifique se a coluna está preenchida para cada linha.

Para assegurar a `Modified At` funciona conforme o esperado, não é possível excluir linhas da tabela. Em vez disso, você deve marcar a linha como inválida adicionando um `deleted` à tabela. Essa coluna retorna um valor de `1` se a linha for inválida e `0` caso contrário. Você pode usar essa coluna para filtrar linhas inválidas ao criar métricas e relatórios.

## Modificações para chave primária de incrementação automática única

Se a variável `Modified At` não puder ser ativado, então a Chave primária de incrementação automática única é a próxima melhor opção. Novos dados são detectados em tabelas usando esse método procurando valores de chave primária que sejam maiores que o valor mais alto atual na Data Warehouse.

Lembre-se, as tabelas que usam este método são colunas únicas com números inteiros incrementando automaticamente as chaves primárias. Para usar esse método no banco de dados, faça as seguintes modificações:

* Se a chave primária for uma chave composta ou um não-inteiro, altere a chave primária para um inteiro de incremento automático
* Se a chave primária for uma única coluna de número inteiro, mas as chaves puderem ser atribuídas não sequencialmente, altere a chave primária para incremento automático

## Encapsulamento

Ao fazer pequenas modificações em suas tabelas, você pode aproveitar os Métodos de replicação incremental mais rápidos e eficientes. No entanto, se isso não for possível, você ainda poderá tomar outras medidas para [reduza o tempo de atualização](../best-practices/reduce-update-cycle-time.md) e [otimizar o banco de dados](../best-practices/opt-db-analysis.md).
