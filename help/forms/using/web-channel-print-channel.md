---
title: 打印渠道和Web渠道
seo-title: 打印渠道和Web渠道
description: 导入打印渠道模板以及创建和启用Web渠道模板
seo-description: 导入打印渠道模板以及创建和启用Web渠道模板
uuid: 2361b1ee-c789-4a5a-9575-8b62b603da1e
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 96d2b1cc-3252-4cc7-8b06-a897cbef8599
docset: aem65
translation-type: tm+mt
source-git-commit: a326e508a781b3afaba8b5e371aa862a30536740

---


# 打印渠道和Web渠道{#print-channel-and-web-channel}

交互式通信可通过两个渠道提供：印刷和Web。 打印渠道用于创建PDF和纸张通信，如作为保险费付款提醒的打印信函，而Web渠道用于提供在线体验，如网站上的信用卡对帐单。

交互通信作者可以重复使用文档片段和图像等资源来创建打印版和Web版的交互通信。

创建交互式通 [信的先决条件之一](../../forms/using/create-interactive-communication.md) ，是在服务器上提供用于打印和／或Web通道的模板。 当模板作者在AEM中创建Web渠道模板时，打印渠道模板XDP在Adobe Forms Designer中创建并上传到服务器。

## Print channel {#printchannel}

交互通信的打印通道使用XFA表单模板XDP。 XDP是在Adobe Forms Designer中设计的。 有关创建打印渠道模板的更多信息，请参阅 [布局设计](../../forms/using/layout-design-details.md)。 要在交互通信中使用打印渠道模板，您需要将模板上传到AEM Forms服务器。

### 上传交互通信打印渠道模板 {#upload-interactive-communication-print-channel-template}

要上传模板，您必须是表单用户组的成员。 使用以下步骤将打印渠道模板(XDP)上传到AEM Forms:

1. 选择“ **[!UICONTROL 表单]** ”>“ **[!UICONTROL 表单和文档”]**。

1. 点按 **[!UICONTROL 创建]** > **[!UICONTROL 文件上传]**。

   导航并选择相应的打印渠道模板(XDP)，然后点按打 **[!UICONTROL 开]**。

## Web channel {#web-channel}

模板作者和管理员可以创建、编辑和启用Web模板。 要允许其他用户创作Web模板，您需要授予他们权限。 有关详细信息，请参 [阅用户、组和访问权限管理](/help/sites-administering/user-group-ac-admin.md)。

### 创作Web渠道模板 {#authoring-web-channel-template}

要创建Web渠道模板，您首先需要创建一个“模板”文件夹。 在模板文件夹内创建Web模板后，您需要启用该模板，以允许表单用户基于该模板创建交互式通信的Web渠道。

要创作Web渠道模板，请完成以下步骤：

1. 创建一个“模板”文件夹以保留您的Interactive Communication web模板（如果您还没有）。 有关详细信息，请参阅页面模板中的模 [板文件夹——可编辑](/help/sites-developing/page-templates-editable.md)。

   1. 点按工 **[!UICONTROL 具]**![>配置浏](assets/tools.png) 览器 ****。
   1. 在“配置浏览器”页面中，点按 **[!UICONTROL 创建]**。
   1. 在“创建配置”对话框中，指定文件夹的标题，选中“可编 **[!UICONTROL 辑模板]**”，然后点 **[!UICONTROL 按创建]**。

      此时会创建文件夹并在“配置浏览器”页面中列出该文件夹。

1. 导览至相应的模板文件夹并创建Web模板。

   1. 通过选择“工具”>“模板” **** **[!UICONTROL >]** ，导览至相 **`[Folder]`**&#x200B;应的模板文件夹。
   1. 点按&#x200B;**[!UICONTROL 创建]**。
   1. 选择 **[!UICONTROL 交互式通信- web渠道]** ，然后点 **[!UICONTROL 按下一步]**。
   1. 输入模板标题和说明，然后点按创 **[!UICONTROL 建]**。

      将创建模板并显示一个对话框。

   1. 点按 **[!UICONTROL 打开]** ，以打开您在模板编辑器中创建的模板。

      此时将显示模板编辑器。

      ![webchanneltemplate](assets/webchanneltemplate.png)

      创建或编辑模板时，模板作者可以定义多个方面。 创建或编辑模板与页面创作类似。 有关详细信息，请参阅创建页面模板中的编辑模 [板——模板作者](/help/sites-authoring/templates.md)。

1. 要允许使用此模板创建交互式通信，请启用该模板。

   1. 点按 **[!UICONTROL 工具]**![>模](assets/tools.png) 板 ****。
   1. 导航到相应的模板，选择它，然后点按启 **[!UICONTROL 用]** ，在警报消息中，点按启 **[!UICONTROL 用]**。

      模板已启用，其状态显示为“已启用”。 现在，您可以继续创建交互式通信，在该通信中可以使用新创建的Web渠道模板。

### 将渠道作为Web渠道的主渠道打印 {#print-channel-as-master-for-web-channel}

创作交互式通信时，作者可以选择此选项以创建与打印通道同步的Web通道。 使用打印渠道作为Web渠道的主渠道确保Web渠道的内容、继承和数据绑定从打印渠道派生，并且打印渠道中所做的更改可以反映在Web渠道中。 但是，允许交互通信作者根据需要中断Web渠道中特定组件的继承。

![以主Web渠道形式打印渠道](assets/create_ic_print_master_new.png) , ![以印刷渠道作为主渠道](assets/create_ic_print_master_web_new.png)

