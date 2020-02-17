---
title: 准备AEM Forms以备份
seo-title: 准备AEM Forms以备份
description: 'null'
seo-description: 'null'
uuid: b8ef2bed-62e2-4000-b55a-30d2fc398a5f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e747147e-e96d-43c7-87b3-55947eef81f5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 准备AEM Forms以备份 {#preparing-aem-forms-for-backup}

## 关于备份和恢复服务 {#about-the-backup-and-restore-service}

通过备份和还原服务，您可以将AEM Forms置入备 *份模式*，这样可以执行热备份。 备份和还原服务实际上不执行AEM Forms备份或还原系统。 相反，它使服务器处于一种状态，以便进行一致、可靠的备份，同时允许服务器继续运行。 您负责备份全局文档存储(GDS)和连接到表单服务器的数据库的操作。 GDS是用于存储长期进程中使用的文件的目录。

备份模式是服务器进入的状态，这样在执行备份过程时，不会清除GDS中的文件。 而是在GDS目录下创建子目录，以在保存备份模式结束后保留要清除的文件记录。 文件旨在在系统重新启动后继续运行，并且可以跨日或数年。 这些文件是表单服务器整体状态的关键部分，可能包括PDF文件、策略或表单模板。 如果这些文件中的任何一个丢失或损坏，表单服务器上的进程可能变得不稳定，数据可能丢失。

您可以选择执行快照备份，通常在备份操作完成后进入备份模式一段时间，然后离开备份模式。 需要退出备份模式，以便能够从GDS中清除文件，以确保它不会不必要地扩大。 您可以显式离开备份模式，也可以等待备份模式会话的过期时间。

您还可以将服务器保留为永久备份模式，这是滚动备份或连续系统覆盖的备份策略的典型操作。 滚动备份模式表示系统始终处于备份模式，新的备份模式会话在前一会话发布后立即启动。 在连续备份模式下，文件在两个备份模式会话后被清除，不再被引用。

您可以使用备份和恢复服务向现有应用程序或您创建的新应用程序添加备份连接到表单服务器的GDS或数据库。

>[!NOTE]
>
>与AEM Forms实施的任何其他方面一样，在生产中使用之前，应在开发或分阶段环境中开发和测试备份和恢复策略，以确保整个解决方案能够按预期工作，而不会丢失数据。

您可以使用备份和还原服务执行以下任务：

* 进入备份模式。
* 退出备份模式。

>[!NOTE]
>
>有关在为AEM Forms执行备份时应考虑的事项的详细信息，请参阅管 [理帮助](https://www.adobe.com/go/learn_aemforms_admin_63)。

>[!NOTE]
>
>有关备份和还原服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 在表单服务器上进入备份模式 {#entering-backup-mode-on-the-forms-server}

进入备份模式以允许对表单服务器进行热备份。 进入备份模式时，根据单位的备份过程指定以下信息：

* 用于标识备份模式会话的唯一标签，该会话可能对备份过程有用。
* 完成备份过程的时间。
* 指示是否处于连续备份模式的标记，仅当您执行滚动备份时，此标记才有用。

在编写应用程序以进入备份模式之前，建议您了解将表单服务器置于备份模式后将使用的备份过程。 有关在为AEM Forms执行备份时应考虑的事项的详细信息，请参阅管 [理帮助](https://www.adobe.com/go/learn_aemforms_admin_63)。

>[!NOTE]
>
>有关备份和还原服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary-of-steps}

要创建进入备份模式的应用程序，请执行以下步骤：

1. 包括项目文件。
1. 创建BackupService客户端对象。
1. 确定唯一标签、执行备份的时间以及是否处于连续备份模式。
1. 进入备份模式。
1. （可选）检索有关服务器上备份模式会话的信息。
1. 执行GDS（全局数据存储）和数据库的备份。

**包括项目文件**

在开发项目中包含必要的文件。 这些文件对于正确编译代码和使用备份和还原服务API而言很重要。

有关这些文件的位置的信息，请参 [阅包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建BackupService Client API对象**

要以编程方式退出备份模式，请创建一个BackupService客户端对象以使用Backup and Restore Service API。

**确定唯一的标签，确定执行备份的时间，并决定是否处于连续备份模式**

在进入备份模式之前，您应该决定一个唯一的标签，确定要分配多少时间来执行备份，并决定是否希望表单服务器保持备份模式。 这些注意事项对于与贵组织建立的备份过程集成非常重要。 (请参阅 [管理帮助](https://www.adobe.com/go/learn_aemforms_admin_63)。)

**进入备份模式**

进入备份模式，并使用与组织中的备份过程一致的参数。

**检索有关服务器上备份模式会话的信息**

进入备份模式后，可以检索有关会话的信息。 此信息可用于与备份过程集成

**执行GDS和数据库的备份**

在成功进入备份模式后，可以执行全局文档存储(GDS)和表单服务器所连接到的数据库的备份。 此步骤特定于您的组织，因为您可以手动执行此步骤，也可以运行其他工具来执行备份过程。

### 使用Java API进入备份模式 {#enter-backup-mode-using-the-java-api}

使用备份和还原服务API进入备份模式：

1. 包括项目文件

   在Java项目的类路径中包含必需的客户端JAR文件，如adobe-backup-restore-client-sdk.jar。 要创建Java客户端应用程序，必须将以下JAR文件添加到项目的类路径中：

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar（在JBoss Application server上部署AEM Forms时为必需）
   * jbossall-client.jar（在JBoss Application server上部署AEM表单时需要）

1. 创建BackupService Client API对象

   将对象 `ServiceClientFactory` 和BackupService客户端API对象结合使用。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。 (请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。)
   * 使用对 `BackupService` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 确定唯一的标签，确定执行备份的时间，并决定是否处于连续备份模式

   确定唯一的标签，确定要分配多少时间来执行备份，并决定是否希望表单服务器保持连续备份模式。

1. 进入备份模式

   通过使用以下参数调用 `enterBackupMode` 方法进入备份模式：

   * 一个 `String` 值，它指定标识备份模式会话的唯一的人可读标签。 建议不要使用无法编码为XML格式的空格或字符。
   * 一个 `int` 值，它指定在备份模式下停留的分钟数。 您可以指定一个从到 `1` 的值( `10080` 一周内的分钟数)。 使用连续备份模式时忽略此值。
   * 一个 `Boolean` 值，它指定是否处于连续备份模式。 值指定 `True` 为连续备份模式。 在连续备份模式下，将忽略您为保持备份模式所指定的分钟数指定的值。

      连续备份模式意味着在当前备份模式会话完成后启动新的备份模式会话。 值表示不 `False` 使用连续备份模式，在退出备份模式后，将恢复从GDS中清除文件。

1. 检索有关服务器上备份模式会话的信息

   使用调用方 `BackupModeEntryResult` 法后返回的对象检索 `enterBackupMode` 信息。 进入备份模式后可以检索的信息可能有助于与备份过程集成。 例如，标签、备份ID和开始时间可能用作备份过程文件名的输入。

1. 执行GDS和数据库的备份

   备份Global Document Storage(GDS)和您的表单服务器所连接的数据库。 用于执行备份的操作不是AEM Forms SDK的一部分，甚至可能包括特定于您组织中备份过程的手动步骤。

### 使用Web服务API进入备份模式 {#enter-backup-mode-using-the-web-service-api}

使用Backup and Restore Service API提供的Web服务进入备份模式：

1. 包括项目文件

   * 创建一个Microsoft .NET客户端组件，它使用Backup and Restore Service API WSDL。
   * 参考Microsoft .NET客户端程序集。

1. 创建BackupService Client API对象

   使用Microsoft .NET客户端程序集，通过调用 `BackupServiceService` 其默认构造函数创建一个对象，然后使用方法指定凭据 `Credentials` 。

1. 确定唯一的标签，确定执行备份的时间，并决定是否处于连续备份模式

   确定唯一的标签，确定要分配多少时间来执行备份，并决定是否希望表单服务器保持连续备份模式。

1. 进入备份模式

   要进入备份模式，请调用enterBackupMode方法并传递以下值：

   * 一个 `String` 值，它指定标识备份模式会话的唯一的人可读标签。 建议不要使用无法编码为XML格式的空格或字符。
   * 一个 `Uint32` 值，它指定在备份模式下停留的分钟数。 您可以指定一个从到 `1` (一 `10080` 周内的分钟数)的值。 使用连续备份模式时忽略此值。
   * 一个 `Boolean` 值，它指定是否处于连续备份模式。 值指定 `True` 为连续备份模式。 在连续备份模式下，将忽略您为保持备份模式所指定的分钟数指定的值。 连续备份模式意味着在当前备份模式会话完成后启动新的备份模式会话。

      值表示不 `False` 使用连续备份模式，在退出备份模式后，将恢复从GDS中清除文件。

1. 检索有关服务器上备份模式会话的信息

   在从BackupModeEntryResult调用enterBackupMode方法后检索有关备份模式会话的信息，该方法将返回以验证备份模式会话是否成功。 进入备份模式后可以检索的信息可能有助于与备份过程集成。 例如，标签、备份ID和开始时间可能用作备份过程文件名的输入。

1. 执行GDS和数据库的备份

   备份Global Document Storage(GDS)和您的表单服务器所连接的数据库。 用于执行备份的操作不是AEM Forms SDK的一部分，甚至可能包括特定于您组织中备份过程的手动步骤。

## 在表单服务器上退出备份模式 {#leaving-backup-mode-on-the-forms-server}

您将退出备份模式，以便表单服务器恢复从表单服务器上的GDS（全局文档存储）清除文件。

在编写应用程序以进入退出模式之前，建议您了解AEM Forms使用的备份过程。 有关在为AEM Forms执行备份时应考虑的事项的详细信息，请参阅管 [理帮助](https://www.adobe.com/go/learn_aemforms_admin_63)。

>[!NOTE]
>
>有关备份和还原服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-1}

要退出备份模式，请执行以下步骤：

1. 包括项目文件。
1. 创建BackupService客户端对象。
1. 退出备份模式。
1. （可选）检索有关在表单服务器上运行的备份模式会话的信息。

**包括项目文件**

在开发项目中包含所有必需的文件。 这些文件对于正确编译代码和使用备份和还原服务API非常重要。

有关这些文件的位置的信息，请参 [阅包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建BackupService Client API对象**

要以编程方式退出备份模式，请创建一个BackupService客户端对象以使用Backup and Restore Service API。

**退出备份模式**

保持备份模式，以继续从全局文档存储(GDS)中正常清除文件。 在退出备份模式之前，应验证备份过程是否已完成。

**检索有关已结束的备份模式会话的信息**

退出备份模式后，可以检索有关会话的信息。 此信息可用于与备份过程集成。

### 使用Java API退出备份模式 {#leave-backup-mode-using-the-java-api}

使用备份和还原服务API(Java)退出备份模式：

1. 包括项目文件

   在Java项目的类路径中包含必需的客户端JAR文件，如adobe-backup-restore-client-sdk.jar。 要创建Java客户端应用程序，必须将以下JAR文件添加到项目的类路径中：

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar（在JBoss Application server上部署AEM Forms时为必需）
   * jbossall-client.jar（在JBoss Application server上部署AEM表单时需要）

1. 创建BackupService Client API对象

   将对象 `ServiceClientFactory` 和BackupService客户端API对象结合使用。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。 (请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。)
   * 通过使 `BackupService` 用对象的构造函数并将对象作为参数 `ServiceClientFactory` 进行传递来创建对象。

1. 进入备份模式

   通过调用方法退出备份 `leaveBackupMode` 模式。

1. 检索有关服务器上备份模式会话的信息

   使用返回的对象检索有关 `BackupModeResult` 操作的信息。 进入备份模式后可以检索的信息可能有助于与备份过程集成。 例如，标签、备份ID和开始时间可能用作备份过程文件名的输入。

### 使用Web服务API退出备份模式 {#leave-backup-mode-using-the-web-service-api}

使用备份和还原服务API（Web服务）退出备份模式：

1. 包括项目文件

   要使用Web服务，必须确保包含代理文件。 请按照以下步骤将项目配置为将备份和还原服务API用作Web服务。

   * 创建一个Microsoft .NET客户端组件，它使用Backup and Restore Service API WSDL。
   * 参考Microsoft .NET客户端程序集。

1. 创建BackupService Client API对象

   使用Microsoft .NET客户端程序集，通过调用 `BackupServiceService` 其默认构造函数创建对象。

1. 进入备份模式

   通过调用Web服务操作 `leaveBackupMode` 退出备份模式。

1. 检索有关服务器上备份模式会话的信息

   在操作后检索备份模式标识符以验证其是否成功。 退出备份模式后可以检索的信息可能有助于与备份过程集成。

