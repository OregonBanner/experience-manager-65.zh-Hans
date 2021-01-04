---
title: 组合多个XDP片段
seo-title: 组合多个XDP片段
description: 使用Java API和Web服务API将多个XDP片段组合到单个XDP文档中。
seo-description: 使用Java API和Web服务API将多个XDP片段组合到单个XDP文档中。
uuid: 0e35ff85-ff40-4878-ae31-aa8da75bd3ec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c4706632-02e5-4510-ad9c-4f732d5fbdad
docset: aem65
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1908'
ht-degree: 0%

---


# 组合多个XDP片段{#assembling-multiple-xdp-fragments}

您可以将多个XDP片段组合到一个XDP文档中。 例如，考虑XDP片段，其中每个XDP文件包含一个或多个用于创建健康表单的子表单。 下图显示了大纲视图(表示&#x200B;*组合多个XDP片段*&#x200B;快速开始中使用的tuc018_template_frued.xdp文件):

![am_am_forma](assets/am_am_forma.png)

下图显示了患者部分(表示&#x200B;*组合多个XDP片段*&#x200B;快速开始中使用的tuc018_contact.xdp文件):

![am_am_formb](assets/am_am_formb.png)

下图显示了患者健康部分(表示&#x200B;*组合多个XDP片段*&#x200B;快速开始中使用的tuc018_patient.xdp文件):

![am_am_formc](assets/am_am_formc.png)

此片段包含两个名为&#x200B;*subPatientPhysical*&#x200B;和&#x200B;*subPatientHealth*&#x200B;的子表单。 这两个子表单都在传递给Assembler服务的DDX文档中被引用。 使用Assembler服务，您可以将所有这些XDP片段合并为一个XDP文档，如下图所示。

![am_am_formd](assets/am_am_formd.png)

以下DDX文档将多个XDP片段组合为XDP文档。

```xml
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

DDX文档包含一个XDP `result`标签，它指定结果的名称。 在这种情况下，该值为`tuc018result.xdp`。 此值在应用程序逻辑中引用，该逻辑用于在Assembler服务返回结果后检索XDP文档。 例如，请考虑以下用于检索已装配的XDP文档的Java应用程序逻辑（注意，该值是加粗的）:

```java
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

`XDP source`标签指定表示完整XDP文档的XDP文件，该容器可用作添加XDP片段的或按顺序附加到一起的多个文档之一。 在这种情况下，XDP文档仅用作容器（第一个图示显示在&#x200B;*组合多个XDP片段*&#x200B;中）。 即，其他XDP文件放在XDP容器中。

对于每个子表单，可以添加`XDPContent`元素（此元素是可选的）。 在上例中，请注意有三个子表单：`subPatientContact`、`subPatientPhysical`和`subPatientHealth`。 `subPatientPhysical`子表单和`subPatientHealth`子表单都位于同一个XDP文件tuc018_patient.xdp中。 片段元素指定子表单的名称，如设计器中所定义。

>[!NOTE]
>
>有关Assembler服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有关DDX文档的详细信息，请参阅[Assembler Service和DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步骤{#summary-of-steps}的摘要

要组合多个XDP片段，请执行以下任务:

1. 包括项目文件。
1. 创建PDF Assembler客户端。
1. 引用现有DDX文档。
1. 参考XDP文档。
1. 设置运行时选项。
1. 组合多个XDP文档。
1. 检索装配的XDP文档。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss上，则为必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必需)

**创建PDF Assembler客户端**

在以编程方式执行Assembler操作之前，请先创建Assembler服务客户端。

**引用现有DDX文档**

必须引用DDX文档才能组合多个XDP文档。 此DDX文档必须包含`XDP result`、`XDP source`和`XDPContent`元素。

**参考XDP文档**

要组合多个XDP文档，请参考用于组合结果的XDP文档的所有XDP文件。 确保在`fragment`属性中指定了XDP文档中包含的由`source`属性引用的子表单的名称。 子表单在设计器中定义。 例如，请考虑以下XML。

```xml
 <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
```

名为&#x200B;*subPatientContact*&#x200B;的子表单必须位于名为&#x200B;*tuc018_contact.xdp*&#x200B;的XDP文件中。

**设置运行时选项**

您可以设置运行时选项，这些选项在Assembler服务执行作业时控制其行为。 例如，您可以设置一个选项，指示Assembler服务在遇到错误时继续处理作业。

**组合多个XDP文档**

要组合多个XDP文件，请调用`invokeDDX`操作。 Assembler服务返回集合对象中已装配的XDP文档。

**检索装配的XDP文档**

在集合对象中返回一个组合的XDP文档。 遍历集合对象，将XDP文档另存为XDP文件。 您还可以将XDP文档传递给其他AEM Forms服务，如“输出”。

**另请参阅**

[使用Java API组合多个XDP片段](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-java-api)

[使用Web服务API组合多个XDP片段](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-web-service-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)

[使用片段创建PDF文档](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)

## 使用Java API {#assemble-multiple-xdp-fragments-using-the-java-api}组合多个XDP片段

使用Assembler Service API(Java)组合多个XDP片段：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建PDF Assembler客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`AssemblerServiceClient`对象的构造函数创建`ServiceClientFactory`对象。

1. 引用现有DDX文档。

   * 通过使用DDX文档的构造函数并传递一个指定DDX文件位置的字符串值，创建一个表示DDX文件的`java.io.FileInputStream`对象。
   * 使用`com.adobe.idp.Document`对象的构造函数并传递`java.io.FileInputStream`对象，创建&lt;a0/>对象。

1. 参考XDP文档。

   * 创建一个`java.util.Map`对象，该对象使用`HashMap`构造函数存储输入的XDP文档。
   * 创建一个`com.adobe.idp.Document`对象，并传递包含输入XDP文件的`java.io.FileInputStream`对象(对每个XDP文件重复此任务)。
   * 通过调用`put`方法并传递以下参数，向`java.util.Map`对象添加一个条目：

      * 表示键名称的字符串值。 此值必须与DDX文档中指定的`source`元素值匹配(对每个XDP文件重复此任务)。
      * 一个`com.adobe.idp.Document`对象，它包含与`source`元素对应的XDP文档(对每个XDP文件重复此任务)。

1. 设置运行时选项。

   * 使用其构造函数创建存储运行时选项的`AssemblerOptionSpec`对象。
   * 通过调用属于`AssemblerOptionSpec`对象的方法，设置运行时选项以满足业务要求。 例如，要指示Assembler服务在出现错误时继续处理作业，请调用`AssemblerOptionSpec`对象的`setFailOnError`方法并传递`false`。

1. 组合多个XDP文档。

   调用`AssemblerServiceClient`对象的`invokeDDX`方法并传递以下必需值：

   * 一个`com.adobe.idp.Document`对象，它表示要使用的DDX文档
   * 包含输入XDP文件的`java.util.Map`对象
   * 一个`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`对象，它指定运行时选项，包括默认字体和作业日志级别

   `invokeDDX`方法返回一个`com.adobe.livecycle.assembler.client.AssemblerResult`对象，该对象包含已装配的XDP文档。

1. 检索装配的XDP文档。

   要获取装配的XDP文档，请执行以下操作：

   * 调用`AssemblerResult`对象的`getDocuments`方法。 此方法返回`java.util.Map`对象。
   * 对`java.util.Map`对象进行迭代，直到找到生成的`com.adobe.idp.Document`对象。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法提取已装配的XDP文档。

**另请参阅**

[组合多个XDP](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[片段快速开始（SOAP模式）:使用Java API(包括AEM FormsJava库文](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)
[件)组合多个XDP片](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[段设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API {#assemble-multiple-xdp-fragments-using-the-web-service-api}组合多个XDP片段

使用Assembler Service API（web服务）组合多个XDP片段：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 请确保在设置服务引用时使用以下WSDL定义：

   ```java
    https://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建PDF Assembler客户端。

   * 使用其默认构造函数创建`AssemblerServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`AssemblerServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务，如`https://localhost:8080/soap/services/AssemblerService?blob=mtom`。 您无需使用`lc_version`属性。 此属性在您创建服务引用时使用。
   * 通过获取`AssemblerServiceClient.Endpoint.Binding`字段的值创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为`AssemblerServiceClient.ClientCredentials.UserName.UserName`字段指定AEM表单用户名。
      * 为`AssemblerServiceClient.ClientCredentials.UserName.Password`字段指定相应的口令值。
      * 将`HttpClientCredentialType.Basic`常数值指定给`BasicHttpBindingSecurity.Transport.ClientCredentialType`字段。
      * 将`BasicHttpSecurityMode.TransportCredentialOnly`常数值指定给`BasicHttpBindingSecurity.Security.Mode`字段。

1. 引用现有DDX文档。

   * 使用`BLOB`对象的构造函数创建&lt;a0/>对象。 `BLOB`对象用于存储DDX文档。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示DDX文档的文件位置以及打开文件的模式。
   * 创建存储`System.IO.FileStream`对象内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性，可以确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，用流数据填充字节数组。 传递要读取的字节数组、开始位置和流长度。
   * 通过为`MTOM`对象的&lt;a1/>属性指定字节数组的内容，填充`BLOB`对象。

1. 参考XDP文档。

   * 对于每个输入XDP文件，使用其构造函数创建一个`BLOB`对象。 `BLOB`对象用于存储输入文件。
   * 通过调用其构造函数并传递一个字符串值来创建`System.IO.FileStream`对象，该字符串值表示输入文件的文件位置以及打开文件的模式。
   * 创建存储`System.IO.FileStream`对象内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性，可以确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，用流数据填充字节数组。 传递要读取的字节数组、开始位置和流长度。
   * 通过为`MTOM`字段指定字节数组的内容，填充`BLOB`对象。
   * 创建`MyMapOf_xsd_string_To_xsd_anyType`对象。 此集合对象用于存储创建组合的XDP文档所需的输入文件。
   * 对于每个输入文件，创建一个`MyMapOf_xsd_string_To_xsd_anyType_Item`对象。
   * 为`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`key`字段指定表示键名的字符串值。 此值必须与在DDX文档中指定的元素值匹配。 (对每个输入的XDP文件执行此任务。)
   * 将存储输入文件的`BLOB`对象指定到`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`value`字段。 (对每个输入的XDP文件执行此任务。)
   * 将`MyMapOf_xsd_string_To_xsd_anyType_Item`对象添加到`MyMapOf_xsd_string_To_xsd_anyType`对象。 调用`MyMapOf_xsd_string_To_xsd_anyType`对象的`Add`方法并传递`MyMapOf_xsd_string_To_xsd_anyType`对象。 (对每个输入XDP任务执行此文档。)

1. 设置运行时选项。

   * 使用其构造函数创建存储运行时选项的`AssemblerOptionSpec`对象。
   * 通过为属于`AssemblerOptionSpec`对象的数据成员分配一个值，设置运行时选项以满足您的业务要求。 例如，要指示Assembler服务在出现错误时继续处理作业，请将`false`分配给`AssemblerOptionSpec`对象的`failOnError`数据成员。

1. 组合多个XDP文档。

   调用`AssemblerServiceClient`对象的`invokeDDX`方法并传递以下值：

   * 表示DDX文档的`BLOB`对象
   * 包含所需文件的`MyMapOf_xsd_string_To_xsd_anyType`对象
   * 指定运行时选项的`AssemblerOptionSpec`对象

   `invokeDDX`方法返回一个`AssemblerResult`对象，该对象包含作业的结果和发生的任何异常。

1. 检索装配的XDP文档。

   要获取新创建的XDP文档，请执行以下操作：

   * 访问`AssemblerResult`对象的`documents`字段，该字段是一个`Map`对象，包含生成的PDF文档。
   * 对`Map`对象进行迭代以获得每个生成文档。 然后，将该数组成员的`value`转换为`BLOB`。
   * 通过访问PDF文档的`BLOB`对象的`MTOM`属性，提取表示PDF数据的二进制数据。 这将返回可写入XDP文件的字节数组。

**另请参阅**

[使用MTOM汇编多](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[个XDP片段调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)