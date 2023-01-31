---
title: Report Builder de coorte
description: Saiba mais sobre a análise de grupos de usuários que compartilham características semelhantes ao longo de seus ciclos de vida.
exl-id: d80c5389-7256-40e0-86e0-49903113f93d
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 0%

---

# Report Builder de coorte

Você já quis estudar como os diferentes subconjuntos de seus usuários se comportam ao longo do tempo? Por exemplo, algum dia se perguntou se os usuários que se registram durante um período promocional têm uma receita vitalícia média mais alta do que aqueles que não possuem? Se a resposta for `Yes`, em seguida, o `Cohort Report Builder` é a ferramenta perfeita para você. [!DNL MBI] O é especificamente otimizado para executar essa análise e torná-la relevante para sua empresa.

## O que é a análise de coorte? {#what}

`Cohort` A análise pode ser amplamente definida como a análise de grupos de utilizadores que partilham características semelhantes ao longo dos seus ciclos de vida. Ela permite identificar tendências comportamentais em diferentes grupos de usuários.

Para obter um guia mais detalhado sobre `cohort` análise, [dê uma olhada aqui](https://www.cohortanalysis.com/) - escrevemos o site nele!

Em seu [!DNL MBI] no painel, é fácil criar o usuário `cohorts` com base em um `cohort` e uma métrica na sua conta.

## Por que a análise de coorte é importante? {#important}

Tal como acima mencionado, `cohort` A análise permite identificar tendências comportamentais entre diferentes grupos de usuários. Com uma sólida compreensão de como certos grupos se comportam, você pode adaptar suas decisões e gastar para maximizar suas vendas. Por exemplo, uma receita vitalícia `cohort` análise - embora esse tipo de análise seja benéfica por várias razões, a imediata é a melhor decisão de aquisição de clientes.

## Como criar meu próprio `cohort` análise?

### Nova arquitetura

Estas são as instruções para usar a variável `Cohort Report Builder` no [Nova arquitetura](../../administrator/account-management/new-architecture.md).

1. Clique em **[!UICONTROL Report Builder]** na guia esquerda ou **[!UICONTROL Add Report** > **Create Report]** em qualquer painel.

1. No `Report Builder` tela de seleção, clique em **[!UICONTROL Create Report]** ao lado do `Visual Report Builder` opção.

**Adicionar uma métrica**

Agora que estamos no `Report Builder`, adicionamos a métrica na qual queremos executar a análise (por exemplo: `Revenue` ou `Orders`).

>[!NOTE]
>
>Nativo [!DNL Google Analytics] não são compatíveis com a `Cohort Report Builder`.

**Alternar a exibição de métrica para`Cohort`**

![](../../assets/visual-report-builder-cohort-toggle.png)

Isso abre uma nova janela onde podemos configurar os detalhes da variável `Cohort` Relatório.

### Cinco especificações são necessárias para criar uma `Cohort` relatório:

1. Como agrupar os `cohorts`
1. O `cohort` período
1. O número de `cohorts` para visualizar
1. A quantidade mínima de dados de cada `cohort` deve conter
1. Intervalo de tempo após `cohort` ocorrência

#### 1. Agrupamento `cohorts`

`Cohorts` são agrupados por um carimbo de data e hora, como **data de registro** ou **data do primeiro pedido**.

>[!NOTE]
>
>Não é possível usar o mesmo carimbo de data e hora em que a métrica foi criada para a variável `cohort` data. Para uma análise que exija isso, é possível usar a variável `Standard report builder` em vez disso.

#### 2. `Cohort` período

Escolha o período de tempo para agrupar `cohorts` por. Em outras palavras, qual parte do carimbo de data e hora selecionado acima é mais importante; o `week`, `month`, `quarter`ou `year`?  Seu relatório exibirá os dados em qualquer intervalo selecionado aqui

#### 3. e 4. Defina o número de `cohorts` para visualizar e quantos dados cada `cohort` deve ter

Esses parâmetros ajudam você a visualizar somente o `cohorts` que você está interessado e o que é útil `Preview` na parte inferior da janela, mostra exatamente quais coortes serão exibidos no relatório.

Por padrão, a variável `cohort` não será incluído a menos que você altere a quantidade mínima de dados necessária para cada `cohort` para `0`. Nesse caso, a variável `cohort` para o período atual, incluirá apenas dados parciais.

#### 5. Intervalo de tempo após `Cohort` Ocorrência

Este recurso permite que você defina o intervalo de tempo de dados que você visualiza para o `cohorts`. Por exemplo, se você quiser exibir 24 mensais `cohorts` baseado em `customer's first order date`, mas você só está interessado nos primeiros 3 meses de dados para cada `cohort`, é possível definir a variável `number of cohorts to view` para `24` e `time range after cohort occurrence` para `3`.

O intervalo desse valor muda com o que você selecionou na variável `cohort time period` e o valor é definido como `12` Por padrão; o valor não será alterado a menos que você clique no ícone do calendário para editá-lo.

![](../../assets/cohort-time-range.png)

#### Outras observações

* [!UICONTROL Filters]: aplicadas às suas métricas permanecerão intactas ao alternar entre `Standard` e `Cohort` exibições.

* Consulte [`Perspectives`](#perspectives).

#### Exemplo

Aqui está um exemplo para juntar tudo. Neste exemplo, eu desejo verificar o comportamento do pedido após uma `cohort`A primeira compra do para ver se o coorte está voltando para fazer compras repetidas nos próximos 6 meses.

![Coorte de pedidos](../../assets/crb_example.gif)

### Arquitetura herdada

#### Arquitetura herdada {#personalinfo}

Abaixo estão as instruções específicas da versão herdada do `Cohort Report Builder`. Se estiver interessado em usar a nova versão, consulte [Nova arquitetura](../../administrator/account-management/new-architecture.md) para obter mais informações sobre como migrar para um [!DNL MBI] Nova conta de Arquitetura.

#### Como criar meu próprio `cohort` análise? {#create}

![](../../assets/create-cohort-analysis.png)

`Cohort` análise em ação! Aqui, podemos ver a receita crescendo ao longo do tempo de forma cumulativa e por usuário.

Nesta seção, orientamos você na criação da sua `cohort` análise. Por exemplo (e GIF animadas demonstrando o processo), observe o [Seção Exemplos](#examples) deste artigo.

1. Clique em **[!UICONTROL Report Builder]** na guia esquerda ou **[!UICONTROL Add Report** > **Create Report]** em qualquer painel.

1. No `Report Builder Selection` , clique em **[!UICONTROL Create Report]** ao lado do `Cohort Analysis` opção.

#### Adicionar uma métrica

Agora que estamos no `Cohort Report Builder`, Vamos adicionar a métrica (exemplo: `Revenue` ou `Number of orders`) que queremos realizar a análise.

>[!NOTE]
>
>Nativo [!DNL Google Analytics] não são compatíveis com a `Cohort Report Builder`.

#### Selecionar a data da coorte {#date}

A próxima etapa é especificar a variável `cohort date`. Essa é a data em que seus usuários serão agrupados. Por exemplo, isso pode ser `User's first order date` ou `User's registration date`.

>[!NOTE]
>
>Não é possível usar a mesma data em que a métrica foi criada (por exemplo: `created at`) como a `cohort date`.

#### Configuração do intervalo e período

Em seguida, definimos o `Interval` e `Time Period`.

`Interval`
O `Interval` permite definir a variável `length` do seu `cohorts`. Por exemplo, se estiver definido como `Month`, seu relatório será medido em meses.

Você pode alterar como esses intervalos são exibidos no eixo x usando o **Duração** menu.

`Time Period`
Use o `Time Period` para escolher o usuário específico `cohorts` para analisar. Você pode mostrar a cada `cohort`, escolha em uma lista, especifique um intervalo de tempo ou defina um intervalo de tempo em andamento de `cohorts` para incluir. Por exemplo, se usarmos a variável `Specific Cohorts` , podemos selecionar meses específicos para incluir na análise:

![Usar o `Time Period` para adicionar Específico `Cohorts`](../../assets/Cohort_Time_Period.gif)

Se agruparmos nossas `cohorts` por data de registro e, em seguida, selecionados abril, maio e junho no `Specific Cohorts` qualquer usuário que se registrasse nesses meses seria incluído.

#### Definição do eixo X

Em `duration`, é possível definir as configurações do eixo X do gráfico. Ou seja, quantos períodos de tempo cada ponto de dados representa e quantos pontos de dados devem ser incluídos na análise.

#### Selecionar o `counting members` tabela

Se você optou por agrupar usuários por um `cohort date` que foi unido de outra tabela, você pode ver uma `counting members in the … table` opção.

![](../../assets/Cohort_Counting_Members_option.png)

Vejamos um exemplo para entender essa configuração. Suponha que você tenha criado um coorte de relatório para `Revenue` métrica por `Customer's registration date`. Você também queria usar a perspectiva `Average value per cohort member` para ver a receita por comprador ao longo do tempo. Para encontrar o valor médio por comprador, precisamos decidir o número de compradores para dividir. É o número de clientes registrados em seu `customers` ou é o número de compradores distintos em sua tabela `orders table` pelo mesmo período?

Essa configuração responde a essa pergunta. Contagem de membros no `customers` a tabela inclui todos os clientes (sejam ou não uma compra, nunca) na média. Contagem de membros no `orders` inclui apenas clientes que fizeram uma compra.

#### Seleção de uma perspectiva {#perspective}

Após definir a métrica e como deseja analisá-la, é possível selecionar a variável `perspective` você deseja usar.

Logo acima da visualização do relatório, há uma lista suspensa de `perspective` configurações.

Consulte [Perspectivas](#perspectives).

![](../../assets/Cohort_Perspective_Menu.png)

## Exemplos de análise de coorte {#examples}

Agora que passamos por como criar um `cohort` analisemos alguns exemplos.

### Quero saber como meu usuário `cohorts` estão crescendo ao longo do tempo.

![Usuário `cohorts` crescendo ao longo do tempo](../../assets/cohort1.gif)

Neste exemplo, analisamos a variável `Revenue` métrica, agrupada pelas coortes pela variável `customer's first order date`e selecionou as 8 mais recentes `cohorts` (definido na variável `Time Period` ) para incluir na análise. Para ver como os coortes cresceram com o tempo, usamos a variável `Cumulative Average Value per Cohort Member` `perspective`.

### Eu quero saber, em média, quantos pedidos um usuário faz em diferentes pontos da vida.

!![Average number of orders users make at different points in their lifetimes](../../assets/cohort2.gif)

Neste exemplo, analisamos a variável `Number of orders` métrica, agrupada pelas coortes pela variável `customer's first order date`e incluiu os 8 coortes mais recentes (definido na variável `Time Period` na análise. Para ver o número médio de pedidos para cada coorte, alteramos o `perspective` para `Average Value per Cohort Member`.

### Quero entender como a atividade futura de compra de um usuário se compara à atividade do primeiro mês com a empresa.

![Comparação da atividade de compra futura de um usuário com o primeiro mês de atividade](../../assets/cohort3.gif)

## `Perspectives` {#perspectives}

`Standard`
Isto mostra o contributo incremental de um determinado grupo de coorte em qualquer ponto do seu ciclo de vida. (exemplo: O ponto &quot;Semana 6&quot; exibe todos os pontos de dados feitos pelos usuários em sua sexta semana.)

`Average Value per Cohort Member`
Isso divide o `Standard cohort` análise em (1) pelo número de usuários em cada `cohort` grupo. Isso pode ser útil para comparar desempenhos de coorte em uma base maçãs com maçãs, pois nem todos os grupos de coorte podem incluir o mesmo número de usuários. Por exemplo, a receita média da semana 6 por usuário de um determinado `cohort`.

`Cumulative`
Essa `perspective` mostra os `cohort` análise em uma `cumulative` base. Por outras palavras, mostra a contribuição total de um determinado coorte até agora em qualquer ponto do seu ciclo de vida. Por exemplo, a receita cumulativa após 6 semanas de usuários de um determinado coorte.

`Cumulative Average Value per Cohort Member`
Isso divide o `Cumulative` análise em (3) pelo número de usuários em cada `cohort` grupo. Ele mostra a contribuição média vitalícia (geralmente a receita média vitalícia) por `cohort` membro em cada período do `cohort's` vida. Por exemplo, a receita média do tempo de vida após 6 meses de usuários que aderiram em junho.

`Percent of First Value (show first value)`
Isso analisa o agregado `cohort` numa determinada altura `cohort's` ciclo de vida em percentagem da sua contribuição no primeiro período. Por exemplo, a receita do mês 6 dividida pela receita do mês 1 dos usuários que ingressaram em junho.

`Percent of First Value (hide first value)`
É o mesmo que o `perspective` acima, exceto que o primeiro valor do período de tempo de 100% está oculto.

## Quebra de linha {#finish}

O `Cohort Report Builder` atualmente é otimizada para agrupar usuários por um `cohort date`. Você pode estar interessado em agrupar os usuários por uma atividade ou atributo semelhante - se esse for o caso, gostaríamos de ajudar! Recomendamos verificar [este tutorial sobre coortes qualitativos](../dev-reports/create-qual-cohort-analysis.md) para começar.
