---
title: Usando o Report Builder SQL
description: Saiba mais sobre como usar o SQL Report Builder.
exl-id: 3a485b00-c59d-4bc5-b78b-57e9e92dd9d6
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '1501'
ht-degree: 0%

---

# Usando `SQL Report Builder`

>[!NOTE]
>
>Exige [Permissões de administrador](../../administrator/user-management/user-management.md) para criar e editar gráficos SQL. `Standard` os usuários podem reorganizar esses gráficos em painéis, e `Read-only` os usuários terão a mesma experiência que os gráficos tradicionais. Além disso, `Read-only` Os usuários do não têm acesso ao texto da query.

Veja nossa [vídeo de treinamento](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html?lang=en) para saber mais.

`SQL`ou Linguagem de consulta estruturada é uma linguagem de programação usada para comunicação com bancos de dados. Em [!DNL MBI], o SQL é usado para consultar ou recuperar dados do data warehouse. Dê uma olhada nos relatórios em seu painel - em segundo plano, cada um é alimentado por uma consulta SQL.

Você pode usar o [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) para consultar diretamente o data warehouse, exibir os resultados e transformá-los em um gráfico. Você pode começar a criar um relatório com a variável `SQL Report Builder` navegando até **[!UICONTROL Report Builder** > **SQL Report Builder]**.

Veja nossa [vídeo de treinamento](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html?lang=en) para saber mais.

O `SQL Report Builder` O permite consultar diretamente o data warehouse, exibir os resultados e transformá-los rapidamente em um gráfico. A melhor parte sobre o uso do SQL para criar relatórios é que você não precisa aguardar os ciclos de atualização para iterar nas colunas criadas. Se os resultados não parecerem corretos, você poderá editar e executar novamente o query rapidamente até que as coisas correspondam às suas expectativas.

Neste artigo, o orientamos usando o `SQL Report Builder`. Depois de saber o caminho, confira o tutorial SQL for visualizations ou tente otimizar algumas das consultas que você gravou.

Esta é uma visão geral do que cobrimos neste artigo:

