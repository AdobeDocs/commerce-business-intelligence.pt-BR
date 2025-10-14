---
title: Google Analytics e atribuição UTM
description: Saiba mais sobre o processo de atribuição de origem do Google Analytics.
exl-id: 48b8a3d3-f1ac-4d3f-8f65-db1245c9ae0a
role: Admin, Data Architect, Data Engineer, User
feature: Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# [!DNL Google Analytics] e atribuição UTM

É essencial [rastrear a fonte de aquisição do usuário](../../data-analyst/analysis/google-track-user-acq.md) para [identificar as campanhas de publicidade com melhor desempenho](../../data-analyst/analysis/most-value-source-channel.md). Este tópico explora o processo de atribuição de origem [!DNL Google Analytics]. Em outras palavras, que parte da informação é registrada quando.

## O que é atribuição?

`Attribution` trata-se de especificar uma fonte de referência de uma atividade específica. Normalmente, essas atividades são macro-conversões ou microconversões, macro sendo coisas como **compras**, micro sendo coisas como **registro, inscrição em email, comentário no blog** e assim por diante.

Idealmente, cada vez que um evento de conversão ocorre, uma fonte de referência é registrada. Mas como se determina a fonte?

A realidade é que os usuários geralmente vêm de muitas fontes antes de atingir/confirmar uma conversão micro ou macro. Por exemplo, elas podem vir ao site por meio de pesquisa orgânica, depois sair, depois vir por meio de pesquisa paga, depois sair, e depois vir diretamente ao próprio site. Essas informações de rastreamento de origem geralmente são fornecidas ao site por meio de parâmetros UTM, mas também há sistemas mais sofisticados. Para sua finalidade, concentre-se em [UTM](https://support.google.com/analytics/answer/1033867?hl=en&ref_topic=1032998).

## Como o [!DNL Google Analytics] atribui fontes de referência por meio de parâmetros UTM?

Quando os parâmetros UTM são especificados na URL, eles são analisados e colocados em um [!DNL Google Analytics] [cookie](https://en.wikipedia.org/wiki/HTTP_cookie). Se um site não tiver [!DNL Google Analytics], não há razão para ter UTMs. [!DNL Google Analytics] tem regras sobre como lida com um usuário que atinge várias URLs com UTMs durante sua vida útil (mais informações sobre isso posteriormente). Supondo que o site esteja configurado para capturar parâmetros UTM em um banco de dados externo, quando uma conversão micro ou macro ocorrer, o que estiver no cookie [!DNL Google Analytics] no momento da conversão será replicado para o banco de dados.

## Primeiro clique vs. Último clique

### Atribuição de último clique

A atribuição de último clique é o modelo de atribuição mais comum empregado por [!DNL Google Analytics]. Nesse caso, o cookie [!DNL Google Analytics] representa os parâmetros UTM da origem mais recente antes do evento de conversão, e isso é [registrado no banco de dados](../../data-analyst/analysis/google-track-user-acq.md). O cookie [!DNL Google Analytics] substituirá os parâmetros UTM anteriores somente se o usuário clicar em uma nova URL que contenha um novo conjunto de parâmetros UTM.

Por exemplo, considere um usuário que visita um site pela primeira vez por meio de [!DNL Google Analytics] *pesquisa paga*, retorna por meio de *pesquisa orgânica* e finalmente retorna ao site *diretamente* ou por meio de um *link de email* **sem parâmetros UTM** antes do evento de conversão. Neste exemplo, o cookie [!DNL Google Analytics] diz que a origem do usuário é orgânica, pois ela representa a última origem antes da conversão. O *caminho* do usuário antes desse evento de conversão final é ignorado. Se, em vez disso, o usuário visitasse o site a partir de um link de email com UTM, o cookie [!DNL Google Analytics] diria que a origem é &quot;email&quot;. Portanto, se houver parâmetros UTM existentes no cookie e o usuário entrar por meio direto, o cookie [!DNL Google Analytics] mostrará os parâmetros UTM em vez de &quot;direto&quot;.

>[!NOTE]
>
>Os [!DNL Google Analytics] parâmetros de cookie de um usuário específico são apagados quando o cookie [expira](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage) ou quando um usuário apaga os cookies no navegador.*

### Atribuição de primeiro clique

Algumas ferramentas de atribuição pagas permitem capturar a &quot;pilha de panquecas&quot; de origens no caminho de um usuário. Nessa situação, no exemplo acima, a atribuição de primeiro clique nos diria pesquisa paga. Como alternativa, alguns sites implementam seus próprios cookies que capturam uma pilha de panquecas e armazenam a primeira fonte em seu banco de dados.

## Como analisar atribuição?

O [!DNL Google Analytics] tem uma funcionalidade robusta em sua interface da Web que permite executar quatro modelos de atribuição diferentes:

1. primeiro clique
1. último clique
1. linear (divide a receita igualmente entre todas as fontes no caminho)
1. ponderado (atribuição personalizada)

Agora que você entende qual é o modelo de atribuição para cada micro ou macroconversão, a questão se torna &quot;O que você faz com a totalidade das conversões de um usuário?&quot;.  Por exemplo, verifique os UTMs registrados com base na lógica do último clique do GA:

* Registros de usuário em orgânico
* Primeira compra do usuário em pesquisa paga US$ 5,00
* Segunda compra do usuário por email US$ 50,00
* Terceira compra do usuário abaixo de orgânico $10,00

Aqui é onde você pergunta, &quot;Quanta receita eu recebi com a pesquisa paga? Do email?  Do orgânico?&quot;. Você pode dizer que as respostas são 5, 50 e 10 (seja qual for a última fonte), ou você também pode dizer que atribui toda a receita à primeira fonte (todos os 65 vão para o orgânico). Você também pode aplicar uma análise ponderada ou aplicar o modelo linear (ou seja, aproximadamente 22 cada).

## Documentação relacionada

* [Rastrear origem da referência de ordem via [!DNL Google Analytics] E-Commerce](../importing-data/integrations/google-ecommerce.md)
* [Rastrear a fonte de referência do usuário no banco de dados](../analysis/google-track-user-acq.md)
* [Rastrear o dispositivo do usuário, o navegador e os dados do sistema operacional no banco de dados](../analysis/google-track-user-acq.md)
* [Descubra as fontes e os canais de aquisição mais valiosos](../analysis/most-value-source-channel.md)
* [Conectar sua conta  [!DNL Google Adwords] &#x200B;](../importing-data/integrations/google-adwords.md)
* [Aumente o ROI em suas campanhas publicitárias](../analysis/roi-ad-camp.md)
* [Cinco práticas recomendadas para marcação UTM em  [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
