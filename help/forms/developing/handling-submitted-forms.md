---
title: 处理提交的表单
seo-title: 处理提交的表单
description: 'null'
seo-description: 'null'
uuid: 673b28f1-f023-4da8-a6a0-c5ff921c5f5d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3d838027-6bde-4a71-a428-4d5102f7d799
translation-type: tm+mt
source-git-commit: b97452eb42275d889a82eb9364b5daf7075fcc41

---


# 处理提交的表单 {#handling-submitted-forms}

使用户能够填写交互式表单的基于Web的应用程序需要将数据提交回服务器。 使用Forms服务，您可以检索用户在交互式表单中输入的数据。 检索数据后，您可以处理数据以满足您的业务需求。 例如，您可以将数据存储在数据库中，将数据发送到另一个应用程序，将数据发送到另一个服务，将数据合并到表单设计中，在Web浏览器中显示数据，等等。

表单数据将作为XML或PDF数据提交到Forms服务，这是在Designer中设置的选项。 作为XML提交的表单使您能够提取单个字段数据值。 即，您可以提取用户在表单中输入的每个表单字段的值。 作为PDF数据提交的表单是二进制数据，而不是XML数据。 您可以将表单另存为PDF文件，或将表单发送到其他服务。 如果要从作为XML提交的表单中提取数据，然后使用表单数据创建PDF文档，请调用其他AEM表单操作。 (请参 [阅使用提交的XML数据创建PDF文档](/help/forms/developing/creating-pdf-documents-submitted-xml.md))

下图显示了从Web浏览器中显示的交互式表 `HandleData` 单提交到名为Java Servlet的数据。

![hs_hs_handlesubmit](assets/hs_hs_handlesubmit.png)

下表说明了图中的步骤。

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
   <td><p>用户填写交互式表单，然后单击表单的“提交”按钮。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>数据作为XML数据提 <code>HandleData</code> 交到Java Servlet。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Java <code>HandleData</code> Servlet包含用于检索数据的应用程序逻辑。</p></td>
  </tr>
 </tbody>
</table>

## 处理提交的XML数据 {#handling-submitted-xml-data}

当表单数据以XML形式提交时，您可以检索表示已提交数据的XML数据。 所有表单字段都显示为XML模式中的节点。 节点值与用户填写的值相对应。 考虑一个贷款表单，其中表单中的每个字段在XML数据中显示为一个节点。 每个节点的值与用户填入的值相对应。 假定用户用以下表单中显示的数据填写贷款表单。

![hs_hs_loanformdata](assets/hs_hs_loanformdata.png)

下图显示了使用Forms服务客户端API检索的相应XML数据。

![hs_hs_loandata](assets/hs_hs_loandata.png)

贷款表单中的字段。 这些值可以使用Java XML类检索。

>[!NOTE]
>
>必须在Designer中正确配置表单设计，才能将数据作为XML数据提交。 要正确配置表单设计以提交XML数据，请确保将表单设计上的“提交”按钮设置为提交XML数据。 有关设置“提交”按钮以提交XML数据的信息，请参 [阅AEM Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)。

## 处理提交的PDF数据 {#handling-submitted-pdf-data}

考虑调用Forms服务的Web应用程序。 在表单服务将交互式PDF表单呈现到客户端Web浏览器后，用户填写该表单并将其作为PDF数据提交回来。 当Forms服务收到PDF数据时，它可以将PDF数据发送到其他服务或将其另存为PDF文件。 下图显示了应用程序的逻辑流程。

![hs_hs_savingforms](assets/hs_hs_savingforms.png)

下表介绍了此图中的步骤。

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
   <td><p>网页包含访问调用Forms服务的Java Servlet的链接。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Forms服务将交互式PDF表单呈现到客户端Web浏览器。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>用户填写交互式表单并单击提交按钮。 表单将作为PDF数据提交回表单服务。 此选项在设计器中设置。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Forms服务将PDF数据保存为PDF文件。 </p></td>
  </tr>
 </tbody>