1. [Gravação de um query](#writing)

1. [Execução da consulta e visualização dos resultados](#runquery)

1. [Criação de uma visualização](#createviz)

1. [Salvamento do relatório](#save)

## Integrações do SQL Report Builder

No estado atual do mundo, [[!DNL Google Analytics]](../importing-data/integrations/google-analytics.md) é a única integração indisponível para uso com o [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md). Estamos trabalhando para incluir essa funcionalidade em uma versão posterior.

Para começar a criar um novo relatório SQL, clique em **[!UICONTROL Report Builder]** ou **[!UICONTROL Add Report]** na parte superior de qualquer painel. No `Report Picker` , clique em **[!UICONTROL SQL Report Builder]** para abrir o editor SQL.

## Introdução

Para editar um relatório, clique na engrenagem (![](../../assets/gear-icon.png)) ícone no canto superior direito de um gráfico baseado em SQL e clique em **[!UICONTROL Edit]**.

## Gravação de um query {#writing}

>[!NOTE]
>
>`SQL Report Builder` as consultas fazem distinção entre maiúsculas e minúsculas. Verifique se você está usando o caso correto ao gravar consultas ou se pode acabar com resultados ou erros inesperados.

Seguindo [diretrizes para otimização de consulta](../../best-practices/optimizing-your-sql-queries.md), escreva uma consulta no editor SQL.

>[!IMPORTANT]
>
>**Métricas em relatórios SQL** - Ao inserir uma métrica em um relatório SQL, a variável `current definition` da métrica será usada.

Se a métrica for atualizada no futuro, o relatório SQL *não* reflita as alterações. Será necessário editar manualmente o relatório para que as alterações tenham efeito.

Ao usar os botões na parte superior da barra lateral, é possível alternar entre listas de tabelas e métricas disponíveis para uso no `SQL Report Builder`. Se você não vir o que está procurando na lista, tente pesquisá-la usando a barra de pesquisa na parte superior da barra lateral.

Você também pode usar a barra lateral no editor SQL para inserir métricas, tabelas e colunas diretamente em suas consultas, passando o mouse sobre elas e clicando em **[!UICONTROL Insert]**:

![Inserção de uma tabela no editor SQL.](../../assets/SQL_RB_Insert_Table.png)

>[!NOTE]
>
>Qualquer [Função SELECT](https://www.postgresql.org/docs/9.5/sql-select.html#SQL-SELECT-LIST)ou qualquer função que não altere dados, compatível com PostgreSQL, é compatível com o SQL Report Builder. Isso inclui, mas não está limitado a, AVG, COUNT, COUNT DISTINCT, MIN/MAX e SUM.

Além disso, qualquer tipo JOIN é compatível, mas recomendamos usar somente INNER JOIN, pois é o menos caro dos tipos JOIN.

## Execução da consulta e visualização dos resultados {#runquery}

Quando terminar de escrever seu query, clique em **[!UICONTROL Run Query]**. Os resultados serão exibidos em uma tabela abaixo do editor SQL:

![Execução da consulta e visualização dos resultados.](../../assets/SQL_Run_Query.gif)

Se algo parecer errado nos resultados, você poderá editar o query e executá-lo novamente até que esteja satisfeito.

Às vezes, você pode ver [mensagens abaixo do editor com EXPLAIN](../../best-practices/optimizing-your-sql-queries.md). Se você vir um desses, significa que seu query não foi executado e precisa de um pouco de ajuste.

Após concluir a edição de sua query, você pode migrar para a criação de uma visualização ou salvar seu trabalho em um painel.

## Criação de uma visualização {#createviz}

Para criar uma visualização com os resultados da consulta, clique no botão **[!UICONTROL Chart]** na guia no `Results` painel. Nesta guia, você selecionará:

* O `Series`ou a coluna que deseja medir, como **Itens vendidos**.
* O `Category`ou a coluna que deseja usar para segmentar seus dados, como **fonte de aquisição**.
* O `Labels`ou valores do eixo X.

Veja a seguir uma rápida aparência do processo de visualização:

![](../../assets/SQL_RB_viz_overview.gif)

Para obter uma apresentação detalhada de como criar uma visualização, consulte nossa [Tutorial Criação de visualizações do SQL queries](../../tutorials/create-visuals-from-sql.md){: target=&quot;_blank&quot;}.

## Salvamento do relatório {#save}

Antes de salvar seu trabalho, você deve dar um nome ao relatório. Lembre-se de seguir o [diretrizes de práticas recomendadas para nomeação](../../best-practices/naming-elements.md){: target=&quot;_blank&quot;} e escolha algo que transmita claramente o que é o relatório!

Clique em **[!UICONTROL Save]** no canto superior direito do editor SQL e selecione o relatório `Type` (`Chart` ou `Table`). Para vincular os itens, selecione o painel para salvar o relatório e clique em **[!UICONTROL Save to Dashboard]**.

![](../../assets/SQL_Save_Report.gif)

### Analisar seus dados

#### `SQL Report Builder`

[`The SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) O oferece o poder de consultar diretamente seu data warehouse, visualizar os resultados e transformá-los rapidamente em um relatório. O uso do SQL também permite [para utilizar funções SQL que não estejam disponíveis](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html) no `Visual` ou `Cohort` Report Builder, fornecendo maior controle sobre os dados.

Gostaríamos de mencionar que as colunas calculadas criadas usando o SQL não dependem dos ciclos de atualização, o que significa que você pode iterá-las como desejar e ver imediatamente os resultados.

>[!NOTE]
>
>Isso se aplica somente à estrutura da coluna, não à atualização dos dados. Os dados novos ainda dependem dos ciclos de atualização concluídos com êxito.

| **Isso é perfeito para...** | **Isso não é tão bom para...** |
|---|---|
| Analistas intermediários/avançados | Iniciantes - você precisa saber SQL. |
| O salvamento do SQL | Análises simples - escrever um query pode ser mais trabalhoso do que simplesmente usar o Visual Report Builder. |
| Criação de colunas calculadas de uso único | Compartilhamento com outras pessoas - considere seu público: eles entendem SQL? Caso contrário, podem ser confundidas com a forma como o relatório é criado. |
| Dados com `one-to-many` relações |  |
| Teste de uma nova coluna ou análise |  |

#### Resultados do Editor de Banco de Dados vs SQL

Na maioria das vezes, as diferenças nos resultados podem ser atribuídas aos ciclos de atualização. If [!DNL MBI] estiver no processo de replicação de dados do banco de dados para a Data Warehouse, você poderá ver resultados diferentes mesmo ao usar a mesma query.

Problemas de conexão também podem resultar em discrepâncias. Navegue até o `Connections` clicando em **[!DNL Manage Data** > **Connections]**) para fazer check-out - há um erro para a integração do banco de dados em questão? Em caso afirmativo, talvez seja necessário [reautenticar a integração](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en) para que as coisas voltem a correr.

Se todas as suas integrações forem conectadas com êxito e você não estiver no meio de um ciclo de atualização, algo diferente poderá estar errado.

#### A exclusão de um relatório SQL também exclui as colunas subjacentes da minha Data Warehouse?

Não, você não perderá colunas de sua Data Warehouse, independentemente de como você as criou.

Colunas criadas usando o `Data Warehouse Manager` não será afetado se você excluir um relatório ou consulta que os use.

Colunas criadas usando o `SQL Report Builder` não são salvas em sua Data Warehouse.


#### `Report Builder` versus `SQL Report Builder`

O `SQL Report Builder` oferece mais flexibilidade ao criar e estruturar seus gráficos - você pode, por exemplo, selecionar quais valores devem mostrar na variável `X` e `Y` eixos. Para obter mais informações sobre a criação de gráficos no `SQL Report Builder`, confira nossa [Criação de visualizações de queries SQL](../../tutorials/create-visuals-from-sql.md) tutorial.

#### `Cohort Report Builder` {#cohortrb}

Ao contrário do `Visual Report Builder`, o [`Cohort Report Builder`](../dev-reports/cohort-rpt-bldr.md) destina-se a um único propósito - análise e identificação de tendências comportamentais de grupos de usuários semelhantes ao longo do tempo. O uso do Report Builder de coorte não requer nenhum SQL salvo, portanto, você pode mergulhar sem hesitar se estiver apenas começando.

| **Isso é perfeito para...** | **Isso não é tão bom para...** |
|---|---|
| Analistas intermediários/avançados | Iniciantes - é necessário praticar a definição de coortes. |
| Identificação de tendências comportamentais ao longo do tempo | Análise qualitativa - pode ser [done](../dev-reports/create-qual-cohort-analysis.md), mas requer a nossa assistência. |

## Reconstruindo Consultas após o Ciclo de Atualização

Não é necessário recriar as consultas. Relatórios criados com o [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) são salvas como as criadas no `Report Builder`. O processo de atualização dos gráficos SQL é exatamente o mesmo - depois que seus dados são atualizados, os valores nos gráficos serão recalculados e exibidos novamente.

>[!NOTE]
>
>Ao excluir um relatório/consulta SQL, ele não exclui as colunas subjacentes da Data Warehouse. Você não perderá colunas, independentemente de como as construiu.

* As colunas criadas usando o Gerenciador de Datas Warehouse não serão afetadas se você excluir um relatório ou uma consulta que as usa.

* As colunas criadas usando o Report Builder SQL não são salvas em sua Data Warehouse.

## Quebra de linha {#wrapup}

Se você quiser tentar algo um pouco mais desafiador, por que não tentar escrever uma consulta que seja otimizada para visualização? Veja nossa [Tutorial Criação de visualizações do SQL queries](../../tutorials/create-visuals-from-sql.md){: target=&quot;_blank&quot;} para começar.
