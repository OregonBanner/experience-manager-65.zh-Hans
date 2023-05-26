---
title: 以编程方式管理端点
seo-title: Programmatically Managing Endpoints
description: 使用“端点注册”服务可以添加EJB端点、添加SOAP端点、添加Watched Folder端点、添加电子邮件端点、添加远程处理端点、添加任务管理器端点、修改端点、删除端点以及检索端点连接器信息。
seo-description: Use the Endpoint Registry service to add EJB endpoints, add SOAP endpoint, add Watched Folder endpoints, add Email endpoints, add  Remoting endpoints, add Task Manager endpoints, modify endpoints, remove endpoints, and retrieve endpoint connector information.
uuid: 5dc50946-3323-4c5d-a43b-31c1c980bd04
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 076889a7-9c9f-4b6f-a45b-67a9b3923c36
role: Developer
exl-id: b94dcca2-136b-4b7d-b5ce-544804575876
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '10805'
ht-degree: 1%

---

# 以编程方式管理端点 {#programmatically-managing-endpoints}

**本文档中的示例和示例仅适用于AEM Forms on JEE环境。**

**关于终结点注册表服务**

Endpoint Registry服务提供了以编程方式管理端点的功能。 例如，您可以将以下类型的端点添加到服务：

* EJB
* SOAP
* 观察文件夹
* 电子邮件
* (对于AEM表单已弃用)远程处理
* 任务管理器

>[!NOTE]
>
>SOAP、EJB和(对于JEE上的AEM Forms已弃用)远程处理端点是为每个激活的服务自动创建的。 SOAP和EJB端点为所有服务操作启用SOAP和EJB。

远程端点使Flex客户端能够调用对端点所添加到的AEM Forms服务的操作。 将创建与端点同名的Flex目标，并且Flex客户端可以创建指向此目标的RemoteObjects以调用对相关服务的操作。

电子邮件、任务管理器和Watched Folder端点仅公开服务的特定操作。 添加这些端点需要执行第二个配置步骤，以选择要调用的方法、设置配置参数以及指定输入和输出参数映射。

您可以将TaskManager端点组织成组，称为 *类别*. 然后，这些类别将通过TaskManager向Workspace公开，最终用户在分类时看到TaskManager端点。 在Workspace中，最终用户可在导航窗格中看到这些类别。 每个类别中的端点在Workspace的“启动进程”页面上显示为进程卡。

您可以使用Endpoint Registry服务完成以下任务：

