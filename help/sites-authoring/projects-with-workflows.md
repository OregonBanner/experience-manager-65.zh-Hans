---
title: 使用项目工作流
seo-title: Working with Project Workflows
description: 提供了多种开箱即用的项目工作流。
seo-description: A variety of project workflows are available out of the box.
uuid: 376922ca-e09e-4ac8-88c8-23dac2b49dbe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: 9d2bf30c-5190-4924-82cd-bcdfde24eb39
exl-id: 407fc164-291d-42f6-8c46-c1df9ba3d454
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 41%

---


# 使用项目工作流 {#working-with-project-workflows}

现成可用的项目工作流包括：

* **项目审批工作流** – 此工作流让您将内容分配给用户进行审查和批准。
* **请求启动项** – 此工作流用于请求启动项。
* **请求登陆页面** – 此工作流用于请求登陆页面。
* **请求电子邮件** – 此工作流用于请求电子邮件。
* **产品照片拍摄和产品照片拍摄（商务）**  — 将资产与产品映射
* **DAM 创建和翻译副本以及 DAM 创建语言副本** - 为资源和文件夹创建已翻译的二进制文件、元数据和标记。

根据您选择的项目模板，您可以使用特定工作流：

|   | **简单项目** | **媒体项目** | **产品照片拍摄项目** | **翻译项目** |
|---|:-:|:-:|:-:|:-:|
| 请求复制 |  | x |  |  |
| 产品照片拍摄 |  | x | x |  |
| 产品照片拍摄（商务） |  |  | x |  |
| 项目审批 | x |  |  |  |
| 请求启动项 | x |  |  |  |
| 请求登陆页面 | x |  |  |  |
| 请求电子邮件 | x |  |  |  |
| DAM 创建语言副本&amp;ast; |  |  |  | x |
| DAM 创建和翻译语言副本&amp;ast; |  |  |  | x |

>[!NOTE]
>
>&amp;ast;这些工作流不会从项目中的&#x200B;**工作流**&#x200B;拼贴启动。请参阅 [正在创建资产的语言副本。](/help/sites-administering/tc-manage.md)

无论您选择哪个工作流，启动和完成工作流的步骤都是相同的。只是具体的实施步骤有所不同。

您可以直接在项目中启动工作流（DAM 创建语言副本或 DAM 创建和翻译语言副本除外）。项目中任何未完成任务的信息会在&#x200B;**任务**&#x200B;拼贴中列出。用户图标旁边会显示需要完成的任务通知。

有关在AEM中使用工作流的更多信息，请参阅以下文档：

* [参与工作流](/help/sites-authoring/workflows-participating.md)
* [将工作流应用于页面](/help/sites-authoring/workflows-applying.md)
* [配置工作流](/help/sites-administering/workflows.md)

此部分介绍了可用于项目的工作流。

## 请求复制工作流 {#request-copy-workflow}

利用此工作流，可向用户请求手稿，然后审批它。 要启动请求复制工作流，请执行以下操作：

1. 在媒体项目中，点按或单击右上角的向下V形 **工作流** 平铺并选择 **启动工作流**.
1. 在工作流向导中，选择 **请求复制** 并单击 **下一个**.
1. 输入手稿标题和所请求内容的简短摘要。 如果适用，请输入目标字数、任务优先级和截止日期。

   ![请求复制工作流](assets/project-request-copy-workflow.png)

1. 单击&#x200B;**“提交”。**

该工作流随即会启动。任务出现在 **任务** 卡片。

## 产品照片拍摄工作流 {#product-photo-shoot-workflow}

此 **产品照片拍摄** 文档中详细介绍了工作流（商业和非商业） [创意项目](/help/sites-authoring/managing-product-information.md)

## 项目审批工作流 {#project-approval-workflow}

在 **项目审批** 工作流，您可以将内容分配给用户，审阅并批准内容。

1. 在简单项目中，点按或单击右上角的向下V形 **工作流** 平铺并选择 **启动工作流**.
1. 在工作流向导中，选择 **项目审批工作流** 并单击 **下一个**.
1. 输入标题，并选择要为其分配的人员。 在适用的情况下，输入描述、内容路径、任务优先级和到期日期。

   ![项目审批工作流](assets/project-approval-workflow.png)

1. 单击&#x200B;**“提交”。**

该工作流随即会启动。任务出现在 **任务** 卡片。

## 请求启动项工作流程 {#request-launch-workflow}

使用此工作流，您可以请求启动项。

1. 在简单项目中，点按或单击右上角的向下V形 **工作流** 平铺并选择 **启动工作流**.
1. 在工作流向导中，选择 **请求启动项工作流程** 并单击 **下一个**.
1. 输入启动项的标题并提供启动项源路径。在适用的情况下，您还可以添加描述和起始日期。根据您希望启动项具备的行为方式，选择“继承源页面活动数据”或“不包括子页面”。

   ![请求启动工作流](assets/project-request-launch-workflow.png)

1. 单击&#x200B;**“提交”。**

该工作流随即会启动。该工作流将显示在 **工作流** 列表。

## 请求登陆页面工作流 {#request-landing-page-workflow}

此工作流可让您请求登陆页面。

1. 在简单项目中，点按或单击右上角的向下V形 **工作流** 平铺并选择 **启动工作流**.
1. 在工作流向导中，选择 **请求登陆页面** 并单击 **下一个**.
1. 输入登陆页面的标题和父路径。 如果适用，请输入起始日期或为登陆页面选择一个文件。

   ![请求登陆页面工作流](assets/project-request-landing-page-workflow.png)

1. 单击&#x200B;**“提交”。**

该工作流随即会启动。任务出现在 **任务** 卡片。

## 请求电子邮件工作流 {#request-email-workflow}

此工作流可让您请求发送电子邮件。 此工作流与中显示的相同 **电子邮件** 磁贴。

1. 在简单项目中，点按或单击右上角的向下V形 **工作流** 平铺并选择 **启动工作流**.
1. 在工作流向导中，选择 **请求电子邮件** 并单击 **下一个**.
1. 输入电子邮件标题、营销活动和模板路径。 此外，您还可以提供名称、描述和上线日期。

   ![请求电子邮件工作流](assets/project-request-email-workflow.png)

1. 单击&#x200B;**“提交”。**

该工作流随即会启动。任务出现在 **任务** 卡片。

## 为资源创建（和翻译）语言副本工作流 {#create-and-translate-language-copy-workflow-for-assets}

此 **创建语言副本** 和 **创建和翻译语言副本** 文档中详细介绍了工作流 [正在创建资产的语言副本。](/help/assets/translation-projects.md)
