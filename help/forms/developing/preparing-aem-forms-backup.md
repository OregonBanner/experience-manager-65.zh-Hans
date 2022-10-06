---
title: 准备AEM Forms以备份
seo-title: Preparing AEM Forms for Backup
description: 了解如何使用备份和还原服务，通过Java API和Web服务API进入并离开AEM Forms服务器的备份模式。
seo-description: Learn how to use the Backup and Restore service to enter and leave the Backup mode for AEM Forms server using the Java API and the Web Service API.
uuid: b8ef2bed-62e2-4000-b55a-30d2fc398a5f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e747147e-e96d-43c7-87b3-55947eef81f5
role: Developer
exl-id: aeab003d-ba64-4760-9c56-44638501e9ff
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2520'
ht-degree: 0%

---

# 准备AEM Forms以备份 {#preparing-aem-forms-for-backup}

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

## 关于备份和恢复服务 {#about-the-backup-and-restore-service}

备份和还原服务允许您将AEM Forms放入 *备份模式*，用于执行热备份。 备份和恢复服务实际上不执行AEM Forms备份或还原系统。 相反，它会使您的服务器处于状态，以便进行一致且可靠的备份，同时允许您的服务器继续运行。 您负责备份全局文档存储(GDS)和连接到表单服务器的数据库的操作。 GDS是用于存储在长生命周期流程中使用的文件的目录。

备份模式是服务器进入的一种状态，这样在备份过程进行时，GDS中的文件便不会被清除。 相反，会在GDS目录下创建子目录，以在保存备份模式结束后维护要清除的文件记录。 文件旨在在系统重新启动后继续存在，并且可以跨越数天，甚至数年。 这些文件是表单服务器整体状态的关键部分，可能包括PDF文件、策略或表单模板。 如果其中任何文件丢失或损坏，则表单服务器上的进程可能变得不稳定，数据可能丢失。

您可以选择执行快照备份，在快照备份中，您通常会在一段时间内进入备份模式，然后在完成备份活动后退出备份模式。 需要离开备份模式，以便能够从GDS中清除文件，以确保其不会不必要地增大。 您可以明确地离开备份模式，或在备份模式会话中等待时间过期。

您还可以将服务器保留为永久备份模式，这是用于滚动备份或连续系统覆盖的备份策略的典型模式。 滚动备份模式表示系统始终处于备份模式，新备份模式会话在前一会话发布后立即启动。 在连续备份模式下，文件将在两个备份模式会话后清除，不再被引用。

您可以使用备份和恢复服务将您创建的现有应用程序或新应用程序添加到其中，以执行连接到表单服务器的GDS或数据库的备份。

>[!NOTE]
>
>与AEM Forms实施的任何其他方面一样，您的备份和恢复策略应在开发或暂存环境中开发和测试，然后再用于生产，以确保整个解决方案能够按预期工作，而不会丢失数据。

您可以使用备份和恢复服务执行以下任务：

* 进入备份模式。
* 离开备份模式。

