---
title: Aumentar o ROI em suas campanhas publicitárias
description: Saiba mais sobre alguns métodos diferentes de avaliação do desempenho da sua campanha.
exl-id: 4f2bf408-eeaf-4dbf-b62e-89426734640a
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 0%

---

# Campanhas publicitárias e ROI

O MBI permite [casar dados de custo de publicidade e dados de receita](../../data-analyst/importing-data/integrations/google-adwords.md) do banco de dados. Isso ajuda a identificar quais campanhas têm o ROI mais alto. Este artigo explora alguns métodos diferentes de avaliação do desempenho da campanha.

## Pré-requisitos

* Importe os dados de custo de publicidade:
   * [Conecte seu [!DNL Google AdWords] para [!DNL MBI]](../importing-data/integrations/google-adwords.md): sincroniza o [!DNL Adwords] gastar em [!DNL MBI]
   * [Carregar outros dados de custo de publicidade](../importing-data/connecting-data/import-offline-ad-data.md): Isso é recomendado para canais sem um conector direto para [!DNL MBI]
   * Se você importar dados de custo de várias fontes, poderá [consolidar](../../best-practices/consolidating-your-tables.md) os dados em [!DNL MBI]. Simplesmente [enviar um tíquete de suporte](../../guide-overview.md).
* [Rastrear dados do canal de aquisição de usuários](../analysis/google-track-user-acq.md)

## Campanhas de aquisição de usuário

As campanhas direcionadas para a aquisição de usuários podem ser medidas a partir de várias perspectivas, incluindo:

1. O número de novos usuários adquiridos das campanhas
1. A taxa de conversão de registro para compra de campanhas
1. O ROI das campanhas com base no valor médio da vida útil do usuário (LTV)

As análises 1 e 2 acima são exploradas em um tutorial separado sobre [identificação dos principais canais de marketing](../analysis/most-value-source-channel.md). Aqui, você explora a análise (3) para medir o ROI da campanha ao longo do tempo. Isso responde se os usuários adquiridos de uma campanha específica geraram receita vitalícia suficiente para cobrir o custo de aquisição.

>[!NOTE]
>
>Este exemplo assume que todos os custos de campanha foram usados exclusivamente para adquirir novos usuários. Na realidade, o custo da campanha também é compartilhado com a aquisição de visitas não convertidas, compradores recorrentes e assim por diante. Ao assumir que todo o custo é usado para adquirir novos usuários registrados, o ROI resultante leva em conta o pior cenário (custo mais alto por aquisição). Você pode ter certeza de que seu ROI real é superior ao seu cálculo.
>
>Exemplo: supondo que você gastou US$ 20 em uma campanha que gerou 10 novos usuários e 10 compradores recorrentes, seu custo real por novo usuário é de US$ 1. Mas, com a suposição de que todo o custo foi para adquirir novos usuários, o custo por aquisição é de $2.)

**1. Comece criando um gráfico que segmenta o custo do anúncio por campanhas:**

1. Criar um [!UICONTROL Metric] que soma seus gastos ao longo do tempo
1. Ir para [!UICONTROL Data > Metrics]
1. Selecionar `Add New Metric` e selecione o [!DNL `Adwords...`] tabela que está gravando seu [!DNL AdWords] dados de custo.
1. No editor de métricas, nomeie a métrica (por exemplo, [!UICONTROL AdWord Cost])
1. Usando os menus suspensos, execute uma **Sum** no `adCost` na [!DNL Adwords...] tabela (Alteração) ordenada pelo `date` coluna.
   ![](../../assets/success-add-new-metric.png)<!--="500" height="303"}-->
1. Clique em `Back to Metric List` na parte superior e vá para qualquer painel.

1. Criar um relatório que segmente os gastos por campanhas
1. Em qualquer painel, clique em [!UICONTROL Add Report > Create report]
1. Selecione o [!UICONTROL Adword Cost] métrica que você acabou de criar
1. Defina o [!UICONTROL Time period] para `All-time`, e [!UICONTROL Interval] para `None`
1. No `Group by` , adicionar `campaign` as [!UICONTROL grouping field]e clique em `Add All` na caixa.
1. Este relatório mostra o seu [!DNL AdWords] custo por campanhas

