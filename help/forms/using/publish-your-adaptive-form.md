---
title: “教程：发布自适应表单”
seo-title: “教程：发布自适应表单”
description: 将自适应表单发布为AEM页面，将表单嵌入到AEM站点页面，或将自适应表单嵌入到外部网页
seo-description: 将自适应表单发布为AEM页面，将表单嵌入到AEM站点页面，或将自适应表单嵌入到外部网页
uuid: 1b164376-e61a-40aa-9f16-c79d24a72e20
contentOwner: khsingh
topic-tags: introduction
discoiquuid: e24dbd0e-4481-4f9d-9570-3a4046b3ef35
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 教程：发布自适应表单 {#tutorial-publish-your-adaptive-form}

![](do-not-localize/13-publish-your-adaptive-form-small.png)

本教程是“创建您的第一个自 [适应表单”系列中的一个步骤](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html) 。 建议按照时间顺序按照这一系列来了解、执行和演示完整的教程用例。

自适应表单准备就绪后，您可以发布表单以使其可供最终用户使用。 最终用户可以在任何设备和Internet浏览器上打开已发布的表单。 发布自适应表单时，表单和相关内容将从AEM作者实例复制到AEM发布实例。 表单通过发布实例提供给最终用户。

您可以使用以下方法发布自适应表单：

* [将自适应表单发布为AEM页面](../../forms/using/publish-your-adaptive-form.md#publish-the-adaptive-form-as-an-aem-page)
* [在AEM站点页面中嵌入自适应表单](#embed-the-adaptive-form-in-an-aem-sites-page)
* [将自适应表单嵌入到外部网页（在AEM外部托管的非AEM网页）中](../../forms/using/publish-your-adaptive-form.md)

## Before you start {#before-you-start}

* **[设置AEM Forms发布实例](https://helpx.adobe.com/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html)**:发布实例是在发布模式下运行的AEM Forms的面向公共的实例。 在生产环境中，发布实例位于组织的防火墙之外。
* **[设置复制和反向复制](https://helpx.adobe.com/experience-manager/6-3/help/sites-deploying/replication.html)**:复制将内容从作者实例复制到发布实例，并将用户输入（例如，表单输入）从发布实例返回到作者实例。

## 将自适应表单发布为AEM页面 {#publish-the-adaptive-form-as-an-aem-page}

当自适应表单作为AEM页面发布时，整个网页仅包含已发布的表单。 您可以使用自适应表单的URL从其他网页链接它。 要将shipping- **add-update-form自适应表单发布为AEM页** ，请执行以下操作：

1. 登录到AEM Forms作者实例，并在AEM Forms UI中找到shipping-add-update-form自适应表单。
   `https://localhost:4502/aem/forms.html/content/dam/formsanddocuments`
1. 选择送货地址-add-update-form自适应表单，然后点按发 **布**。 此时将显示一个对话框，其中包含与自适应表单相关的资源。 点按&#x200B;**发布**。将发布自适应表单，并显示成功对话框。
1. 在发布实例上打开表单。 表单可供最终用户填写和提交。
   `https://localhost:4503/content/forms/af/shipping-address-add-update-form.html`

## 在AEM站点页面中嵌入自适应表单 {#embed-the-adaptive-form-in-an-aem-sites-page}

AEM Forms允许表单开发人员将自适应表单无缝嵌入到AEM站点页面中。 嵌入式自适应表单功能齐全，用户无需离开页面即可填写和提交表单。 它帮助用户保持在网页上其他元素的上下文中并与表单同时交互。

AEM Forms提供一个组件AEM Forms容器，用于将自适应表单嵌入到AEM站点页面。 默认情况下，该组件在AEM站点容器中不可见。 执行以下步骤以启用AEM Forms容器组件并将自适应表单嵌入到AEM站点页面：

1. 在We.Retail站点中创建并打开一个页面进行编辑。 例如， [https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html](https://localhost:4502/editor.html/content/we-retail/us/en/user/shipping-and-billing-address.html)。 自适应表单已嵌入到站点页面。

   您还可以将自适应表单嵌入到现有We.Retail站点的页面中。 例如，“关于美国”页 [面https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html](https://localhost:4502/editor.html/content/we-retail/us/en/about-us.html)。 它可节省您创建页面的时间。 以下步骤使用新创建的页面。

   We.Retail站点随AEM提供。 如果尚未安装We.Retail站点，请参阅安装 [We.Retail Reference Implementation](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/we-retail.html) （We.Retail参考实施）。

1. 点按 ![属性页](assets/properties.png) ，然后在新创建的We.Retail站点页 **面中选择** “编辑模板”选项。 页面的模板将在浏览器的新选项卡中打开。
1. 在布局容器 **框中点按** ，然后点按 ![feedmanagement](assets/feedmanagement.png)。 在允 **许的组件** ，展开常规 **折叠面板，选择** AEM表单 **，然后点按**![](assets/save_icon.svg)。 此时会为页面启用AEM表单容器组件。

1. 打开包含在步骤1中打开的AEM站点页面的浏览器选项卡。 点按将 **组件拖动到此处** ，然后点 **按+。** 在插入 **新组件框中** ，点按 **AEM表单。** AEM Forms容器组件 **** 即添加到页面。
1. 点按 **AEM Forms容器组件** ，然后点按 ![](assets/configure-icon.svg)。 将显示一个包含AEM Forms容器属性的对话框。 在“资 **产路径** ”字段中，浏览并选择shipping-add-update-form自适应表单。 点按 ![](assets/save_icon.svg). 自适应表单嵌入到页面中。
1. 发布自适应表单和站点页面。 以下是需要考虑的几点：

   * 如果您是第一次发布AEM站点页面，并且该页面包含嵌入式表单，请发布站点页面和嵌入式表单。
   * 如果仅修改已发布站点页面中的嵌入表单，则发布原始表单，而更改将反映在已发布的站点页面中。 已发布的站点页面包含对表单的引用，并且不需要重新发布页面。
   * 如果您修改了站点页面和嵌入的表单，请重新发布站点页面和表单。
   ![embed-in-aem-sites](assets/embed-in-aem-sites.png)

   送货和帐单地址更改表单已添加到AEM站点页面。

## 将自适应表单嵌入到外部网页 {#embed-the-adaptive-form-in-an-external-webpage}

通过在外部网页中插入几行JavaScript，可将自适应表单嵌入到外部网页（AEM外部托管的非AEM网页）。 JavaScript代码向AEM Forms服务器发送自适应表单和相关资源的HTTP请求，并将自适应表单添加到网页。 有关详细步骤，请 [参阅将自适应表单嵌入到外部网页](/help/forms/using/embed-adaptive-form-external-web-page.md)。
