---
title: 组装PDFPortfolio
seo-title: Assembling PDF Portfolios
description: 组合PDF组合以组合多种类型的文档，包括字文件、图像文件和PDF文档。 您可以使用Java API和Web服务API来组合PDF产品组合。
seo-description: Assemble a PDF portfolio to combine several documents of various types, including word file, image files, and PDF documents. You can assemble a PDF portfolio using a Java API and a Web Service API.
uuid: 1778c90b-9d26-466b-a7c7-401d737395e0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 023f0d9e-bfde-4879-a839-085fadffb48e
role: Developer
exl-id: d2bd7c3e-4f75-4234-a7aa-ee8524430493
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1828'
ht-degree: 0%

---

# 组装PDFPortfolio {#assembling-pdf-portfolios}

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

您可以使用汇编程序Java和Web服务API来汇编PDFPortfolio。 组合可以组合多种类型的多个文档，包括字文件、图像文件（例如jpeg文件）和PDF文档。 组合的布局可以设置为不同的样式，如 *预览网格*, *在图像上* 布局甚至 *旋转*.

下图是包含 *在图像上* 样式布局。

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

创建PDFPortfolio可作为传递文档集的无纸化替代方法。 使用AEM Forms，您可以通过使用结构化DDX文档调用汇编程序服务来创建组合。 以下DDX文档是创建PDFPortfolio的DDX文档示例。

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

DXX文档必须包含 `Portfolio` 标记 `Navigator` 标记。 记下标记 `<Resource name="navigator/image.xxx" source="myImage.png"/>` 仅当 `myNavigator` 分配为onImage布局导航器： `AdobeOnImage.nav`. 此标记允许汇编程序服务选择要用作组合背景的图像。 包括 `PackageFiles` 和 `File` 用于定义打包文件的文件名和MIME类型的标记。

