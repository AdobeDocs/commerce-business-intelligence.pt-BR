---
title: Entenda seus [!DNL Commerce Intelligence] Ambiente
description: Saiba como trabalhar com a e melhorar o seu [!DNL Commerce Intelligence] ambiente.
exl-id: 601b5fba-da02-4cc8-96ed-147c24f326f9
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 0%

---

# Seu [!DNL Adobe Commerce Intelligence] Ambiente

Ao analisar seus dados comerciais, esteja ciente desses fatores e dos equívocos comuns. Se precisar de assistência para verificar se está usando o esquema do Commerce corretamente, não hesite em [entre em contato com o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## [!DNL entity\_id]

Muitas das tabelas contêm uma coluna chamada `entity\_id`. Em cada tabela que contém um `entity\_id`, essa coluna é usada para identificar linhas exclusivas.

Por exemplo, cada linha na variável `sales\_order` A tabela é um pedido exclusivo. A chave primária nesta tabela é chamada `entity\_id`. Essa coluna pode ser considerada como `order\_id`. Em uma tabela separada, `customer\_entity`, cada linha representa um cliente único. A chave primária nessa tabela também é chamada de `entity\_id`, que pode ser considerada como `customer\_id`.

Nesses quadros, `sales\_order.entity\_id` não é igual a `customer\_entity.entity\_id`. Isso é verdadeiro para todos os conjuntos de tabelas que contêm `entity\_id`: `table\_A.entity\_id` não é igual a `table\_B.entity\_id`.

## [!DNL Guest orders]

Se você permitir que os clientes façam pedidos no seu site sem ter uma conta (pedidos de convidados), esses clientes não serão preenchidos como uma linha no `customer\_entity` tabela. Além disso, cada pedido feito por um convidado tem um valor nulo `customer\_id` valor no `sales\_order` tabela.

Portanto, se você quiser rastrear os comportamentos dos convidados ao longo do tempo, todas as colunas no nível do cliente devem ser calculadas na variável `sales\_order` tabela, usando um identificador do cliente, como `customer\_email`.

Se você usar o `sales\_order` como uma tabela do cliente, você deve ter cuidado ao criar métricas no nível do cliente. Por exemplo, considere uma métrica de receita média por vida útil. Essa métrica é usada para identificar a receita média ao longo da vida útil da sua base de clientes. Primeiro, é necessária uma nova coluna que retorne a receita vitalícia de cada cliente. Em seguida, você deve calcular a média dessa coluna para obter a receita média ao longo da vida dos clientes.

Se você conseguir usar o `customer\_entity` tabela, cada linha é um único cliente e cada cliente existe apenas nessa tabela uma vez. Portanto, quando você tem a coluna de receita vitalícia, tudo o que é necessário é criar uma métrica média. No entanto, se você usar a variável `sales\_order` como sua tabela do cliente, um cliente pode existir em várias linhas. Depois de configurar a coluna receita vitalícia, cada pedido (linha) feito por um determinado cliente mostrará a receita vitalícia desse cliente, mas você só deseja incluir esse cliente uma vez na métrica média geral.

O truque aqui é que você deve adicionar um filtro à sua métrica para garantir que inclua apenas cada cliente uma vez. O Adobe incentiva você a criar e usar um conjunto de filtros chamado **Clientes que contamos** que filtra para **Número da ordem do cliente = 1** (entre outros filtros, talvez seja necessário excluir clientes indesejados). A adição desse filtro garante que você inclua apenas cada cliente uma vez em uma métrica no nível do cliente.

## Produtos e categorias

Os produtos podem ter várias categorias e as categorias podem ser usadas para mais de um produto. Portanto, ao configurar análises no nível da categoria, você deve ter cuidado para usar as definições corretas. Deseja a categoria de nível superior? Categoria de segundo nível? E se o produto puder se enquadrar em várias categorias de nível superior?

Imagine um par de jeans que se enquadra em três níveis de categoria diferentes, conforme definido por uma implementação do Commerce: &quot;Vestuário&quot; (nível superior), &quot;Outerwear&quot; (segundo nível) e &quot;Calças&quot; (terceiro nível). Talvez você queira analisar o desempenho de categorias por número de unidades vendidas. A métrica necessária para essa análise é _Itens vendidos_, que tem por base o `sales\_order\_item` tabela. Portanto, é necessário mover informações de nível de categoria para a tabela de itens. Cada linha no `sales\_order\_item` a tabela tem um associado `product\_id`, portanto, se você souber as categorias associadas a um produto, poderá trazer essas informações para a tabela desejada.

Antes de mover quaisquer dados, primeiro você deve conhecer as associações e os filtros adequados para garantir que captura a categoria correta. Para algumas análises, você pode precisar saber &quot;Calças&quot;, mas em outras análises, &quot;Roupas&quot; pode ser mais apropriado. Essas são categorias distintas que são identificadas separadamente. Saber como cada nível de categoria é definido garante que você possa atribuir vendas de unidade à categoria apropriada para sua análise específica.

Agora, imagine que você também tem um `Our Favorites` categoria de nível superior na página inicial do site. Talvez você tenha implementado sua loja do Commerce para incluir esses jeans nas `Clothing` categoria e o `Our Favorites` categoria. Nesse caso, esse par de jeans tem mais de uma categoria de nível superior. Nesse caso, mover uma única categoria de nível superior para o `sales\_order\_item` A tabela não faz sentido, pois há várias opções. Para levar em conta isso, o Adobe sugere criar colunas sim/não que verifiquem categorias específicas. Por exemplo, `Is product in Clothing category?` e `Is product in Our Favorites category?` As colunas permitem verificar se um produto se enquadra nessas categorias específicas.
