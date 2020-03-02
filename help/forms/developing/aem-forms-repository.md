---
title: 使用AEM Forms存储库
seo-title: 使用AEM Forms存储库
description: 'null'
seo-description: 'null'
uuid: 6ead49f9-ca0d-4ee4-86a6-0a9ced6ec4f8
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d2c95881-6c02-4e34-85af-84607df54287
translation-type: tm+mt
source-git-commit: 67ea825215d1ca7cc2e350ed1c128c3146de45ec

---


# Working with AEM Forms Repository {#working-with-aem-forms-repository}

**关于存储库服务**

存储库服务为AEM Forms提供资源存储和管理服务。 当开发人员创建 *AEM Forms应用程序时* ，他们可以在存储库而不是文件系统中部署资产。 资产可以包括任何类型的附属品，包括XML表单、PDF表单（包括Acrobat表单）、表单片段、图像、配置文件、策略、SWF文件、DDX文件、XML架构、WSDL文件和测试数据。

例如，请考虑以下名为 *Applications/FormsApplication的Forms应用程序*:

![ww_ww_formrepository](assets/ww_ww_formrepository.png)

请注意，FormsFolder中有一个名为Loan.xdp的文件。 要访问此表单设计，请指定完整路径（包括版本）: `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.

>[!NOTE]
>
>有关使用Workbench创建Forms应用程序的信息，请参阅 [Workbench帮助](https://www.adobe.com/go/learn_aemforms_workbench_63)。

位于AEM Forms存储库中的资源的路径是：

`Applications/Application-name/Application-version/Folder.../Filename`

以下值显示一些URI值的示例：

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

>[!NOTE]
>
>您可以使用Web浏览器浏览AEM Forms存储库。 要浏览存储库，请在Web浏览器中输入以下URL `https://[server name]:[server port]/repository`。 您可以使用Web浏览器验证与使用AEM Forms存储库部分关联的快速启动结果。 例如，如果向AEM Forms存储库添加内容，则可以在Web浏览器中查看该内容。 (请参 [阅快速入门（SOAP模式）:使用Java API编写资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)。)

存储库API提供了许多操作，您可以使用这些操作来存储和检索存储库中的信息。 例如，当处理应用程序时需要资源时，您可以获取资源列表或检索存储在存储库中的特定资源。

>[!NOTE]
>
>存储库API不能用于与Content services交互（已弃用）。 要与内容服务交互（已弃用），请使用Document Management API。

使用存储库服务API，您可以完成以下任务：

