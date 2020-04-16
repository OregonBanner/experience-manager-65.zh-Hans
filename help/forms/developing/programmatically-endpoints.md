---
title: 以编程方式管理端点
seo-title: 以编程方式管理端点
description: 'null'
seo-description: 'null'
uuid: 5dc50946-3323-4c5d-a43b-31c1c980bd04
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 076889a7-9c9f-4b6f-a45b-67a9b3923c36
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3

---


# 以编程方式管理端点 {#programmatically-managing-endpoints}

**关于端点注册服务**

Endpoint Registry服务提供了以编程方式管理端点的能力。 例如，您可以向服务添加以下类型的端点：

* EJB
* SOAP
* 监视文件夹
* 电子邮件
* （AEM表单已弃用）远程处理
* 任务经理

>[!NOTE]
>
>SOAP、EJB和（JEE上的AEM表单已弃用）为每个已激活的服务自动创建远程处理端点。 SOAP和EJB端点为所有服务操作启用SOAP和EJB。

远程处理端点使Flex客户端能够调用将端点添加到的AEM Forms服务上的操作。 创建与端点同名的Flex目标，Flex客户端可以创建指向该目标的RemoteObjects，以调用相关服务上的操作。

电子邮件、任务管理器和监视文件夹端点仅显示服务的特定操作。 添加这些端点需要第二个配置步骤来选择调用、设置配置参数以及指定输入和输出参数映射的方法。

您可以将TaskManager端点组织到称为 *类别的组中*。 然后，这些类别会通过TaskManager向Workspace公开，最终用户在分类时会看到TaskManager端点。 在Workspace中，最终用户可以在导航窗格中看到这些类别。 每个类别中的端点在Workspace的“开始进程”页面上显示为进程卡。

您可以使用Endpoint Registry服务完成以下任务:

