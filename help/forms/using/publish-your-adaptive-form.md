---
title: “教程：发布自适应表单”
seo-title: “教程：发布自适应表单”
description: 将自适应表单发布为AEM页面，将表单嵌入到AEM Sites页面，或将自适应表单嵌入到外部网页
seo-description: 将自适应表单发布为AEM页面，将表单嵌入到AEM Sites页面，或将自适应表单嵌入到外部网页
uuid: 1b164376-e61a-40aa-9f16-c79d24a72e20
contentOwner: khsingh
topic-tags: introduction
discoiquuid: e24dbd0e-4481-4f9d-9570-3a4046b3ef35
docset: aem65
translation-type: tm+mt
source-git-commit: 1a816672b3e97346f5a7a984fcb4dc0df1a5b0da
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 0%

---


# 教程：发布自适应表单{#tutorial-publish-your-adaptive-form}

![](do-not-localize/13-publish-your-adaptive-form-small.png)

本教程是[创建第一个自适应表单](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html)系列中的一个步骤。 建议按照时间顺序按照系列来了解、执行和演示完整的教程用例。

自适应表单准备就绪后，您可以发布表单以使其可供最终用户使用。 最终用户可以在任何设备和Internet浏览器上打开已发布的表单。 发布自适应表单时，表单和相关内容会从AEM作者实例复制到AEM发布实例。 表单通过发布实例提供给最终用户。

您可以通过以下方法发布自适应表单：

* [将自适应表单发布为AEM页面](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [将自适应表单嵌入到AEM Sites页面](#embed-the-adaptive-form-in-an-aem-sites-page)
* [将自适应表单嵌入到外部网页(AEM外部托管的非AEM网页)](../../forms/using/publish-your-adaptive-form.md)

## 开始{#before-you-start}之前

* **[设置AEM Forms发布实例](https://helpx.adobe.com/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**:发布实例是AEM在发布模式下运行的面向 [!DNL Forms] 公共的实例。在生产环境中，发布实例位于组织的防火墙之外。
* **[设置复制和反向复制](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)**:复制将内容从作者实例复制到发布实例，并将用户输入（例如，表单输入）从发布实例返回给作者实例。

## 将自适应表单发布为AEM页面{#publish-the-adaptive-form-as-an-aem-page}

当自适应表单作为AEM页面发布时，整个网页仅包含已发布的表单。 您可以使用自适应表单的URL从其他网页链接它。 要将&#x200B;**shipping-add-update-form**&#x200B;自适应表单发布为AEM页，请执行以下操作：

1. 登录到AEM [!DNL Forms]作者实例，并在AEM [!DNL Forms] UI中找到shipping-add-update-form自适应表单。
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. 选择shipping-add-update-form自适应表单，然后点按&#x200B;**[!UICONTROL 发布]**。 此时将显示一个对话框，其中包含与自适应表单相关的资源。 点按&#x200B;**[!UICONTROL 发布]**。随后将发布自适应表单并显示成功对话框。
1. 在发布实例上打开表单。 表单可供最终用户填写和提交。
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## 将自适应表单嵌入到AEM Sites页面{#embed-the-adaptive-form-in-an-aem-sites-page}

AEM [!DNL Forms]允许表单开发人员将自适应表单无缝嵌入到AEM [!DNL Sites]页面中。 嵌入的自适应表单功能齐全，用户无需离开页面即可填写和提交表单。 它帮助用户保持在网页上其他元素的上下文中并同时与表单交互。

AEM [!DNL Forms]提供一个组件，即AEM [!DNL Forms]容器，以将自适应表单嵌入到AEM [!DNL Sites]页面。 默认情况下，组件在AEM [!DNL Sites]容器中不可见。 执行以下步骤以启用AEM [!DNL Forms]容器组件并将自适应表单嵌入AEM [!DNL Sites]页面：

1. 在We.Retail站点中创建并打开页面进行编辑。 例如，[https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html)。 自适应表单已嵌入到[!DNL Sites]页面。

   您还可以将自适应表单嵌入到现有的We.Retail [!DNL Site's]页面。 例如，“ABOUT US”页[https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html)。 它为您节省了创建页面的时间。 以下步骤使用新创建的页面。

   We.Retail站点随AEM提供。 如果未安装We.Retail站点，请参阅[We.Retail Reference Implementation](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html)安装该站点。

1. 点按![属性](assets/properties.png)页面信息，并在新创建的We.Retail站点页面中选择&#x200B;**[!UICONTROL 编辑模板]**&#x200B;选项。 页面的模板将在浏览器的新选项卡中打开。
1. 点按&#x200B;**[!UICONTROL 布局容器]**&#x200B;框内，然后点按![feedmanagement](assets/feedmanagement.png)。 在&#x200B;**[!UICONTROL 允许的组件]**&#x200B;选项卡中，展开&#x200B;**[!UICONTROL 常规]**&#x200B;折叠面板，选择&#x200B;**[!UICONTROL AEM表单]**&#x200B;选项，然后点按![save_icon](assets/save_icon.svg)。 为页面启用了AEM [!DNL Forms]容器组件。

1. 打开包含AEM [!DNL Sites]的浏览器选项卡，该页面在步骤1中打开。 点按&#x200B;**[!UICONTROL 将组件拖动到此处]**&#x200B;框，然后点按&#x200B;**+。** 在插入 **[!UICONTROL 新组]** 件框中，点 **[!UICONTROL 按AEM表单]**。将&#x200B;**[!UICONTROL AEM Forms容器]**&#x200B;组件添加到页面。
1. 点按&#x200B;**[!UICONTROL AEM Forms容器]**&#x200B;组件，然后点按![configure-icon](assets/configure-icon.svg)。 出现一个具有AEM [!DNL Forms]容器属性的对话框。 在&#x200B;**[!UICONTROL 资产路径]**&#x200B;字段中，浏览并选择shipping-add-update-form自适应表单。 点按![save_icon](assets/save_icon.svg)。 自适应表单嵌入在页面中。
1. 发布自适应表单和[!DNL Sites]页面。 以下是需要考虑的几点：

   * 如果首次发布AEM [!DNL Sites]页面并且该页面包含嵌入式表单，则发布[!DNL Sites]页面和嵌入式表单。
   * 如果仅修改已发布站点页面中的嵌入表单，则发布原始表单，更改将反映在已发布的站点页面中。 已发布的站点页面包含对表单的引用，并且不需要重新发布页面。
   * 如果修改[!DNL Sites]页面和嵌入式表单，请重新发布[!DNL Sites]页面和表单。

      ![embed-in-aem-sites](assets/embed-in-aem-sites.png)
   已将“发运和帐单地址更改”表单添加到AEM [!DNL Sites]页面。

## 将自适应表单嵌入到外部网页{#embed-the-adaptive-form-in-an-external-webpage}

通过在外部网页中插入几行JavaScript，可以将自适应表单嵌入到外部网页(AEM外托管的非AEM网页)。 JavaScript代码向AEM [!DNL Forms]服务器发送自适应表单和相关资源的HTTP请求，并将自适应表单添加到网页。 有关详细步骤，请参阅[将自适应表单嵌入到外部网页](/help/forms/using/embed-adaptive-form-external-web-page.md)。
