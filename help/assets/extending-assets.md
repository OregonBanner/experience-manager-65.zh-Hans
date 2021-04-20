---
title: 自定义和扩展 [!DNL Assets]
description: 了解如何自定义和扩展资产共享和资产编辑器，它们为用户提供了专门定制的界面和功能集。
contentOwner: AG
role: Developer
feature: Developer Tools
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 1%

---


# 自定义和扩展[!DNL Assets] {#customizing-and-extending-assets}

资产编辑器是Adobe Enterprise Manager网站的用户用来查找、视图和操作存储库中的数字资产的主要访问点。

作为[!DNL Experience Manager]开发人员，您可以通过多种方式自定义和扩展资产编辑器，为用户提供专门定制的界面和功能集。

可以自定义或增强功能的以下方面：

* [扩展资产编辑器](asseteditorx.md)
* [扩展资产搜索](searchx.md)
* [使用媒体处理程序和工作流处理资源](media-handlers.md)
* [将资产与活动流集成](extending-activity-stream.md)
* [资产代理开发](proxy.md)
* [配置ImageMagick的最佳实践](best-practices-for-imagemagick.md)

## 自定义外观{#customizing-the-look-and-feel}

资产编辑器外观的以下方面可自定义：

* 徽标：您可以将您自己组织的徽标添加到界面中。
* 颜色和字体：您可以更改界面中使用的颜色和字体。
* HTML代码：要进行更彻底的自定义，您可以更改定义界面的底层HTML代码。

## 自定义演绎版{#customizing-renditions}

在[!DNL Experience Manager Assets]术语中，演绎版是资产在其中呈现的形式。 通常，特定资产可能具有多个演绎版。 例如，全彩色图像可能具有一个原始大小的再现，另一个以缩小大小，另一个以缩小大小缩放并转换为灰度。

特定资产可用的演绎版可以进行自定义，也可以创建新的演绎版。
