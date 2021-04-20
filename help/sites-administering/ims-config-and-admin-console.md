---
title: AdobeIMS身份验证和 [!DNL Admin Console] 支持AEM Managed Services
seo-title: AdobeIMS身份验证和 [!DNL Admin Console] 支持AEM Managed Services
description: 了解如何在AEM中使用 [!DNL Admin Console] 。
seo-description: 了解如何在AEM中使用 [!DNL Admin Console] 。
uuid: 3f5b32c7-cf62-41a4-be34-3f71bbf224eb
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f6112dea-a1eb-4fd6-84fb-f098476deab7
exl-id: 95eae97c-01c2-4f5c-8068-f504eab7c49e
feature: Security
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '1692'
ht-degree: 10%

---

# AdobeIMS身份验证和[!DNL Admin Console]支持AEM Managed Services {#adobe-ims-authentication-and-admin-console-support-for-aem-managed-services}

>[!NOTE]
>
>请注意，此功能仅对Adobe Managed Services客户可用。

## 简介 {#introduction}

AEM 6.4.3.0为&#x200B;**AEM Managed Services**&#x200B;客户引入了对AEM实例和基于Adobe IMS(Identity Management系统)的身份验证的[!DNL Admin Console]支持。

AEM登入[!DNL Admin Console]将允许AEM Managed Services客户在一个控制台中管理所有Experience Cloud用户。 可以将用户和用户组分配给与AEM实例关联的产品用户档案，允许他们登录到特定实例。

## 主要亮点 {#key-highlights}

* AEM IMS身份验证支持仅针对AEM作者、管理员或开发人员，不针对客户站点(如站点访客)的外部最终用户
* [!DNL Admin Console]将AEM Managed Services客户表示为IMS组织，其实例表示为产品上下文。 客户系统和产品管理员将能够管理对实例的访问
* AEM Managed Services将客户拓扑与[!DNL Admin Console]同步。 在[!DNL Admin Console]中，每个实例将有一个AEM Managed Services Product Context实例。
* [!DNL Admin Console]中的产品用户档案将确定用户可以访问的实例
* 支持使用客户自己的符合SAML 2的标识提供者的联合身份验证
* 仅支持Enterprise ID或Federated ID（用于客户单点登录），不支持个人AdobeID。
* [!DNL User Management] (在Adobe [!DNL Admin Console]中)将继续归客户管理员所有。

## 架构 {#architecture}

IMS身份验证是通过在AEM和Adobe IMS端点之间使用OAuth协议来工作的。 将用户添加到 IMS 并拥有 Adobe 身份后，他们便可以使用 IMS 凭证登录到 AEM Managed Services 实例。

用户登录流如下所示，用户将被重定向到IMS，并可选地被重定向到客户IDP以进行SSO验证，然后被重定向回AEM。

![image2018-9-23_23-55-8](assets/image2018-9-23_23-55-8.png)

## 如何设置{#how-to-set-up}

### 将组织加入[!DNL Admin Console] {#onboarding-organizations-to-admin-console}

[!DNL Admin Console]是使用Adobe IMS进行AEM身份验证的先决条件。

