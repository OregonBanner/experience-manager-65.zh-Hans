---
title: 升级后检查和疑难解答
seo-title: 升级后检查和疑难解答
description: 了解如何解决升级后可能出现的问题。
seo-description: 了解如何解决升级后可能出现的问题。
uuid: 3f525f2c-8d25-4bb8-a57e-3adf667edde8
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: 5a67aa9f-e5eb-4d7e-89da-2ee1a45eb8ce
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 升级后检查和疑难解答{#post-upgrade-checks-and-troubleshooting}

## 升级后检查 {#post-upgrade-checks}

在就 [地升级后](/help/sites-deploying/in-place-upgrade.md) ，应执行以下活动以完成升级。 假定AEM已从6.5 jar启动，并且已部署升级的代码库。

* [验证日志是否升级成功](#main-pars-header-290365562)

* [验证OSGi捆绑包](#main-pars-header-1637350649)

* [验证Oak版本](#main-pars-header-1293049773)

* [检查PreUpgradeBackup文件夹](#main-pars-header-988995987)

* [页面的初始验证](#main-pars-header-20827371)
* [应用AEM Service Pack](#main-pars-header-215142387)

* [迁移AEM功能](#main-pars-header-1434457709)

* [验证计划维护配置](#main-pars-header-1552730183)

* [启用复制代理](#main-pars-header-823243751)

* [启用自定义计划作业](#main-pars-header-244535083)

* [执行测试计划](#main-pars-header-1167972233)

### 验证日志是否升级成功 {#verify-logs-for-upgrade-success}

**upgrade.log**

过去，检查实例的升级后状态需要仔细检查各种日志文件、存储库的部分和启动板。 生成升级后报告有助于在上线前检测有缺陷的升级。

此功能的主要目的是减少需要手动解释或跨多个端点的复杂解析逻辑才能确定升级成功与否。 该解决方案旨在为外部自动化系统提供明确的信息，以便对更新的成功或已识别的失败做出反应。

更具体地说，它确保：

* 升级框架检测到的升级故障可以集中在单个升级报告中；
* 升级报告包括关于必要手动干预的指标。

为了适应这一点，对文件中生成日志的方式进行了 `upgrade.log` 更改。

以下是一个示例报告，它在升级过程中不显示错误：

![1487887443006](assets/1487887443006.png)

以下是一个示例报告，其中显示了升级过程中未安装的包：

![1487887532730](assets/1487887532730.png)

**error.log**

在使用目标版本jar启动AEM期间和之后，应仔细查看error.log。 应查看任何警告或错误。 通常，最好在日志的开头查找问题。 日志中稍后出现的错误实际上可能是根本原因的副作用，而根本原因在文件的早期被调用。 如果出现重复的错误和警告，请参阅下 [面的升级问题分析](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md#analyzing-issues-with-the-upgrade)。

### 验证OSGi捆绑包 {#verify-osgi-bundles}

导航到OSGi控制 `/system/console/bundles` 台并查看是否未启动任何捆绑包。 如果任何捆绑包处于安装状态，请咨询 `error.log` 以确定根问题。

### 验证Oak版本 {#verify-oak-version}

升级后，您应该会看到Oak版本已更 **新至1.10.2**。 要验证Oak版本，请导航到OSGi控制台，并查看与Oak捆绑套件相关的版本：Oak Core、Oak Commons、Oak Segment Tar。

### 检查PreUpgradeBackup文件夹 {#inspect-preupgradebackup-folder}

在升级过程中，AEM将尝试备份自定义内容并将其存储在下方 `/var/upgrade/PreUpgradeBackup/<time-stamp-of-upgrade>`。 要在CRXDE lite中查看此文件夹，您可能需要临 [时启用CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md)。

带有时间戳的文件夹应具有一个名为的 `mergeStatus` 属性，其值为 `COMPLETED`。 待处 **理文件夹应为空** ，并且“覆盖”节点 **** 指示在升级期间覆盖了哪些节点。 剩余节点下 **的内容** ，表示在升级过程中无法安全合并的内容。 如果您的实施依赖于任何子节点（并且升级的代码包尚未安装），则需要手动合并这些节点。

在舞台或生产环境中，在本练习后禁用CRXDE Lite。

### 页面的初始验证 {#initial-validation-of-pages}

在AEM中对多个页面执行初始验证。 如果升级创作环境，请打开开始页和欢迎页( `/aem/start.html`, `/libs/cq/core/content/welcome.html`)。 在创作和发布环境中，打开几个应用程序页面并进行烟度测试，它们可以正确呈现。 如果出现任何问题，请咨询 `error.log` 以进行疑难解答。

### 应用AEM Service Pack {#apply-aem-service-packs}

应用任何相关的AEM 6.5 Service Pack（如果已发布）。

### 迁移AEM功能 {#migrate-aem-features}

AEM中的若干功能需要升级后执行其他步骤。 在升级代码和自定义页面上可以找到这些功能以及在AEM 6.5中迁移这些功能和步骤 [的完整列表](/help/sites-deploying/upgrading-code-and-customizations.md) 。

### 验证计划维护配置 {#verify-scheduled-maintenance-configurations}

#### Enable Data Store Garbage Collection {#enable-data-store-garbage-collection}

如果使用文件数据存储，请确保已启用“数据存储垃圾收集”任务并将其添加到“每周维护”列表。 此处列出 [说明](/help/sites-administering/data-store-garbage-collection.md)。

>[!NOTE]
>
>对于S3自定义数据存储安装或在使用共享数据存储时，不建议这样做。

#### 启用联机修订清除 {#enable-online-revision-cleanup}

如果使用MongoMK或新的TarMK段格式，请确保启用“修订清理”任务并将其添加到“每日维护”列表。 此处概述 [的说明](/help/sites-deploying/revision-cleanup.md)。

### 执行测试计划 {#execute-test-plan}

根据“测试过程”部分中定义的“ [升级代码和自定义](/help/sites-deploying/upgrading-code-and-customizations.md) ”执行详 **细的测试计划** 。

### 启用复制代理 {#enable-replication-agents}

发布环境完全升级和验证后，在创作环境上启用复制代理。 验证代理是否能够连接到相应的发布实例。 有关事件 [顺序的更多详细信息](/help/sites-deploying/upgrade-procedure.md) ，请参阅升级过程。

### 启用自定义计划作业 {#enable-custom-scheduled-jobs}

此时，可以启用作为代码库一部分的任何计划作业。

## 分析升级问题 {#analyzing-issues-with-upgrade}

本节包含在升级到AEM 6.3的过程中可能遇到的一些问题方案。

这些方案应有助于跟踪与升级相关问题的根本原因，并有助于确定项目或产品特定问题。

### 存储库迁移失败 {#repository-migration-failing-}

从CRX2到Oak的数据迁移对于从基于CQ 5.4的源实例开始的任何场景都是可行的。确保您完全按照本文档中的升级说明（包括准备）进行操作 `repository.xml`，确保没有通过JAAS启动自定义身份验证器，并且在开始迁移之前已检查实例是否不一致。

如果迁移仍然失败，您可以通过检查找出根本原因 `upgrade.log`。 如果问题尚未确定，请向客户支持报告。

### 升级未运行 {#the-upgrade-did-not-run}

在开始准备步骤之前，请确保首先 **运行** source实例，方法是使用java -jar aem-quickstart.jar命令执行它。 这是必需的，以确保正确生成quickstart.properties文件。 如果缺少，则升级将无法正常运行。 或者，您也可以查看源实例的安装文件夹中 `crx-quickstart/conf` 的下方来检查文件是否存在。 此外，启动AEM以开始升级时，必须使用java -jar aem-quickstart.jar命令执行该升级。 从开始脚本启动不会在升级模式下启动AEM。

### 包和包无法更新 {#packages-and-bundles-fail-to-update-}

如果升级期间无法安装包，则它们包含的包也不会更新。 此类问题通常由数据存储配置错误引起。 它们还将在error.log **中显示****为ERROR** 和WARN消息。 由于在大多数情况下，默认登录可能无法工作，因此您可以直接使用CRXDE来检查和查找配置问题。

### 某些AEM包未切换到活动状态 {#some-aem-bundles-are-not-switching-to-the-active-state}

如果捆绑包未启动，您应检查是否存在任何未满足的依赖关系。

如果存在此问题，但是它基于包安装失败（导致包不进行升级），则它们将被视为与新版本不兼容。 有关如何解决此问题的详细信息，请参 **阅上面的包和包无法更新** 。

还建议将新AEM 6.5实例的捆绑列表与升级实例进行比较，以检测未升级的捆绑。 这将提供更详细的搜索范围 `error.log`。

### 不切换到活动状态的自定义包 {#custom-bundles-not-switching-to-the-active-state}

如果您的自定义捆绑包未切换到活动状态，则极有可能存在未导入更改API的代码。 这通常会导致不满足的依赖关系。

删除的API应在以前的某个版本中标记为已弃用。 您可能会在此弃用通知中找到有关直接迁移代码的说明。 Adobe旨在尽可能实现语义版本控制，以便版本可以指示更改。

最好还是检查导致问题的更改是否绝对必要，如果不必要，还是还原。 另外，请检查在严格的语义版本控制下，包导出的版本增加是否超出必要。

### 故障平台UI {#malfunctioning-platform-ui}

如果某些UI功能在升级后无法正常工作，您应首先检查界面的自定义叠加。 某些结构可能已更改，并且叠加可能需要更新或已过时。

接下来，检查是否有任何Javascript错误，这些错误可以跟踪到已连接到客户端库的自定义添加扩展。 同样，自定义CSS也可能会导致AEM布局出现问题。

最后，检查Javascript可能无法处理的配置错误。 通常情况下，不正确取消激活扩展。

### 故障自定义组件、模板或UI扩展 {#malfunctioning-custom-components-templates-or-ui-extensions}

在大多数情况下，这些问题的根本原因与未启动的包或未安装的包的根本原因相同，但问题在首次使用组件时开始出现的唯一区别。

处理错误的自定义代码的方法是首先执行烟雾测试以识别原因。 找到该建议后，请查看文章的此链接 [部分] ，了解修复建议的方法。

### /etc下缺少自定义 {#missing-customizations-under-etc}

`/apps` 并且 `/libs` 由升级很好地处理，但升级后可能 `/etc` 需要手动恢复下面的更 `/var/upgrade/PreUpgradeBackup` 改。 确保检查此位置是否有需要手动合并的任何内容。

### 分析error.log和upgrade.log {#analyzing-the-error.log-and-upgrade.log}

在大多数情况下，需要查询日志以查找错误的原因。 但是，在进行升级时，也必须监视依赖关系问题，因为旧的捆绑包可能无法正确升级。

执行此操作的最佳方法是删除所有与您面临的问题无关的消息，从而删除error.log。 您可以使用以下工具（如grep）执行此操作：

```shell
grep -v UnrelatedErrorString
```

某些错误消息可能不会立即解释。 在这种情况下，查看发生错误的上下文也有助于了解错误的创建位置。 您可以使用以下方法分隔错误：

* `grep -B` 在错误前添加行；

或

* `grep -A` 用于在之后添加行。

在一些情况下，也可以找到WARN消息，因为可能存在导致此状态的有效案例，并且应用程序并不总是能够确定这是否为实际错误。 确保您也查阅这些消息。

### 联系Adobe支持 {#contacting-adobe-support}

如果您已经听取了本页的建议，但仍然遇到问题，请联系Adobe支持。 要向处理您案例的支持工程师提供尽可能多的信息，请确保从升级中包含upgrade.log文件。
