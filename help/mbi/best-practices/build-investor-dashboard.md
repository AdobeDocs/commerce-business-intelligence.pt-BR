---
title: Criação de um painel para investidores
description: Aprenda a buildr um painel para investidores.
exl-id: 917e7628-3498-4413-a7e1-61799989a7dd
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---

# Criar painel do Investor

Muitos clientes trabalham com investidores e precisam compartilhar informações da plataforma, mas os painéis criados para tomar decisões de negócios diárias podem não ser o que um investidor está procurando. Abaixo, descreve algumas práticas recomendadas para criar um painel abrangente, mas simples, ideal para compartilhar com investidores ativos e potenciais.

Veja o que é necessário para criar relatórios para seu painel de investidores:

## Relatórios escalares

* **[!UICONTROL All-time revenue]**
* **[!UICONTROL Distinct buyers]**
* **[!UICONTROL All-time number of orders]**
* **[!UICONTROL AOV]**
* **[!UICONTROL Items sold]**

## Relatórios Visuais

* **[!UICONTROL Revenue by quarter]**
   * Métrica - Receita
* **[!UICONTROL Revenue from 1st time orders vs repeat orders]**
   * Métrica - Receita de pedido pela primeira vez
   * Filtro - O número de ordem do usuário é igual a 1
   * Métrica 2 – repita solicitar receita
      * Filtrar-o número de solicitar do usuário é maior que 1
   * Desmarcar a caixa para vários eixos Y
   * Alterar para um gráfico de colunas empilhadas
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
   * Métrica-receita do produto
      * Ocultar o gráfico
      * Agrupar por nome de produto. Selecione todos os produtos.
      * Definir o intervalo de tempo como All-Time
      * Definir o intervalo de tempo como Nenhum
      * Em &quot;Mostrar superior/inferior&quot;, mostrar apenas os 10 principais classificados por Lucro do produto
* **[!UICONTROL Cumulative distinct buyers by quarter]**
   * Métrica - Compradores distintos
      * Perspectiva - Cumulativa
* **[!UICONTROL Site visits - New vs. repeat by month]**
* Sessões

Com uma [!DNL Google Analytics] integração, você pode incluir relatórios em:

* Visitas ao site
* Taxa de conversão

Com os serviços ](https://business.adobe.com/products/magento/magento-commerce.html) de enriquecimento de dados do [ comércio, você pode incluir relatórios em:

* Clientes únicos por estado/região, idade e sexo.

## Outras dicas

* Use um método claro e conciso [convenção de nomenclatura](../best-practices/naming-elements.md)
* Compartilhar o painel com usuários investidores
* Ou envie-o via **[!UICONTROL Automated email summary]**(../data-user/export-data/email-summaries.md)
* Crie apenas um painel. Isso facilita a manutenção do conteúdo e você sabe exatamente o que seus investidores estão vendo.

Organize seus relatórios com bastante cuidado e preste atenção nos detalhes. Após a conclusão, a painel é semelhante à seguinte:

![](../../mbi/assets/investor-dboard-example.png)