作为第一步，客户应在Adobe IMS中设置组织。 Adobe企业客户在[Adobe [!DNL Admin Console]](https://helpx.adobe.com/cn/enterprise/using/admin-console.html)中表示为IMS组织。

AEM Managed Services客户应已设置组织，作为IMS设置的一部分，将在[!DNL Admin Console]中提供客户实例，以管理用户权利和访问。

迁移到IMS进行用户身份验证将是AMS和客户之间的共同努力，每个客户都有工作流完成。

一旦客户作为IMS组织存在，并且AMS完成了为IMS为客户设置，这就是所需配置工作流的摘要：

![image2018-9-23_23-33-25](assets/image2018-9-23_23-33-25.png)

1. 指定的系统管理员收到登录到[!DNL Admin Console]的邀请
1. 系统管理员声明域以确认域的所有权（在此示例中为acme.com）
1. 系统管理员设置用户目录
1. 系统管理员在[!DNL Admin Console]中为SSO设置配置标识提供者(IDP)。
1. AEM管理员照常管理本地组、权限和权限。 请参阅用户和组同步

>[!NOTE]
>
>有关Adobe Identity Management基础知识（包括IDP配置）的详细信息，请参阅文章[本页。](https://helpx.adobe.com/cn/enterprise/using/set-up-identity.html)
>
>有关企业管理和[!DNL Admin Console]的详细信息，请参阅文章[本页](https://helpx.adobe.com/cn/enterprise/managing/user-guide.html)。

### 将用户加入[!DNL Admin Console] {#onboarding-users-to-the-admin-console}

根据客户的规模及其偏好，有三种登录用户的方法：

1. 在[!DNL Admin Console]中手动创建用户和用户组
1. 上传包含用户的CSV文件
1. 从客户的企业Active Directory同步用户和用户组。

#### 通过[!DNL Admin Console] UI {#manual-addition-through-admin-console-ui}手动添加

可以在[!DNL Admin Console] UI中手动创建用户和用户组。 如果用户数量不多，则可以使用此方法。 例如，少于50个AEM用户。

如果客户已经使用此方法管理其他Adobe产品(如Analytics、目标或Creative Cloud应用程序)，则还可以手动创建用户。

![image2018-9-23_20-39-9](assets/image2018-9-23_20-39-9.png)

#### 在[!DNL Admin Console] UI {#file-upload-in-the-admin-console-ui}中上载文件

为了轻松处理用户创建，可以上传CSV文件以批量添加用户：

![image2018-9-23_18-59-57](assets/image2018-9-23_18-59-57.png)

#### 用户同步工具 {#user-sync-tool}

用户同步工具（简称UST）使企业客户能够利用Active Directory或其他经测试的OpenLDAP目录服务创建或管理Adobe用户。 目标用户是IT身份管理员（企业目录和系统管理员），他们将能够安装和配置该工具。 开放源工具是可自定义的，因此客户可以让开发人员修改它以满足他们自己的特定要求。

当用户同步运行时，它会从组织的Active Directory（或任何其他兼容的数据源）中获取一列表用户，并将其与[!DNL Admin Console]中的用户列表进行比较。 然后，它调用Adobe[!DNL User Management] API，以便将[!DNL Admin Console]与组织的目录同步。 改变的流程完全是单向的；在[!DNL Admin Console]中所做的任何编辑不会推送到目录。

此工具允许系统管理员将客户目录中的用户组与[!DNL Admin Console]中的产品配置和用户组进行映射，而新的UST版本还允许动态创建[!DNL Admin Console]中的用户组。

要设置用户同步，组织需要创建一组凭据，其方式与使用[[!DNL User Management] API](https://www.adobe.io/apis/cloudplatform/usermanagement/docs/setup.html)相同。

![image2018-9-23_13-36-56](assets/image2018-9-23_13-36-56.png)

User Sync通过Adobe Github存储库分发，位于以下位置：

[https://github.com/adobe-apiplatform/user-sync.py/releases/latest](https://github.com/adobe-apiplatform/user-sync.py/releases/latest)

请注意，预发行版2.4RC1支持动态组创建，可在以下位置找到：[https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1)

此版本的主要功能是动态映射[!DNL Admin Console]中用户成员身份的新LDAP组，以及动态创建用户组。

有关新组功能的更多信息，请访问：

[https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration](https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration.md#additional-group-options)

>[!NOTE]
>
>有关用户同步工具的详细信息，请参阅[文档页面](https://adobe-apiplatform.github.io/user-sync.py/en/)。
>
>
>用户同步工具需要使用[此处](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html)描述的过程注册为Adobe I/O客户端UMAPI。
>
>Adobe I/O控制台文档可在[此处](https://www.adobe.io/apis/cloudplatform/console.html)找到。
>
>
>此[位置](https://www.adobe.io/apis/cloudplatform/umapi-new.html)涵盖用户同步工具使用的[!DNL User Management] API。

>[!NOTE]
>
>AEM IMS配置将由Adobe Managed Services团队处理。 但是，客户管理员可以根据自己的要求（例如“自动组成员关系”或“组映射”）修改它。 IMS客户端也将由您的Managed Services团队注册。

## 使用方法 {#how-to-use}

### 在[!DNL Admin Console] {#managing-products-and-user-access-in-admin-console}中管理产品和用户访问

客户产品管理员登录[!DNL Admin Console]后，将看到AEM Managed Services产品上下文的多个实例，如下所示：

![screen_shot_2018-09-17at105804pm](assets/screen_shot_2018-09-17at105804pm.png)

在此示例中，组织&#x200B;*AEM-MS-Onboard*&#x200B;有32个实例，这些实例跨不同的拓扑和环境，如Stage、Prod等。

![screen_shot_2018-09-17at105517pm](assets/screen_shot_2018-09-17at105517pm.png)

可以检查实例详细信息以标识实例：

![screen_shot_2018-09-17at105601pm](assets/screen_shot_2018-09-17at105601pm.png)

在每个Product Context实例下，都会有一个关联的Product用户档案。 此产品用户档案用于向用户和组分配访问权限。

![image2018-9-18_7-48-50](assets/image2018-9-18_7-48-50.png)

在本产品用户档案下添加的任何用户和用户组都将能够登录到该实例，如下例所示：

![screen_shot_2018-09-17at105623pm](assets/screen_shot_2018-09-17at105623pm.png)

### 登录AEM {#logging-into-aem}

#### 本地管理员登录{#local-admin-login}

AEM可以继续支持管理员用户的本地登录，因为登录屏幕具有在本地登录的选项：

![screen_shot_2018-09-18at121056am](assets/screen_shot_2018-09-18at121056am.png)

#### 基于 IMS 的登录 {#ims-based-login}

对于其他用户，只需在实例上配置 IMS 即可使用基于 IMS 的登录。用户将首先单击&#x200B;**使用Adobe**&#x200B;登录按钮，如下所示：

![image2018-9-18_0-10-32](assets/image2018-9-18_0-10-32.png)

然后，他们将被重定向到IMS登录屏幕并输入其凭据：

![screen_shot_2018-09-17at115629pm](assets/screen_shot_2018-09-17at115629pm.png)

如果在初始[!DNL Admin Console]设置过程中配置了联合IDP，则会将用户重定向到客户IDP以进行SSO。

IDP为Okta，如下例所示：

![screen_shot_2018-09-17at115734pm](assets/screen_shot_2018-09-17at115734pm.png)

身份验证完成后，用户将被重定向回 AEM 并登录：

![screen_shot_2018-09-18at120124am](assets/screen_shot_2018-09-18at120124am.png)

### 迁移现有用户{#migrating-existing-users}

对于使用其他身份验证方法并正在迁移到IMS的现有AEM实例，需要执行迁移步骤。

AEM存储库（通过LDAP或SAML在本地源）中的现有用户可以通过“用户迁移实用程序”迁移到IMS作为IDP。

此实用程序将由您的AMS团队作为IMS设置的一部分运行。

### 管理AEM {#managing-permissions-and-acls-in-aem}中的权限和ACL

访问控制和权限将继续在AEM中进行管理，这可以通过将来自IMS的用户组(例如下例中的AEM-GRP-008)与定义权限和访问控制的本地组分开来实现。 可以将从IMS同步的用户组分配给本地组并继承权限。

在以下示例中，我们将同步的组作为示例添加到本地 *Dam_Users* 组。

此处，用户也已分配到[!DNL Admin Console]中的几个组。 （请注意，用户和用户组可以使用用户同步工具从LDAP同步或在本地创建，请参阅上面&#x200B;[!DNL Admin Console]**的“入门用户”部分。）**

>[!NOTE]
>
>用户组仅在用户登录到实例时进行同步。

![screen_shot_2018-09-17at94207pm](assets/screen_shot_2018-09-17at94207pm.png)

用户是 IMS 中以下组的一部分：

![screen_shot_2018-09-17at94237pm](assets/screen_shot_2018-09-17at94237pm.png)

用户登录时，会同步其组成员资格，如下所示：

![screen_shot_2018-09-17at94033pm](assets/screen_shot_2018-09-17at94033pm.png)

在AEM中，从IMS同步的用户组可以作为成员添加到现有的本地组，例如DAM用户。

![screen_shot_2018-09-17at95804pm](assets/screen_shot_2018-09-17at95804pm.png)

如下所示，组&#x200B;*AEM-GRP_008*&#x200B;继承了DAM用户的权限和权限。 这是管理已同步组权限的有效方式，也常用于基于LDAP的身份验证方法。

![screen_shot_2018-09-17at110505pm](assets/screen_shot_2018-09-17at110505pm.png)
