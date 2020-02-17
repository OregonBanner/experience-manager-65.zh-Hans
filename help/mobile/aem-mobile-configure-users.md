---
title: 配置用户和用户组
seo-title: 配置用户和用户组
description: 可查看本页以了解用户角色以及如何配置用户和用户组以支持移动点播服务应用程序的创作和管理。
seo-description: 可查看本页以了解用户角色以及如何配置用户和用户组以支持移动点播服务应用程序的创作和管理。
uuid: 461e1725-41dd-4883-92b9-a7e175660401
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: c3c73e67-7f85-4308-b4cd-1b42d4f3f2d9
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 配置用户和用户组 {#configure-your-users-and-user-groups}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

本章介绍用户角色以及如何配置用户和用户组以支持移动应用程序的创作和管理。

## AEM Mobile应用程序用户和组管理 {#aem-mobile-application-users-and-group-administration}

### AEM Mobile应用程序内容作者（应用程序作者组） {#aem-mobile-application-content-authors-app-author-group}

应用程序作者组的成员负责创作AEM Mobile应用程序内容，包括页面、文本、图像和视频。

#### 组配置——应用程序作者 {#group-configuration-app-authors}

1. 创建名为“app-authors”的新用户组：

   导航到用户管理控制台： [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   在用户组控制台中，选择“+”按钮以创建组。

   将此组的ID设置为“app-authors”，以表示它是特定于在AEM中创作移动应用程序的特定类型的作者用户组。

1. 将成员添加到组：作者

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. 现在，您已创建应用程序作者用户组，可以通过“用户管理”控制台向此新用户组添 [加单个团队成员](http://localhost:4502/libs/granite/security/content/useradmin.md)。

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. 以下内容允许您添加到AEM的内容作者组：

   （阅读）打开

   * /app
   * /etc/clientlibs
   * /etc/designs
   * /etc/cloudservices/dps2015

### AEM Mobile应用程序管理员组（应用程序管理员组） {#aem-mobile-application-administrators-group-app-admins-group}

应用程序管理员组的成员可以使用应用程序作者附带的相同权限创作应用程序内容 **，此外** ，还负责：

* 暂存、发布和清除应用程序内容同步OTA更新

>[!NOTE]
>
>权限决定了AEM应用程序命令中心中某些用户操作的可用性。
>
>您会注意到，某些选项对于应用程序作者不可用，这些选项对应用程序管理员可用。

### 组配置——应用程序管理员 {#group-configuration-app-admins}

1. 创建一个名为app-admins的新用户组。
1. 将以下用户组添加到您的新应用程序管理员组中：

   * content-authors
   * 工作流用户
   ![chlimage_1-169](assets/chlimage_1-169.png)

   >[!NOTE]
   >
   >使用PhoneGap build服务进行远程构建需要工作流用户

1. 导航到“权 [限”控制台](http://localhost:4502/useradmin) ，并添加管理云服务的权限

   * 在/etc/cloudservices/mobileservices上读取、修改、创建、删除、复制)

1. 在同一“权限”控制台上，为舞台添加权限，发布和清除应用程序内容更新；

   * （读取、修改、创建、删除、复制）/etc/packages/mobileapp
   * （读取）/var/contentsync
   >[!NOTE]
   >
   >包复制用于将应用程序更新从作者实例发布到发布实例

   >[!CAUTION]
   >
   >/var/contentsync访问被拒绝OOTB。
   >
   >忽略“读取”权限可能会导致生成和复制空的更新包。

1. 根据需要将成员添加到此组
1. 导出内容或上传

   * （读取）访问导出模板
   * 在/var上（读取）到，用于读取路径遍历
   * （读、写、修改、删除）/var/contentsync上的内容以写入、读取和清除ContentSync缓存的导出内容

### 其他资源 {#additional-resources}

要进一步了解创建AEM Mobile On-Demand services应用程序的其他两个角色和职责，请参阅以下资源：

* [为AEM Mobile点播服务开发AEM内容](/help/mobile/aem-mobile-on-demand.md)
* [为AEM Mobile点播服务应用程序创作AEM内容](/help/mobile/mobile-apps-ondemand.md)
