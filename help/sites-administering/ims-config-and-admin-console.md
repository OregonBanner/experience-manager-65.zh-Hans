---
title: 针对AEM Managed services的Adobe IMS身份验证和Admin Console支持
seo-title: 针对AEM Managed services的Adobe IMS身份验证和Admin Console支持
description: 了解如何在AEM中使用Admin Console。
seo-description: 了解如何在AEM中使用Admin Console。
uuid: 3f5b32c7-cf62-41a4-be34-3f71bbf224eb
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f6112dea-a1eb-4fd6-84fb-f098476deab7
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# 针对AEM Managed services的Adobe IMS身份验证和Admin Console支持 {#adobe-ims-authentication-and-admin-console-support-for-aem-managed-services}

>[!NOTE]
>
>请注意，此功能仅对Adobe Managed services客户可用。

## 简介 {#introduction}

AEM 6.4.3.0为AEM Managed services客户引入了对AEM实例和基于Adobe IMS（标识管理系统）的身份验证的Admin Console **支持** 。

AEM登录到Admin Console后，AEM Managed services客户可以在一个控制台中管理所有Experience cloud用户。 用户和用户组可以分配到与AEM实例关联的产品配置文件，以便他们登录到特定实例。

## 主要亮点 {#key-highlights}

* AEM IMS身份验证支持仅针对AEM作者、管理员或开发人员，不针对客户站点（如站点访问者）的外部最终用户
* Admin Console将AEM Managed services客户表示为IMS组织，其实例表示为产品上下文。 客户系统和产品管理员将能够管理对实例的访问
* AEM Managed services将客户拓扑与Admin Console同步。 在管理控制台中，每个实例将有一个AEM Managed services产品上下文实例。
* Admin Console中的产品配置将决定用户可以访问的实例
* 支持使用客户自己的符合SAML 2规范的标识提供者的联合身份验证
* 仅支持Enterprise ID或Federated ID（客户单点登录），不支持个人Adobe ID。
* 用户管理（在Adobe Admin Console中）将继续归客户管理员所有。

## 架构 {#architecture}

IMS身份验证通过在AEM和Adobe IMS端点之间使用OAuth协议来工作。 将用户添加到IMS并拥有Adobe Identity后，他们便可以使用IMS凭据登录到AEM Managed services实例。

用户登录流程如下所示，用户将被重定向到IMS，或者被重定向到客户IDP进行SSO验证，然后被重定向回AEM。

![image2018-9-23_23-55-8](assets/image2018-9-23_23-55-8.png)

## 如何设置 {#how-to-set-up}

### 将组织载入Admin Console {#onboarding-organizations-to-admin-console}

使用Adobe IMS进行AEM身份验证的先决条件是客户上次使用Admin Console。

