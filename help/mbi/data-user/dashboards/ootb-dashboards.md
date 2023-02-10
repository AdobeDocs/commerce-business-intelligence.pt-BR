---
title: Painéis incluídos
description: Saiba como verificar a integridade de métricas essenciais, como receita vitalícia do usuário, número de compras repetidas e muito mais, criando assim uma base sólida para exploração futura.
exl-id: f50fc417-e5d4-401c-9baa-cda1468196a2
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 0%

---

# Painéis incluídos

Como parte de nossos serviços, oferecemos comércio eletrônico e `SaaS` Pacotes iniciais. Esses pacotes, criados pelos analistas, contêm um conjunto personalizado de painéis e relatórios para o conjunto de dados. As análises contidas nesses pacotes permitem verificar a integridade de métricas essenciais, como receita vitalícia do usuário, número de compras repetidas e muito mais, criando assim uma base sólida para exploração futura.

>[!NOTE]
>
>A disponibilidade de alguns painéis depende do conjunto de dados.

Em caso de dúvidas ou de interesse em adicionar um pacote à sua conta, envie um [tíquete de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) para obter ajuda.

## Visão geral executiva

O `executive overview` o painel é criado a partir de gráficos que existem em outros painéis. Este painel é uma visão geral de alto nível de seus dados e contém gráficos que seriam revisados diariamente, enquanto outros painéis continham informações mais detalhadas. Inicialmente, é definido como o painel padrão em cada conta.

Embora tenhamos incluído um conjunto geral de gráficos para você, recomendamos que você adapte esse painel às suas necessidades adicionando outros gráficos que você usa com mais frequência.

## Análise de coorte

O `cohort analysis` o painel inclui um conjunto de gráficos que mostram o crescimento médio da receita vitalícia do usuário e o crescimento da receita incremental agrupados por coortes de registro. Isso revela se o valor da vida útil do cliente (LTV), o valor de um cliente para um negócio, aumenta com o tempo e também identifica tendências sobre o crescimento da LTV. Observe que, por padrão, *estamos contabilizando todos os usuários registrados (compradores e não compradores)* no cálculo do LTV médio - consulte o [tópico da análise de coorte](../../data-analyst/dev-reports/cohort-rpt-bldr.md).

Esse painel também pode incluir gráficos de coorte que analisam a receita vitalícia de usuários de uma fonte de aquisição específica, canal ou demografia (por exemplo, Nova York ou Califórnia). Isso é para demonstrar como você pode analisar a LTV para segmentos muito específicos de sua base de usuários e ver se um grupo ou outro gera um LTV maior ao longo do tempo.

Para obter mais informações sobre coortes, consulte [Execução da análise de coorte](../../data-analyst/dev-reports/cohort-rpt-bldr.md).

Se, atualmente, você não estiver rastreando a fonte de aquisição do usuário, consulte [Rastrear Visão geral dos dados da fonte de aquisição do usuário](../../data-analyst/analysis/google-track-user-acq.md).

## Resumo do email

O `Email Summary` o painel inclui um conjunto de gráficos de amostra que podem ser usados em um resumo diário automatizado do email. Consulte [criação de resumos de email automatizados](../../data-user/export-data/email-summaries.md) para obter mais informações sobre como configurar resumos de email.  

## Integridade da retenção

O `Retention health` O painel revela o comportamento de compra repetido da base de usuários.

O `Time between orders` gráfico mostra o tempo médio e/ou mediano decorrido entre o primeiro e o segundo pedidos de um usuário, o segundo e o terceiro pedidos e assim por diante. Você pode [considere usar esses dados para configurar suas campanhas de marketing por email](http://blog.rjmetrics.com/acting-on-marketing-data-in-your-rjmetrics-online-dashboard/).

O `Users by lifetime number of orders` gráfico lista o número total de usuários para cada número de vida útil de pedidos para fornecer uma visão geral do comportamento de compra repetida.  

O `Repeat order probability` gráfico mostra a probabilidade de um usuário com um determinado número de pedido realizar uma compra repetida. Para ver a probabilidade dos clientes que fizeram o `x` ordens para `(x+1)` pedidos, simplesmente divida o número de pessoas que fizeram pelo menos `(x+1)` compras pelo número de pessoas que fizeram pelo menos `x` compras.

### Exemplo

Número de clientes que efetuaram uma compra durante sua vida útil: `90`

Número de clientes que efetuaram duas compras ao longo da vida: `30`

Número de clientes que efetuaram três compras ao longo da vida: `10`

Neste exemplo, a probabilidade de repetição de pedido de clientes que fizeram uma compra em sua vida útil para fazer uma segunda compra é: `(30 + 10) / (30+10+90) = 30.77%`.

## Crescimento da LTV do cliente

O `Customer LTV growth` o painel inclui um conjunto de gráficos que localiza a receita média por usuário. Os gráficos são segmentados com base na receita média gerada nos primeiros 30, 60, 90 ou 365 dias após o registro.  

A linha inferior dos gráficos mostra essas médias segmentadas por fontes de aquisição ou por dados demográficos para revelar quais grupos de usuários geram mais receita ao longo do tempo.

## Desempenho do produto

O `Product Performance` o painel inclui gráficos que revelam o desempenho geral do produto, exibindo o número de itens vendidos e a receita por item, bem como identificando os produtos de maior desempenho.

## Atividade recente

O `Recent Activity` O painel mostra os dados de desempenho dos últimos 30 dias.

## Saúde transacional

O `Transaction Health` o painel inclui gráficos de visão geral de receita, pedidos e valor médio de pedido. Esses gráficos podem ser segmentados por canais de marketing, demografia ou por códigos de cupom especiais.

## Usuários para direcionar

O `Users to target` o painel inclui gráficos de estilo de tabela que listam usuários com comportamentos de compra específicos em comum. Alguns exemplos incluem:

* Lista de compradores únicos que compram `X` meses atrás (quem você pode querer reativar)

* Lista dos principais gastadores (que você pode querer manter felizes)

* Lista dos principais gastadores que estavam ativos no passado `X` dias (quem você pode querer recompensar)

Usando nossas ferramentas de exportação de dados, é fácil [criar listas de email de usuários com comportamento de compra semelhante para marketing direcionado](http://blog.rjmetrics.com/creating-contact-lists-for-top-customers/).

## Atividade do usuário

O `User activity` o painel inclui gráficos que segmentam os usuários por uma variedade de dados, incluindo fonte de aquisição, demografia e média da primeira ordem. Também inclui a análise de coorte de usuário, incluindo a receita média geral do tempo de vida por mês de registro dos usuários.

O `% of cohort members who have purchased` o gráfico é particularmente valioso, pois mostra a taxa de conversão (entre 0 e 1) dos usuários com base em quando se registram (cada linha representa um coorte de usuários) e quando fazem sua primeira compra (por exemplo, no mês 1, 2, 3... após o registro). Isso pode mostrar que 10% dos usuários ativaram no mês 1, enquanto esse número cresce nos meses 2, 3, 4... e pode ser acumulado posteriormente.

Normalmente, as linhas neste gráfico se tornam horizontais após algum período de tempo, indicando que poucos membros de coorte adicionais estão convertendo organicamente após esse ponto - ou seja, a maioria dos usuários que farão uma compra já fez isso. Neste momento, é muito pouco provável que estes membros se convertam em compradores sem intervenção. [Chegar a eles com promoções personalizadas ou emails especificamente direcionados é uma maneira extremamente de baixo risco de iniciar rapidamente a conversão dessa população.](http://blog.rjmetrics.com/acting-on-marketing-data-in-your-rjmetrics-online-dashboard/)
