---
title: Conectar o Adobe Analytics
description: Saiba como reunir o foco completo de jornada do cliente do [!DNL Adobe Analytics] e o foco do eCommerce no qual você depende [!DNL MBI].
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Connect [!DNL Adobe Analytics]

>[!NOTE]
>
>Exige [Permissões de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/adobe-analytic-slogo.png)

O [!DNL Adobe Analytics] integração para [!DNL MBI] permite que você reúna o foco completo de jornada do cliente de [!DNL Adobe Analytics] e o foco do eCommerce no qual você depende [!DNL MBI], para obter uma imagem mais completa do desempenho geral da sua loja.

Mais especificamente, a variável [!DNL Adobe Analytics] integração para [!DNL MBI] O oferece funcionalidade para que os comerciantes comecem a combinar seus conjuntos de dados do Commerce e do Analytics .
- Crie uma conexão do [!DNL Adobe Analytics] conta em [!DNL MBI].
- Selecione até 25 métricas e dimensões de 1 conjunto de relatórios para replicar em seu [!DNL MBI] data warehouse.
- Usar todos os padrões [!DNL MBI] funcionalidade para transformar, associar e gerar relatórios sobre [!DNL Adobe Analytics] dados.

## Pré-requisitos de conexão

As seguintes informações são necessárias para se conectar:
- [!DNL Adobe Analytics] credenciais de logon
- `Name` e/ou `ID` de [!DNL Adobe Analytics] conjunto de relatórios do qual replicar dados
- Lista de métricas e dimensões para as quais replicar [!DNL MBI]

## Conectando o [!DNL Adobe Analytics] Integração para MBI

1. Vá para o `Integrations` página abaixo **[!DNL Manage Data** > **Integrations]**.
1. Clique em **[!UICONTROL Add an Integration]**, localizado no lado direito da tela.
1. Clique no botão **[!UICONTROL Adobe Analytics]** para acessar a página que permite autorizar o [!DNL Adobe Analytics] conexão de conta.
1. Clique em **[!UICONTROL Authorize with Adobe Analytics]**.
1. Insira seu [!DNL Adobe Analytics] credenciais. Após uma autorização bem-sucedida, você é redirecionado para [!DNL MBI].
1. Uma lista de conjuntos de relatórios disponíveis é exibida. Selecione o conjunto de relatórios do qual deseja importar os dados e clique em **[!UICONTROL Continue]**.
1. A tela de seleção de métricas e dimensões é exibida. Selecione pelo menos uma métrica e pelo menos uma dimensão, até um total combinado de 25 métricas e dimensões. Pesquise por nome ou role até encontrar seus componentes e clique nas caixas de seleção para selecionar. Clique em **[!UICONTROL Continue]**.
1. O conjunto de relatórios selecionado é exibido em uma tabela. Clique em **[!UICONTROL Save]** para confirmar a seleção.
1. Informe o [!DNL MBI] Equipe de suporte autorizada pela sua integração e que executará o processo de conexão inicial para você.

Depois que o processo de conexão inicial for executado, a tabela estará disponível na página Data Warehouse, sob a `All Tables` guia . Selecione as colunas que deseja replicar e os dados serão exibidos após a próxima atualização completa.
