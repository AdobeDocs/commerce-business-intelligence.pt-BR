---
title: Rastreamento UTM no Google Analytics
description: Saiba mais sobre as práticas recomendadas para rastreamento UTM (marcação) no Google Analytics.
exl-id: 70bfd855-3b3f-469b-99bc-deb8251904b7
source-git-commit: 8d4e71363edad0613cc0ab277c2a43aad000965e
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# Rastreamento UTM

`UTM` O rastreamento do é uma convenção de marcação para URLs que permite analisar de onde seus usuários vêm. Se você observar os URLs clicados na maioria dos emails de marketing ou anúncios em banners, verá a marcação UTM. São esses links longos que terminam com coisas como `utm\_source` e `utm\_medium`.

[!DNL Google Analytics] usos `UTM` marcando para saber de onde seu tráfego vem. Algumas dessas informações vêm do [Referenciador de HTTP](https://en.wikipedia.org/wiki/HTTP_referer) mas o resto você tem que se abastecer de `UTM` parâmetros. Quando você vê `google adwords` ou `email marketing`, isto é, aqueles `UTM` parâmetros que estão sendo gravados a partir do link original, clique em e, em seguida, armazenado nos cookies dos usuários. A partir daí, [!DNL Google Analytics] O usa esses dados para [atribuir comportamentos interessantes](../data-analyst/analysis/google-track-user-acq.md) no seu site. Entender para que esses parâmetros servem ajuda a entender como configurar e usar melhor a marcação UTM.

## Práticas recomendadas para marcação UTM

A seguir, uma lista das cinco coisas mais importantes a serem lembradas ao configurar seus URLs com o `UTM` marcação.

### 1. Tenha como objetivo marcar cada URL que você pode controlar acessando seu site

Toda vez que você pede às pessoas para clicarem em um link, você deve estar configurando `UTM` marcação. Isso inclui todos os seus links de email (seu provedor de serviços de email provavelmente tem uma maneira de marcar automaticamente seus URLs), links de anúncios, artigos de imprensa, postagens de blog.

### 2. Use uma ferramenta para criar o URL

`UTM`URLs com tags do podem ser complicados. Em vez de tentar digitá-los por muito tempo, use uma ferramenta [curtir](https://support.google.com/analytics/answer/1033867?hl=en) para ajudá-lo. Isso garante que você esteja pensando em adicionar todos os parâmetros adequados ao URL e obtenha o URL para copiar e colar diretamente dele. Para gerenciar links sociais, ferramentas como [!DNL Hootsuite] inclua a opção de adicionar parâmetros de URL personalizados a todos os links.

### 3. Verifique se você diferencia maiúsculas de minúsculas nos valores de parâmetro

É importante lembrar que a tag `utm\_source=adwords` é uma tag diferente de `utm\_source=Adwords`. Considere tornar tudo em letras minúsculas.

### 4. Armazene os valores de parâmetro UTM no banco de dados

Cada vez que uma transação ou evento ocorre, você deseja avaliar o desempenho de suas atividades de marketing. Você pode fazer isso lendo os valores dos valores dos parâmetros UTM na [[!DNL Google Analytics] cookie no banco de dados](../data-analyst/analysis/google-track-user-acq.md).

### 5. Pense em como você nomeia campanhas

Para acompanhar como seus esforços de marketing estão melhorando ao longo do tempo, você precisará conhecer suas convenções de nomenclatura. Mantenha-o simples e minimize o máximo possível. Sistemas de nomenclatura complicados são mais difíceis de manter.

Depois de capturar esses dados no banco de dados, você pode avaliar o desempenho do marketing e da publicidade usando análises mais sofisticadas, incluindo [Valor vitalício do cliente](../data-analyst/analysis/ess-expected-ltv.md), [Taxas de compra repetidas](../data-analyst/analysis/repurchase-behavior.md), e [Valor médio de pedido](../data-analyst/analysis/basic-analytics.md).
