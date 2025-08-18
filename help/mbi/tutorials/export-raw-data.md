---
title: Exportar dados brutos
description: Saiba como exportar registros do seu  [!DNL Commerce Intelligence] Data Warehouse para obter uma visão mais detalhada do que está acionando seu painel.
exl-id: 26decdaf-2b2c-4ca2-b3d5-0386892662e8
role: Admin, Data Architect, Data Engineer, Leader, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# Exportar dados brutos

Usando exportações de dados brutos, você pode exportar registros do seu Data Warehouse para obter uma visão mais detalhada do que está acionando seu painel. Além disso, as exportações de dados brutos podem ajudá-lo a [identificar discrepâncias de dados](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html).

As exportações de dados brutos fornecem acesso a colunas e dimensões adicionais geradas por meio da desnormalização e da pré-agregação de métricas relevantes. Por exemplo, `User's first order date` é uma dimensão que você pode exportar para cada usuário em [!DNL Commerce Intelligence], embora ela possa não estar disponível no banco de dados.

Este tutorial aborda o seguinte:

* [Seleção de dados para exportar](#select)
* [Download da exportação (](#download)
* [Acesso a exportações históricas](#historical)

## Etapa 1: Seleção de Dados para Exportação {#select}

Há duas maneiras de exportar dados brutos para o [!DNL Commerce Intelligence]:

1. no nível do gráfico
1. no nível da tabela

### Exportando no Nível da Tabela na Guia [!UICONTROL Manage Data]

Para exportar a tabela da guia [!UICONTROL Manage Data], são necessárias [permissões de administrador](../administrator/user-management/user-management.md).

1. Clique em **[!UICONTROL Manage Data** > **&#x200B; Exportar Dados &#x200B;**> **Exportação de Dados Brutos]**.
1. Você verá uma `Export List` de exportações de dados criadas recentemente, se houver alguma. Clique em **[!UICONTROL Add Export]** para criar uma exportação.
1. A caixa de diálogo `New Raw Data Export` é exibida. Aqui, você pode personalizar a exportação selecionando ou desmarcando colunas e filtros:

   * `Table` - O campo `Table` seleciona a tabela da qual os dados são exportados. Por padrão, exibe a tabela na qual você navegou.
   * `Export Name` - Neste campo, insira o nome da exportação. Por exemplo: `Philadelphia - Daily Revenue`.
   * `Available Columns` - Este campo lista as colunas (dimensões) do banco de dados que estão disponíveis para inclusão na exportação. Para adicionar uma coluna, clique em seu nome.
   * `Selected Columns` - Este campo lista as colunas (dimensões) atualmente incluídas na exportação. Para remover uma coluna, clique em seu nome.
   * `Filter` - Esta seção lista os filtros atualmente aplicados à exportação. Esses filtros podem ser alterados; novos filtros também podem ser adicionados para exportar um conjunto de dados específico.
   * Quando terminar, clique em **[!UICONTROL Export Data]**.

### Exportar no Nível do Gráfico a partir do Painel

1. Clique no ícone de engrenagem no canto superior direito de qualquer gráfico.

1. Selecione `Raw Export` na lista suspensa para exibir a caixa de diálogo `Raw Export`.

1. Personalize a exportação escolhendo os `table`, `columns` e `filters` a serem incluídos ou excluídos. Consulte a seção anterior para obter informações mais detalhadas sobre os campos deste módulo.

   >[!NOTE]
   >
   >A tabela exibida no campo `Table` é, por padrão, a tabela que ativa o gráfico.

1. Quando terminar, clique em **[!UICONTROL Export Data]**.

Examine todo o processo no nível do gráfico.

![](../assets/Chart-level_export.gif)

## Etapa 2 - Download da exportação {#download}

A exportação começará a ser processada imediatamente após a conclusão das seleções na caixa de diálogo `Raw Data Export`. Como algumas exportações podem ser grandes em tamanho, elas são limitadas a 10 milhões de linhas e podem levar algum tempo para serem executadas.

Para verificar se a exportação está pronta, clique em **[!UICONTROL Raw Data Exports]** no canto superior direito da tela. Clique em **[!UICONTROL Download]** para baixar um arquivo compactado `.csv` da sua exportação.

![](../assets/Downloading_export.gif)

## Etapa 3: Acesso a Exportações Históricas {#historical}

Para exibir suas exportações anteriores, clique em **[!UICONTROL Raw Data Export]** no canto superior direito da tela. Os relatórios pendentes e concluídos podem ser acessados por até sete dias.
