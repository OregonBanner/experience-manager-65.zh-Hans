---
title: 使用已提交的XML数据创建PDF文档
seo-title: 使用已提交的XML数据创建PDF文档
description: 'null'
seo-description: 'null'
uuid: 2676c614-8988-451b-ac7c-bd07731a3f5f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 62490230-a24e-419d-95bb-c0bb04a03f96
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用提交的XML数据创建PDF文档 {#creating-pdf-documents-with-submittedxml-data}

## 使用提交的XML数据创建PDF文档 {#creating-pdf-documents-with-submitted-xml-data}

使用户能够填写交互式表单的基于Web的应用程序需要将数据提交回服务器。 使用Forms服务，您可以检索用户在交互式表单中输入的表单数据。 然后，您可以将表单数据传递到其他AEM Forms服务操作，并使用该数据创建PDF文档。

>[!NOTE]
>
>在阅读此内容之前，建议您对处理已提交表单有深入的了解。 处理提交的表单中介绍了表单设计和提交的XML数据之间的关系等概念。

请考虑以下涉及三个AEM Forms服务的工作流：

* 用户从基于Web的应用程序将XML数据提交到Forms服务。
* 表单服务用于处理提交的表单和提取表单字段。 可以处理表单数据。 例如，可以将数据提交到企业数据库。
* 表单数据将发送到输出服务以创建非交互式PDF文档。
* 非交互式PDF文档存储在Content Services（已弃用）中。

下图提供了此工作流的可视化表示形式。

![cd_cd_finsrv_architecture_xml_pdf1](assets/cd_cd_finsrv_architecture_xml_pdf1.png)

用户从客户端Web浏览器提交表单后，非交互式PDF文档将存储在Content Services（已弃用）中。 下图显示了Content services中存储的PDF文档（已弃用）。

![cd_cd_cs_gui](assets/cd_cd_cs_gui.png)

### 步骤摘要 {#summary-of-steps}

要使用提交的XML数据创建非交互式PDF文档并存储在Content services的PDF文档中（已弃用），请执行以下任务：

1. 包括项目文件。
1. 创建表单、输出和文档管理对象。
1. 使用Forms服务检索表单数据。
1. 使用“输出”服务创建非交互式PDF文档。
1. 使用文档管理服务将PDF表单存储在Content Services（已弃用）中。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建表单、输出和文档管理对象**

在以编程方式执行Forms服务API操作之前，请先创建Forms Client API对象。 同样，由于此工作流调用输出和文档管理服务，因此请创建输出客户端API对象和文档管理客户端API对象。

**使用Forms服务检索表单数据**

检索已提交到表单服务的表单数据。 您可以处理提交的数据以满足您的业务需求。 例如，您可以将表单数据存储在企业数据库中。 但是，要创建非交互式PDF文档，表单数据会传递到“输出”服务。

**使用“输出”服务创建非交互式PDF文档。**

使用“输出”服务创建基于表单设计和XML表单数据的非交互式PDF文档。 在工作流中，从Forms服务检索表单数据。

**使用文档管理服务在Content Services（已弃用）中存储PDF表单**

使用Document Management服务API在Content Services（已弃用）中存储PDF文档。

**另请参阅**

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API快速入门](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

### 使用Java API使用提交的XML数据创建PDF文档 {#create-a-pdf-document-with-submitted-xml-data-using-the-java-api}

使用Forms、Output和Document Management API(Java)创建包含提交的XML数据的PDF文档：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-forms-client.jar、adobe-output-client.jar和adobe-contentservices-client.jar。

1. 创建表单、输出和文档管理对象

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `FormsServiceClient` 象的构造函数并传递该对象来创建 `ServiceClientFactory` 对象。
   * 使用对 `OutputClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。
   * 使用对 `DocumentManagementServiceClientImpl` 象的构造函数并传递该对象来创建 `ServiceClientFactory` 对象。

1. 使用Forms服务检索表单数据

   * 调用对 `FormsServiceClient` 象的方 `processFormSubmission` 法并传递以下值：

      * 包 `com.adobe.idp.Document` 含表单数据的对象。
      * 一个字符串值，它指定环境变量，包括所有相关的HTTP头。 通过为环境变量指定一个或多个值，指定要处理的内 `CONTENT_TYPE` 容类型。 例如，要处理XML数据，请为此参数指定以下字符串值： `CONTENT_TYPE=text/xml`.
      * 指定标题值的 `HTTP_USER_AGENT` 字符串值，如 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
      * 存 `RenderOptionsSpec` 储运行时选项的对象。
      该方 `processFormSubmission` 法返回一个 `FormsResult` 包含表单提交结果的对象。

   * 确定表单服务是否已通过调用对象的方法完 `FormsResult` 成对表单数据的处 `getAction` 理。 如果此方法返回值， `0`则数据即可被处理。
   * 通过调用对象的方 `com.adobe.idp.Document` 法创建对象来 `FormsResult` 检索表单 `getOutputContent` 数据。 （此对象包含可发送到输出服务的表单数据。）
   * 通过调 `java.io.InputStream` 用构造函数并传递对 `java.io.DataInputStream` 象来创建对 `com.adobe.idp.Document` 象。
   * 通过 `org.w3c.dom.DocumentBuilderFactory` 调用静态对象的方 `org.w3c.dom.DocumentBuilderFactory` 法创建对 `newInstance` 象。
   * 通过 `org.w3c.dom.DocumentBuilder` 调用对象的方 `org.w3c.dom.DocumentBuilderFactory` 法创建对 `newDocumentBuilder` 象。
   * 通过调 `org.w3c.dom.Document` 用对象的方 `org.w3c.dom.DocumentBuilder` 法并传递对 `parse` 象来创建对 `java.io.InputStream` 象。
   * 检索XML文档中每个节点的值。 完成此任务的一种方法是创建一个接受两个参数的自定义方法：对象 `org.w3c.dom.Document` 以及要检索其值的节点的名称。 此方法返回表示节点值的字符串值。 在此过程后面的代码示例中，调用了此自定义方法 `getNodeText`。 本文给出了该方法的主体。


1. 使用“输出”服务创建非交互式PDF文档。

   通过调用对象的方法并传 `OutputClient` 递以下值 `generatePDFOutput` 来创建PDF文档：

   * 枚举 `TransformationFormat` 值。 要生成PDF文档，请指定 `TransformationFormat.PDF`。
   * 指定表单设计名称的字符串值。 确保表单设计与从Forms服务检索的表单数据兼容。
   * 一个字符串值，它指定表单设计所在的内容根目录。
   * 包 `PDFOutputOptionsSpec` 含PDF运行时选项的对象。
   * 包含 `RenderOptionsSpec` 渲染运行时选项的对象。
   * 包 `com.adobe.idp.Document` 含XML数据源的对象，该数据源包含要与表单设计合并的数据。 确保对象的方法返回 `FormsResult` 了此对 `getOutputContent` 象。
   * 该方 `generatePDFOutput` 法返回一 `OutputResult` 个包含操作结果的对象。
   * 通过调用对象的方法检索非交 `OutputResult` 互式PDF文 `getGeneratedDoc` 档。 此方法返回 `com.adobe.idp.Document` 表示非交互式PDF文档的实例。

1. 使用文档管理服务在Content Services（已弃用）中存储PDF表单

   通过调用对象的方 `DocumentManagementServiceClientImpl` 法并传递 `storeContent` 以下值来添加内容：

   * 一个字符串值，它指定添加内容的商店。 默认存储为 `SpacesStore`。 此值是必需参数。
   * 一个字符串值，它指定添加内容的空间的完全限定路径(例如， `/Company Home/Test Directory`)。 此值是必需参数。
   * 表示新内容的节点名称(例如， `MortgageForm.pdf`)。 此值是必需参数。
   * 指定节点类型的字符串值。 要添加新内容（如PDF文件），请指定 `{https://www.alfresco.org/model/content/1.0}content`。 此值是必需参数。
   * 表示 `com.adobe.idp.Document` 内容的对象。 此值是必需参数。
   * 一个字符串值，它指定编码值(例如， `UTF-8`)。 此值是必需参数。
   * 一个 `UpdateVersionType` 枚举值，它指定如何处理版本信息(例如， `UpdateVersionType.INCREMENT_MAJOR_VERSION` 增加内容版本)。 )此值是必需参数。
   * 一个 `java.util.List` 实例，它指定与内容相关的方面。 此值是可选参数，您可以指定 `null`。
   * 存储 `java.util.Map` 内容属性的对象。
   该方 `storeContent` 法返回一个 `CRCResult` 描述内容的对象。 例如， `CRCResult` 使用对象，您可以获取内容的唯一标识符值。 要执行此任务，请调 `CRCResult` 用对象的方 `getNodeUuid` 法。

**另请参阅**

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
