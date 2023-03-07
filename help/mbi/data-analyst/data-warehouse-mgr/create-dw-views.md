---
title: Criar e usar visualizações do Data Warehouse
description: Saiba mais sobre um método de criação de novas tabelas armazenadas modificando uma tabela existente ou unindo ou consolidando várias tabelas usando SQL.
exl-id: 5aa571c9-7f38-462c-8f1b-76a826c9dc55
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '1064'
ht-degree: 9%

---

# Trabalhar com visualizações do Data Warehouse

Este documento descreve o objetivo e os usos do `Data Warehouse Views` acessível navegando até **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**. Abaixo está uma explicação do que ele faz e como criar visualizações, bem como um exemplo de como usar o `Data Warehouse Views` para consolidar [!DNL Facebook] e [!DNL AdWords] dados de gastos.

## Propósito geral

A variável `Data Warehouse Views` o recurso é um método de criar novas tabelas armazenadas modificando uma tabela existente ou unindo ou consolidando várias tabelas usando SQL. Uma vez a `Data Warehouse View` foi criada e processada por um ciclo de atualização, ela é preenchida na Data Warehouse como uma nova tabela no `Data Warehouse Views` conforme mostrado abaixo:

![](../../assets/Data_Warehouse.png)

Aqui, a nova visualização funciona como qualquer outra tabela, permitindo criar novas colunas calculadas ou métricas e relatórios.

`Data Warehouse Views` são usados principalmente para consolidar várias tabelas semelhantes, mas diferentes, de modo que todos os relatórios possam ser criados em uma única tabela nova. Alguns exemplos comuns incluem a consolidação das tabelas de um banco de dados herdado e um banco de dados em tempo real para combinar dados históricos e atuais ou combinar várias fontes de anúncios, como o Facebook e o AdWords, em um único `Consolidated ad spend` tabela.

Se você estiver familiarizado com o SQL, esses dois exemplos de consolidação usarão o `UNION` mas você pode usar qualquer sintaxe e função PostgreSQL ao criar uma nova visualização.

## Criação e gerenciamento de visualizações de Data Warehouse

Novo `Data Warehouse Views` podem ser criadas e as exibições existentes podem ser excluídas navegando até **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**, conforme mostrado abaixo:

![](../../assets/Data_Warehouse_Views.png)

Aqui, é possível criar uma visualização seguindo as instruções de exemplo abaixo:

1. Se estiver observando uma view existente, clique em **[!UICONTROL New Data Warehouse View]** para abrir uma janela de consulta em branco. Se uma janela de query em branco já estiver aberta, continue para a próxima etapa.
1. Nomeie a exibição digitando o `View Name` campo. O nome fornecido aqui determina o nome de exibição da exibição na Data Warehouse. `View names` são limitados a letras minúsculas, números e sublinhados (_). Todos os outros caracteres são proibidos.
1. Insira sua consulta na janela intitulada `Select Query`, utilizando a sintaxe PostgreSQL padrão.
   >[!NOTE]
   >
   >Sua consulta deve fazer referência a nomes de coluna específicos. A utilização dos `*`caractere para selecionar todas as colunas não é permitido.

1. Quando terminar, clique em **[!UICONTROL Save]** para salvar a visualização. Sua visualização tem temporariamente um `Pending` até ser processado pelo próximo ciclo de atualização completo, momento em que o status muda para `Active`. Depois de ser processada por uma atualização, sua visualização fica pronta para uso nos relatórios.

É importante mencionar que, após salvar, o query subjacente usado para gerar um `Data Warehouse View` não pode ser editado. Se você precisar ajustar a estrutura de um `Data Warehouse View`, você deve criar uma visualização e migrar manualmente todas as colunas calculadas, métricas ou relatórios da visualização original para a nova. Quando a migração estiver concluída, você poderá excluir com segurança a exibição original. Porque `Data Warehouse Views` não são editáveis, o Adobe recomenda que você teste a saída de seu query usando o `SQL Report Builder` antes de salvar sua consulta como uma Exibição de Data Warehouse.

## Exemplo: [!DNL Facebook] e [!DNL Google AdWords] dados

Veja um dos exemplos mencionados anteriormente neste artigo: consolidação [!DNL Facebook] e [!DNL AdWords] gastar dados em uma nova tabela de anúncios consolidados. Normalmente, isso envolve a consolidação de duas tabelas, com conjuntos de dados de amostra abaixo:

`Ad source: Google AdWords`

`Table name: campaigns67890`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | eee | 60 | 2017-05-05 00:00:00 | 2000 | 10.2 |
| 2 | ggg | 40 | 2017-05-23 00:00:00 | 900 | 4.6 |
| 3 | aaa | 22 | 2017-06-12 00:00:00 | 400 | 2.5 |
| 4 | eee | 350 | 2017-06-30 00:00:00 | 14500 | 35 |
| 5 | fff | 280 | 2017-07-10 00:00:00 | 10200 | 28.5 |

