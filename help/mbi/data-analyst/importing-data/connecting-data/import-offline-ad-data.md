---
title: Importar outros dados de gastos com anúncios
description: Saiba como importar dados offline ou outros dados de gastos com anúncios para o [!DNL MBI].
exl-id: 6f12a397-0927-4e87-95ff-3a55ccc9e14b
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Importar outros dados de gastos com anúncios

Fazer upload dos seus dados de gastos com publicidade permite medir o ROI da campanha ao unir os custos com publicidade e o cliente `lifetime value (CLV)` de usuários adquiridos de suas campanhas.

## Upload de dados de custo de publicidade

A primeira etapa na análise de dados de gastos com anúncios é obter os dados. Como a maioria das plataformas de publicidade permite exportar relatórios, a Adobe recomenda exportar os dados brutos da sua plataforma de anúncios e carregá-los diretamente no [!DNL MBI] sem qualquer manipulação. Você pode executar operações nos dados em sua Data Warehouse, de modo que não há necessidade de duplicar seus esforços.

Após exportar os dados de gastos com anúncios, use o [`File Upload` recurso](../connecting-data/using-file-uploader.md) para trazer os dados para a Data Warehouse. Você pode fazer upload de novos dados para a mesma [!DNL MBI] tabela ao longo do tempo.

## Fontes offline

Além de suas campanhas online, você também pode ter anúncios offline, como no rádio ou em um outdoor. Para levar em conta esses casos, você pode carregar manualmente uma planilha com os dados de custo para [!DNL MBI].

A estrutura da tabela explorada abaixo é recomendada ao criar uma `.csv` arquivo para registrar e gastar dados. Um arquivo de modelo também é anexado na parte inferior deste artigo para servir de exemplo. As colunas recomendadas são:

* `ID` - É um identificador exclusivo para cada linha de dados usada pelo banco de dados como chave primária. Deve ser diferente para cada linha.
* `Date` - Essa é a data em que a campanha foi executada, no formato aaaa-mm-dd.
* `Amount` - Esse é o valor que você gastou na campanha.
* `campaign` - Este é o nome da campanha. Se você estiver usando [!DNL Google Analytics] para acompanhar seus outros dados de gastos com anúncios, ele deve corresponder ao nome utm\_campaign.
* `source` - Este é o nome de origem. Se você estiver usando [!DNL Google Analytics], isso deve corresponder ao `utm_source` nome.
* `other` (Opcional) - Você também pode incorporar colunas adicionais que ajudam a segmentar campanhas e custos. Também pode ser uma maneira de resumir vários nomes de campanha UTM diferentes em uma única campanha coerente para fins de rastreamento. Em vez de configurar isso manualmente, pode ser bom usar um V-Lookup para uma segunda planilha para corresponder cada Nome de campanha ao Outro nome e relatá-lo aqui dinamicamente.

## Relacionados

* [Conectar [!DNL AdWords] dados](../integrations/google-adwords.md)
* [Aumente o ROI em campanhas publicitárias](../../analysis/roi-ad-camp.md)
