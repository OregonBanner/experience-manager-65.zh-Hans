---
title: 使用策略保护文档
seo-title: 使用策略保护文档
description: 'null'
seo-description: 'null'
uuid: 6feb69ef-7b61-4d0b-8c87-d65d98bae9b5
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9b1d2bf3-f28c-41b2-9026-1f3311556422
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# 使用策略保护文档 {#protecting-documents-with-policies}

**关于Document Security Service**

Document security服务使用户能够对Adobe PDF文档动态应用机密性设置，并保持对文档的控制，无论文档的分发范围有多广。

Document Security服务使用户能够保持对收件人使用受策略保护的PDF文档的方式的控制，从而防止信息扩散到用户的范围之外。 用户可以指定谁可以打开文档、限制文档的使用方式以及文档分发后的监控。 用户还可以动态控制对受策略保护的文档的访问，甚至可以动态撤销对文档的访问权。

Document security服务还保护其他文件类型，如Microsoft Word文件（DOC文件）。 您可以使用Document Security Client API处理这些文件类型。 支持以下版本：

* Microsoft Office 2003文件（DOC、XLS、PPT文件）
* Microsoft Office 2007文件（DOCX、XLSX、PPTX文件）
* PTC Pro/E文件

特此说明，以下两节将讨论如何使用Word文档：

