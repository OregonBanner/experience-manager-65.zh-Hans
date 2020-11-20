---
title: 创作 - 环境和工具
seo-title: 创作 - 环境和工具
description: 通过网站控制台，您可以管理网站以及在网站中导航。利用两个窗格，可以扩展网站的结构，并对所需元素执行相应的操作。
seo-description: 通过网站控制台，您可以管理网站以及在网站中导航。利用两个窗格，可以扩展网站的结构，并对所需元素执行相应的操作。
uuid: 0a9ce725-042a-4697-81fe-ac86cbab0398
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 67625e62-7035-4eb5-8dd5-6840d775a547
docset: aem65
translation-type: tm+mt
source-git-commit: 90c99e527a40bb663d4f32d8746b46cf34a2319f
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 88%

---


# 创作 - 环境和工具 {#authoring-the-environment-and-tools}

AEM 的创作环境提供了各种可用于组织和编辑内容的机制。可以从各种控制台和页面编辑器访问提供的工具。

## 站点管理 {#site-administration}

通过&#x200B;**网站**&#x200B;控制台，您可以管理网站以及在网站中导航。利用两个窗格，可以扩展网站的结构，并对所需元素执行相应的操作：

![chlimage_1-108](assets/chlimage_1-108.png)

## 编辑页面内容 {#editing-your-page-content}

经典 UI 使用内容查找器和 Sidekick，提供一个单独的页面编辑器：

