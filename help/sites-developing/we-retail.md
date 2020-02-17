---
title: We.Retail Reference Implementation
seo-title: We.Retail Reference Implementation
description: We.Retail是参考实施的技术预览，它说明了使用AEM设置在线状态的推荐方式
seo-description: We.Retail是参考实施的技术预览，它说明了使用AEM设置在线状态的推荐方式
uuid: d8833192-b592-4812-bf9b-bd882e8ee7f0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: f50150af-deff-4c29-bfe0-1cfc67b29d51
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c

---


# We.Retail Reference Implementation{#we-retail-reference-implementation}

## 简介 {#introduction}

We.Retail是一个参考实施和示例内容，它说明了使用Adobe Experience manager建立在线状态的推荐方式。

We.Retail利用最新的AEM技术，如HTL、响应式布局、可编辑模板、核心组件等。

虽然它说明了零售垂直，但站点设置方式可应用于任何垂直，并且只有产品目录和购物车功能特定于零售。

## 功能 {#features}

作为AEM的标准参考实施，We.Retail展示了AEM的一些最强大的功能。

| **功能** | **描述** | **有兴趣？** |
|---|---|---|
| [全球化的站点结构](/help/sites-administering/tc-bp.md) | We.Retail包括实时复制到国家／地区特定网站的语言母版。 | [试试！](/help/sites-developing/we-retail-globalized-site-structure.md) |
| [响应式布局](/help/sites-authoring/responsive-layout.md) | 所有页面都具有响应式布局，可动态适应屏幕和设备大小。 | [试试！](/help/sites-developing/we-retail-responsive-layout.md) |
| [可编辑的模板](/help/sites-developing/page-templates-editable.md) | 所有页面都基于可编辑的模板，允许非开发人员调整和自定义模板。 | [试试！](/help/sites-developing/we-retail-editable-templates.md) |
| [HTML 模板语言](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) | 所有组件均基于HTL |  |
| [电子商务功能](/help/sites-developing/ecommerce.md) | 提供产品目录 |  |
| [社区站点](/help/communities/overview.md) | 允许访客加入社区讨论、阅读博客等 |  |
| [核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) | 所有组件都基于新的核心组件，并且更可用、用户可开箱即用 | [试试！](/help/sites-developing/we-retail-core-components.md) |
| [内容片段](/help/assets/content-fragments.md) | “We.Retail体验”部分展示了通过内容片段重用内容的强大功能。 | [试试！](/help/sites-developing/we-retail-content-fragments.md) |
| [体验片段](/help/sites-authoring/experience-fragments.md) | 体验片段是由一个或多个组件构成的组件组，包括可在页面内引用的内容和布局。 | [试试！](/help/sites-developing/we-retail-experience-fragments.md) |

## 入门 {#getting-started}

We.Retail作为AEM的示例内容提供。 为了使用，只需 [像通常一样启动AEM](/help/sites-deploying/deploy.md#getting-started)，确保未禁用示例内容。

>[!CAUTION]
>
>We.Retail不应安装在生产实例上。 生产实例应在运行模式 `nosamplecontent` 中 [启动](/help/sites-deploying/configure-runmodes.md)。

>[!CAUTION]
>
>We.Retail基于最新的AEM技术，因此不支持经 [典UI创作](/help/sites-classic-ui-authoring/home.md)。

### 最新版本 {#latest-version}

尽管We.Retail随AEM版本一起分发，但内容及其功能的更新可能会在发布后进行。 因此，可以从GitHub [下载最新版本](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases) ，然后将其作为包上 [传并](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system)[](/help/sites-administering/package-manager.md#installing-packages) 安装在AEM实例上。

### 首要步骤 {#first-steps}

1. 启动AEM（和／或安装We.Retail）后，站点 **We.Retail** 可在站点控制台 [中使用](/help/sites-authoring/basic-handling.md#global-navigation)。
1. 例如，可打开以下页面，其外观应如下面的附 [录所示](#appendix) :

   `https://<server name>:<port number>/editor.html/content/we-retail/language-masters/en.html`

## We.Retail &amp; Geometrixx {#we-retail-geometrixx}

Geometrixx及其许多化身在AEM的早期版本中用作示例内容。 自版本6.3以来，We.Retail一直是随AEM提供的示例内容，并作为新的标准参考实施。

We.Retail在技术上更加强大，利用最新的AEM技术更灵活、更具可扩展性，同时还演示了产品的最新功能。

### 功能比较 {#feature-comparison}

下表概述了We.Retail中与Geometrixx相比的主要功能。

* **“可用** ”表示示例内容中包含该功能的示例。
* **“不可用** ”表示示例内容中不提供该功能的示例，但并不意味着该功能本身不可用。

| **功能** | **We.Retail** | **Geometrixx** |
|---|---|---|
| 全球化的站点结构 | 实时复制到国家／地区特定站点的语言主页 | 不可用 |
| 内容片段 | 可用 | 不可用 |
| 体验片段 | 可用 | 不可用 |
| 响应式布局 | 适用于所有页面 | 仅Geometrixx Media |
| 可编辑的模板 | 适用于所有页面 | 不可用 |
| HTL | 所有组件 | 有限公司 |
| 定位 | 适用于所有页面 | 仅Geometrixx Outdoors |
| 屏幕 | 可用 | 不可用 |
| 移动设备 | 不可用 | 可用 |
| 手稿 | 不可用 | 可用 |
| 传送、下载、图表组件 | 不可用 | 可用 |
| 列控件 | 替换为布局容器 | 可用 |
| Forms | 不可用 | 可用 |
| 营销活动 | 无电子邮件示例 | 可用 |

>[!NOTE]
>
>此列表力求完整，但不应视为详尽无遗。

## Contribute {#contribute}

We.Retail已作为开放源项目发布，最新版本的源代码可从GitHub下载。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-sample-we-retail项目](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail)
* 将项目下载为 [ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/archive/master.zip)

最新版本也可以直接 [下载为可安](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases/latest) 装的包。

如果您遇到问题，请提交 [GitHub问题](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/issues)。

您可以随时购买或投稿 [请求](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/pulls)。

## 预览 {#preview}

We.Retail欢迎页面预览：

![screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32](assets/screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32.png)

