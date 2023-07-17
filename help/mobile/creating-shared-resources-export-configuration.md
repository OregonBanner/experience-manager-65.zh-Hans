---
title: 创建共享资源导出配置
description: 请按照本页面了解如何从Adobe Experience Manager (AEM)导出共享资源以上传到AEM Mobile。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 576b4567-c7b6-4196-84e7-47e980637540
source-git-commit: 96e2e945012046e6eac878389b7332985221204e
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 1%

---

# 创建共享资源导出配置{#creating-shared-resources-export-configuration}

>[!NOTE]
>
>对于需要基于单页应用程序框架的客户端渲染（例如React）的项目，Adobe建议使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>**先决条件**:
>
>在了解如何创建和修改共享资源之前，请参阅 [内容同步](/help/mobile/mobile-ondemand-contentsync.md) 了解基本概念。

Adobe Experience Manager (AEM) Mobile用户使用Content Sync将实时内容导出到静态内容，以便在移动设备应用程序中使用，当内容从AEM Mobile上传到Mobile On-Demand Services时，会发生此导出。

属性 ***dps-exportTemplate*** 在上表中提到，可定义应用程序导出配置的路径。 设置此属性以创建和修改共享资源。

以下资源介绍了如何从AEM导出共享资源以上传到AEM Mobile。

共享的HTML资源允许文章共享原本会复制到所有文章的HTML资源，并且可以包括图标、字体、JavaScript和css。

内容同步配置位于 **&lt;dps-exporttemplate>/dps-HTMLResources>** 应配置为导出设备上属性静态渲染所需的文章中的所有内容。

>[!CAUTION]
>
>只有在具备以下条件时，您才可以执行以下步骤查看共享资源的示例：
>
>* 已安装示例内容
>* 运行AEM实例
>* 没有已配置的自定义上下文或其他端口
>

要查看共享资源示例，请参阅以下步骤：

1. 在AEM服务器上打开CRXDE Lite。
1. 浏览到此路径 *[/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources)*，以查看示例共享资源。

   您可以查看创建共享资源所需的所有属性，如下图所示：

   ![chlimage_1-145](assets/chlimage_1-145.png)

>[!NOTE]
>
>当任何共享资源发生更改时，应将共享资源上传或导出到AEM Mobile On-demand Services。
