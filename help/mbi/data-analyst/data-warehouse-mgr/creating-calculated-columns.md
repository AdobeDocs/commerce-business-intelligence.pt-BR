---
title: Criar colunas calculadas
description: Saiba como consolidar dados de fontes diferentes.
exl-id: 668cbc77-6a96-4687-9f40-3635b1be5c66
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# Criar colunas calculadas

Ao analisar seus dados, é útil consolidar os dados de fontes diferentes. Deseja agrupar a receita por fonte de aquisição, vinculando dados da tabela de pedidos e Google Analytics? Ou como agrupar a receita por gênero de cliente ou unir um atributo de cliente aos dados de transação para segmentação?

Este guia ensina como fazer exatamente isso. Antes de começar, recomendamos que você verifique o [Guia de tipos de colunas calculadas](../../data-analyst/data-warehouse-mgr/calc-column-types.md). O _Guia de tipos de colunas calculadas_ descreve os tipos de colunas que podem ser criadas no Gerenciador de Datas Warehouse, juntamente com suas definições e exemplos.

1. Para começar, clique em **[!DNL Manage Data > Data Warehouse]** na barra lateral.

1. Clique na tabela na qual deseja criar uma coluna. Por exemplo, se quisermos criar um `Customer Gender` para segmentação da receita, selecionamos a variável `sales_flat_order` tabela.

1. O esquema da tabela será exibido. Clique em **[!UICONTROL Create New Column]**.

1. Dê um nome à coluna - por exemplo, `Customer Gender`.

1. Selecione a definição da coluna. É aqui que a variável [Guia Tipos de colunas calculadas](../data-warehouse-mgr/calc-column-types.md) virá a calhar!

1. Para certos tipos de colunas, um pouco mais de informações é necessário para criar a coluna corretamente:
   * Para `One to Many` (unido) e `Many to One` (agregado) , é necessário selecionar as tabelas e colunas.
   * Para um `Same Table calculation`, é necessário selecionar o campo de data desejado na lista suspensa.

Se você estiver criando um `One to Many` (unido) ou `Many to One` (agregação), é necessário selecionar um caminho para conectar as duas tabelas. Nesta etapa, você pode usar um caminho existente ou criar um novo.

>[!NOTE]
>
>Lembre-se de definir corretamente a tabela como muitas ou uma!

* Se desejar, você pode aplicar [filtros](../../data-user/reports/ess-manage-data-filters.md) à nova coluna.
* Quando terminar, clique em **[!UICONTROL Save]**.

Pronto! Sua nova coluna aparecerá na tabela atual com um `Pending` status. Depois que a próxima atualização for concluída, sua coluna estará disponível para uso em métricas e relatórios.

## Mapa de referência útil {#map}

Se você estiver tendo algum problema em lembrar quais são todas as entradas ao criar uma coluna calculada, tente manter esse mapa de referência acessível ao criar:

![](../../assets/Calculated_Columns_Example.png)

## Documentação relacionada

* [Tipos de Colunas Calculadas](../data-warehouse-mgr/calc-column-types.md)
* [Tipos de Colunas Calculadas Avançadas](../data-warehouse-mgr/adv-calc-columns.md)
* [Construção [!DNL Google ECommerce] dimensões com dados de pedido e cliente](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
