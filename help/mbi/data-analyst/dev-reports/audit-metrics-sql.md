---
title: Trabalhar com Report Builder SQL
description: Saiba como auditar dados e métricas usando o Report Builder SQL para poder comparar os resultados com os dados do banco de dados local.
exl-id: d1d9e099-4138-43e6-aaec-6f15ebc5c4d4
role: Admin, Data Architect, Data Engineer, User
feature: Reports, Data Warehouse Manager, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# [!DNL SQL Report Builder]

A variável [!DNL SQL Report Builder] O é usado principalmente para criar novos relatórios e iterar em análises, mas também pode ser usado para auditar dados e métricas com eficiência. As informações a seguir explicam como auditar dados e métricas usando o [!DNL SQL Report Builder] para que você possa comparar os resultados com os dados do banco de dados local.

## Consulta de uma métrica

Para começar, abra o [!DNL SQL Report Builder] navegando até **[!UICONTROL Report Builder > SQL Report Builder > Create Report]**. Você pode usar a barra lateral no [!DNL SQL] editor para inserir uma métrica diretamente na sua consulta, passando o mouse sobre a métrica e clicando em **[!UICONTROL Insert]**. Isso adiciona a definição de consulta dessa métrica ao editor. A definição inclui os seguintes componentes:

- A variável **operação de métrica** sendo executado, indicado por `SUM()` no exemplo abaixo.
- A variável **tabela em** em que a métrica é criada, indicado pela variável `FROM` Cláusula.
- Qualquer **filtros (e conjuntos de filtros)** que foram adicionadas à métrica, indicadas pela variável `WHERE` no exemplo abaixo.
- O componente do **carimbo de data e hora** (ano, mês) em que os dados devem ser solicitados, indicado pela `ORDER BY` no exemplo abaixo.

Para ter uma exibição mais clara da consulta, você pode reformatar como ela é exibida no campo de consulta. Quando estiver pronto, selecione `Run Query`. Os resultados são preenchidos como uma tabela no painel de relatório abaixo do query.

![](../../assets/run-query-results.gif)

## Restrição da consulta

Se você estiver tentando identificar uma discrepância específica ou um conjunto de dados, deverá restringir a consulta a uma amostra específica para verificar o banco de dados local. Você pode fazer isso editando a query para corresponder às restrições desejadas. No exemplo a seguir, você está restringindo o query para incluir somente a receita de 1º de janeiro de 2013 ou posterior. Após atualizar a consulta, selecione **[!UICONTROL Run Query]** novamente para atualizar os resultados.

![](../../assets/restricting-query.gif)

## Salvar e exportar

Quando o relatório atender às suas necessidades, dê um nome distinto ao relatório, clique em **[!UICONTROL Save]** e selecione o tipo de relatório que deseja salvar e o painel. Ao auditar as métricas, o Adobe recomenda salvar o relatório como um `Table` e salvá-lo em um painel de teste.

Depois que o relatório for salvo, navegue até o painel selecionando `Go to Dashboard`. A partir daí, você pode exportar os dados localizando o relatório e selecionando **[!UICONTROL Options gear > Full `.csv`Exportar]** ou **[!UICONTROL Full Excel Export]**.

![](../../assets/export-dboard-data.gif)

## Consultas personalizadas

Você também pode gravar consultas personalizadas e exportar os resultados para comparação com o banco de dados local. Na sequência da [diretrizes para otimização de consulta](../../best-practices/optimizing-your-sql-queries.md), escreva uma consulta no editor SQL. Você pode usar os botões na parte superior da barra lateral para alternar entre listas de tabelas e métricas disponíveis para uso no [!DNL SQL Report Builder] e adicione-os à sua query. Quando a consulta personalizada atender às suas necessidades, você poderá salvar o relatório e exportar esses dados do painel.

>[!NOTE]
>
>Se você encontrar uma discrepância após auditar seus dados, verifique a [Contato com o suporte: discrepâncias de dados](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-data-discrepancies.html) tópico de suporte para obter mais informações sobre o que fazer em seguida.
