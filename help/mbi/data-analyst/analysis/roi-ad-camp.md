---
title: Aumento do ROI em suas campanhas de publicidade
description: Saiba mais sobre alguns métodos diferentes de avaliação do desempenho de sua campanha.
exl-id: 4f2bf408-eeaf-4dbf-b62e-89426734640a
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '1294'
ht-degree: 0%

---

# Campanhas publicitárias e ROI

A MBI permite [dados de custo e receita de publicidade em casamento](../../data-analyst/importing-data/integrations/google-adwords.md) do seu banco de dados. Isso ajudará a identificar quais campanhas têm o ROI mais alto. Neste artigo, exploramos alguns métodos diferentes de avaliação do desempenho de sua campanha.

## Pré-requisitos

* Importe os dados de custo de publicidade:
   * [Conecte seu [!DNL Google AdWords] para [!DNL MBI]](../importing-data/integrations/google-adwords.md): Isso sincronizará automaticamente o [!DNL Adwords] gastar em [!DNL MBI]
   * [Fazer upload de outros dados de custo de publicidade](../importing-data/connecting-data/import-offline-ad-data.md): Isso é recomendado para canais sem um conector direto para [!DNL MBI]
   * Se você importar dados de custo de várias fontes, podemos [consolidar](../../best-practices/consolidating-your-tables.md) os dados em [!DNL MBI]. Simplesmente [enviar um tíquete de suporte](../../guide-overview.md).
* [Rastrear dados do canal de aquisição do usuário](../analysis/google-track-user-acq.md)

## Campanhas de aquisição do usuário

As campanhas direcionadas para a aquisição do usuário podem ser medidas sob diversas perspectivas, incluindo:

1. O número de novos usuários adquiridos de campanhas
1. A taxa de conversão do registro para a compra de campanhas
1. O ROI das campanhas com base no valor médio de vida do usuário (LTV)

As análises (1) e (2) acima são exploradas em um tutorial separado em [identificação dos principais canais de marketing](../analysis/most-value-source-channel.md). Aqui, exploramos a análise (3) para medir o ROI da campanha ao longo do tempo. Isso responderá se os usuários adquiridos de uma campanha específica geraram receita vitalícia suficiente para cobrir o custo de aquisição.

>[!NOTE]
>
>Partiremos do pressuposto de que todos os custos de campanha foram exclusivamente utilizados para adquirir novos utilizadores. Na realidade, o custo da campanha também é compartilhado com a aquisição de visitas não convertidas, compradores repetidos e assim por diante. No entanto, assumindo que todo o custo é usado para adquirir novos usuários registrados, o ROI resultante contabilizará o pior cenário (custo por aquisição mais alto), para que você possa ter certeza de que o ROI real é maior do que nosso cálculo.
>
>Exemplo: Supondo que você gastou $20 em uma campanha que gerou 10 novos usuários e 10 compradores repetidos, seu custo real por novo usuário é $1, mas sob nossa suposição de que todo o custo foi para a aquisição de novos usuários, o custo por aquisição é $2.)

**1. Comece criando um gráfico que segmenta o custo de publicidade por campanhas:**

1. Crie um [!UICONTROL Metric] que resume seu gasto ao longo do tempo
1. Ir para [!UICONTROL Data > Metrics]
1. Selecionar `Add New Metric` e selecione o [!DNL `Adwords...`] tabela que está registrando seu [!DNL AdWords] dados de custo.
1. No editor de métricas, dê um nome à sua métrica (por exemplo, [!UICONTROL AdWord Cost])
1. Usando os detalhamentos, execute uma **Soma** no `adCost` na coluna [!DNL Adwords...] tabela (Alteração) ordenada pela `date` coluna.
   ![](../../assets/success-add-new-metric.png)<!--="500" height="303"}-->
1. já terminámos. Clique em `Back to Metric List` na parte superior e vá para qualquer painel.

1. Criar um relatório que os segmentos gastam por campanhas
1. Em qualquer painel, clique em [!UICONTROL Add Report > Create new report]
1. Selecione o [!UICONTROL Adword Cost] métrica que acabamos de criar
1. Defina as [!UICONTROL Time period] para `All-time`e [!UICONTROL Interval] para `None`
1. Em `Group by` guia , adicionar `campaign` as [!UICONTROL grouping field]e clique em `Add All` na caixa .
1. Este relatório mostrará o tempo todo [!DNL AdWords] custo por campanhas

