---
title: 使用策略保护文档
seo-title: 使用策略保护文档
description: 使用文档安全服务动态地对Adobe PDF文档应用机密性设置并保持对文档的控制。 文档安全服务还使用户能够控制收件人使用受策略保护的PDF文档的方式。
seo-description: 使用文档安全服务动态地对Adobe PDF文档应用机密性设置并保持对文档的控制。 文档安全服务还使用户能够控制收件人使用受策略保护的PDF文档的方式。
uuid: 6feb69ef-7b61-4d0b-8c87-d65d98bae9b5
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9b1d2bf3-f28c-41b2-9026-1f3311556422
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '15544'
ht-degree: 0%

---


# 使用策略{#protecting-documents-with-policies}保护文档

**关于文档安全服务**

文档安全服务使用户能够动态地对Adobe PDF文档应用机密性设置，并保持对文档的控制，无论的分发范围有多广。

文档安全服务通过使用户能够控制收件人使用受策略保护的PDF文档的方式，防止信息扩散到用户触及范围之外。 用户可以指定谁可以打开文档，限制其使用方式，以及在文档分发后监视该数据。 用户还可以动态地控制对受策略保护的文档的访问，甚至可以动态地撤销对文档的访问。

文档安全服务还保护其他文件类型，如Microsoft Word文件（DOC文件）。 您可以使用文档安全客户端API处理这些文件类型。 支持以下版本：

* Microsoft Office 2003文件（DOC、XLS、PPT文件）
* Microsoft Office 2007文件（DOCX、XLSX、PPTX文件）
* PTC Pro/E文件

特此说明，以下两节讨论如何使用Word文档:

