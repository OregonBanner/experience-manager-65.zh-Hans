---
title: 处理提交的Forms
seo-title: Handling Submitted Forms
description: 使用Forms服务检索在交互式表单中输入的提交数据。 用户可以以XML、PDF和URL UTF-16格式提交表单数据。
seo-description: Use the Forms service to retrieve the submitted data entered in an interactive form. The user can submit the form data in XML, PDF, and URL UTF-16 formats.
uuid: 673b28f1-f023-4da8-a6a0-c5ff921c5f5d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3d838027-6bde-4a71-a428-4d5102f7d799
role: Developer
exl-id: 419335b2-2aae-4e83-98ff-18e61b7efa9c
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '2902'
ht-degree: 0%

---

# 处理提交的Forms {#handling-submitted-forms}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms 。**

使用户能够填写交互式表单的基于Web的应用程序要求将数据提交回服务器。 使用Forms服务，您可以检索用户在交互式表单中输入的数据。 检索数据后，您可以处理数据以满足业务要求。 例如，您可以将数据存储在数据库中，将数据发送到另一个应用程序，将数据发送到另一个服务，在表单设计中合并数据，在Web浏览器中显示数据，等等。

表单数据将作为XML或PDF数据（在设计器中设置的选项）提交到Forms服务。 以XML形式提交的表单允许您提取单个字段数据值。 即，您可以提取用户在表单中输入的每个表单字段的值。 作为PDF数据提交的表单是二进制数据，而不是XML数据。 您可以将表单另存为PDF文件，或将表单发送到其他服务。 如果要从以XML形式提交的表单中提取数据，然后使用该表单数据创建PDF文档，请调用另一个AEM Forms操作。 (请参阅 [使用提交的XML数据创建PDF文档](/help/forms/developing/creating-pdf-documents-submitted-xml.md))

下图显示了提交到名为的Java Servlet的数据 `HandleData` 从Web浏览器中显示的交互式表单。

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
   <td><p>用户填写交互式表单，然后单击该表单的“提交”按钮。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>数据提交至 <code>HandleData</code> Java Servlet作为XML数据。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>此 <code>HandleData</code> Java Servlet包含用于检索数据的应用程序逻辑。</p></td>
  </tr>
 </tbody>
</table>

## 处理提交的XML数据 {#handling-submitted-xml-data}

以XML格式提交表单数据时，您可以检索表示所提交数据的XML数据。 所有表单字段在XML架构中显示为节点。 节点值对应于用户填充的值。 考虑一个贷款表单，其中表单中的每个字段都显示为XML数据中的一个节点。 每个节点的值对应于用户填充的值。 假设用户使用下表中显示的数据填写贷款表单。

![hs_hs_loanformdata](assets/hs_hs_loanformdata.png)

下图显示了使用Forms服务客户端API检索到的相应XML数据。

![hs_hs_loandata](assets/hs_hs_loandata.png)

贷款表单中的字段。 可以使用Java XML类检索这些值。

>[!NOTE]
>
>必须在Designer中正确配置表单设计，才能将数据作为XML数据提交。 要正确配置表单设计以提交XML数据，请确保将表单设计上的提交按钮设置为提交XML数据。 有关设置“提交”按钮以提交XML数据的信息，请参见 [AEM Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63_cn).

## 处理提交的PDF数据 {#handling-submitted-pdf-data}

假定一个Web应用程序调用Forms服务。 Forms服务向客户端Web浏览器呈现交互式PDF表单后，用户填写表单并将其作为PDF数据提交回来。 当Forms服务收到PDF数据时，它可以将PDF数据发送到另一个服务或另存为PDF文件。 下图显示了应用程序的逻辑流。

![hs_hs_savingforms](assets/hs_hs_savingforms.png)

