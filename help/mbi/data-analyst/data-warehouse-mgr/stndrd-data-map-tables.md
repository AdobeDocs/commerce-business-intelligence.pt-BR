---
title: Padronizar dados com tabelas de mapeamento
description: Saiba como trabalhar com tabelas de mapeamento.
exl-id: e452ff87-f298-43d5-acc3-af58e53bd0bc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---

# Padronizar Dados com Tabelas de Mapeamento

Imagine que você esteja no `Report Builder` criando um relatório `Revenue by State`. Tudo vai bem até que você tente adicionar um agrupamento `billing state` ao seu relatório e veja o seguinte:

![Gráfico mostrando segmentos de estado confuso com nomenclatura inconsistente](../../assets/Messy_State_Segments.png)

## Como isso pode acontecer?

Infelizmente, a falta de padronização pode, às vezes, causar confusão nos dados e dores de cabeça ao criar relatórios. Neste exemplo, pode não ter havido um menu suspenso ou um modo padronizado para seus clientes inserirem suas informações de estado de faturamento. Isso leva a vários valores - `pa`, `PA`, `penna`, `pennsylvania` e `Pennsylvania` - todos para o mesmo estado, o que leva a alguns resultados estranhos no `Report Builder`.

É possível que haja um recurso técnico que possa ajudar você a limpar os dados ou inserir as colunas necessárias diretamente no banco de dados. Caso contrário, há outra solução - **a tabela de mapeamento**. Uma tabela de mapeamento permite limpar e padronizar de forma rápida e fácil quaisquer dados confusos, mapeando os dados para uma única saída.

>[!NOTE]
>
>Não é possível criar uma tabela de mapeamento para tabelas consolidadas sem a ajuda da equipe de suporte da Adobe.

## Como criá-lo? {#how}

**Atualizador da formatação de dados:**

* Certifique-se de que sua planilha tenha uma linha de cabeçalho.
* Evite usar vírgulas! Isso causa problemas quando você faz upload do arquivo.
* Use o formato de data padrão `(YYYY-MM-DD HH:MM:SS)` para datas.
* As porcentagens devem ser inseridas como decimais.
* Verifique se os zeros à esquerda ou à direita estão retidos corretamente.

Antes de mergulhar, a Adobe recomenda [exportar os dados brutos da tabela](../../tutorials/export-raw-data.md). Observar os dados brutos primeiro significa que você pode explorar todas as combinações possíveis para os dados que precisam ser limpos, garantindo que a tabela de mapeamento cubra tudo.

Para criar uma tabela de mapeamento, você precisa criar uma planilha de duas colunas que siga as [regras de formatação para os uploads de arquivo](../../data-analyst/importing-data/connecting-data/using-file-uploader.md).

Na primeira coluna, insira os valores armazenados no banco de dados com **apenas um valor em cada linha**. Por exemplo, `pa` e `PA` não podem estar na mesma linha - cada entrada precisa ter sua própria linha. Veja um exemplo abaixo.

Na segunda coluna, insira quais valores **devem ser**. Continuando com o exemplo de estado de faturamento, se você quiser que `pa`, `PA`, `Pennsylvania` e `pennsylvania` seja simplesmente `PA`, digite `PA` nesta coluna para cada valor de entrada.

![Exemplo de tabela de mapeamento mostrando valores originais e valores padronizados](../../assets/Mapping_table_examples.jpg)

## O que preciso fazer em [!DNL Commerce Intelligence] para usá-lo? {#use}

Após concluir a criação da tabela de mapeamento, você deve [carregar o arquivo](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) em [!DNL Commerce Intelligence] e [criar uma coluna unida](../../data-analyst/data-warehouse-mgr/calc-column-types.md) que realoca o novo campo para a tabela desejada. Você pode fazer isso depois que o arquivo for sincronizado com a Data Warehouse.

Este exemplo move a coluna criada na tabela `mapping_state` (`state_input`) para a tabela `customer_address` usando uma coluna unida. Isso nos permite agrupar pela coluna `state_input` limpa em seus relatórios em vez da coluna `state`.

Para criar a coluna `joined`, navegue até a tabela para a qual o campo será realocado no Data Warehouse Manager. Neste exemplo, esta seria a tabela `customer_address`.

1. Clique em **[!UICONTROL Create a Column]**.
1. Selecione `Joined Column` na lista suspensa `Definition`.
1. Dê à coluna um nome que a diferencie da coluna `state` no banco de dados. Nomeie a coluna `billing state (mapped)` para que você possa saber qual coluna usar ao segmentar no Report Builder.
1. O caminho necessário para conectar as tabelas não existe, portanto, é necessário criar um. Clique em **[!UICONTROL Create new path]** na lista suspensa `Select a table and column`.

   Se você não tiver certeza do que é a relação de tabela ou como definir corretamente as chaves primária e externa, confira o [tutorial](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md) para obter ajuda.

   * No lado de `Many`, selecione a tabela para a qual você está realocando o campo (novamente, para nós ele é `customer_address`) e a coluna `Foreign Key`, ou coluna `state`, no exemplo.
   * No lado de `One`, selecione a tabela `mapping` e a coluna `Primary key`. Nesse caso, você selecionaria a coluna `state_input` da tabela `mapping_state`.
   * Veja como o caminho se parece:

     ![Data Warehouse Manager mostrando o caminho de cálculo de mapeamento de estado](../../assets/State_Mapping_Path.png)

1. Quando terminar, clique em **[!UICONTROL Save]** para criar o caminho.
1. O caminho pode não ser preenchido imediatamente após salvar. Se isso acontecer, clique na caixa `Path` e selecione o caminho criado.
1. Clique em **[!UICONTROL Save]** para criar a coluna.

## O que eu faço agora? {#wrapup}

Depois que um ciclo de atualização for concluído, você poderá usar sua nova coluna unida para segmentar corretamente os dados em vez da coluna confusa do banco de dados. Olhe para suas opções de agrupamento agora - sem mais confusão de estresse:

![Gráfico mostrando segmentos de estado limpo após a padronização](../../assets/Clean_State_Segments.png)

As tabelas de mapeamento são úteis a qualquer momento em que você desejar limpar alguns dados potencialmente confusos na Data Warehouse. No entanto, as tabelas de mapeamento também podem ser usadas para alguns outros casos de uso interessantes, como [replicar seu [!DNL Google Analytics channels] em [!DNL Commerce Intelligence]](../data-warehouse-mgr/rep-google-analytics-channels.md).

### Relacionados

* [Entendendo e avaliando relações de tabelas](../data-warehouse-mgr/table-relationships.md)
* [Criação/exclusão de caminhos para colunas calculadas](../data-warehouse-mgr/create-paths-calc-columns.md)
