---
title: “教程：发布自适应表单”
seo-title: "Tutorial: Publish your adaptive form"
description: 将自适应表单发布为AEM页面、将表单嵌入到AEM Sites页面，或将自适应表单嵌入到外部网页
seo-description: Publish the adaptive form as an AEM page, embed the form to an AEM Sites page, or embed the adaptive form in an external webpage
uuid: 1b164376-e61a-40aa-9f16-c79d24a72e20
contentOwner: khsingh
topic-tags: introduction
discoiquuid: e24dbd0e-4481-4f9d-9570-3a4046b3ef35
docset: aem65
feature: Adaptive Forms
exl-id: c039faec-f832-43d5-8a86-22afa3bef2a4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 1%

---

# 教程：发布自适应表单 {#tutorial-publish-your-adaptive-form}

![](do-not-localize/13-publish-your-adaptive-form-small.png)

本教程是 [创建您的第一个自适应表单](https://helpx.adobe.com/cn/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html) 系列。 建议按照时间顺序排列系列，以了解、执行和演示完整的教程用例。

自适应表单准备就绪后，您可以发布该表单以供最终用户使用。 最终用户可以在任何设备和Internet浏览器上打开已发布的表单。 发布自适应表单后，表单和相关内容将从AEM创作实例复制到AEM发布实例。 最终用户可通过发布实例访问该表单。

您可以使用以下方法发布自适应表单：

* [将自适应表单作为AEM页面发布](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [在AEM Sites页面中嵌入自适应表单](#embed-the-adaptive-form-in-an-aem-sites-page)
* [将自适应表单嵌入到外部网页(在AEM外部托管的非AEM网页)](../../forms/using/publish-your-adaptive-form.md)

## 开始之前 {#before-you-start}

* **[设置AEM Forms发布实例](https://helpx.adobe.com/cn/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**:发布实例是面向公众的AEM实例 [!DNL Forms] 在发布模式下运行。 在生产环境中，发布实例位于组织防火墙之外。
* **[设置复制和反向复制](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)**:复制将内容从创作实例复制到发布实例，并将用户输入（例如，表单输入）从发布实例返回到创作实例。

## 将自适应表单作为AEM页面发布 {#publish-the-adaptive-form-as-an-aem-page}

当自适应表单作为AEM页面发布时，整个网页仅包含已发布的表单。 您可以使用自适应表单的URL从其他网页链接自适应表单。 要发布 **shipping-add-add-update-form** 自适应表单作为AEM页面：

1. 登录AEM [!DNL Forms] 创作实例，并在AEM中找到shipping-add-update-form自适应表单 [!DNL Forms] UI。
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. 选择送货地址 — add-update-form自适应表单并点按 **[!UICONTROL 发布]**. 此时会显示一个对话框，其中包含与自适应表单相关的资产。 点按&#x200B;**[!UICONTROL 发布]**。此时会发布自适应表单，并显示一个成功对话框。
1. 在发布实例上打开表单。 表单可供最终用户填写和提交。
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## 在AEM Sites页面中嵌入自适应表单 {#embed-the-adaptive-form-in-an-aem-sites-page}

AEM [!DNL Forms] 允许表单开发人员在AEM中无缝嵌入自适应表单 [!DNL Sites] 页面。 嵌入式自适应表单功能齐全，用户无需离开页面即可填写和提交表单。 它有助于用户停留在网页上其他元素的上下文中，并同时与表单进行交互。

AEM [!DNL Forms] 提供组件， AEM [!DNL Forms] 容器，将自适应表单嵌入到AEM [!DNL Sites] 页面。 默认情况下，组件在AEM中不可见 [!DNL Sites] 容器。 执行以下步骤以启用AEM [!DNL Forms] 容器组件和在AEM中嵌入自适应表单 [!DNL Sites] 页面：

1. 在We.Retail网站中创建并打开一个页面进行编辑。 例如， [https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html). 自适应表单嵌入到 [!DNL Sites] 页面。

   您还可以在现有的We.Retail中嵌入自适应表单 [!DNL Site's] 页面。 例如，“关于美国”页面 [https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html). 它可节省您创建页面的时间。 以下步骤使用新创建的页面。

   We.Retail网站随AEM一起提供。 如果尚未安装We.Retail网站，请参阅 [We.Retail参考实施](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html) 安装站点。

1. 点按 ![属性](assets/properties.png) 页面信息并选择 **[!UICONTROL 编辑模板]** 选项。 页面的模板将在浏览器的新选项卡中打开。
1. 在内点按 **[!UICONTROL 布局容器]** 框和点按 ![馈送管理](assets/feedmanagement.png). 在 **[!UICONTROL 允许的组件]** 选项卡，展开 **[!UICONTROL 常规]** 折叠面板，选择 **[!UICONTROL AEM表单]** 选项，然后点按 ![save_icon](assets/save_icon.svg). AEM [!DNL Forms] 已为页面启用容器组件。

1. 打开包含AEM的浏览器选项卡 [!DNL Sites] 页面。 点按 **[!UICONTROL 将组件拖动到此处]** 框和点按 **+。** 在 **[!UICONTROL 插入新组件]** 框，点按 **[!UICONTROL AEM表单]**. 的 **[!UICONTROL AEM Forms容器]** 组件。
1. 点按 **[!UICONTROL AEM Forms容器]** 组件和点按 ![configure-icon](assets/configure-icon.svg). 包含AEM属性的对话框 [!DNL Forms] 随即会显示容器。 在 **[!UICONTROL 资产路径]** 字段中，浏览并选择shipping-add-update-form自适应表单。 点按 ![save_icon](assets/save_icon.svg). 自适应表单会嵌入到页面中。
1. 发布自适应表单和 [!DNL Sites] 页面。 以下是需要考虑的几点：

   * 如果您发布AEM [!DNL Sites] 页面，并且该页面包含嵌入式表单， [!DNL Sites] 页面和嵌入式表单。
   * 如果您只修改已发布站点页面中的嵌入表单，则应发布原始表单，并且所做的更改会反映在已发布的站点页面中。 发布的网站页面包含对表单的引用，无需重新发布页面。
   * 如果您修改 [!DNL Sites] 页面和嵌入的表单中，重新发布 [!DNL Sites] 页面和窗体。

      ![嵌入 — in-aem-sites](assets/embed-in-aem-sites.png)
   已向AEM添加“送货和帐单地址更改”表单 [!DNL Sites] 页面。

## 将自适应表单嵌入到外部网页中 {#embed-the-adaptive-form-in-an-external-webpage}

通过在外部网页中插入几行JavaScript，您可以将自适应表单嵌入到外部网页(AEM外部托管的非AEM网页)。 JavaScript代码会向AEM发送HTTP请求 [!DNL Forms] 服务器，并将自适应表单添加到网页。 有关详细步骤，请参阅 [将自适应表单嵌入到外部网页](/help/forms/using/embed-adaptive-form-external-web-page.md).
