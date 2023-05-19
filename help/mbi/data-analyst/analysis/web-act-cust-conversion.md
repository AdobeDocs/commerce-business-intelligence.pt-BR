---
title: Análise da atividade do site e taxas de conversão do cliente
description: Saiba como configurar um painel que rastreará a atividade do site, incluindo exibições de página, sessões e usuários, e o índice de conversão do cliente ao longo do tempo.
exl-id: 2b57d5b3-3bbf-4ec9-86a6-9fa850c1c459
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 0%

---

# Análise da atividade do site

[!DNL Adobe Commerce Intelligence] O permite integrar facilmente seus dados de custo de publicidade ao restante dos dados. Isso não apenas permite que você entenda a atividade do site, mas também permite que você obtenha a porcentagem de visitantes do site que se tornam um usuário registrado ou fazem uma compra.

Este tópico demonstra como configurar um painel que rastreará as atividades do site, incluindo exibições de página, sessões e usuários, e a taxa de conversão do cliente ao longo do tempo.

## Pré-requisitos

**Importar seus dados de custo de publicidade** - Conectar [!DNL [Google AdWords]](../importing-data/integrations/google-adwords.md) para [!DNL Adobe Commerce Intelligence] - isso sincroniza automaticamente o [!DNL AdWords] gastar no Commerce Intelligence.

**Rastrear dados do canal de aquisição de usuários** - Para amarrar o seu [!DNL Google AdWords] dados para pedidos específicos no banco de dados, é necessário [rastrear aquisição de usuários](../analysis/google-track-user-acq.md) via [!DNL Google Analytics E-commerce]. Isso permite conectar cada pedido a uma fonte e um meio utm.

## Campanhas de aquisição de usuário

Essa coleção de relatórios é criada usando o seguinte:

* Métricas geradas automaticamente quando você se conecta ao [!DNL Google AdWords] dados
* Métricas básicas que já devem estar disponíveis em sua conta, como `Number of orders` e `New users`
* Dimension criado ao ingressar no [!DNL Google Analytics Ecommerce] dados para o banco de dados, como a origem utm do pedido e a mídia utm do pedido. Entre em contato com a equipe de suporte se esses campos não estiverem disponíveis atualmente em sua conta

## Criação de relatórios

**Comece criando um relatório que mostre o número de exibições de página, sessões e usuários ao longo do tempo:**

1. Criar um relatório.
1. Clique em **[!UICONTROL Add Metric]**, em seguida, passe com o mouse sobre o [!DNL Google Analytics] na parte inferior da lista suspensa e selecione `Page Views`.
1. Adicione outra métrica, novamente passando o mouse sobre a [!DNL Google Analytics] seção, desta vez selecionando `Sessions`.
1. Adicione uma terceira métrica, novamente passando o mouse sobre a [!DNL Google Analytics] seção, desta vez selecionando `Users`.
1. Agora, altere o período para um intervalo móvel de 31 dias atrás para 1 dia atrás e ajuste o intervalo de tempo para `by day`.
1. Nomeie seu relatório (por exemplo, `Page views, sessions and users by day`) e clique em **[!UICONTROL Save]**.

**O segundo relatório analisa o número de exibições de página no ano passado:**

1. Criar um relatório.
1. Clique em **[!UICONTROL Add Metric]**, passe o mouse sobre o [!DNL Google Analytics] na parte inferior da lista suspensa e selecione _Exibições de página_.
1. Altere o período para um intervalo móvel, de 13 meses atrás para 1 mês atrás, e ajuste o intervalo de tempo para `by month`.
1. Nomeie o relatório, como `Page views by month,` e clique em **[!UICONTROL Save]**.

**O terceiro gráfico analisa a taxa de rejeição no ano passado:**

1. Criar um relatório.
1. Clique em **[!UICONTROL Add Metric]**, passe o mouse sobre o [!DNL Google Analytics] na parte inferior da lista suspensa e selecione _Taxa de rejeição_.
1. Altere o período para um intervalo móvel, de 13 meses atrás para 1 mês atrás, e ajuste o intervalo de tempo para `by month`.
1. Nomeie o relatório, como `Bounce rate by month`e clique em **[!UICONTROL Save]**.

**Agora, observe a duração média das sessões de novos visitantes em comparação aos visitantes recorrentes:**

1. Criar um relatório.
1. Clique em **Adicionar métrica do UICONTROL**, passe o mouse sobre o [!DNL Google Analytics] na parte inferior da lista suspensa e selecione `Average Session Length`.
1. Altere o período para um intervalo móvel, de 13 meses atrás para 1 mês atrás, e ajuste o intervalo de tempo para `by month`?
1. Adicionar um `Group by` e selecione `New or returning visitor`.  Verifique a `Show All` ; depois clique em **[!UICONTROL Apply]**.
1. Nomeie o relatório, como `Average session length`e clique em **[!UICONTROL Save]**.

**Em seguida, verifique seus principais domínios de referência nos últimos 30 dias:**

1. Criar um relatório.
1. Clique em **[!UICONTROL Add Metric]**, passe o mouse sobre o [!DNL Google Analytics] na parte inferior da lista suspensa e selecione `Sessions`.
1. Altere o período para um intervalo móvel, de 31 dias atrás para 1 dia atrás, e ajuste o intervalo de tempo para `none`.
1. Adicionar um `Group by` e selecione `ga:source`.  Verifique a _Mostrar tudo_ ; depois clique em **[!UICONTROL Apply]**.
1. Adicionar outro `group by` e selecione `ga:medium`. Novamente, verifique a `Show All` ; depois clique em **[!UICONTROL Apply]**.
1. Nomeie o relatório, como `Top 20 Referring Domains, 30 Days`e clique em **[!UICONTROL Save]**.

**Por fim, observe a conversão:**

1. Criar um relatório.
1. Adicione as seguintes métricas:

* `New users`
   * Clique em **[!UICONTROL Hide]** abaixo do nome da métrica

* `Number of orders`
   * Adicionar um filtro para `Customer's order number` = 1 e clique em **[!UICONTROL Apply]**
   * Renomear a métrica clicando no nome da métrica e chamando-a `Number of first orders`e, em seguida, clique em **[!UICONTROL Hide]**

* `Number of orders`
   * **[!UICONTROL Hide]** a métrica

* `Users`
   * **[!UICONTROL Hide]** a métrica
   * Alterar o período para `24 months ago to now`e ajustar o intervalo de tempo para `by month`.
   * Adicione as seguintes fórmulas clicando em **[!UICONTROL Formula]**.
   * A/D e clique em **[!UICONTROL Apply]**
   * Renomear a fórmula `Registration conversion`
   * B/D e clique em **[!UICONTROL Apply]**
   * Renomear a fórmula `First order conversion`
   * C/D e clique em **[!UICONTROL Apply]**
   * Renomear a fórmula `Any order conversion`

* Agora dê um nome ao seu relatório, como `Conversion by month`e clique em **[!UICONTROL Save]**.

## Próximas etapas

Agora que você tem acesso aos dados em seu tráfego da Web e taxas de conversão, pode começar a explorar esses dados para impulsionar decisões de negócios, como Quais sites são melhores para direcionar tráfego para o seu site? ou quais de suas campanhas são mais eficazes para conquistar clientes com o alto valor vitalício?

À medida que ajusta os gastos com anúncios e a estratégia de marketing, você pode continuar a acompanhar os resultados em [!DNL Commerce Intelligence], iterando neste painel para atender às prioridades em evolução da sua empresa.
