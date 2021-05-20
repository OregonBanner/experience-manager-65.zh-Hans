---
title: 使用AEM Forms存储库
seo-title: 使用AEM Forms存储库
description: 管理AEM Forms存储库，以使用Java API和Web服务API创建文件夹、写入、列表、读取、更新和搜索资源。 此外，了解如何创建资源关系、锁定和删除资源。
seo-description: 管理AEM Forms存储库，以使用Java API和Web服务API创建文件夹、写入、列表、读取、更新资源和搜索资源。 此外，了解如何创建资源关系、锁定和删除资源。
uuid: 6ead49f9-ca0d-4ee4-86a6-0a9ced6ec4f8
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d2c95881-6c02-4e34-85af-84607df54287
role: Developer
exl-id: a07e51ca-fea0-4719-8071-1b7e805de2ae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '9157'
ht-degree: 0%

---

# 使用AEM Forms存储库{#working-with-aem-forms-repository}

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

**关于存储库服务**

存储库服务向AEM Forms提供资源存储和管理服务。 当开发人员创建&#x200B;*AEM Forms*&#x200B;应用程序时，他们可以在存储库中部署资产，而不是文件系统。 资产可以包含任何类型的宣传资料，包括XML表单、PDF forms(包括Acrobat表单)、表单片段、图像、配置文件、策略、SWF文件、DDX文件、XML架构、WSDL文件和测试数据。

例如，请考虑以下名为&#x200B;*Applications/FormsApplication*&#x200B;的Forms应用程序：

![ww_ww_formrepository](assets/ww_ww_formrepository.png)

请注意， FormsFolder中有一个名为Loan.xdp的文件。 要访问此表单设计，请指定完整路径（包括版本）：`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。

>[!NOTE]
>
>有关使用Workbench创建Forms应用程序的信息，请参阅[Workbench帮助](https://www.adobe.com/go/learn_aemforms_workbench_63)。

位于AEM Forms存储库中的资源的路径是：

`Applications/Application-name/Application-version/Folder.../Filename`

以下值显示一些URI值示例：

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

>[!NOTE]
>
>您可以使用Web浏览器浏览AEM Forms存储库。 要浏览存储库，请在Web浏览器中输入以下URL`https://[server name]:[server port]/repository`。 您可以使用Web浏览器验证与使用AEM Forms存储库部分关联的快速启动结果。 例如，如果向AEM Forms存储库添加内容，则可以在Web浏览器中查看该内容。 (请参阅[快速入门（SOAP模式）：使用Java API](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)编写资源。)

存储库API提供了许多操作，可用于存储和检索来自存储库的信息。 例如，在处理应用程序时需要某个资源时，您可以获取资源列表或检索存储在存储库中的特定资源。

>[!NOTE]
>
>存储库API无法用于与Content Services进行交互（已弃用）。 要与内容服务进行交互（已弃用），请使用文档管理API。

使用存储库服务API，您可以完成以下任务：