* 创建文件夹。 请参阅 [创建文件夹](aem-forms-repository.md#creating-folders)。
* 编写资源及其属性。 请参阅 [编写资源](aem-forms-repository.md#writing-resources)。
* 列出给定集合中的资源或与其他资源相关的资源。 请参 [阅列表资源](aem-forms-repository.md#listing-resources)。
* 阅读资源及其属性。 请参阅 [阅读资源](aem-forms-repository.md#reading-resources)。
* 更新资源及其属性。 请参阅 [更新资源](aem-forms-repository.md#updating-resources)。
* 搜索资源，包括其历史记录、相关资源和属性。 请参 [阅搜索资源](aem-forms-repository.md#searching-for-resources)。
* 指定资源之间的关系。 请参阅 [创建资源关系](aem-forms-repository.md#creating-resource-relationships)。
* 管理资源访问控制，包括锁定和解锁资源以及读写访问控制列表(ACL)。 请参阅 [锁定资源](aem-forms-repository.md#locking-resources)。
* 删除资源及其属性。 请参阅 [删除资源](aem-forms-repository.md#deleting-resources)。

>[!NOTE]
>
>使用存储库API，您无法通过使用ECM存储库管理资源访问控制、搜索资源或指定资源关系。

>[!NOTE]
>
>将加密的PDF写入存储库时，无法使用自动关系提取功能。 否则，加密的PDF可以存储在存储库中，稍后再进行检索。 在从存储库检索PDF后，检索器可以选择解密该PDF。

>[!NOTE]
>
>有关存储库服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 创建文件夹 {#creating-folders}

文件夹（资源集合）用于按有组织的分组存储对象（文件或资源）。 文件夹可以包含资源和其他文件夹，也称为子文件夹。 资源一次只能存储在一个文件夹中。

文件从文件夹继承访问控制列表(ACL)，子文件夹从父文件夹继承ACL。 因此，在创建子文件夹之前，父文件夹必须存在。 通过IDE，您只能逐个文件夹进行交互，而不能逐个文件进行交互。 您无法版本文件夹，也无需这样做；文件夹不包含数据本身。 相反，它只是包含数据的资源的容器。 默认ACL是系统级权限，这意味着用户必须具有系统级权限（读取、写入、遍历、管理ACL），直到有人授予他们特定文件夹的权限。 ACL仅在IDE中有效。

>[!NOTE]
>
>有关存储库服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary-of-steps}

要创建文件夹，请按照以下步骤操作：

1. 包括项目文件。
1. 创建服务客户端。
1. 创建文件夹。
1. 将文件夹写入存储库。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请包含代理文件。

**创建服务客户端**

在以编程方式创建资源集合之前，必须建立连接并提供凭据。 这是通过创建服务客户端来实现的。

**创建文件夹**

调用存储库服务方法以创建资源集合，并使用标识信息填充资源集合，包括其UUID、文件夹名称和说明。

**将文件夹写入存储库**

调用存储库服务方法以写入资源集合，指定目标文件夹的URI。

**另请参阅**

[使用Java API创建文件夹](aem-forms-repository.md#create-folders-using-the-java-api)

[使用Web服务API创建文件夹](aem-forms-repository.md#create-folders-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速入门](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API创建文件夹 {#create-folders-using-the-java-api}

使用存储库服务API(Java)创建文件夹：

1. 包括项目文件

   将项目文件包含在Java项目的类路径中。

1. 创建服务客户端

   使用对 `ResourceRepositoryClient` 象的构造函数并传递一个包含连接属 `ServiceClientFactory` 性的对象来创建对象。

1. 创建文件夹

   要创建资源集合，必须先创建对 `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` 象。

   调用对 `repositoryInfomodelFactoryBean` 象的方 `newResourceCollection` 法，并传递以下参数：

   * 要分 `com.adobe.repository.infomodel.Id` 配给资源的UUID标识符。
   * 要分 `com.adobe.repository.infomodel.Lid` 配给资源的UUID标识符。
   * 包 `java.lang.String` 含资源集合的名称。 For example, `FormsFolder`.
   该方法返回表示 `com.adobe.repository.infomodel.bean.ResourceCollection` 新文件夹的对象。

   使用方法设置文件夹的说明， `setDescription` 并传递以下参数：

   * 描述 `String` 资源集合的一个。 在此示例中， `"test Folder"` 使用 `.`


1. 将文件夹写入存储库

   调用对 `ResourceRepositoryClient` 象的方 `writeResource` 法并传入文件夹和对象的URI `ResourceCollection` 。 例如，文件夹的URI可以是以下值 `/Applications/FormsApplication/1.0/`。

   该方法返回新创建对象的一个实 `com.adobe.repository.infomodel.bean.Resource` 例。 例如，可以通过调用对象的方法检索新资源的标 `com.adobe.repository.infomodel.bean.Resource` 识符 `getId` 值。

**另请参阅**

[创建文件夹](aem-forms-repository.md#creating-folders)

[快速入门（SOAP模式）:使用Java API创建文件夹](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API创建文件夹 {#create-folders-using-the-web-service-api}

使用存储库服务API（Web服务）创建文件夹：

1. 包括项目文件

   * 创建一个使用base64的存储库WSDL的Microsoft .NET客户端组件。
   * 参考Microsoft .NET客户端程序集。

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用 `RepositoryServiceService` 其默认构造函数创建对象。 使用包 `Credentials` 含用户名和密码 `System.Net.NetworkCredential` 的对象设置其属性。

1. 创建文件夹

   使用类的默认构造函数创建该文 `ResourceCollection` 件夹，并传递以下参数：

   * 对 `Id` 象，通过为类调用默认构造函数创建，并 `Id` 将其分配给 `Resource` 对象的字段 `id` 。
   * 对 `Lid` 象，通过为类调用默认构造函数创建，并 `Lid` 将其分配给 `Resource` 对象的字段 `lid` 。
   * 包含资源集合名称的字符串，该名称被分配给 `Resource` 对象的字 `name` 段。 此示例中使用的名称为 `"testfolder"`。
   * 包含资源集合描述的字符串，该描述被分配给 `Resource` 对象的字 `description` 段。 此示例中使用的说明是 `"test folder"`。

1. 将文件夹写入存储库

   调用对 `RepositoryServiceService` 象的方 `writeResource` 法并传递以下参数：

   * 要创建文件夹的路径。
   * 表示 `ResourceCollection` 文件夹的对象。
   * 传递 `null` 给其他两个参数。

**另请参阅**

[创建文件夹](aem-forms-repository.md#creating-folders)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 编写资源 {#writing-resources}

您可以在存储库中的给定位置创建资源。 自然的文件大小受数据库限制和会话超时的限制。 对于默认配置，文件限制为25 MB。 要增大或减小最大文件大小，必须更改数据库配置。

写入资源等效于将数据存储在存储库中。 将资源写入存储库后，存储库生态系统中的所有客户端都可以访问该资源。 将XML架构、XDP文件和XSD文件等资源写入存储库时，将根据MIME类型分析内容。 如果支持MIME类型，分析器确定是否与其他内容存在默示关系。 例如，如果层叠样式表(CSS)有引用公用CSS的相对URL，则您也应将公用CSS提交到存储库。 两个资源之间的关系被存储为30天不可调节的待处理关系。 在30天内将公用CSS提交到存储库时，将形成关系。

创建资源时，访问控制列表(ACL)将从父文件夹继承。 在创建初始资源或文件夹之前，根文件夹具有系统级权限，此时该资源或文件夹将获得默认的ACL权限。

您可以使用Repository服务Java API或Web服务API以编程方式编写资源。

>[!NOTE]
>
>有关存储库服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-1}

要编写资源，请执行以下步骤：

1. 包括项目文件。
1. 创建存储库服务客户端。
1. 指定要读取的资源的URI。
1. 阅读资源。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请包含代理文件。

**创建服务客户端**

在以编程方式读取资源之前，必须建立连接并提供凭据。 这是通过创建服务客户端来实现的。

**指定资源的目标文件夹的URI**

创建包含要读取的资源的URI的字符串。 语法包括正斜杠，如本例所示：&quot;/*path*/*folder*&quot;。

**创建资源**

调用存储库服务方法以创建资源，并使用标识信息填充资源，包括其UUID、资源名称和说明。

**指定资源内容**

调用存储库服务方法以创建资源内容，并将该内容存储在资源中。

**将资源写入目标文件夹**

调用存储库服务方法以写入资源，指定目标文件夹的URI。

**另请参阅**

[使用Java API编写资源](aem-forms-repository.md#write-resources-using-the-java-api)

[使用Web服务API编写资源](aem-forms-repository.md#write-resources-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速入门](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API编写资源 {#write-resources-using-the-java-api}

使用存储库服务API(Java)编写资源：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件。

1. 创建服务客户端

   使用对 `ResourceRepositoryClient` 象的构造函数并传递一个包含连接属 `ServiceClientFactory` 性的对象来创建对象。

1. 指定资源的目标文件夹的URI

   指定资源的目标文件夹的URI。 在这种情况下，由于名为的资 `testResource` 源将存储在名为的文件夹中， `testFolder`因此该文件夹的URI为 `"/testFolder"`。 URI存储为对 `java.lang.String` 象。

1. 创建资源

   要创建资源，必须先创建对 `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` 象。

   调用对 `RepositoryInfomodelFactoryBean` 象的方 `newResource` 法，该方法创建对 `com.adobe.repository.infomodel.bean.Resource` 象。 在此示例中，提供了以下参数：

   * 通 `com.adobe.repository.infomodel.Id` 过调用类的默认构造函数创建的对 `Id` 象。
   * 通 `com.adobe.repository.infomodel.Lid` 过调用类的默认构造函数创建的对 `Lid` 象。
   * 包 `java.lang.String` 含资源的文件名。
   要指定资源的描述，请调用对象 `Resource` 的方法并 `setDescription` 传递包含描述的字符串。 在本例中，描述为 `"test resource"`。

1. 指定资源内容

   要为资源创建内容，请调用对 `RepositoryInfomodelFactoryBean` 象的方 `newResourceContent` 法，该方法返回一个对 `com.adobe.repository.infomodel.bean.ResourceContent` 象。 向对象添加 `ResourceContent` 内容。 在此示例中，通过执行以下任务来完成此操作：

   * 调用对 `ResourceContent` 象的方 `setDataDocument` 法并传入对象 `com.adobe.idp.Document`
   * 调用对 `ResourceContent` 象的方 `setSize` 法并传入对象的大小（以字节为单位） `Document`
   通过调用对象的方法并传 `Resource` 入对象，将 `setContent` 内容添加到资 `ResourceContent` 源。 有关详细信息，请参 [阅AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

1. 将资源写入目标文件夹

   调用 `ResourceRepositoryClient` 对象的方 `writeResource` 法，并传入文件夹的URI以及对 `Resource` 象。

**另请参阅**

[编写资源](aem-forms-repository.md#writing-resources)

[快速入门（SOAP模式）:使用Java API编写资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API编写资源 {#write-resources-using-the-web-service-api}

使用存储库服务API（Web服务）编写资源：

1. 包括项目文件

   * 创建一个使用base64的存储库WSDL的Microsoft .NET客户端组件。
   * 参考Microsoft .NET客户端程序集。

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用 `RepositoryServiceService` 其默认构造函数创建对象。 使用包 `Credentials` 含用户名和密码 `System.Net.NetworkCredential` 的对象设置其属性。

1. 指定资源的目标文件夹的URI

   指定资源的目标文件夹的URI。 在这种情况下，由于名为的资 `testResource` 源将存储在名为的文件夹中， `testFolder`因此该文件夹的URI为 `"/testFolder"`。 使用与Microsoft .NET Framework（例如，C#）兼容的语言时，将URI存储在对象 `System.String` 中。

1. 创建资源

   要创建资源，请调用类的默认构造函 `Resource` 数。 在此示例中，以下信息存储在对 `Resource` 象中：

   * 对 `com.adobe.repository.infomodel.Id` 象，通过为类调用默认构造函数创建，并 `Id` 将其分配给 `Resource` 对象的字段 `id` 。
   * 对 `com.adobe.repository.infomodel.Lid` 象，通过为类调用默认构造函数创建，并 `Lid` 将其分配给 `Resource` 对象的字段 `lid` 。
   * 包含资源文件名的字符串，该名称被分配给 `Resource` 对象的字 `name` 段。 此示例中使用的名称为 `"testResource"`。
   * 包含资源说明的字符串，该描述被分配给 `Resource` 对象的字 `description` 段。 此示例中使用的说明是 `"test resource"`。

1. 指定资源内容

   要为资源创建内容，请调用类的默认构造函 `ResourceContent` 数。 然后向对象添加 `ResourceContent` 内容。 在此示例中，通过执行以下任务来完成此操作：

   * 将包含 `BLOB` 文档的对象指定到该对 `ResourceContent` 象的字 `dataDocument` 段。
   * 将对象的大小(以字 `BLOB` 节为单位)指 `ResourceContent` 定给对象的字 `size` 段。
   通过将对象分配到对象的字 `ResourceContent` 段，将内 `Resource` 容添加到资 `content` 源。

1. 将资源写入目标文件夹

   调用 `RepositoryServiceService` 对象的方 `writeResource` 法，并传入文件夹的URI以及对 `Resource` 象。 传递 `null` 给其他两个参数。

**另请参阅**

[编写资源](aem-forms-repository.md#writing-resources)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 列表资源 {#listing-resources}

您可以通过列出资源来发现资源。 对存储库执行查询以查找与给定资源集合相关的所有资源。

组织资源后，您可以检查通过查看结构的特定分支创建的结构，就像在操作系统中一样。

上市资源按关系运作：资源是文件夹的成员。 会员资格由“会员”类型的关系表示。 在给定文件夹中列出资源时，您将通过关系“成员”查询与给定文件夹相关的资源。 关系是有方向性的：关系成员具有作为目标成员的源。 来源是资源，目标是父文件夹。

>[!NOTE]
>
>有关存储库服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-2}

要列出资源，请执行以下步骤：

1. 包括项目文件。
1. 创建服务客户端。
1. 指定文件夹路径。
1. 检索资源列表。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请包含代理文件。

**创建服务客户端**

在以编程方式创建资源集合之前，必须建立连接并提供凭据。 这是通过创建服务客户端来实现的。

**指定文件夹路径**

创建一个字符串，其中包含包含资源的文件夹的路径。 语法包括正斜杠，如本例所示：&quot;/*path*/*folder*&quot;。

**检索资源列表**

调用存储库服务方法以检索资源列表，指定目标文件夹的路径。

**另请参阅**

[使用Java API列出资源](aem-forms-repository.md#list-resources-using-the-java-api)

[使用Web服务API列出资源](aem-forms-repository.md#list-resources-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速入门](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API列出资源 {#list-resources-using-the-java-api}

使用存储库服务API(Java)列出资源：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件。

1. 创建服务客户端

   使用对 `ResourceRepositoryClient` 象的构造函数并传递一个包含连接属 `ServiceClientFactory` 性的对象来创建对象。

1. 指定文件夹路径

   指定要查询的资源集合的URI。 在这种情况下，其URI为 `"/testFolder"`。 URI存储为对 `java.lang.String` 象。

1. 检索资源列表

   调用对 `ResourceRepositoryClient` 象的方 `listMembers` 法并传入文件夹的URI。

   该方法返回一 `java.util.List` 组对 `com.adobe.repository.infomodel.bean.Resource` 象，这些对象是类型的 `com.adobe.repository.infomodel.bean.Relation` 源，并 `Relation.TYPE_MEMBER_OF` 且资源集合URI作为目标。 您可以通过迭代 `List` 检索每个资源。 在此示例中，将显示每个资源的名称和说明。

**另请参阅**

[列表资源](aem-forms-repository.md#listing-resources)。

[快速入门（SOAP模式）:使用Java API列出资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API列出资源 {#list-resources-using-the-web-service-api}

使用存储库服务API（Web服务）列出资源：

1. 包括项目文件

   * 创建一个使用存储库WSDL的Microsoft .NET客户端组件。
   * 参考Microsoft .NET客户端程序集。

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用 `RepositoryServiceService` 其默认构造函数创建对象。 使用包 `Credentials` 含用户名和密码 `System.Net.NetworkCredential` 的对象设置其属性。

1. 指定文件夹路径

   指定包含要查询的文件夹的URI的字符串。 在这种情况下，其URI为 `"/testFolder"`。 使用与Microsoft .NET Framework（例如，C#）兼容的语言时，将URI存储在对象 `System.String` 中。

1. 检索资源列表

   调用对 `RepositoryServiceService` 象的方 `listMembers` 法，并作为第一个参数传入文件夹的URI。 传递 `null` 给其他两个参数。

   该方法返回可转换为对象的对象数 `Resource` 组。 您可以遍历对象数组以检索每个相关资源。 在此示例中，将显示每个资源的名称和说明。

**另请参阅**

[列表资源](aem-forms-repository.md#listing-resources)。

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 阅读资源 {#reading-resources}

您可以从存储库中的给定位置检索资源，以读取其内容和元数据。 该工作流由初始化表单作为前端。 该过程具有读取表单所需的所有权限。 系统检索数据表单并从存储库中读取内容。 存储库授予对内容和元数据的访问权限（甚至能够知道资源的存在）。

存储库具有以下四种权限类型：

* **traverse**:允许您列出资源；即，读取资源元数据，但不读取资源内容
* **read**:允许您读取资源内容
* **write**:允许您编写资源内容
* **管理访问控制列表(ACL)**:允许您操作资源上的ACL

用户只能在拥有运行进程权限时运行进程。 IDE用户需要遍历和读取权限才能与存储库同步。 ACL仅在设计时应用，因为运行时在系统上下文中发生。

您可以使用Repository服务Java API或Web服务API以编程方式读取资源。

>[!NOTE]
>
>有关存储库服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-3}

要读取资源，请执行以下步骤：

1. 包括项目文件。
1. 创建存储库服务客户端。
1. 指定要读取的资源的URI。
1. 阅读资源。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请包含代理文件。

**创建服务客户端**

在以编程方式读取资源之前，必须建立连接并提供凭据。 这是通过创建服务客户端来实现的。

**指定要读取的资源的URI**

创建包含要读取的资源的URI的字符串。 语法包括正斜杠，如本例所示：“/*path*/*resource*”。

**阅读资源**

调用存储库服务方法以读取资源，指定URI。

**另请参阅**

[使用Java API读取资源](aem-forms-repository.md#read-resources-using-the-java-api)

[使用Web服务API读取资源](aem-forms-repository.md#reading-resources-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速入门](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API读取资源 {#read-resources-using-the-java-api}

使用存储库服务API(Java)读取资源：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件。

1. 创建服务客户端

   使用对 `ResourceRepositoryClient` 象的构造函数并传递一个包含连接属 `ServiceClientFactory` 性的对象来创建对象。

1. 指定要读取的资源的URI

   指定表示要检索的资源的URI的字符串值。 例如，假定资源名为 *testResource* ，它位于名为testFolder的文件夹中，请 *指定*, `/testFolder/testResource`

1. 阅读资源

   调用对 `ResourceRepositoryClient` 象的方 `readResource` 法，并将资源的URI作为参数传递。 此方法返回 `Resource` 表示资源的实例。

**另请参阅**

[阅读资源](aem-forms-repository.md#reading-resources)

[快速入门（SOAP模式）:使用Java API读取资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API读取资源 {#reading-resources-using-the-web-service-api}

使用存储库服务API（Web服务）读取资源：

1. 包括项目文件

   * 创建一个使用存储库WSDL的Microsoft .NET客户端组件。 (请参 [阅创建使用Base64编码的。NET客户端程序集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)。)
   * 参考Microsoft .NET客户端程序集。 (请参 [阅创建使用Base64编码的。NET客户端程序集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)。)

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用 `RepositoryServiceService` 其默认构造函数创建对象。 使用包 `Credentials` 含用户名和密码 `System.Net.NetworkCredential` 的对象设置其属性。

1. 指定要读取的资源的URI

   指定包含要检索的资源的URI的字符串。 在这种情况下，由于名为的资 `testResource` 源位于名为的文件夹中， `testFolder`因此其URI为 `"/testFolder/testResource"`。 使用与Microsoft .NET Framework（例如，C#）兼容的语言时，将URI存储在对象 `System.String` 中。

1. 阅读资源

   调用对 `RepositoryServiceService` 象的方 `readResource` 法，并将资源的URI作为第一个参数传递。 传递 `null` 给其他两个参数。

**另请参阅**

[阅读资源](aem-forms-repository.md#reading-resources)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 更新资源 {#updating-resources}

您可以检索和更新存储库中资源的内容。 更新资源时，版本之间对这些资源的访问控制将保持不变。 执行更新时，您可以选择增加主版本。 如果不选择增加主版本，则会自动更新次版本。

更新资源时，将根据指定的资源属性创建新版本。 更新资源时，需指定两个重要参数：目标URI和包含所有已更新元数据的资源实例。 请务必注意，如果不更改给定属性（例如，名称），则传入的实例中仍需要该属性。 解析内容时创建的关系将添加到特定版本，除非指定，否则不会提前。

例如，如果更新XDP文件并且该文件包含对其他资源的引用，则还将记录这些附加引用。 假定form.xdp版本1.0有两个外部引用：徽标和样式表，您随后将更新form.xdp，以便它现在具有三个引用：徽标、样式表和架构文件。 在更新过程中，存储库会将第三个关系（到架构文件）添加到其待处理的关系表中。 架构文件出现在存储库中后，该关系将自动形成。 但是，如果form.xdp版本2.0不再使用标志，form.xdp版本2.0将不与标志有关。

所有更新操作都是原子操作和事务操作。 例如，如果两个用户阅读同一资源并且都决定将版本1.0更新到版本2.0，则其中一个将成功，而其中一个将失败，则将维护存储库的完整性，并且两个用户都将收到确认成功或失败的消息。 如果事务不提交，则在出现数据库故障时它将回滚，并根据应用程序服务器超时或回滚。

您可以使用Repository服务Java API或Web服务API以编程方式更新资源。

>[!NOTE]
>
>有关存储库服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-4}

要更新资源，请执行以下步骤：

1. 包括项目文件。
1. 创建存储库服务客户端。
1. 检索要更新的资源。
1. 更新资源。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请包含代理文件。

**创建服务客户端**

在以编程方式读取资源之前，必须建立连接并提供凭据。 这是通过创建服务客户端来实现的。

**检索要更新的资源**

阅读资源。 有关详细信息，请参阅 [阅读资源](aem-forms-repository.md#reading-resources)。

**更新资源**

在资源中设置新信息并调用存储库服务方法以更新资源，指定URI、更新的资源以及如何更新版本信息。

**另请参阅**

[使用Java API更新资源](aem-forms-repository.md#update-resources-using-the-java-api)

[使用Web服务API更新资源](aem-forms-repository.md#update-resources-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速入门](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API更新资源 {#update-resources-using-the-java-api}

使用存储库服务API(Java)更新资源：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件。

1. 创建服务客户端

   使用对 `ResourceRepositoryClient` 象的构造函数并传递一个包含连接属 `ServiceClientFactory` 性的对象来创建对象。

1. 检索要更新的资源

   指定要检索和读取资源的资源的URI。 在此示例中，资源的URI为 `"/testFolder/testResource"`。

1. 更新资源

   更新 `Resource` 对象信息。 在此示例中，要更新描述，请调用对 `Resource` 象的方法并 `setDescription` 将新的描述字符串作为参数传递。

   然后调 `ServiceClientFactory` 用对象的方 `updateResource` 法，并传递以下参数：

   * 包 `java.lang.String` 含资源的URI的对象。
   * 包含 `Resource` 更新的资源信息的对象。
   * 指示 `boolean` 是更新主版本还是次版本的值。 在此示例中，传入一个 `true` 值，指示主版本将递增。

**另请参阅**

[更新资源](aem-forms-repository.md#updating-resources)

[快速入门（SOAP模式）:使用Java API更新资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API更新资源 {#update-resources-using-the-web-service-api}

使用存储库API（Web服务）更新资源：

1. 包括项目文件

   * 创建一个使用存储库WSDL的Microsoft .NET客户端组件。
   * 参考Microsoft .NET客户端程序集。

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用 `RepositoryServiceService` 其默认构造函数创建对象。 使用包 `Credentials` 含用户名和密码 `System.Net.NetworkCredential` 的对象设置其属性。

1. 检索要更新的资源

   指定要检索的资源的URI并读取资源。 在此示例中，资源的URI为 `"/testFolder/testResource"`。 有关详细信息，请参阅 [阅读资源](aem-forms-repository.md#reading-resources)。

1. 更新资源

   更新 `Resource` 对象信息。 在此示例中，要更新描述，请为对象的字段 `Resource` 分配一个新 `description` 值。

1. 调用对 `RepositoryServiceService` 象的方 `updateResource` 法，并传递以下参数：

   * 包 `System.String` 含资源的URI的对象。
   * 包含 `Resource` 更新的资源信息的对象。
   * 指示 `boolean` 是更新主版本还是次版本的值。 在此示例中，传入一个 `true` 值，指示主版本将递增。
   * 传 `null` 递其余两个参数。

**另请参阅**

[更新资源](aem-forms-repository.md#updating-resources)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 搜索资源 {#searching-for-resources}

您可以构建用于在存储库中搜索资源的查询，包括历史记录、相关资源和属性。

您可以检索相关资源以确定表单及其片段之间的依赖关系。 例如，如果您有表单，则可以确定表单使用的片段或外部资源。 如果您有图像，您还可以了解哪些表单使用该图像。 您还可以使用基于属性的筛选来搜索相关资源。 例如，您可以搜索使用指定名称的图像的所有表单，或查找具有指定名称的表单使用的任何图像。 您还可以使用资源属性进行搜索。 例如，您可以进行查询以查找其名称以给定字符串开头的所有表单或资源，该字符串可能包括“%”和“_”通配符。 记住，基于属性的搜索并非基于关系；此类搜索基于您对给定资源具有特定知识的假设。

**查询语句**

查 *询包含* 一个或多个与条件逻辑连接的语句。 语句 *由左操作数* 、运算符和右操作数组成。 此外，您还可以指定用于搜索结果的排序顺序。 排序 *顺序包含与SQL子句等效的信息*`ORDER BY` ，并且由元素组成，这些元素包含搜索所基于的属性以及指示使用升序还是降序的值。

您可以使用Repository service Java API以编程方式搜索资源。 目前，无法使用Web服务API搜索资源。

**排序行为**

调用对象的方法并指定排序 `ResourceRepositoryClient` 顺序时， `searchProperties` 不考虑排序顺序。 例如，假定您创建了一个包含三个自定义属性的资源，其中属 `name`性名 `secondName`为、和 `asecondName`。 然后，在属性名称上创建排序顺序元素，并将该 `ascending` 值设置为 `true`。

然后调用对 `ResourceRepositoryClient` 象的方 `searchProperties` 法并按排序顺序传递。 搜索将返回具有三个属性的正确资源。 但是，属性不按属性名称排序。 它们按添加顺序返回： `name`、 `secondName`和 `asecondName`。

>[!NOTE]
>
>有关存储库服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-5}

要搜索资源，请执行以下步骤：

1. 包括项目文件。
1. 创建存储库服务客户端。
1. 指定搜索的目标文件夹。
1. 指定搜索中使用的属性。
1. 创建搜索中使用的查询。
1. 为搜索结果创建排序顺序。
1. 搜索资源。
1. 从搜索结果中检索资源。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请包含代理文件。

**创建服务客户端**

在以编程方式读取资源之前，必须建立连接并提供凭据。 这是通过创建服务客户端来实现的。

**指定搜索的目标文件夹**

创建一个字符串，其中包含用于执行搜索的基本路径。 语法包括正斜杠，如本例所示：&quot;/*path*/*folder*&quot;。

**指定搜索中使用的属性**

您可以根据资源中包含的属性进行搜索。 指定用于执行搜索的属性的值。

**创建搜索中使用的查询**

使用语句和条件构建查询。 每个语句将指定搜索所基于的属性、要使用的条件以及要在搜索中使用的属性值。

**为搜索结果创建排序顺序**

排序顺序由元素组成，每个元素包含搜索中使用的属性之一以及指示是使用升序还是降序的值。

**搜索资源**

使用文件夹、查询和排序顺序搜索资源。 此外，指示搜索深度以及要返回的结果数的上限。

**从搜索结果中检索资源**

循环访问返回的资源列表并提取信息以进一步处理。

**另请参阅**

[使用Java API搜索资源](aem-forms-repository.md#search-for-resources-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速入门](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API搜索资源 {#search-for-resources-using-the-java-api}

使用存储库服务API(Java)搜索资源：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件。

1. 创建服务客户端

   使用对 `ResourceRepositoryClient` 象的构造函数并传递一个包含连接属 `ServiceClientFactory` 性的对象来创建对象。

1. 指定搜索的目标文件夹

   指定要从中执行搜索的基本路径的URI。 在此示例中，资源的URI为 `/testFolder`。

1. 指定搜索中使用的属性

   指定用于执行搜索的属性的值。 对象中存在属 `com.adobe.repository.infomodel.bean.Resource` 性。 在本例中，将对name属性进行搜索；因此，将 `java.lang.String` 使用包含 `Resource` 对象名称的对象，在本例中 `testResource` 是这样的。

1. 创建搜索中使用的查询

   要创建查询，请通过调 `com.adobe.repository.query.Query` 用类的默认构造函数来创建对象，并 `Query` 向查询添加语句。

   要创建语句，请调用类的构造函 `com.adobe.repository.query.Query.Statement` 数并传递以下参数：

   * 包含资源属性常数的左操作数。 在此示例中，由于资源的名称用作搜索的基础，因此使用静态 `Resource.ATTRIBUTE_NAME` 值。
   * 包含在搜索属性中使用的条件的运算符。 该运算符必须是类中的静态常量之 `Query.Statement` 一。 在此示例中，使用静态 `Query.Statement.OPERATOR_BEGINS_WITH` 值。
   * 包含用于执行搜索的属性值的右操作数。 在此示例中，使用名称属性( `String` 包含值 `"testResource"`)。
   通过调用对象的方法并传递类中包含 `Query.Statement` 的某个静 `setNamespace` 态值，指定左操作数的命名空 `com.adobe.repository.infomodel.bean.ResourceProperty` 间。 在此示例中， `ResourceProperty.RESERVED_NAMESPACE_REPOSITORY` 使用。

   通过调用对象的方法并传入对 `Query` 象，将每 `addStatement` 个语句添加到查 `Query.Statement` 询。

1. 为搜索结果创建排序顺序

   要指定搜索结果中使用的排序顺序，请通过为类调用默认的构造函数 `com.adobe.repository.query.sort.SortOrder` 来创建一个对象，并 `SortOrder` 向排序顺序添加元素。

   要为排序顺序创建元素，请调用类的一个构造函 `com.adobe.repository.query.sort.SortOrder.Element` 数。 在此示例中，由于资源的名称用作搜索的基础，因此静态值将用作第一个参数，并且升序( `Resource.ATTRIBUTE_NAME` 值 `boolean``true`)将指定为第二个参数。

   通过调用对象的方法并传入对象， `SortOrder` 将每个元素 `addSortElement` 添加到排序顺 `SortOrder.Element` 序中。

1. 搜索资源

   要根据属 `resources` 性属性搜索，请调用对象的 `ResourceRepositoryClient` 方法并传 `searchProperties` 递以下参数：

   * 包 `String` 含执行搜索的基本路径。 在这种情况下， `"/testFolder"` 使用。
   * 搜索中使用的查询。
   * 搜索深度。 在这种情况下， `com.adobe.repository.infomodel.bean.ResourceCollection.DEPTH_INFINITE` 将用于指示将使用基本路径及其所有文件夹。
   * 一个 `int` 值，它指示要从中选择未分页结果集的第一行。 在此示例中，指 `0` 定了。
   * 一个 `int` 值，它表示要返回的最大结果数。 在此示例中，指 `10` 定了。
   * 搜索中使用的排序顺序。
   该方法按指定 `java.util.List` 的排 `Resource` 序顺序返回一组对象。

1. 从搜索结果中检索资源

   要检索搜索结果中包含的资源，请对每个对象进行迭代， `List` 并将每个对象转换为一个对象， `Resource` 以便提取其信息。 在此示例中，将显示每个资源的名称。

**另请参阅**

[搜索资源](aem-forms-repository.md#searching-for-resources)

[快速入门（SOAP模式）:使用Java API搜索资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 创建资源关系 {#creating-resource-relationships}

您可以指定存储库中资源之间的关系。 有三种关系：

* **依赖**:资源依赖于其他资源的关系，这意味着存储库中需要所有相关资源。
* **会员资格（文件系统）**:资源位于给定文件夹中的关系。
* **自定义**:您在资源之间指定的关系。 例如，如果一个资源已弃用，而另一个资源已引入存储库，则可以指定您自己的替换关系。

您可以创建自己的自定义关系。 例如，如果将HTML文件存储在存储库中并且它使用图像，则可以指定一个自定义关系以将HTML文件与图像相关联（因为通常只有XML文件使用存储库定义的依赖关系与图像相关联）。 自定义关系的另一个示例是，如果您希望使用循环图结构而不是树结构构建存储库的不同视图。 您可以定义圆形图和查看器来遍历这些关系。 最后，您可以指示资源替换另一个资源，即使这两个资源完全不同。 在这种情况下，您可以定义保留范围之外的关系类型并在这两个资源之间建立关系。 您的应用程序将是唯一能够检测和处理关系的客户端，并且它可用于对该关系进行搜索。

您可以使用Repository service Java API或Web服务API以编程方式指定资源之间的关系。

>[!NOTE]
>
>有关存储库服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-6}

要指定两个资源之间的关系，请执行以下步骤：

1. 包括项目文件。
1. 创建存储库服务客户端。
1. 指定要关联的资源的URI。
1. 创建关系。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请包含代理文件。

**创建服务客户端**

在以编程方式读取资源之前，必须建立连接并提供凭据。 这是通过创建服务客户端来实现的。

**指定要关联的资源的URI**

创建包含要关联的资源的URI的字符串。 语法包括正斜杠，如本例所示：“/*path*/*resource*”。

**创建关系**

调用存储库服务方法以创建和指定关系类型。

**另请参阅**

[使用Java API创建关系资源](aem-forms-repository.md#create-relationship-resources-using-the-java-api)

[使用Web服务API创建关系资源](aem-forms-repository.md#create-relationship-resources-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速入门](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API创建关系资源 {#create-relationship-resources-using-the-java-api}

使用存储库服务Java API创建关系资源，执行以下任务：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件。

1. 创建服务客户端

   使用对 `ResourceRepositoryClient` 象的构造函数并传递一个包含连接属 `ServiceClientFactory` 性的对象来创建对象。

1. 指定要关联的资源的URI

   指定要关联的资源的URI。 在这种情况下，由于资源被命名并 `testResource1` 且位 `testResource2` 于名为的文件夹中，因此其URI `testFolder`是 `"/testFolder/testResource1"` 和 `"/testFolder/testResource2"`。 URI作为对象存 `java.lang.String` 储。 在此示例中，资源首先写入存储库，并检索其URI。 有关编写资源的详细信息，请参阅 [编写资源](aem-forms-repository.md#writing-resources)。

1. 创建关系

   调用对 `ResourceRepositoryClient` 象的方 `createRelationship` 法并传递以下参数：

   * 源资源的URI。
   * 目标资源的URI。
   * 关系的类型，它是类中的静态常量之 `com.adobe.repository.infomodel.bean.Relation` 一。 在本例中，通过指定值来建立依赖关系 `Relation.TYPE_DEPENDANT_OF`。
   * 指示 `boolean` 目标资源是否自动更新为基于新头资 `com.adobe.repository.infomodel.Id`源的标识符的值。 在本例中，由于依赖关系，因此指定 `true` 了值。
   您还可以通过调用对象的方法并传入以下参数来检索给定 `ResourceRepositoryClient` 资源的相 `getRelated` 关资源列表：

   * 要为其检索相关资源的资源的URI。 在此示例中，指定了源资 `"/testFolder/testResource1"`源()。
   * 一个 `boolean` 值，指示指定的资源是否是关系中的源资源。 在此示例中，指定 `true` 了值，因为这是情况。
   * 关系类型，它是类中的静态常量之 `Relation` 一。 在此示例中，使用之前使用的相同值来指定依赖关系： `Relation.TYPE_DEPENDANT_OF`.
   该方 `getRelated` 法返回一 `java.util.List` 系列对象，通过这些对象，您可以进行迭代来检索每个相关资源，并将包含在中的对象按 `Resource` 您的方式 `List``Resource` 转换为。 在此示例中， `testResource2` 应该位于返回的资源列表中。

**另请参阅**

[创建资源关系](aem-forms-repository.md#creating-resource-relationships)

[快速入门（SOAP模式）:使用Java API创建资源之间的关系](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API创建关系资源 {#create-relationship-resources-using-the-web-service-api}

使用存储库API（Web服务）创建关系资源：

1. 包括项目文件

   * 创建一个使用存储库WSDL的Microsoft .NET客户端组件。
   * 参考Microsoft .NET客户端程序集。

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用 `RepositoryServiceService` 其默认构造函数创建对象。 使用包 `Credentials` 含用户名和密码 `System.Net.NetworkCredential` 的对象设置其属性。

1. 指定要关联的资源的URI

   指定要关联的资源的URI。 在这种情况下，由于资源被命名并 `testResource1` 且位 `testResource2` 于名为的文件夹中，因此其URI `testFolder`是 `"/testFolder/testResource1"` 和 `"/testFolder/testResource2"`。 当使用与Microsoft .NET Framework（例如，C#）兼容的语言时，URI将作为对象存 `System.String` 储。 在此示例中，资源首先写入存储库，并检索其URI。 有关编写资源的详细信息，请参阅 [编写资源](aem-forms-repository.md#writing-resources)。

1. 创建关系

   调用对 `RepositoryServiceService` 象的方 `createRelationship` 法并传递以下参数：

   * 源资源的URI。
   * 目标资源的URI。
   * 关系的类型。 在本例中，通过指定值来建立依赖关系 `3`。
   * 一个 `boolean` 值，指示是否指定了关系类型。 在此示例中，指定 `true` 了值。
   * 指示 `boolean` 目标资源是否自动更新为基于新头资 `Id`源的标识符的值。 在本例中，由于依赖关系，因此指定 `true` 了值。
   * 指示 `boolean` 是否已指定目标头的值。 在此示例中，指定 `true` 了值。
   * 传递 `null` 最后一个参数。
   您还可以通过调用对象的方法并传入以下参数来检索给定 `RepositoryServiceService` 资源的相 `getRelated` 关资源列表：

   * 要为其检索相关资源的资源的URI。 在此示例中，指定了源资 `"/testFolder/testResource1"`源()。
   * 一个 `boolean` 值，指示指定的资源是否是关系中的源资源。 在此示例中，指定 `true` 了值，因为这是情况。
   * 指示 `boolean` 是否已指定源资源的值。 在此示例中，提供 `true` 了值。
   * 包含关系类型的整数数组。 在此示例中，通过在数组中使用与之前使用的相同值来指定依赖关系： `3`.
   * 传 `null` 递其余两个参数。
   该方 `getRelated` 法返回可转换为对象的对象数组，通过 `Resource` 该对象可以迭代检索每个相关资源。 在此示例中， `testResource2` 应该位于返回的资源列表中。

**另请参阅**

[创建资源关系](aem-forms-repository.md#creating-resource-relationships)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 锁定资源 {#locking-resources}

您可以锁定某个资源或一组资源，以供特定用户独占使用或在多个用户之间共享使用。 共享锁表示资源会发生某些情况，但不会阻止任何其他人对该资源执行操作。 应将共享锁视为信令机制。 独占锁表示锁定资源的用户将更改资源，并且锁确保在用户不再需要访问资源并释放锁之前，其他人不能这样做。 如果存储库管理员解锁了某个资源，则该资源上的所有独占和共享锁将自动删除。 此类操作适用于用户不再可用且未解锁资源的情况。

当资源被锁定时，当您查看位于Workbench中的“资源”选项卡时，会显示一个锁图标，如下图所示。

![lr_lr_lockrepository](assets/lr_lr_lockrepository.png)

您可以使用Repository服务Java API或Web服务API以编程方式控制对资源的访问。

>[!NOTE]
>
>有关存储库服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-7}

要锁定和解锁资源，请执行以下步骤：

1. 包括项目文件。
1. 创建存储库服务客户端。
1. 指定要锁定的资源的URI。
1. 锁定资源。
1. 检索资源的锁定。
1. 解锁资源

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请包含代理文件。

**创建服务客户端**

在以编程方式读取资源之前，必须建立连接并提供凭据。 这是通过创建服务客户端来实现的。

**指定要锁定的资源的URI**

创建包含要锁定的资源的URI的字符串。 语法包括正斜杠，如本例所示：“/*path*/*resource*”。

**锁定资源**

调用存储库服务方法以锁定资源，指定URI、锁定类型和锁定深度。

**检索资源的锁**

调用存储库服务方法以检索资源的锁，指定URI。

**解锁资源**

调用存储库服务方法以解锁资源，指定URI。

**另请参阅**

[使用Java API锁定资源](aem-forms-repository.md#lock-resources-using-the-java-api)

[使用Web服务API锁定资源](aem-forms-repository.md#lock-resources-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速入门](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API锁定资源 {#lock-resources-using-the-java-api}

使用存储库服务API(Java)锁定资源：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件。

1. 创建服务客户端

   使用对 `ResourceRepositoryClient` 象的构造函数并传递一个包含连接属 `ServiceClientFactory` 性的对象来创建对象。

1. 指定要锁定的资源的URI

   指定要锁定的资源的URI。 在这种情况下，由于名为的资 `testResource` 源位于名为的文件夹中， `testFolder`因此其URI为 `"/testFolder/testResource"`。 URI存储为对 `java.lang.String` 象。

1. 锁定资源

   调用对 `ResourceRepositoryClient` 象的方 `lockResource` 法并传递以下参数：

   * 资源的URI。
   * 锁定范围。 在此示例中，由于资源将被锁定以专用，因此锁定范围将指定为 `com.adobe.repository.infomodel.bean.Lock.SCOPE_EXCLUSIVE`。
   * 锁定深度。 在此示例中，由于锁定将仅应用于特定资源且不应用于其任何成员或子资源，因此锁定深度指定为 `Lock.DEPTH_ZERO`。
   >[!NOTE]
   >
   >需要四个参数的 `lockResource` 方法的重载版本将引发异常。 确保使用需要 `lockResource` 三个参数的方法，如本演练中所示。

1. 检索资源的锁

   调用对 `ResourceRepositoryClient` 象的方 `getLocks` 法，并将资源的URI作为参数传递。 该方法返回可通过其进行迭代的Lock对象列表。 在此示例中，通过分别调用每个锁对象的方法和方法，为每个对象打印锁所有者、深 `getOwnerUserId`度 `getDepth`和 `getType` 范围。

1. 解锁资源

   调用对 `ResourceRepositoryClient` 象的方 `unlockResource` 法，并将资源的URI作为参数传递。 有关详细信息，请参 [阅AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**另请参阅**

[锁定资源](aem-forms-repository.md#locking-resources)

[快速入门（SOAP模式）:使用Java API锁定资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API锁定资源 {#lock-resources-using-the-web-service-api}

使用存储库服务API（Web服务）锁定资源：

1. 包括项目文件

   * 创建一个使用Base64的存储库WSDL的Microsoft .NET客户端组件。
   * 参考Microsoft .NET客户端程序集。

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用 `RepositoryServiceService` 其默认构造函数创建对象。 使用包 `Credentials` 含用户名和密码 `System.Net.NetworkCredential` 的对象设置其属性。

1. 指定要锁定的资源的URI

   指定包含要锁定的资源的URI的字符串。 在这种情况下，由于名为的资 `testResource` 源在文件夹中， `testFolder`因此其URI为 `"/testFolder/testResource"`。 使用与Microsoft .NET Framework（例如，C#）兼容的语言时，将URI存储在对象 `System.String` 中。

1. 锁定资源

   调用对 `RepositoryServiceService` 象的方 `lockResource` 法并传递以下参数：

   * 资源的URI。
   * 锁定范围。 在此示例中，由于资源将被锁定以专用，因此锁定范围将指定为 `11`。
   * 锁定深度。 在此示例中，由于锁定将仅应用于特定资源且不应用于其任何成员或子资源，因此锁定深度指定为 `2`。
   * 一个 `int` 值，指示锁定过期前的秒数。 在此示例中，使用的 `1000` 值为。
   * 传递 `null` 最后一个参数。

1. 检索资源的锁

   调用对 `RepositoryServiceService` 象的方 `getLocks` 法，并将资源的URI作为第一个参数和第二个参数 `null` 传递给它。 该方法返回一个包 `object` 含可通 `Lock` 过其进行迭代的对象的数组。 在此示例中，通过分别访问每个对象的字段、深度和范围，为每 `Lock` 个对象打 `ownerUserId`印 `depth`锁所有者、深 `type` 度和范围。

1. 解锁资源

   调用对 `RepositoryServiceService` 象的方 `unlockResource` 法，并将资源的URI作为第一个参数和第二个参数 `null` 传递给它。

**另请参阅**

[锁定资源](aem-forms-repository.md#locking-resources)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 删除资源 {#deleting-resources}

您可以使用存储库服务Java API(SOAP)从存储库中的给定位置以编程方式删除资源。

删除资源时，删除操作通常是永久的，但在某些情况下，ECM存储库可能会根据其历史机制存储资源的版本。 因此，删除资源时，务必确保您不再需要该资源。 删除资源的常见原因包括需要增加数据库中的可用空间。 您可以删除某个资源版本，但是如果删除，则必须指定资源标识符，而不是其逻辑标识符(LID)或路径。 如果删除文件夹，则该文件夹中的所有内容（包括子文件夹和资源）都将自动删除。

相关资源不会被删除。 例如，如果您有一个使用logo.gif文件的表单，而您删除logo.gif，则关系将存储在待处理的关系表中。 作为替代方法，对于版本弃用，请将最新版本的对象状态设置为已弃用。

在ECM系统中，删除操作不是事务安全的。 例如，如果尝试删除100个资源，而第50个资源上的操作失败，则前49个实例将被删除，但其余实例将不会删除。 否则，默认行为为回滚（非承诺）。

>[!NOTE]
>
>将方法与 `com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient.deleteResources()` ECM存储库（EMC Documentum Content server和IBM FileNet P8 Content Manager）一起使用时，如果某个指定资源的删除失败，则不会回滚事务，这意味着已删除的文件将无法取消删除。

>[!NOTE]
>
>有关存储库服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-8}

要删除资源，请执行以下步骤：

1. 包括项目文件。
1. 创建存储库服务客户端。
1. 指定要删除的资源的URI。
1. 删除资源。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请包含代理文件。

**创建服务客户端**

在以编程方式读取资源之前，必须建立连接并提供凭据。 这是通过创建服务客户端来实现的。

**指定要删除的资源的URI**

创建一个字符串，其中包含要删除的资源的URI。 语法包括正斜杠，如本例所示：“/*path*/*resource*”。 如果要删除的资源是文件夹，则删除将是递归的。

**删除资源**

调用存储库服务方法以删除资源，指定URI。

**另请参阅**

[使用Java API删除资源](aem-forms-repository.md#delete-resources-using-the-java-api-soap)

[使用Web服务API删除资源](aem-forms-repository.md#delete-resources-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速入门](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API(SOAP)删除资源 {#delete-resources-using-the-java-api-soap}

使用存储库API(Java)删除资源：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件。

1. 创建服务客户端

   使用对 `ResourceRepositoryClient` 象的构造函数并传递一个包含连接属 `ServiceClientFactory` 性的对象来创建对象。

1. 指定要删除的资源的URI

   指定要检索的资源的URI。 在这种情况下，由于名为testResourceToBeDeleted的资源位于名为testFolder的文件夹中，因此其URI为 `/testFolder/testResourceToBeDeleted`。 URI存储为对 `java.lang.String` 象。 在此示例中，首先将资源写入存储库，并检索其URI。 有关编写资源的详细信息，请参阅 [编写资源](aem-forms-repository.md#writing-resources)。

1. 删除资源

   调用对 `ResourceRepositoryClient` 象的方 `deleteResource` 法，并将资源的URI作为参数传递。

**另请参阅**

[删除资源](aem-forms-repository.md#deleting-resources)

[快速入门（SOAP模式）:使用Java API搜索资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API删除资源 {#delete-resources-using-the-web-service-api}

使用存储库API（Web服务）删除资源：

1. 包括项目文件

   * 创建一个使用Base64的存储库WSDL的Microsoft .NET客户端组件。
   * 参考Microsoft .NET客户端程序集。

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用 `RepositoryServiceService` 其默认构造函数创建对象。 使用包 `Credentials` 含用户名和密码 `System.Net.NetworkCredential` 的对象设置其属性。

1. 指定要删除的资源的URI

   指定要检索的资源的URI。 在这种情况下，由于名为的资 `testResourceToBeDeleted` 源位于名为的文件夹中， `testFolder`因此其URI为 `"/testFolder/testResourceToBeDeleted"`。 在此示例中，首先将资源写入存储库，并检索其URI。 有关编写资源的详细信息，请参阅 [编写资源](aem-forms-repository.md#writing-resources)。

1. 删除资源

   调用对 `RepositoryServiceService` 象的方 `deleteResources` 法，并传递包 `System.String` 含资源URI的数组作为第一个参数。 传递 `null` 第二个参数。

**另请参阅**

[删除资源](aem-forms-repository.md#deleting-resources)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
