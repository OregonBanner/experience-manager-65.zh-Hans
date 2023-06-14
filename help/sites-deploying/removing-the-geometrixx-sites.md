---
title: 删除Geometrixx站点
description: 了解如何删除示例Geometrixx内容。
uuid: 07d20837-3375-4e64-bb07-3e4d10452335
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 56761a36-ce21-46e1-856f-75a7e94acae9
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
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

还有一个超级套餐：

* `cq-geometrixx-all-pkg-5.6.12.zip`

此包包含上述所有单个包。 要一次删除所有与geometrixx相关的内容，请单击 **卸载** 在此包上。 超级包将进入“未安装”状态，并且所有单个包都将从“包管理器”视图中消失。

现在，您有一个“空”AEM实例，没有任何演示站点。

>[!NOTE]
>
>升级时，会自动重新安装Geometrixx站点。 如果您不需要这些示例，请在升级后删除Geometrixx网站。

