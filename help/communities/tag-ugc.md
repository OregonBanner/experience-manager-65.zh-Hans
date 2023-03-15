---
title: 标记用户生成的内容
seo-title: Tagging User Generated Content
description: 用户生成内容的标记(UGC)是社区成员帮助其他成员搜索内容的方式
seo-description: Tagging of user generated content (UGC) is how community members can help other members search for content
uuid: ce125d7c-6fc1-44c7-9f67-eca6f599d8e3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 1cc8ce66-2c03-44e4-9ddd-8d6944d85c99
role: Admin
exl-id: 1ecb41e5-c959-4380-a5c7-df9fc3a7703a
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 3%

---

# 标记用户生成的内容 {#tagging-user-generated-content}

## 概述 {#overview}

用户生成内容标记(UGC)是社区成员帮助其他成员搜索内容的一种方法。

通常，标记由作者和管理员在创作环境中应用。 标记UGC的独特之处在于UGC标记由发布环境中的社区成员应用。

这两个应用程序的标记命名空间和分类是相同的。

## Communities功能 {#communities-features}

可配置为允许标记的AEM Communities功能包括：

* [博客](blog-feature.md)
* [日程表](calendar.md)
* [文件库](file-library.md)
* [论坛](forum.md#configuretheaddedforum)
* [问题与解答](working-with-qna.md)

## 管理标记 {#administering-tags}

参见 [管理标记](../../help/sites-administering/tags.md#tagging-console) 用于创建和管理标记命名空间和分类。

参见 [Tag Essentials](tag.md) 了解开发人员信息。

参见 [使用社交标签云](tagcloud.md) ，以便将Social Tag Cloud组件添加到页面中，从而方便使用应用的标记搜索已发布的UGC。

### 标记权限 {#tag-permissions}

默认权限设置为不允许发布环境中的每个人都读取标记命名空间。

由于标记应用于发布环境中的UGC，因此需要为社区成员启用读取权限，以便他们能够选择要应用的标记。

参见 [设置标记权限](../../help/sites-administering/tags.md#setting-tag-permissions).

下面是管理员将读取权限应用于 `/etc/tag/discussions` 对于组 `Community Engage Members`.

![tag-permissions](assets/tag-permissions.png)