`https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

![chlimage_1-109](assets/chlimage_1-109.png)

## 访问帮助 {#accessing-help}

可以在 AEM 内直接访问各种&#x200B;**帮助**&#x200B;资源：

在编辑页面时，除了可以访问[控制台工具栏中的帮助](/help/sites-classic-ui-authoring/author-env-basic-handling.md#accessing-help)，您还可以从 Sidekick 中访问帮助（使用 ? 图标）：

![](do-not-localize/sidekick-collapsed-2.png)

或者，使用特定组件编辑对话框中的&#x200B;**帮助**&#x200B;按钮；这将根据上下文显示帮助。

## Sidekick {#sidekick}

通过 Sidekick 的&#x200B;**组件**&#x200B;选项卡可以浏览可加入当前页面的组件。所需组可以展开，然后将组件拖动至页面上的所需位置。

![chlimage_1-110](assets/chlimage_1-110.png)

## 内容查找器 {#the-content-finder}

内容查找器是编辑页面时在存储库内查找资产和/或内容的快速而简单的方法。

您可以使用内容查找器定位资源的范围。如果合适，您可以将项目拖放到页面上的某个段落中：

* [图像](#finding-images)
* [文档](#finding-documents)
* [电影](#finding-movies)
* [Scene 7 媒体浏览器](/help/sites-administering/scene7.md#scene7contentbrowser)
* [](#products) [页面](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#finding-pages)

* [段落](#referencing-paragraphs-from-other-pages)
* [产品](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#products)
* 或[按存储库结构浏览网站](#the-content-finder)

对于所有选项，均可[搜索特定项目](#the-content-finder)。

### 查找图像 {#finding-images}

此选项卡列出了存储库中的所有图像。

您在页面中创建了图像段落后，可以拖曳项目并将其放置在段落中。

![chlimage_1-111](assets/chlimage_1-111.png)

### 查找文档 {#finding-documents}

此选项卡列出了存储库中的所有文档。

您在页面中创建了 Download 段落后，可以拖曳项目并将其放置在段落中。

![chlimage_1-112](assets/chlimage_1-112.png)

### 查找电影 {#finding-movies}

此选项卡列出了存储库中的所有电影（例如 Flash 项目）。

您在页面中创建了合适的段落（例如 Flash）后，可以拖曳项目并将其放置在段落中。

![chlimage_1-113](assets/chlimage_1-113.png)

### 产品 {#products}

此选项卡列出了所有产品。您在页面中创建了合适的段落（例如产品）后，可以拖曳项目并将其放置在段落中。

![chlimage_1-115](assets/chlimage_1-114.png)

### 查找页面 {#finding-pages}

此选项卡显示所有页面。多次-单击任何页面可打开它进行编辑。

![chlimage_1-115](assets/chlimage_1-115.png)

### 从其他页面引用段落 {#referencing-paragraphs-from-other-pages}

此选项卡允许您搜索其他页面。将列出该页面中的所有段落。您随后可以将一个段落拖曳到当前页面，这样会创建一个对原始段落的引用。

![chlimage_1-116](assets/chlimage_1-116.png)

### 使用完整库视图 {#using-the-full-repository-view}

此选项卡显示存储库中的所有资源。

![chlimage_1-117](assets/chlimage_1-117.png)

### 使用带有内容浏览器的搜索功能 {#using-search-with-the-content-browser}

在所有选项上都可以搜索特定项目。列出与搜索模式匹配的所有标记和所有资源：

![screen_shot_2012-02-08at100746am](assets/screen_shot_2012-02-08at100746am.png)

您还可以使用通配符进行搜索。支持的通配符有：

* `*`替代一串零个或多个字符。

* `?`替代单个字符。

>[!NOTE]
>
>还有一个伪属性“name”，必须在执行通配符搜索时使用。

例如，如果有一幅图像的名称为：

`ad-nmvtis.jpg`

，则以下搜索模式可以找到它（以及与此模式相匹配的其他任何图像）：

* `name:*nmv*`
* `name:AD*`
字符匹配*不*&#x200B;区分大小写.

* `name:ad?nm??is.*`
您可以在查询中使用任何数量的通配符.

>[!NOTE]
>
>You can also use [SQL2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/commons/query/sql2/package-summary.html) search.

## 显示引用 {#showing-references}

AEM 允许您查看哪些页面链接至您当前工作的页面。

显示直接页面引用：

1. 在 Sidekick 中，选择&#x200B;**页面**&#x200B;选项卡图标。

   ![screen_shot_2012-02-16at83127pm](assets/screen_shot_2012-02-16at83127pm.png)

1. Select **Show References...** AEM opens the References window and displays which pages refer to the selected page, including their paths.

   ![screen_shot_2012-02-16at83311pm](assets/screen_shot_2012-02-16at83311pm.png)

在某些情况下，您还可以从 Sidekick 执行其他操作，包括：

* [启动项](/help/sites-classic-ui-authoring/classic-launches.md)
* [Live Copy](/help/sites-administering/msm.md)

* [Blueprint](/help/sites-administering/msm-best-practices.md)

其他[页面间关系可以在“网站”控制台中进行查看](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console)。

## 审查日志 {#audit-log}

从 Sidekick 的&#x200B;**信息**&#x200B;选项卡中，可以访问&#x200B;**审核日志**。它列出了对当前页面执行的近期操作，例如：

![chlimage_1-118](assets/chlimage_1-118.png)

## 页面信息 {#page-information}

The Website console also [provides information about the current status of the page](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console) such as publication, modification, locked, livecopy, etc.

## 页面模式 {#page-modes}

使用经典 UI 编辑页面时，可使用 Sidekick 底部的图标访问各种模式：

![](do-not-localize/chlimage_1-12.png)

Sidekick 底部的图标行用于切换处理页面的模式：

* [编辑](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md)
这是默认模式，它允许您通过添加或删除组件以及进行其他更改来编辑页面。

* [预览](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#previewing-pages)
通过此模式，可以预览页面以最终形式在网站中显示的情况。

* [设计](/help/sites-classic-ui-authoring/classic-page-author-design-mode.md#main-pars-procedure-0)
在此模式下，您可以通过配置可访问的组件来编辑页面设计。

>[!NOTE]
>
>还有其他一些可用选项：
>
>* [基架](/help/sites-classic-ui-authoring/classic-feature-scaffolding.md)
>* [ClientContext](/help/sites-administering/client-context.md)
>* 网站 - 将打开“网站”控制台。
>* 重新加载 - 将刷新页面。


## 键盘快捷键 {#keyboard-shortcuts}

可以使用各种[键盘快捷键](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md)。
