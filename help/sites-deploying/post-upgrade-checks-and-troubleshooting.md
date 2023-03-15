---
title: 升级后检查和故障排除
seo-title: Post Upgrade Checks and Troubleshooting
description: 了解如何对升级后可能显示的问题进行故障排除。
seo-description: Learn how to troubleshoot issues that might appear after an upgrade.
uuid: 3f525f2c-8d25-4bb8-a57e-3adf667edde8
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: 5a67aa9f-e5eb-4d7e-89da-2ee1a45eb8ce
docset: aem65
feature: Upgrading
exl-id: ceac2b52-6885-496d-9517-5fc7291ad070
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1813'
ht-degree: 0%

---

# 升级后检查和故障排除{#post-upgrade-checks-and-troubleshooting}

## 升级后检查 {#post-upgrade-checks}

遵循 [就地升级](/help/sites-deploying/in-place-upgrade.md) 应执行以下活动以完成升级。 假定已使用6.5 jar启动了AEM，并且已部署升级的代码库。

* [验证升级成功日志](#main-pars-header-290365562)

* [验证OSGi包](#main-pars-header-1637350649)

* [验证Oak版本](#main-pars-header-1293049773)

* [Inspect PreUpgradeBackup文件夹](#main-pars-header-988995987)

* [页面初始验证](#main-pars-header-20827371)
* [应用AEM Service Pack](#main-pars-header-215142387)

* [迁移AEM功能](#main-pars-header-1434457709)

* [验证计划的维护配置](#main-pars-header-1552730183)

* [启用复制代理](#main-pars-header-823243751)

* [启用自定义计划作业](#main-pars-header-244535083)

* [执行测试计划](#main-pars-header-1167972233)

### 验证升级成功的日志 {#verify-logs-for-upgrade-success}

**upgrade.log**

过去，检查实例的升级后状态需要仔细检查各种日志文件、部分存储库和启动板。 生成升级后报告有助于在升级前检测有缺陷的升级。

此功能的主要用途是，减少鉴定升级成功所需的手动解释或跨多个端点的复杂解析逻辑的需要。 该解决方案旨在为外部自动化系统提供明确的信息，以对更新的成功或识别的失败作出反应。

更具体地说，它确保：

* 升级框架检测到的升级故障可以集中在一个升级报告中；
* 升级报告包含有关必要手动干预的指标。

为了适应这种情况，在中生成日志的方式已发生更改 `upgrade.log` 文件。

以下是升级期间未显示任何错误的示例报表：

![1487887443006](assets/1487887443006.png)

以下是一个示例报告，其中显示了在升级过程中未安装的捆绑包：

![1487887532730](assets/1487887532730.png)

**error.log**

在使用目标版本jar启动AEM期间和之后，应该仔细检查error.log。 应审查任何警告或错误。 一般来说，最好在日志的开头查找问题。 日志中稍后发生的错误实际上可能是文件早期调用的根本原因的副作用。 如果出现重复错误和警告，请参阅下面的 [分析升级问题](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md#analyzing-issues-with-the-upgrade).

### 验证OSGi包 {#verify-osgi-bundles}

导航到OSGi控制台 `/system/console/bundles` 并查看是否有任何捆绑包未启动。 如果有任何捆绑包处于安装状态，请查阅 `error.log` 以确定根问题。

### 验证Oak版本 {#verify-oak-version}

升级后，您应该会看到Oak版本已更新到 **1.10.2**. 要验证Oak版本，请导航到OSGi控制台并查看与Oak捆绑包关联的版本：Oak Core、Oak Commons、Oak Segment Tar。

### Inspect PreUpgradeBackup文件夹 {#inspect-preupgradebackup-folder}

在升级期间，AEM将尝试备份自定义项并将其存储在下方 `/var/upgrade/PreUpgradeBackup/<time-stamp-of-upgrade>`. 要在CRXDE Lite中查看此文件夹，您可能需要 [临时启用CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md).

具有时间戳的文件夹应具有名为的属性 `mergeStatus` 具有值 `COMPLETED`. 此 **待处理** 文件夹应为空，并且 **被覆盖** 节点指示在升级期间被覆盖的节点。 下的内容 **剩余** 节点表示在升级期间无法安全合并的内容。 如果您的实施依赖于任何子节点（并且尚未由升级后的代码包安装），则需要手动合并这些子节点。

如果在暂存或生产环境中，则禁用此练习后的CRXDE Lite。

### 页面初始验证 {#initial-validation-of-pages}

对AEM中的多个页面执行初始验证。 如果升级创作环境，请打开开始页面和欢迎页面( `/aem/start.html`， `/libs/cq/core/content/welcome.html`)。 在创作和发布环境中，打开几个应用程序页面并进行冒烟测试，以使其正确呈现。 如果有任何问题，请参阅 `error.log` 以进行故障排除。

### 应用AEM Service Pack {#apply-aem-service-packs}

应用任何相关的AEM 6.5 Service Pack（如果已发布）。

### 迁移AEM功能 {#migrate-aem-features}

升级后，AEM中的多项功能需要执行其他步骤。 有关这些功能的完整列表以及在AEM 6.5中迁移这些功能的步骤，请参阅 [升级代码和自定义项](/help/sites-deploying/upgrading-code-and-customizations.md) 页面。

### 验证计划的维护配置 {#verify-scheduled-maintenance-configurations}

#### 启用数据存储垃圾收集 {#enable-data-store-garbage-collection}

如果使用文件数据存储，请确保已启用数据存储垃圾收集任务并将其添加到每周维护列表。 说明已概述 [此处](/help/sites-administering/data-store-garbage-collection.md).

>[!NOTE]
>
>对于S3自定义数据存储安装或使用共享数据存储时，不建议这样做。

#### 启用联机修订版清理 {#enable-online-revision-cleanup}

如果使用MongoMK或新的TarMK区段格式，请确保已启用“修订版清理”任务并将其添加到“每日维护”列表中。 说明概述 [此处](/help/sites-deploying/revision-cleanup.md).

### 执行测试计划 {#execute-test-plan}

根据定义执行详细的测试计划 [升级代码和自定义项](/help/sites-deploying/upgrading-code-and-customizations.md) 在 **测试过程** 部分。

### 启用复制代理 {#enable-replication-agents}

发布环境完全升级并验证后，在创作环境中启用复制代理。 验证代理是否能够连接到各自的发布实例。 参见U [升级过程](/help/sites-deploying/upgrade-procedure.md) 以了解有关事件顺序的更多详细信息。

### 启用自定义计划作业 {#enable-custom-scheduled-jobs}

此时可以启用任何作为代码库一部分的计划作业。

## 分析升级问题 {#analyzing-issues-with-upgrade}

此部分包含升级到AEM 6.3的过程中可能会遇到的一些问题场景。

这些场景应该有助于找到与升级相关问题的根本原因，并且应该有助于识别项目或产品特定问题。

### 存储库迁移失败  {#repository-migration-failing-}

对于以基于CQ 5.4的源实例开始的任何场景，从CRX2到Oak的数据迁移应该是可行的。确保完全按照本文档中的升级说明进行操作，包括准备 `repository.xml`，确保在开始迁移之前，没有通过JAAS启动自定义身份验证器，并且已检查实例是否不一致。

如果迁移仍然失败，您可以通过检查 `upgrade.log`. 如果问题尚未知，请向客户支持部门报告。

### 升级未运行 {#the-upgrade-did-not-run}

在开始准备步骤之前，请确保运行 **源** 首先使用java -jar aem-quickstart.jar命令执行实例。 这是确保正确生成quickstart.properties文件所必需的。 如果缺少该参数，则升级将不起作用。 或者，您可以通过查看以下内容来检查文件是否存在 `crx-quickstart/conf` 在源实例的安装文件夹中。 此外，在启动AEM以开始升级时，必须使用java -jar aem-quickstart.jar命令执行该升级。 从启动脚本启动时，在升级模式下不会启动AEM。

### 包和捆绑包无法更新  {#packages-and-bundles-fail-to-update-}

如果在升级期间无法安装包，则不会更新包中包含的包。 此类问题通常是由数据存储错误配置引起的。 它们还将显示为 **错误** 和 **警告** error.log中的消息。 由于在大多数情况下，默认登录可能无法工作，因此您可以直接使用CRXDE来检查和查找配置问题。

### 某些AEM捆绑包未切换到活动状态 {#some-aem-bundles-are-not-switching-to-the-active-state}

如果捆绑包未启动，则应检查是否存在任何未满足的依赖关系。

如果存在此问题，但此问题基于失败的软件包安装，从而导致捆绑包无法升级，则它们将被视为与新版本不兼容。 有关如何对此进行故障排除的更多信息，请参阅 **包和捆绑包无法更新** 上面。

此外，还建议将新的AEM 6.5实例的捆绑包列表与已升级的实例进行比较，以检测未升级的捆绑包。 这将提供一个更小的范围，让您了解在 `error.log`.

### 自定义捆绑包未切换到活动状态 {#custom-bundles-not-switching-to-the-active-state}

如果您的自定义捆绑包未切换到活动状态，则很可能是因为存在未导入更改API的代码。 这通常会导致依赖关系得不到满足。

以前的一个版本应将已删除的API标记为已弃用。 您可以在此弃用通知中找到有关直接迁移代码的说明。 Adobe旨在尽可能进行语义版本控制，以便版本能够指示重大更改。

另外，最好检查导致问题的更改是否是绝对必要的，如果不是，则恢复它。 此外，在严格的语义版本控制之后，检查资源包导出的版本增加是否超过需要。

### 平台UI出现故障 {#malfunctioning-platform-ui}

如果在升级后某些UI功能无法正常工作，则应首先检查界面的自定义叠加。 某些结构可能已更改，并且叠加可能需要更新或过时。

接下来，检查是否存在任何可以向下跟踪到已链接到客户端库的自定义添加扩展的Javascript错误。 这同样适用于可能导致AEM布局问题的自定义CSS。

最后，检查Javascript可能无法处理的错误配置。 不正确取消激活的扩展通常会出现这种情况。

### 自定义组件、模板或UI扩展出现故障 {#malfunctioning-custom-components-templates-or-ui-extensions}

在大多数情况下，这些问题的根本原因与未启动的捆绑包或未安装的包相同，只是首次使用组件时问题开始发生。

处理错误自定义代码的方法是首先执行烟雾测试，以确定原因。 找到后，请查看以下推荐 [链接] 部分以了解修复方法。

### /etc下缺少自定义项 {#missing-customizations-under-etc}

`/apps` 和 `/libs` 升级处理得当，但更改位于 `/etc` 可能需要从手动恢复 `/var/upgrade/PreUpgradeBackup` 升级后。 确保检查此位置是否有任何需要手动合并的内容。

### 分析error.log和upgrade.log {#analyzing-the-error.log-and-upgrade.log}

在大多数情况下，需要查阅日志中的错误信息，以找出问题的原因。 但是，在升级时，还需要监测依赖项问题，因为旧捆绑包可能无法正确升级。

最好的方法是删除error.log ，方法是删除预期与您面临的问题无关的所有消息。 您可以使用以下工具通过grep等工具执行此操作：

```shell
grep -v UnrelatedErrorString
```

某些错误消息可能不会立即具有说明性。 在这种情况下，查看发生错误的上下文也有助于了解错误是在何处创建的。 您可以使用以下内容分隔错误：

* `grep -B` 用于在错误前添加行；

或

* `grep -A` 用于在后面添加行。

在少数情况下，还可以找到错误WARN消息，因为可能存在导致此状态的有效案例，并且应用程序并不总是能够确定这是否是实际的错误。 请务必查阅这些信息。

### 联系 Adobe 支持 {#contacting-adobe-support}

如果您已阅读本页上的建议，但仍遇到问题，请联系Adobe支持。 为了向处理您的案例的支持工程师提供尽可能多的信息，请确保升级中包含upgrade.log文件。