>[!NOTE]
>
>有关汇编程序服务的详细信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>有关DDX文档的更多信息，请参阅 [汇编程序服务和DDX参考](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 步骤摘要 {#summary-of-steps}

要创建PDFPortfolio，请执行以下任务：

1. 包括项目文件。
1. 创建PDF汇编程序客户端。
1. 引用现有DDX文档。
1. 引用所需文档。
1. 设置运行时选项。
1. 组合组合。
1. 保存组合。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此变量为必需变量)

**创建PDF汇编程序客户端**

在以编程方式执行汇编程序操作之前，请创建汇编程序服务客户端。

**引用现有DDX文档**

必须引用DDX文档才能组合PDFPortfolio。 此DDX文档必须包含 `Portfolio`, `Navigator` 和 `PackageFiles` 元素。

**参考所需文档**

要组合PDFPortfolio，请引用表示要组合的文档的所有文件。 例如，将DDX文档中指定的所有图像文件传递到汇编程序服务。 请注意，这些文件在本节中指定的DDX文档中引用： *myImage.png* 和 *saint_bernard.jpg*.

组装PDFPortfolio时，将NAV文件（导航器文件）传递到汇编程序服务。 您传递到汇编程序服务的NAV文件取决于要创建的PDFPortfolio类型。 例如，创建 *在图像上* 布局中，传递AdobeOnImage.nav文件。 您可以在以下文件夹中找到NAV文件：

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

从Acrobat 9（或更高版本）安装目录复制NAV文件。 将NAV文件放置在您的客户端应用程序可以访问的位置。 所有文件都将传递到映射集合对象中的汇编程序服务。

>[!NOTE]
>
>与“组装PDFPortfolio”关联的快速入门使用AdobeOnImage.nav。

**设置运行时选项**

您可以设置运行时选项，以在汇编程序服务执行作业时控制其行为。 例如，您可以设置一个选项，指示汇编程序服务在遇到错误时继续处理作业。

**组合组合**

要组合PDFPortfolio，请将 `invokeDDX` 操作。 汇编程序服务在集合对象中返回PDFPortfolio。

**保存组合**

PDFPortfolio在集合对象中返回。 遍历收集对象，并将PDFPortfolio另存为PDF文件。

**另请参阅**

[使用Java API组合PDFPortfolio](#assemble-a-pdf-portfolio-using-the-java-api)

[使用Web服务API组合PDFPortfolio](#assemble-a-pdf-portfolio-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API组合PDFPortfolio {#assemble-a-pdf-portfolio-using-the-java-api}

使用汇编程序服务API(Java)来汇编PDFPortfolio:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建PDF汇编程序客户端。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `AssemblerServiceClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 引用现有DDX文档。

   * 创建 `java.io.FileInputStream` 使用其构造函数并传递指定DDX文件位置的字符串值来表示DDX文档的对象。
   * 创建 `com.adobe.idp.Document` 对象，并使用其构造函数进行传递 `java.io.FileInputStream` 对象。

1. 引用所需文档。

   * 创建 `java.util.Map` 用于通过使用 `HashMap` 构造函数。
   * 创建 `java.io.FileInputStream` 对象。 传递所需NAV文件的位置（对创建组合所需的每个文件重复此任务）。
   * 创建 `com.adobe.idp.Document` 对象并传递 `java.io.FileInputStream` 包含NAV文件的对象（对创建组合所需的每个文件重复此任务）。
   * 在 `java.util.Map` 通过调用对象 `put` 方法和传递以下参数：

      * 表示键名称的字符串值。 此值必须匹配DDX文档中指定的源元素值。 （对创建组合所需的每个文件重复此任务）。
      * A `com.adobe.idp.Document` 包含PDF文档的对象。 （对创建组合所需的每个文件重复此任务）。

1. 设置运行时选项。

   * 创建 `AssemblerOptionSpec` 使用其构造函数存储运行时选项的对象。
   * 通过调用属于 `AssemblerOptionSpec` 对象。 例如，要指示汇编程序服务在发生错误时继续处理作业，请调用 `AssemblerOptionSpec` 对象 `setFailOnError` 方法和传递 `false`.

1. 组合组合。

   调用 `AssemblerServiceClient` 对象 `invokeDDX` 方法，并传递以下必需值：

   * A `com.adobe.idp.Document` 表示要使用的DDX文档的对象
   * A `java.util.Map` 对象，其中包含构建PDFPortfolio所需的文件。
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定运行时选项（包括默认字体和作业日志级别）的对象

   的 `invokeDDX` 方法返回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含已装配的PDFPortfolio和发生的任何异常的对象。

1. 保存组合。

   要获取PDFPortfolio，请执行以下操作：

   * 调用 `AssemblerResult` 对象 `getDocuments` 方法。 此方法将返回 `java.util.Map` 对象。
   * 循环访问 `java.util.Map` 对象，直到找到结果 `com.adobe.idp.Document` 对象。
   * 调用 `com.adobe.idp.Document` 对象 `copyToFile` 方法提取PDFPortfolio。

**另请参阅**

[快速入门（SOAP模式）：使用Java API组装PDFPortfolio](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API组合PDFPortfolio {#assemble-a-pdf-portfolio-using-the-web-service-api}

使用汇编程序服务API（Web服务）来汇编PDFPortfolio:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 在设置服务引用时，请确保使用以下WSDL定义： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 具有托管AEM Forms的服务器的IP地址。

1. 创建PDF汇编程序客户端。

   * 创建 `AssemblerServiceClient` 对象。
   * 创建 `AssemblerServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递到AEM Forms服务(例如， `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您无需使用 `lc_version` 属性。 在创建服务引用时，会使用此属性。
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `AssemblerServiceClient.Endpoint.Binding` 字段。 将返回值转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象 `MessageEncoding` 字段 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * 为字段分配相应的密码值 `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * 指定常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指定常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 引用现有DDX文档。

   * 创建 `BLOB` 对象。 的 `BLOB` 对象用于存储DDX文档。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示DDX文档的文件位置以及打开文件的模式。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法。 传递字节数组、开始位置和流长度以读取。
   * 填充 `BLOB` 通过指定对象 `MTOM` 属性。

1. 引用所需文档。

   * 对于每个输入文件，请创建 `BLOB` 对象。 的 `BLOB` 对象用于存储输入文件。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示输入文件的文件位置和打开文件的模式。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法。 传递字节数组、开始位置和流长度以读取。
   * 填充 `BLOB` 通过指定对象 `MTOM` 字段中，显示字节数组的内容。
   * 创建 `MyMapOf_xsd_string_To_xsd_anyType` 对象。 此集合对象用于存储创建PDFPortfolio所需的输入文件。
   * 对于每个输入文件，请创建 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象。
   * 为分配表示键名称的字符串值 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象 `key` 字段。 此值必须匹配DDX文档中指定的元素值。 （为每个输入文件执行此任务。）
   * 分配 `BLOB` 将输入文件存储到 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象 `value` 字段。 (对每个输入PDF文档执行此任务。)
   * 添加 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象 `MyMapOf_xsd_string_To_xsd_anyType` 对象。 调用 `MyMapOf_xsd_string_To_xsd_anyType` 对象 `Add` 方法和通过 `MyMapOf_xsd_string_To_xsd_anyType` 对象。 (对每个输入PDF文档执行此任务。)

1. 设置运行时选项。

   * 创建 `AssemblerOptionSpec` 使用其构造函数存储运行时选项的对象。
   * 通过为属于 `AssemblerOptionSpec` 对象。 例如，要指示汇编程序服务在发生错误时继续处理作业，请指定 `false` 到 `AssemblerOptionSpec` 对象 `failOnError` 数据成员。

1. 组合组合。

   调用 `AssemblerServiceClient` 对象 `invokeDDX` 方法并传递以下值：

   * A `BLOB` 表示DDX文档的对象
   * 的 `MyMapOf_xsd_string_To_xsd_anyType` 包含所需文件的对象
   * 安 `AssemblerOptionSpec` 指定运行时选项的对象

   的 `invokeDDX` 方法返回 `AssemblerResult` 包含作业结果和发生的任何例外的对象。

1. 保存组合。

   要获取新创建的PDFPortfolio，请执行以下操作：

   * 访问 `AssemblerResult` 对象 `documents` 字段， `Map` 包含生成PDF文档的对象。
   * 循环访问 `Map` 对象来获取每个生成文档。 然后，将该阵列成员的 `value` 至 `BLOB`.
   * 通过访问表示PDF文档的二进制数据 `BLOB` 对象 `MTOM` 属性。 这会返回一个字节数组，您可以将其写出到PDF文件。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
