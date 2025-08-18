---
title: 'Compreender o ambiente  [!DNL Commerce Intelligence] '
description: Saiba como trabalhar com e melhorar o ambiente do  [!DNL Commerce Intelligence] .
exl-id: 601b5fba-da02-4cc8-96ed-147c24f326f9
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 0%

---

# Seu Ambiente [!DNL Adobe Commerce Intelligence]

Ao analisar seus dados comerciais, esteja ciente desses fatores e dos equívocos comuns. Se precisar de ajuda para verificar se está usando o esquema do Commerce corretamente, não hesite em [contatar o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=pt-BR).

## [!DNL entity\_id]

Muitas tabelas contêm uma coluna chamada `entity\_id`. Em cada tabela que contém um `entity\_id`, essa coluna é usada para identificar linhas exclusivas.

Por exemplo, cada linha na tabela `sales\_order` é uma ordem única. A chave primária nesta tabela é chamada `entity\_id`. Esta coluna pode ser considerada como `order\_id`. Em uma tabela separada, `customer\_entity`, cada linha representa um cliente único. A chave primária nessa tabela também é chamada de `entity\_id`, que pode ser considerada como `customer\_id`.

Nessas tabelas, `sales\_order.entity\_id` não é igual a `customer\_entity.entity\_id`. Isso é verdadeiro para todos os conjuntos de tabelas que contêm `entity\_id`: `table\_A.entity\_id` não é igual a `table\_B.entity\_id`.

## [!DNL Guest orders]

Se você permitir que os clientes façam pedidos no seu site sem ter uma conta (pedidos de convidados), esses clientes não serão preenchidos como uma linha na tabela `customer\_entity`. Além disso, cada pedido feito por um convidado tem um valor `customer\_id` nulo na tabela `sales\_order`.

Portanto, se você quiser rastrear os comportamentos dos convidados ao longo do tempo, todas as colunas no nível do cliente devem ser calculadas na tabela `sales\_order`, usando um identificador de cliente como `customer\_email`.

Se você usar a tabela `sales\_order` como uma tabela do cliente, tenha cuidado ao criar métricas no nível do cliente. Por exemplo, considere uma métrica de receita média por vida útil. Essa métrica é usada para identificar a receita média ao longo da vida útil da sua base de clientes. Primeiro, é necessária uma nova coluna que retorne a receita vitalícia de cada cliente. Em seguida, você deve calcular a média dessa coluna para obter a receita média ao longo da vida dos clientes.

Se você puder usar a tabela `customer\_entity`, cada linha será um único cliente e cada cliente existirá somente nessa tabela uma vez. Portanto, quando você tem a coluna de receita vitalícia, tudo o que é necessário é criar uma métrica média. No entanto, se você usar a tabela `sales\_order` como tabela do cliente, é possível que haja um cliente em várias linhas. Depois de configurar a coluna receita vitalícia, cada pedido (linha) feito por um determinado cliente mostrará a receita vitalícia desse cliente, mas você só deseja incluir esse cliente uma vez na métrica média geral.

O truque aqui é que você deve adicionar um filtro à sua métrica para garantir que inclua apenas cada cliente uma vez. A Adobe incentiva você a criar e usar um conjunto de filtros chamado **Clientes que contamos**, que filtra o **número do pedido do cliente = 1** (entre outros filtros que você pode precisar excluir clientes indesejados). A adição desse filtro garante que você inclua apenas cada cliente uma vez em uma métrica no nível do cliente.

## Produtos e categorias

Os produtos podem ter várias categorias e as categorias podem ser usadas para mais de um produto. Portanto, ao configurar análises no nível da categoria, você deve ter cuidado para usar as definições corretas. Deseja a categoria de nível superior? Categoria de segundo nível? E se o produto puder se enquadrar em várias categorias de nível superior?

Imagine um par de jeans que se enquadra em três níveis de categoria diferentes, conforme definido pela implementação do Commerce: &quot;Vestuário&quot; (nível superior), &quot;Outerwear&quot; (segundo nível) e &quot;Calça&quot; (terceiro nível). Talvez você queira analisar o desempenho de categorias por número de unidades vendidas. A métrica necessária para esta análise é _Itens vendidos_, que é criada na tabela `sales\_order\_item`. Portanto, é necessário mover informações de nível de categoria para a tabela de itens. Cada linha da tabela `sales\_order\_item` tem uma `product\_id` associada. Portanto, se você souber as categorias associadas a um produto, poderá trazer essas informações para a tabela desejada.

Antes de mover quaisquer dados, primeiro você deve conhecer as associações e os filtros adequados para garantir que captura a categoria correta. Para algumas análises, você pode precisar saber &quot;Calças&quot;, mas em outras análises, &quot;Roupas&quot; pode ser mais apropriado. Essas são categorias distintas que são identificadas separadamente. Saber como cada nível de categoria é definido garante que você possa atribuir vendas de unidade à categoria apropriada para sua análise específica.

Agora, imagine que você também tem uma categoria de nível superior `Our Favorites` na home page do seu site. Talvez você tenha implementado sua loja da Commerce para incluir esses jeans nas categorias `Clothing` e `Our Favorites`. Nesse caso, esse par de jeans tem mais de uma categoria de nível superior. Nesse caso, mover uma única categoria de nível superior para a tabela `sales\_order\_item` não faz sentido, pois há várias opções. Para levar em conta isso, a Adobe sugere criar colunas sim/não que verifiquem categorias específicas. Por exemplo, as colunas `Is product in Clothing category?` e `Is product in Our Favorites category?` permitem que você verifique se um produto se enquadra nessas categorias específicas.
