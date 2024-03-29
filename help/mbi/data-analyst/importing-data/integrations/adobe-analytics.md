---
title: Conectar o Adobe Analytics
description: Saiba como reunir o foco completo da jornada do cliente do [!DNL Adobe Analytics] e o foco do eCommerce no qual você depende [!DNL Commerce Intelligence].
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Conectar [!DNL Adobe Analytics]

>[!NOTE]
>
>Exige [Permissões de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/adobe-analytic-slogo.png)

A variável [!DNL Adobe Analytics] integração para [!DNL Adobe Commerce Intelligence] permite reunir o foco completo da jornada do cliente em [!DNL Adobe Analytics] e o foco do eCommerce no qual você depende [!DNL Commerce Intelligence]. Isso dá uma imagem completa do desempenho geral da sua loja.

Mais especificamente, a [!DNL Adobe Analytics] integração para [!DNL Commerce Intelligence] oferece funcionalidade para que os comerciantes comecem a combinar seus [!DNL Adobe Commerce] e [!DNL Adobe Analytics] conjuntos de dados.

- Criar uma conexão a partir de seu existente [!DNL Adobe Analytics] conta em [!DNL Commerce Intelligence].

- Selecione até 25 métricas e dimensões de um conjunto de relatórios para replicar em sua Data Warehouse.

- Usar todos os padrões [!DNL Commerce Intelligence] funcionalidade para transformar, associar e gerar relatórios sobre [!DNL Adobe Analytics] dados.

## Pré-requisitos de conexão

As seguintes informações são necessárias para se conectar:

- [!DNL Adobe Analytics] credenciais de logon

- `Name` e/ou `ID` de [!DNL Adobe Analytics] conjunto de relatórios do qual replicar dados

- Lista de métricas e dimensões para replicar em [!DNL Commerce Intelligence]

## Conectar o [!DNL Adobe Analytics] Integração do [!DNL Commerce Intelligence]

1. Vá para a `Integrations` página abaixo **[!DNL Manage Data** > **Integrations]**.

1. Clique em **[!UICONTROL Add an Integration]**.

1. Clique em **[!UICONTROL Adobe Analytics]** ícone para acessar a página que permite autorizar sua [!DNL Adobe Analytics] conexão com a conta.

1. Clique em **[!UICONTROL Authorize with Adobe Analytics]**.

1. Insira seu [!DNL Adobe Analytics] credenciais. Após a autorização bem-sucedida, você será redirecionado de volta para [!DNL Commerce Intelligence].

1. Uma lista de conjuntos de relatórios disponíveis é exibida. Selecione o conjunto de relatórios do qual deseja importar os dados e clique em **[!UICONTROL Continue]**.

1. A tela de seleção de métricas e dimensões é exibida. Selecione pelo menos uma métrica e pelo menos uma dimensão, até um total combinado de 25 métricas e dimensões. Pesquise por nome ou role para encontrar seus componentes e clique nas caixas de seleção para selecionar. Clique em **[!UICONTROL Continue]**.

1. O conjunto de relatórios selecionado é exibido em uma tabela. Clique em **[!UICONTROL Save]** para confirmar a seleção.

1. Informe o [!DNL Commerce Intelligence] [Equipe de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) que sua integração está autorizada e que eles executam o processo de conexão inicial para você.

Depois que o processo de conexão inicial for executado, sua tabela estará disponível na página Data Warehouse, no `All Tables` guia. Selecione as colunas que deseja replicar e os dados aparecerão após a próxima atualização completa.