`Ad source: Facebook`

`Table name: facebook_ads_insights_12345`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | aaa | 25 | 2017-05-01 00:00:00 | 1200 | 5 |
| 2 | ddd | 12 | 2017-05-15 00:00:00 | 800 | 2.5 |
| 3 | aaa | 40 | 2017-05-22 00:00:00 | 2000 | 7 |
| 4 | aaa | 110 | 2017-06-08 00:00:00 | 6000 | 10 |
| 5 | ccc | 5 | 2017-07-06 00:00:00 | 300 | 1.2 |

Para criar uma única tabela de gastos com anúncios contendo [!DNL Facebook] e [!DNL AdWords] campanhas, você deve escrever uma consulta SQL e usar o método `UNION ALL` função. A `UNION ALL` é usada com mais frequência para combinar várias consultas SQL distintas, ao anexar os resultados de cada consulta a uma única saída.

Há alguns requisitos para uma `UNION` que vale a pena mencionar, conforme descrito no PostgreSQL [documentação](https://www.postgresql.org/docs/8.3/queries-union.html):

* Todas as consultas devem retornar o mesmo número de colunas
* As colunas correspondentes devem ter tipos de dados idênticos

Ao executar uma `UNION` ou `UNION ALL` Os nomes das colunas na saída final refletem a nomeação das colunas na primeira query.

Normalmente, a consolidação do seu [!DNL Facebook] e [!DNL Google AdWords] gastar dados em um `Data Warehouse View` exigem a criação de uma tabela com sete colunas, com uma consulta semelhante à abaixo:

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
* Uma nova coluna chamada `ad_source` O foi criado para facilitar a filtragem de [!DNL AdWords] ou [!DNL Facebook] dados. Lembre-se de que esta consulta combina todos os dados de ambas as tabelas. Se você não criar uma coluna como `ad_source`No entanto, não há uma maneira fácil de identificar gastos de uma determinada fonte.

Salvando a consulta acima como um `Data Warehouse View` cria uma tabela com ambos [!DNL Facebook] e [!DNL AdWords] gastos, semelhantes aos abaixo:

| **`id`** | **`ad_source`** | **`date`** | **`campaign`** | **`spend`** | **`impressions`** | **`clicks`** |
|--- |--- |--- |--- |--- |--- |--- |
| **1** | [!DNL Facebook] | 2017-05-01 00:00:00 | aaa | 5 | 1200 | 25 |
| **1** | [!DNL Google AdWords] | 2017-05-05 00:00:00 | eee | 10.2 | 2000 | 60 |
| **2** | [!DNL Facebook] | 2017-05-15 00:00:00 | ddd | 2.5 | 800 | 12 |
| **2** | [!DNL Google AdWords] | 2017-05-23 00:00:00 | ggg | 4.6 | 900 | 40 |
| **3** | [!DNL Facebook] | 2017-05-22 00:00:00 | aaa | 7 | 2000 | 40 |
| **3** | [!DNL Google AdWords] | 2017-06-12 00:00:00 | aaa | 2.5 | 400 | 22 |
| **4** | [!DNL Facebook] | 2017-06-08 00:00:00 | aaa | 10 | 6000 | 110 |
| **4** | [!DNL Google AdWords] | 2017-06-30 00:00:00 | eee | 35 | 14500 | 350 |
| **5** | [!DNL Facebook] | 2017-07-06 00:00:00 | ccc | 1.2 | 300 | 5 |
| **5** | [!DNL Google AdWords] | 2017-07-10 00:00:00 | fff | 28.5 | 10200 | 280 |

Em vez de criar um conjunto separado de métricas de marketing para cada fonte de anúncio, agora é possível criar um único conjunto de métricas usando a tabela acima para capturar todos os seus anúncios.

**Procurando ajuda adicional?**

Gravação de SQL e criação `Data Warehouse Views` O não está incluído no Suporte técnico da. No entanto, a equipe de Serviços oferece assistência na criação de visualizações. A equipe de suporte pode ajudar em tudo, desde migrar um banco de dados herdado por um novo banco de dados até criar uma única Exibição do Data Warehouse para fins de análise específica.

Normalmente, a criação de um novo `Data Warehouse View` para fins de consolidação de 2 a 3 tabelas estruturadas de forma semelhante, são necessárias cinco horas de serviço, o que se traduz em aproximadamente US$ 1.250 de trabalho. No entanto, abaixo estão alguns fatores comuns que podem aumentar o investimento esperado necessário:

* Consolidação de mais de três tabelas em uma única visualização
* Criação de mais de uma visualização de Data Warehouse
* Lógica de ligação complexa ou condições de filtragem
* Consolidação de duas ou mais tabelas com estruturas de dados diferentes
