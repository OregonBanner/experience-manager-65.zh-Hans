---
title: 汇编PDFPortfolio
seo-title: 汇编PDFPortfolio
description: 组合一个PDF包，组合多种文档的不同类型，包括word文件、图像文件和PDF文档。 您可以使用Java API和Web服务API组合PDF包。
seo-description: 组合一个PDF包，组合多种文档的不同类型，包括word文件、图像文件和PDF文档。 您可以使用Java API和Web服务API组合PDF包。
uuid: 1778c90b-9d26-466b-a7c7-401d737395e0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 023f0d9e-bfde-4879-a839-085fadffb48e
role: 开发人员
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1866'
ht-degree: 0%

---


# 汇编PDFPortfolio{#assembling-pdf-portfolios}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

您可以使用Assembler Java和Web服务API组合PDFPortfolio。 一个包可以组合多种类型的文档，包括word文件、图像文件（例如jpeg文件）和PDF文档。 作品集的布局可以设置为不同样式，如具有预览&#x200B;*的* Grid、*On a Image*&#x200B;布局，甚至&#x200B;*Revolve*。

下图是具有&#x200B;*On a Image*&#x200B;样式布局的包的屏幕截图。

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

创建PDFPortfolio可以作为传递一组文档的无纸替代方式。 使用AEM Forms，您可以通过使用结构化DDX文档调用Assembler服务来创建包。 以下DDX文档是创建PDF文档的DDXPortfolio的示例。

```xml
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="portfolio1.pdf">
         <Portfolio>
             <Navigator source="myNavigator">
                 <Resource name="navigator/image.xxx" source="myImage.png"/>
             </Navigator>
         </Portfolio>
         <PackageFiles source="dog1"  >
              <FieldData name="X">72</FieldData>
             <FieldData name="Y">72</FieldData>
             <File filename="saint_bernard.jpg" mimetype="image/jpeg"/>
         </PackageFiles>
         <PackageFiles source="dog2"  >
             <FieldData name="X">120</FieldData>
             <FieldData name="Y">216</FieldData>
             <File filename="greyhound.pdf"/>
         </PackageFiles>
     </PDF>
 </DDX>
```

DXX文档必须包含一个`Portfolio`标记，该标记带有嵌套的`Navigator`标记。 请注意，仅当`myNavigator`被指定为onImage布局导航器时，`<Resource name="navigator/image.xxx" source="myImage.png"/>`才是必需的：`AdobeOnImage.nav`。 此标签允许Assembler服务选择要用作包背景的图像。 包括`PackageFiles`和`File`标记，以定义打包文件的文件名和MIME类型。

