---
title: We.Retail参考实施
description: We.Retail是参考实施的技术预览，它说明了使用AEM设置在线展示的推荐方法
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 504c61c7-dcd3-412c-9239-d24a2b78e4b9
source-git-commit: f7b24617dec77c6907798b1615debdc2329c9d80
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 10%

---

# We.Retail参考实施{#we-retail-reference-implementation}

## 简介 {#introduction}

We.Retail是一个参考实施和示例内容，它说明了使用Adobe Experience Manager设置在线展示的推荐方法。

We.Retail使用最新的Adobe Experience Manager (AEM)技术，例如HTL、响应式布局、可编辑模板、核心组件等。

虽然它说明了零售行业，但网站设置方式可应用于任何行业，并且只有产品目录和购物车功能是零售特定的。

## 功能 {#features}

作为AEM标准参考实施，We.Retail展示了AEM的一些最强大的功能。

| **专题** | **描述** | **有兴趣吗？** |
|---|---|---|
| [全局化站点结构](/help/sites-administering/tc-bp.md) | We.Retail包括语言母版，这些母版将实时复制到国家/地区特定的站点中。 | [试试看！](/help/sites-developing/we-retail-globalized-site-structure.md) |
| [响应式布局](/help/sites-authoring/responsive-layout.md) | 所有页面都具有响应式布局，可动态调整以适应屏幕和设备大小。 | [试试看！](/help/sites-developing/we-retail-responsive-layout.md) |
| [可编辑的模板](/help/sites-developing/page-templates-editable.md) | 所有页面都基于可编辑的模板，允许非开发人员调整和自定义模板。 | [试试看！](/help/sites-developing/we-retail-editable-templates.md) |
| [HTML 模板语言](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) | 所有组件都基于HTL |  |
| [电子商务功能](/help/commerce/cif-classic/developing/ecommerce.md) | 功能产品目录 |  |
| [社区站点](/help/communities/overview.md) | 允许访客加入社区讨论、阅读博客等 |  |
| [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) | 所有组件都基于新的核心组件，并且更加可用，可开箱即用且可由用户配置 | [试试看！](/help/sites-developing/we-retail-core-components.md) |
| [内容片段](/help/assets/content-fragments/content-fragments.md) | We.Retail体验部分展示了通过内容片段重用内容的强大功能。 | [试试看！](/help/sites-developing/we-retail-content-fragments.md) |
| [体验片段](/help/sites-authoring/experience-fragments.md) | 体验片段是由一个或多个组件组成的组，其中包括可在页面中引用的内容和布局。 | [试试看！](/help/sites-developing/we-retail-experience-fragments.md) |

## 快速入门 {#getting-started}

We.Retail作为AEM示例内容提供。 要使用，只需使用 [像往常一样启动AEM](/help/sites-deploying/deploy.md#getting-started)，并确保未禁用示例内容。

>[!CAUTION]
>
>请勿在生产实例上安装We.Retail。 生产实例应在中启动 `nosamplecontent` [运行模式](/help/sites-deploying/configure-runmodes.md).

>[!CAUTION]
>
>We.Retail基于最新的AEM技术，因此不支持 [经典UI创作](/help/sites-classic-ui-authoring/home.md).

### 最新版本 {#latest-version}

尽管We.Retail随AEM版本一起分发，但可能会在该版本之后对内容及其功能进行更新。 因此，可以 [从GitHub下载最新版本](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases) 然后 [上传](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system) 和 [安装](/help/sites-administering/package-manager.md#installing-packages) 它会在您的AEM实例中作为包提供。

### 首要步骤 {#first-steps}

1. 启动AEM（和/或安装We.Retail）后，网站 **We.Retail** 可在 [站点控制台](/help/sites-authoring/basic-handling.md#global-navigation).
1. 例如，可以打开以下页面，它应看起来像中显示在 [附录](#appendix) 下：

   `https://<server name>:<port number>/editor.html/content/we-retail/language-masters/en.html`

## We.Retail和Geometrixx {#we-retail-geometrixx}

Geometrixx及其许多化身在早期版本的AEM中用作示例内容。 自版本6.3开始，We.Retail是与AEM一起提供的示例内容，可用作新的标准参考实施。

We.Retail在技术上更加稳健，它利用最新的AEM技术变得更加灵活和可扩展，同时还演示了该产品的最新功能。

### 功能比较 {#feature-comparison}

下表概述了与Geometrixx相比，We.Retail中可用的主要功能。

* **可用** 表示在示例内容中找到该功能的示例。
* **不可用** 表示该功能的示例在示例内容中不可用，但并不意味着该功能本身不可用。

| **专题** | **We.Retail** | **Geometrixx** |
|---|---|---|
| 全局化站点结构 | 语言母版实时复制到国家/地区特定的站点 | 不可用 |
| 内容片段 | 可用 | 不可用 |
| 体验片段 | 可用 | 不可用 |
| 响应式布局 | 对于所有页面 | 仅Geometrixx Media |
| 可编辑模板 | 对于所有页面 | 不可用 |
| HTL | 所有组件 | 有限 |
| 定位 | 对于所有页面 | 仅Geometrixx Outdoors |
| Screens | 可用 | 不可用 |
| 移动设备 | 不可用 | 可用 |
| 手稿 | 不可用 | 可用 |
| 轮播查看器、下载和图表组件 | 不可用 | 可用 |
| 列控件 | 替换为布局容器 | 可用 |
| Forms | 不可用 | 可用 |
| 营销活动 | 无电子邮件示例 | 可用 |

>[!NOTE]
>
>此列表力求完整，但不应视为详尽无遗。

## Contribute {#contribute}

We.Retail已作为开源项目发布，可以从GitHub下载最新版本的源代码。

GITHUB上的代码

您可以在 GitHub 上找到此页面的代码。

* [在GitHub上打开aem-sample-we-retail项目](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail)
* 将项目下载为 [ZIP文件](https://codeload.github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/zip/refs/heads/master)

最新版本也可以是 [已直接下载](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases/tag/we.retail.reactor-4.0.0) 作为可安装的包。

如果遇到问题，请将 [GitHub问题](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/issues).

欢迎您随心所欲地提出建议或投稿 [拉取请求](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/pulls).

## 预览 {#preview}

We.Retail欢迎页面预览：

![screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32](assets/screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32.png)