**2. Em seguida, criaremos um relatório que conta novos usuários por campanhas:**

1. Em qualquer painel, clique em **[!UICONTROL Add Report > Create new report]**
1. Selecione o `New users` métrica que conta o número de novos usuários registrados ao longo do tempo
1. Defina as [!UICONTROL Time period] para `All-time`e [!UICONTROL Interval] para `None`
1. Em `Group by` guia , adicionar `campaign` as `grouping field`e clique em **`Add All`** na caixa
1. Este relatório mostrará seus usuários registrados por campanhas

**3. Vamos criar um relatório que segmente o LTV do usuário médio por campanhas:**

1. Em qualquer painel, clique em **[!UICONTROL Add Report > Create new report]**
1. Selecione o `Average lifetime revenue` métrica que calcula a receita média do ciclo de vida de um usuário
1. Defina as [!UICONTROL Time period] para `All-time`e [!UICONTROL Interval] para `None`
1. Em `Group by` guia , adicionar `campaign` ou `utm\_campaign` as [!UICONTROL grouping field]e clique em `Add All` na caixa
1. Este relatório mostrará a receita média do ciclo de vida do usuário por campanhas

**Por fim, calcularemos o ROI da campanha reunindo essas três análises em um relatório:**

1. Em qualquer painel, clique em **[!UICONTROL Add Report > Create new report]**
1. Adicionar como entrada usaremos as três métricas usadas acima. Cada um receberá uma carta (por exemplo,\[`A`\], \[`B`\] e \[`C`\])
1. [!UICONTROL Cost]: Adicione a métrica Custo do AdWords - será a variável \[A\]. Isso simplesmente retornará o custo por campanhas.
1. [!UICONTROL Users]: Adicione a métrica Novos usuários - esta será a variável \[B\]. Isso simplesmente retornará o número de usuários por campanhas.
1. [!UICONTROL LTV]: Adicione a métrica Receita média de duração - essa será a variável \[`C`\]. Isso simplesmente retornará o LTV por campanhas.

1. Clique no ícone de ocultação ao lado da palavra Gráfico para que você possa se concentrar na tabela
1. Agora vamos usar `Add Formula` para combinar essas métricas, da seguinte maneira:
1. [!UICONTROL ROI]: Informe a fórmula `(\[C\]-\[A\]/\[B\])/(\[A\]/\[B\])`, se \[`A`\] representa `Ad Cost by Campaigns`, \[`B`\] representa `New users by campaigns`e \[`C`\] `LTV by campaigns`. Isso retornará a proporção de (custo médio do usuário LTV - custo médio por aquisição) / (custo médio por aquisição)
1. [!UICONTROL Avg Return per User]: Informe a fórmula **\[`C`\]-(\[`A`\]/\[`B`\])**. Isso retornará a margem média feita em um usuário calculando (usuário médio LTV) - (custo médio por aquisição).
1. [!UICONTROL CPA]: Informe a fórmula **`\[A\]/\[B\]`**. Isso retornará o custo real da campanha por aquisição.
1. Outras métricas em potencial para incluir no [!DNL AdWords] os dados incluem somas de  `Impressions` e `adClicks` de [!DNL AdWords] dados), juntamente com o total `number of orders` feito por meio de uma campanha específica.
1. Também pode ser interessante calcular o ROI baseado na LTV 30 dias e 90 dias depois que um usuário se registra ou faz uma primeira compra.

1. Você pode clicar e arrastar suas métricas e fórmulas para reorganizar as colunas de seu relatório
1. Dê um nome ao seu relatório e certifique-se de salvar como uma tabela.

## Campanhas do produto

Você está executando anúncios específicos do produto? Em caso positivo, é possível medir o ROI nessas campanhas, calculando a receita/o custo de produtos específicos.

