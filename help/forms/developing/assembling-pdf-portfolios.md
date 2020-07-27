---
title: 汇编PDF包
seo-title: 汇编PDF包
description: 'null'
seo-description: 'null'
uuid: 1778c90b-9d26-466b-a7c7-401d737395e0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 023f0d9e-bfde-4879-a839-085fadffb48e
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1785'
ht-degree: 0%

---


# 汇编PDF包 {#assembling-pdf-portfolios}

您可以使用Assembler Java和Web服务API组合PDF包。 一个包可以组合多种文档的不同类型，包括word文件、图像文件（例如jpeg文件）和PDF文档。 作品集的布局可以设置为不同的样式，如 *带预览的Grid*、 *在图像上* 或甚至 *Revolve*。

下图是具有“在图像样式上”布 *局的包的截屏* 。

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

创建PDF包可以作为传递文档集的无纸替代方法。 使用AEM Forms，您可以通过使用结构化DDX文档调用Assembler服务来创建包。 以下DDX文档是创建PDF包的DDX文档的示例。

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

DXX文档必须包含 `Portfolio` 带有嵌套标记的 `Navigator` 标记。 请注意，仅当 `<Resource name="navigator/image.xxx" source="myImage.png"/>` 将标记指定 `myNavigator` 为onImage布局导航器时，才必须使用： `AdobeOnImage.nav`. 此标记允许Assembler服务选择要用作包背景的图像。 包含 `PackageFiles` 和标 `File` 记以定义打包文件的文件名和MIME类型。

