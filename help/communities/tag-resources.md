---
title: 标记支持资源
seo-title: 标记支持资源
description: Tagging of enablement resources allows for fillering resources and learning paths as members browse catalogs
seo-description: Tagging of enablement resources allows for fillering resources and learning paths as members browse catalogs
uuid: daf8a4f4-486b-498c-99e9-d1533a830e64
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: c012d639-c6e6-4f73-bbd8-78a4baa38c17
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---


# 标记启用资源{#tagging-enablement-resources}

## 概述 {#overview}

启用资源的标记允许在成员浏览[目录](functions.md#catalog-function)时筛选资源和学习路径。

本质上：

* [为每个目录创](../../help/sites-administering/tags.md#creating-a-namespace) 建标记名称

   * [设置标记权限](../../help/sites-administering/tags.md#setting-tag-permissions)
   * 仅适用于社区成员（封闭社区）

      * 允许对[社区站点的成员组](users.md#publish-group-roles)进行读取访问
   * 对于任何站点访客，无论是登录还是匿名（开放社区）

      * 允许`Everyone`组的读访问
   * [发布标记](../../help/sites-administering/tags.md#publishing-tags)



* [定义社区站点的标记范围](sites-console.md#tagging)

   * [配置站点结构中存在的目录](functions.md#catalog-function)

      * 可以向目录实例添加标记以控制在UI过滤器中显示的标记的列表。
      * 可以添加[预过滤器](catalog-developer-essentials.md#pre-filters)以限制目录包含的资源。

* [发布社区站点](sites-console.md#publishing-the-site)
* [将标记应用于](resources.md#create-a-resource) 支持资源，以便明确筛选
* [发布支持资源](resources.md#publish)

## 社区站点标记{#community-site-tags}

在创建或编辑社区站点时，[标记设置](sites-console.md#tagging)通过选择现有标记命名空间的子集来设置可用于站点功能的标记的范围。

尽管可以随时创建标记并将其添加到社区站点，但建议事先设计分类，类似于设计数据库。 请参阅[使用标记](../../help/sites-authoring/tags.md)。

以后向现有社区站点添加标记时，必须先保存编辑，然后才能将新标记添加到站点结构中的目录功能。

对于社区站点，在发布站点和发布标记后，必须启用对社区成员的读取访问权限。 请参阅[设置标记权限](../../help/sites-administering/tags.md#setting-tag-permissions)。

以下是当管理员对组`Community Enable Members`的`/etc/tags/ski-catalog`应用读取权限时，CRXDE中显示的方式。

![站点标签](assets/site-tags.png)

## 目录标签命名空间{#catalog-tag-namespaces}

目录功能使用标签来定义自己。 在社区站点中配置目录功能时，要选择的标签命名空间集由社区站点的标签空间集的范围定义。

Catalog函数包含一个标记设置，用于定义目录的过滤器UI中列出的标记。 设置“所有命名空间”是指为社区站点选择的标记命名空间的范围。

![catalog-命名空间](assets/catalog-namespace.png)

## 将标记应用到Enablement Resources {#applying-tags-to-enablement-resources}

选中`Show in Catalog`后，启用资源和学习路径将显示在所有目录中。 向资源和学习路径添加标记将允许预过滤到特定目录中以及在目录UI中过滤。

通过创建[预过滤器](catalog-developer-essentials.md#pre-filters)，可以限制启用资源和特定目录的学习路径。

目录UI允许访客将标签过滤器应用于该目录中显示的资源和学习路径列表。

将标签应用到Enablement Resource的管理员必须了解与目录关联的标签命名空间以及分类，以便选择子标签以更精细地分类。

例如，如果在名为`Ski Catalog`的目录上创建并设置了`ski-catalog`命名空间，则它可能有两个子标签：`lesson-1`和`lesson-2`。

因此，使用以下任一选项标记的任何支持资源：

* ski-catalog:lesson-1
* ski-catalog:lesson-2

在enablement resource发布后，将显示在`Ski Catalog`中。

![基本信息](assets/applytags-basicinfo.png)

## 查看发布时的目录{#viewing-catalog-on-publish}

从创作环境设置所有内容并发布后，在发布环境中就可以体验使用目录查找支持资源的体验。

如果下拉列表中未显示任何标记命名空间，请确保在发布环境中正确设置了权限。

如果添加了标记命名空间且缺少标记，请确保重新发布标记和站点。

如果在查看目录时选择标记后未显示启用资源，请确保目录的命名空间中有一个标记已应用到启用资源。

![视图目录](assets/viewcatalog.png)

