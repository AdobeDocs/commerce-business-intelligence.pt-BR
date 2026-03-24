---
title: Conectar o Google Adwords
description: Saiba como medir o ROI da campanha casando seu custo de publicidade e o valor vitalício do cliente (CLV) dos usuários adquiridos de suas campanhas.
exl-id: db99f817-2a2e-4194-9dd2-ec2d6b27a118
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/mZ8R2vPyFy8pGpYi4KhqocVnP-OlgMPGU3KJ4C9vsTo
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 322
ht-degree: 0%

---

# Conectar [!DNL Google Adwords]

>[!NOTE]
>
>Requer [permissões de administrador](../../../administrator/user-management/user-management.md).

![Logotipo do Google AdWords](../../../assets/Google_Adwords_logo.png)

Você fez sua pesquisa, criou seus anúncios, iniciou sua campanha [!DNL Google]. Agora é hora de analisar seus dados de gastos com anúncios e ver se seu dinheiro está sendo gasto de maneira eficaz. Usando seus dados de gastos com anúncios, você pode [medir o ROI da campanha ao casar seu custo de publicidade com o valor vitalício do cliente (CLV)](../../analysis/roi-ad-camp.md) dos usuários adquiridos de suas campanhas.

Comece digitando suas credenciais do [!DNL Google Adwords] em [!DNL Commerce Intelligence].

1. Vá para a página `Connections` em **Gerenciar Dados > Integrações**.
1. Clique em **Adicionar integração**, localizado no lado superior direito da tela.
1. Clique no ícone **[!DNL Google Adwords]**. Isso abre a página de credenciais do [!DNL Google Adwords].
1. Insira suas credenciais do [!DNL Google Analytics]. Após a conclusão do processo de autorização, você será redirecionado de volta para [!DNL Commerce Intelligence].
1. Uma lista de IDs de perfil é exibida. Verifique os perfis aos quais você deseja se conectar [!DNL Commerce Intelligence].

   ![Caixa de diálogo de conexão do Google AdWords mostrando a seleção de perfil](../../../assets/cnnct-profile.png)

1. As alterações são salvas automaticamente, portanto, clique em **[!UICONTROL Back to Connections]** quando terminar.

Se você tiver vários perfis e precisar de ajuda para identificar qual é qual, consulte a seção `Connecting Multiple Google Analytics profiles` abaixo.

## Conectando vários perfis [!DNL Google Analytics]

Você pode ter vários sites conectados a uma única conta do [!DNL Google Analytics], identificada pela sua própria ID de perfil do [!DNL Google Analytics]. Nesse caso, você tem a opção de incluir todas as IDs de perfil em [!DNL Commerce Intelligence]. Marque as IDs de perfil que você deseja incluir durante a etapa de seleção de perfil.

**Para identificar a ID de Perfil do Google Analytics de um site específico:**

1. Fazer logon em [!DNL Google Analytics]
1. Ir para o painel do site específico [!DNL Google Analytics]
1. Examine a URL - a ID do Perfil corresponde aos oito números que seguem `p` no final da linha:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## Desconectando [!DNL Google Adwords]

1. Visite a página [!DNL Google] [configurações da conta](https://www.google.com/account/about/?hl=en).
1. Na seção `Security`, clique em **[!UICONTROL edit]** ao lado de `Authorizing` aplicativos e sites.
1. Clique em **[!UICONTROL revoke access]**.

## Relacionados

* [Reautenticando integrações](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=pt-BR)
* [Rastrear origem da referência de ordem via [!DNL Google ECommerce]](../integrations/google-ecommerce.md)
* [Rastrear a fonte de referência do usuário no banco de dados](../../analysis/google-track-user-acq.md)
* [Descubra as fontes e os canais de aquisição mais valiosos](../../analysis/most-value-source-channel.md)
* [Aumente o ROI em suas campanhas publicitárias](../../analysis/roi-ad-camp.md)
* [Como funciona a atribuição  [!DNL Google Analytics] UTM?](../../analysis/utm-attributes.md)