>[!NOTE]
>
>有关Assembler服务的详细信息，请参 [阅Services Reference forAEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有关DDX文档的详细信息，请参 [阅Assembler Service和DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步骤摘要 {#summary-of-steps}

要创建PDF包，请执行以下任务:

1. 包括项目文件。
1. 创建PDF Assembler客户端。
1. 引用现有DDX文档。
1. 引用所需文档。
1. 设置运行时选项。
1. 组合个人信息。
1. 保存组合的包。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时为必需)
* jbossall-client.jar(在JBoss上部署AEM Forms时需要)

**创建PDF Assembler客户端**

在以编程方式执行Assembler操作之前，请先创建Assembler服务客户端。

**引用现有DDX文档**

必须引用DDX文档来组合PDF包。 此DDX文档必须包 `Portfolio`含 `Navigator` 元素和 `PackageFiles` 元素。

**引用所需文档**

要组合PDF包，请参考表示要组合的文档的所有文件。 例如，将DDX文档中指定的所有图像文件传递给Assembler服务。 请注意，这些文件在本节中指定的DDX文档中被引用： *myImage.png* 和 *saint_bernard.jpg*。

汇编PDF包时，将NAV文件（导航器文件）传递给Assembler服务。 传递给Assembler服务的NAV文件取决于要创建的PDF包类型。 例如，要创建“ *在图像上* ”布局，请传递AdobeOnImage.nav文件。 可以在以下文件夹中找到NAV文件：

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

从Acrobat 9（或更高版本）安装目录复制NAV文件。 将NAV文件放在客户端应用程序可以访问的位置。 所有文件都会传递到Map集合对象中的Assembler服务。

>[!NOTE]
>
>与汇编PDF包相关的快速开始使用AdobeOnImage.nav。

**设置运行时选项**

您可以设置运行时选项，这些选项在Assembler服务执行作业时控制其行为。 例如，您可以设置一个选项，指示Assembler服务在遇到错误时继续处理作业。

**组合作品集**

要组合PDF包，您需要调用该 `invokeDDX` 操作。 Assembler服务返回集合对象中的PDF包。

**保存组合的包**

PDF包在集合对象中返回。 对集合对象进行迭代，将PDF包另存为PDF文件。

**另请参阅**

[使用Java API组合PDF包](#assemble-a-pdf-portfolio-using-the-java-api)

[使用Web服务API组合PDF包](#assemble-a-pdf-portfolio-using-the-web-service-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API组合PDF包 {#assemble-a-pdf-portfolio-using-the-java-api}

使用Assembler Service API(Java)组合PDF包：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建PDF Assembler客户端。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `AssemblerServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 引用现有DDX文档。

   * 通过 `java.io.FileInputStream` 使用DDX文档的构造函数并传递指定DDX文件位置的字符串值，创建一个表示该DDX文件的对象。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对 `java.io.FileInputStream` 象。

1. 引用所需文档。

   * 使用构 `java.util.Map` 造函数创建用于存储输入PDF文档的对 `HashMap` 象。
   * 使用对 `java.io.FileInputStream` 象的构造函数创建对象。 传递所需NAV文件的位置(对于创建包所需的每个文件重复此任务)。
   * 创建一 `com.adobe.idp.Document` 个对象并传 `java.io.FileInputStream` 递包含NAV文件的对象(对于创建包所需的每个文件重复此任务)。
   * 通过调用对象的方 `java.util.Map` 法并传递以 `put` 下参数，向对象添加一个条目：

      * 表示键名称的字符串值。 此值必须与在DDX文档中指定的源元素值匹配。 (对创建包所需的每个文件重复此任务)。
      * 包 `com.adobe.idp.Document` 含PDF文档的对象。 (对创建包所需的每个文件重复此任务)。

1. 设置运行时选项。

   * 使用 `AssemblerOptionSpec` 其构造函数创建存储运行时选项的对象。
   * 通过调用属于对象的方法，设置运行时选项以满足业务 `AssemblerOptionSpec` 要求。 例如，要指示Assembler服务在出现错误时继续处理作业，请调 `AssemblerOptionSpec` 用对象的 `setFailOnError` 方法并传递 `false`。

1. 组合个人信息。

   调用对 `AssemblerServiceClient` 象的方 `invokeDDX` 法并传递以下必需值：

   * 表 `com.adobe.idp.Document` 示要使用的DDX文档的对象
   * 包 `java.util.Map` 含构建PDF包所需文件的对象。
   * 指定 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 运行时选项（包括默认字体和作业日志级别）的对象

   该方 `invokeDDX` 法返回一个 `com.adobe.livecycle.assembler.client.AssemblerResult` 对象，该对象包含已组合的PDF包和发生的任何异常。

1. 保存组合的包。

   要获取PDF包，请执行以下操作：

   * 调用 `AssemblerResult` 对象的方 `getDocuments` 法。 此方法返回一个 `java.util.Map` 对象。
   * 遍历对象 `java.util.Map` ，直到找到生成的对 `com.adobe.idp.Document` 象。
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法以提取PDF包。

**另请参阅**

[快速开始（SOAP模式）: 使用Java API组合PDF包](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API组合PDF包 {#assemble-a-pdf-portfolio-using-the-web-service-api}

使用Assembler Service API（Web服务）组合PDF包：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 请确保在设置服务引用时使用以下WSDL定义： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建PDF Assembler客户端。

   * 使用对象 `AssemblerServiceClient` 的默认构造函数创建对象。
   * 使用构 `AssemblerServiceClient.Endpoint.Address` 造函数创建 `System.ServiceModel.EndpointAddress` 对象。 将指定WSDL的字符串值传递给AEM Forms服务(例如 `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您无需使用该属 `lc_version` 性。 此属性在您创建服务引用时使用。
   * 通过获 `System.ServiceModel.BasicHttpBinding` 取字段的值创建对 `AssemblerServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常量值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常量值 `BasicHttpBindingSecurity.Security.Mode`。

1. 引用现有DDX文档。

   * 使用对 `BLOB` 象的构造函数创建对象。 该 `BLOB` 对象用于存储DDX文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示DDX文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法，用流数 `System.IO.FileStream` 据填充字节 `Read` 数组。 传递要读取的字节数组、开始位置和流长度。
   * 通过 `BLOB` 将对象属性 `MTOM` 赋予字节数组的内容来填充对象。

1. 引用所需文档。

   * 对于每个输入文件，使用其构 `BLOB` 造函数创建一个对象。 该 `BLOB` 对象用于存储输入文件。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示输入文件的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法，用流数 `System.IO.FileStream` 据填充字节 `Read` 数组。 传递要读取的字节数组、开始位置和流长度。
   * 通过 `BLOB` 为对象的字段 `MTOM` 指定字节数组的内容来填充对象。
   * 创建对 `MyMapOf_xsd_string_To_xsd_anyType` 象。 此集合对象用于存储创建PDF包所需的输入文件。
   * 对于每个输入文件，创建一个 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象。
   * 为对象的字段指定表示键名 `MyMapOf_xsd_string_To_xsd_anyType_Item` 的字符串 `key` 值。 此值必须与在DDX文档中指定的元素值匹配。 (对每个输入文件执行此任务。)
   * 将存储 `BLOB` 输入文件的对象指定到该 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象的字 `value` 段。 (对每个输入的PDF任务执行此文档。)
   * 将对 `MyMapOf_xsd_string_To_xsd_anyType_Item` 象添加到对 `MyMapOf_xsd_string_To_xsd_anyType` 象。 调用 `MyMapOf_xsd_string_To_xsd_anyType` 对象的方 `Add` 法并传递对 `MyMapOf_xsd_string_To_xsd_anyType` 象。 (对每个输入的PDF任务执行此文档。)

1. 设置运行时选项。

   * 使用 `AssemblerOptionSpec` 其构造函数创建存储运行时选项的对象。
   * 通过为属于该对象的数据成员分配一个值，设置运行时选项以满足您的业务 `AssemblerOptionSpec` 要求。 例如，要指示Assembler服务在出现错误时继续处理作业，请 `false` 指定 `AssemblerOptionSpec` 对象的数据 `failOnError` 成员。

1. 组合个人信息。

   调用对 `AssemblerServiceClient` 象的方 `invokeDDX` 法并传递以下值：

   * 表 `BLOB` 示DDX文档的对象
   * 包 `MyMapOf_xsd_string_To_xsd_anyType` 含所需文件的对象
   * 指定 `AssemblerOptionSpec` 运行时选项的对象

   方 `invokeDDX` 法返回一 `AssemblerResult` 个对象，其中包含作业的结果和发生的任何异常。

1. 保存组合的包。

   要获取新创建的PDF包，请执行以下操作：

   * 访问对 `AssemblerResult` 象的字 `documents` 段，该字段是包含 `Map` 生成的PDF文档的对象。
   * 对对象进行 `Map` 迭代以获得每个生成文档。 然后，将该阵列成员 `value` 转换为 `BLOB`。
   * 通过访问PDF文档对象的属性提取表示PDF `BLOB` 的二进制 `MTOM` 数据。 这将返回可写入PDF文件的字节数组。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
