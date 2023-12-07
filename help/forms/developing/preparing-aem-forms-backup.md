---
title: 正在准备AEM Forms以进行备份
description: 了解如何使用Backup and Restore服务通过Java API和Web服务API进入和离开AEM Forms服务器的备份模式。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: aeab003d-ba64-4760-9c56-44638501e9ff
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2484'
ht-degree: 0%

---

# 正在准备AEM Forms以进行备份 {#preparing-aem-forms-for-backup}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms 。**

## 关于备份和还原服务 {#about-the-backup-and-restore-service}

通过备份和还原服务，您可以将AEM Forms放入 *备份模式*，可以执行热备份。 备份和还原服务实际上不会执行AEM Forms的备份或还原您的系统。 相反，它使您的服务器处于一致且可靠的备份状态，同时允许您的服务器继续运行。 您负责备份全局文档存储(GDS)和连接到Forms服务器的数据库。 GDS是用于存储长期进程中使用的文件的目录。

备份模式是服务器进入的一种状态，这样在执行备份过程时就不会清除GDS中的文件。 而是在GDS目录下创建子目录，以在保存备份模式结束后维护要清除的文件的记录。 文件可在系统重新启动后继续保存，可以持续数天甚至数年。 这些文件是Forms服务器整体状态的关键部分，可能包括PDF文件、策略或表单模板。 如果这些文件中的任何一个丢失或损坏，Forms服务器上的进程可能会变得不稳定，并且数据可能会丢失。

您可以选择执行快照备份，通常在快照备份中进入一段时间的备份模式，然后在完成备份活动后退出备份模式。 需要退出备份模式，以便可以从GDS中清除文件，确保不会不必要地增大文件大小。 您可以明确退出备份模式，或等待备份模式会话的过期时间。

您还可以将服务器保留为永久备份模式，这是用于滚动备份或连续系统覆盖的典型备份策略。 滚动备份模式表示系统始终处于备份模式，一旦释放上一个会话，就会启动新的备份模式会话。 当处于连续备份模式时，文件将在两个备份模式会话之后清除，并且不再被引用。

您可以使用“备份和还原”服务向现有应用程序或新建的应用程序添加数据，这些应用程序是为执行连接到Forms Server的GDS或数据库的备份而创建的。

>[!NOTE]
>
>与AEM Forms实施的任何其他方面一样，您的备份和恢复策略应在生产中使用之前在开发或暂存环境中开发和测试，以确保整个解决方案按预期工作，且不会丢失数据。

您可以使用备份和还原服务执行以下任务：

* 进入备份模式。
* 离开备份模式。

