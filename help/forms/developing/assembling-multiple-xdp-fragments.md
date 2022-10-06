---
title: 组装多个XDP片段
seo-title: Assembling Multiple XDP Fragments
description: 使用Java API和Web服务API将多个XDP片段组合到单个XDP文档中。
seo-description: Assemble multiple XDP fragments into a single XDP document using the Java API and Web Service API.
uuid: 0e35ff85-ff40-4878-ae31-aa8da75bd3ec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c4706632-02e5-4510-ad9c-4f732d5fbdad
docset: aem65
role: Developer
exl-id: 54d98c69-2b2e-46cb-9f6a-7e9bdbe5c378
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1887'
ht-degree: 0%

---

# 组装多个XDP片段{#assembling-multiple-xdp-fragments}

您可以将多个XDP片段组合到一个XDP文档中。 例如，假定XDP片段中每个XDP文件都包含一个或多个用于创建运行状况表单的子表单。 下图显示了大纲视图(表示 *组装多个XDP片段* 快速入门):

![am_am_forma](assets/am_am_forma.png)

下图显示了患者部分(表示 *组装多个XDP片段* 快速入门):

![am_am_formb](assets/am_am_formb.png)

下图显示了患者健康部分(表示 *组装多个XDP片段* 快速入门):

![am_am_formc](assets/am_am_formc.png)

此片段包含两个名为 *subPatientPhysical* 和 *subPatientHealth*. 这两个子表单在传递到汇编程序服务的DDX文档中均被引用。 使用汇编程序服务，您可以将所有这些XDP片段合并到一个XDP文档中，如下图所示。

![am_am_formd](assets/am_am_formd.png)

以下DDX文档将多个XDP片段组合到一个XDP文档中。

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

DDX文档包含XDP `result` 用于指定结果名称的标记。 在这种情况下，其价值是 `tuc018result.xdp`. 在汇编程序服务返回结果后，该值在用于检索XDP文档的应用程序逻辑中引用。 例如，请考虑以下用于检索已装配的XDP文档的Java应用程序逻辑（请注意，值显示为粗体）：

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

的 `XDP source` 标记会指定XDP文件，该文件表示一个完整的XDP文档，该文档可用作添加XDP片段的容器，或作为按顺序附加在一起的多个文档之一。 在这种情况下，XDP文档仅用作容器(如 *组装多个XDP片段*)。 即，其他XDP文件放置在XDP容器中。

对于每个子表单，您可以添加 `XDPContent` 元素（此元素是可选的）。 在上例中，请注意有三个子表单： `subPatientContact`, `subPatientPhysical`和 `subPatientHealth`. 和 `subPatientPhysical` 子窗体和 `subPatientHealth` 子表单位于同一XDP文件tuc018_patient.xdp中。 片段元素指定子表单的名称，如Designer中所定义。

