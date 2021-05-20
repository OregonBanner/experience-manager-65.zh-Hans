---
title: 创建文章导出配置
seo-title: 创建文章导出配置
description: 可查看本页以了解有关将内容从Adobe Experience Manager(AEM)导出以上传到AEM Mobile的信息。
seo-description: 可查看本页以了解有关将内容从Adobe Experience Manager(AEM)导出以上传到AEM Mobile的信息。
uuid: 089bc15b-669e-4623-bdbb-fd9abf46e098
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: bc681589-5d46-44cd-888d-b0722a2fd006
exl-id: 5295f383-3b46-4456-9177-65de68e39a85
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# 创建文章导出配置{#creating-article-export-configuration}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

>[!CAUTION]
>
>**先决条件**:
>
>要了解有关创建和修改共享资源的信息，请参阅[内容同步](/help/mobile/mobile-ondemand-contentsync.md)以了解基本概念。

AEM Mobile用户使用“内容同步”将实时内容导出为静态内容以供在移动设备应用程序中使用，当内容从AEM Mobile上传到Mobile On-Demand Services时，会执行此导出。

上表中提到的属性&#x200B;***dps-exportTemplate***&#x200B;定义应用程序导出配置的路径。 设置此属性可创建和修改共享资源。

以下资源介绍如何将内容从Adobe Experience Manager(AEM)导出以上传到AEM Mobile。

文章包含需要导出和上传的内容。 其中某些内容可以在文章之间共享。

使用[ContentSync](/help/mobile/mobile-ondemand-contentsync.md)将内容收集到一起并创建一个&#x200B;***共享资源***&#x200B;包。

应将&#x200B;**&lt;dps-exportTemplate>/dps-article>**&#x200B;中找到的ContentSync配置配置为导出设备上属性静态渲染所需的所有内容和文章。

>[!CAUTION]
>
>仅当您具有以下权限时，才可以执行以下步骤来查看示例共享资源：
>
>* 安装了示例内容
>* 运行AEM实例
>* 未配置自定义上下文或其他端口

>



要查看共享资源示例，请参阅以下步骤：

1. 在AEM服务器上打开CRXDE Lite。
1. 浏览此路径[/etc/contentsync/templates/dps-we-unlimited-app/dps-article](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-article)，以查看共享资源示例。

   您可以查看创建共享资源所需的所有属性，如下图所示：

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>当文章内容发生更改时，应将文章上传或导出到AEM Mobile On-demand Services。
