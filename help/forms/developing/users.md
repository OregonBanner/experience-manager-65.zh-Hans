---
title: 管理用户
description: 使用用户管理API创建可以管理角色、权限和主体（可以是用户或组）的客户端应用程序，并对用户进行身份验证。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: d7c5bb84-a988-4b2e-a587-f4e5b50fea58
source-git-commit: 5e56441d2dc9b280547c91def8d971e7b1dfcfe3
workflow-type: tm+mt
source-wordcount: '6218'
ht-degree: 0%

---

# 管理用户 {#managing-users}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms 。**

**关于用户管理**

您可以使用用户管理API创建客户端应用程序，这些应用程序可以管理角色、权限和主体（可以是用户或组），并对用户进行身份验证。 用户管理API包含以下AEM Forms API：

* 目录管理器服务API
* Authentication Manager服务API
* 授权管理器服务API

用户管理允许您分配、删除和确定角色和权限。 它还允许您分配、删除和查询域、用户和组。 最后，您可以使用“用户管理”来验证用户。

在 [添加用户](users.md#adding-users) 您将了解如何以编程方式添加用户。 本节使用目录管理器服务API。

在 [删除用户](users.md#deleting-users) 您将了解如何以编程方式删除用户。 本节使用目录管理器服务API。

在 [管理用户和组](users.md#managing-users-and-groups) 您将了解本地用户和目录用户之间的区别，并查看有关如何使用Java和Web服务API以编程方式管理用户和组的示例。 本节使用目录管理器服务API。

在 [管理角色和权限](users.md#managing-roles-and-permissions) 您将了解系统角色和权限，以及可以通过编程方式执行哪些操作来增强这些角色和权限，并查看有关如何使用Java和Web服务API以编程方式管理角色和权限的示例。 本节同时使用目录管理器服务API和授权管理器服务API。

在 [验证用户](users.md#authenticating-users) 您将看到有关如何使用Java和Web服务API以编程方式对用户进行身份验证的示例。 本节使用授权管理器服务API。

**了解身份验证过程**

“用户管理”提供内置的身份验证功能，并使您能够将其连接到您自己的身份验证提供程序。 当用户管理收到身份验证请求（例如，用户尝试登录）时，它会将用户信息传递给身份验证提供程序以进行身份验证。 User Management在对用户进行身份验证后，会从身份验证提供程序接收结果。

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
   <td><p>用户尝试登录到调用“用户管理”的服务。 用户指定用户名和密码。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>“用户管理”将用户名和密码以及配置信息发送给验证提供程序。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>验证提供程序连接到用户存储区并验证用户。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>身份验证提供程序将结果返回到“用户管理”。</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>用户管理可让用户登录或拒绝对产品的访问。</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>如果服务器时区与客户端时区不同，则在WebSphere Application Server群集上使用.NET客户端在本机SOAP栈栈上使用AEM Forms生成PDF服务的WSDL时，可能会出现以下用户管理身份验证错误：

`[com.adobe.idp.um.webservices.WSSecurityHandler] errorCode:12803 errorCodeHEX:0x3203 message:WSSecurityHandler: UM authenticate returns exception : An error was discovered processing the <wsse:Security> header. (WSSecurityEngine: Invalid timestamp The security semantics of message have expired).`

**了解目录管理**

“用户管理”与支持连接到LDAP目录的目录服务提供程序(DirectoryManagerService)一起打包。 如果您的组织使用非LDAP存储库来存储用户记录，则可以创建自己的目录服务提供程序，该服务提供程序可与您的存储库配合使用。

目录服务提供者应用户管理的请求，从用户存储中检索记录。 用户管理定期缓存数据库中的用户和组记录以提高性能。

目录服务提供程序可用于将User Management数据库与用户存储同步。 此步骤确保所有用户目录信息以及所有用户和组记录都是最新的。

此外， DirectoryManagerService还让您能够创建和管理域。 域定义了不同的用户群。 通常根据组织结构或用户存储设置方式定义域边界。 用户管理域提供身份验证提供程序和目录服务提供程序使用的配置设置。

在User Management导出的配置XML中，具有属性值的根节点 `Domains` 包含为用户管理定义的每个域的XML元素。 这些元素中的每一个都包含定义与特定服务提供者相关联的领域方面的其他元素。

**了解objectSID值**

使用Active Directory时，必须了解 `objectSID` 值不是跨多个域的唯一属性。 此值存储对象的安全标识符。 在多域环境（例如，域树）中， `objectSID` 值可以不同。

An `objectSID` 如果将对象从一个Active Directory域移动到另一个域，则该值会发生变化。 某些对象具有相同的 `objectSID` 值。 例如，BUILTIN\Administrators、BUILTIN\Power Users等组将具有相同的 `objectSID` 值（不考虑域）。 这些 `objectSID` 值是众所周知的。

## 添加用户 {#adding-users}

您可以使用目录管理器服务API（Java和Web服务）以编程方式将用户添加到AEM Forms。 添加用户后，您可以在执行需要用户的服务操作时使用该用户。 例如，您可以将任务分配给新用户。

### 步骤摘要 {#summary-of-steps}

要添加用户，请执行以下步骤：

1. 包括项目文件。
1. 创建DirectoryManagerService客户端。
1. 定义用户信息。
1. 将用户添加到AEM Forms。
1. 验证是否已添加用户。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请包含代理文件。

**创建DirectoryManagerService客户端**

在以编程方式执行目录管理器服务操作之前，请先创建目录管理器服务API客户端。

**定义用户信息**

使用目录管理器服务API添加新用户时，请定义该用户的信息。 通常，在添加新用户时，您会定义以下值：

* **域名**：用户所属的域(例如， `DefaultDom`)。
* **用户标识符值**：用户的标识符值(例如， `wblue`)。
* **主体类型**：用户的类型(例如，您可以指定 `USER)`.
* **名字**：用户的给定名称(例如， `Wendy`)。
* **姓氏**：用户的姓氏(例如， `Blue)`.
* **区域设置**：用户的区域设置信息。

**将用户添加到AEM Forms**

定义用户信息后，即可将用户添加到AEM Forms。 要添加用户，请调用 `DirectoryManagerServiceClient` 对象的 `createLocalUser` 方法。

**验证是否已添加用户**

您可以验证是否添加了用户，以确保未发生任何问题。 使用用户标识符值找到新用户。

**另请参阅**

[使用Java API添加用户](users.md#add-users-using-the-java-api)

[使用Web服务API添加用户](users.md#add-users-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[删除用户](users.md#deleting-users)

### 使用Java API添加用户 {#add-users-using-the-java-api}

使用目录管理器服务API (Java)添加用户：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-usermanager-client.jar。

1. 创建DirectoryManagerServices客户端。

   创建 `DirectoryManagerServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 包含连接属性的对象。

1. 定义用户信息。

   * 创建 `UserImpl` 对象。
   * 通过调用 `UserImpl` 对象的 `setDomainName` 方法。 传递指定域名的字符串值。
   * 通过调用 `UserImpl` 对象的 `setPrincipalType` 方法。 传递一个指定用户类型的字符串值。 例如，您可以指定 `USER`.
   * 通过调用 `UserImpl` 对象的 `setUserid` 方法。 传递一个指定用户标识符值的字符串值。 例如，您可以指定 `wblue`.
   * 通过调用 `UserImpl` 对象的 `setCanonicalName` 方法。 传递一个指定用户规范名称的字符串值。 例如，您可以指定 `wblue`.
   * 通过调用 `UserImpl` 对象的 `setGivenName` 方法。 传递一个指定用户给定名称的字符串值。 例如，您可以指定 `Wendy`.
   * 通过调用 `UserImpl` 对象的 `setFamilyName` 方法。 传递一个指定用户姓氏的字符串值。 例如，您可以指定 `Blue`.

   >[!NOTE]
   >
   >调用属于 `UserImpl` 对象以设置其他值。 例如，可以通过调用 `UserImpl` 对象的 `setLocale` 方法。

1. 将用户添加到AEM Forms。

   调用 `DirectoryManagerServiceClient` 对象的 `createLocalUser` 方法并传递以下值：

   * 此 `UserImpl` 表示新用户的对象
   * 表示用户密码的字符串值

   此 `createLocalUser` 方法会返回一个指定本地用户标识符值的字符串值。

1. 验证是否已添加用户。

   * 创建 `PrincipalSearchFilter` 对象。
   * 通过调用 `PrincipalSearchFilter` 对象的 `setUserId` 方法。 传递表示用户标识符值的字符串值。
   * 调用 `DirectoryManagerServiceClient` 对象的 `findPrincipals` 方法并传递 `PrincipalSearchFilter` 对象。 此方法会返回 `java.util.List` 实例，其中每个元素为 `User` 对象。 循环访问 `java.util.List` 实例以查找用户。

**另请参阅**

[步骤摘要](users.md#summary-of-steps)

[快速入门（SOAP模式）：使用Java API添加用户](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-adding-users-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API添加用户 {#add-users-using-the-web-service-api}

使用目录管理器服务API（Web服务）添加用户：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 请确保为服务引用使用以下WSDL定义： `http://localhost:8080/soap/services/DirectoryManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` ，其中包含托管AEM Forms的服务器的IP地址。

1. 创建DirectoryManagerService客户端。

   * 创建 `DirectoryManagerServiceClient` 对象使用默认构造函数。
   * 创建 `DirectoryManagerServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`)。 您无需使用 `lc_version` 属性。 此属性在创建服务引用时使用。 请确保您指定 `?blob=mtom`.
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `DirectoryManagerServiceClient.Endpoint.Binding` 字段。 将返回值强制转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象的 `MessageEncoding` 字段至 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`.
      * 将相应的密码值分配给字段 `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`.
      * 分配常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 分配常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 定义用户信息。

   * 创建 `UserImpl` 对象。
   * 通过将字符串值分配给 `UserImpl` 对象的 `domainName` 字段。
   * 通过将字符串值分配给 `UserImpl` 对象的 `principalType` 字段。 例如，您可以指定 `USER`.
   * 通过将字符串值分配给 `UserImpl` 对象的 `userid` 字段。
   * 通过将字符串值分配给 `UserImpl` 对象的 `canonicalName` 字段。
   * 通过将字符串值分配给 `UserImpl` 对象的 `givenName` 字段。
   * 通过将字符串值指定给 `UserImpl` 对象的 `familyName` 字段。

1. 将用户添加到AEM Forms。

   调用 `DirectoryManagerServiceClient` 对象的 `createLocalUser` 方法并传递以下值：

   * 此 `UserImpl` 表示新用户的对象
   * 表示用户密码的字符串值

   此 `createLocalUser` 方法会返回一个指定本地用户标识符值的字符串值。

1. 验证是否已添加用户。

   * 创建 `PrincipalSearchFilter` 对象。
   * 通过将表示用户标识符值的字符串值指定给 `PrincipalSearchFilter` 对象的 `userId` 字段。
   * 调用 `DirectoryManagerServiceClient` 对象的 `findPrincipals` 方法并传递 `PrincipalSearchFilter` 对象。 此方法会返回 `MyArrayOfUser` 集合对象，其中每个元素为 `User` 对象。 循环访问 `MyArrayOfUser` 收藏集以查找用户。

**另请参阅**

[步骤摘要](users.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 删除用户 {#deleting-users}

您可以使用目录管理器服务API（Java和Web服务）以编程方式从AEM Forms中删除用户。 删除用户后，无法再使用该用户执行需要用户的服务操作。 例如，您无法将任务分配给已删除的用户。

### 步骤摘要 {#summary_of_steps-1}

要删除用户，请执行以下步骤：

1. 包括项目文件。
1. 创建DirectoryManagerService客户端。
1. 指定要删除的用户。
1. 从AEM Forms中删除用户。

**包含项目文件**

在开发项目中包含必要的文件。 如果使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请包含代理文件。

**创建DirectoryManagerService客户端**

在以编程方式执行目录管理器服务API操作之前，请先创建目录管理器服务客户端。

**指定要删除的用户**

您可以使用用户的标识符值指定要删除的用户。

**从AEM Forms中删除用户**

要删除用户，请调用 `DirectoryManagerServiceClient` 对象的 `deleteLocalUser` 方法。

**另请参阅**

[使用Java API删除用户](users.md#delete-users-using-the-java-api)

[使用Web服务API删除用户](users.md#delete-users-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加用户](users.md#adding-users)

### 使用Java API删除用户 {#delete-users-using-the-java-api}

使用目录管理器服务API (Java)删除用户：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-usermanager-client.jar。

1. 创建DirectoryManagerService客户端。

   创建 `DirectoryManagerServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 包含连接属性的对象。

1. 指定要删除的用户。

   * 创建 `PrincipalSearchFilter` 对象。
   * 通过调用 `PrincipalSearchFilter` 对象的 `setUserId` 方法。 传递表示用户标识符值的字符串值。
   * 调用 `DirectoryManagerServiceClient` 对象的 `findPrincipals` 方法并传递 `PrincipalSearchFilter` 对象。 此方法会返回 `java.util.List` 实例，其中每个元素为 `User` 对象。 循环访问 `java.util.List` 实例以查找要删除的用户。

1. 从AEM Forms中删除用户。

   调用 `DirectoryManagerServiceClient` 对象的 `deleteLocalUser` 方法并传递的值 `User` 对象的 `oid` 字段。 调用 `User` 对象的 `getOid` 方法。 使用 `User` 对象检索自 `java.util.List` 实例。

**另请参阅**

[步骤摘要](users.md#summary-of-steps)

[快速启动（EJB模式）：使用Java API删除用户](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[快速入门（SOAP模式）：使用Java API删除用户](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API删除用户 {#delete-users-using-the-web-service-api}

使用目录管理器服务API（Web服务）删除用户：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-usermanager-client.jar。

1. 创建DirectoryManagerService客户端。

   * 创建 `DirectoryManagerServiceClient` 对象使用默认构造函数。
   * 创建 `DirectoryManagerServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/DirectoryManagerService?blob=mtom`)。 您无需使用 `lc_version` 属性。 此属性在创建服务引用时使用。 请确保您指定 `blob=mtom.`
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `DirectoryManagerServiceClient.Endpoint.Binding` 字段。 将返回值强制转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象的 `MessageEncoding` 字段至 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `DirectoryManagerServiceClient.ClientCredentials.UserName.UserName`.
      * 将相应的密码值分配给字段 `DirectoryManagerServiceClient.ClientCredentials.UserName.Password`.
      * 分配常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 分配常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 指定要删除的用户。

   * 创建 `PrincipalSearchFilter` 对象。
   * 通过将字符串值分配给 `PrincipalSearchFilter` 对象的 `userId` 字段。
   * 调用 `DirectoryManagerServiceClient` 对象的 `findPrincipals` 方法并传递 `PrincipalSearchFilter` 对象。 此方法会返回 `MyArrayOfUser` 集合对象，其中每个元素为 `User` 对象。 循环访问 `MyArrayOfUser` 收藏集以查找用户。 此 `User` 对象检索自 `MyArrayOfUser` 收藏集对象用于删除用户。

1. 从AEM Forms中删除用户。

   通过传递 `User` 对象的 `oid` 字段值到 `DirectoryManagerServiceClient` 对象的 `deleteLocalUser` 方法。

**另请参阅**

[步骤摘要](users.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 创建组 {#creating-groups}

您可以使用目录管理器服务API（Java和Web服务）以编程方式创建AEM Forms组。 创建组后，可以使用该组执行需要组的服务操作。 例如，您可以将用户分配给新组。 (请参阅 [管理用户和组](users.md#managing-users-and-groups).)

### 步骤摘要 {#summary_of_steps-2}

要创建组，请执行以下步骤：

1. 包括项目文件。
1. 创建DirectoryManagerService客户端。
1. 确定组不存在。
1. 创建组。
1. 对组执行操作。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

有关这些JAR文件位置的信息，请参见 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建DirectoryManagerService客户端**

在以编程方式执行目录管理器服务操作之前，请先创建目录管理器服务API客户端。

**确定组是否存在**

创建组时，请确保该组不在同一域中。 也就是说，两个组不能在同一域中具有相同的名称。 要执行此任务，请执行搜索并根据两个值筛选搜索结果。 将主体类型设置为 `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP` 以确保仅返回组。 另外，请确保指定域名。

**创建组**

确定域中不存在该组后，请创建该组并指定以下属性：

* **公用名**：组的名称。
* **域**：添加组的域。
* **描述**：组的描述。

**对组执行操作**

创建组后，可以使用该组执行操作。 例如，可以向组中添加用户。 要将用户添加到组，请检索用户和组的唯一标识符值。 将这些值传递给 `addPrincipalToLocalGroup` 方法。

**另请参阅**

[使用Java API创建组](users.md#create-groups-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加用户](users.md#adding-users)

[删除用户](users.md#deleting-users)

### 使用Java API创建组 {#create-groups-using-the-java-api}

使用目录管理器服务API (Java)创建组：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-usermanager-client.jar。

1. 创建DirectoryManagerService客户端。

   创建 `DirectoryManagerServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 包含连接属性的对象。

1. 确定组是否存在。

   * 创建 `PrincipalSearchFilter` 对象。
   * 通过调用 `PrincipalSearchFilter` 对象的 `setPrincipalType` 对象。 传递值 `com.adobe.idp.um.api.infomodel.Principal.PRINCIPALTYPE_GROUP`.
   * 通过调用 `PrincipalSearchFilter` 对象的 `setSpecificDomainName` 对象。 传递指定域名的字符串值。
   * 要查找组，请调用 `DirectoryManagerServiceClient` 对象的 `findPrincipals` 方法（主体可以是组）。 传递 `PrincipalSearchFilter` 指定主体类型和域名的对象。 此方法会返回 `java.util.List` 其中每个元素为 `Group` 实例。 每个组实例都符合通过使用 `PrincipalSearchFilter` 对象。
   * 循环访问 `java.util.List` 实例。 对于每个元素，检索组名。 确保组名不等于新组名。

1. 创建组。

   * 如果组不存在，则调用 `Group` 对象的 `setCommonName` 方法，并传递一个指定组名的字符串值。
   * 调用 `Group` 对象的 `setDescription` 方法，并传递一个指定组描述的字符串值。
   * 调用 `Group` 对象的 `setDomainName` 方法，并传递一个指定域名的字符串值。
   * 调用 `DirectoryManagerServiceClient` 对象的 `createLocalGroup` 方法并传递 `Group` 实例。

   此 `createLocalUser` 方法会返回一个指定本地用户标识符值的字符串值。

1. 对组执行操作。

   * 创建 `PrincipalSearchFilter` 对象。
   * 通过调用 `PrincipalSearchFilter` 对象的 `setUserId` 方法。 传递表示用户标识符值的字符串值。
   * 调用 `DirectoryManagerServiceClient` 对象的 `findPrincipals` 方法并传递 `PrincipalSearchFilter` 对象。 此方法会返回 `java.util.List` 实例，其中每个元素为 `User` 对象。 循环访问 `java.util.List` 实例以查找用户。
   * 通过调用 `DirectoryManagerServiceClient` 对象的 `addPrincipalToLocalGroup` 方法。 传递的返回值 `User` 对象的 `getOid` 方法。 传递的返回值 `Group` 对象的 `getOid` 方法(使用 `Group` 表示新组的实例)。

**另请参阅**

[步骤摘要](users.md#summary-of-steps)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 管理用户和组 {#managing-users-and-groups}

本主题介绍如何使用(Java)以编程方式分配、删除和查询域、用户和组。

>[!NOTE]
>
>配置域时，必须为组和用户设置唯一标识符。 选择的属性不仅必须在LDAP环境中是唯一的，还必须不可变，并且不会在目录中更改。 此属性还必须属于简单字符串数据类型(Active Directory 2000/2003当前允许的唯一例外为 `"objectsid"`，二进制值)。 Novell eDirectory属性 `"GUID"`例如，不是简单的字符串数据类型，因此将无法使用。

* 对于Active Directory，使用 `"objectsid"`.
* 对于SunOne，使用 `"nsuniqueid"`.

>[!NOTE]
>
>不支持在进行LDAP目录同步时创建多个本地用户和组。 尝试此过程可能会导致错误。

### 步骤摘要 {#summary_of_steps-3}

要管理用户和组，请执行以下步骤：

1. 包括项目文件。
1. 创建DirectoryManagerService客户端。
1. 调用相应的用户或组操作。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建DirectoryManagerService客户端**

您必须先创建目录管理器服务客户端，然后才能以编程方式执行目录管理器服务操作。 使用Java API，可通过创建 `DirectoryManagerServiceClient` 对象。 使用Web服务API，可通过创建 `DirectoryManagerServiceService` 对象。

**调用相应的用户或组操作**

创建服务客户端后，可以调用用户或组管理操作。 服务客户端允许您分配、删除和查询域、用户和组。 请注意，可以将目录承担者或本地承担者添加到本地组，但不能将本地承担者添加到目录组。

**另请参阅**

[使用Java API管理用户和组](users.md#managing-users-and-groups-using-the-java-api)

[使用Web服务API管理用户和组](users.md#managing-users-and-groups-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[用户管理器API快速入门](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### 使用Java API管理用户和组 {#managing-users-and-groups-using-the-java-api}

要使用(Java)以编程方式管理用户、组和域，请执行以下任务：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-usermanager-client.jar。 有关这些文件的位置的信息，请参见 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. 创建DirectoryManagerService客户端。

   创建 `DirectoryManagerServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 包含连接属性的对象。 有关信息，请参阅 [设置连接属性&#x200B;](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)*.*

1. 调用相应的用户或组操作。

   要查找用户或组，请调用 `DirectoryManagerServiceClient` 对象查找承担者的方法（因为承担者可以是用户或组）。 在以下示例中， `findPrincipals` 使用搜索过滤器(a)调用方法 `PrincipalSearchFilter` 对象)。

   因为在此例中，返回值为 `java.util.List` 包含 `Principal` 对象，遍历结果并强制转换 `Principal` 对象的 `User` 或 `Group` 对象。

   使用结果 `User` 或 `Group` 对象(都继承自 `Principal` 界面)，检索工作流中所需的信息。 例如，域名和规范名称值组合唯一标识主体。 这些请求可通过调用 `Principal` 对象的 `getDomainName` 和 `getCanonicalName` 方法。

   要删除本地用户，请调用 `DirectoryManagerServiceClient` 对象的 `deleteLocalUser` 方法，并传递用户的标识符。

   要删除本地组，请调用 `DirectoryManagerServiceClient` 对象的 `deleteLocalGroup` 方法，并传递组的标识符。

**另请参阅**

[步骤摘要](users.md#summary-of-steps)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API管理用户和组 {#managing-users-and-groups-using-the-web-service-api}

要使用“目录管理器服务API”（Web服务）以编程方式管理用户、组和域，请执行以下任务：

1. 包括项目文件。

   * 创建使用目录管理器WSDL的Microsoft .NET客户端程序集。 (请参阅 [使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * 引用Microsoft .NET客户端程序集。 (请参阅 [创建使用Base64编码的.NET客户端程序集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. 创建DirectoryManagerService客户端。

   创建 `DirectoryManagerServiceService` 对象的proxy类的构造函数。

1. 调用相应的用户或组操作。

   要查找用户或组，请调用 `DirectoryManagerServiceService` 对象查找承担者的方法（因为承担者可以是用户或组）。 在以下示例中， `findPrincipalsWithFilter` 使用搜索过滤器(a)调用方法 `PrincipalSearchFilter` 对象)。 使用 `PrincipalSearchFilter` 对象，仅当 `isLocal` 属性设置为 `true`. 此行为与Java API的情况不同。

   >[!NOTE]
   >
   >如果未在搜索筛选器中指定最大结果数(通过 `PrincipalSearchFilter.resultsMax` 字段)，最多可返回1000个结果。 这与使用Java API时的行为不同，在Java API中，默认最大值为10个结果。 此外，搜索方法如 `findGroupMembers` 将不会产生任何结果，除非在搜索筛选条件中指定了最大结果数(例如，通过 `GroupMembershipSearchFilter.resultsMax` 字段)。 这适用于继承自 `GenericSearchFilter` 类。 有关更多信息，请参阅 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   因为在此例中，返回值是 `object[]` 包含 `Principal` 对象，遍历结果并强制转换 `Principal` 对象的 `User` 或 `Group` 对象。

   使用结果 `User` 或 `Group` 对象(都继承自 `Principal` 界面)，检索工作流中所需的信息。 例如，域名和规范名称值组合唯一标识主体。 这些请求可通过调用 `Principal` 对象的 `domainName` 和 `canonicalName` 字段。

   要删除本地用户，请调用 `DirectoryManagerServiceService` 对象的 `deleteLocalUser` 方法，并传递用户的标识符。

   要删除本地组，请调用 `DirectoryManagerServiceService` 对象的 `deleteLocalGroup` 方法，并传递组的标识符。

**另请参阅**

[步骤摘要](users.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 管理角色和权限 {#managing-roles-and-permissions}

本主题介绍如何使用授权管理器服务API (Java)以编程方式分配、删除和确定角色和权限。

在AEM Forms中， *角色* 是用于访问一个或多个系统级资源的一组权限。 这些权限通过“用户管理”创建，并由服务组件强制执行。 例如，管理员可以将“策略集作者”的角色分配给一组用户。 然后，Rights Management将允许该组中具有该角色的用户通过管理控制台创建策略集。

有两种类型的角色： *默认角色* 和 *自定义角色*. 默认角色(*系统角色)* 已驻留在AEM Forms。 假定管理员不能删除或修改默认角色，因此这些角色是不可变的。 管理员创建的自定义角色随后可能会进行修改或删除，因此这些角色是可变的。

角色使权限管理更轻松。 当角色分配给承担者时，一组权限会自动分配给该承担者，承担者的所有特定访问相关决策都基于该总体分配权限集。

### 步骤摘要 {#summary_of_steps-4}

要管理角色和权限，请执行以下步骤：

1. 包括项目文件。
1. 创建AuthorizationManagerService客户端。
1. 调用相应的角色或权限操作。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建AuthorizationManagerService客户端**

必须先创建AuthorizationManagerService客户端，然后才能以编程方式执行用户管理AuthorizationManagerService操作。 使用Java API，可通过创建 `AuthorizationManagerServiceClient` 对象。

**调用相应的角色或权限操作**

创建服务客户端后，您可以调用角色或权限操作。 通过服务客户端，您可以分配、删除和确定角色和权限。

**另请参阅**

[使用Java API管理角色和权限](users.md#managing-roles-and-permissions-using-the-java-api)

[使用Web服务API管理角色和权限](users.md#managing-roles-and-permissions-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[用户管理器API快速入门](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

### 使用Java API管理角色和权限 {#managing-roles-and-permissions-using-the-java-api}

要使用授权管理器服务API (Java)管理角色和权限，请执行以下任务：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-usermanager-client.jar。

1. 创建AuthorizationManagerService客户端。

   创建 `AuthorizationManagerServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 包含连接属性的对象。

1. 调用相应的角色或权限操作。

   要将角色分配给承担者，请调用 `AuthorizationManagerServiceClient` 对象的 `assignRole` 方法并传递以下值：

   * A `java.lang.String` 包含角色标识符的对象
   * 数组 `java.lang.String` 包含主体标识符的对象。

   要从主体中删除角色，请调用 `AuthorizationManagerServiceClient` 对象的 `unassignRole` 方法并传递以下值：

   * A `java.lang.String` 包含角色标识符的对象。
   * 数组 `java.lang.String` 包含主体标识符的对象。

**另请参阅**

[步骤摘要](users.md#summary-of-steps)

[快速入门（SOAP模式）：使用Java API管理角色和权限](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API管理角色和权限 {#managing-roles-and-permissions-using-the-web-service-api}

使用授权管理器服务API（Web服务）管理角色和权限：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/AuthorizationManagerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` ，其中包含托管AEM Forms的服务器的IP地址。

1. 创建AuthorizationManagerService客户端。

   * 创建 `AuthorizationManagerServiceClient` 对象使用默认构造函数。
   * 创建 `AuthorizationManagerServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/AuthorizationManagerService?blob=mtom`.) 您无需使用 `lc_version` 属性。 此属性在创建服务引用时使用。
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `AuthorizationManagerServiceClient.Endpoint.Binding` 字段。 将返回值强制转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象的 `MessageEncoding` 字段至 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `AuthorizationManagerServiceClient.ClientCredentials.UserName.UserName`.
      * 将相应的密码值分配给字段 `AuthorizationManagerServiceClient.ClientCredentials.UserName.Password`.
      * 分配常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 分配常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 调用相应的角色或权限操作。

   要将角色分配给承担者，请调用 `AuthorizationManagerServiceClient` 对象的 `assignRole` 方法并传递以下值：

   * A `string` 包含角色标识符的对象
   * A `MyArrayOf_xsd_string` 包含主体标识符的对象。

   要从主体中删除角色，请调用 `AuthorizationManagerServiceService` 对象的 `unassignRole` 方法并传递以下值：

   * A `string` 包含角色标识符的对象。
   * 数组 `string` 包含主体标识符的对象。

**另请参阅**

[步骤摘要](users.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 验证用户 {#authenticating-users}

本主题介绍如何使用Authentication Manager服务API (Java)使客户端应用程序能够以编程方式对用户进行身份验证。

与存储安全数据的企业数据库或其他企业资料档案库交互可能需要用户身份验证。

例如，假设用户在网页中输入用户名和密码，并将值提交到托管Forms的J2EE应用程序服务器。 Forms自定义应用程序可以使用Authentication Manager服务对用户进行身份验证。

如果验证成功，应用程序将访问受保护的企业数据库。 否则，将向用户发送一条消息，说明该用户不是授权用户。

下图显示了应用程序的逻辑流。

![au_au_umauth_process](assets/au_au_umauth_process.png)

下表描述了此图中的步骤

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
   <td><p>用户访问网站并指定用户名和密码。 此信息将提交给托管AEM Forms的J2EE应用程序服务器。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>用户凭据通过Authentication Manager服务进行身份验证。 如果用户凭据有效，工作流将继续执行步骤3。 否则，将向用户发送一条消息，说明该用户不是授权用户。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>从安全企业数据库中检索用户信息和表单设计。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>用户信息与表单设计合并，并且表单呈现给用户。 </p></td>
  </tr>
 </tbody>
</table>

### 步骤摘要 {#summary_of_steps-5}

要以编程方式验证用户，请执行以下步骤：

1. 包括项目文件。
1. 创建AuthenticationManagerService客户端。
1. 调用身份验证操作。
1. 如有必要，请检索上下文，以便客户端应用程序可以将其转发到另一个AEM Forms服务进行身份验证。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建AuthenticationManagerService客户端**

必须先创建AuthenticationManagerService客户端，然后才能以编程方式对用户进行身份验证。 使用Java API时，创建 `AuthenticationManagerServiceClient` 对象。

**调用身份验证操作**

创建服务客户端后，可以调用身份验证操作。 此操作将需要有关用户的信息，例如用户名和密码。 如果用户未进行身份验证，则会引发异常。

**检索身份验证上下文**

对用户进行身份验证后，即可基于经过身份验证的用户创建上下文。 然后，您可以使用内容调用其他AEM Forms服务。 例如，您可以使用上下文创建 `EncryptionServiceClient` 并用密码加密PDF文档。 确保经过身份验证的用户具有名为的角色 `Services User` 调用AEM Forms服务所需的其他资源。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[用户管理器API快速入门](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[使用密码加密PDF文档](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API验证用户 {#authenticate-a-user-using-the-java-api}

使用Authentication Manager服务API (Java)对用户进行身份验证：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-usermanager-client.jar。

1. 创建AuthenticationManagerServices客户端。

   创建 `AuthenticationManagerServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 包含连接属性的对象。

1. 调用身份验证操作。

   调用 `AuthenticationManagerServiceClient` 对象的 `authenticate` 方法并传递以下值：

   * A `java.lang.String` 包含用户名的对象。
   * 字节数组(a) `byte[]` 对象)，其中包含用户的密码。 您可以获取 `byte[]` 对象，方法是调用 `java.lang.String` 对象的 `getBytes` 方法。

   身份验证方法返回 `AuthResult` 对象，其中包含有关已验证用户的信息。

1. 检索身份验证上下文。

   调用 `ServiceClientFactory` 对象的 `getContext` 方法，它将返回 `Context` 对象。

   然后调用 `Context` 对象的 `initPrincipal` 方法并传递 `AuthResult`.

### 使用Web服务API验证用户 {#authenticate-a-user-using-the-web-service-api}

使用Authentication Manager服务API（Web服务）对用户进行身份验证：

1. 包括项目文件。

   * 创建使用Authentication Manager WSDL的Microsoft .NET客户端程序集。 (请参阅 [使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * 引用Microsoft .NET客户端程序集。 (请参阅中的“引用.NET客户端程序集” [使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)

1. 创建AuthenticationManagerService客户端。

   创建 `AuthenticationManagerServiceService` 对象的proxy类的构造函数。

1. 调用身份验证操作。

   调用 `AuthenticationManagerServiceClient` 对象的 `authenticate` 方法并传递以下值：

   * A `string` 包含用户名的对象
   * 字节数组(a) `byte[]` 对象)，其中包含用户的密码。 您可以获取 `byte[]` 对象通过转换 `string` 包含密码的对象 `byte[]` 数组，其逻辑如下例所示。
   * 返回的值将为 `AuthResult` 对象，可用于检索有关用户的信息。 在以下示例中，通过首先获取 `AuthResult` 对象的 `authenticatedUser` 字段并随后获得结果 `User` 对象的 `canonicalName` 和 `domainName` 字段。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 以编程方式同步用户 {#programmatically-synchronizing-users}

您可以使用用户管理API以编程方式同步用户。 在同步用户时，您将使用用户存储库中的用户数据更新AEM Forms。 例如，假设您将新用户添加到用户存储库中。 执行同步操作后，新用户将成为AEM Forms用户。 此外，用户存储库中不再存在的用户也将从AEM Forms中删除。

下图显示了AEM Forms与用户存储库进行同步的情况。

![ps_ps_umauth_sync](assets/ps_ps_umauth_sync.png)

下表描述了此图中的步骤

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
   <td><p>用户能够查看更新的用户信息。 </p></td>
  </tr>
 </tbody>
</table>

### 步骤摘要 {#summary_of_steps-6}

要以编程方式同步用户，请执行以下步骤：

1. 包括项目文件。
1. 创建UserManagerUtilServiceClient客户端。
1. 指定企业域。
1. 调用身份验证操作。
1. 确定同步操作是否已完成

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建UserManagerUtilServiceClientclient**

在以编程方式同步用户之前，您必须创建 `UserManagerUtilServiceClient` 对象。

**指定企业域**

在使用用户管理API执行同步操作之前，请指定用户所属的企业域。 可以指定一个或多个企业域。 必须先使用Administration Console设置企业域，然后才能以编程方式执行同步操作。 (请参阅 [管理帮助](https://www.adobe.com/go/learn_aemforms_admin_63).)

**调用同步操作**

指定一个或多个企业域后，可以执行同步操作。 执行此操作所需的时间取决于用户存储库中的用户记录数。

**确定同步操作是否已完成**

以编程方式执行同步操作后，可以确定操作是否已完成。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[用户管理器API快速入门](/help/forms/developing/user-manager-java-api-quick.md#user-manager-java-api-quick-start-soap)

[使用密码加密PDF文档](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API以编程方式同步用户 {#programmatically-synchronizing-users-using-the-java-api}

使用用户管理API (Java)同步用户：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-usermanager-client.jar和adobe-usermanager-util-client.jar。

1. 创建UserManagerUtilServiceClient客户端。

   创建 `UserManagerUtilServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 包含连接属性的对象。

1. 指定企业域。

   * 调用 `UserManagerUtilServiceClient` 对象的 `scheduleSynchronization` 启动用户同步操作的方法。
   * 创建 `java.util.Set` 使用实例 `HashSet` 构造函数。 请确保您指定 `String` 作为数据类型。 此 `Java.util.Set` 实例存储同步操作应用于的域名。
   * 对于要添加的每个域名，调用 `java.util.Set` 对象的add方法并传递域名。

1. 调用同步操作。

   调用 `ServiceClientFactory` 对象的 `getContext` 方法，它将返回 `Context` 对象。

   然后调用 `Context` 对象的 `initPrincipal` 方法并传递 `AuthResult`.

**另请参阅**

[以编程方式同步用户](users.md#programmatically-synchronizing-users)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