下表描述了此图中的步骤。

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
   <td><p>网页包含一个链接，该链接访问调用Forms服务的Java Servlet。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Forms服务向客户端Web浏览器呈现交互式PDF表单。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>用户填写交互式表单并单击提交按钮。 该表单将作为PDF数据提交回Forms服务。 此选项在Designer中设置。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Forms服务将PDF数据另存为PDF文件。 </p></td>
  </tr>
 </tbody>
</table>

## 处理提交的URL UTF-16数据 {#handling-submitted-url-utf-16-data}

如果表单数据作为URL UTF-16数据提交，则客户端计算机需要Adobe Reader或Acrobat 8.1或更高版本。 此外，如果表单设计包含具有URL编码数据(HTTP Post)的提交按钮，并且数据编码选项是UTF-16，则必须在文本编辑器（例如记事本）中修改表单设计。 您可以将编码选项设置为 `UTF-16LE` 或 `UTF-16BE` （对于提交按钮）。 Designer不提供此功能。

>[!NOTE]
>
>有关Forms服务的更多信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

## 步骤摘要 {#summary-of-steps}

要处理已提交的表单，请执行以下任务：

1. 包括项目文件。
1. 创建Forms客户端API对象。
1. 检索表单数据。
1. 确定表单提交是否包含文件附件。
1. 处理提交的数据。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

**创建Forms客户端API对象**

您必须先创建Forms服务客户端，然后才能以编程方式执行Forms服务客户端API操作。 如果您使用的是Java API，请创建 `FormsServiceClient` 对象。 如果您使用的是Forms Web服务API，请创建 `FormsService` 对象。

**检索表单数据**

要检索已提交的表单数据，您可以调用 `FormsServiceClient` 对象的 `processFormSubmission` 方法。 调用此方法时，您必须指定已提交表单的内容类型。 当数据从客户端Web浏览器提交到Forms服务时，它可以作为XML或PDF数据提交。 要检索输入到表单字段中的数据，可以作为XML数据提交这些数据。

您还可以通过设置以下运行时选项，从作为PDF数据提交的表单中检索表单字段：

* 将以下值传递给 `processFormSubmission` 方法作为内容类型参数： `CONTENT_TYPE=application/pdf`.
* 设置 `RenderOptionsSpec` 对象的 `PDFToXDP` 值至 `true`
* 设置 `RenderOptionsSpec` 对象的 `ExportDataFormat` 值至 `XMLData`

在调用时，您可以指定已提交表单的内容类型 `processFormSubmission` 方法。 以下列表指定了适用的内容类型值：

* **text/xml**：表示在PDF表单以XML形式提交表单数据时使用的内容类型。
* **application/x-www-form-urlencoded**：表示在HTML表单以XML形式提交数据时使用的内容类型。
* **application/pdf**：表示在PDF表单将数据作为PDF提交时使用的内容类型。

>[!NOTE]
>
>您会注意到有三个与处理提交的Forms部分相关的快速启动。 使用Java API快速入门以PDF形式提交的处理PDF forms演示了如何处理提交的PDF数据。 此快速入门中指定的内容类型为 `application/pdf`. 使用Java API快速入门以XML形式提交的处理PDF forms演示了如何处理从PDF表单提交的提交的XML数据。 此快速入门中指定的内容类型为 `text/xml`. 同样，使用Java API快速入门以XML形式提交的处理HTML表单演示了如何处理从HTML表单提交的提交的XML数据。 此快速入门中指定的内容类型为application/x-www-form-urlencoded。

您可以检索发布到Forms服务的表单数据，并确定其处理状态。 也就是说，将数据提交到Forms服务时，这并不一定意味着Forms服务已完成数据处理，数据已准备好进行处理。 例如，可以将数据提交到Forms服务，以便执行计算。 计算完成后，表单会呈现回用户并显示计算结果。 在处理提交的数据之前，建议您确定Forms服务是否已完成数据处理。

Forms服务将返回以下值，以指示它是否已完成处理数据：

