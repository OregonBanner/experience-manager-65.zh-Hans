---
title: 处理已提交的Forms
seo-title: 处理已提交的Forms
description: 使用Forms服务检索在交互式表单中输入的已提交数据。 用户可以提交XML、PDF和URL UTF-16格式的表单数据。
seo-description: 使用Forms服务检索在交互式表单中输入的已提交数据。 用户可以提交XML、PDF和URL UTF-16格式的表单数据。
uuid: 673b28f1-f023-4da8-a6a0-c5ff921c5f5d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3d838027-6bde-4a71-a428-4d5102f7d799
role: Developer
exl-id: 419335b2-2aae-4e83-98ff-18e61b7efa9c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2935'
ht-degree: 0%

---

# 处理已提交的Forms {#handling-submitted-forms}

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

使用户能够填写交互式表单的基于Web的应用程序需要将数据提交回服务器。 使用Forms服务，您可以检索用户在交互式表单中输入的数据。 在检索数据后，您可以处理数据以满足您的业务要求。 例如，您可以将数据存储在数据库中，将数据发送到另一个应用程序，将数据发送到另一个服务，将数据合并到表单设计中，在Web浏览器中显示数据，等等。

表单数据将以XML或PDF数据的形式提交到Forms服务，这是在Designer中设置的选项。 以XML形式提交的表单允许您提取单个字段数据值。 即，您可以提取用户在表单中输入的每个表单字段的值。 作为PDF数据提交的表单是二进制数据，而不是XML数据。 您可以将表单另存为PDF文件，或将表单发送给其他服务。 如果要从以XML形式提交的表单中提取数据，然后使用该表单数据创建PDF文档，请调用另一个AEM Forms操作。 （请参阅[使用已提交的XML数据创建PDF文档](/help/forms/developing/creating-pdf-documents-submitted-xml.md)）

下图显示了从Web浏览器中显示的交互式表单提交到名为`HandleData`的Java Servlet的数据。

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
   <td><p>用户填写交互式表单并单击表单的“提交”按钮。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>数据以XML数据的形式提交到<code>HandleData</code> Java Servlet。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p><code>HandleData</code> Java Servlet包含用于检索数据的应用程序逻辑。</p></td>
  </tr>
 </tbody>
</table>

## 处理提交的XML数据{#handling-submitted-xml-data}

将表单数据作为XML提交时，您可以检索表示已提交数据的XML数据。 所有表单字段都以节点形式显示在XML架构中。 节点值与用户填充的值相对应。 考虑使用贷款表单，其中表单中的每个字段在XML数据中显示为一个节点。 每个节点的值对应于用户填入的值。 假定用户在贷款表单中填写如下表所示的数据。

![hs_hs_loanformdata](assets/hs_hs_loanformdata.png)

下图显示了使用Forms服务客户端API检索到的相应XML数据。

![hs_hs_loandata](assets/hs_hs_loandata.png)

贷款表单中的字段。 这些值可以检索
使用Java XML类。

>[!NOTE]
>
>表单设计必须在Designer中正确配置，才能作为XML数据提交数据。 要正确配置表单设计以提交XML数据，请确保将表单设计上的“提交”按钮设置为提交XML数据。 有关设置提交按钮以提交XML数据的信息，请参阅[AEM Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)。

## 处理提交的PDF数据{#handling-submitted-pdf-data}

考虑调用Forms服务的Web应用程序。 在Forms服务将交互式PDF表单呈现到客户端Web浏览器后，用户填写表单并将其作为PDF数据提交回来。 当Forms服务收到PDF数据时，它可以将PDF数据发送到其他服务或将其另存为PDF文件。 下图显示了应用程序的逻辑流程。

