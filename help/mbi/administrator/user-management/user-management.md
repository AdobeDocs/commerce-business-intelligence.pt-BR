---
title: Gerenciamento de usuários e permissões do Adobe Commerce
description: Saiba como gerenciar usuários do Commerce Intelligence.
exl-id: 2a5eeabb-3c13-4ca1-b845-ed255b389c9f
role: Admin, User
feature: User Management
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# Gerenciar permissões do usuário

[!DNL Adobe Commerce Intelligence] deve ser uma única fonte de verdade para toda a sua organização. Cada usuário tem seu próprio conjunto de painéis que pode [compartilhar com outros usuários](../../data-user/dashboards/share-dashboard-with-users.md).

## Níveis de permissão do usuário

Em [!DNL Commerce Intelligence], há três níveis de permissão gerais que se aplicam aos usuários, que são selecionados quando uma conta é criada:

* `Admin`
* `Standard`
* `Read-Only`

Essas permissões permitem que os usuários executem determinadas ações ou acessem partes específicas do [!DNL Commerce Intelligence]. Esta é uma tabela do que cada nível de permissão pode fazer em [!DNL Commerce Intelligence]:

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
| **Acessar o Data Warehouse Manager** | ✔ |   |   |
| **Sincronizar/dessincronizar tabelas e colunas** | ✔ |   |   |
| **Criar/editar métricas** | ✔ |   |   |
| **Criar/editar conjuntos de filtros** | ✔ |   |   |
| **Criar/editar colunas calculadas** | ✔ |   |   |
| **Criar lista de relatórios dependentes** | ✔ |   |   |
| **Resumo do Sistema de Acesso** | ✔ |   |   |
| **Acessar configurações de fuso horário** | ✔ |   |   |
| **Faturamento de Acesso** | ✔ | ✔** |   |
| **Contate o Suporte** | ✔ | ✔ | ✔ |

{style="table-layout:auto"}

>[!NOTE]
>
>_Você pode limitar o **[!UICONTROL Standard]**acesso a métricas específicas[ de um usuário ](../../administrator/user-management/restrict-metric-access.md)._
>
>**[!UICONTROL Standard] _usuários podem acessar o Faturamento com uma configuração de permissão extra._
>
>**[!UICONTROL Read-Only]** usuários só podem _exibir_ painéis que foram compartilhados com eles; eles não podem criar ou editar nada em [!DNL Commerce Intelligence], nem podem pesquisar e adicionar novos painéis às suas contas. A Adobe recomenda que você compartilhe um conjunto específico de painéis com **[!UICONTROL Read-Only]** usuários que você ou outro membro de sua equipe mantém. Não clone um conjunto de painéis para eles.

## Permissões adicionais: faturamento e técnicas {#billingtech}

Além dos níveis de permissão gerais, existem duas outras designações de usuário - `Billing` e `Technical`. Essas designações devem ser usadas com os níveis de permissão gerais.

### Faturamento

`Billing` usuários têm acesso à página de cobrança e podem alterar informações de pagamento. Além disso, elas também podem ser contatadas pela Adobe em caso de dúvidas sobre cobrança.

Por padrão, `Admin` usuários têm acesso à guia `Billing`, mas `Standard` usuários também podem obter acesso se tiverem a caixa de seleção `Billing` marcada em seus perfis.

![Página de cobrança](../../assets/billing.png)<!--{: width="550" height="363"}-->

### Técnico

`Technical` usuários não têm permissões específicas para eles - essa configuração apenas marca um contato técnico em sua organização. A Adobe pode entrar em contato com esses usuários para perguntas técnicas.

`Admin` usuários podem adicionar novos usuários às suas contas clicando em **[!UICONTROL Account Settings]** > **[!UICONTROL Create Users]** e seguindo os prompts. Depois que o usuário for criado em [!DNL Commerce Intelligence], a pessoa de sorte que você está convidando receberá instruções por email sobre como concluir o processo de configuração da conta.

A qualquer momento, `Admins` pode exibir todos os usuários em sua conta clicando em **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**. Esta página exibe as permissões do usuário e quais métricas e painéis podem ser acessados.
