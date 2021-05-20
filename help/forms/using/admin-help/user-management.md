---
title: 用户管理
seo-title: 用户管理
description: 用户管理允许您使用SAML在AEM表单模块与受Netegrity SiteMinder保护的应用程序之间启用单点登录。 本文档提供了有关“用户管理”的详细信息。
seo-description: 用户管理允许您使用SAML在AEM表单模块与受Netegrity SiteMinder保护的应用程序之间启用单点登录。 本文档提供了有关“用户管理”的详细信息。
uuid: f0c8331a-d995-483d-97b7-259df53b1a1a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 10e6177a-8228-4515-aba9-bbe59bede449
exl-id: 1da1f6de-ac0d-4e0d-b8bb-956420e42699
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 1%

---

# 用户管理 {#user-management}

用户管理允许您使用安全断言标记语言(SAML)在AEM表单模块和受Netegrity SiteMinder保护的应用程序之间启用单点登录(SSO)。 实施SSO后，无需AEM Forms用户登录页面，如果用户已通过公司门户进行身份验证，则不会显示SSO。

有关提高DB2的数据库和目录同步性能的信息，请参阅[IBM DB2数据库：正在运行用于常规维护的命令](/help/forms/using/admin-help/ibm-db2-database-running-commands.md#ibm-db2-database-running-commands-for-regular-maintenance)。

## 为启用SSL的LDAP服务器{#configuring-user-management-for-an-ssl-enabled-ldap-server}配置用户管理

如果您有启用SSL的LDAP服务器，请配置“用户管理”以使用该服务器。 （请参阅[为启用SSL的LDAP服务器配置用户管理](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server)。）

## 设置用于Document Security {#setting-user-privileges-for-use-with-document-security}的用户权限

创建具有创建用户和组的适当权限的管理员用户。 如果您的AEM表单环境包含“文档安全”，请将管理受邀用户和本地用户的权限授予用户，该用户将是这些用户的管理员。 此外，还分配管理控制台用户角色，以向用户提供对管理控制台的访问权限。 （请参阅[创建和配置角色](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles)。）

要在策略用户搜索期间查看选定域中的用户和组，超级管理员或策略集管理员必须选择域（在用户管理中创建）并将其添加到每个已创建策略集的可见用户和组列表中。

可见的用户和组列表对策略集协调器可见，用于限制最终用户在选择要添加到策略的用户或组时可以浏览的域。 如果未执行此任务，则策略集协调器将找不到要添加到策略的任何用户或组。 任何给定策略集都可以有多个策略集协调器。

>[!NOTE]
>
>必须先创建域，然后才能创建任何策略。

### 设置可见用户和组{#set-visible-users-and-groups}

使用文档安全安装和配置AEM表单环境后，请在“用户管理”中设置所有相应的域。

1. 在管理控制台中，单击“服务”>“文档安全”>“策略”，然后单击“策略集”选项卡。
1. 选择全局策略集，然后单击可见的用户和组选项卡。
1. 单击添加域，然后根据需要添加现有域。
1. 导航至服务>文档安全>配置>我的策略，然后单击可见的用户和组选项卡。
1. 单击添加域，然后根据需要添加现有域。

## 管理员用户限制{#administrator-user-restrictions}

出于安全原因，具有某些类型管理员权限的用户无法访问工作区最终用户网页。 由于这些网页可以存在于防火墙之外，因此允许管理级别的任务可能会带来安全风险。 只有具有工作区管理员或工作区用户权限的用户才能访问最终用户网页。

>[!NOTE]
>
>AEM Forms版本已弃用Flex Workspace。
