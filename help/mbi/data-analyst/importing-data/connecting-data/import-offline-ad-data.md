---
title: Importar dados de gastos com outros anúncios
description: Saiba como importar dados offline ou de outros gastos com anúncios para o [!DNL MBI].
exl-id: 6f12a397-0927-4e87-95ff-3a55ccc9e14b
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Importar dados de gastos com outros anúncios

O upload dos dados de gastos com publicidade permitirá medir o ROI da campanha, casando-se com o custo de publicidade e o cliente `lifetime value (CLV)` de usuários adquiridos em suas campanhas.

## Upload de dados de custo de publicidade

A primeira etapa na análise de dados de e gasto é obter os dados. Como a maioria das plataformas de publicidade permite exportar relatórios, recomendamos que você exporte os dados brutos de sua plataforma de publicidade e faça o upload diretamente para o [!DNL MBI] sem qualquer manipulação. Você pode executar operações nos dados do data warehouse, de modo que não há necessidade de duplicar seus esforços.

Depois de exportar os dados de gastos com anúncios, use a [`File Upload` recurso](../connecting-data/using-file-uploader.md) para trazer os dados para o data warehouse. Você pode fazer upload de novos dados para o mesmo [!DNL MBI] tabela ao longo do tempo.

## Fontes offline

Além de suas campanhas online, você também pode ter anúncios offline, como no rádio ou em um outdoor. Para contabilizar esses casos, é possível fazer upload manual de uma planilha com os dados de custo para o [!DNL MBI].

A estrutura de tabela explorada abaixo é recomendada ao criar um `.csv` para registrar os dados de gastos com anúncios. Um arquivo de modelo também é anexado na parte inferior deste artigo para servir como exemplo. As colunas recomendadas são:

* `ID` - Esse é um identificador exclusivo para cada linha de dados usada pelo banco de dados como chave primária. Deve ser diferente para cada linha.
* `Date` - Esta é a data de execução da campanha, em formato aaaa-mm-dd.
* `Amount` - Esse é o valor que você gastou com a campanha.
* `campaign` - Este é o nome da campanha. Se estiver usando [!DNL Google Analytics] para rastrear seus outros dados de gastos com publicidade, eles devem corresponder ao nome utm\_campaign.
* `source` - Esse é o nome de origem. Se estiver usando [!DNL Google Analytics], deve corresponder ao valor da variável `utm_source` nome.
* `other` (Opcional) - Também é possível incorporar colunas adicionais que ajudarão a segmentar campanhas e custos. Também pode ser uma maneira de resumir vários nomes diferentes de campanha da UTM em uma campanha única e coerente para fins de rastreamento. Em vez de configurá-lo manualmente, pode ser bom usar a Pesquisa V para uma segunda planilha para corresponder cada Nome da Campanha ao Outro Nome e relatá-lo dinamicamente aqui.

## Relacionado

* [Connect [!DNL AdWords] dados](../integrations/google-adwords.md)
* [Aumente o ROI em campanhas publicitárias](../../analysis/roi-ad-camp.md)