</table>

## 处理已提交的URL UTF-16数据 {#handling-submitted-url-utf-16-data}

如果表单数据以URL UTF-16数据形式提交，则客户端计算机需要Adobe Reader或Acrobat 8.1或更高版本。 此外，如果表单设计包含一个具有URL编码数据(HTTP Post)的提交按钮，且数据编码选项为UTF-16，则必须在文本编辑器（如记事本）中修改表单设计。 您可以将编码选项设置为提交 `UTF-16LE` 按钮 `UTF-16BE` 或提交按钮。 设计人员不提供此功能。

>[!NOTE]
>
>有关Forms服务的详细信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步骤摘要 {#summary-of-steps}

要处理提交的表单，请执行以下任务:

1. 包括项目文件。
1. 创建Forms Client API对象。
1. 检索表单数据。
1. 确定表单提交是否包含文件附件。
1. 处理提交的数据。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建Forms Client API对象**

在以编程方式执行Forms服务客户端API操作之前，必须先创建Forms服务客户端。 如果您使用Java API，请创建一个对 `FormsServiceClient` 象。 如果您使用的是Forms Web服务API，请创建一个对 `FormsService` 象。

**检索表单数据**

要检索提交的表单数据，请调 `FormsServiceClient` 用对象的方 `processFormSubmission` 法。 调用此方法时，您必须指定已提交表单的内容类型。 当数据从客户端Web浏览器提交到Forms服务时，它可以作为XML或PDF数据提交。 要检索输入到表单字段中的数据，可以将数据作为XML数据提交。

您还可以通过设置以下运行时选项从作为PDF数据提交的表单中检索表单字段：

* 将以下值作为内容类 `processFormSubmission` 型参数传递给方法： `CONTENT_TYPE=application/pdf`.
* 将对 `RenderOptionsSpec` 象的值设 `PDFToXDP` 置为 `true`
* 将对 `RenderOptionsSpec` 象的值设 `ExportDataFormat` 置为 `XMLData`

调用方法时，可指定已提交表单的内容类 `processFormSubmission` 型。 以下列表指定适用的内容类型值：

* **text/xml**:表示当PDF表单以XML形式提交表单数据时要使用的内容类型。
* **application/x-www-form-urlencoded**:表示当HTML表单以XML形式提交数据时要使用的内容类型。
* **application/pdf**:表示当PDF表单以PDF形式提交数据时要使用的内容类型。

>[!NOTE]
>
>您会注意到，有三个相应的快速开始与“处理提交的表单”部分相关联。 使用Java API快速开始处理作为PDF提交的PDF表单演示了如何处理提交的PDF数据。 此快速开始中指定的内容类型为 `application/pdf`。 使用Java API快速开始处理作为XML提交的PDF表单演示了如何处理从PDF表单提交的已提交XML数据。 此快速开始中指定的内容类型为 `text/xml`。 同样，使用Java API快速开始处理作为XML提交的HTML表单演示了如何处理从HTML表单提交的已提交XML数据。 此快速开始中指定的内容类型为application/x-www-form-urlencoded。

您可以检索发布到表单服务的表单数据并确定其处理状态。 即，当数据提交到Forms服务时，它不一定表示Forms服务已经完成了对数据的处理，并且数据已准备好进行处理。 例如，可以向Forms服务提交数据，以便执行计算。 计算完成后，表单将呈现回用户并显示计算结果。 在处理提交的数据之前，建议您确定Forms服务是否已完成处理数据。

Forms服务返回以下值以指示它是否已完成数据处理：

* **0（提交）:** 已提交的数据已准备好进行处理。
* **1（计算）:** Forms服务对数据执行了计算操作，结果必须呈现给用户。
* **2（验证）:** Forms服务验证的表单数据和结果必须呈现给用户。
* **3（下一个）:** 当前页面已更改，结果必须写入客户端应用程序。
* **4(前**):当前页面已更改，结果必须写入客户端应用程序。

>[!NOTE]
>
>必须将计算和验证返回给用户。 (请参阅 [计算表单数据](/help/forms/developing/calculating-form-data.md#calculating-form-data)。

**确定表单提交是否包含文件附件**

提交到Forms服务的表单可以包含文件附件。 例如，使用Acrobat的内置附件窗格，用户可以选择要与表单一起提交的文件附件。 此外，用户还可以使用HTML工具栏选择文件附件，该工具栏以HTML文件呈现。

在确定表单是否包含文件附件后，您可以处理数据。 例如，可以将文件附件保存到本地文件系统。

>[!NOTE]
>
>表单必须作为PDF数据提交，才能检索文件附件。 如果表单以XML数据形式提交，则不会提交文件附件。

**处理提交的数据**

根据提交数据的内容类型，您可以从提交的XML数据中提取单个表单字段值，或将提交的PDF数据另存为PDF文件（或将其发送到其他服务）。 要提取单个表单字段，请将提交的XML数据转换为XML数据源，然后使用类检索XML数据源 `org.w3c.dom` 值。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API快速开始](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[将文档传递到Forms服务](/help/forms/developing/passing-documents-forms-service.md)

[创建呈现表单的Web 应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API处理提交的表单 {#handle-submitted-forms-using-the-java-api}

使用Forms API(Java)处理提交的表单：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-forms-client.jar。

1. 创建Forms Client API对象

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `FormsServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 检索表单数据

   * 要检索发布到Java Servlet的表单数据，请使用对象的构造函数 `com.adobe.idp.Document` ，并从构造函数中调用该对 `javax.servlet.http.HttpServletResponse` 象的 `getInputStream` 方法来创建对象。
   * 使用对 `RenderOptionsSpec` 象的构造函数创建对象。 通过调用对象的方法并传 `RenderOptionsSpec` 递指定区 `setLocale` 域设置值的字符串值来设置区域设置值。
   >[!NOTE]
   >
   >您可以通过调用对象的方法、传递以及调用和传递，指示Forms服务从提交的PDF内 `RenderOptionsSpec` 容创建XDP或XML `setPDF2XDP` 数据 `true``setXMLData``true`。 然后，可以调 `FormsResult` 用对象的 `getOutputXML` 方法来检索与XDP/XML数据对应的XML数据。 (对 `FormsResult` 象由方法返回， `processFormSubmission` 将在下一个子步骤中说明。)

   * 调用对 `FormsServiceClient` 象的方 `processFormSubmission` 法并传递以下值：

      * 包 `com.adobe.idp.Document` 含表单数据的对象。
      * 一个字符串值，它指定包括所有相关HTTP头的环境变量。 指定要处理的内容类型。 要处理XML数据，请为此参数指定以下字符串值： `CONTENT_TYPE=text/xml`. 要处理PDF数据，请为此参数指定以下字符串值： `CONTENT_TYPE=application/pdf`.
      * 一个字符串值，它指 `HTTP_USER_AGENT` 定标题值，例如，。 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. 此参数值是可选的。
      * 存 `RenderOptionsSpec` 储运行时选项的对象。
      该方 `processFormSubmission` 法返回一个 `FormsResult` 包含表单提交结果的对象。

   * 确定表单服务是否已通过调用对象的方法完 `FormsResult` 成对表单数据的处 `getAction` 理。 如果此方法返回值， `0`则数据即可被处理。



1. 确定表单提交是否包含文件附件

   * 调用 `FormsResult` 对象的方 `getAttachments` 法。 此方法返回一 `java.util.List` 个对象，该对象包含随表单一起提交的文件。
   * 遍历对象 `java.util.List` 以确定是否存在文件附件。 如果存在文件附件，则每个元素都是一个 `com.adobe.idp.Document` 实例。 可以通过调用对象的方法并传递对 `com.adobe.idp.Document` 象来保存 `copyToFile` 文件附件 `java.io.File` 。
   >[!NOTE]
   >
   >此步骤仅在表单以PDF形式提交时适用。

1. 处理提交的数据

   * 如果数据内容类型是或， `application/vnd.adobe.xdp+xml` 请创 `text/xml`建应用程序逻辑以检索XML数据值。

      * 通过 `com.adobe.idp.Document` 调用对象的方 `FormsResult` 法创建对 `getOutputContent` 象。
      * 通过调 `java.io.InputStream` 用构造函数并传递对 `java.io.DataInputStream` 象来创建对 `com.adobe.idp.Document` 象。
      * 通过 `org.w3c.dom.DocumentBuilderFactory` 调用静态对象的方 `org.w3c.dom.DocumentBuilderFactory` 法创建对 `newInstance` 象。
      * 通过 `org.w3c.dom.DocumentBuilder` 调用对象的方 `org.w3c.dom.DocumentBuilderFactory` 法创建对 `newDocumentBuilder` 象。
      * 通过调 `org.w3c.dom.Document` 用对象的方 `org.w3c.dom.DocumentBuilder` 法并传递对 `parse` 象来创建对 `java.io.InputStream` 象。
      * 检索XML文档中每个节点的值。 实现此任务的一种方法是创建一个接受两个参数的自定义方法：对象 `org.w3c.dom.Document` 以及要检索其值的节点的名称。 此方法返回表示节点值的字符串值。 在此过程后面的代码示例中，调用了此自定义方法 `getNodeText`。 本文给出了该方法的主体。
   * 如果数据内容类型为，则 `application/pdf`创建应用程序逻辑以将提交的PDF数据另存为PDF文件。

      * 通过 `com.adobe.idp.Document` 调用对象的方 `FormsResult` 法创建对 `getOutputContent` 象。
      * 使用对 `java.io.File` 象的公共构造函数创建对象。 请务必指定PDF作为文件扩展名。
      * 通过调用对象的方法并 `com.adobe.idp.Document` 传递对象 `copyToFile` 来填充PDF `java.io.File` 文件。


**另请参阅**

[快速开始（SOAP模式）:使用Java API处理作为XML提交的PDF表单](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api)

[快速开始（SOAP模式）:使用Java API处理作为XML提交的HTML表单](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api)

[快速开始（SOAP模式）:使用Java API处理作为PDF提交的PDF表单](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API处理提交的PDF数据 {#handle-submitted-pdf-data-using-the-web-service-api}

使用Forms API（Web服务）处理提交的表单：

1. 包括项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 将Java代理类包含到类路径中。

1. 创建Forms Client API对象

   创建对 `FormsService` 象并设置身份验证值。

1. 检索表单数据

   * 要检索发布到Java Servlet的表单数据，请使用其构 `BLOB` 造函数创建一个对象。
   * 通过 `java.io.InputStream` 调用对象的方 `javax.servlet.http.HttpServletResponse` 法创建对 `getInputStream` 象。
   * 使用 `java.io.ByteArrayOutputStream` 对象的构造函数并传递对象的长 `java.io.InputStream` 度。
   * 将对象的内 `java.io.InputStream` 容复制到对 `java.io.ByteArrayOutputStream` 象中。
   * 通过调用对象的方法 `java.io.ByteArrayOutputStream` 创建字节数 `toByteArray` 组。
   * 通过调 `BLOB` 用对象的方法并将字 `setBinaryData` 节数组作为参数进行传递来填充对象。
   * 使用对 `RenderOptionsSpec` 象的构造函数创建对象。 通过调用对象的方法并传 `RenderOptionsSpec` 递指定区 `setLocale` 域设置值的字符串值来设置区域设置值。
   * 调用对 `FormsService` 象的方 `processFormSubmission` 法并传递以下值：

      * 包 `BLOB` 含表单数据的对象。
      * 一个字符串值，它指定包括所有相关HTTP头的环境变量。 指定要处理的内容类型。 要处理XML数据，请为此参数指定以下字符串值： `CONTENT_TYPE=text/xml`. 要处理PDF数据，请为此参数指定以下字符串值： `CONTENT_TYPE=application/pdf`.
      * 指定标题值的字 `HTTP_USER_AGENT` 符串值；例如， `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
      * 存 `RenderOptionsSpec` 储运行时选项的对象。
      * 由方 `BLOBHolder` 法填充的空对象。
      * 由方 `javax.xml.rpc.holders.StringHolder` 法填充的空对象。
      * 由方 `BLOBHolder` 法填充的空对象。
      * 由方 `BLOBHolder` 法填充的空对象。
      * 由方 `javax.xml.rpc.holders.ShortHolder` 法填充的空对象。
      * 由方 `MyArrayOf_xsd_anyTypeHolder` 法填充的空对象。 此参数用于存储随表单一起提交的文件附件。
      * 由方 `FormsResultHolder` 法填充的空对象，其中包含提交的表单。
      该方 `processFormSubmission` 法使用表 `FormsResultHolder` 单提交的结果填充该参数。

   * 确定表单服务是否已通过调用对象的方法完 `FormsResult` 成对表单数据的处 `getAction` 理。 如果此方法返回值， `0`表单数据就可以被处理了。 可以通过获 `FormsResult` 取对象数据成员的 `FormsResultHolder` 值来获取 `value` 对象。


1. 确定表单提交是否包含文件附件

   获取对象数 `MyArrayOf_xsd_anyTypeHolder` 据成员的 `value` 值(对象已 `MyArrayOf_xsd_anyTypeHolder` 传递给方法 `processFormSubmission` )。 此数据成员返回一组 `Objects`。 数组中的每个 `Object` 元素都与 `Object`随表单一起提交的文件相对应。 您可以获取数组中的每个元素并将其转换为对 `BLOB` 象。

1. 处理提交的数据

   * 如果数据内容类型是或， `application/vnd.adobe.xdp+xml` 请创 `text/xml`建应用程序逻辑以检索XML数据值。

      * 通过 `BLOB` 调用对象的方 `FormsResult` 法创建对 `getOutputContent` 象。
      * 通过调用对象的方法 `BLOB` 创建字节数 `getBinaryData` 组。
      * 通过调 `java.io.InputStream` 用构造函数并传递字 `java.io.ByteArrayInputStream` 节数组来创建对象。
      * 通过 `org.w3c.dom.DocumentBuilderFactory` 调用静态对象的方 `org.w3c.dom.DocumentBuilderFactory` 法创建对 `newInstance` 象。
      * 通过 `org.w3c.dom.DocumentBuilder` 调用对象的方 `org.w3c.dom.DocumentBuilderFactory` 法创建对 `newDocumentBuilder` 象。
      * 通过调 `org.w3c.dom.Document` 用对象的方 `org.w3c.dom.DocumentBuilder` 法并传递对 `parse` 象来创建对 `java.io.InputStream` 象。
      * 检索XML文档中每个节点的值。 实现此任务的一种方法是创建一个接受两个参数的自定义方法：对象 `org.w3c.dom.Document` 以及要检索其值的节点的名称。 此方法返回表示节点值的字符串值。 在此过程后面的代码示例中，调用了此自定义方法 `getNodeText`。 本文给出了该方法的主体。
   * 如果数据内容类型为，则 `application/pdf`创建应用程序逻辑以将提交的PDF数据另存为PDF文件。

      * 通过 `BLOB` 调用对象的方 `FormsResult` 法创建对 `getOutputContent` 象。
      * 通过调用对象的方法 `BLOB` 创建字节数 `getBinaryData` 组。
      * 使用对 `java.io.File` 象的公共构造函数创建对象。 请务必指定PDF作为文件扩展名。
      * 使用对 `java.io.FileOutputStream` 象的构造函数并传递该对象来创建 `java.io.File` 对象。
      * 通过调用对象的方法并 `java.io.FileOutputStream` 传递字节数 `write` 组来填充PDF文件。


**另请参阅**

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)