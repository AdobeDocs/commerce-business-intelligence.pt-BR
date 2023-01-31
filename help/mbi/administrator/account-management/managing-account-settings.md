---
title: Gerenciar as configurações da conta
description: Saiba como personalizar várias configurações de conta para seu data warehouse.
exl-id: 847d51b1-287e-4c14-b64e-0bd9bfcccedc
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# Personalização das configurações da sua conta

>[!NOTE]
>
>Exige [Permissões de administrador.](../../administrator/user-management/user-management.md)

Em seu [!DNL MBI] você pode personalizar várias configurações de conta para seu data warehouse. Elas podem ser acessadas selecionando o nome da organização no canto superior direito de qualquer tela e escolhendo **[!UICONTROL Account Settings]** na lista suspensa.

* **[!UICONTROL Client Name:]** Essa configuração aparece no canto superior direito de todos os painéis e em qualquer outro lugar da conta. Se desejar alterar **[!UICONTROL "Vandelay Industries Co., Ltd]** para apenas **[!UICONTROL "Vandelay]**, este é o local para fazer isso.

* **[!UICONTROL Currency:]** Este é o *moeda padrão* para todos os valores monetários na sua conta. Sempre que um valor decimal ou de moeda é sincronizado com o data warehouse, essa configuração determina o símbolo colocado antes desse valor em seus relatórios.

* **[!UICONTROL Blackout Hours:]** Essa configuração garante que, durante as horas do dia selecionadas, seu data warehouse não acesse seus bancos de dados conectados. Todas as horas são expressas em zero hora e no horário padrão do leste (EST). Por exemplo, se você não quiser que seu banco de dados de produção seja acessado entre as horas de 9:00 EST e 1:00 EST, digite a seguinte matriz de dígitos: **9, 10, 11, 12**.

* **[!UICONTROL Forced update hours:]** Essa configuração garante que uma atualização do data warehouse comece automaticamente em sua conta *na(s) hora(s)* você especificou. Tal como acontece com as horas de blecaute, estas também estão em ET. Por exemplo, se você deseja que as atualizações do data warehouse comecem automaticamente em **meia-noite** e **meio-dia** EST, você deve digitar a seguinte matriz de dígitos: **0, 12**.

* **[!UICONTROL Send email summaries if the data has not updated yet:]** Essa opção informa ao sistema o que fazer em situações em que um resumo de email é programado para ser enviado *antes dos dados em um de seus relatórios* é atualizado até o presente. Se você escolher **Não**, sua conta ignorará o envio do email no horário agendado e, em vez disso, o enviará após a atualização dos dados. Se você escolher **[!UICONTROL Yes]**, sua conta enviará o email, incluirá uma mensagem explicando que os dados estão obsoletos e enviará outro email após a atualização dos dados.

* **[!UICONTROL Enable data updates:]** Essa opção garante que as atualizações de dados sejam executadas em sua conta. Se você alterar a configuração para **[!UICONTROL No]**, sincronizações de dados e cálculos de coluna interromperão completamente em sua conta do .

>[!NOTE]
>
>Certifique-se de selecionar **[!UICONTROL Save Customizations]** depois de fazer qualquer alteração.
