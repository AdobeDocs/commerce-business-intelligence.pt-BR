---
title: Conectar seus dados
description: Saiba como procurar as tabelas disponíveis para sincronização no Data Warehouse Manager.
exl-id: 94beba8b-6a86-4af9-87fb-96b1cf8f8fa2
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration
TQID: https://experienceleague.adobe.com/WwUCbK9dC39RSVL8Nf0PdL10wAdxje-9deR20JScqj0
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 3a6b80d7bcfa5db4d86ab4da81239e3ea804f6ad
workflow-type: tm+mt
source-wordcount: 628
ht-degree: 0%

---

# Conectar seus dados

Em [!DNL Adobe Commerce Intelligence], as fontes de dados são chamadas `integrations`. Depois que um `integration` for conectado com êxito, você poderá procurar as tabelas disponíveis para sincronização no Data Warehouse Manager.

As integrações são adicionadas e gerenciadas usando a página `Connections`, que pode ser acessada clicando em **[!UICONTROL Manage Data** > **Connections]**. Aqui, você vê:

* uma lista de todas as integrações conectadas à sua conta

* o tipo de integração

* ([!DNL Google Analytics] e [!DNL Data Import API] conexões têm campos de status em branco)

* a última vez que um teste de conexão (`Last Connection Started` coluna) foi executado

![Dados\_Fontes\_Tabela.png](../../../assets/Data_Sources_Table.png)

## Tipos de integrações

Há quatro maneiras de obter seus dados no [!DNL Commerce Intelligence]: conectar um banco de dados, conectar uma integração SaaS, carregar um arquivo `.csv` ou usar a API do Adobe.

## Integrações de banco de dados

![Banco_de_dados\_icons.jpg](../../../assets/Database_icons.jpg)

[!DNL Commerce Intelligence] dá suporte a bancos de dados NoSQL e baseados em SQL, como [MySQL](../../importing-data/integrations/mysql-via-ssh-tunnel.md), [Microsoft SQL](../integrations/microsoft-sql-server.md), [MongoDB](../integrations/mongodb-via-ssh-tunnel.md) e [PostgreSQL](../integrations/postgresql.md).

Embora você possa conectar seu banco de dados diretamente ao [!DNL Commerce Intelligence] usando credenciais de banco de dados, a Adobe recomenda usar um método de criptografia comprovado, como um túnel SSH. Isso garante que seus dados permaneçam seguros à medida que são direcionados para a Data Warehouse. Para registro, erros e solução de problemas da chave do host SSH, consulte [Verificação da chave do host SSH](../integrations/ssh-host-key-verification.md).

Dependendo do método de conexão e do tipo de banco de dados, talvez seja necessário algum conhecimento técnico para concluir a configuração.

## `SaaS` Integrações

![Ícones de integração do SaaS mostrando várias plataformas com suporte](../../../assets/SaaS_icons.jpg)spree-commerce-logo.png

`SaaS` integrações são serviços como [[!DNL Google Adwords]](../integrations/google-adwords.md), [[!DNL Salesforce]](../integrations/salesforce.md) e [[!DNL Zendesk]](../integrations/zendesk.md). Como os dados de terceiros residem no servidor do fornecedor, não é possível acessá-los diretamente como é possível com os dados no banco de dados.

Normalmente, configurar uma integração no [!DNL Commerce Intelligence] é tão fácil quanto simplesmente inserir suas credenciais de conta. Alguns serviços podem exigir uma chave de API para concluir a autorização. Confira a [seção de integrações](../integrations/integrations.md) para obter instruções sobre como gerar as credenciais necessárias.

## Upload de arquivo

Não tem certeza de como obter dados de uma fonte complementar para o Data Warehouse? [Usar o recurso `File Upload`](../connecting-data/using-file-uploader.md) é uma boa maneira de obter dados que você não precisa para tomar decisões diárias. Seguindo as regras de formatação, você pode carregar rapidamente arquivos do `.csv` na Data Warehouse e associá-los a outras fontes de dados.

## [!DNL Commerce Intelligence] `Import API`

Se você preferir automatizar a recuperação de dados de uma de suas próprias fontes, poderá usar o [!DNL Commerce Intelligence] `Import API`. Basicamente, se não estiver em um banco de dados ou em uma integração do `SaaS`, a função `Import API` será a sua melhor opção.

O uso da API requer um pouco de conhecimento técnico - alguém que esteja familiarizado com a escrita e manutenção de um pequeno script Ruby ou PHP é mais do que qualificado.

Para saber mais sobre a introdução ao `Import API`, verifique o [site do desenvolvedor](https://developer.adobe.com/commerce/services/reporting/) e [como gerar uma chave de API](https://developer.adobe.com/commerce/services/reporting/import-api/).

## Adicionar uma integração

Para adicionar uma integração, clique em **[!UICONTROL Manage Data** > **Connections]** e em **[!UICONTROL Add a New Data Source]**. Clique no ícone da integração que deseja adicionar e siga as instruções nos tópicos de ajuda para configurar:

* [Perguntas frequentes sobre integração](https://support.magento.com/hc/en-us/sections/360003161871-Integration-FAQ)
* [Integrações `SaaS` e `database` disponíveis](../integrations/integrations.md)
* [Consolidação de tabelas](../../../best-practices/consolidating-your-tables.md)
* [Restrição do acesso ao banco de dados](../../../administrator/account-management/restrict-db-access.md)

**Não está vendo uma integração desejada?** Algumas integrações devem ser ativadas para que fiquem visíveis em sua conta. Se você estiver procurando algo como [!DNL Facebook], mas ele não está listado, [envie um tíquete de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=pt-BR).

**Se você vir um status de erro para uma integração**, confira a [seção Solução de problemas](https://support.magento.com/hc/en-us/sections/360003078151) para obter ajuda.

## Monitorar integridade da atualização (opcional)

Depois de conectar origens, talvez você queira automatizar uma verificação básica de integridade para confirmar se as atualizações completas estão sendo concluídas. Use a [API de Status do Ciclo de Atualização](https://developer.adobe.com/commerce/services/reporting/update-cycle-status-api/) na documentação do desenvolvedor para buscar o ciclo de atualização concluído mais recente para o cliente e exibi-lo em painéis ou alertas internos.
