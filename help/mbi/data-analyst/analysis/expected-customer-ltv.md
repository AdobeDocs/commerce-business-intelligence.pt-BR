---
title: Análise do valor vitalício esperado (LTV) para Pro
description: Saiba como configurar um painel que ajuda você a entender o crescimento do valor vitalício do cliente e o valor vitalício esperado de seus clientes.
exl-id: e353b92a-ff3b-466b-b519-4f86d054c0bc
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---

# Análise do valor vitalício esperado

Este artigo demonstra como configurar um painel de controle que ajuda você a entender o crescimento do valor vitalício do cliente e o valor vitalício esperado de seus clientes.

![](../../assets/exp-lifetim-value-anyalysis.png)

Essa análise só está disponível para clientes da conta Pro na nova arquitetura. Se sua conta tiver acesso ao `Persistent Views` recurso no `Manage Data` barra lateral, você está na nova arquitetura e pode seguir as instruções listadas aqui para criar essa análise você mesmo.

Antes de começar, você deseja se familiarizar com o [construtor de relatórios de coorte.](../dev-reports/cohort-rpt-bldr.md)

## Colunas calculadas

Colunas para criar no **pedidos** tabela se estiver usando **30 dias por mês**:

* [!UICONTROL Column name]: `Months between first order and this order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: A = `Seconds between customer's first order date and this order`
* 
   [!UICONTROL Datatype]: `Integer`
* **Definição:**`case when A is null then null when A <= 0 then '1'::int else (ceil(A)/2629800)::int end`

* [!UICONTROL Column name]: `Months since order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: A = `created_at`
* 
   [!UICONTROL Datatype]: `Integer`
* Definição: `case when created_at is null then null else (ceil((extract(epoch from current_timestamp) - extract(epoch from created_at))/2629800))::int end`

Colunas para criar no **`orders`** tabela se estiver usando **calendário** meses:

* [!UICONTROL Column name]: `Calendar months between first order and this order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column inputs]:
   * `A` = `created_at`
   * `B` = `Customer's first order date`

* 
   [!UICONTROL Datatype]: `Integer`
* Definição: `case when (A::date is null) or (B::date is null) then null else ((date_part('year',A::date) - date_part('year',B::date))*12 + date_part('month',A::date) - date_part('month',B::date))::int end`

* [!UICONTROL Column name]: `Calendar months since order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: `A` = `created_at`
* 
   [!UICONTROL Datatype]: `Integer`
* **Definição:**`case when A is null then null else ((date_part('year',current_timestamp::date) - date_part('year',A::date))*12 + date_part('month',current_timestamp::date) - date_part('month',A::date))::int end`

* [!UICONTROL Column name]: `Is in current month? (Yes/No)`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: A = `created_at`
* 
   [!UICONTROL Datatype]: `String`
* Definição: `case when A is null then null when (date_trunc('month', current_timestamp::date))::varchar = (date_trunc('month', A::date))::varchar then 'Yes' else 'No' end`

## Métricas

### Instruções de métrica

Métricas para criar

* **Clientes distintos pela data da primeira ordem**
   * Se você ativar ordens de convidados, use `customer_email`

* No **`orders`** tabela
* Essa métrica executa uma **Contar valores distintos**
* No **`customer_id`** coluna
* Ordenado por **`Customer's first order date`** carimbo de data e hora

>[!NOTE]
>
>Verifique se [adicionar todas as novas colunas como dimensões às métricas](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de criar novos relatórios.

## Relatórios

### Instruções do relatório

**Receita esperada por cliente por mês**

* Métrica `A`: `Revenue (hide)`
   * `Calendar months between first order and this order` `<= X` (Escolha um número razoável para X, por exemplo, 24 meses)
   * `Is in current month?` = `No`

* 
   [!UICONTROL Métrica]: `Revenue`
* [!UICONTROL Filter]:

* Métrica `B`: `All time customers (hide)`
   * `Is in current month?` = `No`

* [!UICONTROL Metric]: `New customers by first order date`
* [!UICONTROL Filter]:

* Métrica `C`: `All time customers by month since first order (hide)`
   * `Calendar months since order` `<= X`
   * `Is in current month?` = `No`

* [!UICONTROL Metric]: `New customers by first order date`
* [!UICONTROL Filter]:

* [!UICONTROL Formula]: `Expected revenue`
* [!UICONTROL Formula]: `A / (B - C)`
* 

   [!UICONTROL Format]: `Currency`

Outros detalhes do gráfico

* [!UICONTROL Time period]: `All time`
* Intervalo: `None`
* [!UICONTROL Group by]: `Calendar months between first order and this order` - mostrar tudo
* Altere o `group by` para o `All time customers` para Independente usando o ícone de lápis ao lado da `group by`
* Edite o `Show top/bottom` seguintes campos:
   * [!UICONTROL Revenue]: `Top 24 sorted by Calendar months between first order and this order`
   * [!UICONTROL All time customers]: `Top 24 sorted by All time customers`
   * [!UICONTROL All time customers by month since first order]: `Top 24 sorted by All time customers by month since first order`

**Receita mensal média por coorte**

* Métrica `A`: `Revenue`
* 
   [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]: `Customer's first order date`
* [!UICONTROL Perspective]: `Average value per cohort member`

**Receita média cumulativa por mês por coorte**

* Métrica `A`: `Revenue`
* 
   [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]: `Customer's first order date`
* [!UICONTROL Perspective]: `Cumulative average value per cohort member`

Após compilar todos os relatórios, você pode organizá-los no painel conforme desejar. O resultado pode parecer com a imagem na parte superior da página.

Se você tiver dúvidas ao criar essa análise ou se quiser simplesmente envolver a equipe de serviços profissionais, [entre em contato com o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
