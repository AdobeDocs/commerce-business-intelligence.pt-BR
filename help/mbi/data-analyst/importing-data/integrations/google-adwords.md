---
title: Conexão de palavras-chave do Google
description: Saiba como medir o ROI da campanha, casando-se com seu custo de publicidade e o valor da vida útil do cliente (CLV) dos usuários adquiridos de suas campanhas.
exl-id: db99f817-2a2e-4194-9dd2-ec2d6b27a118
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Connect [!DNL Google Adwords]

>[!NOTE]
>
>Exige [Permissões de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/Google_Adwords_logo.png)

Você fez sua pesquisa, criou seus anúncios, lançou sua campanha. Agora é hora de analisar os dados de gastos com publicidade e ver se seu dinheiro está sendo gasto de maneira eficaz. Com os dados de gastos com sua publicidade, você pode [avalie o ROI da campanha relacionando-se com seu custo de publicidade e o valor da vida útil do cliente (CLV)](../../analysis/roi-ad-camp.md) de usuários adquiridos em suas campanhas.

Vamos começar entrando em nosso [!DNL Google Adwords] credenciais em [!DNL MBI]:

1. Vá para a página Conexões em **Gerenciar dados > Integrações**.
1. Clique em **Adicionar integração**, localizado no lado superior direito da tela.
1. Clique no botão **[!DNL Google Adwords]** ícone . Isso abrirá o [!DNL Google Adwords] credenciais.
1. Insira seu [!DNL Google Analytics] credenciais. Após a conclusão do processo de autorização, você será redirecionado para [!DNL MBI].
1. Uma lista de IDs de perfil será exibida. Verifique os perfis aos quais deseja se conectar [!DNL MBI].

   ![](../../../assets/cnnct-profile.png)

1. As alterações são salvas automaticamente, portanto, clique em **[!UICONTROL Back to Connections]** quando terminar.

Se você tiver vários perfis e precisar de ajuda para identificar qual, consulte a `Connecting Multiple Google Analytics profiles` abaixo.

## `Connecting multiple Google Analytics profiles`

Você pode ter vários sites conectados a um único [!DNL Google Analytics] , identificada por sua própria conta [!DNL Google Analytics] ID do perfil. Nesse caso, você terá a opção de incluir todas as IDs de perfil no [!DNL MBI]. Basta verificar as IDs de perfil que deseja incluir durante a etapa de seleção de perfil.

**Para identificar a ID de perfil do Google Analytics de um site específico:**

1. Faça logon [!DNL Google Analytics]
1. Vá para o site específico [!DNL Google Analytics] painel
1. Examine o URL - a ID de perfil corresponde aos 8 números que seguem `p` no final da linha:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## Desconectar [!DNL Google Adwords]

1. Visite seu [!DNL Google] [configurações da conta](https://www.google.com/accounts/) página.
1. Em `Security` e clique em **[!UICONTROL edit]** ao lado de `Authorizing` aplicativos e sites.
1. Clique em **[!UICONTROL revoke access]** ao lado de [!DNL MBI].

## Relacionado

* [Reautenticação de integrações](https://support.magento.com/hc/en-us/articles/360016733151)
* [Rastrear origem de referência do pedido via [!DNL Google ECommerce]](../integrations/google-ecommerce.md)
* [Rastrear a fonte de referência do usuário no seu banco de dados](../../analysis/google-track-user-acq.md)
* [Rastrear dados do dispositivo do usuário, do navegador e do SO no seu banco de dados](https://support.magento.com/hc/en-us/articles/360016732911)
* [Descubra as fontes e os canais de aquisição mais valiosos](../../analysis/most-value-source-channel.md)
* [Aumente o ROI em suas campanhas publicitárias](../../analysis/roi-ad-camp.md)
* [Como [!DNL Google Analytics] A atribuição de UTM funciona?](../../analysis/utm-attributes.md)
