---
title: We.Retail参考实施
seo-title: We.Retail Reference Implementation
description: We.Retail是参考实施的技术预览，它说明了使用AEM设置在线展示的推荐方法
seo-description: We.Retail is a technology preview of a reference implementation that illustrates the recommended way of setting up an online presence with AEM
uuid: d8833192-b592-4812-bf9b-bd882e8ee7f0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: f50150af-deff-4c29-bfe0-1cfc67b29d51
exl-id: 504c61c7-dcd3-412c-9239-d24a2b78e4b9
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 11%

---

# We.Retail参考实施{#we-retail-reference-implementation}

## 简介 {#introduction}

We.Retail是一个参考实施和示例内容，说明了使用Adobe Experience Manager设置在线展示的推荐方法。

We.Retail使用最新的AEM技术，例如HTL、响应式布局、可编辑模板、核心组件等。

虽然它演示了一个零售垂直领域，但网站设置的方式可应用于任何垂直领域，并且只有产品目录和购物车功能特定于零售领域。

## 功能 {#features}

作为AEM标准参考实施，We.Retail展示了AEM的一些最强大的功能。

| **功能** | **描述** | **有兴趣吗？** |
|---|---|---|
| [全局化站点结构](/help/sites-administering/tc-bp.md) | We.Retail包括语言母版，这些母版会实时复制到特定于国家/地区的站点中。 | [试试看！](/help/sites-developing/we-retail-globalized-site-structure.md) |
| [响应式布局](/help/sites-authoring/responsive-layout.md) | 所有页面均采用响应式布局，可动态适应屏幕和设备大小。 | [试试看！](/help/sites-developing/we-retail-responsive-layout.md) |
| [可编辑的模板](/help/sites-developing/page-templates-editable.md) | 所有页面都基于可编辑的模板，允许非开发人员调整和自定义模板。 | [试试看！](/help/sites-developing/we-retail-editable-templates.md) |
| [HTML 模板语言](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) | 所有组件都基于HTL |  |
| [电子商务功能](/help/commerce/cif-classic/developing/ecommerce.md) | 功能产品目录 |  |
| [社区站点](/help/communities/overview.md) | 允许访客加入社区讨论、阅读博客等 |  |
| [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) | 所有组件都基于新的核心组件，更易于使用且用户可立即配置 | [试试看！](/help/sites-developing/we-retail-core-components.md) |
| [内容片段](/help/assets/content-fragments/content-fragments.md) | We.Retail体验部分展示了通过内容片段重用内容的强大功能。 | [试试看！](/help/sites-developing/we-retail-content-fragments.md) |
| [体验片段](/help/sites-authoring/experience-fragments.md) | 体验片段是由一个或多个组件构成的组件组，包括可在页面内引用的内容和布局。 | [试试看！](/help/sites-developing/we-retail-experience-fragments.md) |

## 快速入门 {#getting-started}

We.Retail作为AEM示例内容提供。 为了使用，只需 [像往常一样启动AEM](/help/sites-deploying/deploy.md#getting-started)，确保未禁用示例内容。

>[!CAUTION]
>
>不应在生产实例上安装We.Retail。 生产实例应在中启动 `nosamplecontent` [运行模式](/help/sites-deploying/configure-runmodes.md).

>[!CAUTION]
>
>We.Retail基于最新的AEM技术，因此不支持 [经典UI创作](/help/sites-classic-ui-authoring/home.md).

### 最新版本 {#latest-version}

尽管We.Retail随AEM版本一起分发，但在该版本之后可能会对内容及其功能进行更新。 因此，可以 [从GitHub下载最新版本](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases) 然后 [上传](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system) 和 [安装](/help/sites-administering/package-manager.md#installing-packages) 它作为您的AEM实例上的包。

### 首要步骤 {#first-steps}

1. 启动AEM（和/或安装We.Retail）后，网站 **We.Retail** 可在 [站点控制台](/help/sites-authoring/basic-handling.md#global-navigation).
1. 例如，可以打开以下页面，它应看起来像中显示在 [附录](#appendix) 下：

   `https://<server name>:<port number>/editor.html/content/we-retail/language-masters/en.html`

## We.Retail和Geometrixx {#we-retail-geometrixx}

在AEM的早期版本中，Geometrixx及其许多化身用作示例内容。 自6.3版本以来，We.Retail一直是随AEM提供的示例内容，并用作新的标准参考实施。

We.Retail在技术上更加稳健，它利用最新的AEM技术来提高灵活性和可扩展性，同时还演示了该产品的最新功能。

### 功能比较 {#feature-comparison}

下表概述了与Geometrixx相比，We.Retail中可用的主要功能。

* **可用** 表示在示例内容中找到该功能的示例。
* **不可用** 表示该功能的示例在示例内容中不可用，但并不意味着该功能本身不可用。

| **功能** | **We.Retail** | **Geometrixx** |
|---|---|---|
| 全局化站点结构 | 语言母版实时复制到国家/地区特定的站点 | 不可用 |
| 内容片段 | 可用 | 不可用 |
| 体验片段 | 可用 | 不可用 |
| 响应式布局 | 对于所有页面 | 仅Geometrixx Media |
| 可编辑模板 | 对于所有页面 | 不可用 |
| HTL | 所有组件 | 有限 |
| 定位 | 对于所有页面 | 仅Geometrixx Outdoors |
| 屏幕 | 可用 | 不可用 |
| 移动设备 | 不可用 | 可用 |
| 手稿 | 不可用 | 可用 |
| 轮播、下载、图表组件 | 不可用 | 可用 |
| 列控件 | 替换为布局容器 | 可用 |
| Forms | 不可用 | 可用 |
| 营销活动 | 无电子邮件示例 | 可用 |

>[!NOTE]
>
>此列表力求完整，但不应被视为详尽无遗。

## Contribute {#contribute}

We.Retail已作为开源项目发布，并且可以从GitHub下载源代码的最新版本。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-sample-we-retail项目](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail)
* 将项目下载为 [ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/archive/master.zip)

最新版本也可以是 [已直接下载](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases/latest) 作为可安装的包。

如果遇到问题，请归档 [GitHub问题](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/issues).

您可以随意取舍，也可以参与其中 [拉取请求](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/pulls).

## 预览 {#preview}

We.Retail欢迎页面预览：

![screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32](assets/screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32.png)
