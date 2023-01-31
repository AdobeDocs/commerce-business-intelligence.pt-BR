---
title: Rastreamento de UTM no Google Analytics
description: Saiba mais sobre as práticas recomendadas para rastreamento de UTM (marcação) no Google Analytics.
exl-id: 70bfd855-3b3f-469b-99bc-deb8251904b7
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# Rastreamento de UTM

`UTM` O rastreamento é uma convenção de marcação para URLs que permite analisar de onde vêm seus usuários. Se você observar os URLs que clica da maioria dos emails de marketing ou anúncios de banner, verá a marcação UTM. São esses links longos que terminam com coisas como `utm\_source` e `utm\_medium`.

[!DNL Google Analytics] uses `UTM` marcando para saber de onde o tráfego está vindo. Algumas dessas informações vêm do [Referenciador HTTP](https://en.wikipedia.org/wiki/HTTP_referer) Mas o resto tem que se abastecer `UTM` parâmetros. Quando você vê `google adwords` ou `email marketing` significa que `UTM` parâmetros que estão sendo registrados no link original, clique em e depois armazenado nos cookies do usuário. Daí, [!DNL Google Analytics] O usa esses dados para [atribuir comportamentos interessantes](../data-analyst/analysis/google-track-user-acq.md) no seu site. Entender para o que esses parâmetros são, ajuda você a entender como configurar e usar a marcação de UTM.

## Práticas recomendadas para marcação de UTM

A seguir são listados os cinco itens mais importantes a serem lembrados ao configurar URLs com `UTM` marcação.

### 1. Tem como objetivo marcar cada URL que você pode controlar para acessar seu site

Toda vez que você solicita que as pessoas cliquem em um link, você deve estar configurando `UTM` marcação. Isso inclui todos os links de email (o provedor de serviços de email provavelmente tem uma maneira de marcar automaticamente seus URLs), links de anúncios, artigos de imprensa, publicações de blog.

### 2. Use uma ferramenta para criar o URL

`UTM`URLs com tags de podem ser muito complicadas. Em vez de tentar digitá-los por mais tempo, use uma ferramenta [como este](https://support.google.com/analytics/answer/1033867?hl=en) para ajudá-lo. Isso garante que você esteja pensando em adicionar todos os parâmetros adequados ao URL e obtenha o URL para copiar e colar diretamente dele. Para gerenciar links sociais, ferramentas como [!DNL Hootsuite] inclua a opção para adicionar parâmetros de URL personalizados a todos os links.

### 3. Certifique-se de que os valores de parâmetro fazem distinção entre maiúsculas e minúsculas

É importante lembrar que a tag `utm\_source=adwords` é uma tag diferente de `utm\_source=Adwords`. Considere fazer tudo em minúsculas.

### 4. Armazene os valores do parâmetro da UTM no seu banco de dados

Sempre que uma transação ou um evento ocorrer, você deverá avaliar o desempenho de suas atividades de marketing. Você pode fazer isso lendo os valores dos valores do parâmetro UTM da variável [[!DNL Google Analytics] cookie no banco de dados](../data-analyst/analysis/google-track-user-acq.md).

### 5. Pense em como você nomeia campanhas

Para acompanhar como seus esforços de marketing estão melhorando ao longo do tempo, você precisará ser inteligente sobre suas convenções de nomenclatura. Mantenha-o simples e minimize o máximo possível. Os sistemas de nomenclatura complicados são mais difíceis de manter.

Depois de capturar esses dados no banco de dados, você pode avaliar o desempenho de marketing e publicidade por meio de análises mais sofisticadas, incluindo [Valor vitalício do cliente](../data-analyst/analysis/ess-expected-ltv.md), [Repetir Taxas de Compra](../data-analyst/analysis/repurchase-behavior.md)e [Valor médio de pedido](../data-analyst/analysis/basic-analytics.md).
