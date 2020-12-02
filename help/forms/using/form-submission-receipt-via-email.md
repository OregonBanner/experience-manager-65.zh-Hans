---
title: 通过电子邮件发送表单提交确认
seo-title: 通过电子邮件发送表单提交确认
description: AEM Forms允许您配置电子邮件提交操作，在用户提交表单时向其发送确认。
seo-description: AEM Forms允许您配置电子邮件提交操作，在用户提交表单时向其发送确认。
uuid: c80b1ef4-8fe3-48e0-8fc6-3032dc022a38
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 574de3d5-69ba-4e2f-a8ab-c59f357e4386
docset: aem65
translation-type: tm+mt
source-git-commit: acc2a3977353386d7e1dfd1344a61d78812fe3fc
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---


# 通过电子邮件{#sending-a-form-submission-acknowledgement-via-email}发送表单提交确认

## 自适应表单数据提交{#adaptive-form-data-submission}

自适应表单提供了多种现成的[提交操作](../../forms/using/configuring-submit-actions.md)工作流，用于将表单数据提交到不同的端点。

例如，**[!UICONTROL 发送电子邮件]**&#x200B;提交操作会在自适应表单成功提交时发送电子邮件。 还可以将其配置为发送电子邮件中的表单数据和PDF。

本文详细介绍了在自适应表单上启用“电子邮件”操作的步骤及其提供的不同配置。

>[!NOTE]
>
>您还可以使用&#x200B;**[!UICONTROL 通过电子邮件]**&#x200B;发送PDF选项，以PDF附件的形式通过电子邮件发送完成的表单。 此操作的可用配置选项与&#x200B;**[!UICONTROL 发送电子邮件]**&#x200B;操作的可用选项相同。 “通过电子邮件发送PDF”操作仅对基于XFA的自适应表单可用

## 发送电子邮件操作{#email-action}

“发送电子邮件”操作使作者能够在自适应表单成功提交时自动向一个或多个收件人发送电子邮件。

>[!NOTE]
>
>要使用“发送电子邮件”操作，您需要按照[配置邮件服务](/help/sites-administering/notification.md#configuring-the-mail-service)中的说明配置AEM邮件服务。

### 在自适应表单{#enabling-email-action-on-an-adaptive-form}上启用“发送电子邮件”操作

1. 在&#x200B;**[!UICONTROL edit]**&#x200B;模式下打开自适应表单。

1. 在&#x200B;**[!UICONTROL 内容]**&#x200B;选项卡中，点按&#x200B;**[!UICONTROL 表单容器]**，然后点按![配置](assets/configure-icon.svg)以视图自适应表单属性。

1. 在&#x200B;**[!UICONTROL 提交]**&#x200B;部分，从&#x200B;**[!UICONTROL 提交操作]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 发送电子邮件]**。

   ![提交操作](assets/submission-actions.png)

1. 在&#x200B;**[!UICONTROL To]**、**[!UICONTROL CC]**&#x200B;和&#x200B;**[!UICONTROL BCC]**&#x200B;字段中指定有效的电子邮件ID。

   在&#x200B;**[!UICONTROL 主题]**&#x200B;和&#x200B;**[!UICONTROL 电子邮件模板]**&#x200B;字段中分别指定电子邮件的主题和正文。

   您还可以在字段中指定变量占位符，在这种情况下，当最终用户成功提交表单时，将处理字段的值。 有关详细信息，请参阅[使用自适应表单字段名称动态创建电子邮件内容](../../forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p)。

   如果表单包含文件附件，并且您希望在电子邮件中附加这些文件，请选择&#x200B;**[!UICONTROL 包含附件]**。

   >[!NOTE]
   >
   >如果选择&#x200B;**[!UICONTROL 通过电子邮件发送PDF]**&#x200B;选项，则必须选择包含附件选项。

1. 单击![save](assets/save_icon.svg)以保存更改。

### 使用自适应表单字段名称动态创建电子邮件内容{#using-adaptive-form-field-names-to-dynamically-create-email-content}

自适应表单中的字段名称称为占位符，用户提交表单后，将替换为该字段的值。

在&#x200B;**[!UICONTROL 发送电子邮件]**&#x200B;操作中，可以使用在执行操作时处理的占位符。 这意味着当用户提交表单时，将生成电子邮件的标题（如&#x200B;**[!UICONTROL To]**、**[!UICONTROL CC]**、**[!UICONTROL BCC]**、**[!UICONTROL Subject]**）。

要定义占位符，请在选择&#x200B;**[!UICONTROL 发送电子邮件]**&#x200B;作为提交操作后在字段中指定`${<field name>}`。

例如，如果表单包含名为`email_addr`的&#x200B;**[!UICONTROL 电子邮件地址]**&#x200B;字段，用于捕获用户的电子邮件ID，则可以在&#x200B;**[!UICONTROL To]**、**[!UICONTROL CC]**&#x200B;或&#x200B;**[!UICONTROL 密件抄送]**&#x200B;字段中指定以下内容。

`${email_addr}`

当用户提交表单时，将向表单的`email_addr`字段中输入的电子邮件ID发送电子邮件。

>[!NOTE]
>
>您可以在字段的&#x200B;**[!UICONTROL 编辑]**&#x200B;对话框中找到字段的名称。

变量占位符还可用于&#x200B;**[!UICONTROL 主题]**&#x200B;和&#x200B;**[!UICONTROL 电子邮件模板]**&#x200B;字段。

例如：

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>可重复面板中的字段不能用作变量占位符。

