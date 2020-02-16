---
title: 升级前维护任务
seo-title: 升级前维护任务
description: 了解AEM中的预升级任务。
seo-description: 了解AEM中的预升级任务。
uuid: 5da1cfc7-8a10-47b1-aafb-2cd112e3f818
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 291c91e5-65ff-473d-ac11-3da480239e76
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 升级前维护任务{#pre-upgrade-maintenance-tasks}

在开始升级之前，务必执行以下维护任务以确保系统准备就绪，并且如果出现问题，可以回退：

* [确保足够的磁盘空间](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#ensure-sufficient-disk-space)
* [完全备份AEM](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#fully-back-up-aem)
* [将更改备份到/etc](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#backup-changes-etc)
* [生成quickstart.properties文件](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#generate-quickstart-properties)
* [配置工作流和审核日志清除](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#configure-wf-audit-purging)
* [安装、配置和运行升级前任务](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#install-configure-run-pre-upgrade-tasks)
* [禁用自定义登录模块](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-login-modules)
* [从/install目录中删除更新](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#remove-updates-install-directory)
* [停止任何冷备用实例](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#stop-tarmk-coldstandby-instance)
* [禁用自定义计划作业](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-scheduled-jobs)
* [执行脱机修订清除](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-offline-revision-cleanup)
* [执行数据存储垃圾收集](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-datastore-garbage-collection)
* [根据需要升级数据库架构](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#upgradethedatabaseschemaifneeded)
* [删除可能妨碍升级的用户](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#delete-users-that-might-hinder-the-upgrade)

* [旋转日志文件](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#rotate-log-files)

## 确保足够的磁盘空间 {#ensure-sufficient-disk-space}

执行升级时，除了内容和代码升级活动之外，还需要执行存储库迁移。 迁移将以新的Segment Tar格式创建存储库的副本。 因此，您需要足够的磁盘空间来保留第二个可能更大的存储库版本。

## 完全备份AEM {#fully-back-up-aem}

在开始升级之前，应完全备份AEM。 确保备份存储库、应用程序安装、数据存储和Mongo实例（如果适用）。 有关备份和恢复AEM实例的详细信息，请参阅备 [份和恢复](/help/sites-administering/backup-and-restore.md)。

## 将更改备份到/etc {#backup-changes-etc}

升级过程很好地维护和合并了存储库中的和路径下的现有 `/apps` 内容 `/libs` 和配置。 对于路径(包括Context `/etc` Hub配置)所做的更改，通常需要在升级后重新应用这些更改。 虽然升级将备份它无法合并到的任何更改，但我们建议在开始升级之前手动备份这些更改 `/var`。

## 生成quickstart.properties文件 {#generate-quickstart-properties}

从jar文件启动AEM时，将在 `quickstart.properties` 下生成一个文件 `crx-quickstart/conf`。 如果AEM过去只使用启动脚本启动，则此文件将不存在，并且升级将失败。 确保检查此文件是否存在，并从jar文件中重新启动AEM（如果该文件不存在）。

## 配置工作流和审核日志清除 {#configure-wf-audit-purging}

这些 `WorkflowPurgeTask` 和任 `com.day.cq.audit.impl.AuditLogMaintenanceTask` 务需要单独的OSGi配置，如果没有这些配置，它们将无法工作。 如果在预升级任务执行期间失败，则最可能的原因是缺少配置。 因此，如果您不希望运行这些任务，请确保为这些任务添加OSGi配置，或将它们从升级前优化任务列表中完全删除。 有关配置工作流清除任务的文档，请参阅管理工作流 [实例](/help/sites-administering/workflows-administering.md) ，审计日志维护任务配置可在AEM 6的 [审计日志维护中找到](/help/sites-administering/operations-audit-log.md)。

有关在CQ 5.6上清除工作流和审核日志以及在AEM 6.0上清除审核日志，请参阅清 [除工作流和审核节点](https://helpx.adobe.com/experience-manager/kb/howtopurgewf.html)。

## 安装、配置和运行升级前任务 {#install-configure-run-pre-upgrade-tasks}

由于AEM允许的自定义级别，环境通常不遵循执行升级的统一方式。 这使得创建标准化的升级过程成为一个困难的过程。

在以前版本中，停止或无法安全恢复的AEM升级也很困难。 这导致需要重新启动完整升级程序或执行有缺陷的升级而不触发任何警告的情况。

为了解决这些问题，Adobe为升级过程添加了多项增强功能，使其更具弹性和用户友好性。 之前必须手动执行的升级前维护任务正在优化和自动化。 此外，已添加升级后报告，以便能够充分审查该过程，希望更轻松地找到任何问题。

预升级维护任务当前分布在手动部分或完全执行的各种界面上。 AEM 6.3中引入的升级前维护优化使您能够以统一的方式触发这些任务并能够按需检查其结果。

升级前优化步骤中包含的所有任务都与AEM 6.0以后的所有版本兼容。

### 如何设置 {#how-to-set-it-up}

在AEM 6.3和更高版本中，升级前维护优化任务包含在快速启动jar中。 如果您从旧版AEM 6升级，则可以通过单独的包使用它们，您可以从包管理器下载这些包。

您可以在以下位置找到包：

* [从AEM 6.0升级](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq600/product/pre-upgrade-tasks-content-cq60)

* [从AEM 6.1升级](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq610/product/pre-upgrade-tasks-content-cq61)

* [从AEM 6.2升级](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq620/product/pre-upgrade-tasks-content-cq62)

### How to Use It {#how-to-use-it}

OSGI组 `PreUpgradeTasksMBean` 件预配置了升级前维护任务列表，可同时运行这些任务。 您可以按照以下过程配置任务：

1. 通过浏览至https://serveraddress:serverport/system/console/configMgr，转到Web控 *制台*

1. 搜索“预&#x200B;**升级任务**”，然后单击第一个匹配的组件。 组件的全名是 `com.adobe.aem.upgrade.prechecks.mbean.impl.PreUpgradeTasksMBeanImpl`

1. 修改需要运行的维护任务列表，如下所示：

   ![1487758925984](assets/1487758925984.png)

任务列表因用于启动实例的运行模式而异。 以下是每个维护任务所针对的运行模式说明。

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
   <td>会做标记和扫描。 对于共享数据存储，请删除此步骤<br /> ，然后在执行之前手动或正确地运行实例。</td>
  </tr>
  <tr>
   <td><code>ConsistencyCheckTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>WorkflowPurgeTask</code></td>
   <td>crx2/crx3</td>
   <td>运行前必须配置Adobe Granite Workflow Purge Configuration OSGi。</td>
  </tr>
  <tr>
   <td><code>GenerateBundlesListFileTask</code></td>
   <td>crx2/crx3</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>RevisionCleanupTask</code></td>
   <td>crx3</td>
   <td>对于AEM 6.0到6.2上的TarMK实例，请手动运行“脱机修订清除”。</td>
  </tr>
  <tr>
   <td><code>com.day.cq.audit.impl.AuditLogMaintenanceTask</code></td>
   <td>crx3</td>
   <td>运行前必须配置审核日志清除调度程序OSGi配置。</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>`DataStoreGarbageCollectionTask` 使用标记和扫描阶段调用数据存储垃圾收集操作（如果使用）。 对于使用共享数据存储的部署，请确保重新配置或正确准备该实例，以避免删除其他实例引用的项目。 这可能需要在触发此预升级任务之前，在所有实例上手动运行标记阶段。

### 升级前运行状况检查的默认配置 {#default-configuration-of-the-pre-upgrade-health-checks}

OSGI `PreUpgradeTasksMBeanImpl` 组件预配置了升级前运行状况检查标记列表，该列表将在调用该方法时 `runAllPreUpgradeHealthChecks` 执行：

* **system** —— 花岗岩维护运行状况检查使用的标签

* **升级前** -这是一个自定义标记，可添加到升级前可设置运行的所有运行状况检查中

列表可编辑。 除了标记之外，您还 **可以使用加号** (+)和减号(-) **** 按钮来添加更多自定义标记，或删除默认标记。

**MBean方法**

可以使用 [JMX控制台访问受管Bean功能](/help/sites-administering/jmx-console.md)。

您可以通过以下方式访问MBean:

1. 转到JMX控制台，网址为 *https://serveraddress:serverport/system/console/jmx*
1. 搜索预 **升级任务** ，然后单击结果

1. 从“操作”部分选择任 **意方法** ，然后在以 **下窗口中选择** “调用”。

以下是公开的所有可用方法的列 `PreUpgradeTasksMBeanImpl` 表：

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
   <td>显示可用的升级前维护任务名称列表。</td>
  </tr>
  <tr>
   <td><code>getAvailablePreUpgradeHealthChecksTagNames()</code></td>
   <td>信息</td>
   <td>显示升级前运行状况检查标记名称列表。</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeTasks()</code></td>
   <td>动作</td>
   <td>运行列表中的所有升级前维护任务。</td>
  </tr>
  <tr>
   <td><code>runPreUpgradeTask(preUpgradeTaskName)</code></td>
   <td>动作</td>
   <td>运行升级前维护任务，并以给定的名称作为参数。</td>
  </tr>
  <tr>
   <td><code>isRunAllPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>检查任务 <code>runAllPreUpgradeTasksmaintenance</code> 当前是否正在运行。</td>
  </tr>
  <tr>
   <td><code>getAnyPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>检查是否有任何预升级维护任务当前正在运行<br /> ，并返回包含当前正在运行任务名称的数组。</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunTime(preUpgradeTaskName)</code></td>
   <td>动作</td>
   <td>显示升级前维护任务的确切运行时间，并以给定的名称作为参数。</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunState(preUpgradeTaskName)</code></td>
   <td>动作</td>
   <td>显示升级前维护任务的上次运行状态，并以给定的名称作为参数。</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeHealthChecks(shutDownOnSuccess)</code></td>
   <td>动作</td>
   <td><p>运行所有升级前运行状况检查，并将其状态保存在sling <code>preUpgradeHCStatus.properties</code> home路径中名为的文件中。 如果将 <code>shutDownOnSuccess</code> 该参数设置为 <code>true</code>，则AEM实例将关闭，但前提是所有升级前运行状况检查都处于“正常”状态。</p> <p>属性文件将用作将来任何升级的先决条件<br /> ，如果升级前运行状况检查执行失败，升级过程将停止<br /> 。 如果要忽略升级前运行状况检查的结果<br /> ，并仍然启动升级，则可以删除该文件。</p> </td>
  </tr>
  <tr>
   <td><code>detectUsageOfUnavailableAPI(aemVersion)</code></td>
   <td>动作</td>
   <td>列出升级到指定AEM版本后将不再满足的<br /> 所有导入的包。 目标AEM版本必须作为参数<br /> 提供。</td>
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
>只有从AEM 5版本升级时，才需要此步骤。 可以完全跳过该步骤以从旧版AEM 6升级。

在Apache Oak中， `LoginModules` 在存储库级别配置自定义身份验证的方式已发生根本变化。

在使用CRX2配置的AEM版本中，将CRX2配置放在文件中，而从 `repository.xml` AEM 6开始，将通过Web控制台在Apache Felix JAAS配置工厂服务中完成该操作。

因此，升级后，必须禁用并重新为Apache Oak创建任何现有配置。

要禁用在的JAAS配置中定义的自定义模块 `repository.xml`，您需要修改配置以使用默认模块 `LoginModule`，如本例所示：

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
>有关详细信息，请参 [阅使用外部登录模块进行身份验证](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html)。
>
>有关AEM 6中的配 `LoginModule` 置示例，请参阅 [使用AEM 6配置LDAP](/help/sites-administering/ldap-config.md)。

## 从/install目录中删除更新 {#remove-updates-install-directory}

>[!NOTE]
>
>在关闭AEM实例后，仅从crx-quickstart/install目录中删除包。 这是开始就地升级过程之前的最后一步。

删除通过本地文件系统上的目录部署的所有服务包、功 `crx-quickstart/install` 能包或修补程序。 这将防止在更新完成后在新AEM版本上意外安装旧的修补程序和服务包。

## 停止任何冷备用实例 {#stop-tarmk-coldstandby-instance}

如果使用TarMK冷备用，请停止任何冷备用实例。 这将保证在出现升级问题时能够有效地恢复联机状态。 成功完成升级后，需要从升级的主实例重建冷备用实例。

## 禁用自定义计划作业 {#disable-custom-scheduled-jobs}

禁用应用程序代码中包含的任何OSGi计划作业。

## 执行脱机修订清除 {#execute-offline-revision-cleanup}

>[!NOTE]
>
>此步骤仅对TarMK安装是必需的

如果使用TarMK，则应在升级前执行“脱机修订清理”。 这将使存储库迁移步骤和后续升级任务的执行速度更快，并有助于确保在升级完成后可以成功执行联机修订清除。 有关运行“脱机修订清除”的信息，请参阅执 [行脱机修订清除](/help/sites-deploying/storage-elements-in-aem-6.md#performing-offline-revision-cleanup)。

## 执行数据存储垃圾收集 {#execute-datastore-garbage-collection}

>[!NOTE]
>
>此步骤仅对运行crx3的实例是必需的

在对CRX3实例运行修订清除后，您应运行Datastore Garbage Collection以删除数据存储中任何未引用的blob。 有关说明，请参阅有关 [Data Store垃圾收集的文档](/help/sites-administering/data-store-garbage-collection.md)。

## 根据需要升级数据库架构 {#upgrade-the-database-schema-if-needed}

通常，AEM用于持久化的底层Apache Oak堆栈将根据需要负责升级数据库架构。

但是，当无法自动升级架构时，可能会出现这些情况。 这些环境大多是高安全性环境，其中数据库在权限非常有限的用户下运行。 如果发生这种情况，AEM将继续使用旧架构。

要防止这种情况发生，您需要按照以下步骤升级架构：

1. 关闭需要升级的AEM实例。
1. 升级数据库架构。 请查阅有关数据库类型的文档，以了解实现此目的需要使用哪些工具。

   有关Oak如何处理架构升级的详细信息，请 [参阅Apache网站的此页](https://jackrabbit.apache.org/oak/docs/nodestore/document/rdb-document-store.html#upgrade)。

1. 继续升级AEM。

## 删除可能妨碍升级的用户 {#delete-users-that-might-hinder-the-upgrade}

>[!NOTE]
>
>此升级前维护任务仅在以下情况下才是必需的：
>
>* 您是从AEM 6.3以前的AEM版本升级
>* 在升级过程中，您会遇到以下任何错误。
>



有时，服务用户可能会在较旧的AEM版本中被错误地标记为常规用户，这种情况是例外的。

如果发生这种情况，升级将失败，并显示如下消息：

```
ERROR [Apache Sling Repository Startup Thread] com.adobe.granite.repository.impl.SlingRepositoryManager Exception in a SlingRepositoryInitializer, SlingRepository service registration aborted
java.lang.RuntimeException: Unable to create service user [communities-utility-reader]:java.lang.RuntimeException: Existing user communities-utility-reader is not a service user.
```

要解决此问题，请确保执行以下操作：

1. 将实例与生产流量分离
1. 创建导致问题的用户的备份。 您可以通过包管理器执行此操作。 有关详细信息，请参 [阅如何使用包。](/help/sites-administering/package-manager.md)
1. 删除导致问题的用户。 以下是可能属于此类别的用户列表：

   1. `dynamic-media-replication`
   1. `communities-ugc-writer`
   1. `communities-utility-reader`
   1. `communities-user-admin`
   1. `oauthservice`
   1. `sling-scripting`

## 旋转日志文件 {#rotate-log-files}

我们建议在开始升级之前存档您的当前日志文件。 这样，在升级过程中和升级后可以更轻松地监视和扫描日志文件，以识别和解决可能发生的任何问题。
