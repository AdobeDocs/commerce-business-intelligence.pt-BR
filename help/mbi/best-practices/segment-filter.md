---
title: Dimensões de dados recomendadas para segmentação e filtragem
description: Saiba mais sobre as práticas recomendadas para segmentação e filtragem.
exl-id: 66391bce-bdeb-4e9d-8089-1c796e00d91e
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 0%

---

# Segmentação e filtragem

Uma boa segmentação é o que transforma uma estatística superficial em uma métrica de negócios que orienta as decisões.

Quer saber quem são seus clientes mais valiosos? Quais são seus canais de marketing mais valiosos? Quais de seus produtos estão evoluindo mais rápido e por quê? Para obter qualquer uma dessas respostas, você precisa começar segmentando seus dados.

Este tópico aborda segmentos críticos que geralmente são recomendados aos clientes. Também entra em detalhes sobre quais perguntas esses segmentos podem ajudar você a responder. Tecnicamente, os segmentos são colunas de dados no banco de dados. Em [!DNL Adobe Commerce Intelligence], eles são chamados de dimensões.

![Painel mostrando filtros e segmentos críticos do cliente](../../mbi/assets/mbi-critical-segments.png)


## Segmentos de usuário

Os segmentos de usuários ajudam você a entender quem são seus usuários e como eles se comportam.

* **Idade/Ano de Nascimento**: quantos anos seus usuários têm? Quantos anos têm seus usuários mais ativos? Normalmente, faz sentido agrupar os valores em intervalos para uma análise mais eficaz.
* **Gênero**: os gêneros diferentes interagem com seu site de maneira diferente?
* **Endereço**: de onde vêm seus usuários? Você deve concentrar seus esforços de marketing em uma região específica? Suas campanhas publicitárias recentes tiveram o desempenho esperado em suas regiões de destino?
* **Fonte de aquisição do cliente**\: você sabe de qual canal de marketing seus usuários vêm? Eles clicaram em um anúncio ou o encontraram por meio de uma pesquisa? [A segmentação de dados por fonte de aquisição de usuário](../data-analyst/analysis/google-track-user-acq.md) é a primeira etapa na otimização da nova aquisição de cliente. O segundo passo é gastar mais dinheiro no que funciona e matar o que não funciona.
* **Dispositivo de registro**: os usuários se registraram pelo seu aplicativo móvel ou site? iOS ou Android™? Sua base de usuários móveis é grande o suficiente para alocar mais recursos para desenvolver seu produto móvel? Se você ainda não estiver rastreando, consulte este tópico [sobre o rastreamento de dispositivo de usuário](../data-analyst/analysis/track-usr-dev-browser.md).
* **Indicado por**: quem são seus maiores influenciadores? Quantos usuários foram referenciados diretamente por outros?
* **Setor**: se você é um negócio B2B, em quais setores seus usuários trabalham? Que organizações comerciais merecem ser filiadas?
* **Respostas da pesquisa**: se você realizar pesquisas com clientes, use as respostas como segmentos para obter um nível mais profundo de criação de perfil. Você pode fazer perguntas que complementam o que já sabe sobre os usuários ou confirmar suas suposições.
* **Valor do primeiro pedido e categoria do produto**: há uma correlação entre o primeiro pedido de um usuário e os padrões de compra futuros?

## Segmentos de pedidos/eventos

Os segmentos de pedido e evento ajudam a analisar o comportamento e o engajamento do usuário ao longo do tempo.

* **[!UICONTROL Billing / Shipping Address]**: De onde vem a maioria de seus pedidos? Há uma diferença entre endereços de cobrança e de envio?
* **[!UICONTROL Status]**: quantos dos seus pedidos falharam ao serem concluídos? Qual é a proporção de pedidos pendentes nos últimos sete dias?
* **[!UICONTROL Customer acquisition source]**: além de rastrear os dados de aquisição de usuário no nível do usuário, você também pode [rastreá-los no nível de um pedido ou evento](../data-analyst/analysis/google-track-user-acq.md). Um usuário que se registrou por meio de uma fonte pode continuar acessando seu site por meio de outras fontes.
* **[!UICONTROL Device]**: o número de pedidos móveis está aumentando? Quanto da sua receita é gerada através de compras móveis? (Se você ainda não estiver rastreando este item, consulte este tópico [sobre ordem de rastreamento de dados do dispositivo](../data-analyst/analysis/track-usr-dev-browser.md).
* **[!UICONTROL Fulfillment Center]**: qual de seus centros de atendimento está gerando mais receita? Se você estiver analisando a diferença entre o horário do pedido e o horário de envio, qual centro de atendimento é mais responsivo?
* **[!UICONTROL Delivery Carrier]**: qual é a operadora mais popular? Qual transportadora tem o menor número de itens devolvidos?
* **[!UICONTROL Discount / Coupon Codes]**: suas promoções estão realmente gerando negócios extras? Quantos itens extras seus clientes compraram além do item à venda? Como os cupons afetam o valor médio de seu pedido? Qual é sua margem média sobre itens com e sem desconto?
* **[!UICONTROL Satisfaction / Rating]**: quão satisfeitos seus clientes estão com seus pedidos? É provável que seus clientes encaminhem seus negócios para você?

## Segmentos de produto

Segmentos de produtos ajudam você a tomar decisões de merchandising.

* **[!UICONTROL Merchant / Brand]**: uma marca específica está vendendo mais rápido que o resto? Quais marcas têm baixo desempenho?
* **[!UICONTROL Type / Category]**: diferentes segmentos de usuários desfrutam de diferentes tipos de produtos? Quais categorias de produtos geram negócios mais repetidos?
* **[!UICONTROL Discount / Coupon Codes]**: as promoções estão prejudicando as vendas de produtos sem desconto? Como os cupons afetam o valor percebido de seus produtos?
* **[!UICONTROL Social Activity]**: Existe uma correlação entre a repercussão gerada nas mídias sociais e a quantidade vendida para um produto?
* **[!UICONTROL Size / Variant]**: qual é a proporção de estoque de que você precisa para cada variante? Quais variantes podem ser vendidas a taxas de desconto?

Se você estiver interessado em merchandising, confira [como usar segmentos de produtos para orientar negócios repetidos](../data-analyst/analysis/most-value-source-channel.md).

## Estabelecer Perfis de Cliente

Os especialistas em segmentação podem querer ir além de fatias unidimensionais e começar a estabelecer perfis de clientes reais. Por exemplo, pessoas entre 13 e 24 anos que se registraram por meio de um dispositivo móvel colocaram em um grupo &quot;Jovem e móvel&quot;. Como o comportamento desse grupo se compara ao restante da sua base de usuários?

Esse tipo de análise é o que os profissionais de marketing das empresas Fortune 1000 fazem o dia todo. Antes do advento de plataformas de inteligência empresarial baseadas em nuvem como o [!DNL Commerce Intelligence], ele estava amplamente fora de alcance para o resto de nós. Felizmente, isso já não acontece.

## Rastreamento de novos segmentos

A primeira etapa para segmentar suas métricas pelas dimensões acima é verificar se você está rastreando esses dados no banco de dados. Se não for rastreado, reúna-se com sua equipe técnica e encontre uma maneira de começar a rastrear esses dados.

Após confirmar que os dados estão sendo rastreados em seu banco de dados, [contate a equipe de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) para enviar as dimensões para suas métricas e gráficos do [!DNL Commerce Intelligence]. Você também pode usar a ferramenta *Gerenciamento de campos* para rastrear esses campos em [!DNL Commerce Intelligence].

## Relacionados

* [Otimização do banco de dados para análise](../best-practices/opt-db-analysis.md)
