---
title: 组合多个XDP片段
seo-title: 组合多个XDP片段
description: 'null'
seo-description: 'null'
uuid: 0e35ff85-ff40-4878-ae31-aa8da75bd3ec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c4706632-02e5-4510-ad9c-4f732d5fbdad
docset: aem65
translation-type: tm+mt
source-git-commit: 9678b4979580bab23dea8ca7493b48b63d5bcfa6

---


# 组合多个XDP片段{#assembling-multiple-xdp-fragments}

您可以将多个XDP片段组合到一个XDP文档中。 例如，考虑XDP片段，其中每个XDP文件包含一个或多个用于创建健康表单的子表单。 下图显示了大纲视图(表示在组合多个XDP片段快速启动中使用的tuc018_template_frued.xdp *文件* ):

![am_am_format](assets/am_am_forma.png)

下图显示了患者部分(表示在组合多个XDP片段快速启动中使用的tuc018_contact.xdp *文件* ):

![am_am_formb](assets/am_am_formb.png)

下图显示了患者健康部分(表示在组合多个XDP片段快速启动中使用的tuc018_patient ** .xdp文件):

![am_am_formc](assets/am_am_formc.png)

此片段包含两个名为subPatientPhysical *和subPatientHealth**的子表单*。 这两个子表单都在传递给Assembler服务的DDX文档中被引用。 使用Assembler服务，您可以将所有这些XDP片段合并到一个XDP文档中，如下图所示。

![am_am_formd](assets/am_am_formd.png)

以下DDX文档将多个XDP片段组合到一个XDP文档中。

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <XDP result="tuc018result.xdp">
            <XDP source="tuc018_template_flowed.xdp">
             <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
               <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientPhysical" required="false"/>
               <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientHealth" required="false"/>
            </XDP>
         </XDP>
 </DDX>
```

DDX文档包含一个XDP `result` 标签，它指定结果的名称。 在这种情况下，价值是 `tuc018result.xdp`。 该值在应用程序逻辑中引用，该逻辑用于在Assembler服务返回结果后检索XDP文档。 例如，请考虑以下用于检索已装配的XDP文档的Java应用程序逻辑（注意，该值是粗体字）:

```as3
 //Iterate through the map object to retrieve the result XDP document
 for (Iterator i = allDocs.entrySet().iterator(); i.hasNext();) {
     // Retrieve the Map object’s value
     Map.Entry e = (Map.Entry)i.next();
     //Get the key name as specified in the
     //DDX document
     String keyName = (String)e.getKey();
     if (keyName.equalsIgnoreCase("tuc018result.xdp"))
                 {
         Object o = e.getValue();
         outDoc = (Document)o;
         //Save the result PDF file
         File myOutFile = new File("C:\\AssemblerResultXDP.xdp");
         outDoc.copyToFile(myOutFile);
     }
 }
```

标 `XDP source` 签指定表示完整XDP文档的XDP文件，该文档可用作添加XDP片段的容器或按顺序附加在一起的多个文档之一。 在这种情况下，XDP文档仅用作容器(如组合多个XDP片段中所 *示的第一个图示*)。 即，其他XDP文件放在XDP容器中。

对于每个子表单，您可以添加一 `XDPContent` 个元素（此元素是可选的）。 在上例中，请注意有三个子表单： `subPatientContact`、 `subPatientPhysical`和 `subPatientHealth`。 子表 `subPatientPhysical` 单和子表 `subPatientHealth` 单都位于同一个XDP文件tuc018_patient.xdp中。 片段元素指定子表单的名称，如设计器中所定义。

>[!NOTE]
>
>有关Assembler服务的详细信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有关DDX文档的详细信息，请参 [阅Assembler service和DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步骤摘要 {#summary-of-steps}

要组合多个XDP片段，请执行以下任务：

1. 包括项目文件。
1. 创建PDF Assembler客户端。
1. 引用现有DDX文档。
1. 引用XDP文档。
1. 设置运行时选项。
1. 组合多个XDP文档。
1. 检索已装配的XDP文档。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（在JBoss上部署AEM表单时为必需）
* jbossall-client.jar（在JBoss上部署AEM表单时需要）

**创建PDF Assembler客户端**

在以编程方式执行Assembler操作之前，请先创建Assembler服务客户端。

**引用现有DDX文档**

必须引用DDX文档才能组合多个XDP文档。 此DDX文档必须包 `XDP result`含、 `XDP source`和元 `XDPContent` 素。

**引用XDP文档**

要组合多个XDP文档，请参考用于组合结果XDP文档的所有XDP文件。 确保在属性中指定XDP文档中包含的由属性引用的子表 `source` 单的名 `fragment` 称。 子表单在设计器中定义。 例如，请考虑以下XML。

```as3
 <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
