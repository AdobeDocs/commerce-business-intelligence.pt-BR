---
title: Dimension recomendados para segmentação e filtragem
description: Saiba mais sobre as práticas recomendadas para segmentação e filtragem.
exl-id: 66391bce-bdeb-4e9d-8089-1c796e00d91e
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 0%

---

# Segmentação e filtragem

Uma boa segmentação é o que transforma uma estatística superficial em uma métrica de negócios que orienta as decisões.

Quer saber quem são seus clientes mais valiosos? Quais são seus canais de marketing mais valiosos? Quais de seus produtos estão evoluindo mais rápido e por quê? Para obter qualquer uma dessas respostas, você precisa começar segmentando seus dados.

Este tópico aborda segmentos críticos que geralmente são recomendados aos clientes. Também entra em detalhes sobre quais perguntas esses segmentos podem ajudar você a responder. Tecnicamente, os segmentos são colunas de dados no banco de dados. Entrada [!DNL Adobe Commerce Intelligence], eles são chamados de dimensões.

![](../../mbi/assets/mbi-critical-segments.png)


## Segmentos de usuário

Os segmentos de usuários ajudam você a entender quem são seus usuários e como eles se comportam.

* **Idade / Ano de Nascimento**: Quantos anos seus usuários têm? Quantos anos têm seus usuários mais ativos? Normalmente, faz sentido agrupar os valores em intervalos para uma análise mais eficaz.
* **Sexo**: Gêneros diferentes se envolvem com seu site de forma diferente?
* **Endereço**: De onde vêm seus usuários? Você deve concentrar seus esforços de marketing em uma região específica? Suas campanhas publicitárias recentes tiveram o desempenho esperado em suas regiões de destino?
* **Fonte de aquisição do cliente**\: Você sabe de qual canal de marketing seus usuários vêm? Eles clicaram em um anúncio ou o encontraram por meio de uma pesquisa? [Segmentação de dados por fonte de aquisição de usuário](../data-analyst/analysis/google-track-user-acq.md) O é o primeiro passo para otimizar a aquisição de um novo cliente. O segundo passo é gastar mais dinheiro no que funciona e matar o que não funciona.
* **Dispositivo de registro**: os usuários se registraram por meio do aplicativo móvel ou do site? iOS ou Android™? Sua base de usuários móveis é grande o suficiente para alocar mais recursos para desenvolver seu produto móvel? Se você ainda não estiver rastreando, consulte este tópico [sobre o dispositivo de rastreamento de usuário](../data-analyst/analysis/track-usr-dev-browser.md).
* **Referenciado por**: quem são seus principais influenciadores? Quantos usuários foram referenciados diretamente por outros?
* **Setor**: se você for um negócio B2B, em quais setores seus usuários trabalham? Que organizações comerciais merecem ser filiadas?
* **Respostas da pesquisa**: se você realizar pesquisas com os clientes, use as respostas como segmentos para obter um nível mais profundo de criação de perfil. Você pode fazer perguntas que complementam o que já sabe sobre os usuários ou confirmar suas suposições.
* **Valor do primeiro pedido e categoria do produto**: há uma correlação entre o primeiro pedido de um usuário e os padrões de compra futuros?

## Segmentos de pedidos/eventos

Os segmentos de pedido e evento ajudam a analisar o comportamento e o engajamento do usuário ao longo do tempo.

* **[!UICONTROL Billing / Shipping Address]**: De onde vem a maioria de seus pedidos? Há uma diferença entre endereços de cobrança e de envio?
* **[!UICONTROL Status]**: quantos dos seus pedidos falharam ao serem concluídos? Qual é a proporção de pedidos pendentes nos últimos sete dias?
* **[!UICONTROL Customer acquisition source]**: além de rastrear os dados de aquisição de usuários no nível do usuário, você também pode [rastrear em um nível de pedido ou evento](../data-analyst/analysis/google-track-user-acq.md). Um usuário que se registrou por meio de uma fonte pode continuar acessando seu site por meio de outras fontes.
* **[!UICONTROL Device]**: o número de pedidos de celular está aumentando? Quanto da sua receita é gerada através de compras móveis? (Se você ainda não estiver rastreando isso, consulte este tópico [sobre dados do dispositivo de ordem de rastreamento](../data-analyst/analysis/track-usr-dev-browser.md).
* **[!UICONTROL Fulfillment Center]**: qual dos seus centros de atendimento está gerando mais receita? Se você estiver analisando a diferença entre o horário do pedido e o horário de envio, qual centro de atendimento é mais responsivo?
* **[!UICONTROL Delivery Carrier]**: qual é a operadora mais popular? Qual transportadora tem o menor número de itens devolvidos?
* **[!UICONTROL Discount / Coupon Codes]**: suas promoções estão realmente gerando negócios extras? Quantos itens extras seus clientes compraram além do item à venda? Como os cupons afetam o valor médio de seu pedido? Qual é sua margem média sobre itens com e sem desconto?
* **[!UICONTROL Satisfaction / Rating]**: quão satisfeitos seus clientes estão com seus pedidos? É provável que seus clientes encaminhem seus negócios para você?

## Segmentos de produto

Segmentos de produtos ajudam você a tomar decisões de merchandising.

* **[!UICONTROL Merchant / Brand]**: uma marca específica está vendendo mais rápido do que as outras? Quais marcas têm baixo desempenho?
* **[!UICONTROL Type / Category]**: diferentes segmentos de usuários desfrutam de diferentes tipos de produtos? Quais categorias de produtos geram negócios mais repetidos?
* **[!UICONTROL Discount / Coupon Codes]**: as promoções estão prejudicando as vendas de produtos sem desconto? Como os cupons afetam o valor percebido de seus produtos?
* **[!UICONTROL Social Activity]**: Há uma correlação entre o burburinho gerado nas mídias sociais e a quantidade vendida para um produto?
* **[!UICONTROL Size / Variant]**: qual é a proporção do inventário de que você precisa para cada variante? Quais variantes podem ser vendidas a taxas de desconto?

Se você estiver interessado em merchandising, confira [como usar segmentos de produtos para orientar negócios repetidos](../data-analyst/analysis/most-value-source-channel.md).

## Estabelecer Perfis de Cliente

Os especialistas em segmentação podem querer ir além de fatias unidimensionais e começar a estabelecer perfis de clientes reais. Por exemplo, pessoas entre 13 e 24 anos que se registraram por meio de um dispositivo móvel colocaram em um grupo &quot;Jovem e móvel&quot;. Como o comportamento desse grupo se compara ao restante da sua base de usuários?

Esse tipo de análise é o que os profissionais de marketing das empresas Fortune 1000 fazem o dia todo. Antes do advento de plataformas de business intelligence baseadas em nuvem, como [!DNL Commerce Intelligence]No entanto, estava em grande parte fora do alcance para o resto de nós. Felizmente, isso já não acontece.

## Rastreamento de novos segmentos

A primeira etapa para segmentar suas métricas pelas dimensões acima é verificar se você está rastreando esses dados no banco de dados. Se não for rastreado, reúna-se com sua equipe técnica e encontre uma maneira de começar a rastrear esses dados.

Depois de confirmar que os dados são rastreados no banco de dados, [entre em contato com a equipe de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) para encaminhar as dimensões ao seu [!DNL Commerce Intelligence] métricas e gráficos. Você também pode usar a variável *Gerenciamento de campo* ferramenta para rastrear esses campos em [!DNL Commerce Intelligence].

## Relacionados

* [Otimização do banco de dados para análise](../best-practices/opt-db-analysis.md)
