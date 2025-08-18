---
title: Data Warehouse Manager
description: Saiba como gerenciar configurações de sincronização de tabela e coluna, detalhar um esquema de tabela e criar colunas calculadas para usar em relatórios.
exl-id: b9577919-0db0-47f1-a426-1abe48443ac0
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 0%

---

# Data Warehouse Manager

>[!NOTE]
>
>Requer [permissões de administrador](../../administrator/user-management/user-management.md)

O Data Warehouse Manager, acessado ao clicar em **[!UICONTROL Manage Data > Data Warehouse]**, é o portal para o seu Data Warehouse [!DNL Adobe Commerce Intelligence]. Usando o Data Warehouse Manager, você pode gerenciar configurações de sincronização de tabela e coluna, detalhar um esquema de tabela e criar colunas calculadas para usar em relatórios.

Este tópico abrange:

* [Aprendendo o seu caminho](#learning)
* [Sincronização de tabelas e colunas](#syncing)
* [Criação de colunas calculadas](#calculated)
* [Eliminando tabelas e removendo colunas](#delete)
* [Sincronização de novas tabelas em segundo plano](#syncnew)
* [Então, quando posso usar minhas novas colunas?](#when)

## Aprendendo o seu caminho {#learning}

O lado esquerdo da página `Data Warehouse Manager` contém a lista de tabelas, permitindo que você alterne facilmente entre tabelas. Quando você seleciona uma tabela na lista, a área de gerenciamento de tabela é preenchida com o schema da tabela, onde você pode modificar a tabela selecionada.

Na lista de tabelas, as tabelas são agrupadas por sua origem de conexão. Estas fontes são adicionadas em [!UICONTROL Manage Data > Integrations] e podem ser um banco de dados, uma [API](https://developer.adobe.com/commerce/services/reporting/) ou um conector de terceiros. Na parte superior da lista de tabelas, há uma caixa de pesquisa que permite localizar facilmente as tabelas desejadas.

Abaixo da caixa de pesquisa, você vê duas opções: `All Tables` e `Synced Tables`. A opção `All Tables` lista todas as tabelas que você disponibilizou para a Data Warehouse, que inclui tabelas sincronizadas e não sincronizadas.

A opção `Synced Tables` mostra todas as tabelas que já foram adicionadas ao Data Warehouse e cujos dados estão sendo replicados das colunas selecionadas.

Não está vendo a tabela que você está procurando na lista `All Tables`? Há algumas razões possíveis para isso:

* A fonte de dados ainda não foi adicionada
* A fonte de dados é um banco de dados e o usuário [!DNL Commerce Intelligence] que você criou não tem acesso. Nesse caso, você ou o administrador do banco de dados deve conceder acesso.
* A fonte de dados ou tabela foi adicionada recentemente e ainda não foi sincronizada

## Sincronização de tabelas e colunas {#syncing}

### Sincronizando Novas Tabelas e Colunas Nativas

O Data Warehouse Manager não apenas oferece a capacidade de visualizar e gerenciar facilmente suas fontes de dados, mas também tem a liberdade de selecionar as tabelas e colunas individuais que deseja sincronizar.

1. Clique na opção `All Tables` e localize a tabela que deseja sincronizar.
1. Clique no nome da tabela para visualizar o schema. Se a tabela for nova, todas as colunas serão exibidas como `Unsynced`.
1. Marque as colunas que deseja sincronizar.

   >[!NOTE]
   >
   >As colunas nativas de uma tabela têm Do Seu Banco de Dados na coluna `Location`.

1. Verifique as colunas `Primary Key` - essas colunas têm um símbolo de chave ao lado do nome da coluna. Um `Primary Key` é necessário para sincronizar dados corretamente na Data Warehouse.

   Se você estiver sincronizando uma tabela que vem diretamente do seu banco de dados, é possível que `Primary Keys` não seja indicado. Nesse caso, entre em contato com o administrador do banco de dados para solicitar que uma ou mais chaves primárias sejam adicionadas à tabela.
1. Quando terminar, clique no botão ![botão](../../assets/button.png).

*Sucesso!* mensagem é exibida e o status muda para `Pending` para as colunas selecionadas. Depois que a próxima atualização completa for concluída, as tabelas e colunas recém-sincronizadas estarão disponíveis para uso nos relatórios. Você também pode definir novos [métodos de replicação](./cfg-replication-methods.md) após a sincronização inicial.

Aqui está uma rápida visão de todo o processo:

![Adicionando colunas ao data warehouse](../../assets/DW_sync.gif)

### Sincronizando Novas Tabelas em Segundo Plano {#syncnew}

Ao sincronizar uma tabela grande pela primeira vez, o Data Warehouse precisa capturar retroativamente todos os pontos de dados na tabela antes de capturar novos dados de forma contínua. Se sua tabela for grande, talvez você não queira que essa sincronização inicial seja executada em sequência com seu **ciclo de atualização**. Nesta situação, você deseja que a sincronização inicial ocorra em segundo plano, em *paralelo* com qualquer atualização em execução no momento.

Para ter certeza de que isso ocorre, você deve selecionar a opção `Save and Sync Data Immediately` sincronizando essa tabela pela primeira vez.

### Verificação de novas tabelas e colunas {#forceupdate}

Seu Data Warehouse não detecta automaticamente novas fontes, tabelas ou colunas no momento em que são adicionadas. Um processo de sincronização é executado durante toda a semana para localizar novas adições e disponibilizá-las, mas você pode forçar uma sincronização de estrutura se quiser acessar tabelas e colunas recém-adicionadas antes que o processo seja executado.

Abaixo da barra de pesquisa na lista de tabelas há um link `Check for new tables and columns`. Clicar nesse link forçará o início do processo de sincronização de estrutura; normalmente, novas adições estão disponíveis após 10 minutos. Atualize a página para ver a nova fonte, tabela ou coluna.

## Criação de Colunas Calculadas {#calculated}

Simplesmente ser capaz de ver e gerenciar dados de todas as fontes torna muito mais fácil obter insights sobre os negócios. Mas, no Data Warehouse Manager, você pode ir além criando colunas calculadas dentro das tabelas. `Calculated` colunas derivam novas informações de seus dados existentes.

Digamos que você queira adicionar `user's lifetime revenue` à tabela `users` para encontrar usuários de alto valor. Ou, se você quiser segmentar a receita por gênero, adicione `customer's gender` à tabela `orders`.

Para obter mais informações, confira este [tutorial](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md).

## Eliminando Tabelas e Removendo Colunas {#delete}

Da mesma forma que você pode selecionar tabelas e colunas para sincronização com sua Data Warehouse, também é possível removê-las ou removê-las.

>[!NOTE]
>
>Eliminar uma tabela ou remover colunas exclui quaisquer relatórios, métricas, conjuntos de filtros e colunas dependentes depois de confirmar a exclusão. Certifique-se de que deseja fazer isso - **essa ação não pode ser desfeita.**

Não se preocupe se você clicar em **[!UICONTROL Delete]** acidentalmente. Uma verificação de dependência é executada antes da exclusão de qualquer item, portanto, você tem a chance de revisar tudo antes de confirmar.

Para remover colunas, clique na tabela à qual a coluna pertence. Verifique as colunas que deseja remover e clique no botão ![button\_1.png](../../assets/button_1.png).

Para remover uma tabela sincronizada, selecione todas as colunas da tabela e clique novamente no botão ![botão](../../assets/button_1.png). Isso remove todas as colunas nativas e calculadas que usam essa tabela da sua Data Warehouse.

### Confirmação de alterações

Se você estiver eliminando uma tabela ou removendo colunas, uma verificação de dependência será executada antes que o processo de exclusão seja concluído. As dependências são colunas calculadas, métricas, conjuntos de filtros e relatórios que usam a tabela ou as colunas que estão sendo removidas. Qualquer dependência descoberta será exibida - neste ponto, você pode cancelar o processo ou clicar em **[!UICONTROL Confirm Changes]** para descartar a tabela/remover a(s) coluna(s).

Embora as dependências excluídas não possam ser restauradas, as tabelas e as colunas ainda estarão disponíveis se você precisar sincronizar novamente qualquer coluna nativa no futuro.

Veja rapidamente como remover uma coluna:

![Removendo uma coluna do data warehouse](../../assets/DW_delete.gif)

## Então, quando posso usar minhas novas colunas? {#when}

Novas colunas sincronizadas e colunas calculadas novas/atualizadas estarão prontas para uso após a conclusão da próxima atualização completa. Se uma atualização ainda não estiver em andamento, você poderá forçar uma atualização clicando em **[!UICONTROL Force update]** exibido na parte superior da página `Data Warehouse` ou `Integrations`. Você também pode agendar uma notificação por email ao concluir a atualização clicando em **[!UICONTROL Email me when complete]**.

Quando estiver pronto para usar suas novas colunas em relatórios, [você precisará adicioná-las às métricas primeiro](../data-warehouse-mgr/manage-data-dimensions-metrics.md). Embora os dados não estejam disponíveis até que uma atualização seja concluída, ainda é possível usar novas colunas nos relatórios. Os dados contidos no relatório são exibidos quando a atualização é concluída.

## Encapsulamento

Este artigo cobriu um monte de material. Até agora, você deve ter uma sólida compreensão do que é um banco de dados, como os dados são organizados, como as tabelas se relacionam entre si e o que você pode fazer com o Data Warehouse Manager.

Teste seu conhecimento [criando uma coluna calculada](../data-warehouse-mgr/creating-calculated-columns.md) ou [criando alguns relatórios interessantes](../../tutorials/using-visual-report-builder.md).
