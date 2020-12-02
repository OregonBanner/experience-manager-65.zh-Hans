---
title: 升级前维护任务
seo-title: 升级前维护任务
description: 了解AEM的预升级任务。
seo-description: 了解AEM的预升级任务。
uuid: 5da1cfc7-8a10-47b1-aafb-2cd112e3f818
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 291c91e5-65ff-473d-ac11-3da480239e76
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '2158'
ht-degree: 0%

---


# 升级前维护任务{#pre-upgrade-maintenance-tasks}

在开始升级之前，请遵循这些维护任务，以确保系统准备就绪，并在出现问题时可以回滚：

* [确保足够的磁盘空间](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#ensure-sufficient-disk-space)
* [完全备份AEM](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#fully-back-up-aem)
* [备份对/etc的更改](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#backup-changes-etc)
* [生成quickstart.properties文件](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#generate-quickstart-properties)
* [配置工作流和审核日志清除](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#configure-wf-audit-purging)
* [安装、配置和运行预升级任务](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#install-configure-run-pre-upgrade-tasks)
* [禁用自定义登录模块](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-login-modules)
* [从/install目录中删除更新](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#remove-updates-install-directory)
* [停止任何冷待机实例](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#stop-tarmk-coldstandby-instance)
* [禁用自定义计划作业](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-scheduled-jobs)
* [执行脱机修订清除](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-offline-revision-cleanup)
* [执行数据存储垃圾收集](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-datastore-garbage-collection)
* [根据需要升级数据库模式](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#upgradethedatabaseschemaifneeded)
* [删除可能妨碍升级的用户](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#delete-users-that-might-hinder-the-upgrade)

* [旋转日志文件](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#rotate-log-files)

## 确保足够的磁盘空间{#ensure-sufficient-disk-space}

执行升级时，除了内容和代码升级活动之外，还需要执行存储库迁移。 迁移将以新的“区段Tar”格式创建存储库的副本。 因此，您需要足够的磁盘空间来保留第二个可能更大的存储库版本。

## 完全备份AEM {#fully-back-up-aem}

在开始升级之前，AEM应完全备份。 确保备份您的存储库、应用程序安装、数据存储和Mongo实例（如果适用）。 有关备份和恢复AEM实例的详细信息，请参见[备份和恢复](/help/sites-administering/backup-and-restore.md)。

## 备份对/etc {#backup-changes-etc}的更改

升级过程能够很好地维护和合并存储库中`/apps`和`/libs`路径下的现有内容和配置。 对于对`/etc`路径（包括Context Hub配置）所做的更改，通常需要在升级后重新应用这些更改。 虽然升级将备份其无法合并到`/var`下的任何更改，但我们建议在开始升级之前手动备份这些更改。

## 生成快速启动。properties文件{#generate-quickstart-properties}

从jar文件启动AEM时，将在`crx-quickstart/conf`下生成`quickstart.properties`文件。 如果AEM过去只是使用开始脚本启动，则此文件将不存在，并且升级将失败。 确保检查此文件是否存在，并从jar文件重新启动AEM（如果不存在）。

## 配置工作流和审核日志清除{#configure-wf-audit-purging}

`WorkflowPurgeTask`和`com.day.cq.audit.impl.AuditLogMaintenanceTask`任务需要单独的OSGi配置，如果没有这些配置，它们将无法工作。 如果在预升级任务执行期间失败，则最可能的原因是缺少配置。 因此，如果您不想运行这些任务，请确保为这些任务添加OSGi配置，或将它们从升级前优化列表中完全删除。 有关配置工作流清除任务的文档，请访问[管理工作流实例](/help/sites-administering/workflows-administering.md)，审计日志维护任务配置可在AEM 6](/help/sites-administering/operations-audit-log.md)的[审计日志维护中找到。

有关在CQ 5.6上清除工作流和审核日志以及在AEM 6.0上清除审核日志，请参阅[清除工作流和审核节点](https://helpx.adobe.com/experience-manager/kb/howtopurgewf.html)。

## 安装、配置和运行预升级任务{#install-configure-run-pre-upgrade-tasks}

由于AEM允许的定制级别，环境通常不遵循统一的升级方式。 这使得创建标准化的升级过程成为一个困难的过程。

在以前版本中，AEM升级也很难停止或无法安全恢复。 这导致需要重新启动完整升级程序或执行有缺陷的升级而不触发任何警告的情况。

为了解决这些问题，Adobe在升级过程中增加了多项增强功能，使其更具弹性和用户友好性。 之前必须手动执行的升级前维护任务正在优化和自动化。 此外，还添加了升级后报告，以便能够充分审查该过程，希望更轻松地找到任何问题。

预升级维护任务当前分布于手动部分或完全执行的各种界面上。 AEM 6.3中引入的升级前维护优化使得能够以统一的方式触发这些任务并能够按需检查其结果。

升级前优化步骤中包含的所有任务都与AEM 6.0之后的所有版本兼容。

### 如何设置{#how-to-set-it-up}

在AEM 6.3和更高版本中，快速启动程序中包含升级前维护优化任务。 如果您从AEM 6的旧版本升级，则可以通过从包管理器下载的单独包提供它们。

您可以在以下位置找到包：

* [从AEM 6.0升级](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq600/product/pre-upgrade-tasks-content-cq60)

* [从AEM 6.1升级](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq610/product/pre-upgrade-tasks-content-cq61)

* [从AEM 6.2升级](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq620/product/pre-upgrade-tasks-content-cq62)

### 如何使用它{#how-to-use-it}

`PreUpgradeTasksMBean` OSGI组件预配置了一列表升级前维护任务，可以一次全部运行。 您可以按照以下过程配置任务:

1. 浏览至&#x200B;*https://serveraddress:serverport/system/console/configMgr*，转到Web控制台

1. 搜索“**预升级任务**”，然后单击第一个匹配的组件。 组件的完整名称为`com.adobe.aem.upgrade.prechecks.mbean.impl.PreUpgradeTasksMBeanImpl`

1. 修改需要运行的维护任务的列表，如下所示：

   ![1487758925984](assets/1487758925984.png)

任务列表会因用于开始实例的运行模式而异。 以下是每个维护任务所针对的运行模式的说明。

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
   <td>会进行标记和扫描。 对于共享数据存储，请删除此步骤，并在执行前手动或正确地运行<br />准备实例。</td>
  </tr>
  <tr>
   <td><code>ConsistencyCheckTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>WorkflowPurgeTask</code></td>
   <td>crx2/crx3</td>
   <td>运行之前，必须配置AdobeGranite工作流清除配置OSGi。</td>
  </tr>
  <tr>
   <td><code>GenerateBundlesListFileTask</code></td>
   <td>crx2/crx3</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>RevisionCleanupTask</code></td>
   <td>crx3</td>
   <td>对于AEM 6.0到6.2上的TarMK实例，请手动运行脱机修订清理。</td>
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
>`DataStoreGarbageCollectionTask` 正在调用带有标记和扫描阶段的数据存储垃圾收集操作（如果使用）。对于使用共享数据存储的部署，请确保重新配置它或正确准备实例，以避免删除其他实例引用的项目。 这可能需要在触发此预升级任务之前，在所有实例上手动运行标记阶段。

### 升级前运行状况检查的默认配置{#default-configuration-of-the-pre-upgrade-health-checks}

`PreUpgradeTasksMBeanImpl` OSGI组件预配置了一列表升级前运行状况检查标记，在调用`runAllPreUpgradeHealthChecks`方法时执行：

* **system** -花岗岩维护运行状况检查使用的标签

* **升级前** -这是一个自定义标记，可添加到升级前可以设置为运行的所有运行状况检查中

列表可编辑。 除了标记外，您可以使用加号&#x200B;**(+)**&#x200B;和减号&#x200B;**(-)**&#x200B;按钮添加更多自定义标记，或删除默认标记。

**MBean方法**

可以使用[JMX控制台](/help/sites-administering/jmx-console.md)访问托管Bean功能。

可通过以下方式访问MBean:

1. 转到位于&#x200B;*https://serveraddress:serverport/system/console/jmx*&#x200B;的JMX控制台
1. 搜索&#x200B;**PreUpgradeTasks**&#x200B;并单击结果

1. 从&#x200B;**操作**&#x200B;部分选择任何方法，并在以下窗口中选择&#x200B;**调用**。

以下是`PreUpgradeTasksMBeanImpl`公开的所有可用方法的列表:

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
   <td>运行升级前维护任务，其名称为参数。</td>
  </tr>
  <tr>
   <td><code>isRunAllPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>检查<code>runAllPreUpgradeTasksmaintenance</code>任务当前是否正在运行。</td>
  </tr>
  <tr>
   <td><code>getAnyPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>检查是否有任何预升级维护任务当前正在运行，<br />返回一个包含当前正在运行的任务名称的阵列。</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunTime(preUpgradeTaskName)</code></td>
   <td>动作</td>
   <td>显示升级前维护任务的确切运行时间，其名称为参数。</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunState(preUpgradeTaskName)</code></td>
   <td>动作</td>
   <td>显示升级前维护任务的上次运行状态，其名称为参数。</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeHealthChecks(shutDownOnSuccess)</code></td>
   <td>动作</td>
   <td><p>运行所有升级前运行状况检查，并将其状态保存在sling home路径中名为<code>preUpgradeHCStatus.properties</code>的文件中。 如果<code>shutDownOnSuccess</code>参数设置为<code>true</code>，则AEM实例将关闭，但前提是所有升级前运行状况检查都处于“OK”状态。</p> <p>属性文件将用作任何未来升级的先决条件<br />，如果升级前运行状况检查<br />执行失败，则升级过程将停止。 如果要忽略预升级<br />运行状况检查的结果并仍启动升级，可以删除该文件。</p> </td>
  </tr>
  <tr>
   <td><code>detectUsageOfUnavailableAPI(aemVersion)</code></td>
   <td>动作</td>
   <td>列表在<br />升级到指定的AEM版本时不再满足的所有导入的包。 目标AEM版本必须<br />作为参数提供。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>可通过以下方式调用MBean方法：
>
>* JMX控制台
>* 连接到JMX的任何外部应用程序
>* cURL

>



## 禁用自定义登录模块{#disable-custom-login-modules}

>[!NOTE]
>
>只有从AEM 5版本升级时，才需要此步骤。 可以完全跳过它，从AEM 6旧版本升级。

在Apache Oak中，自定义`LoginModules`在存储库级别进行身份验证的配置方式已发生根本变化。

在AEM版本中，使用CRX2配置的配置放在`repository.xml`文件中，而从AEM 6开始，通过Web控制台在Apache Felix JAAS配置工厂服务中完成配置。

因此，升级后，必须为Apache Oak禁用和重新创建任何现有配置。

要禁用`repository.xml`的JAAS配置中定义的自定义模块，您需要修改配置以使用默认的`LoginModule`，如本例所示：

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
>有关详细信息，请参阅[使用外部登录模块进行身份验证](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html)。
>
>有关AEM 6中`LoginModule`配置的示例，请参阅[使用AEM 6](/help/sites-administering/ldap-config.md)配置LDAP。

## 从/install目录{#remove-updates-install-directory}中删除更新

>[!NOTE]
>
>在关闭AEM实例后，仅从crx-quickstart/install目录中删除包。 这是开始就地升级过程之前的最后步骤之一。

删除通过本地文件系统上的`crx-quickstart/install`目录部署的所有服务包、功能包或修补程序。 这将防止在更新完成后在新的AEM版本上意外安装旧的修补程序和服务包。

## 停止任何冷备用实例{#stop-tarmk-coldstandby-instance}

如果使用TarMK冷备用，请停止任何冷备用实例。 这将保证在出现升级问题时有效地恢复在线。 升级成功完成后，需要从升级的主实例重建冷备用实例。

## 禁用自定义计划作业{#disable-custom-scheduled-jobs}

禁用应用程序代码中包含的任何OSGi计划作业。

## 执行脱机修订清理{#execute-offline-revision-cleanup}

>[!NOTE]
>
>此步骤仅对TarMK安装是必需的

如果使用TarMK，则应在升级前执行脱机修订清理。 这将使存储库迁移步骤和后续升级任务执行得更快，并有助于确保在升级完成后可以成功执行在线修订清理。 有关运行脱机修订清除的信息，请参阅[执行脱机修订清除](/help/sites-deploying/storage-elements-in-aem-6.md#performing-offline-revision-cleanup)。

## 执行数据存储垃圾收集{#execute-datastore-garbage-collection}

>[!NOTE]
>
>此步骤仅对运行crx3的实例是必需的

在对CRX3实例运行修订清理后，您应运行数据存储垃圾收集，以删除数据存储中任何未引用的blob。 有关说明，请参阅[数据存储垃圾收集](/help/sites-administering/data-store-garbage-collection.md)上的文档。

## 如果需要，请升级模式库{#upgrade-the-database-schema-if-needed}

通常，Apache Oak堆栈AEM用于持久性的底层将负责根据需要升级数据库模式。

但是，当模式无法自动升级时，可能会出现这种情况。 这些环境大多是高安全性的，数据库在权限非常有限的用户下运行。 如果发生这种情况，AEM将继续使用旧模式。

为防止这种情况发生，您需要按照以下步骤升级模式:

1. 关闭需要升级的AEM实例。
1. 升级数据库模式。 请查阅有关数据库类型的文档，以了解实现此目的需要使用哪些工具。

   有关Oak如何处理模式升级的详细信息，请参阅Apache网站](https://jackrabbit.apache.org/oak/docs/nodestore/document/rdb-document-store.html#upgrade)上的[此页。

1. 继续升级AEM。

## 删除可能妨碍升级的用户{#delete-users-that-might-hinder-the-upgrade}

>[!NOTE]
>
>此升级前维护任务仅在以下情况下是必需的：
>
>* 您是从AEM 6.3之前的版本升级
>* 在升级过程中，您会遇到以下任何错误。

>



服务用户最终可能被误标记为常规用户的AEM旧版本时，会出现特殊情况。

如果发生这种情况，升级将失败，并显示如下消息：

```
ERROR [Apache Sling Repository Startup Thread] com.adobe.granite.repository.impl.SlingRepositoryManager Exception in a SlingRepositoryInitializer, SlingRepository service registration aborted
java.lang.RuntimeException: Unable to create service user [communities-utility-reader]:java.lang.RuntimeException: Existing user communities-utility-reader is not a service user.
```

要解决此问题，请确保执行以下操作：

1. 将实例与生产流量分离
1. 创建导致问题的用户的备份。 您可以通过包管理器执行此操作。 有关详细信息，请参阅[如何使用包。](/help/sites-administering/package-manager.md)
1. 删除导致问题的用户。 以下是可能属于此类别的用户列表:

   1. `dynamic-media-replication`
   1. `communities-ugc-writer`
   1. `communities-utility-reader`
   1. `communities-user-admin`
   1. `oauthservice`
   1. `sling-scripting`

## 旋转日志文件{#rotate-log-files}

我们建议在开始升级之前存档您的当前日志文件。 这样，在升级过程中和升级后，可以更轻松地监视和扫描日志文件，以识别和解决可能出现的任何问题。
