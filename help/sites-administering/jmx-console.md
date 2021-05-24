---
title: 使用JMX控制台监控服务器资源
seo-title: 使用JMX控制台监控服务器资源
description: 了解如何使用JMX控制台监控服务器资源。
seo-description: 了解如何使用JMX控制台监控服务器资源。
uuid: 0a28aafe-61b2-472b-8f8f-2cd6540cbfee
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 873ce073-0055-4e1b-b3c6-ae7967700894
docset: aem65
exl-id: eabd8335-6140-4c15-8cff-21608719aa5f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4974'
ht-degree: 1%

---

# 使用JMX控制台监视服务器资源{#monitoring-server-resources-using-the-jmx-console}

通过JMX控制台，您可以监控和管理CRX服务器上的服务。 以下各节概述了通过JMX框架公开的属性和操作。

有关如何使用控制台控件的信息，请参阅[使用JMX控制台](#using-the-jmx-console)。 有关JMX的背景信息，请参阅Oracle网站上的[Java管理扩展(JMX)技术](https://www.oracle.com/technetwork/java/javase/tech/javamanagement-140525.html)页面。

有关创建MBean以使用JMX控制台管理服务的信息，请参阅[将服务与JMX控制台集成](/help/sites-developing/jmx-integration.md)。

## 工作流维护{#workflow-maintenance}

用于管理正在运行、已完成、已失效和失败的工作流实例的操作。

* 域：com.adobe.granite.workflow
* 类型：维护

>[!NOTE]
>
>有关其他工作流管理工具以及可能工作流实例状态的描述，请参阅[工作流控制台](/help/sites-administering/workflows-administering.md)。

### 运营 {#operations}

**** listRunningWorkflowsPerModel列出为每个工作流模型运行的工作流实例数。

* 参数：无
* 返回的值：包含Count和ModelId列的表格数据。

**** listCompletedWorkflowsPerModel列出每个工作流模型的已完成工作流实例数。

* 参数：无
* 返回的值：包含Count和ModelId列的表格数据。

**** returnWorkflowQueueInfoLists有关已处理和已排队等待处理的工作流项目的信息。

* 参数：无
* 返回的值：包含以下列的表数据：

   * 作业
   * 队列名称
   * 活动作业
   * 平均处理时间
   * 平均等待时间
   * 取消的作业
   * 失败的作业
   * 已完成的作业
   * 已处理的作业
   * 已排队作业

**** returnWorkflowJobTopicInfoLists按主题组织的工作流作业的处理信息。

* 参数：无
* 返回的值：包含以下列的表格数据：

   * 主题名称
   * 平均处理时间
   * 平均等待时间
   * 取消的作业
   * 失败的作业
   * 已完成的作业
   * 已处理的作业

**** returnFailedWorkflowCount显示失败的工作流实例数。您可以指定工作流模型来查询或检索所有工作流模型的信息。

* 参数:

   * 模型：要查询的模型的ID。 要查看所有工作流模型的失败工作流实例计数，请不指定任何值。 ID是模型节点的路径，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 返回的值：失败的工作流实例数。

**** returnFailedWorkflowCountPerModel显示每个工作流模型失败的工作流实例数。

* 参数：无。
* 返回的值：包含计数和模型ID列的表格数据。

**** terminateFailedInstancesTerminate失败的工作流实例。您可以终止所有失败实例，或仅终止特定模型的失败实例。 （可选）您可以在实例终止后重新启动实例。 您还可以测试操作以查看结果，而不实际执行操作。

* 参数:

   * 重新启动实例：（可选）指定值`true`，以在实例终止后重新启动实例。 默认值`false`不会重新启动已终止的工作流实例。
   * 练习：（可选）指定值`true` ，以查看操作结果，而不实际执行操作。 默认值`false`会导致执行该操作。
   * 模型：（可选）应用操作的模型的ID。 指定任何模型，以将操作应用到所有工作流模型的失败实例。 ID是模型节点的路径，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 返回的值：有关已终止的实例的表格数据，包含以下列：

   * 发起者
   * InstanceId
   * ModelId
   * 有效负荷
   * StartComment
   * WorkflowTitle

**** retryFailedWorkItemsAttems执行失败的工作项步骤。您可以重试所有失败的工作项，或仅重试特定工作流模型的失败工作项。 您可以选择测试该操作以查看结果，而不实际执行该操作。

* 参数:

   * 练习：（可选）指定值`true` ，以查看操作结果，而不实际执行操作。 默认值`false`会导致执行该操作。
   * 模型：（可选）应用操作的模型的ID。 指定任何模型，以将操作应用于所有工作流模型的失败工作项。 ID是模型节点的路径，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 返回的值：有关重试的失败工作项的表格数据，包括以下列：

   * 发起者
   * InstanceId
   * ModelId
   * 有效负荷
   * StartComment
   * WorkflowTitle

**** PurgeActiveRemoves特定页面的活动工作流实例。您可以清除所有模型的活动实例，或仅清除特定模型的实例。 您可以选择测试操作以查看结果，而不实际执行操作。

* 参数:

   * 模型：（可选）应用操作的模型的ID。 指定任何模型，以将该操作应用到所有工作流模型的工作流实例。 ID是模型节点的路径，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * 工作流启动后间隔的天数：要清除的工作流实例的年龄（以天为单位）。
   * 练习：（可选）指定值`true` ，以查看操作结果，而不实际执行操作。 默认值`false`会导致执行该操作。

* 返回的值：有关已清除的活动工作流实例的表格数据，包括以下列：

   * 发起者
   * InstanceId
   * ModelId
   * 有效负荷
   * StartComment
   * WorkflowTitle

**** countStaleWorkflows返回过时的工作流实例数。您可以检索所有工作流模型或特定模型的过时实例数。

* 参数:

   * 模型：（可选）应用操作的模型的ID。 指定任何模型，以将该操作应用到所有工作流模型的工作流实例。 ID是模型节点的路径，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 返回的值：过时的工作流实例数。

**** restartStaleWorkflows重新启动过时的工作流实例。您可以为特定模型重新启动所有过时实例或仅重新启动过时实例。 您还可以测试操作以查看结果，而不实际执行操作。

* 参数:

   * 模型：（可选）应用操作的模型的ID。 指定任何模型以将操作应用到所有工作流模型的失效实例。 ID是模型节点的路径，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * 练习：（可选）指定值`true` ，以查看操作结果，而不实际执行操作。 默认值`false`会导致执行该操作。

* 返回的值：重新启动的工作流实例列表。

**** fetchModelListList列出所有工作流模型。

* 参数：无
* 返回的值：用于标识工作流模型（包括ModelId和ModelName列）的表格数据。

**** countRunningWorkflows返回正在运行的工作流实例数。您可以检索所有工作流模型或特定模型的正在运行的实例数。

* 参数:

   * 模型：（可选）返回运行实例数的模型的ID。 指定不返回所有工作流模型正在运行的实例数的模型。 ID是模型节点的路径，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 返回的值：正在运行的工作流实例数。

**** countCompletedWorkflows返回已完成的工作流实例数。您可以检索所有工作流模型或特定模型的已完成实例数。

* 参数:

   * 模型：（可选）返回已完成实例数的模型的ID。 指定任何模型以返回所有工作流模型的已完成实例数。 ID是模型节点的路径，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 返回的值：已完成的工作流实例数。

**** purgeCompletedRemoves从存储库中删除特定年龄的已完成工作流的记录。当您大量使用工作流时，请定期使用此操作以最大程度地减小存储库的大小。 您可以清除所有模型的已完成实例，或仅清除特定模型的实例。 您可以选择测试操作以查看结果，而不实际执行操作。

* 参数:

   * 模型：（可选）应用操作的模型的ID。 指定任何模型，以将该操作应用到所有工作流模型的工作流实例。 ID是模型节点的路径，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * 工作流完成后间隔的天数：工作流实例处于已完成状态的天数。
   * 练习：（可选）指定值`true` ，以查看操作结果，而不实际执行操作。 默认值`false`会导致执行该操作。

* 返回的值：有关已清除的已完成工作流实例的表格数据，包括以下列：

   * 发起者
   * InstanceId
   * ModelId
   * 有效负荷
   * StartComment
   * WorkflowTitle

## 存储库 {#repository}

有关CRX存储库的信息

* 域：com.adobe.granite
* 类型：存储库

### 属性 {#attributes}

**** 名称JCR存储库实施的名称。只读.

**** 版本存储库实施版本。只读.

**** HomeDir存储库所在的目录。默认位置为&lt;QuickStart_Jar_Location>/crx-quickstart/repository。 只读.

**** CustomerName软件许可证颁发给的客户的名称。只读.

**** 许可证密钥此存储库安装的唯一许可证密钥。只读.

**** AvailableDiskSpace存储库的此实例可用的磁盘空间（以MB为单位）。只读.

**** MaximumNumberOfOpenFiles一次可打开的文件数。只读.

**** SessionTrackercrx.debug.sessions系统变量的值。true表示调试会话。 false表示正常会话。 读/写。

**** 描述符表示存储库属性的一组键值对。所有属性均为只读。

<table>
 <tbody>
  <tr>
   <th>键</th>
   <th>值</th>
  </tr>
  <tr>
   <td>option.node.and.property.with.same.name.supported</td>
   <td>指示节点和节点的属性是否可以具有相同的名称。 true表示支持相同的名称，false表示不支持。 </td>
  </tr>
  <tr>
   <td>identifier.stability</td>
   <td>指示不可引用节点标识符的稳定性。 可以使用以下值：
    <ul>
     <li>identifier.stability.indeltimed.duration:标识符不会更改。</li>
     <li>identifier.stability.method.duration:标识符在方法调用之间可能会发生更改。</li>
     <li>identifier.stability.save.duration:标识符在保存/刷新周期内不会更改。</li>
     <li>identifier.stability.session.duration:标识符在会话期间不会更改。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>query.xpath.pos.index</td>
   <td>指示是否支持JCR 1.0 XPath查询语言。 true表示支持，false表示不支持。</td>
  </tr>
  <tr>
   <td>crx.repository.systemid</td>
   <td>系统标识符，在system.id文件中找到。</td>
  </tr>
  <tr>
   <td>option.query.sql.supported</td>
   <td>指示是否支持JCR 1.0 XPath查询语言。 true表示支持，false表示不支持。</td>
  </tr>
  <tr>
   <td>jcr.repository.version</td>
   <td>存储库实施的版本。</td>
  </tr>
  <tr>
   <td>option.update.primary.node.type.supported</td>
   <td>指示节点的主节点类型是否可以更改。 true表示可以更改主节点类型，false表示不支持更改。</td>
  </tr>
  <tr>
   <td>option.node.type.management.supported</td>
   <td>指示是否支持节点类型管理。 true表示支持，false表示不支持。</td>
  </tr>
  <tr>
   <td>node.type.management.overrides.supported</td>
   <td>指示是否可以覆盖节点类型的继承属性或子节点定义。 true表示支持覆盖，false表示不覆盖。</td>
  </tr>
  <tr>
   <td>option.observation.supported</td>
   <td>true表示支持异步观察存储库更改。 支持异步观察，使应用程序能够在每次发生更改时接收并响应通知。</td>
  </tr>
  <tr>
   <td>query.jcrscore</td>
   <td><p>true表示jcr:score伪属性在包含jcrfn:contains（在XPath中）或CONTAINS（在SQL中）函数的XPath和SQL查询中可用，以执行全文搜索。</p> </td>
  </tr>
  <tr>
   <td>option.simple.versioning.supported</td>
   <td>true表示存储库支持简单的版本化。 通过简单的版本控制，存储库会维护节点的一系列连续版本。</td>
  </tr>
  <tr>
   <td>option.workspace.management.supported</td>
   <td>true表示存储库支持使用API创建和删除工作区。</td>
  </tr>
  <tr>
   <td>option.update.mixin.node.types.supported</td>
   <td>true表示存储库支持添加和删除现有节点的mixin节点类型。</td>
  </tr>
  <tr>
   <td>node.type.management.primary.item.name.supported</td>
   <td>true表示存储库使节点定义能够将主项包含为子项。 无需知道项目名称，即可使用API访问主项目。</td>
  </tr>
  <tr>
   <td>level.2.supported</td>
   <td>true表示LEVEL_1_SUPPORTED和OPTION_XML_IMPORT_SUPPORTED都为true。</td>
  </tr>
  <tr>
   <td>write.supported</td>
   <td>true表示存储库使用API提供写访问。 false表示只读访问。</td>
  </tr>
  <tr>
   <td>node.type.management.update.in.use.supported</td>
   <td>true表示您可以更改现有节点正在使用的节点定义。</td>
  </tr>
  <tr>
   <td>jcr.specification.version</td>
   <td>存储库实施的JCR规范的版本。</td>
  </tr>
  <tr>
   <td>option.journaled.observation.supported</td>
   <td>true表示应用程序可以执行对存储库的日志观察。 通过日志观察，可以在特定时间段内获得一组变化通知。 </td>
  </tr>
  <tr>
   <td>query.languages</td>
   <td>存储库支持的查询语言。 没有值表示不支持查询。</td>
  </tr>
  <tr>
   <td>option.xml.export.supported</td>
   <td>true表示存储库支持将节点导出为XML代码。</td>
  </tr>
  <tr>
   <td>node.type.management.multiple.binary.properties.supported</td>
   <td>true表示存储库支持注册具有多个二进制属性的节点类型。 false表示节点类型支持单个二进制属性。</td>
  </tr>
  <tr>
   <td>option.access.control.supported</td>
   <td>true表示存储库支持访问控制，用于设置和确定节点访问的用户权限。</td>
  </tr>
  <tr>
   <td>option.baselines.supported</td>
   <td>true表示存储库支持配置和基线。</td>
  </tr>
  <tr>
   <td>option.shareable.nodes.supported</td>
   <td>true表示存储库支持创建可共享节点。</td>
  </tr>
  <tr>
   <td>crx.cluster.id</td>
   <td>存储库群集的标识符。</td>
  </tr>
  <tr>
   <td>query.stored.queries.supported</td>
   <td>true表示存储库支持存储的查询。</td>
  </tr>
  <tr>
   <td>query.full.text.search.supported</td>
   <td>true表示存储库支持全文搜索。</td>
  </tr>
  <tr>
   <td>node.type.management.inheritance</td>
   <td><p>指示对节点类型继承的存储库支持级别。 可以使用以下值：</p> <p>node.type.management.interhance.minimal:主节点类型的注册仅限于仅将nt:base作为超类型的节点类型。 混合节点类型的注册仅限于那些没有超类型的节点类型。</p> <p>node.type.management.international.single:主节点类型的注册仅限于具有一个超类型的节点类型。 混合节点类型的配准被限制为最多具有一个超类型的节点类型。</p> <p><br /> node.type.management.international.multiple:主节点类型可以注册为一个或多个超类型。 混合节点类型可以用零个或多个超类型进行注册。</p> </td>
  </tr>
  <tr>
   <td>crx.cluster.preferredMaster</td>
   <td>true表示此群集节点是群集的首选主控。</td>
  </tr>
  <tr>
   <td>option.transactions.supported</td>
   <td>true表示存储库支持交易。</td>
  </tr>
  <tr>
   <td>jcr.repository.vendor.url</td>
   <td>存储库供应商的URL。</td>
  </tr>
  <tr>
   <td>node.type.management.value.constraints.supported</td>
   <td>true表示存储库支持节点属性的值约束。</td>
  </tr>
  <tr>
   <td>node.type.management.property.types</td>
   <td>javax.jcr.PropertyType常量的数组，表示注册节点类型可以指定的属性类型。 零长度数组表示注册的节点类型无法指定属性定义。 属性类型包括字符串、URI、布尔值、长、双精度、小数、二进制、日期、名称、路径、弱引用、引用和未定义（如果支持）</td>
  </tr>
  <tr>
   <td>node.type.management.orderable.child.nodes.supported</td>
   <td>true表示存储库支持保留子节点的顺序。</td>
  </tr>
  <tr>
   <td>jcr.repository.vendor</td>
   <td>存储库供应商的名称。</td>
  </tr>
  <tr>
   <td>query.joins</td>
   <td><p>对查询中连接的支持级别。 可以使用以下值：</p>
    <ul>
     <li>query.joins.none:不支持加入。 查询可以使用一个选择器。</li>
     <li>query.joins.inner:支持内部连接。</li>
     <li>query.joins.inner.outer:支持内连接和外连接。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>org.apache.jackrabbit.spi.commons.AdditionalEventInfo</td>
   <td> </td>
  </tr>
  <tr>
   <td>query.xpath.doc.order</td>
   <td>true表示存储库支持XPath 1.0查询语言。</td>
  </tr>
  <tr>
   <td>query.jcrpath</td>
   <td> </td>
  </tr>
  <tr>
   <td>option.xml.import.supported</td>
   <td>true表示存储库支持将XML代码导入为内容。</td>
  </tr>
  <tr>
   <td>node.type.management.same.name.siblings.supported</td>
   <td>true表示存储库支持具有相同名称的同级节点（具有相同父项的节点）。</td>
  </tr>
  <tr>
   <td>node.type.management.residual.definitions.supported</td>
   <td>true表示存储库支持具有剩余定义的名称属性。 如果支持，项目定义的name属性可以是星号("*")。</td>
  </tr>
  <tr>
   <td>node.type.management.autocreated.definitions.supported</td>
   <td>true表示在创建节点时，存储库支持自动创建节点的子项（节点或属性）。</td>
  </tr>
  <tr>
   <td>crx.cluster.master</td>
   <td>true表示此存储库节点是群集的主控节点。</td>
  </tr>
  <tr>
   <td>level.1.受支持</td>
   <td>true表示option.xml.export.support为true，query.languages的长度为非零。</td>
  </tr>
  <tr>
   <td>option.unfiled.content.supported</td>
   <td>true表示存储库支持未存档的内容。 未存档的节点不是存储库层次结构的一部分。</td>
  </tr>
  <tr>
   <td>jcr.specification.name</td>
   <td>存储库实施的JCR规范的名称。</td>
  </tr>
  <tr>
   <td>option.versioning.supported</td>
   <td>true表示存储库支持完全版本控制。</td>
  </tr>
  <tr>
   <td>jcr.repository.name</td>
   <td>存储库的名称。</td>
  </tr>
  <tr>
   <td>option.locking.supported</td>
   <td>true表示存储库支持节点锁定。 通过锁定，用户可暂时阻止其他用户进行更改。</td>
  </tr>
  <tr>
   <td>jcr.repository.version.display</td>
   <td> </td>
  </tr>
  <tr>
   <td>option.activities.supported</td>
   <td>true表示存储库支持活动。 活动是在工作区中执行的一组更改，这些更改会合并到另一个工作区中。</td>
  </tr>
  <tr>
   <td>node.type.management.multivalued.properties.supported</td>
   <td>true表示存储库支持的节点属性可以具有零个或更多值。</td>
  </tr>
  <tr>
   <td>option.retention.supported</td>
   <td>true表示存储库支持使用外部保留管理应用程序将保留策略应用于内容，并支持保留和释放。</td>
  </tr>
  <tr>
   <td>option.lifecycle.supported</td>
   <td>true表示存储库支持生命周期管理。</td>
  </tr>
 </tbody>
</table>

**** 工作区名称存储库中工作区的名称。只读.

**** DataStoreGarbageCollectionDelay垃圾收集在每十个节点扫描后休眠的时间（以毫秒为单位）。读/写。

**** BackupDelay备份过程在备份的每个步骤之间休眠的时间（以毫秒为单位）。读/写。

**** BackupInProgressA值为true表示正在执行备份进程。只读.

**** BackupProgress对于当前备份，备份的所有文件所占的百分比。只读.

**** CurrentBackupTarget对于当前备份，是存储备份文件的ZIP文件。当备份未进行时，不会显示任何值。 只读.

**** BackupWasSuccessfulA值为true表示在当前备份期间未发生错误，或未进行任何备份。false表示当前备份期间发生错误。 只读.

**** BackupResult当前备份的状态。可以使用以下值：

* 正在进行备份：当前正在执行备份。
* 备份已取消：备份已取消。
* 备份已完成，但出现错误：备份期间出错。 错误消息提供了有关原因的信息。
* 备份已完成：备份成功。
* 迄今未执行备份：没有正在进行的备份。

只读.

**** TarOptimizationRunningSince当前TAR文件优化过程开始的时间。只读.

**** TarOptimizationDelayTAR优化流程在流程每个步骤之间停留的时间（以毫秒为单位）。读/写。

**** ClusterProperties（群集属性）一组表示群集属性和值的键值对。表中的每一行都表示一个群集属性。 只读.

**** ClusterNodes存储库群集的成员。

**** ClusterId此存储库群集的标识符。只读.

**** ClusterMasterId此存储库群集主控节点的标识符。只读.

**** ClusterNodeId存储库群集的此节点的标识符。只读.

### 操作 {#operations-1}

**** createWorkspace在此存储库中创建工作区。

* 参数:

   * 名称：表示新工作区名称的字符串值。

* 返回的值：无

**** runDataStoreGarbageCollectionExces对存储库节点执行垃圾收集。

* 参数:

   * 删除：一个布尔值，指示是否删除未使用的存储库项目。 如果值为true，则会删除未使用的节点和属性。 如果值为false，则会扫描所有节点，但不会删除任何节点。

* 返回的值：无

**** stopDataStoreGarbageCollectionStops运行的数据存储垃圾收集。

* 参数：无
* 返回的值：当前状态的字符串表示形式

**** startBackup在ZIP文件中备份存储库数据。

* 参数:

   * `target`:（可选）一 `String` 个值，表示要在其中存档存储库数据的ZIP文件或目录的名称。要使用ZIP文件，请包含ZIP文件扩展名。 要使用目录，请不包含文件扩展名。

      要执行增量备份，请指定以前用于备份的目录。

      您可以指定绝对路径或相对路径。 相对路径是相对于crx-quickstart目录的父路径。

      未指定值时，将使用默认值`backup-currentdate.zip`，其中`currentdate`的格式为`yyyyMMdd-HHmm`。

* 返回的值：无

**** cancelBackup停止当前备份进程并删除该进程为存档数据而创建的临时存档。

* 参数：无
* 返回的值：无

**** blockRepositoryWritesBlocks对存储库数据的更改。所有存储库备份侦听器都会收到该块的通知。

* 参数：无
* 返回的值：无

**** unlockRepositoryWrites从存储库中删除块。所有存储库备份侦听器都会收到删除块的通知。

* 参数：无
* 返回的值：无

**** startTarOptimization使用tarOptimizationDelay的默认值启动TAR文件优化流程。

* 参数：无
* 返回的值：无

**** stopTarOptimizationStops TAR文件优化。

* 参数：无
* 返回的值：无

**** tarIndexMerge合并所有TAR集的顶级索引文件。顶级索引文件是具有不同主要版本的文件。 例如，以下文件将合并到文件index_3_1.tar中：index_1_1.tar、index_2_0.tar、index_3_0.tar。 将删除已合并的文件（在上一个示例中，将删除index_1_1.tar、index_2_0.tar和index_3_0.tar）。

* 参数:

   * `background`:一个布尔值，指示是否在后台运行操作，以便在执行期间可以使用Web控制台。值为true会在后台运行操作。

* 返回的值：无

**** becomeClusterMaster将此存储库节点设置为群集的主控节点。如果尚未主控，此命令将停止当前主控实例的侦听器，并在当前节点上启动主控侦听器。 然后，此节点将设置为主控节点并重新启动，从而导致群集中的所有其他节点(即由主控控制的节点)连接到此实例。

* 参数：无
* 返回的值：无

**** joinCluster将此存储库作为由群集主控控制的节点添加到群集中。您必须提供用户名和密码才能进行身份验证。 连接使用基本身份验证。 安全凭据在发送到服务器之前进行base-64编码。

* 参数:

   * `master`:一个字符串值，表示运行主控存储库节点的计算机的IP地址或计算机名称。
   * `username`:用于通过群集进行身份验证的名称。
   * `password`:用于身份验证的密码。

* 返回的值：无

**** traversalCheckTroverses和（可选）修复特定节点处子树开头的不一致问题。持久性管理器文档中详细介绍了该内容。

**** consistencyCheckChecks和（可选）修复数据存储中的一致性。有关数据存储的文档中详细介绍了该内容。

## 存储库统计信息（时间系列）{#repository-statistics-timeseries}

`org.apache.jackrabbit.api.stats.RepositoryStatistics`定义的每个统计类型的TimeSeries字段值。

* 域: `com.adobe.granite`
* 类型: `TimeSeries`
* 名称：`org.apache.jackrabbit.api.stats.RepositoryStatistics.Type`枚举类中的以下值之一：

   * BUNDLE_CACHE_ACCESS_COUNTER
   * BUNDLE_CACHE_MISS_AVERAGE
   * BUNDLE_CACHE_MISS_COUNTER
   * BUNDLE_CACHE_MISS_DURATION
   * BUNDLE_CACHE_SIZE_COUNTER
   * BUNDLE_COUNTER
   * BUNDLE_READ_COUNTER
   * BUNDLE_WRITE_AVERAGE
   * BUNDLE_WRITE_COUNTER
   * BUNDLE_WRITE_DURATION
   * 捆绑_WS_SIZE_COUNTER
   * QUERY_AVERAGE
   * QUERY_COUNT
   * QUERY_DURATION
   * SESSION_COUNT
   * SESSION_LOGIN_COUNTER
   * SESSION_READ_AVERAGE
   * SESSION_READ_COUNTER
   * SESSION_READ_DURATION
   * SESSION_WRITE_AVERAGE
   * SESSION_WRITE_COUNTER
   * SESSION_WRITE_DURATION

### 属性 {#attributes-1}

为报告的每种统计类型提供了以下属性：

* ValuePerSecond:最后一分钟内每秒的测量值。 只读.
* ValuePerMinute:最后一小时内每分钟的测量值。 只读.
* ValuePerHour:上周的每小时测量值。 只读.
* ValuePerWeek:过去三年的每周测量值。 只读.

## 存储库查询统计资料{#repository-query-stats}

有关存储库查询的统计信息。

* 域：com.adobe.granite
* 类型：QueryStat

### 属性 {#attributes-2}

**** SlowQueryes有关完成所用时间最长的存储库查询的信息。只读.

**** SlowQueryesQueueSize要包含在SlowQuerys列表中的查询数上限。读写。

**** PopularQueries关于发生次数最多的存储库查询的信息。只读.

**** PopulalQueriesQueueSizePopulalQuerys列表中的最大查询数。读写。

### 操作 {#operations-2}

**** clearSlowQueryesQueue从SlowQuerys列表中删除所有查询。

* 参数：无
* 返回的值：无

**** clearPopulalQueriesQueue从PopulalQuerys列表中删除所有查询。

* 参数：无
* 返回的值：无

## 复制代理 {#replication-agents}

监控每个复制代理的服务。 创建复制代理时，该服务会自动显示在JMX控制台中。

* **域：** com.adobe.granite.replication
* **类型：** 代理
* **名称：** 无值
* **属性：** {id=&quot;*名称*&quot;}，其中 ** Name是代理Name属性的值。

### 属性 {#attributes-3}

**** Id表示复制代理配置标识符的字符串值。多个代理可以使用相同的配置。 只读.

**** ValidA布尔值，指示代理配置是否正确：

* `true`:配置有效。
* `false` :配置包含错误。

只读.

**** Enabled：指示是否启用代理的布尔值：

* `true`: 启用.
* `false`: 已禁用.

**** QueueBlockedA布尔值，指示队列是否存在且被阻止：

* `true`: 已阻止. 自动重试挂起。
* `false`:未阻止或不存在。

只读.

**** QueuePaused布尔值，指示作业队列是否暂停：

* `true`:暂停（暂停）
* `false`:未暂停或不存在。

读写。

**** QueueNumEntries表示代理队列中作业数的整数值。只读.

**** QueueStatusTimeA日期值，指示获取显示状态值时服务器上的时间。值与页面加载时间相对应。 只读.

**** QueueNextRetryTimeFor blocked queues，一个日期值，指示何时发生下一次自动重试。当没有时间显示时，不会阻止队列。 只读.

**** QueueProcessingSinceA日期值，指示当前作业处理开始的时间。当没有出现时间时，队列会被阻止或空闲。 只读.

**** QueueLastProcessTime指示上一个作业完成时间的日期值。只读.

### 操作 {#operations-3}

**** queueForceRetryFor blocked队列向队列发出重试命令。

* 参数：无
* 返回的值：无

**** queueClearRemoves队列中的所有作业。

* 参数：无
* 返回的值：无

## Sling引擎{#sling-engine}

提供有关HTTP请求的统计信息，以便您能够监控SlingRequestProcessor服务的性能。

* 域：org.apache.sling
* 类型：引擎
* 属性：{service=RequestProcessor}

### 属性 {#attributes-4}

**** RequestsCount自上次重置统计信息以来发生的请求数。

**** MinRequestDurationMsec自上次重置统计信息以来处理请求所需的最短时间（以毫秒为单位）。

**** MaxRequestDuratioMsec处理请求自上次重置统计信息以来所需的最长时间（以毫秒为单位）。

**** StandardDevationDurationMsec处理请求所需时间量的标准偏差。自上次重置统计信息以来，标准偏差会使用所有请求进行计算。

**** MeanRequestDurationMsec处理请求所需的平均时间。自上次重置统计信息后，平均值会使用所有请求计算

### 操作 {#operations-4}

**** resetStatistics将所有统计信息设置为零。当您需要分析特定时间段内的请求处理性能时，请重置统计信息。

* 参数：无
* 返回的值：无

**** id包ID的字符串表示形式。

**** installed：指示是否安装了包的布尔值：

* `true`: 已安装.
* `false`: 未安装.

**** installedBy上次安装包的用户ID。

**** installedDate上次安装包的日期。

**** size（大小）保存包大小（以字节为单位）的长值。


## 快速启动启动器{#quickstart-launcher}

有关启动过程和快速启动启动启动器的信息。

* 域：com.adobe.granite.quickstart
* 类型：启动器

### 操作 {#operations-5}

**日志**

在“快速启动”窗口中显示一条消息。

参数:

* p1:表示要显示的消息的`String`值。
* 返回的值：无

**startupFinished**

调用服务器启动器的startupFinished方法。 方法会尝试在Web浏览器中打开欢迎页面。

* 参数：无
* 返回的值：无

**startupProgress**

设置服务器启动进程的完成值。 “快速启动”窗口中的进度条表示完成值。

* 参数:
   * p1:浮点值，表示完成启动过程的次数（作为一小部分）。 值应介于0和1之间。 例如，0.3表示完成30%。
* 返回的值：无。

## 第三方服务{#third-party-services}

若干第三方服务器资源安装向JMX控制台显示属性和操作的MBean。 下表列出了第三方资源并提供了指向更多信息的链接。

<table>
 <tbody>
  <tr>
   <th>域</th>
   <th>类型</th>
   <th>MBean类</th>
  </tr>
  <tr>
   <td>JMI实施</td>
   <td>MBeanServerDelegate</td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/javax/management/MBeanServerDelegate.html">javax.management.MBeanServerDelegate</a></td>
  </tr>
  <tr>
   <td>com.sun.management</td>
   <td>热点诊断</td>
   <td><a href="https://docs.oracle.com/javase/8/docs/jre/api/management/extension/com/sun/management/HotSpotDiagnosticMXBean.html">com.sun.management.HotSpotDiagnosticMXBean</a></td>
  </tr>
  <tr>
   <td>java.lang</td>
   <td>
    <ul>
     <li>类加载</li>
     <li>编译</li>
     <li>垃圾收集器</li>
     <li>内存</li>
     <li>MemoryManager</li>
     <li>内存池</li>
     <li>操作系统</li>
     <li>运行时</li>
     <li>线程</li>
    </ul> </td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/javax/management/package-summary.html">javax.</a> managementpackage</td>
  </tr>
  <tr>
   <td>java.util.logging</td>
   <td> </td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/java/util/logging/LoggingMXBean.html">java.util.logging.LoggingMXBean</a></td>
  </tr>
  <tr>
   <td>osgi.core</td>
   <td>
    <ul>
     <li>bundleState</li>
     <li>框架</li>
     <li>packageState</li>
     <li>serviceState</li>
    </ul> </td>
   <td><a href="https://osgi.org/specification/osgi.enterprise/7.0.0/service.jmx.html#d0e42567">org.osgi.jmx.</a> frameworkpackage</td>
  </tr>
 </tbody>
</table>

## 使用JMX控制台{#using-the-jmx-console}

JMX控制台显示有关服务器上运行的多项服务的信息：

* 属性：服务属性，如配置或运行时数据。 属性可以是只读或读写。
* 操作：可在服务中调用的命令。

与OSGi服务一起部署的MBean向控制台显示服务属性和操作。 MBean确定公开的属性和操作，以及属性是只读还是读写。

JMX控制台的主页包含一个服务表。 表中的每一行都表示由MBean公开的服务。

1. 打开Web控制台，然后单击JMX选项卡。 ([http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
2. 单击服务的单元格值可查看服务的属性和操作。
3. 要更改属性值，请单击该值，在显示的对话框中指定值，然后单击“保存”。
4. 要调用服务操作，请单击操作名称，在显示的对话框中指定参数值，然后单击调用。

## 使用外部JMX应用程序监视{#using-external-jmx-applications-for-monitoring}

CRX允许外部应用程序通过[Java管理扩展(JMX)](https://docs.oracle.com/javase/6/docs/technotes/guides/management/overview.html)与受管Bean(MBean)进行交互。 使用通用控制台（如[JConsole](https://java.sun.com/developer/technicalArticles/J2SE/jconsole.html)或特定于域的监控应用程序），可以获取和设置CRX配置和属性，以及监控性能和资源使用情况。

### 使用JConsole连接到CRX {#using-jconsole-to-connect-to-crx}

要使用JConsole连接到CRX，请执行以下步骤：

1. 打开终端窗口。
1. 输入以下命令：

   `jconsole`

将启动JConsole，并出现JConsole窗口。

### 连接到本地CRX进程{#connecting-to-a-local-crx-process}

JConsole将显示本地Java虚拟机进程的列表。 该列表将包含两个快速启动进程。 从本地进程（通常是PID较高的进程）列表中选择快速启动“CHILD”进程。

![screen_shot_2012-03-26at114557am](assets/screen_shot_2012-03-26at114557am.png)

### 连接到远程CRX进程{#connecting-to-a-remote-crx-process}

要连接到远程CRX进程，需要启用承载远程CRX进程的JVM以接受远程JMX连接。

要启用远程JMX连接，在启动JVM时必须设置以下系统属性：

`com.sun.management.jmxremote.port=portNum`

在上述属性中，`portNum`是要启用JMX RMI连接的端口号。 请务必指定未使用的端口号。 除了发布用于本地访问的RMI连接器外，设置此属性还会在指定端口的专用只读注册表中使用众所周知的名称“jmxrmi”发布一个额外的RMI连接器。

默认情况下，启用JMX代理进行远程监视时，它会根据在启动Java VM时需要使用以下系统属性指定的密码文件使用密码验证：

`com.sun.management.jmxremote.password.file=pwFilePath`

有关设置密码文件的详细说明，请参阅[相关JMX文档](https://docs.oracle.com/javase/6/docs/technotes/guides/management/agent.html)。

示例:

```shell
$ java
  -Dcom.sun.management.jmxremote.password.file=pwFilePath
  -Dcom.sun.management.jmxremote.port=8463
  -jar ./cq-quickstart.jar
```

### 使用CRX {#using-the-mbeans-provided-by-crx}提供的MBean

在连接到快速启动进程后，JConsole为CRX正在运行的JVM提供一系列常规监控工具。

![screen_shot_2012-03-26at115056am](assets/screen_shot_2012-03-26at115056am.png)

要访问CRX的内部监控和配置选项，请转到MBeans选项卡，然后从左侧的分层内容树中，选择您感兴趣的“属性”或“操作”部分。 例如com.adobe.granite/Repository/Operations部分。

在该部分中，在左窗格中选择所需的属性或操作。

![screen_shot_2012-03-26at115728am](assets/screen_shot_2012-03-26at115728am.png)
