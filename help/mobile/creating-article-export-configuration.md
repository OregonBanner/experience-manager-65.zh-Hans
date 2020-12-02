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
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---


# 创建文章导出配置{#creating-article-export-configuration}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>**先决条件**:
>
>要了解有关创建和修改共享资源的信息，请参阅[内容同步](/help/mobile/mobile-ondemand-contentsync.md)以了解基本概念。

AEM Mobile用户使用内容同步将实时内容导出为静态内容以用于移动应用程序，当内容从AEM Mobile上传到移动点播服务时，将发生此导出。

上表中提到的属性&#x200B;***dps-exportTemplate***&#x200B;定义应用程序导出配置的路径。 设置此属性可创建和修改共享资源。

以下资源介绍从Adobe Experience Manager(AEM)导出内容以上传到AEM Mobile。

文章包含需要导出和上传的内容。 其中一些内容可在文章之间共享。

使用[ContentSync](/help/mobile/mobile-ondemand-contentsync.md)将内容收集到一起并创建一个&#x200B;***共享资源***&#x200B;包。

**&lt;dps-exportTemplate>/dps-article>**&#x200B;的ContentSync配置应配置为导出设备上属性静态渲染所需的所有内容和文章。

>[!CAUTION]
>
>只有在具有以下各项时，您才能执行以下步骤来视图示例共享资源：
>
>* 已安装示例内容
>* 运行AEM实例
>* 未配置自定义上下文或其他端口

>



要视图示例共享资源，请参阅以下步骤：

1. 在AEM服务器上打开CRXDE Lite。
1. 浏览至此路径[/etc/contentsync/templates/dps-we-unlimited-app/dps-article](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-article),视图示例共享资源。

   您可以视图创建共享资源所需的所有属性，如下图所示：

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>当文章内容发生更改时，应将文章上传或导出到AEM Mobile On-demand Services。

