---
title: 配置用户和用户组
seo-title: 配置用户和用户组
description: 可查看本页以了解用户角色以及如何配置用户和组以支持移动点播服务应用程序的创作和管理。
seo-description: 可查看本页以了解用户角色以及如何配置用户和组以支持移动点播服务应用程序的创作和管理。
uuid: 461e1725-41dd-4883-92b9-a7e175660401
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: c3c73e67-7f85-4308-b4cd-1b42d4f3f2d9
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---


# 配置用户和用户组{#configure-your-users-and-user-groups}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

本章介绍用户角色以及如何配置用户和用户组以支持移动应用程序的创作和管理。

## AEM Mobile应用程序用户和组管理{#aem-mobile-application-users-and-group-administration}

### AEM Mobile应用程序内容作者（app-author组）{#aem-mobile-application-content-authors-app-author-group}

应用程序作者组的成员负责创作AEM移动应用程序内容，包括页面、文本、图像和视频。

#### 组配置- app-authors {#group-configuration-app-authors}

1. 新建一个名为“app-authors”的用户组：

   导航到用户Admin Console:[http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   在用户组控制台中，选择“+”按钮以创建组。

   将此组的ID设置为“app-authors”以表示它是特定于在AEM内创作移动应用程序的特定类型的作者用户组。

1. 将成员添加到组：作者

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. 现在，您已经创建了应用程序作者用户组，可以通过[用户管理控制台](http://localhost:4502/libs/granite/security/content/useradmin.md)向此新用户组添加各个团队成员。

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. 以下内容允许您添加到AEM内容作者组：

   （阅读）打开

   * /app
   * /etc/clientlibs
   * /etc/designs
   * /etc/cloudservices/dps2015

### AEM Mobile应用程序管理员组（应用程序管理员组）{#aem-mobile-application-administrators-group-app-admins-group}

app-admins组的成员还可以使用应用程序作者&#x200B;**和**&#x200B;附带的相同权限创作应用程序内容，此外，他们还负责：

* 暂存、发布和清除应用程序ContentSync OTA更新

>[!NOTE]
>
>权限决定AEM App Command Center中某些用户操作的可用性。
>
>您会注意到有些选项对于应用程序作者不可用，而应用程序管理员则可用。

### 组配置- app-admins {#group-configuration-app-admins}

1. 新建一个名为app-admins的组。
1. 将以下用户组添加到新的应用程序管理员组：

   * content-authors
   * 工作流用户

   ![chlimage_1-169](assets/chlimage_1-169.png)

   >[!NOTE]
   >
   >使用PhoneGap Build服务进行远程构建需要工作流用户

1. 导航到[权限控制台](http://localhost:4502/useradmin)并添加管理云服务的权限

   * /etc/cloudservices/mobileservices上的（读取、修改、创建、删除、复制）

1. 在同一“权限”控制台上，为舞台添加权限，发布和清除应用程序内容更新；

   * /etc/packages/mobileapp上的（读取、修改、创建、删除、复制）
   * /var/contentsync上的（读取）

   >[!NOTE]
   >
   >包复制用于将应用程序更新从作者实例发布到发布实例

   >[!CAUTION]
   >
   >/var/contentsync访问被拒绝OOTB。
   >
   >忽略READ权限可能会导致生成和复制空的更新包。

1. 根据需要向此组添加成员
1. 导出内容或上传

   * （读取）在/etc/contentsync上访问导出模板
   * （读取）在/var上执行路径遍历
   * （读取、写入、修改、删除）/var/contentsync上的内容以写入、读取和清除ContentSync缓存的导出内容

### 其他资源 {#additional-resources}

要进一步了解创建AEM Mobile On-demand Services应用程序的其他两个角色和职责，请参阅以下资源：

* [为AEM Mobile On-demand Services开发AEM内容](/help/mobile/aem-mobile-on-demand.md)
* [为AEM Mobile On-demand Services应用程序创作AEM内容](/help/mobile/mobile-apps-ondemand.md)
