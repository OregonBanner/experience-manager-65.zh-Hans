---
title: 升级前维护任务
description: 了解为AEM推荐的升级前任务。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
docset: aem65
feature: Upgrading
exl-id: 37d4aee4-15eb-41ab-ad71-dfbd5c7910f8
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2014'
ht-degree: 0%

---

# 升级前维护任务{#pre-upgrade-maintenance-tasks}

在开始升级之前，请务必遵循这些维护任务，以确保系统已准备就绪，并且可以在出现问题时回滚：

* [确保有足够的磁盘空间](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#ensure-sufficient-disk-space)
* [完全备份AEM](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#fully-back-up-aem)
* [将更改备份到/etc](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#backup-changes-etc)
* [生成快速入门.properties文件](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#generate-quickstart-properties)
* [配置工作流和审核日志清除](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#configure-wf-audit-purging)
* [安装、配置和运行升级前任务](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#install-configure-run-pre-upgrade-tasks)
* [禁用自定义登录模块](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-login-modules)
* [从/install目录中删除更新](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#remove-updates-install-directory)
* [停止任何冷备用实例](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#stop-tarmk-coldstandby-instance)
* [禁用自定义计划作业](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-scheduled-jobs)
* [执行脱机修订版清理](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-offline-revision-cleanup)
* [执行数据存储垃圾收集](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-datastore-garbage-collection)
* [根据需要升级数据库模式](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#upgradethedatabaseschemaifneeded)
* [删除可能妨碍升级的用户](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#delete-users-that-might-hinder-the-upgrade)

* [旋转日志文件](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#rotate-log-files)

## 确保有足够的磁盘空间 {#ensure-sufficient-disk-space}

在执行升级时，除了内容和代码升级活动之外，还必须执行存储库迁移。 迁移过程会以新的Segment Tar格式创建存储库的副本。 因此，您需要足够的磁盘空间来保留存储库的第二个（可能更大）版本。

## 完全备份AEM {#fully-back-up-aem}

在开始升级之前，应完全备份AEM。 确保备份存储库、应用程序安装、数据存储和Mongo实例（如果适用）。 有关备份和恢复AEM实例的详细信息，请参阅 [备份和恢复](/help/sites-administering/backup-and-restore.md).

## 将更改备份到/etc {#backup-changes-etc}

升级过程很好地维护和合并了下的现有内容和配置 `/apps` 和 `/libs` 存储库中的路径。 对于所做的更改 `/etc` 路径（包括Context Hub配置），通常需要在升级后重新应用这些更改。 在升级过程中，会为无法合并的任何更改创建备份副本 `/var`，Adobe建议您在开始升级之前手动备份这些更改。

## 生成快速入门.properties文件 {#generate-quickstart-properties}

从jar文件启动AEM时， `quickstart.properties` 文件生成于 `crx-quickstart/conf`. 如果AEM以前仅使用启动脚本启动，则此文件不存在，升级失败。 确保检查此文件是否存在，如果AEM不存在，请从jar文件重新启动该文件。

## 配置工作流和审核日志清除 {#configure-wf-audit-purging}

此 `WorkflowPurgeTask` 和 `com.day.cq.audit.impl.AuditLogMaintenanceTask` 任务需要单独的OSGi配置，没有它们将无法工作。 如果它们在升级前任务执行期间失败，则缺少配置是最可能的原因。 因此，请确保为这些任务添加OSGi配置，或者如果不想运行它们，则从升级前优化任务列表中完全删除它们。 有关配置工作流清除任务的文档，请访问 [管理工作流实例](/help/sites-administering/workflows-administering.md) 和审核日志维护任务配置位于 [AEM 6中的审核日志维护](/help/sites-administering/operations-audit-log.md).

有关CQ 5.6上的工作流和审核日志清除以及AEM 6.0上的审核日志清除，请参阅 [清除工作流和审核节点](https://helpx.adobe.com/experience-manager/kb/howtopurgewf.html).

## 安装、配置和运行升级前任务 {#install-configure-run-pre-upgrade-tasks}

由于AEM所允许的自定义级别，环境通常不遵循统一的升级执行方式。 因此，创建标准化的升级程序是一个困难的过程。

在以前的版本中，对于已停止或无法安全恢复的AEM升级，也会遇到困难。 此问题导致出现以下情况：需要重新启动完整升级过程，或者执行了有缺陷的升级而未触发任何警告。

为了解决这些问题，Adobe在升级过程中添加了几项增强功能，使其更具可复原性并且更便于用户使用。 以前必须手动执行的升级前维护任务正在优化和自动化。 此外，还添加了升级后报告，以便可以完全审查该过程，希望更容易发现任何问题。

升级前维护任务当前分布于各种手动部分或完全执行的接口上。 AEM 6.3中引入的升级前维护优化功能能够以统一的方式触发这些任务，并能够根据需要检查其结果。

从AEM 6.0开始，升级前优化步骤中包含的所有任务都与所有版本兼容。

### 如何设置 {#how-to-set-it-up}

在AEM 6.3及更高版本中，快速入门jar中包含升级前维护优化任务。

<!-- URLs below are all 404s. This content should probably be removed because it is entirely obsolete.

If you are upgrading from an older version of AEM 6, they are made available through separate packages that you can download from the Package Manager.

You can find the packages at these locations:

* [For upgrading from AEM 6.0](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq600/product/pre-upgrade-tasks-content-cq60)

* [For upgrading from AEM 6.1](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq610/product/pre-upgrade-tasks-content-cq61)

* [For upgrading from AEM 6.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq620/product/pre-upgrade-tasks-content-cq62) -->

### 使用方法 {#how-to-use-it}

此 `PreUpgradeTasksMBean` OSGI组件预配置了可以一次运行的所有升级前维护任务的列表。 您可以按照以下步骤配置任务：

1. 通过浏览至Web控制台 *https://serveraddress:serverport/system/console/configMgr*

1. 搜索&quot;**预升级任务**“”，然后单击第一个匹配的组件。 组件的全名为 `com.adobe.aem.upgrade.prechecks.mbean.impl.PreUpgradeTasksMBeanImpl`

1. 修改必须运行的维护任务列表，如下所示：

   ![1487758925984](assets/1487758925984.png)

根据用于启动实例的运行模式，任务列表会有所不同。 以下是对每个维护任务所针对的运行模式的描述。

<table>
 <tbody>
  <tr>
   <td><strong>任务</strong></td>
   <td><strong>运行模式</strong></td>
   <td><strong>注释</strong></td>
  </tr>
  <tr>
   <td><code>TarIndexMergeTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>DataStoreGarbageCollectionTask</code></td>
   <td>crx2</td>
   <td>运行标记和整理。 对于共享数据存储，请删除此步骤并运行<br /> 在执行之前手动或正确准备实例。</td>
  </tr>
  <tr>
   <td><code>ConsistencyCheckTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>WorkflowPurgeTask</code></td>
   <td>crx2/crx3</td>
   <td>必须在运行之前配置AdobeGranite工作流清除配置OSGi。</td>
  </tr>
  <tr>
   <td><code>GenerateBundlesListFileTask</code></td>
   <td>crx2/crx3</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>RevisionCleanupTask</code></td>
   <td>crx3</td>
   <td>对于AEM 6.0到6.2上的TarMK实例，请改为手动运行离线修订清理。</td>
  </tr>
  <tr>
   <td><code>com.day.cq.audit.impl.AuditLogMaintenanceTask</code></td>
   <td>crx3</td>
   <td>在运行之前必须配置审计日志清除计划程序OSGi配置。</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>此 `DataStoreGarbageCollectionTask` 调用具有标记和扫描阶段（如果已使用）的数据存储垃圾收集操作。 对于使用共享数据存储的部署，请确保正确重新配置它或准备实例以避免删除另一个实例引用的项目。 在触发此升级前任务之前，此过程可能需要在所有实例上手动运行标记阶段。

### 升级前运行状况检查的默认配置 {#default-configuration-of-the-pre-upgrade-health-checks}

此 `PreUpgradeTasksMBeanImpl` OSGI组件预配置了一个预升级运行状况检查标记列表，以便 `runAllPreUpgradeHealthChecks` 方法名为：

* **系统** - granite维护运行状况检查使用的标记

* **预升级**  — 一个自定义标记，可添加到所有可设置为在升级前运行的运行状况检查中

该列表可编辑。 您可以使用加号 **(+)** 和减号 **(-)** 按钮以添加更多自定义标记，或删除默认标记。

**MBean方法**

可以使用访问受管Bean功能 [JMX控制台](/help/sites-administering/jmx-console.md).

您可以通过以下方式访问MBean：

1. 转到位于的JMX控制台 *https://serveraddress:serverport/system/console/jmx*
1. 搜索 **PreUpgradeTasks** 并单击结果

1. 从中选择任意方法 **操作** 部分并选择 **调用** 在下面的窗口中。

以下是 `PreUpgradeTasksMBeanImpl` 公开：

<table>
 <tbody>
  <tr>
   <td><strong>方法名称</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td><code>getAvailablePreUpgradeTasksNames()</code></td>
   <td>信息</td>
   <td>显示可用升级前维护任务名称的列表。</td>
  </tr>
  <tr>
   <td><code>getAvailablePreUpgradeHealthChecksTagNames()</code></td>
   <td>信息</td>
   <td>显示升级前运行状况检查标记名称的列表。</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeTasks()</code></td>
   <td>动作</td>
   <td>运行列表中的所有升级前维护任务。</td>
  </tr>
  <tr>
   <td><code>runPreUpgradeTask(preUpgradeTaskName)</code></td>
   <td>动作</td>
   <td>运行升级前维护任务，其名称作为参数给定。</td>
  </tr>
  <tr>
   <td><code>isRunAllPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>检查 <code>runAllPreUpgradeTasksmaintenance</code> 任务正在运行。</td>
  </tr>
  <tr>
   <td><code>getAnyPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>检查是否有任何升级前维护任务正在运行，并且<br /> 返回一个数组，其中包含当前正在运行的任务的名称。</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunTime(preUpgradeTaskName)</code></td>
   <td>动作</td>
   <td>显示升级前维护任务的确切运行时间，其名称作为参数提供。</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunState(preUpgradeTaskName)</code></td>
   <td>动作</td>
   <td>显示升级前维护任务的上次运行状态，其名称作为参数提供。</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeHealthChecks(shutDownOnSuccess)</code></td>
   <td>动作</td>
   <td><p>运行所有升级前运行状况检查，并将其状态保存在名为的文件中 <code>preUpgradeHCStatus.properties</code> 在sling home的路径上。 如果 <code>shutDownOnSuccess</code> 参数设置为 <code>true</code>，AEM实例将关闭，但前提是所有升级前运行状况检查的状态均为“正常”。</p> <p>属性文件用作任何未来升级的前提条件<br /> 并且如果升级前运行状况检查，升级过程将停止<br /> 执行失败。 如果您要忽略预升级的结果<br /> 运行状况检查并启动升级，但您可以删除文件。</p> </td>
  </tr>
  <tr>
   <td><code>detectUsageOfUnavailableAPI(aemVersion)</code></td>
   <td>动作</td>
   <td>列出所有导入的包，这些包在<br /> 升级到指定的AEM版本。 目标AEM版本必须为<br /> 以参数形式给出。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>可以通过以下方式调用MBean方法：
>
>* JMX控制台
>* 连接到JMX的任何外部应用程序
>* cURL
>

## 禁用自定义登录模块 {#disable-custom-login-modules}

>[!NOTE]
>
>仅当从AEM 5版本升级时，才需要执行此步骤。 从旧版AEM 6升级时，可以完全跳过该步骤。

自定义方式 `LoginModules` 配置为在存储库级别进行身份验证，这在Apache Oak中发生了根本性更改。

在使用CRX2配置的AEM版本中，将置于 `repository.xml` 文件，而从AEM 6开始，则是通过Web控制台在Apache Felix JAAS Configuration Factory服务中完成。

因此，在升级后，必须禁用任何现有配置并重新创建Apache Oak。

禁用的JAAS配置中定义的自定义模块 `repository.xml`，则必须编辑配置以使用默认设置 `LoginModule`，如以下示例所示：

```xml
<Security >
             ....
          <!--
                 Use LoginModule authenticating against repository itself
                 -->
                 <LoginModule class = "com.day.crx.core.CRXLoginModule" >
                     <param name = "anonymousId" value = "anonymous" />
                     <param name = "adminId" value ="admin" />
                     <param name = "disableNTLMAuth" value = "true" />
                     <param name = "tokenExpiration" value = "43200000" />
                     <!-- param name="trust_credentials_attribute" value="d5b9167e95dad6e7d3b5d6fa8df48af8"/
                -->
                 </LoginModule >
         </ Security>
```

>[!NOTE]
>
>有关更多信息，请参阅 [使用外部登录模块进行身份验证](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html).
>
>例如 `LoginModule` AEM 6中的配置，请参见 [使用AEM 6配置LDAP](/help/sites-administering/ldap-config.md).

## 从/install目录中删除更新 {#remove-updates-install-directory}

>[!NOTE]
>
>在关闭AEM实例后，仅从crx-quickstart/install目录中删除包。 此步骤是开始就地升级过程之前的最后一个步骤。

删除通过部署的所有Service Pack、功能包或修补程序 `crx-quickstart/install` 目录。 这样做可防止在更新完成后，在新AEM版本之上意外安装旧修补程序和Service Pack。

## 停止任何冷备用实例 {#stop-tarmk-coldstandby-instance}

如果使用TarMK冷备用，请停止任何冷备用实例。 这样做可以确保在升级过程中出现问题，高效地重新上线。 成功完成升级后，必须从升级的主实例重建冷备用实例。

## 禁用自定义计划作业 {#disable-custom-scheduled-jobs}

禁用应用程序代码中包含的任何OSGi计划作业。

## 执行脱机修订版清理 {#execute-offline-revision-cleanup}

>[!NOTE]
>
>此步骤仅对于TarMK安装是必需的

如果使用TarMK，则在升级之前应运行脱机修订版清理。 这样做可以使存储库迁移步骤和后续升级任务的执行速度更快，并且有助于确保在升级完成后可以成功执行在线修订版清理。 有关运行脱机修订版清理的信息，请参阅 [正在执行脱机修订清理](/help/sites-deploying/storage-elements-in-aem-6.md#performing-offline-revision-cleanup).

## 执行数据存储垃圾收集 {#execute-datastore-garbage-collection}

>[!NOTE]
>
>只有运行crx3的实例才需要此步骤

在CRX3实例上运行修订清理后，您应该运行数据存储垃圾收藏集以删除数据存储中的任何未引用Blob。 有关说明，请参阅以下文档 [数据存储垃圾收集](/help/sites-administering/data-store-garbage-collection.md).

## 根据需要升级数据库模式 {#upgrade-the-database-schema-if-needed}

通常，如果需要，AEM用于持久性的基础Apache Oak栈栈会负责升级数据库架构。

但是，在架构无法自动升级时可能会出现这种情况。 此类情况大多是高安全性环境，在这种环境中，数据库以权限有限的用户身份运行。 如果发生这种情况，AEM将继续使用旧架构。

要防止发生这种情况，请执行以下操作升级架构：

1. 关闭必须升级的AEM实例。
1. 升级数据库模式。 请查阅数据库类型的文档，了解需要什么工具才能获得结果。

   有关Oak如何处理模式升级的更多信息，请参阅 [Apache网站上的此页面](https://jackrabbit.apache.org/oak/docs/nodestore/document/rdb-document-store.html#upgrade).

1. 继续升级AEM。

## 删除可能妨碍升级的用户 {#delete-users-that-might-hinder-the-upgrade}

>[!NOTE]
>
>仅在以下情况下，才需要执行升级前维护任务：
>
>* 您正在从AEM 6.3之前的AEM版本升级
>* 在升级过程中，您会遇到以下提到的任何错误。
>

在极少数情况下，服务用户的最终版本可能会是较早的AEM版本，无法正确标记为常规用户。

如果发生这种情况，升级将失败，并出现如下消息：

```
ERROR [Apache Sling Repository Startup Thread] com.adobe.granite.repository.impl.SlingRepositoryManager Exception in a SlingRepositoryInitializer, SlingRepository service registration aborted
java.lang.RuntimeException: Unable to create service user [communities-utility-reader]:java.lang.RuntimeException: Existing user communities-utility-reader is not a service user.
```

要解决此问题，请确保执行以下操作：

1. 将实例与生产流量分离
1. 创建一个或多个导致问题的用户的备份。 您可以通过包管理器完成此任务。 有关更多信息，请参阅 [如何使用包。](/help/sites-administering/package-manager.md)
1. 删除一个或多个导致问题的用户。 以下是可能属于此类别的用户列表：

   1. `dynamic-media-replication`
   1. `communities-ugc-writer`
   1. `communities-utility-reader`
   1. `communities-user-admin`
   1. `oauthservice`
   1. `sling-scripting`

## 旋转日志文件 {#rotate-log-files}

Adobe建议在开始升级之前存档当前的日志文件。 这样，在升级期间和升级后，可以更轻松地监视和扫描日志文件，以识别并解决可能出现的任何问题。
