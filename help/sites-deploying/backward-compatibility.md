---
title: AEM 6.5中的向后兼容性
seo-title: Backward Compatibility in AEM 6.5
description: 了解如何使您的应用程序和配置与AEM 6.5兼容
seo-description: Learn how to keep your apps and configurations compatible with AEM 6.5
uuid: 81dc2771-f59b-4b24-8932-9e938cba05e0
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: f3b4ec1d-9054-47d4-afcb-0a0121b94190
docset: aem65
feature: Upgrading
exl-id: c432a014-2dab-4c49-a25b-e4f461d13f9b
source-git-commit: 50a11e30ccd720065962e8dd03cbcc71ec9f715a
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 1%

---

# Backward Compatibility in AEM 6.5{#backward-compatibility-in-aem}

## 概述 {#overview}

>[!NOTE]
>
>有关不在兼容包范围内的内容和配置更改列表，请参阅 [AEM中的存储库重组](/help/sites-deploying/repository-restructuring.md).

在AEM 6.5中，开发所有功能时都考虑到了向后兼容性。

在大多数情况下，运行AEM 6.3的客户在进行升级时，不应该更改代码或自定义设置。 对于AEM 6.1和6.2客户，没有比升级到6.3期间面临的其他重大更改。

对于无法保持向后兼容功能的例外情况，可通过安装适用于6.4的兼容包来缓解包和内容的向后不兼容问题（有关下载位置的详细信息，请参阅下面的设置）。 此复合包有助于在大多数情况下恢复与AEM 6.4兼容的应用程序的兼容性。

兼容包允许您在兼容模式下运行AEM，并根据新增的AEM功能推迟自定义开发：

>[!NOTE]
>
>请注意，兼容包只是一个临时解决方案，用于推迟兼容AEM 6.5所需的开发，仅当您在升级后无法立即通过开发解决兼容性问题时，才建议将其作为最后一个选项。 强烈建议在您决定继续基于6.5的自定义开发并使用完整的6.5功能后，切换到本机模式并卸载兼容包。

![sase](assets/sase.png)

兼容包有两种模式： **已启用路由** 和 **路由已禁用**.

这允许以三种模式运行AEM 6.5:

**本机模式：**

本机模式适用于那些希望使用AEM 6.5的所有新增功能，并且已准备好进行一些开发以使其自定义功能与所有新增功能配合使用的客户。

这意味着在升级后，您可能需要立即对应用程序进行调整。

**兼容性模式：安装了启用路由的兼容包**

兼容性模式适用于自定义了无法向后兼容的界面的客户。 这允许AEM在兼容模式下运行，并针对与某些自定义代码不兼容的新AEM功能推迟所需的自定义开发。

**旧版模式：安装了禁用路由的兼容包**

旧版模式适用于具有基于兼容性包中已移出的AEM中旧版或已弃用代码的自定义界面的客户。

![萨普特](assets/sapte.png)

## 如何设置 {#how-to-set-up}

的 **AEM 6.4适用于6.5的兼容包** 可以使用包管理器作为包安装。 您可以下载 [AEM 6.4 Software Distribution中适用于6.5的兼容包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=compat*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=20&amp;package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fcompatpack%2Faem-compat-cq65-to-cq64) 网站。

安装兼容包后，可以使用OSGI配置中的交换机启用或禁用路由，如下所示：

![比较交换机](assets/compat-switches.png)

安装并设置兼容包后，将根据所选的兼容模式来使用这些功能。
