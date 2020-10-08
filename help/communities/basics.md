---
title: 社区组件基础知识
seo-title: 社区组件基础知识
description: 在编辑模式下向AEM站点添加社区功能并配置组件
seo-description: 在编辑模式下向AEM站点添加社区功能并配置组件
uuid: c017a7c5-40d1-4592-9317-96fd727dac86
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 21714581-7645-4b47-a9b0-9f1424013240
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 1%

---


# 社区组件基础知识 {#communities-components-basics}

## 概述 {#overview}

文档的创作部分介绍在作者编辑模式下将社区功能添加到AEM站点，并描述组件配置。

可以使用AEM实例和交互式社区组件指 [南探索组件](components-guide.md)。

## 访问社区组件 {#accessing-communities-components}

创作页面内容时，如果基础模板允许更改页面设计，则可以启用站点设计中组件浏览器中尚未提供的组件。

此处列出可用的社区 [组件](author-communities.md#available-communities-components)。

>[!NOTE]
>
>有关一般创作信息，请视图 [页面创作快速指南](../../help/sites-authoring/qg-page-authoring.md)。
>
>如果不熟悉AEM，请视图有关基本操 [作的文档](../../help/sites-authoring/basic-handling.md)。

### 进入设计模式 {#entering-design-mode}

如果在 **组件** 浏览器(Sidekick)中找不到Communities组件，则需要进入才能添 `Design Mode` 加其他Communities组件。 [可能还需要添加所需的客户端](#required-clientlibs) 库(clientlibs)。

有关详细信息，请 [参阅在设计模式下配置组件](../../help/sites-authoring/default-components-designmode.md)。

以下是选择几个社区组件并在组件浏览器中查看它们的图像：

![组件设计](assets/component-design.png)

现在，组件浏览器中提供选定的组件：

![component-design1](assets/component-design1.png)

## 必需的客户端库 {#required-clientlibs}

[需要客户端库](../../help/sites-developing/clientlibs.md) (clientlibs)，组件才能正常工作(JavaScript)和样式(CSS)。

在向页面添加社区组件时，如果结果是错误或意外外观，首先要尝试为社区组件添加所需的客户端库。 有关详细信息，请 [参阅Clientlibs for Communities组件](clientlibs.md)。

### 示例：最初放置的审阅没有客户端库…… {#example-initially-placed-reviews-without-client-libraries}

![clientlibs1](assets/clientlibs1.png)

### ...使用客户端库 {#and-with-client-libraries}

![clientlibs2](assets/clientlibs2.png)

## 标记 {#tagging}

许多Communities功能可配置为允许成员标记在发布环境中输入（发布）的内容。

如果允许标记，则社区站点的配置可设置为限制向发布环境中的成员显示的命名空间。 请参阅社 [区站点控制台](sites-console.md#tagging)。

允许标记的功能： [博客](blog-feature.md), [日历](calendar.md), [文件库](file-library.md)，论 [坛](forum.md)

使用标记的功能： [目录](catalog.md)、 [搜索](search.md)、 [社交标记云](tagcloud.md)

对于创作信息：

* [使用标记](../../help/sites-authoring/tags.md)

有关管理信息：

* 创建标记命名空间（分类）: [管理标记](../../help/sites-administering/tags.md)
* 社区站点配置：请参阅 [标记](sites-console.md#tagging)
* [标记用户生成的内容](../../help/sites-authoring/tags.md)
* [标记支持资源](tag-resources.md)

有关开发人员信息：

* [AEM Tagging Framework](../../help/sites-developing/framework.md)
* [Tagging Essentials](tag.md)