* 创建文件夹。 请参阅[创建文件夹](aem-forms-repository.md#creating-folders)。
* 编写资源及其属性。 请参阅[编写资源](aem-forms-repository.md#writing-resources)。
* 列出给定集合中的资源或与其他资源相关的资源。 请参阅[列出资源](aem-forms-repository.md#listing-resources)。
* 读取资源及其属性。 请参阅[读取资源](aem-forms-repository.md#reading-resources)。
* 更新资源及其属性。 请参阅[更新资源](aem-forms-repository.md#updating-resources)。
* 搜索资源，包括其历史记录、相关资源和属性。 请参阅[搜索资源](aem-forms-repository.md#searching-for-resources)。
* 指定资源之间的关系。 请参阅[创建资源关系](aem-forms-repository.md#creating-resource-relationships)。
* 管理资源访问控制，包括锁定和解锁资源，以及读取和写入访问控制列表(ACL)。 请参阅[锁定资源](aem-forms-repository.md#locking-resources)。
* 删除资源及其属性。 请参阅[删除资源](aem-forms-repository.md#deleting-resources)。

>[!NOTE]
>
>使用存储库API，您无法使用ECM存储库管理资源访问控制、搜索资源或指定资源关系。

>[!NOTE]
>
>将加密的PDF写入存储库后，将无法使用自动关系提取功能。 否则，加密的PDF可以存储在存储库中，稍后进行检索。 在从存储库检索PDF后，检索器可以选择解密该PDF。

>[!NOTE]
>
>有关Repository服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 创建文件夹{#creating-folders}

文件夹（资源集合）用于按有组织的分组存储对象（文件或资源）。 文件夹可以包含资源和其他文件夹，也称为子文件夹。 资源一次只能存储在一个文件夹中。

文件会从文件夹继承访问控制列表(ACL)，子文件夹会从其父文件夹继承ACL。 因此，在创建子文件夹之前，父文件夹必须存在。 IDE仅允许您逐个文件夹进行交互，而不允许逐个文件进行交互。 无法对文件夹进行版本更改，因此无需这样做；文件夹本身不包含数据。 相反，它只是包含数据的资源容器。 默认ACL是系统级权限，这意味着用户必须具有系统级权限（读取、写入、遍历、管理ACL），直到有人授予他们对特定文件夹的权限。 ACL仅在IDE中工作。

>[!NOTE]
>
>有关Repository服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary-of-steps}的摘要

要创建文件夹，请执行以下步骤：

1. 包括项目文件。
1. 创建服务客户端。
1. 创建文件夹。
1. 将文件夹写入存储库。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请包含代理文件。

**创建服务客户端**

在以编程方式创建资源集合之前，必须建立连接并提供凭据。 这是通过创建服务客户端来完成的。

**创建文件夹**

调用存储库服务方法以创建资源集合，并使用标识信息（包括其UUID、文件夹名称和描述）填充资源集合。

**将文件夹写入存储库**

调用存储库服务方法以写入资源集合，并指定目标文件夹的URI。

**另请参阅**

[使用Java API创建文件夹](aem-forms-repository.md#create-folders-using-the-java-api)

[使用Web服务API创建文件夹](aem-forms-repository.md#create-folders-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速入门](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API {#create-folders-using-the-java-api}创建文件夹

使用存储库服务API(Java)创建文件夹：

1. 包含项目文件

   将项目文件包含在您Java项目的类路径中。

1. 创建服务客户端

   使用其构造函数创建`ResourceRepositoryClient`对象，并传递包含连接属性的`ServiceClientFactory`对象。

1. 创建文件夹

   要创建资源集合，必须先创建`com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean`对象。

   调用`repositoryInfomodelFactoryBean`对象的`newResourceCollection`方法，并传入以下参数：

   * 要分配给资源的`com.adobe.repository.infomodel.Id` UUID标识符。
   * 要分配给资源的`com.adobe.repository.infomodel.Lid` UUID标识符。
   * 包含资源集合名称的`java.lang.String`。 例如，`FormsFolder`。

   方法会返回表示新文件夹的`com.adobe.repository.infomodel.bean.ResourceCollection`对象。

   使用`setDescription`方法设置文件夹的描述，并传入以下参数：

   * 描述资源集合的`String`。 在本例中，使用`"test Folder"` `.`


1. 将文件夹写入存储库

   调用`ResourceRepositoryClient`对象的`writeResource`方法，并在文件夹和`ResourceCollection`对象的URI中传递。 例如，文件夹的URI可以是以下值`/Applications/FormsApplication/1.0/`。

   方法会返回新创建的`com.adobe.repository.infomodel.bean.Resource`对象的实例。 例如，您可以通过调用`com.adobe.repository.infomodel.bean.Resource`对象的`getId`方法来检索新资源的标识符值。

**另请参阅**

[创建文件夹](aem-forms-repository.md#creating-folders)

[快速入门（SOAP模式）：使用Java API创建文件夹](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#create-folders-using-the-web-service-api}创建文件夹

使用存储库服务API（Web服务）创建文件夹：

1. 包含项目文件

   * 使用base64创建使用存储库WSDL的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用其默认构造函数创建`RepositoryServiceService`对象。 使用包含用户名和密码的`System.Net.NetworkCredential`对象设置其`Credentials`属性。

1. 创建文件夹

   使用`ResourceCollection`类的默认构造函数创建文件夹，并传入以下参数：

   * `Id`对象，通过调用`Id`类的默认构造函数来创建该对象，并将其分配给`Resource`对象的`id`字段。
   * `Lid`对象，通过调用`Lid`类的默认构造函数来创建该对象，并将其分配给`Resource`对象的`lid`字段。
   * 包含资源集合名称的字符串，该名称被分配给`Resource`对象的`name`字段。 此示例中使用的名称为`"testfolder"`。
   * 包含资源集合描述的字符串，该描述被分配给`Resource`对象的`description`字段。 此示例中使用的描述为`"test folder"`。

1. 将文件夹写入存储库

   调用`RepositoryServiceService`对象的`writeResource`方法并传入以下参数：

   * 创建文件夹的路径。
   * 表示文件夹的`ResourceCollection`对象。
   * 传递`null`以获取其他两个参数。

**另请参阅**

[创建文件夹](aem-forms-repository.md#creating-folders)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 编写资源{#writing-resources}

您可以在存储库的给定位置创建资源。 自然文件大小受数据库限制和会话超时的限制。 对于默认配置，文件长度限制为25 MB。 要提高或降低最大文件大小，必须更改数据库配置。

写入资源等同于在存储库中存储数据。 将资源写入存储库后，存储库生态系统中的所有客户端都可以访问该资源。 将资源（如XML架构、XDP文件和XSD文件）写入存储库时，将根据MIME类型分析内容。 如果支持MIME类型，则解析器会确定是否与其他内容存在隐含关系。 例如，如果级联样式表(CSS)具有引用通用CSS的相对URL，则您也应将通用CSS提交到存储库。 两个资源之间的关系被存储为30天的不可调整期间的挂起关系。 在30天内将通用CSS提交到存储库时，将形成关系。

创建资源时，访问控制列表(ACL)将继承自父文件夹。 在创建初始资源或文件夹之前，根文件夹具有系统级别的权限，此时该资源或文件夹会获得默认的ACL权限。

您可以使用存储库服务Java API或Web服务API以编程方式写入资源。

>[!NOTE]
>
>有关Repository服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-1}的摘要

要编写资源，请执行以下步骤：

1. 包括项目文件。
1. 创建存储库服务客户端。
1. 指定要读取的资源的URI。
1. 读取资源。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请包含代理文件。

**创建服务客户端**

在以编程方式读取资源之前，必须建立连接并提供凭据。 这是通过创建服务客户端来完成的。

**为资源指定目标文件夹的URI**

创建包含要读取的资源URI的字符串。 语法包括正斜杠，如以下示例所示：&quot;/*path*/*folder*&quot;。

**创建资源**

调用存储库服务方法以创建资源，并使用标识信息（包括其UUID、资源名称和描述）填充资源。

**指定资源内容**

调用存储库服务方法以创建资源内容，并将该内容存储在资源中。

**将资源写入目标文件夹**

调用存储库服务方法以写入资源，并指定目标文件夹的URI。

**另请参阅**

[使用Java API写入资源](aem-forms-repository.md#write-resources-using-the-java-api)

[使用Web服务API写入资源](aem-forms-repository.md#write-resources-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速入门](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API {#write-resources-using-the-java-api}写入资源

使用存储库服务API(Java)编写资源：

1. 包含项目文件

   将客户端JAR文件包含在您Java项目的类路径中。

1. 创建服务客户端

   使用其构造函数创建`ResourceRepositoryClient`对象，并传递包含连接属性的`ServiceClientFactory`对象。

1. 为资源指定目标文件夹的URI

   为资源指定目标文件夹的URI。 在这种情况下，由于名为`testResource`的资源将存储在名为`testFolder`的文件夹中，因此该文件夹的URI为`"/testFolder"`。 URI将存储为`java.lang.String`对象。

1. 创建资源

   要创建资源，必须先创建`com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean`对象。

   调用`RepositoryInfomodelFactoryBean`对象的`newResource`方法，该方法将创建`com.adobe.repository.infomodel.bean.Resource`对象。 在本例中，提供了以下参数：

   * `com.adobe.repository.infomodel.Id`对象，通过为`Id`类调用默认构造函数来创建。
   * `com.adobe.repository.infomodel.Lid`对象，通过为`Lid`类调用默认构造函数来创建。
   * 包含资源文件名的`java.lang.String`。

   要指定资源的描述，请调用`Resource`对象的`setDescription`方法，并传递包含该描述的字符串。 在本例中，描述为`"test resource"`。

1. 指定资源内容

   要为资源创建内容，请调用`RepositoryInfomodelFactoryBean`对象的`newResourceContent`方法，该方法将返回`com.adobe.repository.infomodel.bean.ResourceContent`对象。 向`ResourceContent`对象添加内容。 在本例中，可通过执行以下任务来完成此操作：

   * 调用`ResourceContent`对象的`setDataDocument`方法并传入`com.adobe.idp.Document`对象
   * 调用`ResourceContent`对象的`setSize`方法并传入`Document`对象的大小（以字节为单位）

   通过调用`Resource`对象的`setContent`方法并传入`ResourceContent`对象，将内容添加到资源中。 有关更多信息，请参阅[AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

1. 将资源写入目标文件夹

   调用`ResourceRepositoryClient`对象的`writeResource`方法，并在文件夹的URI以及`Resource`对象中传递。

**另请参阅**

[编写资源](aem-forms-repository.md#writing-resources)

[快速入门（SOAP模式）：使用Java API编写资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#write-resources-using-the-web-service-api}写入资源

使用存储库服务API（Web服务）写入资源：

1. 包含项目文件

   * 使用base64创建使用存储库WSDL的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用其默认构造函数创建`RepositoryServiceService`对象。 使用包含用户名和密码的`System.Net.NetworkCredential`对象设置其`Credentials`属性。

1. 为资源指定目标文件夹的URI

   为资源指定目标文件夹的URI。 在这种情况下，由于名为`testResource`的资源将存储在名为`testFolder`的文件夹中，因此该文件夹的URI为`"/testFolder"`。 使用与Microsoft .NET Framework（例如C#）兼容的语言时，将URI存储在`System.String`对象中。

1. 创建资源

   要创建资源，请调用`Resource`类的默认构造函数。 在此示例中，以下信息存储在`Resource`对象中：

   * `com.adobe.repository.infomodel.Id`对象，通过调用`Id`类的默认构造函数来创建该对象，并将其分配给`Resource`对象的`id`字段。
   * `com.adobe.repository.infomodel.Lid`对象，通过调用`Lid`类的默认构造函数来创建该对象，并将其分配给`Resource`对象的`lid`字段。
   * 包含资源文件名的字符串，该文件名被分配给`Resource`对象的`name`字段。 此示例中使用的名称为`"testResource"`。
   * 包含资源描述的字符串，该描述被分配给`Resource`对象的`description`字段。 此示例中使用的描述为`"test resource"`。

1. 指定资源内容

   要为资源创建内容，请调用`ResourceContent`类的默认构造函数。 然后，向`ResourceContent`对象添加内容。 在本例中，可通过执行以下任务来完成此操作：

   * 将包含文档的`BLOB`对象分配给`ResourceContent`对象的`dataDocument`字段。
   * 将`BLOB`对象的大小（以字节为单位）分配给`ResourceContent`对象的`size`字段。

   通过将`ResourceContent`对象分配给`Resource`对象的`content`字段，将内容添加到资源中。

1. 将资源写入目标文件夹

   调用`RepositoryServiceService`对象的`writeResource`方法，并在文件夹的URI以及`Resource`对象中传递。 传递`null`以获取其他两个参数。

**另请参阅**

[编写资源](aem-forms-repository.md#writing-resources)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 列出资源{#listing-resources}

您可以通过列出资源来发现资源。 将对存储库执行查询，以查找与给定资源集合相关的所有资源。

整理资源后，您可以检查通过查看结构的特定分支创建的结构，就像在操作系统中一样。

上市资源按关系运作：资源是文件夹的成员。 会员资格由“会员”类型的关系表示。 在给定文件夹中列出资源时，您正在查询与给定文件夹相关的资源，其关系为“成员”。 关系是方向性的：关系成员具有作为目标成员的源。 来源是资源；目标是父文件夹。

>[!NOTE]
>
>有关Repository服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-2}的摘要

要列出资源，请执行以下步骤：

1. 包括项目文件。
1. 创建服务客户端。
1. 指定文件夹路径。
1. 检索资源列表。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请包含代理文件。

**创建服务客户端**

在以编程方式创建资源集合之前，必须建立连接并提供凭据。 这是通过创建服务客户端来完成的。

**指定文件夹路径**

创建包含资源文件夹路径的字符串。 语法包括正斜杠，如以下示例所示：&quot;/*path*/*folder*&quot;。

**检索资源列表**

调用存储库服务方法以检索资源列表，并指定目标文件夹的路径。

**另请参阅**

[使用Java API列出资源](aem-forms-repository.md#list-resources-using-the-java-api)

[使用Web服务API列出资源](aem-forms-repository.md#list-resources-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速入门](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API {#list-resources-using-the-java-api}列出资源

使用存储库服务API(Java)列出资源：

1. 包含项目文件

   将客户端JAR文件包含在您Java项目的类路径中。

1. 创建服务客户端

   使用其构造函数创建`ResourceRepositoryClient`对象，并传递包含连接属性的`ServiceClientFactory`对象。

1. 指定文件夹路径

   指定要查询的资源集合的URI。 在这种情况下，其URI为`"/testFolder"`。 URI将存储为`java.lang.String`对象。

1. 检索资源列表

   调用`ResourceRepositoryClient`对象的`listMembers`方法，并在文件夹的URI中传递。

   该方法返回`com.adobe.repository.infomodel.bean.Resource`对象的`java.util.List`，这些对象是`Relation.TYPE_MEMBER_OF`类型的`com.adobe.repository.infomodel.bean.Relation`的源，并且以资源集合URI作为目标。 您可以遍历此`List`以检索每个资源。 在此示例中，将显示每个资源的名称和描述。

**另请参阅**

[列出资源](aem-forms-repository.md#listing-resources)。

[快速入门（SOAP模式）：使用Java API列出资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#list-resources-using-the-web-service-api}列出资源

使用存储库服务API（Web服务）列出资源：

1. 包含项目文件

   * 创建使用存储库WSDL的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用其默认构造函数创建`RepositoryServiceService`对象。 使用包含用户名和密码的`System.Net.NetworkCredential`对象设置其`Credentials`属性。

1. 指定文件夹路径

   指定包含要查询的文件夹URI的字符串。 在这种情况下，其URI为`"/testFolder"`。 使用与Microsoft .NET Framework（例如C#）兼容的语言时，将URI存储在`System.String`对象中。

1. 检索资源列表

   调用`RepositoryServiceService`对象的`listMembers`方法，并将文件夹的URI作为第一个参数传递。 传递`null`以获取其他两个参数。

   该方法会返回一个对象数组，这些对象可以转换为`Resource`对象。 您可以遍历对象数组以检索每个相关资源。 在此示例中，将显示每个资源的名称和描述。

**另请参阅**

[列出资源](aem-forms-repository.md#listing-resources)。

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 读取资源{#reading-resources}

您可以从存储库中的给定位置检索资源，以读取其内容和元数据。 该工作流由初始化表单前端。 该流程具有读取表单所需的所有权限。 系统检索数据表单并从存储库中读取内容。 存储库授予对内容和元数据的访问权限（甚至能够知道资源存在）。

存储库具有以下四种权限类型：

* **遍历**:允许您列出资源；即，读取资源元数据，但不读取资源内容
* **阅读**:用于读取资源内容
* **写入**:允许您编写资源内容
* **管理访问控制列表(ACL)**:允许您处理资源上的ACL

用户只有在有权运行进程时才能运行进程。 IDE用户需要遍历和读取权限才能与存储库同步。 ACL仅在设计时应用，因为运行时在系统上下文中发生。

您可以使用存储库服务Java API或Web服务API以编程方式读取资源。

>[!NOTE]
>
>有关Repository服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-3}的摘要

要读取资源，请执行以下步骤：

1. 包括项目文件。
1. 创建存储库服务客户端。
1. 指定要读取的资源的URI。
1. 读取资源。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请包含代理文件。

**创建服务客户端**

在以编程方式读取资源之前，必须建立连接并提供凭据。 这是通过创建服务客户端来完成的。

**指定要读取的资源的URI**

创建包含要读取的资源URI的字符串。 语法包括正斜杠，如以下示例所示：&quot;/*path*/*resource*&quot;。

**读取资源**

调用存储库服务方法以读取资源，并指定URI。

**另请参阅**

[使用Java API读取资源](aem-forms-repository.md#read-resources-using-the-java-api)

[使用Web服务API读取资源](aem-forms-repository.md#reading-resources-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速入门](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API {#read-resources-using-the-java-api}读取资源

使用存储库服务API(Java)读取资源：

1. 包含项目文件

   将客户端JAR文件包含在您Java项目的类路径中。

1. 创建服务客户端

   使用其构造函数创建`ResourceRepositoryClient`对象，并传递包含连接属性的`ServiceClientFactory`对象。

1. 指定要读取的资源的URI

   指定表示要检索的资源的URI的字符串值。 例如，假定资源名为&#x200B;*testResource*，该资源位于名为&#x200B;*testFolder*&#x200B;的文件夹中，请指定`/testFolder/testResource`。

1. 读取资源

   调用`ResourceRepositoryClient`对象的`readResource`方法，并将资源的URI作为参数传递。 此方法会返回表示资源的`Resource`实例。

**另请参阅**

[读取资源](aem-forms-repository.md#reading-resources)

[快速入门（SOAP模式）：使用Java API读取资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#reading-resources-using-the-web-service-api}读取资源

使用存储库服务API（Web服务）读取资源：

1. 包含项目文件

   * 创建使用存储库WSDL的Microsoft .NET客户端程序集。 （请参阅[创建使用Base64编码](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)的.NET客户端程序集。）
   * 引用Microsoft .NET客户端程序集。 （请参阅[创建使用Base64编码](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)的.NET客户端程序集。）

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用其默认构造函数创建`RepositoryServiceService`对象。 使用包含用户名和密码的`System.Net.NetworkCredential`对象设置其`Credentials`属性。

1. 指定要读取的资源的URI

   指定包含要检索的资源URI的字符串。 在这种情况下，由于名为`testResource`的资源位于名为`testFolder`的文件夹中，因此其URI为`"/testFolder/testResource"`。 使用与Microsoft .NET Framework（例如C#）兼容的语言时，将URI存储在`System.String`对象中。

1. 读取资源

   调用`RepositoryServiceService`对象的`readResource`方法，并将资源的URI作为第一个参数传递。 传递`null`以获取其他两个参数。

**另请参阅**

[读取资源](aem-forms-repository.md#reading-resources)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 更新资源{#updating-resources}

您可以检索和更新存储库中资源的内容。 在更新资源时，这些资源的访问控制在不同版本之间保持不变。 执行更新时，您可以选择增加主版本。 如果不选择递增主版本，则会自动更新次版本。

更新资源时，将根据指定的资源属性创建新版本。 在更新资源时，可以指定两个重要参数：目标URI和包含所有更新元数据的资源实例。 请务必注意，如果您没有更改给定属性（例如，名称），则在您传入的实例中仍需要该属性。 解析内容时创建的关系将添加到特定版本，除非另外指定，否则不会推出。

例如，如果您更新了XDP文件，并且该文件包含对其他资源的引用，则还会记录这些附加引用。 假定form.xdp版本1.0具有两个外部引用：徽标和样式表，然后您随后更新了form.xdp，以便它现在有三个引用：徽标、样式表和模式文件。 在更新期间，存储库会将第三种关系（到架构文件）添加到其挂起关系表。 当架构文件存在于存储库中后，将自动形成关系。 但是，如果form.xdp版本2.0不再使用徽标，则form.xdp版本2.0将与徽标不相关。

所有更新操作都是原子操作和事务操作。 例如，如果两个用户读取同一资源并同时决定将版本1.0更新到版本2.0，则其中一个用户将成功，其中一个用户将失败，则存储库的完整性将得到维护，并且两用户都将收到一条消息，确认成功或失败。 如果事务未提交，则在出现数据库故障时将回滚，并且会超时或回滚，具体取决于应用程序服务器。

您可以使用存储库服务Java API或Web服务API以编程方式更新资源。

>[!NOTE]
>
>有关Repository服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-4}的摘要

要更新资源，请执行以下步骤：

1. 包括项目文件。
1. 创建存储库服务客户端。
1. 检索要更新的资源。
1. 更新资源。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请包含代理文件。

**创建服务客户端**

在以编程方式读取资源之前，必须建立连接并提供凭据。 这是通过创建服务客户端来完成的。

**检索要更新的资源**

读取资源。 有关更多信息，请参阅[读取资源](aem-forms-repository.md#reading-resources)。

**更新资源**

在资源中设置新信息并调用Repository服务方法来更新资源、指定URI、更新的资源以及应如何更新版本信息。

**另请参阅**

[使用Java API更新资源](aem-forms-repository.md#update-resources-using-the-java-api)

[使用Web服务API更新资源](aem-forms-repository.md#update-resources-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速入门](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API {#update-resources-using-the-java-api}更新资源

使用存储库服务API(Java)更新资源：

1. 包含项目文件

   将客户端JAR文件包含在您Java项目的类路径中。

1. 创建服务客户端

   使用其构造函数创建`ResourceRepositoryClient`对象，并传递包含连接属性的`ServiceClientFactory`对象。

1. 检索要更新的资源

   指定要检索和读取资源的资源的URI。 在此示例中，资源的URI为`"/testFolder/testResource"`。

1. 更新资源

   更新`Resource`对象的信息。 在此示例中，要更新描述，请调用`Resource`对象的`setDescription`方法，并将新描述字符串作为参数传递。

   然后调用`ServiceClientFactory`对象的`updateResource`方法，并传递以下参数：

   * 包含资源URI的`java.lang.String`对象。
   * 包含更新的资源信息的`Resource`对象。
   * `boolean`值，指示是更新主版本还是次版本。 在此示例中，传递值`true`，以指示主版本将递增。

**另请参阅**

[更新资源](aem-forms-repository.md#updating-resources)

[快速入门（SOAP模式）：使用Java API更新资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#update-resources-using-the-web-service-api}更新资源

使用存储库API（Web服务）更新资源：

1. 包含项目文件

   * 创建使用存储库WSDL的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用其默认构造函数创建`RepositoryServiceService`对象。 使用包含用户名和密码的`System.Net.NetworkCredential`对象设置其`Credentials`属性。

1. 检索要更新的资源

   指定要检索并读取资源的资源的URI。 在此示例中，资源的URI为`"/testFolder/testResource"`。 有关更多信息，请参阅[读取资源](aem-forms-repository.md#reading-resources)。

1. 更新资源

   更新`Resource`对象的信息。 在此示例中，要更新描述，请为`Resource`对象的`description`字段分配一个新值。

1. 调用`RepositoryServiceService`对象的`updateResource`方法，并传入以下参数：

   * 包含资源URI的`System.String`对象。
   * 包含更新的资源信息的`Resource`对象。
   * `boolean`值，指示是更新主版本还是次版本。 在此示例中，传递值`true`，以指示主版本将递增。
   * 传递`null`以获取其余两个参数。

**另请参阅**

[更新资源](aem-forms-repository.md#updating-resources)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 搜索资源{#searching-for-resources}

您可以构建查询，用于在存储库中搜索资源，包括历史记录、相关资源和属性。

您可以检索相关资源以确定表单及其片段之间的依赖关系。 例如，如果您有表单，则可以确定它使用的片段或外部资源。 如果您有图像，则还可以查找使用该图像的表单。 您还可以使用基于属性的过滤功能搜索相关资源。 例如，您可以搜索所有使用指定名称的图像的表单，或查找具有指定名称的表单使用的任何图像。 您还可以使用资源属性进行搜索。 例如，您可以执行查询以查找名称以给定字符串开头的所有表单或资源，该字符串可能包含“%”和“_”通配符。 请记住，基于属性的搜索不基于关系；此类搜索基于您对给定资源具有特定知识的假设。

**查询语句**

*查询*&#x200B;包含一个或多个语句，这些语句在逻辑上与条件联接。 *语句*&#x200B;由左操作数、运算符和右操作数组成。 此外，您还可以指定用于搜索结果的排序顺序。 *排序顺序*&#x200B;包含与SQL `ORDER BY`子句等效的信息，该信息由包含搜索所依据的属性的元素以及指示是使用升序还是降序的值组成。

您可以使用存储库服务Java API以编程方式搜索资源。 目前，无法使用Web服务API来搜索资源。

**排序行为**

调用`ResourceRepositoryClient`对象的`searchProperties`方法并指定排序顺序时，不遵循排序顺序。 例如，假定您创建一个具有三个自定义属性的资源，其中属性名称为`name`、`secondName`和`asecondName`。 接下来，在属性名称中创建排序顺序元素，并将`ascending`值设置为`true`。

然后调用`ResourceRepositoryClient`对象的`searchProperties`方法并按排序顺序传递。 搜索会返回具有三个属性的正确资源。 但是，属性不会按属性名称排序。 系统会按添加顺序返回它们：`name`、`secondName`和`asecondName`。

>[!NOTE]
>
>有关Repository服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-5}的摘要

要搜索资源，请执行以下步骤：

1. 包括项目文件。
1. 创建存储库服务客户端。
1. 指定搜索的目标文件夹。
1. 指定搜索中使用的属性。
1. 创建搜索中使用的查询。
1. 为搜索结果创建排序顺序。
1. 搜索资源。
1. 从搜索结果中检索资源。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请包含代理文件。

**创建服务客户端**

在以编程方式读取资源之前，必须建立连接并提供凭据。 这是通过创建服务客户端来完成的。

**指定搜索的目标文件夹**

创建一个字符串，其中包含用于执行搜索的基本路径。 语法包括正斜杠，如以下示例所示：&quot;/*path*/*folder*&quot;。

**指定搜索中使用的属性**

您可以根据资源中包含的属性进行搜索。 指定用于执行搜索的属性值。

**创建搜索中使用的查询**

使用语句和条件构建查询。 每个语句都将指定搜索所依据的属性、要使用的条件以及要在搜索中使用的属性值。

**为搜索结果创建排序顺序**

排序顺序由元素组成，每个元素都包含搜索中使用的一个属性和一个值，该值指示是使用升序还是降序。

**搜索资源**

使用文件夹、查询和排序顺序搜索资源。 此外，还指示搜索的深度和返回结果数的上限。

**从搜索结果中检索资源**

遍历返回的资源列表并提取信息以供进一步处理。

**另请参阅**

[使用Java API搜索资源](aem-forms-repository.md#search-for-resources-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速入门](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API {#search-for-resources-using-the-java-api}搜索资源

使用存储库服务API(Java)搜索资源：

1. 包含项目文件

   将客户端JAR文件包含在您Java项目的类路径中。

1. 创建服务客户端

   使用其构造函数创建`ResourceRepositoryClient`对象，并传递包含连接属性的`ServiceClientFactory`对象。

1. 指定搜索的目标文件夹

   指定要从中执行搜索的基本路径的URI。 在此示例中，资源的URI为`/testFolder`。

1. 指定搜索中使用的属性

   指定用于执行搜索的属性的值。 属性存在于`com.adobe.repository.infomodel.bean.Resource`对象中。 在本例中，将对名称属性进行搜索；因此，将使用包含`Resource`对象名称的`java.lang.String`，在本例中为`testResource`。

1. 创建搜索中使用的查询

   要创建查询，请通过调用`Query`类的默认构造函数创建`com.adobe.repository.query.Query`对象，并向查询中添加语句。

   要创建语句，请调用`com.adobe.repository.query.Query.Statement`类的构造函数，并传入以下参数：

   * 包含资源属性常量的左操作数。 在此示例中，由于资源的名称用作搜索的基础，因此会使用静态值`Resource.ATTRIBUTE_NAME`。
   * 包含搜索属性时所用条件的运算符。 运算符必须是`Query.Statement`类中的静态常量之一。 在此示例中，使用静态值`Query.Statement.OPERATOR_BEGINS_WITH`。
   * 右操作数，其中包含用于执行搜索的属性值。 在此示例中，使用名称属性`String`（包含值`"testResource"`）。

   通过调用`Query.Statement`对象的`setNamespace`方法并传入`com.adobe.repository.infomodel.bean.ResourceProperty`类中包含的一个静态值，指定左操作数的命名空间。 在本例中，使用`ResourceProperty.RESERVED_NAMESPACE_REPOSITORY`。

   通过调用`Query`对象的`addStatement`方法并传入`Query.Statement`对象，将每个语句添加到查询中。

1. 为搜索结果创建排序顺序

   要指定搜索结果中使用的排序顺序，请通过调用`SortOrder`类的默认构造函数来创建`com.adobe.repository.query.sort.SortOrder`对象，并将元素添加到排序顺序。

   要为排序顺序创建元素，请调用`com.adobe.repository.query.sort.SortOrder.Element`类的构造函数之一。 在此示例中，由于资源的名称用作搜索的基础，因此静态值`Resource.ATTRIBUTE_NAME`将用作第一个参数，而升序（`boolean`值`true`）将指定为第二个参数。

   通过调用`SortOrder`对象的`addSortElement`方法并传入`SortOrder.Element`对象，将每个元素添加到排序顺序中。

1. 搜索资源

   要根据属性属性搜索`resources`，请调用`ResourceRepositoryClient`对象的`searchProperties`方法并传递以下参数：

   * `String`，包含执行搜索的基本路径。 在这种情况下，使用`"/testFolder"`。
   * 搜索中使用的查询。
   * 搜索的深度。 在这种情况下，使用`com.adobe.repository.infomodel.bean.ResourceCollection.DEPTH_INFINITE`指示将使用基本路径及其所有文件夹。
   * `int`值，指示要从中选择未分页结果集的第一行。 在本例中，指定了`0`。
   * `int`值，指示要返回的结果的最大数量。 在本例中，指定了`10`。
   * 搜索中使用的排序顺序。

   方法会按指定的排序顺序返回`Resource`对象的`java.util.List`。

1. 从搜索结果中检索资源

   要检索搜索结果中包含的资源，请遍历`List`并将每个对象转换为`Resource`，以提取其信息。 在此示例中，将显示每个资源的名称。

**另请参阅**

[搜索资源](aem-forms-repository.md#searching-for-resources)

[快速入门（SOAP模式）：使用Java API搜索资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 创建资源关系{#creating-resource-relationships}

您可以指定存储库中资源之间的关系。 有三种关系：

* **依赖**:资源依赖于其他资源的关系，这意味着存储库中需要所有相关资源。
* **成员资格（文件系统）**:资源位于给定文件夹中的关系。
* **自定义**:您在资源之间指定的关系。例如，如果一个资源已被弃用，而另一个资源被引入到存储库中，则可以指定您自己的替换关系。

您可以创建自己的自定义关系。 例如，如果将HTML文件存储在存储库中，并且它使用图像，则可以指定一个自定义关系，以将HTML文件与图像相关联（因为通常只有XML文件与图像关联时使用存储库定义的依赖关系）。 自定义关系的另一个示例是，如果您希望使用循环图结构而不是树结构来构建存储库的不同视图。 您可以定义一个与查看器一起的圆形图来遍历这些关系。 最后，您可以指示某个资源替换了另一个资源，即使这两个资源完全不同。 在这种情况下，您可以在保留范围之外定义一种关系类型，并在这两种资源之间创建一种关系。 您的应用程序将是唯一能够检测和处理关系的客户端，并且可用于对该关系进行搜索。

您可以使用存储库服务Java API或Web服务API以编程方式指定资源之间的关系。

>[!NOTE]
>
>有关Repository服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-6}的摘要

要指定两个资源之间的关系，请执行以下步骤：

1. 包括项目文件。
1. 创建存储库服务客户端。
1. 指定要关联的资源的URI。
1. 创建关系。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请包含代理文件。

**创建服务客户端**

在以编程方式读取资源之前，必须建立连接并提供凭据。 这是通过创建服务客户端来完成的。

**指定要关联的资源的URI**

创建包含要关联的资源URI的字符串。 语法包括正斜杠，如以下示例所示：&quot;/*path*/*resource*&quot;。

**创建关系**

调用存储库服务方法以创建和指定关系类型。

**另请参阅**

[使用Java API创建关系资源](aem-forms-repository.md#create-relationship-resources-using-the-java-api)

[使用Web服务API创建关系资源](aem-forms-repository.md#create-relationship-resources-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速入门](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API {#create-relationship-resources-using-the-java-api}创建关系资源

使用存储库服务Java API创建关系资源，然后执行以下任务：

1. 包含项目文件

   将客户端JAR文件包含在您Java项目的类路径中。

1. 创建服务客户端

   使用其构造函数创建`ResourceRepositoryClient`对象，并传递包含连接属性的`ServiceClientFactory`对象。

1. 指定要关联的资源的URI

   指定要关联的资源的URI。 在这种情况下，由于资源名为`testResource1`和`testResource2`，并位于名为`testFolder`的文件夹中，因此它们的URI为`"/testFolder/testResource1"`和`"/testFolder/testResource2"`。 URI将作为`java.lang.String`对象存储。 在本例中，首先将资源写入存储库，并检索其URI。 有关编写资源的更多信息，请参阅[编写资源](aem-forms-repository.md#writing-resources)。

1. 创建关系

   调用`ResourceRepositoryClient`对象的`createRelationship`方法并传入以下参数：

   * 源资源的URI。
   * 目标资源的URI。
   * 关系的类型，是`com.adobe.repository.infomodel.bean.Relation`类中的静态常量之一。 在本例中，通过指定值`Relation.TYPE_DEPENDANT_OF`建立依赖关系。
   * 指示目标资源是否自动更新为新头资源的基于`com.adobe.repository.infomodel.Id`的标识符的`boolean`值。 在本例中，由于依赖关系，指定了值`true`。

   您还可以通过调用`ResourceRepositoryClient`对象的`getRelated`方法并传递以下参数来检索给定资源的相关资源列表：

   * 要为其检索相关资源的资源的URI。 在本例中，指定了源资源(`"/testFolder/testResource1"`)。
   * `boolean`值，指示指定的资源是否是关系中的源资源。 在此示例中，指定了值`true`，因为这是这种情况。
   * 关系类型，是`Relation`类中的静态常量之一。 在本例中，依赖关系通过使用之前使用的相同值来指定：`Relation.TYPE_DEPENDANT_OF`。

   `getRelated`方法返回`Resource`对象的`java.util.List`，您可以通过该对象进行迭代以检索每个相关资源，并将`List`中包含的对象按照其操作方式浇铸为`Resource`。 在本例中，`testResource2`应位于返回的资源列表中。

**另请参阅**

[创建资源关系](aem-forms-repository.md#creating-resource-relationships)

[快速入门（SOAP模式）：使用Java API创建资源之间的关系](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#create-relationship-resources-using-the-web-service-api}创建关系资源

使用存储库API（Web服务）创建关系资源：

1. 包含项目文件

   * 创建使用存储库WSDL的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用其默认构造函数创建`RepositoryServiceService`对象。 使用包含用户名和密码的`System.Net.NetworkCredential`对象设置其`Credentials`属性。

1. 指定要关联的资源的URI

   指定要关联的资源的URI。 在这种情况下，由于资源名为`testResource1`和`testResource2`，并位于名为`testFolder`的文件夹中，因此它们的URI为`"/testFolder/testResource1"`和`"/testFolder/testResource2"`。 使用与Microsoft .NET Framework（例如C#）兼容的语言时，URI将存储为`System.String`对象。 在本例中，首先将资源写入存储库，并检索其URI。 有关编写资源的更多信息，请参阅[编写资源](aem-forms-repository.md#writing-resources)。

1. 创建关系

   调用`RepositoryServiceService`对象的`createRelationship`方法并传入以下参数：

   * 源资源的URI。
   * 目标资源的URI。
   * 关系的类型。 在本例中，通过指定值`3`建立依赖关系。
   * `boolean`值，指示是否指定了关系类型。 在本例中，指定了值`true`。
   * 指示目标资源是否自动更新为新头资源的基于`Id`的标识符的`boolean`值。 在本例中，由于依赖关系，指定了值`true`。
   * `boolean`值，指示是否指定了目标头。 在本例中，指定了值`true`。
   * 传递`null`作为最后一个参数。

   您还可以通过调用`RepositoryServiceService`对象的`getRelated`方法并传递以下参数来检索给定资源的相关资源列表：

   * 要为其检索相关资源的资源的URI。 在本例中，指定了源资源(`"/testFolder/testResource1"`)。
   * `boolean`值，指示指定的资源是否是关系中的源资源。 在此示例中，指定了值`true`，因为这是这种情况。
   * 指示是否指定了源资源的`boolean`值。 在本例中，提供了值`true`。
   * 包含关系类型的整数数组。 在此示例中，依赖关系是使用数组中与之前使用的值相同的值指定的：`3`。
   * 传递`null`以获取其余两个参数。

   `getRelated`方法会返回一个对象数组，这些对象可以转换为`Resource`对象，您可以通过这些对象进行迭代以检索每个相关资源。 在本例中，`testResource2`应位于返回的资源列表中。

**另请参阅**

[创建资源关系](aem-forms-repository.md#creating-resource-relationships)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 锁定资源{#locking-resources}

您可以锁定某个资源或一组资源，以供特定用户专用或在多个用户之间共享使用。 共享锁表示资源将发生某些情况，但不会阻止其他任何人使用该资源执行操作。 共享锁应被视为信令机制。 独占锁表示锁定资源的用户将更改资源，而锁则确保在用户不再需要访问该资源并释放锁之前，其他任何人都不能这样做。 如果存储库管理员解锁某个资源，则该资源上的所有独占和共享锁定将自动删除。 此类操作适用于用户不再可用且未解锁资源的情况。

资源被锁定后，当您查看位于Workbench中的“资源”选项卡时，会显示一个锁图标，如下图所示。

![lr_lr_lockrepository](assets/lr_lr_lockrepository.png)

您可以使用存储库服务Java API或Web服务API以编程方式控制对资源的访问。

>[!NOTE]
>
>有关Repository服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-7}的摘要

要锁定和解锁资源，请执行以下步骤：

1. 包括项目文件。
1. 创建存储库服务客户端。
1. 指定要锁定的资源的URI。
1. 锁定资源。
1. 检索资源的锁。
1. 解锁资源

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请包含代理文件。

**创建服务客户端**

在以编程方式读取资源之前，必须建立连接并提供凭据。 这是通过创建服务客户端来完成的。

**指定要锁定的资源的URI**

创建包含要锁定的资源URI的字符串。 语法包括正斜杠，如以下示例所示：&quot;/*path*/*resource*&quot;。

**锁定资源**

调用存储库服务方法以锁定资源，指定URI、锁定类型和锁定深度。

**检索资源的锁**

调用Repository服务方法以检索资源的锁，并指定URI。

**解锁资源**

调用存储库服务方法以解锁资源，并指定URI。

**另请参阅**

[使用Java API锁定资源](aem-forms-repository.md#lock-resources-using-the-java-api)

[使用Web服务API锁定资源](aem-forms-repository.md#lock-resources-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速入门](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API {#lock-resources-using-the-java-api}锁定资源

使用存储库服务API(Java)锁定资源：

1. 包含项目文件

   将客户端JAR文件包含在您Java项目的类路径中。

1. 创建服务客户端

   使用其构造函数创建`ResourceRepositoryClient`对象，并传递包含连接属性的`ServiceClientFactory`对象。

1. 指定要锁定的资源的URI

   指定要锁定的资源的URI。 在这种情况下，由于名为`testResource`的资源位于名为`testFolder`的文件夹中，因此其URI为`"/testFolder/testResource"`。 URI将存储为`java.lang.String`对象。

1. 锁定资源

   调用`ResourceRepositoryClient`对象的`lockResource`方法并传入以下参数：

   * 资源的URI。
   * 锁定范围。 在本例中，由于资源将被锁定以供独占使用，因此锁定范围被指定为`com.adobe.repository.infomodel.bean.Lock.SCOPE_EXCLUSIVE`。
   * 锁的深度。 在此示例中，由于锁定将仅应用于特定资源，且不应用其成员或子资源，因此锁定深度指定为`Lock.DEPTH_ZERO`。

   >[!NOTE]
   >
   >需要四个参数的`lockResource`方法的重载版本会引发异常。 请确保使用`lockResource`方法，该方法需要三个参数，如本演练中所示。

1. 检索资源的锁

   调用`ResourceRepositoryClient`对象的`getLocks`方法，并将资源的URI作为参数传递。 该方法会返回一个Lock对象列表，您可以通过该列表进行迭代。 在此示例中，通过分别调用每个锁定对象的`getOwnerUserId`、`getDepth`和`getType`方法，为每个对象打印锁定所有者、深度和范围。

1. 解锁资源

   调用`ResourceRepositoryClient`对象的`unlockResource`方法，并将资源的URI作为参数传递。 有关更多信息，请参阅[AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**另请参阅**

[锁定资源](aem-forms-repository.md#locking-resources)

[快速入门（SOAP模式）：使用Java API锁定资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#lock-resources-using-the-web-service-api}锁定资源

使用存储库服务API（Web服务）锁定资源：

1. 包含项目文件

   * 使用Base64创建使用存储库WSDL的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用其默认构造函数创建`RepositoryServiceService`对象。 使用包含用户名和密码的`System.Net.NetworkCredential`对象设置其`Credentials`属性。

1. 指定要锁定的资源的URI

   指定包含要锁定的资源URI的字符串。 在这种情况下，由于名为`testResource`的资源位于文件夹`testFolder`中，因此其URI为`"/testFolder/testResource"`。 使用与Microsoft .NET Framework（例如C#）兼容的语言时，将URI存储在`System.String`对象中。

1. 锁定资源

   调用`RepositoryServiceService`对象的`lockResource`方法并传入以下参数：

   * 资源的URI。
   * 锁定范围。 在本例中，由于资源将被锁定以供独占使用，因此锁定范围被指定为`11`。
   * 锁的深度。 在此示例中，由于锁定将仅应用于特定资源，且不应用其成员或子资源，因此锁定深度指定为`2`。
   * `int`值，指示锁定过期的秒数。 在此示例中，使用值`1000`。
   * 传递`null`作为最后一个参数。

1. 检索资源的锁

   调用`RepositoryServiceService`对象的`getLocks`方法，并将资源的URI作为第一个参数传递，并将`null`作为第二个参数传递。 该方法会返回一个包含`Lock`对象的`object`数组，您可以通过该数组进行迭代。 在本例中，通过分别访问每个`Lock`对象的`ownerUserId`、`depth`和`type`字段，为每个对象打印锁所有者、深度和范围。

1. 解锁资源

   调用`RepositoryServiceService`对象的`unlockResource`方法，并将资源的URI作为第一个参数传递，并将`null`作为第二个参数传递。

**另请参阅**

[锁定资源](aem-forms-repository.md#locking-resources)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 删除资源{#deleting-resources}

您可以使用存储库服务Java API(SOAP)以编程方式从存储库中的给定位置删除资源。

删除资源时，该删除操作通常是永久性的，但在某些情况下，ECM存储库可能会根据其历史机制存储资源的版本。 因此，在删除资源时，务必确保不再需要该资源。 删除资源的常见原因包括需要增加数据库中的可用空间。 您可以删除资源的某个版本，但是如果删除了该版本，则必须指定资源标识符，而不是其逻辑标识符(LID)或路径。 如果删除文件夹，则该文件夹中的所有内容（包括子文件夹和资源）都将被自动删除。

不会删除相关资源。 例如，如果您有一个使用logo.gif文件的表单，并删除logo.gif，则关系将存储在挂起的关系表中。 作为替代方法，对于弃用的版本，请将最新版本的对象状态设置为已弃用。

在ECM系统中，删除操作不是事务安全的。 例如，如果您尝试删除100个资源，并且该操作在第50个资源上失败，则将删除前49个实例，但其余实例将不会删除。 否则，默认行为为回滚（非承诺）。

>[!NOTE]
>
>在将`com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient.deleteResources()`方法与ECM存储库（EMC Documentum Content Server和IBM FileNet P8 Content Manager）一起使用时，如果某个指定资源的删除失败，则不会回滚事务，这意味着无法删除那些已删除的文件。

>[!NOTE]
>
>有关Repository服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-8}的摘要

要删除资源，请执行以下步骤：

1. 包括项目文件。
1. 创建存储库服务客户端。
1. 指定要删除的资源的URI。
1. 删除资源。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请包含代理文件。

**创建服务客户端**

在以编程方式读取资源之前，必须建立连接并提供凭据。 这是通过创建服务客户端来完成的。

**指定要删除的资源的URI**

创建包含要删除的资源URI的字符串。 语法包括正斜杠，如以下示例所示：&quot;/*path*/*resource*&quot;。 如果要删除的资源是文件夹，则删除将递归。

**删除资源**

调用存储库服务方法以删除资源，并指定URI。

**另请参阅**

[使用Java API删除资源](aem-forms-repository.md#delete-resources-using-the-java-api-soap)

[使用Web服务API删除资源](aem-forms-repository.md#delete-resources-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速入门](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API(SOAP){#delete-resources-using-the-java-api-soap}删除资源

使用存储库API(Java)删除资源：

1. 包含项目文件

   将客户端JAR文件包含在您Java项目的类路径中。

1. 创建服务客户端

   使用其构造函数创建`ResourceRepositoryClient`对象，并传递包含连接属性的`ServiceClientFactory`对象。

1. 指定要删除的资源的URI

   指定要检索的资源的URI。 在这种情况下，由于名为testResourceToBeDeleted的资源位于名为testFolder的文件夹中，因此其URI为`/testFolder/testResourceToBeDeleted`。 URI将存储为`java.lang.String`对象。 在此示例中，资源首先写入存储库，并检索其URI。 有关编写资源的更多信息，请参阅[编写资源](aem-forms-repository.md#writing-resources)。

1. 删除资源

   调用`ResourceRepositoryClient`对象的`deleteResource`方法，并将资源的URI作为参数传递。

**另请参阅**

[删除资源](aem-forms-repository.md#deleting-resources)

[快速入门（SOAP模式）：使用Java API搜索资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#delete-resources-using-the-web-service-api}删除资源

使用存储库API（Web服务）删除资源：

1. 包含项目文件

   * 使用Base64创建使用存储库WSDL的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用其默认构造函数创建`RepositoryServiceService`对象。 使用包含用户名和密码的`System.Net.NetworkCredential`对象设置其`Credentials`属性。

1. 指定要删除的资源的URI

   指定要检索的资源的URI。 在这种情况下，由于名为`testResourceToBeDeleted`的资源位于名为`testFolder`的文件夹中，因此其URI为`"/testFolder/testResourceToBeDeleted"`。 在此示例中，资源首先写入存储库，并检索其URI。 有关编写资源的更多信息，请参阅[编写资源](aem-forms-repository.md#writing-resources)。

1. 删除资源

   调用`RepositoryServiceService`对象的`deleteResources`方法，并传递一个`System.String`数组，其中包含资源的URI作为第一个参数。 传递`null`作为第二个参数。

**另请参阅**

[删除资源](aem-forms-repository.md#deleting-resources)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
