---
title: Gerenciador de Datas Warehouse
description: Saiba como gerenciar configurações de sincronização de tabela e coluna, detalhar um esquema de tabela e criar colunas calculadas para usar em relatórios.
exl-id: b9577919-0db0-47f1-a426-1abe48443ac0
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 0%

---

# Gerenciador de Datas Warehouse

>[!NOTE]
>
>Exige [Permissões de administrador](../../administrator/user-management/user-management.md)

O Gerenciador de Datas Warehouse, acessado clicando em **[!UICONTROL Manage Data > Data Warehouse]** na barra lateral, é o portal para seu [!DNL MBI] Data Warehouse. Usando o Gerenciador de Datas Warehouse, é possível gerenciar configurações de sincronização de tabela e coluna, detalhar o esquema de uma tabela e criar colunas calculadas a serem usadas nos relatórios.

Neste artigo, cobriremos:

* [Aprenda o caminho](#learning)
* [Sincronização de tabelas e colunas](#syncing)
* [Criação de colunas calculadas](#calculated)
* [Eliminar tabelas e remover colunas](#delete)
* [Sincronização de novas tabelas em segundo plano](#syncnew)
* [Então, quando posso usar minhas novas colunas?](#when)

## Aprenda o caminho {#learning}

O lado esquerdo do `Data Warehouse Manager` contém a lista de tabelas, permitindo alternar facilmente entre tabelas. Quando uma tabela é selecionada na lista, a área de gerenciamento de tabela é preenchida com o schema da tabela, onde é possível fazer alterações na tabela selecionada.

Na lista da tabela, as tabelas são agrupadas por sua fonte de conexão. Essas fontes são adicionadas em [!UICONTROL Manage Data > Integrations] e pode ser um banco de dados, um [API](https://developer.adobe.com/commerce/services/reporting/)ou um conector de terceiros. Na parte superior da lista da tabela, há uma caixa de pesquisa que permite localizar facilmente as tabelas desejadas.

Abaixo da caixa de pesquisa, você verá duas opções: `All Tables` e `Synced Tables`. O `All Tables` lista todas as tabelas que você disponibilizou para sua Data Warehouse, que inclui tabelas sincronizadas e não sincronizadas.

O `Synced Tables` mostra todas as tabelas que já foram adicionadas à Data Warehouse e têm dados sendo replicados das colunas selecionadas.

Não visualize a tabela que você está procurando no `All Tables` lista? Há algumas razões possíveis para isso:

* A fonte de dados ainda não foi adicionada
* A fonte de dados é um banco de dados e a variável [!DNL MBI] o usuário criado não tem acesso. Nesse caso, você ou o administrador do banco de dados precisarão conceder acesso.
* A fonte de dados ou tabela foi adicionada recentemente e ainda não foi sincronizada

## Sincronização de tabelas e colunas {#syncing}

### Sincronização de novas tabelas e colunas nativas

O Gerenciador de Datas Warehouse não somente lhe dá a capacidade de visualizar e gerenciar facilmente suas fontes de dados, como também tem a liberdade de selecionar as tabelas e colunas individuais que deseja sincronizar.

1. Clique no botão `All Tables` e localize a tabela que deseja sincronizar.
1. Clique no nome da tabela para visualizar o schema. Se a tabela for nova, todas as colunas serão exibidas como `Unsynced`.
1. Verifique as colunas que deseja sincronizar.

   >[!NOTE]
   >
   >As colunas nativas de uma tabela terão do seu banco de dados na `Location` coluna.

1. Verifique a `Primary Key` colunas - essas colunas têm um símbolo de chave ao lado do nome da coluna. A `Primary Key` é necessária para sincronizar corretamente os dados na Data Warehouse.

   Se estiver sincronizando uma tabela que vem diretamente do seu banco de dados, é possível que `Primary Keys` não pode ser denotado. Nesse caso, entre em contato com o administrador do banco de dados para solicitar que uma chave primária ou chaves sejam adicionadas à tabela.
1. Quando terminar, clique no botão ![botão](../../assets/button.png) botão.

A *Sucesso!* será exibida e o status será alterado para `Pending` para as colunas selecionadas. Depois que a próxima atualização completa for concluída, as tabelas e colunas sincronizadas recentemente estarão disponíveis para uso nos relatórios; você também pode definir novos [métodos de replicação](./cfg-replication-methods.md) após a sincronização inicial.

Veja a seguir uma rápida visão de todo o processo:

![Adicionar colunas ao data warehouse](../../assets/DW_sync.gif)

### Sincronização de novas tabelas no plano de fundo {#syncnew}

Quando você sincroniza uma tabela grande e nova pela primeira vez, o data warehouse precisa capturar retroativamente todos os pontos de dados na tabela antes de capturar novos dados continuamente. Se a tabela for particularmente grande, talvez você não queira que a sincronização inicial seja executada em sequência com sua **ciclo de atualização** — em uma situação, você desejará que a sincronização inicial ocorra em segundo plano, em *paralelo* com qualquer atualização em execução no momento.

Para garantir que isso ocorra, você deve selecionar a variável `Save and Sync Data Immediately` opção sincronizando essa tabela pela primeira vez.

### Verificando novas tabelas e colunas {#forceupdate}

Sua Data Warehouse não detecta automaticamente novas fontes, tabelas ou colunas no momento em que são adicionadas. Um processo de sincronização é executado durante a semana para localizar novas adições e disponibilizá-las, mas é possível forçar uma sincronização de estrutura se você quiser acessar tabelas e colunas recém-adicionadas antes que o processo seja executado.

Abaixo da barra de pesquisa na lista da tabela há um `Check for new tables and columns` link . Clicar neste link forçará o início do processo de sincronização de estrutura; novas adições normalmente estão disponíveis após 10 minutos. Atualize a página para ver a nova fonte, tabela ou coluna.

## Criação de colunas calculadas {#calculated}

Simplesmente poder ver e gerenciar dados de todas as suas fontes facilita muito a obtenção de insights em sua empresa. Mas no Gerenciador de Datas Warehouse, você pode ir um passo além criando colunas calculadas dentro das tabelas. `Calculated` derivar novas informações dos dados existentes.

Digamos que você queira adicionar `user's lifetime revenue` para `users` tabela para localizar usuários de alto valor. Ou, se desejar segmentar a receita por gênero, é possível adicionar `customer's gender` para `orders` tabela.

Para ajudá-lo a criar essas colunas principais, [criamos um tutorial](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md) para te guiar por isso.

## Eliminando Tabelas e Removendo Colunas {#delete}

Assim como você tem a capacidade de selecionar tabelas e colunas para sincronizar com sua Data Warehouse, você também pode soltá-las ou removê-las.

>[!NOTE]
>
>Soltar uma tabela ou remover colunas excluirá quaisquer relatórios, métricas, conjuntos de filtros e colunas dependentes após confirmar a exclusão. Certifique-se de que deseja fazer isso - **esta ação não pode ser desfeita.**

Não se preocupe se clicar em **[!UICONTROL Delete]** por acidente. Uma verificação de dependência é executada antes de qualquer item ser excluído, portanto, você terá a chance de revisar tudo antes de confirmar.

Para remover colunas, clique na tabela à qual a coluna pertence. Verifique as colunas que deseja remover e clique no botão ![button\_1.png](../../assets/button_1.png) botão.

Para remover uma tabela sincronizada, selecione todas as colunas na tabela e clique novamente no ![botão](../../assets/button_1.png) botão. Isso removerá todas as colunas nativas e calculadas que usam essa tabela do data warehouse.

### Confirmação de alterações

Se você estiver soltando uma tabela ou removendo colunas, uma verificação de dependência será executada antes da conclusão do processo de exclusão. As dependências são colunas calculadas, métricas, conjuntos de filtros e relatórios que utilizam a tabela ou as colunas que estão sendo removidas. Quaisquer dependências descobertas serão exibidas - neste ponto, você pode cancelar o processo ou clicar em **[!UICONTROL Confirm Changes]** para soltar a tabela/remover a(s) coluna(s).

Embora as dependências excluídas não possam ser restauradas, as tabelas e colunas ainda estarão disponíveis se você precisar sincronizar novamente qualquer coluna nativa no futuro.

Veja a seguir uma visão rápida da remoção de uma coluna:

![Remoção de uma coluna do data warehouse](../../assets/DW_delete.gif)

## Então, quando posso usar minhas novas colunas? {#when}

Novas colunas sincronizadas e colunas calculadas novas/atualizadas estarão prontas para uso após a conclusão da próxima atualização completa. Se uma atualização ainda não estiver em andamento, é possível forçar uma atualização clicando em **[!UICONTROL Force update]** exibido na parte superior do `Data Warehouse` ou `Integrations` página. Você também pode agendar uma notificação por email após a conclusão da atualização clicando em **[!UICONTROL Email me when complete]**.

Quando estiver pronto para usar suas novas colunas em relatórios, [você precisa adicioná-las às métricas primeiro](../data-warehouse-mgr/manage-data-dimensions-metrics.md). Embora os dados não estejam disponíveis até que uma atualização seja concluída, você ainda pode usar novas colunas nos relatórios. Os dados no relatório serão exibidos quando a atualização for concluída.

## É isso - estamos no fim!

Nós cobrimos muito material neste tutorial. Por enquanto, você deve ter uma sólida compreensão do que é um banco de dados, como os dados são organizados, como as tabelas se relacionam umas às outras e o que pode fazer com o Gerenciador de Datas Warehouse.

Excelente! Faça testes em seu novo conhecimento [criação de uma coluna calculada](../data-warehouse-mgr/creating-calculated-columns.md) ou [fazendo alguns relatórios interessantes](../../tutorials/using-visual-report-builder.md).