* 添加EJB端点。 (请参阅 [添加EJB端点](programmatically-endpoints.md#adding-ejb-endpoints).)
* 添加SOAP端点。 (请参阅 [添加SOAP端点](programmatically-endpoints.md#adding-soap-endpoints).)
* 添加Watched文件夹端点(请参阅 [添加观察文件夹端点](programmatically-endpoints.md#adding-watched-folder-endpoints).)
* 添加电子邮件端点。 (请参阅 [添加电子邮件端点](programmatically-endpoints.md#adding-email-endpoints).)
* 添加远程处理端点。 (请参阅 [添加远程端点](programmatically-endpoints.md#adding-remoting-endpoints).)
* 添加任务管理器端点(请参阅 [添加TaskManager端点](programmatically-endpoints.md#adding-taskmanager-endpoints).)
* 修改端点(请参阅 [修改端点](programmatically-endpoints.md#modifying-endpoints).)
* 删除端点(请参阅 [删除端点](programmatically-endpoints.md#removing-endpoints).)
* 检索终结点连接器信息(请参阅 [正在检索终结点连接器信息](programmatically-endpoints.md#retrieving-endpoint-connector-information).)

## 添加EJB端点 {#adding-ejb-endpoints}

您可以使用AEM Forms Java API以编程方式将EJB端点添加到服务。 通过将EJB端点添加到服务，可以使客户机应用程序使用EJB模式调用该服务。 也就是说，在设置调用AEM Forms所需的连接属性时，可以选择EJB模式。 (请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>无法使用Web服务添加EJB端点。

>[!NOTE]
>
>通常，默认情况下会将EJB端点添加到服务中。但是，可以将EJB端点添加到以编程方式部署的进程中，或者在删除了EJB端点且必须再次添加时，可以将EJB端点添加到进程中。

### 步骤摘要 {#summary-of-steps}

要向服务添加EJB端点，请执行以下任务：

1. 包括项目文件。
1. 创建 `EndpointRegistry Client` 对象。
1. 设置EJB终结点属性。
1. 创建EJB端点。
1. 启用端点。

**包括项目文件**

在开发项目中包含必要的文件。 必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)
* jbossall-client.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)

有关这些JAR文件位置的信息，请参见 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建EndpointRegistry客户端对象**

必须先创建一个 `EndpointRegistryClient` 对象。

**设置EJB终结点属性**

要为服务创建EJB端点，请指定以下值：

* **连接器标识符**：指定要创建的终结点的类型。 要创建EJB端点，请指定 `EJB`.
* **描述**：指定终结点描述。
* **名称**：指定端点的名称。
* **服务标识符**：指定终结点所属的服务。
* **操作名称**：指定使用端点调用的操作的名称。 创建EJB端点时，请指定通配符( `*`)。 但是，如果要指定特定操作而不是调用所有服务操作，请指定操作名称，而不是使用通配符( `*`)。

**创建EJB端点**

设置EJB终结点属性后，可以为服务创建EJB终结点。

**启用端点**

创建新端点后，必须启用它。 启用端点后，便可用于调用服务。 启用该端点后，您可以在管理控制台中查看它。

**另请参阅**

[使用Java API添加EJB端点](programmatically-endpoints.md#adding-an-ejb-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API添加EJB端点 {#adding-an-ejb-endpoint-using-the-java-api}

使用Java API添加EJB端点：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，例如adobe-livecycle-client.jar。 （

1. 创建EndpointRegistry客户端对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `EndpointRegistryClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 设置EJB终结点属性。

   * 创建 `CreateEndpointInfo` 对象。
   * 通过调用 `CreateEndpointInfo` 对象的 `setConnectorId` 方法和传递字符串值 `EJB`.
   * 通过调用 `CreateEndpointInfo` 对象的 `setDescription` 方法和传递描述端点的字符串值。
   * 通过调用 `CreateEndpointInfo` 对象的 `setName` 方法，并传递一个指定名称的字符串值。
   * 通过调用 `CreateEndpointInfo` 对象的 `setServiceId` 方法，并传递一个指定服务名称的字符串值。
   * 指定通过调用 `CreateEndpointInfo` 对象的 `setOperationName` 方法，并传递一个指定操作名称的字符串值。 对于SOAP和EJB端点，请指定通配符( `*`)，这表示所有操作。

1. 创建EJB端点。

   通过调用 `EndpointRegistryClient` 对象的 `createEndpoint` 方法和传递 `CreateEndpointInfo` 对象。 此方法会返回 `Endpoint` 表示新EJB端点的对象。

1. 启用端点。

   通过调用 `EndpointRegistryClient` 对象的enable方法和传递 `Endpoint` 返回的对象 `createEndpoint` 方法。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速入门：使用Java API添加EJB端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-ejb-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 添加SOAP端点 {#adding-soap-endpoints}

您可以使用AEM Forms Java API以编程方式将SOAP端点添加到服务。 通过添加SOAP端点，可以使客户端应用程序使用SOAP模式调用该服务。 也就是说，在设置调用AEM Forms所需的连接属性时，可以选择SOAP模式。

>[!NOTE]
>
>无法使用Web服务添加SOAP端点。

>[!NOTE]
>
>通常，默认情况下会向服务添加SOAP端点。但是，可以将SOAP端点添加到以编程方式部署的进程，或者在删除了SOAP端点且必须再次添加时。

### 步骤摘要 {#summary_of_steps-1}

要向服务添加SOAP端点，请执行以下任务：

1. 包括项目文件。
1. 创建 `EndpointRegistryClient` 对象。
1. 设置SOAP端点属性。
1. 创建SOAP端点。
1. 启用端点。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)
* jbossall-client.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)

创建SOAP端点需要这些JAR文件。 但是，如果使用SOAP端点调用服务，则需要添加JAR文件。 有关AEM Forms JAR文件的信息，请参见 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建EndpointRegistry客户端对象**

要以编程方式将SOAP端点添加到服务，您必须创建 `EndpointRegistryClient` 对象。

**设置SOAP端点属性**

要向服务添加SOAP端点，请指定以下值：

* **连接器标识符值**：指定要创建的终结点的类型。 要创建SOAP端点，请指定 `SOAP`.
* **描述**：指定终结点描述。
* **名称**：指定终结点名称。
* **服务标识符值**：指定终结点所属的服务。
* **操作名称**：指定使用端点调用的操作的名称。 创建SOAP端点时，指定通配符( `*`)。 但是，如果要指定特定操作而不是调用所有服务操作，请指定操作名称，而不是使用通配符( `*`)。

**创建SOAP端点**

设置SOAP端点属性后，可以创建SOAP端点。

**启用端点**

创建新端点后，必须启用它。 启用端点后，可用于调用服务。 启用该端点后，您可以在管理控制台中查看它。

**另请参阅**

[使用Java API添加SOAP端点](programmatically-endpoints.md#add-a-soap-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API添加SOAP端点 {#add-a-soap-endpoint-using-the-java-api}

使用Java API向服务添加SOAP端点：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，例如adobe-livecycle-client.jar。

1. 创建EndpointRegistry客户端对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `EndpointRegistryClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 设置SOAP端点属性。

   * 创建 `CreateEndpointInfo` 对象。
   * 通过调用 `CreateEndpointInfo` 对象的 `setConnectorId` 方法和传递字符串值 `SOAP`.
   * 通过调用 `CreateEndpointInfo` 对象的 `setDescription` 方法和传递描述端点的字符串值。
   * 通过调用 `CreateEndpointInfo` 对象的 `setName` 方法，并传递一个指定名称的字符串值。
   * 通过调用 `CreateEndpointInfo` 对象的 `setServiceId` 方法，并传递一个指定服务名称的字符串值。
   * 指定通过调用 `CreateEndpointInfo` 对象的 `setOperationName` 方法，并传递一个指定操作名称的字符串值。 对于SOAP和EJB端点，请指定通配符( `*`)，这表示所有操作。

1. 创建SOAP端点。

   通过调用 `EndpointRegistryClient` 对象的 `createEndpoint` 方法和传递 `CreateEndpointInfo` 对象。 此方法会返回 `Endpoint` 表示新SOAP端点的对象。

1. 启用端点。

   通过调用 `EndpointRegistryClient` 对象的enable方法并传递 `Endpoint` 返回的对象 `createEndpoint` 方法。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速入门：使用Java API添加SOAP端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-soap-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 添加观察文件夹端点 {#adding-watched-folder-endpoints}

您可以使用AEM Forms Java API以编程方式将Watched Folder端点添加到服务。 通过添加Watched Folder端点，您可以使用户能够将文件(如PDF文件)放置在文件夹中。 将文件放在文件夹中后，将调用配置的服务并操作文件。 服务执行指定的操作后，会将修改的文件保存在指定的输出文件夹中。 观察文件夹配置为按固定速率间隔或按cron时间表进行扫描，例如每个星期一、星期三和星期五中午。

为了以编程方式将Watched Folder端点添加到服务，请考虑以下命名的短暂过程 *EncryDocument*. (请参阅 [了解AEM Forms流程](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes).)

![aw_aw_encryptdocumentprocess](assets/aw_aw_encryptdocumentprocess.png)

此流程接受不安全的PDF文档作为输入值，然后将不安全的PDF文档传递到加密服务的 `EncryptPDFUsingPassword` 操作。 PDF文档使用密码进行加密，密码加密的PDF文档是此过程的输出值。 输入值(无保护PDF文档)的名称为 `InDoc` 并且数据类型是 `com.adobe.idp.Document`. 输出值(口令加密的PDF文档)的名称为 `SecuredDoc` 并且数据类型是 `com.adobe.idp.Document`.

>[!NOTE]
>
>无法使用Web服务添加Watched Folder端点。

### 步骤摘要 {#summary_of_steps-2}

要向服务添加Watched Folder端点，请执行以下任务：

1. 包括项目文件。
1. 创建 `EndpointRegistryClient` 对象。
1. 设置Watched Folder端点属性。
1. 指定配置值。
1. 定义输入参数值。
1. 定义输出参数值。
1. 创建Watched文件夹端点。
1. 启用端点。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)
* jbossall-client.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)

有关这些JAR文件位置的信息，请参见 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建EndpointRegistry客户端对象**

要以编程方式添加观察文件夹端点，您必须创建 `EndpointRegistryClient` 对象。

**设置Watched文件夹端点属性**

要为服务创建Watched Folder端点，请指定以下值：

* **连接器标识符**：指定创建的端点的类型。 要创建Watched文件夹端点，请指定 `WatchedFolder`.
* **描述**：指定端点的描述。
* **名称**：指定端点的名称。
* **服务标识符**：指定终结点所属的服务。 例如，要将Watched文件夹端点添加到此部分中介绍的进程（使用Workbench激活进程时，该进程将成为服务），请指定 `EncryptDocument`.
* **操作名称**：指定使用端点调用的操作的名称。 通常，在为源自于Workbench中创建的进程的服务创建Watched文件夹端点时，操作的名称为 `invoke`.

**指定配置值**

以编程方式将Watched文件夹端点添加到服务时，必须指定Watched文件夹端点的配置值。 如果使用管理控制台添加了Watched文件夹端点，则这些配置值由管理员指定。

以下列表指定以编程方式将Watched文件夹端点添加到服务时设置的配置值：

* **url**：指定Watched文件夹位置。 在群集环境中，此值必须指向可从群集中的每台计算机访问的共享网络文件夹。
* **异步**：将调用类型标识为异步或同步。 只能同步调用瞬态和同步进程。 默认值为true。 建议使用异步。
* **cronExpression**：由Quartz用来安排对输入目录的轮询。
* **purgeDuration**：这是一个必需属性。 当结果文件夹中的文件和文件夹早于此值时，将清除这些文件和文件夹。 此值以天为单位。 此属性对于确保结果文件夹不会填满非常有用。 值为–1天表示从不删除结果文件夹。 缺省值为–1。
* **repeateinterval**：扫描Watched文件夹以进行输入的间隔，以秒为单位。 除非启用了限制，否则该值应比处理平均作业的时间长；否则，系统可能会过载。 默认值为 5。
* **repeatcount**：观察文件夹扫描文件夹或目录的次数。 值–1表示无限扫描。 缺省值为–1。
* **throttleOn**：限制可在任何给定时间处理的Watched Folder作业数。 最大作业数由batchSize值决定。
* **用户名**：从Watched文件夹调用目标服务时使用的用户名。 此值是必需的。 默认值为SuperAdmin。
* **域名**：用户的域。 此值是必需的。 默认值为DefaultDom。
* **batchSize**：每次扫描要提取的文件或文件夹数。 使用此值可防止系统过载；一次扫描太多文件可能会导致崩溃。 默认值为 2。
* **waitetime**：创建文件夹或文件后等待扫描的时间，以毫秒为单位。 例如，如果等待时间为36,000,000毫秒（1小时），文件是在一分钟前创建的，则将在59分钟或更长时间后提取此文件。 此属性对于确保文件或文件夹完全复制到输入文件夹非常有用。 例如，如果处理一个大文件，而下载该文件需要10分钟，则将等待时间设置为10&amp;ast；60 &amp;ast；1000毫秒。 此设置可防止观察文件夹在等待10分钟后扫描文件。 默认值为 0。
* **excludeFilePattern**：观察文件夹用于确定要扫描和选取的文件和文件夹的模式。 不会扫描任何具有此模式的文件或文件夹以进行处理。 当输入是包含多个文件的文件夹时，此设置很有用。 可以将文件夹的内容复制到一个名称为的文件夹中，该名称将由watched文件夹提取。 此步骤可防止watched文件夹在文件夹完全复制到输入文件夹之前拾取要处理的文件夹。 例如，如果excludeFilePattern值为 `data*`，所有匹配的文件和文件夹 `data*` 不会被接听。 这包括名为的文件和文件夹 `data1`， `data2`，等等。 此外，还可以使用通配符模式对模式进行补充，以指定文件模式。 观察文件夹修改正则表达式以支持通配符模式，例如 `*.*` 和 `*.pdf`. 正则表达式不支持这些通配符模式。
* **includeFilePattern**：观察文件夹用于确定要扫描和选取的文件夹和文件的模式。 例如，如果此值为 `*`，所有匹配的文件和文件夹 `input*` 被捡起来了。 这包括名为的文件和文件夹 `input1`， `input2`，等等。 默认值为 `*`。此值表示所有文件和文件夹。 此外，还可以使用通配符模式对模式进行补充，以指定文件模式。 观察文件夹修改正则表达式以支持通配符模式，例如 `*.*` 和 `*.pdf`. 正则表达式不支持这些通配符模式。 此值是必需的。
* **resultFolderName**：存储所保存结果的文件夹。 此位置可以是绝对或相对目录路径。 如果结果未出现在此文件夹中，请检查故障文件夹。 不处理只读文件，这些文件将保存在故障文件夹中。 默认值为 `result/%Y/%M/%D/`。这是watched文件夹中的结果文件夹。
* **preserveFolderName**：成功扫描和提取后存储文件的位置。 此位置可以是绝对、相对或空目录路径。 默认值为 `preserve/%Y/%M/%D/`。
* **failureFolderName**：保存失败文件的文件夹。 此位置始终相对于观察文件夹。 不处理只读文件，这些文件将保存在故障文件夹中。 默认值为 `failure/%Y/%M/%D/`。
* **preserveOnFailure**：如果无法对服务执行操作，则保留输入文件。 默认值为true。
* **overwriteDuplicateFilename**：设置为true时，将覆盖结果文件夹和保留文件夹中的文件。 当设置为false时，使用具有数字索引后缀的文件和文件夹作为名称。 默认值为false。

**定义输入参数值**

创建Watched文件夹端点时，必须定义输入参数值。 也就是说，必须描述传递给watched文件夹调用的操作的输入值。 例如，请考虑本主题中引入的过程。 它具有一个名为的输入值 `InDoc` 并且它的数据类型为 `com.adobe.idp.Document`. 为此进程创建Watched文件夹端点时（激活进程后，该进程将成为服务），必须定义输入参数值。

要定义Watched Folder端点所需的输入参数值，请指定以下值：

**输入参数名称**：输入参数的名称。 在Workbench中为进程指定输入值的名称。 如果输入值属于服务操作（不是在Workbench中创建的进程的服务），则在component.xml文件中指定输入名称。 例如，本节介绍的进程的输入参数的名称为 `InDoc`.

**映射类型**：用于配置调用服务操作所需的输入值。 有两种类型的映射类型：

* `Literal`：观察文件夹端点使用在显示的字段中输入的值。 支持所有基本Java类型。 例如，如果API使用字符串、long、int和Boolean等输入，则字符串将转换为正确类型并调用服务。
* `Variable`：输入的值是watched文件夹用来选取输入的文件模式。 例如，如果为映射类型选择“变量”，并且输入文档必须是PDF文件，则可以指定 `*.pdf`作为映射值。

**映射值**：指定映射类型的值。 例如，如果您选择 `Variable` 映射类型，您可以指定 `*.pdf` 作为文件模式。

**数据类型**：指定输入值的数据类型。 例如，本节介绍的进程的输入值的数据类型为 `com.adobe.idp.Document`.

**定义输出参数值**

创建Watched文件夹端点时，必须定义一个输出参数值。 也就是说，必须描述由Watched Folder端点调用的服务返回的输出值。 例如，请考虑本主题中引入的过程。 它有一个输出值，名为 `SecuredDoc` 并且它的数据类型为 `com.adobe.idp.Document`. 为此进程创建Watched文件夹端点时（激活进程后，该进程将成为服务），必须定义输出参数值。

要定义Watched Folder端点所需的输出参数值，请指定以下值：

**输出参数名称**：输出参数的名称。 进程输出值的名称在Workbench中指定。 如果输出值属于服务操作（不是在Workbench中创建的流程的服务），则输出名称在component.xml文件中指定。 例如，本节介绍的进程的输出参数的名称为 `SecuredDoc`.

**映射类型**：用于配置服务和操作的输出。 以下选项可供选择：

* 如果服务返回单个对象（单个文档），则模式为 `%F.pdf` 源目标是sourcefilename.pdf。 例如，本节介绍的流程会返回单个文档。 因此，映射类型可以定义为 `%F.pdf` ( `%F` 表示使用给定的文件名)。 模式 `%E` 指定输入文档的扩展名。
* 如果服务返回列表，则模式为 `Result\%F\`，源目标是Result\sourcefilename\source1 （输出1）和Result\sourcefilename\source2 （输出2）。
* 如果服务返回映射，则模式为 `Result\%F\`，源目标是Result\sourcefilename\file1和Result\sourcefilename\file2。 如果地图有多个对象，则模式为 `Result\%F.pdf` 源目标为Result\sourcefilename1.pdf （输出1）、Result\sourcefilenam2.pdf （输出2）等。

**数据类型**：指定返回值的数据类型。 例如，本节介绍的进程的返回值的数据类型为 `com.adobe.idp.Document`.

**创建Watched文件夹端点**

在设置端点的属性、配置值以及定义输入和输出参数值后，必须创建Watched Folder端点。

**启用端点**

创建Watched Folder端点后，必须启用它。 启用端点后，可用于调用服务。 启用该端点后，您可以在管理控制台中查看它。

**另请参阅**

[使用Java API添加Watched文件夹端点](programmatically-endpoints.md#add-a-watched-folder-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API添加Watched文件夹端点 {#add-a-watched-folder-endpoint-using-the-java-api}

使用AEM Forms Java API添加Watched文件夹端点：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，例如adobe-livecycle-client.jar。

1. 创建EndpointRegistry客户端对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `EndpointRegistryClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 设置Watched Folder端点属性。

   * 创建 `CreateEndpointInfo` 对象。
   * 通过调用 `CreateEndpointInfo` 对象的 `setConnectorId` 方法和传递字符串值 `WatchedFolder`.
   * 通过调用 `CreateEndpointInfo` 对象的 `setDescription` 方法和传递描述端点的字符串值。
   * 通过调用 `CreateEndpointInfo` 对象的 `setName` 方法，并传递一个指定名称的字符串值。
   * 通过调用 `CreateEndpointInfo` 对象的 `setServiceId` 方法，并传递一个指定服务名称的字符串值。
   * 指定通过调用 `CreateEndpointInfo` 对象的 `setOperationName` 方法，并传递一个指定操作名称的字符串值。 通常，在为源自于Workbench中创建的进程的服务创建Watched文件夹端点时，会调用操作的名称。

1. 指定配置值。

   对于要为Watched文件夹端点设置的每个配置值，您必须调用 `CreateEndpointInfo` 对象的 `setConfigParameterAsText` 方法。 例如，要设置 `url` 配置值，调用 `CreateEndpointInfo` 对象的 `setConfigParameterAsText` 方法，并传递以下字符串值：

   * 一个字符串值，它指定配置值的名称。 设置时 `url` 配置值，指定 `url`.
   * 指定配置值值的字符串值。 设置时 `url` 配置值，指定watched文件夹位置。

   >[!NOTE]
   >
   >要查看EncryptDocument服务设置的所有配置值，请参阅位于以下位置的Java代码示例： [快速启动：使用Java API添加Watched文件夹端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api).

1. 定义输入参数值。

   通过调用 `CreateEndpointInfo` 对象的 `setInputParameterMapping` 方法，并传递以下值：

   * 一个字符串值，它指定输入参数的名称。 例如，EncryptDocument服务的输入参数的名称为 `InDoc`.
   * 指定输入参数的数据类型的字符串值。 例如，以下类型的数据类型 `InDoc` 输入参数为 `com.adobe.idp.Document`.
   * 指定映射类型的字符串值。 例如，您可以指定 `variable`.
   * 一个字符串值，它指定映射类型值。 例如，您可以指定&amp;ast；.pdf作为文件模式。

   >[!NOTE]
   >
   >调用 `setInputParameterMapping` 用于定义每个输入参数值的方法。 由于EncryptDocument进程只有一个输入参数，因此您需要调用此方法一次。

1. 定义输出参数值。

   通过调用 `CreateEndpointInfo` 对象的 `setOutputParameterMapping` 方法，并传递以下值：

   * 一个字符串值，它指定输出参数的名称。 例如，EncryptDocument服务的输出参数的名称为 `SecuredDoc`.
   * 指定输出参数的数据类型的字符串值。 例如，以下类型的数据类型 `SecuredDoc` 输出参数为 `com.adobe.idp.Document`.
   * 指定映射类型的字符串值。 例如，您可以指定 `%F.pdf`.

1. 创建Watched文件夹端点。

   通过调用 `EndpointRegistryClient` 对象的 `createEndpoint` 方法和传递 `CreateEndpointInfo` 对象。 此方法会返回 `Endpoint` 表示Watched文件夹端点的对象。

1. 启用端点。

   通过调用 `EndpointRegistryClient` 对象的 `enable` 方法和传递 `Endpoint` 返回的对象 `createEndpoint` 方法。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速启动：使用Java API添加Watched文件夹端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 观察文件夹配置值常量文件 {#watched-folder-configuration-values-constant-file}

此 [快速启动：使用Java API添加Watched文件夹端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api) 使用一个必须是Java项目一部分的常量文件来编译快速入门。 此常量文件表示添加Watched文件夹端点时必须设置的配置值。 以下Java代码表示常量文件。

```java
 /**
     * This class contains constants that can be used when setting Watched Folder
     * configuration values
     */

 public final class WatchedFolderEndpointConfigConstants {

         public static final String PROPERTY_FILEPROVIDER_URL = "url";
         public static final String PROPERTY_PROPERTY_ASYNCHRONOUS = "asynchronous";
         public static final String PROPERTY_CRON_EXPRESSION = "cronExpression";
         public static final String PROPERTY_PURGE_DURATION = "purgeDuration";
         public static final String PROPERTY_REPEAT_INTERVAL = "repeatInterval";
         public static final String PROPERTY_REPEAT_COUNT = "repeatCount";
         public static final String PROPERTY_THROTTLE = "throttleOn";
         public static final String PROPERTY_USERNAMER = "userName";
         public static final String PROPERTY_DOMAINNAME = "domainName";
         public static final String PROPERTY_FILEPROVIDER_BATCH_SIZE = "batchSize";
         public static final String PROPERTY_FILEPROVIDER_WAIT_TIME = "waitTime";
         public static final String PROPERTY_EXCLUDE_FILE_PATTERN = "excludeFilePattern";
         public static final String PROPERTY_INCLUDE_FILE_PATTERN = "excludeFilePattern";
         public static final String PROPERTY_FILEPROVIDER_RESULT_FOLDER_NAME =  "resultFolderName";
         public static final String PROPERTY_FILEPROVIDER_PRESERVE_FOLDER_NAME = "preserveFolderName";
         public static final String PROPERTY_FILEPROVIDER_FAILURE_FOLDER_NAME = "failureFolderName";
         public static final String PROPERTY_FILEPROVIDER_PRESERVE_ON_FAILURE = "preserveOnFailure";
         public static final String PROPERTY_FILEPROVIDER_OVERWRITE_DUPLICATE_FILENAME = "overwriteDuplicateFilename";
        }
```

## 添加电子邮件端点 {#adding-email-endpoints}

您可以使用AEM Forms Java API以编程方式将电子邮件端点添加到服务。 通过添加电子邮件端点，可让用户将包含一个或多个文件附件的电子邮件发送到指定的电子邮件帐户。 然后调用配置服务操作并操作文件。 服务执行指定的操作后，会向发件人发送一封电子邮件，其中包含作为文件附件的修改文件。

为了以编程方式将电子邮件端点添加到服务，请考虑以下命名的短暂过程 *MyApplication\EncryDocument*. 有关短暂进程的信息，请参见 [了解AEM Forms流程](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes).

![ae_ae_encryptdocumentprocess](assets/ae_ae_encryptdocumentprocess.png)

此流程接受不安全的PDF文档作为输入值，然后将不安全的PDF文档传递到加密服务的 `EncryptPDFUsingPassword` 操作。 此过程使用密码对PDF文档进行加密，并将经过密码加密的PDF文档作为输出值返回。 输入值(无保护PDF文档)的名称为 `InDoc` 并且数据类型是 `com.adobe.idp.Document`. 输出值(口令加密的PDF文档)的名称为 `SecuredDoc` 并且数据类型是 `com.adobe.idp.Document`.

>[!NOTE]
>
>无法使用Web服务添加电子邮件端点。

### 步骤摘要 {#summary_of_steps-3}

要将电子邮件端点添加到服务，请执行以下步骤：

1. 包括项目文件。
1. 创建 `EndpointRegistryClient` 对象。
1. 设置电子邮件端点属性。
1. 指定配置值。
1. 定义输入参数值。
1. 定义输出参数值。
1. 创建电子邮件端点。
1. 启用端点。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)
* jbossall-client.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)

有关这些JAR文件位置的信息，请参见 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建EndpointRegistry客户端对象**

在以编程方式添加电子邮件端点之前，您必须创建 `EndpointRegistryClient` 对象。

**设置电子邮件端点属性**

要为服务创建电子邮件端点，请指定以下值：

* **连接器标识符值**：指定创建的端点的类型。 要创建电子邮件端点，请指定 `Email`.
* **描述**：指定端点的描述。
* **名称**：指定端点的名称。
* **服务标识符值**：指定终结点所属的服务。 例如，要将电子邮件端点添加到此部分中介绍的流程（使用Workbench激活流程时，流程会变成服务），请指定 `EncryptDocument`.
* **操作名称**：指定使用端点调用的操作的名称。 通常，在为源自于Workbench中创建的流程的服务创建电子邮件端点时，操作的名称为 `invoke`.

**指定配置值**

以编程方式将电子邮件端点添加到服务时，必须指定电子邮件端点的配置值。 如果使用管理控制台添加电子邮件端点，则这些配置值由管理员指定。

>[!NOTE]
>
>受监视的电子邮件帐户是仅用于电子邮件端点的特殊帐户。 此帐户不是常规用户的电子邮件帐户。 不能将常规用户的电子邮件帐户配置为电子邮件提供商使用的帐户，因为电子邮件提供商在完成邮件的处理之后会从收件箱中删除电子邮件。

以编程方式将电子邮件端点添加到服务时，会设置以下配置值：

* **cronExpression**：如果必须使用cron表达式计划电子邮件，则为cron表达式。
* **repeatcount**：电子邮件端点扫描文件夹或目录的次数。 值–1表示无限扫描。 缺省值为–1。
* **repeateinterval**：接收方用于检查传入邮件的扫描速率（以秒为单位）。 默认值为 10。
* **startDelay**：计划程序启动后等待扫描的时间。 默认时间为0。
* **batchSize**：为了优化性能，接收者每次扫描处理的电子邮件数量。 值为–1表示所有电子邮件。 默认值为 2。
* **用户名**：从电子邮件调用目标服务时使用的用户名。 默认值为 `SuperAdmin`。
* **域名**：必需的配置值。 默认值为 `DefaultDom`。
* **域模式**：指定提供程序接受的传入电子邮件的域模式。 例如，如果 `adobe.com` 使用，仅处理来自adobe.com的电子邮件，而忽略来自其他域的电子邮件。
* **filePattern**：指定提供程序接受的传入文件附件模式。 这包括具有特定文件扩展名(&amp;ast；.dat、&amp;ast；.xml)的文件、具有特定名称（数据）的文件以及具有组合表达式名称和扩展名(&amp;ast；)的文件。[dD][aA]&#39;端口&#39;)。 默认值为 `*`。
* **recipientSuccessfulJob**：发送消息以指示作业成功的电子邮件地址。 默认情况下，成功的工作消息始终发送给发件人。 如果您键入 `sender`，将电子邮件结果发送给发件人。 支持最多100个收件人。 使用电子邮件地址指定其他收件人，每个收件人之间用逗号分隔。 要关闭此选项，请将此值留空。 在某些情况下，您可能希望触发一个进程，而不希望通过电子邮件通知结果。 默认值为 `sender`。
* **recipientFailedJob**：发送消息以指示失败的作业的电子邮件地址。 默认情况下，始终向发件人发送失败的作业消息。 如果您键入 `sender`，将电子邮件结果发送给发件人。 支持最多100个收件人。 使用电子邮件地址指定其他收件人，每个收件人之间用逗号分隔。 要关闭此选项，请将此值留空。 默认值为 `sender`。
* **inboxHost**：要扫描的电子邮件提供程序的收件箱主机名或IP地址。
* **inboxPort**：电子邮件服务器使用的端口。 POP3的默认值为110，IMAP的默认值为143。 如果启用了SSL，则POP3的默认值为995，而IMAP的默认值为993。
* **inboxProtocol**：用于扫描收件箱的电子邮件端点的电子邮件协议。 选项包括 `IMAP` 或 `POP3`. 收件箱主机邮件服务器必须支持这些协议。
* **收件箱超时**：电子邮件提供商等待收件箱响应的超时（以秒为单位）。 默认值为 60。
* **inboxUser**：登录电子邮件帐户所需的用户名。 根据电子邮件服务器和配置，这可能是电子邮件的用户名部分，也可能是完整的电子邮件地址。
* **inboxPassword**：收件箱用户的密码。
* **inboxSSLEnabled**：设置此值可强制电子邮件提供商在发送结果或错误的通知消息时使用SSL。 确保IMAP或POP3主机支持SSL。
* **smtpHost**：电子邮件提供商向其发送结果和错误消息的邮件服务器的主机名。
* **smtpPort**：SMTP端口的默认值为25。
* **smtuser**：电子邮件提供商在发送有关结果和错误的电子邮件通知时使用的用户帐户。
* **smtpPassword**：SMTP帐户的密码。 某些邮件服务器不需要SMTP密码。
* **charSet**：电子邮件提供商使用的字符集。 默认值为 `UTF-8`。
* **smtpSSLEnabled**：设置此值可强制电子邮件提供商在发送结果或错误的通知消息时使用SSL。 确保SMTP主机支持SSL。
* **failedJobFolder**：指定当SMTP邮件服务器不工作时，用于存储结果的目录。
* **异步**：当设置为synchronous时，将处理所有输入文档并返回单个响应。 当设置为异步时，将为处理的每个输入文档发送响应。 例如，为本主题中介绍的流程创建了一个电子邮件端点，并会向端点的收件箱发送一封包含多个不安全的PDF文档的电子邮件。 当所有PDF文档都使用密码加密时，如果端点配置为同步，则会发送一条响应电子邮件，并附上所有安全的PDF文档。 如果端点配置为异步，则会为每个安全PDF文档发送单独的响应电子邮件消息。 每封电子邮件都包含一个PDF文档作为附件。 默认值为asynchronous。

**定义输入参数值**

创建电子邮件端点时，必须定义输入参数值。 即，必须描述传递到电子邮件端点调用的操作的输入值。 例如，请考虑本主题中引入的过程。 它具有一个名为的输入值 `InDoc` 并且它的数据类型为 `com.adobe.idp.Document`. 为此流程创建电子邮件端点时（激活流程后，该流程将成为服务），必须定义输入参数值。

要定义电子邮件端点所需的输入参数值，请指定以下值：

**输入参数名称**：输入参数的名称。 在Workbench中为进程指定输入值的名称。 如果输入值属于服务操作(不是在Workbench中创建的进程的Forms服务)，则在component.xml文件中指定输入名称。 例如，本节介绍的进程的输入参数的名称为 `InDoc`.

**映射类型**：用于配置调用服务操作所需的输入值。 有两种类型的映射类型，如下所示：

* `Literal`：电子邮件端点使用在显示的字段中输入的值。 支持所有基本Java类型。 例如，如果API使用字符串、long、int和Boolean等输入，则字符串将转换为正确的类型并调用服务。
* `Variable`：输入的值是电子邮件端点用来选取输入的文件模式。 例如，如果为映射类型选择“变量”，并且输入文档必须是PDF文件，则可以指定 `*.pdf` 作为映射值。

**映射值**：指定映射类型的值。 例如，如果选择“变量”映射类型，则可以指定 `*.pdf` 作为文件模式。

**数据类型**：指定输入值的数据类型。 例如，本节介绍的进程的输入值的数据类型是com.adobe.idp.Document。

**定义输出参数值**

创建电子邮件端点时，必须定义输出参数值。 即，必须描述由电子邮件端点调用的服务返回的输出值。 例如，请考虑本主题中引入的过程。 它有一个输出值，名为 `SecuredDoc` 并且它的数据类型为 `com.adobe.idp.Document`. 为此流程创建电子邮件端点时（激活流程后，该流程将成为服务），必须定义输出参数值。

要定义电子邮件端点所需的输出参数值，请指定以下值：

**输出参数名称**：输出参数的名称。 进程输出值的名称在Workbench中指定。 如果输出值属于服务操作（不是在Workbench中创建的流程的服务），则输出名称在component.xml文件中指定。 例如，本节介绍的进程的输出参数的名称为 `SecuredDoc`.

**映射类型**：用于配置服务和操作的输出。 以下选项可供选择：

* 如果服务返回单个对象（单个文档），则模式为 `%F.pdf` 源目标是sourcefilename.pdf。 例如，本节介绍的流程会返回单个文档。 因此，映射类型可以定义为 `%F.pdf` ( `%F` 表示使用给定的文件名)。 模式 `%E` 指定输入文档的扩展名。
* 如果服务返回列表，则模式为 `Result\%F\`，源目标是Result\sourcefilename\source1 （输出1）和Result\sourcefilename\source2 （输出2）。
* 如果服务返回映射，则模式为 `Result\%F\`，源目标是Result\sourcefilename\file1和Result\sourcefilename\file2。 如果地图有多个对象，则模式为 `Result\%F.pdf` 源目标为Result\sourcefilename1.pdf （输出1）、Result\sourcefilenam2.pdf （输出2）等。

**数据类型**：指定返回值的数据类型。 例如，本节介绍的进程的返回值的数据类型为 `com.adobe.idp.Document`.

**创建电子邮件端点**

在设置电子邮件端点属性和配置值并定义输入和输出参数值后，必须创建电子邮件端点。

**启用端点**

创建电子邮件端点后，必须启用它。 启用端点后，可用于调用服务。 启用该端点后，您可以在管理控制台中查看它。

**另请参阅**

[使用Java API添加电子邮件端点](programmatically-endpoints.md#add-an-email-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API添加电子邮件端点 {#add-an-email-endpoint-using-the-java-api}

使用Java API添加电子邮件端点：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，例如adobe-livecycle-client.jar。

1. 创建EndpointRegistry客户端对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `EndpointRegistryClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 设置电子邮件端点属性。

   * 创建 `CreateEndpointInfo` 对象。
   * 通过调用 `CreateEndpointInfo` 对象的 `setConnectorId` 方法和传递字符串值 `Email`.
   * 通过调用 `CreateEndpointInfo` 对象的 `setDescription` 方法和传递描述端点的字符串值。
   * 通过调用 `CreateEndpointInfo` 对象的 `setName` 方法，并传递一个指定名称的字符串值。
   * 通过调用 `CreateEndpointInfo` 对象的 `setServiceId` 方法，并传递一个指定服务名称的字符串值。
   * 指定通过调用 `CreateEndpointInfo` 对象的 `setOperationName` 方法，并传递一个指定操作名称的字符串值。 通常，在为源自于Workbench中创建的流程的服务创建电子邮件端点时，会调用操作的名称。

1. 指定配置值。

   对于要为电子邮件端点设置的每个配置值，您必须调用 `CreateEndpointInfo` 对象的 `setConfigParameterAsText` 方法。 例如，要设置 `smtpHost` 配置值，调用 `CreateEndpointInfo` 对象的 `setConfigParameterAsText` 方法，并传递以下值：

   * 一个字符串值，它指定配置值的名称。 设置时 `smtpHost` 配置值，指定 `smtpHost`.
   * 指定配置值值的字符串值。 设置时 `smtpHost` 配置值，指定指定SMTP服务器名称的字符串值。

   >[!NOTE]
   >
   >要查看本节中引入的EncryptDocument服务的所有配置值集，请参阅位于以下位置的Java代码示例： [快速入门：使用Java API添加电子邮件端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api).

1. 定义输入参数值。

   通过调用 `CreateEndpointInfo` 对象的 `setInputParameterMapping` 方法，并传递以下值：

   * 一个字符串值，它指定输入参数的名称。 例如，EncryptDocument服务的输入参数的名称为 `InDoc`.
   * 指定输入参数的数据类型的字符串值。 例如，以下类型的数据类型 `InDoc` 输入参数为 `com.adobe.idp.Document`.
   * 指定映射类型的字符串值。 例如，您可以指定 `variable`.
   * 一个字符串值，它指定映射类型值。 例如，您可以指定&amp;ast；.pdf作为文件模式。

   >[!NOTE]
   >
   >调用 `setInputParameterMapping` 用于定义每个输入参数值的方法。 由于EncryptDocument进程只有一个输入参数，因此您需要调用此方法一次。

1. 定义输出参数值。

   通过调用 `CreateEndpointInfo` 对象的 `setOutputParameterMapping` 方法，并传递以下值：

   * 一个字符串值，它指定输出参数的名称。 例如，EncryptDocument服务的输出参数的名称为 `SecuredDoc`.
   * 指定输出参数的数据类型的字符串值。 例如，以下类型的数据类型 `SecuredDoc` 输出参数为 `com.adobe.idp.Document`.
   * 指定映射类型的字符串值。 例如，您可以指定 `%F.pdf`.

1. 创建电子邮件端点。

   通过调用 `EndpointRegistryClient` 对象的 `createEndpoint` 方法和传递 `CreateEndpointInfo` 对象。 此方法会返回 `Endpoint` 表示电子邮件端点的对象。

1. 启用端点。

   通过调用 `EndpointRegistryClient` 对象的 `enable` 方法和传递 `Endpoint` 返回的对象 `createEndpoint` 方法。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速启动：使用Java API添加Watched文件夹端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 电子邮件配置值常量文件 {#email-configuration-values-constant-file}

此 [快速入门：使用Java API添加电子邮件端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api) 使用一个必须是Java项目一部分的常量文件来编译快速入门。 此常量文件表示添加电子邮件端点时必须设置的配置值。 以下Java代码表示常量文件。

```java
 /**
     * This class contains constants that can be used when setting email endpoint
     * configuration values
     */
 public class EmailEndpointConfigConstants {

     public static final String PROPERTY_EMAILPROVIDER_CRON_EXPRESSION = "cronExpression";
     public static final String PROPERTY_EMAILPROVIDER_REPREAT_COUNT = "repeatCount";
     public static final String PROPERTY_EMAILPROVIDER_REPREAT_INTERVAL = "repeatInterval";
     public static final String PROPERTY_EMAILPROVIDER_START_DELAY = "startDelay";
     public static final String PROPERTY_EMAILPROVIDER_BATCH_SIZE = "batchSize";
     public static final String PROPERTY_EMAILPROVIDER_USERNAME = "userName";
     public static final String PROPERTY_EMAILPROVIDER_DOMAINNAME = "domainName";
     public static final String PROPERTY_EMAILPROVIDER_DOMAINPATTERN = "domainPattern";
     public static final String PROPERTY_EMAILPROVIDER_FILEPATTERN = "filePattern";
     public static final String PROPERTY_EMAILPROVIDER_RECIPIENT_SUCCESSFUL_JOB = "recipientSuccessfulJob";
     public static final String PROPERTY_EMAILPROVIDER_RECIPIENT_FAILED_JOB = "recipientFailedJob";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_HOST = "inboxHost";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_PORT = "inboxPort";
     public static final String PROPERTY_EMAILPROVIDER_PROTOCOL = "inboxProtocol";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_TIMEOUT = "inboxTimeOut";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_USER = "inboxUser";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_PASSWORD = "inboxPassword";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_SSL = "inboxSSLEnabled";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_HOST = "smtpHost";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_PORT = "smtpPort";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_USER = "smtpUser";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_PASSWORD = "smtpPassword";
     public static final String PROPERTY_EMAILPROVIDER_CHARSET = "charSet";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_SSL = "smtpSSLEnabled";
     public static final String PROPERTY_EMAILPROVIDER_FAILED_FOLDER = "failedJobFolder";
     public static final String PROPERTY_EMAILPROVIDER_ASYNCHRONOUS = "asynchronous";
 }
```

## 添加远程端点 {#adding-remoting-endpoints}

>[!NOTE]
>
>JEE上的AEM表单弃用LiveCycle RemotingAPI。

您可以使用AEM Forms Java API以编程方式将远程端点添加到服务。 通过添加远程处理端点，您可以使Flex应用程序能够使用远程处理来调用服务。 (请参阅 [使用AEM Forms调用(已为AEM表单弃用) AEM Forms远程处理](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

为了以编程方式将远程处理端点添加到服务，请考虑以下命名的短暂过程 *EncryDocument*.

![ar_ar_encryptdocumentprocess](assets/ar_ar_encryptdocumentprocess.png)

此流程接受不安全的PDF文档作为输入值，然后将不安全的PDF文档传递到加密服务的 `EncryptPDFUsingPassword` 操作。 PDF文档使用密码进行加密，密码加密的PDF文档是此过程的输出值。 输入值(无保护PDF文档)的名称为 `InDoc` 并且数据类型是 `com.adobe.idp.Document`. 输出值(口令加密的PDF文档)的名称为 `SecuredDoc` 并且数据类型是 `com.adobe.idp.Document`.

为了演示如何将Remoting端点添加到服务，本节将Remoting端点添加到名为EncryptDocument的服务。

>[!NOTE]
>
>无法使用Web服务添加远程端点。

### 步骤摘要 {#summary_of_steps-4}

要从服务中删除端点，请执行以下任务：

1. 包括项目文件。
1. 创建 `EndpointRegistryClient` 对象。
1. 设置远程端点属性。
1. 创建远程端点。
1. 启用端点。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)
* jbossall-client.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)

有关这些JAR文件位置的信息，请参见 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建EndpointRegistry客户端对象**

要以编程方式添加远程端点，您必须创建 `EndpointRegistryClient` 对象。

**设置远程端点属性**

要为服务创建远程端点，请指定以下值：

* **连接器标识符值**：指定创建的端点的类型。 要创建远程处理端点，请指定 `Remoting`.
* **描述**：指定端点的描述。
* **名称**：指定端点的名称。
* **服务标识符值**：指定终结点所属的服务。 例如，要将Remoting端点添加到此部分中介绍的进程（在Workbench中激活某个进程时，该进程将成为服务），请指定 `EncryptDocument`.
* **操作名称**：指定使用端点调用的操作的名称。 创建远程处理端点时，请指定通配符(&amp;ast；)。

**创建远程端点**

设置远程端点属性后，可以为服务创建远程端点。

**启用端点**

创建新端点后，必须启用它。 启用远程处理端点后，Flex客户端将能够调用该服务。

**另请参阅**

[使用Java API添加远程端点](programmatically-endpoints.md#add-a-remoting-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API添加远程端点 {#add-a-remoting-endpoint-using-the-java-api}

使用Java API添加远程端点：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，例如adobe-livecycle-client.jar。

1. 创建EndpointRegistry客户端对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `EndpointRegistryClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 设置远程端点属性。

   * 创建 `CreateEndpointInfo` 对象。
   * 通过调用 `CreateEndpointInfo` 对象的 `setConnectorId` 方法和传递字符串值 `Remoting`.
   * 通过调用 `CreateEndpointInfo` 对象的 `setDescription` 方法和传递描述端点的字符串值。
   * 通过调用 `CreateEndpointInfo` 对象的 `setName` 方法，并传递一个指定名称的字符串值。
   * 通过调用 `CreateEndpointInfo` 对象的 `setServiceId` 方法，并传递一个指定服务名称的字符串值。
   * 指定调用操作 `CreateEndpointInfo` 对象的 `setOperationName` 方法，并传递一个指定操作名称的字符串值。 对于远程处理端点，请指定通配符(&amp;ast；)。

1. 创建远程端点。

   通过调用 `EndpointRegistryClient` 对象的 `createEndpoint` 方法和传递 `CreateEndpointInfo` 对象。 此方法会返回 `Endpoint` 表示新远程处理端点的对象。

1. 启用端点。

   通过调用 `EndpointRegistryClient` 对象的 `enable` 方法和传递 `Endpoint` 返回的对象 `createEndpoint` 方法。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速入门：使用Java API添加远程端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-remoting-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 添加TaskManager端点 {#adding-taskmanager-endpoints}

您可以使用AEM Forms Java API以编程方式将TaskManager端点添加到服务。 通过将TaskManager端点添加到服务，可以使Workspace用户能够调用该服务。 也就是说，在Workspace中工作的用户可以调用具有相应TaskManager端点的进程。

>[!NOTE]
>
>无法使用Web服务添加TaskManager端点。

### 步骤摘要 {#summary_of_steps-5}

要向服务添加TaskManager端点，请执行以下任务：

1. 包括项目文件。
1. 创建 `EndpointRegistryClient` 对象。
1. 为端点创建类别。
1. 设置TaskManager端点属性。
1. 创建TaskManager端点。
1. 启用端点。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)
* jbossall-client.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)

有关这些JAR文件位置的信息，请参见 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建EndpointRegistry客户端对象**

您必须先创建 `EndpointRegistryClient` 对象。

**为端点创建类别**

类别用于在工作区中组织服务。 也就是说，Workspace用户可以通过在Workspace中选择类别来调用具有TaskManager端点的服务。 创建TaskManager端点时，您可以引用现有类别或以编程方式创建新类别。

>[!NOTE]
>
>此部分在将TaskManager端点添加到服务时创建新类别。

**设置TaskManager端点属性**

要为服务创建TaskManager端点，请指定以下值：

* **连接器标识符**：指定创建的端点的类型。 要创建TaskManager端点，请指定 `TaskManagerConnector`.
* **描述**：指定端点的描述。
* **名称**：指定端点的名称。
* **服务标识符**：指定终结点所属的服务。
* **类别**：指定与TaskManager端点关联的类别标识符值。
* **操作名称**：通常，在为源自于Workbench中创建的进程的服务创建任务管理器端点时，操作的名称为 `invoke`.

**创建TaskManager端点**

设置TaskManager端点属性后，可以为服务创建TaskManager端点。

**启用端点**

创建新端点后，必须启用它。 启用该端点后，可用于从Workspace中调用服务。 启用该端点后，您可以在管理控制台中查看它。

**另请参阅**

[使用Java API添加TaskManager端点](programmatically-endpoints.md#add-a-taskmanager-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API添加TaskManager端点 {#add-a-taskmanager-endpoint-using-the-java-api}

使用Java API添加TaskManager端点：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，例如adobe-livecycle-client.jar。

1. 创建EndpointRegistry客户端对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `EndpointRegistryClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 为端点创建类别。

   * 创建 `CreateEndpointCategoryInfo` 对象，方法是：使用其构造函数并传递以下值：

      * 一个字符串值，它指定类别的标识符值
      * 指定类别说明的字符串值
   * 通过调用 `EndpointRegistryClient` 对象的 `createEndpointCategory` 方法和传递 `CreateEndpointCategoryInfo` 对象。 此方法会返回 `EndpointCategory` 表示新类别的对象。


1. 设置TaskManager端点属性。

   * 创建 `CreateEndpointInfo` 对象。
   * 通过调用 `CreateEndpointInfo` 对象的 `setConnectorId` 方法和传递字符串值 `TaskManagerConnector`.
   * 通过调用 `CreateEndpointInfo` 对象的 `setDescription` 方法和传递描述端点的字符串值。
   * 通过调用 `CreateEndpointInfo` 对象的 `setName` 方法，并传递一个指定名称的字符串值。
   * 通过调用 `CreateEndpointInfo` 对象的 `setServiceId` 方法，并传递一个指定服务名称的字符串值。
   * 通过调用 `CreateEndpointInfo` 对象的 `setCategoryId` 和传递指定类别标识符值的字符串值。 您可以调用 `EndpointCategory` 对象的 `getId` 用于获取此类别的标识符值的方法。
   * 指定通过调用 `CreateEndpointInfo` 对象的 `setOperationName` 方法，并传递一个指定操作名称的字符串值。 通常，在创建 `TaskManager` 源自在Workbench中创建的进程的服务的端点，该操作的名称为 `invoke`.

1. 创建TaskManager端点。

   通过调用 `EndpointRegistryClient` 对象的 `createEndpoint` 方法和传递 `CreateEndpointInfo` 对象。 此方法会返回 `Endpoint` 表示新TaskManager端点的对象。

1. 启用端点。

   通过调用 `EndpointRegistryClient` 对象的 `enable` 方法和传递 `Endpoint` 返回的对象 `createEndpoint` 方法。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速入门：使用Java API添加TaskManager端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-taskmanager-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 修改端点 {#modifying-endpoints}

您可以使用AEM Forms Java API以编程方式修改现有端点。 通过修改端点，可以更改端点的行为。 例如，假定一个Watched文件夹端点，它指定用作Watched文件夹的文件夹。 您可以通过编程方式修改属于Watched文件夹端点的配置值，从而让另一个文件夹充当Watched文件夹。 有关属于观察文件夹端点的配置值的信息，请参见 [添加观察文件夹端点](programmatically-endpoints.md#adding-watched-folder-endpoints).

为了演示如何修改端点，本节通过更改作为Watched文件夹的文件夹来修改Watched文件夹端点。

>[!NOTE]
>
>无法使用Web服务修改端点。

### 步骤摘要 {#summary_of_steps-6}

要修改端点，请执行以下任务：

1. 包括项目文件。
1. 创建 `EndpointRegistryClient` 对象。
1. 检索端点。
1. 指定新的配置值。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)
* jbossall-client.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)

有关这些JAR文件位置的信息，请参见 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建EndpointRegistry客户端对象**

要以编程方式修改端点，您必须创建 `EndpointRegistryClient` 对象。

**检索要修改的端点**

必须先检索端点，然后才能修改端点。 要检索端点，您必须以能够访问端点的用户身份连接。 建议您以管理员身份连接。 (请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties))。

您可以通过检索端点列表来检索端点。 然后，您可以遍历列表，搜索要删除的特定端点。 例如，您可以通过确定与端点对应的服务和端点类型来定位端点。 找到端点后，可以对其进行修改。

**指定新的配置值**

修改端点时，请指定新的配置值。 例如，要修改Watched Folder端点，请重置所有Watched Folder端点配置值，而不仅仅是要修改的值。 有关属于观察文件夹端点的配置值的信息，请参见 [添加观察文件夹端点](programmatically-endpoints.md#adding-watched-folder-endpoints).

>[!NOTE]
>
>有关属于电子邮件端点的配置值的信息，请参阅 [添加电子邮件端点](programmatically-endpoints.md#adding-email-endpoints).

>[!NOTE]
>
>您无法修改终结点调用的服务。 如果尝试修改服务，则会引发异常。 要修改与给定端点关联的服务，请删除端点并创建新端点。 (请参阅 [删除端点](programmatically-endpoints.md#removing-endpoints).)

**另请参阅**

[使用Java API修改端点](programmatically-endpoints.md#modifying-an-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API修改端点 {#modifying-an-endpoint-using-the-java-api}

使用Java API修改端点：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，例如adobe-livecycle-client.jar。

1. 创建EndpointRegistry客户端对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `EndpointRegistryClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 检索要修改的端点。

   * 通过调用，检索当前用户（在连接属性中指定）可以访问的所有端点的列表 `EndpointRegistryClient` 对象的 `getEndpoints` 方法和传递 `PagingFilter` 用作过滤器的对象。 您可以传递 `(PagingFilter)null` 值返回所有端点。 此方法会返回 `java.util.List` 对象，其中每个元素为 `Endpoint` 对象。 有关的信息 `PagingFilter` 对象，请参见 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * 循环访问 `java.util.List` 对象以确定它是否具有端点。 如果存在端点，则每个元素都是一个 `EndPoint` 实例。
   * 通过调用 `EndPoint` 对象的 `getServiceId` 方法。 此方法返回一个指定服务名称的字符串值。
   * 通过调用 `EndPoint` 对象的 `getConnectorId` 方法。 此方法返回一个指定终结点类型的字符串值。 例如，如果端点是Watched Folder端点，则此方法将返回 `WatchedFolder`.

1. 指定新的配置值。

   * 创建 `ModifyEndpointInfo` 对象。
   * 对于要设置的每个配置值，调用 `ModifyEndpointInfo` 对象的 `setConfigParameterAsText` 方法。 例如，要设置url配置值，请调用 `ModifyEndpointInfo` 对象的 `setConfigParameterAsText` 方法，并传递以下值：

      * 一个字符串值，它指定配置值的名称。 例如，要设置 `url` 配置值，指定 `url`.
      * 指定配置值值的字符串值。 要定义 `url` 配置值，指定watched文件夹位置。
   * 调用 `EndpointRegistryClient` 对象的 `modifyEndpoint` 方法并传递 `ModifyEndpointInfo` 对象。


**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速入门：使用Java API修改端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-modifying-an-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 删除端点 {#removing-endpoints}

您可以使用AEM Forms Java API以编程方式从服务中删除端点。 删除终结点后，无法使用终结点启用的调用方法调用该服务。 例如，如果从服务中删除SOAP端点，则无法使用SOAP模式调用该服务。

要演示如何从服务中删除端点，本节从名为的服务中删除EJB端点 *EncryDocument*.

>[!NOTE]
>
>无法使用Web服务删除端点。

### 步骤摘要 {#summary_of_steps-7}

要从服务中删除端点，请执行以下任务：

1. 包括项目文件。
1. 创建 `EndpointRegistryClient` 对象。
1. 检索端点。
1. 删除端点。

**包括项目文件**

将必要的文件包含到开发项目中。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)
* jbossall-client.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)

有关这些JAR文件位置的信息，请参见 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建EndpointRegistry客户端对象**

要以编程方式删除端点，您必须创建 `EndpointRegistryClient` 对象。

**检索要删除的端点**

必须先检索端点，然后才能删除端点。 要检索端点，您必须以能够访问端点的用户身份连接。 建议您以管理员身份连接。 (请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties))。

您可以通过检索端点列表来检索端点。 然后，您可以遍历列表，搜索要删除的特定端点。 例如，您可以通过确定与端点对应的服务和端点类型来定位端点。 找到端点后，可以将其删除。

**删除端点**

创建新端点后，必须启用它。 启用端点后，可用于调用服务。 启用该端点后，您可以在管理控制台中查看它。

**另请参阅**

[使用Java API删除端点](programmatically-endpoints.md#removing-an-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API删除端点 {#removing-an-endpoint-using-the-java-api}

使用Java API删除端点：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，例如adobe-livecycle-client.jar。

1. 创建EndpointRegistry客户端对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `EndpointRegistryClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 检索要删除的端点。

   * 通过调用，检索当前用户（在连接属性中指定）有权访问的所有端点的列表 `EndpointRegistryClient` 对象的 `getEndpoints` 方法和传递 `PagingFilter` 用作过滤器的对象。 你可以通过 `(PagingFilter)null` 以返回所有端点。 此方法会返回 `java.util.List` 对象，其中每个元素为 `Endpoint` 对象。
   * 循环访问 `java.util.List` 对象以确定它是否具有端点。 如果存在端点，则每个元素都为 `EndPoint` 实例。
   * 通过调用 `EndPoint` 对象的 `getServiceId` 方法。 此方法返回一个指定服务名称的字符串值。
   * 通过调用 `EndPoint` 对象的 `getConnectorId` 方法。 此方法返回一个指定终结点类型的字符串值。 例如，如果端点是EJB端点，则此方法将返回 `EJB`.

1. 删除端点。

   通过调用 `EndpointRegistryClient` 对象的 `remove` 方法和传递 `EndPoint` 表示要删除的端点的对象。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速启动：使用Java API删除端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-removing-an-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 正在检索终结点连接器信息 {#retrieving-endpoint-connector-information}

您可以使用AEM Forms API以编程方式检索有关端点连接器的信息。 连接器使端点能够使用各种调用方法调用服务。 例如，Watched文件夹连接器允许端点使用watched文件夹调用服务。 通过以编程方式检索有关端点连接器的信息，可以检索与连接器关联的配置值，例如哪些配置值是必需的以及哪些是可选的。

要演示如何检索有关端点连接器的信息，本节将检索有关Watched Folder连接器的信息。 (请参阅 [添加观察文件夹端点](programmatically-endpoints.md#adding-watched-folder-endpoints).)

>[!NOTE]
>
>无法使用Web服务检索有关终结点的信息。

>[!NOTE]
>
>本主题使用 `ConnectorRegistryClient` 用于检索有关端点连接器信息的API。 (请参阅 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

### 步骤摘要 {#summary_of_steps-8}

要检索终结点连接器信息，请执行以下任务：

1. 包括项目文件。
1. 创建 `ConnectorRegistryClient` 对象。
1. 指定连接器类型。
1. 检索配置值。

**包括项目文件**

将必要的文件包含到开发项目中。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)
* jbossall-client.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)

如果AEM Forms部署在支持的J2EE应用程序服务器（不是JBoss）上，请将adobe-utilities.jar和jbossall-client.jar替换为特定于部署AEM Forms的J2EE应用程序服务器的JAR文件。 有关所有AEM Forms JAR文件位置的信息，请参见 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建ConnectorRegistry客户端对象**

要以编程方式检索端点连接器信息，请创建 `ConnectorRegistryClient` 对象。

**指定连接器类型**

指定要从中检索信息的连接器的类型。 存在以下类型的连接器：

* **EJB**：使客户端应用程序能够使用EJB模式调用服务。
* **SOAP**：使客户端应用程序能够使用SOAP模式调用服务。
* **观察文件夹**：启用Watched文件夹以调用服务。
* **电子邮件**：启用电子邮件以调用服务。
* **远程处理**：使Flex客户端应用程序能够调用服务。
* **任务管理器连接器**：允许Workspace用户从Workspace中调用服务。

**检索配置值**

指定连接器类型后，可以检索有关连接器的信息，如支持的配置值。 例如，对于任何连接器，您可以确定哪些配置值是必需的，哪些是可选的。

**另请参阅**

[使用Java API检索端点连接器信息](programmatically-endpoints.md#retrieve-endpoint-connector-information-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API检索端点连接器信息 {#retrieve-endpoint-connector-information-using-the-java-api}

使用Java API检索端点连接器信息：

1. 包括项目文件。.

   在Java项目的类路径中包含客户端JAR文件，例如adobe-livecycle-client.jar。

1. 创建ConnectorRegistry客户端对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `ConnectorRegistryClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 指定连接器类型。

   通过调用 `ConnectorRegistryClient` 对象的 `getEndpointDefinition` 方法，并传递一个指定连接器类型的字符串值。 例如，要指定Watched Folder连接器类型，请传递字符串值 `WatchedFolder`. 此方法会返回 `Endpoint` 对应于连接器类型的对象。

1. 检索配置值。

   * 通过调用 `Endpoint` 对象的 `getConfigParameters` 方法。 此方法返回一个数组 `ConfigParameter` 对象。
   * 通过检索数组中的每个元素来检索有关每个配置值的信息。 每个元素都是一个 `ConfigParameter` 对象。 例如，您可以通过调用 `ConfigParameter` 对象的 `isRequired` 方法。 如果需要配置值，则此方法将返回 `true`.

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速启动：使用Java API检索端点连接器信息](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-retrieving-endpoint-connector-information-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
