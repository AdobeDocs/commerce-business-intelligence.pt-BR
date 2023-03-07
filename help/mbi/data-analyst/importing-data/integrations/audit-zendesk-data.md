---
title: Auditoria de dados do Zendesk
description: Saiba mais sobre as etapas para exportar seus dados do Zendesk.
exl-id: 3c8dcc72-3623-4c4e-a941-f431a97571e0
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Auditoria de dados do Zendesk

Encontrei algo estranho em seu [[!DNL Zendesk] dados](../integrations/exp-zendesk-data.md)? Para apontar o problema, você precisa explorar seus dados. Isso pode ser feito exportando suas [!DNL Zendesk] para um arquivo baixável.

## Ativação da exportação de dados

A exportação de dados não está habilitada no momento para todos [!DNL Zendesk] contas. Para ativar esse recurso, [enviar um tíquete de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en), mencionando seu [!DNL Zendesk] nome do subdomínio.

>[!NOTE]
>
>Somente `Enterprise` e `Plus` Os planos do atualmente têm acesso a esse recurso.

Depois que a exportação de dados estiver ativada, somente os administradores em um domínio de email específico poderão exportar dados do [!DNL Zendesk] conta. Normalmente, esse domínio de email é o mesmo domínio de email que seu [!DNL Zendesk]. O domínio de email do proprietário da conta é usado como padrão, mas você pode alterar o domínio, se necessário.

## Exportar para um arquivo baixável

1. Clique no ícone Admin (logotipo da engrenagem) na barra lateral e escolha **[!UICONTROL Manage** > **Reports]**.
1. Clique em **[!UICONTROL Export]** guia.
1. Clique em **[!UICONTROL Request file]** ao lado da Exportação de XML completo, como visto na imagem abaixo.

   Nesse ponto, uma criação é iniciada; você é notificado por email quando ela é concluída.
   ![reports_export_new.png](../../../assets/reports_export_new.png)

1. Clique no link em sua notificação por email para baixar um arquivo zip que contém o relatório.

   Esse link de download é válido por pelo menos três dias.

Esse processo cria um arquivo XML contendo todas as informações armazenadas no seu [!DNL Zendesk] conta, incluindo dados de tíquete (com comentários), dados do usuário e dados da conta. Nesse ponto, é possível [enviar um tíquete de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) (certifique-se de anexar esse arquivo!) para que você possa examinar seus dados mais de perto. Se o arquivo for muito grande, compartilhe-o com o [!DNL MBI] equipe via [!DNL Dropbox] ou [!DNL Google Drive].

Para obter mais informações sobre [!DNL Zendesk] exportação de arquivos, consulte o documento oficial [[!DNL Zendesk] documentação de exportação](https://support.zendesk.com/hc/en-us/articles/4408886165402-Exporting-data-to-a-JSON-CSV-or-XML-file).