* [对Word文档应用策略](protecting-documents-policies.md#applying-policies-to-word-documents)
* [从Word文档删除策略](protecting-documents-policies.md#removing-policies-from-word-documents)

您可以使用Document Security服务完成以下任务：

* 创建策略。 有关信息，请参阅 [创建策略](protecting-documents-policies.md#creating-policies)。
* 修改策略。 有关信息，请参阅 [修改策略](protecting-documents-policies.md#modifying-policies)。
* 删除策略。 有关信息，请参阅 [删除策略](protecting-documents-policies.md#deleting-policies)。
* 将策略应用于PDF文档。 有关信息，请参 [阅将策略应用于PDF文档](protecting-documents-policies.md#applying-policies-to-pdf-documents)。
* 从PDF文档中删除策略。 有关信息，请参 [阅从PDF文档删除策略](protecting-documents-policies.md#removing-policies-from-pdf-documents)。
* 检查受策略保护的文档。 有关信息，请参阅检 [查受策略保护的PDF文档](protecting-documents-policies.md#inspecting-policy-protected-pdf-documents)。
* 撤销对PDF文档的访问权。 有关信息，请参 [阅撤销对文档的访问](protecting-documents-policies.md#revoking-access-to-documents)。
* 恢复对已吊销文档的访问权限。 有关信息，请参阅 [恢复对已吊销文档的访问](protecting-documents-policies.md#reinstating-access-to-revoked-documents)。
* 创建水印。 有关信息，请参阅 [创建水印](protecting-documents-policies.md#creating-watermarks)。
* 搜索活动。 有关信息，请参阅 [搜索事件](protecting-documents-policies.md#searching-for-events)。

>[!NOTE]
>
>有关Document security服务的详细信息，请参阅AEM [表单的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 创建策略 {#creating-policies}

您可以使用Document Security Java API或Web服务API以编程方式创建策略。 策 *略* 是包含文档安全性设置、授权用户和使用权限的信息集合。 您可以使用适用于不同情况和用户的安全设置来创建和保存任意数量的策略。

策略允许您执行以下任务：

* 指定可打开文档的个人。 收件人可以属于您的组织，也可以是您的组织之外的收件人。
* 指定收件人如何使用文档。 您可以限制对不同Acrobat和Adobe Reader功能的访问。 这些功能包括打印和复制文本、添加签名以及向文档添加注释的功能。
* 随时更改访问和安全设置，即使在分发受策略保护的文档后也是如此。
* 分发文档后，监控文档的使用情况。 您可以查看文档的使用方式以及使用者。 例如，您可以了解某人何时打开了文档。

### 使用Web服务创建策略 {#creating-a-policy-using-web-services}

使用Web服务API创建策略时，请引用描述策略的现有可移植文档权限语言(PDRL)XML文件。 策略权限和主体在PDRL文档中定义。 以下XML文档是PDRL文档的一个示例。

```as3
 <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
 <Policy PolicyInstanceVersion="1" PolicyID="5DA3F847-DE76-F9CC-63EA-49A8D59154DE" PolicyCreationTime="2004-08-30T00:02:28.294+00:00" PolicyType="1" PolicySchemaVersion="1.0" PolicyName="SDK Test Policy -4344050357301573237" PolicyDescription="An SDK Test policy" xmlns="https://www.adobe.com/schema/1.0/pdrl">
       <PolicyEntry>
          <ns1:Permission PermissionName="com.adobe.aps.onlineOpen" Access="ALLOW" xmlns:ns1="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns2:Permission PermissionName="com.adobe.aps.offlineOpen" Access="ALLOW" xmlns:ns2="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns3:Permission PermissionName="com.adobe.aps.pdf.editNotes" Access="ALLOW" xmlns:ns3="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns4:Permission PermissionName="com.adobe.aps.pdf.fillAndSign" Access="ALLOW" xmlns:ns4="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
          <Principal PrincipalNameType="SYSTEM">
             <PrincipalDomain>EDC_SPECIAL</PrincipalDomain>
 
             <PrincipalName>all_internal_users</PrincipalName>
          </Principal>
       </PolicyEntry>
       <PolicyEntry>
          <ns5:Permission PermissionName="com.adobe.aps.onlineOpen" Access="ALLOW" xmlns:ns5="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns6:Permission PermissionName="com.adobe.aps.offlineOpen" Access="ALLOW" xmlns:ns6="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns7:Permission PermissionName="com.adobe.aps.pdf.copy" Access="ALLOW" xmlns:ns7="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns8:Permission PermissionName="com.adobe.aps.pdf.printLow" Access="ALLOW" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" xmlns:ns8="https://www.adobe.com/schema/1.0/pdrl" />
 
          <ns9:Permission PermissionName="com.adobe.aps.policySwitch" Access="ALLOW" xmlns:ns9="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns10:Permission PermissionName="com.adobe.aps.revoke" Access="ALLOW" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" xmlns:ns10="https://www.adobe.com/schema/1.0/pdrl" />
 
          <ns11:Permission PermissionName="com.adobe.aps.pdf.edit" Access="ALLOW" xmlns:ns11="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns12:Permission PermissionName="com.adobe.aps.pdf.editNotes" Access="ALLOW" xmlns:ns12="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns13:Permission PermissionName="com.adobe.aps.pdf.fillAndSign" Access="ALLOW" xmlns:ns13="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns14:Permission PermissionName="com.adobe.aps.pdf.printHigh" Access="ALLOW" xmlns:ns14="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <Principal PrincipalNameType="SYSTEM">
             <PrincipalDomain>EDC_SPECIAL</PrincipalDomain>
 
             <PrincipalName>publisher</PrincipalName>
          </Principal>
       </PolicyEntry>
 
       <OfflineLeasePeriod>
          <Duration>P31D</Duration>
       </OfflineLeasePeriod>
 
       <AuditSettings isTracked="true" />
 
       <PolicyValidityPeriod isAbsoluteTime="false">
          <ValidityPeriodRelative>
             <NotBeforeRelative>PT0S</NotBeforeRelative>
 
             <NotAfterRelative>P20D</NotAfterRelative>
          </ValidityPeriodRelative>
       </PolicyValidityPeriod>
 </Policy>
 
```

>[!NOTE]
>
>有关Document security服务的详细信息，请参阅AEM [表单的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary-of-steps}

要创建策略，请执行以下步骤：

1. 包括项目文件。
1. 创建Document Security Client API对象。
1. 设置策略的属性。
1. 创建策略条目。
1. 注册策略。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-rightsmanagement-client.jar
* namespace.jar（如果AEM Forms部署在JBoss上）
* jaxb-api.jar（如果AEM Forms部署在JBoss上）
* jaxb-impl.jar（如果AEM Forms部署在JBoss上）
* jaxb-libs.jar（如果AEM Forms部署在JBoss上）
* jaxb-xjc.jar（如果AEM Forms部署在JBoss上）
* lexpangDatatype.jar（如果AEM Forms部署在JBoss上）
* xsdlib.jar（如果AEM Forms部署在JBoss上）
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar
* jbossall-client.jar（如果AEM Forms未部署在JBoss上，请使用其他JAR文件）

有关这些JAR文件的位置的信息，请参 [阅包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建Document Security Client API对象**

在以编程方式执行Document security服务操作之前，请先创建Document security服务客户端对象。

**设置策略的属性**

要创建策略，请设置策略属性。 策略名称是必填属性。 策略名称必须对于每个策略集都是唯一的。 策略集只是策略的集合。 如果策略属于单独的策略集，则可以有两个同名的策略。 但是，单个策略集中的两个策略不能具有相同的策略名称。

要设置的另一个有用属性是有效期。 有效期是授权接收者可以访问受策略保护的文档的时间段。 如果未设置此属性，则策略始终有效。

有效期可以设置为以下选项之一：

* 从文档发布之日起文档可访问的设定天数
* 文档无法访问的结束日期
* 文档可访问的特定日期范围
* 始终有效

您只能指定开始日期，这会导致策略在开始日期之后有效。 如果仅指定结束日期，则策略在结束日期之前有效。 但是，如果未定义开始日期和结束日期，则会引发异常。

在设置属于策略的属性时，您还可以设置加密设置。 这些加密设置在将策略应用到文档时会生效。 您可以指定以下加密值：

* **AES256**:使用256位密钥表示AES加密算法。
* **AES128**:使用128位密钥表示AES加密算法。
* **** 无加密：表示无加密。

指定选 `NoEncryption` 项时，不能将选 `PlaintextMetadata` 项设置为 `false`。 如果尝试这样做，则会引发异常。

>[!NOTE]
>
>有关可设置的其他属性的信息，请参阅 `Policy`[AEM Forms API参考中的界面说明](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**创建策略条目**

策略条目将主体（即组和用户）和权限附加到策略。 政策必须至少包含一个政策条目。 例如，假设您执行以下任务：

* 创建并注册一个策略条目，该条目使用户组只能联机查看文档并禁止收件人复制文档。
* 将策略条目附加到策略。
* 使用Acrobat保护包含策略的文档。

这些操作导致收件人只能联机查看文档，而无法复制文档。 在从文档删除安全性之前，文档将保持安全。

**注册策略**

必须先注册新策略，才能使用新策略。 在注册策略后，可以使用它保护文档。

### 使用Java API创建策略 {#create-a-policy-using-the-java-api}

使用Document Security API(Java)创建策略：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-rightsmanagement-client.jar。

1. 创建Document Security Client API对象。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `DocumentSecurityClient` 象的构造函数并传递该对象来创建 `ServiceClientFactory` 对象。

1. 设置策略的属性。

   * 通过 `Policy` 调用对象的静态 `InfomodelObjectFactory` 方法创建对 `createPolicy` 象。 此方法返回一个 `Policy` 对象。
   * 通过调用对象的方法并传递指定策 `Policy` 略名称的 `setName` 字符串值来设置策略的名称属性。
   * 通过调用对象的方法并传递一个 `Policy` 指定策略 `setDescription` 描述的字符串值来设置策略的描述。
   * 通过调用对象的方法并传递指定策略集名称的 `Policy` 字符串值， `setPolicySetName` 设置新策略所属的策略集。 (可以为此参 `null` 数值指定导致将策略添加到“我的策略 *”策略集* 。)
   * 通过调用对象的静态方法创建策 `InfomodelObjectFactory` 略的有效期 `createValidityPeriod` 限。 此方法返回一个 `ValidityPeriod` 对象。
   * 通过调用对象的方法并传递一个指定天数的整数值，设 `ValidityPeriod` 置受策略保护的文 `setRelativeExpirationDays` 档可访问的天数。
   * 通过调用对象的方法并传递对 `Policy` 象来设置策 `setValidityPeriod` 略的有效期 `ValidityPeriod` 限。

1. 创建策略条目。

   * 通过调用对象的静态方 `InfomodelObjectFactory` 法创建策略 `createPolicyEntry` 条目。 此方法返回一个 `PolicyEntry` 对象。
   * 通过调用对象的静态方法来指 `InfomodelObjectFactory` 定策略的权 `createPermission` 限。 传递属于表示权限的接 `Permission` 口的静态数据成员。 此方法返回一个 `Permission` 对象。 例如，要添加允许用户从受策略保护的PDF文档复制数据的权限，请通过 `Permission.COPY`。 （对要添加的每个权限重复此步骤）。
   * 通过调用对象的方法并传递对象， `PolicyEntry` 将权限添 `addPermission` 加到策略条 `Permission` 目。 (对于您创建的每个对 `Permission` 象，重复此步骤)。
   * 通过调用对象的静态方 `InfomodelObjectFactory` 法创建策略主 `createSpecialPrincipal` 体。 传递属于表示主体的对 `InfomodelObjectFactory` 象的数据成员。 此方法返回一个 `Principal` 对象。 例如，要将文档的发布者添加为主体，请传递 `InfomodelObjectFactory.PUBLISHER_PRINCIPAL`。
   * 通过调用对象的方法并传递对象，将 `PolicyEntry` 主体添 `setPrincipal`加到策略条 `Principal` 目中。
   * 通过调用对象的方法并传递对象，将策 `Policy` 略条目添 `addPolicyEntry` 加到策略 `PolicyEntry` 中。

1. 注册策略。

   * 通过 `PolicyManager` 调用对象的方 `DocumentSecurityClient` 法创建对 `getPolicyManager` 象。
   * 通过调用对象的方 `PolicyManager` 法并传递以 `registerPolicy` 下值来注册策略：

      * 表示 `Policy` 要注册的策略的对象。
   * 表示策略所属的策略集的字符串值。
   如果在连接设置中使用AEM Forms管理员帐户创建对象， `DocumentSecurityClient` 则在调用方法时指定策略集名 `registerPolicy` 称。 如果为策略集 `null` 传递值，则会在管理员“我的策略”策略集 *中创建策略* 。

   如果在连接设置中使用Document security用户，则可以调用仅接受策略 `registerPolicy` 的重载方法。 即，无需指定策略集名称。 但是，该策略会添加到名为“我的策略” *的策略集*。 如果不想将新策略添加到此策略集，请在调用方法时指定策略集名 `registerPolicy` 称。

   >[!NOTE]
   >
   >创建策略时，请引用现有策略集。 如果指定的策略集不存在，则会引发异常。

有关使用Document security服务的代码示例，请参阅以下内容：

* “快速入门（SOAP模式）:使用Java API创建策略”

### 使用Web服务API创建策略 {#create-a-policy-using-the-web-service-api}

使用Document Security API（Web服务）创建策略：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建Document Security Client API对象。

   * 使用对 `DocumentSecurityServiceClient` 象的默认构造函数创建对象。
   * 使用构 `DocumentSecurityServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`.)您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。)
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `RightsManagementServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。


1. 设置策略的属性。

   * 使用对 `PolicySpec` 象的构造函数创建对象。
   * 通过为对象的数据成员分配字符串值来 `PolicySpec` 设置策略 `name` 的名称。
   * 通过为对象的数据成员分配字符串值来设 `PolicySpec` 置策略的 `description` 说明。
   * 通过为对象的数据成员分配字符串值，设置策略将属 `PolicySpec` 于的策略 `policySetName` 集。 必须指定现有策略集名称。 (可以为此参 `null` 数值指定导致将策略添加到“我的策 *略*”。)
   * 通过为对象的数据成员分配一个整数值来设置策略的 `PolicySpec` 脱机租用 `offlineLeasePeriod` 期限。
   * 使用表 `PolicySpec` 示PDRL XML数 `policyXml` 据的字符串值设置对象的数据成员。 要执行此任务，请使用。NET对 `StreamReader` 象的构造函数创建一个。 将表示策略的PDRL XML文件的位置传递给构造函 `StreamReader` 数。 接下来，调 `StreamReader` 用对象的方 `ReadLine` 法，并将返回值指定给字符串变量。 遍历对象 `StreamReader` ，直到方 `ReadLine` 法返回null。 将字符串变量指定 `PolicySpec` 给对象的数 `policyXml` 据成员。

1. 创建策略条目。

   使用Document Security web服务API创建策略时，无需创建策略条目。 策略条目在PDRL文档中定义。

1. 注册策略。

   通过调用对象的方 `DocumentSecurityServiceClient` 法并传递以 `registerPolicy` 下值来注册策略：

   * 表示 `PolicySpec` 要注册的策略的对象。
   * 表示策略所属的策略集的字符串值。 您可以指定一 `null` 个值，该值会导致将策略添加到 *MyPoliges* 策略集。
   如果在连接设置中使用AEM Forms管理员帐户创建对象， `DocumentSecurityClient` 请在调用方法时指定策略集名 `registerPolicy` 称。

   如果在连接设置中使用Document securityDocument security用户，则可以调用仅接受策略 `registerPolicy` 的重载方法。 即，无需指定策略集名称。 但是，该策略会添加到名为“我的策略” *的策略集*。 如果不想将新策略添加到此策略集，请在调用方法时指定策略集名 `registerPolicy` 称。

   >[!NOTE]
   >
   >在创建策略并指定策略集时，请确保指定现有策略集。 如果指定的策略集不存在，则会引发异常。

有关使用Document security服务的代码示例，请参阅以下快速入门：

* “快速入门(MTOM):使用Web服务API创建策略”
* “快速入门(SwaRef):使用Web服务API创建策略”

## 修改策略 {#modifying-policies}

您可以使用Document Security Java API或Web服务API修改现有策略。 要更改现有策略，请检索该策略，修改它，然后在服务器上更新该策略。 例如，假定您检索现有策略并延长其有效期。 在更改生效之前，必须更新策略。

当业务需求发生变化且策略不再反映这些需求时，您可以修改策略。 您只需更新现有策略，而不是创建新策略。

要使用Web服务修改策略属性（例如，使用使用JAX-WS创建的Java代理类），必须确保向Document security服务注册策略。 然后，您可以使用该方法引用现有策略， `PolicySpec.getPolicyXml` 并使用适用的方法修改策略属性。 例如，您可以通过调用方法来修改脱机租用期 `PolicySpec.setOfflineLeasePeriod` 限。

>[!NOTE]
>
>有关Document security服务的详细信息，请参阅AEM [表单的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-1}

要修改现有策略，请执行以下步骤：

1. 包括项目文件。
1. 创建Document Security Client API对象。
1. 检索现有策略。
1. 更改策略属性。
1. 更新策略。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建Document Security Client API对象**

在以编程方式执行Document Securityservice操作之前，必须创建Document security服务客户端对象。 如果您使用Java API，请创建一个对 `RightsManagementClient` 象。 如果您使用的是Document Security web服务API，请创建一个对 `RightsManagementServiceService` 象。

**检索现有策略**

您必须检索现有策略才能对其进行修改。 要检索策略，请指定策略名称和策略所属的策略集。 如果为策略集 `null` 名称指定了值，则将从“我的策略”策略集 *检索策略* 。

**设置策略的属性**

要修改策略，请修改策略属性的值。 唯一无法更改的策略属性是name属性。 例如，要更改策略的脱机租用期，您可以修改策略的脱机租用期属性的值。

使用Web服务修改策略的脱机租用期时，将忽 `offlineLeasePeriod` 略界面上 `PolicySpec` 的字段。 要更新脱机租用期，请修改PDRL XML `OfflineLeasePeriod` 文档中的元素。 然后，使用界面的数据成员引用更 `PolicySpec` 新的PDRL `policyXML` XML文档。

>[!NOTE]
>
>有关可设置的其他属性的信息，请参阅 `Policy`[AEM Forms API参考中的界面说明](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**更新策略**

在对策略所做的更改生效之前，必须使用Document security服务更新策略。 对保护文档的策略所做的更改将在受策略保护的文档下次与Document security服务同步时更新。

### 使用Java API修改现有策略 {#modify-existing-policies-using-the-java-api}

使用Document Security API(Java)修改现有策略：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-rightsmanagement-client.jar。

1. 创建Document Security Client API对象。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `RightsManagementClient` 象的构造函数并传递该对象来创建 `ServiceClientFactory` 对象。

1. 检索现有策略。

   * 通过 `PolicyManager` 调用对象的方 `RightsManagementClient` 法创建对 `getPolicyManager` 象。
   * 创建一 `Policy` 个对象，它通过调用对象的方法并传递以 `PolicyManager` 下值来表示 `getPolicy` 要更新的策略”

      * 一个字符串值，它表示策略所属的策略集名称。 您可以指 `null` 定导致使用策 `MyPolicies` 略集的结果。
      * 表示策略名称的字符串值。

1. 设置策略的属性。

   更改策略的属性以满足您的业务需求。 例如，要更改策略的脱机租用期，请调用对 `Policy` 象的方 `setOfflineLeasePeriod` 法。

1. 更新策略。

   通过调用对象的方 `PolicyManager` 法更新策 `updatePolicy` 略。 传递 `Policy` 表示要更新的策略的对象。

**代码示例**

有关使用Document security服务的代码示例，请参阅快速入门（SOAP模式）:使用Java API部分修改策略。

### 使用Web服务API修改现有策略 {#modify-existing-policies-using-the-web-service-api}

使用Document Security API（Web服务）修改现有策略：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建Document Security Client API对象。

   * 使用对 `RightsManagementServiceClient` 象的默认构造函数创建对象。
   * 使用构 `RightsManagementServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`.)您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。)
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `RightsManagementServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。


1. 检索现有策略。

   创建一 `PolicySpec` 个对象，它通过调用对象的方法并传递以 `RightsManagementServiceClient` 下值来表 `getPolicy` 示要修改的策略：

   * 一个字符串值，它指定策略所属的策略集名称。 您可以指 `null` 定导致使用策 `MyPolicies` 略集的结果。
   * 指定策略名称的字符串值。

1. 设置策略的属性。

   更改策略的属性以满足您的业务需求。

1. 更新策略。

   通过调用对象的方 `RightsManagementServiceClient` 法并传递表示要更 `updatePolicyFromSDK` 新的策略 `PolicySpec` 的对象来更新策略。

**代码示例**

有关使用Document security服务的代码示例，请参阅以下快速入门：

* “快速入门(MTOM):使用Web服务API修改策略”
* “快速入门(SwaRef):使用Web服务API修改策略”

## 删除策略 {#deleting-policies}

您可以使用Document Security Java API或Web服务API删除现有策略。 删除策略后，将无法再使用它保护文档。 但是，使用策略的现有受策略保护的文档仍受到保护。 当较新的策略可用时，您可以删除策略。

>[!NOTE]
>
>有关Document security服务的详细信息，请参阅AEM [表单的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-2}

要删除现有策略，请执行以下步骤：

1. 包括项目文件
1. 创建Document Security Client API对象。
1. 删除策略。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建Document Security Client API对象**

在以编程方式执行Document security服务操作之前，必须创建Document security服务客户端对象。 如果您使用Java API，请创建一个对 `RightsManagementClient` 象。 如果您使用的是Document Security web服务API，请创建一个对 `RightsManagementServiceService` 象。

**删除策略**

要删除策略，请指定要删除的策略和策略所属的策略集。 设置用于调用AEM Forms的用户必须具有删除策略的权限；否则会出现异常。 同样，如果尝试删除不存在的策略，则会出现异常。

### 使用Java API删除策略 {#delete-policies-using-the-java-api}

使用Document Security API(Java)删除策略：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-rightsmanagement-client.jar。

1. 创建Document Security Client API对象。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `RightsManagementClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 删除策略。

   * 通过 `PolicyManager` 调用对象的方 `RightsManagementClient` 法创建对 `getPolicyManager` 象。
   * 通过调用对象的方 `PolicyManager` 法并传递以 `deletePolicy` 下值来删除策略：

      * 一个字符串值，它指定策略所属的策略集名称。 您可以指 `null` 定导致使用策 `MyPolicies` 略集的结果。
      * 一个字符串值，它指定要删除的策略的名称。

**代码示例**

有关使用Document security服务的代码示例，请参阅以下快速入门：

* “快速入门（SOAP模式）:使用Java API删除策略”

### 使用Web服务API删除策略 {#delete-policies-using-the-web-service-api}

使用Document Security API（Web服务）删除策略：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建Document Security Client API对象。

   * 使用对 `RightsManagementServiceClient` 象的默认构造函数创建对象。
   * 使用构 `RightsManagementServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`.)您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。)
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `RightsManagementServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。


1. 删除策略。

   通过调用对象的方 `RightsManagementServiceClient` 法并传递以 `deletePolicy` 下值来删除策略：

   * 一个字符串值，它指定策略所属的策略集名称。 您可以指 `null` 定导致使用策 `MyPolicies` 略集的结果。
   * 一个字符串值，它指定要删除的策略的名称。

**代码示例**

有关使用Document security服务的代码示例，请参阅以下快速入门：

* “快速入门(MTOM):使用Web服务API删除策略”
* “快速入门(SwaRef):使用Web服务API删除策略”

## 将策略应用于PDF文档 {#applying-policies-to-pdf-documents}

可以对PDF文档应用策略以保护文档。 通过将策略应用于PDF文档，可限制对文档的访问。 如果文档已使用策略进行保护，则不能对文档应用策略。

在文档打开时，您还可以限制对Acrobat和Adobe reader功能的访问，包括打印和复制文本、进行更改以及向文档添加签名和注释的能力。 此外，当您不再希望用户访问受策略保护的PDF文档时，您可以撤销该文档。

在分发受策略保护的文档后，可以对其进行监视。 即，您可以查看文档的使用方式以及使用者。 例如，您可以了解某人何时打开了文档。

>[!NOTE]
>
>有关Document security服务的详细信息，请参阅AEM [表单的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-3}

要将策略应用于PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建Document Security Client API对象。
1. 检索应用了策略的PDF文档。
1. 将现有策略应用于PDF文档。
1. 保存受策略保护的PDF文档。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建Document Security Client API对象**

在以编程方式执行Document security服务操作之前，请先创建Document security服务客户端对象。 如果您使用Java API，请创建一个对 `DocumentSecurityClient` 象。 如果您使用的是Document Security web服务API，请创建一个对 `DocumentSecurityServiceService` 象。

**检索PDF文档**

您可以检索PDF文档以应用策略。 对PDF文档应用策略后，用户在使用文档时会受到限制。 例如，如果策略未启用脱机时打开文档，则用户必须联机才能打开文档。

**将现有策略应用于PDF文档**

要将策略应用于PDF文档，请引用现有策略并指定策略所属的策略集。 设置连接属性的用户必须有权访问指定的策略。 否则，会出现异常。

**保存PDF文档**

在Document security服务将策略应用于PDF文档后，您可以将受策略保护的PDF文档另存为PDF文件。

**另请参阅**

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[撤销对文档的访问权](protecting-documents-policies.md#revoking-access-to-documents)

### 使用Java API将策略应用于PDF文档 {#apply-a-policy-to-a-pdf-document-using-the-java-api}

使用Document Security API(Java)将策略应用于PDF文档：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-rightsmanagement-client.jar。

1. 创建Document Security Client API对象。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `RightsManagementClient` 象的构造函数并传递该对象来创建 `ServiceClientFactory` 对象。

1. 检索PDF文档。

   * 使用 `java.io.FileInputStream` 其构造函数创建表示PDF文档的对象。 传递指定PDF文档位置的字符串值。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对象来创建 `java.io.FileInputStream` 对象。

1. 将现有策略应用于PDF文档。

   * 通过 `DocumentManager` 调用对象的方 `RightsManagementClient` 法创建对 `getDocumentManager` 象。
   * 通过调用对象的方法并传递以下值， `DocumentManager` 将策略应 `protectDocument` 用于PDF文档：

      * 包 `com.adobe.idp.Document` 含应用策略的PDF文档的对象。
      * 指定文档名称的字符串值。
      * 一个字符串值，它指定策略所属的策略集的名称。 您可以指定 `null` 一个值，该值导致使 `MyPolicies` 用策略集。
      * 指定策略名称的字符串值。
      * 一个字符串值，它表示作为文档发布者的用户的用户管理器域的名称。 此参数值是可选的，可以为null（如果此参数为null，则下一个参数值必须是null）。
      * 一个字符串值，它表示作为文档发布者的用户管理器用户的规范名称。 此参数值是可选的，可 `null` 以是(如果此参数为null，则上一个参数值必须是 `null`)。
      * 表示 `com.adobe.livecycle.rightsmanagement.Locale` 用于选择MS office模板的区域设置。 此参数值是可选的，不用于PDF文档。 要保护PDF文档，请指定 `null`。
      该方 `protectDocument` 法返回一 `RMSecureDocumentResult` 个包含受策略保护的PDF文档的对象。


1. 保存PDF文档。

   * 调用对 `RMSecureDocumentResult` 象的方 `getProtectedDoc` 法以获取受策略保护的PDF文档。 此方法返回一个 `com.adobe.idp.Document` 对象。
   * 创建一 `java.io.File` 个对象，并确保文件扩展名为PDF。
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法，将对象的内容复制到文件中(确保使用由 `Document` 该方法返回的对 `Document``getProtectedDoc` 象)。

**代码示例**

有关使用Document security服务的代码示例，请参阅以下快速入门：

* “快速入门（EJB模式）:使用Java API将策略应用于PDF文档”
* “快速入门（SOAP模式）:使用Java API将策略应用于PDF文档”

**另请参阅**

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API将策略应用于PDF文档 {#apply-a-policy-to-a-pdf-document-using-the-web-service-api}

使用Document Security API（Web服务）将策略应用于PDF文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建Document Security Client API对象。

   * 使用对 `RightsManagementServiceClient` 象的默认构造函数创建对象。
   * 使用构 `RightsManagementServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给Forms服务(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`.)您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。)
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `RightsManagementServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。


1. 检索PDF文档。

   * 使用对 `BLOB` 象的构造函数创建对象。 对 `BLOB` 象用于存储应用了策略的PDF文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 通过获取对象的属性确定字 `System.IO.FileStream` 节数组大 `Length` 小。
   * 通过调用对象的方法，用流数据 `System.IO.FileStream` 填充字节数 `Read` 组。 传递要读取的字节数组、开始位置和流长度。
   * 通过 `BLOB` 为对象的字段指定 `MTOM` 字节数组的内容来填充该对象。

1. 将现有策略应用于PDF文档。

   通过调用对象的方法并传递以下值， `RightsManagementServiceClient` 将策略应 `protectDocument` 用于PDF文档：

   * 包 `BLOB` 含应用策略的PDF文档的对象。
   * 指定文档名称的字符串值。
   * 一个字符串值，它指定策略所属的策略集的名称。 您可以指定 `null` 一个值，该值导致使 `MyPolicies` 用策略集。
   * 指定策略名称的字符串值。
   * 一个字符串值，它表示作为文档发布者的用户的用户管理器域的名称。 此参数值是可选的，可以为null(如果此参数为null，则下一个参数值必须是 `null`null)。
   * 一个字符串值，它表示作为文档发布者的用户管理器用户的规范名称。 此参数值是可选的，可以为null(如果此参数为null，则上一个参数值必须是 `null`null)。
   * 一个 `RMLocale` 值，它指定区域设置值(例如 `RMLocale.en`)。
   * 用于存储策略标识符值的字符串输出参数。
   * 用于存储受策略保护的标识符值的字符串输出参数。
   * 用于存储mime类型的字符串输出参数(例如， `application/pdf`)。
   该方 `protectDocument` 法返回一 `BLOB` 个包含受策略保护的PDF文档的对象。

1. 保存PDF文档。

   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示受策略保护的PDF文档的文件位置。
   * 创建一个字节数组，它存储由方法返 `BLOB` 回的对象的数据内 `protectDocument` 容。 通过获取对象数据成员的值 `BLOB` 填充字节 `MTOM` 数组。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的内 `Write` 容写入PDF文件。

**代码示例**

有关使用Document security服务的代码示例，请参阅以下快速入门：

* “快速入门(MTOM):使用Web服务API将策略应用于PDF文档”
* “快速入门(SwaRef):使用Web服务API将策略应用于PDF文档”

## 从PDF文档删除策略 {#removing-policies-from-pdf-documents}

您可以从受策略保护的文档中删除策略，以便从文档中删除安全性。 即，如果您不再希望文档受策略保护。 如果要使用较新的策略更新受策略保护的文档，则切换策略比删除策略和添加更新的策略更有效。

>[!NOTE]
>
>有关Document security服务的详细信息，请参阅AEM [表单的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-4}

要从受策略保护的PDF文档中删除策略，请执行以下步骤：

1. 包括项目文件
1. 创建Document Security Client API对象。
1. 检索受策略保护的PDF文档。
1. 从PDF文档中删除策略。
1. 保存不安全的PDF文档。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建Document Security Client API对象**

在以编程方式执行Document security服务操作之前，请先创建Document security服务客户端对象。

**检索受策略保护的PDF文档**

您可以检索受策略保护的PDF文档以删除策略。 如果尝试从未受策略保护的PDF文档中删除策略，将导致异常。

**从PDF文档中删除策略**

您可以从受策略保护的PDF文档中删除策略，前提是在连接设置中指定了管理员。 否则，用于保护文档的策略必须包含权限， `SWITCH_POLICY` 才能从PDF文档中删除策略。 此外，在AEM Forms连接设置中指定的用户也必须具有该权限。 否则，将引发异常。

**保存不安全的PDF文档**

在Document security服务从PDF文档删除策略后，您可以将不安全的PDF文档另存为PDF文件。

**另请参阅**

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[将策略应用于PDF文档](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### 使用Java API从PDF文档中删除策略 {#remove-a-policy-from-a-pdf-document-using-the-java-api}

使用Document Security API(Java)从受策略保护的PDF文档中删除策略：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-rightsmanagement-client.jar。

1. 创建Document Security Client API对象。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `DocumentSecurityClient` 象的构造函数并传递该对象来创建 `ServiceClientFactory` 对象。

1. 检索受策略保护的PDF文档。

   * 使用 `java.io.FileInputStream` 其构造函数并传递一个指定PDF文档位置的字符串值，创建一个表示受策略保护的PDF文档的对象。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对象来创建 `java.io.FileInputStream` 对象。

1. 从PDF文档中删除策略。

   * 通过 `DocumentManager` 调用对象的方 `DocumentSecurityClient` 法创建对 `getDocumentManager` 象。
   * 通过调用对象的方法并传递包含受策 `DocumentManager` 略保护的PDF文 `removeSecurity` 档的对 `com.adobe.idp.Document` 象，从PDF文档中删除策略。 此方法返回一个 `com.adobe.idp.Document` 包含不安全PDF文档的对象。

1. 保存不安全的PDF文档。

   * 创建一 `java.io.File` 个对象，并确保文件扩展名为PDF。
   * 调用对 `Document` 象的方 `copyToFile` 法，将对象的内容复制到文件中(确保使用由 `Document` 该方法返回的对 `Document``removeSecurity` 象)。

**代码示例**

有关使用Document security服务的代码示例，请参阅以下快速入门：

* “快速入门（SOAP模式）:使用Java API从PDF文档删除策略”

### 使用Web服务API删除策略 {#remove-a-policy-using-the-web-service-api}

使用Document Security API（Web服务）从受策略保护的PDF文档中删除策略：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建Document Security Client API对象。

   * 使用对 `DocumentSecurityServiceClient` 象的默认构造函数创建对象。
   * 使用构 `DocumentSecurityServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`.)您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。)
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `DocumentSecurityServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。


1. 检索受策略保护的PDF文档。

   * 使用对 `BLOB` 象的构造函数创建对象。 该 `BLOB` 对象用于存储从中删除策略的受策略保护的PDF文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 为对象的字段指定 `MTOM` 字节数组的内容来填充该对象。

1. 从PDF文档中删除策略。

   通过调用对象的方法并传递包含受策 `DocumentSecurityServiceClient` 略保护的PDF文 `removePolicySecurity` 档的对 `BLOB` 象，从PDF文档中删除策略。 此方法返回一个 `BLOB` 包含不安全PDF文档的对象。

1. 保存不安全的PDF文档。

   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建一个对象，该字符串值表示不安全PDF文档的文件位置。
   * 创建一个字节数组，它存储由方法返 `BLOB` 回的对象的数据内 `removePolicySecurity` 容。 通过获取对象字段的值来填 `BLOB` 充字节数 `MTOM` 组。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。

**代码示例**

有关使用Document security服务的代码示例，请参阅以下快速入门：

* “快速入门(MTOM):使用Web服务API从PDF文档删除策略”
* “快速入门(SwaRef):使用Web服务API从PDF文档删除策略”

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 撤销对文档的访问权 {#revoking-access-to-documents}

您可以撤销对受策略保护的PDF文档的访问权，导致用户无法访问该文档的所有副本。 当用户尝试打开已吊销的PDF文档时，会将其重定向到可查看已修订文档的指定URL。 必须以编程方式指定用户被重定向到的URL。 当您撤销对文档的访问权时，更改将在用户下次通过联机打开受策略保护的文档与Document security服务同步时生效。

撤销对文档的访问权能提供了额外的安全性。 例如，假定文档有较新版本可用，并且您不再希望任何人查看过时的版本。 在这种情况下，可撤销对旧文档的访问权，除非恢复访问权，否则任何人都无法查看该文档。

>[!NOTE]
>
>有关Document security服务的详细信息，请参阅AEM [表单的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-5}

要撤销受策略保护的文档，请执行以下步骤：

1. 包括项目文件。
1. 创建Document Security Client API对象。
1. 检索受策略保护的PDF文档。
1. 撤销受策略保护的文档。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建Document Security Client API对象**

在以编程方式执行Document security服务操作之前，必须创建Document security服务客户端对象。

**检索受策略保护的PDF文档**

您必须检索受策略保护的PDF文档才能撤销它。 您不能撤销已撤销或不是受策略保护的文档。

如果您知道受策略保护的文档的许可证标识符值，则无需检索受策略保护的PDF文档。 但是，在大多数情况下，您需要检索PDF文档才能获得许可证标识符值。

**撤销受策略保护的文档**

要撤销受策略保护的文档，请指定受策略保护的文档的许可证标识符。 此外，您还可以指定用户在尝试打开已吊销的文档时可以查看的文档的URL。 即，假定已吊销过时的文档。 当用户尝试打开已吊销的文档时，他们将看到一个已更新的文档而不是已吊销的文档。

>[!NOTE]
>
>如果尝试撤销已撤销的文档，则会引发异常。

**另请参阅**

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[将策略应用于PDF文档](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[恢复对已吊销文档的访问权限](protecting-documents-policies.md#reinstating-access-to-revoked-documents)

### 使用Java API撤销对文档的访问权 {#revoke-access-to-documents-using-the-java-api}

使用Document Security API(Java)撤销对受策略保护的PDF文档的访问权：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-rightsmanagement-client.jar。

1. 创建Document Security Client API对象

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `DocumentSecurityClient` 象的构造函数并传递该对象来创建 `ServiceClientFactory` 对象。

1. 检索受策略保护的PDF文档

   * 使用 `java.io.FileInputStream` 其构造函数并传递一个指定PDF文档位置的字符串值，创建一个表示受策略保护的PDF文档的对象。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对象来创建 `java.io.FileInputStream` 对象。

1. 撤销受策略保护的文档

   * 通过 `DocumentManager` 调用对象的方 `DocumentSecurityClient` 法创建对 `getDocumentManager` 象。
   * 通过调用对象的方法检索受策略保护的文档的 `DocumentManager` 许可证标识符 `getLicenseId` 值。 传递表 `com.adobe.idp.Document` 示受策略保护的文档的对象。 此方法返回表示许可证标识符值的字符串值。
   * 通过 `LicenseManager` 调用对象的方 `DocumentSecurityClient` 法创建对 `getLicenseManager` 象。
   * 通过调用对象的方法并传递以 `LicenseManager` 下值来撤 `revokeLicense` 销受策略保护的文档：

      * 一个字符串值，它指定受策略保护的文档的许可证标识符值(指定对象方 `DocumentManager` 法的返回 `getLicenseId` 值)。
      * 接口的静态数据成 `License` 员，它指定撤销文档的原因。 例如，您可以指定 `License.DOCUMENT_REVISED`。
      * 一个 `java.net.URL` 值，它指定修订文档所在的位置。 如果您不想将用户重定向到其他URL，则可以传递 `null`。

**代码示例**

有关使用Document security服务的代码示例，请参阅以下快速入门：

* “快速入门（SOAP模式）:使用Java API撤销文档”

### 使用Web服务API撤销对文档的访问权 {#revoke-access-to-documents-using-the-web-service-api}

使用Document Security API（Web服务）撤销对受策略保护的PDF文档的访问权：

1. 包括项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建Document Security Client API对象

   * 使用对 `DocumentSecurityServiceClient` 象的默认构造函数创建对象。
   * 使用构 `DocumentSecurityServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`.)您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。)
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `DocumentSecurityServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。


1. 检索受策略保护的PDF文档

   * 使用对 `BLOB` 象的构造函数创建对象。 该对 `BLOB` 象用于存储被撤销的受策略保护的PDF文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示要撤销受策略保护的PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 为对象的字段指定 `MTOM` 字节数组的内容来填充该对象。

1. 撤销受策略保护的文档

   * 通过调用对象的方法并传递表示受策略保护的文档的 `DocumentSecurityServiceClient` 对象，检索受策 `getLicenseID` 略保护的 `BLOB` 文档的许可证标识符值。 此方法返回表示许可证标识符的字符串值。
   * 通过调用对象的方法并传递以 `DocumentSecurityServiceClient` 下值来撤 `revokeLicense` 销受策略保护的文档：

      * 一个字符串值，它指定受策略保护的文档的许可证标识符值(指定对象方 `DocumentSecurityServiceService` 法的返回 `getLicenseId` 值)。
      * 枚举的静态数据成 `Reason` 员，它指定撤销文档的原因。 例如，您可以指定 `Reason.DOCUMENT_REVISED`。
      * 一个 `string` 值，它指定修订文档所在的URL位置。 如果您不想将用户重定向到其他URL，则可以传递 `null`。

**代码示例**

有关使用Document security服务的代码示例，请参阅以下快速入门：

* “快速入门(MTOM):使用Web服务API撤销文档”
* “快速入门(SwaRef):使用Web服务API撤销文档”

**另请参阅**

[从Word文档删除策略](protecting-documents-policies.md#removing-policies-from-word-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 恢复对已吊销文档的访问权限 {#reinstating-access-to-revoked-documents}

您可以恢复对已吊销的PDF文档的访问权，使用户可以访问已吊销文档的所有副本。 当用户打开已撤销的恢复文档时，用户可以查看该文档。

>[!NOTE]
>
>有关Document security服务的详细信息，请参阅AEM [表单的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-6}

要恢复对已吊销的PDF文档的访问权，请执行以下步骤：

1. 包括项目文件。
1. 创建Document Security Client API对象。
1. 检索已吊销的PDF文档的许可证标识符。
1. 恢复对已吊销的PDF文档的访问权限。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建Document Security Client API对象**

在以编程方式执行Document security服务操作之前，必须创建Document security服务客户端对象。 如果您使用Java API，请创建一个对 `DocumentSecurityClient` 象。 如果您使用的是Document Security web服务API，请创建一个对 `DocumentSecurityServiceService` 象。

**检索已吊销的PDF文档的许可证标识符**

您必须检索已吊销的PDF文档的许可证标识符才能恢复已吊销的PDF文档。 获得许可证标识符值后，可恢复已吊销的文档。 如果尝试恢复未撤销的文档，将导致异常。

**恢复对已吊销的PDF文档的访问权限**

要恢复对已吊销的PDF文档的访问权，必须指定已吊销文档的许可证标识符。 如果尝试恢复未撤销的PDF文档访问权，将导致异常。

**另请参阅**

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[将策略应用于PDF文档](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[撤销对文档的访问权](protecting-documents-policies.md#revoking-access-to-documents)

### 使用Java API恢复对已吊销文档的访问 {#reinstate-access-to-revoked-documents-using-the-java-api}

使用Document Security API(Java)恢复对已吊销文档的访问：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-rightsmanagement-client.jar。

1. 创建Document Security Client API对象。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `DocumentSecurityClient` 象的构造函数并传递该对象来创建 `ServiceClientFactory` 对象。

1. 检索已吊销的PDF文档的许可证标识符。

   * 使用 `java.io.FileInputStream` 其构造函数并传递一个指定PDF文档位置的字符串值，创建一个表示已吊销的PDF文档的对象。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对象来创建 `java.io.FileInputStream` 对象。
   * 通过 `DocumentManager` 调用对象的方 `DocumentSecurityClient` 法创建对 `getDocumentManager` 象。
   * 通过调用对象的方法并传递表示已撤销文档的对 `DocumentManager` 象，检索已撤 `getLicenseId` 销文档的 `com.adobe.idp.Document` 许可证标识符值。 此方法返回表示许可证标识符的字符串值。

1. 恢复对已吊销的PDF文档的访问权限。

   * 通过 `LicenseManager` 调用对象的方 `DocumentSecurityClient` 法创建对 `getLicenseManager` 象。
   * 通过调用对象的方法并传递已吊销文档的许 `LicenseManager` 可证标识符值， `unrevokeLicense` 恢复对已吊销PDF文档的访问。

**代码示例**

有关使用Document security服务的代码示例，请参阅以下快速入门：

* “快速入门（SOAP模式）:使用Web服务API恢复对已吊销文档的访问”

### 使用Web服务API恢复对已吊销文档的访问 {#reinstate-access-to-revoked-documents-using-the-web-service-api}

使用Document Security API（Web服务）恢复对已吊销文档的访问：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建Document Security Client API对象。

   * 使用对 `DocumentSecurityServiceClient` 象的默认构造函数创建对象。
   * 使用构 `DocumentSecurityServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`.)您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。)
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `DocumentSecurityServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。


1. 检索已吊销的PDF文档的许可证标识符。

   * 使用对 `BLOB` 象的构造函数创建对象。 该对 `BLOB` 象用于存储恢复访问权限的已撤销PDF文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示已吊销的PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 为对象的字段指定 `MTOM` 字节数组的内容来填充该对象。

1. 恢复对已吊销的PDF文档的访问权限。

   * 通过调用对象的方法并传递表示已撤销文档的对 `DocumentSecurityServiceClient` 象，检索已撤 `getLicenseID` 销文档的 `BLOB` 许可证标识符值。 此方法返回表示许可证标识符的字符串值。
   * 通过调用对象的方法并传递一个指定已撤销PDF文档的许可证标识符值的字符串值（传递对象方法的返回值），恢复对已撤 `DocumentSecurityServiceClient` 销PDF文档的访 `unrevokeLicense``DocumentSecurityServiceClient``getLicenseId` 问。

**代码示例**

有关使用Document security服务的代码示例，请参阅以下快速入门：

* “快速入门(MTOM):使用Web服务API恢复对已吊销文档的访问”
* “快速入门(SwaRef):使用Web服务API恢复对已吊销文档的访问”

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 检查受策略保护的PDF文档 {#inspecting-policy-protected-pdf-documents}

您可以使用Document Security Service API（Java和Web服务）检查受策略保护的PDF文档。 检查受策略保护的PDF文档会返回有关受策略保护的PDF文档的信息。 例如，您可以确定用于保护文档的策略以及保护文档的日期。

如果您的LiveCycle版本是8.x或更早版本，则无法执行此任务。 在AEM Forms中增加了对检查受策略保护的文档的支持。 如果尝试使用LiveCycle 8.x（或更早版本）检查受策略保护的文档，则会引发异常。

>[!NOTE]
>
>有关Document security服务的详细信息，请参阅AEM [表单的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-7}

要检查受策略保护的PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建Document Security Client API对象。
1. 检索受策略保护的文档以进行检查。
1. 获取有关受策略保护的文档的信息。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建Document Security Client API对象**

在以编程方式执行Document security服务操作之前，请先创建Document security服务客户端对象。 如果您使用Java API，请创建一个对 `RightsManagementClient` 象。 如果您使用的是Document Security web服务API，请创建一个对 `RightsManagementServiceService` 象。

**检索受策略保护的文档以进行检查**

要检查受策略保护的文档，请检索它。 如果尝试检查未通过策略保护或被撤销的文档，则会引发异常。

**检查文档**

检索受策略保护的文档后，可以检查它。

**获取有关受策略保护的文档的信息**

在检查受策略保护的PDF文档后，可以获取有关该文档的信息。 例如，您可以确定用于保护文档的策略。

如果使用属于“我的策略”的策略保护文档，然后调用或， `RMInspectResult.getPolicysetName` 则 `RMInspectResult.getPolicysetId`返回null。

如果文档使用包含在策略集（“我的策略”除外）中的策略进行保护，则返回 `RMInspectResult.getPolicysetName` 有效 `RMInspectResult.getPolicysetId` 的字符串。

**另请参阅**

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API检查受策略保护的PDF文档 {#inspect-policy-protected-pdf-documents-using-the-java-api}

使用Document Security Service API(Java)检查受策略保护的PDF文档：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-rightsmanagement-client.jar。 有关这些文件的位置的信息，请参 [阅包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

1. 创建Document Security Client API对象。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。 (请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。)
   * 使用对 `RightsManagementClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 检索受策略保护的文档以进行检查。

   * 使用 `java.io.FileInputStream` 其构造函数创建一个表示受策略保护的PDF文档的对象。 传递指定PDF文档位置的字符串值。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对 `java.io.FileInputStream` 象。

1. 检查文档。

   * 通过 `DocumentManager` 调用对象的方 `RightsManagementClient` 法创建对 `getDocumentManager` 象。
   * 通过调用对象的方法检查受策 `LicenseManager` 略保护的文 `inspectDocument` 档。 传递包 `com.adobe.idp.Document` 含受策略保护的PDF文档的对象。 此方法返回一个 `RMInspectResult` 对象，其中包含有关受策略保护的文档的信息。

1. 获取有关受策略保护的文档的信息。

   要获取有关受策略保护的文档的信息，请调用属于对象的相应 `RMInspectResult` 方法。 例如，要检索策略名称，请调用对 `RMInspectResult` 象的方 `getPolicyName` 法。

**代码示例**

有关使用Document security服务的代码示例，请参阅以下快速入门：

* “快速入门（SOAP模式）:使用Java API检查受策略保护的PDF文档”

### 使用Web服务API检查受策略保护的PDF文档 {#inspect-policy-protected-pdf-documents-using-the-web-service-api}

使用Document Security Service API（Web服务）检查受策略保护的PDF文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建Document Security Client API对象。

   * 使用对 `RightsManagementServiceClient` 象的默认构造函数创建对象。
   * 使用构 `RightsManagementServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`.)您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。)
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `RightsManagementServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。


1. 检索受策略保护的文档以进行检查。

   * 使用对 `BLOB` 象的构造函数创建对象。 该 `BLOB` 对象用于存储要检查的PDF文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数创建对象。 传递一个字符串值，它表示PDF文档的文件位置以及在中打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法，用流数据 `System.IO.FileStream` 填充字节数 `Read` 组。 传递字节数组、开始位置和流长度以读取。
   * 通过 `BLOB` 为对象的字段指定 `MTOM` 字节数组的内容来填充该对象。

1. 检查文档。

   通过调用对象的方法检查受策 `RightsManagementServiceClient` 略保护的文 `inspectDocument` 档。 传递包 `BLOB` 含受策略保护的PDF文档的对象。 此方法返回一个 `RMInspectResult` 对象，其中包含有关受策略保护的文档的信息。

1. 获取有关受策略保护的文档的信息。

   要获取有关受策略保护的文档的信息，请获取属于该对象的相应字段的 `RMInspectResult` 值。 例如，要检索策略名称，请获取对象字 `RMInspectResult` 段的 `policyName` 值。

**代码示例**

有关使用Document security服务的代码示例，请参阅以下快速入门：

* “快速入门(MTOM):使用Web服务API检查受策略保护的PDF文档”
* “快速入门(SwaRef):使用Web服务API检查受策略保护的PDF文档”

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 创建水印 {#creating-watermarks}

水印通过唯一识别文档并控制版权侵权来帮助确保文档的安全。 例如，您可以创建水印并将其放置在文档的所有页面上，该水印将声明为机密。 在创建水印后，您可以将其作为策略的一部分包含在其中。 即，您可以使用新创建的水印设置策略的水印属性。 在将包含水印的策略应用到文档后，该水印会显示在受策略保护的文档中。

>[!NOTE]
>
>只有具有Document security管理权限的用户才能创建水印。 即，在定义创建Document security服务客户端对象所需的连接设置时，必须指定此类用户。

>[!NOTE]
>
>有关Document security服务的详细信息，请参阅AEM [表单的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-8}

要创建水印，请执行以下步骤：

1. 包括项目文件。
1. 创建Document Security Client API对象。
1. 设置水印属性。
1. 向Document security服务注册水印。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建Document Security Client API对象**

在以编程方式执行Document security服务操作之前，必须创建Document security服务客户端对象。 如果您使用Java API，请创建一个对 `RightsManagementClient` 象。 如果您使用的是Document Security web服务API，请创建一个对 `RightsManagementServiceService` 象。

**设置水印属性**

要创建新水印，必须设置水印属性。 必须始终定义name属性。 除了name属性外，您还必须至少设置下列属性之一：

* 自定义文本
* 包含日期
* UserIdIncluded
* 包含的用户名

下表列出了使用Web服务创建水印时所需的键和值对。

<table>
 <thead>
  <tr>
   <th><p>键名</p></th>
   <th><p>描述</p></th>
   <th><p>值</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERNAME_ENABLED</code></p></td>
   <td><p>指定打开文档的用户的用户名是否属于水印的一部分。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERID_ENABLED</code></p></td>
   <td><p>指定打开文档的用户的标识是否属于水印的一部分。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CURRENTDATE_ENABLED</code></p></td>
   <td><p>指定当前日期是否是水印的一部分。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code></p></td>
   <td><p>如果此值为true，则必须使用指定自定义文本的值 <code>WaterBackCmd:SRCTEXT</code>。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:OPACITY</code></p></td>
   <td><p>指定水印的不透明度。 如果未指定默认值，则默认值为0.5。</p></td>
   <td><p>介于0.0和1.0之间的值。</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:ROTATION</code></p></td>
   <td><p>指定水印的旋转。 默认值为0度。</p></td>
   <td><p>介于0和359之间的值。</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SCALE</code></p></td>
   <td><p>如果指定了此值，则 <code>WaterBackCmd:IS_SIZE_ENABLED</code> 必须存在，且该值必须为true。 如果未指定此属性，则默认行为适合页面大小。</p></td>
   <td><p>大于0.0且小于或等于1.0的值。</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:HORIZ_ALIGN</code></p></td>
   <td><p>指定水印的水平对齐方式。 默认值为center。</p></td>
   <td><p>left、center或right</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:VERT_ALIGN</code></p></td>
   <td><p>指定水印的垂直对齐方式。 默认值为center。</p></td>
   <td><p>顶部、中心或底部</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USE_BACKGROUND</code></p></td>
   <td><p>指定水印是否为背景。 默认值为false。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_SIZE_ENABLED</code></p></td>
   <td><p>如果指定了自定义比例，则返回true。 如果此值为true，则还必须指定SCALE。 如果此值为false，则默认值将适合页面大小。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SRCTEXT</code></p></td>
   <td><p>指定水印的自定义文本。 如果此值存在，则 <code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code> 也必须存在并设置为true。</p></td>
   <td><p>True或False</p></td>
  </tr>
 </tbody>
</table>

所有水印都必须定义以下属性之一：

* `WaterBackCmd:IS_USERNAME_ENABLED`
* `WaterBackCmd:IS_USERID_ENABLED`
* `WaterBackCmd:IS_CURRENTDATE_ENABLED`
* `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`

所有其他属性都是可选的。

**注册水印**

必须先向Document security服务注册新水印，然后才能使用。 在注册水印后，您可以在策略中使用它。

**另请参阅**

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[将策略应用于PDF文档](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### 使用Java API创建水印 {#create-watermarks-using-the-java-api}

使用Document Security API(Java)创建水印：

1. 包括项目文件。

   在Java项目的类路径中 `adobe-rightsmanagement-client.jar`包含客户端JAR文件，如。

1. 创建Document Security Client API对象。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `RightsManagementClient` 象的构造函数并传递该对象来创建 `ServiceClientFactory` 对象。

1. 设置水印属性

   * 通过 `Watermark` 调用对象的静态 `InfomodelObjectFactory` 方法创建对 `createWatermark` 象。 此方法返回一个 `Watermark` 对象。
   * 通过调用对象的方法并传递指定策 `Watermark` 略名称的 `setName` 字符串值来设置水印的name属性。
   * 通过调用对象的方法并传递来设置 `Watermark` 水印的背 `setBackground` 景属性 `true`。 通过设置此属性，水印将显示在文档的背景中。
   * 通过调用对象的方法并传递一个表示水印文 `Watermark` 本的字 `setCustomText` 符串值来设置水印的自定义文本属性。
   * 通过调用对象的方法并传递指定不透 `Watermark` 明度级别的 `setOpacity` 整数值来设置水印的不透明度属性。 值100表示水印完全不透明，值0表示水印完全透明。

1. 注册水印。

   * 通过 `WatermarkManager` 调用对象的方 `RightsManagementClient` 法创建对 `getWatermarkManager` 象。 此方法返回一个 `WatermarkManager` 对象。
   * 通过调用对象的方 `WatermarkManager` 法并传递表示水 `registerWatermark` 印的对象来 `Watermark` 注册水印。 此方法返回一个表示水印标识值的字符串值。

**代码示例**

有关使用Document security服务的代码示例，请参阅以下快速入门：

* “快速入门（SOAP模式）:使用Java API创建水印”

### 使用Web服务API创建水印 {#create-watermarks-using-the-web-service-api}

使用Document Security API（Web服务）创建水印：

1. 创建Document Security Client API对象。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建Document Security Client API对象。

   * 使用对 `RightsManagementServiceClient` 象的默认构造函数创建对象。
   * 使用构 `RightsManagementServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`.)您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。)
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `RightsManagementServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。


1. 设置水印属性。

   * 通过调 `WatermarkSpec` 用构造函数创建对 `WatermarkSpec` 象。
   * 通过为对象的数据成员分配字符串值来设 `WatermarkSpec` 置水印的 `name` 名称。
   * 通过为对象的数 `id` 据成员分配字符串值来设置 `WatermarkSpec` 水印的 `id` 属性。
   * 对于要设置的每个水印属性，创建一个单独的 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象。
   * 通过为对象的数据成员分配 `MyMapOf_xsd_string_To_xsd_anyType_Item` 一个值来 `key` 设置键值(例如， `WaterBackCmd:OPACITY)`。
   * 通过为对象的数据成员 `MyMapOf_xsd_string_To_xsd_anyType_Item` 分配值 `value` 来设置值(例如 `.25`)。
   * 创建对 `MyArrayOf_xsd_anyType` 象。 对于每 `MyMapOf_xsd_string_To_xsd_anyType_Item` 个对象，调用 `MyArrayOf_xsd_anyType` 对象的方 `Add` 法。 传递对 `MyMapOf_xsd_string_To_xsd_anyType_Item` 象。
   * 将对 `MyArrayOf_xsd_anyType` 象指定给对 `WatermarkSpec` 象的数据 `values` 成员。

1. 注册水印。

   通过调用对象的方 `RightsManagementServiceClient` 法并传递表示水 `registerWatermark` 印的对象来 `WatermarkSpec` 注册水印。

**代码示例**

有关使用Document security服务的代码示例，请参阅以下快速入门：

* “快速入门(MTOM):使用Web服务API创建水印»
* “快速入门(SwaRef):使用Web服务API创建水印»

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 修改水印 {#modifying-watermarks}

您可以使用Document Security Java API或Web服务API修改现有水印。 要更改现有水印，请检索它，修改它的属性，然后在服务器上更新它。 例如，假定您检索水印并修改其不透明度属性。 在更改生效之前，您必须更新水印。

当您修改水印时，所做的更改会影响应用了水印的未来文档。 即，包含水印的现有PDF文档不受影响。

>[!NOTE]
>
>只有具有Document Security管理权限的用户才能修改水印。 即，在定义创建Document security服务客户端对象所需的连接设置时，必须指定此类用户。

>[!NOTE]
>
>有关Document security服务的详细信息，请参阅AEM [表单的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-9}

要修改水印，请执行以下步骤：

1. 包括项目文件。
1. 创建Document Security Client API对象。
1. 检索要修改的水印。
1. 设置水印属性。
1. 更新水印。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建Document Security Client API对象**

在以编程方式执行Document security服务操作之前，必须创建Document security服务客户端对象。 如果您使用Java API，请创建一个对 `DocumentSecurityClient` 象。 如果您使用的是Document Security web服务API，请创建一个对 `DocumentSecurityServiceService` 象。

**检索要修改的水印**

要修改水印，必须检索现有水印。 您可以通过指定水印的名称或通过指定水印的标识符值来检索水印。

**设置水印属性**

要修改现有水印，请更改一个或多个水印属性的值。 使用Web服务以编程方式更新水印时，必须设置最初设置的所有属性，即使该值没有更改也是如此。 例如，假定设置了以下水印属性： `WaterBackCmd:IS_USERID_ENABLED`、 `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`、 `WaterBackCmd:OPACITY`和 `WaterBackCmd:SRCTEXT`。 尽管您唯一要修改的属性是 `WaterBackCmd:OPACITY`，但您必须设置其他值。

>[!NOTE]
>
>使用Java API修改水印时，无需指定所有属性。 设置要修改的水印属性。

>[!NOTE]
>
>有关水印属性名称的信息，请参阅创 [建水印](protecting-documents-policies.md#creating-watermarks)。

**更新水印**

修改水印的属性后，必须更新水印。

**另请参阅**

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[创建水印](protecting-documents-policies.md#creating-watermarks)

### 使用Java API修改水印 {#modify-watermarks-using-the-java-api}

使用Document Security API(Java)修改水印：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-rightsmanagement-client.jar。

1. 创建Document Security Client API对象。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `DocumentSecurityClient` 象的构造函数并传递该对象来创建 `ServiceClientFactory` 对象。

1. 检索要修改的水印。

   通过调 `WatermarkManager` 用对象的方 `DocumentSecurityClient` 法创建对象，并传 `getWatermarkManager` 递指定水印名称的字符串值。 此方法返回一 `Watermark` 个表示要修改的水印的对象。

1. 设置水印属性。

   通过调用对象的方法并传递指定不透 `Watermark` 明度级别的 `setOpacity` 整数值来设置水印的不透明度属性。 值100表示水印完全不透明，值0表示水印完全透明。

   >[!NOTE]
   >
   >此示例仅修改不透明度属性。

1. 更新水印。

   * 通过调用对象的方 `WatermarkManager` 法更新水 `updateWatermark` 印，并传递其属 `Watermark` 性被修改的对象。

**代码示例**

有关使用Document security服务的代码示例，请参阅快速入门（SOAP模式）:使用Java API部分修改水印。

### 使用Web服务API修改水印 {#modify-watermarks-using-the-web-service-api}

使用Document Security API（Web服务）修改水印：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建Document Security Client API对象。

   * 使用对 `DocumentSecurityServiceClient` 象的默认构造函数创建对象。
   * 使用构 `RightsManagementServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`.)您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。)
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `DocumentSecurityServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。


1. 检索要修改的水印。

   通过调用对象的方法检索要修 `DocumentSecurityServiceClient` 改的水 `getWatermarkByName` 印。 传递指定水印名称的字符串值。 此方法返回一 `WatermarkSpec` 个表示要修改的水印的对象。

1. 设置水印属性。

   * 对于要更新的每个水印属性，创建一个单独的 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象。
   * 通过为对象的数据成员分配 `MyMapOf_xsd_string_To_xsd_anyType_Item` 一个值来 `key` 设置键值(例如， `WaterBackCmd:OPACITY)`。
   * 通过为对象的数据成员 `MyMapOf_xsd_string_To_xsd_anyType_Item` 分配值 `value` 来设置值(例如 `.50`)。
   * 创建对 `MyArrayOf_xsd_anyType` 象。 对于每 `MyMapOf_xsd_string_To_xsd_anyType_Item` 个对象，调用 `MyArrayOf_xsd_anyType` 对象的方 `Add` 法。 传递对 `MyMapOf_xsd_string_To_xsd_anyType_Item` 象。
   * 将对 `MyArrayOf_xsd_anyType` 象指定给对 `WatermarkSpec` 象的数据 `values` 成员。

1. 更新水印。

   通过调用对象的方 `DocumentSecurityServiceClient` 法并传递表示要修 `updateWatermark` 改的水 `WatermarkSpec` 印的对象来更新水印。

**代码示例**

有关使用Document security服务的代码示例，请参阅以下快速入门：

* “快速入门(MTOM):使用Web服务API修改水印»

## 搜索事件 {#searching-for-events}

Rights Management服务会在特定操作发生时跟踪这些操作，例如对文档应用策略、打开受策略保护的文档以及撤销对文档的访问权。 必须为Rights Management服务启用事件审核，否则不跟踪事件。

事件分为以下类别之一：

* 管理员事件是与管理员相关的操作，如创建新的管理员帐户。
* 文档事件是与文档相关的操作，如关闭受策略保护的文档。
* 策略事件是与策略相关的操作，如创建新策略。
* 服务事件是与Rights Management服务相关的操作，如与用户目录同步。

您可以使用Rights Management Java API或Web服务API搜索指定事件。 通过搜索事件，您可以执行任务，如创建特定事件的日志文件。

>[!NOTE]
>
>有关Rights Management服务的详细信息，请参阅AEM [表单的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-10}

要搜索Rights Management事件，请执行以下步骤：

1. 包括项目文件。
1. 创建Rights Management客户端API对象。
1. 指定要搜索的事件。
1. 搜索活动。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建Rights Management客户端API对象**

在以编程方式执行Rights Management服务操作之前，必须创建Rights Management服务客户端对象。 如果您使用Java API，请创建一个对 `DocumentSecurityClient` 象。 如果您使用Rights Management web服务API，请创建一个对 `DocumentSecurityServiceService` 象。

**指定要搜索的活动**

必须指定要搜索的活动。 例如，您可以搜索策略创建事件，该事件在创建新策略时发生。

**搜索活动**

在指定要搜索的活动后，可以使用Rights Management Java API或Rights Management web服务API搜索该活动。

**另请参阅**

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API搜索事件 {#search-for-events-using-the-java-api}

使用Rights Management API(Java)搜索事件：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-rightsmanagement-client.jar。

1. 创建Rights Management客户端API对象

   使用对 `DocumentSecurityClient` 象的构造函数并传递一个包含连接属 `ServiceClientFactory` 性的对象来创建对象。

1. 指定要搜索的活动

   * 通过 `EventManager` 调用对象的方 `DocumentSecurityClient` 法创建对 `getEventManager` 象。 此方法返回一个 `EventManager` 对象。
   * 通过调用 `EventSearchFilter` 对象的构造函数创建对象。
   * 通过调用对象的方法并传递属于类的静态数据成员（表示要为其搜索的事件），指 `EventSearchFilter``setEventCode``EventManager` 定要为其搜索的事件。 例如，要搜索策略create事件，请传递 `EventManager.POLICY_CREATE_EVENT`。
   >[!NOTE]
   >
   >您可以通过调用对象方法来定义其他 `EventSearchFilter` 搜索条件。 例如，调用该方 `setUserName` 法以指定与该事件关联的用户。

1. 搜索活动

   通过调用对象的方法并传 `EventManager` 递定义事件搜 `searchForEvents` 索条件的 `EventSearchFilter` 对象来搜索事件。 此方法返回一组对 `Event` 象。

**代码示例**

有关使用Rights Management服务的代码示例，请参阅以下快速入门：

* “快速入门(SOAP):使用Java API搜索事件”

### 使用Web服务API搜索事件 {#search-for-events-using-the-web-service-api}

使用Rights Management API（Web服务）搜索事件：

1. 包括项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建Rights Management客户端API对象

   * 使用对 `DocumentSecurityServiceClient` 象的默认构造函数创建对象。
   * 使用构 `DocumentSecurityServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`.)您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。)
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `DocumentSecurityServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。


1. 指定要搜索的活动

   * 使用对 `EventSpec` 象的构造函数创建对象。
   * 通过将对象的数据成员设置为实例，以指 `EventSpec` 定事件发生的时间段的开始 `firstTime.date` ，该 `DataTime` 实例表示事件发生时的日期范围的开始。
   * 将值指 `true` 定给对 `EventSpec` 象的数据 `firstTime.dateSpecified` 成员。
   * 通过将对象的数据成员与实例一起设置，以指 `EventSpec` 定发生事件的时 `lastTime.date` 间 `DataTime` 段的结束时间，该实例表示发生事件的日期范围的结束时间。
   * 将值指 `true` 定给对 `EventSpec` 象的数据 `lastTime.dateSpecified` 成员。
   * 通过为对象的数据成员分配字符串值来设置要 `EventSpec` 搜索的 `eventCode` 事件。 下表列出了可分配给此属性的数值：
   <table>
    <thead>
    <tr>
    <th><p>活动类型</p></th>
    <th><p>值</p></th>
    </tr>
    </thead>
    <tbody>
    <tr>
    <td><p><code>ALL_EVENTS</code></p></td>
    <td><p>999</p></td>
    </tr>
    <tr>
    <td><p><code>USER_CHANGE_PASSWORD_EVENT</code></p></td>
    <td><p>1000</p></td>
    </tr>
    <tr>
    <td><p><code>USER_REGISTER_EVENT</code></p></td>
    <td><p>1001</p></td>
    </tr>
    <tr>
    <td><p><code>USER_PREREGISTER_EVENT</code></p></td>
    <td><p>1002</p></td>
    </tr>
    <tr>
    <td><p><code>USER_ACTIVATE_EVENT</code></p></td>
    <td><p>1003</p></td>
    </tr>
    <tr>
    <td><p><code>USER_DEACTIVATE_EVENT</code></p></td>
    <td><p>1004</p></td>
    </tr>
    <tr>
    <td><p><code>USER_AUTHENTICATE_EVENT</code></p></td>
    <td><p>1005</p></td>
    </tr>
    <tr>
    <td><p><code>USER_AUTHENTICATE_DENY_EVENT </code></p></td>
    <td><p>1006</p></td>
    </tr>
    <tr>
    <td><p><code>USER_ACCOUNT_LOCK_EVENT</code></p></td>
    <td><p>1007</p></td>
    </tr>
    <tr>
    <td><p><code>USER_DELETE_EVENT </code></p></td>
    <td><p>1008</p></td>
    </tr>
    <tr>
    <td><p><code>USER_UPDATE_PROFILE_EVENT </code></p></td>
    <td><p>1009</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_VIEW_EVENT </code></p></td>
    <td><p>2000</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_PRINT_LOW_EVENT </code></p></td>
    <td><p>2001</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_PRINT_HIGH_EVENT </code></p></td>
    <td><p>2002</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SIGN_EVENT </code></p></td>
    <td><p>2003</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_ADD_ANNOTATION_EVENT </code></p></td>
    <td><p>2004</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_FORM_FILL_EVENT </code></p></td>
    <td><p>2005</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CLOSE_EVENT </code></p></td>
    <td><p>2006</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_MODIFY_EVENT </code></p></td>
    <td><p>2007</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CHANGE_SECURITY_HANDLER_EVENT </code></p></td>
    <td><p>2008</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SWITCH_POLICY_EVENT </code></p></td>
    <td><p>2009</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_REVOKE_EVENT </code></p></td>
    <td><p>2010</p></td>
    </tr>
    <tr>
    <td><p><code>$1</code></p></td>
    <td><p>2011</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SECURE_EVENT </code></p></td>
    <td><p>2012</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_UNKNOWN_CLIENT_EVENT </code></p></td>
    <td><p>2013</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CHANGE_REVOKE_URL_EVENT </code></p></td>
    <td><p>2014</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CHANGE_EVENT </code></p></td>
    <td><p>3000</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_ENABLE_EVENT </code></p></td>
    <td><p>3001</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_DISABLE_EVENT </code></p></td>
    <td><p>3002</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CREATE_EVENT </code></p></td>
    <td><p>3003</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_DELETE_EVENT </code></p></td>
    <td><p>3004</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CHANGE_OWNER_EVENT </code></p></td>
    <td><p>3005</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_CLIENT_SYNC_EVENT </code></p></td>
    <td><p>4000</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_SYNC_DIR_INFO_EVENT </code></p></td>
    <td><p>4001</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_SYNC_DIR_COMPLETE_EVENT </code></p></td>
    <td><p>4002</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_VERSION_MISMATCH_EVENT </code></p></td>
    <td><p>4003</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_CONFIG_CHANGE_EVENT </code></p></td>
    <td><p>4004</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_ENABLE_OFFLINE_ACCESS_EVENT </code></p></td>
    <td><p>4005</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_ADD_EVENT </code></p></td>
    <td><p>5000</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_DELETE_EVENT </code></p></td>
    <td><p>5001</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_EDIT_EVENT </code></p></td>
    <td><p>5002</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_ACTIVATE_EVENT </code></p></td>
    <td><p>5003</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_DEACTIVATE_EVENT </code></p></td>
    <td><p>5004</p></td>
    </tr>
    <tr>
    <td><p><code>ERROR_DIRECTORY_SERVICE_EVENT </code></p></td>
    <td><p>6000</p></td>
    </tr>
    <tr>
    <td><p><code>CREATED_POLICYSET_EVENT</code></p></td>
    <td><p>7000</p></td>
    </tr>
    <tr>
    <td><p><code>DELETED_POLICYSET_EVENT</code></p></td>
    <td><p>7001</p></td>
    </tr>
    <tr>
    <td><p><code>MODIFIED_POLICYSET_EVENT</code></p></td>
    <td><p>7002</p></td>
    </tr>
    </tbody>
    </table>

1. 搜索活动

   通过调用对象的方 `DocumentSecurityServiceClient` 法并传递表示要搜索 `searchForEvents``EventSpec` 的事件和最大结果数的对象来搜索事件。 此方法返回一个集 `MyArrayOf_xsd_anyType` 合，其中每个元素都是一个 `AuditSpec` 实例。 使用实 `AuditSpec` 例，您可以获取有关事件的信息，如事件发生的时间。 该实 `AuditSpec` 例包含一个指定 `timestamp` 此信息的数据成员。

**代码示例**

有关使用Rights Management服务的代码示例，请参阅以下快速入门：

* “快速入门(MTOM):使用Web服务API搜索事件”
* “快速入门(SwaRef):使用Web服务API搜索事件”

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 对Word文档应用策略 {#applying-policies-to-word-documents}

除PDF文档外，Rights Management服务还支持其他文档格式，如Microsoft Word文档（DOC文件）和其他Microsoft office文件格式。 例如，您可以将策略应用于Word文档以保护它。 通过将策略应用于Word文档，可限制对文档的访问。 如果文档已使用策略进行保护，则不能对文档应用策略。

在分发受策略保护的Word文档后，可以对其进行监视。 即，您可以查看文档的使用方式以及使用者。 例如，您可以了解某人何时打开了文档。

>[!NOTE]
>
>有关Document security服务的详细信息，请参阅AEM [表单的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-11}

要将策略应用于Word文档，请执行以下步骤：

1. 包括项目文件。
1. 创建Document Security Client API对象。
1. 检索应用了策略的Word文档。
1. 将现有策略应用于Word文档。
1. 保存受策略保护的Word文档。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建Document Security Client API对象**

在以编程方式执行Document security服务操作之前，必须创建Document security服务客户端对象。

**检索Word文档**

必须检索Word文档才能应用策略。 在将策略应用到Word文档后，用户在使用文档时会受到限制。 例如，如果策略未启用脱机时打开文档，则用户必须联机才能打开文档。

**将现有策略应用于Word文档**

要将策略应用于Word文档，必须引用现有策略并指定该策略所属的策略集。 设置连接属性的用户必须有权访问指定的策略。 否则，会出现异常。

**保存Word文档**

在Document security服务将策略应用于Word文档后，您可以将受策略保护的Word文档另存为DOC文件。

**另请参阅**

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[撤销对文档的访问权](protecting-documents-policies.md#revoking-access-to-documents)

### 使用Java API将策略应用于Word文档 {#apply-a-policy-to-a-word-document-using-the-java-api}

使用Document Security API(Java)将策略应用于Word文档：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-rightsmanagement-client.jar。

1. 创建Document Security Client API对象。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `DocumentSecurityClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 检索Word文档。

   * 使用 `java.io.FileInputStream` Word文档的构造函数并传递一个指定Word文档位置的字符串值，创建一个表示该文档的对象。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对 `java.io.FileInputStream` 象。

1. 将现有策略应用于Word文档。

   * 通过 `DocumentManager` 调用对象的方 `DocumentSecurityClient` 法创建对 `getDocumentManager` 象。
   * 通过调用对象的方法并传递以 `DocumentManager` 下值，将策 `protectDocument` 略应用于Word文档：

      * 包 `com.adobe.idp.Document` 含应用策略的Word文档的对象。
      * 指定文档名称的字符串值。
      * 一个字符串值，它指定策略所属的策略集的名称。 您可以指定 `null` 一个值，该值导致使 `MyPolicies` 用策略集。
      * 指定策略名称的字符串值。
      * 一个字符串值，它表示作为文档发布者的用户的用户管理器域的名称。 此参数值是可选的，可以为null（如果此参数为null，则下一个参数值必须是null）。
      * 一个字符串值，它表示作为文档发布者的用户管理器用户的规范名称。 此参数值是可选的，可 `null` 以是(如果此参数是 `null`，则上一个参数值必须是 `null`)。
      * 表示 `com.adobe.livecycle.rightsmanagement.Locale` 用于选择MS office模板的区域设置。 此参数值是可选的，您可以指定 `null`。
      该方 `protectDocument` 法返回一 `RMSecureDocumentResult` 个包含受策略保护的Word文档的对象。


1. 保存Word文档。

   * 调用对 `RMSecureDocumentResult` 象的方 `getProtectedDoc` 法以获取受策略保护的Word文档。 此方法返回一个 `com.adobe.idp.Document` 对象。
   * 创建一 `java.io.File` 个对象，并确保文件扩展名为DOC。
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法，将对象的内容复制到文件中(确保使用由 `Document` 该方法返回的对 `Document``getProtectedDoc` 象)。

**代码示例**

有关使用Document security服务的代码示例，请参阅以下快速入门：

* “快速入门（SOAP模式）:使用Java API将策略应用于Word文档”

### 使用Web服务API将策略应用于Word文档 {#apply-a-policy-to-a-word-document-using-the-web-service-api}

使用Document Security API（Web服务）将策略应用于Word文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/DocumentSecurityService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建Document Security Client API对象。

   * 使用对 `DocumentSecurityServiceClient` 象的默认构造函数创建对象。
   * 使用构 `DocumentSecurityServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`.)您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。)
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `DocumentSecurityServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。


1. 检索Word文档。

   * 使用对 `BLOB` 象的构造函数创建对象。 对 `BLOB` 象用于存储应用了策略的Word文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示Word文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 通过获取对象的属性确定字 `System.IO.FileStream` 节数组大 `Length` 小。
   * 通过调用对象的方法，用流数据 `System.IO.FileStream` 填充字节数 `Read` 组。 传递要读取的字节数组、开始位置和流长度。
   * 通过 `BLOB` 为对象的字段指定 `MTOM` 字节数组的内容来填充该对象。

1. 将现有策略应用于Word文档。

   通过调用对象的方法并传递以 `DocumentSecurityServiceClient` 下值，将策 `protectDocument` 略应用于Word文档：

   * 包 `BLOB` 含应用策略的Word文档的对象。
   * 指定文档名称的字符串值。
   * 一个字符串值，它指定策略所属的策略集的名称。 您可以指定 `null` 一个值，该值导致使 `MyPolicies` 用策略集。
   * 指定策略名称的字符串值。
   * 一个字符串值，它表示作为文档发布者的用户的用户管理器域的名称。 此参数值是可选的，可以为null(如果此参数为null，则下一个参数值必须是 `null`null)。
   * 一个字符串值，它表示作为文档发布者的用户管理器用户的规范名称。 此参数值是可选的，可以为null(如果此参数为null，则上一个参数值必须是 `null`null)。
   * 一个 `RMLocale` 值，它指定区域设置值(例如 `RMLocale.en`)。
   * 用于存储策略标识符值的字符串输出参数。
   * 用于存储受策略保护的标识符值的字符串输出参数。
   * 用于存储mime类型的字符串输出参数(例如， `application/doc`)。
   该方 `protectDocument` 法返回一 `BLOB` 个包含受策略保护的Word文档的对象。

1. 保存Word文档。

   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示受策略保护的Word文档的文件位置。
   * 创建一个字节数组，它存储由方法返 `BLOB` 回的对象的数据内 `protectDocument` 容。 通过获取对象数据成员的值 `BLOB` 填充字节 `MTOM` 数组。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的内 `Write` 容写入Word文件。

**代码示例**

有关使用Document security服务的代码示例，请参阅以下快速入门：

* “快速入门(MTOM):使用Web服务API将策略应用于Word文档”

## 从Word文档删除策略 {#removing-policies-from-word-documents}

您可以从受策略保护的Word文档中删除策略，以便从文档中删除安全性。 即，如果您不再希望文档受策略保护。 如果要使用较新的策略更新受策略保护的Word文档，则切换策略比删除策略和添加更新的策略更有效。

>[!NOTE]
>
>有关Document security服务的详细信息，请参阅AEM [表单的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-12}

要从受策略保护的Word文档中删除策略，请执行以下步骤：

1. 包括项目文件
1. 创建Document Security Client API对象。
1. 检索受策略保护的Word文档。
1. 从Word文档中删除策略。
1. 保存不安全的Word文档。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建Document Security Client API对象**

在以编程方式执行Document security服务操作之前，请先创建Document security服务客户端对象。

**检索受策略保护的Word文档**

要删除策略，必须检索受策略保护的Word文档。 如果尝试从未受策略保护的Word文档中删除策略，将导致异常。

**从Word文档中删除策略**

可以从受策略保护的Word文档中删除策略，前提是在连接设置中指定了管理员。 否则，用于保护文档的策略必须包含权限， `SWITCH_POLICY` 才能从Word文档中删除策略。 此外，在AEM Forms连接设置中指定的用户也必须具有该权限。 否则，将引发异常。

**保存不安全的Word文档**

在Document security服务从Word文档删除策略后，您可以将不安全的Word文档另存为DOC文件。

**另请参阅**

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[对Word文档应用策略](protecting-documents-policies.md#applying-policies-to-word-documents)

### 使用Java API从Word文档删除策略 {#remove-a-policy-from-a-word-document-using-the-java-api}

使用Document Security API(Java)从受策略保护的Word文档中删除策略：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-rightsmanagement-client.jar。

1. 创建Document Security Client API对象

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `RightsManagementClient` 象的构造函数并传递该对象来创建 `ServiceClientFactory` 对象。

1. 检索受策略保护的Word文档

   * 通过使 `java.io.FileInputStream` 用受策略保护的Word文档的构造函数并传递一个指定Word文档位置的字符串值，创建一个表示该文档的对象。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对象来创建 `java.io.FileInputStream` 对象。

1. 从Word文档中删除策略

   * 通过 `DocumentManager` 调用对象的方 `RightsManagementClient` 法创建对 `getDocumentManager` 象。
   * 通过调用对象的方法并传递包含受策 `DocumentManager` 略保护的Word `removeSecurity` 文档的对 `com.adobe.idp.Document` 象，从Word文档中删除策略。 此方法返回一个 `com.adobe.idp.Document` 包含不安全Word文档的对象。

1. 保存不安全的Word文档

   * 创建一 `java.io.File` 个对象，并确保文件扩展名为DOC。
   * 调用对 `Document` 象的方 `copyToFile` 法，将对象的内容复制到文件中(确保使用由 `Document` 该方法返回的对 `Document``removeSecurity` 象)。

**代码示例**

有关使用Document security服务的代码示例，请参阅以下快速入门：

* “快速入门（SOAP模式）:使用Java API从Word文档删除策略”

### 使用Web服务API从Word文档删除策略 {#remove-a-policy-from-a-word-document-using-the-web-service-api}

使用Document Security API（Web服务）从受策略保护的Word文档中删除策略：

1. 包括项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建Document Security Client API对象

   * 使用对 `RightsManagementServiceClient` 象的默认构造函数创建对象。
   * 使用构 `RightsManagementServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/RightsManagementService?WSDL`.)您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。)
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `RightsManagementServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `RightsManagementServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。


1. 检索受策略保护的Word文档

   * 使用对 `BLOB` 象的构造函数创建对象。 该 `BLOB` 对象用于存储从中删除策略的受策略保护的Word文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示Word文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 为对象的字段指定 `MTOM` 字节数组的内容来填充该对象。

1. 从Word文档中删除策略

   通过调用对象的方法并传递包含受策略保 `RightsManagementServiceClient` 护的Word文档的 `removePolicySecurity` 对象，从Word文 `BLOB` 档中删除策略。 此方法返回一个 `BLOB` 包含不安全Word文档的对象。

1. 保存不安全的Word文档

   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示不安全Word文档的文件位置。
   * 创建一个字节数组，它存储由方法返 `BLOB` 回的对象的数据内 `removePolicySecurity` 容。 通过获取对象字段的值来填 `BLOB` 充字节数 `MTOM` 组。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。

**代码示例**

有关使用Document security服务的代码示例，请参阅以下快速入门：

* “快速入门(MTOM):使用Web服务API从Word文档删除策略”

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
