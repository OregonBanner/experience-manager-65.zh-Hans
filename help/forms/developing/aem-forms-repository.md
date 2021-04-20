---
title: 使用AEM Forms Repository
seo-title: 使用AEM Forms Repository
description: 管理AEM Forms存储库，以使用Java API和Web服务API创建文件夹、写入、列表、读取、更新和搜索资源。 此外，了解如何创建资源关系、锁定和删除资源。
seo-description: 使用Java API和Web服务API管理AEM Forms存储库以创建文件夹、写入、列表、读取、更新资源和搜索资源。 此外，了解如何创建资源关系、锁定和删除资源。
uuid: 6ead49f9-ca0d-4ee4-86a6-0a9ced6ec4f8
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d2c95881-6c02-4e34-85af-84607df54287
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '9158'
ht-degree: 0%

---


# 使用AEM Forms Repository {#working-with-aem-forms-repository}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

**关于存储库服务**

存储库服务向AEM Forms提供资源存储和管理服务。 当开发人员创建&#x200B;*AEM Forms*&#x200B;应用程序时，他们可以在存储库中而不是文件系统中部署资源。 资产可以包括任何类型的附属品，包括XML表单、PDF forms(包括Acrobat表单)、表单片段、图像、用户档案、策略、SWF文件、DDX文件、XML模式、WSDL文件和测试数据。

例如，请考虑以下名为&#x200B;*Applications/FormsApplication*&#x200B;的Forms应用程序：

![ww_ww_formrepository](assets/ww_ww_formrepository.png)

请注意，FormsFolder中有一个名为Loan.xdp的文件。 要访问此表单设计，请指定完整路径（包括版本）：`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。

>[!NOTE]
>
>有关使用Workbench创建Forms应用程序的信息，请参阅[Workbench帮助](https://www.adobe.com/go/learn_aemforms_workbench_63)。

位于AEM Forms存储库中的资源的路径为：

`Applications/Application-name/Application-version/Folder.../Filename`

以下值显示一些URI值的示例：

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

>[!NOTE]
>
>您可以使用Web浏览器浏览AEM Forms存储库。 要浏览存储库，请在Web浏览器`https://[server name]:[server port]/repository`中输入以下URL。 您可以使用Web浏览器验证与使用AEM Forms存储库部分关联的快速开始结果。 例如，如果向AEM Forms存储库添加内容，则可以在Web浏览器中查看内容。 (请参阅[快速开始（SOAP模式）：使用Java API](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)编写资源。)

存储库API提供了许多操作，您可以使用这些操作来存储和检索存储库中的信息。 例如，当处理应用程序时需要资源时，您可以获取资源列表或检索存储在存储库中的特定资源。

>[!NOTE]
>
>存储库API不能用于与Content Services交互（已弃用）。 要与内容服务交互（已弃用），请使用文档管理API。

使用存储库服务API，您可以完成以下任务:

