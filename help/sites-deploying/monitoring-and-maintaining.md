---
title: 监控和维护AEM实例
seo-title: 监控和维护AEM实例
description: 了解如何监控AEM。
seo-description: 了解如何监控AEM。
uuid: 14466552-5c92-4730-a427-85675a2b121c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 5d2364b7-4497-4f8b-85ef-6e780bfb8c36
docset: aem65
feature: 配置
exl-id: d3375935-090d-4052-8234-68ef4ddbab6a
source-git-commit: 83383d46a4200eb3d21deee15c71032314694860
workflow-type: tm+mt
source-wordcount: '5878'
ht-degree: 0%

---

# 监控和维护AEM实例{#monitoring-and-maintaining-your-aem-instance}

部署AEM实例后，将需要某些任务来监控和维护其操作、性能和完整性。

这里的一个关键因素是，要识别潜在问题，您需要知道系统在正常情况下的外观和行为。 最好通过监控系统并收集一段时间内的信息来实现这一点。

| 检查 | 注意事项 | 评论/操作 |
|---|---|---|
| 备份计划。 |  | 请参阅如何[备份实例](/help/sites-deploying/monitoring-and-maintaining.md#backups)。 |
| 灾难恢复计划。 | 贵公司的灾难恢复准则。 |  |
| 错误跟踪系统可用于报告问题。 | 例如，[bugzilla](https://www.bugzilla.org/)、[jira](https://www.atlassian.com/software/jira/)或许多其他中的一个。 |  |
| 正在监控文件系统。 | 如果可用磁盘空间不足，CRX存储库将“冻结”。 当空间可用时，它将恢复。 | 可用空间变低时，日志文件中会显示“ `*ERROR* LowDiskSpaceBlocker`”消息。 |
| [正在](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) 监控日志文件。 |  |  |
| 系统监视（持续）在后台运行。 | 包括CPU、内存、磁盘和网络使用情况。 例如，使用iostat / vmstat / perfmon。 | 记录的数据是可视化的，可用于跟踪性能问题。 也可以访问原始数据。 |
| [正在监控AEM性能](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance)。 | 包括[请求计数器](/help/sites-deploying/monitoring-and-maintaining.md#request-counters)以监控流量级别。 | 如出现重大或长期业绩损失，应进行详细调查。 |
| 您正在监控[复制代理](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-your-replication-agents)。 |  |  |
| 定期清除工作流实例。 | 存储库大小和工作流性能。 | 请参阅[定期清除工作流实例](/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances)。 |

## 备份 {#backups}

备份以下内容是最佳做法：

* 您的软件安装 — 在对配置进行重大更改之前/之后
* 存储库中保存的内容 — 定期

贵公司可能会有一个备份策略，您需要遵循该策略，有关备份内容和备份时间的其他考虑事项包括：

* 系统和数据的重要性。
* 软件或数据发生更改的频率。
* 数据量；容量有时可能是问题，执行备份所需的时间也是问题。
* 用户在线时，是否可以进行备份；如果可能，性能会受到什么影响。
* 用户的地理分布；例如，何时是备份的最佳时间（以最大限度地减少影响）？
* 您的灾难恢复政策；有关必须存储备份数据的位置（例如站外、特定介质等）的准则。

通常，完整备份是定期进行（如每日、每周或每月），增量备份介于之间（如每小时、每天或每周）。

>[!CAUTION]
>
>在实施生产实例的备份时，必须&#x200B;*进行测试，以确保能够成功还原备份。*
>
>如果没有这一点，备份就可能毫无用处（最坏的情况）。

>[!NOTE]
>
>有关备份性能的更多信息，请阅读[备份性能](/help/sites-deploying/configuring-performance.md#backup-performance)一节。

### 备份软件安装 {#backing-up-your-software-installation}

安装后或对配置进行重大更改后，请备份软件安装。

为此，您需要[备份整个存储库](#backing-up-your-repository)，然后：

1. 停止AEM。
1. 从文件系统备份整个`<cq-installation-dir>`。

>[!CAUTION]
>
>如果您运行的是第三方应用程序服务器，则其他文件夹可能位于其他位置，并且可能还需要备份。 请参阅[如何使用应用程序服务器](/help/sites-deploying/application-server-install.md)安装AEM ，以了解有关安装应用程序服务器的信息。

>[!CAUTION]
>
>支持文件数据存储的增量备份；对其他组件（如Lucene索引）使用增量备份时，请确保已删除的文件也在备份中标记为已删除。

>[!NOTE]
>
>磁盘镜像也可以用作备份机制。

### 备份存储库 {#backing-up-your-repository}

CRX文档的[备份和还原](/help/sites-administering/backup-and-restore.md)部分涵盖与CRX存储库备份相关的所有问题。

有关进行在线“热”备份的完整详细信息，请参阅[创建在线备份](/help/sites-administering/backup-and-restore.md#online-backup)。

## 版本清除 {#version-purging}

**清除版本**&#x200B;工具用于清除存储库中节点或节点层次结构的版本。 其主要目的是通过删除节点的旧版本来帮助您减小存储库的大小。

本节介绍与AEM的版本控制功能相关的维护操作。 **清除版本**&#x200B;工具用于清除存储库中节点或节点层次结构的版本。 其主要目的是通过删除节点的旧版本来帮助您减小存储库的大小。

### 概述 {#overview}

**清除版本**&#x200B;工具](/help/sites-administering/tools-consoles.md)控制台&#x200B;**下的**&#x200B;版本控制&#x200B;**下提供了**[&#x200B;清除版本工具，或直接从以下位置获取：

`https://<server>:<port>/etc/versioning/purge.html`

![screen_shot_2012-03-15at14418pm](assets/screen_shot_2012-03-15at14418pm.png)

**开始** 路径必须完成清除的绝对路径。您可以通过单击存储库树导航器来选择开始路径。

**** 递归清除数据时，您可以选择对一个节点执行操作，还是通过选择“递归”对整个层次结构执行操作。在最后一种情况下，给定路径定义层级的根节点。

**要保留的** 最大版本要保留的节点最大版本数。当这些数字超过此值时，将清除最早的版本。

**最大版** 本年龄节点版本的最大年龄。当版本的年龄超过此值时，会清除该值。

**干式** 运行由于删除内容的版本是确定的，并且在不恢复备份的情况下无法还原，因此清除版本工具提供了一种干式运行模式，允许您预览已清除的版本。要启动清除流程的干式运行，请单击“干式运行”。

**** 清除启动对“开始路径”定义的节点上的版本的清除。

### 清除网站的版本 {#purging-versions-of-a-web-site}

要清除网站的版本，请按如下步骤操作：

1. 导航到&#x200B;**[工具](/help/sites-administering/tools-consoles.md)** **控制台**，选择&#x200B;**版本控制**&#x200B;并双击&#x200B;**清除版本。**
1. 设置要清除的内容的开始路径(例如，`/content/geometrixx-outdoors`)。

   * 如果只想清除路径定义的节点，请取消选择&#x200B;**Recursive**。
   * 如果要清除路径及其子代定义的节点，请选择&#x200B;**Recursive**。

1. 设置要保留的最大版本数（针对每个节点）。 将留空，以不使用此设置。

1. 设置要保留的最大版本年龄（每个节点），以天为单位。 将留空，以不使用此设置。

1. 单击&#x200B;**干法运行**&#x200B;以预览清除过程将执行的操作。
1. 单击&#x200B;**清除**&#x200B;以启动该进程。

>[!CAUTION]
>
>如果不恢复存储库，则无法恢复已清除的节点。 您应该处理配置，因此我们建议您始终在清除之前执行练习。

### 分析控制台 {#analyzing-the-console}

**Dry Run**&#x200B;和&#x200B;**Purge**&#x200B;进程列出已处理的所有节点。 在此过程中，节点可能具有以下状态之一：

* `ignore (not versionnable)`:该节点不支持版本控制，在过程中会忽略该节点。

* `ignore (no version)`:该节点没有任何版本，在过程中会被忽略。

* `retained`:未清除该节点。
* `purged`:节点已清除。

此外，控制台还提供了有关这些版本的有用信息：

* `V 1.0`:版本号。
* `V 1.0.1`*:星形指示版本为当前版本。

* `Thu Mar 15 2012 08:37:32 GMT+0100`:版本的日期。

在下一个示例中：

* 已清除&#x200B;**[!DNL Shirts]**&#x200B;版本，因为其版本年龄超过2天。
* 将清除&#x200B;**[!DNL Tonga Fashions!]**&#x200B;版本，因为其版本数大于5。

![global_version_screenshot](assets/global_version_screenshot.png)

## 使用审核记录和日志文件 {#working-with-audit-records-and-log-files}

与Adobe Experience Manager(AEM)相关的审核记录和日志文件可以在不同位置找到。 下面提供了您可以在何处查找内容的概述。

### 使用日志 {#working-with-logs}

AEM WCM记录详细日志。 在解包并启动快速入门后，您可以在中找到日志：

* `<cq-installation-dir>/crx-quickstart/logs/`

* `<cq-installation-dir>/crx-quickstart/repository/`

#### 日志文件旋转 {#log-file-rotation}

日志文件旋转是指通过定期创建新文件来限制文件增长的过程。 在AEM中，名为`error.log`的日志文件将根据给定规则每天旋转一次：

* 将根据模式{originalfilename} `.yyyy-MM-dd`重命名`error.log`文件。 例如，在2010年7月11日，当前日志文件被重命名为`error.log-2010-07-10`，然后创建新的`error.og`。

* 以前的日志文件不会被删除，因此您有责任定期清理旧的日志文件以限制磁盘的使用。

>[!NOTE]
>
>如果升级AEM安装，请注意，AEM不再使用的任何现有日志文件都将保留在磁盘上。 你可以不冒险地删除它们。 所有新日志条目都将写入新日志文件中。

### 查找日志文件 {#finding-the-log-files}

安装了AEM的文件服务器上保存了各种日志文件：

* `<cq-installation-dir>/crx-quickstart/logs`

   * `access.log`
此处注册了对AEM WCM和存储库的所有访问请求。

   * `audit.log`
审核操作在此处注册。

   * `error.log`
此处将注册错误消息（严重性级别不同）。

   * [ `ImageServer-<PortId>-yyyy>-<mm>-<dd>.log`](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/config-admin/server-logging/c-image-server-log.html)
此日志仅在启用时 [!DNL Dynamic Media] 使用。它提供用于分析内部ImageServer进程行为的统计和分析信息。

   * `request.log`
每个访问请求都将随响应一起注册。

   * [ `s7access-<yyyy>-<mm>-<dd>.log`](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/config-admin/server-logging/c-access-log.html)
此日志仅在启用时 [!DNL Dynamic Media] 使用。s7access日志记录通过`/is/image`和`/is/content`对[!DNL Dynamic Media]发出的每个请求。

   * `stderr.log`
保存在启动期间生成的、严重性级别不同的错误消息。默认情况下，日志级别设置为 
`Warning` ( `WARN`)

   * `stdout.log`
保存指示启动期间事件的日志记录消息。

   * `upgrade.log`
提供从 
`com.day.compat.codeupgrade` 和 `com.adobe.cq.upgradesexecutor` 包。

* `<cq-installation-dir>/crx-quickstart/repository`

   * `revision.log`
修订日志信息。

>[!NOTE]
>
>从**system/console/status-Bundlist **页面生成的**Download Full **包中未包含ImageServer和s7access日志。 出于支持目的，如果您遇到[!DNL Dynamic Media]问题，请在联系客户支持团队时还附加ImageServer和s7access日志。

### 激活DEBUG日志级别 {#activating-the-debug-log-level}

默认日志级别（[Apache Sling日志记录配置](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration)）为“信息”，因此调试消息不会被记录。

要激活日志记录器的调试日志级别，请将属性`org.apache.sling.commons.log.level`设置为在存储库中进行调试。 例如，在`/libs/sling/config/org.apache.sling.commons.log.LogManager`上配置[全局Apache Sling日志记录](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration)。

>[!CAUTION]
>
>不要将日志保留在调试日志级别，因为它会生成大量日志条目，从而消耗资源。

调试文件中的行通常以DEBUG开头，然后提供日志级别、安装程序操作和日志消息。 例如：

```shell
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

日志级别如下：

| 0 | 致命错误 | 操作失败，安装程序无法继续。 |
|---|---|---|
| 1 | 错误 | 操作失败。 安装将继续，但部分AEM WCM未正确安装，无法正常工作。 |
| 2 | 警告 | 操作已成功，但遇到问题。 AEM WCM可能正常工作，也可能无法正常工作。 |
| 3 | 信息 | 操作成功。 |

### 创建自定义日志文件 {#create-a-custom-log-file}

>[!NOTE]
>
>使用Adobe Experience Manager时，可通过多种方法来管理此类服务的配置设置；有关更多详细信息和建议的实践，请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md) 。

在某些情况下，您可能希望创建具有不同日志级别的自定义日志文件。 您可以在存储库中通过以下方式执行此操作：

1. 如果尚未存在，请为项目`/apps/<project-name>/config`创建新的配置文件夹(`sling:Folder`)。
1. 在`/apps/<project-name>/config`下，为新的[Apache Sling日志记录器配置](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingloggerconfigurationfactoryconfiguration)创建节点：

   * 名称：`org.apache.sling.commons.log.LogManager.factory.config-<identifier>`（因为这是日志记录器）

      其中， `<identifier>`被替换为您（必须）输入以标识实例的自由文本（您不能忽略此信息）。

      例如，`org.apache.sling.commons.log.LogManager.factory.config-MINE`

   * 类型: `sling:OsgiConfig`
   >[!NOTE]
   >
   >虽然不是技术要求，但建议将`<identifier>`设为唯一。

1. 在此节点上设置以下属性：

   * 名称: `org.apache.sling.commons.log.file`

      类型：字符串

      值：指定日志文件；例如，`logs/myLogFile.log`

   * 名称: `org.apache.sling.commons.log.names`

      类型：字符串[]（字符串+多个）

      值：指定记录器要为其记录消息的OSGi服务；例如，以下所有内容：

      * `org.apache.sling`
      * `org.apache.felix`
      * `com.day`
   * 名称: `org.apache.sling.commons.log.level`

      类型：字符串

      值：指定所需的日志级别（`debug`、`info`、`warn`或`error`）；例如`debug`

   * 根据需要配置其他参数：

      * 名称: `org.apache.sling.commons.log.pattern`

         类型: `String`

         值：根据需要指定日志消息的模式；例如，

         `{0,date,dd.MM.yyyy HH:mm:ss.SSS} *{4}* [{2}] {3} {5}`
   >[!NOTE]
   >
   >`org.apache.sling.commons.log.pattern` 最多支持六个参数。
   >
   >{0}类型`java.util.Date`的时间戳
   >
   >{1}日志标记
   >
   >{2}当前线程的名称
   >
   >{3}日志记录器的名称
   >
   >{4}日志级别
   >
   >{5}日志消息
   >
   >如果日志调用包含`Throwable` ，则堆栈跟踪会附加到消息中。

   >[!CAUTION]
   >
   >org.apache.sling.commons.log.names必须具有值。

   >[!NOTE]
   >
   >日志写入程序路径与`crx-quickstart`位置相关。
   >
   >因此，指定为：
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
   >（即`<cq-installation-dir>/crx-quickstart/`旁）

1. 只有在需要新写入程序时（即配置与默认写入程序不同时），才需要执行此步骤。

   >[!CAUTION]
   >
   >只有当现有的默认值不合适时，才需要新的日志记录写入器配置。
   >
   >如果未配置显式写入器，则系统将根据默认值自动生成隐式写入器。

   在`/apps/<project-name>/config`下，为新的[Apache Sling日志记录编写器配置](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingwriterconfigurationfactoryconfiguration)创建一个节点：

   * 名称：`org.apache.sling.commons.log.LogManager.factory.writer-<identifier>`（因为这是Writer）

      与日志记录器一样， `<identifier>`被替换为您（必须）输入用来标识实例的自由文本（您不能忽略此信息）。 例如，`org.apache.sling.commons.log.LogManager.factory.writer-MINE`

   * 类型: `sling:OsgiConfig`
   >[!NOTE]
   >
   >虽然不是技术要求，但建议将`<identifier>`设为唯一。

   在此节点上设置以下属性：

   * 名称: `org.apache.sling.commons.log.file`

      类型: `String`

      值：指定日志文件，使其与日志记录器中指定的文件匹配；

      对于此示例， `../logs/myLogFile.log`。

   * 根据需要配置其他参数：

      * 名称: `org.apache.sling.commons.log.file.number`

         类型: `Long`

         值：指定要保留的日志文件数；例如，`5`

      * 名称: `org.apache.sling.commons.log.file.size`

         类型: `String`

         值：按大小/日期指定控制文件旋转的所需条件；例如，`'.'yyyy-MM-dd`
   >[!NOTE]
   >
   >`org.apache.sling.commons.log.file.size` 通过设置以下任一项来控制日志文件的旋转：
   >
   >* 最大文件大小
   >* 时间/日期计划

   >
   >以指示何时将创建新文件（以及根据名称模式重命名的现有文件）。
   >
   >* 可以使用数字指定大小限制。 如果未提供大小指示器，则将其视为字节数，或者可以添加大小指示器之一 — `KB`、 `MB`或`GB`（忽略大小写）。
   >* 时间/日期计划可以指定为`java.util.SimpleDateFormat`模式。 这定义文件旋转的时间段；还附加到旋转文件的后缀（用于标识）。

   >
   >默认为 &#39;.&#39;yyyy-MM-dd（用于每日日志旋转）。
   >
   >例如，在2010年1月20日的午夜（或当发生此事件后的第一条日志消息更加准确时），../logs/error.log将重命名为../logs/error.log.2010-01-20。 1月21日的日志记录将输出到（新的空）../logs/error.log ，直到在下一天的更改时对其进行滚动。
   >
   >| `'.'yyyy-MM` | 每月初的轮换 |
   >|---|---|
   >| `'.'yyyy-ww` | 每周第一天轮转（取决于区域设置）。 |
   >| `'.'yyyy-MM-dd` | 每天午夜轮调。 |
   >| `'.'yyyy-MM-dd-a` | 每天午夜和中午轮流。 |
   >| `'.'yyyy-MM-dd-HH` | 每小时的顶部旋转一次。 |
   >| `'.'yyyy-MM-dd-HH-mm` | 每分钟开始轮转。 |
   >
   >注意：指定时间/日期时：
   > 1. 应该对单引号(“ ”)中的文本进行“转义”；
      >
      >     
      这是为了避免某些字符被解释为模式字母。
      >
      >  
   1. 在选项中的任意位置，只允许对有效文件名使用允许的字符。


1. 使用所选工具读取新的日志文件。

   此示例创建的日志文件将为`../crx-quickstart/logs/myLogFile.log`。

Felix控制台还在`../system/console/slinglog`提供了有关Sling日志支持的信息；例如`https://localhost:4502/system/console/slinglog`。

### 查找审核记录 {#finding-the-audit-records}

保留审计记录，以提供谁执行了什么和何时执行的记录。 会为AEM WCM和OSGi事件生成不同的审核记录。

#### AEM在页面创作时显示的WCM审核记录 {#aem-wcm-audit-records-shown-when-page-authoring}

1. 打开页面。
1. 在Sidekick中，您可以选择带有锁定图标的选项卡，然后双击&#x200B;**审核日志……**
1. 将打开一个新窗口，显示当前页面的审核记录列表。

   ![screen_shot_2012-02-02at43601pm](assets/screen_shot_2012-02-02at43601pm.png)

1. 要关闭窗口时，单击&#x200B;**确定**。

#### AEM WCM存储库内的审核记录 {#aem-wcm-auditing-records-within-the-repository}

在`/var/audit`文件夹中，会根据资源保留审核记录。 您可以向下展开，直到您看到单个记录及其包含的信息为止。

这些条目包含的信息与编辑页面时显示的信息相同。

#### Web控制台中的OSGi审核记录 {#osgi-audit-records-from-the-web-console}

OSGi事件还会生成审核记录，这些记录可从AEM Web控制台的&#x200B;**配置状态**&#x200B;选项卡 — > **日志文件**&#x200B;选项卡中查看：

![screen_shot_2012-02-13at50346pm](assets/screen_shot_2012-02-13at50346pm.png)

## 监控复制代理 {#monitoring-your-replication-agents}

您可以监视[复制队列](/help/sites-deploying/replication.md)以检测队列何时关闭或被阻止 — 这反过来可能表示发布实例或外部系统有问题：

* 是否启用所有必需队列？
* 是否仍需要任何禁用的队列？
* 所有`enabled`队列应具有状态`idle`或`active`，这表示正常操作；队列不应为`blocked`，这通常表示接收方出现问题。

* 如果队列的大小随时间增长，这可能表示队列被阻止。

要监视复制代理，请执行以下操作：

1. 访问AEM中的&#x200B;**工具**&#x200B;选项卡。
1. 单击&#x200B;**复制**。
1. 双击相应环境（左窗格或右窗格）的代理链接；例如，作者&#x200B;**上的代理。**

   生成的窗口显示了创作环境的所有复制代理的概述，包括其目标和状态。

1. 单击相应的代理名称（即链接）可显示有关该代理的详细信息：

   ![chlimage_1](assets/chlimage_1.jpeg)

   在此对话框中，您可以：

   * 查看是否启用了代理。
   * 查看任何复制的目标。
   * 查看复制队列当前是否处于活动状态（已启用）。
   * 查看队列中是否有任何项目。
   * **** 刷新或 **** 清除以更新队列条目的显示；这有助于您查看进入队列和离开队列的项目。

   * **查** 看日志以访问复制代理执行的任何操作的日志。
   * **测试** 与目标实例的连接。
   * **根据** 需要强制重试任何队列项。

   >[!CAUTION]
   >
   >请勿在发布实例上对反向复制发件箱使用“测试连接”链接。
   >
   >如果对发件箱队列执行复制测试，则所有早于测试复制的项目都将通过每次反向复制进行重新处理。
   >
   >如果此类项目已存在于队列中，则可通过以下XPath JCR查询找到它们，并应将其删除。
   >
   >`/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']`

同样，您可以开发一个解决方案来检测所有复制代理（位于`/etc/replication/author`或`/etc/replication/publish`下），然后检查代理(`enabled`、`disabled`)和底层队列(`active`、`idle`、`blocked`)的状态。

## 监控性能 {#monitoring-performance}

[性能](/help/sites-deploying/configuring-performance.md) 优化是一个交互式过程，在开发过程中会获得焦点。部署后，通常会在特定的间隔或事件后进行审核。

在收集信息以进行优化时使用的方法也可用于持续监控。

>[!NOTE]
>
>还可以检查可用于提高性能的特定[配置](/help/sites-deploying/configuring-performance.md#configuring-for-performance)。

下面列出了发生的常见性能问题，以及关于如何发现和消除这些问题的建议。

| 区域 | 症状 | 要增加容量…… | 要减少音量…… |
|---|---|---|---|
| 客户端 | 客户端CPU使用率较高。 | 安装性能更高的客户端CPU。 | 简化(HTML)布局。 |
|  | 服务器CPU使用率较低。 | 升级到更快的浏览器。 | 改进客户端缓存。 |
|  | 有些客户很快，有些很慢。 |  |  |
| 服务器 |  |  |  |
| 网络 | 服务器和客户端的CPU使用率都较低。 | 消除网络瓶颈。 | 改进/优化客户端缓存的配置。 |
|  | 在服务器上本地浏览的速度（相对）较快。 | 增加网络带宽。 | 减轻网页的“粗细”（例如，图像较少、优化了HTML）。 |
| Web服务器 | Web服务器上的CPU使用率很高。 | 群集Web服务器。 | 减少每页面（访问）的点击量。 |
|  |  | 使用硬件负载平衡器。 |  |
| 应用程序 | 服务器CPU使用率很高。 | 集群您的AEM实例。 | 搜索并消除CPU和内存挂起（使用代码审阅、计时输出等）。 |
|  | 内存消耗高。 |  | 改进所有级别的缓存。 |
|  | 响应时间较短。 |  | 优化模板和组件（例如，结构、逻辑）。 |
| 存储库 |  |  |  |
| 缓存 |  |  |  |

性能问题可能源于许多与网站无关的原因，包括连接速度、CPU负载等方面的暂时缓慢。

它还可能会影响所有访客，或仅影响访客的子集。

在优化一般性能或解决特定问题之前，需要获取、排序和分析所有这些信息。

* 在遇到性能问题之前：

   * 收集尽可能多的信息，以建立正常情况下系统的良好工作知识

* 当您遇到性能问题时：

   * 尝试在您知道具有良好常规性能的其他客户端上和/或在服务器本身（如果可能）上用一个（或更多）标准Web浏览器复制它
   * 检查任何内容（与系统相关）是否在适当的时间空间内发生了更改，以及这些更改中是否有可能影响性能
   * 提问，例如：

      * 问题是否仅在特定时间发生？
      * 问题是否仅在特定页面上发生？
      * 其他请求是否受到影响？
   * 在正常情况下收集尽可能多的信息与您对系统的了解进行比较：


### 用于监控和分析性能的工具 {#tools-for-monitoring-and-analyzing-performance}

下面简要介绍了可用于监控和分析性能的一些工具。

其中某些操作取决于您的操作系统。

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
   <td><a href="#interpreting-the-request-log">解释request.log</a>。</td>
  </tr>
  <tr>
   <td>桁架/地形</td>
   <td>页面加载次数</td>
   <td><p>用于跟踪系统调用和信号的Unix/Linux命令。 将日志级别增加到<code>INFO</code>。</p> <p>分析每个请求加载的页面数量，以及哪些页面等。</p> </td>
  </tr>
  <tr>
   <td>线程转储</td>
   <td>观察JVM线程。 识别争议、锁和长跑者。</td>
   <td><p>取决于操作系统：<br /> - Unix/Linux:<code>kill -QUIT &lt;<em>pid</em>&gt;</code><br /> - Windows（控制台模式）：Ctrl-Break<br /> </p> <p>还提供分析工具，如<a href="https://java.net/projects/tda/">TDA</a>。<br /> </p> </td>
  </tr>
  <tr>
   <td>堆转储</td>
   <td>内存不足问题导致性能缓慢。</td>
   <td><p>在对AEM的java调用中添加：<br /> <code>-XX:+HeapDumpOnOutOfMemoryError</code><br />选项。</p> <p>请参阅<a href="https://java.sun.com/javase/6/webnotes/trouble/TSG-VM/html/clopts.html#gbzrr">《Java SE 6与热点VM的疑难解答指南》</a>。</p> </td>
  </tr>
  <tr>
   <td>系统调用</td>
   <td>确定时间问题。</td>
   <td><p>对<code>System.currentTimeMillis()</code>或<code>com.day.util</code>的调用。Timing用于从代码或通过<a href="#html-comments">HTML-comments</a>生成时间戳。</p> <p><strong>注意：</strong> 应实施这些功能，以便能够根据需要激活/停用它们；当系统运行顺利时，不需要收集统计信息的开销。</p> </td>
  </tr>
  <tr>
   <td>阿帕奇·本奇</td>
   <td>识别内存泄漏，有选择地分析响应时间。</td>
   <td><p>基本用法为：</p> <p><code>ab -k -n &lt;<em>requests</em>&gt; -c &lt;<em>concurrency</em>&gt; &lt;<em>url</em>&gt;</code></p> <p>有关完整的详细信息，请参阅<a href="#apache-bench">Apache Bench</a>和<a href="https://httpd.apache.org/docs/2.2/programs/ab.html">ab手册页</a>。</p> </td>
  </tr>
  <tr>
   <td>搜索分析</td>
   <td> </td>
   <td>脱机执行搜索查询，确定查询的响应时间，测试并确认结果集。<br /> </td>
  </tr>
  <tr>
   <td>JMeter</td>
   <td>加载和功能测试。</td>
   <td><a href="https://jakarta.apache.org/jmeter/">https://jakarta.apache.org/jmeter/</a></td>
  </tr>
  <tr>
   <td>JProfiler</td>
   <td>深入分析CPU和内存。</td>
   <td><a href="https://www.ej-technologies.com/">https://www.ej-technologies.com/</a></td>
  </tr>
  <tr>
   <td>JConsole</td>
   <td>观察JVM量度和线程。</td>
   <td><p>用法：jconsole</p> <p>请参阅<a href="https://java.sun.com/developer/technicalArticles/J2SE/jconsole.html">jconsole</a>和<a href="#monitoring-performance-using-jconsole">使用JConsole</a>监控性能。</p> <p><strong>注意：</strong> 通过JDK 1.6,JConsole可通过插件进行扩展；例如，Top或TDA（线程转储分析器）。</p> </td>
  </tr>
  <tr>
   <td>Java VisualVM</td>
   <td>观察JVM量度、线程、内存和分析。</td>
   <td><p>用法：jvisualvm或visualvm<br /> </p> <p>请参阅<a href="https://java.sun.com/javase/6/docs/technotes/tools/share/jvisualvm.html">jvisualvm</a>、<a href="https://visualvm.dev.java.net/">visualvm</a>和<a href="#monitoring-performance-using-j-visualvm">使用(J)VisualVM</a>监控性能。</p> <p><strong>注意：</strong> 通过JDK 1.6,VisualVM可通过插件进行扩展。</p> </td>
  </tr>
  <tr>
   <td>桁架/地带，lsof</td>
   <td>深入的内核调用和过程分析(Unix)。</td>
   <td>Unix/Linux命令。</td>
  </tr>
  <tr>
   <td>时间统计</td>
   <td>请参阅页面渲染的时间统计信息。</td>
   <td><p>要查看页面渲染的时间统计信息，可以将<strong>Ctrl-Shift-U</strong>与URL中设置的<code>?debugClientLibs=true</code>结合使用。</p> </td>
  </tr>
  <tr>
   <td>CPU和内存分析工具<br /> </td>
   <td><a href="#interpreting-the-request-log">在开发过程中分析缓慢的请求时使用</a>。</td>
   <td>例如，<a href="https://www.yourkit.com/">YourKit</a>。</td>
  </tr>
  <tr>
   <td><a href="#information-collection">信息收集</a></td>
   <td>安装的持续状态。</td>
   <td>尽可能了解您的安装情况还可以帮助您跟踪导致性能变化的原因，以及这些更改是否合理。 需要定期收集这些量度，以便您能够轻松查看重大更改。</td>
  </tr>
 </tbody>
</table>

### 解释request.log {#interpreting-the-request-log}

此文件记录有关对AEM发出的每个请求的基本信息。 从这一有价值的结论中可以提取出来。

`request.log`提供了一种内置方式，用于查看请求需要多长时间。 出于开发目的，`tail -f`和`request.log`在响应缓慢时，会非常有用。 要分析更大的`request.log`，我们建议使用[ `rlog.jar`，以便对响应时间](#using-rlog-jar-to-find-requests-with-long-duration-times)进行排序和筛选。

我们建议从`request.log`中隔离“慢”页面，然后单独调整这些页面以获得更好的性能。 这通常通过包括每个组件的性能量度或使用性能分析工具（如` [yourkit](https://www.yourkit.com/)`）来完成。

#### 监控您网站上的流量 {#monitoring-traffic-on-your-website}

请求日志记录发出的每个请求以及发出的响应：

```xml
09:43:41 [66] -> GET /author/y.html HTTP/1.1
09:43:41 [66] <- 200 text/html 797ms
```

通过在特定时段内（例如，在24小时内）合计所有GET条目，您可以对网站上的平均流量进行声明。

#### 使用request.log监控响应时间 {#monitoring-response-times-with-the-request-log}

性能分析的一个好起点是请求日志：

`<cq-installation-dir>/crx-quickstart/logs/request.log`

日志如下所示（为简便起见，缩短了各行）：

```xml
31/Mar/2009:11:32:57 +0200 [379] -> GET /path/x HTTP/1.1
31/Mar/2009:11:32:57 +0200 [379] <- 200 text/html 33ms
31/Mar/2009:11:33:17 +0200 [380] -> GET /path/y HTTP/1.1
31/Mar/2009:11:33:17 +0200 [380] <- 200 application/json 39ms
```

此日志中每个请求或响应有一行：

* 发出每个请求或响应的日期。
* 请求的编号，用方括号括起来。 此数字与请求和响应的数字匹配。
* 一个箭头，指示这是请求（指向右侧的箭头）还是响应（向左的箭头）。
* 对于请求，行包含：

   * 方法(通常为GET、HEAD或POST)
   * 请求的页面
   * 协议

* 对于响应，行包含：

   * 状态代码（200表示“success”，404表示“页面未找到”）
   * MIME类型
   * 响应时间

使用小脚本，您可以从日志文件中提取所需信息并汇编所需的统计信息。 从中，您可以看到哪些页面或页面类型缓慢，以及整体性能是否令人满意。

#### 使用request.log监控搜索响应时间 {#monitoring-search-response-times-with-the-request-log}

搜索请求也会在日志文件中注册：

```xml
31/Mar/2009:11:35:34 +0200 [338] -> GET /author/playground/en/tools/search.html?query=dilbert&size=5&dispenc=utf-8 HTTP/1.1
31/Mar/2009:11:35:34 +0200 [338] <- 200 text/html 1562ms
```

因此，与上面一样，您可以使用脚本来提取相关信息并构建统计信息。

但是，确定响应时间后，您可能需要分析请求为何需要花费时间，以及可以采取哪些措施来改进响应。

#### 监控并发用户的数量和影响 {#monitoring-the-number-and-impact-of-concurrent-users}

同样，`request.log`可用于监视并发以及系统对它的反应。

必须进行测试以确定系统可以处理的并发用户数，才能看到负面影响。 同样，可以使用脚本从日志文件中提取结果：

* 监视在特定时间范围内发出的请求数，例如一分钟
* 同时（尽可能接近）测试特定数量的用户发出相同请求的效果；例如，30个用户同时单击&#x200B;**Save**。

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

AEM包括位于以下位置的各种帮助程序工具：
`<cq-installation-dir>/crx-quickstart/opt/helpers`

其中一个(`rlog.jar`)可用于快速排序`request.log`，以便按持续时间显示请求，从最长到最短的时间。

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

例如，您可以运行它以指定`request.log`文件作为参数，并显示持续时间最长的10个前请求：

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

如果需要对大型数据采样执行此操作，可能需要连接单个`request.log`文件。

### 阿帕奇·本奇 {#apache-bench}

为了最大限度地减少特殊情况（如垃圾收集等）的影响，建议使用诸如`apachebench`之类的工具（例如，有关进一步文档，请参阅[ab](https://httpd.apache.org/docs/2.2/programs/ab.html)），以帮助识别内存泄漏并有选择地分析响应时间。

Apache Bench可通过以下方式使用：

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

上述数字取自访问geometrixx公司页面的标准MAcBook Pro笔记本电脑（2010年年中），该页面包含在默认AEM安装中。 页面非常简单，但并未针对性能进行优化。

`apachebench` 还显示每个请求的时间作为平均值，涵盖所有并发请求；请参 `Time per request: 54.595 [ms]` 阅（跨所有并发请求的平均值）。您可以更改并发参数`-c`的值（一次要执行的多个请求数），以查看任何效果。

### 请求计数器 {#request-counters}

有关请求流量（特定时间段内的请求数）的信息会指示实例的负载。 此信息可从[request.log](#interpreting-the-request-log)中提取，但使用计数器将自动收集数据，以便您查看：

* 活动方面存在显着差异（即区分“多个请求”和“活动量低”）
* 当未使用实例时
* 任何重新启动（计数器重置为0）

要自动收集信息，您还可以安装RequestFilter ，以在每个请求中递增一个计数器。 多个计数器可用于不同的时间段。

收集的信息可用于指示：

* 活动的重大变化
* 冗余实例
* 任何重新启动（计数器重置为0）

### HTML注释 {#html-comments}

为了提高服务器性能，建议每个项目都包含`html comments`。 可以找到许多好的公共例子；选择一个页面，打开页面源进行查看并滚动到底部，可以看到以下代码：

```xml
</body>
 </html>
        <!--
        Page took 58 milliseconds to be rendered by server
         -->
```

### 使用JConsole监控性能 {#monitoring-performance-using-jconsole}

工具命令`jconsole`可在JDK中使用。

1. 启动AEM实例。
1. 运行 `jconsole.`
1. 选择您的AEM实例并&#x200B;**Connect**。

1. 在`Local`应用程序内，双击`com.day.crx.quickstart.Main`;将默认显示概述：

   ![chlimage_1-1](assets/chlimage_1-1.png)

   之后，您可以选择其他选项。

### 使用(J)VisualVM监控性能 {#monitoring-performance-using-j-visualvm}

自JDK 1.6起，工具命令`jvisualvm`便可用。 安装JDK 1.6后，您可以：

1. 启动AEM实例。

   >[!NOTE]
   >
   >如果使用Java 5，则可以将`-Dcom.sun.management.jmxremote`参数添加到启动JVM的java命令行中。 默认情况下，Java 6会启用JMX。

1. 运行以下任一操作：

   * `jvisualvm`:在JDK 1.6 bin文件夹中（已测试版本）
   * `visualvm`:可以从VisualVM  [](https://visualvm.dev.java.net/) （放血边缘版本）下载

1. 在`Local`应用程序内，双击`com.day.crx.quickstart.Main`;将默认显示概述：

   ![chlimage_1-2](assets/chlimage_1-2.png)

   之后，您可以选择其他选项，包括监视器：

   ![chlimage_1-3](assets/chlimage_1-3.png)

您可以使用此工具生成线程转储和内存头转储。 技术支持团队通常要求提供此信息。

### 信息收集 {#information-collection}

尽可能了解您的安装情况有助于您跟踪哪些因素可能导致性能变化，以及这些变化是否合理。 需要定期收集这些量度，以便您能够轻松查看重大更改。

以下信息可能会很有用：

* [有多少位作者在使用该系统？](#how-many-authors-are-working-with-the-system)
* [每天平均激活页面的次数是多少？](#what-is-the-average-number-of-page-activations-per-day)
* [您当前在此系统上维护多少页？](#how-many-pages-do-you-currently-maintain-on-this-system)
* [如果使用MSM，则每月平均转出次数是多少？](#if-you-use-msm-what-is-the-average-number-of-rollouts-per-month)
* [每月的平均Live Copy数是多少？](#what-is-the-average-number-of-live-copies-per-month)
* [如果您使用AEM Assets，则当前在Assets中维护多少个资产？](#ifyouusecqdamhowmanyassetsdoyoucurrentlymaintainincqdam)
* [资产的平均大小是多少？](#what-is-the-average-size-of-the-assets)
* [当前使用了多少个模板？](#how-many-templates-are-currently-used)
* [当前使用了多少个组件？](#how-many-components-are-currently-used)
* [在高峰时间，您在创作系统上每小时有多少个请求？](#how-many-requests-per-hour-do-you-have-on-the-author-system-at-peak-time)
* [在高峰时间，您在发布系统上每小时有多少个请求？](#how-many-requests-per-hour-do-you-have-on-the-publish-system-at-peak-time)

#### 有多少位作者在使用该系统？ {#how-many-authors-are-working-with-the-system}

要查看自安装以来使用系统的作者人数，请使用命令行：

```shell
cd <cq-installation-dir>/crx-quickstart/logs
cut -d " " -f 3 access.log | sort -u | wc -l
```

要查看在给定日期工作的作者人数，请执行以下操作：

```shell
grep "<date>" access.log | cut -d " " -f 3 | sort -u | wc -l
```

#### 每天平均激活页面的次数是多少？ {#what-is-the-average-number-of-page-activations-per-day}

查看自服务器安装以来使用存储库查询的页面激活总数；通过CRXDE — 工具 — 查询：

* **类型** `XPath`

* **路径** `/`

* **查询** `//element(*, cq:AuditEvent)[@cq:type='Activate']`

然后，计算自安装以来经过的天数，以计算平均值。

#### 您当前在此系统上维护多少页？ {#how-many-pages-do-you-currently-maintain-on-this-system}

若要查看服务器上当前的页数，请使用存储库查询；通过CRXDE — 工具 — 查询：

* **类型** `XPath`

* **路径** `/`

* **查询** `//element(*, cq:Page)`

#### 如果使用MSM，则每月平均转出次数是多少？ {#if-you-use-msm-what-is-the-average-number-of-rollouts-per-month}

确定安装后使用存储库查询的转出总数；通过CRXDE — 工具 — 查询：

* **类型** `XPath`

* **路径** `/`

* **查询** `//element(*, cq:AuditEvent)[@cq:type='PageRolledOut']`

计算自安装以来经过的月数以计算平均值。

#### 每月的平均Live Copy数是多少？ {#what-is-the-average-number-of-live-copies-per-month}

确定自安装后使用存储库查询的Live Copy总数；通过CRXDE — 工具 — 查询：

* **类型** `XPath`

* **路径** `/`

* **查询** `//element(*, cq:LiveSyncConfig)`

再次使用安装后经过的月数来计算平均值。

#### 如果您使用AEM Assets，则当前在Assets中维护多少个资产？ {#if-you-use-aem-assets-how-many-assets-do-you-currently-maintain-in-assets}

要查看您当前维护的DAM资产数量，请使用存储库查询；通过CRXDE — 工具 — 查询：

* **类型** `XPath`
* **路径** `/`
* **查询** `/jcr:root/content/dam//element(*, dam:Asset)`

#### 资产的平均大小是多少？ {#what-is-the-average-size-of-the-assets}

要确定`/var/dam`文件夹的总大小，请执行以下操作：

1. 使用WebDAV将存储库映射到本地文件系统。

1. 使用命令行：

   ```shell
   cd /Volumes/localhost/var
   du -sh dam/
   ```

   要获取平均大小，请将全局大小除以`/var/dam`中的资产总数（如上所示）。

#### 当前使用了多少个模板？ {#how-many-templates-are-currently-used}

若要查看服务器上当前的模板数，请使用存储库查询；通过CRXDE — 工具 — 查询：

* **类型** `XPath`
* **路径** `/`
* **查询** `//element(*, cq:Template)`

#### 当前使用了多少个组件？ {#how-many-components-are-currently-used}

要查看服务器上当前组件的数量，请使用存储库查询；通过CRXDE — 工具 — 查询：

* **类型** `XPath`
* **路径** `/`
* **查询** `//element(*, cq:Component)`

#### 在高峰时间，您在创作系统上每小时有多少个请求？ {#how-many-requests-per-hour-do-you-have-on-the-author-system-at-peak-time}

要确定在高峰时间您在创作系统上的每小时请求数，请执行以下操作：

1. 要确定自安装以来的请求总数，请使用命令行：

   ```shell
   cd <cq-installation-dir>/crx-quickstart/logs
   grep -R "\->" request.log | wc -l
   ```

1. 要确定开始和结束日期，请执行以下操作：

   ```shell
   vim request.log
   G / 1G: for the last/first lines
   ```

   使用这些值可计算自安装以来经过的小时数，以及每小时的平均请求数。

#### 在高峰时间，您在发布系统上每小时有多少个请求？ {#how-many-requests-per-hour-do-you-have-on-the-publish-system-at-peak-time}

对您的发布实例重复上述步骤。

## 分析特定情景 {#analyzing-specific-scenarios}

下面列出了一些建议，说明在开始遇到某些性能问题时要检查哪些内容。 （不幸的）清单并不完全。

>[!NOTE]
>
>有关更多信息，另请参阅以下文章：
>
>* [线程转储](https://helpx.adobe.com/experience-manager/kb/TakeThreadDump.html)
>* [分析内存问题](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)
>* [使用内置探查器分析](https://helpx.adobe.com/experience-manager/kb/AnalyzeUsingBuiltInProfiler.html)
>* [分析慢速和阻止的进程](https://helpx.adobe.com/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)

>



### CPU为100% {#cpu-at}

如果系统的CPU以100%的速度持续运行，请查看：

* 知识库：

   * [分析慢速和阻止的进程](https://helpx.adobe.com/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)

### 内存不足 {#out-of-memory}

尽管在开发和测试期间应检测到此类错误，但某些情况可能会漏掉。

如果您的系统内存不足，则可以通过各种方式查看此情况，包括性能下降和错误消息（包括子文本）：

`java.lang.OutOfMemoryError`

在这些情况下，请检查：

* 用于[启动AEM](/help/sites-deploying/deploy.md#getting-started)的JVM设置
* 知识库：

   * [分析内存问题](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)

### 磁盘I/O {#disk-i-o}

如果您的系统磁盘空间不足，或者您发现磁盘崩溃开始出现，请参阅：

* 是否禁用了调试信息的收集；可以在各种位置进行配置，包括：

   * [Apache Sling JSP脚本处理程序](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjspscripthandler)
   * [Apache Sling Java脚本处理程序](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjavascripthandler)
   * [Apache Sling日志记录配置](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration)
   * [CQ HTML库管理器](/help/sites-deploying/osgi-configuration-settings.md#daycqhtmllibrarymanager)
   * [CQ WCM调试过滤器](/help/sites-deploying/osgi-configuration-settings.md#daycqwcmdebugfilter)
   * [记录器](/help/sites-deploying/monitoring-and-maintaining.md#activating-the-debug-log-level)

* 是否配置了[版本清除](/help/sites-deploying/version-purging.md)以及配置方式
* 知识库：

   * [打开的文件过多](https://helpx.adobe.com/experience-manager/kb/TooManyOpenFiles.html)
   * [日志占用太多磁盘空间](https://helpx.adobe.com/experience-manager/kb/JournalTooMuchDiskSpace.html)

### 常规性能下降 {#regular-performance-degradation}

如果您看到实例在每次重新引导后（有时一周或更晚）性能恶化，则可以检查以下内容：

* [内存不足](#outofmemory)
* 知识库：

   * [未结会话](https://helpx.adobe.com/experience-manager/kb/AnalyzeUnclosedSessions.html)

### JVM优化 {#jvm-tuning}

Java虚拟机(JVM)在调整方面有了显着改进（尤其是自Java 7以来）。 因此，指定合理的固定JVM大小和使用默认值通常是合适的。

如果默认设置不合适，则在尝试调整JVM之前，必须建立一种方法来监控和评估GC性能；这可能涉及监控因素，包括堆大小、算法等。

一些常见的选择包括：

* VerboseGC:

   ```
   -verbose:gc \
    -Xloggc:$LOGS/verbosegc.log \
    -XX:+PrintGCDetails \
    -XX:+PrintGCDateStamps
   ```

生成的日志可由GC可视化器摄取，例如：

` [https://www.ibm.com/developerworks/library/j-ibmtools2/](https://www.ibm.com/developerworks/library/j-ibmtools2/)`

或JConsole:

* 这些设置适用于“宽打开”JMX连接：

   ```
   -Dcom.sun.management.jmxremote \
    -Dcom.sun.management.jmxremote.port=8889 \
    -Dcom.sun.management.jmxremote.authenticate=false \
    -Dcom.sun.management.jmxremote.ssl=false
   ```

* 然后，使用JConsole连接到JVM;请参阅：
   ` [https://docs.oracle.com/javase/6/docs/technotes/guides/management/jconsole.html](https://docs.oracle.com/javase/6/docs/technotes/guides/management/jconsole.html)`

这将帮助您了解正在使用的内存量、GC算法的使用情况、运行时间以及这对应用程序性能有何影响。 如果没有这一点，调整就只是“随机摆弄旋钮”。

>[!NOTE]
>
>对于Oracle的VM，还有以下信息：
>
>[https://docs.oracle.com/javase/7/docs/technotes/guides/vm/server-class.html](https://docs.oracle.com/javase/7/docs/technotes/guides/vm/server-class.html)
