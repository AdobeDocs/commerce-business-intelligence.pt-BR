---
title: Auditar dados do Zendesk
description: Saiba mais sobre as etapas para exportar seus dados do Zendesk.
exl-id: 3c8dcc72-3623-4c4e-a941-f431a97571e0
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# Auditar dados do Zendesk

Encontrou algo estranho em seu [[!DNL Zendesk] dados](../integrations/exp-zendesk-data.md)? Para identificar o problema, precisamos explorar seus dados. Isso pode ser feito exportando o [!DNL Zendesk] para um arquivo baixável.

## Ativação da exportação de dados

A exportação de dados não está atualmente ativada para todos [!DNL Zendesk] contas. Para ativar esse recurso, [enviar um tíquete de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en), mencionando seu [!DNL Zendesk] nome do subdomínio.

>[!NOTE]
>
>Somente `Enterprise` e `Plus` no momento, os planos têm acesso a esse recurso.

Após habilitar a exportação de dados, somente os administradores de um domínio de email específico poderão exportar dados de [!DNL Zendesk] conta. Normalmente, esse domínio de email é o mesmo domínio de email que seu [!DNL Zendesk]. O domínio de email do proprietário da conta é usado como padrão, mas você pode alterar o domínio, se necessário.

## Exportar para um arquivo baixável

1. Clique no ícone Admin (logotipo da engrenagem) na barra lateral e escolha **[!UICONTROL Manage** > **Reports]**.
1. Clique no botão **[!UICONTROL Export]** guia .
1. Clique em **[!UICONTROL Request file]** ao lado de Exportação XML completa, como visto na imagem abaixo.

   Neste ponto, uma construção começará; você será notificado por email quando a conclusão for concluída.
   ![reports_export_new.png](../../../assets/reports_export_new.png)

1. Clique no link na sua notificação por email para baixar um arquivo zip contendo o relatório.

   Este link de download é válido por pelo menos três dias.

Esse processo cria um arquivo XML contendo todas as informações armazenadas no [!DNL Zendesk] , incluindo dados de tíquete (com comentários), dados do usuário e dados da conta. Neste ponto, você pode [enviar um tíquete de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) (anexe este arquivo!) para que possamos examinar seus dados mais de perto. Se o arquivo for muito grande, compartilhe-o com a variável [!DNL MBI] equipe via [!DNL Dropbox] ou [!DNL Google Drive].

Para obter mais informações sobre [!DNL Zendesk] exportações de arquivos, consulte o oficial [[!DNL Zendesk] exportar documentação](https://support.zendesk.com/hc/en-us/articles/4408886165402-Exporting-data-to-a-JSON-CSV-or-XML-file).