**2. Crie um relatório que conte novos usuários por campanhas:**

1. Em qualquer painel, clique em **[!UICONTROL Add Report > Create report]**
1. Selecione o `New users` métrica que conta o número de novos usuários registrados ao longo do tempo
1. Defina o [!UICONTROL Time period] para `All-time`, e [!UICONTROL Interval] para `None`
1. No `Group by` , adicionar `campaign` as `grouping field`e clique em **`Add All`** na caixa
1. Este relatório mostra seus usuários registrados o tempo todo por campanhas

**3. Crie um relatório que segmenta o LTV de usuário médio por campanhas:**

1. Em qualquer painel, clique em **[!UICONTROL Add Report > Create report]**
1. Selecione o `Average lifetime revenue` métrica que calcula a receita vitalícia média de um usuário
1. Defina o [!UICONTROL Time period] para `All-time`, e [!UICONTROL Interval] para `None`
1. No `Group by` , adicionar `campaign` ou `utm\_campaign` as [!UICONTROL grouping field]e clique em `Add All` na caixa
1. Este relatório mostra a receita média do tempo de vida do usuário por campanhas

**Por fim, calcule o ROI da campanha reunindo essas três análises em um relatório:**

1. Em qualquer painel, clique em **[!UICONTROL Add Report > Create new report]**
1. Adicione como entrada, use as três métricas usadas acima. A cada uma é atribuída uma letra (por exemplo,\[`A`\], \[`B`\], e \[`C`\])
1. [!UICONTROL Cost]: adicione a métrica Custo do AdWords - essa é a variável \[A\]. Isso retorna o custo por campanhas.
1. [!UICONTROL Users]: adicione a métrica Novos usuários - isso é variável \[B\]. Isso retorna o número de usuários por campanhas.
1. [!UICONTROL LTV]: adicione a métrica Receita média durante a vida útil. Essa é a variável \[`C`\]. Isso retorna o LTV por campanhas.

1. Clique no ícone de ocultar ao lado da palavra Gráfico para que você possa se concentrar na tabela
1. Agora use `Add Formula` para combinar essas métricas, da seguinte maneira:
1. [!UICONTROL ROI]: Insira a fórmula `(\[C\]-\[A\]/\[B\])/(\[A\]/\[B\])`, se \[`A`\] representa `Ad Cost by Campaigns`, \[`B`\] representa `New users by campaigns`, e \[`C`\] `LTV by campaigns`. Isso retorna a proporção de (LTV de usuário médio - custo médio por aquisição) / (custo médio por aquisição)
1. [!UICONTROL Avg Return per User]: Insira a fórmula **\[`C`\]-(\[`A`\]/\[`B`\])**. Isso retorna a margem média feita em um usuário calculando (LTV de usuário médio) - (custo médio por aquisição).
1. [!UICONTROL CPA]: Insira a fórmula **`\[A\]/\[B\]`**. Retorna o custo real da campanha por aquisição.
1. Outras métricas em potencial a serem incluídas de [!DNL AdWords] os dados incluem somas de  `Impressions` e `adClicks` (de [!DNL AdWords] dados), juntamente com o total de `number of orders` feitas por meio de uma campanha específica.
1. Também pode ser interessante calcular o ROI com base no LTV 30 dias e 90 dias após um usuário se registrar ou efetuar uma primeira compra.

1. Sinta-se à vontade para clicar e arrastar suas métricas e fórmulas para reorganizar as colunas de seu relatório
1. Nomeie seu relatório e salve como uma tabela.

## Campanhas do produto

Você está veiculando anúncios específicos de produtos? Em caso afirmativo, você pode medir o ROI nessas campanhas calculando a receita/custo de produtos específicos.

>[!NOTE]
>
>Este exemplo pressupõe que todos os custos de campanha foram usados exclusivamente para gerar compras de produtos específicos. Ao presumir que todo o custo foi gasto na geração de compras, o ROI resultante leva em conta o pior cenário (custo mais alto por compra). Você pode ter certeza de que seu ROI real é superior a esse cálculo. Exemplo: supondo que você gastou US$ 20 em uma campanha que gerou 10 novos usuários e 10 compras, seu custo real por compra é de US$ 1. Sob a suposição de que todo o custo foi para adquirir novos usuários, o custo por compra é de $2.)*

