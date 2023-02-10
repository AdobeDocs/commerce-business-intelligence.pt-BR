---
title: Análise do valor de duração (LTV) esperado para Pro
description: Saiba como configurar um painel que ajudará você a entender o crescimento do valor vitalício do cliente e o valor vitalício esperado de seus clientes.
exl-id: e353b92a-ff3b-466b-b519-4f86d054c0bc
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# Análise de valor vitalício esperada

Neste artigo, demonstramos como configurar um painel que ajudará você a entender o crescimento do valor do ciclo de vida do cliente e o valor esperado de vida dos clientes.

![](../../assets/exp-lifetim-value-anyalysis.png)

Essa análise só está disponível para clientes da Pro account na nova arquitetura. Se sua conta tiver acesso ao `Persistent Views` no `Manage Data` na barra lateral, você está na nova arquitetura e pode seguir as instruções listadas aqui para criar essa análise por conta própria.

Antes de começar, você deve se familiarizar com a nossa [construtor de relatórios de coorte .](../dev-reports/cohort-rpt-bldr.md)

## Colunas calculadas

Colunas a serem criadas na **ordens** tabela se estiver usando **Meses de 30 dias**:

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

Colunas a serem criadas na **`orders`** tabela se estiver usando **calendário** meses:

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

* **Clientes distintos por data do primeiro pedido**
   * Se você habilitar pedidos de convidado, use `customer_email`

* No **`orders`** tabela
* Essa métrica executa um **Contar valores distintos**
* No **`customer_id`** column
* Solicitado pela **`Customer's first order date`** timestamp

>[!NOTE]
>
>Certifique-se de [adicionar todas as novas colunas como dimensões às métricas](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de criar novos relatórios.

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
* Intervalo de tempo: `None`
* [!UICONTROL Group by]: `Calendar months between first order and this order` - mostrar tudo
* Altere o `group by` para `All time customers` métrica para Independente usando o ícone de lápis ao lado do `group by`
* Edite o `Show top/bottom` campos da seguinte maneira:
   * [!UICONTROL Revenue]: `Top 24 sorted by Calendar months between first order and this order`
   * [!UICONTROL All time customers]: `Top 24 sorted by All time customers`
   * [!UICONTROL All time customers by month since first order]: `Top 24 sorted by All time customers by month since first order`

**Receita média por mês por coorte**

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

Depois de compilar todos os relatórios, você pode organizá-los no painel como desejar. O resultado final pode parecer com a imagem na parte superior da página.

Se você tiver dúvidas ao criar essa análise ou simplesmente quiser envolver nossa equipe de serviços profissionais, [entrar em contato com o suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
