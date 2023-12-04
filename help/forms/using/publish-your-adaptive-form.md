---
title: “教程：发布自适应表单”
seo-title: "Tutorial: Publish your adaptive form"
description: 将自适应表单发布为AEM页面，将表单嵌入到AEM Sites页面，或将自适应表单嵌入到外部网页中
seo-description: Publish the adaptive form as an AEM page, embed the form to an AEM Sites page, or embed the adaptive form in an external webpage
uuid: 1b164376-e61a-40aa-9f16-c79d24a72e20
contentOwner: khsingh
topic-tags: introduction
discoiquuid: e24dbd0e-4481-4f9d-9570-3a4046b3ef35
docset: aem65
feature: Adaptive Forms
exl-id: c039faec-f832-43d5-8a86-22afa3bef2a4
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 2%

---

# 教程：发布自适应表单 {#tutorial-publish-your-adaptive-form}

![主页图像](do-not-localize/13-publish-your-adaptive-form-small.png)

本教程是 [创建您的第一个自适应表单](https://helpx.adobe.com/cn/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html) 系列。 建议按时间顺序跟踪系列，以了解、执行和演示完整的教程用例。

在自适应表单准备就绪后，您可以发布表单以使其对最终用户可用。 最终用户可以在任何设备和互联网浏览器上打开已发布的表单。 发布自适应表单时，表单和相关内容将从AEM创作实例复制到AEM发布实例。 该表单通过发布实例提供给最终用户。

您可以通过以下方法发布自适应表单：

* [将自适应表单发布为AEM页面](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [将自适应表单嵌入到AEM Sites页面中](#embed-the-adaptive-form-in-an-aem-sites-page)
* [将自适应表单嵌入到外部网页(托管在AEM外部的非AEM网页)中](../../forms/using/publish-your-adaptive-form.md)

## 开始之前 {#before-you-start}

* **[设置AEM Forms发布实例](https://helpx.adobe.com/cn/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**：发布实例是AEM的面向公众的实例 [!DNL Forms] 在发布模式下运行。 在生产环境中，发布实例位于组织的防火墙之外。
* **[设置复制和反向复制](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)**：复制操作将内容从创作实例复制到发布实例，并将用户输入（例如，表单输入）从发布实例返回到创作实例。

## 将自适应表单发布为AEM页面 {#publish-the-adaptive-form-as-an-aem-page}

将自适应表单发布为AEM页面时，整个网页只包含已发布的表单。 您可以使用自适应表单的URL将其从其他网页链接。 要发布 **shipping-address-add-update-form** 自适应表单作为AEM页面：

1. 登录到AEM [!DNL Forms] 创作实例并在AEM中找到shipping-address-add-update-form自适应表单 [!DNL Forms] UI。
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. 选择shipping-address-add-update-form自适应表单，然后选择 **[!UICONTROL Publish]**. 此时将显示一个对话框，其中包含与自适应表单相关的资源。 选择 **[!UICONTROL Publish]**. 自适应表单已发布，并且显示成功对话框。
1. 在发布实例上打开表单。 该表单可供最终用户填写和提交。
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## 将自适应表单嵌入到AEM Sites页面中 {#embed-the-adaptive-form-in-an-aem-sites-page}

AEM [!DNL Forms] 允许表单开发人员将自适应表单无缝嵌入到AEM中 [!DNL Sites] 页面。 嵌入的自适应表单功能齐全，用户无需离开页面即可填写并提交表单。它有助于用户停留在网页上其他元素的上下文中，同时与表单交互。

AEM [!DNL Forms] 提供组件AEM [!DNL Forms] 容器，用于将自适应表单嵌入到AEM [!DNL Sites] 页面。 默认情况下，该组件在AEM中不可见 [!DNL Sites] 容器。 执行以下步骤以启用AEM [!DNL Forms] 将自适应表单嵌入到AEM中的容器组件和 [!DNL Sites] 页面：

1. 在We.Retail网站中创建并打开页面以进行编辑。 例如， [https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html). 自适应表单将嵌入到 [!DNL Sites] 页面。

   您还可以在现有We.Retail中嵌入自适应表单 [!DNL Site's] 页面。 例如，“关于美国”页面 [https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html). 这样可节省创建页面的时间。 以下步骤使用新创建的页面。

   We.Retail网站随AEM一起提供。 如果您未安装We.Retail网站，请参阅 [We.Retail参考实施](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html) 安装站点。

1. 选择 ![属性](assets/properties.png) 页面信息并选择 **[!UICONTROL 编辑模板]** 新创建的We.Retail网站页面中的选项。 将在浏览器的新选项卡中打开页面模板。
1. 在内选择 **[!UICONTROL 布局容器]** 框并选择 ![反馈管理](assets/feedmanagement.png). 在 **[!UICONTROL 允许的组件]** 选项卡，展开 **[!UICONTROL 常规]** 折叠面板，选择 **[!UICONTROL AEM表单]** 选项，然后选择 ![保存图标](assets/save_icon.svg). AEM [!DNL Forms] 已为页面启用容器组件。

1. 打开包含AEM的浏览器选项卡 [!DNL Sites] 页面已在步骤1中打开。 选择 **[!UICONTROL 将组件拖动到此处]** 框并选择 **+.** 在 **[!UICONTROL 插入新组件]** 框，选择 **[!UICONTROL AEM表单]**. 此 **[!UICONTROL AEM Forms容器]** 组件将添加到页面中。
1. 选择 **[!UICONTROL AEM Forms容器]** 组件和选择 ![configure-icon](assets/configure-icon.svg). 包含AEM属性的对话框 [!DNL Forms] 此时会显示容器。 在 **[!UICONTROL 资产路径]** 字段，浏览并选择shipping-address-add-update-form自适应表单。 选择 ![保存图标](assets/save_icon.svg). 自适应表单将嵌入到页面中。
1. 发布自适应表单和 [!DNL Sites] 页面。 以下是需要考虑的一些要点：

   * 如果您发布AEM [!DNL Sites] 首次访问该页面，并且它包含一个嵌入式表单，发布 [!DNL Sites] 页面和嵌入的表单。
   * 如果仅修改已发布站点页面中的嵌入表单，请发布原始表单，所做的更改将反映在已发布的站点页面中。 已发布的站点页面包含对表单的引用，无需重新发布页面。
   * 如果您修改了 [!DNL Sites] 页面和嵌入的表单，重新发布 [!DNL Sites] 页面和表单。

     ![embed-in-aem-sites](assets/embed-in-aem-sites.png)

   已将送货和帐单地址更改表单添加到AEM [!DNL Sites] 页面。

## 将自适应表单嵌入到外部网页中 {#embed-the-adaptive-form-in-an-external-webpage}

通过在外部网页中插入几行JavaScript，您可以将自适应表单嵌入到外部网页(托管在AEM外部的非AEM网页)中。 JavaScript代码向AEM发送HTTP请求 [!DNL Forms] 用于自适应表单和相关资源的服务器，并将自适应表单添加到网页。 有关详细步骤，请参阅 [将自适应表单嵌入到外部网页](/help/forms/using/embed-adaptive-form-external-web-page.md).