* 创建文件夹。 请参阅[创建文件夹](aem-forms-repository.md#creating-folders)。
* 编写资源及其属性。 请参阅[编写资源](aem-forms-repository.md#writing-resources)。
* 列表给定集合中的资源或与其他资源相关的资源。 请参阅[列出资源](aem-forms-repository.md#listing-resources)。
* 阅读资源及其属性。 请参阅[阅读资源](aem-forms-repository.md#reading-resources)。
* 更新资源及其属性。 请参阅[更新资源](aem-forms-repository.md#updating-resources)。
* 搜索资源，包括其历史记录、相关资源和属性。 请参阅[搜索资源](aem-forms-repository.md#searching-for-resources)。
* 指定资源之间的关系。 请参阅[创建资源关系](aem-forms-repository.md#creating-resource-relationships)。
* 管理资源访问控制，包括锁定和解锁资源，以及读写访问控制列表(ACL)。 请参阅[锁定资源](aem-forms-repository.md#locking-resources)。
* 删除资源及其属性。 请参阅[删除资源](aem-forms-repository.md#deleting-resources)。

>[!NOTE]
>
>使用存储库API，您无法通过使用ECM存储库管理资源访问控制、搜索资源或指定资源关系。

>[!NOTE]
>
>将加密的PDF写入存储库后，无法使用自动关系提取功能。 否则，加密的PDF可以存储在存储库中，并在以后检索。 在从存储库检索PDF后，检索器可以选择解密它。

>[!NOTE]
>
>有关存储库服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 创建文件夹{#creating-folders}

文件夹（资源集合）用于按有组织的分组存储对象（文件或资源）。 文件夹可以包含资源和其他文件夹，也称为子文件夹。 资源一次只能存储在一个文件夹中。

文件从文件夹继承访问控制列表(ACL)，子文件夹从父文件夹继承ACL。 因此，在创建子文件夹之前，父文件夹必须存在。 IDE仅允许您逐个文件夹进行交互，而不允许逐个文件进行交互。 您无法对文件夹进行版本化，也无需这样做；文件夹不包含数据本身。 相反，它只是包含数据的资源的容器。 默认的ACL是系统级权限，这意味着用户必须具有系统级权限（读取、写入、遍历、管理ACL），直到有人授予他们对特定文件夹的权限。 ACL仅在IDE中有效。

>[!NOTE]
>
>有关存储库服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary-of-steps}的摘要

要创建文件夹，请执行以下步骤：

1. 包括项目文件。
1. 创建服务客户端。
1. 创建文件夹。
1. 将文件夹写入存储库。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请包含代理文件。

**创建服务客户端**

在以编程方式创建资源集合之前，必须建立连接并提供凭据。 这是通过创建服务客户端实现的。

**创建文件夹**

调用存储库服务方法以创建资源集合，并用标识信息填充资源集合，包括其UUID、文件夹名称和说明。

**将文件夹写入存储库**

调用存储库服务方法以写入资源集合，同时指定目标文件夹的URI。

**另请参阅**

[使用Java API创建文件夹](aem-forms-repository.md#create-folders-using-the-java-api)

[使用Web服务API创建文件夹](aem-forms-repository.md#create-folders-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速开始](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API {#create-folders-using-the-java-api}创建文件夹

使用存储库服务API(Java)创建文件夹：

1. 包括项目文件

   在Java项目的类路径中包含项目文件。

1. 创建服务客户端

   使用`ResourceRepositoryClient`对象的构造函数并传递包含连接属性的`ServiceClientFactory`对象，创建对象。

1. 创建文件夹

   要创建资源集合，必须首先创建`com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean`对象。

   调用`repositoryInfomodelFactoryBean`对象的`newResourceCollection`方法，并传递以下参数：

   * 要分配给资源的`com.adobe.repository.infomodel.Id` UUID标识符。
   * 要分配给资源的`com.adobe.repository.infomodel.Lid` UUID标识符。
   * 包含资源集合名称的`java.lang.String`。 例如，`FormsFolder`。

   该方法返回表示新文件夹的`com.adobe.repository.infomodel.bean.ResourceCollection`对象。

   使用`setDescription`方法设置文件夹的说明，并传递以下参数：

   * 描述资源集合的`String`。 在此示例中，使用`"test Folder"``.`


1. 将文件夹写入存储库

   调用`ResourceRepositoryClient`对象的`writeResource`方法并传入文件夹和`ResourceCollection`对象的URI。 例如，文件夹的URI可以是以下值`/Applications/FormsApplication/1.0/`。

   该方法返回新创建的`com.adobe.repository.infomodel.bean.Resource`对象的实例。 例如，可以通过调用`com.adobe.repository.infomodel.bean.Resource`对象的`getId`方法来检索新资源的标识符值。

**另请参阅**

[创建文件夹](aem-forms-repository.md#creating-folders)

[快速开始（SOAP模式）：使用Java API创建文件夹](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#create-folders-using-the-web-service-api}创建文件夹

使用存储库服务API（Web服务）创建文件夹：

1. 包括项目文件

   * 创建一个使用base64使用存储库WSDL的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用其默认构造函数创建`RepositoryServiceService`对象。 使用包含用户名和密码的`System.Net.NetworkCredential`对象设置其`Credentials`属性。

1. 创建文件夹

   使用`ResourceCollection`类的默认构造函数创建文件夹并传递以下参数：

   * `Id`对象，通过为`Id`类调用默认构造函数创建，并分配给`Resource`对象的`id`字段。
   * `Lid`对象，通过为`Lid`类调用默认构造函数创建，并分配给`Resource`对象的`lid`字段。
   * 包含资源集合名称的字符串，该名称已分配给`Resource`对象的`name`字段。 此示例中使用的名称为`"testfolder"`。
   * 包含资源集合描述的字符串，该描述被分配给`Resource`对象的`description`字段。 此示例中使用的描述为`"test folder"`。

1. 将文件夹写入存储库

   调用`RepositoryServiceService`对象的`writeResource`方法并传递以下参数：

   * 要创建文件夹的路径。
   * 表示文件夹的`ResourceCollection`对象。
   * 传递`null`作为其他两个参数。

**另请参阅**

[创建文件夹](aem-forms-repository.md#creating-folders)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 写入资源{#writing-resources}

您可以在存储库中的给定位置创建资源。 正常文件大小受数据库限制和会话超时的影响。 对于默认配置，文件限制为25 MB。 要增大或减小最大文件大小，必须更改数据库配置。

写入资源等效于将数据存储在存储库中。 将资源写入存储库后，存储库生态系统中的所有客户端都可以访问该资源。 将XML模式、XDP文件和XSD文件等资源写入存储库时，将根据MIME类型分析内容。 如果支持MIME类型，则分析器确定是否与其他内容存在隐含关系。 例如，如果层叠样式表(CSS)具有引用公用CSS的相对URL，则您也应将公用CSS提交到存储库中。 两个资源之间的关系被存储为30天不可调节的待处理关系。 在30天内将公用CSS提交到存储库时，将形成关系。

创建资源时，访问控制列表(ACL)会从父文件夹继承。 在创建初始资源或文件夹之前，根文件夹具有系统级权限，此时该资源或文件夹将获得默认的ACL权限。

您可以使用存储库服务Java API或Web服务API以编程方式写入资源。

>[!NOTE]
>
>有关存储库服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-1}的摘要

要编写资源，请执行以下步骤：

1. 包括项目文件。
1. 创建存储库服务客户端。
1. 指定要读取的资源的URI。
1. 阅读资源。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请包含代理文件。

**创建服务客户端**

在以编程方式读取资源之前，必须建立连接并提供凭据。 这是通过创建服务客户端实现的。

**为资源指定目标文件夹的URI**

创建一个字符串，其中包含要读取的资源的URI。 语法包括正斜杠，如本例所示：&quot;/*path*/*folder*&quot;。

**创建资源**

调用存储库服务方法以创建资源，并使用标识信息填充资源，包括其UUID、资源名称和说明。

**指定资源内容**

调用存储库服务方法以创建资源内容，并将该内容存储在资源中。

**将资源写入目标文件夹**

调用存储库服务方法以写入资源，同时指定目标文件夹的URI。

**另请参阅**

[使用Java API写入资源](aem-forms-repository.md#write-resources-using-the-java-api)

[使用Web服务API编写资源](aem-forms-repository.md#write-resources-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速开始](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API {#write-resources-using-the-java-api}写入资源

使用存储库服务API(Java)编写资源：

1. 包括项目文件

   将客户端JAR文件包含在Java项目的类路径中。

1. 创建服务客户端

   使用`ResourceRepositoryClient`对象的构造函数并传递包含连接属性的`ServiceClientFactory`对象，创建对象。

1. 为资源指定目标文件夹的URI

   为资源指定目标文件夹的URI。 在这种情况下，由于名为`testResource`的资源将存储在名为`testFolder`的文件夹中，因此该文件夹的URI为`"/testFolder"`。 URI将作为`java.lang.String`对象存储。

1. 创建资源

   要创建资源，必须首先创建`com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean`对象。

   调用`RepositoryInfomodelFactoryBean`对象的`newResource`方法，该方法创建`com.adobe.repository.infomodel.bean.Resource`对象。 在此示例中，提供了以下参数：

   * `com.adobe.repository.infomodel.Id`对象，通过调用`Id`类的默认构造函数创建。
   * `com.adobe.repository.infomodel.Lid`对象，通过调用`Lid`类的默认构造函数创建。
   * 包含资源文件名的`java.lang.String`。

   要指定资源的描述，请调用`Resource`对象的`setDescription`方法并传递包含该描述的字符串。 在此示例中，说明为`"test resource"`。

1. 指定资源内容

   要为资源创建内容，请调用`RepositoryInfomodelFactoryBean`对象的`newResourceContent`方法，该方法返回`com.adobe.repository.infomodel.bean.ResourceContent`对象。 向`ResourceContent`对象添加内容。 在此示例中，可通过执行以下任务来完成此操作：

   * 调用`ResourceContent`对象的`setDataDocument`方法并传入`com.adobe.idp.Document`对象
   * 调用`ResourceContent`对象的`setSize`方法并传入`Document`对象的字节大小

   通过调用`Resource`对象的`setContent`方法并传入`ResourceContent`对象，将内容添加到资源中。 有关详细信息，请参阅[AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

1. 将资源写入目标文件夹

   调用`ResourceRepositoryClient`对象的`writeResource`方法并传入文件夹的URI以及`Resource`对象。

**另请参阅**

[编写资源](aem-forms-repository.md#writing-resources)

[快速开始（SOAP模式）：使用Java API编写资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#write-resources-using-the-web-service-api}写入资源

使用存储库服务API（Web服务）编写资源：

1. 包括项目文件

   * 创建一个使用base64使用存储库WSDL的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用其默认构造函数创建`RepositoryServiceService`对象。 使用包含用户名和密码的`System.Net.NetworkCredential`对象设置其`Credentials`属性。

1. 为资源指定目标文件夹的URI

   为资源指定目标文件夹的URI。 在这种情况下，由于名为`testResource`的资源将存储在名为`testFolder`的文件夹中，因此该文件夹的URI为`"/testFolder"`。 使用与Microsoft .NET Framework兼容的语言（例如C#）时，将URI存储在`System.String`对象中。

1. 创建资源

   要创建资源，请调用`Resource`类的默认构造函数。 在此示例中，以下信息存储在`Resource`对象中：

   * `com.adobe.repository.infomodel.Id`对象，通过为`Id`类调用默认构造函数创建，并分配给`Resource`对象的`id`字段。
   * `com.adobe.repository.infomodel.Lid`对象，通过为`Lid`类调用默认构造函数创建，并分配给`Resource`对象的`lid`字段。
   * 一个字符串，包含资源的文件名，它被分配给`Resource`对象的`name`字段。 此示例中使用的名称为`"testResource"`。
   * 包含资源描述的字符串，该描述被分配给`Resource`对象的`description`字段。 此示例中使用的描述为`"test resource"`。

1. 指定资源内容

   要为资源创建内容，请调用`ResourceContent`类的默认构造函数。 然后，向`ResourceContent`对象添加内容。 在此示例中，可通过执行以下任务来完成此操作：

   * 将包含文档的`BLOB`对象指定到`ResourceContent`对象的`dataDocument`字段。
   * 将`BLOB`对象的大小（以字节为单位）分配给`ResourceContent`对象的`size`字段。

   通过将`ResourceContent`对象分配给`Resource`对象的`content`字段，将内容添加到资源。

1. 将资源写入目标文件夹

   调用`RepositoryServiceService`对象的`writeResource`方法并传入文件夹的URI以及`Resource`对象。 传递`null`作为其他两个参数。

**另请参阅**

[编写资源](aem-forms-repository.md#writing-resources)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 列出资源{#listing-resources}

您可以通过列出资源来发现资源。 对存储库执行查询，以查找与给定资源集合相关的所有资源。

组织资源后，您可以检查通过查看结构的特定分支所创建的结构，就像在操作系统中一样。

按关系运作的上市资源：资源是文件夹的成员。 会员资格由“会员”类型的关系表示。 在给定文件夹中列表资源时，您将通过关系“成员”查询与给定文件夹相关的资源。 关系是方向性的：关系的成员具有作为目标成员的源。 来源是资源；目标是父文件夹。

>[!NOTE]
>
>有关存储库服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-2}的摘要

要列表资源，请执行以下步骤：

1. 包括项目文件。
1. 创建服务客户端。
1. 指定文件夹路径。
1. 检索资源的列表。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请包含代理文件。

**创建服务客户端**

在以编程方式创建资源集合之前，必须建立连接并提供凭据。 这是通过创建服务客户端实现的。

**指定文件夹路径**

创建一个字符串，其中包含包含资源的文件夹的路径。 语法包括正斜杠，如本例所示：&quot;/*path*/*folder*&quot;。

**检索资源列表**

调用存储库服务方法以检索资源的列表，并指定目标文件夹的路径。

**另请参阅**

[列表资源（使用Java API）](aem-forms-repository.md#list-resources-using-the-java-api)

[列表资源（使用Web服务API）](aem-forms-repository.md#list-resources-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速开始](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 列表资源（使用Java API {#list-resources-using-the-java-api}）

列表资源(通过使用Repository Service API(Java)):

1. 包括项目文件

   将客户端JAR文件包含在Java项目的类路径中。

1. 创建服务客户端

   使用`ResourceRepositoryClient`对象的构造函数并传递包含连接属性的`ServiceClientFactory`对象，创建对象。

1. 指定文件夹路径

   指定要查询的资源集合的URI。 在这种情况下，其URI为`"/testFolder"`。 URI将作为`java.lang.String`对象存储。

1. 检索资源列表

   调用`ResourceRepositoryClient`对象的`listMembers`方法并传入文件夹的URI。

   该方法返回`com.adobe.repository.infomodel.bean.Resource`对象的`java.util.List`，这些对象是`Relation.TYPE_MEMBER_OF`类型`com.adobe.repository.infomodel.bean.Relation`的源，并将资源集合URI作为目标。 您可以循环访问此`List`以检索每个资源。 在此示例中，将显示每个资源的名称和说明。

**另请参阅**

[列出资源](aem-forms-repository.md#listing-resources)。

[快速开始（SOAP模式）：使用Java API列出资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 列表资源（使用Web服务API {#list-resources-using-the-web-service-api}）

列表资源(使用存储库服务API（Web服务）):

1. 包括项目文件

   * 创建一个使用存储库WSDL的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用其默认构造函数创建`RepositoryServiceService`对象。 使用包含用户名和密码的`System.Net.NetworkCredential`对象设置其`Credentials`属性。

1. 指定文件夹路径

   指定包含要查询的文件夹的URI的字符串。 在这种情况下，其URI为`"/testFolder"`。 使用与Microsoft .NET Framework（例如C#）兼容的语言时，将URI存储在`System.String`对象中。

1. 检索资源列表

   调用`RepositoryServiceService`对象的`listMembers`方法，并作为第一个参数传入文件夹的URI。 传递`null`作为其他两个参数。

   该方法返回可转换为`Resource`对象的对象数组。 您可以在对象数组中进行迭代，以检索每个相关资源。 在此示例中，将显示每个资源的名称和说明。

**另请参阅**

[列出资源](aem-forms-repository.md#listing-resources)。

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 读取资源{#reading-resources}

您可以从存储库中的给定位置检索资源，以读取其内容和元数据。 该工作流由初始化表单作为前端。 该过程具有读取表单所需的所有权限。 系统检索数据表单并从存储库读取内容。 存储库授予对内容和元数据的访问权限（甚至能够知道资源存在）。

存储库具有以下四种权限类型：

* **traverse**:允许您列表资源；即，读取资源元数据，但不读取资源内容
* **read**:允许您读取资源内容
* **写**:允许您写入资源内容
* **管理访问控制列表(ACL)**:允许您在资源上操作ACL

用户只有在具有运行进程的权限时才能运行进程。 IDE用户需要具有遍历和读取权限才能与存储库同步。 ACL仅在设计时应用，因为运行时在系统上下文中发生。

您可以使用Repository服务Java API或Web服务API以编程方式读取资源。

>[!NOTE]
>
>有关存储库服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-3}的摘要

要读取资源，请执行以下步骤：

1. 包括项目文件。
1. 创建存储库服务客户端。
1. 指定要读取的资源的URI。
1. 阅读资源。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请包含代理文件。

**创建服务客户端**

在以编程方式读取资源之前，必须建立连接并提供凭据。 这是通过创建服务客户端实现的。

**指定要读取的资源的URI**

创建一个字符串，其中包含要读取的资源的URI。 语法包括正斜杠，如本例所示：&quot;/*path*/*resource*&quot;。

**读取资源**

调用存储库服务方法以读取资源，并指定URI。

**另请参阅**

[使用Java API读取资源](aem-forms-repository.md#read-resources-using-the-java-api)

[使用Web服务API读取资源](aem-forms-repository.md#reading-resources-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速开始](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API {#read-resources-using-the-java-api}读取资源

使用存储库服务API(Java)读取资源：

1. 包括项目文件

   将客户端JAR文件包含在Java项目的类路径中。

1. 创建服务客户端

   使用`ResourceRepositoryClient`对象的构造函数并传递包含连接属性的`ServiceClientFactory`对象，创建对象。

1. 指定要读取的资源的URI

   指定表示要检索的资源的URI的字符串值。 例如，假定资源名为&#x200B;*testResource*，该资源位于名为&#x200B;*testFolder*&#x200B;的文件夹中，请指定`/testFolder/testResource`。

1. 读取资源

   调用`ResourceRepositoryClient`对象的`readResource`方法，并将资源的URI作为参数传递。 此方法返回表示资源的`Resource`实例。

**另请参阅**

[阅读资源](aem-forms-repository.md#reading-resources)

[快速开始（SOAP模式）：使用Java API读取资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#reading-resources-using-the-web-service-api}读取资源

使用存储库服务API（Web服务）读取资源：

1. 包括项目文件

   * 创建一个使用存储库WSDL的Microsoft .NET客户端程序集。 （请参阅[创建使用Base64编码](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)的.NET客户端程序集。）
   * 引用Microsoft .NET客户端程序集。 （请参阅[创建使用Base64编码](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)的.NET客户端程序集。）

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用其默认构造函数创建`RepositoryServiceService`对象。 使用包含用户名和密码的`System.Net.NetworkCredential`对象设置其`Credentials`属性。

1. 指定要读取的资源的URI

   指定包含要检索的资源的URI的字符串。 在这种情况下，由于名为`testResource`的资源位于名为`testFolder`的文件夹中，其URI为`"/testFolder/testResource"`。 使用与Microsoft .NET Framework兼容的语言（例如C#）时，将URI存储在`System.String`对象中。

1. 读取资源

   调用`RepositoryServiceService`对象的`readResource`方法，并传递资源的URI作为第一个参数。 传递`null`作为其他两个参数。

**另请参阅**

[阅读资源](aem-forms-repository.md#reading-resources)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 更新资源{#updating-resources}

您可以检索和更新存储库中的资源内容。 更新资源时，不同版本对这些资源的访问控制将保持不变。 执行更新时，您可以选择增加主版本。 如果您不选择增加主版本，则会自动更新次版本。

更新资源时，将根据指定的资源属性创建新版本。 在更新资源时，需指定两个重要参数：目标URI和包含所有更新元数据的资源实例。 请务必注意，如果不更改给定属性（例如，名称），则传入的实例中仍需要该属性。 解析内容时创建的关系将添加到特定版本，除非指定，否则不会提前。

例如，如果更新XDP文件并且该文件包含对其他资源的引用，则还将记录这些附加引用。 假设form.xdp版本1.0有两个外部引用：徽标和样式表，随后您将更新form.xdp，以便它现在包含三个引用：徽标、样式表和模式文件。 在更新过程中，存储库会将第三个关系(添加到模式文件)添加到其挂起的关系表中。 一旦模式文件存在在存储库中，该关系将自动形成。 但是，如果form.xdp版本2.0不再使用徽标，form.xdp版本2.0将不与徽标相关。

所有更新操作都是原子操作和事务操作。 例如，如果两个用户阅读了相同的资源，并且两个用户都决定将版本1.0更新到版本2.0，则其中一个将成功，其中一个将失败，则存储库的完整性将被保留，并且两者都将收到确认成功或失败的消息。 如果事务未提交，则在出现数据库故障时将回退，并根据应用程序服务器将超时或回退。

您可以使用存储库服务Java API或Web服务API以编程方式更新资源。

>[!NOTE]
>
>有关存储库服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-4}的摘要

要更新资源，请执行以下步骤：

1. 包括项目文件。
1. 创建存储库服务客户端。
1. 检索要更新的资源。
1. 更新资源。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请包含代理文件。

**创建服务客户端**

在以编程方式读取资源之前，必须建立连接并提供凭据。 这是通过创建服务客户端实现的。

**检索要更新的资源**

阅读资源。 有关详细信息，请参阅[读取资源](aem-forms-repository.md#reading-resources)。

**更新资源**

在资源中设置新信息并调用存储库服务方法以更新资源，指定URI、更新的资源以及版本信息的更新方式。

**另请参阅**

[使用Java API更新资源](aem-forms-repository.md#update-resources-using-the-java-api)

[使用Web服务API更新资源](aem-forms-repository.md#update-resources-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速开始](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API {#update-resources-using-the-java-api}更新资源

使用存储库服务API(Java)更新资源：

1. 包括项目文件

   将客户端JAR文件包含在Java项目的类路径中。

1. 创建服务客户端

   使用`ResourceRepositoryClient`对象的构造函数并传递包含连接属性的`ServiceClientFactory`对象，创建对象。

1. 检索要更新的资源

   指定要检索和读取资源的资源的URI。 在此示例中，资源的URI为`"/testFolder/testResource"`。

1. 更新资源

   更新`Resource`对象的信息。 在此示例中，要更新描述，请调用`Resource`对象的`setDescription`方法，并将新的描述字符串作为参数传递。

   然后调用`ServiceClientFactory`对象的`updateResource`方法，并传递以下参数：

   * 包含资源URI的`java.lang.String`对象。
   * `Resource`对象，包含更新的资源信息。
   * 一个`boolean`值，指示是更新主版本还是次版本。 在此示例中，传递值`true`以指示主版本将递增。

**另请参阅**

[更新资源](aem-forms-repository.md#updating-resources)

[快速开始（SOAP模式）：使用Java API更新资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#update-resources-using-the-web-service-api}更新资源

使用存储库API（Web服务）更新资源：

1. 包括项目文件

   * 创建一个使用存储库WSDL的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用其默认构造函数创建`RepositoryServiceService`对象。 使用包含用户名和密码的`System.Net.NetworkCredential`对象设置其`Credentials`属性。

1. 检索要更新的资源

   指定要检索的资源的URI并读取资源。 在此示例中，资源的URI为`"/testFolder/testResource"`。 有关详细信息，请参阅[读取资源](aem-forms-repository.md#reading-resources)。

1. 更新资源

   更新`Resource`对象的信息。 在此示例中，要更新说明，请为`Resource`对象的`description`字段指定新值。

1. 调用`RepositoryServiceService`对象的`updateResource`方法，并传递以下参数：

   * 包含资源URI的`System.String`对象。
   * `Resource`对象，包含更新的资源信息。
   * 一个`boolean`值，指示是更新主版本还是次版本。 在此示例中，传递值`true`以指示主版本将递增。
   * 传递`null`以获取其余两个参数。

**另请参阅**

[更新资源](aem-forms-repository.md#updating-resources)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 搜索资源{#searching-for-resources}

您可以构建用于在存储库中搜索资源的查询，包括历史记录、相关资源和属性。

您可以检索相关资源以确定表单与其片段之间的依赖关系。 例如，如果您有表单，则可以确定表单使用的片段或外部资源。 如果您有图像，您还可以了解哪些表单使用图像。 您还可以使用基于属性的筛选来搜索相关资源。 例如，您可以搜索所有使用具有指定名称的图像的表单，或查找由具有指定名称的表单使用的任何图像。 您还可以使用资源属性进行搜索。 例如，您可以执行查询来查找其名称开始与给定字符串（可能包括“%”和“_”通配符）的所有表单或资源。 请记住，基于属性的搜索并非基于关系；此类搜索基于您对给定资源具有特定知识的假设。

**查询语句**

*查询*&#x200B;包含一个或多个与条件逻辑连接的语句。 *语句*&#x200B;由左操作数、运算符和右操作数组成。 此外，您还可以指定用于搜索结果的排序顺序。 *排序顺序*&#x200B;包含与SQL `ORDER BY`子句等效的信息，并且由包含搜索所基于的属性的元素以及指示将使用升序还是降序的值组成。

您可以使用Repository服务Java API以编程方式搜索资源。 目前，无法使用Web服务API搜索资源。

**排序行为**

调用`ResourceRepositoryClient`对象的`searchProperties`方法并指定排序顺序时，不遵循排序顺序。 例如，假设您创建了一个具有三个自定义属性的资源，其中属性名为`name`、`secondName`和`asecondName`。 然后，在属性名称上创建一个排序顺序元素，并将`ascending`值设置为`true`。

然后调用`ResourceRepositoryClient`对象的`searchProperties`方法并按排序顺序传递。 搜索将返回具有三个属性的正确资源。 但是，属性不按属性名称排序。 它们按添加顺序返回：`name`、`secondName`和`asecondName`。

>[!NOTE]
>
>有关存储库服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-5}的摘要

要搜索资源，请执行以下步骤：

1. 包括项目文件。
1. 创建存储库服务客户端。
1. 指定搜索的目标文件夹。
1. 指定搜索中使用的属性。
1. 创建搜索中使用的查询。
1. 创建搜索结果的排序顺序。
1. 搜索资源。
1. 从搜索结果中检索资源。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请包含代理文件。

**创建服务客户端**

在以编程方式读取资源之前，必须建立连接并提供凭据。 这是通过创建服务客户端实现的。

**指定搜索的目标文件夹**

创建一个字符串，其中包含用于执行搜索的基本路径。 语法包括正斜杠，如本例所示：&quot;/*path*/*folder*&quot;。

**指定搜索中使用的属性**

您可以根据资源中包含的属性进行搜索。 指定用于执行搜索的属性值。

**创建搜索中使用的查询**

使用语句和条件构建查询。 每个语句都将指定搜索所基于的属性、要使用的条件以及要在搜索中使用的属性值。

**创建搜索结果的排序顺序**

排序顺序由元素组成，每个元素都包含搜索中使用的属性之一和指示是升序还是降序的值。

**搜索资源**

使用文件夹、查询和排序顺序搜索资源。 此外，指示搜索深度和要返回的结果数的上限。

**从搜索结果中检索资源**

对返回的资源列表进行迭代，并提取信息供进一步处理。

**另请参阅**

[使用Java API搜索资源](aem-forms-repository.md#search-for-resources-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速开始](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API {#search-for-resources-using-the-java-api}搜索资源

使用存储库服务API(Java)搜索资源：

1. 包括项目文件

   将客户端JAR文件包含在Java项目的类路径中。

1. 创建服务客户端

   使用`ResourceRepositoryClient`对象的构造函数并传递包含连接属性的`ServiceClientFactory`对象，创建对象。

1. 指定搜索的目标文件夹

   指定要从中执行搜索的基本路径的URI。 在此示例中，资源的URI为`/testFolder`。

1. 指定搜索中使用的属性

   指定用于执行搜索的属性的值。 `com.adobe.repository.infomodel.bean.Resource`对象中存在属性。 在本例中，将对name属性进行搜索；因此，使用包含`Resource`对象名称的`java.lang.String`，在本例中为`testResource`。

1. 创建搜索中使用的查询

   要创建查询，请通过调用`Query`类的默认构造函数创建`com.adobe.repository.query.Query`对象，并向查询添加语句。

   要创建语句，请调用`com.adobe.repository.query.Query.Statement`类的构造函数并传入以下参数：

   * 包含资源属性常数的左操作数。 在此示例中，由于资源的名称用作搜索的基础，因此使用静态值`Resource.ATTRIBUTE_NAME`。
   * 包含搜索属性时使用的条件的运算符。 运算符必须是`Query.Statement`类中的静态常量之一。 在此示例中，使用静态值`Query.Statement.OPERATOR_BEGINS_WITH`。
   * 包含用于执行搜索的属性值的右操作数。 在此示例中，使用名称属性`String`（包含值`"testResource"`）。

   通过调用`Query.Statement`对象的`setNamespace`方法并传入`com.adobe.repository.infomodel.bean.ResourceProperty`类中包含的一个静态值，指定左操作数的命名空间。 在此示例中，使用`ResourceProperty.RESERVED_NAMESPACE_REPOSITORY`。

   通过调用`Query`对象的`addStatement`方法并传入`Query.Statement`对象，将每个语句添加到查询。

1. 创建搜索结果的排序顺序

   要指定搜索结果中使用的排序顺序，请通过调用`SortOrder`类的默认构造函数创建`com.adobe.repository.query.sort.SortOrder`对象，并向排序顺序添加元素。

   要为排序顺序创建元素，请调用`com.adobe.repository.query.sort.SortOrder.Element`类的一个构造函数。 在此示例中，由于资源的名称用作搜索的基础，因此静态值`Resource.ATTRIBUTE_NAME`用作第一个参数，而升序顺序（`boolean`值`true`）指定为第二个参数。

   通过调用`SortOrder`对象的`addSortElement`方法并传入`SortOrder.Element`对象，将每个元素添加到排序顺序中。

1. 搜索资源

   要根据属性属性搜索`resources`，请调用`ResourceRepositoryClient`对象的`searchProperties`方法并传递以下参数：

   * `String`，包含要从中执行搜索的基本路径。 在这种情况下，使用`"/testFolder"`。
   * 搜索中使用的查询。
   * 搜索深度。 在这种情况下，`com.adobe.repository.infomodel.bean.ResourceCollection.DEPTH_INFINITE`用于指示将使用基本路径及其所有文件夹。
   * 一个`int`值，指示要从中选择未分页结果集的第一行。 在此示例中，指定了`0`。
   * 一个`int`值，指示要返回的最大结果数。 在此示例中，指定了`10`。
   * 搜索中使用的排序顺序。

   该方法按指定的排序顺序返回`Resource`对象的`java.util.List`。

1. 从搜索结果中检索资源

   要检索搜索结果中包含的资源，请遍历`List`并将每个对象转换为`Resource`以提取其信息。 在此示例中，将显示每个资源的名称。

**另请参阅**

[搜索资源](aem-forms-repository.md#searching-for-resources)

[快速开始（SOAP模式）：使用Java API搜索资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 创建资源关系{#creating-resource-relationships}

您可以在存储库中指定资源之间的关系。 有三种关系：

* **依赖**:资源依赖于其他资源的关系，这意味着存储库中需要所有相关资源。
* **会员资格（文件系统）**:资源位于给定文件夹中的关系。
* **自定义**:您在资源之间指定的关系。例如，如果一个资源已弃用，而另一个资源已引入存储库，则可以指定您自己的替换关系。

您可以创建自己的自定义关系。 例如，如果将HTML文件存储在存储库中，并且它使用图像，则可以指定一个自定义关系以将HTML文件与图像关联（因为通常只有XML文件使用存储库定义的依赖关系与图像关联）。 自定义关系的另一个示例是，如果您希望使用循环图结构而不是树结构构建存储库的不同视图。 您可以定义一个圆形图和一个查看器来遍历这些关系。 最后，您可以指示资源替换另一个资源，即使这两个资源完全不同。 在这种情况下，您可以定义保留范围之外的关系类型，并在这两个资源之间建立关系。 您的应用程序将是唯一能够检测并处理该关系的客户端，并且它可用于对该关系进行搜索。

您可以使用Repository服务Java API或Web服务API以编程方式指定资源之间的关系。

>[!NOTE]
>
>有关存储库服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-6}的摘要

要指定两个资源之间的关系，请执行以下步骤：

1. 包括项目文件。
1. 创建存储库服务客户端。
1. 指定要相关的资源的URI。
1. 创建关系。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请包含代理文件。

**创建服务客户端**

在以编程方式读取资源之前，必须建立连接并提供凭据。 这是通过创建服务客户端实现的。

**指定要相关的资源的URI**

创建包含要相关的资源的URI的字符串。 语法包括正斜杠，如本例所示：&quot;/*path*/*resource*&quot;。

**创建关系**

调用存储库服务方法以创建和指定关系类型。

**另请参阅**

[使用Java API创建关系资源](aem-forms-repository.md#create-relationship-resources-using-the-java-api)

[使用Web服务API创建关系资源](aem-forms-repository.md#create-relationship-resources-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速开始](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API {#create-relationship-resources-using-the-java-api}创建关系资源

通过使用Repository服务Java API创建关系资源，执行以下任务:

1. 包括项目文件

   将客户端JAR文件包含在Java项目的类路径中。

1. 创建服务客户端

   使用`ResourceRepositoryClient`对象的构造函数并传递包含连接属性的`ServiceClientFactory`对象，创建对象。

1. 指定要相关的资源的URI

   指定要相关的资源的URI。 在这种情况下，由于资源名为`testResource1`和`testResource2`，并位于名为`testFolder`的文件夹中，因此其URI为`"/testFolder/testResource1"`和`"/testFolder/testResource2"`。 URI作为`java.lang.String`对象存储。 在此示例中，资源首先写入存储库，并检索其URI。 有关编写资源的详细信息，请参阅[编写资源](aem-forms-repository.md#writing-resources)。

1. 创建关系

   调用`ResourceRepositoryClient`对象的`createRelationship`方法并传递以下参数：

   * 源资源的URI。
   * 目标资源的URI。
   * 关系的类型，它是`com.adobe.repository.infomodel.bean.Relation`类中的静态常量之一。 在此示例中，通过指定值`Relation.TYPE_DEPENDANT_OF`建立依赖关系。
   * 一个`boolean`值，指示目标资源是否自动更新为新头资源的基于`com.adobe.repository.infomodel.Id`的标识符。 在此示例中，由于依赖关系，指定了值`true`。

   您还可以通过调用`ResourceRepositoryClient`对象的`getRelated`方法并传入以下参数，检索给定资源的相关资源列表:

   * 要为其检索相关资源的资源的URI。 在此示例中，指定了源资源(`"/testFolder/testResource1"`)。
   * 一个`boolean`值，指示指定的资源是否是关系中的源资源。 在此示例中，指定值`true`，因为这是这种情况。
   * 关系类型，它是`Relation`类中的静态常量之一。 在此示例中，依赖关系是通过使用之前使用的相同值来指定的：`Relation.TYPE_DEPENDANT_OF`。

   `getRelated`方法返回`Resource`对象的`java.util.List`，通过该对象可以进行迭代以检索每个相关资源，并将`List`中包含的对象转换为`Resource`。 在此示例中，`testResource2`应为返回资源的列表。

**另请参阅**

[创建资源关系](aem-forms-repository.md#creating-resource-relationships)

[快速开始（SOAP模式）：使用Java API创建资源之间的关系](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#create-relationship-resources-using-the-web-service-api}创建关系资源

使用存储库API（Web服务）创建关系资源：

1. 包括项目文件

   * 创建一个使用存储库WSDL的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用其默认构造函数创建`RepositoryServiceService`对象。 使用包含用户名和密码的`System.Net.NetworkCredential`对象设置其`Credentials`属性。

1. 指定要相关的资源的URI

   指定要相关的资源的URI。 在这种情况下，由于资源名为`testResource1`和`testResource2`，并位于名为`testFolder`的文件夹中，因此其URI为`"/testFolder/testResource1"`和`"/testFolder/testResource2"`。 当使用与Microsoft .NET Framework兼容的语言（例如C#）时，URI将存储为`System.String`对象。 在此示例中，资源首先写入存储库，并检索其URI。 有关编写资源的详细信息，请参阅[编写资源](aem-forms-repository.md#writing-resources)。

1. 创建关系

   调用`RepositoryServiceService`对象的`createRelationship`方法并传递以下参数：

   * 源资源的URI。
   * 目标资源的URI。
   * 关系的类型。 在此示例中，通过指定值`3`建立依赖关系。
   * 一个`boolean`值，指示是否指定了关系类型。 在此示例中，指定了值`true`。
   * 一个`boolean`值，指示目标资源是否自动更新为新头资源的基于`Id`的标识符。 在此示例中，由于依赖关系，指定了值`true`。
   * 一个`boolean`值，指示是否指定了目标头。 在此示例中，指定了值`true`。
   * 传递`null`作为最后一个参数。

   您还可以通过调用`RepositoryServiceService`对象的`getRelated`方法并传入以下参数，检索给定资源的相关资源列表:

   * 要为其检索相关资源的资源的URI。 在此示例中，指定了源资源(`"/testFolder/testResource1"`)。
   * 一个`boolean`值，指示指定的资源是否是关系中的源资源。 在此示例中，指定值`true`，因为这是这种情况。
   * 一个`boolean`值，指示是否指定了源资源。 在此示例中，提供了值`true`。
   * 包含关系类型的整数数组。 在此示例中，依赖关系是通过在数组中使用与之前使用相同的值来指定的：`3`。
   * 传递`null`以获取其余两个参数。

   `getRelated`方法返回可转换为`Resource`对象的对象数组，您可以通过它进行迭代以检索每个相关资源。 在此示例中，`testResource2`应为返回资源的列表。

**另请参阅**

[创建资源关系](aem-forms-repository.md#creating-resource-relationships)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 锁定资源{#locking-resources}

您可以锁定某个资源或一组资源，供特定用户独占使用或在多个用户之间共享使用。 共享锁表示资源会发生某些情况，但不会阻止任何其他人对该资源执行操作。 应将共享锁视为信令机制。 独占锁表示锁定资源的用户将更改资源，而锁则确保在用户不再需要访问资源并释放锁之前，其他任何人都不能更改。 如果存储库管理员解锁了某个资源，则该资源上的所有独占和共享锁将自动删除。 此类操作适用于用户不再可用且未解锁资源的情况。

当资源被锁定时，当您视图位于Workbench中的“资源”选项卡时，会显示一个锁图标，如下图所示。

![lr_lr_lockrepository](assets/lr_lr_lockrepository.png)

您可以使用存储库服务Java API或Web服务API以编程方式控制对资源的访问。

>[!NOTE]
>
>有关存储库服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-7}的摘要

要锁定和解锁资源，请执行以下步骤：

1. 包括项目文件。
1. 创建存储库服务客户端。
1. 指定要锁定的资源的URI。
1. 锁定资源。
1. 检索资源的锁。
1. 解锁资源

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请包含代理文件。

**创建服务客户端**

在以编程方式读取资源之前，必须建立连接并提供凭据。 这是通过创建服务客户端实现的。

**指定要锁定的资源的URI**

创建一个字符串，其中包含要锁定的资源的URI。 语法包括正斜杠，如本例所示：&quot;/*path*/*resource*&quot;。

**锁定资源**

调用存储库服务方法以锁定资源，并指定URI、锁定类型和锁定深度。

**检索资源的锁**

调用存储库服务方法以检索资源的锁，同时指定URI。

**解锁资源**

调用存储库服务方法以解锁资源，并指定URI。

**另请参阅**

[使用Java API锁定资源](aem-forms-repository.md#lock-resources-using-the-java-api)

[使用Web服务API锁定资源](aem-forms-repository.md#lock-resources-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速开始](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API {#lock-resources-using-the-java-api}锁定资源

使用存储库服务API(Java)锁定资源：

1. 包括项目文件

   将客户端JAR文件包含在Java项目的类路径中。

1. 创建服务客户端

   使用`ResourceRepositoryClient`对象的构造函数并传递包含连接属性的`ServiceClientFactory`对象，创建对象。

1. 指定要锁定的资源的URI

   指定要锁定的资源的URI。 在这种情况下，由于名为`testResource`的资源位于名为`testFolder`的文件夹中，其URI为`"/testFolder/testResource"`。 URI将作为`java.lang.String`对象存储。

1. 锁定资源

   调用`ResourceRepositoryClient`对象的`lockResource`方法并传递以下参数：

   * 资源的URI。
   * 锁定范围。 在此示例中，由于资源将被锁定以供独占使用，因此锁定范围被指定为`com.adobe.repository.infomodel.bean.Lock.SCOPE_EXCLUSIVE`。
   * 锁的深度。 在此示例中，由于锁定将仅应用于特定资源，且不应用其成员或子资源，因此锁定深度指定为`Lock.DEPTH_ZERO`。

   >[!NOTE]
   >
   >需要四个参数的`lockResource`方法的重载版本将引发异常。 确保使用`lockResource`方法，该方法需要三个参数，如本演练中所示。

1. 检索资源的锁

   调用`ResourceRepositoryClient`对象的`getLocks`方法，并将资源的URI作为参数传递。 该方法返回一列表Lock对象，您可以通过它进行迭代。 在此示例中，通过分别调用每个Lock对象的`getOwnerUserId`、`getDepth`和`getType`方法，为每个对象打印锁所有者、深度和范围。

1. 解锁资源

   调用`ResourceRepositoryClient`对象的`unlockResource`方法，并将资源的URI作为参数传递。 有关详细信息，请参阅[AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**另请参阅**

[锁定资源](aem-forms-repository.md#locking-resources)

[快速开始（SOAP模式）：使用Java API锁定资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#lock-resources-using-the-web-service-api}锁定资源

使用存储库服务API（Web服务）锁定资源：

1. 包括项目文件

   * 创建一个使用Base64使用存储库WSDL的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用其默认构造函数创建`RepositoryServiceService`对象。 使用包含用户名和密码的`System.Net.NetworkCredential`对象设置其`Credentials`属性。

1. 指定要锁定的资源的URI

   指定包含要锁定的资源的URI的字符串。 在这种情况下，由于名为`testResource`的资源位于文件夹`testFolder`中，其URI为`"/testFolder/testResource"`。 使用与Microsoft .NET Framework兼容的语言（例如C#）时，将URI存储在`System.String`对象中。

1. 锁定资源

   调用`RepositoryServiceService`对象的`lockResource`方法并传递以下参数：

   * 资源的URI。
   * 锁定范围。 在此示例中，由于资源将被锁定以供独占使用，因此锁定范围被指定为`11`。
   * 锁的深度。 在此示例中，由于锁定将仅应用于特定资源，且不应用其成员或子资源，因此锁定深度指定为`2`。
   * 一个`int`值，指示锁定过期前的秒数。 在此示例中，使用`1000`的值。
   * 传递`null`作为最后一个参数。

1. 检索资源的锁

   调用`RepositoryServiceService`对象的`getLocks`方法，将资源的URI作为第一个参数传递，将`null`作为第二个参数传递。 该方法返回一个`object`数组，其中包含可通过它进行迭代的`Lock`对象。 在此示例中，通过分别访问每个`Lock`对象的`ownerUserId`、`depth`和`type`字段，为每个对象打印锁所有者、深度和范围。

1. 解锁资源

   调用`RepositoryServiceService`对象的`unlockResource`方法，将资源的URI作为第一个参数传递，将`null`作为第二个参数传递。

**另请参阅**

[锁定资源](aem-forms-repository.md#locking-resources)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 删除资源{#deleting-resources}

您可以使用存储库服务Java API(SOAP)从存储库中的给定位置以编程方式删除资源。

删除资源时，删除操作通常是永久的，但在某些情况下， ECM存储库可能会根据其历史记录机制存储资源的版本。 因此，删除资源时，务必确保您不再需要该资源。 删除资源的常见原因包括需要增加数据库中的可用空间。 您可以删除某个资源版本，但如果删除，则必须指定资源标识符，而不是其逻辑标识符(LID)或路径。 如果删除文件夹，该文件夹中的所有内容（包括子文件夹和资源）都将自动删除。

不删除相关资源。 例如，如果您有一个使用logo.gif文件的表单，并且您删除logo.gif，则关系将存储在挂起的关系表中。 作为替代方法，对于版本弃用，请将最新版本的对象状态设置为已弃用。

在ECM系统中，删除操作不是事务安全操作。 例如，如果尝试删除100个资源，而第50个资源上的操作失败，则前49个实例将被删除，其余实例将不会删除。 否则，默认行为为回滚（非承诺）。

>[!NOTE]
>
>将`com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient.deleteResources()`方法与ECM存储库（EMC Documentum Content Server和IBM FileNet P8 Content Manager）一起使用时，如果某个指定资源的删除失败，则事务将不会回滚，这意味着无法删除已删除的文件。

>[!NOTE]
>
>有关存储库服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-8}的摘要

要删除资源，请执行以下步骤：

1. 包括项目文件。
1. 创建存储库服务客户端。
1. 指定要删除的资源的URI。
1. 删除资源。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请包含代理文件。

**创建服务客户端**

在以编程方式读取资源之前，必须建立连接并提供凭据。 这是通过创建服务客户端实现的。

**指定要删除的资源的URI**

创建一个字符串，其中包含要删除的资源的URI。 语法包括正斜杠，如本例所示：&quot;/*path*/*resource*&quot;。 如果要删除的资源是文件夹，则删除将是递归的。

**删除资源**

调用存储库服务方法以删除资源，并指定URI。

**另请参阅**

[使用Java API删除资源](aem-forms-repository.md#delete-resources-using-the-java-api-soap)

[使用Web服务API删除资源](aem-forms-repository.md#delete-resources-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[存储库服务API快速开始](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API(SOAP){#delete-resources-using-the-java-api-soap}删除资源

使用存储库API(Java)删除资源：

1. 包括项目文件

   将客户端JAR文件包含在Java项目的类路径中。

1. 创建服务客户端

   使用`ResourceRepositoryClient`对象的构造函数并传递包含连接属性的`ServiceClientFactory`对象，创建对象。

1. 指定要删除的资源的URI

   指定要检索的资源的URI。 在这种情况下，由于名为testResourceToBeDeleted的资源位于名为testFolder的文件夹中，其URI为`/testFolder/testResourceToBeDeleted`。 URI将作为`java.lang.String`对象存储。 在此示例中，资源首先写入存储库，并检索其URI。 有关编写资源的详细信息，请参阅[编写资源](aem-forms-repository.md#writing-resources)。

1. 删除资源

   调用`ResourceRepositoryClient`对象的`deleteResource`方法，并将资源的URI作为参数传递。

**另请参阅**

[删除资源](aem-forms-repository.md#deleting-resources)

[快速开始（SOAP模式）：使用Java API搜索资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#delete-resources-using-the-web-service-api}删除资源

使用存储库API（Web服务）删除资源：

1. 包括项目文件

   * 创建一个使用Base64使用存储库WSDL的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建服务客户端

   使用Microsoft .NET客户端程序集，通过调用其默认构造函数创建`RepositoryServiceService`对象。 使用包含用户名和密码的`System.Net.NetworkCredential`对象设置其`Credentials`属性。

1. 指定要删除的资源的URI

   指定要检索的资源的URI。 在这种情况下，由于名为`testResourceToBeDeleted`的资源位于名为`testFolder`的文件夹中，其URI为`"/testFolder/testResourceToBeDeleted"`。 在此示例中，资源首先写入存储库，并检索其URI。 有关编写资源的详细信息，请参阅[编写资源](aem-forms-repository.md#writing-resources)。

1. 删除资源

   调用`RepositoryServiceService`对象的`deleteResources`方法，并传递一个`System.String`数组，该数组包含资源的URI作为第一个参数。 传递`null`作为第二个参数。

**另请参阅**

[删除资源](aem-forms-repository.md#deleting-resources)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