* **0（提交）：** 提交的数据已准备好处理。
* **1（计算）：** Forms服务对数据执行了计算操作，必须向用户呈现结果。
* **2（验证）：** Forms服务验证了表单数据，必须将结果呈现回用户。
* **3（下一个）：** 当前页面已更改，结果必须写入客户端应用程序。
* **4(上一个**)：当前页面已更改，结果必须写入客户端应用程序。

>[!NOTE]
>
>计算和验证必须呈现回用户。 (请参阅 [计算表单数据](/help/forms/developing/calculating-form-data.md#calculating-form-data).

**确定表单提交是否包含文件附件**

提交到Forms服务的Forms可以包含文件附件。 例如，使用Acrobat的内置附件窗格，用户可以选择要与表单一起提交的文件附件。 此外，用户还可以使用随HTML文件一起呈现的HTML工具栏选择文件附件。

确定表单是否包含文件附件后，即可处理数据。 例如，可以将文件附件保存到本地文件系统。

>[!NOTE]
>
>表单必须作为PDF数据提交才能检索文件附件。 如果表单作为XML数据提交，则不会提交文件附件。

**处理提交的数据**

根据提交数据的内容类型，您可以从提交的XML数据中提取单个表单字段值，或将提交的PDF数据保存为PDF文件（或将其发送到其他服务）。 要提取单个表单字段，请将提交的XML数据转换为XML数据源，然后使用检索XML数据源值 `org.w3c.dom` 类。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服务API快速启动](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[将文档传递到Forms服务](/help/forms/developing/passing-documents-forms-service.md)

[创建可渲染Forms的Web应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API处理提交的表单 {#handle-submitted-forms-using-the-java-api}

使用Forms API (Java)处理提交的表单：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，例如adobe-forms-client.jar。

1. 创建Forms客户端API对象

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `FormsServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 检索表单数据

   * 要检索发布到Java Servlet的表单数据，请创建 `com.adobe.idp.Document` 对象通过调用其构造函数 `javax.servlet.http.HttpServletResponse` 对象的 `getInputStream` 方法。
   * 创建 `RenderOptionsSpec` 对象。 通过调用 `RenderOptionsSpec` 对象的 `setLocale` 方法，并传递一个指定区域设置值的字符串值。

   >[!NOTE]
   >
   >您可以指示FormsPDF服务通过调用 `RenderOptionsSpec` 对象的 `setPDF2XDP` 方法和传递 `true` 还致电 `setXMLData` 和传递 `true`. 然后，您可以调用 `FormsResult` 对象的 `getOutputXML` 用于检索与XDP/XML数据对应的XML数据的方法。 (此 `FormsResult` 对象由 `processFormSubmission` 方法，这将在下一个子步骤中说明。)

   * 调用 `FormsServiceClient` 对象的 `processFormSubmission` 方法并传递以下值：

      * 此 `com.adobe.idp.Document` 包含表单数据的对象。
      * 一个字符串值，它指定包含所有相关HTTP标头的环境变量。 指定要处理的内容类型。 要处理XML数据，请为此参数指定以下字符串值： `CONTENT_TYPE=text/xml`. 要处理PDF数据，请为此参数指定以下字符串值： `CONTENT_TYPE=application/pdf`.
      * 一个字符串值，它指定 `HTTP_USER_AGENT` 标头值，例如。 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. 此参数值是可选的。
      * A `RenderOptionsSpec` 存储运行时选项的对象。

     此 `processFormSubmission` 方法返回 `FormsResult` 包含表单提交结果的对象。

   * 确定Forms服务是否通过调用 `FormsResult` 对象的 `getAction` 方法。 如果此方法返回值 `0`，则数据已准备好处理。

1. 确定表单提交是否包含文件附件

   * 调用 `FormsResult` 对象的 `getAttachments` 方法。 此方法会返回 `java.util.List` 包含随表单一起提交的文件的对象。
   * 循环访问 `java.util.List` 对象以确定是否存在文件附件。 如果有文件附件，则每个元素都将 `com.adobe.idp.Document` 实例。 您可以通过调用 `com.adobe.idp.Document` 对象的 `copyToFile` 方法和传递 `java.io.File` 对象。

   >[!NOTE]
   >
   >此步骤仅适用于以PDF形式提交的表单。

1. 处理提交的数据

   * 如果数据内容类型为 `application/vnd.adobe.xdp+xml` 或 `text/xml`，创建应用程序逻辑以检索XML数据值。

      * 创建 `com.adobe.idp.Document` 对象，方法是调用 `FormsResult` 对象的 `getOutputContent` 方法。
      * 创建 `java.io.InputStream` 对象，方法是调用 `java.io.DataInputStream` 构造函数并传递 `com.adobe.idp.Document` 对象。
      * 创建 `org.w3c.dom.DocumentBuilderFactory` 对象，方法是调用静态 `org.w3c.dom.DocumentBuilderFactory` 对象的 `newInstance` 方法。
      * 创建 `org.w3c.dom.DocumentBuilder` 对象，方法是调用 `org.w3c.dom.DocumentBuilderFactory` 对象的 `newDocumentBuilder` 方法。
      * 创建 `org.w3c.dom.Document` 对象，方法是调用 `org.w3c.dom.DocumentBuilder` 对象的 `parse` 方法和传递 `java.io.InputStream` 对象。
      * 检索XML文档中每个节点的值。 完成此任务的一种方法是创建接受两个参数的自定义方法： `org.w3c.dom.Document` 对象以及要检索其值的节点的名称。 此方法返回表示节点值的字符串值。 在此流程之后的代码示例中，调用此自定义方法 `getNodeText`. 给出了该方法的正文。

   * 如果数据内容类型为 `application/pdf`，创建应用程序逻辑以将提交的PDF数据另存为PDF文件。

      * 创建 `com.adobe.idp.Document` 对象，方法是调用 `FormsResult` 对象的 `getOutputContent` 方法。
      * 创建 `java.io.File` 对象。 请确保指定PDF作为文件扩展名。
      * PDF通过调用 `com.adobe.idp.Document` 对象的 `copyToFile` 方法和传递 `java.io.File` 对象。

**另请参阅**

[快速入门（SOAP模式）：使用Java API处理以XML形式提交的PDF forms](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api)

[快速入门（SOAP模式）：使用Java API处理以XML形式提交的HTML表单](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api)

[快速入门（SOAP模式）：使用Java API处理作为PDF提交的PDF forms](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API处理提交的PDF数据 {#handle-submitted-pdf-data-using-the-web-service-api}

使用Forms API（Web服务）处理提交的表单：

1. 包含项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 将Java代理类包含在类路径中。

1. 创建Forms客户端API对象

   创建 `FormsService` 对象并设置身份验证值。

1. 检索表单数据

   * 要检索发布到Java Servlet的表单数据，请创建 `BLOB` 对象。
   * 创建 `java.io.InputStream` 对象，方法是调用 `javax.servlet.http.HttpServletResponse` 对象的 `getInputStream` 方法。
   * 创建 `java.io.ByteArrayOutputStream` 对象，其构造函数传递 `java.io.InputStream` 对象。
   * 复制 `java.io.InputStream` 对象移入 `java.io.ByteArrayOutputStream` 对象。
   * 通过调用 `java.io.ByteArrayOutputStream` 对象的 `toByteArray` 方法。
   * 填充 `BLOB` 对象(通过调用其 `setBinaryData` 方法并将字节数组作为参数传递。
   * 创建 `RenderOptionsSpec` 对象。 通过调用 `RenderOptionsSpec` 对象的 `setLocale` 方法，并传递一个指定区域设置值的字符串值。
   * 调用 `FormsService` 对象的 `processFormSubmission` 方法并传递以下值：

      * 此 `BLOB` 包含表单数据的对象。
      * 一个字符串值，它指定包含所有相关HTTP标头的环境变量。 指定要处理的内容类型。 要处理XML数据，请为此参数指定以下字符串值： `CONTENT_TYPE=text/xml`. 要处理PDF数据，请为此参数指定以下字符串值： `CONTENT_TYPE=application/pdf`.
      * 一个字符串值，它指定 `HTTP_USER_AGENT` 标头值；例如， `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * A `RenderOptionsSpec` 存储运行时选项的对象。
      * 空的 `BLOBHolder` 方法填充的对象。
      * 空的 `javax.xml.rpc.holders.StringHolder` 方法填充的对象。
      * 空的 `BLOBHolder` 方法填充的对象。
      * 空的 `BLOBHolder` 方法填充的对象。
      * 空的 `javax.xml.rpc.holders.ShortHolder` 方法填充的对象。
      * 空的 `MyArrayOf_xsd_anyTypeHolder` 方法填充的对象。 此参数用于存储与表单一起提交的文件附件。
      * 空的 `FormsResultHolder` 使用提交表单的方法填充的对象。

     此 `processFormSubmission` 方法填充 `FormsResultHolder` 带有表单提交结果的参数。

   * 确定Forms服务是否通过调用 `FormsResult` 对象的 `getAction` 方法。 如果此方法返回值 `0`，则表单数据已准备好处理。 您可以获得 `FormsResult` 对象，方法是获取 `FormsResultHolder` 对象的 `value` 数据成员。

1. 确定表单提交是否包含文件附件

   获取 `MyArrayOf_xsd_anyTypeHolder` 对象的 `value` 数据成员( `MyArrayOf_xsd_anyTypeHolder` 对象已传递到 `processFormSubmission` 方法)。 此数据成员返回的数组 `Objects`. 内的每个元素 `Object` 数组是一个 `Object`与随表单一起提交的文件相对应。 您可以获取数组中的每个元素，并将其强制转换为 `BLOB` 对象。

1. 处理提交的数据

   * 如果数据内容类型为 `application/vnd.adobe.xdp+xml` 或 `text/xml`，创建应用程序逻辑以检索XML数据值。

      * 创建 `BLOB` 对象，方法是调用 `FormsResult` 对象的 `getOutputContent` 方法。
      * 通过调用 `BLOB` 对象的 `getBinaryData` 方法。
      * 创建 `java.io.InputStream` 对象，方法是调用 `java.io.ByteArrayInputStream` 构造函数并传递字节数组。
      * 创建 `org.w3c.dom.DocumentBuilderFactory` 对象，方法是调用静态 `org.w3c.dom.DocumentBuilderFactory` 对象的 `newInstance` 方法。
      * 创建 `org.w3c.dom.DocumentBuilder` 对象，方法是调用 `org.w3c.dom.DocumentBuilderFactory` 对象的 `newDocumentBuilder` 方法。
      * 创建 `org.w3c.dom.Document` 对象，方法是调用 `org.w3c.dom.DocumentBuilder` 对象的 `parse` 方法和传递 `java.io.InputStream` 对象。
      * 检索XML文档中每个节点的值。 完成此任务的一种方法是创建接受两个参数的自定义方法： `org.w3c.dom.Document` 对象以及要检索其值的节点的名称。 此方法返回表示节点值的字符串值。 在此流程之后的代码示例中，调用此自定义方法 `getNodeText`. 给出了该方法的正文。

   * 如果数据内容类型为 `application/pdf`，创建应用程序逻辑以将提交的PDF数据另存为PDF文件。

      * 创建 `BLOB` 对象，方法是调用 `FormsResult` 对象的 `getOutputContent` 方法。
      * 通过调用 `BLOB` 对象的 `getBinaryData` 方法。
      * 创建 `java.io.File` 对象。 请确保指定PDF作为文件扩展名。
      * 创建 `java.io.FileOutputStream` 对象，使用它的构造函数传递 `java.io.File` 对象。
      * PDF通过调用 `java.io.FileOutputStream` 对象的 `write` 和传递字节数组。

**另请参阅**

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
