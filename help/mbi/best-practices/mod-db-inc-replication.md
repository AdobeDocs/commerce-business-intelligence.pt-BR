---
title: Modificando o Banco de Dados para Suporte à Replicação Incremental
description: Saiba como modificar seu banco de dados para oferecer suporte à replicação incremental.
exl-id: c9a38892-6096-4eb5-8a53-35b8b7b083dc
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---

# Suporte para replicação incremental

Se as tabelas não permitirem replicação incremental no momento, consulte as seguintes recomendações para obter possíveis soluções.

## Modificações de Modificado em

O método `Modified At`, que é o método de replicação mais ideal, usa uma coluna `datetime` para detectar dados novos e/ou atualizados. Lembre-se de que a coluna `datetime` em tabelas que usam este método deve ser indexada e não pode conter valores nulos a qualquer momento.

Se a tabela não tiver uma coluna `datetime`, você poderá adicionar uma coluna de índice `modified at`. Valores nulos não são permitidos em uma coluna `modified at`. Verifique se a coluna está preenchida para cada linha.

Para garantir que o método `Modified At` funcione conforme o esperado, não é possível excluir linhas da tabela. Em vez disso, você deve marcar a linha como inválida adicionando uma coluna `deleted` à tabela. Esta coluna retorna `1` se a linha for inválida e `0` se não for. Você pode usar essa coluna para filtrar linhas inválidas ao criar métricas e relatórios.

## Modificações para chave primária de incrementação automática única

Se o método `Modified At` não puder ser habilitado, a Chave Primária de Incrementação Automática Única será a próxima melhor opção. Novos dados são detectados em tabelas usando esse método procurando valores de chave primária que sejam maiores que o valor mais alto atual na Data Warehouse.

Lembre-se, as tabelas que usam este método são colunas únicas com números inteiros incrementando automaticamente as chaves primárias. Para usar esse método no banco de dados, faça as seguintes modificações:

* Se a chave primária for uma chave composta ou um não-inteiro, altere a chave primária para um inteiro de incremento automático
* Se a chave primária for uma única coluna de número inteiro, mas as chaves puderem ser atribuídas não sequencialmente, altere a chave primária para incremento automático

## Encapsulamento

Ao fazer pequenas modificações em suas tabelas, você pode aproveitar os Métodos de replicação incremental mais rápidos e eficientes. No entanto, se isso não for possível, você ainda poderá executar outras etapas para [reduzir o tempo de atualização](../best-practices/reduce-update-cycle-time.md) e [otimizar o banco de dados](../best-practices/opt-db-analysis.md).
