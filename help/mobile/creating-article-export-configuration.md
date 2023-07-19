---
title: 创建文章导出配置
seo-title: Creating Article Export Configuration
description: 请按照本页了解如何从Adobe Experience Manager (AEM)导出内容以供上传到AEM Mobile。
seo-description: Follow this page to learn about exporting content from Adobe Experience Manager (AEM) for upload to AEM Mobile.
uuid: 089bc15b-669e-4623-bdbb-fd9abf46e098
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: bc681589-5d46-44cd-888d-b0722a2fd006
exl-id: 5295f383-3b46-4456-9177-65de68e39a85
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 1%

---

# 创建文章导出配置{#creating-article-export-configuration}

>[!NOTE]
>
>对于需要基于单页应用程序框架的客户端渲染（例如React）的项目，Adobe建议使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>**先决条件**:
>
>要了解有关创建和修改共享资源的信息，请参阅 [内容同步](/help/mobile/mobile-ondemand-contentsync.md) 了解基本概念。

AEM Mobile用户使用Content Sync将实时内容导出到静态内容，以供在Mobile Apps中使用，当内容从AEM Mobile上传到Mobile On-Demand Services时，会发生此导出。

属性 ***dps-exportTemplate*** 在上表中提到，可定义应用程序导出配置的路径。 设置此属性以创建和修改共享资源。

以下资源介绍了如何从Adobe Experience Manager (AEM)导出内容以供上传到AEM Mobile。

文章包含需要导出和上传的内容。 某些内容可以在文章之间共享。

使用 [ContentSync](/help/mobile/mobile-ondemand-contentsync.md) 将内容收集在一起并创建 ***共享资源*** 包。

ContentSync配置位于 **&lt;dps-exporttemplate>/dps-article>** 应配置为导出设备上属性静态渲染所需的文章中的所有内容。

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
1. 浏览到此路径 [/etc/contentsync/templates/dps-we-unlimited-app/dps-article](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-article)，以查看示例共享资源。

   您可以查看创建共享资源所需的所有属性，如下图所示：

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>当文章内容发生更改时，应将文章上传或导出到AEM Mobile On-demand Services。
