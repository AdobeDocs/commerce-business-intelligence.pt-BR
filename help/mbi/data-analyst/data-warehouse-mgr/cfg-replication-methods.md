---
title: Configuração de métodos de replicação
description: Saiba como as tabelas são organizadas e como os dados da tabela se comportam permite escolher o melhor método de replicação para suas tabelas.
exl-id: 83895c48-a6ec-4b01-9890-164e0b21dcbc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Data Import/Export
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1433'
ht-degree: 0%

---

# Configuração de métodos de replicação

`Replication` métodos e [reverificações](../data-warehouse-mgr/cfg-data-rechecks.md) são usados para identificar dados novos ou atualizados nas tabelas do banco de dados. Configurar corretamente é fundamental para garantir a precisão dos dados e os tempos de atualização otimizados. Este tópico aborda os métodos de replicação.

Quando novas tabelas são sincronizadas no [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md), um método de replicação é escolhido automaticamente para a tabela. Compreender os vários métodos de replicação, como as tabelas são organizadas e como os dados da tabela se comportam permite escolher o melhor método de replicação para suas tabelas.

## Quais são os métodos de replicação?

Os métodos `Replication` se dividem em três grupos - `Incremental`, `Full Table` e `Paused`.

[**[!UICONTROL Incremental Replication]**](#incremental) significa que [!DNL Commerce Intelligence] replica somente dados novos ou atualizados em cada tentativa de replicação. Como esses métodos reduzem bastante a latência, a Adobe recomenda usá-la sempre que possível.

[**[!UICONTROL Full Table Replication]**](#fulltable) significa que [!DNL Commerce Intelligence] replica todo o conteúdo de uma tabela em cada tentativa de replicação. Devido à quantidade potencialmente grande de dados a serem replicados, esses métodos podem aumentar a latência e os tempos de atualização. Se uma tabela contiver colunas com carimbo de data e hora ou de data e hora, a Adobe recomenda usar um método Incremental.

**[!UICONTROL Paused]** indica que a replicação da tabela foi interrompida ou pausada. [!DNL Commerce Intelligence] não verifica se há dados novos ou atualizados durante um ciclo de atualização; isso significa que nenhum dado é replicado de uma tabela que tenha isso como seu Método de Replicação.

## Métodos de replicação incremental {#incremental}

### Modificado em (mais ideal)

O método de replicação `Modified At` usa uma coluna datetime - que é preenchida quando uma linha é criada e depois atualizada quando os dados são alterados - para encontrar os dados que serão replicados. Este método foi projetado para funcionar com tabelas que atendem aos seguintes critérios:

* contém uma coluna `datetime` que é preenchida inicialmente quando uma linha é criada e é atualizada sempre que a linha é modificada;
* a coluna `datetime` nunca é nula;
* as linhas não são excluídas da tabela

Além desses critérios, a Adobe recomenda a **indexação** da coluna `datetime` usada para a replicação `Modified At`, pois isso ajuda a otimizar a velocidade da replicação.

Quando a atualização é executada, dados novos ou alterados são identificados pela pesquisa de linhas com um valor na coluna `datetime` que ocorreram após a atualização mais recente. Quando novas linhas são descobertas, elas são replicadas para o Data Warehouse. Se houver linhas no [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md), elas serão substituídas pelos valores atuais do banco de dados.

Por exemplo, uma tabela pode ter uma coluna chamada `modified\_at` que indica a última vez que os dados foram alterados. Se a atualização mais recente for executada na terça-feira ao meio-dia, a atualização pesquisará todas as linhas com um valor de `modified\_at` maior que na terça-feira ao meio-dia. Todas as linhas descobertas que foram criadas ou modificadas desde o meio-dia da terça-feira são replicadas para o Data Warehouse.

**Você sabia?**
Mesmo que seu banco de dados não seja compatível com um método de Replicação `Incremental`, você poderá [fazer alterações no banco de dados](../../best-practices/mod-db-inc-replication.md) que permitiriam o uso de `Modified At` ou `Single Auto Incrementing PK`.

`Modified At` não é apenas o método de replicação mais ideal, é também o mais rápido. Esse método não apenas produz aumentos perceptíveis de velocidade com grandes conjuntos de dados, como também não requer a configuração de uma opção de reverificação. Outros métodos precisam iterar por meio de uma tabela inteira para identificar alterações, mesmo se um pequeno subconjunto de dados tiver sido alterado. `Modified At` repete somente através desse pequeno subconjunto.

### Chave primária de incrementação automática única

`Auto Incrementing` é um comportamento que atribui sequencialmente chaves primárias a linhas. Se uma tabela for `Auto Incrementing` e a chave primária mais alta for 1.000, o próximo valor primário será 1.001 ou superior. Uma tabela que não usa o comportamento `Auto Incrementing` pode atribuir um valor de chave primária menor que 1.000 ou saltar para um número muito maior, mas isso não é comumente usado.

Esse método foi projetado para replicar novos dados de tabelas que atendem aos seguintes critérios:

* `single-column primary key`; e
* O tipo de dados `primary key` é `integer`; e
* `auto incrementing` valores de chave primária.

Quando uma tabela está usando a replicação do `Single Auto Incrementing Primary Key`, novos dados são descobertos pela pesquisa de valores de chave primária maiores que o valor mais alto atual em sua Data Warehouse. Por exemplo, se o valor mais alto da chave primária no Data Warehouse for 500, na próxima atualização, ele pesquisará linhas com valores de chave primária de 501 ou superiores.

### Adicionar data

O método `Add Date` funciona de forma semelhante ao método `Single Auto Incrementing Primary Key`. Em vez de usar um número inteiro para a chave primária da tabela, esse método usa uma coluna `timestamped` para verificar se há novas linhas.

Quando uma tabela usa a replicação do `Add Date`, novos dados são descobertos pela pesquisa de valores com carimbo de data e hora maiores que a última data sincronizada com sua Data Warehouse. Por exemplo, se uma última atualização foi executada em 12/20/2015 em 09:00:00, quaisquer linhas com um carimbo de data e hora maior que este serão marcadas como novos dados e replicadas.

>[!NOTE]
>
>Ao contrário do método `Modified At`, `Add Date` não verifica se há linhas existentes para obter informações atualizadas - só aguarda novas linhas.

## Métodos de replicação de tabela completa {#fulltable}

### Tabela completa

A replicação `Full table` atualiza a tabela inteira sempre que novas linhas são detectadas. Esse é de longe o método de replicação menos eficiente, pois todos os dados devem ser reprocessados durante cada atualização, supondo que haja novas linhas.

Novas linhas são detectadas consultando o banco de dados no início do processo de sincronização e contando o número de linhas. Se o banco de dados local contiver mais linhas do que [!DNL Commerce Intelligence], a tabela será atualizada. Se as contagens de linhas forem idênticas ou se [!DNL Commerce Intelligence] contiver *mais* linhas do que o banco de dados local, a tabela será ignorada.

Isso gera o ponto importante de que a replicação **`Full Table`é incompatível quando:**

* mais linhas são excluídas do que criadas na tabela do banco de dados local entre os ciclos de atualização subsequentes, ou
* os valores da coluna são alterados, mas nenhuma linha adicional é criada

Em qualquer um dos cenários acima, a replicação do `Full Table` não detecta nenhuma alteração e seus dados tornam-se obsoletos. Devido à ineficiência deste método de replicação e aos requisitos mencionados acima, a replicação `Full Table` é recomendada somente como último recurso.

### Lote da chave primária

Quando uma tabela usa `Primary Key Batch` (Lote PK), novos dados são descobertos pela contagem de linhas dentro de intervalos, ou lotes, de valores de chave primária. Enquanto você normalmente pensa que isso está sendo usado com inteiros, até mesmo valores de texto podem ser ordenados de uma maneira que permite que o sistema defina intervalos constantes.

Por exemplo, digamos que uma atualização seja executada e execute uma contagem de linhas para o intervalo de chaves de 1 a 100. Nesta atualização, o sistema encontra e registra 37 linhas. Na próxima atualização, uma contagem de linhas é executada novamente no intervalo de 1 a 100 e encontra 41 linhas. Como há uma diferença no número de linhas em comparação à última atualização, o sistema inspeciona esse intervalo (ou lote) com mais detalhes.

Este método tem como objetivo replicar dados de tabelas que atendem aos seguintes critérios:

* não inteiro de coluna única; ou
* chaves compostas (várias colunas que compõem a chave primária): observe que as colunas usadas em uma chave primária composta nunca podem ter valores nulos; ou
* valores de chave primária de coluna única, inteiros, sem incremento automático.

Esse método não é ideal, pois é incrivelmente lento devido à quantidade de processamento que deve ocorrer para examinar os lotes e encontrar alterações. A Adobe recomenda não usar esse método, a menos que seja impossível fazer as modificações necessárias para dar suporte aos outros métodos de replicação. Espere que os tempos de atualização aumentem se esse método precisar ser usado.

## Configuração de métodos de replicação

Os métodos de replicação são definidos tabela por tabela. Para definir um método de replicação para uma tabela, você precisa de [`Admin`](../../administrator/user-management/user-management.md) permissões para acessar o Data Warehouse Manager.

1. No Data Warehouse Manager, selecione a tabela na lista `Synced Tables` para exibir o esquema da tabela.
1. O método de replicação atual está listado abaixo do nome da tabela. Para alterá-lo, clique no link.
1. Na janela pop-up exibida, clique no botão de opção ao lado da replicação `Incremental` ou `Full Table` para selecionar um tipo de replicação.
1. Em seguida, clique na lista suspensa **[!UICONTROL Replication Method]** para selecionar um método. Por exemplo, `Paused` ou `Modified At`.

   >[!NOTE]
   >
   >**Alguns métodos incrementais exigem que você defina um`Replication Key`**. O [!DNL Commerce Intelligence] usará essa chave para determinar onde o próximo ciclo de atualização deve começar.
   >
   >Por exemplo, se você deseja usar o método `modified at` para a tabela `orders`, é necessário definir um `date column` como a chave de replicação. Várias opções para chaves de replicação podem existir, mas você seleciona `created at` ou a hora em que o pedido foi criado. Se o último ciclo de atualização parasse em 01/12/2015 00:10:00, o próximo ciclo começaria a replicar dados com uma data `created at` maior que esta.

1. Quando terminar, clique em **[!UICONTROL Save]**.

Analise todo o processo:

![](../../assets/replication_method.gif)<!--{: width="801" height="341"}-->

## Encapsulamento

Para finalizar, você juntou essa tabela que compara os vários métodos de replicação. É incrivelmente útil ao selecionar um método para as tabelas no Data Warehouse.

| **`Method`** | **`Syncing New Data`** | **`Processing Rechecks on Large Data Sets`** | **`Handle Composite Keys?`** | **`Handle Non-Integer PKs?`** | **`Handle Non-Sequential PK Population?`** | **`Handle Row Deletion?`** |
|-----|-----|-----|-----|-----|-----|-----|
| `Auto-Incrementing Primary Key` | Mais rápido | Lento | Não | Não | Não | Sim |
| `Primary Key Batch Monitoring` | Lento | Lento | Sim | Sim | Sim | Sim |
| `Modified At` | Mais rápido | Mais rápido | Sim | Sim | Sim | Não |

{style="table-layout:auto"}

## Documentação relacionada

* [Noções básicas sobre reverificações de dados](../data-warehouse-mgr/cfg-data-rechecks.md)
* [Modificação do banco de dados para oferecer suporte ](../../best-practices/mod-db-inc-replication.md)
* [Otimização do banco de dados para análise](../../best-practices/opt-db-analysis.md)
* [Redução dos tempos de atualização](../../best-practices/reduce-update-cycle-time.md)
