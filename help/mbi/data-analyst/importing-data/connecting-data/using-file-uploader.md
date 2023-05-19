---
title: Usar o carregador de arquivos
description: Saiba como colocar todos os seus dados em uma única Data Warehouse.
exl-id: 28db0e78-0222-431d-bbb9-6ef133686603
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 0%

---

# Usar o carregador de arquivos

>[!NOTE]
>
>Exige [Permissões de administrador](../../../administrator/user-management/user-management.md).

[!DNL Adobe Commerce Intelligence] O é eficiente não apenas por causa de seus recursos de visualização, mas também porque oferece a capacidade de colocar todos os seus dados em uma única Data Warehouse. Até mesmo dados que estão fora de seus bancos de dados e integrações podem ser trazidos para [!DNL Commerce Intelligence] usando a ferramenta Upload de arquivo no Gerenciador de Datas Warehouse.

Use campanhas publicitárias como exemplo. Se você estiver executando campanhas online e offline, não poderá obter o quadro completo se estiver analisando apenas dados de uma integração online. Fazer o upload de uma planilha com os dados de campanha offline permite analisar ambos os conjuntos de dados e obter uma compreensão mais robusta do desempenho da campanha.

## Restrições e requisitos {#require}

1. **O único formato compatível para uploads de arquivo é `CSV` ou`comma separated values`**. Se estiver trabalhando no Excel, você pode usar a função Salvar como para salvar o arquivo em `.csv` formato.
1. **`CSV`os arquivos devem usar`UTF-8 encoding`**. Na maioria das vezes, isso não é um problema. Se você encontrar esse erro ao fazer upload de um arquivo, [consulte este artigo de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/resolving-utf-8-errors-for-csv-file-uploads.html).
1. **Os arquivos não podem ter mais de 100 MB**. Se o arquivo for maior que isso, separe a tabela em partes e salve-as como arquivos individuais. Você pode anexar os dados depois que o arquivo inicial for carregado.
1. **Todas as tabelas devem ter um`primary key`**. Deve haver pelo menos uma coluna na tabela que possa ser usada como `primary key`ou um identificador exclusivo para cada linha na tabela. Qualquer coluna designada como `primary key` pode *nunca* ser nulo. A `primary key` pode ser tão simples quanto adicionar uma coluna que forneça um número para cada linha, ou pode ser duas colunas concatenadas para criar uma coluna de valores únicos (por exemplo, `campaign name` e `date`).

   Se uma coluna (ou colunas) for designada como exclusiva, mas houver duplicatas, as linhas duplicadas não serão importadas.

## Formatação de dados para upload {#formatting}

Antes de carregar seus dados no [!DNL Commerce Intelligence], verifique se está formatado de acordo com as diretrizes desta seção.

### Linha de cabeçalho {#header}

Para garantir que as colunas sejam rotuladas e importadas corretamente, verifique se a primeira linha da planilha é um cabeçalho que descreve os dados em cada coluna.

Os nomes das colunas devem ser exclusivos e conter apenas letras, números, espaços e estes símbolos: `$ % # /`. Se um nome de coluna contiver uma vírgula, ele será dividido em duas colunas quando o arquivo for carregado. Além disso, a Adobe recomenda que haja menos de 85 colunas no arquivo para otimizar a velocidade de atualização.

### Dados com vírgulas {#commas}

Porque os arquivos devem estar em `CSV` , o uso de vírgulas pode causar problemas com o upload de dados. `CSV` arquivos usam vírgulas para indicar novos valores, portanto, uma coluna com um nome como `Campaigns`, `August` é lida como duas colunas (`Campaigns` e `August`) em vez de um, movendo todos os seus dados em uma linha. Adobe recomenda evitar vírgulas sempre que possível. Você pode usar `Data Preview` para ver se os dados são exibidos corretamente após a conclusão de uma atualização.

### Datas

