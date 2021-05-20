---
title: AEM Mobile设置
seo-title: AEM Mobile设置
description: 请遵循本页设置AEM Mobile，从而允许用户在AEM中创建和管理内容。 本页提供了有关将AEM实例与基于云的AEM Mobile On-demand Services帐户和项目集成的信息。
seo-description: 请遵循本页设置AEM Mobile，从而允许用户在AEM中创建和管理内容。 本页提供了有关将AEM实例与基于云的AEM Mobile On-demand Services帐户和项目集成的信息。
uuid: 03bf5b56-7750-4f76-b079-43761367655a
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: 393cf504-917e-4bf6-9a8b-b7a5bd862c65
exl-id: 0ead982d-2315-4947-b762-596aa2aa42a1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 1%

---

# AEM Mobile SetUp{#aem-mobile-setup}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

>[!CAUTION]
>
>从AEM 6.2或6.3迁移到AEM 6.5的现有AEM Mobile应用程序客户可以通过从PackageShare](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/compatpack/aem-mobile-package)下载[包，继续使用AEM Mobile应用程序。 但是，新安装的AEM 6.5将不支持AEM Mobile应用程序功能。

要使用AEM为AEM Mobile应用程序生成内容，您必须将AEM实例与基于云的AEM Mobile On-demand Services帐户和项目相集成。

按照以下步骤设置AEM Mobile，从而允许用户在AEM中创建和管理内容。

## AEM Mobile配置{#aem-mobile-provisioning}

要开始设置AEM Mobile，您需要：

* **请求API密钥**:要访问On-Demand Services API，您需要请求API密钥。要请求API密钥，请填写[PDF表单](https://helpx.adobe.com/digital-publishing-solution/help/integrating-dps.html)。 将填写好的表单发送到Adobe开发人员支持：[wwds@adobe.com](mailto:wwds@adobe.com)

* **生成设备ID和设备令牌**:收到API密钥后，即可生成设备ID和设备令牌。转到[https://aex.aemmobile.adobe.com](https://aex.aemmobile.adobe.com/)并执行以下操作：

   * 提供API密钥
   * 使用您已添加到AEM Mobile项目的Adobe ID登录，并具有以下权限（请参阅以下创建项目的步骤）

      * 管理>管理项目和用户
      * 内容>添加和编辑内容、删除内容、查看内容、发布内容

如果满足所有条件，将生成设备ID和设备令牌。

>[!NOTE]
>
>需要的Adobe ID应授予对AEM Mobile项目的访问权限。 请参阅联机帮助中的[AEM Mobile的帐户管理](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) 。

## 为AEM Mobile创建项目{#creating-projects-for-aem-mobile}

在创建项目时，您可以为要定位的任何平台指定设置：iOS、Android、Windows和桌面Web查看器。 您指定的许多项目设置都会影响应用程序的行为。

创建项目需要使用具有主控管理员角色的Adobe ID登录到On-Demand Services门户。 编辑项目需要具有主控的管理员角色或具有&#x200B;**管理项目和用户**&#x200B;权限的用户角色。

>[!NOTE]
>
>要了解有关在AEM Mobile中创建项目的更多信息，请单击[此处](https://helpx.adobe.com/digital-publishing-solution/help/creating-projects.html)。

## 配置AEM Mobile连接器{#configuring-an-aem-mobile-connector}

AEM设置涉及以下连接器配置步骤。 完成AEM Mobile连接器配置后，用户可以设置用户组和权限。

AEM Mobile On-Demand连接器用于将AEM Mobile托管内容与Adobe Experience Manager Mobile的On-Demand服务绑定。 这使内容作者能够使用AEM工具为移动应用程序创建和管理材料，同时使用AEM Mobile的按需服务轻松分发移动内容。

>[!NOTE]
>
>这是设置AEM实例的一个步骤。

### 配置AEM Mobile On-demand Services客户端{#configuring-aem-mobile-on-demand-services-client}

您必须完成配置步骤，AEM Mobile集成才能正常运行。

1. 转到OSGI服务配置

   1. AEM >工具>操作> Web Console
   1. 滚动或搜索&#x200B;***Experience ManagerMobile On-demand Services客户端(以前是AdobeDigital Publishing Solution客户端)***

1. 编辑&#x200B;***Experience ManagerMobile On-demand Services客户端***

   1. **（必填）** 输入必填字段：

      1. 客户端 ID.
      1. 客户端密钥.
   1. **（可选）** 编辑现有值。


1. 保存更改。
1. 以下是一个配置示例：

![chlimage_1-53](assets/chlimage_1-53.png)

### 配置AEM Mobile On-demand Services CloudService {#configuring-aem-mobile-on-demand-services-cloudservice}

1. 转到Cloud Services

   1. AEM >工具>部署> [CloudServices](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html)。 滚动或搜索&#x200B;***Adobe Experience Manager Mobile On-demand Services***

1. 选择&#x200B;***Configure now***&#x200B;或&#x200B;***Show Configurations*** ，然后选择添加新配置图标

1. 创建新配置

   1. 输入标题和名称
   1. 输入设备Id
   1. 输入设备令牌
   1. 选择&#x200B;***测试设备配置***&#x200B;以验证输入的值
   1. 选择确定

## 添加AEM Mobile用户角色和分配权限{#adding-aem-mobile-user-roles-and-assigning-permissions}

创建项目后，您应创建角色并授予用户访问权限。 只有主控管理员才能创建和编辑角色。 在创建角色时，您可以为任何分配了这些权限的用户启用这些功能（或权限）。 例如，您可以创建一个角色（其中包含构建应用程序的权限）和另一个角色（其中包含创建和发布内容的权限）。

在AEM Mobile应用程序开发中，存在三种不同的角色：

* 管理员
* 开发人员
* 作者

有关使用不同权限创建角色（如应用程序构建或创建和发布内容）的更多信息，请单击AEM Mobile帮助中的[创建用户角色和授予访问权限](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html)。

>[!NOTE]
>
>管理应用程序内容需要开发人员、内容作者和管理员共同努力。 作者处理页面，这些页面又基于应用程序开发人员生成的模板和组件。 最后，管理员可以战略性地发布更新的应用程序内容。 设置AEM组和权限可在应用程序功能板或控制中心中定义其角色。
>
>有关AEM Mobile功能板的更多信息，请单击[此处](/help/mobile/mobile-apps-ondemand-application-dashboard.md)。

完成使用不同权限（如应用程序构建或创建和发布内容）创建角色后，请参阅&#x200B;[**配置用户和用户组**](/help/mobile/aem-mobile-configure-users.md)&#x200B;以配置用户和组以支持移动设备应用程序的创作和管理。

### 其他资源 {#additional-resources}

要详细了解创建AEM Mobile On-demand Services应用程序的其他两个角色和职责，请参阅以下资源：

* [为AEM Mobile On-demand Services开发AEM内容](/help/mobile/aem-mobile-on-demand.md)
* [为AEM Mobile On-demand Services应用程序创作AEM内容](/help/mobile/mobile-apps-ondemand.md)

>[!NOTE]
>
>要预览应用程序内容（包括浏览页面和文章），请参阅[使用Preflight预览](/help/mobile/aem-mobile-manage-ondemand-services.md)。