>[!NOTE]
>
>Partimos do princípio de que todos os custos de campanha foram exclusivamente utilizados para gerar compras de produtos específicos. Ao assumir que todo o custo foi gasto na geração de compras, o ROI resultante contabilizará o pior cenário (custo por compra mais alto), para que você possa ter certeza de que o ROI real é maior que esse cálculo. Exemplo: Supondo que você gastou $20 em uma campanha que gerou 10 novos usuários e 10 compras, seu custo real por compra é de $1, mas sob nossa suposição de que todo o custo foi para a aquisição de novos usuários, o custo por compra é de $2.)*

Antes de começarmos, [enviar um tíquete de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) para unir as seguintes dimensões à tabela de itens de linha (`sales\_flat\_order\_item, order\_item`):

* Origem do pedido (se você rastrear somente a origem de referência no nível do usuário, associe-se à origem do usuário)
* Campanha do pedido (se você só rastrear a fonte de referência no nível do usuário, participe da campanha do usuário)
* Meio do pedido (se você rastrear apenas a origem da referência no nível do usuário, participe da mídia do usuário)

**1. Agora comece criando um gráfico que retorna receita por campanha para produtos específicos:**

1. Em qualquer painel, clique em **[!UICONTROL Add Report > Create new report]**
1. Selecione o `Revenue by items` métrica que calcula a receita no nível de itens de linha
1. Defina as [!UICONTROL Time period] para `All-time`e [!UICONTROL Interval] para `None`
1. Em `Filter by` guia , adicionar `product name 'IN'` Produto `A`, Produto `B`, Produto `C`, ...&quot; e incluir todos os nomes de produtos direcionados por sua campanha separados por vírgula (por exemplo, `product name 'IN' yellow t-shirt`, `red t-shirt, blue t-shirt`)
1. Em `Group by` guia , adicionar `order's campaign` ou `order's utm\_campaign` as `grouping` e clique em **[!UICONTROL Add All]** na caixa
1. Este relatório mostrará a receita de produtos específicos por campanhas

**2. Para calcular o ROI, vamos combinar novamente as métricas em um relatório:**

1. Em qualquer painel, clique em **[!UICONTROL Add Report > Create new report]**
1. Adicione o `Revenue by items` , seguindo o filtro e agrupe por orientações do relatório de campanha para produtos específicos acima e clique em **[!UICONTROL Hide]** abaixo do valor escalar da métrica
1. Agora adicione o [!DNL AdWords Cost] , seguindo o filtro e agrupe por orientações da `Ad cost by campaigns` relatório explorado na `User acquisition campaigns` seção acima; em seguida, clique em **[!UICONTROL Hide]** abaixo do valor escalar da métrica
1. Com essas métricas em vigor, agora adicionaremos fórmulas:
1. [!UICONTROL ROI]: Informe a fórmula `\[A\]/\[B\]`, se `\[A\]` representa `Revenue per campaign for specific product(s)` e `\[B\]` representa `Ad cost by campaigns`. Isso retornará a proporção de (Receita de produtos específicos) / (Custo da campanha)
1. [!UICONTROL Return]: Informe a fórmula `\[A\]-\[B\]`. Isso retornará a margem média feita em um usuário calculando (usuário médio LTV) - (custo médio por aquisição)
1. (Opcional) [!UICONTROL Revenue]: Mostrar o `Revenue by items` métrica para visualizar a receita de produtos específicos por campanhas
1. (Opcional) [!UICONTROL Cost]: Mostrar o `AdWords Cost` para visualizar o custo de campanhas

1. Dê um nome ao seu relatório e certifique-se de salvá-lo como uma tabela

**3. Repita as etapas 1 e 2 acima para cada produto(s) ou grupo(s) de produtos anunciados.**

## Documentação relacionada

* [Rastrear origem de referência do pedido via [!DNL Google Analytics] Comércio eletrônico](../importing-data/integrations/google-ecommerce.md)
* [Rastrear a fonte de referência do usuário no seu banco de dados](../analysis/google-track-user-acq.md)
* [Rastrear dados do dispositivo do usuário, do navegador e do SO no seu banco de dados](../analysis/track-usr-dev-browser.md)
* [Descubra as fontes e os canais de aquisição mais valiosos](../analysis/most-value-source-channel.md)
* [Conecte seu [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [Como [!DNL Google Analytics] A atribuição de UTM funciona?](../analysis/utm-attributes.md)
* [5 prática recomendada para marcação de UTM no [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
