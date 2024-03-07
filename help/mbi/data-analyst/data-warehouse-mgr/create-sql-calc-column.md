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

Este tópico descreve o objetivo e os usos da `Calculation` tipo de coluna, que pode ser adicionado às tabelas usando o [Gerenciador de Data Warehouse](../data-warehouse-mgr/tour-dwm.md). Abaixo, explica o que os cálculos SQL fazem, por que eles são usados, o processo para criar um cálculo SQL e inclui dois exemplos.

**Explicação**

No passado, as colunas que eram consideradas `advanced` só pode ser feita por um analista na equipe de Sucesso do cliente aqui em [!DNL Adobe Commerce Intelligence]. Agora todo o poder está nas mãos do usuário final, e colunas avançadas podem ser criadas na forma de `SQL Calculation` colunas no novo [!DNL Commerce Intelligence] arquitetura.

A variável `Calculation` O tipo de coluna, agora disponível como uma opção no Gerenciador de Datas Warehouse, é uma mesma operação de tabela que permite transformar as colunas em uma tabela usando a lógica PostgreSQL. Documentação sobre as funções e os operadores que podem ser usados no `Calculation` O tipo de coluna pode ser encontrado no site PostgreSQL [aqui](https://www.postgresql.org/docs/9.6/functions.html).

As diferentes colunas que podem ser criadas com o `Calculation` As colunas são quase ilimitadas, mas a maioria das colunas pode ser criada usando instruções IF-THEN e aritmética básica, que é usada nos exemplos abaixo.

**Exemplo 1: é o último pedido do cliente?**

A maioria das contas tem uma coluna chamada `Is customer's last order?` em seu `orders` tabela para executar análises sobre taxas de compra repetidas e clientes com churn. Se sua conta estiver na nova arquitetura, essa coluna será criada usando uma `Calculation` e podem ser vistas na captura de tela abaixo:

![](../../assets/Is_customer_s_last_order.png)

A variável `Is customer's last order?` A coluna usa as entradas `Customer's lifetime number of orders` e `Customer's order number` com alias como `A` e `B` respectivamente.

Linha por linha, o significado do PostgreSQL é:

* case: inicia uma série de instruções If - Then
* quando `A` é nulo ou `B` é nulo então nulo: se qualquer entrada estiver vazia, a saída também deverá estar vazia. Isso é para evitar erros de SQL
* quando `A=B` depois `Yes`: Se `Customer's lifetime number of orders` igual a `Customer's order number` para esta linha e retornar `Yes`. Portanto, se um cliente tiver feito quatro pedidos, a linha referente à quarta ordem retornará `Yes` para `Is customer's last order?`
* else `No`: Se nenhuma das outras quando as instruções forem atendidas, retorne `No`
* end: Isso encerra as instruções If - Then

Os valores possíveis que podem ser retornados por essa coluna (`NULL`, `Yes`, `No`) contêm caracteres não numéricos, portanto, o tipo de dados aqui é String.

**Exemplo 2: Valor total do item da ordem (quantidade * preço)**

Muitos clientes gostam de analisar a receita no nível do item, fatiando-a por campos como `product name` ou `category`. A maioria dos bancos de dados não fornece a receita de um produto em um pedido; em vez disso, eles fornecem a quantidade vendida no pedido e o preço do item.

Para permitir análises de receita de produtos, a maioria das contas tem uma coluna chamada `Order item total value (quantity * price)` em seu `Orders Items` tabela. Se sua conta estiver na nova arquitetura, essa coluna também será criada usando um `Calculation` e podem ser vistas na captura de tela abaixo:

![](../../assets/Order_item_total_value.png)

No esquema Comércio, a variável `Order item total value (quantity * price)` A coluna usa as entradas `qty ordered` e `base price` com alias como `A` e `B` respectivamente.

Os valores retornados por essa nova coluna estão em dólares e centavos, portanto, o tipo de dados correto é `Decimal(10,2)`.

**Mecânica**

Um novo `Calculation` a coluna pode ser adicionada a uma tabela navegando até **[!DNL Manage Data > Data Warehouse]** conforme mostrado abaixo:

![](../../assets/blobid2.png)

Aqui, você pode criar um `Calculation` seguindo as etapas abaixo:

1. Selecione a tabela na qual você deseja adicionar a variável `Calculation` coluna.
1. Na tabela correta, clique em **[!UICONTROL Create New Column]** na parte superior direita da tela.
1. No `Select a definition` selecione `Same Table`.
1. Selecionar `Calculation` como o `column definition equation`.
1. Insira o nome da coluna.
1. Escolha o `input` colunas da tabela que são usadas na lógica da nova coluna. Cada coluna adicionada recebe um alias de letra, de modo que a primeira coluna é `A`, o segundo é `B` e assim por diante.
1. Na janela, digite a lógica do PostgreSQL para a nova coluna usando os aliases de letra das entradas. O cálculo SQL deve ser limitado a uma única definição de coluna, incluindo toda a lógica entre as instruções SELECT e FROM de uma consulta SQL. As palavras-chave SQL que usam qualquer uma das letras de entrada devem estar em minúsculas. Por exemplo, ao usar o `CASE` deve ser escrito em minúsculas - `case`. O sistema presume que uma caixa alta `A` refere-se a uma das entradas.
1. Escolha o tipo de dados apropriado.
   * `Integer` - Número inteiro
   * `Decimal(10,2)` - um número decimal com 10 dígitos totais, dos quais 2 à direita da casa decimal
   * `String` - Qualquer tipo de texto ou série de caracteres que use números não numéricos
   * `Datetime` - `yyyy-MM-dd hh:mm:ss` formato

1. Clique em **[!UICONTROL test column]**. Isso gera uma lista de cinco valores de teste para cada uma de suas entradas e mostra o resultado da lógica da etapa 6 para cada conjunto de valores de teste. Se qualquer parte do SQL gerar um erro, a mensagem de erro apropriada será retornada. Os resultados de amostra só podem ser gerados se todas as colunas de entrada forem campos nativos. Se qualquer uma das colunas de entrada for calculada, você deverá validar os resultados adicionando a coluna a uma métrica e exibindo no Report Builder visual

1. Quando estiver satisfeito com os resultados, clique em **[!UICONTROL Save]**. A coluna ativa para uso.