>[!NOTE]
>
>有关为AEM Forms执行备份时应考虑哪些内容的更多信息，请参阅 [管理帮助](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>有关备份和还原服务的详细信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

## 在Forms服务器上进入备份模式 {#entering-backup-mode-on-the-forms-server}

进入备份模式以允许Forms服务器的热备份。 进入备份模式时，可根据组织的备份过程指定以下信息：

* 一个唯一标签，用于标识可能对备份过程有用的备份模式会话。
* 备份过程完成的时间。
* 用于指示是否处于连续备份模式的标志，该标志仅在执行滚动备份时才有用。

在将应用程序写入备份模式之前，建议您了解将Forms服务器置于备份模式后所使用的备份过程。 有关为AEM Forms执行备份时应考虑哪些内容的更多信息，请参阅 [管理帮助](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>有关备份和还原服务的详细信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary-of-steps}

要创建进入备份模式的应用程序，请执行以下步骤：

1. 包括项目文件。
1. 创建BackupService客户端对象。
1. 确定唯一标签、执行备份的时间以及是否处于连续备份模式。
1. 进入备份模式。
1. （可选）检索有关服务器上的备份模式会话的信息。
1. 执行GDS （全局数据存储）和数据库的备份。

**包含项目文件**

在开发项目中包含必要的文件。 这些文件非常重要，要包含在您的项目中，以便正确编译代码并使用备份和还原服务API。

有关这些文件的位置的信息，请参见 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建BackupService客户端API对象**

要以编程方式退出备份模式，您需要创建一个BackupService客户端对象，以使用备份和还原服务API。

**确定唯一标签，确定执行备份的时间量，以及是否处于连续备份模式**

在进入备份模式之前，您应该决定一个唯一标签，确定要分配用于执行备份的时间量，以及是否希望Forms服务器保持备份模式。 这些注意事项对于与您的组织建立的备份过程集成非常重要。 (请参阅 [管理帮助](https://www.adobe.com/go/learn_aemforms_admin_63).)

**进入备份模式**

使用与组织中的备份过程一致的参数进入备份模式。

**检索有关服务器上备份模式会话的信息**

进入备份模式后，可以检索有关会话的信息。 此信息可用于集成您的备份过程

**执行GDS和数据库的备份**

成功进入备份模式后，您可以对Global Document Storage (GDS)和Forms Server连接到的数据库执行备份。 此步骤特定于您的组织，因为您可以手动执行此步骤，也可以运行其他工具来执行备份过程。

### 使用Java API进入备份模式 {#enter-backup-mode-using-the-java-api}

使用备份和还原服务API进入备份模式：

1. 包含项目文件

   在Java项目的类路径中包含必要的客户端JAR文件，例如adobe-backup-restore-client-sdk.jar。 要创建Java客户端应用程序，必须将以下JAR文件添加到项目的类路径中：

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar(如果在JBoss Application Server上部署了AEM Forms，则此为必填字段)
   * jbossall-client.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)

1. 创建BackupService客户端API对象

   您使用 `ServiceClientFactory` 对象和BackupService客户端API对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。 (请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * 创建 `BackupService` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 确定唯一标签，确定执行备份的时间量，以及是否处于连续备份模式

   确定唯一标签，确定要分配用于执行备份的时间量，以及是否希望Forms服务器保持连续备份模式。

1. 进入备份模式

   通过调用 `enterBackupMode` 方法：

   * A `String` 值，指定用于标识备份模式会话的唯一人类可读标签。 建议不要使用不能编码为XML格式的空格或字符。
   * An `int` 指定在备份模式下保留的分钟数的值。 您可以指定一个值，从 `1` 到 `10080` （一周内的分钟数）。 使用连续备份模式时，此值将被忽略。
   * A `Boolean` 指定是否处于连续备份模式的值。 值 `True` 指定处于连续备份模式。 当处于连续备份模式时，将忽略您为处于备份模式的分钟数指定的值。

     连续备份模式是指在当前备份模式会话完成后，启动新的备份模式会话。 值 `False` 表示不使用连续备份模式，离开备份模式后，将恢复从GDS中清除文件。

1. 检索有关服务器上备份模式会话的信息

   使用检索信息 `BackupModeEntryResult` 调用后返回的对象 `enterBackupMode` 方法。 进入备份模式后可以检索的信息对于与备份过程集成可能很有用。 例如，标签、备份ID和开始时间可能用作备份过程的文件名输入。

1. 执行GDS和数据库的备份

   备份Global Document Storage (GDS)和Forms Server所连接的数据库。 执行备份的操作不属于AEM Forms SDK的一部分，甚至可能包括特定于组织中备份过程的手动步骤。

### 使用Web服务API进入备份模式 {#enter-backup-mode-using-the-web-service-api}

使用备份和还原服务API提供的Web服务进入备份模式：

1. 包含项目文件

   * 创建使用备份和还原服务API WSDL的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建BackupService客户端API对象

   使用Microsoft .NET客户端程序集，创建 `BackupServiceService` 对象，方法是调用其默认构造函数，并使用 `Credentials` 方法。

1. 确定唯一标签，确定执行备份的时间量，以及是否处于连续备份模式

   确定唯一标签，确定要分配用于执行备份的时间量，以及是否希望Forms服务器保持连续备份模式。

1. 进入备份模式

   要进入备份模式，请调用enterBackupMode方法并传递以下值：

   * A `String` 值，指定用于标识备份模式会话的唯一人类可读标签。 建议不要使用不能编码为XML格式的空格或字符。
   * A `Uint32` 指定在备份模式下保留的分钟数的值。 您可以指定一个值，从 `1` 到 `10080` （一周内的分钟数）。 使用连续备份模式时，此值将被忽略。
   * A `Boolean` 指定是否处于连续备份模式的值。 值 `True` 指定处于连续备份模式。 当处于连续备份模式时，将忽略您为处于备份模式的分钟数指定的值。 连续备份模式是指在当前备份模式会话完成后，启动新的备份模式会话。

     值 `False` 表示不使用连续备份模式，离开备份模式后，将恢复从GDS中清除文件。

1. 检索有关服务器上备份模式会话的信息

   在从BackupModeEntryResult调用enterBackupMode方法后检索有关备份模式会话的信息，返回的方法用于验证是否成功。 进入备份模式后可以检索的信息对于与备份过程集成可能很有用。 例如，标签、备份ID和开始时间可能用作备份过程的文件名输入。

1. 执行GDS和数据库的备份

   备份Global Document Storage (GDS)和Forms Server所连接的数据库。 执行备份的操作不属于AEM Forms SDK的一部分，甚至可能包括特定于组织中备份过程的手动步骤。

## 在Forms服务器上保留备份模式 {#leaving-backup-mode-on-the-forms-server}

离开备份模式后，Forms Server将恢复从Forms Server上的GDS（全局文档存储）中清除文件。

在将应用程序写入离开模式之前，建议您了解与AEM Forms一起使用的备份过程。 有关为AEM Forms执行备份时应考虑哪些内容的更多信息，请参阅 [管理帮助](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>有关备份和还原服务的详细信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-1}

要退出备份模式，请执行以下步骤：

1. 包括项目文件。
1. 创建BackupService客户端对象。
1. 离开备份模式。
1. （可选）检索有关在Forms服务器上运行的备份模式会话的信息。

**包含项目文件**

在开发项目中包含所有必需的文件。 这些文件对于正确编译代码以及使用备份和还原服务API非常重要。

有关这些文件的位置的信息，请参见 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建BackupService客户端API对象**

要以编程方式退出备份模式，您需要创建一个BackupService客户端对象，以使用备份和还原服务API。

**离开备份模式**

离开备份模式以恢复从全局文档存储(GDS)正常清除文件。 离开备份模式之前，应确认备份过程已完成。

**检索有关已结束的备份模式会话的信息**

离开备份模式后，可以检索有关会话的信息。 此信息可用于与备份过程集成。

### 使用Java API退出备份模式 {#leave-backup-mode-using-the-java-api}

使用备份和还原服务API (Java)退出备份模式：

1. 包含项目文件

   在Java项目的类路径中包含必要的客户端JAR文件，例如adobe-backup-restore-client-sdk.jar。 要创建Java客户端应用程序，必须将以下JAR文件添加到项目的类路径中：

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar(如果在JBoss Application Server上部署了AEM Forms，则此为必填字段)
   * jbossall-client.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)

1. 创建BackupService客户端API对象

   您使用 `ServiceClientFactory` 对象和BackupService客户端API对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。 (请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * 创建 `BackupService` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 进入备份模式

   通过调用 `leaveBackupMode` 方法。

1. 检索有关服务器上备份模式会话的信息

   使用检索有关操作的信息 `BackupModeResult` 返回的对象。 进入备份模式后可以检索的信息对于与备份过程集成可能很有用。 例如，标签、备份ID和开始时间可能用作备份过程的文件名输入。

### 使用Web服务API退出备份模式 {#leave-backup-mode-using-the-web-service-api}

使用备份和还原服务API （Web服务）退出备份模式：

1. 包含项目文件

   要使用Web服务，您必须确保包含代理文件。 按照以下步骤将项目配置为使用备份和还原服务API作为Web服务。

   * 创建使用备份和还原服务API WSDL的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建BackupService客户端API对象

   使用Microsoft .NET客户端程序集，创建 `BackupServiceService` 对象。

1. 进入备份模式

   通过调用 `leaveBackupMode` Web服务操作。

1. 检索有关服务器上备份模式会话的信息

   在操作后检索备份模式标识符以验证操作是否成功。 退出备份模式后可以检索的信息对于与备份过程集成可能很有用。
