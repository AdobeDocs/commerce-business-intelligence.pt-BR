---
title: Gerenciamento de usuários e permissões do Adobe Commerce
description: Saiba como gerenciar os usuários do Commerce Intelligence.
exl-id: 2a5eeabb-3c13-4ca1-b845-ed255b389c9f
role: Admin, User
feature: User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Gerenciar permissões do usuário

[!DNL Adobe Commerce Intelligence] O deve ser uma única fonte de verdade em toda a organização. Cada usuário tem seu próprio conjunto de painéis que pode [compartilhar com outros usuários](../../data-user/dashboards/share-dashboard-with-users.md).

## Níveis de permissão do usuário

Entrada [!DNL Commerce Intelligence], há três níveis de permissão gerais que se aplicam aos usuários, que são selecionados quando uma conta é criada:

* `Admin`
* `Standard`
* `Read-Only`

Essas permissões permitem que os usuários executem determinadas ações ou acessem partes específicas do [!DNL Commerce Intelligence]. Esta é uma tabela do que cada nível de permissão pode fazer no [!DNL Commerce Intelligence]:

|   | `Admin` | `Standard` | `Read Only` |
| -----|-----|-----|----|
| **Criar/gerenciar usuários** | ✔ |   |   |
| **Criar resumos de email** | ✔ | ✔ |   |
| **Criar/editar/compartilhar painéis** | ✔ | ✔ |   |
| **Exibir painéis** | ✔ | ✔ | ✔ |
| **Criar/editar/excluir relatórios visuais** | ✔ | ✔* |   |
| **Criar/editar/excluir relatórios SQL** | ✔ |  |   |
| **Clonar painéis** | ✔ |   |   |
| **Adicionar/gerenciar integrações** | ✔ |   |   |
| **Acessar o Gerenciador de Datas Warehouse** | ✔ |   |   |
| **Sincronizar/dessincronizar tabelas e colunas** | ✔ |   |   |
| **Criar/editar métricas** | ✔ |   |   |
| **Criar/editar conjuntos de filtros** | ✔ |   |   |
| **Criar/editar colunas calculadas** | ✔ |   |   |
| **Criar lista de relatórios dependentes** | ✔ |   |   |
| **Resumo do sistema de acesso** | ✔ |   |   |
| **Configurações do fuso horário de acesso** | ✔ |   |   |
| **Faturamento de acesso** | ✔ | ✔** |   |
| **Entrar em contato com o suporte** | ✔ | ✔ | ✔ |

{style="table-layout:auto"}

>[!NOTE]
>
>_É possível limitar um **[!UICONTROL Standard]**do usuário [acesso a métricas específicas](../../administrator/user-management/restrict-metric-access.md)._
>
>**[!UICONTROL Standard] _Os usuários do podem acessar o Faturamento com uma configuração de permissão adicional._
>
>**[!UICONTROL Read-Only]** os usuários só podem _exibir_ painéis que foram compartilhados com eles; eles não podem criar ou editar nada em [!DNL Commerce Intelligence], nem podem pesquisar e adicionar novos painéis à sua conta. A Adobe recomenda que você compartilhe um conjunto específico de painéis com o **[!UICONTROL Read-Only]** usuários que você ou outro membro de sua equipe mantém. Não clone um conjunto de painéis para eles.

## Permissões adicionais: faturamento e técnicas {#billingtech}

Além dos níveis de permissão gerais, há duas outras designações de usuário: `Billing` e `Technical`. Essas designações devem ser usadas com os níveis de permissão gerais.

### Faturamento

`Billing` os usuários têm acesso à página de faturamento e podem alterar as informações de pagamento. Além disso, eles também podem ser contatados pelo Adobe para perguntas sobre faturamento.

`Admin` Os usuários do têm acesso à `Billing` por padrão, mas `Standard` os usuários também podem obter acesso se tiverem o `Billing` caixa de seleção marcada no perfil.

![faturamento](../../assets/billing.png)<!--{: width="550" height="363"}-->

### Técnico

`Technical` os usuários do não têm permissões específicas para eles; essa configuração apenas marca um contato técnico em sua organização. Esses usuários podem ser contatados pelo Adobe para perguntas técnicas.

`Admin` usuários podem adicionar novos usuários às suas contas clicando em **[!UICONTROL Account Settings]** > **[!UICONTROL Create Users]** e seguindo as instruções. Depois que o usuário for criado em [!DNL Commerce Intelligence], a pessoa de sorte que você está convidando receberá instruções por email sobre como concluir o processo de configuração da conta.

A qualquer momento, `Admins` pode exibir todos os usuários em sua conta clicando em **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**. Esta página exibe as permissões do usuário e quais métricas e painéis podem ser acessados.
