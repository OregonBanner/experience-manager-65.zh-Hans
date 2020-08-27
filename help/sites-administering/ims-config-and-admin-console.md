---
title: AdobeIMS对AEM [!DNL Admin Console] Managed Services的身份验证和支持
seo-title: AdobeIMS对AEM [!DNL Admin Console] Managed Services的身份验证和支持
description: 了解如何在AEM中使用[!DNLAdmin Console]。
seo-description: 了解如何在AEM中使用[!DNLAdmin Console]。
uuid: 3f5b32c7-cf62-41a4-be34-3f71bbf224eb
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f6112dea-a1eb-4fd6-84fb-f098476deab7
translation-type: tm+mt
source-git-commit: 5a421c66930d8c7a9eb633c707b4b51d4549b303
workflow-type: tm+mt
source-wordcount: '1730'
ht-degree: 10%

---


# AdobeIMS对AEMManaged Services的 [!DNL Admin Console] 身份验证和支持 {#adobe-ims-authentication-and-admin-console-support-for-aem-managed-services}

>[!NOTE]
>
>请注意，此功能仅对Adobe Managed Services客户可用。

## 简介 {#introduction}

AEM 6.4.3.0引入了对AEM实 [!DNL Admin Console] 例和基于AdobeIMS(Identity Management系统)的AEM **客户身份验证的** 支持。

AEM对AEM的登 [!DNL Admin Console] 录将允许Managed Services客户在一个控制台中管理所有Experience Cloud用户。 用户和用户组可以分配给与AEM实例关联的产品用户档案，允许他们登录到特定实例。

## 主要亮点 {#key-highlights}

* AEM IMS身份验证支持仅针对AEM作者、管理员或开发人员，而不针对客户站点(如站点访客)的外部最终用户
* AEM [!DNL Admin Console] Managed Services客户将代表其为IMS组织，其实例将代表其为产品上下文。 客户系统和产品管理员将能够管理对实例的访问
* AEMManaged Services将将客户拓扑与同步 [!DNL Admin Console]。 在中，每个实例将有一个AEMManaged Services产品上下文实例 [!DNL Admin Console]。
* Product Profiles in [!DNL Admin Console] will determine which instances a user can access
* 支持使用客户自己的符合SAML 2规范的标识提供者的联合身份验证
* 仅支持Enterprise ID或Federated ID（用于客户单点登录），不支持个人AdobeID。
* [!DNL User Management] (在Adobe [!DNL Admin Console]中)将继续归客户管理员所有。

## 架构 {#architecture}

IMS身份验证通过在AEM和AdobeIMS端点之间使用OAuth协议来工作。 将用户添加到 IMS 并拥有 Adobe 身份后，他们便可以使用 IMS 凭证登录到 AEM Managed Services 实例。

用户登录流程如下所示，用户将被重定向到IMS，或者被重定向到客户IDP进行SSO验证，然后被重定向回AEM。

![image2018-9-23_23-55-8](assets/image2018-9-23_23-55-8.png)

## How To Set Up {#how-to-set-up}

### Onboarding Organizations to [!DNL Admin Console] {#onboarding-organizations-to-admin-console}

The customer onboarding to [!DNL Admin Console] is a pre-requisite to using Adobe IMS for AEM authentication.

