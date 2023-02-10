---
title: Gerenciamento de usuários e permissões
description: Saiba como gerenciar seu [!DNL MBI] usuários.
exl-id: 2a5eeabb-3c13-4ca1-b845-ed255b389c9f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# Gerenciar permissões do usuário

O MBI deve ser uma única fonte de verdade em toda a organização. Cada usuário terá seu próprio conjunto de painéis que pode [compartilhar com outros usuários](../../data-user/dashboards/share-dashboard-with-users.md).

## Níveis de permissão do usuário

Em [!DNL MBI], há três níveis de permissão gerais que se aplicam aos usuários, que são selecionados quando uma conta é criada:

* `Admin`
* `Standard`
* `Read-Only`

Essas permissões permitem que os usuários executem determinadas ações ou acessem partes específicas do [!DNL MBI]. Esta é uma tabela do que cada nível de permissão pode fazer no MBI:

|  | `Admin` | `Standard` | `Read Only` |
| -----|-----|-----|----|
| **Criar/gerenciar usuários** | ✔ |  |  |
| **Criar resumos por email** | ✔ | ✔ |  |
| **Criar/editar/compartilhar painéis** | ✔ | ✔ |  |
| **Exibir painéis** | ✔ | ✔ | ✔ |
| **Criar/editar/excluir relatórios visuais** | ✔ | ✔* |  |
| **Criar/editar/excluir relatórios SQL** | ✔ |  |  |
| **Clonar painéis** | ✔ |  |  |
| **Adicionar/gerenciar integrações** | ✔ |  |  |
| **Acesse o Gerenciador de Datas Warehouse** | ✔ |  |  |
| **Sincronizar/não sincronizar tabelas e colunas** | ✔ |  |  |
| **Criar/editar métricas** | ✔ |  |  |
| **Criar/editar conjuntos de filtros** | ✔ |  |  |
| **Criar/editar colunas calculadas** | ✔ |  |  |
| **Criar lista de relatórios dependentes** | ✔ |  |  |
| **Resumo do sistema de acesso** | ✔ |  |  |
| **Acessar configurações de Fuso horário** | ✔ |  |  |
| **Faturamento de acesso** | ✔ | ✔** |  |
| **Entre em contato com o suporte** | ✔ | ✔ | ✔ |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>_É possível limitar uma **[!UICONTROL Standard]**do usuário [acesso a métricas específicas](../../administrator/user-management/restrict-metric-access.md)._
>
>**[!UICONTROL Standard] _Os usuários do podem acessar Faturamento com uma configuração de permissão adicional._
>
>**[!UICONTROL Read-Only]** os usuários podem somente _exibir_ painéis que foram compartilhados com eles; eles não podem criar ou editar nada no [!DNL MBI], e também não podem procurar e adicionar novos painéis à conta deles. Recomendamos que você compartilhe um conjunto específico de painéis com **[!UICONTROL Read-Only]** usuários que você ou outro membro de sua equipe mantém. Não clone um conjunto de painéis para eles.

## Permissões adicionais: Faturamento e técnico {#billingtech}

Além dos níveis de permissão geral, existem também duas outras designações de usuários - `Billing` e `Technical`. Estas denominações destinam-se a ser utilizadas em conjunto com os níveis de permissão geral.

### Faturamento

`Billing` os usuários têm acesso à página de faturamento e podem alterar as informações de pagamento. Além disso, elas também podem ser contatadas por nossas equipes para perguntas de faturamento.

`Admin` os usuários têm acesso à guia Faturamento por padrão, mas os usuários do Standard também podem obter acesso se tiverem a variável `Billing` caixa de seleção selecionada em seu perfil.

![faturamento](../../assets/billing.png)<!--{: width="550" height="363"}-->

### Técnica

`Technical` Os usuários do não têm permissões específicas a eles. Essa configuração marca apenas um contato técnico em sua organização. Esses usuários podem ser contatados por nossas equipes para dúvidas técnicas.

`Admin` os usuários podem adicionar novos usuários à conta clicando em **[!UICONTROL Account Settings]** > **[!UICONTROL Create Users]** e seguir os prompts. Depois que o usuário é criado em [!DNL MBI], a pessoa sortuda que você está convidando receberá por email instruções sobre como concluir o processo de configuração da conta.

A qualquer momento, `Admins` pode exibir todos os usuários em sua conta clicando em **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**. Esta página exibe as permissões do usuário e as métricas e painéis aos quais ele tem acesso.
