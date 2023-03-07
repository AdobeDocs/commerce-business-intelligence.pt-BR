---
title: Usando o Report Builder SQL
description: Saiba mais sobre os detalhes do uso do Report Builder SQL.
exl-id: 3a485b00-c59d-4bc5-b78b-57e9e92dd9d6
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '1461'
ht-degree: 0%

---

# Usar `SQL Report Builder`

>[!NOTE]
>
>Exige [Permissões de administrador](../../administrator/user-management/user-management.md) para criar e editar gráficos SQL. `Standard` os usuários podem reorganizar esses gráficos em painéis e `Read-only` os usuários do têm a mesma experiência que têm com os gráficos tradicionais. Além disso, `Read-only` Os usuários do não têm acesso ao texto do query.

Consulte a [vídeo de treinamento](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html?lang=en) para saber mais.

`SQL`, ou Linguagem de consulta estruturada, é uma linguagem de programação usada para se comunicar com bancos de dados. Entrada [!DNL MBI], o SQL é usado para consultar ou recuperar dados da Data Warehouse. Analise os relatórios em seu painel: nos bastidores, cada um é alimentado por um query SQL.

Você pode usar o [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) para consultar diretamente a Data Warehouse, exibir os resultados e transformá-los em um gráfico. Você pode começar a criar um relatório com o `SQL Report Builder` navegando até **[!UICONTROL Report Builder** > **SQL Report Builder]**.

Consulte a [vídeo de treinamento](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html?lang=en) para saber mais.

A variável `SQL Report Builder` O permite consultar diretamente a Data Warehouse, visualizar os resultados e transformá-los rapidamente em um gráfico. A melhor parte sobre o uso do SQL para criar relatórios é que você não precisa aguardar os ciclos de atualização para iterar nas colunas criadas. Se os resultados não parecerem corretos, você poderá editar e executar novamente a query rapidamente até que tudo corresponda às suas expectativas.

Este artigo o orienta a usar o `SQL Report Builder`. Depois de conhecer sua alternativa, confira o tutorial SQL para visualizações ou tente otimizar algumas das consultas escritas.

Abrangido neste artigo:

