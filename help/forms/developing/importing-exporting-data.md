---
title: 导入和导出数据
seo-title: 导入和导出数据
description: 'null'
seo-description: 'null'
uuid: 94ccb6f2-6e5f-43ea-a954-9a4402871a17
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2e783745-c986-45ba-8e65-7437d114ca38
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2742'
ht-degree: 0%

---


# 导入和导出数据{#importing-and-exporting-data}

## 关于表单数据集成服务{#about-the-form-data-integration-service}

表单数据集成服务可以将数据导入PDF表单并从PDF表单导出数据。 导入和导出操作支持两种PDF forms:

* Acrobat表单(在Acrobat创建)是包含表单字段的PDF文档。
* AdobeXML表单（在设计器中创建）是符合XMLAdobeXMLForms体系结构(XFA)的PDF文档。

根据PDF表单的类型，表单数据可以以下列格式之一存在：

* XFDF文件，是Acrobat表单数据格式的XML版本。
* XDP文件，它是一个XML文件，包含表单字段定义。 它还可能包含表单字段数据和嵌入的PDF文件。 由设计人员生成的XDP文件只能在具有嵌入的基本64编码PDF文档时使用。

您可以使用表单任务集成服务完成这些操作：

* 将数据导入PDF forms。 有关信息，请参阅[导入表单数据](importing-exporting-data.md#importing-form-data)。
* 从PDF forms导出数据。 有关信息，请参阅[导出表单数据](importing-exporting-data.md#exporting-form-data)。

>[!NOTE]
>
>有关表单数据集成服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 导入表单数据{#importing-form-data}

您可以使用表单PDF forms集成服务将表单数据导入交互式数据。 交互式PDF表单是一个PDF文档，其中包含一个或多个字段，用于从用户收集信息或显示自定义信息。 表单数据集成服务不支持表单计算、验证或脚本。

要将数据导入到在Designer中创建的表单中，必须引用有效的XDP XML数据源。 请考虑以下抵押申请表示例。

![ie_ie_loanformdata](assets/ie_ie_loanformdata.png)

要将数据值导入此表单，您必须具有与表单对应的有效XDP XML数据源。 不能使用任意XML数据源使用表单数据集成服务将数据导入表单。 任意XML数据源与XDP XML数据源之间的区别在于，XDP数据源符合XMLForms体系结构(XFA)。 以下XML表示与示例按揭贷款应用程序表单对应的XDP XML数据源。

```xml
 <?xml version="1.0" encoding="UTF-8" ?>
 - <xfa:datasets xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
 - <xfa:data>
 - <data>
     - <Layer>
         <closeDate>1/26/2007</closeDate>
         <lastName>Johnson</lastName>
         <firstName>Jerry</firstName>
         <mailingAddress>JJohnson@NoMailServer.com</mailingAddress>
         <city>New York</city>
         <zipCode>00501</zipCode>
         <state>NY</state>
         <dateBirth>26/08/1973</dateBirth>
         <middleInitials>D</middleInitials>
         <socialSecurityNumber>(555) 555-5555</socialSecurityNumber>
         <phoneNumber>5555550000</phoneNumber>
     </Layer>
     - <Mortgage>
         <mortgageAmount>295000.00</mortgageAmount>
         <monthlyMortgagePayment>1724.54</monthlyMortgagePayment>
         <purchasePrice>300000</purchasePrice>
         <downPayment>5000</downPayment>
         <term>25</term>
         <interestRate>5.00</interestRate>
     </Mortgage>
 </data>
 </xfa:data>
 </xfa:datasets>
```

>[!NOTE]
>
>有关表单数据集成服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary-of-steps}的摘要

要将表单数据导入PDF表单，请执行以下步骤：

1. 包括项目文件。
1. 创建表单数据集成服务客户端。
1. 引用PDF表单。
1. 引用XML数据源。
1. 将数据导入PDF表单。
1. 将PDF表单另存为PDF文件。

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时是必需的)
* jbossall-client.jar(在JBoss上部署AEM Forms时是必需的)

有关这些JAR文件的位置的信息，请参阅[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建表单数据集成服务客户端**

在以编程方式将数据导入PDF表单客户端API之前，必须创建数据集成服务客户端。 在创建服务客户端时，您定义调用服务所需的连接设置。 有关信息，请参阅[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

**引用PDF表单**

要将数据导入PDF表单，您必须引用在设计器中创建的XML表单或在Acrobat创建的Acrobat表单。

**引用XML数据源**

要导入表单数据，必须引用有效的数据源。 要将数据导入在Designer中创建的XFA XML表单，必须使用XDP XML数据源。 如果引用的是Acrobat表单，则必须使用XFDF数据源。 对于要将数据导入的每个字段，必须指定一个值。 如果XML数据源中的元素与表单中的字段不对应，则忽略该元素。

**将数据导入PDF表单**

引用PDF表单和有效的XML数据源后，可以将数据导入PDF表单。

**将PDF表单另存为PDF文件**

将数据导入表单后，可将表单另存为PDF文件。 保存为PDF文件后，用户可以在Adobe Reader或Acrobat打开表单，查看包含导入数据的表单。

**另请参阅**

[使用Java API导入表单数据](importing-exporting-data.md#import-form-data-using-the-java-api)

[使用Web服务API导入表单数据](importing-exporting-data.md#import-form-data-using-the-web-service-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[表单数据集成服务API快速开始](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[导出表单数据](importing-exporting-data.md#exporting-form-data)

### 使用Java API {#import-form-data-using-the-java-api}导入表单数据

使用表单数据集成API(Java)导入表单数据：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-formdataintegration-client.jar。

1. 创建表单数据集成服务客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`FormDataIntegrationClient`对象的构造函数并传递`ServiceClientFactory`对象，创建&lt;a0/>对象。

1. 引用PDF表单。

   * 使用`java.io.FileInputStream`对象的构造函数创建&lt;a0/>对象。 传递一个指定PDF表单位置的字符串值。
   * 使用`com.adobe.idp.Document`构造函数创建存储PDF表单的`com.adobe.idp.Document`对象。 将包含PDF表单的`java.io.FileInputStream`对象传递给构造函数。

1. 引用XML数据源。

   * 使用`java.io.FileInputStream`对象的构造函数创建一个&lt;a0/>对象，并传递一个字符串值，它指定要导入表单的XML文件的位置。
   * 使用`com.adobe.idp.Document`构造函数创建用于存储表单数据的`com.adobe.idp.Document`对象。 将包含表单数据的`java.io.FileInputStream`对象传递给构造函数。

1. 将数据导入PDF表单。

   通过调用`FormDataIntegrationClient`对象的`importData`方法并传递以下值，将数据导入PDF表单：

   * 存储PDF表单的`com.adobe.idp.Document`对象。
   * 存储表单数据的`com.adobe.idp.Document`对象。

   `importData`方法返回一个`com.adobe.idp.Document`对象，该对象存储包含XML数据源中数据的PDF表单。

1. 将PDF表单另存为PDF文件。

   * 创建一个`java.io.File`对象，并确保文件扩展名为“.PDF”。
   * 调用`Document`对象的`copyToFile`方法，将`Document`对象的内容复制到文件（确保使用`importData`方法返回的`Document`对象）。

**另请参阅**

[步骤摘要](importing-exporting-data.md#summary-of-steps)

[快速开始（SOAP模式）:使用Java API导入表单数据](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#import-form-data-using-the-web-service-api}导入表单数据

使用表单数据集成API（Web服务）导入表单数据：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建表单数据集成服务客户端。

   * 使用其默认构造函数创建`FormDataIntegrationClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`FormDataIntegrationClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`）。 您无需使用`lc_version`属性。 此属性在您创建服务引用时使用。 但是，指定`?blob=mtom`以使用MTOM。
   * 通过获取`FormDataIntegrationClient.Endpoint.Binding`字段的值创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段`FormDataIntegrationClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`FormDataIntegrationClient.ClientCredentials.UserName.Password`分配相应的口令值。
      * 将常量值`HttpClientCredentialType.Basic`指定到字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`指定到字段`BasicHttpBindingSecurity.Security.Mode`。

1. 引用PDF表单。

   * 使用`BLOB`对象的构造函数创建&lt;a0/>对象。 此`BLOB`对象用于存储PDF表单。
   * 通过调用其构造函数创建`System.IO.FileStream`对象。 传递一个字符串值，它指定PDF表单的位置以及打开文件的模式。
   * 创建存储`System.IO.FileStream`对象内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性，可以确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，用流数据填充字节数组。 传递要读取的字节数组、开始位置和流长度。
   * 通过为`MTOM`字段指定字节数组的内容，填充`BLOB`对象。

1. 引用XML数据源。

   * 使用`BLOB`对象的构造函数创建&lt;a0/>对象。 此`BLOB`对象用于存储导入到表单中的数据。
   * 通过调用其构造函数创建`System.IO.FileStream`对象。 传递一个字符串值，它指定包含要导入数据的XML文件的位置以及打开文件的模式。
   * 创建存储`System.IO.FileStream`对象内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性，可以确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，用流数据填充字节数组。 传递要读取的字节数组、开始位置和流长度。
   * 通过为`MTOM`字段指定字节数组的内容，填充`BLOB`对象。

1. 将数据导入PDF表单。

   通过调用`FormDataIntegrationClient`对象的`importData`方法并传递以下值，将数据导入PDF表单：

   * 存储PDF表单的`BLOB`对象。
   * 存储表单数据的`BLOB`对象。

   `importData`方法返回一个`BLOB`对象，该对象存储包含XML数据源中数据的PDF表单。

1. 将PDF表单另存为PDF文件。

   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个表示PDF文件的文件位置的字符串值，创建一个&lt;a0/>对象。
   * 创建一个字节数组，用于存储`importData`方法返回的`BLOB`对象的数据内容。 通过获取`BLOB`对象的`MTOM`字段的值，填充字节数组。
   * 通过调用`System.IO.BinaryWriter`对象的构造函数并传递`System.IO.FileStream`对象，创建&lt;a0/>对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

**另请参阅**

[步骤摘要](importing-exporting-data.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 导出表单数据{#exporting-form-data}

您可以使用表单数据集成服务从交互式PDF表单导出表单数据。 导出的数据格式取决于表单类型。 如果表单类型是在Acrobat创建的Acrobat表单，则导出的数据为XFDF。 如果表单类型是在Designer中创建的XML表单，则导出的数据为XDP。

>[!NOTE]
>
>有关表单数据集成服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-1}的摘要

要从PDF表单导出表单数据，请执行以下步骤：

1. 包括项目文件
1. 创建表单数据集成服务客户端。
1. 引用PDF表单。
1. 从PDF表单导出数据。
1. 将导出的数据另存为XML文件。

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时是必需的)
* jbossall-client.jar(在JBoss上部署AEM Forms时是必需的)

**创建表单数据集成服务客户端**

在以编程方式将数据导入PDF formClient API之前，必须创建数据集成服务客户端。 在创建服务客户端时，您定义调用服务所需的连接设置。 有关信息，[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

**引用PDF表单**

要从PDF表单导出数据，必须引用在设计人员或Acrobat中创建并包含表单数据的PDF表单。 如果尝试从空的PDF表单导出数据，您将得到一个空的XML模式。

**从PDF表单导出数据**

引用包含表单数据的PDF表单后，您可以从表单导出数据。 数据将在基于表单的XML模式中导出。

**将表单数据保存为XML文件**

导出表单数据后，可以将数据另存为XML文件。 保存为XML文件后，可以在XML查看器中打开XML文件以视图表单数据。

**另请参阅**

[使用Java API导出表单数据](importing-exporting-data.md#export-form-data-using-the-java-api)

[使用Web服务API导出表单数据](importing-exporting-data.md#export-form-data-using-the-web-service-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[表单数据集成服务API快速开始](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[导入表单数据](importing-exporting-data.md#importing-form-data)

### 使用Java API {#export-form-data-using-the-java-api}导出表单数据

使用表单数据集成API(Java)导出表单数据：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-formdataintegration-client.jar。

1. 创建表单数据集成服务客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`FormDataIntegrationClient`对象的构造函数并传递`ServiceClientFactory`对象，创建&lt;a0/>对象。

1. 引用PDF表单。

   * 使用`java.io.FileInputStream`对象的构造函数创建一个&lt;a0/>对象，并传递一个字符串值，它指定要导出数据的PDF表单的位置。
   * 使用`com.adobe.idp.Document`构造函数创建存储PDF表单的`com.adobe.idp.Document`对象。 将包含PDF表单的`java.io.FileInputStream`对象传递给构造函数。

1. 从PDF表单导出数据。

   通过调用`FormDataIntegrationClient`对象的`exportData`方法导出表单数据，并传递存储PDF表单的`com.adobe.idp.Document`对象。 此方法返回一个`com.adobe.idp.Document`对象，该对象将表单数据存储为XML模式。

1. 将PDF表单另存为PDF文件。

   * 创建一个`java.io.File`对象，并确保文件扩展名为XML。
   * 调用`Document`对象的`copyToFile`方法，将`Document`对象的内容复制到文件（确保使用`exportData`方法返回的`Document`对象）。

**另请参阅**

[步骤摘要](importing-exporting-data.md#summary-of-steps)

[快速开始（SOAP模式）:使用Java API导出表单数据](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#export-form-data-using-the-web-service-api}导出表单数据

使用表单数据集成API（Web服务）导出表单数据：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`。

   * 将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建表单数据集成服务客户端。

   * 使用其默认构造函数创建`FormDataIntegrationClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`FormDataIntegrationClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`）。 您无需使用`lc_version`属性。 此属性在您创建服务引用时使用。 但是，指定`?blob=mtom`以使用MTOM。
   * 通过获取`FormDataIntegrationClient.Endpoint.Binding`字段的值创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段`FormDataIntegrationClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`FormDataIntegrationClient.ClientCredentials.UserName.Password`分配相应的口令值。
      * 将常量值`HttpClientCredentialType.Basic`指定到字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`指定到字段`BasicHttpBindingSecurity.Security.Mode`。

1. 引用PDF表单。

   * 使用`BLOB`对象的构造函数创建&lt;a0/>对象。 此`BLOB`对象用于存储从中导出数据的PDF表单。
   * 通过调用其构造函数创建`System.IO.FileStream`对象。 传递一个字符串值，它指定PDF表单的位置以及打开文件的模式。
   * 创建存储`System.IO.FileStream`对象内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性，可以确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过为`MTOM`字段指定字节数组的内容，填充`BLOB`对象。

1. 从PDF表单导出数据。

   通过调用`FormDataIntegrationClient`对象的`exportData`方法将数据导入PDF表单，并传递存储PDF表单的`BLOB`对象。 此方法返回一个`BLOB`对象，该对象将表单数据存储为XML模式。

1. 将PDF表单另存为PDF文件。

   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个表示XML文件位置的字符串值，创建一个&lt;a0/>对象。
   * 创建一个字节数组，用于存储`exportData`方法返回的`BLOB`对象的数据内容。 通过获取`BLOB`对象的`MTOM`字段的值，填充字节数组。
   * 通过调用`System.IO.BinaryWriter`对象的构造函数并传递`System.IO.FileStream`对象，创建&lt;a0/>对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入XML文件。

**另请参阅**

[步骤摘要](importing-exporting-data.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
