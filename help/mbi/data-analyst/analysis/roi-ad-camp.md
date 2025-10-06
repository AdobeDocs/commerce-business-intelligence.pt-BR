---
title: Aumentar o ROI em suas campanhas publicitárias
description: Saiba mais sobre alguns métodos diferentes de avaliação do desempenho da sua campanha.
exl-id: 4f2bf408-eeaf-4dbf-b62e-89426734640a
role: Admin, User
feature: Data Warehouse Manager, Reports, Campaigns
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '1253'
ht-degree: 0%

---

# Campanhas do Advertising e ROI

O [!DNL Adobe Commerce Intelligence] permite que você [combine facilmente dados de custo e receita de publicidade](../../data-analyst/importing-data/integrations/google-adwords.md) com seu banco de dados. Isso ajuda a identificar quais campanhas têm o maior retorno sobre o investimento (ROI). Este tópico explora alguns métodos diferentes de avaliação do desempenho da campanha.

## Pré-requisitos

* Importe os dados de custo de publicidade:
   * [Conectar  [!DNL Google AdWords] ao [!DNL Commerce Intelligence]](../importing-data/integrations/google-adwords.md): sincroniza seus gastos com [!DNL Adwords] no [!DNL Commerce Intelligence]
   * [Carregar outros dados de custo de publicidade](../importing-data/connecting-data/import-offline-ad-data.md): isso é recomendado para canais sem um conector direto para [!DNL Commerce Intelligence]
   * Se você importar dados de custo de várias fontes, poderá [consolidar](../../best-practices/consolidating-your-tables.md) os dados em [!DNL Commerce Intelligence]. Basta [enviar um tíquete de suporte](../../guide-overview.md#Submitting-a-Support-Ticket).
* [Rastrear dados do canal de aquisição de usuários](../analysis/google-track-user-acq.md)

## Campanhas de aquisição de usuário

As campanhas direcionadas para a aquisição de usuários podem ser medidas a partir de várias perspectivas, incluindo:

1. O número de novos usuários adquiridos das campanhas
1. A taxa de conversão de registro para compra de campanhas
1. O ROI das campanhas com base no valor médio da vida útil do usuário (LTV)

As análises (1) e (2) acima são exploradas em um tutorial separado sobre [identificação dos seus principais canais de marketing](../analysis/most-value-source-channel.md). Aqui, você explora a análise (3) para medir o ROI da campanha ao longo do tempo. Isso responde se os usuários adquiridos de uma campanha específica geraram receita vitalícia suficiente para cobrir o custo de aquisição.

>[!NOTE]
>
>Este exemplo assume que todos os custos de campanha foram usados exclusivamente para adquirir novos usuários. Na realidade, o custo da campanha também é compartilhado com a aquisição de visitas não convertidas, compradores recorrentes e assim por diante. Ao assumir que todo o custo é usado para adquirir novos usuários registrados, o ROI resultante leva em conta o pior cenário (custo mais alto por aquisição). Você pode ter certeza de que seu ROI real é superior ao seu cálculo.
>
>Exemplo: supondo que você gastou US$ 20 em uma campanha que gerou 10 novos usuários e 10 compradores recorrentes, seu custo real por novo usuário é de US$ 1. Mas, com a suposição de que todo o custo foi para adquirir novos usuários, o custo por aquisição é de $2.

**1. Comece criando um gráfico que segmenta seu Custo de Anúncio por Campanhas:**

1. Crie um [!UICONTROL Metric] que some seus gastos ao longo do tempo
1. Ir para [!UICONTROL Data > Metrics]
1. Selecione `Add New Metric` e selecione a tabela [!DNL `Adwords...`] que está gravando seus dados de custo [!DNL AdWords].
1. No editor de métricas, dê um nome à sua métrica (por exemplo, [!UICONTROL AdWord Cost])
1. Usando os menus suspensos, execute uma **Soma** na coluna `adCost` da tabela [!DNL Adwords...] (Alteração) ordenada pela coluna `date`.
   ![Mensagem de sucesso após a adição de nova métrica](../../assets/success-add-new-metric.png)<!--="500" height="303"}-->
1. Clique em `Back to Metric List` na parte superior e vá para qualquer painel.