Antes de começar, [enviar um tíquete de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) para unir as seguintes dimensões à tabela de itens de linha (`sales\_flat\_order\_item, order\_item`):

* Origem do pedido (se você rastrear apenas a origem de referência no nível do usuário, então ingressar na origem do usuário)
* Campanha do pedido (se você só rastrear a fonte de referência no nível do usuário e, em seguida, ingressar na campanha do usuário)
* Meio do pedido (se você só rastrear a origem de referência no nível do usuário, associe a mídia do usuário)

**1. Agora, comece criando um gráfico que retorna a receita por campanha de produto(s) específico(s):**

1. Em qualquer painel, clique em **[!UICONTROL Add Report > Create new report]**
1. Selecione o `Revenue by items` métrica que calcula a receita no nível dos itens de linha
1. Defina o [!UICONTROL Time period] para `All-time`, e [!UICONTROL Interval] para `None`
1. No `Filter by` , adicionar `product name 'IN'` Produto `A`, Produto `B`, Produto `C`, ...&quot; e inclua todos os nomes de produtos direcionados pela sua campanha separados por vírgula (por exemplo, `product name 'IN' yellow t-shirt`, `red t-shirt, blue t-shirt`)
1. No `Group by` , adicionar `order's campaign` ou `order's utm\_campaign` as `grouping` e clique em **[!UICONTROL Add All]** na caixa
1. Este relatório mostra a receita de produtos específicos por campanhas

**2. Para calcular o ROI, combine novamente as métricas em um relatório:**

1. Em qualquer painel, clique em **[!UICONTROL Add Report > Create new report]**
1. Adicione o `Revenue by items` , siga o filtro e agrupe-o por instruções do relatório campanha para produtos específicos acima e clique em **[!UICONTROL Hide]** abaixo do valor escalar da métrica
1. Agora adicione o [!DNL AdWords Cost] métrica, seguindo o filtro e agrupe por direções do `Ad cost by campaigns` relatório que você explorou na `User acquisition campaigns` acima; em seguida, clique em **[!UICONTROL Hide]** abaixo do valor escalar da métrica
1. Com essas métricas implementadas, adicione fórmulas:
1. [!UICONTROL ROI]: Insira a fórmula `\[A\]/\[B\]`, se `\[A\]` representa `Revenue per campaign for specific product(s)` e `\[B\]` representa `Ad cost by campaigns`. Retorna a proporção de (Receita para produtos específicos) / (Custo da campanha)
1. [!UICONTROL Return]: Insira a fórmula `\[A\]-\[B\]`. Retorna a margem média feita em um usuário calculando (LTV de usuário médio) - (custo médio por aquisição)
1. (Opcional) [!UICONTROL Revenue]: Revele o `Revenue by items` para ver a receita de produtos específicos por campanhas
1. (Opcional) [!UICONTROL Cost]: Revele o `AdWords Cost` para ver o custo de campanhas

1. Nomeie o relatório e salve-o como uma tabela

**3. Repita as etapas 1 e 2 acima para cada um dos produtos ou grupos de produtos anunciados.**

## Documentação relacionada

* [Rastrear origem de referência de ordem via [!DNL Google Analytics] Comércio eletrônico](../importing-data/integrations/google-ecommerce.md)
* [Rastrear a fonte de referência do usuário no banco de dados](../analysis/google-track-user-acq.md)
* [Rastrear o dispositivo do usuário, o navegador e os dados do sistema operacional no banco de dados](../analysis/track-usr-dev-browser.md)
* [Descubra as fontes e os canais de aquisição mais valiosos](../analysis/most-value-source-channel.md)
* [Conecte seu [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [Como o [!DNL Google Analytics] A atribuição UTM funciona?](../analysis/utm-attributes.md)
* [Cinco práticas recomendadas para marcação UTM no [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
