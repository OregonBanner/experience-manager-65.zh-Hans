---
title: 在分配任务步骤中使用自定义电子邮件模板
seo-title: Use custom email templates in an Assign Task step
description: 表单工作流电子邮件通知的自定义电子邮件模板
seo-description: Custom email templates for forms workflow email notifications
uuid: ba453d54-813f-4a4f-a82e-1a6a28b6939c
topic-tags: publish
discoiquuid: 2ad4b7b5-2162-4599-af3f-9476f1256de6
docset: aem65
exl-id: d4035c91-ee8d-4f12-bdac-e3912be732d7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 1%

---

# 在分配任务步骤中使用自定义电子邮件模板{#use-custom-email-templates-in-an-assign-task-step}

您可以使用“分配任务”步骤来创建任务并将其分配给用户或组。 将任务分配给用户或组时，会向定义的用户或定义的组的每个成员发送电子邮件通知。 典型的电子邮件通知包含已分配任务的链接以及与该任务相关的信息。 下图显示了一个示例电子邮件通知：

![使用现成模板发送电子邮件通知](do-not-localize/default_email_template_new.png)

您可以自定义外观，并在电子邮件通知中使用自定义元数据。 AEM Forms为电子邮件通知提供了一个现成的模板。 您可以自定义现成模板或从头开始创建新模板。

电子邮件通知模板基于 [HTML电子邮件](https://en.wikipedia.org/wiki/HTML_email). 这些电子邮件会适应不同的电子邮件客户端和屏幕大小。 此外，电子邮件的样式在模板中定义。

下图显示了自定义的电子邮件通知：

![使用自定义模板的电子邮件通知](do-not-localize/customized-email.png)

## 自定义现有模板 {#customize-the-existing-template}

开箱即用的AEM Forms提供了电子邮件通知模板。 模板提供已分配任务的标题描述、截止日期、优先级、工作流名称和链接。 可以自定义模板以更改外观。 执行以下步骤以自定义模板：

1. 使用管理员帐户登录CRXDE。

1. 导航到/libs/fd/dashboard/templates/email。

1. 打开htmlEmailTemplate.txt文件。 它包含默认模板。

1. 将htmlEmailTemplate.txt文件的内容替换为自定义内容。

   电子邮件通知模板是 [HTML电子邮件](https://en.wikipedia.org/wiki/HTML_email). 您可以使用自定义代码替换现有的html代码以更改模板的外观。

1. 保存文件。现在，自定义模板已可供使用。

## 创建电子邮件模板 {#create-an-email-template}

开箱即用的AEM Forms提供了电子邮件通知模板。 模板提供已分配任务的标题描述、截止日期、优先级、工作流名称和链接。 您还可以为分配任务步骤添加自定义电子邮件模板（您自己的模板）。 执行以下步骤可添加自定义电子邮件模板：

1. 使用管理员帐户登录CRXDE。

1. 导航到/libs/fd/dashboard/templates/email。

1. 创建.txt文件。 例如，EmailOnTaskAssign.txt。

1. 将自定义HTML代码添加到文件中。

   电子邮件通知模板是 [HTML电子邮件](https://en.wikipedia.org/wiki/HTML_email). 您可以将自定义HTML代码添加到文件中以创建新模板。

1. 保存文件。该模板已准备好用于分配任务步骤。

## 在“分配任务”步骤中使用电子邮件模板 {#use-an-email-template-in-an-assign-task-step}

开箱即用的“分配任务”步骤配置为使用默认模板htmlEmailTemplate.txt。 您可以选择使用自定义模板。 要更改模板，请执行以下操作：

1. 打开分配任务步骤。

1. 导航到“被分派人”>“HTML电子邮件模板”。

1. 选择新创建的HTML电子邮件模板。

1. 单击确定。模板已更改。

电子邮件通知还使用 [元数据](../../forms/using/use-metadata-in-email-notifications.md). 例如，到期日期、优先级、工作流名称等。 您还可以配置要使用的模板 [自定义元数据](../../forms/using/use-metadata-in-email-notifications.md#using-custom-metadata-in-an-email-notification).