1. Criar um relatório que segmente os gastos por campanhas
1. Em qualquer painel, clique em [!UICONTROL Add Report > Create report]
1. Selecione a métrica [!UICONTROL Adword Cost] que você acabou de criar
1. Defina o [!UICONTROL Time period] como `All-time`, e [!UICONTROL Interval] como `None`
1. Na guia `Group by`, adicione `campaign` como [!UICONTROL grouping field] e clique em `Add All` na caixa.
1. Este relatório mostra seu custo total de [!DNL AdWords] por campanhas

**2. Crie um relatório que conte novos usuários por campanhas:**

1. Em qualquer painel, clique em **[!UICONTROL Add Report > Create report]**
1. Selecione a métrica `New users` que conta o número de novos usuários registrados ao longo do tempo
1. Defina o [!UICONTROL Time period] como `All-time`, e [!UICONTROL Interval] como `None`
1. Na guia `Group by`, adicione `campaign` como `grouping field` e clique em **`Add All`** na caixa
1. Este relatório mostra seus usuários registrados o tempo todo por campanhas

**3. Crie um relatório que segmenta o LTV de usuário médio por campanhas:**

1. Em qualquer painel, clique em **[!UICONTROL Add Report > Create report]**
1. Selecione a métrica `Average lifetime revenue` que calcula a receita média do ciclo de vida do usuário
1. Defina o [!UICONTROL Time period] como `All-time`, e [!UICONTROL Interval] como `None`
1. Na guia `Group by`, adicione `campaign` ou `utm\_campaign` como [!UICONTROL grouping field] e clique em `Add All` na caixa
1. Este relatório mostra a receita média do tempo de vida do usuário por campanhas

**Por fim, calcule o ROI da campanha reunindo estas três análises em um único relatório:**

1. Em qualquer painel, clique em **[!UICONTROL Add Report > Create new report]**
1. Adicione como entrada, use as três métricas usadas acima. Cada uma recebe uma letra (por exemplo,\[`A`\], \[`B`\] e \[`C`\])
1. [!UICONTROL Cost]: Adicione a métrica de custo do AdWords - esta é a variável \[A\]. Isso retorna o custo por campanhas.
1. [!UICONTROL Users]: Adicionar a métrica Novos usuários - esta é a variável \[B\]. Isso retorna o número de usuários por campanhas.
1. [!UICONTROL LTV]: adicione a métrica Receita média durante a vida útil - esta é a variável \[`C`\]. Isso retorna o LTV por campanhas.

1. Clique no ícone de ocultar ao lado da palavra Gráfico para que você possa se concentrar na tabela
1. Agora use `Add Formula` para combinar essas métricas, da seguinte maneira:
1. [!UICONTROL ROI]: Insira a fórmula `(\[C\]-\[A\]/\[B\])/(\[A\]/\[B\])`, se \[`A`\] representa `Ad Cost by Campaigns`, \[`B`\] representa `New users by campaigns` e \[`C`\] `LTV by campaigns`. Isso retorna a proporção de (LTV de usuário médio - custo médio por aquisição) / (custo médio por aquisição)
1. [!UICONTROL Avg Return per User]: Insira a fórmula **\[`C`\]-(\[`A`\]/\[`B`\])**. Isso retorna a margem média feita em um usuário calculando (LTV de usuário médio) - (custo médio por aquisição).
1. [!UICONTROL CPA]: Insira a fórmula **`\[A\]/\[B\]`**. Retorna o custo real da campanha por aquisição.
1. Outras possíveis métricas a serem incluídas dos dados de [!DNL AdWords] incluem somas de `Impressions` e `adClicks` (dos dados de [!DNL AdWords]), juntamente com o total de `number of orders` feitas por meio de uma campanha específica.
1. Também pode ser interessante calcular o ROI com base no LTV 30 dias e 90 dias após um usuário se registrar ou efetuar uma primeira compra.

1. Sinta-se à vontade para clicar e arrastar suas métricas e fórmulas para reorganizar as colunas de seu relatório
1. Nomeie seu relatório e salve como uma tabela.

## Campanhas do produto

Você está veiculando anúncios específicos de produtos? Em caso afirmativo, você pode medir o ROI nessas campanhas calculando a receita/custo de produtos específicos.

