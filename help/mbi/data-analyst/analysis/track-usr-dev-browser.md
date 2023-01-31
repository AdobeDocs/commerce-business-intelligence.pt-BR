---
title: Google Analytics - Rastrear dados do dispositivo e do navegador do usuário no seu banco de dados
description: Saiba quantos usuários estão fazendo logon por dispositivos móveis e como isso afeta o valor da vida útil desses usuários.
exl-id: 57b1bc45-b139-4370-86ea-2fbd021aa14d
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# [!UICONTROL Google Analytics] Rastreamento

Com [!UICONTROL Google Analytics] você pode [salvar informações da fonte de referência](../analysis/google-track-user-acq.md) para entender de onde vêm seus usuários mais valiosos. Neste tópico, você aprenderá sobre a plataforma (por exemplo, dispositivo ou navegador) na qual os usuários estão trabalhando. Com isso, você poderá entender quantos usuários estão fazendo logon por dispositivos móveis e como isso afeta o valor desses usuários ao longo da vida.

## Como salvar o dispositivo do usuário e os dados do navegador

Toda vez que uma solicitação é feita ao seu site, o navegador do usuário envia uma sequência de caracteres Agente do usuário com informações sobre a plataforma que faz a solicitação. Estes são alguns exemplos da string User-Agent:

1. `Mozilla/5.0 (Macintosh; Intel Mac OS X 10\_8\_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36`
1. `Mozilla/5.0 (Windows NT 6.1; WOW64; rv:17.0) Gecko/17.0 Firefox/17.0`
1. `Mozilla/5.0 (iPhone; U; CPU iPhone OS 4\_0 like Mac OS X; en-us) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8A293 Safari/6531.22.7`
1.
` Mozilla/5.0 (iPad; CPU OS 5\_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B176 Safari/7534.48.3`
1. `Mozilla/5.0 (Linux; U; Android 2.2; en-us; Nexus One Build/FRF91) AppleWebKit/533.1 (KHTML, like Gecko) Version/4.0 Mobile Safari/533.1`

Se você observar atentamente, verá que a string contém informações sobre o sistema operacional, o navegador e o nome do dispositivo usado pelo usuário (se ele tiver um nome). Embora as sequências de caracteres User-Agent variem muito entre as plataformas e até mesmo as versões da mesma plataforma, geralmente é verdade que o nome da plataforma existirá em algum lugar dentro dela. Por exemplo, o #1 acima é um Mac com navegador Chrome, o #2 acima é uma máquina Windows com navegador Firefox, o #3 é um iPhone, o #4 é um iPad e o #5 é um dispositivo Android.

Essas informações podem ser acessadas pelo seu servidor sempre que uma solicitação é feita. No PHP, a sequência User-Agent é armazenada em `$_SERVER['HTTP_USER_AGENT']`. No Ruby on Rails, ele é armazenado em `request.env['HTTP_USER_AGENT']`. Outros idiomas e ambientes permitirão acessá-lo de maneira semelhante.

### Quando você deve registrar esses dados?

Recomendamos adicionar um novo campo chamado `Platform` ou `User-Agent` para `Customers` e `Orders` tabelas de banco de dados para armazenar essas informações sempre que um usuário é criado ou um pedido é feito. Se estiver usando um banco de dados SQL, esse campo deverá ser um `VARCHAR(255)`. 

>[!NOTE]
>
>O `User-Agent` é permitido que a string seja muito maior que isso, mas na prática ela raramente excede esse comprimento.

### Como analisar os segmentos úteis?

Há várias bibliotecas disponíveis para ajudá-lo a analisar a variável `User-Agent` string em componentes como sistema operacional, dispositivo e assim por diante. Consulte a [projeto ua-parser](https://github.com/tobie/ua-parser) para saber mais.

Com essas novas informações, você pode entender melhor como os usuários acessam seu site. Você pode, então, adaptar sua experiência ou criar campanhas de marketing para determinados grupos.

## Relacionado

* [Rastrear origem de referência do pedido via [!DNL Google Anaytics] Comércio eletrônico](../importing-data/integrations/google-ecommerce.md)
* [Rastrear a fonte de referência do usuário no seu banco de dados](../analysis/google-track-user-acq.md)
* [Descubra as fontes e os canais de aquisição mais valiosos](../analysis/most-value-source-channel.md)
* [Conecte seu [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [Aumente o ROI em suas campanhas publicitárias](../analysis/roi-ad-camp.md)
* [Como [!DNL Google Analytics] A atribuição de UTM funciona?](../analysis/utm-attributes.md)
