---
title: 创作 — 环境和工具
description: “网站”控制台允许您管理和导航您的网站。 使用两个窗格，可以扩展网站的结构并对所需元素执行操作。
uuid: 0a9ce725-042a-4697-81fe-ac86cbab0398
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 67625e62-7035-4eb5-8dd5-6840d775a547
docset: aem65
exl-id: 5d7b6b2e-d1d8-4efe-b9ff-c9542b4e67d7
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 6%

---

# 创作 — 环境和工具 {#authoring-the-environment-and-tools}

AEM 的创作环境提供了各种可用于组织和编辑内容的机制. 可以从各种控制台和页面编辑器访问提供的工具。

## 站点管理 {#site-administration}

此 **网站** 通过控制台，您可以管理和导航您的网站。 使用这两个窗格，可以展开网站的结构并对所需元素执行操作：

![chlimage_1-108](assets/chlimage_1-108.png)

## 编辑页面内容 {#editing-your-page-content}

使用经典UI有一个单独的页面编辑器，该编辑器使用内容查找器和Sidekick：

`https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

![chlimage_1-109](assets/chlimage_1-109.png)

## 访问帮助 {#accessing-help}

各种 **帮助** 可从AEM中直接访问资源：

以及访问 [控制台工具栏的帮助](/help/sites-classic-ui-authoring/author-env-basic-handling.md#accessing-help)，您还可以从sidekick访问帮助(使用？ 图标)在编辑页面时：

![Sidekick已折叠](do-not-localize/sidekick-collapsed-2.png)

或者使用 **帮助** 按钮；这将显示上下文相关帮助。

## Sidekick {#sidekick}

此 **组件** sidekick的选项卡允许您浏览要添加到当前页面的组件。 可以展开所需的组，然后将组件拖动到页面上的所需位置。

![chlimage_1-110](assets/chlimage_1-110.png)

## 内容查找器 {#the-content-finder}

内容查找器是一种在编辑页面时在存储库中查找资产和/或内容的快速轻松的方法。

您可以使用内容查找器查找一系列资源。 在适当的情况下，您可以将某个项目拖放到页面上的某个段落中：

* [图像](#finding-images)
* [文档](#finding-documents)
* [电影](#finding-movies)
* [Dynamic Media浏览器](/help/sites-administering/scene7.md#scene7contentbrowser)
* [页面](#finding-pages)

* [段落](#referencing-paragraphs-from-other-pages)
* [产品](#products)
* 或者 [按存储库结构浏览网站](#the-content-finder)

您可以利用所有选项 [搜索特定项目](#the-content-finder).

### 查找图像 {#finding-images}

此选项卡列出了存储库中的所有图像。

在页面上创建“图像”段落后，可以将某个项目拖放到段落中。

![chlimage_1-111](assets/chlimage_1-111.png)

### 查找文档 {#finding-documents}

此选项卡列出存储库中的所有文档。

在页面上创建“下载”段落后，您可以将某个项目拖放到段落中。

![chlimage_1-112](assets/chlimage_1-112.png)

### 查找电影 {#finding-movies}

此选项卡列出了存储库中的所有影片(例如，Flash项目)。

在页面上创建相应的段落(例如Flash)后，您可以将某个项目拖放到段落中。

![chlimage_1-113](assets/chlimage_1-113.png)

### 产品 {#products}

此选项卡列出了所有产品。 在页面上创建相应的段落（例如，“产品”）后，您可以将某个项目拖放到段落中。

![chlimage_1-114](assets/chlimage_1-114.png)

### 查找页面 {#finding-pages}

此选项卡显示所有页面。 双击任何页面以打开它进行编辑。

![chlimage_1-115](assets/chlimage_1-115.png)

### 引用其他页面的段落 {#referencing-paragraphs-from-other-pages}

利用此选项卡可搜索其他页面。 将列出该页面中的所有段落。 然后，您可以将段落拖动到当前页面，这将创建对原始段落的引用。

![chlimage_1-116](assets/chlimage_1-116.png)

### 使用完整存储库视图 {#using-the-full-repository-view}

此选项卡显示存储库中的所有资源。

![chlimage_1-117](assets/chlimage_1-117.png)

### 在内容浏览器中使用搜索 {#using-search-with-the-content-browser}

在所有选项上，您可以搜索特定项目。 将列出与搜索模式匹配的任何标记和资源：

![screen_shot_2012-02-08at100746am](assets/screen_shot_2012-02-08at100746am.png)

您还可以使用通配符进行搜索。 支持的通配符包括：

* `*`
匹配零个或更多字符的序列。

* `?`
匹配单个字符。

>[!NOTE]
>
>有一个伪属性“name”，必须使用该属性执行通配符搜索。

例如，如果存在名称为的可用图像：

`ad-nmvtis.jpg`

以下搜索模式将找到它（以及与该模式匹配的任何其他图像）：

* `name:*nmv*`
* `name:AD*`
字符匹配为 *非* 区分大小写。

* `name:ad?nm??is.*`
您可以在查询中使用任意数量的通配符。

>[!NOTE]
>
>您还可以使用 [SQL2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/commons/query/sql2/package-summary.html) 搜索。

## 显示引用 {#showing-references}

AEM允许您查看哪些页面已链接到您当前处理的页面。

要显示直接页面引用，请执行以下操作：

1. 在副手中，选择 **页面** 选项卡图标。

   ![screen_shot_2012-02-16at83127pm](assets/screen_shot_2012-02-16at83127pm.png)

1. 选择 **显示引用……** AEM将打开“引用”窗口，并显示引用选定页面的页面，包括其路径。

   ![screen_shot_2012-02-16at83311pm](assets/screen_shot_2012-02-16at83311pm.png)

在某些情况下，可以从Sidekick中执行其他操作，包括：

* [启动项](/help/sites-classic-ui-authoring/classic-launches.md)
* [Live Copy](/help/sites-administering/msm.md)

* [Blueprint](/help/sites-administering/msm-best-practices.md)

其他 [可以在网站控制台中查看页面间关系](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console).

## 审查日志 {#audit-log}

此 **审核日志** 可从以下位置访问： **信息** 替他搭便车。 其中列出了在当前页面上执行的最新操作；例如：

![chlimage_1-118](assets/chlimage_1-118.png)

## 页面信息 {#page-information}

网站控制台也 [提供了有关页面当前状态的信息](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console) 例如，发布、修改、锁定、活动副本等。

## 页面模式 {#page-modes}

使用经典UI编辑页面时，可以使用Sidekick底部的图标访问各种模式：

![页面模式](do-not-localize/chlimage_1-12.png)

Sidekick底部的一行图标用于切换处理页面的模式：

* [编辑](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md)
这是默认模式，允许您编辑页面，添加或删除组件并进行其他更改。

* [预览](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#previewing-pages)
利用此模式，可预览页面，就像页面以最终形式出现在您的网站中一样。

* [设计](/help/sites-classic-ui-authoring/classic-page-author-design-mode.md#main-pars-procedure-0)
在此模式下，您可以通过配置可访问的组件来编辑页面设计。

>[!NOTE]
>
>还可以使用其他选项：
>
>* [基架](/help/sites-classic-ui-authoring/classic-feature-scaffolding.md)
>* [ClientContext](/help/sites-administering/client-context.md)
>* 网站 — 将打开网站控制台。
>* 重新加载 — 将刷新页面。

## 键盘快捷键 {#keyboard-shortcuts}

可以使用各种[键盘快捷键](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md)。
