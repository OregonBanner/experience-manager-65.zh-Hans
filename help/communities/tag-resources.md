---
title: 标记启用资源
seo-title: Tagging Enablement Resources
description: 启用资源标记允许在成员浏览目录时筛选资源和学习路径
seo-description: Tagging of enablement resources allows for filtering of resources and learning paths as members browse catalogs
uuid: daf8a4f4-486b-498c-99e9-d1533a830e64
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: c012d639-c6e6-4f73-bbd8-78a4baa38c17
role: Admin
exl-id: ce58c8e9-8b4a-43fb-a108-ed2ac40268c7
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---

# 标记启用资源 {#tagging-enablement-resources}

## 概述 {#overview}

启用资源标记允许在成员浏览时筛选资源和学习路径 [目录](functions.md#catalog-function).

基本上：

* [创建标记命名空间](../../help/sites-administering/tags.md#creating-a-namespace) 每个目录

   * [设置标记权限](../../help/sites-administering/tags.md#setting-tag-permissions)
   * 仅适用于社区成员（封闭社区）

      * 允许对的读取权限 [社区站点的成员组](users.md#publish-group-roles)
   * 对于任何网站访客，无论是登录还是匿名（开放社区）

      * 允许对的读取权限 `Everyone` 群组
   * [发布标记](../../help/sites-administering/tags.md#publishing-tags)



* [定义社区站点的标记范围](sites-console.md#tagging)

   * [配置存在于站点结构中的目录](functions.md#catalog-function)

      * 可以将标记添加到目录实例，以控制UI筛选器中提供的标记列表。
      * 可以添加 [预过滤器](catalog-developer-essentials.md#pre-filters)，以限制目录中包含的资源。

* [发布社区站点](sites-console.md#publishing-the-site)
* [将标记应用于启用资源](resources.md#create-a-resource) 所以它们可以被绝对地过滤
* [发布启用资源](resources.md#publish)

## 社区站点标记 {#community-site-tags}

创建或编辑社区站点时， [标记设置](sites-console.md#tagging) 通过选择现有标记命名空间的子集来设置可用于站点功能的标记范围。

虽然可以随时创建标记并将其添加到社区站点，但建议预先设计分类，类似于设计数据库。 参见 [使用标记](../../help/sites-authoring/tags.md).

以后将标记添加到现有社区站点时，必须先保存编辑，然后才能将新标记添加到站点结构中的目录函数。

对于社区站点，在站点发布和标记发布后，必须启用对社区成员的读取权限。 参见 [设置标记权限](../../help/sites-administering/tags.md#setting-tag-permissions).

下面是管理员将读取权限应用于 `/etc/tags/ski-catalog` 对于组 `Community Enable Members`.

![网站标记](assets/site-tags.png)

## 目录标记命名空间 {#catalog-tag-namespaces}

目录功能使用标记来定义自身。 在社区站点中配置目录功能时，为社区站点设置的标记命名空间范围定义了要从中进行选择的标记命名空间集。

“目录”功能包括标记设置，该设置定义了目录的过滤器UI中列出的标记。 “所有命名空间”设置是指为社区站点选择的标记命名空间的范围。

![catalog-namespace](assets/catalog-namespace.png)

## 将标记应用于启用资源 {#applying-tags-to-enablement-resources}

启用资源和学习路径将显示在所有目录中，当 `Show in Catalog` 已选中。 将标记添加到资源和学习路径后，可以预先筛选到特定目录中，并在目录UI中进行筛选。

通过将启用资源和学习路径限制到特定目录，可通过创建 [预过滤器](catalog-developer-essentials.md#pre-filters).

目录UI允许访客将标记过滤器应用于该目录中显示的资源和学习路径列表。

将标记应用于启用资源的管理员必须了解与目录关联的标记命名空间以及分类，以便选择子标记以进行更精细的分类。

例如，如果 `ski-catalog` 在名为的目录中创建和设置命名空间 `Ski Catalog`，它可能会有两个子标记： `lesson-1` 和 `lesson-2`.

因此，任何标有以下一项的启用资源：

* ski-catalog：leasue-1
* ski-catalog：leasue-2

将显示在 `Ski Catalog` 在启用资源发布之后。

![basic-info](assets/applytags-basicinfo.png)

## 在发布时查看目录 {#viewing-catalog-on-publish}

在创作环境中设置并发布所有内容后，即可在发布环境中体验使用目录查找支持资源的体验。

如果下拉列表中未显示标记命名空间，请确保已在发布环境中正确设置权限。

如果添加了标记命名空间但缺少标记命名空间，请确保已重新发布标记和网站。

如果在查看目录时选择标记后未显示任何启用资源，请确保将来自目录命名空间的标记应用于启用资源。

![view-catalog](assets/viewcatalog.png)
