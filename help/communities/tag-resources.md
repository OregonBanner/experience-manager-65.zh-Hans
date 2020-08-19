---
title: 标记支持资源
seo-title: 标记支持资源
description: 标记支持资源允许在成员浏览目录时筛选资源和学习路径
seo-description: 标记支持资源允许在成员浏览目录时筛选资源和学习路径
uuid: daf8a4f4-486b-498c-99e9-d1533a830e64
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: c012d639-c6e6-4f73-bbd8-78a4baa38c17
translation-type: tm+mt
source-git-commit: 2fcd87cd1def7fc265ba40c83b50db86618f3b70
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---


# 标记支持资源 {#tagging-enablement-resources}

## 概述 {#overview}

标记支持资源允许在成员浏览目录时筛选资源和学习 [路径](functions.md#catalog-function)。

本质上：

* [为每个目录创建标记命名空间](../../help/sites-administering/tags.md#creating-a-namespace) ，以便创建

   * [设置标记权限](../../help/sites-administering/tags.md#setting-tag-permissions)
   * 仅限社区成员（封闭社区）

      * 允许对社区站 [点成员组的读取访问](users.md#publish-group-roles)
   * 对于任何站点访客，无论是登录还是匿名（开放社区）

      * 允许对组进行读取访 `Everyone` 问
   * [发布标记](../../help/sites-administering/tags.md#publishing-tags)



* [定义社区站点的标记范围](sites-console.md#tagging)

   * [配置站点结构中存在的目录](functions.md#catalog-function)

      * 可以向目录实例添加标记，以控制在UI过滤器中显示的标记列表。
      * 可以添 [加预过滤器](catalog-developer-essentials.md#pre-filters)，以限制目录的包含资源。

* [发布社区站点](sites-console.md#publishing-the-site)
* [将标记应用于支持资源](resources.md#create-a-resource) ，以便可以断断然筛选它们
* [发布支持资源](resources.md#publish)

## 社区站点标记 {#community-site-tags}

创建或编辑社区站点时，“标 [记](sites-console.md#tagging) ”设置通过选择现有标记命名空间的子集来设置可用于站点功能的标记的范围。

虽然可以随时创建标记并将其添加到社区站点，但建议事先设计分类，类似于设计数据库。 请参 [阅使用标记](../../help/sites-authoring/tags.md)。

以后向现有社区站点添加标记时，必须先保存编辑，然后才能将新标记添加到站点结构中的目录功能。

对于社区站点，在发布站点和发布标记后，必须启用对社区成员的读取访问权限。 请参 [阅设置标记权限](../../help/sites-administering/tags.md#setting-tag-permissions)。

以下是管理员对组应用读取权限时CRXDE中显示 `/etc/tags/ski-catalog` 的方式 `Community Enable Members`。

![站点标签](assets/site-tags.png)

## 目录标记命名空间 {#catalog-tag-namespaces}

目录功能使用标记来定义自身。 在社区站点中配置目录功能时，要选择的标记命名空间集由社区站点的标记空间集的范围定义。

Catalog函数包含一个标记设置，它定义在目录的筛选器UI中列出的标记。 设置“所有命名空间”是指为社区站点选择的标记命名空间的范围。

![catalog-命名空间](assets/catalog-namespace.png)

## 将标记应用到Enablement Resources {#applying-tags-to-enablement-resources}

选中后，Enablement Resources和学习路径将显示在所有 `Show in Catalog` 目录中。 向资源和学习路径添加标记将允许预过滤到特定目录中以及在目录UI中过滤。

通过创建预过滤器，可以限制启用资源和特定目录 [的学习路径](catalog-developer-essentials.md#pre-filters)。

目录UI允许访客将标记过滤器应用于该目录中显示的资源和学习路径的列表。

将标记应用于启用资源的管理员必须了解与目录相关的标记命名空间，以及分类，以便选择子标记以进行更精细的分类。

例如，如果在名 `ski-catalog` 为的目录上创建了命名空间并设置 `Ski Catalog`了该，则它可能有两个子标记： `lesson-1` 和 `lesson-2`。

因此，使用以下任一选项标记的任何支持资源：

* ski-catalog:lesson-1
* ski-catalog:lesson-2

将在启 `Ski Catalog` 用资源发布后显示。

![基本信息](assets/applytags-basicinfo.png)

## 在发布时查看目录 {#viewing-catalog-on-publish}

从创作环境设置所有内容并发布后，在发布环境中即可体验使用目录查找支持资源的体验。

如果下拉列表中未显示标记命名空间，请确保在发布环境中正确设置了权限。

如果添加了标记命名空间且缺少标记，请确保标记和站点已重新发布。

如果在查看目录时选择标记后未显示启用资源，请确保目录的命名空间中有一个标记应用于启用资源。

![视图目录](assets/viewcatalog.png)

