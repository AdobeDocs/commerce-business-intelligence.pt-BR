---
title: Criar e usar visualizações do Data Warehouse
description: Saiba mais sobre um método de criação de novas tabelas armazenadas modificando uma tabela existente ou unindo ou consolidando várias tabelas usando SQL.
exl-id: 5aa571c9-7f38-462c-8f1b-76a826c9dc55
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 6%

---

# Trabalhar com visualizações do Data Warehouse

Este documento descreve a finalidade e os usos do `Data Warehouse Views` acessível navegando até **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**. Abaixo está uma explicação do que ele faz e como criar exibições, bem como um exemplo de como usar o `Data Warehouse Views` para consolidar dados de gastos do [!DNL Facebook] e do [!DNL AdWords].

## Propósito geral

O recurso `Data Warehouse Views` é um método de criar novas tabelas armazenadas modificando uma tabela existente ou unindo ou consolidando várias tabelas usando SQL. Depois que um `Data Warehouse View` é criado e processado por um ciclo de atualização, ele é preenchido no Data Warehouse como uma nova tabela na lista suspensa `Data Warehouse Views`, como mostrado abaixo:

![](../../assets/Data_Warehouse.png)

Aqui, a nova visualização funciona como qualquer outra tabela, permitindo criar novas colunas calculadas ou métricas e relatórios.

`Data Warehouse Views` são usados principalmente para consolidar várias tabelas semelhantes, mas distintas, de modo que todos os relatórios possam ser criados em uma única tabela nova. Alguns exemplos comuns incluem a consolidação de tabelas de um banco de dados herdado e um banco de dados em tempo real para combinar dados históricos e atuais, ou combinar várias fontes de anúncios, como o Facebook e o AdWords, em uma única tabela `Consolidated ad spend`.

Se você estiver familiarizado com SQL, ambos os exemplos de consolidação usam a função `UNION`, mas você pode usar qualquer sintaxe e funções PostgreSQL ao criar uma nova visualização.

## Criação e gerenciamento de visualizações do Data Warehouse

É possível criar novos `Data Warehouse Views` e excluir modos de exibição existentes navegando até **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**, conforme mostrado abaixo:

![](../../assets/Data_Warehouse_Views.png)

Aqui, é possível criar uma visualização seguindo as instruções de exemplo abaixo:

1. Se estiver observando uma exibição existente, clique em **[!UICONTROL New Data Warehouse View]** para abrir uma janela de consulta em branco. Se uma janela de query em branco já estiver aberta, continue para a próxima etapa.
1. Nomeie a exibição digitando o campo `View Name`. O nome fornecido aqui determina o nome de exibição da exibição na Data Warehouse. `View names` estão limitados a letras minúsculas, números e sublinhados (_). Todos os outros caracteres são proibidos.
1. Insira sua consulta na janela denominada `Select Query`, usando a sintaxe PostgreSQL padrão.

   >[!NOTE]
   >
   >Sua consulta deve fazer referência a nomes de coluna específicos. O uso do caractere `*` para selecionar todas as colunas não é permitido.

1. Quando terminar, clique em **[!UICONTROL Save]** para salvar sua exibição. Seu modo de exibição tem temporariamente um status de `Pending` até que seja processado pelo próximo ciclo de atualização completo, momento em que o status muda para `Active`. Depois de ser processada por uma atualização, sua visualização fica pronta para uso nos relatórios.

É importante mencionar que, após salvar, a consulta subjacente usada para gerar um `Data Warehouse View` não pode ser editada. Se você precisar ajustar a estrutura de um `Data Warehouse View`, crie um modo de exibição e migre manualmente quaisquer colunas calculadas, métricas ou relatórios do modo de exibição original para o novo. Quando a migração estiver concluída, você poderá excluir com segurança a exibição original. Como `Data Warehouse Views` não são editáveis, a Adobe recomenda que você teste a saída de sua consulta usando o `SQL Report Builder` antes de salvar sua consulta como uma Exibição do Data Warehouse.

## Exemplo: dados de [!DNL Facebook] e [!DNL Google AdWords]

Veja um dos exemplos mencionados anteriormente neste artigo: consolidação de dados de gastos do [!DNL Facebook] e do [!DNL AdWords] em uma nova tabela de anúncios consolidados. Normalmente, isso envolve a consolidação de duas tabelas, com conjuntos de dados de amostra abaixo:

`Ad source: Google AdWords`

`Table name: campaigns67890`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | eee | 60 | 05-05-2017 00:00:00 | 2000 | 10,2 |
| 2 | ggg | 40 | 23/05/2017 :00:00 | 900 | 4,6 |
| 3 | aaa | 22 | 06-2017-12 00:00:00 | 400 | 2,5 |
| 4 | eee | 350 | 2017-06-30 00:00:00 | 14500 | 35 |
| 5 | fff | 280 | 2017-07-10 00:00:00 | 10200 | 28,5 |

`Ad source: Facebook`