![hs_hs_savforms](assets/hs_hs_savingforms.png)

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
   <td><p>网页包含一个链接，用于访问调用Forms服务的Java Servlet。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Forms服务向客户端Web浏览器呈现交互式PDF表单。</p></td>
  </tr>
  <tr>
   <td><p>1</p></td>
   <td><p>用户填写交互式表单并单击提交按钮。 表单将作为PDF数据提交回Forms服务。 此选项在Designer中设置。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Forms服务将PDF数据另存为PDF文件。 </p></td>
  </tr>
 </tbody>
</table>

## 处理提交的URL UTF-16数据{#handling-submitted-url-utf-16-data}

如果表单数据以URL UTF-16数据形式提交，则客户端计算机需要Adobe Reader或Acrobat 8.1或更高版本。 此外，如果表单设计包含具有URL编码数据(HTTP Post)的提交按钮，且数据编码选项为UTF-16，则必须在文本编辑器（如记事本）中修改表单设计。 对于提交按钮，可以将编码选项设置为`UTF-16LE`或`UTF-16BE`。 Designer不提供此功能。

>[!NOTE]
>
>有关Forms服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步骤{#summary-of-steps}的摘要

要处理提交的表单，请执行以下任务：

1. 包括项目文件。
1. 创建Forms客户端API对象。
1. 检索表单数据。
1. 确定表单提交是否包含文件附件。
1. 处理提交的数据。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建Forms客户端API对象**

您必须先创建Forms服务客户端，然后才能以编程方式执行Forms服务客户端API操作。 如果您使用的是Java API，请创建一个`FormsServiceClient`对象。 如果您使用的是Forms Web服务API，请创建一个`FormsService`对象。

**检索表单数据**

要检索提交的表单数据，请调用`FormsServiceClient`对象的`processFormSubmission`方法。 调用此方法时，必须指定提交表单的内容类型。 从客户端Web浏览器向Forms服务提交数据时，可以以XML或PDF格式提交数据。 要检索输入到表单字段中的数据，可以将数据作为XML数据提交。

您还可以通过设置以下运行时选项，从以PDF格式提交的表单中检索表单字段：

* 将以下值作为内容类型参数传递给`processFormSubmission`方法：`CONTENT_TYPE=application/pdf`。
* 将`RenderOptionsSpec`对象的`PDFToXDP`值设置为`true`
* 将`RenderOptionsSpec`对象的`ExportDataFormat`值设置为`XMLData`

调用`processFormSubmission`方法时，可指定已提交表单的内容类型。 以下列表指定了适用的内容类型值：

* **text/xml**:表示在PDF表单以XML形式提交表单数据时要使用的内容类型。
* **application/x-www-form-urlencoded**:表示在HTML表单以XML形式提交数据时要使用的内容类型。
* **application/pdf**:表示PDF表单将数据提交为PDF时要使用的内容类型。

>[!NOTE]
>
>您会注意到，有三个与处理提交的Forms部分相关的相应快速入门。 使用Java API快速入门将处理以PDF格式提交的PDF forms，演示了如何处理提交的PDF数据。 此快速入门中指定的内容类型是`application/pdf`。 使用Java API快速入门处理作为XML提交的PDF forms，演示了如何处理从PDF表单提交的已提交XML数据。 此快速入门中指定的内容类型是`text/xml`。 同样，使用Java API快速入门处理作为XML提交的HTML表单演示了如何处理从HTML表单提交的已提交XML数据。 此快速入门中指定的内容类型是application/x-www-form-urlencoded。

您可以检索发布到Forms服务的表单数据，并确定其处理状态。 即，在将数据提交到Forms服务时，它不一定意味着Forms服务已完成数据处理，并且数据已准备好进行处理。 例如，可以将数据提交到Forms服务，以便执行计算。 计算完成后，表单会呈现回用户并显示计算结果。 在处理提交的数据之前，建议您确定Forms服务是否已完成数据处理。

Forms服务会返回以下值，以指示它是否已完成数据处理：

* **0（提交）：** 已提交的数据已准备就绪，可供处理。
* **1（计算）：** Forms服务对数据执行了计算操作，结果必须呈现回用户。
* **2（验证）：** Forms服务已验证表单数据，结果必须呈现回用户。
* **3（下一步）：** 当前页面已发生更改，结果必须写入客户端应用程序。
* **4(前一个**):当前页面已发生更改，结果必须写入客户端应用程序。

>[!NOTE]
>
>计算和验证必须重新呈现给用户。 (请参阅[计算表单数据](/help/forms/developing/calculating-form-data.md#calculating-form-data)。

**确定表单提交是否包含文件附件**

Forms已提交到Forms服务可以包含文件附件。 例如，使用Acrobat的内置附件窗格，用户可以选择要与表单一起提交的文件附件。 此外，用户还可以使用通过HTML文件呈现的HTML工具栏来选择文件附件。

确定表单是否包含文件附件后，即可处理数据。 例如，可以将文件附件保存到本地文件系统。

>[!NOTE]
>
>必须以PDF数据形式提交表单，才能检索文件附件。 如果表单以XML数据形式提交，则不会提交文件附件。

**处理提交的数据**

根据已提交数据的内容类型，您可以从已提交的XML数据中提取单个表单字段值，或将已提交的PDF数据另存为PDF文件（或将其发送给其他服务）。 要提取单个表单字段，请将提交的XML数据转换为XML数据源，然后使用`org.w3c.dom`类检索XML数据源值。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API快速入门](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[将文档传递到Forms服务](/help/forms/developing/passing-documents-forms-service.md)

[创建可渲染Forms的Web应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API {#handle-submitted-forms-using-the-java-api}处理提交的表单

使用Forms API(Java)处理提交的表单：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-forms-client.jar。

1. 创建Forms客户端API对象

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用其构造函数创建`FormsServiceClient`对象，并传递`ServiceClientFactory`对象。

1. 检索表单数据

   * 要检索发布到Java Servlet的表单数据，请使用其构造函数创建`com.adobe.idp.Document`对象，并从构造函数中调用`javax.servlet.http.HttpServletResponse`对象的`getInputStream`方法。
   * 使用`RenderOptionsSpec`对象的构造函数创建对象。 通过调用`RenderOptionsSpec`对象的`setLocale`方法并传递指定区域设置值的字符串值来设置区域设置值。

   >[!NOTE]
   >
   >您可以指示Forms服务通过调用`RenderOptionsSpec`对象的`setPDF2XDP`方法并传递`true`，同时调用`setXMLData`并传递`true`，从提交的PDF内容创建XDP或XML数据。 然后，可以调用`FormsResult`对象的`getOutputXML`方法以检索与XDP/XML数据相对应的XML数据。 （`FormsResult`对象由`processFormSubmission`方法返回，有关说明，请参阅下一个子步骤。）

   * 调用`FormsServiceClient`对象的`processFormSubmission`方法并传递以下值：

      * 包含表单数据的`com.adobe.idp.Document`对象。
      * 一个字符串值，用于指定包括所有相关HTTP头的环境变量。 指定要处理的内容类型。 要处理XML数据，请为此参数指定以下字符串值：`CONTENT_TYPE=text/xml`。 要处理PDF数据，请为此参数指定以下字符串值：`CONTENT_TYPE=application/pdf`。
      * 指定`HTTP_USER_AGENT`标头值的字符串值，例如。 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. 此参数值是可选的。
      * 存储运行时选项的`RenderOptionsSpec`对象。

      `processFormSubmission`方法返回一个`FormsResult`对象，其中包含表单提交的结果。

   * 通过调用`FormsResult`对象的`getAction`方法，确定Forms服务是否已完成表单数据的处理。 如果此方法返回值`0`，则数据可供处理。



1. 确定表单提交是否包含文件附件

   * 调用`FormsResult`对象的`getAttachments`方法。 此方法会返回一个`java.util.List`对象，其中包含随表单提交的文件。
   * 遍历`java.util.List`对象，以确定是否存在文件附件。 如果存在文件附件，则每个元素都是一个`com.adobe.idp.Document`实例。 可以通过调用`com.adobe.idp.Document`对象的`copyToFile`方法并传递`java.io.File`对象来保存文件附件。

   >[!NOTE]
   >
   >仅当表单以PDF格式提交时，此步骤才适用。

1. 处理提交的数据

   * 如果数据内容类型为`application/vnd.adobe.xdp+xml`或`text/xml`，请创建应用程序逻辑以检索XML数据值。

      * 通过调用`FormsResult`对象的`getOutputContent`方法创建`com.adobe.idp.Document`对象。
      * 通过调用`java.io.DataInputStream`构造函数并传递`com.adobe.idp.Document`对象来创建`java.io.InputStream`对象。
      * 通过调用静态`org.w3c.dom.DocumentBuilderFactory`对象的`newInstance`方法创建`org.w3c.dom.DocumentBuilderFactory`对象。
      * 通过调用`org.w3c.dom.DocumentBuilderFactory`对象的`newDocumentBuilder`方法创建`org.w3c.dom.DocumentBuilder`对象。
      * 通过调用`org.w3c.dom.DocumentBuilder`对象的`parse`方法并传递`java.io.InputStream`对象来创建`org.w3c.dom.Document`对象。
      * 检索XML文档中每个节点的值。 完成此任务的一种方法是创建一个接受两个参数的自定义方法：`org.w3c.dom.Document`对象以及要检索其值的节点的名称。 此方法会返回表示节点值的字符串值。 在此过程后面的代码示例中，此自定义方法称为`getNodeText`。 此方法的正文如下。
   * 如果数据内容类型为`application/pdf`，请创建应用程序逻辑以将提交的PDF数据另存为PDF文件。

      * 通过调用`FormsResult`对象的`getOutputContent`方法创建`com.adobe.idp.Document`对象。
      * 使用其公共构造函数创建`java.io.File`对象。 请务必指定PDF作为文件扩展名。
      * 通过调用`com.adobe.idp.Document`对象的`copyToFile`方法并传递`java.io.File`对象来填充PDF文件。


**另请参阅**

[快速入门（SOAP模式）：使用Java API处理以XML形式提交的PDF forms](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api)

[快速入门（SOAP模式）：使用Java API处理以XML形式提交的HTML表单](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api)

[快速入门（SOAP模式）：使用Java API处理以PDF格式提交的PDF forms](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API {#handle-submitted-pdf-data-using-the-web-service-api}处理提交的PDF数据

使用Forms API（Web服务）处理提交的表单：

1. 包含项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 将Java代理类包含到类路径中。

1. 创建Forms客户端API对象

   创建`FormsService`对象并设置身份验证值。

1. 检索表单数据

   * 要检索发布到Java Servlet的表单数据，请使用其构造函数创建`BLOB`对象。
   * 通过调用`javax.servlet.http.HttpServletResponse`对象的`getInputStream`方法创建`java.io.InputStream`对象。
   * 使用`java.io.ByteArrayOutputStream`对象的构造函数并传递`java.io.InputStream`对象的长度，以创建该对象。
   * 将`java.io.InputStream`对象的内容复制到`java.io.ByteArrayOutputStream`对象中。
   * 通过调用`java.io.ByteArrayOutputStream`对象的`toByteArray`方法创建字节数组。
   * 通过调用`setBinaryData`方法并将字节数组作为参数进行传递来填充`BLOB`对象。
   * 使用`RenderOptionsSpec`对象的构造函数创建对象。 通过调用`RenderOptionsSpec`对象的`setLocale`方法并传递指定区域设置值的字符串值来设置区域设置值。
   * 调用`FormsService`对象的`processFormSubmission`方法并传递以下值：

      * 包含表单数据的`BLOB`对象。
      * 一个字符串值，用于指定包括所有相关HTTP头的环境变量。 指定要处理的内容类型。 要处理XML数据，请为此参数指定以下字符串值：`CONTENT_TYPE=text/xml`。 要处理PDF数据，请为此参数指定以下字符串值：`CONTENT_TYPE=application/pdf`。
      * 指定`HTTP_USER_AGENT`标头值的字符串值；例如，`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
      * 存储运行时选项的`RenderOptionsSpec`对象。
      * 由方法填充的空`BLOBHolder`对象。
      * 由方法填充的空`javax.xml.rpc.holders.StringHolder`对象。
      * 由方法填充的空`BLOBHolder`对象。
      * 由方法填充的空`BLOBHolder`对象。
      * 由方法填充的空`javax.xml.rpc.holders.ShortHolder`对象。
      * 由方法填充的空`MyArrayOf_xsd_anyTypeHolder`对象。 此参数用于存储随表单一起提交的文件附件。
      * 由方法使用提交的表单填充的空`FormsResultHolder`对象。

      `processFormSubmission`方法使用表单提交结果填充`FormsResultHolder`参数。

   * 通过调用`FormsResult`对象的`getAction`方法，确定Forms服务是否已完成表单数据的处理。 如果此方法返回值`0`，则表单数据即可进行处理。 您可以通过获取`FormsResultHolder`对象`value`数据成员的值来获取`FormsResult`对象。


1. 确定表单提交是否包含文件附件

   获取`MyArrayOf_xsd_anyTypeHolder`对象的`value`数据成员的值（`MyArrayOf_xsd_anyTypeHolder`对象已传递到`processFormSubmission`方法）。 此数据成员返回`Objects`的数组。 `Object`数组中的每个元素都是一个`Object`元素，对应于随表单一起提交的文件。 您可以获取数组中的每个元素，并将其转换为`BLOB`对象。

1. 处理提交的数据

   * 如果数据内容类型为`application/vnd.adobe.xdp+xml`或`text/xml`，请创建应用程序逻辑以检索XML数据值。

      * 通过调用`FormsResult`对象的`getOutputContent`方法创建`BLOB`对象。
      * 通过调用`BLOB`对象的`getBinaryData`方法创建字节数组。
      * 通过调用`java.io.ByteArrayInputStream`构造函数并传递字节数组来创建`java.io.InputStream`对象。
      * 通过调用静态`org.w3c.dom.DocumentBuilderFactory`对象的`newInstance`方法创建`org.w3c.dom.DocumentBuilderFactory`对象。
      * 通过调用`org.w3c.dom.DocumentBuilderFactory`对象的`newDocumentBuilder`方法创建`org.w3c.dom.DocumentBuilder`对象。
      * 通过调用`org.w3c.dom.DocumentBuilder`对象的`parse`方法并传递`java.io.InputStream`对象来创建`org.w3c.dom.Document`对象。
      * 检索XML文档中每个节点的值。 完成此任务的一种方法是创建一个接受两个参数的自定义方法：`org.w3c.dom.Document`对象以及要检索其值的节点的名称。 此方法会返回表示节点值的字符串值。 在此过程后面的代码示例中，此自定义方法称为`getNodeText`。 此方法的正文如下。
   * 如果数据内容类型为`application/pdf`，请创建应用程序逻辑以将提交的PDF数据另存为PDF文件。

      * 通过调用`FormsResult`对象的`getOutputContent`方法创建`BLOB`对象。
      * 通过调用`BLOB`对象的`getBinaryData`方法创建字节数组。
      * 使用其公共构造函数创建`java.io.File`对象。 请务必指定PDF作为文件扩展名。
      * 使用其构造函数创建`java.io.FileOutputStream`对象，并传递`java.io.File`对象。
      * 通过调用`java.io.FileOutputStream`对象的`write`方法并传递字节数组来填充PDF文件。


**另请参阅**

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
