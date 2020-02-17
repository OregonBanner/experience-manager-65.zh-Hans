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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 社区组件基础知识 {#communities-components-basics}

## 概述 {#overview}

文档的创作部分介绍在创作编辑模式下向AEM站点添加社区功能以及组件配置。

可以使用AEM实例和交互式社区组件指南来 [探索组件](components-guide.md)。

## 访问社区组件 {#accessing-communities-components}

在创作页面内容时，如果基础模板允许对页面设计进行更改，则可以启用站点设计中组件浏览器中尚未提供的组件。

此处列出了可用的社区 [组件](author-communities.md#available-communities-components)。

>[!NOTE]
>
>有关常规创作信息，请查 [看页面创作快速指南](../../help/sites-authoring/qg-page-authoring.md)。
>
>如果不熟悉AEM，请查看有关基本操作 [的文档](../../help/sites-authoring/basic-handling.md)。

### 进入设计模式 {#entering-design-mode}

如果在组 **件浏览器** (Sidekick)中找不到Communities组件，则需要进入才能添 `Design Mode` 加其他Communities组件。 [可能还需要添加所需的客户端库](#required-clientlibs) (clientlibs)。

有关详细信息，请参 [阅在设计模式下配置组件](../../help/sites-authoring/default-components-designmode.md)。

以下是选择几个Communities组件并在组件浏览器中查看它们的图像：

![chlimage_1-424](assets/chlimage_1-424.png)

现在，选定的组件在组件浏览器中可用：

![chlimage_1-425](assets/chlimage_1-425.png)

## 必需的Clientlib {#required-clientlibs}

[需要客户端库](../../help/sites-developing/clientlibs.md) (clientlibs)才能正常运行组件(JavaScript)和样式(CSS)。

在向页面添加社区组件时，如果结果是错误或意外外观，则首先要尝试为社区组件添加所需的clientlib。 有关详细信息，请参 [阅Clientlibs for Communities组件](clientlibs.md)。

### 示例：最初放置的审阅没有客户端库…… {#example-initially-placed-reviews-without-client-libraries}

![chlimage_1-426](assets/chlimage_1-426.png)

### ...使用客户端库 {#and-with-client-libraries}

![chlimage_1-427](assets/chlimage_1-427.png)

## 标记 {#tagging}

许多Communities功能可配置为允许成员标记在发布环境中输入（发布）的内容。

如果允许标记，则可以将社区站点的配置设置为限制发布环境中向成员显示的命名空间。 请参阅“社 [区站点”控制台](sites-console.md#tagging)。

允许标记的功能：博 [客](blog-feature.md)，日 [历](calendar.md)，文 [件库](file-library.md)，论 [坛](forum.md)

使用标记的功能：目 [录](catalog.md), [搜索](search.md), [社交标记云](tagcloud.md)

对于创作信息：

* [使用标记](../../help/sites-authoring/tags.md)

有关管理信息：

* 创建标记命名空间（分类）:管理 [标记](../../help/sites-administering/tags.md)
* 社区站点配置：请参阅 [标记](sites-console.md#tagging)
* [标记用户生成的内容](../../help/sites-authoring/tags.md)
* [标记支持资源](tag-resources.md)

有关开发人员信息：

* [AEM Tagging Framework](../../help/sites-developing/framework.md)
* [Tagging Essentials](tag.md)

