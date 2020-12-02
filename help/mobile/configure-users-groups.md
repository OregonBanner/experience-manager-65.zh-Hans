---
title: 配置用户和用户组
seo-title: 配置用户和用户组
description: 可查看本页以了解用户角色以及如何配置用户和组以支持创作和管理移动应用程序。
seo-description: 可查看本页以了解用户角色以及如何配置用户和组以支持创作和管理移动应用程序。
uuid: 55cea2b3-d7e6-4174-92b3-ee97e46b59c4
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 167f3bd9-7dbc-4e6b-9868-3ee53935641b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---


# 配置用户和用户组{#configure-your-users-and-user-groups}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

本章介绍用户角色以及如何配置用户和用户组以支持移动应用程序的创作和管理。

## AEM Mobile应用程序用户和组管理{#aem-mobile-application-users-and-group-administration}

要帮助组织和管理AEM Apps的权限模型，可以使用以下两个组：

* 应用程序管理员的应用程序管理员
* 应用程序作者的app-authors

### AEM Mobile应用程序内容作者（app-author组）{#aem-mobile-application-content-authors-app-author-group}

应用程序作者组的成员负责创作AEM移动应用程序内容，包括页面、文本、图像和视频。

#### 组配置- app-authors {#group-configuration-app-authors}

1. 新建一个名为“app-authors”的用户组：

   导航到用户Admin Console:[http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   在用户组控制台中，选择“+”按钮以创建组。

   将此组的ID设置为“app-authors”以表示它是特定于在AEM内创作移动应用程序的特定类型的作者用户组。

1. 将成员添加到组：作者

   ![chlimage_1-18](assets/chlimage_1-18.png)

   将应用程序作者添加到作者组

1. 现在，您已经创建了应用程序作者用户组，可以通过[用户管理控制台](http://localhost:4502/libs/granite/security/content/useradmin.md)向此新用户组添加各个团队成员。

   ![chlimage_1-19](assets/chlimage_1-19.png)

   编辑用户组

1. 导航到[权限控制台](http://localhost:4502/useradmin)并添加管理云服务的权限

   * /etc/cloudservices上的（读取）
   >[!NOTE]
   >
   >应用程序作者从AEM扩展默认的content-authors（作者）组，从而继承在/content/phonegap下创建内容的能力

### AEM Mobile应用程序管理员组（应用程序管理员组）{#aem-mobile-application-administrators-group-app-admins-group}

app-admins组的成员还可以使用应用程序作者&#x200B;**和**&#x200B;附带的相同权限创作应用程序内容，此外，他们还负责：

* 在AEM中配置PhoneGap Build和AdobeMobile Services云服务
* 暂存、发布和清除应用程序内容同步OTA更新

>[!NOTE]
>
>权限决定AEM App Command Center中某些用户操作的可用性。
>
>您会注意到有些选项对于应用程序作者不可用，而应用程序管理员则可用。

#### 组配置- app-admins {#group-configuration-app-admins}

1. 新建一个名为app-admins的组。
1. 将以下用户组添加到新的应用程序管理员组：

   * content-authors
   * 工作流用户

   ![chlimage_1-20](assets/chlimage_1-20.png)

1. 导航到[权限控制台](http://localhost:4502/useradmin)并添加管理云服务的权限

   * /etc/cloudservices/mobileservices上的（读取、修改、创建、删除、复制）
   * /etc/cloudservices/phonegap-build上的（读取、修改、创建、删除、复制）

1. 在同一“权限”控制台上，向舞台添加权限，发布和清除应用程序内容更新

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

## 仪表板磁贴权限{#dashboard-tile-permissions}

仪表板拼贴可能根据用户拥有的权限显示不同的操作。 下面介绍了每个拼贴可用的操作。

除了这些权限之外，还可以根据当前应用程序的配置方式显示／隐藏操作。 例如，如果尚未为应用程序分配PhoneGap云配置，则公开“远程构建”操作没有意义。 “**配置条件**”部分下将列出这些组件。

### 管理应用程序磁贴{#manage-app-tile}

拼贴当前没有需要权限的操作，但应用程序的详细信息页面具有以下操作：

* *编* 辑app-author和app-admin（UI触发器- jcr:write - on /content/phonegap/{suffix}）
* *下* 载app-author和app-admin（UI触发器——在/content/phonegap/{suffix}上）

下图显示了应用程序的下载和编辑选项：

![chlimage_1-29](assets/chlimage_1-21.png)

