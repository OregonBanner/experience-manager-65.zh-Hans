---
title: 标记支持资源
seo-title: 标记支持资源
description: 通过标记支持资源，可在成员浏览目录时筛选资源和学习路径
seo-description: 通过标记支持资源，可在成员浏览目录时筛选资源和学习路径
uuid: daf8a4f4-486b-498c-99e9-d1533a830e64
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: c012d639-c6e6-4f73-bbd8-78a4baa38c17
translation-type: tm+mt
source-git-commit: fa01c9fad82adb021220631a0536ab77ceb01e31

---


# 标记支持资源 {#tagging-enablement-resources}

## 概述 {#overview}

通过标记支持资源，可在成员浏览目录时筛选资源和学习 [路径](functions.md#catalog-function)。

本质上：

* [为每个目录创建标记命名空间](../../help/sites-administering/tags.md#creating-a-namespace) 。

   * [设置标记权限](../../help/sites-administering/tags.md#setting-tag-permissions)
   * 仅限社区成员（封闭社区）

      * 允许对社区站点 [的成员组进行读取访问](users.md#publish-group-roles)
   * 对于任何站点访客，无论是登录还是匿名（开放社区）

      * 允许对组进行读取访 `Everyone` 问
   * [发布标记](../../help/sites-administering/tags.md#publishing-tags)



* [定义社区站点的标记范围](sites-console.md#tagging)

   * [配置站点结构中存在的目录](functions.md#catalog-function)

      * 可以向目录实例添加标记以控制UI过滤器中显示的标记的列表。
      * 可以添 [加预过滤器](catalog-developer-essentials.md#pre-filters)，以限制目录的包含资源。

* [发布社区站点](sites-console.md#publishing-the-site)
* [将标记应用于支持资源](resources.md#create-a-resource) ，以便可以明确筛选标记
* [发布支持资源](resources.md#publish)

## 社区站点标记 {#community-site-tags}

在创建或编辑社区站点时，“ [Tagging](sites-console.md#tagging) ”设置通过选择现有标记命名空间的子集来设置可用于站点功能的标记的范围。

虽然可以随时创建标记并将其添加到社区站点，但建议事先设计分类，这与设计数据库类似。 请参阅 [使用标记](../../help/sites-authoring/tags.md)。

以后向现有社区站点添加标记时，必须先保存编辑，然后才能将新标记添加到站点结构中的目录功能。

对于社区站点，在发布站点和发布标记后，必须启用对社区成员的读取访问。 请参阅 [设置标记权限](../../help/sites-administering/tags.md#setting-tag-permissions)。

以下是管理员对组应用读取权限时CRXDE中显示 `/etc/tags/ski-catalog` 的方式 `Community Enable Members`。

![chlimage_1-420](assets/chlimage_1-420.png)

## 目录标记命名空间 {#catalog-tag-namespaces}

目录功能使用标记来定义自身。 在社区站点中配置目录功能时，要选择的标签命名空间集由社区站点的标签空间集的范围定义。

“目录”功能包括一个标记设置，该设置定义了目录的过滤器UI中列出的标记。 设置“所有命名空间”是指为社区站点选择的标记命名空间的范围。

![chlimage_1-421](assets/chlimage_1-421.png)

## 将标记应用于Enablement Resources {#applying-tags-to-enablement-resources}

选中此项后，启用资源和学习路径将显示在所有 `Show in Catalog` 目录中。 向资源和学习路径添加标记后，可以预过滤到特定目录中以及在目录UI中过滤。

通过创建预过滤器，可以限制启用资源和特定目录的学 [习路径](catalog-developer-essentials.md#pre-filters)。

目录UI允许访客将标签过滤器应用于该目录中显示的资源和学习路径的列表。

将标记应用到启用资源的管理员必须了解与目录关联的标记命名空间以及分类，以便选择子标记以进行更精细的分类。

例如，如果创建了 `ski-catalog` 命名空间并在名为的目录上进行了设置 `Ski Catalog`，则它可能有两个子标记： `lesson-1` 和 `lesson-2`。

因此，使用以下任一项标记的任何支持资源

* ski-catalog:lesson-1
* ski-catalog:lesson-2

将在启用 `Ski Catalog` 资源发布后显示在中。

![chlimage_1-422](assets/chlimage_1-422.png)

## 在发布时查看目录 {#viewing-catalog-on-publish}

在从创作环境中设置并发布所有内容后，可以在发布环境中体验使用目录查找支持资源的体验。

如果下拉列表中未显示标记命名空间，请确保在发布环境中正确设置了权限。

如果添加了标记命名空间且该标记缺失，请确保标记和站点已重新发布。

如果在查看目录时选择标记后未显示启用资源，请确保目录的命名空间中有一个标记应用于启用资源。

![chlimage_1-423](assets/chlimage_1-423.png)

