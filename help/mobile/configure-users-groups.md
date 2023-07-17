---
title: 配置用户和用户组
description: 关注此页面，了解用户角色以及如何配置用户和组以支持移动应用程序的创作和管理。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: 9f814204-8cd4-4ba9-9e25-3ff1b25c1955
source-git-commit: 96e2e945012046e6eac878389b7332985221204e
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---

# 配置用户和用户组 {#configure-your-users-and-user-groups}

>[!NOTE]
>
>对于需要基于单页应用程序框架的客户端渲染（例如React）的项目，Adobe建议使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md).

本章介绍用户角色以及如何配置用户和组以支持移动设备应用程序的创作和管理。

## AEM Mobile应用程序用户和组管理 {#aem-mobile-application-users-and-group-administration}

为帮助组织和管理AEM应用程序的权限模型，提供了以下两个组：

* 面向应用程序管理员的应用程序管理员
* 面向应用程序作者的应用程序作者

### AEM Mobile应用程序内容作者（应用程序创作组） {#aem-mobile-application-content-authors-app-author-group}

应用程序创作组的成员负责创作AEM移动应用程序内容，包括页面、文本、图像和视频。

#### 组配置 — 应用程序作者 {#group-configuration-app-authors}

1. 创建一个名为“app-authors”的用户组：

   导航到用户Admin Console： [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   在用户组控制台中，选择“+”按钮以创建组。

   将此组的ID设置为“app-authors”，表示它是特定于AEM内创作移动应用程序的创作用户组的特定类型。

1. 将成员添加到组：作者

   ![chlimage_1-18](assets/chlimage_1-18.png)

   将应用程序作者添加到“作者”组

1. 现在您已经创建了应用程序作者用户组，接下来可以通过 [用户Admin Console](http://localhost:4502/libs/granite/security/content/useradmin.md).

   ![chlimage_1-19](assets/chlimage_1-19.png)

   编辑用户组

1. 导航到 [权限控制台](http://localhost:4502/useradmin) 并添加权限以管理cloudservices

   * /etc/cloudservices上的（读取）

   >[!NOTE]
   >
   >应用程序作者扩展了AEM中的默认内容作者（作者）组，以便他们继承在/content/phonegap下创建内容的能力

### AEM Mobile应用程序管理员组（app-admins组） {#aem-mobile-application-administrators-group-app-admins-group}

app-admins组的成员可以使用与应用程序作者相同的权限来创作应用程序内容 **和** 此外，还负责：

* 在AEM中配置PhoneGap Build和AdobeMobile Services云服务
* 暂存、发布和清除应用程序内容同步OTA更新

>[!NOTE]
>
>权限决定AEM App Command Center中某些用户操作的可用性。
>
>请注意，某些选项不适用于可供应用程序管理员使用的应用程序作者。

#### 组配置 — 应用程序管理员 {#group-configuration-app-admins}

1. 创建一个名为app-admins的组。
1. 将以下组添加到新的app-admins组：

   * content-author
   * workflow-users

   ![chlimage_1-20](assets/chlimage_1-20.png)

1. 导航到 [权限控制台](http://localhost:4502/useradmin) 并添加权限以管理cloudservices

   * /etc/cloudservices/mobileservices上的（读取、修改、创建、删除、复制）
   * （读取、修改、创建、删除、复制）/etc/cloudservices/phonegap-build

1. 在同一“权限”控制台上，为暂存、发布和清除应用程序内容更新添加权限

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

## 仪表板磁贴权限 {#dashboard-tile-permissions}

仪表板磁贴可能会根据用户拥有的权限公开不同的操作。 下面描述了每个图块可用的操作。

除了这些权限之外，还可以根据当前应用程序的配置方式显示/隐藏操作。 例如，如果尚未将PhoneGap云配置分配给应用程序，则公开“远程构建”操作没有任何意义。 下面列出了&#39;**配置条件**”部分。

### 管理应用程序磁贴 {#manage-app-tile}

图块当前没有需要权限的操作，但应用程序的详细信息页面具有以下操作：

* *编辑* 对于app-author和app-admin (UI触发器 — jcr：write - on /content/phonegap/{suffix})
* *下载* 对于app-author和app-admin (UI触发器 — on /content/phonegap/{suffix})

下图显示了应用程序的“下载”和“编辑”选项：

![chlimage_1-21](assets/chlimage_1-21.png)
