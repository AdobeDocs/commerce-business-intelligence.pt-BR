---
title: Conecte seus dados
description: Saiba como navegar pelas tabelas disponíveis para sincronização no Gerenciador de Datas Warehouse.
exl-id: 94beba8b-6a86-4af9-87fb-96b1cf8f8fa2
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---

# Conecte seus dados

Em [!DNL MBI], as fontes de dados são chamadas `integrations`. Depois de um `integration` estiver conectado com êxito, você poderá navegar pelas tabelas disponíveis para sincronização no Gerenciador de Datas Warehouse.

As integrações são adicionadas e gerenciadas usando o `Connections` página que pode ser acessada clicando em **[!UICONTROL Manage Data** > **Connections]**. Aqui você vê uma lista de todas as integrações conectadas à sua conta, o tipo de integração, o status ([!DNL Google Analytics] e [!DNL Data Import API] as conexões terão campos de status em branco) e a última vez que uma conexão for testada (`Last Connection` Coluna iniciada) foi executada.

![Data\_Sources\_Table.png](../../../assets/Data_Sources_Table.png)

## Tipos de integrações

Há quatro maneiras de inserir seus dados [!DNL MBI]: conectar um banco de dados, conectar uma integração SaaS, fazer upload de um `.csv` ou use nossa API.

## Integrações do banco de dados

![Banco de dados\_icons.jpg](../../../assets/Database_icons.jpg)

[!DNL MBI] oferece suporte a bancos de dados baseados em SQL e NoSQL, como [MySQL](../../importing-data/integrations/mysql-via-ssh-tunnel.md), [Microsoft SQL](../integrations/microsoft-sql-server.md), [MongoDB](../integrations/mongodb-via-ssh-tunnel.md)e [PostgreSQL](../integrations/postgresql.md).

Ao mesmo tempo, é possível conectar diretamente seu banco de dados ao [!DNL MBI] usando credenciais de banco de dados, recomendamos que você use um método de criptografia comprovado como um túnel SSH. Isso garantirá que seus dados permaneçam seguros e seguros à medida que entram em seu data warehouse.

Dependendo do método de conexão e do tipo de banco de dados, alguns conhecimentos técnicos podem ser necessários para concluir a configuração.

## `SaaS` Integrações

![](../../../assets/SaaS_icons.jpg)

`SaaS` integrações são serviços como [[!DNL Google Adwords]](../integrations/google-adwords.md), [[!DNL Salesforce]](../integrations/salesforce.md)e [[!DNL Zendesk]](../integrations/zendesk.md). É importante observar que, como os dados de terceiros estão no servidor do fornecedor, você não pode acessá-los diretamente como pode fazer com os dados no banco de dados.

Na maioria dos casos, configurar uma integração no [!DNL MBI] O é tão fácil quanto simplesmente inserir as credenciais da conta. Alguns serviços podem exigir uma chave de API para concluir a autorização - confira o [seção integrações](../integrations/integrations.md) para obter instruções sobre como gerar quaisquer credenciais necessárias.

## Upload de arquivo

Não tem certeza de como obter dados de uma fonte adicional em seu data warehouse? [Usar o `File Upload` recurso](../connecting-data/using-file-uploader.md) é uma boa maneira de inserir dados que você não precisa para tomar decisões cotidianas. Após nossas regras de formatação, você pode fazer upload rapidamente `.csv` arquivos no data warehouse e uni-los a outras fontes de dados.

## [!DNL MBI] `Import API`

Se preferir automatizar a recuperação de dados de uma de suas próprias fontes, é possível usar a variável [!DNL MBI] `Import API`. Basicamente: se não estiver em um banco de dados ou um `SaaS` integração, a `Import API` é a melhor opção.

O uso da API requer um pouco de conhecimento técnico - alguém confortável em escrever e manter um pequeno script Ruby ou PHP será mais do que qualificado.

Para saber mais sobre como começar a usar o `Import API`, confira o [Site do desenvolvedor](https://developer.adobe.com/commerce/services/reporting/) e [como gerar uma chave de API](https://developer.adobe.com/commerce/services/reporting/import-api/).

## Adicionar uma integração

Para adicionar uma integração, clique em **[!UICONTROL Manage Data** > **Connections]** e, em seguida, clique em **[!UICONTROL Add a New Data Source]**. Clique no ícone da integração que deseja adicionar e siga as instruções em nossos artigos de ajuda para configurar:

* [Perguntas frequentes sobre integração](https://support.magento.com/hc/en-us/sections/360003161871-Integration-FAQ)
* [Disponível ](../integrations/integrations.md)
* [Consolidação de tabelas](../../../best-practices/consolidating-your-tables.md)
* [Restrição do acesso ao banco de dados](../../../administrator/account-management/restrict-db-access.md)

**Não está vendo a integração desejada?** Algumas integrações precisam ser ativadas para ficarem visíveis em sua conta. Se estiver procurando algo, por exemplo, [!DNL Facebook] - mas não consta da lista, [enviar um tíquete de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

**Se você vir um status de erro para uma integração**, não entrar em pânico - confira o [Seção Solução de problemas](https://support.magento.com/hc/en-us/sections/360003078151) para obter ajuda.
