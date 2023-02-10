---
title: Trabalhar com o SQL Report Builder
description: Saiba como auditar dados e métricas usando o Report Builder SQL para que você possa comparar os resultados com os dados do banco de dados local.
exl-id: d1d9e099-4138-43e6-aaec-6f15ebc5c4d4
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---

# `SQL Report Builder`

O `SQL Report Builder` O é usado principalmente para criar novos relatórios e iterar em análises, mas também pode ser usado para auditar dados e métricas de maneira eficaz. As informações a seguir explicam como auditar dados e métricas usando o `SQL Report Builder` para que você possa comparar os resultados com os dados do banco de dados local.

## Consulta de uma métrica

Para começar, abra o `SQL Report Builder` navegando até **[!UICONTROL Report Builder > SQL Report Builder > Create Report]**. Você pode usar a barra lateral no editor SQL para inserir uma métrica diretamente no query, passando o mouse sobre a métrica e clicando em **[!UICONTROL Insert]**. Isso adicionará a definição de consulta dessa métrica ao editor. A definição incluirá os seguintes componentes:

- O **operação de métrica** sendo executado, indicado por SUM() no exemplo abaixo.
- O **tabela em** que a métrica é criada, indicado pela cláusula FROM.
- Qualquer **filtros (e conjuntos de filtros)** que foram adicionados à métrica, indicado pela cláusula WHERE no exemplo abaixo.
- O componente do **timestamp** (ano, mês) em que os dados devem ser encomendados, indicado pela cláusula ORDER BY no exemplo abaixo.

Se quiser ter uma exibição mais clara do query, poderá reformatar como ele é exibido no campo de query. Quando estiver pronto, selecione `Run Query`. Os resultados serão preenchidos como uma tabela no painel de relatório abaixo da consulta.

![](../../assets/run-query-results.gif)

## Restrição da consulta

Se você estiver tentando identificar uma discrepância específica ou um conjunto de dados, deverá restringir a consulta a uma amostra específica para verificar o banco de dados local. Você pode fazer isso editando a query para corresponder às restrições desejadas. No exemplo a seguir, estamos restringindo o query para incluir somente a receita de 1º de janeiro de 2013 ou posterior. Após atualizar a consulta, selecione **[!UICONTROL Run Query]** novamente para atualizar os resultados.

![](../../assets/restricting-query.gif)

## Salvar e exportar

Quando o relatório atender às suas necessidades, salve-o em um painel, dando um nome distinto ao relatório, clicando em **[!UICONTROL Save]** e selecionar o tipo de relatório que deseja salvar e o painel. Ao auditar métricas, recomendamos salvar o relatório como um `Table` e salvá-lo em um painel de teste.

Depois que o relatório for salvo, navegue até esse painel selecionando `Go to Dashboard`. A partir daí, é possível exportar os dados localizando o relatório e selecionando **[!UICONTROL Options gear > Full `.csv`Exportar]** ou **[!UICONTROL Full Excel Export]**.

![](../../assets/export-dboard-data.gif)

## Consultas personalizadas

Você também pode gravar queries personalizados e exportar os resultados para comparar com o banco de dados local. Seguindo [diretrizes para otimização de consulta](../../best-practices/optimizing-your-sql-queries.md), escreva uma consulta no editor SQL. Você pode usar os botões na parte superior da barra lateral para alternar entre as listas de tabelas e métricas disponíveis para uso no `SQL Report Builder` e adicioná-las ao seu query. Quando o query personalizada se encaixa nas suas necessidades, você pode salvar o relatório e exportar esses dados do painel.

### Ainda tropeçadas?

Se encontrar uma discrepância após a auditoria de seus dados, consulte o [Entrando em contato com o suporte: Discrepâncias de dados](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-data-discrepancies.html?lang=en) artigo de suporte para obter mais informações sobre o que fazer em seguida.
