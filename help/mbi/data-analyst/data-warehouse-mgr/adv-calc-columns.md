---
title: Tipos de Colunas Calculadas Avançadas
description: Saiba mais sobre as noções básicas para a maioria dos casos de uso de coluna — mas talvez você queira colunas calculadas que sejam um pouco mais complexas do que o Gerenciador de Datas Warehouse pode criar.
exl-id: 9871fa19-95b3-46e4-ae2d-bd7c524d12db
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# Tipos de Colunas Calculadas Avançadas

Muitas análises que você pode tentar criar envolvem o uso de um **nova coluna** que você deseja `group by` ou `filter by`. O [Criação de colunas calculadas](../data-warehouse-mgr/creating-calculated-columns.md) O tutorial aborda as noções básicas da maioria dos casos de uso, mas você pode desejar que a coluna calculada seja um pouco mais complexa do que o Gerenciador de Datas Warehouse pode criar.
{: #top}

Esses tipos de colunas podem ser criadas por nossa equipe de analistas do Data Warehouse. Para definir uma nova coluna calculada, forneça as seguintes informações:

1. O **`definition`** desta coluna (incluindo entradas, fórmulas ou formatação)
1. O **`table`** na qual você deseja criar a coluna
1. Qualquer **`example data points`** que descrevem o que a coluna deve conter

Estes são alguns exemplos comuns de colunas calculadas avançadas que os usuários costumam achar úteis:

* [Evento Order (ou rank) sequencialmente](#compareevents)
* [Encontre o tempo entre dois eventos](#twoevents)
* [Comparar valores de evento sequencial](#sequence)
* [Converter moeda](#currency)
* [Converter fusos horários](#timezone)
* [Algo mais](#else)

## Estou tentando ordenar os eventos sequencialmente {#compareevents}

Chamamos isso de **número do evento** coluna calculada. Isso significa que estamos tentando encontrar a sequência na qual os eventos ocorreram para um proprietário de evento específico, como um cliente ou usuário.

Veja um exemplo:

| **`event\_id`** | **`owner\_id`** | **`timestamp`** | **`Owner's event number`** |
|-----|-----|-----|-----|
| 1 | `A` | 2015-01-01 00:00:00 | 1 |
| 2 | `B` | 2015-01-01 00:30:00 | 1 |
| 3 | `A` | 2015-01-01 02:00:00 | 2 |
| 4 | `A` | 2015-01-02 13:00:00 | 3 |
| 5 | `B` | 2015-01-03 13:00:00 | 2 |

{style=&quot;table-layout:auto&quot;}

Uma coluna calculada com o número de eventos pode ser usada para observar as diferenças de comportamento entre os eventos de primeira hora, repetição ou enésima nos dados.

Deseja ver a coluna Número do pedido do Cliente em ação? Clique na imagem para vê-la usada como uma dimensão Agrupar por em um relatório.

![Usar uma coluna calculada do número de evento para Agrupar pelo número de ordem do cliente.](../../assets/EventNumber.gif)<!--{: style="max-width: 500px;"}-->

Para criar esse tipo de coluna calculada, precisamos saber:

* A tabela na qual você deseja criar essa coluna
* O campo que identifica o proprietário dos eventos (`owner\_id` neste exemplo)
* O campo pelo qual você deseja ordenar os eventos (`timestamp` neste exemplo)

[voltar ao início](#top)

## Estou tentando encontrar o tempo entre dois eventos. {#twoevents}

Chamamos isso de `date difference` coluna calculada. Isso significa que estamos tentando encontrar o tempo entre dois eventos pertencentes a um único registro, com base nos carimbos de data e hora do evento.

Veja um exemplo:

| `id` | `timestamp\_1` | `timestamp\_2` | `Seconds between timestamp\_2 and timestamp\_1` |
|-----|-----|-----|-----|
| `A` | 2015-01-01 00:00:00 | 2015-01-01 12:30:00 | 45000 |
| `B` | 2015-01-01 08:00:00 | 2015-01-01 10:00:00 | 7200 |

{style=&quot;table-layout:auto&quot;}

Uma coluna calculada de diferença de data pode ser usada para criar uma métrica que calcula o tempo médio ou mediano entre dois eventos. Clique na imagem abaixo para verificar como a função `Average time to first order` é usada em um relatório.

![Usando uma coluna calculada de diferença de data para calcular o Tempo médio para a primeira ordem.](../../assets/DateDifference.gif)<!--{: style="max-width: 500px;"}-->

Para criar esse tipo de coluna calculada, precisamos saber:

* A tabela na qual você deseja criar essa coluna
* Os dois carimbos de data e hora entre os quais você deseja saber a diferença

[voltar ao início](#top)

## Estou tentando comparar valores de eventos sequenciais. {#sequence}

Chamamos isso de **comparação de evento sequencial**. Isso significa que estamos tentando encontrar o delta entre um valor (moeda, número, carimbo de data e hora) e o valor correspondente do evento anterior do proprietário.

Veja um exemplo:

| **`event\_id`** | **`owner\_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|-----|-----|-----|-----|
| 1 | `A` | 2015-01-01 00:00:00 | NULL |
| 2 | `B` | 2015-01-01 00:30:00 | NULL |
| 3 | `A` | 2015-01-01 02:00:00 | 7720 |
| 4 | `A` | 2015-01-02 13:00:00 | 126000 |
| 5 | `B` | 2015-01-03 13:00:00 | 217800 |

{style=&quot;table-layout:auto&quot;}

Uma comparação de evento sequencial pode ser usada para encontrar o tempo médio ou mediano entre cada evento sequencial. Clique na imagem abaixo para ver o **Tempo médio entre pedidos** métricas em ação.

=![Usar uma coluna calculada de comparação de eventos sequenciais para calcular o Tempo médio e o Tempo médio entre as ordens.](../../assets/SeqEventComp.gif)<!--{: style="max-width: 500px;"}-->

Para criar esse tipo de coluna calculada, precisamos saber:

* A tabela na qual você deseja criar essa coluna
* O campo que identifica o proprietário dos eventos (`owner\_id` no exemplo)
* O campo de valor que você gostaria de ver a diferença entre para cada evento sequencial (`timestamp` neste exemplo)

[voltar ao início](#top)

## Estou tentando converter moeda. {#currency}

A **conversão de moeda** coluna calculada converte valores de transação de uma moeda registrada em uma moeda de relatório, com base na taxa de câmbio no momento do evento.

Veja um exemplo:

| **`id`** | **`timestamp`** | **`transaction\_value\_EUR`** | **`transaction\_value\_USD`** |
|-----|-----|-----|-----|
| `1` | 2015-01-01 00:00:00 | 30º | 33,57 |
| `2` | 2015-01-02 00:00:00 | 50º | 55,93 |

{style=&quot;table-layout:auto&quot;}

Para criar esse tipo de coluna calculada, precisamos saber:

* A tabela na qual você deseja criar essa coluna
* A coluna do valor da transação que você deseja converter
* A coluna que indica a moeda em que os dados foram registrados (normalmente um código ISO)
* Moeda de reporte preferencial

[voltar ao início](#top)

## Estou tentando converter fusos horários. {#timezone}

A **conversão de fuso horário** coluna calculada converte os carimbos de data e hora de uma fonte de dados específica do fuso horário registrado para um fuso horário de relatório.

Veja um exemplo:

| **`id`** | **`timestamp\_UTC`** | **`timestamp\_ET`** |
|-----|-----|-----|
| `1` | 2015-01-01 00:00:00 | 2014-12-31 19:00:00 |
| `2` | 2015-01-01 12:00:00 | 2015-01-01 07:00:00 |

{style=&quot;table-layout:auto&quot;}

Para criar esse tipo de coluna calculada, precisamos saber:

* A tabela na qual você deseja criar essa coluna
* A coluna de carimbo de data e hora que você deseja converter
* O fuso horário em que os dados foram registrados
* Fuso horário preferencial do relatório

[voltar ao início](#top)

## Estou tentando fazer algo que não está listado aqui. {#else}

Não se preocupe. Só porque não está listado aqui não significa que não seja possível. Nossa equipe de analistas de Datas Warehouse tem você abordado.

Para definir uma nova coluna calculada, [enviar um tíquete de suporte](../../guide-overview.md) com detalhes sobre exatamente o que você gostaria de criar.

## Documentação relacionada

* [Criação de colunas calculadas](../data-warehouse-mgr/creating-calculated-columns.md)
* [Tipos de coluna calculados](../data-warehouse-mgr/calc-column-types.md)
* [Construção [!DNL Google ECommerce] dimensões com dados de pedido e cliente](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
