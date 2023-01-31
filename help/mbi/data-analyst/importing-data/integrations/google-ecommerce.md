---
title: Connect Google Commerce
description: Saiba mais sobre seus canais de referência mais valiosos.
exl-id: c80f52f3-894a-4084-8c0e-aee618ed77f5
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# Connect [!DNL Google ECommerce]

>[!NOTE]
>
>Exige [Permissões de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/google-ecommerce-logo.png)

Você tem um fluxo contínuo de tráfego e pedidos, o que significa que está atingindo e adquirindo clientes com eficiência. Mas quais são seus canais de referência mais valiosos? qual é o valor médio da vida útil dos clientes adquirido de uma origem contra outra? Ao conectar seus dados de origem de referência de pedido de [!DNL Google ECommerce] para [!DNL MBI], é possível criar análises que ajudarão a identificar [canais de marketing mais valiosos](../../../data-analyst/analysis/most-value-source-channel.md).

Vamos começar entrando em nosso [!DNL Google ECommerce] credenciais em [!DNL MBI]:

1. Vá para o `Connections` página abaixo **[!UICONTROL Admin** > **Connections]**.
1. Clique em **[!UICONTROL Add a New Source]**, localizado no lado direito do ecrã acima da `Data Sources` tabela.
1. Clique no botão [!DNL Google ECommerce] ícone . Isso abrirá o [!DNL Google ECommerce] credenciais.
1. Insira seu [!DNL Google Analytics] credenciais. Ao concluir o processo de autorização, você será redirecionado para [!DNL MBI].
1. Uma lista de IDs de perfil será exibida. Verifique os perfis aos quais deseja se conectar [!DNL MBI].

   Se você tiver vários perfis e precisar de ajuda para identificar qual, consulte **Conexão múltipla [!DNL Google Analytics] seção de perfis abaixo.

   ![](../../../assets/conn-mult-ga-profiles.png)<!--{: width="500"}-->

1. As alterações são salvas automaticamente, portanto, basta clicar em **[!UICONTROL Back to Connections]** quando você terminar.

## Conexão múltipla [!DNL Google Analytics] perfis para [!DNL MBI]

Você pode ter vários sites conectados a um único [!DNL Google Analytics] , identificada por sua própria conta [!DNL Google Analytics] ID do perfil. Nesse caso, você terá a opção de incluir todas as IDs de perfil no [!DNL MBI]. Basta verificar as IDs de perfil que você deseja incluir durante a etapa de seleção de perfil.

Para identificar um site específico [!DNL Google Analytics] ID do perfil:

1. Faça logon [!DNL Google Analytics]
1. Vá para o site específico [!DNL Google Analytics] painel
1. Examine o URL - a ID de perfil corresponde aos 8 números que seguem `p` no final da linha

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Desconectar [!DNL Google ECommerce] from [!DNL MBI] {#disconnect}

1. Visite seu [!DNL Google Analytics] [configurações da conta](https://www.google.com/accounts/) página.
1. Em `Security` seção , clique em **[!UICONTROL edit]** ao lado de `Authorizing` aplicativos e sites.
1. Clique em **[!UICONTROL revoke access]** ao lado de [!DNL MBI].

## Relacionadas:

* [Esperado [!DNL Google ECommerce] dados](../integrations/google-ecommerce-data.md)
* [Reautenticação de integrações](https://support.magento.com/hc/en-us/articles/360016733151)
* [Configuração [!DNL Google ECommerce] tracking](https://support.google.com/analytics/answer/1009612?hl=en)
* [Descubra as fontes e os canais de aquisição mais valiosos](../../analysis/most-value-source-channel.md)
* [Aumente o ROI em suas campanhas publicitárias](../../analysis/roi-ad-camp.md)
