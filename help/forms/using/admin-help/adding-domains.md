---
title: 添加域
description: 了解如何使用域管理设置以及域名和ID的一般注意事项来添加企业、本地或混合域。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c708936d-7aa7-4b92-be2d-d97008f187d2
source-git-commit: 3885cc51f7e821cdb352737336a29f9c4f0c2f41
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 0%

---

# 添加域 {#adding-domains}

## 添加企业域 {#add-an-enterprise-domain}

1. 在管理控制台中，单击设置>用户管理>域管理。
1. 单击新建企业域。
1. 在ID框中，键入域的唯一标识符，然后在“名称”框中，键入域的描述性名称。 (请参阅 [有关域名和ID的重要注意事项](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. 指定是否启用帐户锁定。 (请参阅 [配置帐户锁定设置](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings).) 默认情况下，“启用帐户锁定”处于选中状态。
1. 单击添加验证，然后在“验证提供方”列表中选择一个提供方，具体取决于您的组织使用的验证机制。 可能的值包括LDAP、Kerberos、SAML或自定义身份验证提供程序。

   如果选择LDAP，可以使用目录配置中指定的LDAP服务器，也可以选择其他LDAP服务器用于身份验证。 如果选择其他服务器，您的用户必须存在于两个LDAP服务器上。

1. 在页面上提供所需的任何其他信息。 (请参阅 [身份验证设置](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. 添加目录或自定义服务提供者接口(SPI)。 (请参阅 [添加目录或自定义SPI](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
1. 单击“Finish（完成）” ，然后单击“OK（确定）”。

创建企业域后，手动同步目录或创建触发器以执行同步，然后User Management才能使用它。 然后，可以设置目录同步计划并根据需要执行手动同步。 (请参阅 [同步目录](/help/forms/using/admin-help/synchronizing-directories.md#synchronizing-directories).)

## 添加本地域 {#add-a-local-domain}

1. 在管理控制台中，单击设置>用户管理>域管理。
1. 单击“新建本地域”。
1. 在ID框中，键入域的唯一标识符，然后在“名称”框中，键入域的描述性名称。 (请参阅 [有关域名和ID的重要注意事项](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. 指定是否启用帐户锁定，然后单击确定。 (请参阅 [配置帐户锁定设置](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings).) 默认情况下，“启用帐户锁定”处于选中状态。

## 添加混合域 {#add-a-hybrid-domain}

1. 在管理控制台中，单击设置>用户管理>域管理。
1. 单击“新建混合域”。
1. 在ID框中，键入域的唯一标识符，然后在“名称”框中，键入域的描述性名称。 (请参阅 [有关域名和ID的重要注意事项](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. 单击添加验证，然后在“验证提供方”列表中选择一个提供方，具体取决于您的组织使用的验证机制。 可能的值包括LDAP、Kerberos、SAML或自定义身份验证提供程序。
1. 在页面上提供所需的任何其他信息。 (请参阅 [身份验证设置](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. 单击“确定”，然后再次单击“确定”。

## 有关域名和ID的重要注意事项 {#important-considerations-for-domain-names-and-ids}

选择域名和ID时，请牢记以下注意事项：

### 一般注意事项 {#general-considerations}

* 当您使用DB2以外的数据库提供程序时，域ID最多可包含50字节。 如果使用单字节ASCII字符，则限制为50个字符。 如果域标识符包含多字节字符，则此限制会降低。 例如，如果创建的域标识符包含3字节字符，则限制为16个字符。 此外，不能创建包含4字节字符的域。 如果您创建的域ID超过此限制，则AEM表单将处于不稳定状态。 要从这种不稳定状态中恢复，请参见“ [删除包含扩展字符或多字节字符的域](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)”。
* 可以在AEM表单中创建的企业域和本地域的数量取决于每个域ID的长度。 添加企业域或混合域时，“用户管理”会更新AEM Forms配置文件(config.xml)的AuthProviders节点中的configInstance字符串。 configInstance字符串包含与授权提供程序关联的所有域的绝对路径列表（以冒号分隔）。 此字符串的大小限制为8192个字符。 当达到该限制时，您将无法创建其他域。

### 使用DB2时的注意事项 {#considerations-when-using-db2}

为AEM forms数据库使用DB2时，允许的最大域ID长度取决于使用的字符类型：

* 100个单字节(ASCII)（例如，使用英语、法语或德语字符）
* 50双字节（例如，用于中文、日语或韩语的字符）
* 25个四字节（例如，繁体中文中使用的字符）

### 使用MySQL时的注意事项 {#considerations-when-using-mysql}

将MySQL用作AEM表单数据库时，以下限制适用：

* 域ID和域名仅使用单字节(ASCII)字符。 如果您使用扩展ASCII字符，AEM表单将处于不稳定状态，并且在您尝试删除域时可能会引发异常。 要从这种不稳定状态中恢复，请参见“ [删除包含扩展字符或多字节字符的域](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)”主题。
* 您不能创建两个同名但大小写不同的域。 例如，尝试创建名为的域 *Adobe* 当域名为 *adobe* 已存在导致错误。
* “用户管理”无法区分仅在使用扩展字符时不同的两个域名。 例如，如果您创建一个名为 *abcde* 和名为的域 *abcde*，则它们被视为相同。

### 删除包含扩展字符或多字节字符的域 {#remove-a-domain-that-contains-extended-or-multi-byte-characters}

1. 导出配置文件，如中所述 [导入和导出配置文件](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).
1. 打开配置文件，在“域”节点下，找到其名称属性与使用扩展字符或多字节字符创建的域名称相匹配的节点。 删除与该域相关的整个节点。
1. 在数据库中，在edcparcipaldomainentity表中搜索域：

   * 选择 `*` 从edcparcipaldomainentity。
   * 查找包含扩展字符或多字节字符的域名，并将其状态设置为OBSOLETE。

1. 导入更新的配置文件，如中所述 [导入和导出配置文件](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).
