---
title: 卸载作业
seo-title: 卸载作业
description: 了解如何在拓扑中配置和使用AEM实例以执行特定类型的处理。
seo-description: 了解如何在拓扑中配置和使用AEM实例以执行特定类型的处理。
uuid: e971d403-dfd2-471f-b23d-a67e35f1ed88
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 370151df-3b8e-41aa-b586-5c21ecb55ffe
translation-type: tm+mt
source-git-commit: f24142064b15606a5706fe78bf56866f7f9a40ae

---


# 卸载作业{#offloading-jobs}

## 简介 {#introduction}

卸载在拓扑中分发大量Experience Manager实例的处理任务。 通过卸载，您可以使用特定的Experience Manager实例执行特定类型的处理。 专用处理使您能够最大限度地利用可用的服务器资源。

卸载基于 [Apache Sling Discovery和Sling JobManager](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html) 功能。 要使用卸载，可将Experience Manager群集添加到拓扑中，并标识群集处理的作业主题。 群集由一个或多个Experience Manager实例组成，因此单个实例被视为群集。

有关将实例添加到拓扑的信息，请参阅管 [理拓扑](/help/sites-deploying/offloading.md#administering-topologies)。

### 作业分配 {#job-distribution}

Sling JobManager和JobConsumer支持创建在拓扑中处理的作业：

* JobManager:为特定主题创建作业的服务。
* JobConsumer:执行一个或多个主题的作业的服务。 可以为同一主题注册多个JobConsumer服务。

当JobManager创建作业时，卸载框架会在拓扑中选择Experience Manager群集以执行该作业：

* 群集必须包括一个或多个运行为作业主题注册的JobConsumer的实例。
* 必须至少为群集中的一个实例启用主题。

有关优 [化任务分配的信息](/help/sites-deploying/offloading.md#configuring-topic-consumption) ，请参阅配置主题冲减。

![chlimage_1-109](assets/chlimage_1-109.png)

当卸载框架选择群集以执行作业，且群集由多个实例组成时，Sling Distribution将确定群集中的哪个实例执行该作业。

### 作业负载 {#job-payloads}

卸载框架支持将作业与存储库中的资源相关联的作业负载。 当为处理资源创建作业并且作业被卸载到另一台计算机时，作业负载很有用。

在创建作业时，仅保证有效负荷位于创建作业的实例上。 卸载作业时，复制代理会确保在最终消耗作业的实例上创建有效负荷。 当作业执行完成时，反向复制会导致有效负荷被复制回创建作业的实例。

## 管理拓扑 {#administering-topologies}

拓扑是松耦合的Experience Manager群集，参与卸载。 群集由一个或多个Experience Manager服务器实例（单个实例被视为群集）组成。

每个Experience Manager实例都运行以下与卸载相关的服务：

* 发现服务：向拓扑连接器发送请求以加入拓扑。
* 拓扑连接器：接收加入请求，并接受或拒绝每个请求。

拓扑中所有成员的发现服务指向其中一个成员上的拓扑连接器。 在随后几节中，此成员称为根成员。

![chlimage_1-110](assets/chlimage_1-110.png)

拓扑中的每个群集都包含一个被识别为引线的实例。 群集领导者代表群集的其他成员与拓扑交互。 当引线离开群集时，会自动选择群集的新引线。

### 查看拓扑 {#viewing-the-topology}

使用拓扑浏览器来探索Experience Manager实例参与的拓扑状态。 拓扑浏览器显示拓扑的簇和实例。

对于每个群集，您会看到一个群集成员列表，它指示每个成员加入群集的顺序以及哪个成员是领导者。 “当前”属性指示您当前管理的实例。

对于群集中的每个实例，您可以看到几个与拓扑相关的属性：

* 实例的作业用户主题的白名单。
* 用于连接拓扑的端点。
* 注册了实例以卸载的作业主题。
* 实例处理的作业主题。

1. 使用触屏UI，单击工具选项卡。 ([http://localhost:4502/tools.html](http://localhost:4502/tools.html))
1. 在“Granite操作”区域，单击“卸载浏览器”。
1. 在导航面板中，单击拓扑浏览器。

   将出现参与拓扑的群集。

   ![chlimage_1-111](assets/chlimage_1-111.png)

1. 单击群集可查看群集中实例及其ID、当前状态和“引线”状态的列表。
1. 单击实例ID可查看更详细的属性。

您还可以使用Web控制台来视图拓扑信息。 该控制台提供了有关拓扑群集的更多信息：

* 哪个实例是本地实例。
* 此实例用来连接到拓扑（传出）的拓扑连接器服务，以及连接到此实例（传入）的服务。
* 更改拓扑和实例属性的历史记录。

请按照以下过程打开Web控制台的“拓扑管理”页：

1. 在浏览器中打开Web控制台。 ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. 单击“主”>“拓扑管理”。

   ![chlimage_1-112](assets/chlimage_1-112.png)

### 配置拓扑成员关系 {#configuring-topology-membership}

Apache Sling Resource-Based Discovery Service在每个实例上运行，以控制Experience Manager实例与拓扑交互的方式。

发现服务向拓扑连接器服务发送定期的POST请求（心跳），以建立和维护与拓扑的连接。 拓扑连接器服务保留允许加入拓扑的IP地址或主机名的白名单：

* 要将实例连接到拓扑，请指定根成员的拓扑连接器服务的URL。
* 要使实例能够加入拓扑，请将该实例添加到根成员的拓扑连接器服务的白名单中。

使用Web控制台或sling:OsgiConfig节点配置org.apache.sling.discovery.impt.Config服务的以下属性：

<table>
 <tbody>
  <tr>
   <th>属性名称</th>
   <th>OSGi名称</th>
   <th>描述</th>
   <th>默认值</th>
  </tr>
  <tr>
   <td>心跳超时（秒）</td>
   <td>heartbeatTimeout</td>
   <td>在目标实例被视为不可用之前等待心跳响应的时间（以秒为单位）。 </td>
   <td>20</td>
  </tr>
  <tr>
   <td>心跳间隔（秒）</td>
   <td>heartbeatInterval</td>
   <td>心跳之间的秒数。</td>
   <td>15</td>
  </tr>
  <tr>
   <td>最小事件延迟（秒）</td>
   <td>minEventDelay</td>
   <td><p>当拓扑发生变化时，将状态从TOPOLOGY_CHANGING延迟到TOPOLOGY_CHANGED的时间。 当状态为TOPOLOGY_CHANGING时发生的每次更改都会将延迟增加这一时间量。</p> <p>这种延迟防止了听众被事件淹没。 </p> <p>要不使用延迟，请指定0或负数。</p> </td>
   <td>3</td>
  </tr>
  <tr>
   <td>拓扑连接器URL</td>
   <td>topologyConnectorUrl</td>
   <td>用于发送心跳消息的拓扑连接器服务的URL。</td>
   <td>http://localhost:4502/libs/sling/topology/connector</td>
  </tr>
  <tr>
   <td>拓扑连接器白名单</td>
   <td>topologyConnectorWhitelist</td>
   <td>列表本地拓扑连接器服务在拓扑中允许的IP地址或主机名。 </td>
   <td><p>localhost</p> <p>127.0.0.1</p> </td>
  </tr>
  <tr>
   <td>存储库描述符名称</td>
   <td>leaderElectionRepositoryDescriptor</td>
   <td> </td>
   <td>&lt;无值&gt;</td>
  </tr>
 </tbody>
</table>

请按照以下过程将CQ实例连接到拓扑的根成员。 该过程将实例指向根拓扑成员的拓扑连接器URL。 对拓扑的所有成员执行此过程。

1. 在浏览器中打开Web控制台。 ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. 单击“主”>“拓扑管理”。
1. 单击“配置发现服务”。
1. 向“拓扑连接器URL”属性添加一个项，并指定根拓扑成员的拓扑连接器服务的URL。 URL的形式为https://rootservername:4502/libs/sling/topology/connector。

对拓扑的根成员执行以下过程。 该过程会将其他拓扑成员的名称添加到其“发现服务”白名单中。

1. 在浏览器中打开Web控制台。 ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. 单击“主”>“拓扑管理”。
1. 单击“配置发现服务”。
1. 对于拓扑的每个成员，向“拓扑连接器白名单”属性添加一个项，并指定拓扑成员的主机名或IP地址。

## 配置主题消耗 {#configuring-topic-consumption}

使用卸载浏览器为拓扑中的Experience Manager实例配置主题使用。 对于每个实例，可指定它使用的主题。 例如，要配置拓扑以便只有一个实例使用特定类型的主题，请禁用除一个实例外的所有实例上的主题。

作业是使用循环法逻辑启用关联主题的分配数量实例。

1. 使用触屏UI，单击工具选项卡。 ([http://localhost:4502/tools.html](http://localhost:4502/tools.html))
1. 在“Granite操作”区域，单击“卸载浏览器”。
1. 在导航面板中，单击“卸载浏览器”。

   将显示卸载主题和可能使用这些主题的服务器实例。

   ![chlimage_1-113](assets/chlimage_1-113.png)

1. 要禁用某个实例的主题的使用，请单击该实例旁边的主题名称下方的禁用。
1. 要配置实例的所有主题使用，请单击任意主题下的实例标识符。

   ![chlimage_1-114](assets/chlimage_1-114.png)

1. 单击主题旁边的以下按钮之一以配置实例的使用行为，然后单击保存：

   * 已启用：此实例会消耗本主题的作业。
   * 禁用：此实例不会占用本主题的作业。
   * 独家：此实例仅会消耗本主题的作业。
   **注意：** 当您为某个主题选择“排他”时，所有其他主题将自动设置为“禁用”。

### 已安装的作业使用者 {#installed-job-consumers}

Experience Manager中安装了多个JobConsumer实施。 注册这些JobConsumer的主题显示在卸载浏览器中。 显示的其他主题是自定义JobConsumers注册的主题。 下表介绍了默认的JobConsumer。

| 作业主题 | 服务PID | 描述 |
|---|---|---|
| / | org.apache.sling.event.impl.jobs.deprecated.EventAdminBridge | 随Apache Sling一起安装。 处理OSGi事件管理员生成的作业，以实现向后兼容性。 |
| com/day/cq/replication/job/&amp;ast; | com.day.cq.replication.impl.AgentManagerImpl | 复制作业负载的复制代理。 |
| com/adobe/granite/workflow/offloading | com.adobe.granite.workflow.core.offloading.WorkflowOffloadingJobConsumer | 处理 [!UICONTROL DAM Update Asset Offloader工作流生成的作] 业。 |

### 实例的禁用和启用主题 {#disabling-and-enabling-topics-for-an-instance}

Apache Sling Job Consumer Manager服务提供主题白名单和黑名单属性。 配置这些属性以启用或禁用对Experience Manager实例上特定主题的处理。

**注意：** 如果实例属于拓扑，则还可以在拓扑中的任何计算机上使用卸载浏览器来启用或禁用主题。

创建已启用主题列表的逻辑首先允许白名单中的所有主题，然后删除黑名单中的主题。默认情况下，将启用所有主题(白名单值为 `*`)，并且不禁用任何主题（黑名单没有值）。

使用Web控制台或 `sling:OsgiConfig` 节点配置以下属性。 对 `sling:OsgiConfig` 于节点，Job Consumer Manager服务的PID是org.apache.sling.事件.impl.jobs.JobConsumerManager。

| Web控制台中的属性名称 | OSGi ID | 描述 |
|---|---|---|
| 主题白名单 | job.consumermanager.whitelist | 本地JobManager服务处理的主题列表。 &amp;ast；的默认值使所有主题都发送到注册的TopicConsumer服务。 |
| 主题黑名单 | job.consumermanager.blacklist | 本地JobManager服务不处理的主题列表。 |

## 创建用于卸载的复制代理 {#creating-replication-agents-for-offloading}

卸载框架使用复制在作者和worker之间传输资源。 卸载框架在实例加入拓扑时自动创建复制代理。 代理是使用默认值创建的。 您必须手动更改代理用于身份验证的密码。

>[!CAUTION]
>
>自动生成的复制代理的一个已知问题要求您手动创建新的复制代理。 在创建要卸载的 [代理之前，请按照问题使用自动生成的复制代理中的步骤操作](/help/sites-deploying/offloading.md#problems-using-the-automatically-generated-replication-agents) 。

创建复制代理，用于在实例之间传输作业负载以便卸载。 下图显示了从作者卸载到工作器实例所需的代理。 作者的Sling ID为1，而工作实例的Sling ID为2:

![chlimage_1-115](assets/chlimage_1-115.png)

此设置需要以下三个代理：

1. 创作实例上复制到该工作器实例的传出代理。
1. 创作实例上的反向代理，它从worker实例的发件箱中提取。
1. worker实例上的发件箱代理。

此复制方案与创作实例和发布实例之间使用的复制方案类似。 但是，对于卸载情况，涉及的所有实例都是创作实例。

>[!NOTE]
>
>卸载框架使用拓扑获取卸载实例的IP地址。 然后，框架会根据这些IP地址自动创建复制代理。 如果卸载实例的IP地址稍后发生更改，则在实例重新启动后，该更改会自动在拓扑上传播。 但是，卸载框架不会自动更新复制代理以反映新的IP地址。 要避免这种情况，请对拓扑中的所有实例使用固定的IP地址。

### 命名复制代理以进行卸载 {#naming-the-replication-agents-for-offloading}

对复制代理的 ***Name*** 属性使用特定格式，以便卸载框架自动为特定worker实例使用正确的代理。

**在创作实例上命名传出代理：**

`offloading_<slingid>`，其 `<slingid>` 中是worker实例的Sling ID。

示例: `offloading_f5c8494a-4220-49b8-b079-360a72f71559`

**在创作实例上命名反向代理：**

`offloading_reverse_<slingid>`，其 `<slingid>` 中是worker实例的Sling ID。

示例: `offloading_reverse_f5c8494a-4220-49b8-b079-360a72f71559`

**命名worker实例上的输出框：**

`offloading_outbox`

### 创建传出代理 {#creating-the-outgoing-agent}

1. 在作者 **上创建Replication Agent** 。 (请参阅有关 [复制代理的文档](/help/sites-deploying/replication.md))。 指定任何 **标题**。 名 **称必须遵** 循命名约定。
1. 使用以下属性创建代理：

   | 属性 | 值 |
   |---|---|
   | “设置”>“序列化类型” | 默认 |
   | “传输”>“传输URI” | https://*`<ip of target instance>`*:*`<port>`*`/bin/receive?sling:authRequestLogin=1` |
   | “传输”>“传输用户” | 目标实例上的复制用户 |
   | “传输”>“传输密码” | 目标实例上的复制用户口令 |
   | “扩展”>“HTTP方法” | POST |
   | “触发器”>“忽略默认值” | True |

### 创建反向代理 {#creating-the-reverse-agent}

1. 在作者 **上创建反向复制代理** 。 (请参阅有关 [复制代理的文档](/help/sites-deploying/replication.md)。)指定任何 **标题**。 名 **称必须遵** 循命名约定。
1. 使用以下属性创建代理：

   | 属性 | 值 |
   |---|---|
   | “设置”>“序列化类型” | 默认 |
   | “传输”>“传输URI” | https://*`<ip of target instance>`*:*`<port>`*`/bin/receive?sling:authRequestLogin=1` |
   | “传输”>“传输用户” | 目标实例上的复制用户 |
   | “传输”>“传输密码” | 目标实例上的复制用户口令 |
   | “扩展”>“HTTP方法” | 获取 |

### 创建Outbox代理 {#creating-the-outbox-agent}

1. 在worker实 **例上创建复制代理** 。 (请参阅有关 [复制代理的文档](/help/sites-deploying/replication.md)。)指定任何 **标题**。 名 **称必须** 是 `offloading_outbox`。
1. 使用以下属性创建代理。

   | 属性 | 值 |
   |---|---|
   | “设置”>“序列化类型” | 默认 |
   | “传输”>“传输URI” | repo://var/replication/outbox |
   | “触发器”>“忽略默认值” | True |

### 查找Sling ID {#finding-the-sling-id}

使用以下任一方法获取Experience Manager实例的Sling ID:

* 打开Web控制台，在“Sling设置”中，找到Sling ID属性的值([http://localhost:4502/system/console/status-slingsettings](http://localhost:4502/system/console/status-slingsettings))。 如果实例尚不是拓扑的一部分，则此方法可用。
* 如果实例已是拓扑的一部分，请使用拓扑浏览器。

## 卸载DAM资产的处理 {#offloading-the-processing-of-dam-assets}

配置拓扑实例，以便特定实例对在DAM中添加或更新的资产执行后台处理。

默认情况下，当DAM资产发生更改或  将DAM添加到DAM时，Experience Manager会执行DAM更新资产工作流。 更改默认行为，以便Experience Manager改为执行 [!UICONTROL DAM更新资产卸载程序工作流] 。 此工作流会生成一个主题为的JobManager作业 `com/adobe/granite/workflow/offloading`。 然后，配置拓扑，以便将作业卸载到专用Worker。

>[!CAUTION]
>
>当与工作流卸载一起使用时，任何工作流都不应为临时工作流。 例如，  DAM更新资产工作流在用于资产卸载时不得为临时工作流。 要在工作流中设置／取消设置临时标志，请参阅临时 [工作流](/help/assets/performance-tuning-guidelines.md#workflows)。

以下过程为卸载拓扑假设以下特征：

* 一个或多个Experience Manager实例正在创作用户与之交互以添加或更新DAM资产的实例。
* 用户不能直接与处理DAM资产的一个或多个Experience Manager实例交互。 这些实例专用于DAM资产的后台处理。

1. 在每个Experience Manager实例上，配置Discovery服务，使其指向根Tormiply Connector。 (请参阅 [配置拓扑成员关系](#title4)。)
1. 配置根拓扑连接器，使连接实例位于白名单中。
1. 打开卸载浏览器，并禁 `com/adobe/granite/workflow/offloading` 用用户与之交互以上传或更改DAM资产的实例上的主题。

   ![chlimage_1-116](assets/chlimage_1-116.png)

1. 在用户与之交互以上传或更改DAM资产的每个实例上，将工作流启动器配置为使用 [!UICONTROL DAM更新资产分载工作流] :

   1. 打开“工作流”控制台。
   1. 单击“启动器”选项卡。
   1. 找到执行 [!UICONTROL DAM更新资产工作流的两个启动器配置] 。 一个启动程序配置事件类型是“已创建节点”，另一个类型是“已修改节点”。
   1. 更改这两个事件类型，以便它们执行 [!UICONTROL DAM更新资产卸载工作流] 。 (有关启动器配置的信息，请参 [阅当节点更改时启动工作流](/help/sites-administering/workflows-starting.md)。)

1. 在执行DAM资产后台处理的实例上，禁用执行 [!UICONTROL DAM更新资产工作流的工作流启动程序] 。

## 进一步阅读 {#further-reading}

除了本页中显示的详细信息之外，您还可以阅读以下内容：

* 有关使用Java API创建作业和作业使用者的信息，请参 [阅创建和使用卸载作业](/help/sites-developing/dev-offloading.md)。
