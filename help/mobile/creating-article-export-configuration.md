---
title: 创建文章导出配置
description: 请参阅此页面，了解如何从Adobe Experience Manager (AEM)导出内容以供上传到AEM Mobile。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 5295f383-3b46-4456-9177-65de68e39a85
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# 创建文章导出配置{#creating-article-export-configuration}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md)。

>[!CAUTION]
>
>**先决条件**：
>
>要了解有关创建和修改共享资源的信息，请参阅 [内容同步](/help/mobile/mobile-ondemand-contentsync.md) 了解基本概念。

AEM Mobile用户使用Content Sync将实时内容导出到静态内容以供在移动设备应用程序中使用，当内容从AEM Mobile上传到Mobile On-Demand Services时，会发生此导出。

属性 ***dps-exportTemplate*** 在上表中提到，可定义应用程序导出配置的路径。 设置此属性以创建和修改共享资源。

以下资源介绍了如何从Adobe Experience Manager (AEM)导出内容以供上传到AEM Mobile。

文章包含需要导出和上传的内容。 这些内容中的一部分可在文章之间共享。

使用 [ContentSync](/help/mobile/mobile-ondemand-contentsync.md) 将内容收集在一起并创建 ***共享资源*** 包。

ContentSync配置位于 **&lt;dps-exporttemplate>/dps-article>** 应配置为导出设备上属性静态呈现所需的文章中的所有内容。

>[!CAUTION]
>
>只有在具备以下条件时，您才可以执行以下步骤来查看共享资源的示例：
>
>* 已安装示例内容
>* 运行AEM实例
>* 没有已配置的自定义上下文或其他端口
>

要查看共享资源的示例，请参阅以下步骤：

1. 在AEM服务器上打开CRXDE Lite。
1. 浏览到此路径 [/etc/contentsync/templates/dps-we-unlimited-app/dps-article](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-article)，以查看示例共享资源。

   您可以查看创建共享资源所需的所有属性，如下图所示：

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>当文章内容发生变化时，应将文章上传或导出到AEM Mobile On-demand Services。
