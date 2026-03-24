---
title: Conectar o Adobe Analytics
description: Saiba como reunir o foco completo da jornada do cliente do  [!DNL Adobe Analytics] e o foco do eCommerce do qual você depende [!DNL Commerce Intelligence].
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/KkiKySM2q8ewqhQ1kdUjLuTM4iOpzrZb5Ok-UvBBpJE
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 312
ht-degree: 0%

---

# Conectar [!DNL Adobe Analytics]

>[!NOTE]
>
>Requer [permissões de administrador](../../../administrator/user-management/user-management.md).

![logotipo do Adobe Analytics](../../../assets/adobe-analytic-slogo.png)

A integração do [!DNL Adobe Analytics] para [!DNL Adobe Commerce Intelligence] permite reunir o foco de jornada completa do cliente do [!DNL Adobe Analytics] e o foco de comércio eletrônico do qual você depende a partir do [!DNL Commerce Intelligence]. Isso dá uma imagem completa do desempenho geral da sua loja.

Mais especificamente, a integração do [!DNL Adobe Analytics] para [!DNL Commerce Intelligence] fornece funcionalidade para que os comerciantes comecem a combinar seus conjuntos de dados [!DNL Adobe Commerce] e [!DNL Adobe Analytics].

- Crie uma conexão da sua conta existente do [!DNL Adobe Analytics] com o [!DNL Commerce Intelligence].

- Selecione até 25 métricas e dimensões de um conjunto de relatórios para replicar em sua Data Warehouse.

- Use toda a funcionalidade padrão [!DNL Commerce Intelligence] para transformar, ingressar e gerar relatórios sobre dados [!DNL Adobe Analytics] replicados.

## Pré-requisitos de conexão

As seguintes informações são necessárias para se conectar:

- [!DNL Adobe Analytics] credenciais de logon

- `Name` e/ou `ID` de [!DNL Adobe Analytics] conjunto de relatórios do qual replicar dados

- Lista de métricas e dimensões para replicar em [!DNL Commerce Intelligence]

## Conectando a Integração do [!DNL Adobe Analytics] para [!DNL Commerce Intelligence]

1. Vá para a página `Integrations` em **[!DNL Manage Data** > **Integrations]**.

1. Clique em **[!UICONTROL Add an Integration]**.

1. Clique no ícone **[!UICONTROL Adobe Analytics]** para acessar a página que permite autorizar a conexão da conta [!DNL Adobe Analytics].

1. Clique em **[!UICONTROL Authorize with Adobe Analytics]**.

1. Insira suas credenciais do [!DNL Adobe Analytics]. Após a autorização bem-sucedida, você será redirecionado de volta para [!DNL Commerce Intelligence].

1. Uma lista de conjuntos de relatórios disponíveis é exibida. Selecione o conjunto de relatórios do qual deseja importar os dados e clique em **[!UICONTROL Continue]**.

1. A tela de seleção de métricas e dimensões é exibida. Selecione pelo menos uma métrica e pelo menos uma dimensão, até um total combinado de 25 métricas e dimensões. Pesquise por nome ou role para encontrar seus componentes e clique nas caixas de seleção para selecionar. Clique em **[!UICONTROL Continue]**.

1. O conjunto de relatórios selecionado é exibido em uma tabela. Clique em **[!UICONTROL Save]** para confirmar a seleção.

1. Informe à [!DNL Commerce Intelligence] [Equipe de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) que sua integração está autorizada e que eles executam o processo de conexão inicial para você.

Depois que o processo de conexão inicial for executado, sua tabela estará disponível na página do Data Warehouse, na guia `All Tables`. Selecione as colunas que deseja replicar e os dados aparecerão após a próxima atualização completa.
