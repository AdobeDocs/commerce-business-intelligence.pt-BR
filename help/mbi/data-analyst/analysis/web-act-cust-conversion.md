---
title: Análise da atividade do site e taxas de conversão do cliente
description: Saiba como configurar um painel que rastreará a atividade do site, incluindo exibições de página, sessões e usuários, e o índice de conversão do cliente ao longo do tempo.
exl-id: 2b57d5b3-3bbf-4ec9-86a6-9fa850c1c459
role: Admin, User
feature: Reports, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 0%

---

# Análise da atividade do site

O [!DNL Adobe Commerce Intelligence] permite que você integre facilmente seus dados de custo de publicidade ao restante dos seus dados. Isso não apenas permite que você entenda a atividade do site, mas também permite que você obtenha a porcentagem de visitantes do site que se tornam um usuário registrado ou fazem uma compra.

Este tópico demonstra como configurar um painel que rastreará as atividades do site, incluindo exibições de página, sessões e usuários, e a taxa de conversão do cliente ao longo do tempo.

## Pré-requisitos

**Importar seus dados de custo de publicidade** - Conectar [[!DNL [Google AdWords]]](../importing-data/integrations/google-adwords.md) a [!DNL Adobe Commerce Intelligence] - sincroniza automaticamente seus gastos com [!DNL AdWords] no Commerce Intelligence.

**Rastrear dados do canal de aquisição de usuário** - Para vincular os dados de [!DNL Google AdWords] a pedidos específicos no banco de dados, é necessário [rastrear a aquisição de usuário](../analysis/google-track-user-acq.md) via [!DNL Google Analytics E-commerce]. Isso permite conectar cada pedido a uma fonte e um meio utm.

## Campanhas de aquisição de usuário

Essa coleção de relatórios é criada usando o seguinte:

* Métricas geradas automaticamente quando você conecta os dados do [!DNL Google AdWords]
* Métricas básicas que já devem estar disponíveis em sua conta, como `Number of orders` e `New users`
* Dimension criado ao unir os dados do [!DNL Google Analytics Ecommerce] ao banco de dados, como a origem utm do pedido e a mídia utm do pedido. Entre em contato com a equipe de suporte se esses campos não estiverem disponíveis atualmente em sua conta

## Criação de relatórios

**Comece criando um relatório que mostre o número de exibições de página, sessões e usuários ao longo do tempo:**

1. Criar um relatório.
1. Clique em **[!UICONTROL Add Metric]**, em seguida passe o mouse sobre a seção [!DNL Google Analytics] na parte inferior da lista suspensa e selecione `Page Views`.
1. Adicione outra métrica, novamente passando o mouse sobre a seção [!DNL Google Analytics], desta vez selecionando `Sessions`.
1. Adicione uma terceira métrica, novamente passando o mouse sobre a seção [!DNL Google Analytics], desta vez selecionando `Users`.
1. Agora altere o período de tempo para um intervalo móvel, de 31 dias atrás para 1 dia atrás, e ajuste o intervalo de tempo para `by day`.
1. Dê um nome ao seu relatório (por exemplo, `Page views, sessions and users by day`) e clique em **[!UICONTROL Save]**.

**O segundo relatório analisa o número de exibições de página no ano passado:**

1. Criar um relatório.
1. Clique em **[!UICONTROL Add Metric]**, passe o mouse sobre a seção [!DNL Google Analytics] na parte inferior da lista suspensa e selecione _Exibições de página_.
1. Altere seu período de tempo para um intervalo móvel, de 13 meses atrás para 1 mês atrás, e ajuste o intervalo de tempo para `by month`.
1. Nomeie seu relatório, como `Page views by month,` e Clique em **[!UICONTROL Save]**.

**O terceiro gráfico analisa a taxa de rejeição no ano passado:**

1. Criar um relatório.
1. Clique em **[!UICONTROL Add Metric]**, passe o mouse sobre a seção [!DNL Google Analytics] na parte inferior da lista suspensa e selecione _Taxa de rejeição_.
1. Altere seu período de tempo para um intervalo móvel, de 13 meses atrás para 1 mês atrás, e ajuste o intervalo de tempo para `by month`.
1. Nomeie seu relatório, como `Bounce rate by month`, e clique em **[!UICONTROL Save]**.

**Agora, observe a duração média de sessão de novos visitantes em comparação com visitantes recorrentes:**

1. Criar um relatório.
1. Clique em **UICONTROL Adicionar métrica**, passe o mouse sobre a seção [!DNL Google Analytics] na parte inferior da lista suspensa e selecione `Average Session Length`.
1. Alterar o período de tempo para um intervalo móvel, de 13 meses atrás para 1 mês atrás, e ajustar o intervalo de tempo para `by month`?
1. Adicione um `Group by` e selecione `New or returning visitor`.  Marque a caixa `Show All` e clique em **[!UICONTROL Apply]**.
1. Nomeie seu relatório, como `Average session length`, e clique em **[!UICONTROL Save]**.

**Em seguida, verifique seus principais domínios de referência nos últimos 30 dias:**

1. Criar um relatório.
1. Clique em **[!UICONTROL Add Metric]**, passe o mouse sobre a seção [!DNL Google Analytics] na parte inferior da lista suspensa e selecione `Sessions`.
1. Altere o período para um intervalo móvel, de 31 dias atrás para 1 dia atrás, e ajuste o intervalo de tempo para `none`.
1. Adicione um `Group by` e selecione `ga:source`.  Marque a caixa _Mostrar tudo_ e clique em **[!UICONTROL Apply]**.
1. Adicione outro `group by` e selecione `ga:medium`. Novamente, marque a caixa `Show All` e clique em **[!UICONTROL Apply]**.
1. Dê um nome ao seu relatório, como `Top 20 Referring Domains, 30 Days`, e clique em **[!UICONTROL Save]**.

**Por fim, observe a conversão:**

1. Criar um relatório.
1. Adicione as seguintes métricas:

* `New users`
   * Clique em **[!UICONTROL Hide]** abaixo do nome da métrica

* `Number of orders`
   * Adicione um filtro para `Customer's order number` = 1 e clique em **[!UICONTROL Apply]**
   * Renomeie a métrica clicando no nome da métrica, chamando-a de `Number of first orders` e clique em **[!UICONTROL Hide]**

* `Number of orders`
   * **[!UICONTROL Hide]** a métrica

* `Users`
   * **[!UICONTROL Hide]** a métrica
   * Altere o período de tempo para `24 months ago to now` e ajuste o intervalo de tempo para `by month`.
   * Adicione as seguintes fórmulas clicando em **[!UICONTROL Formula]**.
   * A/D, em seguida, clique em **[!UICONTROL Apply]**
   * Renomear a fórmula `Registration conversion`
   * B/D e clique em **[!UICONTROL Apply]**
   * Renomear a fórmula `First order conversion`
   * C/D e clique em **[!UICONTROL Apply]**
   * Renomear a fórmula `Any order conversion`

* Agora dê um nome ao seu relatório, como `Conversion by month`, e clique em **[!UICONTROL Save]**.

## Próximas etapas

Agora que você tem acesso aos dados em seu tráfego da Web e taxas de conversão, pode começar a explorar esses dados para impulsionar decisões de negócios, como Quais sites são melhores para direcionar tráfego para o seu site? ou quais de suas campanhas são mais eficazes para conquistar clientes com o alto valor vitalício?

À medida que você ajusta os gastos com anúncios e a estratégia de marketing, pode continuar a acompanhar os resultados em [!DNL Commerce Intelligence], iterando neste painel para atender às prioridades em evolução da sua empresa.
