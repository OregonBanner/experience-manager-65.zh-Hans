---
title: 通过电子邮件发送表单提交确认
description: AEM Forms允许您配置电子邮件提交操作，以在提交表单时向用户发送确认。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: bca4044a-18a9-4b97-92de-eff1e9a840f9
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 0%

---

# 通过电子邮件发送表单提交确认 {#sending-a-form-submission-acknowledgement-via-email}

## 自适应表单数据提交 {#adaptive-form-data-submission}

自适应表单提供了多个现成的表单 [提交操作](../../forms/using/configuring-submit-actions.md) 用于将表单数据提交到不同端点的工作流。

例如， **[!UICONTROL 发送电子邮件]** 提交操作会在成功提交自适应表单时发送电子邮件。 您还可以将其配置为通过电子邮件发送表单数据和PDF。

本文详细介绍在自适应表单及其提供的不同配置上启用电子邮件操作的步骤。

>[!NOTE]
>
>您也可以使用 **[!UICONTROL 通过电子邮件发送PDF]** 选项，通过电子邮件将填写的表单作为PDF附件发送。 可用于此操作的配置选项与可用于的选项相同。 **[!UICONTROL 发送电子邮件]** 操作。 电子邮件PDF操作仅适用于基于XFA的自适应表单

## 发送电子邮件操作 {#email-action}

利用“发送电子邮件”操作，作者可在自适应表单成功提交后自动向一个或多个收件人发送电子邮件。

>[!NOTE]
>
>要使用“发送电子邮件”操作，您需要配置AEM邮件服务，如中所述 [配置邮件服务](/help/sites-administering/notification.md#configuring-the-mail-service).

### 在自适应表单上启用“发送电子邮件”操作 {#enabling-email-action-on-an-adaptive-form}

1. 在中打开自适应表单 **[!UICONTROL 编辑]** 模式。

1. 在 **[!UICONTROL 内容]** 选项卡，选择 **[!UICONTROL 表单容器]** 并选择 ![配置](assets/configure-icon.svg) 查看自适应表单属性。

1. 在 **[!UICONTROL 提交]** 部分，选择 **[!UICONTROL 发送电子邮件]** 从 **[!UICONTROL 提交操作]** 下拉列表。

   ![提交操作](assets/submission-actions.png)

1. 在中指定有效的电子邮件ID **[!UICONTROL 至]**， **[!UICONTROL 抄送]**、和 **[!UICONTROL 密件抄送]** 字段。

   在中指定电子邮件的主题和正文 **[!UICONTROL 主题]** 和 **[!UICONTROL 电子邮件模板]** 字段。

   您还可以在字段中指定变量占位符，在这种情况下，当最终用户成功提交表单时，将处理字段的值。 有关更多信息，请参阅 [使用自适应表单字段名称动态创建电子邮件内容](../../forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p).

   选择 **[!UICONTROL 包括附件]** 如果表单包含文件附件，并且您希望在电子邮件中附加这些文件。

   >[!NOTE]
   >
   >如果您选择 **[!UICONTROL 通过电子邮件发送PDF]** 选项，则必须选择包括附件选项。

1. 单击 ![保存](assets/save_icon.svg) 以保存更改。

### 使用自适应表单字段名称动态创建电子邮件内容 {#using-adaptive-form-field-names-to-dynamically-create-email-content}

自适应表单中的字段名称称为占位符，在用户提交表单后，这些占位符将替换为该字段的值。

在 **[!UICONTROL 发送电子邮件]** 操作，则可以使用在执行操作时处理的占位符。 这意味着电子邮件的标题(如 **[!UICONTROL 至]**， **[!UICONTROL 抄送]**， **[!UICONTROL 密件抄送]**， **[!UICONTROL 主题]**)将在用户提交表单时生成。

要定义占位符，请指定 `${<field name>}` 在字段中选择 **[!UICONTROL 发送电子邮件]** 作为“提交”操作。

例如，如果表单包含 **[!UICONTROL 电子邮件地址]** 字段，已命名 `email_addr`，要捕获用户的电子邮件ID，您可以在 **[!UICONTROL 至]**， **[!UICONTROL 抄送]**，或 **[!UICONTROL 密件抄送]** 字段。

`${email_addr}`

当用户提交表单时，会向中输入的电子邮件ID发送电子邮件 `email_addr` 表单的字段。

>[!NOTE]
>
>您可以在以下位置找到字段名称： **[!UICONTROL 编辑]** 字段对应的对话框。

变量占位符还可用于 **[!UICONTROL 主题]** 和 **[!UICONTROL 电子邮件模板]** 字段。

例如：

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>可重复面板中的字段不能用作变量占位符。
