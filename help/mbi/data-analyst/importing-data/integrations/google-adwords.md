---
title: Conectar o Google Adwords
description: Saiba como medir o ROI da campanha casando seu custo de publicidade e o valor vitalício do cliente (CLV) dos usuários adquiridos de suas campanhas.
exl-id: db99f817-2a2e-4194-9dd2-ec2d6b27a118
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# Conectar [!DNL Google Adwords]

>[!NOTE]
>
>Exige [Permissões de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/Google_Adwords_logo.png)

Você fez sua pesquisa, você criou seus anúncios, você lançou seu [!DNL Google] campanha. Agora é hora de analisar seus dados de gastos com anúncios e ver se seu dinheiro está sendo gasto de maneira eficaz. Usando seus dados de gastos com anúncios, você pode [meça o ROI da campanha casando seu custo de publicidade com o valor vitalício do cliente (CLV)](../../analysis/roi-ad-camp.md) de usuários adquiridos de suas campanhas.

Comece digitando seu [!DNL Google Adwords] credenciais para [!DNL Commerce Intelligence].

1. Vá para a `Connections` página abaixo **Gerenciar dados > Integrações**.
1. Clique em **Adicionar integração**, localizado no lado superior direito da tela.
1. Clique em **[!DNL Google Adwords]** ícone. Isso abre o [!DNL Google Adwords] página de credenciais.
1. Insira seu [!DNL Google Analytics] credenciais. Após a conclusão do processo de autorização, você será redirecionado de volta para [!DNL Commerce Intelligence].
1. Uma lista de IDs de perfil é exibida. Marque os perfis aos quais deseja se conectar [!DNL Commerce Intelligence].

   ![](../../../assets/cnnct-profile.png)

1. As alterações são salvas automaticamente, portanto, clique em **[!UICONTROL Back to Connections]** quando terminar.

Se você tiver vários perfis e precisar de ajuda para identificar qual é qual, consulte `Connecting Multiple Google Analytics profiles` abaixo.

## Conectando vários [!DNL Google Analytics] perfis

Você pode ter vários sites conectados a um único [!DNL Google Analytics] conta, identificada pelos seus próprios [!DNL Google Analytics] ID do perfil. Nesse caso, você tem a opção de incluir todas as IDs de perfil no [!DNL Commerce Intelligence]. Marque as IDs de perfil que você deseja incluir durante a etapa de seleção de perfil.

**Para identificar a ID de perfil do Google Analytics de um site específico:**

1. Efetue logon no [!DNL Google Analytics]
1. Ir para o site específico [!DNL Google Analytics] painel
1. Examine o URL - a ID do perfil corresponde aos oito números seguintes `p` no final da linha:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## Desconectando [!DNL Google Adwords]

1. Visite seu [!DNL Google] [configurações da conta](https://www.google.com/account/about/?hl=en) página.
1. No `Security` clique em **[!UICONTROL edit]** ao lado de `Authorizing` aplicativos e sites.
1. Clique em **[!UICONTROL revoke access]**.

## Relacionados

* [Reautenticação de integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Rastrear origem de referência de ordem via [!DNL Google ECommerce]](../integrations/google-ecommerce.md)
* [Rastrear a fonte de referência do usuário no banco de dados](../../analysis/google-track-user-acq.md)
* [Descubra as fontes e os canais de aquisição mais valiosos](../../analysis/most-value-source-channel.md)
* [Aumente o ROI em suas campanhas publicitárias](../../analysis/roi-ad-camp.md)
* [Como o [!DNL Google Analytics] A atribuição UTM funciona?](../../analysis/utm-attributes.md)
