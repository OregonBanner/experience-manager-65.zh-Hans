---
title: 管理用户
seo-title: 管理用户
description: 'null'
seo-description: 'null'
uuid: 68d8a0bc-6e3d-4286-ba5c-534dcf58cb84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 95804bff-9e6f-4807-aae4-790bd9e7cb57
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 管理用户 {#managing-users}

**关于用户管理**

您可以使用用户管理API创建客户端应用程序，这些应用程序可以管理角色、权限和承担者（可以是用户或用户组）以及验证用户身份。 用户管理API由以下AEM Forms API组成：

* 目录管理器服务API
* Authentication Manager Service API
* Authorization Manager Service API

用户管理允许您分配、删除和确定角色和权限。 它还允许您分配、删除和查询域、用户和用户组。 最后，您可以使用用户管理来验证用户身份。

在“ [添加用户](users.md#adding-users) ”中，您将了解如何以编程方式添加用户。 本节使用目录管理器服务API。

在“ [删除用户](users.md#deleting-users) ”中，您将了解如何以编程方式删除用户。 本节使用目录管理器服务API。

在“ [管理用户和用户组](users.md#managing-users-and-groups) ”中，您将了解本地用户与目录用户之间的区别，并查看如何使用Java和Web服务API以编程方式管理用户和用户组的示例。 本节使用目录管理器服务API。

在“ [管理角色和权限](users.md#managing-roles-and-permissions) ”中，您将了解系统角色和权限以及您可以通过编程方式增强这些角色和权限的功能，并查看如何使用Java和Web服务API以编程方式管理角色和权限的示例。 本节同时使用Directory Manager Service API和Authorization Manager Service API。

在“ [验证用户](users.md#authenticating-users) ”中，您将看到如何使用Java和Web服务API以编程方式验证用户的示例。 本节使用Authorization Manager Service API。

**了解身份验证过程**

用户管理提供内置的身份验证功能，还允许您将其连接到您自己的身份验证提供者。 当用户管理收到身份验证请求（例如，用户尝试登录）时，会将用户信息传递给身份验证提供者以进行身份验证。 用户管理在验证用户后，会从验证提供者接收结果。

下图显示了尝试登录的最终用户、用户管理和身份验证提供者之间的交互。

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
   <td><p>用户尝试登录调用用户管理的服务。 用户指定用户名和口令。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>用户管理会将用户名和密码以及配置信息发送给身份验证提供者。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>身份验证提供者连接到用户存储并验证用户。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>身份验证提供者会将结果返回给用户管理。</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>用户管理允许用户登录或拒绝对产品的访问。</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>如果服务器时区与客户端时区不同，则在WebSphere Application server群集上使用。NET客户端在本机SOAP堆栈上使用AEM Forms的WSDL生成PDF服务时，可能会发生以下用户管理身份验证错误：

`[com.adobe.idp.um.webservices.WSSecurityHandler] errorCode:12803 errorCodeHEX:0x3203 message:WSSecurityHandler: UM authenticate returns exception : An error was discovered processing the <wsse:Security> header. (WSSecurityEngine: Invalid timestamp The security semantics of message have expired).`

**了解目录管理**

用户管理与支持LDAP目录连接的目录服务提供程序(DirectoryManagerService)一起打包。 如果您的单位使用非LDAP存储库存储用户记录，则可以创建您自己的与存储库一起使用的目录服务提供者。

目录服务提供商应用户管理的请求从用户存储检索记录。 用户管理会定期将用户和组记录缓存到数据库中以提高性能。

目录服务提供者可用于将用户管理数据库与用户存储同步。 此步骤可确保所有用户目录信息以及所有用户和组记录均为最新状态。

此外，DirectoryManagerService还允许您创建和管理域。 域定义不同的用户群。 域的边界通常根据组织的结构或用户存储的设置来定义。 用户管理域提供身份验证提供者和目录服务提供者使用的配置设置。

在“用户管理”导出的配置XML中，属性值为的根节点包含为“用户管理”定义的 `Domains` 每个域的XML元素。 这些元素中的每一个都包含定义与特定服务提供商相关联的域的各方面的其他元素。

**了解objectSID值**

使用Active Directory时，请务必了解值不是跨多 `objectSID` 个域的唯一属性。 此值存储对象的安全标识符。 在多域环境中（例如，一个域树），该 `objectSID` 值可以不同。

如果 `objectSID` 将对象从一个Active Directory域移动到另一个域，则值会发生更改。 某些对象在域中的任 `objectSID` 何位置都具有相同的值。 例如，BUILTIN\Administrators、BUILTIN\Power Users等组的值与域 `objectSID` 相同。 这些 `objectSID` 值是众所周知的。

## 添加用户 {#adding-users}

可以使用Directory Manager Service API（Java和Web服务）以编程方式将用户添加到AEM Forms。 添加用户后，您可以在执行需要用户的服务操作时使用该用户。 例如，可以为新用户分配任务。

### 步骤摘要 {#summary-of-steps}

要添加用户，请执行以下步骤：

1. 包括项目文件。
1. 创建DirectoryManagerService客户端。
1. 定义用户信息。
1. 将用户添加到AEM Forms。
1. 确认已添加用户。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请包含代理文件。

**创建DirectoryManagerService客户端**

在以编程方式执行目录管理器服务操作之前，请先创建目录管理器服务API客户端。

**定义用户信息**

使用Directory Manager Service API添加新用户时，请为该用户定义信息。 通常，在添加新用户时，您会定义以下值：

* **域名**:用户所属的域(例如 `DefaultDom`)。
* **用户标识符值**:用户的标识符值(例如， `wblue`)。
* **主体类型**:用户的类型(例如，您可以指定 `USER)`。
* **给定名称**:用户的指定名称(例如 `Wendy`)。
* **姓氏**:用户的系列名称(例如 `Blue)`。
* **区域设置**:用户的区域设置信息。

**将用户添加到AEM Forms**

定义用户信息后，可以将用户添加到AEM Forms。 要添加用户，请调用对 `DirectoryManagerServiceClient` 象的方 `createLocalUser` 法。

**验证是否已添加用户**

您可以验证是否已添加用户以确保未出现问题。 使用用户标识符值找到新用户。

**另请参阅**

[使用Java API添加用户](users.md#add-users-using-the-java-api)

[使用Web服务API添加用户](users.md#add-users-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[删除用户](users.md#deleting-users)

### 使用Java API添加用户 {#add-users-using-the-java-api}

使用Directory Manager Service API(Java)添加用户：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-usermanager-client.jar。

1. 创建DirectoryManagerServices客户端。

   使用对 `DirectoryManagerServiceClient` 象的构造函数并传递一个包含连接属 `ServiceClientFactory` 性的对象来创建对象。

1. 定义用户信息。

   * 使用对 `UserImpl` 象的构造函数创建对象。
   * 通过调用对象的方法 `UserImpl` 来设置维名 `setDomainName` 称。 传递指定域名的字符串值。
   * 通过调用对象的方法来 `UserImpl` 设置主体类 `setPrincipalType` 型。 传递指定用户类型的字符串值。 例如，您可以指定 `USER`。
   * 通过调用对象的方法设置用 `UserImpl` 户标识符 `setUserid` 值。 传递指定用户标识符值的字符串值。 例如，您可以指定 `wblue`。
   * 通过调用对象的方法 `UserImpl` 设置规范名 `setCanonicalName` 称。 传递指定用户规范名称的字符串值。 例如，您可以指定 `wblue`。
   * 通过调用对象的方法 `UserImpl` 设置给定 `setGivenName` 名称。 传递一个指定用户给定名称的字符串值。 例如，您可以指定 `Wendy`。
   * 通过调用对象的方法 `UserImpl` 设置族名 `setFamilyName` 称。 传递一个指定用户姓氏的字符串值。 例如，您可以指定 `Blue`。
   >[!NOTE]
   >
   >调用属于该对象的方 `UserImpl` 法以设置其他值。 例如，可以通过调用对象的方法来设置 `UserImpl` 区域设置 `setLocale` 值。

1. 将用户添加到AEM Forms。

   调用对 `DirectoryManagerServiceClient` 象的方 `createLocalUser` 法并传递以下值：

   * 表示 `UserImpl` 新用户的对象
   * 表示用户口令的字符串值
   该方 `createLocalUser` 法返回一个指定本地用户标识符值的字符串值。

1. 确认已添加用户。

   * 使用对 `PrincipalSearchFilter` 象的构造函数创建对象。
   * 通过调用对象的方法设置用 `PrincipalSearchFilter` 户标识符 `setUserId` 值。 传递表示用户标识符值的字符串值。
   * 调用对 `DirectoryManagerServiceClient` 象的方 `findPrincipals` 法并传递对 `PrincipalSearchFilter` 象。 此方法返回一 `java.util.List` 个实例，其中每个元素都是一个对 `User` 象。 遍历实 `java.util.List` 例以定位用户。

**另请参阅**

[步骤摘要](users.md#summary-of-steps)

[快速入门（SOAP模式）:使用Java API添加用户](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-adding-users-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API添加用户 {#add-users-using-the-web-service-api}

使用目录管理器服务API（Web服务）添加用户：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保将以下WSDL定义用于服务引用： `http://localhost:8080/soap/services/DirectoryManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建DirectoryManagerService客户端。

   * 使用对 `DirectoryManagerServiceClient` 象的默认构造函数创建对象。
   * 使用构 `DirectoryManagerServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`)。 您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。 确保您指定 `?blob=mtom`。
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `DirectoryManagerServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。

1. 定义用户信息。

   * 使用对 `UserImpl` 象的构造函数创建对象。
   * 通过为对象的字段指定字符串值来 `UserImpl` 设置demain名 `domainName` 称。
   * 通过为对象的字段指定字符串值来 `UserImpl` 设置主体类 `principalType` 型。 例如，您可以指定 `USER`。
   * 通过为对象的字段分配字符串值来设 `UserImpl` 置用户标识符 `userid` 值。
   * 通过为对象的字段指定字符串值来设 `UserImpl` 置规范名称 `canonicalName` 值。
   * 通过为对象的字段分配字符串值来设 `UserImpl` 置给定的名 `givenName` 称值。
   * 通过为对象的字段指定字符串值来设 `UserImpl` 置族名 `familyName` 值。

1. 将用户添加到AEM Forms。

   调用对 `DirectoryManagerServiceClient` 象的方 `createLocalUser` 法并传递以下值：

   * 表示 `UserImpl` 新用户的对象
   * 表示用户口令的字符串值
   该方 `createLocalUser` 法返回一个指定本地用户标识符值的字符串值。

1. 确认已添加用户。

   * 使用对 `PrincipalSearchFilter` 象的构造函数创建对象。
   * 通过将表示用户标识符值的字符串值分配给对象字段，设置用户的用 `PrincipalSearchFilter` 户标识符 `userId` 值。
   * 调用对 `DirectoryManagerServiceClient` 象的方 `findPrincipals` 法并传递对 `PrincipalSearchFilter` 象。 此方法返回一个 `MyArrayOfUser` 集合对象，其中每个元素都是一个对 `User` 象。 遍历集合 `MyArrayOfUser` 以定位用户。

**另请参阅**

[步骤摘要](users.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 删除用户 {#deleting-users}

您可以使用Directory Manager Service API（Java和Web服务）从AEM Forms中以编程方式删除用户。 删除用户后，用户无法再用于执行需要用户的服务操作。 例如，您无法将任务分配给已删除的用户。

### 步骤摘要 {#summary_of_steps-1}

要删除用户，请执行以下步骤：

1. 包括项目文件。
1. 创建DirectoryManagerService客户端。
1. 指定要删除的用户。
1. 从AEM Forms中删除用户。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请包含代理文件。

**创建DirectoryManagerService客户端**

在以编程方式执行Directory Manager Service API操作之前，请先创建Directory manager服务客户端。

**指定要删除的用户**

您可以使用用户的标识符值指定要删除的用户。

**从AEM Forms中删除用户**

要删除用户，请调用对 `DirectoryManagerServiceClient` 象的方 `deleteLocalUser` 法。

**另请参阅**

[使用Java API删除用户](users.md#delete-users-using-the-java-api)

[使用Web服务API删除用户](users.md#delete-users-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加用户](users.md#adding-users)

### 使用Java API删除用户 {#delete-users-using-the-java-api}

使用目录管理器服务API(Java)删除用户：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-usermanager-client.jar。

1. 创建DirectoryManagerService客户端。

   使用对 `DirectoryManagerServiceClient` 象的构造函数并传递一个包含连接属 `ServiceClientFactory` 性的对象来创建对象。

1. 指定要删除的用户。

   * 使用对 `PrincipalSearchFilter` 象的构造函数创建对象。
   * 通过调用对象的方法设置用 `PrincipalSearchFilter` 户标识符 `setUserId` 值。 传递表示用户标识符值的字符串值。
   * 调用对 `DirectoryManagerServiceClient` 象的方 `findPrincipals` 法并传递对 `PrincipalSearchFilter` 象。 此方法返回一 `java.util.List` 个实例，其中每个元素都是一个对 `User` 象。 遍历实 `java.util.List` 例以找到要删除的用户。

1. 从AEM Forms中删除用户。

   调用 `DirectoryManagerServiceClient` 对象的方 `deleteLocalUser` 法并传递对象字 `User` 段的值 `oid` 。 调用 `User` 对象的方 `getOid` 法。 使用从 `User` 实例检索到的对 `java.util.List` 象。

**另请参阅**

[步骤摘要](users.md#summary-of-steps)

[快速入门（EJB模式）:使用Java API删除用户](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[快速入门（SOAP模式）:使用Java API删除用户](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API删除用户 {#delete-users-using-the-web-service-api}

使用目录管理器服务API（Web服务）删除用户：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-usermanager-client.jar。

1. 创建DirectoryManagerService客户端。

   * 使用对 `DirectoryManagerServiceClient` 象的默认构造函数创建对象。
   * 使用构 `DirectoryManagerServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`)。 您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。 确保指定 `blob=mtom.`
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `DirectoryManagerServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。

1. 指定要删除的用户。

   * 使用对 `PrincipalSearchFilter` 象的构造函数创建对象。
   * 通过为对象的字段分配字符串值来设 `PrincipalSearchFilter` 置用户标识符 `userId` 值。
   * 调用对 `DirectoryManagerServiceClient` 象的方 `findPrincipals` 法并传递对 `PrincipalSearchFilter` 象。 此方法返回一个 `MyArrayOfUser` 集合对象，其中每个元素都是一个对 `User` 象。 遍历集合 `MyArrayOfUser` 以定位用户。 从集 `User` 合对象检索 `MyArrayOfUser` 的对象用于删除用户。

1. 从AEM Forms中删除用户。

   通过将对象的字 `User` 段值传递 `oid` 给对象的方 `DirectoryManagerServiceClient` 法来删除用 `deleteLocalUser` 户。

**另请参阅**

[步骤摘要](users.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 创建组 {#creating-groups}

可以使用Directory Manager Service API（Java和Web服务）以编程方式创建AEM Forms组。 创建组后，您可以使用该组执行需要组的服务操作。 例如，可将用户分配给新用户组。 (See [Managing Users and Groups](users.md#managing-users-and-groups).)

### 步骤摘要 {#summary_of_steps-2}

要创建用户组，请执行以下步骤：

1. 包括项目文件。
1. 创建DirectoryManagerService客户端。
1. 确定组不存在。
1. 创建用户组。
1. 对组执行操作。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（在JBoss上部署AEM表单时为必需）
* jbossall-client.jar（在JBoss上部署AEM表单时为必需）

有关这些JAR文件的位置的信息，请参 [阅包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建DirectoryManagerService客户端**

在以编程方式执行目录管理器服务操作之前，请先创建目录管理器服务API客户端。

**确定组是否存在**

创建组时，请确保该组不存在于同一域中。 也就是说，两个组不能在同一域内具有相同的名称。 要执行此任务，请执行搜索并基于两个值筛选搜索结果。 将主体类型设置为 `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP` 确保只返回组。 另外，请确保指定域名。

**创建用户组**

在确定域中不存在该组后，创建该组并指定以下属性：

* **CommonName**:用户组的名称。
* **域**:添加组的域。
* **说明**:用户组的说明。

**对组执行操作**

在创建用户组后，可以使用该用户组执行操作。 例如，您可以向用户组添加用户。 要将用户添加到用户组，请检索用户和用户组的唯一标识符值。 将这些值传递给 `addPrincipalToLocalGroup` 方法。

**另请参阅**

[使用Java API创建组](users.md#create-groups-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加用户](users.md#adding-users)

[删除用户](users.md#deleting-users)

### 使用Java API创建组 {#create-groups-using-the-java-api}

使用目录管理器服务API(Java)创建用户组：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-usermanager-client.jar。

1. 创建DirectoryManagerService客户端。

   使用对 `DirectoryManagerServiceClient` 象的构造函数并传递一个包含连接属 `ServiceClientFactory` 性的对象来创建对象。

1. 确定组是否存在。

   * 使用对 `PrincipalSearchFilter` 象的构造函数创建对象。
   * 通过调用对象的对象来 `PrincipalSearchFilter` 设置主体类 `setPrincipalType` 型。 传递值 `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP`。
   * 通过调用对象的对 `PrincipalSearchFilter` 象来设置域 `setSpecificDomainName` 。 传递指定域名的字符串值。
   * 要查找组，请调用对 `DirectoryManagerServiceClient` 象的方 `findPrincipals` 法（主体可以是组）。 传递 `PrincipalSearchFilter` 指定主体类型和域名的对象。 此方法返回一个实 `java.util.List` 例，其中每个元素都是一个 `Group` 实例。 每个组实例都符合使用对象指定的过滤 `PrincipalSearchFilter` 器。
   * 在实例中 `java.util.List` 迭代。 对于每个元素，检索组名称。 确保用户组名称不等于新用户组名称。

1. 创建用户组。

   * 如果组不存在，请调用对象 `Group` 的方法并传 `setCommonName` 递指定组名称的字符串值。
   * 调用对 `Group` 象的方 `setDescription` 法并传递一个指定组描述的字符串值。
   * 调用对 `Group` 象的方 `setDomainName` 法并传递指定域名的字符串值。
   * 调用对 `DirectoryManagerServiceClient` 象的方 `createLocalGroup` 法并传递实 `Group` 例。
   该方 `createLocalUser` 法返回一个指定本地用户标识符值的字符串值。

1. 对组执行操作。

   * 使用对 `PrincipalSearchFilter` 象的构造函数创建对象。
   * 通过调用对象的方法设置用 `PrincipalSearchFilter` 户标识符 `setUserId` 值。 传递表示用户标识符值的字符串值。
   * 调用对 `DirectoryManagerServiceClient` 象的方 `findPrincipals` 法并传递对 `PrincipalSearchFilter` 象。 此方法返回一 `java.util.List` 个实例，其中每个元素都是一个对 `User` 象。 遍历实 `java.util.List` 例以定位用户。
   * 通过调用对象的方法将用户 `DirectoryManagerServiceClient` 添加到用 `addPrincipalToLocalGroup` 户组。 传递对象方 `User` 法的返回 `getOid` 值。 传递对象方法 `Group` 的返回值 `getOid` (使用 `Group` 表示新组的实例)。

**另请参阅**

[步骤摘要](users.md#summary-of-steps)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Managing Users and Groups {#managing-users-and-groups}

本主题介绍如何使用(Java)以编程方式分配、删除和查询域、用户和用户组。

>[!NOTE]
>
>配置域时，必须为组和用户设置唯一标识符。 所选的属性不仅必须在LDAP环境中是唯一的，而且必须是不可变的，并且不会在目录中更改。 此属性还必须是简单的字符串数据类型(Active Directory 2000/2003当前允许的唯一例外是二进制 `"objectsid"`值，它是二进制值)。 例如，Novell eDirectory `"GUID"`属性不是简单的字符串数据类型，因此将无法工作。

* 对于Active Directory，请使用 `"objectsid"`。
* 对于SunOne，请使用 `"nsuniqueid"`。

>[!NOTE]
>
>不支持在LDAP目录同步过程中创建多个本地用户和用户组。 尝试此过程可能会导致错误。

### 步骤摘要 {#summary_of_steps-3}

要管理用户和用户组，请执行以下步骤：

1. 包括项目文件。
1. 创建DirectoryManagerService客户端。
1. 调用相应的用户或用户组操作。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建DirectoryManagerService客户端**

在以编程方式执行目录管理器服务操作之前，必须先创建目录管理器服务客户端。 使用Java API，可通过创建对象来实现这 `DirectoryManagerServiceClient` 一点。 借助Web服务API，这可以通过创建对象来 `DirectoryManagerServiceService` 实现。

**调用相应的用户或用户组操作**

创建服务客户端后，您便可以调用用户或组管理操作。 服务客户端允许您分配、删除和查询域、用户和用户组。 请注意，可以将目录主体或本地主体添加到本地组，但不能将本地主体添加到目录组。

**另请参阅**

[使用Java API管理用户和用户组](users.md#managing-users-and-groups-using-the-java-api)

[使用Web服务API管理用户和用户组](users.md#managing-users-and-groups-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[User Manager API快速入门](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### 使用Java API管理用户和用户组 {#managing-users-and-groups-using-the-java-api}

要使用(Java)以编程方式管理用户、组和域，请执行以下任务：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-usermanager-client.jar。 有关这些文件的位置的信息，请参 [阅包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

1. 创建DirectoryManagerService客户端。

   使用对 `DirectoryManagerServiceClient` 象的构造函数并传递一个包含连接属 `ServiceClientFactory` 性的对象来创建对象。 有关信息，请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)*。*

1. 调用相应的用户或用户组操作。

   要查找用户或用户组，请调用对象的一种方法来查找承担者（因为主体可以是用户或用户组）。 `DirectoryManagerServiceClient` 在以下示例中，使用 `findPrincipals` 搜索过滤器（对象）调用 `PrincipalSearchFilter` 该方法。

   由于此例中的返回值是包含对 `java.util.List` 象的 `Principal` 值，因此对结果进行迭代并将对象转 `Principal` 换为 `User` 或对 `Group` 象。

   使用生成 `User` 或对 `Group` 象（两者都从界面继承）检索 `Principal` 工作流中需要的信息。 例如，域名和规范名称值组合在一起可唯一标识主体。 通过分别调用对象和 `Principal` 方法来检 `getDomainName` 索 `getCanonicalName` 这些属性。

   要删除本地用户，请调用对 `DirectoryManagerServiceClient` 象的方 `deleteLocalUser` 法并传递用户的标识符。

   要删除本地组，请调用对 `DirectoryManagerServiceClient` 象的方 `deleteLocalGroup` 法并传递组的标识符。

**另请参阅**

[步骤摘要](users.md#summary-of-steps)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API管理用户和用户组 {#managing-users-and-groups-using-the-web-service-api}

要使用目录管理器服务API（Web服务）以编程方式管理用户、组和域，请执行以下任务：

1. 包括项目文件。

   * 创建一个使用目录管理器WSDL的Microsoft .NET客户端组件。 (请参 [阅使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)。)
   * 参考Microsoft .NET客户端程序集。 (请参 [阅创建使用Base64编码的。NET客户端程序集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)。)

1. 创建DirectoryManagerService客户端。

   使用代 `DirectoryManagerServiceService` 理类的构造函数创建对象。

1. 调用相应的用户或用户组操作。

   要查找用户或用户组，请调用对象的一种方法来查找承担者（因为主体可以是用户或用户组）。 `DirectoryManagerServiceService` 在以下示例中，使用 `findPrincipalsWithFilter` 搜索过滤器（对象）调用 `PrincipalSearchFilter` 该方法。 当使用对 `PrincipalSearchFilter` 象时，仅当属性设置为时，才返回 `isLocal` 本地承担者 `true`。 此行为与Java API的行为不同。

   >[!NOTE]
   >
   >如果未在搜索筛选器（通过字段）中指定最 `PrincipalSearchFilter.resultsMax` 大结果数，则最多将返回1000个结果。 这与使用Java API时的行为不同，在Java API中，默认的最大值为10个结果。 此外，搜索方法(例 `findGroupMembers` 如，通过字段)不会产生任何结果，除非在搜索筛选器中指定最大结果 `GroupMembershipSearchFilter.resultsMax` 数。 这适用于继承自类的所有搜索过 `GenericSearchFilter` 滤器。 有关详细信息，请参 [阅AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

   由于此例中的返回值是包含对 `object[]` 象的 `Principal` 值，因此对结果进行迭代并将对象转 `Principal` 换为 `User` 或对 `Group` 象。

   使用生成 `User` 或对 `Group` 象（两者都从界面继承）检索 `Principal` 工作流中需要的信息。 例如，域名和规范名称值组合在一起可唯一标识主体。 通过分别调用对象 `Principal` 的字段和字 `domainName` 段来 `canonicalName` 检索这些字段。

   要删除本地用户，请调用对 `DirectoryManagerServiceService` 象的方 `deleteLocalUser` 法并传递用户的标识符。

   要删除本地组，请调用对 `DirectoryManagerServiceService` 象的方 `deleteLocalGroup` 法并传递组的标识符。

**另请参阅**

[步骤摘要](users.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 管理角色和权限 {#managing-roles-and-permissions}

本主题介绍如何使用Authorization Manager Service API(Java)以编程方式分配、删除和确定角色和权限。

在AEM Forms中，角 *色* 是一组访问一个或多个系统级资源的权限。 这些权限是通过用户管理创建的，并由服务组件实施。 例如，管理员可以将“策略集作者”角色分配给一组用户。 然后，Rights Management将允许具有该角色的组的用户通过管理控制台创建策略集。

有两种类型的角色：默 *认角色**和自定义角色*。 默认角色(*系统角色)* 已驻留在AEM Forms中。 假定默认角色不能由管理员删除或修改，因此不可变。 因此，管理员创建的自定义角色可变，管理员随后可以修改或删除这些角色。

角色使权限管理更加简单。 当角色被分配给主体时，一组权限被自动分配给该主体，并且主体的所有与访问相关的特定决策都基于所分配的总权限集。

### 步骤摘要 {#summary_of_steps-4}

要管理角色和权限，请执行以下步骤：

1. 包括项目文件。
1. 创建AuthorizationManagerService客户端。
1. 调用相应的角色或权限操作。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建AuthorizationManagerService客户端**

在以编程方式执行User Management AuthorizationManagerService操作之前，必须创建AuthorizationManagerService客户端。 使用Java API，可通过创建对象来实现这 `AuthorizationManagerServiceClient` 一点。

**调用适当的角色或权限操作**

创建服务客户端后，您便可以调用角色或权限操作。 服务客户端允许您分配、删除和确定角色和权限。

**另请参阅**

[使用Java API管理角色和权限](users.md#managing-roles-and-permissions-using-the-java-api)

[使用Web服务API管理角色和权限](users.md#managing-roles-and-permissions-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[User Manager API快速入门](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### 使用Java API管理角色和权限 {#managing-roles-and-permissions-using-the-java-api}

要使用Authorization Manager Service API(Java)管理角色和权限，请执行以下任务：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-usermanager-client.jar。

1. 创建AuthorizationManagerService客户端。

   使用对 `AuthorizationManagerServiceClient` 象的构造函数并传递一个包含连接属 `ServiceClientFactory` 性的对象来创建对象。

1. 调用相应的角色或权限操作。

   要为主体分配角色，请调用对象 `AuthorizationManagerServiceClient` 的方法并 `assignRole` 传递以下值：

   * 包 `java.lang.String` 含角色标识符的对象
   * 包含主标识 `java.lang.String` 符的对象的数组。
   要从主体中删除角色，请调用对 `AuthorizationManagerServiceClient` 象的方法并 `unassignRole` 传递以下值：

   * 包 `java.lang.String` 含角色标识符的对象。
   * 包含主标识 `java.lang.String` 符的对象的数组。


**另请参阅**

[步骤摘要](users.md#summary-of-steps)

[快速入门（SOAP模式）:使用Java API管理角色和权限](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API管理角色和权限 {#managing-roles-and-permissions-using-the-web-service-api}

使用Authorization Manager Service API（Web服务）管理角色和权限：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/AuthorizationManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建AuthorizationManagerService客户端。

   * 使用对 `AuthorizationManagerServiceClient` 象的默认构造函数创建对象。
   * 使用构 `AuthorizationManagerServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/AuthorizationManagerService?blob=mtom`.)您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `AuthorizationManagerServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `AuthorizationManagerServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `AuthorizationManagerServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。

1. 调用相应的角色或权限操作。

   要为主体分配角色，请调用对象 `AuthorizationManagerServiceClient` 的方法并 `assignRole` 传递以下值：

   * 包 `string` 含角色标识符的对象
   * 包含 `MyArrayOf_xsd_string` 主标识符的对象。
   要从主体中删除角色，请调用对 `AuthorizationManagerServiceService` 象的方法并 `unassignRole` 传递以下值：

   * 包 `string` 含角色标识符的对象。
   * 包含主标识 `string` 符的对象的数组。


**另请参阅**

[步骤摘要](users.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 验证用户身份 {#authenticating-users}

本主题介绍如何使用Authentication Manager Service API(Java)使客户端应用程序能够以编程方式验证用户身份。

可能需要用户身份验证才能与存储安全数据的企业数据库或其他企业存储库进行交互。

例如，假设用户在网页中输入用户名和密码并将值提交到承载表单的J2EE应用程序服务器。 Forms自定义应用程序可以使用Authentication Manager服务对用户进行身份验证。

如果身份验证成功，则应用程序访问受保护的企业数据库。 否则，将向用户发送一条消息，声明该用户不是授权用户。

下图显示了应用程序的逻辑流程。

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
   <td><p>用户凭据将通过Authentication manager服务进行身份验证。 如果用户凭据有效，则工作流将继续执行步骤3。 否则，将向用户发送一条消息，声明该用户不是授权用户。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>从受保护的企业数据库检索用户信息和表单设计。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>用户信息将与表单设计合并，表单将呈现给用户。 </p></td>
  </tr>
 </tbody>
</table>

### 步骤摘要 {#summary_of_steps-5}

要以编程方式验证用户身份，请执行以下步骤：

1. 包括项目文件。
1. 创建AuthenticationManagerService客户端。
1. 调用身份验证操作。
1. 如果需要，请检索上下文，以便客户端应用程序可以将其转发到其他AEM Forms服务进行身份验证。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建AuthenticationManagerService客户端**

在以编程方式验证用户之前，必须先创建AuthenticationManagerService客户端。 使用Java API时，创建一个对 `AuthenticationManagerServiceClient` 象。

**调用身份验证操作**

创建服务客户端后，您便可以调用身份验证操作。 此操作需要有关用户的信息，如用户名和密码。 如果用户未进行身份验证，则会引发异常。

**检索身份验证上下文**

对用户进行身份验证后，可以在经过身份验证的用户中创建上下文。 然后，您可以使用内容调用其他AEM Forms服务。 例如，您可以使用上下文创建PDF文 `EncryptionServiceClient` 档并使用口令加密PDF文档。 确保已通过身份验证的用户具有调用AEM Forms `Services User` 服务所需的名为的角色。

**另请参阅**

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[User Manager API快速入门](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[使用口令加密PDF文档](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API验证用户身份 {#authenticate-a-user-using-the-java-api}

使用Authentication Manager Service API(Java)对用户进行身份验证：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-usermanager-client.jar。

1. 创建AuthenticationManagerServices客户端。

   使用对 `AuthenticationManagerServiceClient` 象的构造函数并传递一个包含连接属 `ServiceClientFactory` 性的对象来创建对象。

1. 调用身份验证操作。

   调用对 `AuthenticationManagerServiceClient` 象的方 `authenticate` 法并传递以下值：

   * 包 `java.lang.String` 含用户名的对象。
   * 包含用户口令 `byte[]` 的字节数组（对象）。 可以通过调 `byte[]` 用对象的方 `java.lang.String` 法来获取对 `getBytes` 象。
   authenticate方法返回一个对 `AuthResult` 象，该对象包含关于已验证用户的信息。

1. 检索身份验证上下文。

   调用对 `ServiceClientFactory` 象的方 `getContext` 法，该方法将返回一个对 `Context` 象。

   然后调 `Context` 用对象的方 `initPrincipal` 法并传递 `AuthResult`。

### 使用Web服务API验证用户身份 {#authenticate-a-user-using-the-web-service-api}

使用Authentication Manager Service API（Web服务）对用户进行身份验证：

1. 包括项目文件。

   * 创建一个Microsoft .NET客户端组件，它使用Authentication Manager WSDL。 (请参 [阅使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)。)
   * 参考Microsoft .NET客户端程序集。 (请参阅使用Base64编码调用AEM Forms中的“ [引用。NET客户端程序集](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)”。)

1. 创建AuthenticationManagerService客户端。

   使用代 `AuthenticationManagerServiceService` 理类的构造函数创建对象。

1. 调用身份验证操作。

   调用对 `AuthenticationManagerServiceClient` 象的方 `authenticate` 法并传递以下值：

   * 包 `string` 含用户名的对象
   * 包含用户口令 `byte[]` 的字节数组（对象）。 您可以使用 `byte[]` 以下示例中所示的逻 `string` 辑，将包含密码的对象转换为数 `byte[]` 组，从而获得该对象。
   * 返回的值将是一个 `AuthResult` 对象，它可用于检索有关用户的信息。 在以下示例中，首先获取对象的字段，然后获取生成对象的字段，以 `AuthResult` 便检索用户的信 `authenticatedUser` 息和字 `User``canonicalName``domainName` 段。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 以编程方式同步用户 {#programmatically-synchronizing-users}

您可以使用用户管理API以编程方式同步用户。 同步用户时，您将使用用户存储库中的用户数据更新AEM Forms。 例如，假定您向用户存储库添加新用户。 执行同步操作后，新用户将成为AEM Forms用户。 此外，不再位于用户存储库中的用户也会从AEM Forms中删除。

下图显示了与用户存储库同步的AEM Forms。

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
   <td><p>1</p></td>
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
   <td><p>用户可以查看更新的用户信息。 </p></td>
  </tr>
 </tbody>
</table>

### 步骤摘要 {#summary_of_steps-6}

要以编程方式同步用户，请执行以下步骤：

1. 包括项目文件。
1. 创建UserManagerUtilServiceClient客户端。
1. 指定企业域。
1. 调用身份验证操作。
1. 确定同步操作是否完成

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建UserManagerUtilServiceClientclient**

在以编程方式同步用户之前，必须先创建一个 `UserManagerUtilServiceClient` 对象。

**指定企业域**

在使用用户管理API执行同步操作之前，您需要指定用户所属的企业域。 可以指定一个或多个企业域。 在以编程方式执行同步操作之前，必须使用管理控制台设置企业域。 (请参阅 [管理帮助](https://www.adobe.com/go/learn_aemforms_admin_63)。)

**调用同步操作**

指定一个或多个企业域后，可以执行同步操作。 执行此操作所花费的时间取决于位于用户存储库中的用户记录数。

**确定同步操作是否完成**

在以编程方式执行同步操作后，可以确定操作是否完成。

**另请参阅**

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[User Manager API快速入门](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[使用口令加密PDF文档](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API以编程方式同步用户 {#programmatically-synchronizing-users-using-the-java-api}

使用用户管理API(Java)同步用户：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-usermanager-client.jar和adobe-usermanager-util-client.jar。

1. 创建UserManagerUtilServiceClient客户端。

   使用对 `UserManagerUtilServiceClient` 象的构造函数并传递一个包含连接属 `ServiceClientFactory` 性的对象来创建对象。

1. 指定企业域。

   * 调用对 `UserManagerUtilServiceClient` 象的方 `scheduleSynchronization` 法以启动用户同步操作。
   * 使用构 `java.util.Set` 造函数创建实 `HashSet` 例。 确保指定 `String` 为数据类型。 此实 `Java.util.Set` 例存储应用同步操作的域名。
   * 对于要添加的每个域名，调用对 `java.util.Set` 象的add方法并传递域名。

1. 调用同步操作。

   调用对 `ServiceClientFactory` 象的方 `getContext` 法，该方法将返回一个对 `Context` 象。

   然后调 `Context` 用对象的方 `initPrincipal` 法并传递 `AuthResult`。

**另请参阅**

[以编程方式同步用户](users.md#programmatically-synchronizing-users)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