* 添加EJB端点。 (请参阅 [添加EJB端点](programmatically-endpoints.md#adding-ejb-endpoints)。)
* 添加SOAP端点。 (请参阅 [添加SOAP端点](programmatically-endpoints.md#adding-soap-endpoints)。)
* 添加监视文件夹端点(请参阅 [添加监视文件夹端点](programmatically-endpoints.md#adding-watched-folder-endpoints)。)
* 添加电子邮件端点。 (请参阅 [添加电子邮件端点](programmatically-endpoints.md#adding-email-endpoints)。)
* 添加远程处理端点。 (请参阅 [添加远程处理端点](programmatically-endpoints.md#adding-remoting-endpoints)。)
* 添加TaskManager端点(请参 [阅添加TaskManager端点](programmatically-endpoints.md#adding-taskmanager-endpoints)。)
* 修改端点(请参 [阅修改端点](programmatically-endpoints.md#modifying-endpoints)。)
* 删除端点(请参 [阅删除端点](programmatically-endpoints.md#removing-endpoints)。)
* 检索端点连接器信息(请参 [阅检索端点连接器信息](programmatically-endpoints.md#retrieving-endpoint-connector-information)。)

## 添加EJB端点 {#adding-ejb-endpoints}

可以使用AEM Forms Java API以编程方式将EJB端点添加到服务。 通过向服务添加EJB端点，您可以使客户端应用程序通过使用EJB模式调用该服务。 即，在设置调用AEM Forms所需的连接属性时，可以选择EJB模式。 (请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。)

>[!NOTE]
>
>不能使用Web服务添加EJB端点。

>[!NOTE]
>
>通常，EJB端点在默认情况下会添加到服务中，但是，EJB端点可以添加到以编程方式部署的进程中，或者在删除EJB端点后必须重新添加。

### 步骤摘要 {#summary-of-steps}

要将EJB端点添加到服务，请执行以下任务:

1. 包括项目文件。
1. 创建对 `EndpointRegistry Client` 象。
1. 设置EJB端点属性。
1. 创建EJB端点。
1. 启用端点。

**包括项目文件**

在开发项目中包含必要的文件。 以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（在JBoss Application Server上部署AEM Forms时为必需）
* jbossall-client.jar（在JBoss Application Server上部署AEM表单时需要）

有关这些JAR文件的位置的信息，请参 [阅包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建EndpointRegistry客户端对象**

在以编程方式添加EJB端点之前，必须先创建一个 `EndpointRegistryClient` 对象。

**设置EJB端点属性**

要为服务创建EJB端点，请指定以下值：

* **连接器标识符**:指定要创建的端点类型。 要创建EJB端点，请指定 `EJB`。
* **说明**:指定端点描述。
* **名称**:指定端点的名称。
* **服务标识符**:指定端点所属的服务。
* **操作名称**:指定使用端点调用的操作的名称。 创建EJB端点时，请指定通配符( `*`)。 但是，如果要指定特定操作而不是调用所有服务操作，则指定操作的名称，而不是使用通配符( `*`)。

**创建EJB端点**

设置EJB端点属性后，可以为服务创建EJB端点。

**启用端点**

创建新端点后，必须启用它。 在启用端点后，可以使用它调用服务。 启用端点后，可以在管理控制台中视图它。

**另请参阅**

[使用Java API添加EJB端点](programmatically-endpoints.md#adding-an-ejb-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API添加EJB端点 {#adding-an-ejb-endpoint-using-the-java-api}

使用Java API添加EJB端点：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-livecycle-client.jar。 （

1. 创建EndpointRegistry客户端对象。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `EndpointRegistryClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 设置EJB端点属性。

   * 使用对 `CreateEndpointInfo` 象的构造函数创建对象。
   * 通过调用对象的方法并传递 `CreateEndpointInfo` 字符串值 `setConnectorId` 来指定连接器标识符值 `EJB`。
   * 通过调用对象的方法并传递描述端 `CreateEndpointInfo` 点的字符串 `setDescription` 值来指定端点的描述。
   * 通过调用对象的方法并传递指定 `CreateEndpointInfo` 该名称的 `setName` 字符串值，指定端点的名称。
   * 通过调用对象的方法并传递指定服务名 `CreateEndpointInfo` 的字符串 `setServiceId` 值，指定端点所属的服务。
   * 指定通过调用对象的方法来调 `CreateEndpointInfo` 用的操作， `setOperationName` 并传递一个指定操作名称的字符串值。 对于SOAP和EJB端点，指定通配符( `*`)，表示所有操作。

1. 创建EJB端点。

   通过调用对象的方 `EndpointRegistryClient` 法并传递对 `createEndpoint` 象来创建端 `CreateEndpointInfo` 点。 此方法返回一 `Endpoint` 个表示新EJB端点的对象。

1. 启用端点。

   通过调用对象的启 `EndpointRegistryClient` 用方法并传递由该方 `Endpoint` 法返回的对象来启用端 `createEndpoint` 点。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速入门：使用Java API添加EJB端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-ejb-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 添加SOAP端点 {#adding-soap-endpoints}

您可以使用AEM Forms Java API以编程方式将SOAP端点添加到服务。 通过添加SOAP端点，您使客户端应用程序能够使用SOAP模式调用服务。 即，在设置调用AEM表单所需的连接属性时，您可以选择SOAP模式。

>[!NOTE]
>
>不能使用Web服务添加SOAP端点。

>[!NOTE]
>
>通常，SOAP端点在默认情况下会添加到服务中，但是，SOAP端点可以添加到以编程方式部署的进程中，或者在删除SOAP端点后必须再次添加。

### 步骤摘要 {#summary_of_steps-1}

要向服务添加SOAP端点，请执行以下任务:

1. 包括项目文件。
1. 创建对 `EndpointRegistryClient` 象。
1. 设置SOAP端点属性。
1. 创建SOAP端点。
1. 启用端点。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（在JBoss Application Server上部署AEM Forms时为必需）
* jbossall-client.jar（在JBoss Application Server上部署AEM表单时需要）

创建SOAP端点时需要这些JAR文件。 但是，如果使用SOAP端点调用服务，则需要添加JAR文件。 有关AEM Forms JAR文件的信息，请参 [阅包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建EndpointRegistry客户端对象**

要以编程方式将SOAP端点添加到服务，必须创建一个对 `EndpointRegistryClient` 象。

**设置SOAP端点属性**

要向服务添加SOAP端点，请指定以下值：

* **连接器标识符值**:指定要创建的端点类型。 要创建SOAP端点，请指定 `SOAP`。
* **说明**:指定端点描述。
* **名称**:指定端点名称。
* **服务标识符值**:指定端点所属的服务。
* **操作名称**:指定使用端点调用的操作的名称。 创建SOAP端点时，请指定通配符( `*`)。 但是，如果要指定特定操作而不是调用所有服务操作，则指定操作的名称，而不是使用通配符( `*`)。

**创建SOAP端点**

在设置SOAP端点属性后，可以创建SOAP端点。

**启用端点**

创建新端点后，必须启用它。 启用端点后，可使用它调用服务。 启用端点后，您可以视图在管理控制台中看到它。

**另请参阅**

[使用Java API添加SOAP端点](programmatically-endpoints.md#add-a-soap-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API添加SOAP端点 {#add-a-soap-endpoint-using-the-java-api}

使用Java API向服务添加SOAP端点：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-livecycle-client.jar。

1. 创建EndpointRegistry客户端对象。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `EndpointRegistryClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 设置SOAP端点属性。

   * 使用对 `CreateEndpointInfo` 象的构造函数创建对象。
   * 通过调用对象的方法并传递 `CreateEndpointInfo` 字符串值 `setConnectorId` 来指定连接器标识符值 `SOAP`。
   * 通过调用对象的方法并传递描述端 `CreateEndpointInfo` 点的字符串 `setDescription` 值来指定端点的描述。
   * 通过调用对象的方法并传递指定 `CreateEndpointInfo` 该名称的 `setName` 字符串值，指定端点的名称。
   * 通过调用对象的方法并传递指定服务名 `CreateEndpointInfo` 的字符串 `setServiceId` 值，指定端点所属的服务。
   * 指定通过调用对象的方法并传 `CreateEndpointInfo` 递指定操 `setOperationName` 作名称的字符串值来调用的操作。 对于SOAP和EJB端点，指定通配符( `*`)，表示所有操作。

1. 创建SOAP端点。

   通过调用对象的方 `EndpointRegistryClient` 法并传递对 `createEndpoint` 象来创建端 `CreateEndpointInfo` 点。 此方法返回 `Endpoint` 表示新SOAP端点的对象。

1. 启用端点。

   通过调用对象的启 `EndpointRegistryClient` 用方法启用端点，并传递 `Endpoint` 由该方法返回的对 `createEndpoint` 象。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速入门：使用Java API添加SOAP端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-soap-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 添加监视文件夹端点 {#adding-watched-folder-endpoints}

您可以使用AEM Forms Java API以编程方式将监视文件夹端点添加到服务。 通过添加“监视文件夹”端点，用户可以将文件（如PDF文件）放置到文件夹中。 将文件放在文件夹中后，将调用所配置的服务并处理文件。 服务执行指定操作后，会将修改后的文件保存到指定的输出文件夹中。 已将监视的文件夹配置为以固定速率间隔或cron计划（如每周一、周三和星期五中午）进行扫描。

为了以编程方式向服务添加监视文件夹端点，请考虑以下名为 *EncryptDocument的短时过程*。 (请参 [阅了解AEM Forms流程](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)。)

![aw_aw_encryptdocumentprocess](assets/aw_aw_encryptdocumentprocess.png)

此过程接受一个不安全的PDF文档作为输入值，然后将该不安全的PDF文档传递给加密服务的操 `EncryptPDFUsingPassword` 作。 PDF文档使用密码加密，密码加密的PDF文档是此过程的输出值。 输入值的名称(不安全的PDF文档) `InDoc` 和数据类型为 `com.adobe.idp.Document`。 输出值的名称(密码加密的PDF文档) `SecuredDoc` 和数据类型为 `com.adobe.idp.Document`。

>[!NOTE]
>
>不能使用Web服务添加监视文件夹端点。

### 步骤摘要 {#summary_of_steps-2}

要将监视文件夹端点添加到服务，请执行以下任务:

1. 包括项目文件。
1. 创建对 `EndpointRegistryClient` 象。
1. 设置监视文件夹端点属性。
1. 指定配置值。
1. 定义输入参数值。
1. 定义输出参数值。
1. 创建监视文件夹端点。
1. 启用端点。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（在JBoss Application Server上部署AEM Forms时为必需）
* jbossall-client.jar（在JBoss Application Server上部署AEM表单时需要）

有关这些JAR文件的位置的信息，请参 [阅包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建EndpointRegistry客户端对象**

要以编程方式添加监视文件夹端点，必须创建一个 `EndpointRegistryClient` 对象。

**设置监视文件夹端点属性**

要为服务创建监视文件夹端点，请指定以下值：

* **连接器标识符**:指定所创建的端点的类型。 要创建监视文件夹端点，请指定 `WatchedFolder`。
* **说明**:指定端点的描述。
* **名称**:指定端点的名称。
* **服务标识符**:指定端点所属的服务。 例如，要向本节介绍的进程添加“监视文件夹”端点（当使用Workbench激活某个进程时，该进程将变为服务），请指定 `EncryptDocument`。
* **操作名称**:指定使用端点调用的操作的名称。 通常，在为源自在Workbench中创建的进程的服务创建“监视文件夹”端点时，操作的名称为 `invoke`。

**指定配置值**

在以编程方式将监视文件夹端点添加到服务时，必须为监视文件夹端点指定配置值。 如果通过使用管理控制台添加了监视文件夹端点，则管理员将指定这些配置值。

以下列表指定在以编程方式将监视文件夹端点添加到服务时设置的配置值：

* **url**:指定监视的文件夹位置。 在群集环境中，此值必须指向可从群集中的每台计算机访问的共享网络文件夹。
* **异步**:将调用类型标识为异步或同步。 瞬态和同步进程只能同步调用。 默认值为true。 建议使用异步。
* **cronExpression**:由石英使用以计划输入目录的轮询。 有关配置cron表达式的详细信息，请参 [阅https://quartz.sourceforge.net/javadoc/org/quartz/CronTrigger.html](https://quartz.sourceforge.net/javadoc/org/quartz/CronTrigger.html)。
* **purgeDuration**:这是一个必填属性。 当结果文件夹中的文件和文件夹比此值大时，它们将被清除。 此值以天数计量。 此属性有助于确保结果文件夹未变为完整文件夹。 值为-1天表示从不删除结果文件夹。 默认值是-1。
* **repeatInterval**:扫描“监视的文件夹”进行输入的时间间隔（以秒为单位）。 除非启用限制，否则此值应比处理平均作业的时间长；否则，系统可能会过载。 默认值为 5。
* **repeatCount**:监视文件夹扫描文件夹或目录的次数。 值为-1表示扫描不确定。 默认值是-1。
* **throttleOn**:限制在任意给定时间可处理的“监视文件夹”作业的数量。 作业的最大数量由batchSize值确定。
* **userName**:从监视文件夹调用目标服务时使用的用户名。 此值为必填。 默认值为SuperAdmin。
* **domainName**:用户的域。 此值为必填。 默认值为DefaultDom。
* **batchSize**:每次扫描要选取的文件或文件夹数。 使用此值可防止系统过载；一次扫描过多文件可能会导致崩溃。 默认值为 2。
* **waitTime**:在创建后扫描文件夹或文件之前等待的时间（以毫秒为单位）。 例如，如果等待时间为36,000,000毫秒（1小时），且文件是在一分钟前创建的，则在59分钟或更长时间后会选取此文件。 此属性有助于确保将文件或文件夹完全复制到输入文件夹。 例如，如果要处理一个大文件，而该文件需要10分钟才能下载，请将等待时间设置为10&amp;ast;60 &amp;ast;1000毫秒。 如果监视的文件夹已等待了10分钟，则此设置将阻止其扫描文件。 默认值为 0。
* **excludeFilePattern**:监视文件夹用于确定扫描和拾取哪些文件和文件夹的模式。 不会扫描任何具有此模式的文件或文件夹进行处理。 当输入是包含多个文件的文件夹时，此设置很有用。 可以将文件夹的内容复制到一个名称由监视文件夹选取的文件夹中。 此步骤可防止监视的文件夹在将文件夹完全复制到输入文件夹之前拾取要处理的文件夹。 例如，如果excludeFilePattern值为，则不 `data*`会选取所有匹配的文件 `data*` 和文件夹。 这包括名为、 `data1`等的 `data2`文件和文件夹。 此外，该模式可以用通配符模式来补充以指定文件模式。 监视的文件夹会修改常规表达式以支持通配符模式，如 `*.*` 和 `*.pdf`。 常规表达式不支持这些通配符模式。
* **includeFilePattern**:监视文件夹用于确定扫描和拾取哪些文件夹和文件的模式。 例如，如果此值为，则 `*`会选取所有匹配的文件 `input*` 和文件夹。 这包括名为、 `input1`等的 `input2`文件和文件夹。 默认值为 `*`. 此值指示所有文件和文件夹。 此外，该模式可以用通配符模式来补充以指定文件模式。 监视的文件夹会修改常规表达式以支持通配符模式，如 `*.*` 和 `*.pdf`。 常规表达式不支持这些通配符模式。 此值是必填项。
* **resultFolderName**:保存的结果的存储位置。 此位置可以是绝对路径或相对目录路径。 如果结果未显示在此文件夹中，请检查失败文件夹。 只读文件不会被处理，并将保存在失败文件夹中。 默认值为 `result/%Y/%M/%D/`. 这是监视文件夹内的结果文件夹。
* **preserveFolderName**:成功扫描和拾取文件后存储文件的位置。 此位置可以是绝对路径、相对路径或空目录路径。 默认值为 `preserve/%Y/%M/%D/`.
* **failureFolderName**:保存失败文件的文件夹。 此位置始终与监视的文件夹相关。 只读文件不会被处理，并将保存在失败文件夹中。 默认值为 `failure/%Y/%M/%D/`.
* **preserveOnFailure**:在服务上执行操作失败时保留输入文件。 默认值为true。
* **overwriteDuplicateFilename**:设置为true时，结果文件夹和保留文件夹中的文件将被覆盖。 设置为false时，名称将使用具有数字索引后缀的文件和文件夹。 默认值为false。

**定义输入参数值**

创建监视文件夹端点时，必须定义输入参数值。 即，必须描述传递给被监视文件夹调用的操作的输入值。 例如，请考虑本主题中介绍的过程。 它有一个输入值名 `InDoc` 称，其数据类型为 `com.adobe.idp.Document`。 为此进程创建“监视文件夹”端点时（在激活进程后，它将变为服务），必须定义输入参数值。

要定义监视文件夹端点所需的输入参数值，请指定以下值：

**输入参数名称**:输入参数的名称。 输入值的名称在Workbench中为进程指定。 如果输入值属于服务操作（不是在Workbench中创建的进程的服务），则输入名称在component.xml文件中指定。 例如，本节介绍的进程的输入参数名称为 `InDoc`。

**映射类型**:用于配置调用服务操作所需的输入值。 映射类型有两种：

* `Literal`:“监视文件夹”端点在显示时使用在字段中输入的值。 支持所有基本的Java类型。 例如，如果API使用String、long、int和Boolean等输入，则字符串将转换为正确的类型并调用服务。
* `Variable`:输入的值是被监视的文件夹用来选择输入的文件模式。 例如，如果为映射类型选择“变量”，且输入文档必须是PDF文件，则可以指 `*.pdf`定为映射值。

**映射值**:指定映射类型的值。 例如，如果选择映射类 `Variable` 型，则可以指定 `*.pdf` 为文件模式。

**数据类型**:指定输入值的数据类型。 例如，本节介绍的进程输入值的数据类型是 `com.adobe.idp.Document`。

**定义输出参数值**

创建“监视文件夹”端点时，必须定义一个输出参数值。 即，必须描述由监视文件夹端点调用的服务返回的输出值。 例如，请考虑本主题中介绍的过程。 它有一个名为的输出 `SecuredDoc` 值，其数据类型为 `com.adobe.idp.Document`。 为此进程创建“监视文件夹”端点时（在激活进程后，它将变为服务），必须定义输出参数值。

要定义监视文件夹端点所需的输出参数值，请指定以下值：

**输出参数名称**:输出参数的名称。 进程输出值的名称在Workbench中指定。 如果输出值属于服务操作（不是在Workbench中创建的进程的服务），则输出名称在component.xml文件中指定。 例如，本节介绍的进程的输出参数的名称是 `SecuredDoc`。

**映射类型**:用于配置服务和操作的输出。 以下选项可供选择：

* 如果服务返回单个对象(单个文档)，则模式为， `%F.pdf` 源目标为sourcefilename.pdf。 例如，本节介绍的过程会返回一个文档。 因此，映射类型可定义为( `%F.pdf` 表示使 `%F` 用给定的文件名)。 该模式 `%E` 指定输入文档的扩展。
* 如果服务返回列表，则模式为 `Result\%F\`，源目标为Result\sourcefilename\source1 (output 1)和Result\sourcefilename\source2 (output 2)。
* 如果服务返回映射，则模式为 `Result\%F\`，源目标为Result\sourcefilename\file1 and Result\sourcefilename\file2。 如果映射有多个对象，则模式为 `Result\%F.pdf` ，而源目标为Result\sourcefilename1.pdf(output 1)、Result\sourcefilename2.pdf(output 2)，依此类推。

**数据类型**:指定返回值的数据类型。 例如，本节介绍的进程返回值的数据类型为 `com.adobe.idp.Document`。

**创建监视文件夹端点**

在设置端点的属性、配置值和定义输入和输出参数值后，必须创建“监视文件夹”端点。

**启用端点**

创建“监视文件夹”端点后，必须启用该端点。 启用端点后，可使用它调用服务。 启用端点后，可以在管理控制台中视图它。

**另请参阅**

[使用Java API添加监视文件夹端点](programmatically-endpoints.md#add-a-watched-folder-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API添加监视文件夹端点 {#add-a-watched-folder-endpoint-using-the-java-api}

使用AEM Forms Java API添加监视文件夹端点：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-livecycle-client.jar。

1. 创建EndpointRegistry客户端对象。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `EndpointRegistryClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 设置监视文件夹端点属性。

   * 使用对 `CreateEndpointInfo` 象的构造函数创建对象。
   * 通过调用对象的方法并传递 `CreateEndpointInfo` 字符串值 `setConnectorId` 来指定连接器标识符值 `WatchedFolder`。
   * 通过调用对象的方法并传递描述端 `CreateEndpointInfo` 点的字符串 `setDescription` 值来指定端点的描述。
   * 通过调用对象的方法并传递指定 `CreateEndpointInfo` 该名称的 `setName` 字符串值，指定端点的名称。
   * 通过调用对象的方法并传递指定服务名 `CreateEndpointInfo` 的字符串 `setServiceId` 值，指定端点所属的服务。
   * 指定通过调用对象的方法并传 `CreateEndpointInfo` 递指定操 `setOperationName` 作名称的字符串值来调用的操作。 通常，在为源自在Workbench中创建的进程的服务创建“监视文件夹”端点时，将调用操作的名称。

1. 指定配置值。

   对于要为“监视文件夹”端点设置的每个配置值，必须调 `CreateEndpointInfo` 用对象的方 `setConfigParameterAsText` 法。 例如，要设置配 `url` 置值，请调用对象的 `CreateEndpointInfo` 方法并传 `setConfigParameterAsText` 递以下字符串值：

   * 一个字符串值，它指定配置值的名称。 设置配置 `url` 值时，请指定 `url`。
   * 一个字符串值，它指定配置值的值。 设置配置 `url` 值时，指定监视的文件夹位置。
   >[!NOTE]
   >
   >要查看为EncryptDocument服务设置的所有配置值，请参阅 [QuickStart上的Java代码示例：使用Java API添加监视文件夹端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)。

1. 定义输入参数值。

   通过调用对象的方法来定义输 `CreateEndpointInfo` 入参数值， `setInputParameterMapping` 并传递以下值：

   * 指定输入参数名称的字符串值。 例如，EncryptDocument服务的输入参数的名称为 `InDoc`。
   * 一个字符串值，它指定输入参数的数据类型。 例如，输入参数的数据 `InDoc` 类型是 `com.adobe.idp.Document`。
   * 指定映射类型的字符串值。 For example, you can specify `variable`.
   * 指定映射类型值的字符串值。 例如，可以指定&amp;ast;.pdf作为文件模式。
   >[!NOTE]
   >
   >调用每 `setInputParameterMapping` 个输入参数值的方法进行定义。 由于EncryptDocument进程只有一个输入参数，因此您需要调用此方法一次。

1. 定义输出参数值。

   通过调用对象的方法来定义输 `CreateEndpointInfo` 出参数值， `setOutputParameterMapping` 并传递以下值：

   * 一个字符串值，它指定输出参数的名称。 例如，EncryptDocument服务的输出参数的名称为 `SecuredDoc`。
   * 一个字符串值，它指定输出参数的数据类型。 例如，输出参数的数据 `SecuredDoc` 类型是 `com.adobe.idp.Document`。
   * 指定映射类型的字符串值。 For example, you can specify `%F.pdf`.

1. 创建监视文件夹端点。

   通过调用对象的方 `EndpointRegistryClient` 法并传递对 `createEndpoint` 象来创建端 `CreateEndpointInfo` 点。 此方法返回一个 `Endpoint` 表示“监视文件夹”端点的对象。

1. 启用端点。

   通过调用对象的方 `EndpointRegistryClient` 法并传递 `enable` 该方法返 `Endpoint` 回的对象来启用端 `createEndpoint` 点。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速入门：使用Java API添加监视文件夹端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 监视文件夹配置值常数文件 {#watched-folder-configuration-values-constant-file}

快速 [入门：使用Java API添加监视文件夹端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api) ，会使用一个常量文件，该常量文件必须是Java项目的一部分，才能编译快速开始。 此常量文件表示添加“监视文件夹”端点时必须设置的配置值。 以下Java代码表示常量文件。

```as3
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

您可以使用AEM Forms Java API以编程方式将电子邮件端点添加到服务。 通过添加电子邮件端点，用户可以向指定的电子邮件帐户发送包含一个或多个文件附件的电子邮件。 然后调用配置服务操作并处理文件。 服务执行指定操作后，会向发送方发送一封电子邮件，其中已修改的文件作为文件附件。

为了以编程方式向服务添加电子邮件端点，请考虑以下名为MyApplication\EncryptDocument的短时 *间进程*。 有关短时间流程的信息，请参阅了 [解AEM表单流程](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)。

![ae_ae_encryptdocumentprocess](assets/ae_ae_encryptdocumentprocess.png)

此过程接受一个不安全的PDF文档作为输入值，然后将该不安全的PDF文档传递给加密服务的操 `EncryptPDFUsingPassword` 作。 此过程使用密码加密PDF文档，并返回密码加密的PDF文档作为输出值。 输入值的名称(不安全的PDF文档) `InDoc` 和数据类型为 `com.adobe.idp.Document`。 输出值的名称(密码加密的PDF文档) `SecuredDoc` 和数据类型为 `com.adobe.idp.Document`。

>[!NOTE]
>
>不能使用Web服务添加电子邮件端点。

### 步骤摘要 {#summary_of_steps-3}

要向服务添加电子邮件端点，请执行以下任务:

1. 包括项目文件。
1. 创建对 `EndpointRegistryClient` 象。
1. 设置电子邮件端点属性。
1. 指定配置值。
1. 定义输入参数值。
1. 定义输出参数值。
1. 创建电子邮件端点。
1. 启用端点。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（在JBoss Application Server上部署AEM Forms时为必需）
* jbossall-client.jar（在JBoss Application Server上部署AEM表单时需要）

有关这些JAR文件的位置的信息，请参 [阅包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建EndpointRegistry客户端对象**

在以编程方式添加电子邮件端点之前，必须先创建一个 `EndpointRegistryClient` 对象。

**设置电子邮件端点属性**

要为服务创建电子邮件端点，请指定以下值：

* **连接器标识符值**:指定所创建的端点的类型。 要创建电子邮件端点，请指定 `Email`。
* **说明**:指定端点的描述。
* **名称**:指定端点的名称。
* **服务标识符值**:指定端点所属的服务。 例如，要向本节中引入的进程添加电子邮件端点（当使用Workbench激活某个进程时，该进程将变为服务），请指定 `EncryptDocument`。
* **操作名称**:指定使用端点调用的操作的名称。 通常，在为源自在Workbench中创建的进程的服务创建电子邮件端点时，操作的名称为 `invoke`。

**指定配置值**

在以编程方式将电子邮件端点添加到服务时，必须为电子邮件端点指定配置值。 如果使用管理控制台添加了电子邮件端点，则管理员会指定这些配置值。

>[!NOTE]
>
>受监视的电子邮件帐户是仅用于电子邮件端点的特殊帐户。 此帐户不是普通用户的电子邮件帐户。 不能将常规用户的电子邮件帐户配置为电子邮件提供者使用的帐户，因为电子邮件提供者在邮件完成后会从收件箱中删除电子邮件。

以编程方式将电子邮件端点添加到服务时，将设置以下配置值：

* **cronExpression**:如果必须使用cron表达式来计划电子邮件，则为cron表达式。
* **repeatCount**:电子邮件端点扫描文件夹或目录的次数。 值为-1表示扫描不确定。 默认值是-1。
* **repeatInterval**:接收方用于检查传入邮件的扫描速率（以秒为单位）。 默认值为 10。
* **startDelay**:在调度程序开始后等待扫描的时间。 默认时间为0。
* **batchSize**:接收方每次扫描处理的电子邮件数量，以获得最佳性能。 值-1表示所有电子邮件。 默认值为 2。
* **userName**:从电子邮件调用目标服务时使用的用户名。 默认值为 `SuperAdmin`.
* **domainName**:强制配置值。 默认值为 `DefaultDom`.
* **domainPattern**:指定提供者接受的传入电子邮件的域模式。 例如，如果使 `adobe.com` 用，则只会处理adobe.com的电子邮件，而忽略来自其他域的电子邮件。
* **filePattern**:指定提供者接受的传入文件附件模式。 这包括具有特定文件扩展名(&amp;ast;.dat,&amp;ast;.xml)的文件，具有特定名称（数据）的文件，以及具有以名称和扩展名(&amp;ast;)表示的复合表达式的文件。[dD][aA]&#39;port&#39;)。 默认值为 `*`.
* **recipientSuccessfulJob**:发送消息以指示作业成功的电子邮件地址。 默认情况下，成功的作业消息始终会发送给发送者。 如果您键入 `sender`内容，则电子邮件结果将发送给发送方。 最多支持100个收件人。 指定其他电子邮件地址收件人，每个电子邮件地址以逗号分隔。 要关闭此选项，请将此值留空。 在某些情况下，您可能希望触发进程，而不希望收到结果的电子邮件通知。 默认值为 `sender`.
* **recipientFailedJob**:发送用于指示失败作业的消息的电子邮件地址。 默认情况下，失败的作业消息始终发送给发送者。 如果您键入 `sender`内容，则电子邮件结果将发送给发送方。 最多支持100个收件人。 指定其他电子邮件地址收件人，每个电子邮件地址以逗号分隔。 要关闭此选项，请将此值留空。 默认值为 `sender`.
* **inboxHost**:要扫描的电子邮件提供者的收件箱主机名或IP地址。
* **inboxPort**:电子邮件服务器使用的端口。 POP3的默认值为110,IMAP的默认值为143。 如果启用了SSL，则POP3的默认值为995,IMAP的默认值为993。
* **inboxProtocol**:用于扫描收件箱的电子邮件端点的电子邮件协议。 选项为 `IMAP` 或 `POP3`。 收件箱主机邮件服务器必须支持这些协议。
* **inboxTimeOut**:电子邮件提供商等待收件箱响应的超时时间（以秒为单位）。 默认值为 60。
* **inboxUser**:登录电子邮件帐户所需的用户名。 根据电子邮件服务器和配置的不同，这可能只是电子邮件的用户名部分，也可能是完整的电子邮件地址。
* **inboxPassword**:收件箱用户的密码。
* **inboxSSLEnabled**:设置此值后，电子邮件提供者在发送结果或错误的通知消息时必须使用SSL。 确保IMAP或POP3主机支持SSL。
* **smtp主机**:电子邮件提供者向其发送结果和错误消息的邮件服务器的主机名。
* **smtp端口**:SMTP端口的默认值为25。
* **smtp用户**:电子邮件提供者在发送结果和错误的电子邮件通知时使用的用户帐户。
* **smtp密码**:SMTP帐户的口令。 某些邮件服务器不需要SMTP密码。
* **charSet**:电子邮件提供者使用的字符集。 默认值为 `UTF-8`.
* **smtpSSLEnabled**:设置此值后，电子邮件提供者在发送结果或错误的通知消息时必须使用SSL。 确保SMTP主机支持SSL。
* **failedJobFolder**:指定在SMTP邮件服务器不工作时存储结果的目录。
* **异步**:设置为同步时，将处理所有输入文档并返回单个响应。 当设置为异步时，将为处理的每个输入文档发送响应。 例如，会为本主题中引入的过程创建电子邮件端点，并向端点的收件箱发送电子邮件，该收件箱中包含多个不安全的PDF文档。 当所有PDF文档都使用密码加密，并且如果端点配置为同步，则会发送一封单一响应电子邮件，并附上所有受保护的PDF文档。 如果端点配置为异步，则为每个受保护的PDF文档发送单独的响应电子邮件。 每封电子邮件都包含一个PDF文档作为附件。 默认值为异步。

**定义输入参数值**

创建电子邮件端点时，必须定义输入参数值。 即，必须描述传递给电子邮件端点调用的操作的输入值。 例如，请考虑本主题中介绍的过程。 它有一个输入值名 `InDoc` 称，其数据类型为 `com.adobe.idp.Document`。 为此进程创建电子邮件端点时（在激活进程后，该进程将变为服务），必须定义输入参数值。

要定义电子邮件端点所需的输入参数值，请指定以下值：

**输入参数名称**:输入参数的名称。 输入值的名称在Workbench中为进程指定。 如果输入值属于服务操作（不是在Workbench中创建的进程的Forms服务），则输入名称在component.xml文件中指定。 例如，本节介绍的进程的输入参数名称为 `InDoc`。

**映射类型**:用于配置调用服务操作所需的输入值。 映射类型有两种：

* `Literal`:电子邮件端点使用在显示时在字段中输入的值。 支持所有基本的Java类型。 例如，如果API使用String、long、int和Boolean等输入，则字符串将转换为正确的类型并调用服务。
* `Variable`:输入的值是电子邮件端点用来选取输入的文件模式。 例如，如果为映射类型选择“变量”，且输入文档必须是PDF文件，则可以指 `*.pdf` 定为映射值。

**映射值**:指定映射类型的值。 例如，如果选择“变量”映射类型，则可以将 `*.pdf` 其指定为文件模式。

**数据类型**:指定输入值的数据类型。 例如，本节介绍的进程输入值的数据类型为com.adobe.idp.文档。

**定义输出参数值**

创建电子邮件端点时，必须定义输出参数值。 即，必须描述由电子邮件端点调用的服务返回的输出值。 例如，请考虑本主题中介绍的过程。 它有一个名为的输出 `SecuredDoc` 值，其数据类型为 `com.adobe.idp.Document`。 为此进程创建电子邮件端点时（在激活进程后，该进程将变为服务），必须定义输出参数值。

要定义电子邮件端点所需的输出参数值，请指定以下值：

**输出参数名称**:输出参数的名称。 进程输出值的名称在Workbench中指定。 如果输出值属于服务操作（不是在Workbench中创建的进程的服务），则输出名称在component.xml文件中指定。 例如，本节介绍的进程的输出参数的名称是 `SecuredDoc`。

**映射类型**:用于配置服务和操作的输出。 以下选项可供选择：

* 如果服务返回单个对象(单个文档)，则模式为， `%F.pdf` 源目标为sourcefilename.pdf。 例如，本节介绍的过程会返回一个文档。 因此，映射类型可定义为( `%F.pdf` 表示使 `%F` 用给定的文件名)。 该模式 `%E` 指定输入文档的扩展。
* 如果服务返回列表，则模式为 `Result\%F\`，源目标为Result\sourcefilename\source1 (output 1)和Result\sourcefilename\source2 (output 2)。
* 如果服务返回映射，则模式为 `Result\%F\`，源目标为Result\sourcefilename\file1 and Result\sourcefilename\file2。 如果映射有多个对象，则模式为 `Result\%F.pdf` ，而源目标为Result\sourcefilename1.pdf(output 1)、Result\sourcefilename2.pdf(output 2)，依此类推。

**数据类型**:指定返回值的数据类型。 例如，本节介绍的进程返回值的数据类型为 `com.adobe.idp.Document`。

**创建电子邮件端点**

在设置电子邮件端点属性和配置值并定义输入和输出参数值后，必须创建电子邮件端点。

**启用端点**

创建电子邮件端点后，必须启用它。 启用端点后，可使用它调用服务。 启用端点后，可以在管理控制台中视图它。

**另请参阅**

[使用Java API添加电子邮件端点](programmatically-endpoints.md#add-an-email-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API添加电子邮件端点 {#add-an-email-endpoint-using-the-java-api}

使用Java API添加电子邮件端点：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-livecycle-client.jar。

1. 创建EndpointRegistry客户端对象。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `EndpointRegistryClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 设置电子邮件端点属性。

   * 使用对 `CreateEndpointInfo` 象的构造函数创建对象。
   * 通过调用对象的方法并传递 `CreateEndpointInfo` 字符串值 `setConnectorId` 来指定连接器标识符值 `Email`。
   * 通过调用对象的方法并传递描述端 `CreateEndpointInfo` 点的字符串 `setDescription` 值来指定端点的描述。
   * 通过调用对象的方法并传递指定 `CreateEndpointInfo` 该名称的 `setName` 字符串值，指定端点的名称。
   * 通过调用对象的方法并传递指定服务名 `CreateEndpointInfo` 的字符串 `setServiceId` 值，指定端点所属的服务。
   * 指定通过调用对象的方法并传 `CreateEndpointInfo` 递指定操 `setOperationName` 作名称的字符串值来调用的操作。 通常，在为源自在Workbench中创建的进程的服务创建电子邮件端点时，将调用操作的名称。

1. 指定配置值。

   对于要为电子邮件端点设置的每个配置值，必须调 `CreateEndpointInfo` 用对象的方 `setConfigParameterAsText` 法。 例如，要设置配 `smtpHost` 置值，请调用对象的 `CreateEndpointInfo` 方法并传 `setConfigParameterAsText` 递以下值：

   * 一个字符串值，它指定配置值的名称。 设置配置 `smtpHost` 值时，请指定 `smtpHost`。
   * 一个字符串值，它指定配置值的值。 设置配 `smtpHost` 置值时，请指定指定SMTP服务器名称的字符串值。
   >[!NOTE]
   >
   >要查看本节中介绍的为EncryptDocument服务设置的所有配置值，请参阅 [QuickStart上的Java代码示例：使用Java API添加电子邮件端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api)。

1. 定义输入参数值。

   通过调用对象的方法来定义输 `CreateEndpointInfo` 入参数值， `setInputParameterMapping` 并传递以下值：

   * 指定输入参数名称的字符串值。 例如，EncryptDocument服务的输入参数的名称为 `InDoc`。
   * 一个字符串值，它指定输入参数的数据类型。 例如，输入参数的数据 `InDoc` 类型是 `com.adobe.idp.Document`。
   * 指定映射类型的字符串值。 For example, you can specify `variable`.
   * 指定映射类型值的字符串值。 例如，可以指定&amp;ast;.pdf作为文件模式。
   >[!NOTE]
   >
   >调用每 `setInputParameterMapping` 个输入参数值的方法进行定义。 由于EncryptDocument进程只有一个输入参数，因此您需要调用此方法一次。

1. 定义输出参数值。

   通过调用对象的方法并传递 `CreateEndpointInfo` 以下值来 `setOutputParameterMapping` 定义输出参数值：

   * 一个字符串值，它指定输出参数的名称。 例如，EncryptDocument服务的输出参数的名称为 `SecuredDoc`。
   * 一个字符串值，它指定输出参数的数据类型。 例如，输出参数的数据 `SecuredDoc` 类型是 `com.adobe.idp.Document`。
   * 指定映射类型的字符串值。 For example, you can specify `%F.pdf`.

1. 创建电子邮件端点。

   通过调用对象的方 `EndpointRegistryClient` 法并传递对 `createEndpoint` 象来创建端 `CreateEndpointInfo` 点。 此方法返回一个 `Endpoint` 表示电子邮件端点的对象。

1. 启用端点。

   通过调用对象的方 `EndpointRegistryClient` 法并传递 `enable` 该方法返 `Endpoint` 回的对象来启用端 `createEndpoint` 点。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速入门：使用Java API添加监视文件夹端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 电子邮件配置值常数文件 {#email-configuration-values-constant-file}

快速 [入门：使用Java API添加电子邮件端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api) ，会使用一个常量文件，该常量文件必须是Java项目的一部分，才能编译快速开始。 此常量文件表示添加电子邮件端点时必须设置的配置值。 以下Java代码表示常量文件。

```as3
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

## 添加远程处理端点 {#adding-remoting-endpoints}

>[!NOTE]
>
>已为JEE上的AEM表单弃用的LiveCycle Remoting API。

您可以使用AEM Forms Java API以编程方式将远程处理端点添加到服务。 通过添加远程处理端点，您使Flex应用程序能够通过使用远程处理调用服务。 (请参 [阅使用（AEM表单已弃用）调用AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)。)

为了以编程方式向服务添加远程处理端点，请考虑以下名为 *EncryptDocument的短时过程*。

![ar_ar_encryptdocumentprocess](assets/ar_ar_encryptdocumentprocess.png)

此过程接受一个不安全的PDF文档作为输入值，然后将该不安全的PDF文档传递给加密服务的操 `EncryptPDFUsingPassword` 作。 PDF文档使用密码加密，密码加密的PDF文档是此过程的输出值。 输入值的名称(不安全的PDF文档) `InDoc` 和数据类型为 `com.adobe.idp.Document`。 输出值的名称(密码加密的PDF文档) `SecuredDoc` 和数据类型为 `com.adobe.idp.Document`。

要演示如何向服务添加远程处理端点，本节将一个远程处理端点添加到名为EncryptDocument的服务。

>[!NOTE]
>
>不能使用Web服务添加远程处理端点。

### 步骤摘要 {#summary_of_steps-4}

要从服务中删除端点，请执行以下任务:

1. 包括项目文件。
1. 创建对 `EndpointRegistryClient` 象。
1. 设置远程处理端点属性。
1. 创建远程处理端点。
1. 启用端点。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（在JBoss Application Server上部署AEM Forms时为必需）
* jbossall-client.jar（在JBoss Application Server上部署AEM表单时需要）

有关这些JAR文件的位置的信息，请参 [阅包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建EndpointRegistry客户端对象**

要以编程方式添加远程处理端点，必须创建一个 `EndpointRegistryClient` 对象。

**设置远程处理端点属性**

要为服务创建远程处理端点，请指定以下值：

* **连接器标识符值**:指定所创建的端点的类型。 要创建远程处理端点，请指定 `Remoting`。
* **说明**:指定端点的描述。
* **名称**:指定端点的名称。
* **服务标识符值**:指定端点所属的服务。 例如，要向本节中引入的进程添加远程处理端点（当在Workbench中激活进程时，该进程将变为服务），请指定 `EncryptDocument`。
* **操作名称**:指定使用端点调用的操作的名称。 创建远程处理端点时，请指定通配符(&amp;ast;)。

**创建远程处理端点**

在设置“远程处理”端点属性后，可以为服务创建远程处理端点。

**启用端点**

创建新端点后，必须启用它。 启用远程处理端点后，它使Flex客户端能够调用该服务。

**另请参阅**

[使用Java API添加远程处理端点](programmatically-endpoints.md#add-a-remoting-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API添加远程处理端点 {#add-a-remoting-endpoint-using-the-java-api}

使用Java API添加远程处理端点：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-livecycle-client.jar。

1. 创建EndpointRegistry客户端对象。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `EndpointRegistryClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 设置远程处理端点属性。

   * 使用对 `CreateEndpointInfo` 象的构造函数创建对象。
   * 通过调用对象的方法并传递 `CreateEndpointInfo` 字符串值 `setConnectorId` 来指定连接器标识符值 `Remoting`。
   * 通过调用对象的方法并传递描述端 `CreateEndpointInfo` 点的字符串 `setDescription` 值来指定端点的描述。
   * 通过调用对象的方法并传递指定 `CreateEndpointInfo` 该名称的 `setName` 字符串值，指定端点的名称。
   * 通过调用对象的方法并传递指定服务名 `CreateEndpointInfo` 的字符串 `setServiceId` 值，指定端点所属的服务。
   * 指定对象方法调用的操 `CreateEndpointInfo` 作，并传 `setOperationName` 递指定操作名称的字符串值。 对于远程处理端点，指定通配符(&amp;ast;)。

1. 创建远程处理端点。

   通过调用对象的方 `EndpointRegistryClient` 法并传递对 `createEndpoint` 象来创建端 `CreateEndpointInfo` 点。 此方法返回一 `Endpoint` 个表示新远程处理端点的对象。

1. 启用端点。

   通过调用对象的方 `EndpointRegistryClient` 法并传递 `enable` 该方法返 `Endpoint` 回的对象来启用端 `createEndpoint` 点。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速入门：使用Java API添加远程处理端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-remoting-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 添加TaskManager端点 {#adding-taskmanager-endpoints}

您可以使用AEM Forms Java API以编程方式将TaskManager端点添加到服务。 通过向服务添加TaskManager端点，可使Workspace用户调用该服务。 即，在Workspace中工作的用户可以调用具有相应TaskManager端点的进程。

>[!NOTE]
>
>不能使用Web服务添加TaskManager端点。

### 步骤摘要 {#summary_of_steps-5}

要向服务添加TaskManager端点，请执行以下任务:

1. 包括项目文件。
1. 创建对 `EndpointRegistryClient` 象。
1. 为端点创建类别。
1. 设置TaskManager端点属性。
1. 创建TaskManager端点。
1. 启用端点。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（在JBoss Application Server上部署AEM Forms时为必需）
* jbossall-client.jar（在JBoss Application Server上部署AEM表单时需要）

有关这些JAR文件的位置的信息，请参 [阅包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建EndpointRegistry客户端对象**

在以编程方式添加TaskManager端点之前，必须先创建一个对 `EndpointRegistryClient` 象。

**为端点创建类别**

类别用于在Workspace中组织服务。 即，工作区用户可以通过在工作区中选择类别来调用具有TaskManager端点的服务。 创建TaskManager端点时，可以引用现有类别或以编程方式创建新类别。

>[!NOTE]
>
>此部分将创建新类别，作为向服务添加TaskManager端点的一部分。

**设置TaskManager端点属性**

要为服务创建TaskManager端点，请指定以下值：

* **连接器标识符**:指定所创建的端点的类型。 要创建TaskManager端点，请指定 `TaskManagerConnector`。
* **说明**:指定端点的描述。
* **名称**:指定端点的名称。
* **服务标识符**:指定端点所属的服务。
* **类别**:指定与TaskManager端点关联的类别标识符值。
* **操作名称**:通常，在为源自在Workbench中创建的进程的服务创建TaskManager端点时，操作的名称为 `invoke`。

**创建TaskManager端点**

在设置TaskManager端点属性后，可以为服务创建TaskManager端点。

**启用端点**

创建新端点后，必须启用它。 启用端点后，可以使用它从工作区中调用服务。 启用端点后，可以在管理控制台中视图它。

**另请参阅**

[使用Java API添加TaskManager端点](programmatically-endpoints.md#add-a-taskmanager-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API添加TaskManager端点 {#add-a-taskmanager-endpoint-using-the-java-api}

使用Java API添加TaskManager端点：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-livecycle-client.jar。

1. 创建EndpointRegistry客户端对象。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `EndpointRegistryClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 为端点创建类别。

   * 使用对 `CreateEndpointCategoryInfo` 象的构造函数并传递以下值来创建对象：

      * 一个字符串值，它指定类别的标识符值
      * 一个字符串值，它指定类别的说明
   * 通过调用对象的方 `EndpointRegistryClient` 法并传递对 `createEndpointCategory` 象来创建 `CreateEndpointCategoryInfo` 类别。 此方法返回 `EndpointCategory` 表示新类别的对象。


1. 设置TaskManager端点属性。

   * 使用对 `CreateEndpointInfo` 象的构造函数创建对象。
   * 通过调用对象的方法并传递 `CreateEndpointInfo` 字符串值 `setConnectorId` 来指定连接器标识符值 `TaskManagerConnector`。
   * 通过调用对象的方法并传递描述端 `CreateEndpointInfo` 点的字符串 `setDescription` 值来指定端点的描述。
   * 通过调用对象的方法并传递指定 `CreateEndpointInfo` 该名称的 `setName` 字符串值，指定端点的名称。
   * 通过调用对象的方法并传递指定服务名 `CreateEndpointInfo` 的字符串 `setServiceId` 值，指定端点所属的服务。
   * 通过调用对象的方法并传递指定类别标识符值的字符串值， `CreateEndpointInfo` 指 `setCategoryId` 定端点所属的类别。 可以调用对 `EndpointCategory` 象的方 `getId` 法来获取此类别的标识符值。
   * 指定通过调用对象的方法并传 `CreateEndpointInfo` 递指定操 `setOperationName` 作名称的字符串值来调用的操作。 通常，在为源自 `TaskManager` 在Workbench中创建的进程的服务创建端点时，操作的名称为 `invoke`。

1. 创建TaskManager端点。

   通过调用对象的方 `EndpointRegistryClient` 法并传递对 `createEndpoint` 象来创建端 `CreateEndpointInfo` 点。 此方法返回一 `Endpoint` 个表示新TaskManager端点的对象。

1. 启用端点。

   通过调用对象的方 `EndpointRegistryClient` 法并传递 `enable` 该方法返 `Endpoint` 回的对象来启用端 `createEndpoint` 点。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速入门：使用Java API添加TaskManager端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-taskmanager-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 修改端点 {#modifying-endpoints}

您可以使用AEM Forms Java API以编程方式修改现有端点。 通过修改端点，可以更改端点的行为。 例如，考虑一个“监视文件夹”端点，它指定一个用作监视文件夹的文件夹。 您可以通过编程方式修改属于“监视文件夹”端点的配置值，从而使另一个文件夹能够充当监视文件夹。 有关属于监视文件夹端点的配置值的信息，请参阅添 [加监视文件夹端点](programmatically-endpoints.md#adding-watched-folder-endpoints)。

要演示如何修改端点，本节将通过更改与监视文件夹一样的文件夹来修改监视文件夹端点。

>[!NOTE]
>
>不能使用Web服务修改端点。

### 步骤摘要 {#summary_of_steps-6}

要修改端点，请执行以下任务:

1. 包括项目文件。
1. 创建对 `EndpointRegistryClient` 象。
1. 检索端点。
1. 指定新配置值。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（在JBoss Application Server上部署AEM Forms时为必需）
* jbossall-client.jar（在JBoss Application Server上部署AEM表单时需要）

有关这些JAR文件的位置的信息，请参 [阅包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建EndpointRegistry客户端对象**

要以编程方式修改端点，必须创建对 `EndpointRegistryClient` 象。

**检索要修改的端点**

在修改端点之前，必须先检索它。 要检索端点，您必须以可访问端点的用户身份进行连接。 建议您以管理员身份进行连接。 (请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties))。

可以通过检索端点的列表来检索端点。 然后，您可以遍历列表，搜索要删除的特定端点。 例如，可以通过确定与端点对应的服务以及端点的类型来定位端点。 在找到端点时，可以修改它。

**指定新配置值**

修改端点时，请指定新的配置值。 例如，要修改监视文件夹端点，请重置所有监视文件夹端点配置值，而不仅仅是要修改的值。 有关属于监视文件夹端点的配置值的信息，请参阅添 [加监视文件夹端点](programmatically-endpoints.md#adding-watched-folder-endpoints)。

>[!NOTE]
>
>有关属于电子邮件端点的配置值的信息，请参阅添 [加电子邮件端点](programmatically-endpoints.md#adding-email-endpoints)。

>[!NOTE]
>
>不能修改端点调用的服务。 如果尝试修改服务，则会引发异常。 要修改与给定端点关联的服务，请删除该端点并创建新端点。 (请参阅 [删除端点](programmatically-endpoints.md#removing-endpoints)。)

**另请参阅**

[使用Java API修改端点](programmatically-endpoints.md#modifying-an-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API修改端点 {#modifying-an-endpoint-using-the-java-api}

使用Java API修改端点：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-livecycle-client.jar。

1. 创建EndpointRegistry客户端对象。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `EndpointRegistryClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 检索要修改的端点。

   * 检索当前用户（在连接属性中指定）可访问的所有端点的列表，方法是调用对象的方法并传递一个用作 `EndpointRegistryClient` 过滤 `getEndpoints` 器的 `PagingFilter` 对象。 您可以传递一 `(PagingFilter)null` 个值以返回所有端点。 此方法返回一个对 `java.util.List` 象，其中每个元素都是一个 `Endpoint` 对象。 有关对象的信 `PagingFilter` 息，请参 [阅AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 遍历对 `java.util.List` 象以确定它是否具有端点。 如果存在端点，则每个元素都是一个 `EndPoint` 实例。
   * 通过调用对象的方法确定与端点对 `EndPoint` 应的服 `getServiceId` 务。 此方法返回指定服务名的字符串值。
   * 通过调用对象的方法确 `EndPoint` 定端点的类 `getConnectorId` 型。 此方法返回一个指定端点类型的字符串值。 例如，如果端点是“监视文件夹”端点，则此方法返回 `WatchedFolder`。

1. 指定新配置值。

   * 通过调 `ModifyEndpointInfo` 用对象的构造函数创建对象。
   * 对于要设置的每个配置值，调用 `ModifyEndpointInfo` 对象的方 `setConfigParameterAsText` 法。 例如，要设置url配置值，请调用对象 `ModifyEndpointInfo` 的方法并 `setConfigParameterAsText` 传递以下值：

      * 一个字符串值，它指定配置值的名称。 例如，要设置配 `url` 置值，请指定 `url`。
      * 一个字符串值，它指定配置值的值。 要为配置值定义一个 `url` 值，请指定监视的文件夹位置。
   * 调用对 `EndpointRegistryClient` 象的方 `modifyEndpoint` 法并传递对 `ModifyEndpointInfo` 象。


**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速入门：使用Java API修改端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-modifying-an-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 删除端点 {#removing-endpoints}

您可以使用AEM Forms Java API从服务中以编程方式删除端点。 删除端点后，无法使用启用端点的调用方法调用服务。 例如，如果从服务中删除SOAP端点，则无法使用SOAP模式调用该服务。

要演示如何从服务中删除端点，本节将从名为 *EncryptDocument的服务中删除EJB端点*。

>[!NOTE]
>
>不能使用Web服务删除端点。

### 步骤摘要 {#summary_of_steps-7}

要从服务中删除端点，请执行以下任务:

1. 包括项目文件。
1. 创建对 `EndpointRegistryClient` 象。
1. 检索端点。
1. 删除端点。

**包括项目文件**

将必要的文件包含到开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（在JBoss Application Server上部署AEM Forms时为必需）
* jbossall-client.jar（在JBoss Application Server上部署AEM表单时需要）

有关这些JAR文件的位置的信息，请参 [阅包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建EndpointRegistry客户端对象**

要以编程方式删除端点，必须创建一个 `EndpointRegistryClient` 对象。

**检索要删除的端点**

在删除端点之前，必须先检索它。 要检索端点，您必须以可访问端点的用户身份进行连接。 建议您以管理员身份进行连接。 (请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties))。

可以通过检索端点的列表来检索端点。 然后，您可以遍历列表，搜索要删除的特定端点。 例如，可以通过确定与端点对应的服务以及端点的类型来定位端点。 在找到端点后，可以删除它。

**删除端点**

创建新端点后，必须启用它。 启用端点后，可使用它调用服务。 启用端点后，可以在管理控制台中视图它。

**另请参阅**

[使用Java API删除端点](programmatically-endpoints.md#removing-an-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API删除端点 {#removing-an-endpoint-using-the-java-api}

使用Java API删除端点：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-livecycle-client.jar。

1. 创建EndpointRegistry客户端对象。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `EndpointRegistryClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 检索要删除的端点。

   * 通过调用对象的方法并传递用作过滤器的对象，检索当前用户（在连接属性中指定）有权访问的所 `EndpointRegistryClient` 有端 `getEndpoints` 点的列表 `PagingFilter` 。 您可以传递 `(PagingFilter)null` 以返回所有端点。 此方法返回一个对 `java.util.List` 象，其中每个元素都是一个 `Endpoint` 对象。
   * 遍历对 `java.util.List` 象以确定它是否具有端点。 如果存在端点，则每个元素都是一个 `EndPoint` 实例。
   * 通过调用对象的方法确定与端点对 `EndPoint` 应的服 `getServiceId` 务。 此方法返回指定服务名的字符串值。
   * 通过调用对象的方法确 `EndPoint` 定端点的类 `getConnectorId` 型。 此方法返回一个指定端点类型的字符串值。 例如，如果endpoint是EJB端点，则此方法返回 `EJB`。

1. 删除端点。

   通过调用对象的方 `EndpointRegistryClient` 法并传递表示要 `remove` 删除的端 `EndPoint` 点的对象来删除端点。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速入门：使用Java API删除端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-removing-an-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 检索端点连接器信息 {#retrieving-endpoint-connector-information}

您可以使用AEM Forms API以编程方式检索有关端点连接器的信息。 连接器使端点能够使用各种调用方法调用服务。 例如，监视文件夹连接器使端点能够使用监视文件夹调用服务。 通过以编程方式检索有关端点连接器的信息，您可以检索与连接器相关联的配置值，例如需要哪些配置值以及哪些配置值是可选的。

要演示如何检索有关端点连接器的信息，本节将检索有关“监视文件夹”连接器的信息。 (请参阅 [添加监视文件夹端点](programmatically-endpoints.md#adding-watched-folder-endpoints)。)

>[!NOTE]
>
>不能通过使用Web服务检索有关端点的信息。

>[!NOTE]
>
>本主题使用 `ConnectorRegistryClient` API检索有关端点连接器的信息。 (请参 [阅AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。)

### 步骤摘要 {#summary_of_steps-8}

要检索端点连接器信息，请执行以下任务:

1. 包括项目文件。
1. 创建对 `ConnectorRegistryClient` 象。
1. 指定连接器类型。
1. 检索配置值。

**包括项目文件**

将必要的文件包含到开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（在JBoss Application Server上部署AEM Forms时为必需）
* jbossall-client.jar（在JBoss Application Server上部署AEM表单时需要）

如果AEM Forms部署在非JBoss的受支持J2EE应用程序服务器上，则将adobe-utilities.jar和jbossall-client.jar替换为特定于部署了AEM Forms的J2EE应用程序服务器的JAR文件。 有关所有AEM Forms JAR文件的位置的信息，请参 [阅包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建ConnectorRegistry客户端对象**

要以编程方式检索端点连接器信息，请创建一个 `ConnectorRegistryClient` 对象。

**指定连接器类型**

指定要从中检索信息的连接器类型。 存在以下类型的连接器：

* **EJB**:使客户端应用程序能够使用EJB模式调用服务。
* **SOAP**:使客户端应用程序能够使用SOAP模式调用服务。
* **监视文件夹**:启用监视文件夹以调用服务。
* **电子邮件**:使电子邮件能够调用服务。
* **远程处理**:使Flex客户端应用程序能够调用服务。
* **TaskManagerConnector**:使工作区用户能够从工作区内调用服务。

**检索配置值**

指定连接器类型后，可检索有关连接器的信息，如支持的配置值。 例如，对于任何连接器，您可以确定需要哪些配置值以及哪些配置值是可选的。

**另请参阅**

[使用Java API检索端点连接器信息](programmatically-endpoints.md#retrieve-endpoint-connector-information-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API检索端点连接器信息 {#retrieve-endpoint-connector-information-using-the-java-api}

使用Java API检索端点连接器信息：

1. 包括项目文件。.

   在Java项目的类路径中包含客户端JAR文件，如adobe-livecycle-client.jar。

1. 创建ConnectorRegistry客户端对象。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `ConnectorRegistryClient` 象的构造函数并传递该对象来创建 `ServiceClientFactory` 对象。

1. 指定连接器类型。

   通过调用对象的方法并传 `ConnectorRegistryClient` 递指定连接 `getEndpointDefinition` 器类型的字符串值来指定连接器类型。 例如，要指定“监视文件夹”连接器类型，请传递字符串值 `WatchedFolder`。 此方法返回与 `Endpoint` 连接器类型对应的对象。

1. 检索配置值。

   * 通过调用对象的方法检索在此端点中关 `Endpoint` 联的配置 `getConfigParameters` 值。 此方法返回一组对 `ConfigParameter` 象。
   * 通过检索数组中的每个元素来检索有关每个配置值的信息。 每个元素都是一个 `ConfigParameter` 对象。 例如，可以通过调用对象的方法来确定配置值是必需的还是 `ConfigParameter` 可选的 `isRequired` 。 如果需要配置值，则此方法返回 `true`。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速入门：使用Java API检索端点连接器信息](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-retrieving-endpoint-connector-information-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
