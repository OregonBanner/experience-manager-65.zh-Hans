---
title: 删除Geometrixx站点
seo-title: 删除Geometrixx站点
description: 了解如何删除示例Geometrixx内容。
seo-description: 了解如何删除示例Geometrixx内容。
uuid: 07d20837-3375-4e64-bb07-3e4d10452335
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 56761a36-ce21-46e1-856f-75a7e94acae9
translation-type: tm+mt
source-git-commit: 1f7a45adc73b407c402a51b061632e72d97ca306

---


# 删除Geometrixx站点{#removing-the-geometrixx-sites}

AEM附带一组Geometrixx示例网站。 您可以通过包管理器删除此示 **例内容**。

与geometrixx相关的单个包包括：

* `cq-geometrixx-outdoors-ugc-pkg-<version>.zip`
* `cq-geometrixx-pkg-<version>.zip`
* `cq-content-mac-<version>.zip`
* `cq-geometrixx-login-pkg-<version>.zip`
* `cq-geometrixx-users-pkg-<version>.zip`
* `cq-geometrixx-workflow-pkg-<version>.zip`
* `cq-geometrixx-outdoors-pkg-<version>.zip`
* `cq-geometrixx-commons-pkg-<version>.zip`
* `cq-geometrixx-media-pkg-<version>.zip`

要删除单个包，只需单击该包上 **的** “卸载”。

还有一个超级包：

* `cq-geometrixx-all-pkg-5.6.12.zip`

此包包括上述所有单个包。 要同时删除所有与geometrixx相关的内容，请单击此包 **上的** “卸载”。 超级包将进入卸载状态，并且所有单个包都将从包管理器视图中消失。

您现在有一个“空”AEM实例，没有任何演示站点。

>[!NOTE]
>
>升级时，geometrixx站点将自动重新安装。 如果不需要这些示例，您可能需要在升级后删除geometrixx网站。

