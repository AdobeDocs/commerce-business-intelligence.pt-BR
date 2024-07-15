---
title: Google Analytics - Rastrear o dispositivo do usuário e os dados do navegador no banco de dados
description: Saiba quantos usuários estão realmente fazendo logon por dispositivos móveis e como isso afeta o valor vitalício desses usuários.
exl-id: 57b1bc45-b139-4370-86ea-2fbd021aa14d
role: Admin, User
feature: Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# Acompanhamento de [!UICONTROL Google Analytics]

Com o [!UICONTROL Google Analytics] você pode [salvar informações da fonte de referência](../analysis/google-track-user-acq.md) para entender de onde vêm seus usuários mais valiosos. Este tópico discute a plataforma (por exemplo, dispositivo ou navegador) em que seus usuários estão trabalhando. Com isso, você poderá entender quantos usuários estão realmente fazendo logon por dispositivos móveis e como isso afeta o valor vitalício desses usuários.

## Salvamento dos dados do dispositivo do usuário e do navegador

Toda vez que uma solicitação é feita ao seu site, o navegador do usuário envia uma cadeia de caracteres usuário-agente com informações sobre a plataforma que faz a solicitação. Estes são alguns exemplos da string do usuário-agente:

1. `Mozilla/5.0 (Macintosh; Intel Mac OS X 10\_8\_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36`
1. `Mozilla/5.0 (Windows NT 6.1; WOW64; rv:17.0) Gecko/17.0 Firefox/17.0`
1. `Mozilla/5.0 (iPhone; U; CPU iPhone OS 4\_0 like Mac OS X; en-us) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8A293 Safari/6531.22.7`
1.` Mozilla/5.0 (iPad; CPU OS 5\_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B176 Safari/7534.48.3`
1. `Mozilla/5.0 (Linux; U; Android 2.2; en-us; Nexus One Build/FRF91) AppleWebKit/533.1 (KHTML, like Gecko) Version/4.0 Mobile Safari/533.1`

Se você observar com atenção, verá que a cadeia de caracteres contém informações sobre o sistema operacional do usuário, o navegador e o nome do dispositivo que ele está usando (se tiver um nome). Embora as strings usuário-agente variem amplamente entre as plataformas e até mesmo versões da mesma plataforma, geralmente é verdade que o nome da plataforma existirá em algum lugar dentro do. Por exemplo, #1 acima é um Mac com o navegador Chrome, #2 acima é uma máquina Windows com o navegador Firefox, #3 é um iPhone, #4 é um iPad e #5 é um dispositivo Android.

Essas informações podem ser acessadas pelo servidor sempre que uma solicitação for feita. No PHP, a sequência usuário-agente é armazenada em `$_SERVER['HTTP_USER_AGENT']`. No Ruby on Rails, ele é armazenado em `request.env['HTTP_USER_AGENT']`. Outros idiomas e ambientes permitirão acessá-lo de maneiras semelhantes.

### Quando você deve registrar esses dados?

A [!DNL Adobe] recomenda adicionar um novo campo chamado `Platform` ou `User-Agent` às tabelas de banco de dados `Customers` e `Orders` para armazenar essas informações sempre que um usuário for criado ou um pedido for feito. Se você estiver usando um banco de dados SQL, este campo deverá ser um `VARCHAR(255)`. 

>[!NOTE]
>
>A cadeia de caracteres `User-Agent` pode ser muito mais longa do que isso, mas na prática ela raramente excede esse comprimento.

### Como analisar os segmentos úteis?

Há várias bibliotecas lá fora para ajudá-lo a analisar a cadeia de caracteres `User-Agent` em componentes como sistema operacional, dispositivo e assim por diante. Consulte o [projeto ua-parser](https://github.com/tobie/ua-parser) para saber mais.

Com essas novas informações, você pode entender melhor como os usuários acessam seu site. Em seguida, você pode adaptar a experiência ou criar campanhas de marketing para determinados grupos.

## Relacionados

* [Rastrear origem da referência de ordem via [!DNL Google Anaytics] E-Commerce](../importing-data/integrations/google-ecommerce.md)
* [Rastrear a fonte de referência do usuário no banco de dados](../analysis/google-track-user-acq.md)
* [Descubra as fontes e os canais de aquisição mais valiosos](../analysis/most-value-source-channel.md)
* [Conectar sua conta  [!DNL Google Adwords] ](../importing-data/integrations/google-adwords.md)
* [Aumente o ROI em suas campanhas publicitárias](../analysis/roi-ad-camp.md)
* [Como funciona a atribuição  [!DNL Google Analytics] UTM?](../analysis/utm-attributes.md)