>[!NOTE]
>
>有关汇编程序服务的详细信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>有关DDX文档的更多信息，请参阅 [汇编程序服务和DDX参考](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 步骤摘要 {#summary-of-steps}

要组合多个XDP片段，请执行以下任务：

1. 包括项目文件。
1. 创建PDF汇编程序客户端。
1. 引用现有DDX文档。
1. 引用XDP文档。
1. 设置运行时选项。
1. 组合多个XDP文档。
1. 检索已装配的XDP文档。

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

必须引用DDX文档来组合多个XDP文档。 此DDX文档必须包含 `XDP result`, `XDP source`和 `XDPContent` 元素。

**引用XDP文档**

要组合多个XDP文档，请引用用于组合结果XDP文档的所有XDP文件。 确保XDP文档中包含且由 `source` 属性在 `fragment` 属性。 子表单在Designer中定义。 例如，请考虑以下XML。

```xml
 <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
```

名为的子窗体 *subPatientContact* 必须位于名为的XDP文件中 *tuc018_contact.xdp*.

**设置运行时选项**

您可以设置运行时选项，以在汇编程序服务执行作业时控制其行为。 例如，您可以设置一个选项，指示汇编程序服务在遇到错误时继续处理作业。

**组合多个XDP文档**

要组合多个XDP文件，请调用 `invokeDDX` 操作。 汇编程序服务返回集合对象中装配的XDP文档。

**检索已装配的XDP文档**

在集合对象中返回装配的XDP文档。 遍历集合对象，并将XDP文档另存为XDP文件。 您还可以将XDP文档传递到其他AEM Forms服务，如“输出”。

**另请参阅**

[使用Java API组合多个XDP片段](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-java-api)

[使用Web服务API组合多个XDP片段](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)

[使用片段创建PDF文档](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)

## 使用Java API组合多个XDP片段 {#assemble-multiple-xdp-fragments-using-the-java-api}

使用汇编程序服务API(Java)组合多个XDP片段：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建PDF汇编程序客户端。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `AssemblerServiceClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 引用现有DDX文档。

   * 创建 `java.io.FileInputStream` 使用其构造函数并传递指定DDX文件位置的字符串值来表示DDX文档的对象。
   * 创建 `com.adobe.idp.Document` 对象，并使用其构造函数进行传递 `java.io.FileInputStream` 对象。

1. 引用XDP文档。

   * 创建 `java.util.Map` 用于通过 `HashMap` 构造函数。
   * 创建 `com.adobe.idp.Document` 对象并传递 `java.io.FileInputStream` 包含输入XDP文件的对象（对每个XDP文件重复此任务）。
   * 在 `java.util.Map` 通过调用对象 `put` 方法和传递以下参数：

      * 表示键名称的字符串值。 此值必须匹配 `source` 在DDX文档中指定的元素值（对每个XDP文件重复此任务）。
      * A `com.adobe.idp.Document` 包含与 `source` 元素（对每个XDP文件重复此任务）。

1. 设置运行时选项。

   * 创建 `AssemblerOptionSpec` 使用其构造函数存储运行时选项的对象。
   * 通过调用属于 `AssemblerOptionSpec` 对象。 例如，要指示汇编程序服务在发生错误时继续处理作业，请调用 `AssemblerOptionSpec` 对象 `setFailOnError` 方法和传递 `false`.

1. 组合多个XDP文档。

   调用 `AssemblerServiceClient` 对象 `invokeDDX` 方法，并传递以下必需值：

   * A `com.adobe.idp.Document` 表示要使用的DDX文档的对象
   * A `java.util.Map` 包含输入XDP文件的对象
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定运行时选项（包括默认字体和作业日志级别）的对象

   的 `invokeDDX` 方法返回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含已装配的XDP文档的对象。

1. 检索已装配的XDP文档。

   要获取已装配的XDP文档，请执行以下操作：

   * 调用 `AssemblerResult` 对象 `getDocuments` 方法。 此方法将返回 `java.util.Map` 对象。
   * 循环访问 `java.util.Map` 对象，直到找到结果 `com.adobe.idp.Document` 对象。
   * 调用 `com.adobe.idp.Document` 对象 `copyToFile` 提取组合XDP文档的方法。

**另请参阅**

[组装多个XDP片段](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[快速入门（SOAP模式）：使用Java API组装多个XDP片段](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)
[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API组合多个XDP片段 {#assemble-multiple-xdp-fragments-using-the-web-service-api}

使用汇编程序服务API（Web服务）组合多个XDP片段：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 在设置服务引用时，请确保使用以下WSDL定义：

   ```java
    https://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   >[!NOTE]
   >
   >替换 `localhost` 具有托管AEM Forms的服务器的IP地址。

1. 创建PDF汇编程序客户端。

   * 创建 `AssemblerServiceClient` 对象。
   * 创建 `AssemblerServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递给AEM Forms服务，例如 `https://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您无需使用 `lc_version` 属性。 在创建服务引用时，会使用此属性。
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `AssemblerServiceClient.Endpoint.Binding` 字段。 将返回值转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象 `MessageEncoding` 字段 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给 `AssemblerServiceClient.ClientCredentials.UserName.UserName` 字段。
      * 为 `AssemblerServiceClient.ClientCredentials.UserName.Password`字段。
      * 分配 `HttpClientCredentialType.Basic` 常量值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`字段。
      * 分配 `BasicHttpSecurityMode.TransportCredentialOnly` 常量值 `BasicHttpBindingSecurity.Security.Mode`字段。

1. 引用现有DDX文档。

   * 创建 `BLOB` 对象。 的 `BLOB` 对象用于存储DDX文档。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示DDX文档的文件位置以及打开文件的模式。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法。 传递字节数组、开始位置和流长度以读取。
   * 填充 `BLOB` 通过指定对象 `MTOM` 属性。

1. 引用XDP文档。

   * 对于每个输入的XDP文件，创建一个 `BLOB` 对象。 的 `BLOB` 对象用于存储输入文件。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示输入文件的文件位置和打开文件的模式。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法。 传递字节数组、开始位置和流长度以读取。
   * 填充 `BLOB` 通过指定对象 `MTOM` 字段中，显示字节数组的内容。
   * 创建 `MyMapOf_xsd_string_To_xsd_anyType` 对象。 此集合对象用于存储创建组合的XDP文档所需的输入文件。
   * 对于每个输入文件，请创建 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象。
   * 为分配表示键名称的字符串值 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象 `key` 字段。 此值必须匹配DDX文档中指定的元素值。 （对每个输入的XDP文件执行此任务。）
   * 分配 `BLOB` 将输入文件存储到 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象 `value` 字段。 （对每个输入的XDP文件执行此任务。）
   * 添加 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象 `MyMapOf_xsd_string_To_xsd_anyType` 对象。 调用 `MyMapOf_xsd_string_To_xsd_anyType` 对象 `Add` 方法和通过 `MyMapOf_xsd_string_To_xsd_anyType` 对象。 （对每个输入的XDP文档执行此任务。）

1. 设置运行时选项。

   * 创建 `AssemblerOptionSpec` 使用其构造函数存储运行时选项的对象。
   * 通过为属于 `AssemblerOptionSpec` 对象。 例如，要指示汇编程序服务在发生错误时继续处理作业，请指定 `false` 到 `AssemblerOptionSpec` 对象 `failOnError` 数据成员。

1. 组合多个XDP文档。

   调用 `AssemblerServiceClient` 对象 `invokeDDX` 方法并传递以下值：

   * A `BLOB` 表示DDX文档的对象
   * 的 `MyMapOf_xsd_string_To_xsd_anyType` 包含所需文件的对象
   * 安 `AssemblerOptionSpec` 指定运行时选项的对象

   的 `invokeDDX` 方法返回 `AssemblerResult` 包含作业结果和发生的任何例外的对象。

1. 检索已装配的XDP文档。

   要获取新创建的XDP文档，请执行以下操作：

   * 访问 `AssemblerResult` 对象 `documents` 字段， `Map` 包含生成PDF文档的对象。
   * 循环访问 `Map` 对象来获取每个生成文档。 然后，将该阵列成员的 `value` 至 `BLOB`.
   * 通过访问表示PDF文档的二进制数据 `BLOB` 对象 `MTOM` 属性。 这会返回一个字节数组，您可以将其写出到XDP文件。

**另请参阅**

[组装多个XDP片段](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
