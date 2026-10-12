---
title: Relatórios anuais, mensais e semanais
description: Saiba como ver facilmente as tendências ao longo do tempo e alterar a perspectiva de períodos que você pode querer comparar.
exl-id: 74cf11c3-7ce0-477f-9a28-9d782e5da3d9
role: Admin, Developer, Leader, User
feature: Reports, Dashboards
TQID: 'https://experienceleague.adobe.com/KHFNcuiZONPjk6D4ijyAfcPSrP84xWMOcTub80REqPM'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
    internal-label: Reporting
  - id: f842eedf-96a8-52c7-891d-4e56f7441a7e
    internal-label: Reports
  - id: 06e518d4-11ae-5c20-98b0-ce8ab05d7166
    internal-label: Dashboards
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 30%
---
# Relatório em Períodos de Tempo

>[!NOTE]
>
>Este tópico contém instruções para clientes que estão usando a arquitetura original e a nova arquitetura. Você está na [nova arquitetura](../../administrator/account-management/new-architecture.md) se tiver a seção [!DNL _Exibições do Data Warehouse_] disponível após selecionar [!DNL Manage Data] na barra de ferramentas principal.

O Report Builder permite ver facilmente as tendências ao longo do tempo e alterar a perspectiva dos períodos que você deseja comparar. Este tópico demonstra como configurar um painel para detalhar, permitindo criar relatórios para análises semana a semana, mês a mês e ano a ano.

![Painel que mostra comparações entre semanas, meses e anos](../../assets/Wow__mom__yoy.png)

Antes de começar, você deve examinar as perspectivas mais detalhadamente [aqui](../../tutorials/using-visual-report-builder.md) e as opções de tempo independentes [aqui](../../tutorials/time-options-visual-rpt-bldr.md).

Esta análise contém [colunas calculadas avançadas](../data-warehouse-mgr/adv-calc-columns.md).

## Colunas calculadas

* Tabela **`Sales_flat_order`**
* **Arquitetura original:** as colunas abaixo são criadas por um analista como parte do seu tíquete `[YoY WoW MoM ANALYSIS]`
* `created_at (month-day)`
* `created_at (month)`
* `created_at (day of the month)`
* `created_at (day of the week)`
* `created_at (hour of the day)`

* **Nova arquitetura:** SQL listado abaixo com uma foto de um exemplo de como criar este cálculo
  * `created_at (month-day)` [!UICONTROL Calculation]: **to_char(A, &#39;mm-dd&#39;)**
  * `created_at (month)` [!UICONTROL Calculation]: **to_char(A, &#39;mm-month&#39;)**
  * `created_at (day of the month)`&lt; [!UICONTROL Calculation]: **to_char(A, &#39;dd&#39;)**
  * `created_at (day of the week)` [!UICONTROL Calculation]: **to_char(A, &#39;d-Day&#39;)**
  * **`created_at (hour of the day)` [!UICONTROL Calculation]: &#x200B;** to_char(A, &#39;hh24&#39;)**
    ![Criar interface de coluna calculada no Data Warehouse Manager](../../assets/new-arch-create-calc.png)

## Métricas

Nenhum.

>[!NOTE]
>
>[adicione todas as novas colunas como dimensões às métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de criar novos relatórios.

## Relatórios

* **Gráfico YoY**
  * [!UICONTROL Metric]&#x200B;: `Number of orders`

  * [!UICONTROL Metric]&#x200B;: `Number of orders`
  * [!UICONTROL Time options]: `Time range (Custom)`: `2 years ago to 1 year ago`

  * [!UICONTROL Show top/bottom]: 100% melhores classificados por **`created_at (month-day)`***

* Métrica `A`: `This year`
* Métrica `B`: `Last year`
* [!UICONTROL Time period]&#x200B;: `1 year ago to 0 years ago`
* &#x200B;
  [!UICONTROL Interval]&#x200B;: `None`
* [!UICONTROL Group by]&#x200B;: `created_at (month-day)`
* &#x200B;
  [!UICONTROL Chart Type]&#x200B;: `Line`

* **Gráfico MoM**
  * [!UICONTROL Metric]&#x200B;: `Number of orders`

  * [!UICONTROL Metric]&#x200B;: `Number of orders`
  * Opções de tempo: `Time range (Custom)`: `2 months ago to 1 month ago`

  * Mostrar superior/inferior: 100% principais classificados por **`created_at (day of month)`***

* Métrica `A`: Este mês*
* Métrica `B`: mês passado*
* [!UICONTROL Time period]: um mês atrás para 0 meses atrás
* &#x200B;
  [!UICONTROL Interval]&#x200B;: None
* [!UICONTROL Group by]&#x200B;: `created_at (day of month)`
* &#x200B;
  [!UICONTROL Chart Type]&#x200B;: Line

* **Gráfico mundial**
  * [!UICONTROL Metric]&#x200B;: `Number of orders`

  * [!UICONTROL Metric]&#x200B;: `Number of orders`
  * [!UICONTROL Time options]: `Time range (Custom)`: `2 weeks ago to 1 week ago`

  * [!UICONTROL Show top/bottom]: 100% melhores classificados por `created_at (day of week)`

* Métrica `A`: `This week`
* Métrica `B`: `Last week`
* [!UICONTROL Time period]&#x200B;: `1 week ago to 0 weeks ago`
* &#x200B;
  [!UICONTROL Interval]&#x200B;: `None`
* [!UICONTROL Group by]&#x200B;: `created_at (day of week)`
* &#x200B;
  [!UICONTROL Chart Type]&#x200B;: `Line`

* **Gráfico DoD**
  * [!UICONTROL Metric]&#x200B;: `Number of orders`

  * [!UICONTROL Metric]&#x200B;: `Number of orders`
  * [!UICONTROL Time options]: `Time range (Custom)`: `2 days ago to 1 day ago`

  * [!UICONTROL Show top/bottom]: 100% melhores classificados por `created_at (hour of day)`

* Métrica `A`: `Today`
* Métrica B: `Yesterday`
* [!UICONTROL Time period]&#x200B;: `1 day ago to 0 days ago`
* &#x200B;
  [!UICONTROL Interval]&#x200B;: `None`
* [!UICONTROL Group by]&#x200B;: `created_at (hour of day)`
* &#x200B;
  [!UICONTROL Chart Type]&#x200B;: `Line`

Após compilar todos os relatórios, você pode organizá-los no painel conforme desejar. O resultado pode parecer com a imagem na parte superior desta página.
