---
title: 印刷渠道和Web渠道
seo-title: 印刷渠道和Web渠道
description: 导入打印渠道模板并创建和启用Web渠道模板
seo-description: 导入打印渠道模板并创建和启用Web渠道模板
uuid: 2361b1ee-c789-4a5a-9575-8b62b603da1e
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 96d2b1cc-3252-4cc7-8b06-a897cbef8599
docset: aem65
feature: Interactive Communication
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 0%

---


# 打印渠道和Web渠道{#print-channel-and-web-channel}

交互式通信可通过两种渠道提供：印刷和Web。 打印渠道用于创建PDF和纸质通信，如作为保险费付款提醒的打印信函，而Web渠道用于提供在线体验，如网站上的信用卡对帐单。

交互通信的作者可以重复使用文档片段和图像等资源来创建交互通信的打印版和Web版。

[创建交互式通信](../../forms/using/create-interactive-communication.md)的先决条件之一是服务器上提供用于打印和/或Web渠道的模板。 模板作者在AEM中创建Web渠道模板时，打印渠道模板XDP在Adobe Forms Designer中创建并上传到服务器。

## 打印渠道{#printchannel}

交互通信的打印渠道使用XFA表单模板XDP。 XDP是在Adobe Forms Designer中设计的。 有关创建打印渠道模板的详细信息，请参阅[布局设计](../../forms/using/layout-design-details.md)。 要在交互通信中使用打印渠道模板，您需要将模板上传到AEM Forms服务器。

### 上传交互通信打印渠道模板{#upload-interactive-communication-print-channel-template}

要上传模板，您必须是表单用户组的成员。 使用以下步骤将打印渠道模板(XDP)上传到AEM Forms:

1. 选择&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。

1. 点按&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 文件上载]**。

   导航并选择相应的打印渠道模板(XDP)，然后点按&#x200B;**[!UICONTROL 打开]**。

## Web渠道{#web-channel}

模板作者和管理员可以创建、编辑和启用Web模板。 要允许其他用户创作Web模板，您需要授予其权限。 有关详细信息，请参阅[用户、组和访问权限管理](/help/sites-administering/user-group-ac-admin.md)。

### 创作Web渠道模板{#authoring-web-channel-template}

要创建Web渠道模板，您首先需要创建一个“模板”文件夹。 在模板文件夹内创建Web模板后，您需要启用该模板，以允许表单用户基于模板创建交互式通信的Web渠道。

要创作Web渠道模板，请完成以下步骤：

1. 创建一个“模板”文件夹以保留您的Interactive Communication Web模板（如果您还没有）。 有关详细信息，请参阅[页面模板 — 可编辑](/help/sites-developing/page-templates-editable.md)中的模板文件夹。

   1. 点按&#x200B;**[!UICONTROL 工具]** ![工具](assets/tools.png) > **[!UICONTROL 配置浏览器]**。
      * 有关详细信息，请参阅[配置浏览器](/help/sites-administering/configurations.md)文档。
   1. 在“配置浏览器”页中，点按&#x200B;**[!UICONTROL 创建]**。
   1. 在“创建配置”对话框中，指定文件夹的标题，选中&#x200B;**[!UICONTROL 可编辑模板]**，然后点按&#x200B;**[!UICONTROL 创建]**。

      文件夹将创建并列在“配置浏览器”页面中。

1. 导览至相应的模板文件夹并创建Web模板。

   1. 选择&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 模板]** > **`[Folder]`**，导览至相应的模板文件夹。
   1. 点按&#x200B;**[!UICONTROL 创建]**。
   1. 选择&#x200B;**[!UICONTROL 交互式通信 — Web渠道]**，然后点按&#x200B;**[!UICONTROL 下一步]**。
   1. 输入模板标题和说明，然后点按&#x200B;**[!UICONTROL 创建]**。

      将创建模板并显示一个对话框。

   1. 点按&#x200B;**[!UICONTROL 打开]**&#x200B;以打开您在模板编辑器中创建的模板。

      此时将显示模板编辑器。

      ![webchanneltemplate](assets/webchanneltemplate.png)

      创建或编辑模板时，模板作者可以定义多个方面。 创建或编辑模板与页面创作类似。 有关详细信息，请参阅[创建页面模板](/help/sites-authoring/templates.md)中的“编辑模板 — 模板作者”。

1. 要允许使用此模板创建交互式通信，请启用该模板。

   1. 点按&#x200B;**[!UICONTROL 工具]** ![工具](assets/tools.png) > **[!UICONTROL 模板]**。
   1. 导航到相应的模板，选择它，然后点按&#x200B;**[!UICONTROL 启用]**，在警报消息中，点按&#x200B;**[!UICONTROL 启用]**。

      模板已启用，其状态显示为“已启用”。 现在，您可以继续创建交互式通信，以便使用新创建的Web渠道模板。

### 将渠道打印为Web渠道{#print-channel-as-master-for-web-channel}的主控

在创作交互式通信时，作者可以选择此选项以创建与打印渠道同步的Web渠道。 将打印渠道用作Web渠道的主控，可确保Web渠道的内容、继承和数据绑定从打印渠道派生，并且打印渠道中所做的更改可以反映在Web渠道中。 但是，允许交互通信作者根据需要中断Web渠道中特定组件的继承。

![将渠道打印为](assets/create_ic_print_master_new.png) ![主渠道将打印渠道打印为主控](assets/create_ic_print_master_web_new.png)

