---
title: 打印渠道和Web渠道
seo-title: 打印渠道和Web渠道
description: 导入打印渠道模板并创建和启用Web渠道模板
seo-description: 导入打印渠道模板并创建和启用Web渠道模板
uuid: 2361b1ee-c789-4a5a-9575-8b62b603da1e
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 96d2b1cc-3252-4cc7-8b06-a897cbef8599
docset: aem65
feature: 交互式通信
exl-id: cd7dbdac-dc76-4a1f-b850-0a9f47ae08de
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 0%

---

# 打印渠道和Web渠道{#print-channel-and-web-channel}

交互式通信可以通过两种渠道来提供：打印和web。 打印渠道用于创建PDF和纸面通信，例如作为保险费付款提醒的打印信件，而Web渠道用于提供在线体验，如网站上的信用卡报表。

交互式通信作者可以重复使用诸如文档片段和图像之类的资产来创建交互式通信的打印版本和Web版本。

[创建交互式通信](../../forms/using/create-interactive-communication.md)的先决条件之一是，在服务器上提供用于打印和/或Web通道的模板。 当模板作者在AEM中创建Web渠道模板时，打印渠道模板XDP会在AdobeForms Designer中创建并上传到服务器。

## 打印渠道 {#printchannel}

交互式通信的打印渠道使用XFA表单模板XDP。 XDP是在AdobeForms Designer中设计的。 有关创建打印渠道模板的更多信息，请参阅[布局设计](../../forms/using/layout-design-details.md)。 要在交互式通信中使用打印渠道模板，您需要将该模板上传到AEM Forms服务器。

### 上传交互式通信打印渠道模板{#upload-interactive-communication-print-channel-template}

要上载模板，您需要是表单用户组的成员。 请按照以下步骤将打印渠道模板(XDP)上传到AEM Forms:

1. 选择&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。

1. 点按&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 文件上传]**。

   导航并选择相应的打印渠道模板(XDP)，然后点按&#x200B;**[!UICONTROL 打开]**。

## Web渠道{#web-channel}

模板作者和管理员可以创建、编辑和启用Web模板。 要允许其他用户创作Web模板，您需要为其授予权限。 有关更多信息，请参阅[用户、组和访问权限管理](/help/sites-administering/user-group-ac-admin.md)。

### 创作Web渠道模板{#authoring-web-channel-template}

要创建Web渠道模板，您需要先创建Template文件夹。 在模板文件夹中创建Web模板后，您需要启用该模板，以便表单用户能够基于该模板创建交互式通信的Web渠道。

要创作Web渠道模板，请完成以下步骤：

1. 创建模板文件夹以保留您的交互式通信Web模板（如果尚未创建）。 有关更多信息，请参阅[页面模板 — 可编辑](/help/sites-developing/page-templates-editable.md)中的模板文件夹。

   1. 点按&#x200B;**[!UICONTROL 工具]** ![工具](assets/tools.png) > **[!UICONTROL 配置浏览器]**。
      * 有关更多信息，请参阅[配置浏览器](/help/sites-administering/configurations.md)文档。
   1. 在配置浏览器页面中，点按&#x200B;**[!UICONTROL 创建]**。
   1. 在创建配置对话框中，指定文件夹的标题，选中&#x200B;**[!UICONTROL 可编辑的模板]**，然后点按&#x200B;**[!UICONTROL 创建]**。

      文件夹已创建并列在配置浏览器页面中。

1. 导航到相应的模板文件夹并创建Web模板。

   1. 通过选择&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 模板]** > **`[Folder]`**，导航到相应的模板文件夹。
   1. 点按&#x200B;**[!UICONTROL 创建]**。
   1. 选择&#x200B;**[!UICONTROL 交互式通信 — Web渠道]**，然后点按&#x200B;**[!UICONTROL 下一步]**。
   1. 输入模板标题和描述，然后点按&#x200B;**[!UICONTROL 创建]**。

      随即会创建模板并显示一个对话框。

   1. 点按&#x200B;**[!UICONTROL 打开]**&#x200B;以打开您在模板编辑器中创建的模板。

      此时将显示模板编辑器。

      ![webchanneltemplate](assets/webchanneltemplate.png)

      创建或编辑模板时，模板作者可以定义多个方面。 创建或编辑模板与页面创作类似。 有关更多信息，请参阅[创建页面模板](/help/sites-authoring/templates.md)中的编辑模板 — 模板作者。

1. 要允许使用此模板创建交互式通信，请启用该模板。

   1. 点按&#x200B;**[!UICONTROL 工具]** ![工具](assets/tools.png) > **[!UICONTROL 模板]**。
   1. 导航到相应的模板，将其选中，然后点按&#x200B;**[!UICONTROL 启用]**，然后在警报消息中，点按&#x200B;**[!UICONTROL 启用]**。

      模板已启用，其状态显示为“已启用”。 现在，您可以继续创建交互式通信，以便使用新创建的Web渠道模板。

### 为Web渠道{#print-channel-as-master-for-web-channel}主控打印渠道

在创作交互式通信时，作者可以选择此选项以创建与打印渠道同步的Web渠道。 使用打印渠道作为Web渠道的主控，可确保Web渠道的内容、继承和数据绑定从打印渠道派生，并且在打印渠道中所做的更改可以反映在Web渠道中。 但是，交互式通信作者可以根据需要中断Web渠道中特定组件的继承。

![将渠道打印为主](assets/create_ic_print_master_new.png) ![Web渠道，将打印渠道打印为主控](assets/create_ic_print_master_web_new.png)
