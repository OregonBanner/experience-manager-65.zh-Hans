---
title: 配置用户和用户组
description: 关注此页面，了解用户角色以及如何配置用户和组以支持创作和管理您的Mobile On-Demand Services应用程序。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
exl-id: 58b7d1b9-a851-442a-9d02-212cad8abbed
source-git-commit: 60924e7ee204e43a2ff833fbc394beca8db9c9d9
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---

# 配置用户和用户组 {#configure-your-users-and-user-groups}

>[!NOTE]
>
>对于需要基于单页应用程序框架的客户端渲染（例如React）的项目，Adobe建议使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md).

本章介绍用户角色以及如何配置用户和组以支持移动设备应用程序的创作和管理。

## AEM Mobile应用程序用户和组管理 {#aem-mobile-application-users-and-group-administration}

### AEM Mobile应用程序内容作者（应用程序创作组） {#aem-mobile-application-content-authors-app-author-group}

应用程序创作组的成员负责创作AEM移动应用程序内容，包括页面、文本、图像和视频。

#### 组配置 — 应用程序作者 {#group-configuration-app-authors}

1. 创建一个名为“app-authors”的用户组：

   导航到用户Admin Console： [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   在用户组控制台中，选择“+”按钮以创建组。

   将此组的ID设置为“app-authors”，表示它是特定于AEM内创作移动应用程序的创作用户组的特定类型。

1. 将成员添加到组：作者

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. 现在您已经创建了应用程序作者用户组，接下来可以通过 [用户Admin Console](http://localhost:4502/libs/granite/security/content/useradmin.md).

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. 以下内容允许您添加到AEM内容作者组：

   （读取）于

   * /app
   * /etc/clientlibs
   * /etc/designs
   * /etc/cloudservices/dps2015

### AEM Mobile应用程序管理员组（app-admins组） {#aem-mobile-application-administrators-group-app-admins-group}

app-admins组的成员可以使用与应用程序作者相同的权限来创作应用程序内容 **和** 此外，还负责：

* 暂存、发布和清除应用程序ContentSync OTA更新

>[!NOTE]
>
>权限决定AEM App Command Center中某些用户操作的可用性。
>
>请注意，某些选项不适用于可供应用程序管理员使用的应用程序作者。

### 组配置 — 应用程序管理员 {#group-configuration-app-admins}

1. 创建一个名为app-admins的组。
1. 将以下组添加到新的app-admins组：

   * content-author
   * workflow-users

   ![chlimage_1-169](assets/chlimage_1-169.png)

   >[!NOTE]
   >
   >使用PhoneGap Build服务进行远程构建需要workflow-users

1. 导航到 [权限控制台](http://localhost:4502/useradmin) 并添加权限以管理cloudservices

   * /etc/cloudservices/mobileservices上的（读取、修改、创建、删除、复制）

1. 在相同的“权限”控制台上，为暂存、发布和清除应用程序内容更新添加权限；

   * /etc/packages/mobileapp上的（读取、修改、创建、删除、复制）
   * /var/contentsync上的（读取）

   >[!NOTE]
   >
   >包复制用于将应用程序更新从创作实例发布到发布实例

   >[!CAUTION]
   >
   >/var/contentsync访问被拒绝为OOTB。
   >
   >省略READ权限可能会导致生成和复制空更新包。

1. 根据需要向此组添加成员
1. 导出内容或上传

   * /etc/contentsync上的（读取）以访问导出模板
   * /var上的（读取）路径在读取时遍历
   * /var/contentsync上的（读取、写入、修改、删除）以写入、读取和清理ContentSync缓存的导出内容

### 其他资源 {#additional-resources}

要详细了解创建AEM Mobile On-demand Services应用程序的其他两个角色和职责，请参阅以下资源：

* [为AEM Mobile On-demand Services开发AEM内容](/help/mobile/aem-mobile-on-demand.md)
* [为AEM Mobile On-demand Services应用程序创作AEM内容](/help/mobile/mobile-apps-ondemand.md)