```

名为subPatientContact的子表 *单必须位于名为* tuc018_contact.xdp的XDP文件中 **。

**设置运行时选项**

您可以设置运行时选项，这些选项控制Assembler服务在执行作业时的行为。 例如，您可以设置一个选项，指示Assembler服务在遇到错误时继续处理作业。

**组合多个XDP文档**

要组合多个XDP文件，请调用该 `invokeDDX` 操作。 Assembler服务返回集合对象中已装配的XDP文档。

**检索组合的XDP文档**

集合对象中会返回一个组合的XDP文档。 遍历集合对象并将XDP文档另存为XDP文件。 您还可以将XDP文档传递给其他AEM Forms服务，如“输出”。

**另请参阅**

[使用Java API组合多个XDP片段](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-java-api)

[使用Web服务API组合多个XDP片段](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)

[使用片段创建PDF文档](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)

## 使用Java API组合多个XDP片段 {#assemble-multiple-xdp-fragments-using-the-java-api}

使用Assembler Service API(Java)组合多个XDP片段：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建PDF Assembler客户端。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `AssemblerServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 引用现有DDX文档。

   * 使用 `java.io.FileInputStream` DDX文档的构造函数并传递一个指定DDX文件位置的字符串值，创建一个表示该文档的对象。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对象来创建 `java.io.FileInputStream` 对象。

1. 引用XDP文档。

   * 创建一 `java.util.Map` 个对象，该对象使用构造函数存储输入的XDP文 `HashMap` 档。
   * 创建一 `com.adobe.idp.Document` 个对象，并传递包 `java.io.FileInputStream` 含输入XDP文件的对象（对每个XDP文件重复此任务）。
   * 通过调用对象的方 `java.util.Map` 法并传递以下参数， `put` 向对象添加一个条目：

      * 表示键名的字符串值。 此值必须与DDX文档 `source` 中指定的元素值匹配（对于每个XDP文件重复此任务）。
      * 包 `com.adobe.idp.Document` 含与元素对应的XDP文档的对象(对于每个XDP `source` 文件重复此任务)。

1. 设置运行时选项。

   * 使用 `AssemblerOptionSpec` 其构造函数创建存储运行时选项的对象。
   * 通过调用属于对象的方法，设置运行时选项以满足您的业务 `AssemblerOptionSpec` 要求。 例如，要指示Assembler服务在发生错误时继续处理作业，请调用对 `AssemblerOptionSpec` 象的方 `setFailOnError` 法并传递 `false`。

1. 组合多个XDP文档。

   调用对 `AssemblerServiceClient` 象的方 `invokeDDX` 法并传递以下所需值：

   * 表示 `com.adobe.idp.Document` 要使用的DDX文档的对象
   * 包 `java.util.Map` 含输入XDP文件的对象
   * 指定 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 运行时选项（包括默认字体和作业日志级别）的对象
   该方 `invokeDDX` 法返回包 `com.adobe.livecycle.assembler.client.AssemblerResult` 含已组合的XDP文档的对象。

1. 检索已装配的XDP文档。

   要获取已装配的XDP文档，请执行以下操作：

   * 调用 `AssemblerResult` 对象的方 `getDocuments` 法。 此方法返回一个 `java.util.Map` 对象。
   * 遍历对象， `java.util.Map` 直到找到生成的对 `com.adobe.idp.Document` 象。
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法提取组合的XDP文档。

**另请参阅**