作为第一步，客户应在AdobeIMS中设置组织。 Adobe企业客户在Adobe中以IMS组织的形 [式表示 [!DNL Admin Console]](https://helpx.adobe.com/cn/enterprise/using/admin-console.html)。

AEM Managed Services customers should already have an organization provisioned, and as part of the IMS provisioning, the customer instances will be made available in the [!DNL Admin Console] for managing user entitlements and access.

转向IMS进行用户身份验证将是AMS和客户之间的共同努力，每个客户都有工作流完成。

一旦客户作为IMS组织存在，并且AMS完成为客户供应IMS的过程，这就是所需配置工作流的摘要：

![image2018-9-23_23-33-25](assets/image2018-9-23_23-33-25.png)

1. The designated System Admin receives an invite to log in to the [!DNL Admin Console]
1. 系统管理员声明域以确认域的所有权（在此示例中为acme.com）
1. 系统管理员设置用户目录
1. 系统管理员在SSO设置中配置标识提供 [!DNL Admin Console] 者(IDP)。
1. AEM管理员照常管理本地组、权限和权限。 请参阅用户和组同步

>[!NOTE]
>
>有关AdobeIdentity Management基础知识（包括IDP配置）的详细信息，请参阅 [本页文章。](https://helpx.adobe.com/cn/enterprise/using/set-up-identity.html)
>
>有关企业管理的更多信息， [!DNL Admin Console] 请参阅本 [页文章](https://helpx.adobe.com/cn/enterprise/managing/user-guide.html)。

### 入门用户 [!DNL Admin Console] {#onboarding-users-to-the-admin-console}

根据客户的规模及其偏好，有三种登录用户的方法：

1. 在 [!DNL Admin Console]
1. 上传包含用户的CSV文件
1. 从客户的企业Active Directory同步用户和用户组。

#### Manual Addition through [!DNL Admin Console] UI {#manual-addition-through-admin-console-ui}

Users and Groups can be manually created in the [!DNL Admin Console] UI. 如果用户数不多，则可以使用此方法。 例如，少于50个AEM用户。

如果客户已使用此方法管理其他Adobe产品(如Analytics、目标或Creative Cloud应用程序)，则还可以手动创建用户。

![image2018-9-23_20-39-9](assets/image2018-9-23_20-39-9.png)

#### 在UI中上传文 [!DNL Admin Console] 件 {#file-upload-in-the-admin-console-ui}

为便于用户创建，可以上传CSV文件以批量添加用户：

![image2018-9-23_18-59-57](assets/image2018-9-23_18-59-57.png)

#### 用户同步工具 {#user-sync-tool}

用户同步工具（简称UST）使企业客户能够利用Active Directory或其他经测试的OpenLDAP目录服务创建或管理Adobe用户。 目标用户是IT身份管理员（企业目录和系统管理员），他们将能够安装和配置该工具。 开放源工具可自定义，这样客户就可以让开发人员修改它以满足自己的特定要求。

When User Sync runs, it fetches a list of users from the organization’s Active Directory (or any other compatible data source) and compares it with the list of users within the [!DNL Admin Console]. It then calls the Adobe [!DNL User Management] API so that the [!DNL Admin Console] is synchronized with the organization’s directory. 改变流完全是单向的；在中所做的任 [!DNL Admin Console] 何编辑不会推送到目录。

此工具允许系统管理员将客户目录中的用户组与产品配置以及新UST版本中的用户组进行映射 [!DNL Admin Console]，新UST版本还允许在中动态创建用户组 [!DNL Admin Console]。

To set up User Sync, the organization needs to create a set of credentials in the same way they would use the [[!DNL User Management] API](https://www.adobe.io/apis/cloudplatform/usermanagement/docs/setup.html).

![image2018-9-23_13-36-56](assets/image2018-9-23_13-36-56.png)

用户同步通过AdobeGithub存储库分发，该位置为：

[https://github.com/adobe-apiplatform/user-sync.py/releases/latest](https://github.com/adobe-apiplatform/user-sync.py/releases/latest)

请注意，预发行版2.4RC1支持动态组创建，可在以下位置找到： [https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1)

The major features for this release are the ability to dynamically map new LDAP groups for user membership in the [!DNL Admin Console], as well as dynamic user group creation.

有关新组功能的更多信息，请访问：

[https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration](https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration.md#additional-group-options)

>[!NOTE]
>
>有关用户同步工具的详细信息，请参阅 [文档页](https://adobe-apiplatform.github.io/user-sync.py/en/)。
>
>
>The User Sync Tool needs to register as an Adobe I/O client UMAPI using the procedure described [here](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html).
>
>The Adobe I/O Console Documentation can be found [here](https://www.adobe.io/apis/cloudplatform/console.html).
>
>
>用 [!DNL User Management] 户同步工具使用的API在此位 [置介绍](https://www.adobe.io/apis/cloudplatform/umapi-new.html)。

>[!NOTE]
>
>AEM IMS配置将由Adobe Managed Services团队处理。 但是，客户管理员可以根据其要求修改它（例如“自动组成员关系”或“组映射”）。 IMS客户端也将由您的Managed Services团队注册。

## 使用方法 {#how-to-use}

### Managing Products and User Access in [!DNL Admin Console] {#managing-products-and-user-access-in-admin-console}

When the customer Product Administrator logs in to [!DNL Admin Console], they will see multiple instances of the AEM Managed Services Product Context as shown below:

![screen_shot_2018-09-17at105804pm](assets/screen_shot_2018-09-17at105804pm.png)

In this example, the org *AEM-MS-Onboard* has 32 instances spanning different topologies and environments like Stage, Prod, etc.

![screen_shot_2018-09-17at105517pm](assets/screen_shot_2018-09-17at105517pm.png)

可以检查实例详细信息以标识实例：

![screen_shot_2018-09-17at105601pm](assets/screen_shot_2018-09-17at105601pm.png)

在每个Product Context实例下，将有一个关联的Product用户档案。 此产品用户档案用于为用户和组分配访问权限。

![image2018-9-18_7-48-50](assets/image2018-9-18_7-48-50.png)

在此产品用户档案下添加的任何用户和用户组都将能够登录到该实例，如下例所示：

![screen_shot_2018-09-17at105623pm](assets/screen_shot_2018-09-17at105623pm.png)

### 登录AEM {#logging-into-aem}

#### 本地管理员登录 {#local-admin-login}

AEM可以继续支持管理员用户的本地登录，因为登录屏幕具有本地登录选项：

![screen_shot_2018-09-18at121056am](assets/screen_shot_2018-09-18at121056am.png)

#### 基于 IMS 的登录 {#ims-based-login}

对于其他用户，只需在实例上配置 IMS 即可使用基于 IMS 的登录。The user will first click on the **Sign in with Adobe** button as shown below:

![image2018-9-18_0-10-32](assets/image2018-9-18_0-10-32.png)

然后，他们将被重定向到IMS登录屏幕并输入其凭据：

![screen_shot_2018-09-17at115629pm](assets/screen_shot_2018-09-17at115629pm.png)

If a federated IDP is configured during initial [!DNL Admin Console] setup, then the user will be redirected to the customer IDP for SSO.

以下示例中的IDP为Okta:

![screen_shot_2018-09-17at115734pm](assets/screen_shot_2018-09-17at115734pm.png)

身份验证完成后，用户将被重定向回 AEM 并登录：

![screen_shot_2018-09-18at120124am](assets/screen_shot_2018-09-18at120124am.png)

### 迁移现有用户 {#migrating-existing-users}

对于使用其他身份验证方法并正在迁移到IMS的现有AEM实例，需要执行迁移步骤。

AEM存储库（通过LDAP或SAML本地源）中的现有用户可以使用用户迁移实用程序迁移到IMS作为IDP。

此实用程序将由您的AMS团队作为IMS配置的一部分运行。

### 管理AEM中的权限和ACL {#managing-permissions-and-acls-in-aem}

访问控制和权限将继续在AEM中进行管理，这可以通过将来自IMS的用户组(如下例中的AEM- GRP-008)与定义权限和访问控制的本地组分开来实现。 可以将从IMS同步的用户组分配给本地组并继承权限。

在以下示例中，我们将同步的组作为示例添加到本地 *Dam_Users* 组。

此处，用户也已分配到中的几个组 [!DNL Admin Console]。 (请注意，用户和用户组可以使用用户同步工具从LDAP同步或在本地创建，请参阅上 **面的入门[!DNL Admin Console]** 用户部分)。

&amp;ast；请注意，用户只有登录到实例时才会同步用户组，对于拥有大量用户和用户组的客户，AMS可以运行组同步实用程序以预取组，以进行上述访问控制和权限管理。

![screen_shot_2018-09-17at94207pm](assets/screen_shot_2018-09-17at94207pm.png)

用户是 IMS 中以下组的一部分：

![screen_shot_2018-09-17at94237pm](assets/screen_shot_2018-09-17at94237pm.png)

用户登录时，会同步其组成员资格，如下所示：

![screen_shot_2018-09-17at94033pm](assets/screen_shot_2018-09-17at94033pm.png)

在AEM中，可以将从IMS同步的用户组添加为现有本地组（如DAM用户）的成员。

![screen_shot_2018-09-17at95804pm](assets/screen_shot_2018-09-17at95804pm.png)

如下所示，AEM- *GRP_008组继承* DAM用户的权限和权限。 这是管理已同步组权限的有效方法，也常用于基于LDAP的身份验证方法。

![screen_shot_2018-09-17at110505pm](assets/screen_shot_2018-09-17at110505pm.png)