>[!NOTE]
>
>有关为AEM Forms执行备份时应考虑的事项的详细信息，请参阅 [管理帮助](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>有关备份和还原服务的详细信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

## 在表单服务器上进入备份模式 {#entering-backup-mode-on-the-forms-server}

您进入备份模式，以允许对表单服务器进行热备份。 进入备份模式时，您可以根据贵组织的备份过程指定以下信息：

* 标识备份模式会话的唯一标签，可能对您的备份过程有用。
* 备份过程完成的时间。
* 用于指示是否处于连续备份模式的标记，仅当您执行滚动备份时，此标记才有用。

在将应用程序写入备份模式之前，建议您了解在将表单服务器置于备份模式后将使用的备份过程。 有关为AEM Forms执行备份时应考虑的事项的详细信息，请参阅 [管理帮助](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>有关备份和还原服务的详细信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary-of-steps}

要创建进入备份模式的应用程序，请执行以下步骤：

1. 包括项目文件。
1. 创建BackupService客户端对象。
1. 确定唯一的标签、执行备份的时间以及是否处于连续备份模式。
1. 进入备份模式。
1. （可选）检索有关服务器上备份模式会话的信息。
1. 执行GDS（全局数据存储）和数据库的备份。

**包含项目文件**

在开发项目中包含必需的文件。 这些文件对于在您的项目中正确编译代码和使用备份和恢复服务API非常重要。

有关这些文件位置的信息，请参阅 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建BackupService客户端API对象**

要以编程方式离开备份模式，请创建一个BackupService客户端对象以使用备份和还原服务API。

**确定唯一的标签，确定执行备份的时间，并决定是否处于连续备份模式**

在进入备份模式之前，您应该确定一个唯一的标签，确定要分配多少时间来执行备份，并确定是否希望表单服务器保持备份模式。 这些注意事项对于与贵组织建立的备份过程集成非常重要。 (请参阅 [管理帮助](https://www.adobe.com/go/learn_aemforms_admin_63).)

**进入备份模式**

使用与贵组织的备份过程一致的参数进入备份模式。

**检索有关服务器上备份模式会话的信息**

进入备份模式后，可以检索有关会话的信息。 此信息可用于与备份过程集成

**执行GDS和数据库的备份**

成功进入备份模式后，可以执行全局文档存储(GDS)和表单服务器所连接的数据库的备份。 此步骤特定于您的组织，因为您可以手动执行此步骤，也可以运行其他工具来执行备份过程。

### 使用Java API进入备份模式 {#enter-backup-mode-using-the-java-api}

使用备份和还原服务API进入备份模式：

1. 包含项目文件

   在您Java项目的类路径中包含必要的客户端JAR文件，如adobe-backup-restore-client-sdk.jar。 要创建Java客户端应用程序，必须将以下JAR文件添加到您项目的类路径中：

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar(如果AEM Forms部署在JBoss应用程序服务器上，则此变量为必需变量)
   * jbossall-client.jar(如果AEM Forms部署在JBoss应用程序服务器上，则此为必需字段)

1. 创建BackupService客户端API对象

   您使用 `ServiceClientFactory` 对象和BackupService客户端API对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。 (请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * 创建 `BackupService` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 确定唯一的标签，确定执行备份的时间，并决定是否处于连续备份模式

   确定唯一标签，确定要分配多少时间来执行备份，并确定是否希望表单服务器保持连续备份模式。

1. 进入备份模式

   通过调用 `enterBackupMode` 方法：

   * A `String` 值，指定标识备份模式会话的唯一人类可读标签。 建议不要使用无法编码为XML格式的空格或字符。
   * 安 `int` 值，指定在备份模式下停留的分钟数。 您可以从 `1` to `10080` （一周内的分钟数）。 使用连续备份模式时，将忽略此值。
   * A `Boolean` 指定是否处于连续备份模式的值。 值 `True` 指定为处于连续备份模式。 在连续备份模式下，将忽略您指定的在备份模式下停留的分钟数值。

      连续备份模式是指在当前备份模式会话完成后启动新的备份模式会话。 值 `False` 表示不使用连续备份模式，在离开备份模式后，将恢复从GDS中清除文件。

1. 检索有关服务器上备份模式会话的信息

   使用 `BackupModeEntryResult` 调用后返回的对象 `enterBackupMode` 方法。 在进入备份模式后可检索到的信息对于与备份过程集成可能非常有用。 例如，标签、备份ID和开始时间可能会用作备份过程文件名的输入。

1. 执行GDS和数据库的备份

   备份全局文档存储(GDS)和表单服务器所连接的数据库。 用于执行备份的操作不属于AEM Forms SDK的一部分，甚至可能包括特定于贵组织中备份过程的手动步骤。

### 使用Web服务API进入备份模式 {#enter-backup-mode-using-the-web-service-api}

使用备份和还原服务API提供的Web服务进入备份模式：

1. 包含项目文件

   * 创建使用备份和还原服务API WSDL的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建BackupService客户端API对象

   使用Microsoft .NET客户端程序集，创建 `BackupServiceService` 对象，方法是调用其默认构造函数，并使用 `Credentials` 方法。

1. 确定唯一的标签，确定执行备份的时间，并决定是否处于连续备份模式

   确定唯一标签，确定要分配多少时间来执行备份，并确定是否希望表单服务器保持连续备份模式。

1. 进入备份模式

   要进入备份模式，请调用enterBackupMode方法并传递以下值：

   * A `String` 值，指定标识备份模式会话的唯一人类可读标签。 建议不要使用无法编码为XML格式的空格或字符。
   * A `Uint32` 值，指定在备份模式下停留的分钟数。 您可以从 `1` to `10080` （一周内的分钟数）。 使用连续备份模式时，将忽略此值。
   * A `Boolean` 指定是否处于连续备份模式的值。 值 `True` 指定为处于连续备份模式。 在连续备份模式下，将忽略您指定的在备份模式下停留的分钟数值。 连续备份模式是指在当前备份模式会话完成后启动新的备份模式会话。

      值 `False` 表示不使用连续备份模式，在离开备份模式后，将恢复从GDS中清除文件。

1. 检索有关服务器上备份模式会话的信息

   在从BackupModeEntryResult中调用enterBackupMode方法以验证备份模式会话是否成功后，检索有关备份模式会话的信息。 在进入备份模式后可检索到的信息对于与备份过程集成可能非常有用。 例如，标签、备份ID和开始时间可能会用作备份过程文件名的输入。

1. 执行GDS和数据库的备份

   备份全局文档存储(GDS)和表单服务器所连接的数据库。 用于执行备份的操作不属于AEM Forms SDK的一部分，甚至可能包括特定于贵组织中备份过程的手动步骤。

## 在Forms服务器上保留备份模式 {#leaving-backup-mode-on-the-forms-server}

您退出备份模式，以便表单服务器从表单服务器上的GDS（全局文档存储）恢复清除文件。

在编写应用程序以进入离开模式之前，建议您了解与AEM Forms一起使用的备份过程。 有关为AEM Forms执行备份时应考虑的事项的详细信息，请参阅 [管理帮助](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>有关备份和还原服务的详细信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-1}

要离开备份模式，请执行以下步骤：

1. 包括项目文件。
1. 创建BackupService客户端对象。
1. 离开备份模式。
1. （可选）检索有关在表单服务器上运行的备份模式会话的信息。

**包含项目文件**

在开发项目中包含所有必需的文件。 这些文件对于正确编译代码和使用备份和恢复服务API非常重要。

有关这些文件位置的信息，请参阅 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建BackupService客户端API对象**

要以编程方式离开备份模式，请创建一个BackupService客户端对象以使用备份和还原服务API。

**退出备份模式**

保留备份模式，以恢复从全局文档存储(GDS)中正常清除文件。 在离开备份模式之前，您应该验证备份过程是否已完成。

**检索有关已结束的备份模式会话的信息**

离开备份模式后，可以检索有关会话的信息。 此信息可用于与备份过程集成。

### 使用Java API退出备份模式 {#leave-backup-mode-using-the-java-api}

使用备份和还原服务API(Java)离开备份模式：

1. 包含项目文件

   在您Java项目的类路径中包含必要的客户端JAR文件，如adobe-backup-restore-client-sdk.jar。 要创建Java客户端应用程序，必须将以下JAR文件添加到您项目的类路径中：

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar(如果AEM Forms部署在JBoss应用程序服务器上，则此变量为必需变量)
   * jbossall-client.jar(如果AEM Forms部署在JBoss应用程序服务器上，则此为必需字段)

1. 创建BackupService客户端API对象

   您使用 `ServiceClientFactory` 对象和BackupService客户端API对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。 (请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * 创建 `BackupService` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 进入备份模式

   通过调用 `leaveBackupMode` 方法。

1. 检索有关服务器上备份模式会话的信息

   使用 `BackupModeResult` 返回的对象。 在进入备份模式后可检索到的信息对于与备份过程集成可能非常有用。 例如，标签、备份ID和开始时间可能会用作备份过程文件名的输入。

### 使用Web服务API退出备份模式 {#leave-backup-mode-using-the-web-service-api}

使用备份和还原服务API（Web服务）离开备份模式：

1. 包含项目文件

   要使用Web服务，必须确保包含代理文件。 请按照以下步骤将项目配置为使用备份和恢复服务API作为Web服务。

   * 创建使用备份和还原服务API WSDL的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建BackupService客户端API对象

   使用Microsoft .NET客户端程序集，创建 `BackupServiceService` 对象。

1. 进入备份模式

   通过调用 `leaveBackupMode` web服务操作。

1. 检索有关服务器上备份模式会话的信息

   在操作后检索备份模式标识符，以验证其是否成功。 离开备份模式后可检索到的信息对于与备份过程集成可能非常有用。
