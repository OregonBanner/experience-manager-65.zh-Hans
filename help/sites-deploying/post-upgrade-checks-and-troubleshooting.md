---
title: 升级后检查和疑难解答
seo-title: 升级后检查和疑难解答
description: 了解如何对升级后可能显示的问题进行故障诊断。
seo-description: 了解如何对升级后可能显示的问题进行故障诊断。
uuid: 3f525f2c-8d25-4bb8-a57e-3adf667edde8
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: 5a67aa9f-e5eb-4d7e-89da-2ee1a45eb8ce
docset: aem65
feature: 升级
exl-id: ceac2b52-6885-496d-9517-5fc7291ad070
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1830'
ht-degree: 0%

---

# 升级后检查和疑难解答{#post-upgrade-checks-and-troubleshooting}

## 升级后检查{#post-upgrade-checks}

在[就地升级](/help/sites-deploying/in-place-upgrade.md)之后，应执行以下活动以完成升级。 假定AEM已从6.5 jar启动，并且已部署升级的代码库。

* [验证日志是否升级成功](#main-pars-header-290365562)

* [验证OSGi包](#main-pars-header-1637350649)

* [验证Oak版本](#main-pars-header-1293049773)

* [Inspect PreUpgradeBackup文件夹](#main-pars-header-988995987)

* [页面的初始验证](#main-pars-header-20827371)
* [应用AEM Service Pack](#main-pars-header-215142387)

* [迁移AEM功能](#main-pars-header-1434457709)

* [验证计划维护配置](#main-pars-header-1552730183)

* [启用复制代理](#main-pars-header-823243751)

* [启用自定义计划作业](#main-pars-header-244535083)

* [执行测试计划](#main-pars-header-1167972233)

### 验证升级成功的日志{#verify-logs-for-upgrade-success}

**upgrade.log**

过去，检查实例的升级后状态需要仔细检查各种日志文件、存储库的部分和启动板。 生成升级后报告有助于在上线前检测有缺陷的升级。

此功能的主要目的是减少需要跨多个端点进行手动解释或复杂解析逻辑的情况，以确定升级是否成功。 该解决方案旨在为外部自动化系统提供明确的信息，以便对更新的成功或已识别的失败做出反应。

更具体地说，它确保：

* 升级框架检测到的升级失败可以集中在单个升级报告中；
* 升级报告包括关于必要手动干预的指标。

为了适应此情况，已对`upgrade.log`文件中生成日志的方式进行了更改。

以下是升级期间未显示错误的示例报表：

![1487887443006](assets/1487887443006.png)

以下是一个示例报表，其中显示了升级过程中未安装的包：

![1487887532730](assets/1487887532730.png)

**error.log**

在使用目标版本jar启动AEM期间和之后，应仔细查看error.log。 应审核任何警告或错误。 通常最好在日志开头查找问题。 日志中稍后发生的错误实际上可能是文件早期调用的根本原因的副作用。 如果出现重复的错误和警告，请参阅下面的[分析升级问题](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md#analyzing-issues-with-the-upgrade)。

### 验证OSGi包{#verify-osgi-bundles}

导航到OSGi控制台`/system/console/bundles`，然后查看是否未启动任何包。 如果有任何包处于安装状态，请咨询`error.log`以确定根问题。

### 验证Oak版本{#verify-oak-version}

升级后，您应会看到Oak版本已更新为&#x200B;**1.10.2**。 要验证Oak版本，请导航到OSGi控制台并查看与Oak包关联的版本：Oak Core、Oak Commons、Oak Segment Tar。

### Inspect PreUpgradeBackup文件夹{#inspect-preupgradebackup-folder}

在升级过程中，AEM将尝试备份自定义项并将其存储在`/var/upgrade/PreUpgradeBackup/<time-stamp-of-upgrade>`下。 要在CRXDE Lite中查看此文件夹，您可能需要[临时启用CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md)。

带有时间戳的文件夹应具有名为`mergeStatus`的属性，其值为`COMPLETED`。 **to-process**&#x200B;文件夹应为空，**被覆盖的**&#x200B;节点指示升级期间覆盖了哪些节点。 **pecting**&#x200B;节点下方的内容表示升级期间无法安全合并的内容。 如果您的实施依赖于任何子节点（并且尚未由升级的代码包安装），则需要手动合并这些节点。

如果在暂存或生产环境中，则在执行本练习后禁用CRXDE Lite。

### 页面{#initial-validation-of-pages}的初始验证

在AEM中对多个页面执行初始验证。 如果升级创作环境，请打开开始页面和欢迎页面(`/aem/start.html`、`/libs/cq/core/content/welcome.html`)。 在创作和发布环境中，会打开一些应用程序页面并进行烟雾测试，以确保它们能够正确呈现。 如果出现任何问题，请咨询`error.log`以进行故障排除。

### 应用AEM Service Pack {#apply-aem-service-packs}

应用任何相关的AEM 6.5 Service Pack（如果已发布）。

### 迁移AEM功能{#migrate-aem-features}

AEM中的几项功能在升级后需要执行其他步骤。 在[升级代码和自定义](/help/sites-deploying/upgrading-code-and-customizations.md)页面上，可以找到这些功能以及在AEM 6.5中迁移这些功能的步骤的完整列表。

### 验证计划维护配置{#verify-scheduled-maintenance-configurations}

#### 启用数据存储垃圾收集{#enable-data-store-garbage-collection}

如果使用文件数据存储，请确保已启用数据存储垃圾收集任务并将其添加到每周维护列表。 此处](/help/sites-administering/data-store-garbage-collection.md)列出了说明。[

>[!NOTE]
>
>对于S3自定义数据存储安装或使用共享数据存储时，不建议这样做。

#### 启用联机修订版清理{#enable-online-revision-cleanup}

如果使用MongoMK或新的TarMK区段格式，请确保已启用修订清理任务并将其添加到每日维护列表。 此处](/help/sites-deploying/revision-cleanup.md)列出的说明。[

### 执行测试计划{#execute-test-plan}

根据&#x200B;**测试过程**&#x200B;部分下定义的[升级代码和自定义](/help/sites-deploying/upgrading-code-and-customizations.md)执行详细的测试计划。

### 启用复制代理{#enable-replication-agents}

完全升级和验证发布环境后，请在创作环境中启用复制代理。 验证代理是否能够连接到相应的发布实例。 有关事件顺序的更多详细信息，请参阅U [升级过程](/help/sites-deploying/upgrade-procedure.md) 。

### 启用自定义计划作业{#enable-custom-scheduled-jobs}

此时，任何作为代码库一部分的计划作业都可以启用。

## 分析升级{#analyzing-issues-with-upgrade}中的问题

本节包含在升级到AEM 6.3的过程中可能遇到的一些问题情景。

这些方案应有助于跟踪与升级相关问题的根本原因，并应有助于确定项目或产品特定问题。

### 存储库迁移失败{#repository-migration-failing-}

从CRX2到Oak的数据迁移对于任何以基于CQ 5.4的源实例开始的情景都应该是可行的。请确保您完全遵循本文档中的升级说明（包括`repository.xml`的准备），确保没有通过JAAS启动自定义身份验证，并且在开始迁移之前已检查实例是否存在不一致。

如果迁移仍然失败，您可以通过检查`upgrade.log`找出根本原因。 如果问题尚未知晓，请向客户支持报告。

### 升级未运行{#the-upgrade-did-not-run}

在开始准备步骤之前，请确保首先使用java -jar aem-quickstart.jar命令执行&#x200B;**source**&#x200B;实例。 这是必需的，以确保正确生成quickstart.properties文件。 如果缺少，则升级将无法正常进行。 或者，您也可以通过查看源实例安装文件夹的`crx-quickstart/conf`下的来检查文件是否存在。 此外，在启动AEM以开始升级时，必须使用java -jar aem-quickstart.jar命令执行该操作。 在升级模式下，从开始脚本开始不会启动AEM。

### 包和包无法更新{#packages-and-bundles-fail-to-update-}

如果升级期间无法安装包，则包中包含的包也不会更新。 此类问题通常由数据存储配置错误引起。 它们还将在error.log中显示为&#x200B;**ERROR**&#x200B;和&#x200B;**WARN**&#x200B;消息。 由于在大多数情况下，默认登录可能无法正常工作，因此您可以直接使用CRXDE来检查和查找配置问题。

### 某些AEM包未切换到活动状态{#some-aem-bundles-are-not-switching-to-the-active-state}

如果包未启动，则应检查是否存在任何未满足的依赖项。

如果存在此问题，但该问题基于包安装失败，导致包未升级，则它们将被视为与新版本不兼容。 有关如何对此进行故障诊断的更多信息，请参阅上面的&#x200B;**包和包无法更新**。

还建议将新AEM 6.5实例的包列表与已升级的实例进行比较，以检测未升级的包。 这将在`error.log`中提供更详细的搜索内容。

### 自定义包未切换到活动状态{#custom-bundles-not-switching-to-the-active-state}

如果自定义包未切换到活动状态，则很可能存在未导入更改API的代码。 这通常会导致不满足的依赖关系。

在以前的某个版本中，删除的API应标记为已弃用。 您可以在此弃用通知中找到有关直接迁移代码的说明。 Adobe旨在尽可能实现语义版本控制，以便版本可以指示中断更改。

最好还是检查是否绝对有必要对问题做出更改，如果不必要，还是还原。 另外，在严格的语义版本控制后，还检查是否超出必要时增加了包导出的版本。

### 运行不良的平台UI {#malfunctioning-platform-ui}

如果某些UI功能在升级后无法正常运行，则应首先检查界面的自定义叠加。 某些结构可能已更改，并且叠加可能需要更新或已过时。

接下来，检查是否存在任何可跟踪到已将自定义扩展添加到客户端库的Javascript错误。 这同样适用于可能导致AEM布局问题的自定义CSS。

最后，检查Javascript可能无法处理的配置错误。 通常情况下，失效扩展会被不正确停用。

### 自定义组件、模板或UI扩展出现故障{#malfunctioning-custom-components-templates-or-ui-extensions}

在大多数情况下，这些问题的根本原因与未启动的包或未安装的包的根本原因相同，只是问题在首次使用组件时开始出现的唯一差异。

处理错误自定义代码的方法是首先进行烟雾测试，以识别原因。 找到该建议后，请查看文章[链接]部分中的推荐，以了解修复这些建议的方法。

### /etc {#missing-customizations-under-etc}下缺少自定义设置

`/apps` 和可 `/libs` 由升级很好地处理，但升级后可 `/etc` 能需要手动从中恢复 `/var/upgrade/PreUpgradeBackup` 下的更改。确保检查此位置，以查找需要手动合并的任何内容。

### 分析error.log和upgrade.log {#analyzing-the-error.log-and-upgrade.log}

在大多数情况下，需要查阅日志以查找错误原因。 但是，在升级时，还需要监控依赖关系问题，因为旧包可能无法正确升级。

执行此操作的最佳方法是删除error.log ，方法是删除所有与您面临的问题无关的消息。 为此，您可以使用以下工具（如grep）：

```shell
grep -v UnrelatedErrorString
```

某些错误消息可能不会立即解释。 在这种情况下，查看发生错误的上下文也有助于了解错误的创建位置。 您可以使用以下方法来分隔错误：

* `grep -B` 在错误前添加行；

或

* `grep -A` 添加行。

在少数情况下，还会发现WARN消息错误，因为可能存在导致此状态的有效案例，并且应用程序并不总是能够确定这是否是实际错误。 另请务必查阅这些邮件。

### 联系Adobe支持{#contacting-adobe-support}

如果您已通过此页面上的建议，但仍遇到问题，请联系Adobe支持。 要向处理您案例的支持工程师提供尽可能多的信息，请确保从升级中包含upgrade.log文件。