* [将策略应用于Word文档](protecting-documents-policies.md#applying-policies-to-word-documents)
* [从Word文档删除策略](protecting-documents-policies.md#removing-policies-from-word-documents)

您可以使用任务安全服务来完成这些文档:

* 创建策略。 有关信息，请参阅[创建策略](protecting-documents-policies.md#creating-policies)。
* 修改策略。 有关信息，请参阅[修改策略](protecting-documents-policies.md#modifying-policies)。
* 删除策略。 有关信息，请参阅[删除策略](protecting-documents-policies.md#deleting-policies)。
* 将策略应用于PDF文档。 有关信息，请参阅[将策略应用于PDF文档](protecting-documents-policies.md#applying-policies-to-pdf-documents)。
* 从PDF文档中删除策略。 有关信息，请参阅[从PDF文档删除策略](protecting-documents-policies.md#removing-policies-from-pdf-documents)。
* Inspect受政策保护的文档。 有关信息，请参阅[检查受策略保护的PDF文档](protecting-documents-policies.md#inspecting-policy-protected-pdf-documents)。
* 撤销对PDF文档的访问权。 有关信息，请参阅[撤销对文档的访问权](protecting-documents-policies.md#revoking-access-to-documents)。
* 恢复对已吊销文档的访问权限。 有关信息，请参阅[恢复对已吊销文档的访问权限](protecting-documents-policies.md#reinstating-access-to-revoked-documents)。
* 创建水印。 有关信息，请参阅[创建水印](protecting-documents-policies.md#creating-watermarks)。
* 搜索事件。 有关信息，请参阅[搜索事件](protecting-documents-policies.md#searching-for-events)。

>[!NOTE]
>
>有关文档安全服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 创建策略{#creating-policies}

您可以使用文档安全Java API或Web服务API以编程方式创建策略。 *策略*&#x200B;是包含文档安全设置、授权用户和使用权限的信息集合。 您可以使用适用于不同情况和用户的安全设置来创建和保存任意数量的策略。

策略允许您执行以下任务:

* 指定可以打开文档的个人。 收件人可以属于您的组织，也可以属于您的组织之外。
* 指定收件人如何使用文档。 您可以限制访问不同的Acrobat和Adobe Reader功能。 这些功能包括打印和复制文本、添加签名以及向文档添加注释的功能。
* 随时更改访问和安全设置，即使在分发受策略保护的文档后也是如此。
* 分发文档后，监视其使用情况。 您可以看到文档的使用情况以及使用者。 例如，您可以了解某人何时打开文档。

### 使用Web服务{#creating-a-policy-using-web-services}创建策略

使用Web服务API创建策略时，请引用描述策略的现有可移植文档权限语言(PDRL)XML文件。 策略权限和主体在PDRL文档中定义。 以下XML文档是PDRL文档的示例。

```xml
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
>有关文档安全服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary-of-steps}的摘要

要创建策略，请执行以下步骤：

1. 包括项目文件。
1. 创建文档安全客户端API对象。
1. 设置策略的属性。
1. 创建策略条目。
1. 注册策略。

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-rightsmanagement-client.jar
* 命名空间.jar(如果在JBoss上部署了AEM Forms)
* jaxb-api.jar(如果AEM Forms部署在JBoss上)
* jaxb-impl.jar(如果AEM Forms部署在JBoss上)
* jaxb-libs.jar(如果AEM Forms部署在JBoss上)
* jaxb-xjc.jar(如果AEM Forms部署在JBoss上)
* lexpingDatatype.jar(如果在JBoss上部署了AEM Forms)
* xsdlib.jar(如果AEM Forms部署在JBoss上)
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar
* jbossall-client.jar(如果未在JBoss上部署AEM Forms，请使用其他JAR文件)

有关这些JAR文件的位置的信息，请参阅[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建文档安全客户端API对象**

在以编程方式执行文档安全服务操作之前，请创建文档安全服务客户端对象。

**设置策略的属性**

要创建策略，请设置策略属性。 强制属性是策略名称。 策略名称对于每个策略集必须唯一。 策略集只是策略的集合。 如果策略属于单独的策略集，则可以有两个同名的策略。 但是，单个策略集中的两个策略不能具有相同的策略名称。

要设置的另一个有用属性是有效期。 有效期是授权文档可访问受策略保护的收件人的时间段。 如果未设置此属性，则策略始终有效。

有效期可以设置为以下选项之一：

* 从文档发布之日起，文档可访问的设定天数
* 结束日期，在此日期之后文档将无法访问
* 可访问文档的特定日期范围
* 始终有效

您只能指定开始日期，这会导致策略在开始日期之后有效。 如果仅指定结束日期，则策略在结束日期之前有效。 但是，如果未定义开始日期和结束日期，则会引发异常。

在设置属于策略的属性时，还可以设置加密设置。 这些加密设置在将策略应用于文档时生效。 您可以指定以下加密值：

* **AES256**:使用256位密钥表示AES加密算法。
* **AES128**:使用128位密钥表示AES加密算法。
* **NoEncryption：表** 示无加密。

指定`NoEncryption`选项时，不能将`PlaintextMetadata`选项设置为`false`。 如果尝试这样做，则会引发异常。

>[!NOTE]
>
>有关可设置的其他属性的信息，请参见[AEM FormsAPI参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`Policy`接口说明。

**创建策略条目**

策略条目将主体（即组和用户）和权限附加到策略。 策略必须至少包含一个策略条目。 例如，假定您执行以下任务:

* 创建并注册一个策略条目，该条目使组在联机时只能视图文档，并禁止收件人复制。
* 将策略条目附加到策略。
* 使用Acrobat确保策略文档。

这些操作导致收件人只能在线视图文档，而无法复制。 文档在安全性从其中删除之前保持安全。

**注册策略**

必须先注册新策略，才能使用新策略。 注册策略后，可以使用它保护文档。

### 使用Java API {#create-a-policy-using-the-java-api}创建策略

使用文档安全API(Java)创建策略：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-rightsmanagement-client.jar。

1. 创建文档安全客户端API对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`DocumentSecurityClient`对象的构造函数并传递`ServiceClientFactory`对象，创建&lt;a0/>对象。

1. 设置策略的属性。

   * 通过调用`InfomodelObjectFactory`对象的静态`createPolicy`方法创建`Policy`对象。 此方法返回`Policy`对象。
   * 通过调用`Policy`对象的`setName`方法并传递指定策略名称的字符串值，设置策略的名称属性。
   * 通过调用`Policy`对象的`setDescription`方法并传递指定策略描述的字符串值，设置策略的描述。
   * 通过调用`Policy`对象的`setPolicySetName`方法并传递指定策略集名称的字符串值，设置新策略所属的策略集。 （可以为此参数值指定`null`，以将策略添加到&#x200B;*My Policies*&#x200B;策略集。）
   * 通过调用`InfomodelObjectFactory`对象的静态`createValidityPeriod`方法创建策略的有效期。 此方法返回`ValidityPeriod`对象。
   * 通过调用`ValidityPeriod`对象的`setRelativeExpirationDays`方法并传递一个指定天数的整数值，设置可访问受策略保护的文档的天数。
   * 通过调用`Policy`对象的`setValidityPeriod`方法并传递`ValidityPeriod`对象，设置策略的有效期。

1. 创建策略条目。

   * 通过调用`InfomodelObjectFactory`对象的静态`createPolicyEntry`方法创建策略条目。 此方法返回`PolicyEntry`对象。
   * 通过调用`InfomodelObjectFactory`对象的静态`createPermission`方法指定策略的权限。 传递属于表示权限的`Permission`接口的静态数据成员。 此方法返回`Permission`对象。 例如，要添加允许用户从受策略保护的PDF文档复制数据的权限，请传递`Permission.COPY`。 （对要添加的每个权限重复此步骤）。
   * 通过调用`PolicyEntry`对象的`addPermission`方法并传递`Permission`对象，将权限添加到策略条目。 （对您创建的每个`Permission`对象重复此步骤）。
   * 通过调用`InfomodelObjectFactory`对象的静态`createSpecialPrincipal`方法创建策略主体。 传递属于表示主体的`InfomodelObjectFactory`对象的数据成员。 此方法返回`Principal`对象。 例如，要将文档的发布者添加为主体，请传递`InfomodelObjectFactory.PUBLISHER_PRINCIPAL`。
   * 通过调用`PolicyEntry`对象的`setPrincipal`方法并传递`Principal`对象，将主体添加到策略条目中。
   * 通过调用`Policy`对象的`addPolicyEntry`方法并传递`PolicyEntry`对象，将策略条目添加到策略中。

1. 注册策略。

   * 通过调用`DocumentSecurityClient`对象的`getPolicyManager`方法创建`PolicyManager`对象。
   * 通过调用`PolicyManager`对象的`registerPolicy`方法并传递以下值来注册策略：

      * 表示要注册的策略的`Policy`对象。
   * 一个字符串值，它表示策略所属的策略集。

   如果在连接设置中使用AEM forms administrator帐户创建`DocumentSecurityClient`对象，则在调用`registerPolicy`方法时指定策略集名称。 如果为策略集传递`null`值，则在管理员&#x200B;*我的策略*&#x200B;策略集中创建策略。

   如果在连接设置中使用文档安全用户，则可以调用仅接受策略的重载`registerPolicy`方法。 即，您无需指定策略集名称。 但是，策略将添加到名为&#x200B;*My Policys*&#x200B;的策略集。 如果不想将此新策略添加到此策略集，请在调用`registerPolicy`方法时指定策略集名称。

   >[!NOTE]
   >
   >创建策略时，请引用现有策略集。 如果指定的策略集不存在，则会引发异常。

有关使用文档安全服务的代码示例，请参阅：

* &quot;快速开始（SOAP模式）:使用Java API创建策略”

### 使用Web服务API {#create-a-policy-using-the-web-service-api}创建策略

使用文档安全API（Web服务）创建策略：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建文档安全客户端API对象。

   * 使用其默认构造函数创建`DocumentSecurityServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`DocumentSecurityServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 您无需使用`lc_version`属性。 此属性在您创建服务引用时使用。)
   * 通过获取`RightsManagementServiceClient.Endpoint.Binding`字段的值创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段`RightsManagementServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`RightsManagementServiceClient.ClientCredentials.UserName.Password`分配相应的口令值。
      * 将常量值`HttpClientCredentialType.Basic`指定到字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`指定到字段`BasicHttpBindingSecurity.Security.Mode`。


1. 设置策略的属性。

   * 使用`PolicySpec`对象的构造函数创建&lt;a0/>对象。
   * 通过为`PolicySpec`对象的`name`数据成员分配字符串值来设置策略的名称。
   * 通过为`PolicySpec`对象的`description`数据成员分配字符串值来设置策略的说明。
   * 通过为`PolicySpec`对象的`policySetName`数据成员分配字符串值，设置策略将属于的策略集。 必须指定现有策略集名称。 （可以为此参数值指定`null`，以将策略添加到&#x200B;*My Policys*。）
   * 通过为`PolicySpec`对象的`offlineLeasePeriod`数据成员分配整数值来设置策略的脱机租用期。
   * 使用表示PDRL XML数据的字符串值设置`PolicySpec`对象的`policyXml`数据成员。 要执行此任务，请使用其构造函数创建。NET `StreamReader`对象。 将表示策略的PDRL XML文件的位置传递给`StreamReader`构造函数。 然后，调用`StreamReader`对象的`ReadLine`方法，并将返回值指定给字符串变量。 对`StreamReader`对象进行迭代，直到`ReadLine`方法返回null。 将字符串变量指定给`PolicySpec`对象的`policyXml`数据成员。

1. 创建策略条目。

   使用文档安全Web服务API创建策略时，无需创建策略条目。 策略条目在PDRL文档中定义。

1. 注册策略。

   通过调用`DocumentSecurityServiceClient`对象的`registerPolicy`方法并传递以下值来注册策略：

   * 表示要注册的策略的`PolicySpec`对象。
   * 一个字符串值，它表示策略所属的策略集。 可以指定一个`null`值，该值导致将策略添加到&#x200B;*MyPoliges*&#x200B;策略集。

   如果在连接设置中使用AEM forms administrator帐户创建`DocumentSecurityClient`对象，请在调用`registerPolicy`方法时指定策略集名称。

   如果在连接设置中使用文档SecurityDocument Security用户，则可以调用仅接受策略的重载`registerPolicy`方法。 即，您无需指定策略集名称。 但是，策略将添加到名为&#x200B;*My Policys*&#x200B;的策略集。 如果不想将此新策略添加到此策略集，请在调用`registerPolicy`方法时指定策略集名称。

   >[!NOTE]
   >
   >创建策略并指定策略集时，请确保指定现有策略集。 如果指定的策略集不存在，则会引发异常。

有关使用文档安全服务的代码示例，请参阅以下快速开始:

* “快速开始(MTOM):使用Web服务API创建策略”
* “快速开始(SwaRef):使用Web服务API创建策略”

## 修改策略{#modifying-policies}

您可以使用文档安全Java API或Web服务API修改现有策略。 要更改现有策略，请检索该策略，修改它，然后在服务器上更新该策略。 例如，假定您检索现有策略并延长其有效期。 在更改生效之前，必须更新策略。

当业务需求发生变化且策略不再反映这些要求时，您可以修改策略。 您只需更新现有策略，而不是创建新策略。

要使用Web服务修改策略属性（例如，使用使用JAX-WS创建的Java代理类），必须确保向文档安全服务注册策略。 然后，可以使用`PolicySpec.getPolicyXml`方法引用现有策略，并使用适用的方法修改策略属性。 例如，可以通过调用`PolicySpec.setOfflineLeasePeriod`方法来修改脱机租用期。

>[!NOTE]
>
>有关文档安全服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-1}的摘要

要修改现有策略，请执行以下步骤：

1. 包括项目文件。
1. 创建文档安全客户端API对象。
1. 检索现有策略。
1. 更改策略属性。
1. 更新策略。

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建文档安全客户端API对象**

在以编程方式执行文档安全服务操作之前，必须创建文档安全服务客户端对象。 如果您使用Java API，请创建`RightsManagementClient`对象。 如果您使用文档安全Web服务API，请创建`RightsManagementServiceService`对象。

**检索现有策略**

您必须检索现有策略才能对其进行修改。 要检索策略，请指定策略名称和策略所属的策略集。 如果为策略集名称指定`null`值，则从&#x200B;*My Policys*&#x200B;策略集检索策略。

**设置策略的属性**

要修改策略，请修改策略属性的值。 唯一无法更改的策略属性是name属性。 例如，要更改策略的脱机租用期，可以修改策略的脱机租用期属性的值。

使用Web服务修改策略的脱机租用期时，将忽略`PolicySpec`接口上的`offlineLeasePeriod`字段。 要更新脱机租用期，请修改PDRL XML文档中的`OfflineLeasePeriod`元素。 然后，使用`PolicySpec`接口的`policyXML`文档成员引用更新的PDRL XML。

>[!NOTE]
>
>有关可设置的其他属性的信息，请参见[AEM FormsAPI参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`Policy`接口说明。

**更新策略**

在对策略所做的更改生效之前，必须使用文档安全服务更新策略。 对保护文档的策略所做的更改将在受策略保护的文档下次与文档安全服务同步时更新。

### 使用Java API {#modify-existing-policies-using-the-java-api}修改现有策略

使用文档安全API(Java)修改现有策略：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-rightsmanagement-client.jar。

1. 创建文档安全客户端API对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`RightsManagementClient`对象的构造函数并传递`ServiceClientFactory`对象，创建&lt;a0/>对象。

1. 检索现有策略。

   * 通过调用`RightsManagementClient`对象的`getPolicyManager`方法创建`PolicyManager`对象。
   * 通过调用`PolicyManager`对象的`getPolicy`方法并传递以下值，创建表示要更新的策略的`Policy`对象&quot;

      * 一个字符串值，它表示策略所属的策略集名称。 可以指定导致使用`MyPolicies`策略集的`null`。
      * 表示策略名称的字符串值。

1. 设置策略的属性。

   更改策略属性以满足您的业务需求。 例如，要更改策略的脱机租用期，请调用`Policy`对象的`setOfflineLeasePeriod`方法。

1. 更新策略。

   通过调用`PolicyManager`对象的`updatePolicy`方法更新策略。 传递表示要更新的策略的`Policy`对象。

**代码示例**

有关使用文档安全服务的代码示例，请参阅快速开始（SOAP模式）:使用Java API部分修改策略。

### 使用Web服务API {#modify-existing-policies-using-the-web-service-api}修改现有策略

使用文档安全API（Web服务）修改现有策略：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建文档安全客户端API对象。

   * 使用其默认构造函数创建`RightsManagementServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`RightsManagementServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 您无需使用`lc_version`属性。 此属性在您创建服务引用时使用。)
   * 通过获取`RightsManagementServiceClient.Endpoint.Binding`字段的值创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段`RightsManagementServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`RightsManagementServiceClient.ClientCredentials.UserName.Password`分配相应的口令值。
      * 将常量值`HttpClientCredentialType.Basic`指定到字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`指定到字段`BasicHttpBindingSecurity.Security.Mode`。


1. 检索现有策略。

   通过调用`RightsManagementServiceClient`对象的`getPolicy`方法并传递以下值，创建表示要修改的策略的`PolicySpec`对象：

   * 一个字符串值，它指定策略所属的策略集名称。 可以指定导致使用`MyPolicies`策略集的`null`。
   * 指定策略名称的字符串值。

1. 设置策略的属性。

   更改策略属性以满足您的业务需求。

1. 更新策略。

   通过调用`RightsManagementServiceClient`对象的`updatePolicyFromSDK`方法并传递表示要更新的策略的`PolicySpec`对象来更新策略。

**代码示例**

有关使用文档安全服务的代码示例，请参阅以下快速开始:

* “快速开始(MTOM):使用Web服务API修改策略”
* “快速开始(SwaRef):使用Web服务API修改策略”

## 删除策略{#deleting-policies}

您可以使用文档安全Java API或Web服务API删除现有策略。 删除策略后，将不再能用于保护文档。 但是，使用策略的现有受策略保护的文档仍受到保护。 当较新的策略可用时，可以删除策略。

>[!NOTE]
>
>有关文档安全服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-2}的摘要

要删除现有策略，请执行以下步骤：

1. 包括项目文件
1. 创建文档安全客户端API对象。
1. 删除策略。

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建文档安全客户端API对象**

在以编程方式执行文档安全服务操作之前，必须创建文档安全服务客户端对象。 如果您使用Java API，请创建`RightsManagementClient`对象。 如果您使用文档安全Web服务API，请创建`RightsManagementServiceService`对象。

**删除策略**

要删除策略，请指定要删除的策略以及策略所属的策略集。 设置用于调用AEM Forms的用户必须具有删除策略的权限；否则会出现异常。 同样，如果尝试删除不存在的策略，则会发生异常。

### 使用Java API {#delete-policies-using-the-java-api}删除策略

使用文档安全API(Java)删除策略：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-rightsmanagement-client.jar。

1. 创建文档安全客户端API对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`RightsManagementClient`对象的构造函数并传递`ServiceClientFactory`对象，创建&lt;a0/>对象。

1. 删除策略。

   * 通过调用`RightsManagementClient`对象的`getPolicyManager`方法创建`PolicyManager`对象。
   * 通过调用`PolicyManager`对象的`deletePolicy`方法并传递以下值来删除策略：

      * 一个字符串值，它指定策略所属的策略集名称。 可以指定导致使用`MyPolicies`策略集的`null`。
      * 一个字符串值，它指定要删除的策略的名称。

**代码示例**

有关使用文档安全服务的代码示例，请参阅以下快速开始:

* &quot;快速开始（SOAP模式）:使用Java API删除策略”

### 使用Web服务API {#delete-policies-using-the-web-service-api}删除策略

使用文档安全API（Web服务）删除策略：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建文档安全客户端API对象。

   * 使用其默认构造函数创建`RightsManagementServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`RightsManagementServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 您无需使用`lc_version`属性。 此属性在您创建服务引用时使用。)
   * 通过获取`RightsManagementServiceClient.Endpoint.Binding`字段的值创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段`RightsManagementServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`RightsManagementServiceClient.ClientCredentials.UserName.Password`分配相应的口令值。
      * 将常量值`HttpClientCredentialType.Basic`指定到字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`指定到字段`BasicHttpBindingSecurity.Security.Mode`。


1. 删除策略。

   通过调用`RightsManagementServiceClient`对象的`deletePolicy`方法并传递以下值来删除策略：

   * 一个字符串值，它指定策略所属的策略集名称。 可以指定导致使用`MyPolicies`策略集的`null`。
   * 一个字符串值，它指定要删除的策略的名称。

**代码示例**

有关使用文档安全服务的代码示例，请参阅以下快速开始:

* “快速开始(MTOM):使用Web服务API删除策略”
* “快速开始(SwaRef):使用Web服务API删除策略”

## 将策略应用于PDF文档{#applying-policies-to-pdf-documents}

您可以将策略应用于PDF文档以保护文档。 通过将策略应用于PDF文档，您可以限制对文档的访问。 如果文档已使用策略保护，则不能对文档应用策略。

在文档打开时，您还可以限制对Acrobat和Adobe Reader功能的访问，包括打印和复制文本、进行更改以及向文档添加签名和注释的能力。 此外，当您不再希望用户访问受策略保护的PDF文档时，您可以撤销该文档。

在分发受策略保护的文档后，可以监视其使用情况。 即，您可以看到文档的使用方式以及使用者。 例如，您可以查找某人何时打开文档。

>[!NOTE]
>
>有关文档安全服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-3}的摘要

要将策略应用于PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建文档安全客户端API对象。
1. 检索应用策略的PDF文档。
1. 将现有策略应用于PDF文档。
1. 保存受策略保护的PDF文档。

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建文档安全客户端API对象**

在以编程方式执行文档安全服务操作之前，请创建文档安全服务客户端对象。 如果您使用Java API，请创建`DocumentSecurityClient`对象。 如果您使用文档安全Web服务API，请创建`DocumentSecurityServiceService`对象。

**检索PDF文档**

您可以检索PDF文档以应用策略。 对PDF文档应用策略后，用户在使用该文档时受到限制。 例如，如果策略未启用脱机时文档的打开，则用户必须联机才能打开文档。

**将现有策略应用于PDF文档**

要将策略应用于PDF文档，请引用现有策略并指定策略所属的策略集。 设置连接属性的用户必须有权访问指定的策略。 否则，会出现异常。

**保存PDF文档**

在文档安全服务将策略应用于PDF文档后，您可以将受策略保护的PDF文档另存为PDF文件。

**另请参阅**

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[撤销对文档的访问](protecting-documents-policies.md#revoking-access-to-documents)

### 使用Java API {#apply-a-policy-to-a-pdf-document-using-the-java-api}将策略应用于PDF文档

使用文档安全API(Java)将策略应用于PDF文档:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-rightsmanagement-client.jar。

1. 创建文档安全客户端API对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`RightsManagementClient`对象的构造函数并传递`ServiceClientFactory`对象，创建&lt;a0/>对象。

1. 检索PDF文档。

   * 使用PDF文档的构造函数创建一个`java.io.FileInputStream`对象。 传递一个指定PDF文档位置的字符串值。
   * 使用`com.adobe.idp.Document`对象的构造函数并传递`java.io.FileInputStream`对象，创建&lt;a0/>对象。

1. 将现有策略应用于PDF文档。

   * 通过调用`RightsManagementClient`对象的`getDocumentManager`方法创建`DocumentManager`对象。
   * 通过调用`DocumentManager`对象的`protectDocument`方法并传递以下值，将策略应用于PDF文档:

      * `com.adobe.idp.Document`对象，其中包含应用策略的PDF文档。
      * 一个字符串值，它指定文档的名称。
      * 一个字符串值，它指定策略所属的策略集的名称。 可以指定一个`null`值，该值会导致使用`MyPolicies`策略集。
      * 指定策略名称的字符串值。
      * 一个字符串值，它表示作为文档发布者的用户的用户管理器域的名称。 此参数值是可选的，可以为null（如果此参数为null，则下一个参数值必须为null）。
      * 一个字符串值，它表示作为文档发布者的用户管理器用户的规范名称。 此参数值是可选的，可以是`null`（如果此参数为null，则前一个参数值必须为`null`）。
      * 一个`com.adobe.livecycle.rightsmanagement.Locale`，它表示用于选择MS Office模板的区域设置。 此参数值是可选的，不用于PDF文档。 要保护PDF文档，请指定`null`。

      `protectDocument`方法返回一个`RMSecureDocumentResult`对象，该对象包含受策略保护的PDF文档。


1. 保存PDF文档。

   * 调用`RMSecureDocumentResult`对象的`getProtectedDoc`方法以获取受策略保护的PDF文档。 此方法返回`com.adobe.idp.Document`对象。
   * 创建`java.io.File`对象，并确保文件扩展名为PDF。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法，将`Document`对象的内容复制到文件（确保使用`getProtectedDoc`方法返回的`Document`对象）。

**代码示例**

有关使用文档安全服务的代码示例，请参阅以下快速开始:

* “快速开始（EJB模式）:使用Java API将策略应用于PDF文档”
* &quot;快速开始（SOAP模式）:使用Java API将策略应用于PDF文档”

**另请参阅**

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#apply-a-policy-to-a-pdf-document-using-the-web-service-api}将策略应用于PDF文档

使用文档安全API（Web服务）将策略应用于PDF文档:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建文档安全客户端API对象。

   * 使用其默认构造函数创建`RightsManagementServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`RightsManagementServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给Forms服务（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 您无需使用`lc_version`属性。 此属性在您创建服务引用时使用。)
   * 通过获取`RightsManagementServiceClient.Endpoint.Binding`字段的值创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段`RightsManagementServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`RightsManagementServiceClient.ClientCredentials.UserName.Password`分配相应的口令值。
      * 将常量值`HttpClientCredentialType.Basic`指定到字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`指定到字段`BasicHttpBindingSecurity.Security.Mode`。


1. 检索PDF文档。

   * 使用`BLOB`对象的构造函数创建&lt;a0/>对象。 `BLOB`对象用于存储应用策略的PDF文档。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示PDF文档的文件位置以及打开文件的模式。
   * 创建存储`System.IO.FileStream`对象内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性，确定字节数组大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，用流数据填充字节数组。 传递要读取的字节数组、开始位置和流长度。
   * 通过为`MTOM`字段指定字节数组的内容，填充`BLOB`对象。

1. 将现有策略应用于PDF文档。

   通过调用`RightsManagementServiceClient`对象的`protectDocument`方法并传递以下值，将策略应用于PDF文档:

   * `BLOB`对象，其中包含应用策略的PDF文档。
   * 一个字符串值，它指定文档的名称。
   * 一个字符串值，它指定策略所属的策略集的名称。 可以指定一个`null`值，该值会导致使用`MyPolicies`策略集。
   * 指定策略名称的字符串值。
   * 一个字符串值，它表示作为文档发布者的用户的用户管理器域的名称。 此参数值是可选的，可以为null（如果此参数为null，则下一个参数值必须为`null`）。
   * 一个字符串值，它表示作为文档发布者的用户管理器用户的规范名称。 此参数值是可选的，可以为null（如果此参数为null，则上一个参数值必须为`null`）。
   * 一个`RMLocale`值，它指定区域设置值（例如`RMLocale.en`）。
   * 用于存储策略标识符值的字符串输出参数。
   * 用于存储受策略保护的标识符值的字符串输出参数。
   * 用于存储mime类型的字符串输出参数（例如，`application/pdf`）。

   `protectDocument`方法返回一个`BLOB`对象，该对象包含受策略保护的PDF文档。

1. 保存PDF文档。

   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示受策略保护的PDF文档的文件位置。
   * 创建一个字节数组，用于存储`protectDocument`方法返回的`BLOB`对象的数据内容。 通过获取`BLOB`对象的`MTOM`数据成员的值，填充字节数组。
   * 通过调用`System.IO.BinaryWriter`对象的构造函数并传递`System.IO.FileStream`对象，创建&lt;a0/>对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

**代码示例**

有关使用文档安全服务的代码示例，请参阅以下快速开始:

* “快速开始(MTOM):使用Web服务API将策略应用于PDF文档”
* “快速开始(SwaRef):使用Web服务API将策略应用于PDF文档”

## 从PDF文档{#removing-policies-from-pdf-documents}删除策略

您可以从受策略保护的文档中删除策略，以便从文档中删除安全性。 也就是说，如果您不再希望文档受策略保护。 如果要使用较新的策略更新受策略保护的文档，则切换策略比删除策略和添加更新的策略更有效。

>[!NOTE]
>
>有关文档安全服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-4}的摘要

要从受策略保护的PDF文档中删除策略，请执行以下步骤：

1. 包括项目文件
1. 创建文档安全客户端API对象。
1. 检索受策略保护的PDF文档。
1. 从PDF文档中删除策略。
1. 保存不安全的PDF文档。

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建文档安全客户端API对象**

在以编程方式执行文档安全服务操作之前，请创建文档安全服务客户端对象。

**检索受策略保护的PDF文档**

您可以检索受策略保护的PDF文档以删除策略。 如果尝试从未受策略保护的PDF文档中删除策略，将引起异常。

**从PDF文档中删除策略**

如果在连接设置中指定了管理员，则可以从受策略保护的PDF文档中删除策略。 否则，用于保护文档的策略必须包含`SWITCH_POLICY`权限，才能从PDF文档中删除策略。 此外，在AEM Forms连接设置中指定的用户也必须具有该权限。 否则，将引发异常。

**保存不安全的PDF文档**

在文档安全服务从PDF文档中删除策略后，您可以将不安全的PDF文档另存为PDF文件。

**另请参阅**

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[将策略应用于PDF文档](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### 使用Java API {#remove-a-policy-from-a-pdf-document-using-the-java-api}从PDF文档中删除策略

使用文档安全API(Java)从受策略保护的PDF文档中删除策略：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-rightsmanagement-client.jar。

1. 创建文档安全客户端API对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`DocumentSecurityClient`对象的构造函数并传递`ServiceClientFactory`对象，创建&lt;a0/>对象。

1. 检索受策略保护的PDF文档。

   * 使用`java.io.FileInputStream`对象的构造函数并传递一个指定PDF文档位置的字符串值，创建一个表示受策略保护的PDF文档的&lt;a0/>对象。
   * 使用`com.adobe.idp.Document`对象的构造函数并传递`java.io.FileInputStream`对象，创建&lt;a0/>对象。

1. 从PDF文档中删除策略。

   * 通过调用`DocumentSecurityClient`对象的`getDocumentManager`方法创建`DocumentManager`对象。
   * 通过调用`DocumentManager`对象的`removeSecurity`方法并传递包含受策略保护的PDF文档的`com.adobe.idp.Document`对象，从PDF文档中删除策略。 此方法返回一个`com.adobe.idp.Document`对象，它包含一个不安全的PDF文档。

1. 保存不安全的PDF文档。

   * 创建`java.io.File`对象，并确保文件扩展名为PDF。
   * 调用`Document`对象的`copyToFile`方法，将`Document`对象的内容复制到文件（确保使用`removeSecurity`方法返回的`Document`对象）。

**代码示例**

有关使用文档安全服务的代码示例，请参阅以下快速开始:

* &quot;快速开始（SOAP模式）:使用Java API从PDF文档删除策略”

### 使用Web服务API {#remove-a-policy-using-the-web-service-api}删除策略

使用文档安全API（Web服务）从受策略保护的PDF文档中删除策略：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建文档安全客户端API对象。

   * 使用其默认构造函数创建`DocumentSecurityServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`DocumentSecurityServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 您无需使用`lc_version`属性。 此属性在您创建服务引用时使用。)
   * 通过获取`DocumentSecurityServiceClient.Endpoint.Binding`字段的值创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段`DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`DocumentSecurityServiceClient.ClientCredentials.UserName.Password`分配相应的口令值。
      * 将常量值`HttpClientCredentialType.Basic`指定到字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`指定到字段`BasicHttpBindingSecurity.Security.Mode`。


1. 检索受策略保护的PDF文档。

   * 使用`BLOB`对象的构造函数创建&lt;a0/>对象。 `BLOB`对象用于存储受策略保护的PDF文档，从中删除策略。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示PDF文档的文件位置以及打开文件的模式。
   * 创建存储`System.IO.FileStream`对象内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性，可以确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过为`MTOM`字段指定字节数组的内容，填充`BLOB`对象。

1. 从PDF文档中删除策略。

   通过调用`DocumentSecurityServiceClient`对象的`removePolicySecurity`方法并传递包含受策略保护的PDF文档的`BLOB`对象，从PDF文档中删除策略。 此方法返回一个`BLOB`对象，它包含一个不安全的PDF文档。

1. 保存不安全的PDF文档。

   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示不安全的PDF文档的文件位置。
   * 创建一个字节数组，用于存储`removePolicySecurity`方法返回的`BLOB`对象的数据内容。 通过获取`BLOB`对象的`MTOM`字段的值，填充字节数组。
   * 通过调用`System.IO.BinaryWriter`对象的构造函数并传递`System.IO.FileStream`对象，创建&lt;a0/>对象。

**代码示例**

有关使用文档安全服务的代码示例，请参阅以下快速开始:

* “快速开始(MTOM):使用Web服务API从PDF文档删除策略”
* “快速开始(SwaRef):使用Web服务API从PDF文档删除策略”

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 撤销对文档{#revoking-access-to-documents}的访问

您可以撤销对受策略保护的PDF文档的访问权，导致用户无法访问该文档的所有副本。 当用户尝试打开已撤销的PDF文档时，会将其重定向到可查看修改的文档的指定URL。 必须以编程方式指定用户被重定向到的URL。 当您撤销对文档的访问权时，更改将在用户下次通过联机打开受策略保护的文档与文档安全服务同步时生效。

撤销对文档的访问权限的能力提供了额外的安全性。 例如，假定文档有较新版本可用，并且您不再希望任何人查看过时的版本。 在这种情况下，可以撤销对旧文档的访问权，除非恢复访问权，否则任何人都无法视图文档。

>[!NOTE]
>
>有关文档安全服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-5}的摘要

要撤销受策略保护的文档，请执行以下步骤：

1. 包括项目文件。
1. 创建文档安全客户端API对象。
1. 检索受策略保护的PDF文档。
1. 撤销受策略保护的文档。

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建文档安全客户端API对象**

在以编程方式执行文档安全服务操作之前，必须创建文档安全服务客户端对象。

**检索受策略保护的PDF文档**

您必须检索受策略保护的PDF文档才能撤销它。 您不能撤销已撤销或不是受策略保护的文档的文档。

如果您知道受策略保护的文档的许可证标识符值，则无需检索受策略保护的PDF文档。 但是，在大多数情况下，您需要检索PDF文档才能获得许可证标识符值。

**撤销受策略保护的文档**

要撤销受策略保护的文档，请指定受策略保护的文档的许可证标识符。 此外，还可以指定用户在尝试打开已吊销文档时可以视图的文档的URL。 即假设已过时的文档被吊销。 当用户尝试打开已撤销的文档时，他们将看到更新的文档而不是已撤销的文档。

>[!NOTE]
>
>如果尝试撤销已撤销的文档，则会引发异常。

**另请参阅**

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[将策略应用于PDF文档](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[恢复对已吊销文档的访问](protecting-documents-policies.md#reinstating-access-to-revoked-documents)

### 使用Java API {#revoke-access-to-documents-using-the-java-api}撤销对文档的访问权

使用文档安全API(Java)撤销对受策略保护的PDF文档的访问权：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-rightsmanagement-client.jar。

1. 创建文档安全客户端API对象

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`DocumentSecurityClient`对象的构造函数并传递`ServiceClientFactory`对象，创建&lt;a0/>对象。

1. 检索受策略保护的PDF文档

   * 使用`java.io.FileInputStream`对象的构造函数并传递一个指定PDF文档位置的字符串值，创建一个&lt;a0/>对象，它表示受策略保护的PDF文档。
   * 使用`com.adobe.idp.Document`对象的构造函数并传递`java.io.FileInputStream`对象，创建&lt;a0/>对象。

1. 撤销受策略保护的文档

   * 通过调用`DocumentSecurityClient`对象的`getDocumentManager`方法创建`DocumentManager`对象。
   * 通过调用`DocumentManager`对象的`getLicenseId`方法，检索受策略保护的文档的许可证标识符值。 传递表示受策略保护的文档的`com.adobe.idp.Document`对象。 此方法返回表示许可证标识符值的字符串值。
   * 通过调用`DocumentSecurityClient`对象的`getLicenseManager`方法创建`LicenseManager`对象。
   * 通过调用`LicenseManager`对象的`revokeLicense`方法并传递以下值，撤销受策略保护的文档:

      * 一个字符串值，它指定受策略保护的文档的许可证标识符值（指定`DocumentManager`对象的`getLicenseId`方法的返回值）。
      * `License`接口的静态数据成员，它指定撤销文档的原因。 例如，可以指定`License.DOCUMENT_REVISED`。
      * 一个`java.net.URL`值，它指定修订文档所在的位置。 如果您不想将用户重定向到另一个URL，则可以传递`null`。

**代码示例**

有关使用文档安全服务的代码示例，请参阅以下快速开始:

* &quot;快速开始（SOAP模式）:使用Java API撤销文档”

### 使用Web服务API {#revoke-access-to-documents-using-the-web-service-api}撤销对文档的访问权

使用文档安全API（Web服务）撤销对受策略保护的PDF文档的访问权：

1. 包括项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建文档安全客户端API对象

   * 使用其默认构造函数创建`DocumentSecurityServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`DocumentSecurityServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 您无需使用`lc_version`属性。 此属性在您创建服务引用时使用。)
   * 通过获取`DocumentSecurityServiceClient.Endpoint.Binding`字段的值创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段`DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`DocumentSecurityServiceClient.ClientCredentials.UserName.Password`分配相应的口令值。
      * 将常量值`HttpClientCredentialType.Basic`指定到字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`指定到字段`BasicHttpBindingSecurity.Security.Mode`。


1. 检索受策略保护的PDF文档

   * 使用`BLOB`对象的构造函数创建&lt;a0/>对象。 `BLOB`对象用于存储已撤销的受策略保护的PDF文档。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示要撤销的受策略保护的PDF文档的文件位置以及打开文件的模式。
   * 创建存储`System.IO.FileStream`对象内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性，可以确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过为`MTOM`字段指定字节数组的内容，填充`BLOB`对象。

1. 撤销受策略保护的文档

   * 通过调用`DocumentSecurityServiceClient`对象的`getLicenseID`方法并传递表示受策略保护的文档的`BLOB`对象，检索受策略保护的文档的许可证标识符值。 此方法返回表示许可证标识符的字符串值。
   * 通过调用`DocumentSecurityServiceClient`对象的`revokeLicense`方法并传递以下值，撤销受策略保护的文档:

      * 一个字符串值，它指定受策略保护的文档的许可证标识符值（指定`DocumentSecurityServiceService`对象的`getLicenseId`方法的返回值）。
      * `Reason`枚举的静态数据成员，它指定撤销文档的原因。 例如，可以指定`Reason.DOCUMENT_REVISED`。
      * 一个`string`值，它指定修订文档所在的URL位置。 如果您不想将用户重定向到另一个URL，则可以传递`null`。

**代码示例**

有关使用文档安全服务的代码示例，请参阅以下快速开始:

* “快速开始(MTOM):使用Web服务API撤销文档”
* “快速开始(SwaRef):使用Web服务API撤销文档”

**另请参阅**

[从Word文档删除策略](protecting-documents-policies.md#removing-policies-from-word-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 恢复对已吊销文档的访问权限{#reinstating-access-to-revoked-documents}

您可以恢复对已撤销PDF文档的访问权，使用户可以访问已撤销文档的所有副本。 当用户打开被撤销的恢复文档时，用户能够视图文档。

>[!NOTE]
>
>有关文档安全服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-6}的摘要

要恢复对已吊销的PDF文档的访问权限，请执行以下步骤：

1. 包括项目文件。
1. 创建文档安全客户端API对象。
1. 检索已吊销的PDF文档的许可证标识符。
1. 恢复对已吊销的PDF文档的访问权限。

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建文档安全客户端API对象**

在以编程方式执行文档安全服务操作之前，必须创建文档安全服务客户端对象。 如果您使用Java API，请创建`DocumentSecurityClient`对象。 如果您使用文档安全Web服务API，请创建`DocumentSecurityServiceService`对象。

**检索已吊销的PDF文档的许可证标识符**

您必须检索已吊销的PDF文档的许可证标识符，才能恢复已吊销的PDF文档。 获取许可证标识符值后，可恢复已吊销的文档。 如果尝试恢复未撤销的文档，将导致异常。

**恢复对已吊销的PDF文档的访问权限**

要恢复对已吊销的PDF文档的访问权，必须指定已吊销的文档的许可证标识符。 如果尝试恢复未撤销的PDF文档的访问权限，将引起异常。

**另请参阅**

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[将策略应用于PDF文档](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[撤销对文档的访问](protecting-documents-policies.md#revoking-access-to-documents)

### 使用Java API {#reinstate-access-to-revoked-documents-using-the-java-api}恢复对已吊销文档的访问

使用文档安全API(Java)恢复对已吊销文档的访问：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-rightsmanagement-client.jar。

1. 创建文档安全客户端API对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`DocumentSecurityClient`对象的构造函数并传递`ServiceClientFactory`对象，创建&lt;a0/>对象。

1. 检索已吊销的PDF文档的许可证标识符。

   * 使用`java.io.FileInputStream`对象的构造函数并传递一个指定PDF文档位置的字符串值，创建一个表示已吊销的PDF文档的&lt;a0/>对象。
   * 使用`com.adobe.idp.Document`对象的构造函数并传递`java.io.FileInputStream`对象，创建&lt;a0/>对象。
   * 通过调用`DocumentSecurityClient`对象的`getDocumentManager`方法创建`DocumentManager`对象。
   * 通过调用`DocumentManager`对象的`getLicenseId`方法并传递表示已吊销文档的`com.adobe.idp.Document`对象，检索已吊销文档的许可证标识符值。 此方法返回表示许可证标识符的字符串值。

1. 恢复对已吊销的PDF文档的访问权限。

   * 通过调用`DocumentSecurityClient`对象的`getLicenseManager`方法创建`LicenseManager`对象。
   * 通过调用`LicenseManager`对象的`unrevokeLicense`方法并传递已吊销文档的许可证标识符值，恢复对已吊销PDF文档的访问权。

**代码示例**

有关使用文档安全服务的代码示例，请参阅以下快速开始:

* &quot;快速开始（SOAP模式）:使用Web服务API恢复对已吊销文档的访问权”

### 使用Web服务API {#reinstate-access-to-revoked-documents-using-the-web-service-api}恢复对已吊销文档的访问

使用文档安全API（Web服务）恢复对已吊销文档的访问：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建文档安全客户端API对象。

   * 使用其默认构造函数创建`DocumentSecurityServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`DocumentSecurityServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 您无需使用`lc_version`属性。 此属性在您创建服务引用时使用。)
   * 通过获取`DocumentSecurityServiceClient.Endpoint.Binding`字段的值创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段`DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`DocumentSecurityServiceClient.ClientCredentials.UserName.Password`分配相应的口令值。
      * 将常量值`HttpClientCredentialType.Basic`指定到字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`指定到字段`BasicHttpBindingSecurity.Security.Mode`。


1. 检索已吊销的PDF文档的许可证标识符。

   * 使用`BLOB`对象的构造函数创建&lt;a0/>对象。 `BLOB`对象用于存储已撤销的PDF文档，恢复对其访问。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示已撤销的PDF文档的文件位置以及打开文件的模式。
   * 创建存储`System.IO.FileStream`对象内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性，可以确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过为`MTOM`字段指定字节数组的内容，填充`BLOB`对象。

1. 恢复对已吊销的PDF文档的访问权限。

   * 通过调用`DocumentSecurityServiceClient`对象的`getLicenseID`方法并传递表示已吊销文档的`BLOB`对象，检索已吊销文档的许可证标识符值。 此方法返回表示许可证标识符的字符串值。
   * 通过调用`DocumentSecurityServiceClient`对象的`unrevokeLicense`方法并传递指定已撤销PDF文档的许可证标识符值的字符串值（传递`DocumentSecurityServiceClient`对象的`getLicenseId`方法的返回值），恢复对已撤销PDF文档的访问。

**代码示例**

有关使用文档安全服务的代码示例，请参阅以下快速开始:

* “快速开始(MTOM):使用Web服务API恢复对已吊销文档的访问权”
* “快速开始(SwaRef):使用Web服务API恢复对已吊销文档的访问权”

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 检查受策略保护的PDF文档{#inspecting-policy-protected-pdf-documents}

您可以使用文档安全服务API（Java和Web服务）检查受策略保护的PDF文档。 检查受策略保护的PDF文档会返回有关受策略保护的PDF文档的信息。 例如，您可以确定用于保护文档的策略以及保护文档的日期。

如果您的任务版本是8.x或更早版本，则无法执行此LiveCycle。 在AEM Forms增加了对受策略保护的文档的检查支持。 如果尝试使用LiveCycle8.x（或更低版本）检查受策略保护的文档，将引发异常。

>[!NOTE]
>
>有关文档安全服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-7}的摘要

要检查受策略保护的PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建文档安全客户端API对象。
1. 检索受策略保护的文档进行检查。
1. 获取有关受策略保护的文档的信息。

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建文档安全客户端API对象**

在以编程方式执行文档安全服务操作之前，请创建文档安全服务客户端对象。 如果您使用Java API，请创建`RightsManagementClient`对象。 如果您使用文档安全Web服务API，请创建`RightsManagementServiceService`对象。

**检索受策略保护的文档以进行检查**

要检查受策略保护的文档，请检索它。 如果尝试检查未通过策略保护或被吊销的文档，将引发异常。

**Inspect文档**

检索受策略保护的文档后，可以检查它。

**获取有关受策略保护的文档的信息**

检查受策略保护的PDF文档后，可以获取其相关信息。 例如，您可以确定用于保护文档的策略。

如果使用属于“我的策略”的策略保护文档，然后调用`RMInspectResult.getPolicysetName`或`RMInspectResult.getPolicysetId`，则返回null。

如果文档是使用包含在策略集（非“我的策略”）中的策略进行保护的，则`RMInspectResult.getPolicysetName`和`RMInspectResult.getPolicysetId`将返回有效的字符串。

**另请参阅**

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Inspect策略保护的PDF文档（使用Java API {#inspect-policy-protected-pdf-documents-using-the-java-api}）

Inspect使用文档安全服务API(Java)创建受策略保护的PDF文档:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-rightsmanagement-client.jar。 有关这些文件的位置的信息，请参见[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

1. 创建文档安全客户端API对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。 （请参阅[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。）
   * 使用`RightsManagementClient`对象的构造函数并传递`ServiceClientFactory`对象，创建&lt;a0/>对象。

1. 检索受策略保护的文档进行检查。

   * 使用`java.io.FileInputStream`对象的构造函数创建一个&lt;a0/>对象，它表示受策略保护的PDF文档。 传递一个指定PDF文档位置的字符串值。
   * 使用`com.adobe.idp.Document`对象的构造函数并传递`java.io.FileInputStream`对象，创建&lt;a0/>对象。

1. Inspect文档。

   * 通过调用`RightsManagementClient`对象的`getDocumentManager`方法创建`DocumentManager`对象。
   * Inspect通过调用`LicenseManager`对象的`inspectDocument`方法来设置受策略保护的文档。 传递包含受策略保护的PDF文档的`com.adobe.idp.Document`对象。 此方法返回一个`RMInspectResult`对象，其中包含有关受策略保护的文档的信息。

1. 获取有关受策略保护的文档的信息。

   要获取有关受策略保护的文档的信息，请调用属于`RMInspectResult`对象的相应方法。 例如，要检索策略名称，请调用`RMInspectResult`对象的`getPolicyName`方法。

**代码示例**

有关使用文档安全服务的代码示例，请参阅以下快速开始:

* &quot;快速开始（SOAP模式）:使用Java API检查受策略保护的PDF文档&quot;

### Inspect策略保护的PDF文档（使用Web服务API {#inspect-policy-protected-pdf-documents-using-the-web-service-api}）

Inspect使用文档安全服务API（web服务）创建受策略保护的PDF文档:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建文档安全客户端API对象。

   * 使用其默认构造函数创建`RightsManagementServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`RightsManagementServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 您无需使用`lc_version`属性。 此属性在您创建服务引用时使用。)
   * 通过获取`RightsManagementServiceClient.Endpoint.Binding`字段的值创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段`RightsManagementServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`RightsManagementServiceClient.ClientCredentials.UserName.Password`分配相应的口令值。
      * 将常量值`HttpClientCredentialType.Basic`指定到字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`指定到字段`BasicHttpBindingSecurity.Security.Mode`。


1. 检索受策略保护的文档进行检查。

   * 使用`BLOB`对象的构造函数创建&lt;a0/>对象。 `BLOB`对象用于存储要检查的PDF文档。
   * 通过调用其构造函数创建`System.IO.FileStream`对象。 传递一个字符串值，它表示PDF文档的文件位置以及在中打开文件的模式。
   * 创建存储`System.IO.FileStream`对象内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性，可以确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，用流数据填充字节数组。 传递要读取的字节数组、开始位置和流长度。
   * 通过为`MTOM`字段指定字节数组的内容，填充`BLOB`对象。

1. Inspect文档。

   Inspect通过调用`RightsManagementServiceClient`对象的`inspectDocument`方法来设置受策略保护的文档。 传递包含受策略保护的PDF文档的`BLOB`对象。 此方法返回一个`RMInspectResult`对象，其中包含有关受策略保护的文档的信息。

1. 获取有关受策略保护的文档的信息。

   要获取有关受策略保护的文档的信息，请获取属于`RMInspectResult`对象的相应字段的值。 例如，要检索策略名称，请获取`RMInspectResult`对象的`policyName`字段的值。

**代码示例**

有关使用文档安全服务的代码示例，请参阅以下快速开始:

* “快速开始(MTOM):使用Web服务API检查受策略保护的PDF文档&quot;
* “快速开始(SwaRef):使用Web服务API检查受策略保护的PDF文档&quot;

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 创建水印{#creating-watermarks}

水印通过唯一识别文档并控制版权侵权来帮助确保文档的安全。 例如，您可以创建水印并将其放置在文档的所有页面上，该水印将声明机密性。 创建水印后，您可以将其作为策略的一部分包含。 也就是说，您可以使用新创建的水印设置策略的水印属性。 在将包含水印的策略应用到文档后，该水印会显示在受策略保护的文档中。

>[!NOTE]
>
>只有具有文档安全管理权限的用户才能创建水印。 即，在定义创建文档安全服务客户端对象所需的连接设置时，必须指定此类用户。

>[!NOTE]
>
>有关文档安全服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-8}的摘要

要创建水印，请执行以下步骤：

1. 包括项目文件。
1. 创建文档安全客户端API对象。
1. 设置水印属性。
1. 向文档安全服务注册水印。

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建文档安全客户端API对象**

在以编程方式执行文档安全服务操作之前，必须创建文档安全服务客户端对象。 如果您使用Java API，请创建`RightsManagementClient`对象。 如果您使用文档安全Web服务API，请创建`RightsManagementServiceService`对象。

**设置水印属性**

要创建新水印，必须设置水印属性。 必须始终定义名称属性。 除了name属性之外，您还必须至少设置以下属性之一：

* 自定义文本
* 包含日期
* 包含的用户ID
* 包含的用户名

下表列表了使用Web服务创建水印时所需的键和值对。

<table>
 <thead>
  <tr>
   <th><p>密钥名称</p></th>
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
   <td><p>指定打开文档的用户的标识是否是水印的一部分。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CURRENTDATE_ENABLED</code></p></td>
   <td><p>指定当前日期是否是水印的一部分。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code></p></td>
   <td><p>如果此值为true，则必须使用<code>WaterBackCmd:SRCTEXT</code>指定自定义文本的值。</p></td>
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
   <td><p>如果指定了此值，则<code>WaterBackCmd:IS_SIZE_ENABLED</code>必须存在，且该值必须为true。 如果未指定此属性，则默认行为适合页面。</p></td>
   <td><p>大于0.0且小于或等于1.0的值。</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:HORIZ_ALIGN</code></p></td>
   <td><p>指定水印的水平对齐方式。 默认值为中心。</p></td>
   <td><p>左、中或右</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:VERT_ALIGN</code></p></td>
   <td><p>指定水印的垂直对齐方式。 默认值为中心。</p></td>
   <td><p>顶部、中心或底部</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USE_BACKGROUND</code></p></td>
   <td><p>指定水印是否为背景。 默认值为false。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_SIZE_ENABLED</code></p></td>
   <td><p>如果指定了自定义比例，则为True。 如果此值为true，则还必须指定SCALE。 如果此值为false，则默认值将适合页面大小。</p></td>
   <td><p>True或False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SRCTEXT</code></p></td>
   <td><p>指定水印的自定义文本。 如果此值存在，则<code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code>也必须存在并设置为true。</p></td>
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

必须先在文档安全服务中注册新水印，然后才能使用。 注册水印后，您可以在策略中使用它。

**另请参阅**

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[将策略应用于PDF文档](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### 使用Java API {#create-watermarks-using-the-java-api}创建水印

使用文档安全API(Java)创建水印：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如`adobe-rightsmanagement-client.jar`。

1. 创建文档安全客户端API对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`RightsManagementClient`对象的构造函数并传递`ServiceClientFactory`对象，创建&lt;a0/>对象。

1. 设置水印属性

   * 通过调用`InfomodelObjectFactory`对象的静态`createWatermark`方法创建`Watermark`对象。 此方法返回`Watermark`对象。
   * 通过调用`Watermark`对象的`setName`方法并传递指定策略名称的字符串值，设置水印的name属性。
   * 通过调用`Watermark`对象的`setBackground`方法并传递`true`来设置水印的后台属性。 通过设置此属性，水印会显示在文档的背景中。
   * 通过调用`Watermark`对象的`setCustomText`方法并传递一个表示水印文本的字符串值，设置水印的自定义文本属性。
   * 通过调用`Watermark`对象的`setOpacity`方法并传递指定不透明度级别的整数值，设置水印的不透明度属性。 值100表示水印完全不透明，值0表示水印完全透明。

1. 注册水印。

   * 通过调用`RightsManagementClient`对象的`getWatermarkManager`方法创建`WatermarkManager`对象。 此方法返回`WatermarkManager`对象。
   * 通过调用`WatermarkManager`对象的`registerWatermark`方法并传递表示要注册的水印的`Watermark`对象来注册水印。 此方法返回一个表示水印标识值的字符串值。

**代码示例**

有关使用文档安全服务的代码示例，请参阅以下快速开始:

* &quot;快速开始（SOAP模式）:使用Java API创建水印”

### 使用Web服务API {#create-watermarks-using-the-web-service-api}创建水印

使用文档安全API（Web服务）创建水印：

1. 创建文档安全客户端API对象。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建文档安全客户端API对象。

   * 使用其默认构造函数创建`RightsManagementServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`RightsManagementServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 您无需使用`lc_version`属性。 此属性在您创建服务引用时使用。)
   * 通过获取`RightsManagementServiceClient.Endpoint.Binding`字段的值创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段`RightsManagementServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`RightsManagementServiceClient.ClientCredentials.UserName.Password`分配相应的口令值。
      * 将常量值`HttpClientCredentialType.Basic`指定到字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`指定到字段`BasicHttpBindingSecurity.Security.Mode`。


1. 设置水印属性。

   * 通过调用`WatermarkSpec`构造函数创建`WatermarkSpec`对象。
   * 通过为`WatermarkSpec`对象的`name`数据成员分配字符串值来设置水印的名称。
   * 通过为`WatermarkSpec`对象的`id`数据成员分配字符串值来设置水印的`id`属性。
   * 对于要设置的每个水印属性，请创建单独的`MyMapOf_xsd_string_To_xsd_anyType_Item`对象。
   * 通过为`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`key`数据成员（例如`WaterBackCmd:OPACITY)`）分配值来设置键值。
   * 通过为`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`value`数据成员（例如`.25`）分配值来设置值。
   * 创建`MyArrayOf_xsd_anyType`对象。 对于每个`MyMapOf_xsd_string_To_xsd_anyType_Item`对象，调用`MyArrayOf_xsd_anyType`对象的`Add`方法。 传递`MyMapOf_xsd_string_To_xsd_anyType_Item`对象。
   * 将`MyArrayOf_xsd_anyType`对象指定给`WatermarkSpec`对象的`values`数据成员。

1. 注册水印。

   通过调用`RightsManagementServiceClient`对象的`registerWatermark`方法并传递表示要注册的水印的`WatermarkSpec`对象来注册水印。

**代码示例**

有关使用文档安全服务的代码示例，请参阅以下快速开始:

* “快速开始(MTOM):使用Web服务API创建水印”
* “快速开始(SwaRef):使用Web服务API创建水印”

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 修改水印{#modifying-watermarks}

您可以使用文档安全Java API或Web服务API修改现有水印。 要更改现有水印，请检索它，修改它的属性，然后在服务器上更新它。 例如，假定您检索水印并修改其不透明度属性。 在更改生效之前，您必须更新水印。

当您修改水印时，更改会影响应用了水印的未来文档。 即，包含水印的现有PDF文档不受影响。

>[!NOTE]
>
>只有具有文档安全管理权限的用户才能修改水印。 即，在定义创建文档安全服务客户端对象所需的连接设置时，必须指定此类用户。

>[!NOTE]
>
>有关文档安全服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-9}的摘要

要修改水印，请执行以下步骤：

1. 包括项目文件。
1. 创建文档安全客户端API对象。
1. 检索要修改的水印。
1. 设置水印属性。
1. 更新水印。

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建文档安全客户端API对象**

在以编程方式执行文档安全服务操作之前，必须创建文档安全服务客户端对象。 如果您使用Java API，请创建`DocumentSecurityClient`对象。 如果您使用文档安全Web服务API，请创建`DocumentSecurityServiceService`对象。

**检索要修改的水印**

要修改水印，必须检索现有水印。 您可以通过指定水印名称或指定水印的标识符值来检索水印。

**设置水印属性**

要修改现有水印，请更改一个或多个水印属性的值。 当使用Web服务以编程方式更新水印时，必须设置最初设置的所有属性，即使该值没有更改也是如此。 例如，假定设置了以下水印属性：`WaterBackCmd:IS_USERID_ENABLED`、`WaterBackCmd:IS_CUSTOMTEXT_ENABLED`、`WaterBackCmd:OPACITY`和`WaterBackCmd:SRCTEXT`。 尽管您唯一要修改的属性是`WaterBackCmd:OPACITY`，但必须设置其他值。

>[!NOTE]
>
>使用Java API修改水印时，无需指定所有属性。 设置要修改的水印属性。

>[!NOTE]
>
>有关水印属性名称的信息，请参阅[创建水印](protecting-documents-policies.md#creating-watermarks)。

**更新水印**

修改水印属性后，必须更新水印。

**另请参阅**

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[创建水印](protecting-documents-policies.md#creating-watermarks)

### 使用Java API {#modify-watermarks-using-the-java-api}修改水印

使用文档安全API(Java)修改水印：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-rightsmanagement-client.jar。

1. 创建文档安全客户端API对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`DocumentSecurityClient`对象的构造函数并传递`ServiceClientFactory`对象，创建&lt;a0/>对象。

1. 检索要修改的水印。

   通过调用`DocumentSecurityClient`对象的`getWatermarkManager`方法创建`WatermarkManager`对象，并传递一个指定水印名称的字符串值。 此方法返回一个`Watermark`对象，它表示要修改的水印。

1. 设置水印属性。

   通过调用`Watermark`对象的`setOpacity`方法并传递指定不透明度级别的整数值，设置水印的不透明度属性。 值100表示水印完全不透明，值0表示水印完全透明。

   >[!NOTE]
   >
   >此示例仅修改不透明度属性。

1. 更新水印。

   * 通过调用`WatermarkManager`对象的`updateWatermark`方法更新水印，并传递其属性已修改的`Watermark`对象。

**代码示例**

有关使用文档安全服务的代码示例，请参阅快速开始（SOAP模式）:使用Java API部分修改水印。

### 使用Web服务API {#modify-watermarks-using-the-web-service-api}修改水印

使用文档安全API（Web服务）修改水印：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建文档安全客户端API对象。

   * 使用其默认构造函数创建`DocumentSecurityServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`RightsManagementServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/DocumentSecurityService?WSDL`）。 您无需使用`lc_version`属性。 此属性在您创建服务引用时使用。)
   * 通过获取`DocumentSecurityServiceClient.Endpoint.Binding`字段的值创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段`DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`DocumentSecurityServiceClient.ClientCredentials.UserName.Password`分配相应的口令值。
      * 将常量值`HttpClientCredentialType.Basic`指定到字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`指定到字段`BasicHttpBindingSecurity.Security.Mode`。


1. 检索要修改的水印。

   通过调用`DocumentSecurityServiceClient`对象的`getWatermarkByName`方法检索要修改的水印。 传递指定水印名称的字符串值。 此方法返回一个`WatermarkSpec`对象，它表示要修改的水印。

1. 设置水印属性。

   * 对于要更新的每个水印属性，请创建单独的`MyMapOf_xsd_string_To_xsd_anyType_Item`对象。
   * 通过为`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`key`数据成员（例如`WaterBackCmd:OPACITY)`）分配值来设置键值。
   * 通过为`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`value`数据成员（例如`.50`）分配值来设置值。
   * 创建`MyArrayOf_xsd_anyType`对象。 对于每个`MyMapOf_xsd_string_To_xsd_anyType_Item`对象，调用`MyArrayOf_xsd_anyType`对象的`Add`方法。 传递`MyMapOf_xsd_string_To_xsd_anyType_Item`对象。
   * 将`MyArrayOf_xsd_anyType`对象指定给`WatermarkSpec`对象的`values`数据成员。

1. 更新水印。

   通过调用`DocumentSecurityServiceClient`对象的`updateWatermark`方法并传递表示要修改的水印的`WatermarkSpec`对象来更新水印。

**代码示例**

有关使用文档安全服务的代码示例，请参阅以下快速开始:

* “快速开始(MTOM):使用Web服务API修改水印»

## 搜索事件{#searching-for-events}

Rights Management服务在特定操作发生时跟踪这些操作，如将策略应用于文档、打开受策略保护的文档以及撤销对文档的访问。 必须为事件服务启用Rights Management审核，否则不跟踪事件。

事件属于以下类别之一：

* 管理员事件是与管理员相关的操作，如创建新的管理员帐户。
* 文档事件是与文档相关的操作，如关闭受策略保护的文档。
* 策略事件是与策略相关的操作，如创建新策略。
* 服务事件是与Rights Management服务相关的操作，如与用户目录同步。

您可以使用Rights ManagementJava API或Web服务API搜索指定事件。 通过搜索事件，您可以执行任务，如创建某些事件的日志文件。

>[!NOTE]
>
>有关Rights Management服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-10}的摘要

要搜索Rights Management事件，请执行以下步骤：

1. 包括项目文件。
1. 创建Rights Management客户端API对象。
1. 指定要搜索的事件。
1. 搜索事件。

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建Rights Management客户端API对象**

在以编程方式执行Rights Management服务操作之前，必须创建Rights Management服务客户端对象。 如果您使用Java API，请创建`DocumentSecurityClient`对象。 如果您使用Rights ManagementWeb服务API，请创建`DocumentSecurityServiceService`对象。

**指定要搜索的事件**

必须指定要搜索的事件。 例如，您可以搜索策略创建事件，创建新策略时即发生此情况。

**搜索事件**

在指定要搜索的事件后，您可以使用Rights ManagementJava API或Rights ManagementWeb服务API搜索事件。

**另请参阅**

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#search-for-events-using-the-java-api}搜索事件

使用事件API(Java)搜索Rights Management:

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-rightsmanagement-client.jar。

1. 创建Rights Management客户端API对象

   使用`DocumentSecurityClient`对象的构造函数创建一个`ServiceClientFactory`对象，并传递一个包含连接属性的&lt;a1/>对象。

1. 指定要搜索的事件

   * 通过调用`DocumentSecurityClient`对象的`getEventManager`方法创建`EventManager`对象。 此方法返回一个`EventManager`对象。
   * 通过调用其构造函数创建`EventSearchFilter`对象。
   * 通过调用`EventSearchFilter`对象的`setEventCode`方法并传递属于`EventManager`类的静态数据成员(表示要搜索的事件)，指定要搜索的事件。 例如，要搜索策略创建事件，请传递`EventManager.POLICY_CREATE_EVENT`。

   >[!NOTE]
   >
   >可以通过调用`EventSearchFilter`对象方法来定义其他搜索条件。 例如，调用`setUserName`方法以指定与事件关联的用户。

1. 搜索事件

   通过调用`EventManager`对象的`searchForEvents`方法并传递定义事件搜索条件的`EventSearchFilter`对象，搜索事件。 此方法返回`Event`对象的数组。

**代码示例**

有关使用Rights Management服务的代码示例，请参阅以下快速开始:

* “快速开始(SOAP):使用Java API搜索事件”

### 使用Web服务API {#search-for-events-using-the-web-service-api}搜索事件

使用事件API（Web服务）搜索Rights Management:

1. 包括项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建Rights Management客户端API对象

   * 使用其默认构造函数创建`DocumentSecurityServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`DocumentSecurityServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 您无需使用`lc_version`属性。 此属性在您创建服务引用时使用。)
   * 通过获取`DocumentSecurityServiceClient.Endpoint.Binding`字段的值创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段`DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`DocumentSecurityServiceClient.ClientCredentials.UserName.Password`分配相应的口令值。
      * 将常量值`HttpClientCredentialType.Basic`指定到字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`指定到字段`BasicHttpBindingSecurity.Security.Mode`。


1. 指定要搜索的事件

   * 使用`EventSpec`对象的构造函数创建&lt;a0/>对象。
   * 通过将`EventSpec`对象的`firstTime.date`数据成员设置为`DataTime`实例，以指定发生事件的时间段的开始，该实例表示发生事件时的日期范围的开始。
   * 将值`true`指定给`EventSpec`对象的`firstTime.dateSpecified`数据成员。
   * 通过使用`DataTime`实例设置`EventSpec`对象的`lastTime.date`数据成员，指定发生事件的时间段的结束，该实例表示发生事件时的日期范围的结束。
   * 将值`true`指定给`EventSpec`对象的`lastTime.dateSpecified`数据成员。
   * 通过为`EventSpec`对象的`eventCode`数据成员分配字符串值来设置要搜索的事件。 下表列表了可分配给此属性的数值：

   <table>
    <thead>
    <tr>
    <th><p>事件类型</p></th>
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

1. 搜索事件

   通过调用`DocumentSecurityServiceClient`对象的`searchForEvents`方法并传递表示要搜索的事件和结果最大数的`EventSpec`对象，搜索事件。 此方法返回`MyArrayOf_xsd_anyType`集合，其中每个元素都是`AuditSpec`实例。 使用`AuditSpec`实例，您可以获取有关事件的信息，如发生时间。 `AuditSpec`实例包含指定此信息的`timestamp`数据成员。

**代码示例**

有关使用Rights Management服务的代码示例，请参阅以下快速开始:

* “快速开始(MTOM):使用Web服务API搜索事件&quot;
* “快速开始(SwaRef):使用Web服务API搜索事件&quot;

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 将策略应用于Word文档{#applying-policies-to-word-documents}

除PDF文档外，权限管理服务还支持其他文档格式，如Microsoft Word文档（DOC文件）和其他Microsoft office文件格式。 例如，您可以将策略应用于Word文档以保护它。 通过将策略应用于Word文档，可以限制对文档的访问。 如果文档已使用策略保护，则不能对文档应用策略。

在分发受策略保护的Word文档后，可以监视其使用情况。 即，您可以看到文档的使用方式以及使用者。 例如，您可以查找某人何时打开文档。

>[!NOTE]
>
>有关文档安全服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-11}的摘要

要将策略应用于Word文档，请执行以下步骤：

1. 包括项目文件。
1. 创建文档安全客户端API对象。
1. 检索应用策略的Word文档。
1. 将现有策略应用于Word文档。
1. 保存受策略保护的Word文档。

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建文档安全客户端API对象**

在以编程方式执行文档安全服务操作之前，必须创建文档安全服务客户端对象。

**检索Word文档**

必须检索Word文档才能应用策略。 将策略应用于Word文档后，用户在使用文档时受到限制。 例如，如果策略未启用脱机时文档的打开，则用户必须联机才能打开文档。

**将现有策略应用于Word文档**

要将策略应用于Word文档，必须引用现有策略并指定策略所属的策略集。 设置连接属性的用户必须有权访问指定的策略。 否则，会出现异常。

**保存Word文档**

在文档安全服务将策略应用于Word文档后，可以将受策略保护的Word文档另存为DOC文件。

**另请参阅**

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[撤销对文档的访问](protecting-documents-policies.md#revoking-access-to-documents)

### 使用Java API {#apply-a-policy-to-a-word-document-using-the-java-api}将策略应用于Word文档

使用文档安全API(Java)将策略应用于Word文档:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-rightsmanagement-client.jar。

1. 创建文档安全客户端API对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`DocumentSecurityClient`对象的构造函数并传递`ServiceClientFactory`对象，创建&lt;a0/>对象。

1. 检索Word文档。

   * 通过使用Word文档的构造函数并传递一个指定Word文档位置的字符串值，创建一个表示Word的`java.io.FileInputStream`对象。
   * 使用`com.adobe.idp.Document`对象的构造函数并传递`java.io.FileInputStream`对象，创建&lt;a0/>对象。

1. 将现有策略应用于Word文档。

   * 通过调用`DocumentSecurityClient`对象的`getDocumentManager`方法创建`DocumentManager`对象。
   * 通过调用`DocumentManager`对象的`protectDocument`方法并传递以下值，将策略应用于Word文档:

      * `com.adobe.idp.Document`对象，其中包含应用策略的Word文档。
      * 一个字符串值，它指定文档的名称。
      * 一个字符串值，它指定策略所属的策略集的名称。 可以指定一个`null`值，该值会导致使用`MyPolicies`策略集。
      * 指定策略名称的字符串值。
      * 一个字符串值，它表示作为文档发布者的用户的用户管理器域的名称。 此参数值是可选的，可以为null（如果此参数为null，则下一个参数值必须为null）。
      * 一个字符串值，它表示作为文档发布者的用户管理器用户的规范名称。 此参数值是可选的，可以是`null`（如果此参数为`null`，则前一个参数值必须为`null`）。
      * 一个`com.adobe.livecycle.rightsmanagement.Locale`，它表示用于选择MS Office模板的区域设置。 此参数值是可选的，您可以指定`null`。

      `protectDocument`方法返回一个`RMSecureDocumentResult`对象，该对象包含受策略保护的Word文档。


1. 保存Word文档。

   * 调用`RMSecureDocumentResult`对象的`getProtectedDoc`方法以获取受策略保护的Word文档。 此方法返回`com.adobe.idp.Document`对象。
   * 创建`java.io.File`对象，并确保文件扩展名为DOC。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法，将`Document`对象的内容复制到文件（确保使用`getProtectedDoc`方法返回的`Document`对象）。

**代码示例**

有关使用文档安全服务的代码示例，请参阅以下快速开始:

* &quot;快速开始（SOAP模式）:使用Java API将策略应用于Word文档”

### 使用Web服务API {#apply-a-policy-to-a-word-document-using-the-web-service-api}将策略应用于Word文档

使用文档安全API（Web服务）将策略应用于Word文档:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/DocumentSecurityService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建文档安全客户端API对象。

   * 使用其默认构造函数创建`DocumentSecurityServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`DocumentSecurityServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/DocumentSecurityService?WSDL`）。 您无需使用`lc_version`属性。 此属性在您创建服务引用时使用。)
   * 通过获取`DocumentSecurityServiceClient.Endpoint.Binding`字段的值创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段`DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`DocumentSecurityServiceClient.ClientCredentials.UserName.Password`分配相应的口令值。
      * 将常量值`HttpClientCredentialType.Basic`指定到字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`指定到字段`BasicHttpBindingSecurity.Security.Mode`。


1. 检索Word文档。

   * 使用`BLOB`对象的构造函数创建&lt;a0/>对象。 `BLOB`对象用于存储应用策略的Word文档。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示Word文档的文件位置以及打开文件的模式。
   * 创建存储`System.IO.FileStream`对象内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性，确定字节数组大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，用流数据填充字节数组。 传递要读取的字节数组、开始位置和流长度。
   * 通过为`MTOM`字段指定字节数组的内容，填充`BLOB`对象。

1. 将现有策略应用于Word文档。

   通过调用`DocumentSecurityServiceClient`对象的`protectDocument`方法并传递以下值，将策略应用于Word文档:

   * `BLOB`对象，其中包含应用策略的Word文档。
   * 一个字符串值，它指定文档的名称。
   * 一个字符串值，它指定策略所属的策略集的名称。 可以指定一个`null`值，该值会导致使用`MyPolicies`策略集。
   * 指定策略名称的字符串值。
   * 一个字符串值，它表示作为文档发布者的用户的用户管理器域的名称。 此参数值是可选的，可以为null（如果此参数为null，则下一个参数值必须为`null`）。
   * 一个字符串值，它表示作为文档发布者的用户管理器用户的规范名称。 此参数值是可选的，可以为null（如果此参数为null，则上一个参数值必须为`null`）。
   * 一个`RMLocale`值，它指定区域设置值（例如`RMLocale.en`）。
   * 用于存储策略标识符值的字符串输出参数。
   * 用于存储受策略保护的标识符值的字符串输出参数。
   * 用于存储mime类型的字符串输出参数（例如，`application/doc`）。

   `protectDocument`方法返回一个`BLOB`对象，该对象包含受策略保护的Word文档。

1. 保存Word文档。

   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示受策略保护的Word文档的文件位置。
   * 创建一个字节数组，用于存储`protectDocument`方法返回的`BLOB`对象的数据内容。 通过获取`BLOB`对象的`MTOM`数据成员的值，填充字节数组。
   * 通过调用`System.IO.BinaryWriter`对象的构造函数并传递`System.IO.FileStream`对象，创建&lt;a0/>对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入Word文件。

**代码示例**

有关使用文档安全服务的代码示例，请参阅以下快速开始:

* “快速开始(MTOM):使用Web服务API将策略应用于Word文档”

## 从Word文档{#removing-policies-from-word-documents}删除策略

您可以从受策略保护的Word文档中删除策略，以便从文档中删除安全性。 也就是说，如果您不再希望文档受策略保护。 如果要使用较新的策略更新受策略保护的Word文档，则切换策略比删除策略和添加更新的策略更有效。

>[!NOTE]
>
>有关文档安全服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-12}的摘要

要从受策略保护的Word文档中删除策略，请执行以下步骤：

1. 包括项目文件
1. 创建文档安全客户端API对象。
1. 检索受策略保护的Word文档。
1. 从Word文档中删除策略。
1. 保存不安全的Word文档

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建文档安全客户端API对象**

在以编程方式执行文档安全服务操作之前，请创建文档安全服务客户端对象。

**检索受策略保护的Word文档**

必须检索受策略保护的Word文档才能删除策略。 如果尝试从未受策略保护的Word文档中删除策略，将引起异常。

**从Word文档中删除策略**

可以从受策略保护的Word文档中删除策略，前提是在连接设置中指定了管理员。 否则，用于保护文档的策略必须包含`SWITCH_POLICY`权限才能从Word文档中删除策略。 此外，在AEM Forms连接设置中指定的用户也必须具有该权限。 否则，将引发异常。

**保存不安全的Word文档**

在文档安全服务从Word文档中删除策略后，可以将不安全的Word文档另存为DOC文件。

**另请参阅**

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[将策略应用于Word文档](protecting-documents-policies.md#applying-policies-to-word-documents)

### 使用Java API {#remove-a-policy-from-a-word-document-using-the-java-api}从Word文档中删除策略

使用文档安全API(Java)从受策略保护的Word文档中删除策略：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-rightsmanagement-client.jar。

1. 创建文档安全客户端API对象

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`RightsManagementClient`对象的构造函数并传递`ServiceClientFactory`对象，创建&lt;a0/>对象。

1. 检索受策略保护的Word文档

   * 创建一个`java.io.FileInputStream`对象，它使用其构造函数并传递一个指定Word文档位置的字符串值来表示受策略保护的Word文档。
   * 使用`com.adobe.idp.Document`对象的构造函数并传递`java.io.FileInputStream`对象，创建&lt;a0/>对象。

1. 从Word文档中删除策略

   * 通过调用`RightsManagementClient`对象的`getDocumentManager`方法创建`DocumentManager`对象。
   * 通过调用`DocumentManager`对象的`removeSecurity`方法并传递包含受策略保护的Word文档的`com.adobe.idp.Document`对象，从Word文档中删除策略。 此方法返回一个`com.adobe.idp.Document`对象，它包含一个不安全的Word文档。

1. 保存不安全的Word文档

   * 创建`java.io.File`对象，并确保文件扩展名为DOC。
   * 调用`Document`对象的`copyToFile`方法，将`Document`对象的内容复制到文件（确保使用`removeSecurity`方法返回的`Document`对象）。

**代码示例**

有关使用文档安全服务的代码示例，请参阅以下快速开始:

* &quot;快速开始（SOAP模式）:使用Java API从Word文档删除策略”

### 使用Web服务API {#remove-a-policy-from-a-word-document-using-the-web-service-api}从Word文档中删除策略

使用文档安全API（Web服务）从受策略保护的Word文档中删除策略：

1. 包括项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建文档安全客户端API对象

   * 使用其默认构造函数创建`RightsManagementServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`RightsManagementServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 您无需使用`lc_version`属性。 此属性在您创建服务引用时使用。)
   * 通过获取`RightsManagementServiceClient.Endpoint.Binding`字段的值创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段`RightsManagementServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`RightsManagementServiceClient.ClientCredentials.UserName.Password`分配相应的口令值。
      * 将常量值`HttpClientCredentialType.Basic`指定到字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`指定到字段`BasicHttpBindingSecurity.Security.Mode`。


1. 检索受策略保护的Word文档

   * 使用`BLOB`对象的构造函数创建&lt;a0/>对象。 `BLOB`对象用于存储从中删除策略的受策略保护的Word文档。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示Word文档的文件位置以及打开文件的模式。
   * 创建存储`System.IO.FileStream`对象内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性，可以确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过为`MTOM`字段指定字节数组的内容，填充`BLOB`对象。

1. 从Word文档中删除策略

   通过调用`RightsManagementServiceClient`对象的`removePolicySecurity`方法并传递包含受策略保护的Word文档的`BLOB`对象，从Word文档中删除策略。 此方法返回一个`BLOB`对象，它包含一个不安全的Word文档。

1. 保存不安全的Word文档

   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值来创建一个&lt;a0/>对象，该字符串值表示不安全的Word文档的文件位置。
   * 创建一个字节数组，用于存储`removePolicySecurity`方法返回的`BLOB`对象的数据内容。 通过获取`BLOB`对象的`MTOM`字段的值，填充字节数组。
   * 通过调用`System.IO.BinaryWriter`对象的构造函数并传递`System.IO.FileStream`对象，创建&lt;a0/>对象。

**代码示例**

有关使用文档安全服务的代码示例，请参阅以下快速开始:

* “快速开始(MTOM):使用Web服务API从Word文档删除策略”

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
