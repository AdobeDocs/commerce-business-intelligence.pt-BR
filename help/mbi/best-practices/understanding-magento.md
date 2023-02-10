---
title: Entenda seu [!DNL MBI] Ambiente
description: Saiba mais sobre como trabalhar e melhorar seu [!DNL MBI] ambiente.
exl-id: 601b5fba-da02-4cc8-96ed-147c24f326f9
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 0%

---

# Seu [!DNL MBI] Ambiente

Ao analisar seus dados de comércio, esteja ciente desses fatores e equívocos comuns. Se precisar de ajuda para garantir que você esteja usando seu esquema do Commerce corretamente, não hesite em [entrar em contato com o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

## [!DNL entity\_id]

Muitas das tabelas contêm uma coluna nomeada `entity\_id`. Em cada tabela que contém uma `entity\_id`, essa coluna é usada para identificar linhas exclusivas.

Por exemplo, cada linha no `sales\_order` tabela é um pedido exclusivo. A chave primária nesta tabela é chamada de `entity\_id`. Essa coluna pode ser considerada como `order\_id`. Em uma tabela separada, `customer\_entity`, cada linha representa um cliente exclusivo. A chave primária nesta tabela também é chamada de `entity\_id`, que podem ser consideradas como `customer\_id`.

Nessas tabelas, `sales\_order.entity\_id` não é igual `customer\_entity.entity\_id`. Isso é verdadeiro para todos os conjuntos de tabelas que contêm `entity\_id`: `table\_A.entity\_id` não é igual `table\_B.entity\_id`.

## [!DNL Guest orders]

Se você permitir que os clientes façam pedidos em seu site sem ter uma conta (pedidos de convidado), esses clientes não serão preenchidos como uma linha em seu `customer\_entity` tabela. Além disso, cada pedido colocado por um convidado terá um valor nulo `customer\_id` no `sales\_order` tabela.

Portanto, se você quiser rastrear os comportamentos dos convidados ao longo do tempo, todas as colunas em nível de cliente devem ser calculadas no relatório de `sales\_order` tabela, usando um identificador do cliente como `customer\_email`.

Se você utilizar a variável `sales\_order` como uma tabela do cliente, você deve tomar cuidado ao criar métricas no nível do cliente. Por exemplo, considere uma métrica média de receita vitalícia. Essa métrica é usada para identificar a receita média da vida útil na base do cliente. Isso primeiro requer uma nova coluna que, para cada cliente, retorne sua receita vitalícia. Em seguida, é necessário fazer a média dessa coluna para obter a receita média da vida útil de seus clientes.

Se você conseguir usar a variável `customer\_entity` cada linha é um único cliente e cada cliente só existe nessa tabela uma vez. Portanto, quando você tem a coluna receita vitalícia, basta criar uma métrica média. No entanto, se você usar a variável `sales\_order` como sua tabela de clientes, um cliente pode potencialmente existir em várias linhas. Após configurar a coluna receita vitalícia, cada pedido (linha) colocado por um determinado cliente mostrará a receita vitalícia desse cliente; mas você só deseja incluir esse cliente uma vez na métrica média geral.

O truque aqui é adicionar um filtro à métrica que garante que você inclua apenas cada cliente uma vez. Recomendamos criar e usar um conjunto de filtros chamado **Clientes que contamos** que filtrará para **Número do pedido do cliente = 1** (entre outros filtros, talvez seja necessário excluir clientes indesejados). Adicionar esse filtro garante que você inclua cada cliente apenas uma vez em uma métrica no nível do cliente.

## Produtos e categorias

Os produtos podem ter várias categorias, e as categorias podem ser usadas para mais de um produto. Portanto, ao configurar análises no nível da categoria, você deve ter cuidado para usar as definições corretas. Deseja a categoria de nível superior? Categoria de segundo nível? E se o produto puder se encaixar em várias categorias de nível superior?

Imagine um par de jeans que caiba em três níveis de categoria diferentes, conforme definido por uma implementação do Commerce: &quot;Vestuário&quot; (nível superior), &quot;Vestuário externo&quot; (segundo nível) e &quot;Calças&quot; (terceiro nível). Talvez você queira analisar o desempenho de suas categorias por número de unidades vendidas. A métrica necessária para essa análise é _Itens vendidos_, que é construído na variável `sales\_order\_item` tabela. Portanto, é necessário mover informações a nível de categoria para a tabela de itens. Cada linha no `sales\_order\_item` terá um `product\_id`, portanto, se você souber as categorias associadas a um produto, poderá trazer essas informações para a tabela desejada.

Antes de mover quaisquer dados, você deve primeiro saber as associações e filtros adequados para garantir que você pegue a categoria correta. Para algumas análises, talvez seja necessário saber &quot;Calças&quot;, mas em outras análises, o &quot;Vestuário&quot; pode ser mais apropriado. São categorias distintas identificadas separadamente. Saber como cada nível de categoria é definido garantirá que você possa atribuir vendas unitárias à categoria apropriada para sua análise específica.

Agora, imagine que você também tem uma categoria de nível superior de &quot;Nossos Favoritos&quot; na página inicial do seu site. Talvez você tenha implementado sua loja de Comércio para incluir esses jeans tanto na categoria &quot;Vestuário&quot; quanto na categoria &quot;Nossos Favoritos&quot;. Em caso afirmativo, esse par de jeans terá mais de uma categoria de nível superior. Nesse caso, mover uma única categoria de nível superior para a `sales\_order\_item` não faz muito sentido, pois há várias opções. Para considerar isso, sugerimos criar colunas sim/não que verifiquem categorias específicas. Por exemplo, `Is product in Clothing category?` e `Is product in Our Favorites category?` permitem verificar se um produto se enquadra nessas categorias específicas.
