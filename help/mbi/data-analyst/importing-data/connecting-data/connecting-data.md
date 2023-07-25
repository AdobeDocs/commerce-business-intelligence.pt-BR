---
title: Conectar seus dados
description: Saiba como procurar as tabelas disponíveis para sincronização no Gerenciador de Datas Warehouse.
exl-id: 94beba8b-6a86-4af9-87fb-96b1cf8f8fa2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Conectar seus dados

Entrada [!DNL Adobe Commerce Intelligence], fontes de dados são chamadas `integrations`. Depois de um `integration` for conectado com êxito, você poderá procurar as tabelas disponíveis para sincronização no Gerenciador de Datas Warehouse.

As integrações são adicionadas e gerenciadas usando o `Connections` página, que pode ser acessada clicando em **[!UICONTROL Manage Data** > **Connections]**. Aqui, você vê:

* uma lista de todas as integrações conectadas à sua conta

* o tipo de integração

* status ([!DNL Google Analytics] e [!DNL Data Import API] as conexões têm campos de status em branco)

* a última vez que um teste de conexão (`Last Connection Started` column) foi executado

![Data\_Sources\_Table.png](../../../assets/Data_Sources_Table.png)

## Tipos de integrações

Há quatro maneiras de inserir seus dados no [!DNL Commerce Intelligence]: conectar um banco de dados, conectar uma integração SaaS, fazer upload de um `.csv` ou use a API de Adobe.

## Integrações de banco de dados

![Database\_icons.jpg](../../../assets/Database_icons.jpg)

[!DNL Commerce Intelligence] suporta bancos de dados baseados em SQL e NoSQL, como [MySQL](../../importing-data/integrations/mysql-via-ssh-tunnel.md), [MICROSOFT SQL](../integrations/microsoft-sql-server.md), [MongoDB](../integrations/mongodb-via-ssh-tunnel.md), e [PostgreSQL](../integrations/postgresql.md).

Embora você possa conectar seu banco de dados diretamente ao [!DNL Commerce Intelligence] usando credenciais de banco de dados, o Adobe recomenda usar um método de criptografia comprovado, como um túnel SSH. Isso garante que seus dados permaneçam seguros à medida que são enviados para sua Data Warehouse.

Dependendo do método de conexão e do tipo de banco de dados, talvez seja necessário algum conhecimento técnico para concluir a configuração.

## `SaaS` Integrações

![](../../../assets/SaaS_icons.jpg)spree-commerce-logo.png

`SaaS` integrações são serviços como [[!DNL Google Adwords]](../integrations/google-adwords.md), [[!DNL Salesforce]](../integrations/salesforce.md), e [[!DNL Zendesk]](../integrations/zendesk.md). Como os dados de terceiros residem no servidor do fornecedor, não é possível acessá-los diretamente como é possível com os dados no banco de dados.

Normalmente, a configuração de uma integração no [!DNL Commerce Intelligence] é tão fácil quanto simplesmente inserir suas credenciais de conta. Alguns serviços podem exigir uma chave de API para concluir a autorização. Confira o [seção integrações](../integrations/integrations.md) para obter instruções sobre como gerar as credenciais necessárias.

## Upload de arquivo

Não tem certeza de como obter dados de uma fonte complementar na sua Data Warehouse? [Usar o `File Upload` recurso](../connecting-data/using-file-uploader.md) O é uma boa maneira de obter dados de que você não precisa para tomar decisões diárias. Seguindo as regras de formatação, você pode fazer upload rapidamente `.csv` arquivos na Data Warehouse e associá-los a outras fontes de dados.

## [!DNL Commerce Intelligence] `Import API`

Se você preferir automatizar a recuperação de dados de uma de suas próprias fontes, poderá usar o [!DNL Commerce Intelligence] `Import API`. Basicamente, se não estiver em um banco de dados ou um `SaaS` integração, o `Import API` A função é a melhor opção.

O uso da API requer um pouco de conhecimento técnico - alguém que esteja familiarizado com a escrita e manutenção de um pequeno script Ruby ou PHP é mais do que qualificado.

Para saber mais sobre a introdução ao `Import API`, confira o [Site do desenvolvedor](https://developer.adobe.com/commerce/services/reporting/) e [como gerar uma chave de API](https://developer.adobe.com/commerce/services/reporting/import-api/).

## Adicionar uma integração

Para adicionar uma integração, clique em **[!UICONTROL Manage Data** > **Connections]** e clique em **[!UICONTROL Add a New Data Source]**. Clique no ícone da integração que deseja adicionar e siga as instruções nos tópicos de ajuda para configurar:

* [Perguntas frequentes sobre integração](https://support.magento.com/hc/en-us/sections/360003161871-Integration-FAQ)
* [Disponível ](../integrations/integrations.md)
* [Consolidação de tabelas](../../../best-practices/consolidating-your-tables.md)
* [Restrição do acesso ao banco de dados](../../../administrator/account-management/restrict-db-access.md)

**Não está vendo uma integração que você deseja?** Algumas integrações devem ser ativadas para que fiquem visíveis em sua conta. Se você estiver procurando algo como [!DNL Facebook] mas não está listado, [enviar um tíquete de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

**Se você vir um status de erro para uma integração**, confira o [Seção Solução de problemas](https://support.magento.com/hc/en-us/sections/360003078151) para obter ajuda.
