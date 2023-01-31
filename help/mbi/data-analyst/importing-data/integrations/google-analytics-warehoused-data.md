---
title: Dados do Google Analytics Warehouse Esperados
description: Saiba como interagir com seus dados armazenados em Google Analytics.
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# Esperado [!DNL Google Analytics] Dados do Warehouse

>[!NOTE]
>
>Exige [Permissões de administrador](../../../administrator/user-management/user-management.md).

>[!NOTE]
>
>Algumas informações foram usadas com permissão de nossos amigos em [[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics).

[!DNL Google Analytics Warehoused] integração no [!DNL MBI] utiliza o [!DNL Google Analytics] [API dos Relatórios principais](https://developers.google.com/analytics/devguides/reporting/core/v3/).

>[!NOTE]
>
>Para evitar resultados inesperados ou sem sentido, confirme se as dimensões usadas são [compatível com a(s) métrica(s)](https://developers.google.com/analytics/devguides/reporting/core/dimsmets) você usa no `Report Builder`.

Uma única tabela - chamada de `report` - será criado na sua Data Warehouse.

O esquema desta tabela será composto pelas Métricas e Dimension selecionadas durante o processo de configuração e duas outras colunas: `start-date` e `end-date`.

Por exemplo, se você selecionou as seguintes Métricas e Dimension durante a configuração:

* `Metrics`: `ga:users`
* `Dimensions`: `ga:month`

A tabela seria parecida com o exemplo abaixo.

| **Nome da coluna** | **Descrição** |
|-----|-----|
| `\_id` | Essa coluna é a `primary key`. |
| `\_rjm\_record\_hash` | [!DNL MBI] identificador exclusivo. Essa coluna é criada por [!DNL MBI]. |
| `\_updated\_at` | Essa coluna contém a última vez que a linha de dados foi atualizada. Essa coluna é criada por [!DNL MBI]. |
| `start-date` | Identificação de que dia a linha serve. |
| `end-date` | Identificação de que dia a linha serve. |
| `month` | Dimensão selecionada: Mês da sessão, um número inteiro de dois dígitos de 01 a 12. |
| `users` | Métrica selecionada: O número total de usuários do período solicitado. |

{style=&quot;table-layout:auto&quot;}

## Lembrete: Diferença entre o Google Analytics Warehouse e a integração ao vivo

O principal diferencial é que uma integração é armazenada ([!DNL Google Analytics Warehoused]) e o outro não é ([!DNL Google Analytics Live]). No caso de [!DNL Google Analytics Warehoused], isso permite a manipulação do [!DNL Google Analytics] e oferece a capacidade de combinar [!DNL Google Analytics] e outras fontes de dados para criar relatórios esclarecedores.

Vamos olhar para [!DNL Google Analytics] campanhas de publicidade para obter um exemplo do que pode ser feito de um ponto de vista de manipulação. Suponha que você tenha várias campanhas publicitárias para o quarto trimestre com nomes diferentes. As campanhas foram resultado de uma iniciativa de marketing específica. Com dados armazenados no , podemos criar uma nova coluna que localiza os nomes de campanha em questão e retorna o nome da iniciativa do T4 de `Operation Dumbo`.

O aspecto de combinação permite [!DNL Google Analytics] dados a juntar a outros dados para realizar análises. Por exemplo, considere `Total Time On Site By Ad Campaign` dados de [!DNL Google Analytics] e junte-se a isso `Total Spent Per Campaign` dados de [!DNL Facebook Ads] para obter uma imagem completa de quanto de envolvimento está lhe custando.

Com o [!DNL Google Analytics Live] integração, por outro lado, a cada [!DNL Google Analytics] é como um silo pequeno que não está armazenado em seu [!DNL MBI] data warehouse.

## Relacionadas:

* [Conexão [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)
