---
title: 云配置
seo-title: 云配置
description: 将点播应用程序与云配置关联允许Adobe Experience Manager(AEM)通过建立双向链接直接与移动点播托管项目进行通信。 可查看本页以了解更多信息。
seo-description: 将点播应用程序与云配置关联允许Adobe Experience Manager(AEM)通过建立双向链接直接与移动点播托管项目进行通信。 可查看本页以了解更多信息。
uuid: f377f2af-864b-43df-9d42-4a5fd6cd70d5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: d0d29b99-53d4-4b0d-947b-39d91b381de7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 2%

---


# 云配置{#cloud-configuration}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

将点播应用程序与云配置关联允许Adobe Experience Manager(AEM)通过建立双向链接直接与移动点播托管项目进行通信。 通过将您的应用程序链接到移动点播项目，您将能够在AEM中创建内容（如文章、横幅和集合），同时将该内容提供给移动点播。

从那里，发布、预览和管理内容变得可能。 您还可以将现有的Mobile On-Demand内容导入AEM并执行内容编辑。

## 设置云配置{#setting-up-cloud-configuration}

>[!CAUTION]
>
>在开始为On-Demand应用程序配置云配置之前，您必须熟悉AEM Mobile配置和配置AEM Mobile On-demand Services客户端。
>
>有关详细信息，请参阅管理部分中的[设置AEM Mobile On-demand Services](/help/mobile/aem-mobile-setup.md)。

要配置Mobile On-DemandCloud Services，请单击应用程序仪表板中&#x200B;**管理连接**&#x200B;拼贴右上角的顶齿轮。

您应熟悉应用程序仪表板和可用拼贴。 有关详细信息，请参阅[AEM Mobile应用程序仪表板](/help/mobile/mobile-apps-ondemand-application-dashboard.md)。

### 设置指向云配置的链接{#setting-up-link-to-cloud-configuration}

>[!CAUTION]
>
>确保您拥有现有的点播客户端和云配置。
>
>有关详细信息，请参阅管理部分中的[设置AEM Mobile On-demand Services](/help/mobile/aem-mobile-setup.md)。

以下步骤介绍了如何设置指向云配置的链接：

1. 从&#x200B;**Mobile**&#x200B;中，选择&#x200B;**Apps**，然后从目录中选择您的Mobile On-Demand应用程序。
1. 单击&#x200B;**管理连接**&#x200B;拼贴上的齿轮图标。

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 输入已有的配置或通过输入&#x200B;**配置标题**、**设备Id**&#x200B;和&#x200B;**设备令牌**&#x200B;创建新配置。

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. 验证&#x200B;**设备Id**&#x200B;和&#x200B;**设备令牌**&#x200B;后，从列表中选择您的点播项目。

   单击&#x200B;**提交**。

   ![chlimage_1-67](assets/chlimage_1-67.png)

   **管理连接**&#x200B;拼贴显示您的云配置。

   ![chlimage_1-68](assets/chlimage_1-68.png)

   >[!CAUTION]
   >
   >如果您尝试更改此应用程序与哪个项目关联，则在仪表板中切换项目时，您将收到有关内容完整性问题的警告，如下图所示：

   ![chlimage_1-69](assets/chlimage_1-69.png)

### 后续步骤 {#the-next-steps}

为应用程序配置云配置后，请参阅以下内容管理资源：

* [管理文章](/help/mobile/mobile-on-demand-managing-articles.md)
* [管理横幅](/help/mobile/mobile-on-demand-managing-banners.md)
* [管理收藏集](/help/mobile/mobile-on-demand-managing-collections.md)
* [上传共享资源](/help/mobile/mobile-on-demand-shared-resources.md)
* [发布／取消发布内容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [使用预检预览](/help/mobile/aem-mobile-manage-ondemand-services.md)
