---
title: Relatórios anuais, mensais e semanais
description: Saiba como visualizar facilmente tendências ao longo do tempo e alterar a perspectiva de períodos que você pode querer comparar.
exl-id: 74cf11c3-7ce0-477f-9a28-9d782e5da3d9
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Relatório ao longo de períodos

>[!NOTE]
>
>Este artigo contém instruções para clientes que estão usando a arquitetura original e a nova arquitetura. Você está no [nova arquitetura](../../administrator/account-management/new-architecture.md) se você tiver o _Exibições de Data Warehouse_ seção disponível após a seleção `Manage Data` na barra de ferramentas principal.

O construtor de relatórios permite ver facilmente as tendências ao longo do tempo e alterar a perspectiva de períodos que você pode querer comparar. Neste artigo, demonstraremos como configurar um painel para ir um nível mais fundo e permitir que você crie relatórios para análise semana a semana, mês a mês e ano a ano.

![](../../assets/Wow__mom__yoy.png)

Antes de começar, você quer se familiarizar com as perspectivas de exploração com mais detalhes [here](../../tutorials/using-visual-report-builder.md) bem como opções de tempo independentes [here](../../tutorials/time-options-visual-rpt-bldr.md).

Esta análise contém [colunas calculadas avançadas](../data-warehouse-mgr/adv-calc-columns.md).

## Colunas calculadas

* **`Sales_flat_order`** tabela
* **Arquitetura original:** as colunas abaixo serão criadas por um analista como parte de seu `[YoY WoW MoM ANALYSIS]` ticket
* `created_at (month-day)`
* `created_at (month)`
* `created_at (day of the month)`
* `created_at (day of the week)`
* `created_at (hour of the day)`

* **Nova arquitetura:** SQL listado abaixo com uma foto de exemplo para criar este cálculo
   * `created_at (month-day)` [!UICONTROL Calculation]: **to_char(A, &#39;mm-dd&#39;)**
   * `created_at (month)` [!UICONTROL Calculation]: **to_char(A, &#39;mm-mês&#39;)**
   * `created_at (day of the month)`&lt; [!UICONTROL Calculation]: **to_char(A, &#39;dd&#39;)**
   * `created_at (day of the week)` [!UICONTROL Calculation]: **to_char(A, &#39;d-Day&#39;)**
   * **`created_at (hour of the day)` [!UICONTROL Calculation]: **to_char(A, &#39;hh24&#39;)**

      ![](../../assets/new-arch-create-calc.png)

## Métricas

Nenhum.

>[!NOTE]
>
>Certifique-se de [adicionar todas as novas colunas como dimensões às métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de criar novos relatórios.

## Relatórios

* **Gráfico YoY**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 years ago to 1 year ago`

   * [!UICONTROL Show top/bottom]: Os 100% principais classificados por **`created_at (month-day)`***

* Métrica `A`: `This year`
* Métrica `B`: `Last year`
* [!UICONTROL Time period]: `1 year ago to 0 years ago`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (month-day)`
* 
   [!UICONTROL Chart Type]: `Line`

* **Gráfico MoM**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * Opções de tempo: `Time range (Custom)`: `2 months ago to 1 month ago`

   * Mostrar parte superior/inferior: Os 100% principais classificados por **`created_at (day of month)`***

* Métrica `A`: Este mês*
* Métrica `B`: Mês passado*
* [!UICONTROL Time period]: 1 mês atrás a 0 meses atrás
* 
   [!UICONTROL Interval]: None
* [!UICONTROL Group by]: `created_at (day of month)`
* 
   [!UICONTROL Chart Type]: Line

* **Gráfico de W**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 weeks ago to 1 week ago`

   * [!UICONTROL Show top/bottom]: Os 100% principais classificados por `created_at (day of week)`

* Métrica `A`: `This week`
* Métrica `B`: `Last week`
* [!UICONTROL Time period]: `1 week ago to 0 weeks ago`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (day of week)`
* 
   [!UICONTROL Chart Type]: `Line`

* **Gráfico DoD**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 days ago to 1 day ago`

   * [!UICONTROL Show top/bottom]: Os 100% principais classificados por `created_at (hour of day)`

* Métrica `A`: `Today`
* Métrica B: `Yesterday`
* [!UICONTROL Time period]: `1 day ago to 0 days ago`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (hour of day)`
* 
   [!UICONTROL Chart Type]: `Line`

Depois de compilar todos os relatórios, você pode organizá-los no painel como desejar. O resultado final pode parecer com a imagem na parte superior desta página.
