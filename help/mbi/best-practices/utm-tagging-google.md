---
title: Rastreamento UTM no Google Analytics
description: Saiba mais sobre as práticas recomendadas para rastreamento UTM (marcação) no Google Analytics.
exl-id: 70bfd855-3b3f-469b-99bc-deb8251904b7
role: Admin, Developer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
TQID: https://experienceleague.adobe.com/IX5oaIr8tbUUeA3ZrIQNUMnG8ApXMBS1hcpecqFW8kg
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: beb7a3c1-66ab-4786-b879-7621375b3c40id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 450
ht-degree: 0%

---

# Rastreamento UTM

O rastreamento de `UTM` é uma convenção de marcação para URLs que permite analisar de onde seus usuários vêm. Se você observar os URLs clicados na maioria dos emails de marketing ou anúncios em banners, verá a marcação UTM. Esses links longos terminam com coisas como `utm\_source` e `utm\_medium`.

O [!DNL Google Analytics] usa a marcação `UTM` para saber de onde vem seu tráfego. Algumas destas informações vêm do [referenciador de HTTP](https://en.wikipedia.org/wiki/HTTP_referer), mas o resto você precisa se informar com `UTM` parâmetros. Quando você vê `google adwords` ou `email marketing`, significa que esses `UTM` parâmetros estão sendo gravados a partir do clique no link original e, em seguida, armazenados nos cookies dos usuários. A partir daí, [!DNL Google Analytics] usa esses dados para [atribuir comportamentos interessantes](../data-analyst/analysis/google-track-user-acq.md) ao seu site. Entender para que esses parâmetros servem ajuda a entender como configurar e usar melhor a marcação UTM.

## Práticas recomendadas para marcação UTM

A seguir, uma lista dos cinco itens mais importantes a serem lembrados ao configurar suas URLs com a marcação `UTM`.

### &#x200B;1. Tenha como objetivo marcar cada URL que você pode controlar acessando seu site

Toda vez que você pede às pessoas para clicarem em um link, você deve configurar a marcação `UTM`. Isso inclui todos os seus links de email (seu provedor de serviços de email provavelmente tem uma maneira de marcar automaticamente seus URLs), links de anúncios, artigos de imprensa, postagens de blog.

### &#x200B;2. Use uma ferramenta para criar o URL

URLs com marcas de `UTM` podem ser complicadas. Em vez de tentar digitá-los por muito tempo, use uma ferramenta [como esta](https://support.google.com/analytics/answer/1033867?hl=en) para ajudá-lo. Isso garante que você esteja pensando em adicionar todos os parâmetros adequados ao URL e obtenha o URL para copiar e colar diretamente dele. Para gerenciar links sociais, ferramentas como o [!DNL Hootsuite] incluem a opção de adicionar parâmetros de URL personalizados a todos os seus links.

### &#x200B;3. Verifique se você diferencia maiúsculas de minúsculas nos valores de parâmetro

É importante lembrar que a marca `utm\_source=adwords` é diferente da marca `utm\_source=Adwords`. Considere tornar tudo em letras minúsculas.

### &#x200B;4. Armazene os valores de parâmetro UTM no banco de dados

Cada vez que uma transação ou evento ocorre, você deseja avaliar o desempenho de suas atividades de marketing. Você pode fazer isso lendo os valores dos parâmetros UTM do [[!DNL Google Analytics] cookie no banco de dados](../data-analyst/analysis/google-track-user-acq.md).

### &#x200B;5. Pense em como você nomeia campanhas

Para acompanhar como seus esforços de marketing estão melhorando ao longo do tempo, você precisará conhecer suas convenções de nomenclatura. Mantenha-o simples e minimize o máximo possível. Sistemas de nomenclatura complicados são mais difíceis de manter.

Depois de capturar esses dados no banco de dados, você pode avaliar o desempenho de marketing e publicidade usando análises mais sofisticadas, incluindo [Valor vitalício do cliente](../data-analyst/analysis/ess-expected-ltv.md), [Taxas de repetição de compra](../data-analyst/analysis/repurchase-behavior.md) e [Valor médio de pedido](../data-analyst/analysis/basic-analytics.md).
