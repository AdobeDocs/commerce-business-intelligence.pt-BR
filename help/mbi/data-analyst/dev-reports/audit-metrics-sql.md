---
title: Trabalhar com Report Builder SQL
description: Saiba como auditar dados e métricas usando o Report Builder SQL para poder comparar os resultados com os dados do banco de dados local.
exl-id: d1d9e099-4138-43e6-aaec-6f15ebc5c4d4
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---

# `SQL Report Builder`

A variável `SQL Report Builder` O é usado principalmente para criar novos relatórios e iterar em análises, mas também pode ser usado para auditar dados e métricas com eficiência. As informações a seguir explicam como auditar dados e métricas usando o `SQL Report Builder` para que você possa comparar os resultados com os dados do banco de dados local.

## Consulta de uma métrica

Para começar, abra o `SQL Report Builder` navegando até **[!UICONTROL Report Builder > SQL Report Builder > Create Report]**. Você pode usar a barra lateral no editor SQL para inserir uma métrica diretamente em sua consulta, passando o mouse sobre a métrica e clicando em **[!UICONTROL Insert]**. Isso adiciona a definição de consulta dessa métrica ao editor. A definição inclui os seguintes componentes:

- A variável **operação de métrica** sendo executado, indicado por SUM() no exemplo abaixo.
- A variável **tabela em** a métrica é criada, indicado pela cláusula FROM.
- Qualquer **filtros (e conjuntos de filtros)** que foram adicionados à métrica, indicada pela cláusula WHERE no exemplo abaixo.
- O componente do **carimbo de data e hora** (ano, mês) em que os dados devem ser solicitados, indicado pela cláusula ORDER BY no exemplo abaixo.

Se quiser ter uma visualização mais clara da consulta, você poderá reformatar como ela é exibida no campo de consulta. Quando estiver pronto, selecione `Run Query`. Os resultados são preenchidos como uma tabela no painel de relatório abaixo do query.

![](../../assets/run-query-results.gif)

## Restrição da consulta

Se você estiver tentando identificar uma discrepância específica ou um conjunto de dados, deverá restringir a consulta a uma amostra específica para verificar o banco de dados local. Você pode fazer isso editando a query para corresponder às restrições desejadas. No exemplo a seguir, você está restringindo o query para incluir somente a receita de 1º de janeiro de 2013 ou posterior. Após atualizar a consulta, selecione **[!UICONTROL Run Query]** novamente para atualizar os resultados.

![](../../assets/restricting-query.gif)

## Salvar e exportar

Quando o relatório atender às suas necessidades, salve-o em um painel dando ao relatório um nome distinto, clicando em **[!UICONTROL Save]** e selecionando o tipo de relatório que deseja salvar e o painel. Ao auditar as métricas, o Adobe recomenda salvar o relatório como um `Table` e salvá-lo em um painel de teste.

Depois que o relatório for salvo, navegue até o painel selecionando `Go to Dashboard`. A partir daí, você pode exportar os dados localizando o relatório e selecionando **[!UICONTROL Options gear > Full `.csv`Exportar]** ou **[!UICONTROL Full Excel Export]**.

![](../../assets/export-dboard-data.gif)

## Consultas personalizadas

Você também pode gravar consultas personalizadas e exportar os resultados para comparação com o banco de dados local. Na sequência da [diretrizes para otimização de consulta](../../best-practices/optimizing-your-sql-queries.md), escreva uma consulta no editor SQL. Você pode usar os botões na parte superior da barra lateral para alternar entre listas de tabelas e métricas disponíveis para uso no `SQL Report Builder` e adicione-os à sua query. Quando a consulta personalizada atender às suas necessidades, você poderá salvar o relatório e exportar esses dados do painel.

### Ainda tropeçou?

Se você encontrar uma discrepância após auditar seus dados, verifique a [Contato com o suporte: discrepâncias de dados](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-data-discrepancies.html?lang=en) artigo de suporte para obter mais informações sobre o que fazer em seguida.
