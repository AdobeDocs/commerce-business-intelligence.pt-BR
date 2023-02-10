---
title: Dimension de dados recomendados para segmentação e filtragem
description: Saiba mais sobre as práticas recomendadas para segmentação e filtragem.
exl-id: 66391bce-bdeb-4e9d-8089-1c796e00d91e
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---

# Segmentação e filtragem

Uma boa segmentação é o que transforma uma estatística superficial em uma métrica de negócios que orienta as decisões.

Quer saber quem são seus clientes mais valiosos? Quais são seus canais de marketing mais valiosos? Quais de seus produtos estão se movendo mais rápido e por quê? Para chegar a qualquer uma dessas respostas, você precisa começar por segmentar seus dados.

Neste artigo, compartilhamos alguns segmentos críticos que geralmente recomendamos para nossos clientes. Também detalhamos as perguntas que esses segmentos podem ajudar a responder. Tecnicamente, os segmentos são colunas de dados no seu banco de dados. Em [!DNL MBI], chamamos-lhes dimensões.

![](../../mbi/assets/mbi-critical-segments.png)


## Segmentos do usuário

Os segmentos de usuários ajudam você a entender quem são seus usuários e como eles se comportam.

* **Idade/Ano de Nascimento**: Quantos anos seus usuários têm? Quantos anos seus usuários mais ativos têm? Geralmente faz sentido agrupar os valores em intervalos para uma análise mais eficaz.
* **Gênero**: Os homens e mulheres se envolvem com seu site de maneira diferente?
* **Endereço**: De onde vêm seus usuários? Você deve concentrar seus esforços de marketing em uma região específica? Suas campanhas publicitárias recentes tiveram o desempenho esperado em suas regiões de destino?
* **Fonte de aquisição do cliente**\: Você sabe de que canal de marketing seus usuários vêm? Eles clicaram em um anúncio ou o encontraram por meio de pesquisa? [Segmentação de dados por fonte de aquisição de usuário](../data-analyst/analysis/google-track-user-acq.md) é a primeira etapa na otimização da aquisição do novo cliente. O segundo passo é gastar mais dinheiro no que está a funcionar e matar o que não está.
* **Dispositivo de registro**: Os usuários se registraram no seu aplicativo móvel ou site? iOS ou Android? Sua base de usuários móveis é grande o suficiente para alocar mais recursos para desenvolver seu produto móvel? (Se você ainda não estiver rastreando isso, consulte este tópico [sobre o dispositivo do usuário de rastreamento](../data-analyst/analysis/track-usr-dev-browser.md).
* **Referenciado por**: Quem são seus principais influenciadores? Quantos usuários foram referenciados diretamente por outros?
* **Setor**: Se você for uma empresa B2B, em quais setores seus usuários trabalham? Que organizações profissionais vale a pena aderir?
* **Respostas da pesquisa**: Se você realizar pesquisas de clientes, use as respostas como segmentos para obter um nível mais profundo de criação de perfis. Você pode fazer perguntas que complementam o que já sabe sobre seus usuários ou confirmar suas suposições.
* **Valor do primeiro pedido e categoria do produto**: Existe uma correlação entre o primeiro pedido de um usuário e os padrões de compra futuros?

## Segmentos de pedidos/eventos

Os segmentos de pedido e evento ajudam a analisar o comportamento e o envolvimento do usuário ao longo do tempo.

* **[!UICONTROL Billing / Shipping Address]**: De onde vem a maioria de seus pedidos? Existe uma diferença entre endereços de faturamento e de envio?
* **[!UICONTROL Status]**: Quantos de seus pedidos falharam ao serem concluídos? Qual é a proporção de pedidos pendentes nos últimos sete dias?
* **[!UICONTROL Customer acquisition source]**: Além de rastrear os dados de aquisição do usuário em um nível de usuário, você também pode [rastreá-lo em um nível de pedido ou evento](../data-analyst/analysis/google-track-user-acq.md). Um usuário que se registrou por meio de uma fonte pode muito bem continuar a acessar seu site por meio de outras fontes.
* **[!UICONTROL Device]**: O número de pedidos móveis está aumentando? Qual é a receita gerada atualmente pelas compras de dispositivos móveis? (Se você ainda não estiver rastreando isso, consulte este tópico [sobre os dados do dispositivo de ordem de rastreamento](../data-analyst/analysis/track-usr-dev-browser.md).
* **[!UICONTROL Fulfillment Center]**: Qual de seus centros de atendimento está gerando mais receita? Se você estiver analisando a diferença entre o tempo do pedido e o tempo de envio, qual centro de atendimento é mais responsivo?
* **[!UICONTROL Delivery Carrier]**: Qual é o carro mais popular? Qual operadora tem o menor número de itens retornados?
* **[!UICONTROL Discount / Coupon Codes]**: Suas promoções estão gerando negócios adicionais? Quantos itens extras seus clientes compraram além do item à venda? Como os cupons afetam seu valor médio de pedido? Qual é a sua margem média em itens com desconto ou sem desconto?
* **[!UICONTROL Satisfaction / Rating]**: Quão satisfeitos estão seus clientes com seus pedidos? Seus clientes têm probabilidade de encaminhar seus negócios para você?

## Segmentos do produto

Os segmentos de produto ajudam você a tomar decisões de comercialização.

* **[!UICONTROL Merchant / Brand]**: Uma marca específica está vendendo mais rápido que a restante? Quais marcas estão com baixo desempenho?
* **[!UICONTROL Type / Category]**: Segmentos de usuários diferentes desfrutam de diferentes tipos de produtos? Quais categorias de produtos geram os negócios mais repetidos?
* **[!UICONTROL Discount / Coupon Codes]**: As promoções estão prejudicando as vendas de produtos não descontados? Como os cupons afetam o valor percebido de seus produtos?
* **[!UICONTROL Social Activity]**: Existe uma correlação entre o burburinho gerado nas redes sociais e a quantidade vendida por um produto?
* **[!UICONTROL Size / Variant]**: Qual é a proporção de inventário que você precisa de cada variante? Quais variantes podem ser vendidas a taxas de desconto?

Se você estiver interessado em merchandising, confira uma postagem no blog onde exploramos [como usar segmentos de produtos para impulsionar negócios repetidos](../data-analyst/analysis/most-value-source-channel.md).

## Estabeleça perfis do cliente

Os especialistas em segmentação podem querer ir além de fatias unidimensionais e começar a estabelecer perfis de clientes reais. Por exemplo, pessoas entre 13 e 24 anos que se registraram por meio de um dispositivo móvel colocaram em um grupo &quot;Jovem &amp; móvel&quot;. Como o comportamento desse grupo se compara ao resto da base de usuários?

Esse tipo de análise é o que os profissionais de marketing das empresas Fortune 1000 fazem o dia todo. Antes do advento de plataformas de inteligência empresarial baseadas em nuvem como [!DNL MBI]Mas estava em grande parte fora do alcance do resto de nós. Felizmente, já não é esse o caso.

## Rastreamento de novos segmentos

A primeira etapa para segmentar suas métricas pelas dimensões acima é garantir que você esteja rastreando esses dados no banco de dados. Se não for rastreado, entre em contato com a equipe técnica e encontre uma maneira de começar a rastrear esses dados.

Depois de confirmar que os dados são rastreados no banco de dados, [entre em contato com nossa equipe de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) para enviar as dimensões para a [!DNL MBI] métricas e gráficos, ou use a ferramenta de gerenciamento de campo para rastrear esses campos em [!DNL MBI].

## Relacionado

* [Otimização do banco de dados para análise](../best-practices/opt-db-analysis.md)