1. [Gravação de uma consulta](#writing)

1. [Execução da consulta e exibição dos resultados](#runquery)

1. [Criação de uma visualização](#createviz)

1. [Salvamento do relatório](#save)

## Integrações de Report Builder SQL

No estado atual do mundo, [[!DNL Google Analytics]](../importing-data/integrations/google-analytics.md) é a única integração indisponível para uso com o [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md). Essa funcionalidade está em desenvolvimento.

Para começar a criar um relatório SQL, clique em **[!UICONTROL Report Builder]** ou **[!UICONTROL Add Report]** na parte superior de qualquer painel. No `Report Picker` clique em **[!UICONTROL SQL Report Builder]** para abrir o editor SQL.

## Introdução

Para editar um relatório, clique no botão de engrenagem (![](../../assets/gear-icon.png)) no canto superior direito de um gráfico baseado em SQL e clique em **[!UICONTROL Edit]**.

## Gravação de uma consulta {#writing}

>[!NOTE]
>
>`SQL Report Builder` as consultas diferenciam maiúsculas de minúsculas. Verifique se está usando as letras maiúsculas e minúsculas corretas ao escrever consultas ou você pode acabar com resultados inesperados ou erros.

Na sequência da [diretrizes para otimização de consulta](../../best-practices/optimizing-your-sql-queries.md), escreva uma consulta no editor SQL.

>[!IMPORTANT]
>
>**Métricas em relatórios SQL** - Ao inserir uma métrica em um relatório SQL, a variável `current definition` da métrica é usada.

Se a métrica for atualizada no futuro, o relatório SQL *não* refletir as alterações. Você deve editar o relatório manualmente para que as alterações entrem em vigor.

Usando os botões na parte superior da barra lateral, é possível alternar entre listas de tabelas e métricas disponíveis para uso no `SQL Report Builder`. Se você não vir o que está procurando na lista, tente pesquisá-lo usando a barra de pesquisa na parte superior da barra lateral.

Você também pode usar a barra lateral no editor SQL para inserir métricas, tabelas e colunas diretamente em suas consultas, passando o mouse sobre elas e clicando em **[!UICONTROL Insert]**:

![Inserir uma tabela no editor SQL.](../../assets/SQL_RB_Insert_Table.png)

>[!NOTE]
>
>Qualquer [função SELECT](https://www.postgresql.org/docs/9.5/sql-select.html#SQL-SELECT-LIST), ou qualquer função que não altere dados, que seja suportada pelo PostgreSQL, é suportada no Report Builder SQL. Isso inclui, mas não está limitado a, MÉDIA, CONTAGEM, CONTAGEM DISTINTA, MÍN/MAX e SOMA.

Além disso, qualquer tipo JOIN é suportado, mas o Adobe recomenda usar somente JOIN INTERNO, pois é o mais barato dos tipos JOIN.

## Execução da consulta e exibição dos resultados {#runquery}

Quando terminar de escrever a consulta, clique em **[!UICONTROL Run Query]**. Os resultados são exibidos em uma tabela abaixo do editor SQL:

![Execução da consulta e exibição dos resultados.](../../assets/SQL_Run_Query.gif)

Se algo parecer incorreto nos resultados, você poderá editar a consulta e executá-la novamente até que esteja satisfeito.

Às vezes, você pode ver [mensagens abaixo do editor com EXPLICAR](../../best-practices/optimizing-your-sql-queries.md). Se você vir um desses, significa que o query não foi executado e precisa de um pouco de ajuste.

Após concluir a edição do query, você pode criar uma visualização ou salvar o trabalho em um painel.

## Criação de uma visualização {#createviz}

Para criar uma visualização com seus resultados de query, clique no link **[!UICONTROL Chart]** na guia `Results` painel. Nesta guia, você seleciona:

* A variável `Series`ou a coluna que deseja medir, como **Itens vendidos**.
* A variável `Category`ou a coluna que deseja usar para segmentar seus dados, como **fonte de aquisição**.
* A variável `Labels`ou valores do eixo X.

Veja abaixo como é o processo de visualização:

![](../../assets/SQL_RB_viz_overview.gif)

Para obter uma apresentação detalhada sobre como criar uma visualização, consulte [Tutorial de criação de visualizações de consultas SQL](../../tutorials/create-visuals-from-sql.md){: target=&quot;_blank&quot;}.

## Salvamento do relatório {#save}

Antes de salvar seu trabalho, você deve dar um nome ao relatório. Lembre-se de seguir o [diretrizes de práticas recomendadas para nomeação](../../best-practices/naming-elements.md){: target=&quot;_blank&quot;} e escolha algo que transmita claramente o que é o relatório!

Clique em **[!UICONTROL Save]** no canto superior direito do editor SQL e selecione o relatório `Type` (`Chart` ou `Table`). Para finalizar, selecione o painel no qual salvar o relatório e clique em **[!UICONTROL Save to Dashboard]**.

![](../../assets/SQL_Save_Report.gif)

### Analisar seus dados

#### `SQL Report Builder`

[`The SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) O oferece o poder de consultar diretamente a Data Warehouse, visualizar os resultados e transformá-los rapidamente em um relatório. Usar SQL também permite [para usar funções SQL que não estão disponíveis](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html) no `Visual` ou `Cohort` Report Builder, proporcionando maior controle sobre seus dados.

As colunas calculadas criadas usando SQL não dependem dos ciclos de atualização, o que significa que você pode iterar nelas da maneira que desejar e ver os resultados imediatamente.

>[!NOTE]
>
>Isso se aplica somente à estrutura da coluna, não à atualização dos dados. Os dados atualizados ainda dependem dos ciclos de atualização concluídos com êxito.

| **Isso é perfeito para...** | **Isso não é tão bom para...** |
|---|---|
| Analistas intermediários/avançados | Iniciantes - você precisa conhecer SQL. |
| A experiência em SQL | Análises simples - escrever uma consulta pode ser mais trabalhoso do que simplesmente usar o Report Builder visual. |
| Criação de colunas calculadas de uso único | Compartilhamento com outras pessoas - considere seu público-alvo: elas entendem SQL? Caso contrário, eles podem se confundir com a forma como o relatório é construído. |
| Dados com `one-to-many` relacionamentos |  |
| Teste de uma nova coluna ou análise |  |

#### Resultados do Editor de Banco de Dados vs SQL

Na maioria das vezes, as diferenças nos resultados podem ser atribuídas aos ciclos de atualização. Se [!DNL MBI] estiver replicando dados do banco de dados para a Data Warehouse, você poderá ver resultados diferentes mesmo ao usar a mesma consulta.

Problemas de conexão também podem resultar em discrepâncias. Navegue até a `Connections` clicando em **[!DNL Manage Data** > **Connections]**) para conferir - há um erro para a integração de banco de dados em questão? Em caso afirmativo, talvez seja necessário [autenticar novamente a integração](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en) para que tudo funcione novamente.

Se todas as suas integrações forem conectadas com êxito e você não estiver no meio de um ciclo de atualização, talvez haja algo errado.

#### A exclusão de um relatório SQL também exclui as colunas subjacentes da minha Data Warehouse?

Não, você não perde nenhuma coluna da Data Warehouse, independentemente de como as criou.

Colunas criadas usando o `Data Warehouse Manager` não serão afetadas se você excluir um relatório ou query que as utiliza.

Colunas criadas usando o `SQL Report Builder` não são salvas na Data Warehouse.


#### `Report Builder` versus `SQL Report Builder`

A variável `SQL Report Builder` O oferece mais flexibilidade ao criar e estruturar seus gráficos - você pode, por exemplo, selecionar quais valores devem ser mostrados na `X` e `Y` eixos. Para obter mais informações sobre como criar gráficos na `SQL Report Builder`, confira o [Criar visualizações de consultas SQL](../../tutorials/create-visuals-from-sql.md) tutorial.

#### `Cohort Report Builder` {#cohortrb}

Ao contrário do `Visual Report Builder`, o [`Cohort Report Builder`](../dev-reports/cohort-rpt-bldr.md) O é destinado a um único propósito - analisar e identificar tendências comportamentais de grupos de usuários semelhantes ao longo do tempo. O uso do Report Builder de coorte não requer nenhum conhecimento em SQL, portanto, você pode mergulhar sem hesitar se estiver apenas começando.

| **Isso é perfeito para...** | **Isso não é tão bom para...** |
|---|---|
| Analistas intermediários/avançados | Iniciantes - você precisa de coortes que definam práticas. |
| Identificação de tendências comportamentais ao longo do tempo | Análise qualitativa - pode ser [concluído](../dev-reports/create-qual-cohort-analysis.md), mas requer assistência do Adobe. |

## Reconstrução de Consultas após o Ciclo de Atualização

Não é necessário recriar as consultas. Relatórios criados usando o [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) são salvas como as criadas no `Report Builder`. O processo de atualização dos gráficos SQL é o mesmo: depois que os dados forem atualizados, os valores nos gráficos serão recalculados e exibidos novamente.

>[!NOTE]
>
>Ao excluir um relatório/consulta SQL, as colunas subjacentes não são excluídas da Data Warehouse. Você não perde nenhuma coluna, independentemente de como as criou.

* As colunas criadas usando o Gerenciador de Datas Warehouse não serão afetadas se você excluir um relatório ou consulta que as utiliza.

* As colunas criadas usando o Report Builder SQL não são salvas na Data Warehouse.

## Encapsulamento {#wrapup}

Se você deseja tentar algo um pouco mais desafiador, por que não tentar escrever uma consulta otimizada para visualização? Confira o [Tutorial de criação de visualizações de consultas SQL](../../tutorials/create-visuals-from-sql.md){: target=&quot;_blank&quot;} para começar.
