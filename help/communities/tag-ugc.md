---
title: 标记用户生成的内容
seo-title: 标记用户生成的内容
description: 标记用户生成的内容(UGC)是社区成员如何帮助其他成员搜索内容
seo-description: 标记用户生成的内容(UGC)是社区成员如何帮助其他成员搜索内容
uuid: ce125d7c-6fc1-44c7-9f67-eca6f599d8e3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 1cc8ce66-2c03-44e4-9ddd-8d6944d85c99
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 标记用户生成的内容 {#tagging-user-generated-content}

## 概述 {#overview}

标记用户生成的内容(UGC)是社区成员帮助其他成员搜索内容的方式。

通常，创作环境中的作者和管理员会应用标记。 标记UGC的独特之处在于UGC标记由发布环境中的社区成员应用。

这两个应用程序的标记命名空间和分类相同。

## 社区功能 {#communities-features}

可以配置为允许标记的AEM Communities功能包括

* [博客](blog-feature.md)
* [日历](calendar.md)
* [文件库](file-library.md)
* [论坛](forum.md#configuretheaddedforum)
* [问题与解答](working-with-qna.md)

## 管理标记 {#administering-tags}

请参 [阅管理标记](../../help/sites-administering/tags.md#tagging-console) ，以创建和管理标记命名空间和分类。

有关开 [发人员信息](tag.md) ，请参阅Tag Essentials。

请参 [阅使用社交标记云](tagcloud.md) ，以便将社交标记云组件添加到页面，以便于使用应用的标记搜索已发布的UGC。

### 标记权限 {#tag-permissions}

默认权限设置为不允许发布环境中的每个人都读取标记命名空间。

由于标签在发布环境中应用于UGC，因此需要为社区成员启用读取权限，以便他们能够选择要应用的标签。

请参阅 [设置标记权限](../../help/sites-administering/tags.md#setting-tag-permissions)。

以下是管理员对组应用读取权限时CRXDE中显示 `/etc/tag/discussions` 的方式 `*Community Engage Members*`。

![chlimage_1-74](assets/chlimage_1-74.png)

