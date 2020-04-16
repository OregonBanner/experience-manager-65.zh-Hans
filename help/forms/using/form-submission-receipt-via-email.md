---
title: 通过电子邮件发送表单提交确认
seo-title: 通过电子邮件发送表单提交确认
description: AEM Forms允许您配置电子邮件提交操作，该操作在提交表单时向用户发送确认。
seo-description: AEM Forms允许您配置电子邮件提交操作，该操作在提交表单时向用户发送确认。
uuid: c80b1ef4-8fe3-48e0-8fc6-3032dc022a38
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 574de3d5-69ba-4e2f-a8ab-c59f357e4386
docset: aem65
translation-type: tm+mt
source-git-commit: acc2a3977353386d7e1dfd1344a61d78812fe3fc

---


# 通过电子邮件发送表单提交确认 {#sending-a-form-submission-acknowledgement-via-email}

## 自适应表单数据提交 {#adaptive-form-data-submission}

自适应表单提供了多种现成的提交操作 [工作流](../../forms/using/configuring-submit-actions.md) ，用于将表单数据提交到不同的端点。

例如，“发送电 **[!UICONTROL 子邮件]** ”提交操作会在自适应表单成功提交时发送电子邮件。 还可以将其配置为发送电子邮件中的表单数据和PDF。

本文详细介绍了在自适应表单上启用电子邮件操作的步骤及其提供的不同配置。

>[!NOTE]
>
>您还可以使用“通过电子邮件 **[!UICONTROL 发送PDF”选项]** ，以PDF附件的形式通过电子邮件发送完成的表单。 此操作的可用配置选项与“发送电子邮件”操作的可用 **[!UICONTROL 选项相同]** 。 “通过电子邮件发送PDF”动作仅适用于基于XFA的自适应表单

## 发送电子邮件操作 {#email-action}

通过“发送电子邮件”动作，作者可以在自适应表单成功提交时自动向一个或多个收件人发送电子邮件。

>[!NOTE]
>
>要使用“发送电子邮件”操作，您需要配置AEM邮件服务，如配置邮 [件服务中所述](/help/sites-administering/notification.md#configuring-the-mail-service)。

### 在自适应表单上启用“发送电子邮件”操作 {#enabling-email-action-on-an-adaptive-form}

1. 在编辑模式下打开自适 **[!UICONTROL 应表单]** 。

1. 在“内 **[!UICONTROL 容]** ”选项卡中，点 **[!UICONTROL 按表单容器]** ，然后点 ![按配置](assets/configure-icon.svg) ，以视图自适应表单属性。

1. 在“提 **[!UICONTROL 交]** ”部分，从“提交操作”下拉 **[!UICONTROL 列表中选]** 择“发送电子邮件 **** ”。

   ![提交操作](assets/submission-actions.png)

1. 在“收件人”、“抄送” **[!UICONTROL 和“密件抄送]**”字段中指定有 **[!UICONTROL 效的电子邮件]** ID **** 。

   在“主题”和“电子邮件模板”字段中分别指 **[!UICONTROL 定电子邮件]****[!UICONTROL 的主题和正]** 文。

   您还可以在字段中指定变量占位符，在这种情况下，当最终用户成功提交表单时，将处理字段的值。 有关详细信息，请参 [阅使用自适应表单字段名称动态创建电子邮件内容](../../forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p)。

   如果 **[!UICONTROL 表单包含文件附件]** ，并且您希望将这些文件附加到电子邮件中，请选择“包含附件”。

   >[!NOTE]
   >
   >如果选择“通过电 **[!UICONTROL 子邮件发送PDF]** ”选项，则必须选择“包括附件”选项。

1. Click ![save](assets/save_icon.svg) to save the changes.

### 使用自适应表单字段名称动态创建电子邮件内容 {#using-adaptive-form-field-names-to-dynamically-create-email-content}

自适应表单中的字段名称称为占位符，用户提交表单后，这些占位符将替换为该字段的值。

在“发 **[!UICONTROL 送电子邮件]** ”操作中，您可以使用在执行操作时处理的占位符。 这意味着当用户提交表单时，会生成电子邮件的标题( **[!UICONTROL 如To]**、 **[!UICONTROL CC]**、 **[!UICONTROL BCC]**、Subject ****)。

要定义占位符，请在选择“ `${<field name>}` 发送电子邮件”作为“提 **[!UICONTROL 交操作]** ”后在字段中指定。

例如，如果包含“电子邮件地址 **[!UICONTROL ”字段，]** 则为了捕获用户的电子邮件ID，可以在“收件人”、“ `email_addr`CC ************ ”、“密件抄送”或“密件抄送”表单字段中指定以下字段。

`${email_addr}`

当用户提交表单时，会向在表单字段中输入的电子邮件ID `email_addr` 发送电子邮件。

>[!NOTE]
>
>您可以在字段的“编辑”对话 **[!UICONTROL 框中]** ，找到字段的名称。

变量占位符也可用于“主题”和“电 **[!UICONTROL 子邮件]****[!UICONTROL 模板”字段]** 。

例如：

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>可重复面板中的字段不能用作变量占位符。

