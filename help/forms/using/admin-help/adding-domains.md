---
title: 添加域
seo-title: 添加域
description: 了解如何使用域管理设置和域名和ID的一般注意事项添加企业、本地或混合域。
seo-description: 了解如何使用域管理设置和域名和ID的一般注意事项添加企业、本地或混合域。
uuid: 3ae1e5d4-ea5b-4e0b-be97-3957c3702d5f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d4004ffe-c981-487d-b803-dc4492ae5998
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 0%

---


# 添加域{#adding-domains}

## 添加企业域{#add-an-enterprise-domain}

1. 在管理控制台中，单击设置>用户管理>域管理。
1. 单击“新建企业域”。
1. 在ID框中，键入域的唯一标识符，在“名称”框中，键入域的描述性名称。 （请参阅[域名和ID的重要注意事项](adding-domains.md#important-considerations-for-domain-names-and-ids)。）
1. 指定是否启用帐户锁定。 （请参阅[配置帐户锁定设置](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings)。） 默认情况下，“启用帐户锁定”处于选中状态。
1. 单击“添加身份验证”，然后在“身份验证提供程序”列表中，根据您的单位使用的身份验证机制选择一个提供程序。 可能的值包括LDAP、Kerberos、SAML或自定义身份验证提供程序。

   如果选择LDAP，则可以使用在目录配置中指定的LDAP服务器，也可以选择其他LDAP服务器进行身份验证。 如果选择其他服务器，则用户必须同时存在于两个LDAP服务器上。

1. 在页面上提供所需的任何其他信息。 （请参阅[身份验证设置](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings)。）
1. 添加目录或自定义服务提供商接口(SPI)。 （请参阅[添加目录或自定义SPI](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis)。）
1. 单击“完成”，然后单击“确定”。

创建企业域后，请在用户管理可以使用目录之前手动同步目录或创建触发器以执行同步。 然后，可以设置目录同步计划，并根据需要执行手动同步。 （请参阅[同步目录](/help/forms/using/admin-help/synchronizing-directories.md#synchronizing-directories)。）

## 添加本地域{#add-a-local-domain}

1. 在管理控制台中，单击设置>用户管理>域管理。
1. 单击“新建本地域”。
1. 在“ID”框中，键入域的唯一标识符，并在“名称”框中，键入域的描述性名称。 （请参阅[域名和ID的重要注意事项](adding-domains.md#important-considerations-for-domain-names-and-ids)。）
1. 指定是否启用帐户锁定，然后单击“确定”。 （请参阅[配置帐户锁定设置](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings)。） 默认情况下，“启用帐户锁定”处于选中状态。

## 添加混合域{#add-a-hybrid-domain}

1. 在管理控制台中，单击设置>用户管理>域管理。
1. 单击“新建混合域”。
1. 在“ID”框中，键入域的唯一标识符，并在“名称”框中，键入域的描述性名称。 （请参阅[域名和ID的重要注意事项](adding-domains.md#important-considerations-for-domain-names-and-ids)。）
1. 单击“添加身份验证”，然后在“身份验证提供程序”列表中，根据您的单位使用的身份验证机制选择一个提供程序。 可能的值包括LDAP、Kerberos、SAML或自定义身份验证提供程序。
1. 在页面上提供所需的任何其他信息。 （请参阅[身份验证设置](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings)。）
1. 单击“确定”，然后再次单击“确定”。

## 域名和ID {#important-considerations-for-domain-names-and-ids}的重要注意事项

在选择域名和ID时，请记住以下注意事项：

### 一般注意事项{#general-considerations}

* 当您使用数据库提供程序（非DB2）时，域ID最多可包含50个字节。 如果您使用单字节ASCII字符，则限制为50个字符。 如果域标识符包含多字节字符，则此限制会降低。 例如，如果创建的域的标识符包含3字节字符，则限制为16个字符。 此外，不能创建包含4字节字符的域。 如果创建的域ID超过此限制，AEM表单将处于不稳定状态。 要从此不稳定状态中恢复，请参阅本页上的“删除包含扩展或多字节字符[的域”。](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)
* 可在AEM表单中创建的企业域和本地域的数量取决于每个域ID的长度。 在添加企业或混合域时，用户管理会更新AEM表单配置文件(config.xml)的AuthProviders节点中的configInstance字符串。 configInstance字符串包含与授权提供程序关联的所有域的绝对路径的冒号分隔列表。 此字符串的大小限制为8192个字符。 当达到该限制时，无法创建其他域。

### 使用DB2 {#considerations-when-using-db2}时的注意事项

对AEM表单数据库使用DB2时，域ID的最大允许长度取决于使用的字符类型：

* 100个单字节(ASCII)（例如，英语、法语或德语中使用的字符）
* 50个多次字节（例如，中文、日语或朝鲜语使用的字符）
* 25个四字节（例如，繁体中文中使用的字符）

### 使用MySQL {#considerations-when-using-mysql}时的注意事项

将MySQL用作AEM表单数据库时，有以下限制：

* 域ID和域名仅使用单字节(ASCII)字符。 如果使用扩展ASCII字符，AEM表单将处于不稳定状态，并且如果尝试删除域，可能会引发异常。 要从这种不稳定状态中恢复，请参阅本页上的“删除包含扩展或多字节字符[的域”主题。](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)
* 不能创建两个名称相同但大小写不同的域。 例如，当名为&#x200B;*adobe*&#x200B;的域已存在时，尝试创建名为&#x200B;*Adobe*&#x200B;的域会导致错误。
* 用户管理不能区分两个域名，这两个域名仅在使用扩展字符时有所不同。 例如，如果创建名为&#x200B;*abcde*&#x200B;的域和名为&#x200B;*âbcdè*&#x200B;的域，则它们被视为相同。

### 删除包含扩展或多字节字符{#remove-a-domain-that-contains-extended-or-multi-byte-characters}的域

1. 导出配置文件，如[导入和导出配置文件](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)中所述。
1. 打开配置文件，在“域”节点下，找到名称属性与使用扩展或多字节字符创建的域名称相匹配的节点。 删除与该域相关的整个节点。
1. 在数据库中，在edgeprincipaldomainentity表中搜索域：

   * 从edcprincipaldomainentity中选择`*`。
   * 查找包含扩展或多字节字符的域名，并将其状态设置为OBSOLETE。

1. 导入更新的配置文件，如[导入和导出配置文件](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)中所述。

