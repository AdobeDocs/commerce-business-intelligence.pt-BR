---
title: Criando e Usando uma Coluna Calculada SQL
description: Saiba como colunas avançadas podem ser criadas no formato de colunas de Cálculo SQL na nova arquitetura do Adobe Commerce Intelligence.
exl-id: f16e4ee4-ed73-4ddb-b701-1fe3db14346a
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, SQL Report Builder, Commerce Tables
source-git-commit: 8090c2e0f17f0e8d3bdec668ce546206bf024691
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 0%

---

# Criar uma Coluna Calculada de SQL

Este tópico descreve a finalidade e os usos do tipo de coluna `Calculation`, que pode ser adicionado às tabelas usando o [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md). Abaixo, explica o que os cálculos SQL fazem, por que eles são usados, o processo para criar um cálculo SQL e inclui dois exemplos.

**Explicação**

Antigamente, as colunas consideradas `advanced` só podiam ser feitas por um analista da equipe de Sucesso do cliente aqui em [!DNL Adobe Commerce Intelligence]. Agora todo o poder está nas mãos do usuário final, e colunas avançadas podem ser criadas no formato de `SQL Calculation` colunas na nova arquitetura [!DNL Commerce Intelligence].

O tipo de coluna `Calculation`, agora disponível como uma opção no Data Warehouse Manager, é uma mesma operação de tabela que permite transformar as colunas em uma tabela usando a lógica PostgreSQL. A documentação sobre as funções e operadores que podem ser usados no tipo de coluna `Calculation` pode ser encontrada no site PostgreSQL [aqui](https://www.postgresql.org/docs/9.6/functions.html).

As diferentes colunas que podem ser criadas com a coluna `Calculation` são quase ilimitadas, mas a maioria das colunas pode ser criada usando instruções IF-THEN e aritmética básica, que é usada nos exemplos abaixo.

**Exemplo 1: é o último pedido do cliente?**

A maioria das contas tem uma coluna chamada `Is customer's last order?` na tabela `orders` para executar análises em taxas de compra repetidas e clientes com churn. Se sua conta estiver na nova arquitetura, essa coluna será criada usando uma coluna `Calculation` e poderá ser vista na captura de tela abaixo:

![](../../assets/Is_customer_s_last_order.png)

A coluna `Is customer's last order?` usa as entradas `Customer's lifetime number of orders` e `Customer's order number` com alias como `A` e `B`, respectivamente.

Linha por linha, o significado do PostgreSQL é:

* case: inicia uma série de instruções If - Then
* quando `A` é nulo ou `B` é nulo então nulo: Se qualquer entrada estiver vazia, então a saída também deve estar vazia. Isso é para evitar erros de SQL
* quando `A=B` então `Yes`: se `Customer's lifetime number of orders` for igual a `Customer's order number` para esta linha, então retorne `Yes`. Portanto, se um cliente tiver feito quatro pedidos, a linha referente à quarta ordem retornará `Yes` para `Is customer's last order?`
* else `No`: Se nenhuma das outras instruções when for atendida, retornar `No`
* end: Isso encerra as instruções If - Then

Os valores possíveis que podem ser retornados por esta coluna (`NULL`, `Yes`, `No`) contêm caracteres não numéricos, portanto, o tipo de dados aqui é String.

**Exemplo 2: valor total do item da ordem (quantidade * preço)**

Muitos clientes gostam de analisar a receita no nível do item, fatiando-a por campos como `product name` ou `category`. A maioria dos bancos de dados não fornece a receita de um produto em um pedido; em vez disso, eles fornecem a quantidade vendida no pedido e o preço do item.

Para habilitar análises de receita de produtos, a maioria das contas tem uma coluna chamada `Order item total value (quantity * price)` na tabela `Orders Items`. Se sua conta estiver na nova arquitetura, essa coluna também será criada usando uma coluna `Calculation` e poderá ser vista na captura de tela abaixo:

![](../../assets/Order_item_total_value.png)

No esquema Commerce, a coluna `Order item total value (quantity * price)` usa as entradas `qty ordered` e `base price` com alias como `A` e `B`, respectivamente.

Os valores retornados por esta nova coluna estão em dólares e centavos, portanto, o tipo de dados correto é `Decimal(10,2)`.

**Mecânica**

Uma nova coluna `Calculation` pode ser adicionada a uma tabela navegando até **[!DNL Manage Data > Data Warehouse]** como mostrado abaixo:

![](../../assets/blobid2.png)

Aqui, você pode criar uma coluna `Calculation` seguindo as etapas abaixo:

1. Selecione a tabela na qual você deseja adicionar a coluna `Calculation`.
1. Enquanto estiver na tabela correta, clique em **[!UICONTROL Create New Column]** na parte superior direita da tela.
1. Na lista suspensa `Select a definition`, selecione `Same Table`.
1. Selecione `Calculation` como `column definition equation`.
1. Insira o nome da coluna.
1. Escolha as `input` colunas da tabela que são usadas na lógica da nova coluna. Cada coluna adicionada recebe um alias de letra, de modo que a primeira coluna é `A`, a segunda é `B` e assim por diante.
1. Na janela, digite a lógica do PostgreSQL para a nova coluna usando os aliases de letra das entradas. O cálculo SQL deve ser limitado a uma única definição de coluna, incluindo toda a lógica entre as instruções SELECT e FROM de uma consulta SQL. As palavras-chave SQL que usam qualquer uma das letras de entrada devem estar em minúsculas. Por exemplo, ao usar a instrução `CASE`, ela deve ser gravada em minúsculas - `case`. O sistema presume que um `A` maiúsculo se refere a uma das entradas.
1. Escolha o tipo de dados apropriado.
   * `Integer` - Número inteiro
   * `Decimal(10,2)` - um número decimal com 10 dígitos totais, dos quais 2 estão à direita do ponto decimal
   * `String` - Qualquer tipo de texto ou série de caracteres que use números não numéricos
   * `Datetime` - Formato `yyyy-MM-dd hh:mm:ss`

1. Clique em **[!UICONTROL test column]**. Isso gera uma lista de cinco valores de teste para cada uma de suas entradas e mostra o resultado da lógica da etapa 6 para cada conjunto de valores de teste. Se qualquer parte do SQL gerar um erro, a mensagem de erro apropriada será retornada. Os resultados de amostra só podem ser gerados se todas as colunas de entrada forem campos nativos. Se qualquer uma das colunas de entrada for calculada, você deverá validar os resultados adicionando a coluna a uma métrica e exibindo no Visual Report Builder

1. Quando estiver satisfeito com os resultados, clique em **[!UICONTROL Save]**. A coluna ativa para uso.