`Table name: facebook_ads_insights_12345`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | aaa | 25 | 01-05-2017 00:00:00 | 1200 | 5 |
| 2 | ddd | 12 | 05-2017-15 00:00:00 | 800 | 2,5 |
| 3 | aaa | 40 | 2017-05-22:00:00 | 2000 | 7 |
| 4 | aaa | 110 | 08-06-2017 00:00:00 | 6000 | 10 |
| 5 | ccc | 5 | 06/07/2017 :00:00 | 300 | 1,2 |

Para criar uma única tabela de gastos com anúncios contendo campanhas [!DNL Facebook] e [!DNL Google AdWords], você deve gravar uma consulta SQL e usar a função `UNION ALL`. Uma instrução `UNION ALL` é usada com mais frequência para combinar várias consultas SQL distintas ao anexar os resultados de cada consulta a uma única saída.

Há alguns requisitos de uma instrução `UNION` que vale a pena mencionar, conforme descrito na [documentação](https://www.postgresql.org/docs/8.3/queries-union.html) do PostgreSQL:

* Todas as consultas devem retornar o mesmo número de colunas
* As colunas correspondentes devem ter tipos de dados idênticos

Ao executar uma instrução `UNION` ou `UNION ALL`, os nomes das colunas na saída final refletem o nome das colunas na primeira consulta.

Normalmente, a consolidação dos dados de gastos do [!DNL Facebook] e do [!DNL Google AdWords] em um `Data Warehouse View` requer a criação de uma tabela com sete colunas, com uma consulta semelhante à seguinte:

```sql
    SELECT
        "_id" as id,
        'AdWords' as ad_source,
        "date",
        "campaign",
        "adCost" as spend,
        "impressions",
        "adClicks" as clicks
    FROM campaigns67890
    UNION
    SELECT
        "_id" as id,
        'Facebook' as ad_source,
        "date_start" as date,
        "campaign_name" as campaign,
        "spend",
        "impressions",
        "clicks"
    FROM facebook_ads_insights_12345
```

Alguns pontos importantes sobre o exposto acima:

* Por motivos de clareza, todas as colunas recebem alias acima, de modo que os nomes correspondam a todas as consultas. No entanto, isso não é um requisito. A ordem em que as colunas são chamadas nas consultas SELECT determina como elas são alinhadas.
* Uma nova coluna chamada `ad_source` é criada para facilitar a filtragem de dados [!DNL AdWords] ou [!DNL Facebook]. Lembre-se de que esta consulta combina todos os dados de ambas as tabelas. Se você não criar uma coluna como `ad_source`, não há uma maneira fácil de identificar gastos de uma origem específica.

Salvar a consulta acima como um `Data Warehouse View` cria uma tabela com gastos de [!DNL Facebook] e [!DNL AdWords], semelhante ao seguinte:

| **`id`** | **`ad_source`** | **`date`** | **`campaign`** | **`spend`** | **`impressions`** | **`clicks`** |
|--- |--- |--- |--- |--- |--- |--- |
| **1** | [!DNL Facebook] | 01-05-2017 00:00:00 | aaa | 5 | 1200 | 25 |
| **1** | [!DNL Google AdWords] | 05-05-2017 00:00:00 | eee | 10,2 | 2000 | 60 |
| **2** | [!DNL Facebook] | 05-2017-15 00:00:00 | ddd | 2,5 | 800 | 12 |
| **2** | [!DNL Google AdWords] | 23/05/2017 :00:00 | ggg | 4,6 | 900 | 40 |
| **3** | [!DNL Facebook] | 2017-05-22:00:00 | aaa | 7 | 2000 | 40 |
| **3** | [!DNL Google AdWords] | 06-2017-12 00:00:00 | aaa | 2,5 | 400 | 22 |
| **4** | [!DNL Facebook] | 08-06-2017 00:00:00 | aaa | 10 | 6000 | 110 |
| **4** | [!DNL Google AdWords] | 2017-06-30 00:00:00 | eee | 35 | 14500 | 350 |
| **5** | [!DNL Facebook] | 06/07/2017 :00:00 | ccc | 1,2 | 300 | 5 |
| **5** | [!DNL Google AdWords] | 2017-07-10 00:00:00 | fff | 28,5 | 10200 | 280 |

Em vez de criar um conjunto separado de métricas de marketing para cada fonte de anúncio, você pode criar um único conjunto de métricas usando a tabela acima para capturar todos os seus anúncios.

**Procurando ajuda adicional?**

A gravação de SQL e a criação de `Data Warehouse Views` não estão incluídas no Suporte Técnico. No entanto, a [equipe de Serviços](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) oferece assistência para a criação de exibições. A equipe de suporte pode ajudar em tudo, desde migrar um banco de dados herdado por um novo banco de dados até criar uma única visualização do Data Warehouse para fins de análise específica.

Normalmente, a criação de um novo `Data Warehouse View` com a finalidade de consolidar de 2 a 3 tabelas estruturadas de forma semelhante requer cinco horas de serviço, o que se traduz em aproximadamente US$ 1.250 de trabalho. No entanto, abaixo estão alguns fatores comuns que podem aumentar o investimento esperado necessário:

* Consolidação de mais de três tabelas em uma única visualização
* Criação de mais de uma visualização do Data Warehouse
* Lógica de ligação complexa ou condições de filtragem
* Consolidação de duas ou mais tabelas com estruturas de dados diferentes