>[!NOTE]
>
>Este exemplo pressupõe que todos os custos de campanha foram usados exclusivamente para gerar compras de produtos específicos. Ao presumir que todo o custo foi gasto na geração de compras, o ROI resultante leva em conta o pior cenário (custo mais alto por compra). Você pode ter certeza de que seu ROI real é superior a esse cálculo. Exemplo: supondo que você gastou US$ 20 em uma campanha que gerou 10 novos usuários e 10 compras, seu custo real por compra é de US$ 1. Sob a suposição de que todo o custo foi para adquirir novos usuários, o custo por compra é de $2.

Antes de começar, [envie um tíquete de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=pt-BR) para unir as seguintes dimensões à tabela de itens de linha (`sales\_flat\_order\_item, order\_item`):

* Origem do pedido (se você rastrear apenas a origem de referência no nível do usuário, então ingressar na origem do usuário)
* Campanha do pedido (se você só rastrear a fonte de referência no nível do usuário e, em seguida, ingressar na campanha do usuário)
* Meio do pedido (se você só rastrear a origem de referência no nível do usuário, associe a mídia do usuário)

**1. Agora comece criando um gráfico que retorna a receita por campanha para produtos específicos:**

1. Em qualquer painel, clique em **[!UICONTROL Add Report > Create new report]**
1. Selecione a métrica `Revenue by items` que calcula a receita no nível dos itens de linha
1. Defina o [!UICONTROL Time period] como `All-time`, e [!UICONTROL Interval] como `None`
1. Na guia `Filter by`, adicione `product name 'IN'` Produto `A`, Produto `B`, Produto `C`, ...&quot; e inclua todos os nomes de produtos direcionados pela sua campanha separados por vírgula (por exemplo, `product name 'IN' yellow t-shirt`, `red t-shirt, blue t-shirt`)
1. Na guia `Group by`, adicione `order's campaign` ou `order's utm\_campaign` como campo `grouping` e clique em **[!UICONTROL Add All]** na caixa
1. Este relatório mostra a receita de produtos específicos por campanhas

**2. Para calcular o ROI, você combina métricas novamente em um relatório:**

1. Em qualquer painel, clique em **[!UICONTROL Add Report > Create new report]**
1. Adicione a métrica `Revenue by items`, seguindo o filtro e agrupe por orientações do relatório de campanha para produtos específicos acima e clique em **[!UICONTROL Hide]** abaixo do valor escalar da métrica
1. Agora adicione a métrica [!DNL AdWords Cost], seguindo o filtro e agrupe por direções do relatório `Ad cost by campaigns` explorado na seção `User acquisition campaigns` acima; em seguida, clique em **[!UICONTROL Hide]** abaixo do valor escalar da métrica
1. Com essas métricas implementadas, adicione fórmulas:
1. [!UICONTROL ROI]: Insira a fórmula `\[A\]/\[B\]`, se `\[A\]` representa `Revenue per campaign for specific product(s)` e `\[B\]` representa `Ad cost by campaigns`. Retorna a proporção de (Receita para produtos específicos) / (Custo da campanha)
1. [!UICONTROL Return]: Insira a fórmula `\[A\]-\[B\]`. Retorna a margem média feita em um usuário calculando (LTV de usuário médio) - (custo médio por aquisição)
   1. (Opcional) [!UICONTROL Revenue]: mostre a métrica `Revenue by items` para ver a receita de produtos específicos por campanhas
   1. (Opcional) [!UICONTROL Cost]: Revele a métrica `AdWords Cost` para ver o custo de campanhas

1. Nomeie o relatório e salve-o como uma tabela

**3. Repita as etapas 1 e 2 acima para cada um dos seus produtos ou grupos de produtos anunciados.**

## Documentação relacionada

* [Rastrear origem da referência de ordem via [!DNL Google Analytics] E-Commerce](../importing-data/integrations/google-ecommerce.md)
* [Rastrear a fonte de referência do usuário no banco de dados](../analysis/google-track-user-acq.md)
* [Rastrear o dispositivo do usuário, o navegador e os dados do sistema operacional no banco de dados](../analysis/track-usr-dev-browser.md)
* [Descubra as fontes e os canais de aquisição mais valiosos](../analysis/most-value-source-channel.md)
* [Conectar sua conta  [!DNL Google Adwords] &#x200B;](../importing-data/integrations/google-adwords.md)
* [Como funciona a atribuição  [!DNL Google Analytics] UTM?](../analysis/utm-attributes.md)
* [Cinco práticas recomendadas para marcação UTM em  [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
