---
title: Criar colunas calculadas
description: Saiba como consolidar dados de diferentes fontes.
exl-id: 668cbc77-6a96-4687-9f40-3635b1be5c66
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---

# Criar Colunas Calculadas

Ao analisar seus dados, é útil consolidar dados de diferentes fontes. Deseja agrupar a receita por fonte de aquisição, vinculando os dados dos `orders` tabela e [!DNL Google Analytics] dados? Talvez você queira agrupar a receita por gênero do cliente ou associar um atributo do cliente aos dados da transação para segmentação. Este tópico discute como fazer isso.

Antes de começar, o Adobe recomenda que você revise o [Guia de Tipos de Coluna Calculada](../../data-analyst/data-warehouse-mgr/calc-column-types.md) para obter informações sobre os tipos de colunas que você pode criar no Gerenciador de Datas Warehouse, juntamente com suas definições e exemplos.

1. Para começar, clique em **[!DNL Manage Data > Data Warehouse]**.

1. Clique na tabela em que deseja criar uma coluna. Por exemplo, se você deseja criar um `Customer Gender` para segmentação de receita, você selecionaria a variável `sales_flat_order` tabela.

1. O esquema de tabela é exibido. Clique em **[!UICONTROL Create New Column]**.

1. Nomeie sua coluna. Por exemplo, `Customer Gender`.

1. Selecione a definição da coluna. É aqui que a [Guia de Tipos de coluna calculada](../data-warehouse-mgr/calc-column-types.md) vem a calhar!

1. Para certos tipos de colunas, são necessárias um pouco mais de informações para criar a coluna corretamente:

   * Para `One to Many` (unidos) e `Many to One` (agregar), é necessário selecionar as tabelas e colunas.

   * Para um `Same Table calculation`, é necessário selecionar o campo de data desejado na lista suspensa.

Se você estiver criando uma `One to Many` (unidos) ou `Many to One` (agregado), é necessário selecionar um caminho para conectar as duas tabelas. Nesta etapa, você pode usar um caminho existente ou criar um.

>[!NOTE]
>
>Lembre-se de definir corretamente a tabela como muitas ou uma!

* Se desejar, é possível aplicar [filtros](../../data-user/reports/ess-manage-data-filters.md) à nova coluna.

* Quando terminar, clique em **[!UICONTROL Save]**.

Sua nova coluna aparece na tabela atual com um `Pending` status. Quando a próxima atualização for concluída, a coluna estará disponível para uso nas métricas e nos relatórios.

## Mapa de referência prático {#map}

Se você estiver tendo problemas para lembrar o que são todas as entradas ao criar uma coluna calculada, tente manter esse mapa de referência disponível quando estiver criando:

![](../../assets/Calculated_Columns_Example.png)

## Documentação relacionada

* [Tipos de Colunas Calculadas](../data-warehouse-mgr/calc-column-types.md)
* [Tipos de Coluna Calculados Avançados](../data-warehouse-mgr/adv-calc-columns.md)
* [Criação [!DNL Google ECommerce] dimensões com dados de pedido e cliente](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
