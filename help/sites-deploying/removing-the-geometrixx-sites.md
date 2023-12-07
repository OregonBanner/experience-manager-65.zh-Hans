---
title: 删除Geometrixx站点
description: 了解如何删除示例Geometrixx内容。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# 删除Geometrixx站点{#removing-the-geometrixx-sites}

AEM随附了一组示例Geometrixx网站。 您可以通过以下方式删除此示例内容 **包管理器**.

单独的geometrixx相关包包括：

* `cq-geometrixx-outdoors-ugc-pkg-<version>.zip`
* `cq-geometrixx-pkg-<version>.zip`
* `cq-content-mac-<version>.zip`
* `cq-geometrixx-login-pkg-<version>.zip`
* `cq-geometrixx-users-pkg-<version>.zip`
* `cq-geometrixx-workflow-pkg-<version>.zip`
* `cq-geometrixx-outdoors-pkg-<version>.zip`
* `cq-geometrixx-commons-pkg-<version>.zip`
* `cq-geometrixx-media-pkg-<version>.zip`

要删除单个包，只需单击 **卸载** 在那个包上。

还有一个超级包：

* `cq-geometrixx-all-pkg-5.6.12.zip`

此包包含上述所有单个包。 要一次删除所有与geometrixx相关的内容，请单击 **卸载** 在此包上。 超级包将进入未安装状态，并且所有单个包都将从“包管理器”视图中消失。

您现在拥有一个“空”AEM实例，没有任何演示站点。

>[!NOTE]
>
>升级时，会自动重新安装Geometrixx站点。 如果不需要这些示例，请在升级后删除Geometrixx网站。

