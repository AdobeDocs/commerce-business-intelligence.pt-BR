---
title: Atribuição de Google Analytics e UTM
description: Saiba mais sobre o processo de atribuição de origem do Google Analytics.
exl-id: 48b8a3d3-f1ac-4d3f-8f65-db1245c9ae0a
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 0%

---

# Atribuição de Google Analytics e UTM

É fundamental para [rastrear fonte de aquisição do usuário](../../data-analyst/analysis/google-track-user-acq.md) para [identificar as campanhas publicitárias com melhor desempenho](../../data-analyst/analysis/most-value-source-channel.md). Neste tutorial, exploramos o processo de atribuição de origem do Google Analytics. Em outras palavras, quando é que a informação é registrada.

## O que é atribuição?

`Attribution` O é sobre especificar uma fonte de referência de uma atividade específica. Essas atividades são tipicamente macroconversões ou microconversões, macro sendo coisas como **compras**, micróbio sendo coisas como **registro, inscrição por email, comentário do blog,** e assim por diante.

Idealmente, sempre que um evento de conversão ocorrer, uma fonte de referência será registrada. Mas como é determinada a fonte?

A realidade é que os usuários muitas vezes vêm de várias fontes antes de acessarem/confirmarem uma micro ou macro conversão (por exemplo, eles podem vir para o site via orgânica, sair, vir por pesquisa paga, sair e vir diretamente para o próprio site). Essas informações de rastreamento da fonte geralmente são fornecidas ao site por meio de parâmetros da UTM, mas também há sistemas mais sofisticados. Para nossos propósitos, nos concentraremos em [UTM](https://support.google.com/analytics/answer/1033867?hl=en&amp;ref_topic=1032998).

## Como [!DNL Google Analytics] fontes de referência de atributo por meio de parâmetros do UTM?

Quando os parâmetros de UTM são especificados no URL, eles são analisados e colocados em um [!DNL Google Analytics] [cookie](https://en.wikipedia.org/wiki/HTTP_cookie). Se um site não tiver [!DNL Google Analytics], não adianta ter UTMs. [!DNL Google Analytics] O tem regras para lidar com um usuário que acessa vários URLs com UTMs ao longo de sua vida (mais informações sobre isso posteriormente). Supondo que o site esteja configurado para capturar parâmetros de UTM em um banco de dados externo, sempre que uma micro ou macro conversão ocorrer, o que estiver na função [!DNL Google Analytics] no momento da conversão, seria replicado para o banco de dados.

## Primeiro clique vs. Último clique

### Atribuição de último clique

A atribuição de último clique é o modelo de atribuição mais comum usado por [!DNL Google Analytics]. Nesse caso, a variável [!DNL Google Analytics] representa os parâmetros da UTM para a última fonte ou a mais recente antes do evento de conversão, e é isso que é [registrado na base de dados](../../data-analyst/analysis/google-track-user-acq.md). Observe que a variável [!DNL Google Analytics] O cookie só substitui os parâmetros da UTM anteriores se o usuário clicar em um novo URL que contenha um novo conjunto de parâmetros da UTM.

Por exemplo, considere um usuário que visita um site pela primeira vez via [!DNL Google Analytics][!DNL Google Analytics][!DNL Google Analytics] *pesquisa paga*, em seguida, retorna via *pesquisa orgânica* e finalmente volta ao *site diretamente* ou através de uma *link de email* **sem parâmetros de UTM** antes do evento de conversão. Neste exemplo, a variável [!DNL Google Analytics] diz que a fonte do usuário é orgânica, pois representa a última fonte antes da conversão. O *caminho* do usuário antes que esse evento de conversão final seja ignorado. Se, em vez disso, o usuário visitou o site a partir de um link de email com o UTM, a função [!DNL Google Analytics] o cookie diria que a fonte é &quot;email&quot;. Portanto, se houver parâmetros de UTM no cookie e o usuário entrar por meio do diretamente, a variável [!DNL Google Analytics] sempre mostrará os parâmetros da UTM em vez de &quot;direto&quot;.

>[!NOTE]
>
>Um usuário específico [!DNL Google Analytics] os parâmetros de cookie serão apagados quando o cookie [expira](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage)ou quando um usuário limpa os cookies no navegador.*)

### Atribuição de primeiro clique

Algumas ferramentas de atribuição paga permitirão capturar a &quot;pilha de panquecas&quot; de fontes no caminho de um usuário. Nessa situação, no nosso exemplo acima, a atribuição do primeiro clique nos informaria sobre a pesquisa paga. Como alternativa, uma minoria de sites implementa seus próprios cookies que capturam uma pilha de panquecas e armazenam a primeira fonte em seu banco de dados.

## Como analisar atribuição?

[!DNL Google Analytics] O tem funcionalidades mais robustas na interface da Web, que permitem executar quatro modelos de atribuição diferentes: primeiro clique, último clique, linear (divida a receita igualmente entre todas as fontes no caminho) e ponderada (atribuição personalizada).

Agora que você entende qual é o modelo de atribuição para cada micro ou macro conversão, a questão se torna o que você faz com a totalidade das conversões de um usuário?  Por exemplo, veja os UTMs registrados com base na lógica de último clique do GA:

* O usuário se registra em forma orgânica
* Primeira compra do usuário em pesquisa paga $5,00
* Segunda compra do usuário por email US$ 50,00
* Terceira compra do usuário sob orgânico de US$ 10,00

Aqui é onde você pergunta: Quanto receita eu recebi da pesquisa paga?  Do e-mail?  De orgânico?  Você poderia dizer que as respostas são 5, 50 e 10 (ou seja, qualquer que seja a última fonte), ou você também poderia dizer que atribui toda a receita à primeira fonte (ou seja, todos os 65 vão para o orgânico). Também é possível aplicar alguma análise ponderada ou o modelo linear (ou seja, aproximadamente 22 cada).

## Documentação relacionada

* [Rastrear origem de referência do pedido via [!DNL Google Analytics] Comércio eletrônico](../importing-data/integrations/google-ecommerce.md)
* [Rastrear a fonte de referência do usuário no seu banco de dados](../analysis/google-track-user-acq.md)
* [Rastrear dados do dispositivo do usuário, do navegador e do SO no seu banco de dados](../analysis/google-track-user-acq.md)
* [Descubra as fontes e os canais de aquisição mais valiosos](../analysis/most-value-source-channel.md)
* [Conecte seu [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [Aumente o ROI em suas campanhas publicitárias](../analysis/roi-ad-camp.md)
* [5 prática recomendada para marcação de UTM no [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
