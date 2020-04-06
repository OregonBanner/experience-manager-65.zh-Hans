---
title: 监视和维护AEM实例
seo-title: 监视和维护AEM实例
description: 了解如何监视AEM。
seo-description: 了解如何监视AEM。
uuid: 14466552-5c92-4730-a427-85675a2b121c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 5d2364b7-4497-4f8b-85ef-6e780bfb8c36
docset: aem65
translation-type: tm+mt
source-git-commit: a6f95e04fd5b8ed28beaa12e9fd170ed495397b8

---


# 监视和维护AEM实例{#monitoring-and-maintaining-your-aem-instance}

部署AEM实例后，将需要某些任务来监视和维护其操作、性能和完整性。

这里的一个关键因素是，要识别潜在问题，您需要了解系统在正常情况下的外观和行为。 最好通过监控系统并收集一段时间内的信息来实现这一点。

| 检查 | 注意事项 | 评论／操作 |
|---|---|---|
| 备份计划。 |  | 了解如何 [备份实例](/help/sites-deploying/monitoring-and-maintaining.md#backups)。 |
| 灾难恢复计划。 | 您的公司的灾难恢复指南。 |  |
| 错误跟踪系统可用于解决报告问题。 | 例如， [bugzilla](https://www.bugzilla.org/)、 [jira](https://www.atlassian.com/software/jira/)，或其他许多对象之一。 |  |
| 正在监视文件系统。 | 如果可用磁盘空间不足，CRX存储库将“冻结”。 当空间可用时，它将恢复。 | 当可 `*ERROR* LowDiskSpaceBlocker`用空间变低时，日志文件中会显示“ ”消息。 |
| [正在监视日志文件](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) 。 |  |  |
| 系统监控（持续）在后台运行。 | 包括CPU、内存、磁盘和网络使用。 例如，使用iostat / vmstat / perfmon。 | 记录的数据是可视化的，可用于跟踪性能问题。 还可以访问原始数据。 |
| [正在监视AEM性能](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance)。 | 包括请 [求计数器](/help/sites-deploying/monitoring-and-maintaining.md#request-counters) ，以监控流量级别。 | 如果出现重大或长期业绩损失，应进行详细调查。 |
| 您正在监视您的复 [制代理](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-your-replication-agents)。&quot; |  |  |
| 定期清除工作流实例。 | 存储库大小和工作流性能。 | 请参 [阅定期清除工作流实例](/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances)。 |

## 备份 {#backups}

最好对以下内容进行备份：

* 您的软件安装——在配置发生重大更改之前／之后
* 存储库中保存的内容——定期

您的公司可能需要遵循一个备份策略，并考虑要备份的内容以及备份时间：

* 系统和数据的重要性。
* 对软件或数据进行更改的频率。
* 数据量；容量有时可能是个问题，执行备份所需的时间也是如此。
* 用户在线时是否可以进行备份；如果可能，性能影响是什么。
* 用户的地理分布；例如，何时是备份（以最大限度地减少影响）的最佳时间？
* 您的灾难恢复策略；是否有关于必须存储备份数据的位置的准则（例如，离站、特定介质等）。

通常，完整备份会定期执行（例如，每日、每周或每月），增量备份介于每小时、每日或每周之间。

>[!CAUTION]
>
>在实施生产实例的备份时，必 *须进行测试* ，以确保能够成功恢复备份。

>如果没有这一点，备份可能就毫无用处（最坏情况）。
>
>[!NOTE]
有关备份性能的详细信息，请阅读备份 [性能部分](/help/sites-deploying/configuring-performance.md#backup-performance) 。

### 备份软件安装 {#backing-up-your-software-installation}

在安装或对配置进行重大更改后，备份软件安装。

为此，您需要备份整 [个存储库](#backing-up-your-repository) ，然后：

1. 停止AEM。
1. 从文件系统 `<cq-installation-dir>` 备份整个文件。

>[!CAUTION]
如果运行的是第三方应用程序服务器，则其他文件夹可能位于不同的位置，并且可能还需要备份。 有关 [安装应用程序服务器的信息，请参阅如何与应用程序服务器一起安装AEM](/help/sites-deploying/application-server-install.md) 。 [](/content/docs/en/aem/6-3/deploy/installing.md#Installing adobe experience manager with application server)

>[!CAUTION]
支持文件数据存储的增量备份；对其他组件（如Lucene索引）使用增量备份时，请确保已删除的文件也在备份中标记为已删除。

>[!NOTE]
磁盘镜像也可用作备份机制。

### 备份存储库 {#backing-up-your-repository}

CRX文 [档的“备份和恢复](/help/sites-administering/backup-and-restore.md) ”部分涵盖与CRX存储库备份相关的所有问题。

有关制作在线“热”备份的完整详细信息，请参 [阅创建在线备份](/help/sites-administering/backup-and-restore.md#online-backup)。

## 版本清除 {#version-purging}

清 **除版本工具** ，用于清除存储库中节点或节点层次结构的版本。 其主要用途是通过删除旧版本的节点来帮助您减小存储库的大小。

本节介绍与AEM版本控制功能相关的维护操作。 清除 **** 版本工具用于清除存储库中节点或节点层次结构的版本。 其主要用途是通过删除旧版本的节点来帮助您减小存储库的大小。

### 概述 {#overview}

“清 **除版本** ”工具位于“版本控制”下的“工 **[具](/help/sites-administering/tools-consoles.md)**”控制台中**，或直&#x200B;**接位于：

`https://<server>:<port>/etc/versioning/purge.html`

![screen_shot_2012-03-15at14418pm](assets/screen_shot_2012-03-15at14418pm.png)

**开始路径** ：必须执行清除的绝对路径。 单击存储库树导航器可以选择开始路径。

**递归** 在清除数据时，您可以选择在一个节点上或通过选择递归对整个层次结构执行操作。 在最后一种情况下，给定路径定义层次的根节点。

**要保留的最大版本** 。节点要保留的最大版本数。 当这些数字超过此值时，将清除最旧版本。

**最大版本** ：节点版本的最大版本。 当版本的年龄超过此值时，将清除该版本。

**练习** 由于删除内容版本是确定的，并且在不恢复备份的情况下无法还原，因此清除版本工具提供了练习模式，允许您预览已清除的版本。 要启动清除流程的练习，请单击练习。

**清除** 启动对开始路径定义的节点上的版本的清除。

### 清除网站的版本 {#purging-versions-of-a-web-site}

要清除网站的版本，请按照以下步骤继续：

1. 导航到工具控 **[制台](/help/sites-administering/tools-consoles.md)**，选&#x200B;**择版本**，然后&#x200B;**多次单击清****除版本。**
1. 设置要清除的内容的开始路径(例如， `/content/geometrixx-outdoors`)。

   * 如果只想清除路径定义的节点，请取消选择“递归 **”**。
   * 如果要清除由路径及其子代定义的节点，请选择“递归 **”**。

1. 设置要保留的最大版本数（对于每个节点）。 如果留空，则不使用此设置。

1. 设置要保留的最大版本年龄（对于每个节点），以天为单位。 如果留空，则不使用此设置。

1. 单 **击“练习** ”以预览清除过程的操作。
1. 单击 **清除** ，以启动进程。

>[!CAUTION]
如果未恢复存储库，则无法恢复已清除的节点。 您应该处理配置，因此我们建议您在清除之前始终执行练习。

### 分析控制台 {#analyzing-the-console}

“干 **运行** ”和“清 **除** ”将列表所有已处理的节点。 在此过程中，节点可以具有以下状态之一：

* `ignore (not versionnable)`:该节点不支持版本控制，在该过程中会被忽略。

* `ignore (no version)`:该节点没有任何版本，在此过程中将被忽略。&quot;

* `retained`:不会清除该节点。
* `purged`:此时将清除该节点。

此外，控制台还提供有关这些版本的有用信息：

* `V 1.0`:版本号。
* `V 1.0.1`*:星形表示版本是当前版本。

* `Thu Mar 15 2012 08:37:32 GMT+0100`:版本的日期。

在下一个示例中：

* 衬 **衫版本会被清除** ，因为其版本年龄大于2天。
* 汤加 **时尚队！** 版本会被清除，因为其版本数大于5。

![global_version_screenshot](assets/global_version_screenshot.png)

## 使用审计记录和日志文件 {#working-with-audit-records-and-log-files}

可以在不同位置找到与Adobe Experience Manager(AEM)相关的审核记录和日志文件。 下面提供了您可以在何处找到的内容的概述。

### 使用日志 {#working-with-logs}

AEM WCM记录详细的日志。 解包并开始快速入门后，您可以找到登录：

* `<cq-installation-dir>/crx-quickstart/logs/`

* `<cq-installation-dir>/crx-quickstart/repository/`

#### 日志文件旋转 {#log-file-rotation}

日志文件旋转是指通过定期创建新文件来限制文件增长的过程。 在AEM中，将根据给 `error.log` 定规则每天旋转一次名为日志文件的日志：

* 将 `error.log` 根据模式{original_filename}重命名文件 `.yyyy-MM-dd`。 例如，在2010年7月11日，将重命名当前日志文 `error.log-2010-07-10`件，然后创建新 `error.og` 的日志文件。

* 以前的日志文件不会被删除，因此您有责任定期清除旧的日志文件以限制磁盘的使用。

>[!NOTE]
如果您升级了AEM安装，请注意，AEM不再使用的任何现有日志文件将保留在磁盘上。 您可以不冒风险地删除它们。 所有新日志条目都将写入新日志文件中。

### 查找日志文件 {#finding-the-log-files}

安装AEM的文件服务器上包含各种日志文件：

* `<cq-installation-dir>/crx-quickstart/logs`

   * `access.log`
此处将注册对AEM WCM和存储库的所有访问请求。

   * `audit.log`
此处将注册审核操作。

   * `error.log`
此处会注册错误消息（严重性级别不同）。

   * [ 仅 `ImageServer-<PortId>-yyyy>-<mm>-<dd>.log`](https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/c_image_server_log.html)在启用此日志时才 [!DNL Dynamic Media] 使用它。 它提供用于分析内部ImageServer进程行为的统计和分析信息。

   * `request.log`
每个访问请求都在此处注册，并随响应一起注册。

   * [ 仅 `s7access-<yyyy>-<mm>-<dd>.log`](https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/c_Access_Log.html)在启用此日志时才 [!DNL Dynamic Media] 使用它。 s7access日志记录对和发出的每 [!DNL Dynamic Media] 个请 `/is/image` 求 `/is/content`。

   * `stderr.log`
保留在启动过程中生成的严重性级别不同的错误消息。 默认情况下，日志级别设置为 `Warning` ( `WARN`)

   * `stdout.log`
保存指示启动期间事件的日志记录消息。

   * `upgrade.log`
提供从和包运行的所有升级操作的 `com.day.compat.codeupgrade` 日志 `com.adobe.cq.upgradesexecutor` 记录。

* `<*cq-installation-dir*>/crx-quickstart/repository`

   * `revision.log`
修订日志信息。

>[!NOTE]
ImageServer和s7access日志不包含在从**system/console/status-Bundlelist **页生成的**Download Full **包中。 出于支持目的，如果您有 [!DNL Dynamic Media] 问题，请在联系客户支持时附加ImageServer和s7access日志。

### 激活调试日志级别 {#activating-the-debug-log-level}

默认日志级别([Apache Sling日志记录配置](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration))为“信息”，因此调试消息不会记录。

要激活Logger的调试日志级别，请在存储库中 `org.apache.sling.commons.log.level` 设置要调试的属性。 例如，开始 `/libs/sling/config/org.apache.sling.commons.log.LogManager` 配置全 [局Apache Sling日志](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration)。

>[!CAUTION]
不要将日志保留在调试日志级别上的时间比必需的时间长，因为它会生成大量日志条目，从而消耗资源。

调试文件中的一行通常与DEBUG开始，然后提供日志级别、安装程序操作和日志消息。 例如：

```shell
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

日志级别如下：

| 0 | 致命错误 | 操作失败，安装程序无法继续。 |
|---|---|---|
| 1 | 错误 | 操作已失败。 安装将继续，但AEM WCM的某部分安装不正确，因此将无法运行。 |
| 2 | 警告 | 该操作已成功，但遇到问题。 AEM WCM可能正常工作，也可能无法正常工作。 |
| 3 | 信息 | 该操作已成功。 |

### 创建自定义日志文件 {#create-a-custom-log-file}

>[!NOTE]
When working with Adobe Experience Manager there are several methods of managing the configuration settings for such services; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

在某些情况下，您可能希望创建具有不同日志级别的自定义日志文件。 您可以通过以下方式在存储库中执行此操作：

1. 如果项目尚未存在，请为项目创建新的配置文 `sling:Folder`件夹() `/apps/<*project-name*>/config`。
1. 在下 `/apps/<*project-name*>/config`面，为新的 [Apache Sling Logging Logger配置创建一个节点](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingloggerconfigurationfactoryconfiguration):

   * 名称： `org.apache.sling.commons.log.LogManager.factory.config-<*identifier*>` （因为这是记录器）

      其中， `<*identifier*>` 将替换为您（必须）输入以标识实例的自由文本（您不能忽略此信息）。

      例如，`org.apache.sling.commons.log.LogManager.factory.config-MINE`

   * 类型: `sling:OsgiConfig`
   >[!NOTE]
   虽然不是技术要求，但最好是使其与众不同 `<*identifier*>` 。

1. 在此节点上设置以下属性：

   * 名称: `org.apache.sling.commons.log.file`

      类型：字符串

      值：指定日志文件；例如， `logs/myLogFile.log`

   * 名称: `org.apache.sling.commons.log.names`

      类型：字符串[] （字符串+多个）

      值：指定记录器要为其记录消息的OSGi服务；例如，以下所有内容：

      * `org.apache.sling`
      * `org.apache.felix`
      * `com.day`
   * 名称: `org.apache.sling.commons.log.level`

      类型：字符串

      值：指定所需的日志级 `debug`别( `info`、 `warn` 或 `error`);示例 `debug`

   * 根据需要配置其他参数：

      * 名称: `org.apache.sling.commons.log.pattern`

         类型: `String`

         值：根据需要指定日志消息的模式；例如，

         `{0,date,dd.MM.yyyy HH:mm:ss.SSS} *{4}* [{2}] {3} {5}`
   >[!NOTE]
   `org.apache.sling.commons.log.pattern` 最多支持六个参数。

   >{0}类型{1} the log marker{2} the name of the current thread{3} the logger{4} the log level{5} the log message `java.util.Date`

   >如果日志调用包括堆栈 `Throwable` 跟踪，则该堆栈跟踪将附加到消息。

   >[!CAUTION]
   org.apache.sling.commons.log.names必须具有值。

   >[!NOTE]
   日志写入程序路径是相对于位置 `crx-quickstart` 的。
   因此，日志文件指定为：
   `logs/thelog.log`

   >写入：
   `` ` ` `<*cq-installation-dir*>/``crx-quickstart/logs/thelog.log。
   以及指定为：
   `../logs/thelog.log`

   >写入到目录：
   ` <*cq-installation-dir*>/logs/`
&quot;(即，在 ` `&lt;*cq-installation-dir*`crx-quickstart/`>/旁)

1. 仅当需要新的Writer时（即，配置与默认Writer不同），才需要执行此步骤。

   >[!CAUTION]
   仅当现有默认值不适合时，才需要新的日志记录写入程序配置。

   >如果未配置显式编写器，则系统将根据默认值自动生成隐式编写器。

   在下 `/apps/<*project-name*>/config`面，为新的 [Apache Sling记录编写器配置创建一个节点](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingwriterconfigurationfactoryconfiguration):

   * 名称：( `org.apache.sling.commons.log.LogManager.factory.writer-<*identifier*>` 作者为作者)

      与记录器一样， `<*identifier*>` 将替换为您（必须）输入用来标识实例的自由文本（您不能忽略此信息）。 例如，`org.apache.sling.commons.log.LogManager.factory.writer-MINE`

   * 类型: `sling:OsgiConfig`
   >[!NOTE]
   虽然不是技术要求，但最好是使其与众不同 `<*identifier*>` 。

   在此节点上设置以下属性：

   * 名称: `org.apache.sling.commons.log.file`

      类型: `String`

      值：指定日志文件，使其与记录器中指定的文件匹配；

      例如， `../logs/myLogFile.log`

   * 根据需要配置其他参数：

      * 名称: `org.apache.sling.commons.log.file.number`

         类型: `Long`

         值：指定要保留的日志文件数；例如， `5`

      * 名称: `org.apache.sling.commons.log.file.size`

         类型: `String`

         值：根据大小／日期指定控制文件旋转的要求；例如， `'.'yyyy-MM-dd`
   >[!NOTE]
   `org.apache.sling.commons.log.file.size` 通过设置以下任一项来控制日志文件的旋转：
   * 最大文件大小
   * 时间／日期计划
   以指示何时创建新文件（以及根据名称模式重命名的现有文件）。
   * 可以用数字指定大小限制。 如果未提供大小指示符，则将其视为字节数，或者您可以添加大小指示符 `KB`- `MB`、 `GB` 或（忽略大小写）。
   * 时间／日期计划可以指定为模 `java.util.SimpleDateFormat` 式。 这定义了文件旋转的时间段；还有附加到旋转文件（用于标识）的后缀。
   默认为 &#39;.&#39;yyyy-MM-dd（用于日志旋转）。
   例如，在2010年1月20日午夜（或者，当这之后的第一条日志消息准确无误时）,../logs/error.log将更名为../logs/error.log.2010-01-20。 1月21日的日志记录将输出到../logs/error.log（新的和空的），直到在下一天的更改时滚过。
       | `&#39;.&#39;yyyy-MM`|每月初的轮换|
    |—|—|
    |“”yyyy-ww`|每周第一天的旋转（取决于区域设置）。 |
       | `&#39;.&#39;yyyy-MM-dd`每天午夜时分旋转。 |
       | `&#39;.&#39;yyyy-MM-dd-a每天午夜和中午的轮换。 |
       | `&#39;.&#39;yyyy-MM-dd-HH`每小时的顶部旋转。 |
       | `&#39;.&#39;yyyy-MM-dd-HH-mm`每分钟开始时的旋转。 |
 注     
    意：指定时间／日期时：
      1. 您应该在单引号(&#39; &#39;)中“转义”文本；
  这     是为了避免某些字符被解释为模式字母。
       1. 在选项中的任意位置仅使用允许用于有效文件名的字符。
   

1. 使用所选工具阅读新的日志文件。

   此示例创建的日志文件将为 `../crx-quickstart/logs/myLogFile.log`。

Felix Console还提供有关Sling Log支持的信息，网址为 `../system/console/slinglog`;例如 `https://localhost:4502/system/console/slinglog`,

### 查找审计记录 {#finding-the-audit-records}

审计记录旨在提供由谁进行何事何时进行的记录。 为AEM WCM和OSGi事件生成不同的审计记录。

#### AEM WCM页面创作时显示的审核记录 {#aem-wcm-audit-records-shown-when-page-authoring}

1. 打开页面。
1. 在Sidekick中，您可以选择带有锁定图标的选项卡，然后多次单击审 **核日志……**
1. 将打开一个新窗口，其中显示当前页面的审计记录列表。

   ![screen_shot_2012-02-02at43601pm](assets/screen_shot_2012-02-02at43601pm.png)

1. 当您 **要关闭窗口** 时，单击“确定”。

#### 存储库中的AEM WCM审核记录 {#aem-wcm-auditing-records-within-the-repository}

在该文 `/var/audit` 件夹中，会根据资源保留审核记录。 您可以向下展开，直到您看到单个记录及其包含的信息。

这些条目包含的信息与编辑页面时显示的信息相同。

#### 从Web控制台中的OSGi审核记录 {#osgi-audit-records-from-the-web-console}

OSGi事件还会生成审核记录，该记录可从AEM Web控制台的“ **Configuration** Status”选项卡-> **Log Files **选项卡中查看：

![screen_shot_2012-02-13at50346pm](assets/screen_shot_2012-02-13at50346pm.png)

## 监视复制代理 {#monitoring-your-replication-agents}

您可以监视复 [制队列](/help/sites-deploying/replication.md) ，以检测队列何时关闭或被阻止——这又可能指示发布实例或外部系统出现问题：

* 是否已启用所有必需队列？
* 是否仍需要任何禁用的队列？
* 所有 `enabled` 队列应具有状态 `idle` 或 `active`（表示正常操作）;不应该有队 `blocked`列，这通常是接收方问题的征兆。

* 如果队列的大小随时间递增，这可能表示队列被阻止。

要监视复制代理，请执行以下操作：

1. 访问AEM中 **的** “工具”选项卡。
1. 单击&#x200B;**复制**。
1. 多次-单击相应环境的代理链接（左窗格或右窗格）;例如，作 **者上的代理**。

   生成的窗口显示了创作环境的所有复制代理的概述，包括其目标和状态。

1. 单击相应的代理名称（即链接）以显示该代理的详细信息：

   ![chlimage_1](assets/chlimage_1.jpeg)

   在此对话框中，您可以：

   * 查看代理是否已启用。
   * 查看任何复制的目标。
   * 查看复制队列当前是否处于活动状态（已启用）。
   * 查看队列中是否有任何项目。
   * **刷新****或清除** ，更新队列条目的显示；这有助于您查看进入和离开队列的项目。

   * **视图日志** ，用于访问复制代理执行的任何操作的日志。
   * **测试与目标实例的连接** 。
   * **如果需要** ，对任何队列项强制重试。
   >[!CAUTION]
   请勿将“测试连接”链接用于发布实例上的反向复制输出框。
   如果对发件箱队列执行复制测试，则所有早于测试复制的项目都将通过每个反向复制重新处理。
   如果此类项目已存在于队列中，则可以使用以下XPath JCR查询找到它们，并应该删除它们。
   `/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']`

同样，您可以开发一个解决方案来检测所有复制代理(位于 `/etc/replication/author` 或 `/etc/replication/publish`)，然后检查代理( `enabled`, `disabled`)和基础队列(、 `active`, `idle``blocked`)的状态。

## 监视性能 {#monitoring-performance}

[性能优化](/help/sites-deploying/configuring-performance.md) (Performance Optimization)是一个交互式过程，在开发过程中会获得焦点。 部署后，通常会在特定的间隔或事件后对其进行审阅。

在收集用于优化的信息时使用的方法也可用于进行持续监视。

>[!NOTE]
还可 [以检查可用于提高性能的](/help/sites-deploying/configuring-performance.md#configuring-for-performance) 特定配置。

以下列表出现的常见性能问题，以及如何发现和消除这些问题的建议。

| 区域 | 症状 | 要提高容量…… | 要减少音量…… |
|---|---|---|---|
| 客户端 | 客户端CPU使用率高。 | 安装性能更高的客户端CPU。 | 简化(HTML)布局。 |
|  | 服务器CPU使用率较低。 | 升级到更快的浏览器。 | 改进客户端缓存。 |
|  | 有些客户速度快，有些客户速度慢。 |  |  |
| 服务器 |  |  |  |
| 网络 | 服务器和客户端的CPU使用率都很低。 | 消除网络瓶颈。 | 改进／优化客户端缓存的配置。 |
|  | （相对而言）在服务器上本地浏览速度较快。 | 增加网络带宽。 | 减少网页的“权重”（例如，减少图像、优化的HTML）。 |
| Web服务器 | Web服务器上的CPU使用率很高。 | 群集您的Web服务器。 | 减少每页的点击量（访问）。 |
|  |  | 使用硬件负载平衡器。 |  |
| 应用程序 | 服务器CPU使用率很高。 | 集群AEM实例。 | 搜索和消除CPU和内存存储（使用代码检查、定时输出等）。 |
|  | 内存消耗高。 |  | 改进所有级别的缓存。 |
|  | 响应时间较短。 |  | 优化模板和组件（例如，结构、逻辑）。 |
| 存储库 |  |  |  |
| 缓存 |  |  |  |

性能问题可能源自与网站无关的许多原因，包括连接速度、CPU负载等方面的暂时性放缓。

它也可能影响您的所有访客，或仅影响其中的子集。

在优化常规性能或解决特定问题之前，需要获取、排序和分析所有这些信息。

* 在遇到性能问题之前：

   * 收集尽可能多的信息，以积累正常情况下系统的良好工作知识

* 遇到性能问题时：

   * 尝试使用一个（或更多）标准Web浏览器在您知道具有良好常规性能的其他客户端上和／或在服务器本身（如果可能）上复制它
   * 检查是否在适当的时间空间内发生了任何更改（与系统相关），以及这些更改中是否有任何可能影响性能
   * 提问，例如：

      * 问题是否仅在特定时间发生？
      * 问题是否仅出现在特定页面上？
      * 其他请求是否受到影响？
   * 收集与您在正常情况下的系统知识进行比较的尽可能多的信息：


### 用于监控和分析性能的工具 {#tools-for-monitoring-and-analyzing-performance}

下面简要概述了一些可用于监控和分析性能的工具。

其中一些将取决于您的操作系统。

<table>
 <tbody>
  <tr>
   <td>工具</td>
   <td>用于分析……</td>
   <td>使用情况／更多信息……</td>
  </tr>
  <tr>
   <td>request.log</td>
   <td>响应时间和并发性。</td>
   <td><a href="#interpreting-the-request-log">解释request.log</a>。</td>
  </tr>
  <tr>
   <td>桁架／地形</td>
   <td>页面加载</td>
   <td><p>用于跟踪系统调用和信号的Unix/Linux命令。 将日志级别提高到 <code>INFO</code>。</p> <p>分析每个请求的页面加载次数，包括哪些页面等。</p> </td>
  </tr>
  <tr>
   <td>线程转储</td>
   <td>观察JVM线程。 识别竞争、锁和长跑者。</td>
   <td><p>取决于操作系统：<br /> - Unix/Linux: <code>kill -QUIT &lt;<em>pid</em>&gt;</code><br /> - Windows（控制台模式）:Ctrl-Break<br /> </p> <p>分析工具也可用，如 <a href="https://java.net/projects/tda/">TDA</a>。<br /> </p> </td>
  </tr>
  <tr>
   <td>堆转储</td>
   <td>内存不足，导致性能降低。</td>
   <td><p>添加：<br /> 选项 <code>-XX:+HeapDumpOnOutOfMemoryError</code><br /> 中，单击此图标。</p> <p>请参阅 <a href="https://java.sun.com/javase/6/webnotes/trouble/TSG-VM/html/clopts.html#gbzrr">Java SE 6与热点虚拟机的疑难解答指南</a>。</p> </td>
  </tr>
  <tr>
   <td>系统调用</td>
   <td>确定时间问题。</td>
   <td><p>调用或 <code>System.currentTimeMillis()</code> . <code>com.day.util</code>Timing可用于根据代码或通过 <a href="#html-comments">HTML-comments生成时间戳</a>。</p> <p><strong>注意：</strong> 应实现这些功能，以便根据需要激活／取消激活它们；当系统运行顺利时，不需要收集统计信息的开销。</p> </td>
  </tr>
  <tr>
   <td>Apache Bench</td>
   <td>识别内存泄漏，有选择地分析响应时间。</td>
   <td><p>基本用法为：</p> <p><code>ab -k -n &lt;<em>requests</em>&gt; -c &lt;<em>concurrency</em>&gt; &lt;<em>url</em>&gt;</code></p> <p>有关 <a href="#apache-bench">完整详细信息</a> ，请参 <a href="https://httpd.apache.org/docs/2.2/programs/ab.html">阅Apache Bench和ab手册页</a> 。</p> </td>
  </tr>
  <tr>
   <td>搜索分析</td>
   <td> </td>
   <td>脱机执行搜索查询，识别查询响应时间，测试和确认结果集。<br /> </td>
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
   <td>观察JVM度量和线程。</td>
   <td><p>用法：jconsole</p> <p>请参 <a href="https://java.sun.com/developer/technicalArticles/J2SE/jconsole.html">阅使用</a> JConsole <a href="#monitoring-performance-using-jconsole">监视性能</a>。</p> <p><strong>注意：</strong> 借助JDK 1.6,JConsole可通过插件进行扩展；例如，Top或TDA（线程转储分析器）。</p> </td>
  </tr>
  <tr>
   <td>Java VisualVM</td>
   <td>观察JVM度量、线程、内存和概要分析。</td>
   <td><p>用法：jvisualvm或visualvm<br /> </p> <p>请参 <a href="https://java.sun.com/javase/6/docs/technotes/tools/share/jvisualvm.html">阅jvisualvm</a>、 <a href="https://visualvm.dev.java.net/">visualvm</a><a href="#monitoring-performance-using-j-visualvm">和使用(J)VisualVM监视性能</a>。</p> <p><strong>注意：</strong> 借助JDK 1.6,VisualVM可通过插件进行扩展。</p> </td>
  </tr>
  <tr>
   <td>桁架／地形，lsof</td>
   <td>深入的内核调用和进程分析(Unix)。</td>
   <td>Unix/Linux命令。</td>
  </tr>
  <tr>
   <td>计时统计信息</td>
   <td>请参阅页面渲染的计时统计信息。</td>
   <td><p>要查看页面渲染的计时统计信息，可 <strong>以将Ctrl-Shift-U</strong><code>?debugClientLibs=true</code> 与URL中的设置结合使用。</p> </td>
  </tr>
  <tr>
   <td>CPU和内存分析工具<br /> </td>
   <td><a href="#interpreting-the-request-log">在开发过程中分析慢速请求时使用</a>。</td>
   <td>例如， <a href="https://www.yourkit.com/">YourKit</a>。</td>
  </tr>
  <tr>
   <td><a href="#information-collection">信息收集</a></td>
   <td>您的安装的当前状态。</td>
   <td>尽可能地了解您的安装还有助于您跟踪可能导致性能变化的原因，以及这些更改是否合理。 需要定期收集这些指标，以便您能够轻松查看重大更改。</td>
  </tr>
 </tbody>
</table>

### 解释request.log {#interpreting-the-request-log}

此文件注册有关向AEM发出的每个请求的基本信息。 从中可以得出有价值的结论。

优惠 `request.log` 使用内置方式查看请求需要多长时间。 出于开发目的，它有助于 `tail -f` 观看 `request.log` 响应速度缓慢的情况。 要分析更大的 `request.log` 问题，我们建 [议您 `rlog.jar` 使用它来排序和筛选响应时间](#using-rlog-jar-to-find-requests-with-long-duration-times)。

我们建议将“慢”页面与页面隔离，然 `request.log`后单独调整这些页面以获得更好的性能。 这通常通过包括每个组件的性能指标或使用性能概要分析工具(如 ` [yourkit](https://www.yourkit.com/)`)来实现。

#### 监控网站上的流量 {#monitoring-traffic-on-your-website}

请求日志会记录发出的每个请求，以及作出的响应：

```xml
09:43:41 [66] -> GET /author/y.html HTTP/1.1
09:43:41 [66] <- 200 text/html 797ms
```

通过在特定时间段内（例如，在不同的24小时时间段内）汇总所有GET条目，您可以对您网站的平均流量进行声明。

#### 使用request.log监视响应时间 {#monitoring-response-times-with-the-request-log}

性能分析的一个好起点是请求日志：

`<*cq-installation-dir*>/crx-quickstart/logs/request.log`

日志如下所示（为简单起见，缩短了这些行）:

```xml
31/Mar/2009:11:32:57 +0200 [379] -> GET /path/x HTTP/1.1
31/Mar/2009:11:32:57 +0200 [379] <- 200 text/html 33ms
31/Mar/2009:11:33:17 +0200 [380] -> GET /path/y HTTP/1.1
31/Mar/2009:11:33:17 +0200 [380] <- 200 application/json 39ms
```

此日志每个请求或响应有一行：

* 发出每个请求或响应的日期。
* 请求的编号，用方括号表示。 此编号与请求和响应匹配。
* 一个箭头，指示这是请求（指向右侧的箭头）还是响应（向左箭头）。
* 对于请求，行包含：

   * 方法（通常为GET、HEAD或POST）
   * 请求的页面
   * 协议

* 对于响应，该行包含：

   * 状态代码(200表示“success”,404表示“page not found”
   * MIME类型
   * 响应时间

使用小脚本，您可以从日志文件中提取所需的信息并汇总所需的统计信息。 从中，您可以看到哪些页面或类型的页面速度较慢，以及整体性能是否令人满意。

#### 使用request.log监视搜索响应时间 {#monitoring-search-response-times-with-the-request-log}

搜索请求也会在日志文件中注册：

```xml
31/Mar/2009:11:35:34 +0200 [338] -> GET /author/playground/en/tools/search.html?query=dilbert&size=5&dispenc=utf-8 HTTP/1.1
31/Mar/2009:11:35:34 +0200 [338] <- 200 text/html 1562ms
```

因此，如上所述，您可以使用脚本提取相关信息并建立统计信息。

但是，一旦确定了响应时间，您可能需要分析请求花费的时间的原因以及可以采取什么措施来改进响应。

#### 监控并发用户的数量和影响 {#monitoring-the-number-and-impact-of-concurrent-users}

同样， `request.log` 该系统还可用于监控并发和系统对它的反应。

必须进行测试，以确定系统可处理的并发用户数，才能看到负面影响。 同样，脚本可用于从日志文件中提取结果：

* 监视在特定时间范围内发出的请求数，例如1分钟
* 测试特定数量的用户在（尽可能接近）同时发出相同请求的效果；例如，30个用户同时单 **击** “保存”。

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

AEM包括位于以下位置的各种帮助工具：
`<*cq-installation-dir*>/crx-quickstart/opt/helpers`

其中一个可 `rlog.jar`用于快速排序，以便按持续时间 `request.log` （从最长到最短的时间）显示请求。

以下命令显示了可能的参数：

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

例如，您可以运行它，将 `request.log` 文件指定为参数并显示持续时间最长的10个第一个请求：

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

如果需要对大数据样本执 `request.log` 行此操作，您可能需要连接单个文件。

### Apache Bench {#apache-bench}

为了最大限度地减少特殊情况（如垃圾收集等）的影响，建议使用诸如 `apachebench` (例如， [ab](https://httpd.apache.org/docs/2.2/programs/ab.html) ，获取更多文档)这样的工具来帮助识别内存泄漏并有选择地分析响应时间。

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

以上数字取自访问geometrixx公司页面的标准MAcBook Pro笔记本电脑（2010年中），如默认AEM安装中所示。 页面非常简单，但并未针对性能进行优化。

`apachebench` 还以平均方式显示每个请求的时间，即所有并发请求；请参 `Time per request: 54.595 [ms]` 阅（平均值，跨所有并发请求）。 您可以更改并发参数的值( `-c` 一次要执行的多个请求数)以查看任何效果。

### 请求计数器 {#request-counters}

有关请求流量（特定时间段内的请求数）的信息会指示实例的负载。 此信息可从 [request.log提取](#interpreting-the-request-log)，但使用计数器将自动收集数据，以便您查看：

* 在活动方面存在显着差异(即区分“许多请求”和“低活动”)
* 当不使用实例时
* 任何重新启动（计数器重置为0）

要自动收集信息，您还可以安装RequestFilter以在每个请求中增加计数器。 多个计数器可用于不同的时间段。

收集的信息可用于指示：

* 活动之重大变动
* 冗余实例
* 任何重新启动（计数器重置为0）

### HTML注释 {#html-comments}

建议每个项目都包含服务 `html comments` 器性能。 许多好的公开例子，选择页面，打开页面源进行查看并滚动到底部，可看到以下代码：

```xml
</body>
 </html>
        <!--
        Page took 58 milliseconds to be rendered by server
         -->
```

### 使用JConsole监控性能 {#monitoring-performance-using-jconsole}

工具命令 `jconsole` 随JDK一起提供。

1. 开始AEM实例。
1. 运行 `jconsole.`
1. 选择您的AEM实例和 **Connect**。

1. 在应用程序 `Local` 中，多次单击 `com.day.crx.quickstart.Main`;概述将显示为默认值：

   ![chlimage_1-1](assets/chlimage_1-1.png)

   之后，您可以选择其他选项。

### 使用(J)VisualVM监控性能 {#monitoring-performance-using-j-visualvm}

自JDK 1.6起，工具命令便 `jvisualvm` 可用。 安装JDK 1.6后，您可以：

1. 开始AEM实例。

   >[!NOTE]
   如果使用Java 5，则可以将参 `-Dcom.sun.management.jmxremote` 数添加到开始JVM的java命令行。 默认情况下，JMX在Java 6中处于启用状态。

1. 运行以下任一操作：

   * `jvisualvm`:在JDK 1.6 bin文件夹中（测试版）
   * `visualvm`:可从VisualVM [](https://visualvm.dev.java.net/) （最低版本）下载

1. 在应用程序 `Local` 中，多次单击 `com.day.crx.quickstart.Main`;概述将显示为默认值：

   ![chlimage_1-2](assets/chlimage_1-2.png)

   之后，您可以选择其他选项，包括监视器：

   ![chlimage_1-3](assets/chlimage_1-3.png)

您可以使用此工具生成线程转储和内存头转储。 技术支持团队经常要求提供此信息。

### 信息收集 {#information-collection}

尽可能地了解您的安装有助于您了解可能导致性能变化的原因，以及这些更改是否合理。 需要定期收集这些指标，以便您能够轻松查看重大更改。

以下信息可能很有用：

* [有多少作者使用该系统？](#how-many-authors-are-working-with-the-system)
* [每日平均页面激活数是多少？](#what-is-the-average-number-of-page-activations-per-day)
* [您当前在此系统上维护多少页？](#how-many-pages-do-you-currently-maintain-on-this-system)
* [如果使用MSM，则每月平均转出次数是多少？](#if-you-use-msm-what-is-the-average-number-of-rollouts-per-month)
* [每月Live Copy的平均数量是多少？](#what-is-the-average-number-of-live-copies-per-month)
* [如果您使用AEM资产，您当前在资产中维护的资产数量是多少？](#ifyouusecqdamhowmanyassetsdoyoucurrentlymaintainincqdam)
* [资产的平均大小是多少？](#what-is-the-average-size-of-the-assets)
* [当前使用了多少个模板？](#how-many-templates-are-currently-used)
* [当前使用了多少个组件？](#how-many-components-are-currently-used)
* [在高峰时间，创作系统每小时有多少个请求？](#how-many-requests-per-hour-do-you-have-on-the-author-system-at-peak-time)
* [在高峰时间，发布系统每小时有多少个请求？](#how-many-requests-per-hour-do-you-have-on-the-publish-system-at-peak-time)

#### 有多少作者使用该系统？ {#how-many-authors-are-working-with-the-system}

要查看自安装以来使用系统的作者人数，请使用命令行：

```shell
cd <cq-installation-dir>/crx-quickstart/logs
cut -d " " -f 3 access.log | sort -u | wc -l
```

要查看在给定日期工作的作者人数，请执行以下操作：

```shell
grep "<date>" access.log | cut -d " " -f 3 | sort -u | wc -l
```

#### 每日平均页面激活数是多少？ {#what-is-the-average-number-of-page-activations-per-day}

查看自服务器安装以来使用存储库激活的页面查询总数；通过CRXDE —— 工具-查询:

* **类型** `XPath`

* **路径** `/`

* **查询**`//element(*, cq:AuditEvent)[@cq:type='Activate']`

然后计算自安装以来经过的天数以计算平均值。

#### 您当前在此系统上维护多少页？ {#how-many-pages-do-you-currently-maintain-on-this-system}

要查看服务器上当前的页数，请使用存储库查询;通过CRXDE —— 工具-查询:

* **类型** `XPath`

* **路径** `/`

* **查询**`//element(*, cq:Page)`

#### 如果使用MSM，则每月平均转出次数是多少？ {#if-you-use-msm-what-is-the-average-number-of-rollouts-per-month}

确定自安装以来使用存储库查询的转出总数；通过CRXDE —— 工具-查询:

* **类型** `XPath`

* **路径** `/`

* **查询**`//element(*, cq:AuditEvent)[@cq:type='PageRolledOut']`

计算自安装以来已用的月数以计算平均值。

#### 每月Live Copy的平均数量是多少？ {#what-is-the-average-number-of-live-copies-per-month}

确定自安装以来创建的Live Copy总数，使用存储库查询;通过CRXDE —— 工具-查询:

* **类型** `XPath`

* **路径** `/`

* **查询**`//element(*, cq:LiveSyncConfig)`

再次使用自安装以来已用过的月数来计算平均值。

#### 如果您使用AEM资产，您当前在资产中维护的资产数量是多少？ {#if-you-use-aem-assets-how-many-assets-do-you-currently-maintain-in-assets}

要查看您当前维护的DAM资产数量，请使用存储库查询;通过CRXDE —— 工具-查询:

* **类型** `XPath`
* **路径** `/`
* **查询**`/jcr:root/content/dam//element(*, dam:Asset)`

#### 资产的平均大小是多少？ {#what-is-the-average-size-of-the-assets}

要确定文件夹的总大小，请执行以 `/var/dam` 下操作：

1. 使用WebDAV将存储库映射到本地文件系统。

1. 使用命令行：

   ```shell
   cd /Volumes/localhost/var
   du -sh dam/
   ```

   要获取平均大小，请将全局大小除以（在上面获取）中的 `/var/dam` 资产总数。

#### 当前使用了多少个模板？ {#how-many-templates-are-currently-used}

要查看服务器上当前的模板数，请使用存储库查询;通过CRXDE —— 工具-查询:

* **类型** `XPath`
* **路径** `/`
* **查询**`//element(*, cq:Template)`

#### 当前使用了多少个组件？ {#how-many-components-are-currently-used}

要查看服务器上当前的组件数，请使用存储库查询;通过CRXDE —— 工具-查询:

* **类型** `XPath`
* **路径** `/`
* **查询**`//element(*, cq:Component)`

#### 在高峰时间，创作系统每小时有多少个请求？ {#how-many-requests-per-hour-do-you-have-on-the-author-system-at-peak-time}

要确定在高峰期您在创作系统上的每小时请求数，请执行以下操作：

1. 要确定自安装以来请求的总数，请使用命令行：

   ```shell
   cd <cq-installation-dir>/crx-quickstart/logs
   grep -R "\->" request.log | wc -l
   ```

1. 要确定开始和结束日期，请执行以下操作：

   ```shell
   vim request.log
   G / 1G: for the last/first lines
   ```

   使用这些值可计算自安装以来已用的小时数，然后计算每小时的平均请求数。

#### 在高峰时间，发布系统每小时有多少个请求？ {#how-many-requests-per-hour-do-you-have-on-the-publish-system-at-peak-time}

对发布实例重复上述步骤。

## 分析特定场景 {#analyzing-specific-scenarios}

以下是一列表建议，说明在开始遇到某些性能问题时要检查什么。 列表（不幸的是）并不完全全面。

>[!NOTE]
另请参阅以下文章以了解更多信息：
* [线程转储](https://helpx.adobe.com/experience-manager/kb/TakeThreadDump.html)
* [分析内存问题](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)
* [使用内置概要分析器进行分析](https://helpx.adobe.com/experience-manager/kb/AnalyzeUsingBuiltInProfiler.html)
* [分析慢速和阻止的进程](https://helpx.adobe.com/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)



### 100%的CPU {#cpu-at}

如果系统的CPU持续以100%的速度运行，请查看：

* 知识库：

   * [分析慢速和阻止的进程](https://helpx.adobe.com/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)

### 内存不足 {#out-of-memory}

尽管在开发和测试过程中应检测到此类错误，但某些情形可能会漏掉。

如果系统内存不足，可以通过各种方式查看此问题，包括性能下降和包含子文本的错误消息：

`java.lang.OutOfMemoryError`

在这些情况下，请检查：

* 用于 [开始AEM的JVM设置](/help/sites-deploying/deploy.md#getting-started)
* 知识库：

   * [分析内存问题](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)

### 磁盘I/O {#disk-i-o}

如果系统磁盘空间不足，或者您注意到磁盘崩溃开始，请参阅：

* 您是否已禁用调试信息的集合；可以在以下不同位置进行配置：

   * [Apache Sling JSP脚本处理程序](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjspscripthandler)
   * [Apache Sling Java脚本处理程序](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjavascripthandler)
   * [Apache Sling日志配置](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration)
   * [CQ HTML库管理器](/help/sites-deploying/osgi-configuration-settings.md#daycqhtmllibrarymanager)
   * [CQ WCM调试过滤器](/help/sites-deploying/osgi-configuration-settings.md#daycqwcmdebugfilter)
   * [伐木工](/help/sites-deploying/monitoring-and-maintaining.md#activating-the-debug-log-level)[](/help/sites-deploying/configuring.md#loggersandwritersforindividualservices)

* 是否以及如何配置版 [本清除](/help/sites-deploying/version-purging.md)
* 知识库：

   * [打开的文件过多](https://helpx.adobe.com/experience-manager/kb/TooManyOpenFiles.html)
   * [日志占用太多磁盘空间](https://helpx.adobe.com/experience-manager/kb/JournalTooMuchDiskSpace.html)

### 常规性能降级 {#regular-performance-degradation}

如果您看到实例的性能在每次重新启动后（有时为一周或更长时间）恶化，则可以检查以下内容：

* [内存不足](#outofmemory)
* 知识库：

   * [未结束的会话](https://helpx.adobe.com/experience-manager/kb/AnalyzeUnclosedSessions.html)

### JVM调整 {#jvm-tuning}

Java虚拟机(JVM)在调整方面已有显着改进（特别是自Java 7以来）。 因此，指定合理的固定JVM大小和使用默认值通常是合适的。

如果默认设置不合适，则在尝试调整JVM之前，必须建立一种方法来监视和评估GC性能；这可能涉及监视因素，包括堆大小、算法等。

一些常见选择是：

* VerboseGC:

   ```
   -verbose:gc \
    -Xloggc:$LOGS/verbosegc.log \
    -XX:+PrintGCDetails \
    -XX:+PrintGCDateStamps
   ```

生成的日志可由GC可视器摄取，如：

` [https://www.ibm.com/developerworks/library/j-ibmtools2/](https://www.ibm.com/developerworks/library/j-ibmtools2/)`

或JConsole:

* 这些设置用于“宽开放”JMX连接：

   ```
   -Dcom.sun.management.jmxremote \
    -Dcom.sun.management.jmxremote.port=8889 \
    -Dcom.sun.management.jmxremote.authenticate=false \
    -Dcom.sun.management.jmxremote.ssl=false
   ```

* 然后使用JConsole连接到JVM;请参阅：
   ` [https://docs.oracle.com/javase/6/docs/technotes/guides/management/jconsole.html](https://docs.oracle.com/javase/6/docs/technotes/guides/management/jconsole.html)`

这将帮助您了解使用了多少内存、GC算法的使用情况、运行时间以及这对应用程序性能的影响。 如果没有这种情况，调音就只是“随手摇动的旋钮”。

>[!NOTE]
对于Oracle的VM，还有以下信息：
[https://docs.oracle.com/javase/7/docs/technotes/guides/vm/server-class.html](https://docs.oracle.com/javase/7/docs/technotes/guides/vm/server-class.html)