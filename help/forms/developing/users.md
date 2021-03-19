---
title: 管理用户
seo-title: 管理用户
description: 使用用户管理API创建客户端应用程序，这些应用程序可以管理角色、权限和主体（可以是用户或用户组）以及验证用户身份。
seo-description: 使用用户管理API创建客户端应用程序，这些应用程序可以管理角色、权限和主体（可以是用户或用户组）以及验证用户身份。
uuid: 68d8a0bc-6e3d-4286-ba5c-534dcf58cb84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 95804bff-9e6f-4807-aae4-790bd9e7cb57
role: 开发人员
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '6258'
ht-degree: 0%

---


# 管理用户{#managing-users}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

**关于用户管理**

您可以使用用户管理API创建客户端应用程序，这些应用程序可以管理角色、权限和承担者（可以是用户或用户组）以及验证用户身份。 用户管理API包含以下AEM Forms API:

* 目录管理器服务API
* Authentication Manager Service API
* Authorization Manager Service API

用户管理允许您分配、删除和确定角色和权限。 它还允许您分配、删除和查询域、用户和用户组。 最后，您可以使用“用户管理”对用户进行身份验证。

在[添加用户](users.md#adding-users)中，您将了解如何以编程方式添加用户。 本节使用目录管理器服务API。

在[删除用户](users.md#deleting-users)中，您将了解如何以编程方式删除用户。 本节使用目录管理器服务API。

在[管理用户和用户组](users.md#managing-users-and-groups)中，您将了解本地用户与目录用户之间的区别，并查看如何使用Java和Web服务API以编程方式管理用户和组的示例。 本节使用目录管理器服务API。

在[管理角色和权限](users.md#managing-roles-and-permissions)中，您将了解系统角色和权限以及您可以通过编程方式增强这些角色和权限的方法，并查看如何使用Java和Web服务API以编程方式管理角色和权限的示例。 本节同时使用目录管理器服务API和授权管理器服务API。

在[验证用户](users.md#authenticating-users)中，您将看到如何使用Java和Web服务API以编程方式验证用户身份的示例。 本节使用Authorization Manager Service API。

**了解身份验证过程**

“用户管理”提供内置的身份验证功能，还允许您将其与自己的身份验证提供程序连接。 当用户管理收到身份验证请求（例如，用户尝试登录）时，会将用户信息传递给身份验证提供者以进行身份验证。 用户管理在验证用户后从身份验证提供程序接收结果。

下图显示了尝试登录的最终用户、用户管理和身份验证提供程序之间的交互。

![mu_mu_umauth_process](assets/mu_mu_umauth_process.png)

下表描述了身份验证过程的每个步骤。

<table>
 <thead>
  <tr>
   <th><p>步骤</p></th>
   <th><p>描述</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>用户尝试登录调用用户管理的服务。 用户指定用户名和密码。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>用户管理会将用户名和密码以及配置信息发送给身份验证提供程序。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>身份验证提供程序连接到用户存储并对用户进行身份验证。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>身份验证提供程序会将结果返回给用户管理。</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>用户管理允许用户登录或拒绝对产品的访问。</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>如果服务器时区与客户端时区不同，则在WebSphere Application Server群集上使用.NET客户端在本机SOAP堆栈上使用AEM Forms的WSDL生成PDF服务时，可能会发生以下用户管理身份验证错误：

`[com.adobe.idp.um.webservices.WSSecurityHandler] errorCode:12803 errorCodeHEX:0x3203 message:WSSecurityHandler: UM authenticate returns exception : An error was discovered processing the <wsse:Security> header. (WSSecurityEngine: Invalid timestamp The security semantics of message have expired).`

**了解目录管理**

用户管理与支持到LDAP目录的连接的目录服务提供商(DirectoryManagerService)打包。 如果您的单位使用非LDAP存储库存储用户记录，则可以创建您自己的与存储库一起使用的目录服务提供商。

目录服务提供商应用户管理的请求从用户存储中检索记录。 用户管理会定期将用户和组记录缓存到数据库中，以提高性能。

目录服务提供商可用于将用户管理数据库与用户存储同步。 此步骤可确保所有用户目录信息以及所有用户和组记录都是最新的。

此外，DirectoryManagerService还允许您创建和管理域。 域定义不同的用户群。 域的边界通常根据组织的结构或用户存储的设置来定义。 用户管理域提供身份验证提供者和目录服务提供商使用的配置设置。

在用户管理导出的配置XML中，属性值为`Domains`的根节点包含为用户管理定义的每个域的XML元素。 这些元素中的每个元素都包含定义与特定服务提供商关联的域的各个方面的其他元素。

**了解objectSID值**

使用Active Directory时，请务必了解`objectSID`值不是跨多个域的唯一属性。 此值存储对象的安全标识符。 在多域环境（例如，域树）中，`objectSID`值可以不同。

如果将对象从一个Active Directory域移动到另一个域，则`objectSID`值将发生更改。 某些对象在域中的任意位置具有相同的`objectSID`值。 例如，BUILTIN\Administrators、BUILTIN\Power Users等组无论域如何，都具有相同的`objectSID`值。 这些`objectSID`值已知。

## 添加用户{#adding-users}

可以使用目录管理器服务API（Java和Web服务）以编程方式将用户添加到AEM Forms。 添加用户后，在执行需要用户的服务操作时，可以使用该用户。 例如，您可以为新用户分配任务。

### 步骤{#summary-of-steps}的摘要

要添加用户，请执行以下步骤：

1. 包括项目文件。
1. 创建DirectoryManagerService客户端。
1. 定义用户信息。
1. 将用户添加到AEM Forms。
1. 验证是否已添加用户。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请包含代理文件。

**创建DirectoryManagerService客户端**

在以编程方式执行目录管理器服务操作之前，请先创建目录管理器服务API客户端。

**定义用户信息**

使用目录管理器服务API添加新用户时，请为该用户定义信息。 通常，在添加新用户时，您定义以下值：

* **域名**:用户所属的域(例如 `DefaultDom`)。
* **用户标识符值**:用户的标识符值(例如， `wblue`)。
* **主体类型**:用户的类型(例如，您可以指定 `USER)`。
* **给定名称**:用户的指定名称(例如 `Wendy`)。
* **姓氏**:用户的系列名称(例如 `Blue)`。
* **区域设置**:用户的区域设置信息。

**将用户添加到AEM Forms**

定义用户信息后，可以将用户添加到AEM Forms。 要添加用户，请调用`DirectoryManagerServiceClient`对象的`createLocalUser`方法。

**验证是否已添加用户**

您可以验证是否已添加用户，以确保未出现任何问题。 使用用户标识符值查找新用户。

**另请参阅**

[使用Java API添加用户](users.md#add-users-using-the-java-api)

[使用Web服务API添加用户](users.md#add-users-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[删除用户](users.md#deleting-users)

### 使用Java API {#add-users-using-the-java-api}添加用户

使用目录管理器服务API(Java)添加用户：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-usermanager-client.jar。

1. 创建DirectoryManagerServices客户端。

   使用`DirectoryManagerServiceClient`对象的构造函数并传递包含连接属性的`ServiceClientFactory`对象，创建对象。

1. 定义用户信息。

   * 使用`UserImpl`对象的构造函数创建对象。
   * 通过调用`UserImpl`对象的`setDomainName`方法来设置demain名称。 传递指定域名的字符串值。
   * 通过调用`UserImpl`对象的`setPrincipalType`方法来设置主体类型。 传递指定用户类型的字符串值。 例如，可以指定`USER`。
   * 通过调用`UserImpl`对象的`setUserid`方法设置用户标识符值。 传递指定用户标识符值的字符串值。 例如，可以指定`wblue`。
   * 通过调用`UserImpl`对象的`setCanonicalName`方法设置规范名称。 传递一个指定用户规范名称的字符串值。 例如，可以指定`wblue`。
   * 通过调用`UserImpl`对象的`setGivenName`方法来设置给定名称。 传递一个字符串值，它指定用户的给定名称。 例如，可以指定`Wendy`。
   * 通过调用`UserImpl`对象的`setFamilyName`方法来设置系列名称。 传递一个字符串值，它指定用户的族名。 例如，可以指定`Blue`。

   >[!NOTE]
   >
   >调用属于`UserImpl`对象的方法以设置其他值。 例如，可以通过调用`UserImpl`对象的`setLocale`方法来设置区域设置值。

1. 将用户添加到AEM Forms。

   调用`DirectoryManagerServiceClient`对象的`createLocalUser`方法并传递以下值：

   * 表示新用户的`UserImpl`对象
   * 表示用户密码的字符串值

   `createLocalUser`方法返回指定本地用户标识符值的字符串值。

1. 验证是否已添加用户。

   * 使用`PrincipalSearchFilter`对象的构造函数创建对象。
   * 通过调用`PrincipalSearchFilter`对象的`setUserId`方法设置用户标识符值。 传递表示用户标识符值的字符串值。
   * 调用`DirectoryManagerServiceClient`对象的`findPrincipals`方法并传递`PrincipalSearchFilter`对象。 此方法返回一个`java.util.List`实例，其中每个元素都是一个`User`对象。 遍历`java.util.List`实例以找到用户。

**另请参阅**

[步骤摘要](users.md#summary-of-steps)

[快速开始（SOAP模式）：使用Java API添加用户](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-adding-users-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#add-users-using-the-web-service-api}添加用户

使用目录管理器服务API（Web服务）添加用户：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保对服务引用使用以下WSDL定义：`http://localhost:8080/soap/services/DirectoryManagerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建DirectoryManagerService客户端。

   * 使用`DirectoryManagerServiceClient`对象的默认构造函数创建对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`DirectoryManagerServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如`http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`）。 您无需使用`lc_version`属性。 在创建服务引用时使用此属性。 确保指定`?blob=mtom`。
   * 通过获取`DirectoryManagerServiceClient.Endpoint.Binding`字段的值，创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 为字段`DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`DirectoryManagerServiceClient.ClientCredentials.UserName.Password`分配相应的密码值。
      * 将常量值`HttpClientCredentialType.Basic`赋给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`赋给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 定义用户信息。

   * 使用`UserImpl`对象的构造函数创建对象。
   * 通过为`UserImpl`对象的`domainName`字段指定字符串值来设置demain名称。
   * 通过为`UserImpl`对象的`principalType`字段指定字符串值来设置主体类型。 例如，可以指定`USER`。
   * 通过为`UserImpl`对象的`userid`字段分配字符串值来设置用户标识符值。
   * 通过为`UserImpl`对象的`canonicalName`字段指定字符串值来设置规范名称值。
   * 通过为`UserImpl`对象的`givenName`字段指定字符串值来设置给定的名称值。
   * 通过为`UserImpl`对象的`familyName`字段指定字符串值来设置系列名称值。

1. 将用户添加到AEM Forms。

   调用`DirectoryManagerServiceClient`对象的`createLocalUser`方法并传递以下值：

   * 表示新用户的`UserImpl`对象
   * 表示用户密码的字符串值

   `createLocalUser`方法返回指定本地用户标识符值的字符串值。

1. 验证是否已添加用户。

   * 使用`PrincipalSearchFilter`对象的构造函数创建对象。
   * 通过为`PrincipalSearchFilter`对象的`userId`字段分配表示用户标识符值的字符串值来设置用户的用户标识符值。
   * 调用`DirectoryManagerServiceClient`对象的`findPrincipals`方法并传递`PrincipalSearchFilter`对象。 此方法返回一个`MyArrayOfUser`集合对象，其中每个元素都是一个`User`对象。 遍历`MyArrayOfUser`集合以找到用户。

**另请参阅**

[步骤摘要](users.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 删除用户{#deleting-users}

可以使用目录管理器服务API（Java和Web服务）从AEM Forms以编程方式删除用户。 删除用户后，用户无法再用于执行需要用户的服务操作。 例如，您不能将任务分配给已删除的用户。

### 步骤{#summary_of_steps-1}的摘要

要删除用户，请执行以下步骤：

1. 包括项目文件。
1. 创建DirectoryManagerService客户端。
1. 指定要删除的用户。
1. 从AEM Forms中删除用户。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请包含代理文件。

**创建DirectoryManagerService客户端**

在以编程方式执行目录管理器服务API操作之前，请先创建一个目录管理器服务客户端。

**指定要删除的用户**

您可以使用用户的标识符值指定要删除的用户。

**从AEM Forms中删除用户**

要删除用户，请调用`DirectoryManagerServiceClient`对象的`deleteLocalUser`方法。

**另请参阅**

[使用Java API删除用户](users.md#delete-users-using-the-java-api)

[使用Web服务API删除用户](users.md#delete-users-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加用户](users.md#adding-users)

### 使用Java API {#delete-users-using-the-java-api}删除用户

使用目录管理器服务API(Java)删除用户：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-usermanager-client.jar。

1. 创建DirectoryManagerService客户端。

   使用`DirectoryManagerServiceClient`对象的构造函数并传递包含连接属性的`ServiceClientFactory`对象，创建对象。

1. 指定要删除的用户。

   * 使用`PrincipalSearchFilter`对象的构造函数创建对象。
   * 通过调用`PrincipalSearchFilter`对象的`setUserId`方法设置用户标识符值。 传递表示用户标识符值的字符串值。
   * 调用`DirectoryManagerServiceClient`对象的`findPrincipals`方法并传递`PrincipalSearchFilter`对象。 此方法返回一个`java.util.List`实例，其中每个元素都是一个`User`对象。 遍历`java.util.List`实例，找到要删除的用户。

1. 从AEM Forms中删除用户。

   调用`DirectoryManagerServiceClient`对象的`deleteLocalUser`方法并传递`User`对象的`oid`字段的值。 调用`User`对象的`getOid`方法。 使用从`java.util.List`实例检索的`User`对象。

**另请参阅**

[步骤摘要](users.md#summary-of-steps)

[快速开始（EJB模式）：使用Java API删除用户](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[快速开始（SOAP模式）：使用Java API删除用户](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#delete-users-using-the-web-service-api}删除用户

使用目录管理器服务API（Web服务）删除用户：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-usermanager-client.jar。

1. 创建DirectoryManagerService客户端。

   * 使用`DirectoryManagerServiceClient`对象的默认构造函数创建对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`DirectoryManagerServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如`http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`）。 您无需使用`lc_version`属性。 在创建服务引用时使用此属性。 确保指定`blob=mtom.`
   * 通过获取`DirectoryManagerServiceClient.Endpoint.Binding`字段的值，创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 为字段`DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`DirectoryManagerServiceClient.ClientCredentials.UserName.Password`分配相应的密码值。
      * 将常量值`HttpClientCredentialType.Basic`赋给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`赋给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 指定要删除的用户。

   * 使用`PrincipalSearchFilter`对象的构造函数创建对象。
   * 通过为`PrincipalSearchFilter`对象的`userId`字段分配字符串值来设置用户标识符值。
   * 调用`DirectoryManagerServiceClient`对象的`findPrincipals`方法并传递`PrincipalSearchFilter`对象。 此方法返回一个`MyArrayOfUser`集合对象，其中每个元素都是一个`User`对象。 遍历`MyArrayOfUser`集合以找到用户。 从`MyArrayOfUser`集合对象检索的`User`对象用于删除用户。

1. 从AEM Forms中删除用户。

   通过将`User`对象的`oid`字段值传递给`DirectoryManagerServiceClient`对象的`deleteLocalUser`方法来删除用户。

**另请参阅**

[步骤摘要](users.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 创建组{#creating-groups}

可以使用目录管理器服务API（Java和Web服务）以编程方式创建AEM Forms组。 创建组后，您可以使用该组执行需要组的服务操作。 例如，可将用户分配给新用户组。 （请参阅[管理用户和用户组](users.md#managing-users-and-groups)。）

### 步骤{#summary_of_steps-2}的摘要

要创建用户组，请执行以下步骤：

1. 包括项目文件。
1. 创建DirectoryManagerService客户端。
1. 确定组不存在。
1. 创建组。
1. 对组执行操作。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时为必需)
* jbossall-client.jar(在JBoss上部署AEM Forms时为必需)

有关这些JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建DirectoryManagerService客户端**

在以编程方式执行目录管理器服务操作之前，请先创建目录管理器服务API客户端。

**确定组是否存在**

创建组时，请确保该组不存在于同一域中。 也就是说，两个组不能在同一域内具有相同的名称。 要执行此任务，请执行搜索并根据两个值筛选搜索结果。 将主体类型设置为`com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP`以确保只返回组。 另外，请确保指定域名。

**创建组**

确定域中不存在该组后，创建该组并指定以下属性：

* **CommonName**:组的名称。
* **域**:添加组的域。
* **描述**:组的描述。

**对组执行操作**

创建用户组后，可以使用用户组执行操作。 例如，您可以将用户添加到组。 要将用户添加到组，请检索用户和组的唯一标识符值。 将这些值传递给`addPrincipalToLocalGroup`方法。

**另请参阅**

[使用Java API创建组](users.md#create-groups-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加用户](users.md#adding-users)

[删除用户](users.md#deleting-users)

### 使用Java API {#create-groups-using-the-java-api}创建组

使用目录管理器服务API(Java)创建组：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-usermanager-client.jar。

1. 创建DirectoryManagerService客户端。

   使用`DirectoryManagerServiceClient`对象的构造函数并传递包含连接属性的`ServiceClientFactory`对象，创建对象。

1. 确定组是否存在。

   * 使用`PrincipalSearchFilter`对象的构造函数创建对象。
   * 通过调用`PrincipalSearchFilter`对象的`setPrincipalType`对象来设置主体类型。 传递值`com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP`。
   * 通过调用`PrincipalSearchFilter`对象的`setSpecificDomainName`对象来设置域。 传递指定域名的字符串值。
   * 要查找组，请调用`DirectoryManagerServiceClient`对象的`findPrincipals`方法（主体可以是组）。 传递指定主体类型和域名的`PrincipalSearchFilter`对象。 此方法返回一个`java.util.List`实例，其中每个元素都是一个`Group`实例。 每个组实例都符合使用`PrincipalSearchFilter`对象指定的筛选器。
   * 遍历`java.util.List`实例。 对于每个元素，检索组名称。 请确保组名称不等于新组名称。

1. 创建组。

   * 如果组不存在，请调用`Group`对象的`setCommonName`方法并传递一个指定组名称的字符串值。
   * 调用`Group`对象的`setDescription`方法并传递一个指定组描述的字符串值。
   * 调用`Group`对象的`setDomainName`方法并传递指定域名的字符串值。
   * 调用`DirectoryManagerServiceClient`对象的`createLocalGroup`方法并传递`Group`实例。

   `createLocalUser`方法返回指定本地用户标识符值的字符串值。

1. 对组执行操作。

   * 使用`PrincipalSearchFilter`对象的构造函数创建对象。
   * 通过调用`PrincipalSearchFilter`对象的`setUserId`方法设置用户标识符值。 传递表示用户标识符值的字符串值。
   * 调用`DirectoryManagerServiceClient`对象的`findPrincipals`方法并传递`PrincipalSearchFilter`对象。 此方法返回一个`java.util.List`实例，其中每个元素都是一个`User`对象。 遍历`java.util.List`实例以找到用户。
   * 通过调用`DirectoryManagerServiceClient`对象的`addPrincipalToLocalGroup`方法将用户添加到组。 传递`User`对象的`getOid`方法的返回值。 传递`Group`对象的`getOid`方法的返回值（使用表示新组的`Group`实例）。

**另请参阅**

[步骤摘要](users.md#summary-of-steps)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 管理用户和组{#managing-users-and-groups}

本主题介绍如何使用(Java)以编程方式分配、删除和查询域、用户和用户组。

>[!NOTE]
>
>配置域时，必须为组和用户设置唯一标识符。 所选的属性不仅必须在LDAP环境中唯一，而且必须是不可变的，并且不会在目录中更改。 此属性还必须为简单字符串数据类型（Active Directory 2000/2003当前允许的唯一例外是`"objectsid"`，它是二进制值）。 例如，Novell eDirectory属性`"GUID"`不是简单的字符串数据类型，因此将无法工作。

* 对于Active Directory，请使用`"objectsid"`。
* 对于SunOne，请使用`"nsuniqueid"`。

>[!NOTE]
>
>不支持在LDAP目录同步过程中创建多个本地用户和用户组。 尝试此过程可能会导致错误。

### 步骤{#summary_of_steps-3}的摘要

要管理用户和用户组，请执行以下步骤：

1. 包括项目文件。
1. 创建DirectoryManagerService客户端。
1. 调用相应的用户或组操作。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建DirectoryManagerService客户端**

在以编程方式执行目录管理器服务操作之前，必须创建目录管理器服务客户端。 通过Java API，可通过创建`DirectoryManagerServiceClient`对象来实现这一点。 通过Web服务API，可通过创建`DirectoryManagerServiceService`对象来实现此目的。

**调用适当的用户或组操作**

创建服务客户端后，即可调用用户或组管理操作。 服务客户端允许您分配、删除和查询域、用户和组。 请注意，可以将目录主体或本地主体添加到本地组，但无法将本地主体添加到目录组。

**另请参阅**

[使用Java API管理用户和用户组](users.md#managing-users-and-groups-using-the-java-api)

[使用Web服务API管理用户和用户组](users.md#managing-users-and-groups-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[用户管理器API快速开始](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### 使用Java API {#managing-users-and-groups-using-the-java-api}管理用户和用户组

要使用(Java)以编程方式管理用户、组和域，请执行以下任务:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-usermanager-client.jar。 有关这些文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

1. 创建DirectoryManagerService客户端。

   使用`DirectoryManagerServiceClient`对象的构造函数并传递包含连接属性的`ServiceClientFactory`对象，创建对象。 有关信息，请参阅[设置连接属性&#x200B;](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)*。*

1. 调用相应的用户或组操作。

   要查找用户或组，请调用`DirectoryManagerServiceClient`对象的方法之一来查找主体（因为主体可以是用户或组）。 在以下示例中，使用搜索筛选器（`PrincipalSearchFilter`对象）调用`findPrincipals`方法。

   由于此情况下的返回值是包含`Principal`对象的`java.util.List`，因此对结果进行迭代，并将`Principal`对象转换为`User`或`Group`对象。

   使用生成的`User`或`Group`对象（两者都继承自`Principal`接口），检索您在工作流中需要的信息。 例如，域名和规范名值组合起来可唯一标识主体。 通过分别调用`Principal`对象的`getDomainName`和`getCanonicalName`方法来检索这些对象。

   要删除本地用户，请调用`DirectoryManagerServiceClient`对象的`deleteLocalUser`方法并传递用户的标识符。

   要删除本地组，请调用`DirectoryManagerServiceClient`对象的`deleteLocalGroup`方法并传递组的标识符。

**另请参阅**

[步骤摘要](users.md#summary-of-steps)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#managing-users-and-groups-using-the-web-service-api}管理用户和用户组

要使用目录管理器服务API（Web服务）以编程方式管理用户、组和域，请执行以下任务:

1. 包括项目文件。

   * 创建一个使用目录管理器WSDL的Microsoft .NET客户端程序集。 (请参阅[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)。)
   * 引用Microsoft .NET客户端程序集。 （请参阅[创建使用Base64编码](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)的.NET客户端程序集。）

1. 创建DirectoryManagerService客户端。

   使用proxy类的构造函数创建`DirectoryManagerServiceService`对象。

1. 调用相应的用户或组操作。

   要查找用户或组，请调用`DirectoryManagerServiceService`对象的方法之一来查找主体（因为主体可以是用户或组）。 在以下示例中，使用搜索筛选器（`PrincipalSearchFilter`对象）调用`findPrincipalsWithFilter`方法。 使用`PrincipalSearchFilter`对象时，仅当`isLocal`属性设置为`true`时，才返回本地主体。 此行为与Java API会发生的情况不同。

   >[!NOTE]
   >
   >如果未在搜索筛选器（通过`PrincipalSearchFilter.resultsMax`字段）中指定最大结果数，则最多将返回1000个结果。 这与使用Java API时的行为不同，在Java API中，默认最大值为10个结果。 此外，搜索方法（如`findGroupMembers`）不会生成任何结果，除非在搜索筛选器（例如，通过`GroupMembershipSearchFilter.resultsMax`字段）中指定了最大结果数。 这适用于从`GenericSearchFilter`类继承的所有搜索过滤器。 有关详细信息，请参阅[AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

   由于此情况下的返回值是包含`Principal`对象的`object[]`，因此对结果进行迭代，并将`Principal`对象转换为`User`或`Group`对象。

   使用生成的`User`或`Group`对象（两者都继承自`Principal`接口），检索您在工作流中需要的信息。 例如，域名和规范名值组合起来可唯一标识主体。 通过分别调用`Principal`对象的`domainName`和`canonicalName`字段来检索这些字段。

   要删除本地用户，请调用`DirectoryManagerServiceService`对象的`deleteLocalUser`方法并传递用户的标识符。

   要删除本地组，请调用`DirectoryManagerServiceService`对象的`deleteLocalGroup`方法并传递组的标识符。

**另请参阅**

[步骤摘要](users.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 管理角色和权限{#managing-roles-and-permissions}

本主题介绍如何使用Authorization Manager Service API(Java)以编程方式分配、删除和确定角色和权限。

在AEM Forms中，*role*&#x200B;是一组访问一个或多个系统级资源的权限。 这些权限是通过用户管理创建的，并由服务组件实施。 例如，管理员可以向一组用户分配“策略集作者”角色。 Rights Management随后将允许具有该角色的组的用户通过管理控制台创建策略集。

有两种角色：*默认角色*&#x200B;和&#x200B;*自定义角色*。 默认角色（*系统角色）*&#x200B;已驻留在AEM Forms中。 假定默认角色不能由管理员删除或修改，因此是不可变的。 因此，管理员创建的自定义角色可变。管理员随后可以修改或删除这些角色。

角色使权限管理更简单。 当角色被分配给主体时，一组权限被自动分配给该主体，并且主体的所有与访问相关的特定决策都基于所分配的整个权限集。

### 步骤{#summary_of_steps-4}的摘要

要管理角色和权限，请执行以下步骤：

1. 包括项目文件。
1. 创建AuthorizationManagerService客户端。
1. 调用相应的角色或权限操作。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建AuthorizationManagerService客户端**

在以编程方式执行User Management AuthorizationManagerService操作之前，必须创建AuthorizationManagerService客户端。 通过Java API，可通过创建`AuthorizationManagerServiceClient`对象来实现这一点。

**调用适当的角色或权限操作**

创建服务客户端后，即可调用角色或权限操作。 服务客户端允许您分配、删除和确定角色和权限。

**另请参阅**

[使用Java API管理角色和权限](users.md#managing-roles-and-permissions-using-the-java-api)

[使用Web服务API管理角色和权限](users.md#managing-roles-and-permissions-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[用户管理器API快速开始](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### 使用Java API {#managing-roles-and-permissions-using-the-java-api}管理角色和权限

要使用Authorization Manager Service API(Java)管理角色和权限，请执行以下任务:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-usermanager-client.jar。

1. 创建AuthorizationManagerService客户端。

   使用`AuthorizationManagerServiceClient`对象的构造函数并传递包含连接属性的`ServiceClientFactory`对象，创建对象。

1. 调用相应的角色或权限操作。

   要向主体分配角色，请调用`AuthorizationManagerServiceClient`对象的`assignRole`方法并传递以下值：

   * 包含角色标识符的`java.lang.String`对象
   * 包含主标识符的`java.lang.String`对象的数组。

   要从主体中删除角色，请调用`AuthorizationManagerServiceClient`对象的`unassignRole`方法并传递以下值：

   * 包含角色标识符的`java.lang.String`对象。
   * 包含主标识符的`java.lang.String`对象的数组。


**另请参阅**

[步骤摘要](users.md#summary-of-steps)

[快速开始（SOAP模式）：使用Java API管理角色和权限](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#managing-roles-and-permissions-using-the-web-service-api}管理角色和权限

使用Authorization Manager Service API（Web服务）管理角色和权限：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/AuthorizationManagerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建AuthorizationManagerService客户端。

   * 使用`AuthorizationManagerServiceClient`对象的默认构造函数创建一个对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`AuthorizationManagerServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如`http://localhost:8080/soap/services/AuthorizationManagerService?blob=mtom`）。 您无需使用`lc_version`属性。 在创建服务引用时使用此属性。
   * 通过获取`AuthorizationManagerServiceClient.Endpoint.Binding`字段的值，创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 为字段`AuthorizationManagerServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`AuthorizationManagerServiceClient.ClientCredentials.UserName.Password`分配相应的密码值。
      * 将常量值`HttpClientCredentialType.Basic`赋给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`赋给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 调用相应的角色或权限操作。

   要向主体分配角色，请调用`AuthorizationManagerServiceClient`对象的`assignRole`方法并传递以下值：

   * 包含角色标识符的`string`对象
   * 包含主标识符的`MyArrayOf_xsd_string`对象。

   要从主体中删除角色，请调用`AuthorizationManagerServiceService`对象的`unassignRole`方法并传递以下值：

   * 包含角色标识符的`string`对象。
   * 包含主标识符的`string`对象的数组。


**另请参阅**

[步骤摘要](users.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 验证用户{#authenticating-users}

本主题介绍如何使用Authentication Manager Service API(Java)使您的客户端应用程序能够以编程方式验证用户身份。

可能需要用户身份验证才能与存储安全数据的企业数据库或其他企业存储库进行交互。

例如，假设用户在网页中输入用户名和密码并将这些值提交到承载Forms的J2EE应用程序服务器。 Forms自定义应用程序可以使用身份验证管理器服务对用户进行身份验证。

如果身份验证成功，则应用程序将访问安全的企业数据库。 否则，将向用户发送一条消息，声明用户不是授权用户。

下图显示了应用程序的逻辑流。

![au_au_umauth_process](assets/au_au_umauth_process.png)

下表介绍了此图中的步骤

<table>
 <thead>
  <tr>
   <th><p>步骤</p></th>
   <th><p>描述</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>用户访问网站并指定用户名和密码。 此信息将提交到承载AEM Forms的J2EE应用程序服务器。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>用户凭据将通过Authentication Manager服务进行身份验证。 如果用户凭据有效，则工作流将继续执行步骤3。 否则，将向用户发送一条消息，声明用户不是授权用户。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>从安全的企业数据库检索用户信息和表单设计。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>用户信息将与表单设计合并，表单将呈现给用户。 </p></td>
  </tr>
 </tbody>
</table>

### 步骤{#summary_of_steps-5}的摘要

要以编程方式验证用户身份，请执行以下步骤：

1. 包括项目文件。
1. 创建AuthenticationManagerService客户端。
1. 调用身份验证操作。
1. 如有必要，请检索上下文，以便客户端应用程序可以将其转发到其他AEM Forms服务进行身份验证。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建AuthenticationManagerService客户端**

在以编程方式验证用户之前，必须创建AuthenticationManagerService客户端。 使用Java API时，创建一个`AuthenticationManagerServiceClient`对象。

**调用身份验证操作**

创建服务客户端后，即可调用身份验证操作。 此操作需要有关用户的信息，如用户名和密码。 如果用户未进行身份验证，则会引发异常。

**检索身份验证上下文**

对用户进行身份验证后，可以根据经过身份验证的用户创建上下文。 然后，您可以使用内容调用其他AEM Forms服务。 例如，您可以使用上下文创建`EncryptionServiceClient`并使用口令加密PDF文档。 确保已验证的用户具有调用AEM Forms服务所需的名为`Services User`的角色。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[用户管理器API快速开始](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[使用密码加密PDF文档](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API {#authenticate-a-user-using-the-java-api}验证用户身份

使用Authentication Manager Service API(Java)对用户进行身份验证：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-usermanager-client.jar。

1. 创建AuthenticationManagerServices客户端。

   使用`AuthenticationManagerServiceClient`对象的构造函数并传递包含连接属性的`ServiceClientFactory`对象，创建对象。

1. 调用身份验证操作。

   调用`AuthenticationManagerServiceClient`对象的`authenticate`方法并传递以下值：

   * 包含用户名的`java.lang.String`对象。
   * 包含用户密码的字节数组（`byte[]`对象）。 可以通过调用`java.lang.String`对象的`getBytes`方法来获取`byte[]`对象。

   authenticate方法返回一个`AuthResult`对象，该对象包含有关已验证用户的信息。

1. 检索身份验证上下文。

   调用`ServiceClientFactory`对象的`getContext`方法，该方法将返回`Context`对象。

   然后调用`Context`对象的`initPrincipal`方法并传递`AuthResult`。

### 使用Web服务API {#authenticate-a-user-using-the-web-service-api}验证用户身份

使用Authentication Manager Service API（Web服务）对用户进行身份验证：

1. 包括项目文件。

   * 创建一个Microsoft .NET客户端程序集，它使用Authentication Manager WSDL。 (请参阅[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)。)
   * 引用Microsoft .NET客户端程序集。 (请参阅[使用Base64编码](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)调用AEM Forms中的“引用.NET客户端程序集”。)

1. 创建AuthenticationManagerService客户端。

   使用proxy类的构造函数创建`AuthenticationManagerServiceService`对象。

1. 调用身份验证操作。

   调用`AuthenticationManagerServiceClient`对象的`authenticate`方法并传递以下值：

   * 包含用户名的`string`对象
   * 包含用户密码的字节数组（`byte[]`对象）。 可以使用以下示例中显示的逻辑将包含密码的`string`对象转换为`byte[]`数组，从而获得`byte[]`对象。
   * 返回的值将是`AuthResult`对象，可用于检索有关用户的信息。 在以下示例中，首先获取`AuthResult`对象的`authenticatedUser`字段，然后获取生成的`User`对象的`canonicalName`和`domainName`字段，以检索用户信息。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 以编程方式同步用户{#programmatically-synchronizing-users}

您可以使用用户管理API以编程方式同步用户。 同步用户时，您将使用位于用户存储库中的用户数据更新AEM Forms。 例如，假定您向用户存储库添加新用户。 执行同步操作后，新用户将成为AEM forms用户。 此外，不再在您的用户存储库中的用户也会从AEM Forms中删除。

下图显示了AEM Forms与用户存储库同步的情况。

![ps_ps_umauth_sync](assets/ps_ps_umauth_sync.png)

下表介绍了此图中的步骤

<table>
 <thead>
  <tr>
   <th><p>步骤</p></th>
   <th><p>描述</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>3</p></td>
   <td><p>客户端应用程序请求AEM Forms执行同步操作。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>AEM Forms执行同步操作。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>用户信息已更新。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>用户能够视图更新的用户信息。 </p></td>
  </tr>
 </tbody>
</table>

### 步骤{#summary_of_steps-6}的摘要

要以编程方式同步用户，请执行以下步骤：

1. 包括项目文件。
1. 创建UserManagerUtilServiceClient客户端。
1. 指定企业域。
1. 调用身份验证操作。
1. 确定同步操作是否完成

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建UserManagerUtilServiceClientclient**

必须先创建`UserManagerUtilServiceClient`对象，然后才能以编程方式同步用户。

**指定企业域**

在使用用户管理API执行同步操作之前，您需要指定用户所属的企业域。 可以指定一个或多个企业域。 在以编程方式执行同步操作之前，必须使用管理控制台设置企业域。 （请参阅[管理帮助](https://www.adobe.com/go/learn_aemforms_admin_63)。）

**调用同步操作**

指定一个或多个企业域后，可以执行同步操作。 执行此操作所需的时间取决于位于用户存储库中的用户记录数。

**确定同步操作是否完成**

在以编程方式执行同步操作后，可以确定操作是否完成。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[用户管理器API快速开始](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[使用密码加密PDF文档](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API {#programmatically-synchronizing-users-using-the-java-api}以编程方式同步用户

使用用户管理API(Java)同步用户：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-usermanager-client.jar和adobe-usermanager-util-client.jar。

1. 创建UserManagerUtilServiceClient客户端。

   使用`UserManagerUtilServiceClient`对象的构造函数并传递包含连接属性的`ServiceClientFactory`对象，创建对象。

1. 指定企业域。

   * 调用`UserManagerUtilServiceClient`对象的`scheduleSynchronization`方法以开始用户同步操作。
   * 使用`HashSet`构造函数创建`java.util.Set`实例。 确保指定`String`为数据类型。 此`Java.util.Set`实例存储同步操作所应用的域名。
   * 对于要添加的每个域名，调用`java.util.Set`对象的add方法并传递域名。

1. 调用同步操作。

   调用`ServiceClientFactory`对象的`getContext`方法，该方法将返回`Context`对象。

   然后调用`Context`对象的`initPrincipal`方法并传递`AuthResult`。

**另请参阅**

[以编程方式同步用户](users.md#programmatically-synchronizing-users)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
