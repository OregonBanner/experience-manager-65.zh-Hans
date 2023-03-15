---
title: 监控和维护AEM实例
seo-title: Monitoring and Maintaining Your AEM instance
description: 了解如何监视AEM。
seo-description: Learn how to monitor AEM.
uuid: 14466552-5c92-4730-a427-85675a2b121c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 5d2364b7-4497-4f8b-85ef-6e780bfb8c36
docset: aem65
feature: Configuring
exl-id: d3375935-090d-4052-8234-68ef4ddbab6a
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '5972'
ht-degree: 1%

---

# 监控和维护AEM实例{#monitoring-and-maintaining-your-aem-instance}

在部署AEM实例后，需要执行某些任务来监视和维护其操作、性能和完整性。

这里的一个关键因素是，要识别潜在问题，您需要了解系统在正常条件下的外观和行为。 最好通过监视系统和在一段时间内收集信息来完成此操作。

| 检查 | 注意事项 | 评论/操作 |
|---|---|---|
| 备份计划。 |  | 了解如何 [备份实例](/help/sites-deploying/monitoring-and-maintaining.md#backups). |
| 灾难恢复计划。 | 您公司的灾难恢复准则。 |  |
| 错误跟踪系统可用于报告问题。 | 例如， [bugzilla](https://www.bugzilla.org/)， [jira](https://www.atlassian.com/software/jira/)或许多其他条件中的一个。 |  |
| 正在监视文件系统。 | 如果可用磁盘空间不足，则CRX存储库将“冻结”。 一旦空间可用，它将恢复。 | ” `*ERROR* LowDiskSpaceBlocker`可用空间不足时，可在日志文件中看到“ ”消息。 |
| [日志文件](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) 正在被监视。 |  |  |
| 系统监控在后台持续运行。 | 包括CPU、内存、磁盘和网络使用。 例如，使用iostat / vmstat / perfmon。 | 记录的数据是可视化的，可用于跟踪性能问题。 原始数据也可访问。 |
| [正在监视AEM性能](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance). | 包括 [请求计数器](/help/sites-deploying/monitoring-and-maintaining.md#request-counters) 以监控通信量级别。 | 如果出现重大或长期的业绩损失，应进行详细调查。 |
| 您正在监控 [复制代理](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-your-replication-agents). |  |  |
| 定期清除工作流实例。 | 存储库大小和工作流性能。 | 参见 [定期清除工作流实例](/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances). |

## 备份 {#backups}

最佳做法是将备份用于：

* 软件安装 — 在配置发生重大更改之前/之后
* 存储库中保存的内容 — 定期

贵公司可能会有您需要遵循的备份策略，关于要备份的内容和何时进行备份的其他注意事项：

* 系统和数据的重要性如何。
* 对软件或数据进行更改的频率。
* 数据量大；容量偶尔可能会成为一个问题，执行备份所需的时间也会成为一个问题。
* 是否可以在用户在线时进行备份；如果可能，会对性能产生什么影响。
* 用户的地理分布，即何时是最佳备份时间（以最大程度地降低影响）？
* 您的灾难恢复策略；是否有存储备份数据（如非现场、特定介质等）的指导原则。

通常，会定期（例如，每日、每周或每月）执行完整备份，并在中间进行增量备份（例如，每小时、每日或每周）。

>[!CAUTION]
>
>在实施生产实例的备份时，测试 *必须* 以确保备份可以成功恢复。
>
>否则，备份可能会毫无用处（最坏的情况）。

>[!NOTE]
>
>有关备份性能的详细信息，请阅读 [备份性能](/help/sites-deploying/configuring-performance.md#backup-performance) 部分。

### 备份软件安装 {#backing-up-your-software-installation}

在安装或配置发生重大更改后，备份软件安装。

为此，您需要 [备份整个存储库](#backing-up-your-repository) 然后：

1. 停止AEM。
1. 备份整个 `<cq-installation-dir>` 从您的文件系统删除。

>[!CAUTION]
>
>如果您运行的是第三方应用程序服务器，则其他文件夹可能位于不同的位置，并且可能也需要备份。 参见 [如何将AEM与应用程序服务器一起安装](/help/sites-deploying/application-server-install.md) 有关安装应用程序服务器的信息。

>[!CAUTION]
>
>支持文件数据存储的增量备份；当对其他组件（如Lucene索引）使用增量备份时，请确保已删除的文件在备份中也标记为已删除。

>[!NOTE]
>
>磁盘镜像还可以用作备份机制。

### 备份存储库 {#backing-up-your-repository}

此 [备份和恢复](/help/sites-administering/backup-and-restore.md) CRX文档的部分涵盖了与CRX存储库备份相关的所有问题。

有关进行在线“热”备份的完整详细信息，请参阅 [创建联机备份](/help/sites-administering/backup-and-restore.md#online-backup).

## 版本清除 {#version-purging}

此 **清除版本** 工具用于清除存储库中节点或节点层次结构的版本。 它的主要用途是通过删除节点的旧版本来帮助您减小存储库的大小。

本节介绍与AEM版本控制功能相关的维护操作。 此 **清除版本** 工具用于清除存储库中节点或节点层次结构的版本。 它的主要用途是通过删除节点的旧版本来帮助您减小存储库的大小。

### 概述 {#overview}

此 **清除版本** 工具作为每周维护任务提供。 在首次使用之前，需要添加该区段，然后对其进行配置。 之后，它可以按请求运行，也可以每周运行。

### 清除网站的版本 {#purging-versions-of-a-web-site}

要清除网站的版本，请按照以下步骤操作：

1. 导航到 **[工具](/help/sites-administering/tools-consoles.md)** **控制台**，选择 **操作**， **维护**，则 **每周维护时段**.

1. 选择 **+添加** 从顶部工具栏中。

   ![添加版本清除](assets/version-purge-add.png)

1. 选择 **版本清除** 从 **添加新任务** 对话框。 则 **保存**.

   ![添加版本清除](assets/version-purge-add-new-task.png)

1. 此 **版本清除** 将添加任务。 使用卡操作可以：
   * 选择 — 将显示顶部工具栏中的其他操作
   * 运行 — 立即运行配置的清除
   * 配置 — 配置每周清除任务

   ![版本清除操作](assets/version-purge-actions.png)

1. 选择 **配置** 打开Web控制台的操作 **Day CQ WCM版本清除任务**，您可以在其中配置：

   ![版本清除配置](assets/version-purge-configuration.png)

   * **清除路径**
设置要清除的内容的起始路径；例如， 
`/content/wknd`。

      >[!CAUTION]
      >
      >强烈建议您为每个网站定义多个路径。
      >
      >定义包含太多子项的路径会显着延长执行清除所需的时间。

   * **递归清除版本**

      * 如果只想清除由路径定义的节点，请取消选择。
      * 选择是否要清除由路径及其子节点定义的节点。
   * **最大版本数**
设置要保留的最大版本数（针对每个节点）。 留空将不使用此设置。

   * **最小版本数**
设置要保留的最小版本数（针对每个节点）。 留空将不使用此设置。

   * **最大版本期限**
设置要保留的最长版本保留时间（以天为单位，针对每个节点）。 留空将不使用此设置。
   则 **保存**.

1. 导航/返回 **每周维护时段** 窗口并选择 **运行** 以立即启动该流程。

>[!CAUTION]
>
>您可以使用经典UI对话框执行 [练习](#analyzing-the-console) 配置：
>
>* http://localhost:4502/etc/versioning/purge.html
>
>如果不恢复存储库，则无法还原已清除的节点。 您应该会处理好您的配置，因此我们建议您始终在清除之前执行试运行。

#### 试运行 — 分析控制台 {#analyzing-the-console}

经典UI提供了 **练习** 选项来源：

* http://localhost:4502/etc/versioning/purge.html

该流程会列出已处理的所有节点。 在此过程中，节点可以具有以下状态之一：

* `ignore (not versionnable)`：节点不支持版本控制，因此会在进程中忽略。

* `ignore (no version)`：节点没有任何版本，因此会在进程中忽略。

* `retained`：未清除节点。
* `purged`：清除节点。

此外，控制台还提供了有关版本的有用信息：

* `V 1.0`：版本号。
* `V 1.0.1`&#42;：星号表示版本是当前（基本）版本，无法清除。

* `Thu Mar 15 2012 08:37:32 GMT+0100`：版本的日期。

在下一个示例中：

* 此 **[!DNL Shirts]** 版本将被清除，因为其版本存在时间大于2天。
* 此 **[!DNL Tonga Fashions!]** 版本将被清除，因为其版本数大于5。

![global_version_screenshot](assets/global_version_screenshot.png)

## 使用审计记录和日志文件 {#working-with-audit-records-and-log-files}

可在多个位置找到与Adobe Experience Manager (AEM)相关的审核记录和日志文件。 下面提供了可在何处查找的内容的概述。

### 使用日志 {#working-with-logs}

AEM WCM会记录详细的日志。 打开包装并启动快速入门后，您可以找到以下日志：

* `<cq-installation-dir>/crx-quickstart/logs/`

* `<cq-installation-dir>/crx-quickstart/repository/`

#### 日志文件轮换 {#log-file-rotation}

日志文件轮换是指通过定期创建新文件来限制文件增长的过程。 在AEM中，一个名为 `error.log` 将根据以下既定规则每天轮换一次：

* 此 `error.log` 文件已根据模式{original_filename}重命名 `.yyyy-MM-dd`. 例如，在2010年7月11日，当前日志文件被重命名 `error.log-2010-07-10`，然后是新的 `error.og` 创建。

* 先前的日志文件不会被删除，因此您有责任定期清理旧日志文件，以限制磁盘的使用量。

>[!NOTE]
>
>如果升级AEM安装，请注意，任何不再由AEM使用的现有日志文件都将保留在磁盘上。 您可以无风险地删除它们。 所有新的日志条目将写入新的日志文件中。

### 查找日志文件 {#finding-the-log-files}

各种日志文件保存在安装AEM的文件服务器上：

* `<cq-installation-dir>/crx-quickstart/logs`

   * `access.log`
此处注册了对AEM WCM和存储库的所有访问请求。

   * `audit.log`
审核操作在此处注册。

   * `error.log`
错误消息（严重程度不同）在此处注册。

   * [ `ImageServer-<PortId>-yyyy>-<mm>-<dd>.log`](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/config-admin/server-logging/c-image-server-log.html)
此日志仅用于 [!DNL Dynamic Media] 已启用。 它提供用于分析ImageServer内部进程行为的统计和分析信息。

   * `request.log`
每个访问请求在这里与响应一起注册。

   * [ `s7access-<yyyy>-<mm>-<dd>.log`](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/config-admin/server-logging/c-access-log.html)
此日志仅用于 [!DNL Dynamic Media] 已启用。 s7access日志记录向发出的每个请求 [!DNL Dynamic Media] 到 `/is/image` 和 `/is/content`.

   * `stderr.log`
保留启动期间生成的错误消息，同样具有各种严重性级别。 默认情况下，日志级别设置为 
`Warning` ( `WARN`)

   * `stdout.log`
保留指示启动期间事件的日志消息。

   * `upgrade.log`
提供从运行的所有升级操作的日志 
`com.day.compat.codeupgrade` 和 `com.adobe.cq.upgradesexecutor` 包。

* `<cq-installation-dir>/crx-quickstart/repository`

   * `revision.log`
修订日志信息。

>[!NOTE]
>
>ImageServer和s7访问日志未包含在**system/console/status-Bundlelist**页面生成的**Download Full**包中。 出于支持目的，如果您拥有 [!DNL Dynamic Media] 问题，请在联系客户支持时附加ImageServer和s7access日志。

### 激活DEBUG日志级别 {#activating-the-debug-log-level}

默认日志级别([Apache Sling日志记录配置](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration))是信息，因此不会记录调试消息。

要为记录器激活调试日志级别，请设置属性 `org.apache.sling.commons.log.level` 以在存储库中进行调试。 例如，在 `/libs/sling/config/org.apache.sling.commons.log.LogManager` 配置 [全局Apache Sling日志记录](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration).

>[!CAUTION]
>
>不要让调试日志级别上的日志超过所需的时间，因为它会生成大量日志条目，从而占用资源。

调试文件中的一行通常以DEBUG开头，然后提供日志级别、安装程序操作和日志消息。 例如：

```shell
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

日志级别如下：

| 0 | 致命错误 | 操作失败，安装程序无法继续。 |
|---|---|---|
| 1 | 错误 | 操作失败。 安装将继续，但部分AEM WCM安装不正确，无法正常工作。 |
| 2 | 警告 | 操作已成功，但遇到了问题。 AEM WCM可能正常工作，也可能无法正常工作。 |
| 3 | 信息 | 操作已成功。 |

### 创建自定义日志文件 {#create-a-custom-log-file}

>[!NOTE]
>
>使用Adobe Experience Manager时，可通过多种方法管理此类服务的配置设置；请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 了解更多详细信息和建议的做法。

在某些情况下，您可能希望创建具有不同日志级别的自定义日志文件。 可通过以下方式在存储库中执行此操作：

1. 如果尚未存在，请创建新的配置文件夹( `sling:Folder`) `/apps/<project-name>/config`.
1. 下 `/apps/<project-name>/config`，为新建一个节点 [Apache Sling日志记录器配置](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingloggerconfigurationfactoryconfiguration)：

   * 名称： `org.apache.sling.commons.log.LogManager.factory.config-<identifier>` （因为这是Logger）

      位置 `<identifier>` 替换为（必须）输入以标识实例的自由文本（不能忽略此信息）。

      例如，`org.apache.sling.commons.log.LogManager.factory.config-MINE`

   * 类型: `sling:OsgiConfig`
   >[!NOTE]
   >
   >虽然不是技术要求，但建议将 `<identifier>` 独特。

1. 在此节点上设置以下属性：

   * 名称: `org.apache.sling.commons.log.file`

      类型：字符串

      值：指定日志文件；例如， `logs/myLogFile.log`

   * 名称: `org.apache.sling.commons.log.names`

      类型：字符串[] （字符串+多个）

      值：指定记录器将为其记录消息的OSGi服务；例如，以下所有项：

      * `org.apache.sling`
      * `org.apache.felix`
      * `com.day`
   * 名称: `org.apache.sling.commons.log.level`

      类型：字符串

      值：指定所需的日志级别( `debug`， `info`， `warn` 或 `error`)；例如 `debug`

   * 根据需要配置其他参数：

      * 名称: `org.apache.sling.commons.log.pattern`

         类型: `String`

         值：根据需要指定日志消息的模式；例如，

         `{0,date,dd.MM.yyyy HH:mm:ss.SSS} *{4}* [{2}] {3} {5}`
   >[!NOTE]
   >
   >`org.apache.sling.commons.log.pattern` 支持最多六个参数。
   >
   >{0}类型的时间戳 `java.util.Date`
   >
   >{1}日志标记
   >
   >{2}当前线程的名称
   >
   >{3}记录器的名称
   >
   >{4}日志级别
   >
   >{5}日志消息
   >
   >如果日志调用包括 `Throwable` 栈栈跟踪将附加到消息中。

   >[!CAUTION]
   >
   >org.apache.sling.commons.log.names必须具有值。

   >[!NOTE]
   >
   >日志编写器路径相对于 `crx-quickstart` 位置。
   >
   >因此，日志文件指定为：
   >
   >`logs/thelog.log`
   >
   >写入：
   >
   >`<cq-installation-dir>/crx-quickstart/logs/thelog.log`。
   >
   >以及指定为：
   >
   >`../logs/thelog.log`
   >
   >写入目录：
   >
   >`<cq-installation-dir>/logs/`\
   >(即在 `<cq-installation-dir>/crx-quickstart/`)

1. 仅当需要新的Writer时（即，使用与默认Writer不同的配置），才需要执行此步骤。

   >[!CAUTION]
   >
   >仅当现有默认值不适用时，才需要新的日志记录编写器配置。
   >
   >如果未配置显式写入程序，则系统将根据默认值自动生成隐式写入程序。

   下 `/apps/<project-name>/config`，为新建一个节点 [Apache Sling日志记录编写器配置](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingwriterconfigurationfactoryconfiguration)：

   * 名称： `org.apache.sling.commons.log.LogManager.factory.writer-<identifier>` （因为这是作家）

      和记录器一样， `<identifier>` 替换为（必须）输入以标识实例的自由文本（不能忽略此信息）。 例如，`org.apache.sling.commons.log.LogManager.factory.writer-MINE`

   * 类型: `sling:OsgiConfig`
   >[!NOTE]
   >
   >虽然不是技术要求，但建议将 `<identifier>` 独特。

   在此节点上设置以下属性：

   * 名称: `org.apache.sling.commons.log.file`

      类型: `String`

      值：指定“日志文件”，使其与“记录器”中指定的文件匹配；

      对于此示例， `../logs/myLogFile.log`.

   * 根据需要配置其他参数：

      * 名称: `org.apache.sling.commons.log.file.number`

         类型: `Long`

         值：指定要保留的日志文件数；例如， `5`

      * 名称: `org.apache.sling.commons.log.file.size`

         类型: `String`

         值：根据需要指定以大小/日期控制文件旋转；例如， `'.'yyyy-MM-dd`
   >[!NOTE]
   >
   >`org.apache.sling.commons.log.file.size` 通过设置以下任一值来控制日志文件的旋转：
   >
   >* 最大文件大小
   >* 时间/日期计划

   >
   >指示何时创建新文件（以及根据名称模式重命名现有文件）。
   >
   >* 可使用数字指定大小限制。 如果未指定大小指示器，则将此值视为字节数，或者您可以添加一个大小指示器 —  `KB`， `MB`，或 `GB` （忽略大小写）。
   >* 可将时间/日期计划指定为 `java.util.SimpleDateFormat` 模式。 这定义了文件旋转的时间段；还定义了附加到已旋转文件的后缀（用于标识）。

   >
   >默认为 &#39;.&#39;yyyy-MM-dd（用于每日日志轮换）。
   >
   >因此，例如，在2010年1月20日午夜（或准确显示之后的第一条日志消息时），../logs/error.log将重命名为../logs/error.log.2010-01-20。 1月21日的日志记录将输出到（一个新的和空的） ../logs/error.log ，直到该日志在下一次更改日期时滚动。
   >
   >| `'.'yyyy-MM` | 每月月初的轮换 |
   >|---|---|
   >| `'.'yyyy-ww` | 每周第一天的轮换（取决于区域设置）。 |
   >| `'.'yyyy-MM-dd` | 在每天的午夜轮换。 |
   >| `'.'yyyy-MM-dd-a` | 在每天的午夜和中午轮换。 |
   >| `'.'yyyy-MM-dd-HH` | 每小时顶部的旋转。 |
   >| `'.'yyyy-MM-dd-HH-mm` | 每分钟开头的旋转。 |
   >
   >注：指定时间/日期时：
   >
   >1. 您应该在一对单引号(“ ”)中“转义”文字文本；
      >
      >    这是为了避免某些字符被解释为模式字母。
   >
   >1. 在选项中的任意位置，仅使用允许用于有效文件名的字符。


1. 使用您选择的工具读取新日志文件。

   此示例创建的日志文件将为 `../crx-quickstart/logs/myLogFile.log`.

Felix控制台还提供了有关Sling日志支持的信息，位于 `../system/console/slinglog`；例如 `https://localhost:4502/system/console/slinglog`.

### 查找审核记录 {#finding-the-audit-records}

审核记录用以提供谁做了哪些工作及何时做了哪些工作的记录。 AEM WCM和OSGi事件会生成不同的审核记录。

#### 页面创作时显示的AEM WCM审核记录 {#aem-wcm-audit-records-shown-when-page-authoring}

1. 打开一个页面。
1. 从sidekick中，您可以选择带有锁图标的选项卡，然后双击 **审核日志……**
1. 此时将打开一个新窗口，显示当前页面的审核记录列表。

   ![screen_shot_2012-02-02at43601pm](assets/screen_shot_2012-02-02at43601pm.png)

1. 单击 **确定** 关闭窗口时。

#### AEM WCM审核存储库中的记录 {#aem-wcm-auditing-records-within-the-repository}

在 `/var/audit` 文件夹内，根据资源保存审计记录。 您可以向下展开，直至看到各个记录及其包含的信息。

这些条目包含的信息与编辑页面时显示的信息相同。

#### Web控制台中的OSGi审核记录 {#osgi-audit-records-from-the-web-console}

OSGi事件还会生成审核记录，这些记录可以从 **配置状态** 选项卡 — > **日志文件** 选项卡(在AEM Web控制台中)：

![screen_shot_2012-02-13at50346pm](assets/screen_shot_2012-02-13at50346pm.png)

## 监视复制代理 {#monitoring-your-replication-agents}

您可以监控 [复制队列](/help/sites-deploying/replication.md) 检测队列何时关闭或阻止 — 这反过来可能表明发布实例或外部系统有问题：

* 是否已启用所有必需的队列？
* 是否仍需要任何禁用的队列？
* 所有 `enabled` 队列应具有状态 `idle` 或 `active`，表示操作正常；不应有队列 `blocked`，这通常是接收器端出现问题的迹象。

* 如果队列的大小随时间增加，这可能表示队列被阻止。

监视复制代理：

1. 访问 **工具** AEM选项卡。
1. 单击&#x200B;**复制**。
1. 双击相应环境（左窗格或右窗格）的代理链接；例如 **作者代理**.

   生成的窗口将显示创作环境的所有复制代理的概述，包括其目标和状态。

1. 单击相应的代理名称（一个链接）以显示有关该代理的详细信息：

   ![chlimage_1](assets/chlimage_1.jpeg)

   在此编辑器中，您可以：

   * 查看代理是否已启用。
   * 查看任何复制的目标。
   * 查看复制队列当前是否处于活动状态（已启用）。
   * 查看队列中是否有任何项目。
   * **刷新** 或 **清除** 更新队列条目的显示；这有助于查看进入和离开队列的项目。

   * **查看日志** 用于访问复制代理执行的任何操作的日志。
   * **测试连接** 到目标实例。
   * **强制重试** 在任何队列项目上（如果需要）。

   >[!CAUTION]
   >
   >请不要在发布实例上对“反向复制发件箱”使用“测试连接”链接。
   >
   >如果为Outbox队列执行复制测试，则任何早于测试复制的项目都将通过每次反向复制重新处理。
   >
   >如果此类项目已存在于队列中，则可通过以下XPath JCR查询找到它们，应将其删除。
   >
   >`/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']`

同样，您可以开发一个解决方案来检测所有复制代理(位于 `/etc/replication/author` 或 `/etc/replication/publish`)，然后检查代理的状态( `enabled`， `disabled`)和基础队列( `active`， `idle`， `blocked`)。

## 监控性能 {#monitoring-performance}

[性能优化](/help/sites-deploying/configuring-performance.md) 是一个在开发过程中获得焦点的交互式进程。 部署后，通常会在特定时间间隔或事件后对其进行审查。

收集优化信息时使用的方法也可以用于持续监测。

>[!NOTE]
>
>特定 [可用于提高性能的配置](/help/sites-deploying/configuring-performance.md#configuring-for-performance) 也可以选中。

下面列出了出现的常见性能问题，以及如何发现和处理这些问题的建议。

| 区域 | 症状 | 增加容量…… | 减少数量…… |
|---|---|---|---|
| 客户端 | 高客户端CPU使用率。 | 安装更高性能的客户端CPU。 | 简化(HTML)布局。 |
|  | 服务器CPU使用率低。 | 升级到更快的浏览器。 | 改进客户端缓存。 |
|  | 有些客户速度很快，有些速度很慢。 |  |  |
| 服务器 |  |  |  |
| 网络 | 服务器和客户端的CPU使用率都较低。 | 消除所有网络瓶颈。 | 改进/优化客户端缓存的配置。 |
|  | 在服务器上本地浏览的速度（相对而言）比较快。 | 增加网络带宽。 | 减少网页的“重量”(例如，减少图像、优化的HTML)。 |
| Web服务器 | Web服务器上的CPU使用率很高。 | 将Web服务器群集起来。 | 减少每页的点击量（访问）。 |
|  |  | 使用硬件负载平衡器。 |  |
| 应用程序 | 服务器CPU使用率很高。 | 群集您的AEM实例。 | 搜索并消除CPU和内存缺陷（使用代码审查、计时输出等）。 |
|  | 内存消耗高。 |  | 改进所有级别的缓存。 |
|  | 响应时间短。 |  | 优化模板和组件（例如结构、逻辑）。 |
| 存储库 |  |  |  |
| 缓存 |  |  |  |

性能问题可能源自与您的网站无关的许多原因，包括连接速度暂时减慢、CPU负载等等。

它还可能影响您的所有访客或其中仅一部分访客。

您需要获取、排序和分析所有这些信息，然后才能优化常规性能或解决特定问题。

* 在您遇到性能问题之前：

   * 尽可能多的收集信息，以建立良好的系统正常工作时的知识

* 当您遇到性能问题时：

   * 尝试将其复制到一个（最好是多个）标准Web浏览器中，复制到您知道通用性能良好的其他客户端和/或服务器本身（如果可能）
   * 检查是否在适当的时空内更改了任何内容（与系统相关），以及这些更改中是否有任何更改影响了性能
   * 提出以下问题：

      * 问题是否只出现在特定时间？
      * 问题是否只出现在特定页面上？
      * 其他请求是否受到影响？
   * 收集尽可能多的信息，以便与您在正常情况下了解的系统进行比较：


### 用于监控和分析性能的工具 {#tools-for-monitoring-and-analyzing-performance}

下面简要概述了可用于监控和分析性能的一些工具。

其中某些组件将取决于您的操作系统。

<table>
 <tbody>
  <tr>
   <td>工具</td>
   <td>用于分析……</td>
   <td>使用情况/更多信息……</td>
  </tr>
  <tr>
   <td>request.log</td>
   <td>响应时间和并发性。</td>
   <td><a href="#interpreting-the-request-log">解释request.log</a>.</td>
  </tr>
  <tr>
   <td>桁架/桁架</td>
   <td>页面加载次数</td>
   <td><p>Unix/Linux命令用于跟踪系统调用和信号。 将日志级别提高至 <code>INFO</code>.</p> <p>分析每个请求的页面加载次数、哪些页面等。</p> </td>
  </tr>
  <tr>
   <td>线程转储</td>
   <td>观察JVM线程。 识别争用、锁定和长跑者。</td>
   <td><p>取决于操作系统：<br /> - Unix/Linux： <code>kill -QUIT &lt;<em>pid</em>&gt;</code><br /> - Windows（控制台模式）：Ctrl-Break<br /> </p> <p>还提供分析工具，例如 <a href="https://github.com/irockel/tda">TDA</a>.<br /> </p> </td>
  </tr>
  <tr>
   <td>栈转储</td>
   <td>内存不足问题导致性能降低。</td>
   <td><p>添加：<br /> <code>-XX:+HeapDumpOnOutOfMemoryError</code><br /> 选项调用的AEM。</p> <p>请参阅 <a href="https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/prepapp002.html#CEGBHDFH">“JVM疑难解答的选项/标记”页</a>.</p> </td>
  </tr>
  <tr>
   <td>系统调用</td>
   <td>确定计时问题。</td>
   <td><p>调用 <code>System.currentTimeMillis()</code> 或 <code>com.day.util</code>.计时用于从代码生成时间戳，也可以通过 <a href="#html-comments">HTML注释</a>.</p> <p><strong>注意：</strong> 应实施这些步骤，以便可以根据需要激活/停用它们；当系统顺利运行时，不需要收集统计信息的开销。</p> </td>
  </tr>
  <tr>
   <td>Apache Bench</td>
   <td>识别内存泄漏，有选择地分析响应时间。</td>
   <td><p>基本用法为：</p> <p><code>ab -k -n &lt;<em>requests</em>&gt; -c &lt;<em>concurrency</em>&gt; &lt;<em>url</em>&gt;</code></p> <p>参见 <a href="#apache-bench">Apache Bench</a> 和 <a href="https://httpd.apache.org/docs/2.4/programs/ab.html">ab手册页</a> 以了解完整的详细信息。</p> </td>
  </tr>
  <tr>
   <td>搜索分析</td>
   <td> </td>
   <td>脱机执行搜索查询，确定查询的响应时间，测试并确认结果集。<br /> </td>
  </tr>
  <tr>
   <td>JMet</td>
   <td>负载和功能测试。</td>
   <td><a href="https://jmeter.apache.org/">https://jmeter.apache.org/</a></td>
  </tr>
  <tr>
   <td>JProfiler</td>
   <td>深入的CPU和内存分析。</td>
   <td><a href="https://www.ej-technologies.com/">https://www.ej-technologies.com/</a></td>
  </tr>
  <tr>
   <td>Java Flight Recorder</td>
   <td>Java Flight Recorder (JFR)是一种用于收集有关正在运行的Java应用程序的诊断和性能分析数据的工具。</td>
   <td><a href="https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/tooldescr004.html#BABJJEEE">https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/tooldescr004.html#BABJJEEE</a></td>
  </tr>
  <tr>
   <td>JConsole</td>
   <td>观察JVM量度和线程。</td>
   <td><p>用法： jconsole</p> <p>参见 <a href="https://docs.oracle.com/javase/8/docs/technotes/guides/management/jconsole.html">jconsole</a> 和 <a href="#monitoring-performance-using-jconsole">使用JConsole监控性能</a>.</p> <p><strong>注意：</strong> 在JDK 1.8中，JConsole可通过插件进行扩展；例如，Top或TDA（线程转储分析器）。</p> </td>
  </tr>
  <tr>
   <td>Java VisualVM</td>
   <td>观察JVM量度、线程、内存和性能分析。</td>
   <td><p>用法： visualvm或visualvm<br /> </p> <p>参见 <a href="https://docs.oracle.com/javase/8/docs/technotes/guides/visualvm/">visualvm</a> 和 <a href="#monitoring-performance-using-j-visualvm">使用(J)VisualVM监控性能</a>.</p> <p><strong>注意：</strong> 在JDK 1.8中，VisualVM可通过插件进行扩展。 VisualVM在JDK 9之后停止使用。 请改用Java Flight Recorder。</p> </td>
  </tr>
  <tr>
   <td>桁架/桁架，lsof</td>
   <td>深入的内核调用和进程分析(Unix)。</td>
   <td>Unix/Linux命令。</td>
  </tr>
  <tr>
   <td>计时统计数据</td>
   <td>请参阅页面渲染的计时统计信息。</td>
   <td><p>要查看页面渲染的计时统计信息，您可以使用 <strong>Ctrl-Shift-U</strong> 与 <code>?debugClientLibs=true</code> 在URL中设置。</p> </td>
  </tr>
  <tr>
   <td>CPU和内存分析工具<br /> </td>
   <td><a href="#interpreting-the-request-log">在开发期间分析慢速请求时使用</a>.</td>
   <td>例如， <a href="https://www.yourkit.com/">您的Kit</a>. 或 <a href="https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/tooldescr004.html#BABJJEEE">Java Flight Recorder</a>.</td>
  </tr>
  <tr>
   <td><a href="#information-collection">信息收集</a></td>
   <td>安装的持续状态。</td>
   <td>尽可能多地了解您的安装还有助于您追查可能导致性能更改的原因以及这些更改是否合理。 需要定期收集这些量度，以便轻松查看重大更改。</td>
  </tr>
 </tbody>
</table>

### 解释request.log {#interpreting-the-request-log}

此文件注册有关向AEM发出的每个请求的基本信息。 由此可以得出有价值的结论。

此 `request.log` 提供了一个内置方式，用于了解请求需要多长时间。 对于开发目的，此函数应 `tail -f` 此 `request.log` 并留意缓慢的响应时间。 要分析更大的 `request.log` 我们推荐 [使用 `rlog.jar` 允许您对响应时间进行排序和过滤](#using-rlog-jar-to-find-requests-with-long-duration-times).

我们建议将“慢”页面与 `request.log`，然后单独对其进行调整以获得更好的性能。 这通常通过包含每个组件的性能指标或使用性能分析工具(例如 ` [yourkit](https://www.yourkit.com/)`.

#### 监测网站流量 {#monitoring-traffic-on-your-website}

请求日志记录发出的每个请求，以及发出的响应：

```xml
09:43:41 [66] -> GET /author/y.html HTTP/1.1
09:43:41 [66] <- 200 text/html 797ms
```

通过合计特定时段（例如，各种24小时时段）内的所有GET条目，您可以声明网站上的平均流量。

#### 使用request.log监控响应时间 {#monitoring-response-times-with-the-request-log}

请求日志是性能分析的良好起点：

`<cq-installation-dir>/crx-quickstart/logs/request.log`

日志如下所示（为了简单起见，这些行被缩短）：

```xml
31/Mar/2009:11:32:57 +0200 [379] -> GET /path/x HTTP/1.1
31/Mar/2009:11:32:57 +0200 [379] <- 200 text/html 33ms
31/Mar/2009:11:33:17 +0200 [380] -> GET /path/y HTTP/1.1
31/Mar/2009:11:33:17 +0200 [380] <- 200 application/json 39ms
```

此日志的每个请求或响应都有一行：

* 发出每个请求或响应的日期。
* 方括号中的请求编号。 此数字与请求和响应匹配。
* 指示这是请求（指向右侧的箭头）还是响应（指向左侧的箭头）的箭头。
* 对于请求，该行包含：

   * 方法(通常为GET、HEAD或POST)
   * 请求的页面
   * 协议

* 对于响应，该行包含：

   * 状态代码(200表示“成功”，404表示“页面未找到”
   * MIME类型
   * 响应时间

使用小型脚本，您可以从日志文件中提取所需信息并汇编所需的统计信息。 从这些页面中，您可以看到哪些页面或页面类型速度较慢，以及整体性能是否令人满意。

#### 使用request.log监控搜索响应时间 {#monitoring-search-response-times-with-the-request-log}

搜索请求也将在日志文件中注册：

```xml
31/Mar/2009:11:35:34 +0200 [338] -> GET /author/playground/en/tools/search.html?query=dilbert&size=5&dispenc=utf-8 HTTP/1.1
31/Mar/2009:11:35:34 +0200 [338] <- 200 text/html 1562ms
```

因此，如上所述，您可以使用脚本来提取相关信息并构建统计信息。

但是，确定响应时间后，您可能需要分析请求花费时间的原因，以及可以采取哪些措施来改进响应。

#### 监控并发用户的数量和影响 {#monitoring-the-number-and-impact-of-concurrent-users}

再次 `request.log` 可用于监测并发情况以及系统对并发情况的反应。

在出现负面影响之前，必须进行测试以确定系统可处理多少并发用户。 再次可使用脚本从日志文件中提取结果：

* 监测在特定时间范围（例如1分钟）内发出的请求数
* 测试特定数量的用户的影响，所有这些用户同时（尽可能接近）提出相同的请求；例如30个用户单击 **保存** 同时。

```xml
31/Mar/2009:11:45:29 +0200 [333] -> GET /author/libs/Personalize/content/statics.close.gif HTTP/1.1
31/Mar/2009:11:45:29 +0200 [334] -> GET /author/libs/Personalize/content/statics.detach.gif HTTP/1.1
31/Mar/2009:11:45:30 +0200 [335] -> GET /author/libs/CFC/content/imgs/logo.rZMNURccynWcTpCxyuBNiTCoiBMmw000.default.gif HTTP/1.1
31/Mar/2009:11:45:32 +0200 [335] <- 304 text/html 0ms
31/Mar/2009:11:45:33 +0200 [334] <- 200 image/gif 31ms
31/Mar/2009:11:45:38 +0200 [333] <- 200 image/gif 31ms
31/Mar/2009:11:45:42 +0200 [336] -> GET /author/libs/CFC/content/imgs/logo.rZMNURccynWcTZRXunQbbQtvuuCMbRRBuWXz0000.default.gif HTTP/1.1
31/Mar/2009:11:45:43 +0200 [337] -> GET /author/titlebar_bg.gif HTTP/1.1
31/Mar/2009:11:45:43 +0200 [336] <- 304 text/html 0ms
31/Mar/2009:11:45:44 +0200 [337] <- 304 text/html 0ms
```

### 使用rlog.jar查找持续时间较长的请求 {#using-rlog-jar-to-find-requests-with-long-duration-times}

AEM包括以下位置的各种辅助工具：
`<cq-installation-dir>/crx-quickstart/opt/helpers`

其中一个， `rlog.jar`，可用于快速排序 `request.log` 以便按持续时间（从最长到最短）显示请求。

以下命令显示可能的参数：

```shell
$java -jar rlog.jar
Request Log Analyzer Version 21584 Copyright 2005 Day Management AG
Usage:
  java -jar rlog.jar [options] <filename>
Options:
  -h               Prints this usage.
  -n <maxResults>  Limits output to <maxResults> lines.
  -m <maxRequests> Limits input to <maxRequest> requests.
  -xdev            Exclude POST request to CRXDE.
```

例如，您可以运行它并指定 `request.log` 文件，并显示持续时间最长的10个第一个请求：

```shell
$ java -jar ../opt/helpers/rlog.jar -n 10 request.log
*Info * Parsed 464 requests.
*Info * Time for parsing: 22ms
*Info * Time for sorting: 2ms
*Info * Total Memory: 1mb
*Info * Free Memory: 1mb
*Info * Used Memory: 0mb
------------------------------------------------------
     18051ms 31/Mar/2009:11:15:34 +0200 200 GET /content/geometrixx/en/company.html text/ html
      2198ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/cq/widgets.js application/x-javascript
      1981ms 31/Mar/2009:11:15:11 +0200 200 GET /libs/wcm/content/welcome.html text/html
      1973ms 31/Mar/2009:11:15:52 +0200 200 GET /content/campaigns/geometrixx.teasers..html text/html
      1883ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/security/cq-security.js application/x-javascript
      1876ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/tagging/widgets.js application/x-javascript
      1869ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/tagging/widgets/themes/default.js application/x-javascript
      1729ms 30/Mar/2009:16:45:56 +0200 200 GET /libs/wcm/content/welcome.html text/html; charset=utf-8
      1510ms 31/Mar/2009:11:15:34 +0200 200 GET /bin/wcm/contentfinder/asset/view.json/ content/dam?_dc=1238490934657&query=&mimeType=image&_charset_=utf-8 application/json
      1462ms 30/Mar/2009:17:23:08 +0200 200 GET /libs/wcm/content/welcome.html text/html; charset=utf-8
```

您可能需要关联个人 `request.log` 文件（如果您需要对大型数据示例执行此操作）。

### Apache Bench {#apache-bench}

为了最大程度地降低特殊情况（如垃圾收集等）的影响，建议使用这样的工具 `apachebench` (例如，请参阅 [ab](https://httpd.apache.org/docs/2.4/programs/ab.html) 以获取更多文档)，以帮助识别内存泄漏和有选择地分析响应时间。

Apache Bench可以通过以下方式使用：

```shell
$ ab -c 5 -k -n 1000 "https://localhost:4503/content/geometrixx/en/company.html"
This is ApacheBench, Version 2.3 <$Revision: 655654 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, https://www.zeustech.net/
Licensed to The Apache Software Foundation, https://www.apache.org/

Benchmarking localhost (be patient)
Completed 100 requests
Completed 200 requests
Completed 300 requests
Completed 400 requests
Completed 500 requests
Completed 600 requests
Completed 700 requests
Completed 800 requests
Completed 900 requests
Completed 1000 requests
Finished 1000 requests

Server Software: Day-Servlet-Engine/4.1.52
Server Hostname: localhost
Server Port: 4503

Document Path: /content/geometrixx/en/company.html
Document Length: 24127 bytes

Concurrency Level: 5
Time taken for tests: 69.766 seconds
Complete requests: 1000
Failed requests: 998
(Connect: 0, Receive: 0, Length: 998, Exceptions: 0)
Write errors: 0
Keep-Alive requests: 0
Total transferred: 24160923 bytes
HTML transferred: 24010923 bytes
Requests per second: 14.33 /sec (mean)
Time per request: 348.828 [ms] (mean)
Time per request: 69.766 [ms] (mean, across all concurrent requests)
Transfer rate: 338.20 [Kbytes/sec] received

Connection Times (ms)
min mean[+/-sd] median max
Connect: 0 1 3.9 0 58
Processing: 138 347 568.5 282 8106
Waiting: 137 344 568.1 281 8106
Total: 139 348 568.4 283 8106

Percentage of the requests served within a certain time (ms)
50% 283
66% 323
75% 356
80% 374
90% 439
95% 512
98% 1047
99% 1132
100% 8106 (longest request)
```

上述数字取自访问geometrixx公司页面的标准MAcBook Pro笔记本电脑（2010年年中），如默认AEM安装中所包含。 页面非常简单，但并未针对性能进行优化。

`apachebench` 还显示所有并发请求中每个请求的平均时间；请参阅 `Time per request: 54.595 [ms]` （所有并发请求中的平均值）。 您可以更改并发参数的值 `-c` （一次要执行的多个请求数）以查看任何效果。

### 请求计数器 {#request-counters}

有关请求流量（特定时间段内的请求数）的信息可让您指示实例上的负载。 此信息可以提取自 [request.log](#interpreting-the-request-log)，但使用计数器将会自动收集数据，让您看到：

* 活动方面的显着差异（即区分“许多请求”和“低活动”）
* 当实例未被使用时
* 任何重新启动（计数器将重置为0）

要自动收集信息，您还可以安装RequestFilter以在每个请求上递增一个计数器。 多个计数器可用于不同的时间段。

收集的信息可用于指示：

* 活动发生重大变化
* 冗余实例
* 任何重新启动（计数器重置为0）

### HTML注释 {#html-comments}

建议每个项目都包含 `html comments` 提高服务器性能。 可以找到许多很好的公共示例；选择一个页面，打开页面源进行查看并滚动到底部，可以看到以下代码：

```xml
</body>
 </html>
        <!--
        Page took 58 milliseconds to be rendered by server
         -->
```

### 使用JConsole监控性能 {#monitoring-performance-using-jconsole}

刀具命令 `jconsole` 可用于JDK。

1. 启动AEM实例。
1. 运行 `jconsole.`
1. 选择您的AEM实例并 **Connect**.

1. 从 `Local` 应用程序，双击 `com.day.crx.quickstart.Main`；概述将显示为默认设置：

   ![chlimage_1-1](assets/chlimage_1-1.png)

   之后，您可以选择其他选项。

### 使用(J)VisualVM监控性能 {#monitoring-performance-using-j-visualvm}

对于JDK 6-8，使用工具命令 `visualvm` 可用。 安装JDK后，您可以：

1. 启动AEM实例。

   >[!NOTE]
   >
   >如果使用Java 5，您可以添加 `-Dcom.sun.management.jmxremote` 启动JVM的java命令行的参数。 Java 6默认启用JMX。

1. 运行以下任一项：

   * `jvisualvm`：在JDK 1.6 bin文件夹中（已测试版本）
   * `visualvm`：可以从中下载 [VisualVM](https://docs.oracle.com/javase/8/docs/technotes/guides/visualvm/) （出血边缘版本）

1. 从 `Local` 应用程序，双击 `com.day.crx.quickstart.Main`；概述将显示为默认设置：

   ![chlimage_1-2](assets/chlimage_1-2.png)

   之后，您可以选择其他选项，包括“监视器”：

   ![chlimage_1-3](assets/chlimage_1-3.png)

您可以使用此工具生成线程转储和内存头转储。 技术支持团队经常要求提供此信息。

### 信息收集 {#information-collection}

尽可能多地了解您的安装情况可以帮助您追查可能导致性能更改的原因以及这些更改是否合理。 需要定期收集这些量度，以便轻松查看重大更改。

以下信息可能会很有用：

* [有多少作者正在使用该系统？](#how-many-authors-are-working-with-the-system)
* [每天的平均页面激活数是多少？](#what-is-the-average-number-of-page-activations-per-day)
* [您当前在此系统上维护多少个页面？](#how-many-pages-do-you-currently-maintain-on-this-system)
* [如果您使用MSM，则每月平均转出次数是多少？](#if-you-use-msm-what-is-the-average-number-of-rollouts-per-month)
* [每月平均活动副本数是多少？](#what-is-the-average-number-of-live-copies-per-month)
* [如果您使用AEM Assets，则您当前在Assets中维护多少项资源？](#ifyouusecqdamhowmanyassetsdoyoucurrentlymaintainincqdam)
* [资产的平均大小是多少？](#what-is-the-average-size-of-the-assets)
* [当前使用了多少个模板？](#how-many-templates-are-currently-used)
* [当前使用了多少个组件？](#how-many-components-are-currently-used)
* [在峰值时间，您每小时在创作系统上有多少请求？](#how-many-requests-per-hour-do-you-have-on-the-author-system-at-peak-time)
* [在峰值时间，您每小时在发布系统上有多少请求？](#how-many-requests-per-hour-do-you-have-on-the-publish-system-at-peak-time)

#### 有多少作者正在使用该系统？ {#how-many-authors-are-working-with-the-system}

要查看自安装以来使用系统的作者数量，请使用命令行：

```shell
cd <cq-installation-dir>/crx-quickstart/logs
cut -d " " -f 3 access.log | sort -u | wc -l
```

要查看在给定日期工作的作者数量，请执行以下操作：

```shell
grep "<date>" access.log | cut -d " " -f 3 | sort -u | wc -l
```

#### 每天的平均页面激活数是多少？ {#what-is-the-average-number-of-page-activations-per-day}

要查看自服务器安装以来页面激活的总次数，请使用存储库查询；通过CRXDE — 工具 — 查询：

* **类型** `XPath`

* **路径** `/`

* **查询** `//element(*, cq:AuditEvent)[@cq:type='Activate']`

然后，计算自安装以来经过的天数来计算平均值。

#### 您当前在此系统上维护多少个页面？ {#how-many-pages-do-you-currently-maintain-on-this-system}

要查看服务器上当前页数，请使用存储库查询；通过CRXDE — 工具 — 查询：

* **类型** `XPath`

* **路径** `/`

* **查询** `//element(*, cq:Page)`

#### 如果您使用MSM，则每月平均转出次数是多少？ {#if-you-use-msm-what-is-the-average-number-of-rollouts-per-month}

要确定自安装以来的转出总数，请使用存储库查询；通过CRXDE — 工具 — 查询：

* **类型** `XPath`

* **路径** `/`

* **查询** `//element(*, cq:AuditEvent)[@cq:type='PageRolledOut']`

计算安装后经过的月数以计算平均值。

#### 每月平均活动副本数是多少？ {#what-is-the-average-number-of-live-copies-per-month}

要确定自安装以来创建的活动副本总数，请使用存储库查询；通过CRXDE — 工具 — 查询：

* **类型** `XPath`

* **路径** `/`

* **查询** `//element(*, cq:LiveSyncConfig)`

再次使用安装后经过的月数来计算平均值。

#### 如果您使用AEM Assets，则您当前在Assets中维护多少项资源？ {#if-you-use-aem-assets-how-many-assets-do-you-currently-maintain-in-assets}

要查看您当前维护的DAM资产数量，请使用存储库查询；通过CRXDE — 工具 — 查询：

* **类型** `XPath`
* **路径** `/`
* **查询** `/jcr:root/content/dam//element(*, dam:Asset)`

#### 资产的平均大小是多少？ {#what-is-the-average-size-of-the-assets}

要确定 `/var/dam` 文件夹：

1. 使用WebDAV将存储库映射到本地文件系统。

1. 使用命令行：

   ```shell
   cd /Volumes/localhost/var
   du -sh dam/
   ```

   要获取平均大小，请将全局大小除以中的资源总数 `/var/dam` （参见上文）。

#### 当前使用了多少个模板？ {#how-many-templates-are-currently-used}

要查看当前服务器上模板的数量，请使用存储库查询；通过CRXDE — 工具 — 查询：

* **类型** `XPath`
* **路径** `/`
* **查询** `//element(*, cq:Template)`

#### 当前使用了多少个组件？ {#how-many-components-are-currently-used}

要查看当前服务器上组件的数量，请使用存储库查询；通过CRXDE — 工具 — 查询：

* **类型** `XPath`
* **路径** `/`
* **查询** `//element(*, cq:Component)`

#### 在峰值时间，您每小时在创作系统上有多少请求？ {#how-many-requests-per-hour-do-you-have-on-the-author-system-at-peak-time}

要确定在峰值时间创作系统上每小时的请求数，请执行以下操作：

1. 要确定自安装以来的请求总数，请使用命令行：

   ```shell
   cd <cq-installation-dir>/crx-quickstart/logs
   grep -R "\->" request.log | wc -l
   ```

1. 要确定起始日期和终止日期，请执行以下操作：

   ```shell
   vim request.log
   G / 1G: for the last/first lines
   ```

   使用这些值可计算自安装以来经过的小时数，以及每小时的平均请求数。

#### 在峰值时间，您每小时在发布系统上有多少请求？ {#how-many-requests-per-hour-do-you-have-on-the-publish-system-at-peak-time}

在发布实例上重复上述过程。

## 分析特定方案 {#analyzing-specific-scenarios}

下面列出了一些建议，说明如果开始遇到某些性能问题，应检查哪些内容。 这份清单（不幸的是）并不完整。

>[!NOTE]
>
>有关更多信息，另请参阅以下文章：
>
>* [线程转储](https://helpx.adobe.com/experience-manager/kb/TakeThreadDump.html)
>* [分析内存问题](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)
>* [使用内置探查器分析](https://helpx.adobe.com/experience-manager/kb/AnalyzeUsingBuiltInProfiler.html)
>* [分析缓慢进程和受阻进程](https://helpx.adobe.com/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)
>


### CPU为100% {#cpu-at}

如果系统的CPU一直以100%的速度运行，请参阅：

* 知识库：

   * [分析慢速进程和受阻进程](https://helpx.adobe.com/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)

### 内存不足 {#out-of-memory}

尽管此类错误应在开发和测试期间检测到，但某些场景可能会漏过。

如果您的系统内存不足，可以通过多种方式看到这种情况，包括性能下降和错误消息，包括潜文：

`java.lang.OutOfMemoryError`

在这些情况下，请检查：

* JVM设置用于 [启动AEM](/help/sites-deploying/deploy.md#getting-started)
* 知识库：

   * [分析内存问题](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)

### 磁盘I/O {#disk-i-o}

如果您的系统磁盘空间不足，或者您注意到开始出现磁盘抖动，请参阅：

* 是否禁用了调试信息收集；这可以在多个位置进行配置，包括：

   * [Apache Sling JSP脚本处理程序](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjspscripthandler)
   * [Apache Sling Java脚本处理程序](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjavascripthandler)
   * [Apache Sling日志记录配置](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration)
   * [CQHTML库管理器](/help/sites-deploying/osgi-configuration-settings.md#daycqhtmllibrarymanager)
   * [CQ WCM调试过滤器](/help/sites-deploying/osgi-configuration-settings.md#daycqwcmdebugfilter)
   * [记录器](/help/sites-deploying/monitoring-and-maintaining.md#activating-the-debug-log-level)

* 是否以及如何配置 [版本清除](/help/sites-deploying/version-purging.md)
* 知识库：

   * [打开的文件过多](https://helpx.adobe.com/experience-manager/kb/TooManyOpenFiles.html)
   * [日志占用太多磁盘空间](https://helpx.adobe.com/experience-manager/kb/JournalTooMuchDiskSpace.html)

### 性能定期下降 {#regular-performance-degradation}

如果在每次重新启动后（有时为一周或更长时间）发现实例性能下降，则可以检查以下内容：

* [内存不足](#outofmemory)
* 知识库：

   * [未关闭的会话](https://helpx.adobe.com/experience-manager/kb/AnalyzeUnclosedSessions.html)

### JVM调整 {#jvm-tuning}

Java虚拟机(JVM)在调整方面有显着改进（尤其是自Java 7以来）。 因此，指定合理的固定JVM大小并使用默认值通常是合适的。

如果默认设置不适用，则在尝试调整JVM之前，必须建立一个监测和评估GC性能的方法；这可能涉及监测因素，包括栈大小、算法和其他方面。

一些常见选项包括：

* VerboseGC：

   ```
   -verbose:gc \
    -Xloggc:$LOGS/verbosegc.log \
    -XX:+PrintGCDetails \
    -XX:+PrintGCDateStamps
   ```

生成的日志可由GC可视化器摄取，例如：

` [https://www.ibm.com/developerworks/library/j-ibmtools2/](https://www.ibm.com/developerworks/library/j-ibmtools2/)`

或JConsole：

* 这些设置适用于“宽打开”的JMX连接：

   ```
   -Dcom.sun.management.jmxremote \
    -Dcom.sun.management.jmxremote.port=8889 \
    -Dcom.sun.management.jmxremote.authenticate=false \
    -Dcom.sun.management.jmxremote.ssl=false
   ```

* 然后使用JConsole连接到JVM；请参阅：
   ` [https://docs.oracle.com/javase/8/docs/technotes/guides/management/jconsole.html](https://docs.oracle.com/javase/8/docs/technotes/guides/management/jconsole.html)`

这将帮助您了解使用了多少内存、使用了哪些GC算法、运行它们需要多长时间，以及这对于应用程序性能有何影响。 如果没有这些，调整就只是“随机转动的旋钮”。

>[!NOTE]
>
>对于Oracle的VM，还可以在以下位置找到相关信息：
>
>[https://docs.oracle.com/javase/8/docs/technotes/guides/vm/server-class.html](https://docs.oracle.com/javase/8/docs/technotes/guides/vm/server-class.html)
