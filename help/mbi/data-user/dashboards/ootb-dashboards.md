---
title: Painéis incluídos
description: Saiba como verificar a integridade de métricas essenciais, como a receita vitalícia do usuário, o número de compras repetidas e muito mais, criando assim uma base sólida para exploração futura.
exl-id: f50fc417-e5d4-401c-9baa-cda1468196a2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 0%

---

# Painéis incluídos

[!DNL Adobe] oferece `eCommerce` e `SaaS` Pacotes de Início. Esses pacotes, criados pelos analistas do Adobe, contêm um conjunto personalizado de painéis e relatórios para seu conjunto de dados. As análises contidas nesses pacotes permitem verificar a integridade de métricas essenciais, como a receita vitalícia do usuário, o número de compras repetidas e muito mais, criando, assim, uma base sólida para exploração futura.

>[!NOTE]
>
>A disponibilidade de alguns painéis depende do seu conjunto de dados.

Em caso de dúvidas ou se você estiver interessado em adicionar um pacote à sua conta, envie um [tíquete de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=pt-BR) para obter ajuda.

## Visão geral executiva

O painel `executive overview` é construído a partir de gráficos que existem em outros painéis. Esse painel é uma visão geral de alto nível de seus dados e contém gráficos que seriam revisados diariamente, enquanto outros painéis continham informações mais detalhadas. Inicialmente, ele é definido como o painel padrão em cada conta.

Um conjunto geral de gráficos é incluído para você. A Adobe recomenda que você personalize esse painel de acordo com suas necessidades, adicionando outros gráficos usados com mais frequência.

## Análise de coorte

O painel `cohort analysis` inclui um conjunto de gráficos que mostram o crescimento médio da receita do tempo de vida do usuário e o crescimento incremental da receita agrupados por coortes de registro. Isso revela se o valor vitalício do cliente (LTV), o valor de um cliente para uma empresa, aumenta com o tempo e também identifica tendências em torno do crescimento do LTV. Por padrão, *todos os usuários registrados (compradores e não compradores) são contabilizados* no cálculo de LTV médio - consulte o [tópico de análise de coorte](../../data-analyst/dev-reports/cohort-rpt-bldr.md).

Esse painel também pode incluir gráficos de coorte que analisam a receita vitalícia de usuários de uma fonte de aquisição, canal ou demografia específica (por exemplo, Nova York ou Califórnia). Isso é para demonstrar como você pode analisar o LTV para segmentos específicos da sua base de usuários e ver se um grupo ou outro produz um LTV mais alto ao longo do tempo.

Para obter mais informações sobre coortes, consulte [Executando Análise de Coorte](../../data-analyst/dev-reports/cohort-rpt-bldr.md).

Se você não estiver rastreando a fonte de aquisição do usuário no momento, consulte a [Visão geral dos dados do Source de Aquisição do usuário](../../data-analyst/analysis/google-track-user-acq.md).

## Resumo de email

O painel `Email Summary` inclui um conjunto de amostras de gráficos que podem ser usados em um resumo de email diário automatizado. Consulte [criando resumos automatizados de email](../../data-user/export-data/email-summaries.md) para obter mais informações sobre como configurar resumos de email.  

## Integridade da retenção

O painel `Retention health` revela o comportamento de compra repetida da sua base de usuários.

O gráfico `Time between orders` mostra o tempo médio e/ou mediano decorrido entre a primeira e a segunda ordem de um usuário, a segunda e a terceira ordem e assim por diante. Você pode [considerar o uso desses dados para configurar suas campanhas de marketing por email](http://blog.rjmetrics.com/acting-on-marketing-data-in-your-rjmetrics-online-dashboard/).

O gráfico `Users by lifetime number of orders` lista o número total de usuários para cada número de pedidos vitalício para fornecer uma visão geral do comportamento de compra repetida.  

O gráfico `Repeat order probability` mostra a probabilidade de um usuário com um determinado número de pedido fazer uma compra repetida. Para ver a probabilidade de clientes que fizeram `x` pedidos para fazer `(x+1)` pedidos, divida o número de pessoas que fizeram pelo menos `(x+1)` compras pelo número de pessoas que fizeram pelo menos `x` compras.

### Exemplo

Número de clientes que fizeram uma compra em sua vida: `90`

Número de clientes que fizeram duas compras durante sua vida útil: `30`

Número de clientes que fizeram três compras durante sua vida útil: `10`

Neste exemplo, a probabilidade de ordem de repetição de clientes que fizeram uma compra em sua vida para fazer uma segunda compra é: `(30 + 10) / (30+10+90) = 30.77%`.

## Crescimento do LTV do cliente

O painel `Customer LTV growth` inclui um conjunto de gráficos que encontram a receita média por usuário. Os gráficos são segmentados com base na receita média gerada nos primeiros 30, 60, 90 ou 365 dias após o registro.  

A linha inferior dos gráficos mostra que essas médias segmentadas por fontes de aquisição ou dados demográficos para revelar quais grupos de usuários geram mais receita ao longo do tempo.

## Desempenho do produto

O painel `Product Performance` inclui gráficos que revelam o desempenho geral do produto, exibindo o número de itens vendidos e a receita por item e identificando os produtos com melhor desempenho.

## Atividade recente

O painel `Recent Activity` mostra os dados de desempenho dos últimos 30 dias.

## Integridade transacional

O painel `Transaction Health` inclui gráficos de visão geral de receita, pedidos e valor médio de pedido. Esses gráficos podem ser segmentados por canais de marketing, dados demográficos ou por códigos de cupom especiais.

## Usuários a serem direcionados

O painel `Users to target` inclui gráficos de estilo de tabela que listam usuários com comportamentos de compra específicos em comum. Alguns exemplos incluem:

* Lista de compradores únicos que compraram `X` meses atrás (quem você pode reativar)

* Lista dos principais gastadores (quem você pode querer manter feliz)

* Lista dos principais gastadores que estavam ativos nos últimos `X` dias (quem você pode premiar)

Usando suas ferramentas de exportação de dados, é fácil [criar listas de email de usuários com comportamento de compra semelhante para marketing de público alvo](http://blog.rjmetrics.com/creating-contact-lists-for-top-customers/).

## Atividade do usuário

O painel `User activity` inclui gráficos que segmentam os usuários por vários dados, incluindo fonte de aquisição, dados demográficos e a primeira vez que a média é solicitada. Também inclui análise de coorte de usuários, incluindo a receita média geral por vida útil por mês de registro dos usuários.

O gráfico `% of cohort members who have purchased` é importante porque mostra a taxa de conversão (de 0 a 1) dos usuários com base em quando eles se registram (cada linha representa um coorte de usuários). Ele também mostra quando eles fazem sua primeira compra (por exemplo, no mês 1, 2, 3... após o registro). Isso pode mostrar que 10% dos usuários foram ativados no mês 1, enquanto esse número cresce no mês 2, 3, 4... e pode estabilizar posteriormente.

Normalmente, as linhas neste gráfico se tornam horizontais após algum período de tempo. Isso indica que poucos membros de coorte adicionais estão fazendo uma conversão orgânica depois desse ponto - a maioria dos usuários que vai fazer uma compra já fez isso. Neste ponto, é altamente improvável que esses membros se convertam em compradores sem intervenção. [Contatá-los com promoções personalizadas ou emails direcionados é uma maneira de baixo risco de iniciar a conversão dessa população.](http://blog.rjmetrics.com/acting-on-marketing-data-in-your-rjmetrics-online-dashboard/)
