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
role: Admin
exl-id: ce58c8e9-8b4a-43fb-a108-ed2ac40268c7
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---

# 标记支持资源 {#tagging-enablement-resources}

## 概述 {#overview}

标记启用资源允许在成员浏览[目录](functions.md#catalog-function)时筛选资源和学习路径。

基本上：

* [为每个目录创](../../help/sites-administering/tags.md#creating-a-namespace) 建标记名称包

   * [设置标记权限](../../help/sites-administering/tags.md#setting-tag-permissions)
   * 仅适用于社区成员（封闭社区）

      * 允许对[社区站点成员组](users.md#publish-group-roles)进行读取访问
   * 对于任何网站访客，无论是登录还是匿名（开放社区）

      * 允许对`Everyone`组进行读取访问
   * [发布标记](../../help/sites-administering/tags.md#publishing-tags)



* [定义社区网站的标记范围](sites-console.md#tagging)

   * [配置网站结构中存在的目录](functions.md#catalog-function)

      * 可以向目录实例添加标记，以控制UI过滤器中显示的标记列表。
      * 可以添加[pre-filters](catalog-developer-essentials.md#pre-filters)，以限制目录所包含的资源。

* [发布社区站点](sites-console.md#publishing-the-site)
* [将标记应用于启用](resources.md#create-a-resource) 资源，以便可以明确过滤它们
* [发布支持资源](resources.md#publish)

## 社区站点标记 {#community-site-tags}

创建或编辑社区站点时，[标记设置](sites-console.md#tagging)通过选择现有标记命名空间的子集来设置可用于站点功能的标记范围。

虽然可以随时创建标记并将其添加到社区站点，但建议事先设计分类，类似于设计数据库。 请参阅[使用标记](../../help/sites-authoring/tags.md)。

稍后向现有社区网站添加标记时，必须先保存编辑，然后才能将新标记添加到网站结构中的目录函数。

对于社区网站，在发布网站和发布标记后，必须启用对社区成员的读取访问权限。 请参阅[设置标记权限](../../help/sites-administering/tags.md#setting-tag-permissions)。

以下是管理员对组`Community Enable Members`的`/etc/tags/ski-catalog`应用读取权限时CRXDE中显示的方式。

![网站标签](assets/site-tags.png)

## 目录标记命名空间 {#catalog-tag-namespaces}

目录功能使用标记来定义自身。 在社区站点中配置目录函数时，要从中选择的标记命名空间集由社区站点设置的标记命名空间范围定义。

“目录”函数包含一个标记设置，用于定义目录的过滤器UI中列出的标记。 “所有命名空间”设置是指为社区站点选择的标记命名空间的范围。

![catalog-namespace](assets/catalog-namespace.png)

## 将标记应用到启用资源 {#applying-tags-to-enablement-resources}

选中`Show in Catalog`后，启用资源和学习路径将显示在所有目录中。 向资源和学习路径添加标记后，可以预过滤到特定目录，以及在目录UI中进行过滤。

通过创建[pre-filters](catalog-developer-essentials.md#pre-filters)，可以限制特定目录的启用资源和学习路径。

目录UI允许访客将标记过滤器应用到该目录中显示的资源和学习路径列表。

将标记应用到启用资源的管理员必须了解与目录关联的标记命名空间以及分类，才能选择子标记以进行更细化的分类。

例如，如果在名为`Ski Catalog`的目录中创建并设置了`ski-catalog`命名空间，则该命名空间可能有两个子标记：`lesson-1`和`lesson-2`。

因此，使用以下任一项标记的任何启用资源：

* ski-catalog:lesson-1
* ski-catalog:lesson-2

在发布启用资源后，将显示在`Ski Catalog`中。

![基本信息](assets/applytags-basicinfo.png)

## 在发布时查看目录 {#viewing-catalog-on-publish}

从创作环境中设置并发布所有内容后，便可以在发布环境中体验使用目录查找支持资源的体验。

如果下拉列表中未显示标记命名空间，请确保在发布环境中正确设置了权限。

如果添加了标记命名空间且缺少标记，请确保重新发布了标记和网站。

如果在查看目录时选择标记后未显示任何启用资源，请确保目录的命名空间中有一个标记已应用于启用资源。

![view-catalog](assets/viewcatalog.png)
