---
title: Criando e Usando uma Coluna Calculada SQL
description: Saiba como colunas avançadas podem ser criadas na forma de colunas de Cálculo SQL na nova arquitetura MBI.
exl-id: f16e4ee4-ed73-4ddb-b701-1fe3db14346a
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---

# Criar uma Coluna Calculada SQL

Este tópico descreve a finalidade e os usos do `Calculation` tipo de coluna: que pode ser adicionado às tabelas usando o [Gerenciador de Datas Warehouse](../data-warehouse-mgr/tour-dwm.md). Abaixo está uma explicação do que os cálculos SQL fazem, por que são usados, o processo para criar um cálculo SQL e dois exemplos.

**Explicação**

Anteriormente, colunas que eram consideradas `advanced` só pode ser feito por um analista da equipe de sucesso do cliente aqui em [!DNL MBI]. Agora todo o poder está nas mãos do usuário final, e colunas avançadas podem ser criadas na forma de `SQL Calculation` nas novas colunas [!DNL MBI] arquitetura.

O `Calculation` o tipo de coluna, agora disponível como uma opção no Gerenciador de Datas Warehouse, é uma operação de tabela que permite transformar as colunas em uma tabela usando a lógica PostgreSQL. Documentação sobre as funções e operadores que podem ser usados no `Calculatio`Um tipo de coluna pode ser encontrado no site PostgreSQL [here](https://www.postgresql.org/docs/9.6/static/functions.html).

As diferentes colunas que podem ser criadas com a variável `Calculation` são quase ilimitadas, mas a maioria das colunas pode ser criada usando instruções IF-THEN e aritmética básica, que será usada nos exemplos abaixo.

**Exemplo 1: O último pedido do cliente é?**

A maioria das contas tem uma coluna chamada `Is customer's last order?` no `orders` tabela para executar análises sobre taxas de compra repetidas e clientes vinculados. Se sua conta estiver na nova arquitetura, essa coluna será criada usando um `Calculation` e pode ser visto na captura de tela abaixo:

![](../../assets/Is_customer_s_last_order.png)

O `Is customer's last order?` usa as entradas `Customer's lifetime number of orders` e `Customer's order number` alias como `A` e `B` respectivamente.

Linha por linha, o significado do PostgreSQL é:

* caso: Isso inicia uma série de instruções If - Then
* when `A` é nulo ou `B` é nulo e nulo: Se uma das entradas estiver vazia, a saída também deverá estar vazia. Isso é para evitar erros de SQL
* when `A=B` then `Yes`: If `Customer's lifetime number of orders` igual `Customer's order number` para esta linha, retornar `Yes`. Portanto, se um cliente tiver feito quatro pedidos, a linha para seu quarto pedido retornará `Yes` para `Is customer's last order?`
* else `No`: Se nenhuma das outras instruções quando forem atendidas, retorne `No`
* fim: Isso encerra as instruções If - Then

Os valores possíveis que podem ser retornados por esta coluna (`NULL`, `Yes`, `No`) contém caracteres não numéricos, portanto, o tipo de dados aqui é String.

**Exemplo 2: Valor total do item de ordem (quantidade * preço)**

Muitos de nossos clientes gostam de analisar a receita no nível do item, dividindo-a por campos como `product name` ou `category`. A maioria dos bancos de dados não fornece a receita de um produto em um pedido; em vez disso, fornecem a quantidade vendida no pedido e o preço do item.

Para permitir análises de receita do produto, a maioria das contas tem uma coluna chamada `Order item total value (quantity * price)` no `Orders Items` tabela. Se sua conta estiver na nova arquitetura, essa coluna também será criada usando uma `Calculation` e pode ser visto na captura de tela abaixo:

![](../../assets/Order_item_total_value.png)

No schema Comércio , a variável `Order item total value (quantity * price)` usa as entradas `qty ordered` e `base price` alias como `A` e `B` respectivamente.

Os valores que serão retornados por esta nova coluna serão um dólar e centavos, então o tipo de dados correto é `Decimal(10,2)`.

**Mecânica**

Um novo `Calculation` pode ser adicionada a uma tabela navegando até **[!DNL Manage Data > Data Warehouse]** conforme mostrado abaixo:

![](../../assets/blobid2.png)

Aqui você pode criar um novo `Calculation` seguindo as etapas abaixo:

1. Selecione a tabela na qual deseja adicionar o `Calculation` coluna.
1. Na tabela correta, clique em **[!UICONTROL Create New Column]** na parte superior direita da tela.
1. No `Select a definition` lista suspensa, selecione `Same Table`.
1. Selecionar `Calculation` como `column definition equation`.
1. Insira o nome da coluna.
1. Escolha a `input` colunas da tabela que será usada na lógica da nova coluna. Cada coluna adicionada receberá um alias de letra, de modo que a primeira coluna será `A`, o segundo será `B` e assim por diante.
1. Na janela , digite a lógica PostgreSQL para sua nova coluna usando os aliases de letras de suas entradas. O cálculo SQL deve ser limitado a uma única definição de coluna, incluindo toda a lógica entre as instruções SELECT e FROM de uma consulta SQL. Observe que as palavras-chave SQL que usam qualquer uma das letras de entrada devem estar em minúsculas. Por exemplo, ao usar a variável `CASE` deve ser escrito em minúsculas - `case`. O sistema parte do princípio de que um `A` refere-se a uma das entradas.
1. Escolha o tipo de dados apropriado.
   * `Integer` - Número inteiro
   * `Decimal(10,2)` - um número decimal com 10 algarismos totais, dos quais 2 à direita da casa decimal
   * `String` - Qualquer tipo de texto ou série de caracteres que use não números
   * `Datetime` - aaaa-MM-dd hh:mm:formato ss

1. Clique em **[!UICONTROL test column]**. Isso gerará uma lista de 5 valores de teste para cada entrada e mostrará o resultado da lógica da etapa 6 para cada conjunto de valores de teste. Se qualquer parte do SQL gerar um erro, a mensagem de erro apropriada será retornada. Observe que os resultados da amostra só podem ser gerados se todas as colunas de entrada forem campos nativos. Se qualquer coluna de entrada for calculada, será necessário validar os resultados adicionando a coluna a uma métrica e visualizando no Visual Report Builder
1. Quando estiver satisfeito com os resultados, clique em **[!UICONTROL Save]** e sua coluna estará disponível para uso.
