---
title: Configuração de métodos de replicação
description: Saiba como as tabelas são organizadas e como os dados da tabela se comportam permitirá escolher o melhor método de replicação para as tabelas.
exl-id: 83895c48-a6ec-4b01-9890-164e0b21dcbc
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1455'
ht-degree: 0%

---

# Configuração de métodos de replicação

`Replication` métodos e [verificações](../data-warehouse-mgr/cfg-data-rechecks.md) são usados para identificar dados novos ou atualizados nas tabelas do banco de dados. A configuração correta dos dados é fundamental para garantir a precisão dos dados e o tempo de atualização otimizado. Neste artigo, nos concentraremos apenas nos métodos de replicação.

Quando novas tabelas são sincronizadas no Gerenciador de Datas Warehouse, um método de replicação é escolhido automaticamente para a tabela. Entendendo os vários métodos de replicação, como as tabelas são organizadas e como os dados da tabela se comportam permitirá escolher o melhor método de replicação para as tabelas.

## Quais são os métodos de replicação?

`Replication` os métodos são em três grupos - `Incremental`, `Full Table`e `Paused`.

[**[!UICONTROL Incremental Replication]**](#incremental) significa que [!DNL MBI] replicará somente dados novos ou atualizados em cada tentativa de replicação. Como esses métodos reduzirão bastante a latência, recomendamos usá-la sempre que possível.

[**[!UICONTROL Full Table Replication]**](#fulltable) significa que [!DNL MBI] replicará todo o conteúdo de uma tabela em cada tentativa de replicação. Devido à quantidade potencialmente grande de dados a serem replicados, esses métodos podem aumentar a latência e os tempos de atualização. Se uma tabela contém qualquer coluna com ou sem carimbos de data e hora, recomendamos usar um método Incremental em vez disso.

**[!UICONTROL Paused]** indica que a replicação da tabela está interrompida ou pausada. [!DNL MBI] não verificará dados novos ou atualizados durante um ciclo de atualização; isso significa que nenhum dado será replicado de uma tabela que tenha isso como seu Método de Replicação.

## Métodos de replicação incremental {#incremental}

### Modificado em (mais ideal)

O `Modified At` o método de replicação usa uma coluna datetime - que é preenchida quando uma linha é criada e atualizada quando os dados são alterados - para localizar dados a serem replicados. Esse método foi projetado para funcionar com tabelas que atendam aos seguintes critérios:

* contém um `datetime` coluna que é inicialmente preenchida quando uma linha é criada e atualizada sempre que a linha é modificada;
* o `datetime` coluna nunca é nula;
* linhas não são excluídas da tabela

Além desses critérios, recomendamos também que **indexação** o `datetime` coluna usada para `Modified At` replicação, pois isso ajudará a otimizar a velocidade de replicação.

Quando a atualização é executada, os dados novos ou alterados são identificados procurando por linhas que tenham um valor na variável `datetime` coluna que ocorreu após a atualização mais recente. Quando novas linhas são descobertas, elas são replicadas na Data Warehouse. Se já houver linhas na Data Warehouse, elas serão substituídas pelos valores atuais do banco de dados.

Por exemplo, uma tabela pode ter uma coluna chamada `modified\_at` que indica a última vez que os dados foram alterados. Se a atualização mais recente tiver sido executada terça-feira ao meio-dia, a atualização pesquisará todas as linhas que tiverem uma `modified\_at` maior que terça-feira ao meio-dia. Todas as linhas descobertas que foram criadas ou modificadas desde a terça-feira ao meio-dia serão replicadas para a Data Warehouse.

**Você sabia?**
Mesmo que o banco de dados não possa suportar um `Incremental` Método de replicação, talvez seja possível [fazer algumas alterações no banco de dados](../../best-practices/mod-db-inc-replication.md) que permitiria utilizar `Modified At` ou `Single Auto Incrementing PK`.

`Modified At` não é apenas o método de replicação mais ideal, é também o mais rápido. Esse método não produz apenas aumentos de velocidade perceptíveis com grandes conjuntos de dados, mas também não requer a configuração de uma opção de reverificação. Outros métodos precisarão repetir em uma tabela inteira para identificar as alterações, mesmo se um pequeno subconjunto de dados tiver sido alterado. `Modified At` repete somente esse pequeno subconjunto.

### Chave primária de incremento automático único

`Auto Incrementing` é um comportamento que atribui sequencialmente as chaves primárias a linhas. Se uma tabela for `Auto Incrementing` e a chave primária mais alta na tabela é atualmente 1000, então o próximo valor primário será 1001 ou superior. Uma tabela que não usa `Auto Incrementing` O comportamento pode atribuir um valor de chave primária menor que 1000 ou saltar para um número muito maior, mas isso não é comumente usado.

Esse método é projetado para replicar novos dados de tabelas que atendem aos seguintes critérios:

* `single-column primary key`; e
* `primary key` o tipo de dados é `integer`; e
* `auto incrementing` valores da chave primária.

Quando uma tabela está usando `Single Auto Incrementing Primary Key` Na replicação, novos dados são descobertos pela pesquisa por valores de chave primária que são maiores que o valor mais alto atual em sua Data Warehouse. Por exemplo, se o valor mais alto da chave primária na sua Data Warehouse for 500, quando a próxima atualização for executada, ela pesquisará linhas com valores da chave primária de 501 ou superior.

### Adicionar data

O `Add Date` O método funciona de forma semelhante à `Single Auto Incrementing Primary Key` método . Em vez de usar um número inteiro para a chave primária da tabela, este método usará um `timestamped` coluna para verificar novas linhas.

Quando uma tabela usa `Add Date` Na replicação, novos dados são descobertos pela pesquisa por valores com carimbo de data e hora que são maiores que a data mais recente sincronizada com sua Data Warehouse. Por exemplo, se uma atualização foi executada pela última vez em 12/2015 09:00:00, qualquer linha com um carimbo de data e hora maior que isso será marcada como novos dados e replicada.

>[!NOTE]
>
>Ao contrário do `Modified At` método , `Add Date` não verificará as linhas existentes para obter informações atualizadas. Ele só aguardará as novas linhas.

## Métodos de replicação de tabela completa {#fulltable}

### Tabela completa

`Full table` a replicação atualiza a tabela inteira sempre que novas linhas são detectadas. Esse é de longe o método de replicação menos eficiente, devido ao fato de que todos os dados devem ser reprocessados durante cada atualização, supondo que haja novas linhas.

Novas linhas são detectadas consultando o banco de dados no início do processo de sincronização e contando o número de linhas. Se o banco de dados local contiver mais linhas do que [!DNL MBI], a tabela é atualizada. Se as contagens de linha forem idênticas, ou se [!DNL MBI] contém *more* linhas do que o banco de dados local, a tabela é ignorada.

Isto levanta a questão importante de que **`Full Table`a replicação é incompatível quando:**

* mais linhas são excluídas do que as criadas na tabela de banco de dados local entre ciclos de atualização subsequentes, ou
* os valores da coluna são alterados, mas nenhuma linha adicional é criada

Em qualquer um dos cenários acima, `Full Table` a replicação não detectará alterações e seus dados ficarão obsoletos. Devido à ineficiência deste método de replicação e aos requisitos acima mencionados, `Full Table` a replicação é recomendada somente como último recurso.

### Lote de chaves primárias

Quando uma tabela usa `Primary Key Batch` (Lote de PK), novos dados são descobertos pela contagem de linhas dentro de intervalos, ou lotes, de valores principais. Embora normalmente pensemos que isso é usado com números inteiros, até mesmo valores de texto podem ser ordenados de uma maneira que permite que o sistema defina intervalos constantes.

Por exemplo, Digamos que uma atualização seja executada e execute uma contagem de linhas para o intervalo de chaves de 1 a 100. Nesta atualização, o sistema encontra e registra 37 linhas. Na próxima atualização, uma contagem de linhas é executada novamente no intervalo de 1 a 100 e encontra 41 linhas. Como há uma diferença no número de linhas em comparação à última atualização, o sistema inspecionará esse intervalo (ou lote) com mais detalhes.

Este método destina-se a replicar dados de tabelas que atendem aos seguintes critérios:

* não-inteiro de coluna única; ou
* chaves compostas (várias colunas incluindo a chave primária) - observe que as colunas usadas em uma chave primária composta nunca podem ter valores nulos; ou
* coluna única, número inteiro, não incrementando automaticamente os valores da chave primária.

Esse método não é ideal, pois é incrivelmente lento devido à quantidade de processamento que deve ocorrer para examinar os lotes e encontrar alterações. Não recomendamos usar esse método a menos que não seja possível fazer as modificações necessárias para suportar os outros métodos de replicação. Esperar que os tempos de atualização aumentem se esse método precisar ser usado.

## Configuração de métodos de replicação

Os métodos de replicação são definidos tabela a tabela. Para definir um método de replicação para uma tabela, é necessário [`Admin`](../../administrator/user-management/user-management.md) para que você possa acessar o Gerenciador de Datas Warehouse.

1. Uma vez no Gerenciador de Datas Warehouse, selecione a tabela no `Synced Tables` para exibir o schema da tabela.
1. O método de replicação atual está listado abaixo do nome da tabela. Para alterá-lo, clique no link .
1. Na janela pop-up exibida, clique no botão de opção ao lado de `Incremental` ou `Full Table` replicação para selecionar um tipo de replicação.
1. Em seguida, clique no botão **[!UICONTROL Replication Method]** lista suspensa para selecionar um método - por exemplo, `Paused` ou `Modified At`.

   >[!NOTE]
   >
   >**Alguns métodos incrementais exigem que você defina uma`Replication Key`**. [!DNL MBI] O usará essa chave para determinar onde o próximo ciclo de atualização deve começar.
   >
   >Por exemplo, se queremos usar a variável `modified at` para nosso `orders` , precisamos definir uma `date column` como a chave de replicação. Várias opções para chaves de replicação podem existir, mas nós selecionaremos `created at`ou a hora em que o pedido foi criado. Se o último ciclo de atualização parou em 12/1/2015 00:10:00, o próximo ciclo começaria a replicar dados com um `created at` data maior que essa.

1. Quando terminar, clique em **[!UICONTROL Save]**.

Dê uma olhada em todo o processo:

![](../../assets/replication_method.gif)<!--{: width="801" height="341"}-->

## Quebra de linha

Para finalizar, montamos essa tabela que compara os vários métodos de replicação. Achamos incrivelmente útil ao selecionar um método para as tabelas em nosso data warehouse.

| **`Method`** | **`Syncing New Data`** | **`Processing Rechecks on Large Data Sets`** | **`Handle Composite Keys?`** | **`Handle Non-Integer PKs?`** | **`Handle Non-Sequential PK Population?`** | **`Handle Row Deletion?`** |
|-----|-----|-----|-----|-----|-----|-----|
| `Auto-Incrementing Primary Key` | Mais rápido | Lento | Não | Não | Não | Sim |
| `Primary Key Batch Monitoring` | Lento | Lento | Sim | Sim | Sim | Sim |
| `Modified At` | Mais rápido | Mais rápido | Sim | Sim | Sim | Não |

{style=&quot;table-layout:auto&quot;}

## Documentação relacionada

* [Noções básicas sobre reverificações de dados](../data-warehouse-mgr/cfg-data-rechecks.md)
* [Modificação do banco de dados para oferecer suporte ao ](../../best-practices/mod-db-inc-replication.md)
* [Otimização do banco de dados para análise](../../best-practices/opt-db-analysis.md)
* [Redução dos tempos de atualização](../../best-practices/reduce-update-cycle-time.md)
