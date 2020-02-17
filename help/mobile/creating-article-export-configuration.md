---
title: 创建文章导出配置
seo-title: 创建文章导出配置
description: 可查看本页以了解如何从Adobe Experience Manager(AEM)导出内容以上传到AEM Mobile。
seo-description: 可查看本页以了解如何从Adobe Experience Manager(AEM)导出内容以上传到AEM Mobile。
uuid: 089bc15b-669e-4623-bdbb-fd9abf46e098
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: bc681589-5d46-44cd-888d-b0722a2fd006
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 创建文章导出配置{#creating-article-export-configuration}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>**入门项目**:
>
>要了解有关创建和修改共享资源的信息，请参 [阅内容同步](/help/mobile/mobile-ondemand-contentsync.md) ，了解基本概念。

AEM mobile用户使用内容同步将活动内容导出为静态内容以在Mobile Apps中使用，当内容从AEM Mobile上传到Mobile On-Demand Services时，将发生此导出。

上表 ***中提到的dps-exportTemplate*** ，属性定义应用程序导出配置的路径。 设置此属性可创建和修改共享资源。

以下资源介绍了如何从Adobe Experience Manager(AEM)导出内容以上传到AEM Mobile。

文章包含需要导出和上传的内容。 其中某些内容可在文章之间共享。

使 [用ContentSync](/help/mobile/mobile-ondemand-contentsync.md) 收集内容并创建共 ***享资源包*** 。

位于 **** &lt;dps-exportTemplate>/dps-article>的ContentSync配置应配置为导出设备上属性静态渲染所需的所有内容和文章。

>[!CAUTION]
>
>只有在具有以下各项时，您才可以执行以下步骤来查看示例共享资源：
>
>* 已安装示例内容
>* 运行AEM实例
>* 未配置自定义上下文或其他端口
>



要查看示例共享资源，请参阅以下步骤：

1. 在AEM服务器上打开CRXDE Lite。
1. 浏览至此路 [径/etc/contentsync/templates/dps-we-unlimited-app/dps-article](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-article)，查看示例共享资源。

   您可以查看创建共享资源所需的所有属性，如下图所示：

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>当文章内容发生更改时，应将文章上传或导出到AEM Mobile On-Demand Services。

