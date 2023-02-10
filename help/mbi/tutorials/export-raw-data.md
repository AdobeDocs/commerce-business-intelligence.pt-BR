---
title: Exportar dados brutos
description: Saiba como exportar registros de seu [!DNL MBI] Data Warehouse para obter uma visão mais detalhada do que está acionando seu painel.
exl-id: 26decdaf-2b2c-4ca2-b3d5-0386892662e8
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# Exportar dados brutos

Com exportações de dados brutos, é possível exportar registros de [!DNL MBI] Data Warehouse para obter uma visão mais detalhada do que está acionando seu painel. Além disso, as exportações de dados brutos podem ajudar você [discrepâncias de dados do ponto de extremidade](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html?lang=en).

As exportações de dados brutos fornecem acesso a colunas e dimensões adicionais geradas por meio da desnormalização e pré-agregação de métricas relevantes. Por exemplo, `User's first order date` é uma dimensão que pode ser exportada para cada usuário no [!DNL MBI], embora possa não estar disponível no seu banco de dados.

Este tutorial aborda o seguinte:

* [Selecionar dados para exportar](#select)
* [Fazendo download do arquivo Exportar (](#download)
* [Acesso a Exportações Históricas](#historical)

## Etapa 1: Selecionar dados para exportar {#select}

Há duas maneiras de exportar dados brutos no [!DNL MBI]: no nível do gráfico ou no nível da tabela.

### Exportar no nível da tabela em `Manage Data` Tabulação

Se quiser exportar a tabela de `Manage Data` , será necessário [Administrador](../administrator/user-management/user-management.md) permissões.

1. Clique em **[!UICONTROL Manage Data** > ** Exportar dados **> **Exportação de dados brutos]** para começar.
1. Você verá um `Export List` de exportações de dados criadas recentemente, se houver. Clique em **[!UICONTROL Add Export]** para criar uma nova exportação.
1. O `New Raw Data Export` será exibida. Aqui, você pode personalizar sua exportação selecionando ou desmarcando colunas e filtros:

   * `Table` - O `Table` seleciona a tabela da qual os dados serão exportados. Por padrão, isso exibirá a tabela na qual você navegou.
   * `Export Name` - Nesse campo, insira o nome da exportação. Por exemplo: `Philadelphia - Daily Revenue`.
   * `Available Columns` - Esse campo lista as colunas (dimensões) no banco de dados que estão disponíveis para inclusão na exportação. Para adicionar uma coluna, clique em seu nome.
   * `Selected Columns` - Esse campo lista as colunas (dimensões) incluídas atualmente na exportação. Para remover uma coluna, clique em seu nome.
   * `Filter` - Esta seção lista os filtros aplicados atualmente à exportação. Estes filtros podem ser alterados; novos filtros também podem ser adicionados para exportar um conjunto de dados específico.
   * Quando terminar, clique em **[!UICONTROL Export Data]**.

### Exportar no nível do gráfico do painel

1. Clique no ícone de engrenagem no canto superior direito de qualquer gráfico.
1. Selecionar `Raw Export` na lista suspensa para exibir a variável `Raw Export` caixa de diálogo.
1. Personalize a exportação escolhendo o `table`, `columns`e `filters` para incluir ou excluir. Consulte a seção anterior para obter informações mais detalhadas sobre os campos neste módulo.
   >[!NOTE]
   >
   >A tabela exibida na `Table` é, por padrão, a tabela que alimenta o gráfico.

1. Quando terminar, clique em **[!UICONTROL Export Data]**.

Vejamos todo o processo no nível do gráfico.

![](../assets/Chart-level_export.gif)

## Etapa 2: Download da exportação {#download}

A exportação começará o processamento imediatamente após concluir suas seleções na `Raw Data Export` caixa de diálogo. Como algumas exportações podem ter um tamanho grande, elas estão limitadas a 10 milhões de linhas e podem levar algum tempo para serem executadas.

Para verificar se a exportação está pronta, clique em **[!UICONTROL Raw Data Exports]** no canto superior direito da tela. Clique em **[!UICONTROL Download]** para baixar um arquivo zipado `.csv` da exportação.

![](../assets/Downloading_export.gif)

## Etapa 3: Acesso a Exportações Históricas {#historical}

Para exibir suas exportações anteriores, clique em **[!UICONTROL Raw Data Export]** no canto superior direito da tela. Relatórios pendentes e concluídos podem ser acessados por até sete dias.

Parabéns! Você terminou.
