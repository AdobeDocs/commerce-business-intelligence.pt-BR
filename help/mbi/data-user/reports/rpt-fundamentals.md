---
title: Usar um relatório
description: Saiba como usar os dados do relatório.
exl-id: 94d4db27-0e06-4066-9c03-036b109d2d9b
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 0%

---

# Usar um relatório

Usar relatórios no [!DNL Adobe Commerce Intelligence] para ajudá-lo a responder as perguntas de negócios - se você simplesmente quer ver a receita deste mês em comparação com o ano passado ou entender seus custos de aquisição para o seu [!DNL Google AdWords] campanha.

Como é esse caminho de pergunta a resposta, exatamente?

Para ajudar a visualizar esse processo, essa rota é mapeada abaixo. Este tópico esclarece como você aborda uma questão analítica e a logística de back-end necessária para obter os dados necessários.

## Começando com a pergunta

Você sabe que está constantemente fazendo perguntas para melhorar seus negócios, desde aumentar a satisfação do cliente até cortar custos de suprimento. Você se concentra em como traduzir suas perguntas em análises que ajudam a orientar decisões.

Neste exemplo, suponha que você deseja responder à seguinte pergunta:

* Com que velocidade meus novos inscritos são convertidos?

## Identificação de uma medição

É hora de identificar uma lista de análises e medidas possíveis para ajudar a responder à pergunta. Para este exemplo, concentre-se na seguinte métrica:

* Tempo médio desde o registro até a primeira data de compra por uso.

Isso revela o tempo médio que decorre entre a data de registro e a primeira data de compra dos usuários e fornece uma ideia sobre como os usuários se comportam nesta etapa final do funil de conversão.

## Localização dos dados

Entender o que medir só nos leva a parte do caminho até lá. Para avaliar o tempo médio desde o registro até a primeira data de compra por usuário, é necessário identificar todos os pontos de dados dos quais sua medida é composta.

Detalhe sua medida em seus componentes principais. Você deve saber a contagem, ou número, de pessoas que se registraram, a contagem de pessoas que fizeram uma compra e o tempo decorrido entre esses dois eventos.

Em um nível superior, você precisa saber onde encontrar esses dados no banco de dados, especificamente:

* A tabela que registra uma linha de dados sempre que alguém se registra
* A tabela que registra uma linha de dados que sempre que alguém faz uma compra
* A coluna que pode ser usada para unir ou fazer referência a `purchase` tabela para a `customer` tabela - permite saber quem fez uma compra

Em um nível mais granular, é necessário identificar os campos de dados exatos usados para essa análise:

* A tabela e a coluna de dados que contêm a data de registro de um cliente: por exemplo `user.created\_at`
* A tabela e a coluna de dados que contêm uma data de compra: por exemplo `order.created\_at`

## Criação de colunas de dados para análise

Além das colunas de dados nativas descritas acima, também é necessário um conjunto de campos de dados calculados para habilitar essa análise, incluindo:

* `Customer's first purchase date` que retorna o perfil de um usuário específico `MIN(order.created_at`)

Isso é usado para criar:

* `Time between a customer's registration date and first purchase date`, que retorna o tempo decorrido de um usuário específico entre o registro e a primeira data de compra. Essa é a base para sua métrica posteriormente.

Ambos os campos precisam ser criados no nível do usuário (por exemplo, no `user` tabela). Isso permite que a análise média possa ser normalizada por usuários (em outras palavras, o denominador nesse cálculo médio é a contagem de usuários).

É aqui que [!DNL Commerce Intelligence] passos! Você pode usar seu [!DNL Commerce Intelligence] Data Warehouse para criar as colunas acima. Entre em contato com a equipe de analistas do Adobe e forneça a definição específica de suas novas colunas para criação. Você também pode usar a variável [Editor de coluna](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md).

É uma prática recomendada evitar a criação desses campos de dados calculados diretamente no banco de dados, pois sobrecarrega desnecessariamente os servidores de produção.

## Criação da métrica

Agora que você tem os campos de dados necessários para a análise, é hora de encontrar ou criar a métrica relevante para criar a análise.

Aqui você deseja executar o seguinte cálculo:


_[SOMA de `Time between a customer's registration date and first purchase date`] / [Número total de clientes que se registraram e compraram]_

E você deseja ver esse cálculo representado ao longo do tempo, ou tendência, de acordo com a data de registro de um cliente. E aqui está como: [criar esta métrica](../../data-user/reports/ess-manage-data-metrics.md) in [!DNL Commerce Intelligence]:

1. Ir para **[!UICONTROL Data]** e selecione o `Metrics` guia.
1. Clique em **[!UICONTROL Add New Metric]** e selecione o `user` tabela (onde você criou as dimensões acima).
1. Na lista suspensa, selecione `Average` no`Time between a customer's registration date and first purchase date` na `user` tabela ordenada pelo `Customer's registration date`  coluna.
1. Adicione filtros ou conjuntos de filtros relevantes.

Essa métrica agora está pronta.

## Criação do relatório

Com a nova métrica configurada, você pode usá-la para relatar o tempo médio entre o registro e a primeira data de compra por data de registro.

Basta ir a qualquer painel e [criar um relatório](../../data-user/reports/ess-manage-data-metrics.md) usando a métrica criada acima.

### `Visual Report Builder` {#visualrb}

[A variável `Visual Report Builder`](../../data-user/reports/ess-rpt-build-visual.md) é a maneira mais fácil de visualizar seus dados. Se você não estiver familiarizado com o SQL ou se quiser criar um relatório rapidamente, o Visual Report Builder é a sua melhor opção. Com apenas alguns cliques, você pode adicionar métricas, segmentar seus dados e criar relatórios no em toda a organização. Essa opção é perfeita para iniciantes e especialistas, pois não requer conhecimento técnico.

|  |  |
|--- |--- |
| **Isso é perfeito para...** | **Isso não é tão bom para...** |
| - Todos os níveis de experiência técnica/de análise<br>- Criar relatórios rapidamente<br>- Criação de análises para compartilhar com outros usuários | - Análises que exigem funções específicas de SQL<br>- Teste de novas colunas - as colunas calculadas dependem dos ciclos de atualização da população de dados inicial, enquanto as criadas usando o SQL não dependem. |

{style="table-layout:auto"}

### Descrições e imagens de relatório

#### Adição de descrições a relatórios

Ao criar relatórios compartilhados com outros membros da equipe, o Adobe recomenda adicionar descrições que permitam que outros usuários entendam melhor sua análise.

1. Clique em **[!UICONTROL i]** na parte superior de qualquer relatório.
1. Digite uma descrição na caixa de palavras.
1. Clique em **[!UICONTROL Save Description]**.

Consulte abaixo:

![Descrição do gráfico](../../assets/Chart_Description.gif)

#### Exportação de relatórios como imagens

Precisa incluir um relatório em uma apresentação ou documento? Qualquer relatório pode ser salvo como uma imagem (no formato PNG, PDF ou SVG) usando `Report Options` localizado no canto superior direito de cada relatório.

1. Clique no ícone de engrenagem no canto superior direito de qualquer relatório.
1. Na lista suspensa, selecione `Enlarge`.
1. Quando o relatório aumentar, clique em **[!UICONTROL Download]** no canto superior direito do relatório.
1. Selecione o formato de imagem preferencial na lista suspensa. O download começa imediatamente.

Consulte abaixo:

![](../../assets/exp-rep-as-image.gif)
