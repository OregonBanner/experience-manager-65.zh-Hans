---
title: 云配置
seo-title: Cloud Configuration
description: 将按需应用程序关联到云配置可允许Adobe Experience Manager (AEM)通过建立双向链接直接与托管的Mobile On-Demand项目通信。 关注此页面以了解更多信息。
seo-description: Associating an On-Demand App to a Cloud Configuration allows Adobe Experience Manager (AEM) to communicate directly with a Mobile On-Demand hosted project by establishing a two way link. Follow this page to learn more.
uuid: f377f2af-864b-43df-9d42-4a5fd6cd70d5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: d0d29b99-53d4-4b0d-947b-39d91b381de7
exl-id: 37428543-c310-4712-a4ec-1f482579fb4b
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 2%

---

# 云配置{#cloud-configuration}

>[!NOTE]
>
>对于需要基于单页应用程序框架的客户端渲染（例如React）的项目，Adobe建议使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md).

将按需应用程序关联到云配置可允许Adobe Experience Manager (AEM)通过建立双向链接直接与托管的Mobile On-Demand项目通信。 通过将您的应用程序关联到Mobile On-Demand项目，您将能够在AEM中执行内容创建（例如文章、横幅和收藏集），但还可以将该内容提供给Mobile On-Demand。

从那里，可以发布、预览和管理内容。 您还可以将现有Mobile On-Demand内容导入AEM并执行内容编辑。

## 设置云配置 {#setting-up-cloud-configuration}

>[!CAUTION]
>
>在开始为On-Demand应用程序配置云配置之前，您必须熟悉AEM Mobile配置和配置AEM Mobile On-demand Services客户端。
>
>有关详细信息，请参阅 [设置AEM Mobile On-demand Services](/help/mobile/aem-mobile-setup.md) 在管理部分中。

要配置Mobile On-DemandCloud Services，请单击 **管理连接** 从应用程序仪表板中拼贴。

您应该熟悉应用程序功能板和可用的磁贴。 参见 [AEM Mobile应用程序功能板](/help/mobile/mobile-apps-ondemand-application-dashboard.md) 了解更多详细信息。

### 设置指向云配置的链接 {#setting-up-link-to-cloud-configuration}

>[!CAUTION]
>
>确保您具有现有的按需客户端和云配置。
>
>有关详细信息，请参阅 [设置AEM Mobile On-demand Services](/help/mobile/aem-mobile-setup.md) 在管理部分中。

以下步骤介绍了如何设置指向云配置的链接：

1. 起始日期 **移动设备**，选择 **应用程序** 以及目录中的Mobile On-Demand应用程序。
1. 单击 **管理连接** 图块。

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 输入现有配置，或通过输入 **配置标题**， **设备ID**、和 **设备令牌**.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. 一旦您的 **设备ID** 和 **设备令牌** 已验证，请从列表中选择您的按需项目。

   单击 **提交**.

   ![chlimage_1-67](assets/chlimage_1-67.png)

   此 **管理连接** 图块显示您的云配置。

   ![chlimage_1-68](assets/chlimage_1-68.png)

   >[!CAUTION]
   >
   >如果您尝试更改此应用程序与哪个项目相关联，则在仪表板中切换项目时，您将收到内容完整性问题警告，如下图所示：

   ![chlimage_1-69](assets/chlimage_1-69.png)

### 后续步骤 {#the-next-steps}

为应用程序配置云配置后，请参阅以下资源以管理内容：

* [管理文章](/help/mobile/mobile-on-demand-managing-articles.md)
* [管理横幅](/help/mobile/mobile-on-demand-managing-banners.md)
* [管理收藏集](/help/mobile/mobile-on-demand-managing-collections.md)
* [上传共享资源](/help/mobile/mobile-on-demand-shared-resources.md)
* [发布/取消发布内容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [使用Preflight预览](/help/mobile/aem-mobile-manage-ondemand-services.md)
