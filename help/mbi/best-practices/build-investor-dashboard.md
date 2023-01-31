---
title: Criar um painel para investidores
description: Saiba como criar um painel para investidores.
exl-id: 917e7628-3498-4413-a7e1-61799989a7dd
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# Criar painel do investidor

Muitos de nossos clientes estão trabalhando com investidores e precisam compartilhar informações da plataforma com eles, mas os painéis criados para tomar decisões comerciais diárias podem não ser o que um investidor está procurando. Aqui abordamos algumas práticas recomendadas para criar um painel abrangente, mas simples, ideal para compartilhar com investidores ativos e potenciais.

Aqui está o que você precisa criar relatórios para seu painel de investidores:

## Relatórios escalares

* **[!UICONTROL All-time revenue]**
* **[!UICONTROL Distinct buyers]**
* **[!UICONTROL All-time number of orders]**
* **[!UICONTROL AOV]**
* **[!UICONTROL Items sold]**

## Relatórios visuais

* **[!UICONTROL Revenue by quarter]**
   * Métrica - Receita
* **[!UICONTROL Revenue from 1st time orders vs repeat orders]**
   * Métrica - Receita da primeira ordem
   * Filtro - O número do pedido do usuário é igual a 1
   * Métrica 2 - Repetir receita da ordem
      * Filtro - O número do pedido do usuário é maior que 1
   * Desmarque a caixa para Vários eixos Y
   * Alterar para um gráfico de Coluna empilhada
* **[!UICONTROL AOV by quarter]**
   * Métrica 1 - Receita
      * Ocultar esta métrica
   * Métrica 2 - Número de pedidos
      * Ocultar esta métrica
   * Fórmula - AOV
      * A/B
* **[!UICONTROL All-time revenue by source]**
   * Métrica - Receita
   * Agrupar por cliente `utm_source`
* **[!UICONTROL Revenue from top 10 products]**
   * Métrica - receita do produto
      * Ocultar o gráfico
      * Agrupar pelo nome do produto. Selecione todos os produtos.
      * Defina o intervalo de tempo como All-Time (Todas as horas)
      * Defina o intervalo de tempo como Nenhum
      * Em &quot;Mostrar de cima/baixo&quot;, mostrar apenas os 10 principais classificados por lucro do produto
* **[!UICONTROL Cumulative distinct buyers by quarter]**
   * Métrica - Compradores distintos
      * Perspectiva - Cumulativa
* **[!UICONTROL Site visits - New vs. repeat by month]**
* Sessões

Com um [!DNL Google Analytics] , você pode incluir relatórios sobre:

* Visitas ao site
* Índice de conversão

Com o [Serviços de enriquecimento de dados de comércio](https://business.adobe.com/products/magento/magento-commerce.html), você pode incluir relatórios sobre:

* Clientes únicos por estado/região, idade, gênero.

## Outras dicas

* Use um [convenção de nomenclatura](../best-practices/naming-elements.md)
* Compartilhar o painel com usuários investidores
* Ou envie-o via **[!UICONTROL Automated email summary]**(../data-user/export-data/email-summaries.md)
* Crie apenas um painel. Isso facilitará a manutenção do conteúdo e você saberá exatamente o que seus investidores estão vendo.

Organize seus relatórios com cuidado e preste atenção nos detalhes. Depois de concluído, o painel será semelhante ao abaixo:

![](../../mbi/assets/investor-dboard-example.png)
