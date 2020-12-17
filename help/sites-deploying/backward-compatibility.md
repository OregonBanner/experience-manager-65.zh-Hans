---
title: AEM 6.5中的向后兼容性
seo-title: AEM 6.5中的向后兼容性
description: 了解如何使您的应用程序和配置与AEM 6.5兼容
seo-description: 了解如何使您的应用程序和配置与AEM 6.5兼容
uuid: 81dc2771-f59b-4b24-8932-9e938cba05e0
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: f3b4ec1d-9054-47d4-afcb-0a0121b94190
docset: aem65
translation-type: tm+mt
source-git-commit: 303841896717448947aa48ece7ae86519a5450d5
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---


# AEM 6.5{#backward-compatibility-in-aem}中的向后兼容性

## 概述 {#overview}

>[!NOTE]
>
>有关不在兼容性包范围内的列表内容和配置更改，请参见AEM](/help/sites-deploying/repository-restructuring.md)中的[存储库重组。

在AEM 6.5中，所有功能都是在开发时考虑到向后兼容性的。

在大多数情况下，运行AEM 6.3的客户在进行升级时不必更改代码或自定义。 对于AEM 6.1和6.2客户，没有比升级到6.3时更多的中断更改。

对于无法保持向后兼容的功能的例外，可通过安装6.4版兼容性包来缓解捆绑套件和内容的向后不兼容问题（有关下载位置的详细信息，请参阅下面的设置）。 在大多数情况下，此组件包有助于恢复符合AEM 6.4规范的应用程序的兼容性。

兼容性包允许您在兼容模式下运行AEM，并根据新的AEM功能推迟自定义开发：

>[!NOTE]
>
>请注意，兼容性软件包只是一个临时解决方案，可推迟AEM 6.5兼容性所需的开发，如果升级后无法立即通过开发解决兼容性问题，则建议将其作为最后一个选项。 强烈建议在您决定继续基于6.5的自定义开发并使用完整的6.5功能后，切换到本机模式并卸载兼容包。

![酶](assets/sase.png)

兼容性包有两种模式：**已启用路由**&#x200B;和&#x200B;**已禁用路由**。

这允许AEM 6.5以三种模式运行：

**本机模式：**

本机模式适用于希望使用AEM 6.5的所有新增功能并准备进行一些开发以使其自定义功能与所有新增功能一起使用的客户。

这意味着您可能需要在升级后立即调整应用程序。

**兼容性模式：已安装兼容包且已启用路由**

兼容性模式适用于具有自定义的不向后兼容的界面的客户。 这允许AEM以兼容模式运行，并推迟针对与某些自定义代码不兼容的新AEM功能所需的自定义开发。

**旧模式：已安装兼容包且禁用路由**

传统模式适用于具有基于AEM的旧代码或已弃用代码的自定义界面的客户，该代码已在兼容性包中移出。

![萨普特](assets/sapte.png)

## 如何设置 {#how-to-set-up}

AEM 6.3兼容性包可以使用包管理器作为包进行安装。 您可以从软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/compatpack/aem-compat-cq64-to-cq63)站点下载[AEM 6.3兼容性包。

安装兼容性包后，可以使用OSGI配置中的交换机启用或禁用路由，如下所示：

![screen_shot_2017-11-27at122421pm](assets/screen_shot_2017-11-27at122421pm.png)

安装并设置兼容性包后，将根据已选择的兼容性模式使用这些功能。