[组合多个XDP片段](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)[快速启动（SOAP模式）:使用Java API(包括AEM Forms Java库文件](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)[)组合多个XDP片段设置](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)[连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API组合多个XDP片段 {#assemble-multiple-xdp-fragments-using-the-web-service-api}

使用Assembler Service API（Web服务）组合多个XDP片段：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保在设置服务引用时使用以下WSDL定义：

   ```as3
    https://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建PDF Assembler客户端。

   * 使用对 `AssemblerServiceClient` 象的默认构造函数创建对象。
   * 使用构 `AssemblerServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务，如 `https://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `AssemblerServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字 `AssemblerServiceClient.ClientCredentials.UserName.UserName` 段。
      * 为字段分配相应的密码 `AssemblerServiceClient.ClientCredentials.UserName.Password`值。
      * 为字段 `HttpClientCredentialType.Basic` 指定常 `BasicHttpBindingSecurity.Transport.ClientCredentialType`数值。
      * 为字段 `BasicHttpSecurityMode.TransportCredentialOnly` 指定常 `BasicHttpBindingSecurity.Security.Mode`数值。

1. 引用现有DDX文档。

   * 使用对 `BLOB` 象的构造函数创建对象。 对 `BLOB` 象用于存储DDX文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示DDX文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法，用流数据 `System.IO.FileStream` 填充字节数 `Read` 组。 传递字节数组、开始位置和流长度以读取。
   * 通过 `BLOB` 将对象的属性指定 `MTOM` 为字节数组的内容来填充对象。

1. 引用XDP文档。

   * 对于每个输入XDP文件，使用其构 `BLOB` 造函数创建一个对象。 对象 `BLOB` 用于存储输入文件。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示输入文件的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法，用流数据 `System.IO.FileStream` 填充字节数 `Read` 组。 传递字节数组、开始位置和流长度以读取。
   * 通过 `BLOB` 为对象的字段指定 `MTOM` 字节数组的内容来填充该对象。
   * 创建对 `MyMapOf_xsd_string_To_xsd_anyType` 象。 此集合对象用于存储创建组合的XDP文档所需的输入文件。
   * 对于每个输入文件，创建一个 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象。
   * 为对象的字段指定表示键名 `MyMapOf_xsd_string_To_xsd_anyType_Item` 的字符串 `key` 值。 此值必须与DDX文档中指定的元素的值匹配。 （对每个输入的XDP文件执行此任务。）
   * 将存储 `BLOB` 输入文件的对象指定到该对 `MyMapOf_xsd_string_To_xsd_anyType_Item` 象的字 `value` 段。 （对每个输入的XDP文件执行此任务。）
   * 将对 `MyMapOf_xsd_string_To_xsd_anyType_Item` 象添加到对 `MyMapOf_xsd_string_To_xsd_anyType` 象。 调用 `MyMapOf_xsd_string_To_xsd_anyType` 对象的方 `Add` 法并传递对 `MyMapOf_xsd_string_To_xsd_anyType` 象。 （对每个输入的XDP文档执行此任务。）

1. 设置运行时选项。

   * 使用 `AssemblerOptionSpec` 其构造函数创建存储运行时选项的对象。
   * 通过为属于该对象的数据成员分配一个值，设置运行时选项以满足您的业务 `AssemblerOptionSpec` 要求。 例如，要指示Assembler服务在发生错误时继续处理作业，请为对 `false` 象的数 `AssemblerOptionSpec` 据成员分 `failOnError` 配。

1. 组合多个XDP文档。

   调用对 `AssemblerServiceClient` 象的方 `invokeDDX` 法并传递以下值：

   * 表示 `BLOB` DDX文档的对象
   * 包 `MyMapOf_xsd_string_To_xsd_anyType` 含所需文件的对象
   * 指定 `AssemblerOptionSpec` 运行时选项的对象
   该方 `invokeDDX` 法返回一个对 `AssemblerResult` 象，该对象包含作业的结果和发生的任何例外。

1. 检索已装配的XDP文档。

   要获取新创建的XDP文档，请执行以下操作：

   * 访问对 `AssemblerResult` 象的字 `documents` 段，该字段是包含生成 `Map` 的PDF文档的对象。
   * 遍历对象 `Map` 以获得每个生成的文档。 然后，将该阵列成员转 `value` 换为 `BLOB`。
   * 通过访问PDF文档对象的属性提取表示该PDF文 `BLOB` 档的二进制数 `MTOM` 据。 这将返回可写入XDP文件的字节数组。

**另请参阅**

[使用MTOM组合多个XDP](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)[片段调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)