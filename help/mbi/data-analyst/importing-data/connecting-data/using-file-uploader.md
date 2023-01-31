---
title: Usar Upload de Arquivo
description: Saiba como colocar todos os seus dados em um único data warehouse.
exl-id: 28db0e78-0222-431d-bbb9-6ef133686603
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '1386'
ht-degree: 0%

---

# Usar Upload de Arquivo

>[!NOTE]
>
>Exige [Permissões de administrador](../../../administrator/user-management/user-management.md).

[!DNL MBI] O é poderoso não apenas por causa de seus recursos de visualização, mas porque oferece a capacidade de colocar todos os seus dados em um único data warehouse. Até mesmo os dados que estão fora de seus bancos de dados e integrações podem ser trazidos para [!DNL MBI] usando a ferramenta Upload de arquivo no Gerenciador de Datas Warehouse.

Vamos usar campanhas de publicidade como exemplo. Se você estiver executando campanhas online e offline, não será possível obter toda a imagem se estiver analisando apenas dados de uma integração online. Fazer upload de uma planilha com os dados da campanha offline permite analisar ambos os conjuntos de dados e obter uma compreensão mais robusta do desempenho da sua campanha.

## Restrições e requisitos {#require}

1. **O único formato compatível para uploads de arquivo é `CSV` ou`comma separated values`**. Se você estiver trabalhando no Excel, poderá usar a função Salvar como para salvar o arquivo no `.csv` formato.
1. **`CSV`os arquivos devem usar`UTF-8 encoding`**. Na maior parte do tempo, não se trata de uma questão. Se encontrar este erro ao carregar um arquivo, [consulte este artigo de suporte](https://support.magento.com/hc/en-us/articles/360016730591).
1. **Os arquivos não podem ter mais de 100 MB**. Se o arquivo for maior que isso, separe a tabela em partes e salve-a como arquivos individuais. Você pode usar Anexar os dados após o carregamento do arquivo inicial.
1. **Todas as tabelas devem ter uma`primary key`**. Deve haver pelo menos uma coluna na tabela que possa ser usada como `primary key`ou um identificador exclusivo para cada linha da tabela. Qualquer coluna designada como `primary key` can *never* ser nulo. A `primary key` pode ser tão simples quanto adicionar uma coluna que dê um número a cada linha, ou duas colunas podem ser concatenadas para criar uma coluna de valores únicos (por exemplo, `campaign name` e `date`).

   Se uma coluna (ou colunas) forem designadas como exclusivas, mas houver duplicatas, as linhas duplicadas não serão importadas.

## Formatação de dados para upload {#formatting}

Antes de fazer upload dos dados no [!DNL MBI], verifique se ele está formatado de acordo com as diretrizes desta seção.

### Linha de cabeçalho {#header}

Para garantir que as colunas sejam rotuladas e importadas corretamente, verifique se a primeira linha da planilha é um cabeçalho que descreve os dados em cada coluna.

Os nomes de colunas devem ser exclusivos e conter somente letras, números, espaços e estes símbolos: `$ % # /`. Se um nome de coluna contiver uma vírgula, ele será dividido em duas colunas quando o arquivo for carregado. Além disso, recomendamos que haja menos de 85 colunas no arquivo para otimizar a velocidade de atualização.

### Dados com vírgulas {#commas}

Porque os arquivos devem estar em `CSV` , o uso de vírgulas pode causar problemas com o upload de dados. `CSV` os arquivos usam vírgulas para indicar novos valores, portanto, uma coluna com um nome como `Campaigns`, `August` será lido como duas colunas (`Campaigns` e `August`) em vez de um, alterando todos os seus dados para uma linha. Recomendamos evitar vírgulas sempre que possível. Você pode usar `Data Preview` para ver se os dados são exibidos corretamente após a conclusão de uma atualização.

### Datas

Qualquer conjunto de dados que inclua datas deve usar a variável [formato de data padrão](https://dev.mysql.com/doc/refman/5.7/en/datetime.html) `YYYY-MM-DD HH:MM:SS` ou `MM/DD/YYYY`.

### Caracteres especiais

Alguns caracteres especiais não são aceitos. Por exemplo, o símbolo da barra vertical `& # 1 2 4` é interpretado como criando uma nova coluna e causará erros ao carregar um arquivo.

### Números decimais

Os valores de moeda devem ter o tipo de dados `Decimal Number` selecionado e essas colunas serão arredondadas automaticamente para duas casas decimais no data warehouse. Se você não quiser arredondar seus números decimais ou se tiver um grau de precisão maior que isso, selecione a opção `Non-Currency Decimal Number` tipo de dados.

### Porcentagens

As porcentagens devem ser inseridas como decimais. Por exemplo:

| **Direita:** | **Errado:** |
|-----|-----|
| `.05` | `5%` |
| `.23` | `23` |

{style=&quot;table-layout:auto&quot;}

### Valores com zeros à esquerda e/ou à direita {#zeroes}

Alguns valores no arquivo - como CEPs e IDs - podem começar ou terminar com zeros. Para garantir que os zeros sejam retidos e carregados corretamente, é possível alterar o tipo de formatação (por exemplo, [de número a texto](https://support.office.com/en-US/article/format-numbers-as-text-583160db-936b-4e52-bdff-6f1863518ba4)) ou impor a formatação de números.

Vamos usar `US ZIP codes` como exemplo de como alterar a formatação de números. Em [!DNL Excel], destaque a coluna que contém `ZIP codes` e [alterar o formato de número](https://support.office.com/en-za/article/Display-numbers-as-postal-codes-61b55c9f-6fe3-4e54-96ca-9e85c38a5a1d) para `ZIP code`. Você também pode selecionar um formato de número personalizado e, no `Type` janela , insira `00000`. Lembre-se que esse método pode causar problemas se alguns códigos forem formatados como `00000` e outros `00000-0000`.

O `Type` pode ser [formatada de forma diferente para acomodar outros tipos de dados](https://support.office.com/en-us/article/Keep-leading-zeros-in-number-codes-1bf7b935-36e1-4985-842f-5dfa51f85fe7?CorrelationId=e1d4c2d3-cd5d-4a14-999d-437800274a90&amp;ui=en-US&amp;rs=en-US&amp;ad=US), como IDs. Se uma `ID` tem nove dígitos, por exemplo, a variável `Type` poderia ser `000000000` ou `000-000-000`. Isso mudaria `123456` para `000-123-456`.

Para [!DNL Google Docs] e [!DNL Apple Numbers] recursos, consulte [Relacionado](#related) na parte inferior desta página.

## Upload de dados {#uploading}

Agora que sua planilha está formatada corretamente e [!DNL MBI]amigável, vamos adicioná-lo ao data warehouse.

1. Para começar, acesse **[!UICONTROL Data** > **File Uploads]**.

1. Clique no botão **[!UICONTROL Upload to New Table]** guia .

1. Clique em **[!UICONTROL Choose File]** e selecione o arquivo . Clique em **[!UICONTROL Open]** para iniciar o upload.

   Depois que o upload for concluído, você verá uma lista das colunas [!DNL MBI] encontrado no arquivo .

1. Verifique se os nomes das colunas e os tipos de dados estão corretos. Especificamente, verifique se qualquer coluna de data está sendo lida como datas e não como números.

   >[!NOTE]
   >
   >O `datatype` é extremamente importante, por isso não ignore este passo!

1. Selecione a coluna (ou colunas) que compõe a variável `primary key` para a tabela usando as caixas de seleção no ícone de chave .

1. Nomeie a tabela.

1. Clique em **[!UICONTROL Save Table]**.

A *Sucesso!* aparecerá na parte superior da tela depois que a tabela for salva.

Se você precisar de um visual, veja todo o processo:

![](../../../assets/fileupload.gif)

As tabelas carregadas são exibidas sob a **Uploads de arquivo** da lista da tabela (nas opções Todas as tabelas e Tabelas sincronizadas ) no Gerenciador de Datas Warehouse:

![](../../../assets/upload-tables.png)

## Atualização ou anexação de dados a uma tabela existente {#appending}

Tem novos dados para adicionar a um arquivo que já foi carregado? Nenhum problema - você pode atualizar e anexar dados facilmente em [!DNL MBI].

1. Para começar, acesse **[!UICONTROL Manage Data** > **File Uploads]**.

1. Clique no botão **[!UICONTROL Edit/Upload `.csv`para tabelas existentes]** guia .

1. Na lista suspensa, clique no nome da tabela que deseja atualizar ou anexar.

1. Use a lista suspensa para selecionar a opção para manipular linhas duplicadas:

   |  |  |
   |---|---|
   | `Overwrite old row with new row` | Isso substituirá os dados existentes por novos dados se uma linha tiver a mesma chave primária na tabela existente e no novo arquivo. Esse é o método a ser usado para colunas com valores que mudam ao longo do tempo - por exemplo, uma coluna Status . Os dados existentes serão substituídos e atualizados com os novos dados. As linhas com chaves primárias que não estiverem na tabela existente serão adicionadas como novas linhas. |
   | `Retain old row; discard new row` | Isso fará com que novos dados sejam ignorados se uma linha tiver a mesma chave primária na tabela existente e no novo arquivo. |
   | `Purge all existing rows first and ignore duplicate keys within the file` | Isso excluirá todos os dados existentes e os substituirá pelos novos dados do arquivo. Você só deve usar essa opção se não precisar de dados na tabela existente. |

1. Clique em **[!UICONTROL Choose File]** e selecione o arquivo .

1. Clique em **[!UICONTROL Open]** para iniciar o upload.

   Após a conclusão do upload, [!DNL MBI] O validará a estrutura de dados no arquivo. A *Sucesso!* aparecerá na parte superior da tela depois que a tabela for salva.

## Disponibilidade de dados {#availability}

Assim como as colunas calculadas, os dados dos uploads de arquivo estão disponíveis após a conclusão do próximo ciclo de atualização. Se uma atualização estava em andamento durante o upload do arquivo, os dados não estarão disponíveis até após a próxima atualização. Depois que um ciclo de atualização é concluído, você pode navegar para a variável `Data Preview` no data warehouse para garantir que o arquivo carregado corretamente e os dados estejam sendo exibidos conforme esperado.

## Quebra de linha {#wrapup}

Este artigo cobriu apenas os fundamentos para o uso de dados de importação, mas acreditamos que você queira fazer algo um pouco mais avançado. Consulte os artigos Relacionados para obter orientação sobre a formatação e importação de dados financeiros, de comércio eletrônico, gastos com anúncios e outros tipos de dados.

Além disso, o upload de arquivo não é a única maneira de inserir os dados [!DNL MBI]. O [API de importação de dados](https://developer.adobe.com/commerce/services/reporting/import-api/) permite que você envie dados arbitrários para seus [!DNL MBI] data warehouse.

## Relacionado {#related}

* [Formatação e importação de dados financeiros](../../../best-practices/format-import-financial-data.md)
* [Importação de dados offline e de outros gastos com anúncios](../connecting-data/import-offline-ad-data.md)
* [Esperado[!DNL Google ECommerce] dados](../integrations/google-ecommerce-data.md)

## Recursos de terceiros

* [Guia de formatação de dados de números](http://www.dummies.com/how-to/content/how-to-choose-a-number-format-in-your-numbers-spre.html)
* [[!DNL Google Docs] Guia de formatação de dados](https://support.google.com/docs/answer/56470?hl=en)
