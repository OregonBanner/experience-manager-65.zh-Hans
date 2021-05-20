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
exl-id: eb5ce76a-bf28-4540-bc2d-3b5ecb8286f2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 1%

---

# 社区组件基础知识{#communities-components-basics}

## 概述 {#overview}

文档的创作部分介绍了如何在创作编辑模式下将社区功能添加到AEM站点，以及组件配置的说明。

可以使用AEM实例和交互式[社区组件指南](components-guide.md)来探索组件。

## 访问社区组件{#accessing-communities-components}

在创作页面内容时，如果基础模板允许更改页面设计，则可以启用组件浏览器中尚未在站点设计中提供的组件。

此处](author-communities.md#available-communities-components)列出了可用的社区组件。[

>[!NOTE]
>
>有关一般创作信息，请查看[页面创作快速指南](../../help/sites-authoring/qg-page-authoring.md)。
>
>如果不熟悉AEM，请查看有关[基本操作](../../help/sites-authoring/basic-handling.md)的文档。

### 进入设计模式{#entering-design-mode}

如果在组件浏览器(Sidekick)中未找到&#x200B;**Communities**&#x200B;组件，则需要输入`Design Mode`以添加其他Communities组件。 [可能还需要添加所需的客户端库](#required-clientlibs) (clientlibs)。

有关详细信息，请参阅[在设计模式下配置组件](../../help/sites-authoring/default-components-designmode.md)。

以下是选择一些社区组件并在组件浏览器中查看这些组件的图像：

![组件设计](assets/component-design.png)

现在，组件浏览器中提供了选定的组件：

![component-design1](assets/component-design1.png)

## 必需的Clientlibs {#required-clientlibs}

[需要客户端库](../../help/sites-developing/clientlibs.md) (clientlibs)才能正常运行(JavaScript)和组件样式(CSS)。

在向页面添加社区组件时，如果结果出现错误或意外外观，则首先要尝试为社区组件添加所需的clientlib。 有关详细信息，请参阅[Clientlibs for Communities Components](clientlibs.md)。

### 示例：最初放置的审阅没有客户端库…… {#example-initially-placed-reviews-without-client-libraries}

![clientlibs1](assets/clientlibs1.png)

### ...使用客户端库{#and-with-client-libraries}

![clientlibs2](assets/clientlibs2.png)

## 标记 {#tagging}

可以将许多社区功能配置为允许成员标记在发布环境中输入（发布）的内容。

如果允许添加标记，则可以将社区站点的配置设置为限制发布环境中向成员呈现的命名空间。 请参阅[社区站点控制台](sites-console.md#tagging)。

允许标记的功能：[blog](blog-feature.md), [calend](calendar.md), [文件库](file-library.md), [forum](forum.md)

使用标记的功能：[catalog](catalog.md), [search](search.md), [social tag cloud](tagcloud.md)

对于创作信息：

* [使用标记](../../help/sites-authoring/tags.md)

有关管理信息：

* 创建标记命名空间（分类）：[管理标记](../../help/sites-administering/tags.md)
* 社区站点配置：请参阅[TAGGING](sites-console.md#tagging)
* [标记用户生成的内容](../../help/sites-authoring/tags.md)
* [标记支持资源](tag-resources.md)

有关开发人员信息：

* [AEM Tagging Framework](../../help/sites-developing/framework.md)
* [标记要点](tag.md)
