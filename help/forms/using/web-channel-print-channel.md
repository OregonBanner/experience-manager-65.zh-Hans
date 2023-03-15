---
title: 打印渠道和Web渠道
seo-title: Print channel and web channel
description: 导入打印渠道模板以及创建和启用Web渠道模板
seo-description: Importing print channel templates and creating and enabling web channel templates
uuid: 2361b1ee-c789-4a5a-9575-8b62b603da1e
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 96d2b1cc-3252-4cc7-8b06-a897cbef8599
docset: aem65
feature: Interactive Communication
exl-id: cd7dbdac-dc76-4a1f-b850-0a9f47ae08de
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# 打印渠道和Web渠道{#print-channel-and-web-channel}

交互式通信可通过两种渠道提供：打印和Web。 打印渠道用于创建PDF和纸面通信，例如作为保险费支付提醒的打印信件，而Web渠道用于提供在线体验，例如网站上的信用卡对帐单。

交互式通信作者可以重用文档片段和图像等资产，以创建交互式通信的打印版本和Web版本。

的先决条件之一 [创建交互式通信](../../forms/using/create-interactive-communication.md) 需要在服务器上提供打印和/或web channel模板。 当模板作者在AEM本身中创建Web渠道模板时，打印渠道模板XDP是在AdobeForms Designer中创建并上传到服务器。

## 打印渠道 {#printchannel}

交互式通信的打印渠道使用XFA表单模板XDP。 在AdobeForms Designer中设计了XDP。 有关创建打印渠道模板的详细信息，请参阅 [布局设计](../../forms/using/layout-design-details.md). 要在交互式通信中使用打印渠道模板，您需要将该模板上传到AEM Forms服务器。

### 上传交互式通信打印渠道模板 {#upload-interactive-communication-print-channel-template}

要上传模板，您需要是表单用户组的成员。 使用以下步骤将打印渠道模板(XDP)上传到AEM Forms：

1. 选择 **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.

1. 点按 **[!UICONTROL 创建]** > **[!UICONTROL 文件上传]**.

   导航并选择相应的打印渠道模板(XDP)并点按 **[!UICONTROL 打开]**.

## Web渠道 {#web-channel}

模板作者和管理员可以创建、编辑和启用Web模板。 要允许其他用户创作Web模板，您需要授予他们权限。 有关更多信息，请参阅 [用户、组和访问权限管理](/help/sites-administering/user-group-ac-admin.md).

### 创作Web渠道模板 {#authoring-web-channel-template}

要创建Web渠道模板，您需要首先创建模板文件夹。 在模板文件夹内创建Web模板后，需要启用该模板以允许表单用户根据该模板创建交互式通信的Web渠道。

要创作Web渠道模板，请完成以下步骤：

1. 创建模板文件夹以保留交互式通信Web模板（如果尚未创建）。 有关更多信息，请参阅模板文件夹，位置在 [页面模板 — 可编辑](/help/sites-developing/page-templates-editable.md).

   1. 点按 **[!UICONTROL 工具]** ![工具](assets/tools.png) > **[!UICONTROL 配置浏览器]**.
      * 请参阅 [配置浏览器](/help/sites-administering/configurations.md) 文档，以了解更多信息。
   1. 在配置浏览器页面中，点按 **[!UICONTROL 创建]**.
   1. 在创建配置对话框中，指定文件夹的标题，选中 **[!UICONTROL 可编辑的模板]**，然后点按 **[!UICONTROL 创建]**.

      将创建文件夹，并在配置浏览器页面中列出该文件夹。

1. 导航到相应的模板文件夹并创建Web模板。

   1. 通过选择导航到相应的模板文件夹 **[!UICONTROL 工具]** > **[!UICONTROL 模板]** > **`[Folder]`**.
   1. 点按&#x200B;**[!UICONTROL 创建]**。
   1. 选择 **[!UICONTROL 交互式通信 — Web渠道]** 并点按 **[!UICONTROL 下一个]**.
   1. 输入模板标题和描述，然后点按 **[!UICONTROL 创建]**.

      模板随即创建，并出现一个对话框。

   1. 点按 **[!UICONTROL 打开]** 以打开您在模板编辑器中创建的模板。

      此时将显示模板编辑器。

      ![webchanneltemplate](assets/webchanneltemplate.png)

      创建或编辑模板时，模板作者可以定义多个方面。 创建或编辑模板与页面创作类似。 有关更多信息，请参阅编辑模板 — 模板作者，位于 [创建页面模板](/help/sites-authoring/templates.md).

1. 要允许使用此模板创建交互式通信，请启用该模板。

   1. 点按 **[!UICONTROL 工具]** ![工具](assets/tools.png) > **[!UICONTROL 模板]**.
   1. 导航到相应的模板，选择它，然后点按 **[!UICONTROL 启用]** 在警报消息中，点按 **[!UICONTROL 启用]**.

      模板已启用，其状态显示为“已启用”。 现在，您可以继续创建交互式通信，您可以在其中使用新创建的Web渠道模板。

### 将Web渠道的渠道打印为主控 {#print-channel-as-master-for-web-channel}

在创作交互式通信时，作者可以选择此选项，以创建与打印渠道同步的Web渠道。 使用打印渠道作为Web渠道的主控可以确保Web渠道的内容、继承和数据绑定是从打印渠道派生出来的，并且打印渠道中所做的更改可以反映在Web渠道中。 但是，交互式通信作者可以根据需要中断Web渠道中特定组件的继承。

![将渠道打印为主控](assets/create_ic_print_master_new.png) ![打印渠道为主控的Web渠道](assets/create_ic_print_master_web_new.png)