作为第一步，客户应在Adobe IMS中配置组织。 Adobe Enterprise客户在 [Adobe Admin Console中表示为IMS组织](https://helpx.adobe.com/enterprise/using/admin-console.html)。

AEM Managed services客户应已配置组织，作为IMS配置的一部分，客户实例将在管理控制台中提供，用于管理用户权利和访问权限。

转向IMS进行用户身份验证将是AMS和客户之间的共同努力，每个客户都有自己的工作流程要完成。

一旦客户作为IMS组织存在并且AMS完成了为IMS为客户提供的配置，这就是所需配置工作流程的摘要：

![image2018-9-23_23-33-25](assets/image2018-9-23_23-33-25.png)

1. 指定的系统管理员将收到登录到Admin Console的邀请
1. 系统管理员声明域，用于确认域的所有权（在此示例中为acme.com）
1. 系统管理员设置用户目录
1. 系统管理员在管理控制台中配置标识提供者(IDP)以进行SSO设置。
1. AEM管理员会像往常一样管理本地用户组、权限和权限。 请参阅用户和用户组同步

>[!NOTE]
>
>有关Adobe Identity Management基础知识（包括IDP配置）的详细信息，请参阅 [本页文章。](https://helpx.adobe.com/enterprise/using/set-up-identity.html)
>
>有关Enterprise Administration和Admin Console的详细信息，请参阅本 [页文章](https://helpx.adobe.com/enterprise/managing/user-guide.html)。

### 将用户载入Admin Console {#onboarding-users-to-the-admin-console}

根据客户的规模和偏好，可通过三种方式建立用户：

1. 在Admin Console中手动创建用户和用户组
1. 上传包含用户的CSV文件
1. 从客户的企业Active Directory中同步用户和用户组。

#### 通过Admin Console UI手动添加 {#manual-addition-through-admin-console-ui}

用户和用户组可以在Admin Console UI中手动创建。 如果用户数不多，则可以使用此方法。 例如，少于50个AEM用户。

如果客户已使用此方法管理其他Adobe产品（如Analytics、Target或Creative cloud应用程序），则还可以手动创建用户。

![image2018-9-23_20-39-9](assets/image2018-9-23_20-39-9.png)

#### 在管理控制台UI中上传文件 {#file-upload-in-the-admin-console-ui}

为便于用户创建，可以上传CSV文件以批量添加用户：

![image2018-9-23_18-59-57](assets/image2018-9-23_18-59-57.png)

#### 用户同步工具 {#user-sync-tool}

用户同步工具（简称UST）使企业客户能够使用Active Directory或其他经测试的OpenLDAP目录服务创建或管理Adobe用户。 目标用户是IT标识管理员（企业目录和系统管理员），他们将能够安装和配置该工具。 开放源代码工具可自定义，这样客户就可以让开发人员修改它，以满足他们自己的特定要求。

当用户同步运行时，它会从组织的Active Directory（或任何其他兼容数据源）中获取用户列表，并将其与Admin Console中的用户列表进行比较。 然后，它调用Adobe用户管理API，以便Admin Console与组织的目录同步。 改变的流程完全是单向的；在Admin Console中所做的任何编辑不会推送到该目录。

此工具允许系统管理员将客户目录中的用户组与Admin Console中的产品配置和用户组进行映射，新的UST版本还允许在Admin Console中动态创建用户组。

要设置用户同步，组织需要创建一组凭据，其方式与使用用户管理API [的方式相同](https://www.adobe.io/apis/cloudplatform/usermanagement/docs/setup.html)。

![image2018-9-23_13-36-56](assets/image2018-9-23_13-36-56.png)

用户同步通过Adobe Github存储库分发，位于以下位置：

[https://github.com/adobe-apiplatform/user-sync.py/releases/latest](https://github.com/adobe-apiplatform/user-sync.py/releases/latest)

请注意，预发行版2.4RC1支持动态组创建，可在以下网址找到： [https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1)

此版本的主要功能是能够在Admin Console中动态地映射新的LDAP用户组以作为用户成员，以及创建动态用户组。

有关新组功能的更多信息，请访问：

[https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration](https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration.md#additional-group-options)

>[!NOTE]
>
>有关用户同步工具的详细信息，请参阅文 [档页面](https://adobe-apiplatform.github.io/user-sync.py/en/)。
>
>
>用户同步工具需要按照此处描述的过程注册为Adobe I/O客户端UMAPI [](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html)。
>
>Adobe I/O控制台文档可在此处找 [到](https://www.adobe.io/apis/cloudplatform/console.html)。
>
>
>用户同步工具使用的用户管理API在此位置被 [介绍](https://www.adobe.io/apis/cloudplatform/umapi-new.html)。

>[!NOTE]
>
>AEM IMS配置将由Adobe Managed services团队处理。 但是，客户管理员可以根据其要求修改它（例如“自动用户组成员关系”或“用户组映射”）。 IMS客户端也将由您的托管服务团队进行注册。

## 使用方法 {#how-to-use}

### 在Admin Console中管理产品和用户访问 {#managing-products-and-user-access-in-admin-console}

当客户产品管理员登录到Admin Console时，他们将看到AEM Managed Services产品上下文的多个实例，如下所示：

![screen_shot_2018-09-17at105804pm](assets/screen_shot_2018-09-17at105804pm.png)

在此示例中，组织 *AEM-MS-Onboard有* 32个实例，这些实例跨不同的拓扑和环境（如Stage、Prod等）。

![screen_shot_2018-09-17at105517pm](assets/screen_shot_2018-09-17at105517pm.png)

可以检查实例详细信息以标识该实例：

![screen_shot_2018-09-17at105601pm](assets/screen_shot_2018-09-17at105601pm.png)

在每个Product Context实例下，将有一个关联的Product Profile。 此产品配置文件用于为用户和组分配访问权限。

![image2018-9-18_7-48-50](assets/image2018-9-18_7-48-50.png)

在此产品配置文件下添加的任何用户和用户组都将能够登录到该实例，如下例所示：

![screen_shot_2018-09-17at105623pm](assets/screen_shot_2018-09-17at105623pm.png)

### 登录AEM {#logging-into-aem}

#### 本地管理员登录名 {#local-admin-login}

AEM可以继续支持管理员用户的本地登录，因为登录屏幕有一个用于本地登录的选项：

![screen_shot_2018-09-18at121056am](assets/screen_shot_2018-09-18at121056am.png)

#### 基于IMS的登录 {#ims-based-login}

对于其他用户，一旦在实例上配置了IMS，就可以使用基于IMS的登录。 用户将首先单击“使 **用Adobe登录** ”按钮，如下所示：

![image2018-9-18_0-10-32](assets/image2018-9-18_0-10-32.png)

然后，他们将被重定向到IMS登录屏幕并输入其凭据：

![screen_shot_2018-09-17at115629pm](assets/screen_shot_2018-09-17at115629pm.png)

如果在初始Admin Console设置过程中配置了联合IDP，则用户将被重定向到客户IDP以进行SSO。

IDP为Okta，如下例所示：

![screen_shot_2018-09-17at115734pm](assets/screen_shot_2018-09-17at115734pm.png)

身份验证完成后，用户将被重定向回AEM并登录：

![screen_shot_2018-09-18at120124am](assets/screen_shot_2018-09-18at120124am.png)

### 迁移现有用户 {#migrating-existing-users}

对于使用其他身份验证方法并正在迁移到IMS的现有AEM实例，需要执行迁移步骤。

AEM存储库（通过LDAP或SAML本地源）中的现有用户可以使用用户迁移实用程序迁移到IMS作为IDP。

此实用程序将由AMS团队作为IMS配置的一部分运行。

### 管理AEM中的权限和ACL {#managing-permissions-and-acls-in-aem}

在AEM中将继续管理访问控制和权限，这可以通过使用来自IMS的用户组（例如，以下示例中的AEM-GRP-008）和定义权限和访问控制的本地组来实现。 可以将从IMS同步的用户组分配给本地用户组并继承权限。

在以下示例中，我们将同步的组添加到本地 *Dam_Users* 组作为示例。

此处，用户也已分配到管理控制台中的几个组。 (请注意，用户和用户组可以使用用户同步工具从LDAP同步或在本地创建，请参阅上述“ **Admin Console入门用户”部分** )。

&amp;ast；请注意，用户组仅在登录实例时才会同步，对于拥有大量用户和用户组的客户，AMS可以运行组同步实用程序以预取组，以进行上述访问控制和权限管理。

![screen_shot_2018-09-17at94207pm](assets/screen_shot_2018-09-17at94207pm.png)

用户是IMS中以下组的一部分：

![screen_shot_2018-09-17at94237pm](assets/screen_shot_2018-09-17at94237pm.png)

用户登录时，会同步其用户组成员关系，如下所示：

![screen_shot_2018-09-17at94033pm](assets/screen_shot_2018-09-17at94033pm.png)

在AEM中，可以将从IMS同步的用户组作为成员添加到现有的本地组，例如DAM用户。

![screen_shot_2018-09-17at95804pm](assets/screen_shot_2018-09-17at95804pm.png)

如下所示，组 *AEM-GRP_008* 会继承DAM用户的权限和权限。 这是管理已同步组权限的有效方法，也常用于基于LDAP的身份验证方法。

![screen_shot_2018-09-17at110505pm](assets/screen_shot_2018-09-17at110505pm.png)

