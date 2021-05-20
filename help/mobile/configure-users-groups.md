---
title: 配置用户和用户组
seo-title: 配置用户和用户组
description: 请阅读本页，了解用户角色以及如何配置用户和群组以支持移动设备应用程序的创作和管理。
seo-description: 请阅读本页，了解用户角色以及如何配置用户和群组以支持移动设备应用程序的创作和管理。
uuid: 55cea2b3-d7e6-4174-92b3-ee97e46b59c4
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 167f3bd9-7dbc-4e6b-9868-3ee53935641b
exl-id: 9f814204-8cd4-4ba9-9e25-3ff1b25c1955
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---

# 配置用户和用户组{#configure-your-users-and-user-groups}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

本章介绍用户角色以及如何配置用户和群组以支持移动设备应用程序的创作和管理。

## AEM Mobile应用程序用户和组管理{#aem-mobile-application-users-and-group-administration}

为帮助组织和管理AEM应用程序的权限模型，可使用以下两个组：

* 应用程序管理员的应用程序管理员
* 适用于应用程序作者的应用程序作者

### AEM Mobile应用程序内容作者（应用程序作者组）{#aem-mobile-application-content-authors-app-author-group}

应用程序作者组的成员负责创作AEM移动应用程序内容，包括页面、文本、图像和视频。

#### 组配置 — app-authors {#group-configuration-app-authors}

1. 创建一个名为“app-authors”的新用户组：

   导航到用户Admin Console:[http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   在用户组控制台中，选择“+”按钮以创建组。

   将此组的ID设置为“应用程序作者”，表示它是特定于在AEM中创作移动应用程序的特定类型的作者用户组。

1. 将成员添加到组：作者

   ![chlimage_1-18](assets/chlimage_1-18.png)

   将应用程序作者添加到作者组

1. 现在，您已创建应用程序作者用户群组，接下来可以通过[用户管理控制台](http://localhost:4502/libs/granite/security/content/useradmin.md)向此新群组添加各个团队成员。

   ![chlimage_1-19](assets/chlimage_1-19.png)

   编辑用户组

1. 导航到[权限控制台](http://localhost:4502/useradmin)并添加用于管理cloudservices的权限

   * /etc/cloudservices上的（读取）
   >[!NOTE]
   >
   >应用程序作者从AEM中扩展了默认的内容作者（作者）组，从而继承了在/content/phonegap下创建内容的功能

### AEM Mobile应用程序管理员组（应用程序管理员组）{#aem-mobile-application-administrators-group-app-admins-group}

应用程序管理员组的成员还可以使用应用程序作者&#x200B;**AND**&#x200B;附带的相同权限创作应用程序内容：

* 在AEM中配置PhoneGap Build和AdobeMobile Services云服务
* 暂存、发布和清除应用程序内容同步OTA更新

>[!NOTE]
>
>权限决定了AEM应用程序命令中心中某些用户操作的可用性。
>
>您会注意到，有些选项对于应用程序作者而言不可用，而应用程序管理员则可用。

#### 组配置 — 应用程序管理员{#group-configuration-app-admins}

1. 创建一个名为应用程序管理员的新组。
1. 将以下组添加到新的应用程序管理员组：

   * content-authors
   * 工作流用户

   ![chlimage_1-20](assets/chlimage_1-20.png)

1. 导航到[权限控制台](http://localhost:4502/useradmin)并添加用于管理cloudservices的权限

   * （读取、修改、创建、删除、复制）/etc/cloudservices/mobileservices
   * （读取、修改、创建、删除、复制）/etc/cloudservices/phonegap-build

1. 在同一“权限”控制台上，添加用于暂存、发布和清除应用程序内容更新的权限

   * （读取、修改、创建、删除、复制）/etc/packages/mobileapp
   * /var/contentsync上的（读取）

   >[!NOTE]
   >
   >包复制用于将应用程序更新从创作实例发布到发布实例

   >[!CAUTION]
   >
   >/var/contentsync访问被拒绝OOTB。
   >
   >省略“读取”权限可能会导致生成和复制空的更新包。

1. 根据需要向此组添加成员

## 功能板磁贴权限{#dashboard-tile-permissions}

功能板图块可能根据用户拥有的权限显示不同的操作。 下面描述了每个图块可使用的操作。

除了这些权限之外，还可以根据当前应用程序的配置方式显示/隐藏操作。 例如，如果尚未向应用程序分配PhoneGap云配置，则公开“远程构建”操作没有意义。 这些参数将列在“**配置条件**”部分下。

### 管理应用程序磁贴{#manage-app-tile}

图块当前没有需要权限的操作，但应用程序的详细信息页面具有以下操作：

* ** 为app-author和app-admin编辑（UI触发器 — jcr:write — 在/content/phonegap/{suffix}上）
* ** 下载应用程序作者和应用程序管理员（UI触发器 — 在/content/phonegap/{suffix}上）

下图显示了应用程序的下载和编辑选项：

![chlimage_1-21](assets/chlimage_1-21.png)
