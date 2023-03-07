---
title: Gerenciador de Data Warehouse
description: Saiba como gerenciar configurações de sincronização de tabela e coluna, detalhar um esquema de tabela e criar colunas calculadas para usar em relatórios.
exl-id: b9577919-0db0-47f1-a426-1abe48443ac0
source-git-commit: 8de036e2717aedef95a8bb908898fd9b9bc9c3fa
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 0%

---

# Gerenciador de Data Warehouse

>[!NOTE]
>
>Exige [Permissões de administrador](../../administrator/user-management/user-management.md)

O Gerenciador de Datas Warehouse, acessado ao clicar em **[!UICONTROL Manage Data > Data Warehouse]** na barra lateral, é o portal para o seu [!DNL MBI] Data Warehouse. Usando o Gerenciador de Data Warehouse, você pode gerenciar configurações de sincronização de tabela e coluna, detalhar um esquema de tabela e criar colunas calculadas para usar em relatórios.

Este artigo abrange:

* [Aprendendo o seu caminho](#learning)
* [Sincronização de tabelas e colunas](#syncing)
* [Criação de colunas calculadas](#calculated)
* [Eliminando tabelas e removendo colunas](#delete)
* [Sincronização de novas tabelas em segundo plano](#syncnew)
* [Então, quando posso usar minhas novas colunas?](#when)

## Aprendendo o seu caminho {#learning}

O lado esquerdo de `Data Warehouse Manager` contém a lista de tabelas, permitindo que você alterne facilmente entre tabelas. Quando você seleciona uma tabela na lista, a área de gerenciamento de tabela é preenchida com o schema da tabela, onde você pode modificar a tabela selecionada.

Na lista de tabelas, as tabelas são agrupadas por sua origem de conexão. Essas fontes são adicionadas em [!UICONTROL Manage Data > Integrations] e pode ser um banco de dados, um [API](https://developer.adobe.com/commerce/services/reporting/)ou um conector de terceiros. Na parte superior da lista de tabelas, há uma caixa de pesquisa que permite localizar facilmente as tabelas desejadas.

Abaixo da caixa de pesquisa, você verá duas opções: `All Tables` e `Synced Tables`. A variável `All Tables` A opção lista todas as tabelas disponibilizadas para a Data Warehouse, que inclui tabelas sincronizadas e não sincronizadas.

A variável `Synced Tables` A opção mostra todas as tabelas que já foram adicionadas à Data Warehouse e cujos dados estão sendo replicados das colunas selecionadas.

Não veja a tabela que você está procurando na `All Tables` lista? Há algumas razões possíveis para isso:

* A fonte de dados ainda não foi adicionada
* A fonte de dados é um banco de [!DNL MBI] que você criou não tem acesso. Nesse caso, você ou o administrador do banco de dados deve conceder acesso.
* A fonte de dados ou tabela foi adicionada recentemente e ainda não foi sincronizada

## Sincronização de tabelas e colunas {#syncing}

### Sincronizando Novas Tabelas e Colunas Nativas

O Gerenciador de Datas Warehouse não só oferece a capacidade de visualizar e gerenciar facilmente suas fontes de dados, como também tem a liberdade de selecionar as tabelas e colunas individuais que deseja sincronizar.

1. Clique em `All Tables` e localize a tabela que deseja sincronizar.
1. Clique no nome da tabela para visualizar o schema. Se a tabela for nova, todas as colunas serão exibidas como `Unsynced`.
1. Marque as colunas que deseja sincronizar.

   >[!NOTE]
   >
   >As colunas nativas de uma tabela têm Do seu banco de dados na `Location` coluna.

1. Verifique o `Primary Key` colunas - essas colunas têm um símbolo de chave ao lado do nome da coluna. A `Primary Key` O é necessário para sincronizar dados corretamente na Data Warehouse.

   Se você estiver sincronizando uma tabela que vem diretamente do seu banco de dados, é possível que `Primary Keys` não podem ser indicadas. Nesse caso, entre em contato com o administrador do banco de dados para solicitar que uma ou mais chaves primárias sejam adicionadas à tabela.
1. Quando terminar, clique no botão ![botão](../../assets/button.png) botão.

A *Sucesso!* será exibida e o status será alterado para `Pending` para as colunas selecionadas. Depois que a próxima atualização completa for concluída, as tabelas e colunas recém-sincronizadas estarão disponíveis para uso nos relatórios. Você também pode definir novas [métodos de replicação](./cfg-replication-methods.md) após a sincronização inicial.

Aqui está uma rápida visão de todo o processo:

![Adicionar colunas ao data warehouse](../../assets/DW_sync.gif)

### Sincronizando Novas Tabelas em Segundo Plano {#syncnew}

Quando você sincroniza uma tabela grande pela primeira vez, sua Data Warehouse precisa capturar retroativamente todos os pontos de dados na tabela antes de capturar novos dados de forma contínua. Se a tabela for grande, talvez você não queira que essa sincronização inicial seja executada em sequência com a **ciclo de atualização**. Nessa situação, você deseja que a sincronização inicial ocorra em segundo plano, no *paralelo* com qualquer atualização em execução.

Para garantir que isso ocorra, selecione o `Save and Sync Data Immediately` opção que sincroniza essa tabela pela primeira vez.

### Verificação de novas tabelas e colunas {#forceupdate}

Sua Data Warehouse não detecta automaticamente novas fontes, tabelas ou colunas no momento em que são adicionadas. Um processo de sincronização é executado durante toda a semana para localizar novas adições e disponibilizá-las, mas você pode forçar uma sincronização de estrutura se quiser acessar tabelas e colunas recém-adicionadas antes que o processo seja executado.

Abaixo da barra de pesquisa na lista de tabelas há uma `Check for new tables and columns` link. Clicar nesse link forçará o início do processo de sincronização de estrutura; normalmente, novas adições estão disponíveis após 10 minutos. Atualize a página para ver a nova fonte, tabela ou coluna.

## Criação de Colunas Calculadas {#calculated}

Simplesmente ser capaz de ver e gerenciar dados de todas as fontes torna muito mais fácil obter insights sobre os negócios. Mas, no Gerenciador de Datas Warehouse, você pode ir além criando colunas calculadas dentro das tabelas. `Calculated` As colunas derivam novas informações dos dados existentes.

Diga que deseja adicionar `user's lifetime revenue` ao seu `users` para encontrar usuários de alto valor. Ou, se quiser segmentar a receita por gênero, adicione `customer's gender` ao seu `orders` tabela.

Para obter mais informações, confira este [tutorial](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md).

## Eliminando Tabelas e Removendo Colunas {#delete}

Da mesma forma que você pode selecionar tabelas e colunas para sincronização com sua Data Warehouse, também é possível removê-las ou removê-las.

>[!NOTE]
>
>Eliminar uma tabela ou remover colunas exclui quaisquer relatórios, métricas, conjuntos de filtros e colunas dependentes depois de confirmar a exclusão. Certifique-se de que deseja fazer isso: **essa ação não pode ser desfeita.**

Não se preocupe se você clicar em **[!UICONTROL Delete]** por acidente. Uma verificação de dependência é executada antes da exclusão de qualquer item, portanto, você tem a chance de revisar tudo antes de confirmar.

Para remover colunas, clique na tabela à qual a coluna pertence. Marque as colunas que deseja remover e clique no link ![button\_1.png](../../assets/button_1.png) botão.

Para remover uma tabela sincronizada, selecione todas as colunas na tabela e clique novamente no link ![botão](../../assets/button_1.png) botão. Isso remove todas as colunas nativas e calculadas que usam essa tabela da Data Warehouse.

### Confirmação de alterações

Se você estiver eliminando uma tabela ou removendo colunas, uma verificação de dependência será executada antes que o processo de exclusão seja concluído. As dependências são colunas calculadas, métricas, conjuntos de filtros e relatórios que usam a tabela ou as colunas que estão sendo removidas. Qualquer dependência detectada é exibida. Nesse momento, é possível cancelar o processo ou clicar em **[!UICONTROL Confirm Changes]** para eliminar a tabela/remover as colunas.

Embora as dependências excluídas não possam ser restauradas, as tabelas e as colunas ainda estarão disponíveis se você precisar sincronizar novamente qualquer coluna nativa no futuro.

Veja rapidamente como remover uma coluna:

![Remoção de uma coluna do data warehouse](../../assets/DW_delete.gif)

## Então, quando posso usar minhas novas colunas? {#when}

Novas colunas sincronizadas e colunas calculadas novas/atualizadas estarão prontas para uso após a conclusão da próxima atualização completa. Se uma atualização ainda não estiver em andamento, é possível forçar uma atualização clicando em **[!UICONTROL Force update]** mostrado na parte superior da `Data Warehouse` ou `Integrations` página. Você também pode agendar uma notificação por email ao concluir a atualização clicando em **[!UICONTROL Email me when complete]**.

Quando estiver pronto para usar suas novas colunas nos relatórios, [primeiro você precisa adicioná-las às métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md). Embora os dados não estejam disponíveis até que uma atualização seja concluída, ainda é possível usar novas colunas nos relatórios. Os dados contidos no relatório são exibidos quando a atualização é concluída.

## Encapsulamento

Este tutorial abordou muito material. Até agora, você deve ter uma sólida compreensão do que é um banco de dados, como os dados são organizados, como as tabelas se relacionam entre si e o que você pode fazer com o Gerenciador de Datas Warehouse.

Excelente! Teste seu novo conhecimento através da [criação de uma coluna calculada](../data-warehouse-mgr/creating-calculated-columns.md) ou [fazer alguns relatórios interessantes](../../tutorials/using-visual-report-builder.md).
