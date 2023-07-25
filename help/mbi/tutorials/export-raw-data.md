---
title: Exportar dados brutos
description: Saiba como exportar registros do seu [!DNL Commerce Intelligence] Data Warehouse para obter uma visão mais detalhada do que está acionando seu painel.
exl-id: 26decdaf-2b2c-4ca2-b3d5-0386892662e8
role: Admin, Data Architect, Data Engineer, Leader, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# Exportar dados brutos

Usando exportações de dados brutos, você pode exportar registros da sua Data Warehouse para ver mais de perto o que está acionando seu painel. Além disso, as exportações de dados brutos podem ajudar você [discrepâncias de dados do pinpoint](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html).

As exportações de dados brutos fornecem acesso a colunas e dimensões adicionais geradas por meio da desnormalização e da pré-agregação de métricas relevantes. Por exemplo, `User's first order date` é uma dimensão que pode ser exportada para cada usuário no [!DNL Commerce Intelligence], embora possa não estar disponível no banco de dados.

Este tutorial aborda o seguinte:

* [Seleção de dados para exportar](#select)
* [Download da exportação (](#download)
* [Acesso a exportações históricas](#historical)

## Etapa 1: Seleção de Dados para Exportação {#select}

Há duas maneiras de exportar dados brutos no [!DNL Commerce Intelligence]:

1. no nível do gráfico
1. no nível da tabela

### Exportar no Nível da Tabela em seu [!UICONTROL Manage Data] Guia

Se desejar exportar a tabela de [!UICONTROL Manage Data] , é necessário [Admin](../administrator/user-management/user-management.md) permissões.

1. Clique em **[!UICONTROL Manage Data** > ** Exportar dados **> **Exportação de dados brutos]**.
1. Você vê um `Export List` de exportações de dados criadas recentemente, se houver. Clique em **[!UICONTROL Add Export]** para criar uma exportação.
1. A variável `New Raw Data Export` é exibida. Aqui, você pode personalizar a exportação selecionando ou desmarcando colunas e filtros:

   * `Table` - A `Table` seleciona a tabela da qual os dados são exportados. Por padrão, exibe a tabela na qual você navegou.
   * `Export Name` - Nesse campo, digite o nome da exportação. Por exemplo: `Philadelphia - Daily Revenue`.
   * `Available Columns` - Esse campo lista as colunas (dimensões) no banco de dados que estão disponíveis para inclusão na exportação. Para adicionar uma coluna, clique em seu nome.
   * `Selected Columns` - Esse campo lista as colunas (dimensões) incluídas na exportação no momento. Para remover uma coluna, clique em seu nome.
   * `Filter` - Essa seção lista os filtros aplicados no momento à exportação. Esses filtros podem ser alterados; novos filtros também podem ser adicionados para exportar um conjunto de dados específico.
   * Quando terminar, clique em **[!UICONTROL Export Data]**.

### Exportar no Nível do Gráfico a partir do Painel

1. Clique no ícone de engrenagem no canto superior direito de qualquer gráfico.

1. Selecionar `Raw Export` na lista suspensa para exibir a variável `Raw Export` diálogo.

1. Personalize a exportação escolhendo o `table`, `columns`, e `filters` para incluir ou excluir. Consulte a seção anterior para obter informações mais detalhadas sobre os campos deste módulo.

   >[!NOTE]
   >
   >A tabela exibida na variável `Table` é, por padrão, a tabela que ativa o gráfico.

1. Quando terminar, clique em **[!UICONTROL Export Data]**.

Examine todo o processo no nível do gráfico.

![](../assets/Chart-level_export.gif)

## Etapa 2 - Download da exportação {#download}

A exportação começará a ser processada imediatamente após concluir as seleções na `Raw Data Export` diálogo. Como algumas exportações podem ser grandes em tamanho, elas são limitadas a 10 milhões de linhas e podem levar algum tempo para serem executadas.

Para verificar se a exportação está pronta, clique em **[!UICONTROL Raw Data Exports]** no canto superior direito da tela. Clique em **[!UICONTROL Download]** para baixar um arquivo compactado `.csv` arquivo da sua exportação.

![](../assets/Downloading_export.gif)

## Etapa 3: Acesso a Exportações Históricas {#historical}

Para exibir suas exportações anteriores, clique em **[!UICONTROL Raw Data Export]** no canto superior direito da tela. Os relatórios pendentes e concluídos podem ser acessados por até sete dias.
