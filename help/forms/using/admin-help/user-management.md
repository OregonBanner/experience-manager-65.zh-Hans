---
title: 用户管理
seo-title: User Management
description: 用户管理允许您使用SAML在AEM Forms模块和Netegrity SiteMinder保护的应用程序之间启用SSO。 本文档提供了有关用户管理的更多信息。
seo-description: User Management lets you enable SSO between AEM forms modules and Netegrity SiteMinder-protected applications by using SAML. This document provides more information about User Management.
uuid: f0c8331a-d995-483d-97b7-259df53b1a1a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 10e6177a-8228-4515-aba9-bbe59bede449
exl-id: 1da1f6de-ac0d-4e0d-b8bb-956420e42699
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# 用户管理 {#user-management}

用户管理允许您使用安全声明标记语言(SAML)，在AEM表单模块与受SiteMinder保护的联网应用程序之间启用单点登录(SSO)。 实施SSO时，AEM Forms用户登录页面不是必需的，并且如果用户已通过公司门户进行身份验证，则不会显示。

有关提高DB2的数据库和目录同步性能的信息，请参见 [IBM DB2数据库：运行命令以进行常规维护](/help/forms/using/admin-help/ibm-db2-database-running-commands.md#ibm-db2-database-running-commands-for-regular-maintenance).

## 为启用了SSL的LDAP服务器配置用户管理 {#configuring-user-management-for-an-ssl-enabled-ldap-server}

如果您具有启用了SSL的LDAP服务器，请配置“用户管理”以与它配合使用。 (请参阅 [为启用了SSL的LDAP服务器配置用户管理](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server).)

## 设置用于Document Security的用户权限 {#setting-user-privileges-for-use-with-document-security}

创建具有创建用户和组的相应权限的管理员用户。 如果您的AEM表单环境包含Document Security，请将管理受邀用户和本地用户的权限授予将成为这些用户管理员的用户。 还可以分配管理控制台用户角色，以便让用户能够访问管理控制台。 (请参阅 [创建和配置角色](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)

要在策略用户搜索期间查看所选域中的用户和组，超级管理员或策略集管理员必须选择域（在用户管理中创建）并将其添加到每个创建的策略集的可见用户和组列表中。

可见的用户和组列表对策略集协调器可见，用于限制最终用户选择要添加到策略中的用户或组时可以浏览的域。 如果未执行此任务，则策略集协调员将找不到任何要添加到策略中的用户或组。 任何给定的策略集都可以有多个策略集协调器。

>[!NOTE]
>
>必须先创建域，然后才能创建任何策略。

### 设置可见的用户和组 {#set-visible-users-and-groups}

使用Document Security安装和配置AEM表单环境后，请在“用户管理”中设置所有相应的域。

1. 在管理控制台中，单击“服务”>“Document Security”>“策略”，然后单击“策略集”选项卡。
1. 选择“全局策略集”，然后单击“可见用户和组”选项卡。
1. 单击添加域，并根据需要添加现有域。
1. 导航到“服务”>“Document Security”>“配置”>“我的策略”，然后单击“可见的用户和组”选项卡。
1. 单击添加域，并根据需要添加现有域。

## 管理员用户限制 {#administrator-user-restrictions}

出于安全原因，具有特定类型管理员权限的用户无法访问Workspace最终用户网页。 由于这些网页可能存在于防火墙之外，因此允许管理级任务可能会带来安全风险。 只有具有“工作区管理员”或“工作区用户”权限的用户才能访问最终用户网页。

>[!NOTE]
>
>AEM Forms版本弃用Flex工作区。