Qualquer conjunto de dados que inclua datas deve usar o [formato de data padrão](https://dev.mysql.com/doc/refman/5.7/en/datetime.html) `YYYY-MM-DD HH:MM:SS` ou `MM/DD/YYYY`.

### Caracteres especiais

Alguns caracteres especiais não são aceitos. Por exemplo, o símbolo de barra vertical `& # 1 2 4` é interpretado como a criação de uma coluna e causa erros ao fazer upload de um arquivo.

### Números Decimais

Os valores de moeda devem ter o tipo de dados `Decimal Number` selecionada e essas colunas são arredondadas automaticamente para duas casas decimais na Data Warehouse. Se você não quiser arredondar seus números decimais ou tiver um grau de precisão maior que este, você deve selecionar o `Non-Currency Decimal Number` tipo de dados.

### Porcentagens

As porcentagens devem ser inseridas como decimais. Por exemplo:

| **Direita:** | **Errado:** |
|-----|-----|
| `.05` | `5%` |
| `.23` | `23` |

{style="table-layout:auto"}

### Valores com zeros iniciais e/ou finais {#zeroes}

Alguns valores no arquivo, como códigos postais e IDs, podem começar ou terminar com zeros. Para garantir que os zeros sejam mantidos e carregados corretamente, é possível alterar o tipo de formatação (por exemplo, [do número ao texto](https://support.microsoft.com/en-us/office/format-numbers-as-text-583160db-936b-4e52-bdff-6f1863518ba4?ui=en-us&amp;rs=en-us&amp;ad=us)) ou impor a formatação de números.

Uso `US ZIP codes` como exemplo de como alterar a formatação numérica. Entrada [!DNL Excel], realce a coluna que contém `ZIP codes` e [alterar o formato do número](https://support.microsoft.com/en-us/office/display-numbers-as-postal-codes-61b55c9f-6fe3-4e54-96ca-9e85c38a5a1d?ui=en-us&amp;rs=en-us&amp;ad=us) para `ZIP code`. Também é possível selecionar um formato de número personalizado e, na guia `Type` janela, insira `00000`. Lembre-se que esse método pode apresentar problemas se alguns códigos forem formatados como `00000` e outros são `00000-0000`.

A variável `Type` pode ser [formatado de forma diferente para acomodar outros tipos de dados](https://support.microsoft.com/en-us/office/keeping-leading-zeros-and-large-numbers-1bf7b935-36e1-4985-842f-5dfa51f85fe7?correlationid=e1d4c2d3-cd5d-4a14-999d-437800274a90&amp;ui=en-us&amp;rs=en-us&amp;ad=us), como IDs. Se um `ID` tem nove dígitos, por exemplo, a variável `Type` poderia ser `000000000` ou `000-000-000`. Isso mudaria `123456` para `000-123-456`.

Para [!DNL Google Docs] e [!DNL Apple Numbers] recursos, consulte a seção [Relacionados](#related) na parte inferior desta página.

## Upload de dados {#uploading}

Agora que sua planilha está formatada corretamente e [!DNL Commerce Intelligence]-amigável, adicione-o à sua Data Warehouse.

1. Para começar, acesse **[!UICONTROL Data** > **File Uploads]**.

1. Clique em **[!UICONTROL Upload to New Table]** guia.

1. Clique em **[!UICONTROL Choose File]** e selecione o arquivo. Clique em **[!UICONTROL Open]** para iniciar o upload.

   Depois que o upload for concluído, uma lista das colunas [!DNL Commerce Intelligence] encontrado no seu arquivo é exibido.

1. Verifique se os nomes das colunas e os tipos de dados estão corretos. Especificamente, verifique se qualquer coluna de data está sendo lida como datas, não como números.

   >[!NOTE]
   >
   >A variável `datatype` é importante, portanto, não ignore esta etapa!

1. Selecione a(s) coluna(s) que compõe(m) o `primary key` para a tabela usando as caixas de seleção no ícone de chave.

1. Nomeie a tabela.

1. Clique em **[!UICONTROL Save Table]**.

A *Sucesso!* é exibida na parte superior da tela depois que a tabela é salva.

Se você precisar de um visual, observe todo o processo:

![](../../../assets/fileupload.gif)

As tabelas carregadas são exibidas sob o **Uploads de arquivo** seção da lista de tabelas (nas opções Todas as Tabelas e Tabelas Sincronizadas) no Gerenciador de Datas Warehouse:

![](../../../assets/upload-tables.png)

## Atualização ou anexação de dados a uma tabela existente {#appending}

Tem novos dados para adicionar a um arquivo que você já carregou? Sem problemas - você pode atualizar e anexar dados facilmente no [!DNL Commerce Intelligence].

1. Para começar, acesse **[!UICONTROL Manage Data** > **File Uploads]**.

1. Clique em **[!UICONTROL Edit/Upload `.csv`em Tabelas Existentes]** guia.

1. Na lista suspensa, clique no nome da tabela que deseja atualizar ou anexar.

1. Use a lista suspensa para selecionar a opção para manipular linhas duplicadas:

   | Opção | Descrição |
   |---|---|
   | `Overwrite old row with new row` | Isso substituirá os dados existentes pelos novos dados se uma linha tiver a mesma chave primária tanto na tabela existente quanto no novo arquivo. Este é o método a ser usado para colunas com valores que mudam com o tempo - por exemplo, uma coluna Status. Os dados existentes são substituídos e atualizados com os novos dados. Linhas com chaves primárias que não estão na tabela existente são adicionadas como novas linhas. |
   | `Retain old row; discard new row` | Isso faz com que os novos dados sejam ignorados se uma linha tiver a mesma chave primária tanto na tabela existente quanto no novo arquivo. |
   | `Purge all existing rows first and ignore duplicate keys within the file` | Isso exclui todos os dados existentes e os substitui pelos novos dados do arquivo. Use essa opção somente se não precisar dos dados na tabela existente. |

1. Clique em **[!UICONTROL Choose File]** e selecione o arquivo.

1. Clique em **[!UICONTROL Open]** para iniciar o upload.

   Após a conclusão do upload, [!DNL Commerce Intelligence] validará a estrutura de dados no arquivo. A *Sucesso!* é exibida na parte superior da tela depois que a tabela é salva.

## Disponibilidade de dados {#availability}

Assim como as colunas calculadas, os dados de uploads de arquivo ficam disponíveis após a conclusão do próximo ciclo de atualização. Se uma atualização estava em andamento durante o upload do arquivo, os dados não estarão disponíveis até após a próxima atualização. Depois que um ciclo de atualização for concluído, você poderá navegar até a `Data Preview` na Data Warehouse para garantir que o arquivo carregado corretamente e os dados sejam exibidos conforme esperado.

## Encapsulamento {#wrapup}

Este tópico abordou apenas as noções básicas de uso da importação de dados, mas convém fazer algo mais avançado. Confira os artigos relacionados para obter orientação sobre formatação e importação de dados financeiros, de comércio eletrônico e de gastos com anúncios, entre outros.

Além disso, o upload de arquivo não é a única maneira de obter seus dados no [!DNL Commerce Intelligence]. A variável [API de importação de dados](https://developer.adobe.com/commerce/services/reporting/import-api/) As funções do permitem enviar dados arbitrários para o [!DNL Commerce Intelligence] Data Warehouse.

## Relacionados {#related}

* [Formatação e importação de dados financeiros](../../../best-practices/format-import-financial-data.md)
* [Importação offline/outros dados de gastos com anúncios](../connecting-data/import-offline-ad-data.md)
* [Esperado[!DNL Google ECommerce] dados](../integrations/google-ecommerce-data.md)

## Recursos de terceiros

* [Guia de formatação de dados de números](http://www.dummies.com/how-to/content/how-to-choose-a-number-format-in-your-numbers-spre.html)
* [[!DNL Google Docs] Guia de formatação de dados](https://support.google.com/docs/answer/56470?hl=en)
