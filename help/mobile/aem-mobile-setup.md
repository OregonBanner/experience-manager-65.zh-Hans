---
title: AEM Mobile设置
description: 按照此页面设置AEM Mobile，从而允许用户在Adobe Experience Manager (AEM)中创建和管理内容。 本页提供有关将AEM实例与基于云的AEM Mobile On-demand Services帐户和项目集成的信息。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
exl-id: 0ead982d-2315-4947-b762-596aa2aa42a1
source-git-commit: 99808cb38c5d376ccb7fb550c5212138890cec11
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 2%

---

# AEM Mobile设置{#aem-mobile-setup}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md)。

>[!CAUTION]
>
>从AEM 6.2或6.3迁移到AEM 6.5的现有Adobe Experience Manager (AEM)移动应用程序客户可以通过从包共享下载包来继续使用AEM Mobile应用程序。 但是，新安装的AEM 6.5不支持AEM Mobile应用程序功能。

要使用AEM为AEM Mobile应用程序生成内容，您必须将AEM实例与基于云的AEM Mobile On-demand Services帐户和项目集成。

请按照以下步骤设置AEM Mobile，从而允许用户在AEM中创建和管理内容。

## AEM Mobile配置 {#aem-mobile-provisioning}

要开始设置AEM Mobile，您必须：

* **请求API密钥**：要访问On-Demand Services API，您必须请求API密钥。 要请求API密钥，请完成 [PDF表单](https://helpx.adobe.com/digital-publishing-solution/help/aem-mobile-end-of-life-faq.html). 将填写好的表单发送到Adobe Developer支持部门： [wwds@adobe.com](mailto:wwds@adobe.com)

* **生成设备ID和设备标记**：收到API密钥后，即可生成设备ID和设备令牌。 转到 `https://aex.aemmobile.adobe.com` 并执行以下操作：

   * 提供API密钥
   * 使用已添加到AEM Mobile项目的Adobe ID登录，并具有以下权限（请参阅以下创建项目的步骤）

      * 管理>管理项目和用户
      * 内容>添加和编辑内容、删除内容、查看内容、发布内容

如果满足所有条件，则会生成设备ID和设备令牌。

>[!NOTE]
>
>应向所需的Adobe ID授予对AEM Mobile项目的访问权限。 请参阅 [AEM Mobile帐户管理](https://helpx.adobe.com/digital-publishing-solution/help/aem-mobile-end-of-life-faq.html) 在线帮助中。

## 为AEM Mobile创建项目 {#creating-projects-for-aem-mobile}

在创建项目时，您可以为要定位的任何平台指定设置：iOS、Android™、Windows和Desktop Web Viewer。 您指定的许多项目设置都会影响应用程序的行为。

创建项目需要使用具有主管理员角色的Adobe ID登录到On-Demand Services门户。 编辑项目需要主管理员角色或具有的用户角色 **管理项目和用户** 许可。

>[!NOTE]
>
>要了解有关在AEM Mobile中创建项目的更多信息，请单击 [此处](https://helpx.adobe.com/digital-publishing-solution/help/creating-projects.html).

## 配置AEM Mobile连接器 {#configuring-an-aem-mobile-connector}

AEM设置涉及连接器配置的以下步骤。 AEM Mobile连接器配置完成后，用户可以设置用户组和权限。

AEM Mobile On-Demand连接器用于将AEM Mobile管理的内容与Adobe Experience Manager Mobile的On-Demand服务绑定。 这使内容作者能够使用AEM工具创建和管理移动应用程序的材料，同时使用AEM Mobile的On-Demand Services轻松分发移动内容。

>[!NOTE]
>
>这是设置AEM实例的一次性步骤。

### 配置AEM Mobile On-demand Services客户端 {#configuring-aem-mobile-on-demand-services-client}

完成配置步骤以使AEM Mobile集成正常运行。

1. 转到OSGI服务配置

   1. AEM >工具>操作> Web控制台
   1. 滚动或搜索 ***Experience ManagerMobile On-demand Services客户端(是AdobeDigital Publishing Solution客户端)***

1. 编辑 ***Experience ManagerMobile On-demand Services客户端***

   1. **（必需）** 输入必填字段：

      1. 客户端 ID.
      1. 客户端密钥.

   1. **（可选）** 编辑现有值。

1. 保存更改。
1. 以下是配置示例：

![chlimage_1-53](assets/chlimage_1-53.png)

### 配置AEM Mobile On-demand Services云服务 {#configuring-aem-mobile-on-demand-services-cloudservice}

1. 转到Cloud Service。

   1. AEM >工具>部署> [云服务](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html). 滚动或搜索 ***Adobe Experience Manager Mobile On-demand Service***

1. 选择 ***立即配置*** 或 ***显示配置*** 并选择添加配置图标。

1. 创建配置

   1. 输入标题和名称
   1. 输入设备ID
   1. 输入设备令牌
   1. 选择 ***测试设备配置*** 以便验证输入的值
   1. 选择“确定”

## 添加AEM Mobile用户角色和分配权限 {#adding-aem-mobile-user-roles-and-assigning-permissions}

创建项目后，您应创建角色并授予用户访问权限。 只有主管理员才能创建和编辑角色。 在创建角色时，可为分配了这些权限的任何用户启用权能（或权限）。 例如，您可以创建一个角色，其中包含应用程序构建权限，再创建一个角色，其中包含创建和发布内容的权限。

在AEM Mobile应用程序开发中，存在三种不同的角色：

* 管理员
* 开发人员
* 创作

有关创建具有不同权限的角色（如应用程序构建角色或创建和发布内容角色）的更多信息，请单击 [创建用户角色和授予访问权限](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) AEM Mobile帮助中的。

>[!NOTE]
>
>管理应用程序内容需要开发人员、内容作者和管理员共同努力。 作者处理页面，这些页面又基于模板和应用程序开发人员生成的组件。 最后，管理员策略性地发布更新的应用程序内容。 设置AEM组和权限会定义它们在应用程序功能板或控制中心中的角色。
>
>请参阅 [AEM Mobile Dashboard](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

创建完具有不同权限的角色后（例如，用于应用程序构建或用于创建和发布内容的角色），请参阅 [**配置用户和用户组**](/help/mobile/aem-mobile-configure-users.md). 这样做可帮助您配置用户和组，以支持移动应用程序的创作和管理。

### 其他资源 {#additional-resources}

要详细了解创建AEM Mobile On-demand Services应用程序的其他两个角色和职责，请参阅以下资源：

* [为AEM Mobile On-demand Services开发AEM内容](/help/mobile/aem-mobile-on-demand.md)
* [为AEM Mobile On-demand Services应用程序创作AEM内容](/help/mobile/mobile-apps-ondemand.md)

>[!NOTE]
>
>要预览应用程序内容（包括浏览页面和文章），请参阅 [使用Preflight预览](/help/mobile/aem-mobile-manage-ondemand-services.md).
