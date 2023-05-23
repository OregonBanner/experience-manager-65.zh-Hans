---
title: 移除Geometrixx網站
seo-title: Removing the Geometrixx Sites
description: 瞭解如何移除範例Geometrixx內容。
seo-description: Learn how to remove the sample Geometrixx content.
uuid: 07d20837-3375-4e64-bb07-3e4d10452335
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 56761a36-ce21-46e1-856f-75a7e94acae9
source-git-commit: 1f7a45adc73b407c402a51b061632e72d97ca306
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---


# 移除Geometrixx網站{#removing-the-geometrixx-sites}

AEM隨附一組範例Geometrixx網站。 您可以透過以下方式移除此範例內容： **封裝管理員**.

個別geometrixx相關套件包括：

* `cq-geometrixx-outdoors-ugc-pkg-<version>.zip`
* `cq-geometrixx-pkg-<version>.zip`
* `cq-content-mac-<version>.zip`
* `cq-geometrixx-login-pkg-<version>.zip`
* `cq-geometrixx-users-pkg-<version>.zip`
* `cq-geometrixx-workflow-pkg-<version>.zip`
* `cq-geometrixx-outdoors-pkg-<version>.zip`
* `cq-geometrixx-commons-pkg-<version>.zip`
* `cq-geometrixx-media-pkg-<version>.zip`

若要移除個別套件，只要按一下 **解除安裝** 在該套件上。

此外，還有超級套件：

* `cq-geometrixx-all-pkg-5.6.12.zip`

此套件包含上述所有個別套件。 若要一次移除所有geometrixx相關內容，請按一下 **解除安裝** 在此封裝上。 超級套件會進入解除安裝狀態，而所有個別套件會從套件管理員檢視中消失。

您現在有「空白」AEM執行個體，沒有任何示範網站。

>[!NOTE]
>
>升級時，會自動重新安裝geometrixx網站。 如果您不想要這些範例，升級後可能需要移除geometrixx網站。

