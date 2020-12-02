---
title: 用户管理
seo-title: 用户管理
description: 用户管理允许您通过使用SAML在AEM表单模块和受Netegrity SiteMinder保护的应用程序之间启用SSO。 此文档提供有关用户管理的更多信息。
seo-description: 用户管理允许您通过使用SAML在AEM表单模块和受Netegrity SiteMinder保护的应用程序之间启用SSO。 此文档提供有关用户管理的更多信息。
uuid: f0c8331a-d995-483d-97b7-259df53b1a1a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 10e6177a-8228-4515-aba9-bbe59bede449
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 1%

---


# 用户管理 {#user-management}

用户管理允许您通过使用安全断言标记语言(SAML)在AEM表单模块和受Netegrity SiteMinder保护的应用程序之间启用单一登录(SSO)。 实施SSO时，AEM表单用户登录页面不是必需的，如果用户已通过公司门户进行身份验证，则不显示。

有关提高DB2的数据库和目录同步性能的信息，请参见[IBM DB2数据库：运行用于常规维护的命令](/help/forms/using/admin-help/ibm-db2-database-running-commands.md#ibm-db2-database-running-commands-for-regular-maintenance)。

## 为启用SSL的LDAP服务器{#configuring-user-management-for-an-ssl-enabled-ldap-server}配置用户管理

如果您有启用SSL的LDAP服务器，请配置“用户管理”以使用它。 （请参阅[为启用SSL的LDAP服务器配置用户管理](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server)。）

## 设置与文档安全{#setting-user-privileges-for-use-with-document-security}一起使用的用户权限

创建具有创建用户和组的适当权限的管理员用户。 如果您的AEM表单环境包含文档安全，则将管理已邀请用户和本地用户的权限授予这些用户的管理员用户。 此外，分配管理控制台用户角色，以向用户提供对管理控制台的访问权限。 （请参阅[创建和配置角色](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles)。）

要在策略用户搜索期间视图所选域中的用户和用户组，超级管理员或策略集管理员必须选择域（在用户管理中创建）并将其添加到创建的每个策略集的可见用户和组列表。

可见的用户和组列表对策略集协调器是可见的，用于限制最终用户在选择要添加到策略的用户或组时可以浏览的域。 如果未执行此任务，则策略集协调员将找不到要添加到策略的任何用户或组。 对于任何给定的策略集，都可以有多个策略集协调器。

>[!NOTE]
>
>必须先创建域，然后才能创建任何策略。

### 设置可见的用户和用户组{#set-visible-users-and-groups}

安装并配置AEM表单环境及文档安全后，请在“用户管理”中设置所有适当的域。

1. 在管理控制台中，单击“服务”>“文档安全”>“策略”，然后单击“策略集”选项卡。
1. 选择“全局策略集”，然后单击“可见的用户和用户组”选项卡。
1. 单击“添加域”，然后根据需要添加现有域。
1. 导航到服务>文档安全>配置>我的策略，然后单击可见的用户和用户组选项卡。
1. 单击“添加域”，然后根据需要添加现有域。

## 管理员用户限制{#administrator-user-restrictions}

具有某些类型管理员权限的用户出于安全原因无法访问Workspace最终用户网页。 由于这些网页可能存在于防火墙之外，因此允许管理级别的任务可能会带来安全风险。 只有具有“工作区管理员”或“工作区用户”权限的用户才能访问最终用户网页。

>[!NOTE]
>
>Flex工作区已弃用于AEM表单发布。

