---
title: 使用项目工作流
seo-title: 使用项目工作流
description: 提供了多种开箱即用的项目工作流。
seo-description: 提供了多种开箱即用的项目工作流。
uuid: 376922ca-e09e-4ac8-88c8-23dac2b49dbe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: 9d2bf30c-5190-4924-82cd-bcdfde24eb39
translation-type: tm+mt
source-git-commit: 0033dfac2540f56b3903c19f6ca19677af050db3
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 84%

---


# 使用项目工作流{#working-with-project-workflows}

现成可用的项目工作流包括：

* **项目批准工作流** -此工作流允许您将内容分配给用户，审核，然后批准。
* **请求启动项** -请求启动项的工作流。
* **请求登陆页** -此工作流请求登陆页。
* **请求电子邮件** - 此工作流用于请求电子邮件。
* **产品照片拍摄以及产品照片拍摄（商务）**- 映射包含产品的资产。
* **DAM 创建和翻译副本以及 DAM 创建语言副本** - 为资产和文件夹创建已翻译的二进制文件、元数据和标记。

根据您选择的项目模板，您可以使用特定工作流：

|  | **简单项目** | **媒体项目** | **产品照片拍摄项目** | **翻译项目** |
|---|:-:|:-:|:-:|:-:|
| 请求复制 |  | x |  |  |
| 产品照片拍摄 |  | x | x |  |
| 产品照片拍摄（商务） |  |  | x |  |
| 项目批准 | x |  |  |  |
| 请求启动项 | x |  |  |  |
| 请求登陆页面 | x |  |  |  |
| 请求电子邮件 | x |  |  |  |
| DAM创建语言复制和放大； |  |  |  | x |
| DAM创建和翻译语言副本&amp;ast; |  |  |  | x |

>[!NOTE]
>
>&amp;ast;这些工作流不是从项目中的&#x200B;**Workflow**&#x200B;拼贴中启动的。 请参阅[为资产创建语言副本](/help/sites-administering/tc-manage.md)。

无论您选择哪个工作流，启动和完成工作流的步骤都是相同的。只是具体的实施步骤有所不同。

您可以直接在项目中启动工作流（DAM 创建语言副本或 DAM 创建和翻译语言副本除外）。项目中任何未完成任务的信息会在&#x200B;**任务**&#x200B;拼贴中列出。用户图标旁边会显示需要完成的任务通知。

有关在 AEM 中使用工作流的更多信息，请参阅以下内容：

* [参与工作流](/help/sites-authoring/workflows-participating.md)
* [将工作流应用于页面](/help/sites-authoring/workflows-applying.md)
* [配置工作流](/help/sites-administering/workflows.md)

此部分介绍了可用于项目的工作流。

## 请求复制工作流  {#request-copy-workflow}

使用此工作流，您可以请求用户提供手稿，然后批准该手稿。要启动请求复制工作流，请执行以下操作：

1. 在您的媒体项目中，选择工作流拼 **贴中的+** 符号，然后选 **择** “请求复 **制工作流”**。
1. 输入手稿标题和您所请求内容的简短摘要。在适用的情况下，输入目标字数、任务优先级和到期日期。

   ![chlimage_1-321](assets/chlimage_1-321.png)

1. 单击&#x200B;**创建**。该工作流随即会启动。相应任务会显示在&#x200B;**任务**&#x200B;拼贴中。

   ![chlimage_1-322](assets/chlimage_1-322.png)

## 产品照片拍摄工作流 {#product-photo-shoot-workflow}

[创意项目](/help/sites-authoring/managing-product-information.md)中详细介绍了产品照片拍摄工作流（商务和无商务）。

## 项目批准工作流  {#project-approval-workflow}

在项目批准工作流中，您可以将内容分配给用户进行审核，然后批准内容。

1. 在您的简单项目中，选择&#x200B;**工作流**&#x200B;拼贴中的&#x200B;**`+`**&#x200B;符号，然后选择&#x200B;**项目批准工作流**。
1. 输入标题并从“团队”列表中选择要将其分配给的对象。在适用的情况下，输入描述、内容路径、任务优先级和到期日期。

   ![chlimage_1-323](assets/chlimage_1-323.png)

1. 单击&#x200B;**创建**。该工作流随即会启动。相应任务会显示在&#x200B;**任务**&#x200B;拼贴中。

   ![chlimage_1-324](assets/chlimage_1-324.png)

## 请求启动项工作流 {#request-launch-workflow}

使用此工作流，您可以请求启动项。

1. 在您的简单项目中，选择工 **作流拼贴** 中的+ **符号** ，然后选择 **请求启动工作流**。
1. 输入启动项的标题并提供启动项源路径。在适用的情况下，您还可以添加描述和起始日期。根据您希望启动项具备的行为方式，选择“继承源页面活动数据”或“不包括子页面”。

   ![chlimage_1-325](assets/chlimage_1-325.png)

1. 单击&#x200B;**创建**。该工作流随即会启动。该工作流将显示在&#x200B;**工作流**&#x200B;列表中(单击省略号&#x200B;**...**&#x200B;工作流&#x200B;**拼贴上的**&#x200B;可访问此列表)。

## 请求登陆页面工作流 {#request-landing-page-workflow}

使用此工作流，您可以请求登陆页面。

1. 在您的简单项目中，选择&#x200B;**工作流**&#x200B;拼贴中的 **+** 符号，然后选择“请求登陆页面工作流”。
1. 输入登陆页面的标题和父路径。在适用的情况下，输入起始日期或为登陆页面选择一个文件。

   ![chlimage_1-326](assets/chlimage_1-326.png)

1. 单击&#x200B;**创建**。该工作流随即会启动。相应任务会显示在&#x200B;**任务**&#x200B;拼贴中。

## 请求电子邮件工作流  {#request-email-workflow}

使用此工作流，您可以请求电子邮件。此工作流与在&#x200B;**电子邮件**&#x200B;拼贴中显示的工作流相同。

1. 在您的媒体或简单项目中，选择&#x200B;**工作流**&#x200B;拼贴中的 **+** 符号，然后选择&#x200B;**请求电子邮件工作流**。
1. 输入电子邮件标题以及营销活动和模板路径。此外，您还可以提供名称、描述和起始日期。

   ![chlimage_1-327](assets/chlimage_1-327.png)

1. 单击&#x200B;**创建**。该工作流随即会启动。相应任务会显示在&#x200B;**任务**&#x200B;拼贴中。

   ![chlimage_1-328](assets/chlimage_1-328.png)

## 为资产创建（和翻译）语言副本工作流 {#create-and-translate-language-copy-workflow-for-assets}

[为资产创建语言副本](/help/assets/translation-projects.md)中详细介绍了&#x200B;**创建语言副本**&#x200B;及&#x200B;**创建和翻译语言副本**&#x200B;工作流。