>[!NOTE]
>
>有关Assembler服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有关DDX文档的详细信息，请参阅[Assembler Service和DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步骤{#summary-of-steps}的摘要

要创建PDFPortfolio，请执行以下任务:

1. 包括项目文件。
1. 创建PDF Assembler客户端。
1. 引用现有DDX文档。
1. 引用所需的文档。
1. 设置运行时选项。
1. 组合个人信息。
1. 保存组合包。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时为必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则为必需)

**创建PDF Assembler客户端**

在以编程方式执行Assembler操作之前，请先创建一个Assembler服务客户端。

**引用现有DDX文档**

必须引用DDX文档才能组合PDFPortfolio。 此DDX文档必须包含`Portfolio`、`Navigator`和`PackageFiles`元素。

**引用所需文档**

要汇编PDFPortfolio，请参考表示要汇编的文档的所有文件。 例如，将DDX文档中指定的所有图像文件传递给Assembler服务。 请注意，这些文件在本节中指定的DDX文档中引用：*myImage.png*&#x200B;和&#x200B;*saint_bernard.jpg*。

汇编PDFPortfolio时，将NAV文件（导航器文件）传递给Assembler服务。 传递给Assembler服务的NAV文件取决于要创建的PDFPortfolio类型。 例如，要在Image *布局上创建*，请传递AdobeOnImage.nav文件。 可以在以下文件夹中找到NAV文件：

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

从Acrobat 9（或更高版本）安装目录复制NAV文件。 将NAV文件放在客户端应用程序可以访问它的位置。 所有文件都传递到Map集合对象中的Assembler服务。

>[!NOTE]
>
>与汇编PDFPortfolio相关的快速开始使用AdobeOnImage.nav。

**设置运行时选项**

您可以设置运行时选项，以在Assembler服务执行作业时控制其行为。 例如，您可以设置一个选项，指示Assembler服务在遇到错误时继续处理作业。

**组合作品集**

要组合PDFPortfolio，请调用`invokeDDX`操作。 Assembler服务返回集合对象中的PDFPortfolio。

**保存组合的包**

PDFPortfolio在集合对象中返回。 遍历集合对象，将PDFPortfolio另存为PDF文件。

**另请参阅**

[使用Java API组合PDFPortfolio](#assemble-a-pdf-portfolio-using-the-java-api)

[使用Web服务API组合PDFPortfolio](#assemble-a-pdf-portfolio-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API {#assemble-a-pdf-portfolio-using-the-java-api}组合PDFPortfolio

使用Assembler Service API(Java)汇编PDFPortfolio:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建PDF Assembler客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`AssemblerServiceClient`对象的构造函数并传递`ServiceClientFactory`对象，创建对象。

1. 引用现有DDX文档。

   * 使用DDX文档的构造函数并传递一个指定DDX文件位置的字符串值，创建一个表示DDX文件的`java.io.FileInputStream`对象。
   * 使用`com.adobe.idp.Document`对象的构造函数并传递`java.io.FileInputStream`对象，创建对象。

1. 引用所需的文档。

   * 使用`HashMap`构造函数创建用于存储输入PDF文档的`java.util.Map`对象。
   * 使用`java.io.FileInputStream`对象的构造函数创建对象。 传递所需NAV文件的位置(对创建包所需的每个文件重复此任务)。
   * 创建一个`com.adobe.idp.Document`对象，并传递包含NAV文件的`java.io.FileInputStream`对象(对创建包所需的每个文件重复此任务)。
   * 通过调用`put`方法并传递以下参数，向`java.util.Map`对象添加一个条目：

      * 表示键名的字符串值。 此值必须与在DDX文档中指定的源元素的值匹配。 (对创建包所需的每个文件重复此任务)。
      * 包含PDF文档的`com.adobe.idp.Document`对象。 (对创建包所需的每个文件重复此任务)。

1. 设置运行时选项。

   * 使用`AssemblerOptionSpec`的构造函数创建存储运行时选项的对象。
   * 通过调用属于`AssemblerOptionSpec`对象的方法，设置运行时选项以满足您的业务要求。 例如，要指示Assembler服务在发生错误时继续处理作业，请调用`AssemblerOptionSpec`对象的`setFailOnError`方法并传递`false`。

1. 组合个人信息。

   调用`AssemblerServiceClient`对象的`invokeDDX`方法并传递以下必需值：

   * 一个`com.adobe.idp.Document`对象，它表示要使用的DDX文档
   * 一个`java.util.Map`对象，其中包含构建PDFPortfolio所需的文件。
   * 一个`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`对象，它指定运行时选项，包括默认字体和作业日志级别

   `invokeDDX`方法返回一个`com.adobe.livecycle.assembler.client.AssemblerResult`对象，该对象包含已装配的PDFPortfolio和发生的任何异常。

1. 保存组合包。

   要获取PDFPortfolio，请执行以下操作：

   * 调用`AssemblerResult`对象的`getDocuments`方法。 此方法返回`java.util.Map`对象。
   * 遍历`java.util.Map`对象，直到找到生成的`com.adobe.idp.Document`对象。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法以提取PDFPortfolio。

**另请参阅**

[快速开始（SOAP模式）：使用Java API汇编PDFPortfolio](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API {#assemble-a-pdf-portfolio-using-the-web-service-api}组合PDFPortfolio

使用Assembler Service API（Web服务）汇编PDFPortfolio:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 请确保在设置服务引用时使用以下WSDL定义：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建PDF Assembler客户端。

   * 使用`AssemblerServiceClient`对象的默认构造函数创建一个对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`AssemblerServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 您无需使用`lc_version`属性。 在创建服务引用时使用此属性。
   * 通过获取`AssemblerServiceClient.Endpoint.Binding`字段的值，创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 为字段`AssemblerServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`AssemblerServiceClient.ClientCredentials.UserName.Password`分配相应的密码值。
      * 将常量值`HttpClientCredentialType.Basic`赋给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`赋给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 引用现有DDX文档。

   * 使用`BLOB`对象的构造函数创建对象。 `BLOB`对象用于存储DDX文档。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值来创建对象，该字符串值表示DDX文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储`System.IO.FileStream`对象的内容。 可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，用流数据填充字节数组。 传递要读取的字节数组、起始位置和流长度。
   * 通过将`MTOM`属性赋予字节数组的内容，填充`BLOB`对象。

1. 引用所需的文档。

   * 对于每个输入文件，使用其构造函数创建一个`BLOB`对象。 `BLOB`对象用于存储输入文件。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值来创建一个对象，该字符串值表示输入文件的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储`System.IO.FileStream`对象的内容。 可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，用流数据填充字节数组。 传递要读取的字节数组、起始位置和流长度。
   * 将`BLOB`对象的`MTOM`字段指定为字节数组的内容，从而填充该对象。
   * 创建`MyMapOf_xsd_string_To_xsd_anyType`对象。 此集合对象用于存储创建PDFPortfolio所需的输入文件。
   * 对于每个输入文件，创建一个`MyMapOf_xsd_string_To_xsd_anyType_Item`对象。
   * 为`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`key`字段指定表示键名的字符串值。 此值必须与在DDX文档中指定的元素值匹配。 (对每个输入文件执行此任务。)
   * 将存储输入文件的`BLOB`对象指定到`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`value`字段。 (对每个输入的PDF任务执行此文档。)
   * 将`MyMapOf_xsd_string_To_xsd_anyType_Item`对象添加到`MyMapOf_xsd_string_To_xsd_anyType`对象。 调用`MyMapOf_xsd_string_To_xsd_anyType`对象的`Add`方法并传递`MyMapOf_xsd_string_To_xsd_anyType`对象。 (对每个输入的PDF任务执行此文档。)

1. 设置运行时选项。

   * 使用`AssemblerOptionSpec`的构造函数创建存储运行时选项的对象。
   * 通过为属于`AssemblerOptionSpec`对象的数据成员分配一个值，设置运行时选项以满足您的业务需求。 例如，要指示Assembler服务在发生错误时继续处理作业，请将`false`分配给`AssemblerOptionSpec`对象的`failOnError`数据成员。

1. 组合个人信息。

   调用`AssemblerServiceClient`对象的`invokeDDX`方法并传递以下值：

   * 表示DDX文档的`BLOB`对象
   * 包含所需文件的`MyMapOf_xsd_string_To_xsd_anyType`对象
   * 指定运行时选项的`AssemblerOptionSpec`对象

   `invokeDDX`方法返回一个`AssemblerResult`对象，其中包含作业的结果和发生的任何异常。

1. 保存组合包。

   要获取新创建的PDFPortfolio，请执行以下操作：

   * 访问`AssemblerResult`对象的`documents`字段，该字段是一个`Map`对象，其中包含生成的PDF文档。
   * 循环访问`Map`对象以获得每个生成文档。 然后，将该数组成员的`value`转换为`BLOB`。
   * 通过访问PDF文档的`BLOB`对象的`MTOM`属性提取表示PDF数据的二进制数据。 这将返回可写入PDF文件的字节数组。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
