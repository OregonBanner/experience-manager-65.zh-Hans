---
title: 使用JMX控制台监视服务器资源
seo-title: 使用JMX控制台监视服务器资源
description: 了解如何使用JMX控制台监视服务器资源。
seo-description: 了解如何使用JMX控制台监视服务器资源。
uuid: 0a28aafe-61b2-472b-8f8f-2cd6540cbfee
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 873ce073-0055-4e1b-b3c6-ae7967700894
docset: aem65
translation-type: tm+mt
source-git-commit: f64eb57a69f2124523bd6eaed3e2f58a54c1ea8e
workflow-type: tm+mt
source-wordcount: '4989'
ht-degree: 1%

---


# 使用JMX控制台监视服务器资源{#monitoring-server-resources-using-the-jmx-console}

JMX控制台使您能够监视和管理CRX服务器上的服务。 下面几节总结了通过JMX框架公开的属性和操作。

有关如何使用控制台控件的信息，请参阅[使用JMX控制台](#using-the-jmx-console)。 有关JMX的背景信息，请参阅Oracle网站上的[Java管理扩展(JMX)技术](https://www.oracle.com/technetwork/java/javase/tech/javamanagement-140525.html)页。

有关创建MBean以使用JMX控制台管理服务的信息，请参阅[将服务与JMX控制台集成](/help/sites-developing/jmx-integration.md)。

## 工作流维护{#workflow-maintenance}

用于管理正在运行、已完成、过时和失败的工作流实例的操作。

* 域：com.adobe.granite.workflow
* 类型：维护

>[!NOTE]
>
>有关其他工作流管理工具以及可能的工作流实例状态的说明，请参阅[工作流控制台](/help/sites-administering/workflows-administering.md)。

### 操作 {#operations}

**listRunningWorkflowsPerModel** 列出为每个工作流模型运行的工作流实例数。

* 参数：无
* 返回值：包含Count和ModelId列的表格数据。

**listCompletedWorkflowsPerModel** 列出每个工作流模型的已完成工作流实例数。

* 参数：无
* 返回值：包含Count和ModelId列的表格数据。

**returnWorkflowQueueInfoLists** 有关已处理和已排队等待处理的工作流项的信息。

* 参数：无
* 返回值：包含以下列的表格数据：

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

**returnWorkflowJobTopicInfoLists** 处理工作流作业的信息，按主题组织。

* 参数：无
* 返回值：包含以下列的表格式数据：

   * 主题名称
   * 平均处理时间
   * 平均等待时间
   * 取消的作业
   * 失败的作业
   * 已完成的作业
   * 已处理的作业

**返** 回FailedWorkflowCount显示失败的工作流实例数。您可以指定工作流模型以查询或检索所有工作流模型的信息。

* 参数:

   * 模型：要查询的模型ID。 要查看所有工作流模型的失败工作流实例计数，请不指定值。 ID是模型节点的路径，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 返回值：失败的工作流实例数。

**返** 回FailedWorkflowCountPerModel显示每个工作流模型失败的工作流实例数。

* 参数：没有。
* 返回值：包含“计数”和“模型ID”列的表格数据。

**TerminateFailedInstances** 已失败的工作流实例终止。您可以终止所有失败的实例，或仅终止特定模型的失败实例。 或者，您可以在实例终止后重新启动它们。 您还可以测试操作以查看结果，而无需实际执行操作。

* 参数:

   * 重新启动实例：（可选）指定值`true`，以在实例终止后重新启动它们。 默认值`false`不导致终止的工作流实例重新启动。
   * 练习：（可选）指定值`true`，查看操作结果，而不实际执行操作。 默认值`false`将导致执行操作。
   * 模型：（可选）应用操作的模型的ID。 指定任何模型，以将操作应用于所有工作流模型的失败实例。 ID是模型节点的路径，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 返回值：终止的实例的表格数据，包含以下列：

   * 发起者
   * 实例ID
   * ModelId
   * 有效负荷
   * 开始注释
   * 工作流标题

**retryFailedWorkItems** 尝试执行已失败的工作项步骤。您可以重试所有失败的工作项，也可以只重试特定工作流模型的失败的工作项。 您可以选择测试操作，以查看结果，而无需实际执行操作。

* 参数:

   * 练习：（可选）指定值`true`，查看操作结果，而不实际执行操作。 默认值`false`将导致执行操作。
   * 模型：（可选）应用操作的模型的ID。 指定任何模型，以将操作应用于所有工作流模型的失败工作项。 ID是模型节点的路径，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 返回值：有关要重试的失败工作项的表格数据，包括以下列：

   * 发起者
   * 实例ID
   * ModelId
   * 有效负荷
   * 开始注释
   * 工作流标题

**PurgeActive** 删除特定年龄的活动工作流实例。可清除所有模型的活动实例，也可仅清除特定模型的实例。 您可以选择测试操作，以查看结果，而无需实际执行操作。

* 参数:

   * 模型：（可选）应用操作的模型的ID。 指定任何模型，以将操作应用于所有工作流模型的工作流实例。 ID是模型节点的路径，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * 工作流启动后的天数：要清除的工作流实例的年龄（以天为单位）。
   * 练习：（可选）指定值`true`，查看操作结果，而不实际执行操作。 默认值`false`将导致执行操作。

* 返回值：清除的活动工作流实例的表格数据，包括以下列：

   * 发起者
   * 实例ID
   * ModelId
   * 有效负荷
   * 开始注释
   * 工作流标题

**** countStaleWorkflows返回过时的工作流实例数。您可以检索所有工作流模型或特定模型的过时实例数。

* 参数:

   * 模型：（可选）应用操作的模型的ID。 指定任何模型，以将操作应用于所有工作流模型的工作流实例。 ID是模型节点的路径，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 返回值：过时的工作流实例数。

**restartStaleWorkflows** 重新启动过时的工作流实例。您可以重新启动特定模型的所有过时实例或仅重新启动过时实例。 您还可以测试操作以查看结果，而无需实际执行操作。

* 参数:

   * 模型：（可选）应用操作的模型的ID。 指定任何模型以将操作应用于所有工作流模型的旧实例。 ID是模型节点的路径，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * 练习：（可选）指定值`true`，查看操作结果，而不实际执行操作。 默认值`false`将导致执行操作。

* 返回值：已重新启动的工作流实例的列表。

**fetchModelList** 列出所有工作流模型。

* 参数：无
* 返回值：用于标识工作流模型（包括ModelId和ModelName列）的表格数据。

**** countRunningWorkflows返回正在运行的工作流实例数。您可以检索所有工作流模型或特定模型正在运行的实例数。

* 参数:

   * 模型：（可选）返回其运行实例数的模型的ID。 指定任何模型以返回所有工作流模型正在运行的实例数。 ID是模型节点的路径，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 返回值：正在运行的工作流实例数。

**** countCompletedWorkflows返回已完成的工作流实例数。您可以检索所有工作流模型或特定模型的已完成实例数。

* 参数:

   * 模型：（可选）返回已完成实例数的模型的ID。 指定任何模型以返回所有工作流模型的已完成实例数。 ID是模型节点的路径，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 返回值：已完成的工作流实例数。

**清除** 已完成从存储库中删除特定年龄的已完成工作流记录。定期使用此操作，在大量使用工作流时最大限度地减小存储库的大小。 您可以清除所有模型的已完成实例，也可以只清除特定模型的实例。 您可以选择测试操作，以查看结果，而无需实际执行操作。

* 参数:

   * 模型：（可选）应用操作的模型的ID。 指定任何模型，以将操作应用于所有工作流模型的工作流实例。 ID是模型节点的路径，例如：

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * 工作流完成后的天数：工作流实例处于完成状态的天数。
   * 练习：（可选）指定值`true`，查看操作结果，而不实际执行操作。 默认值`false`将导致执行操作。

* 返回值：有关已清除的已完成工作流实例的表格数据，包括以下列：

   * 发起者
   * 实例ID
   * ModelId
   * 有效负荷
   * 开始注释
   * 工作流标题

## 存储库 {#repository}

有关CRX存储库的信息

* 域：com.adobe.granite
* 类型：存储库

### 属性 {#attributes}

**名** 称JCR存储库实现的名称。只读.

**版** 本存储库实施版本。只读.

**** HomeDir存储库所在的目录。默认位置为&lt;QuickStart_Jar_Location>/crx-quickstart/repository。 只读.

**客** 户名称软件许可证授予的客户的名称。只读.

**许** 可证密钥此存储库安装的唯一许可证密钥。只读.

**AvailableDiskSpace** 存储库的此实例可用的磁盘空间，以兆字节为单位。只读.

**MaximumNumberOfOpenFiles** 一次可打开的文件数。只读.

**SessionTracker** crx.debug.sessions系统变量的值。true表示调试会话。 false表示正常会话。 读／写。

**描** 述符表示存储库属性的键值对集。所有属性都是只读的。

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
   <td>指示不可引用节点标识符的稳定性。 可能有以下值：
    <ul>
     <li>identifier.stability.indelight.duration:标识符不会更改。</li>
     <li>identifier.stability.method.duration:标识符可以在方法调用之间更改。</li>
     <li>identifier.stability.save.duration:标识符在保存／刷新周期中不会更改。</li>
     <li>identifier.stability.session.duration:标识符在会话期间不会更改。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>query.xpath.pos.index</td>
   <td>指示是否支持JCR 1.0 XPath查询语言。 true表示支持，false表示不支持。</td>
  </tr>
  <tr>
   <td>crx.repository.systemid</td>
   <td>在system.id文件中找到的系统标识符。</td>
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
   <td>指示是否可以更改节点的主节点类型。 true表示可以更改主节点类型，false表示不支持更改。</td>
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
   <td>true表示支持对存储库更改进行异步观察。 异步观察支持使应用程序能够在每次发生更改时接收并响应通知。</td>
  </tr>
  <tr>
   <td>query.jcrscore</td>
   <td><p>true表示jcr:score伪属性在XPath和SQL查询中可用，这些包含jcrfn:contains（在XPath中）或CONTAINS（在SQL中）函数，以执行全文搜索。</p> </td>
  </tr>
  <tr>
   <td>option.simple.versioning.supported</td>
   <td>true表示存储库支持简单的版本控制。 借助简单的版本控制，存储库保留节点的一系列连续版本。</td>
  </tr>
  <tr>
   <td>option.workspace.management.supported</td>
   <td>true表示存储库支持使用API创建和删除工作区。</td>
  </tr>
  <tr>
   <td>option.update.mixin.node.types.supported</td>
   <td>true表示存储库支持添加和删除现有节点的混合节点类型。</td>
  </tr>
  <tr>
   <td>node.type.management.primary.item.name.supported</td>
   <td>true表示存储库启用节点定义将主项作为子项包含。 使用API可访问主项目，无需知道项目名称。</td>
  </tr>
  <tr>
   <td>level.2.supported</td>
   <td>true表示LEVEL_1_SUPPORTED和OPTION_XML_IMPORT_SUPPORTED均为true。</td>
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
   <td>存储库实现的JCR规范的版本。</td>
  </tr>
  <tr>
   <td>option.journaled.observation.supported</td>
   <td>true表示应用程序可以执行存储库的常规观察。 通过记录观察，可以在特定时间段内获得一组改变通知。 </td>
  </tr>
  <tr>
   <td>query.languages</td>
   <td>存储库支持的查询语言。 无值表示无查询支持。</td>
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
   <td>true表示存储库支持访问控制，用于设置和确定用户访问节点的权限。</td>
  </tr>
  <tr>
   <td>option.baselines.supported</td>
   <td>true表示存储库同时支持配置和基准。</td>
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
   <td><p>指示节点类型继承的存储库支持级别。 可能有以下值：</p> <p>node.type.management.inheritance.minimal:主节点类型的注册仅限于那些仅具有nt:base作为超类型的节点类型。 混合节点类型的注册仅限于那些没有超类型的节点类型。</p> <p>node.type.management.inheritance.single:主节点类型的注册仅限于具有一个超级类型的节点类型。 混合节点类型的注册仅限于最多具有一个超类型的节点类型。</p> <p><br /> node.type.management.inheritance.multiple:主节点类型可以注册为一个或多个超类型。 可以用零个或多个超类型注册混合节点类型。</p> </td>
  </tr>
  <tr>
   <td>crx.cluster.preferredMaster</td>
   <td>true表示此群集节点是群集的首选主控。</td>
  </tr>
  <tr>
   <td>option.transactions.supported</td>
   <td>true表示存储库支持事务。</td>
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
   <td>javax.jcr.PropertyType常量的数组，这些常量表示注册节点类型可以指定的属性类型。 零长度数组表示已注册的节点类型无法指定属性定义。 属性类型有STRING、URI、BOOLEAN、LONG、DECIMAL、BINARY、DATE、NAME、PATH、WEAKREFERENCE、REFERENCE和UNDEFINED（如果支持）</td>
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
   <td><p>查询中加入的支持级别。 可能有以下值：</p>
    <ul>
     <li>查询.joins.none:不支持加入。 查询可以使用一个选择器。</li>
     <li>查询.joins.inner:支持内部连接。</li>
     <li>查询.joins.inner.outer:支持内连接和外连接。</li>
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
   <td>true表示存储库支持将XML代码作为内容导入。</td>
  </tr>
  <tr>
   <td>node.type.management.same.name.siblings.supported</td>
   <td>true表示存储库支持具有相同名称的同级节点（父节点相同）。</td>
  </tr>
  <tr>
   <td>node.type.management.residual.definitions.supported</td>
   <td>true表示存储库支持具有剩余定义的名称属性。 如果支持，项目定义的名称属性可以是星号(“*”)。</td>
  </tr>
  <tr>
   <td>node.type.management.autocreated.definitions.supported</td>
   <td>true表示存储库支持在创建节点时自动创建节点的子项（节点或属性）。</td>
  </tr>
  <tr>
   <td>crx.cluster.master</td>
   <td>true表示此存储库节点是群集的主控节点。</td>
  </tr>
  <tr>
   <td>level.1.supported</td>
   <td>true表示option.xml.export.support为true，且查询.languages的长度为非零。</td>
  </tr>
  <tr>
   <td>option.unfiled.content.supported</td>
   <td>true表示存储库支持未存档的内容。 未存档节点不是存储库层次结构的一部分。</td>
  </tr>
  <tr>
   <td>jcr.specification.name</td>
   <td>存储库实现的JCR规范的名称。</td>
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
   <td>true表示存储库支持节点锁定。 锁定使用户能够临时阻止其他用户进行更改。</td>
  </tr>
  <tr>
   <td>jcr.repository.version.display</td>
   <td> </td>
  </tr>
  <tr>
   <td>option.activities.supported</td>
   <td>true表示存储库支持活动。 活动是在工作区中执行的一组更改，这些更改合并到另一个工作区中。</td>
  </tr>
  <tr>
   <td>node.type.management.multivalued.properties.supported</td>
   <td>true表示存储库支持的节点属性可以具有零个或多个值。</td>
  </tr>
  <tr>
   <td>option.retention.supported</td>
   <td>true表示存储库支持使用外部保留管理应用程序将保留策略应用于内容并支持保留和释放。</td>
  </tr>
  <tr>
   <td>option.lifecycle.supported</td>
   <td>true表示存储库支持生命周期管理。</td>
  </tr>
 </tbody>
</table>

**工** 作区名称存储库中工作区的名称。只读.

**DataStoreGarbageCollectionDelay** 垃圾收集在每十个节点扫描后休眠的时间（以毫秒为单位）。读／写。

**BackupDelay** 备份过程在每个备份步骤之间休眠的时间（以毫秒为单位）。读／写。

**BackupInProgressA** 值为true表示正在执行备份进程。只读.

**BackupProgress** 对于当前备份，指已备份的所有文件的百分比。只读.

**CurrentBackupTarget** 对于当前备份，存储备份文件的ZIP文件。当备份未进行时，不显示任何值。 只读.

**BackupWasSuccessfulA** 值为true表示当前备份期间未发生错误，或者未进行任何备份。false表示在当前备份期间发生错误。 只读.

**BackupResult** 当前备份的状态。可能有以下值：

* 正在进行备份：当前正在执行备份。
* 备份已取消：备份已取消。
* 备份已完成，出现错误：备份过程中出错。 错误消息提供有关原因的信息。
* 备份已完成：备份成功。
* 迄今未执行备份：未进行备份。

只读.

**TarOptimization** RunningSince当前TAR文件优化过程开始的时间。只读.

**TarOptimizationDelay** TAR优化流程在每个步骤之间休眠的时间（以毫秒为单位）。读／写。

**ClusterProperties** 表示群集属性和值的键值对集。表中的每一行都表示群集属性。 只读.

**ClusterNodes** 存储库群集的成员。

**ClusterId** 此存储库群集的标识符。只读.

**ClusterMasterId** 此存储库群集的主控节点的标识符。只读.

**ClusterNodeId** 存储库群集的此节点的标识符。只读.

### 操作 {#operations-1}

**createWorkspace** 在此存储库中创建工作区。

* 参数:

   * 名称：表示新工作区名称的字符串值。

* 返回值：无

**runDataStoreGarbageCollection** 在存储库节点上执行垃圾收集。

* 参数:

   * 删除：一个布尔值，指示是否删除未使用的存储库项目。 如果值为true，则会删除未使用的节点和属性。 如果值为false，则会扫描所有节点，但不会删除任何节点。

* 返回值：无

**stopDataStoreGarbageCollection停** 止正在运行的数据存储垃圾收集。

* 参数：无
* 返回值：当前状态的字符串表示

**startBackup** 备份ZIP文件中的存储库数据。

* 参数:

   * `target`:（可选）一 `String` 个值，它表示要在其中存档存储库数据的ZIP文件或目录的名称。要使用ZIP文件，请包含ZIP文件扩展名。 要使用目录，请不包含文件扩展名。

      要执行增量备份，请指定以前用于备份的目录。

      可以指定绝对路径或相对路径。 相对路径相对于crx-quickstart目录的父目录。

      如果未指定任何值，则使用默认值`backup-currentdate.zip`，其中`currentdate`的格式为`yyyyMMdd-HHmm`。

* 返回值：无

**取** 消备份停止当前备份过程并删除该过程为存档数据而创建的临时存档。

* 参数：无
* 返回值：无

**块** RepositoryWritesBlocks对存储库数据的更改。系统会通知所有存储库备份监听器该块。

* 参数：无
* 返回值：无

**取** 消阻止存储库写入操作从存储库删除块。所有存储库备份监听器都会收到删除块的通知。

* 参数：无
* 返回值：无

**** startTarOptimization使用tarOptimizationDelay的默认值启动TAR文件优化过程。

* 参数：无
* 返回值：无

**stopTarOptimization** 停止TAR文件优化。

* 参数：无
* 返回值：无

**tarIndexMerge** 合并所有TAR集的顶部索引文件。顶级索引文件是具有不同主要版本的文件。 例如，以下文件被合并到文件index_3_1.tar中：index_1_1.tar、index_2_0.tar、index_3_0.tar。 已合并的文件将被删除（在上一个示例中，将删除index_1_1.tar、index_2_0.tar和index_3_0.tar）。

* 参数:

   * `background`:一个布尔值，指示是否在后台运行操作，以便在执行期间Web控制台可用。如果值为true，则在后台运行该操作。

* 返回值：无

**beceClusterMaster** 将此存储库节点设置为群集的主控节点。如果不是主控的，此命令将停止当前主控实例的监听器，并在当前节点上开始主控的监听器。 然后，此节点设置为主控节点并重新启动，导致群集中的所有其他节点(即由主控控制的节点)连接到此实例。

* 参数：无
* 返回值：无

**joinCluster** 将此存储库作为由群集主控控制的节点添加到群集。您必须提供用户名和密码才能进行身份验证。 连接使用基本身份验证。 安全凭据在发送到服务器之前是基64编码的。

* 参数:

   * `master`:一个字符串值，它表示运行主控存储库节点的计算机的IP地址或计算机名称。
   * `username`:用于在群集中进行身份验证的名称。
   * `password`:用于身份验证的密码。

* 返回值：无

**** traversalCheckTraverses和（可选）修复在特定节点开始的子树中的不一致。持久性管理器相关文档中详细介绍了这一点。

**consistencyCheckChecks** 检查和（可选）修复数据存储中的一致性。Datastore上的文档中对此进行了详细介绍。

## 存储库统计信息(TimeSeries){#repository-statistics-timeseries}

`org.apache.jackrabbit.api.stats.RepositoryStatistics`定义的每个统计类型的TimeSeries字段值。

* 域: `com.adobe.granite`
* 类型: `TimeSeries`
* 名称：`org.apache.jackrabbit.api.stats.RepositoryStatistics.Type`枚举类的以下值之一：

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
   * BUNDLE_WS_SIZE_COUNTER
   * 查询_平均
   * 查询计数
   * 查询持续时间
   * SESSION_COUNT
   * SESSION_LOGIN_COUNTER
   * SESSION_READ_AVERAGE
   * SESSION_READ_COUNTER
   * SESSION_READ_DURATION
   * SESSION_WRITE_AVERAGE
   * SESSION_WRITE_COUNTER
   * SESSION_WRITE_DURATION

### 属性 {#attributes-1}

为报告的每个统计类型提供以下属性：

* ValuePerSecond:最后一分钟每秒的测量值。 只读.
* ValuePerMinute:最后一小时内每分钟的测量值。 只读.
* ValuePerHour:上周每小时的测量值。 只读.
* ValuePerWeek:过去三年的每周测量值。 只读.

## 存储库查询统计数据{#repository-query-stats}

有关存储库查询的统计信息。

* 域：com.adobe.granite
* 类型：QueryStat

### 属性 {#attributes-2}

**SlowQueries** 有关用时最长的存储库查询的信息。只读.

**** SlowQueriesQueueSize要包含在SlowQuerys列表中的最大查询数。读写。

**PopularQueries** 有关发生次数最多的存储库查询的信息。只读.

**** PopularQueriesQueueSizePopularQueries列表中的最大查询数。读写。

### 操作 {#operations-2}

**clearSlowQuerysQueue** 从SlowQuerys列表中删除所有查询。

* 参数：无
* 返回值：无

**clearPopularQueriesQueue** 从PopularQuerys列表中删除所有查询。

* 参数：无
* 返回值：无

## 复制代理 {#replication-agents}

监视每个复制代理的服务。 创建复制代理时，服务会自动显示在JMX控制台中。

* **域：** com.adobe.granite.replication
* **类型：代** 理
* **名称：** 无值
* **属性：** {id=&quot;*Name*&quot;}，其 ** 中Name是代理名称属性的值。

### 属性 {#attributes-3}

**Id** 表示复制代理配置标识符的字符串值。多个代理可以使用相同的配置。 只读.

**有** 效指示代理配置是否正确的布尔值：

* `true`:有效配置。
* `false` :配置包含错误。

只读.

**启** 用指示是否启用代理的布尔值：

* `true`: 启用.
* `false`: 已禁用.

**QueueBlocked** 指示队列是否存在且被阻止的布尔值：

* `true`: 已阻止. 自动重试正在挂起。
* `false`:未阻止或不存在。

只读.

**QueuePaused** 指示作业队列是否已暂停的布尔值：

* `true`:已暂停（已暂停）
* `false`:未暂停或不存在。

读写。

**QueueNumEntries** 表示代理队列中作业数的int值。只读.

**QueueStatusTime** 指示获取显示的状态值时服务器上的时间的日期值。该值与页面加载时间相对应。 只读.

**QueueNextRetryTime** 对于已阻止的队列，一个日期值，指示何时发生下一次自动重试。未显示任何时间时，队列不会被阻止。 只读.

**QueueProcessingSinceA指示当前作业开始处理的日期值。** 当没有时间显示时，队列将被阻止或空闲。 只读.

**QueueLastProcessTime** 指示上一个作业何时完成的日期值。只读.

### 操作 {#operations-3}

**queueForceRetry** 对于被阻止的队列，向队列发出重试命令。

* 参数：无
* 返回值：无

**** queueClear从队列中删除所有作业。

* 参数：无
* 返回值：无

## Sling Engine {#sling-engine}

提供有关HTTP请求的统计信息，以便您能够监视SlingRequestProcessor服务的性能。

* 域：org.apache.sling
* 类型：引擎
* 属性：{service=RequestProcessor}

### 属性 {#attributes-4}

**Requests** Count自上次重置统计信息以来发生的请求数。

**MinRequestDurationMsec自上次重置统计信息以来处理请求所需的最短时间（以毫秒为单位）。** 

**MaxRequestDuratio** Msec自上次重置统计信息以来处理请求所需的最长时间（以毫秒为单位）。

**标** 准偏差持续时间秒处理请求所需的时间量的标准偏差。自上次重置统计信息后，使用所有请求计算标准偏差。

**MeanRequestDurationMsec** 处理请求所需的平均时间。平均值是使用自上次重置统计信息以来的所有请求计算的

### 操作 {#operations-4}

**resetStatistics** 将所有统计信息设置为零。在需要分析特定时间段内的请求处理性能时重置统计信息。

* 参数：无
* 返回值：无

**** id包ID的字符串表示。

**** installed指示是否安装包的布尔值：

* `true`: 已安装.
* `false`: 未安装.

**** installedBy上次安装该包的用户的ID。

**** installedDate上次安装包的日期。

**大** 小包含包大小（以字节为单位）的长值。


## 快速启动启动器{#quickstart-launcher}

有关启动过程和快速启动启动器的信息。

* 域：com.adobe.granite.quickstart
* 类型：启动器

### 操作 {#operations-5}

**日志**

在“快速启动”窗口中显示一条消息。

参数:

* p1:表示要显示的消息的`String`值。 下图显示了使用p1值`this is a log message`调用`log`的结果。

![launcheruiliz](assets/launcheruilog.png)

* 返回值：无

**启动已完成**

调用服务器启动器的startupFinished方法。 该方法尝试在Web浏览器中打开欢迎页面。

* 参数：无
* 返回值：无

**startupProgress**

设置服务器启动进程的完成值。 快速启动窗口上的进度栏表示完成值。

* 参数:

   * p1:一个浮点值，它表示启动过程的完成程度，作为一个小数。 该值应介于零和1之间。 例如，0.3表示完成30%。

* 返回值：没有。

![launcherproges](assets/launcherprogress.png)

## 第三方服务{#third-party-services}

多个第三方服务器资源安装向JMX控制台公开属性和操作的MBean。 下表列表了第三方资源并提供了指向更多信息的链接。

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
   <td><a href="https://docs.oracle.com/javase/8/docs/api/javax/management/package-summary.html">javax.</a> management包</td>
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

JMX控制台显示有关服务器上正在运行的多个服务的信息：

* 属性：服务属性，如配置或运行时数据。 属性可以是只读的或读写的。
* 操作：可在服务上调用的命令。

与OSGi服务一起部署的MBean向控制台公开服务属性和操作。 MBean确定公开的属性和操作，以及属性是只读还是读写。

JMX控制台的主页包含服务表。 表中的每一行都表示由MBean公开的服务。

1. 打开Web控制台并单击JMX选项卡。 ([http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
2. 单击服务的单元格值以查看服务的属性和操作。
3. 要更改属性值，请单击该值，在显示的对话框中指定值，然后单击“保存”。
4. 要调用服务操作，请单击操作名称，在显示的对话框中指定参数值，然后单击调用。

## 使用外部JMX应用程序进行监视{#using-external-jmx-applications-for-monitoring}

CRX允许外部应用程序通过[Java管理扩展(JMX)](https://docs.oracle.com/javase/6/docs/technotes/guides/management/overview.html)与受管Bean(MBean)进行交互。 使用通用控制台（如[JConsole](https://java.sun.com/developer/technicalArticles/J2SE/jconsole.html)或特定于域的监视应用程序），可以获取和设置CRX配置和属性，以及监视性能和资源使用情况。

### 使用JConsole连接到CRX {#using-jconsole-to-connect-to-crx}

要使用JConsole连接到CRX，请执行以下步骤：

1. 打开终端窗口。
1. 输入以下命令：

   `jconsole`

JConsole将开始，并显示JConsole窗口。

### 连接到本地CRX进程{#connecting-to-a-local-crx-process}

JConsole将显示本地Java虚拟机进程的列表。 列表将包含两个快速启动进程。 从本地进程的列表（通常是PID较高的进程）中选择快速启动“CHILD”进程。

![screen_shot_2012-03-26at114557am](assets/screen_shot_2012-03-26at114557am.png)

### 连接到远程CRX进程{#connecting-to-a-remote-crx-process}

要连接到远程CRX进程，需要启用承载远程CRX进程的JVM以接受远程JMX连接。

要启用远程JMX连接，在启动JVM时必须设置以下系统属性：

`com.sun.management.jmxremote.port=portNum`

在以上属性中，`portNum`是要启用JMX RMI连接的端口号。 请务必指定未使用的端口号。 除了发布RMI连接器以进行本地访问外，设置此属性还使用众所周知的名称“jmxrmi”在指定端口的专用只读注册表中发布一个附加的RMI连接器。

默认情况下，启用JMX代理进行远程监视时，它会根据在启动Java VM时需要使用以下系统属性指定的口令文件使用口令身份验证：

`com.sun.management.jmxremote.password.file=pwFilePath`

有关设置密码文件的详细说明，请参见[相关的JMX文档](https://docs.oracle.com/javase/6/docs/technotes/guides/management/agent.html)。

示例:

```shell
$ java
  -Dcom.sun.management.jmxremote.password.file=pwFilePath
  -Dcom.sun.management.jmxremote.port=8463
  -jar ./cq-quickstart.jar
```

### 使用CRX {#using-the-mbeans-provided-by-crx}提供的MBean

在连接到快速启动进程后，JConsole为CRX正在运行的JVM提供一系列常规监视工具。

![screen_shot_2012-03-26at115056am](assets/screen_shot_2012-03-26at115056am.png)

要访问CRX的内部监视和配置选项，请转到MBeans选项卡，并从左侧的分层内容树中选择您感兴趣的“属性”或“操作”部分。 例如，com.adobe.granite/Repository/Operations部分。

在该部分中，在左窗格中选择所需的属性或操作。

![screen_shot_2012-03-26at115728am](assets/screen_shot_2012-03-26at115728am.png)

