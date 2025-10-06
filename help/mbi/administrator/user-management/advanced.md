---
title: Gerenciamento avançado de usuários
description: Melhore a visibilidade dos dados, simplifique a emissão de relatórios, adapte o acesso por grupos de usuários, simplifique o compartilhamento de painéis e garanta a segurança e a escalabilidade para sua organização.
role: Admin, User
feature: User Management
exl-id: d96a075d-53ab-48d3-ba83-3ff4298a0cb7
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---

# Gerenciamento avançado de usuários

O recurso [!DNL Advanced User Management] fornece controles aprimorados de visibilidade de dados e habilita a filtragem de dados lógicos com base em grupos de usuários (regiões organizacionais). Ele permite adaptar a visibilidade dos dados com base nos grupos de usuários e elimina a necessidade de criar uma réplica dos painéis existentes para atender aos requisitos de relatórios específicos da região sempre que os negócios se expandirem para uma nova região.

O [!DNL Advanced User Management] simplifica o compartilhamento de painéis e a visibilidade de dados enquanto garante a segurança e a escalabilidade para grandes organizações. A flexibilidade para configurar grupos de usuários, funções e permissões torna o Commerce Intelligence uma ferramenta avançada para requisitos de nível empresarial.

Com o [!DNL Advanced User Management] habilitado, somente usuários Administradores têm acesso para configurar o seguinte:

- Métricas
- Visual Report Builder
- Relatórios baseados em SQL
- Resumo de email
- Exportações brutas

## Matriz de recursos

O [!DNL Advanced User Management] afeta vários recursos na Commerce Intelligence. A tabela a seguir descreve os recursos, as permissões e sua disponibilidade para várias funções com base no recurso que está sendo ativado ou desativado.

<table><thead>
  <tr>
    <th colspan="3" rowspan="2">Recursos do Commerce Intelligence</th>
    <th colspan="6">Recursos do Gerenciamento avançado de usuários (AUM)</th>
  </tr>
  <tr>
    <th colspan="3">Desabilitado</th>
    <th colspan="3">Ativado</th>
  </tr></thead>
<tbody>
  <tr>
    <td>Grupo de recursos</td>
    <td>Recurso</td>
    <td>Permissões</td>
    <td>Admin</td>
    <td>Padrão</td>
    <td>Somente leitura</td>
    <td>Admin</td>
    <td>Padrão</td>
    <td>Somente leitura</td>
  </tr>
  <tr>
    <td rowspan="7">Gerenciar usuários (acessível a todos os administradores e afeta todas as funções)</td>
    <td>Configurar grupos de usuários</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Convidar usuário</td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Guia Permissões - Mapeamento de funções</td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Guia Permissões - Mapeamento do grupo de usuários (AUM)</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Guia Permissões - Armazena o mapeamento de subconjunto (AUM)</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Guia Métricas</td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Guia Painéis compartilhados</td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="2">Report Builder</td>
    <td>Visual Report Builder</td>
    <td></td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>SQL REPORT BUILDER</td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="2">Resumo de email</td>
    <td>Criar resumos de email sem particionamento de dados</td>
    <td></td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Criar resumos de email com particionamento de dados (AUM)</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="4">Painéis  - Compartilhar</td>
    <td>Compartilhar painel com usuários em várias funções</td>
    <td></td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Compartilhar o painel com grupos de usuários e administradores (AUM)</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="2">Compartilhar painel - Permissões</td>
    <td>Editar</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Exibir</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="18">Painéis - Visualização (Abrir painel compartilhado com permissões fornecidas)</td>
    <td rowspan="2">Compartilhar novamente um painel compartilhado</td>
    <td>Editar</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Exibir</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="2">Filtro de Data (sem sinalizador de recurso EDITAR Opções de HORA)</td>
    <td>Editar</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Exibir</td>
    <td></td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="2">Filtro de Data (com sinalizador de recurso EDITAR Opções de HORA)</td>
    <td>Editar</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Exibir</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
  </tr>
  <tr>
    <td rowspan="2">Filtro de Armazenamento (sem sinalizador de recurso EDIT TIME Options)</td>
    <td>Editar</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Exibir</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="2">Armazenar filtro (com sinalizador de recurso EDITAR opções de HORA)</td>
    <td>Editar</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Exibir</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="2">Dados do painel - Filtrar dados de relatórios com base no AUM (User Group mapping, mapeamento do grupo de usuários)</td>
    <td>Editar</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Exibir</td>
    <td></td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
  </tr>
  <tr>
    <td rowspan="2">Relatório - Editar</td>
    <td>Editar</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Exibir</td>
    <td></td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="2">Exportação de relatórios (CSV, XLSX)</td>
    <td>Editar</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Exibir</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
  </tr>
  <tr>
    <td rowspan="2">Relatório - Exportação Bruta</td>
    <td>Editar</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Exibir</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</tbody></table>

## Controle de administração

Os usuários administradores podem gerenciar as seguintes tarefas:

- Configuração de grupos de usuários
- Atribuir função e grupo de usuários a usuários individuais
- Compartilhar painéis com grupos de usuários ou outros administradores com permissões no nível de painel
- Agendar resumos de email com filtragem de dados a nível de grupo de usuários

### Configurar grupos de usuários

Grupos de usuários são agrupamentos lógicos de regiões mapeadas para filtros de armazenamento específicos (por exemplo, grupos de usuários criados com base em nomes de continentes, países e regiões).

Para configurar grupos de usuários:

1. Vá para [!UICONTROL **Gerenciar Usuários**] > [!UICONTROL **User Groups]**, para ver os grupos de usuários existentes.

   ![Configurar grupos de usuários](../../assets/configure-user-groups.png)

1. [!UICONTROL **Adicionar Grupo**] permite que os administradores criem um novo grupo de usuários:

   - Insira um nome para o grupo (por exemplo, &quot;Américas&quot;).

   - Selecione armazenamentos ou filtros relevantes ao grupo de usuários.

   - Salve a configuração.

     ![Adicionar grupos de usuários](../../assets/add-group.png)

1. Os administradores podem:

   - Edite grupos de usuários para atualizar mapeamentos de armazenamento ou renomeie-os para maior clareza.

   - Exclua grupos de usuários quando eles não forem mais necessários. Os administradores devem reatribuir manualmente os usuários existentes que estão mapeados para o grupo de usuários excluído.

1. Grupos padrão:

   - [!UICONTROL **None]**: um grupo de fallback para usuários ainda não mapeados para um grupo específico. Esses usuários não verão nenhum dado até que sejam atribuídos a um grupo apropriado.

   - [!UICONTROL **Todos**]: fornece acesso irrestrito a todos os dados (normalmente reservados para usuários administradores).

### Atribuir usuários a grupos de usuários

Os administradores podem mapear novos usuários para grupos relevantes durante a integração usando [!UICONTROL **Convidar um Usuário**]. Os usuários existentes podem ser mapeados para grupos de usuários com base nas necessidades de negócios.

![Atribuir usuários a grupos de usuários](../../assets/assign-users-to-groups.png)

>[!TIP]
>
>- Até que um usuário [!UICONTROL **Padrão**] ou [!UICONTROL **Somente leitura**] seja atribuído a um grupo de usuários relevante, é seguro atribuí-lo a [!UICONTROL **Nenhum**] para garantir que ele não acesse, por engano, nenhum dado do painel.
>
>- Durante a atribuição de permissões a um usuário, com base nos requisitos de negócios, há a possibilidade de restringir armazenamentos específicos em um grupo para um controle aprimorado.

Os usuários administradores são sempre mapeados para [!UICONTROL **Todos**] lojas por padrão, o que lhes permite exibir painéis com a exibição de loja completa.

### Compartilhar painéis

O [!DNL Advanced User Management] fornece opções avançadas para compartilhar painéis enquanto mantém a segurança dos dados.

- Os administradores podem compartilhar painéis com os grupos de usuários, bem como com outros usuários administradores para colaborar. Isso permite o gerenciamento centralizado de painéis de controle e simplifica o gerenciamento para grandes organizações.

  ![Compartilhar painéis](../../assets/share-dashboards.png)

- As permissões de compartilhamento de painel incluem:

   - [!UICONTROL **Editar**]: disponível somente para usuários administradores para modificar painéis, filtrar dados, modificar relatórios ou exportar dados.

   - [!UICONTROL **Exibição**]: disponível para usuários em todas as funções com (determinadas restrições).

   - [!UICONTROL **Nenhum**]: revoga o acesso ao painel para determinados grupos de usuários ou administradores.

  >[!NOTE]
  >
  >Consulte a [matriz de recursos](#feature-matrix) para obter a usabilidade de vários recursos do Commerce Intelligence com base na regra e nas permissões de painel para entender várias combinações.

#### Visualizações de painéis

Os usuários administradores podem visualizar dados do painel com acesso a todas as lojas.

![Exibir administrador do painel](../../assets/view-dashboard-admin.png)

No entanto, os usuários podem visualizar dados do painel filtrados com base nos armazenamentos mapeados para eles durante a configuração do usuário.

![Exibir administrador filtrado pelo painel](../../assets/view-dashboard-user.png)

>[!TIP]
>
>Os administradores podem ativar filtros de data para painéis compartilhados, permitindo que os usuários visualizem dados em diferentes intervalos de datas, em vez do período padrão definido durante a criação do relatório. Esse recurso pode ser ativado ou desativado com base nas necessidades comerciais.

### Agendar resumos de email

O [!DNL Advanced User Management] estende os recursos de filtragem de dados para resumos de email. Dependendo do público-alvo, os usuários administradores podem especificar grupos de usuários para os quais os relatórios selecionados devem ser filtrados.

![Resumo do email da agenda](../../assets/schedule-email-summary.png)
