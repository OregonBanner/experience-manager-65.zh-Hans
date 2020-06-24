---
title: 操作仪表板
seo-title: 操作仪表板
description: 了解如何使用“操作”仪表板。
seo-description: 了解如何使用“操作”仪表板。
uuid: ef24813f-a7a8-4b26-a496-6f2a0d9efef6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: b210f5d7-1d68-49ee-ade7-667c6ab11d2b
docset: aem65
translation-type: tm+mt
source-git-commit: 9eb8f3921e7d485ca4eb035cd04a9d8731dd6b06
workflow-type: tm+mt
source-wordcount: '6229'
ht-degree: 2%

---


# 操作仪表板 {#operations-dashboard}

## 简介 {#introduction}

AEM 6中的“操作”仪表板可帮助系统操作员一览地监视AEM系统运行状况。 它还提供有关AEM相关方面的自动生成的诊断信息，并允许配置和运行自包含的维护自动化，从而显着减少项目操作和支持案例。 “操作”仪表板可通过自定义运行状况检查和维护任务进行扩展。 此外，操作仪表板数据可通过JMX从外部监视工具访问。

**运营仪表板:**

* 是一键式系统状态，帮助运营部门提高效率
* 在一个集中的位置提供系统运行状况概述
* 缩短查找、分析和修复问题的时间
* 提供自带的维护自动化功能，有助于显着降低项目运营成本

可以从AEM欢迎屏幕转 **到工** 具 **-** 操作，访问它。

>[!NOTE]
>
>要能够访问“操作”仪表板，登录用户必须是“操作员”用户组的一部分。 有关详细信息，请参阅有关用户、 [组和访问权限管理的文档](/help/sites-administering/user-group-ac-admin.md)。

## 健康报表 {#health-reports}

运行状况报告系统通过Sling运行状况检查提供AEM实例的运行状况信息。 这可以通过OSGI、JMX、HTTP请求（通过JSON）或通过触屏UI来完成。 它优惠某些可配置计数器的度量值和阈值，在某些情况下，将优惠有关如何解决该问题的信息。

它具有以下几个功能。

## 运行状况检查 {#health-checks}

健康 **报告** (Health Reports)是一个卡片系统，表明特定产品区域的健康状况是否良好。 这些卡是Sling运行状况检查的可视化功能，它将来自JMX和其他来源的数据聚合，并再次以MBean的身份显示处理的信息。 这些MBean还可在JMX Web控 [制台中](/help/sites-administering/jmx-console.md)，在 **org.apache.sling.healthcheck域下进行检查** 。

运行状况报告界面可通过AEM欢迎屏 **幕上的** 工具 **-** 操作 **-** 运行状况报告，或直接通过以下URL进行访问：

`https://<serveraddress>:port/libs/granite/operations/content/healthreports/healthreportlist.html`

![chlimage_1-116](assets/chlimage_1-116.png)

卡系统显示三种可能的状态： **确定**, **警告** , **严重**。 这些状态是规则和阈值的结果，可以通过将鼠标悬停在卡上并单击操作栏中的齿轮图标来配置这些规则和阈值：

![chlimage_1-117](assets/chlimage_1-117.png)

### 运行状况检查类型 {#health-check-types}

AEM 6中有两种类型的运行状况检查：

1. 个人运行状况检查
1. 综合运行状况检查

“个 **人健康检查** ”是与状态卡对应的单个健康检查。 单个运行状况检查可以配置规则或阈值，并可提供一个或多个提示和链接以解决已识别的运行状况问题。 让我们以“日志错误”检查为例： 如果实例日志中有ERROR条目，您将在运行状况检查的详细信息页面上找到它们。 在页面顶部，您将在“诊断工具”部分看到指向“日志消息”分析器的链接，该链接将使您能够更详细地分析这些错误并重新配置记录器。

复 **合运行状况检查** (Composite Health Check)是一种检查，可从多个单独的检查中聚合信息。

复合运行状况检查是借助过滤器标 **签配置的**。 本质上，具有相同筛选器标签的所有单个检查都将被分组为复合运行状况检查。 仅当聚合的所有单个检查都具有“OK”状态时，“Composite Health Check”（综合运行状况检查）才会具有“OK”状态。

### 如何创建运行状况检查 {#how-to-create-health-checks}

在“操作”仪表板中，您可以直观地显示单个运行状况检查和复合运行状况检查的结果。

### 创建单个运行状况检查 {#creating-an-individual-health-check}

创建单个运行状况检查涉及两个步骤： 实施Sling运行状况检查并在仪表板的配置节点中添加运行状况检查项。

1. 要创建Sling运行状况检查，您需要创建实施Sling HealthCheck界面的OSGI组件。 您将此组件添加到捆绑包中。 组件的属性将完全标识运行状况检查。 安装该组件后，将自动为运行状况检查创建JMX MBean。 有关更多 [信息，请参阅Sling](https://sling.apache.org/documentation/bundles/sling-health-check-tool.html) Health Check文档。

   Sling Health Check组件的示例，它用OSGI服务组件注释编写：

   ```java
   @Component(service = HealthCheck.class,
   property = {
       HealthCheck.NAME + "=Example Check",
       HealthCheck.TAGS + "=example",
       HealthCheck.TAGS + "=test",
       HealthCheck.MBEAN_NAME + "=exampleHealthCheckMBean"
   })
    public class ExampleHealthCheck implements HealthCheck {
       @Override
       public Result execute() {
           // health check code
       }
    }
   ```

   >[!NOTE]
   >
   >该 `MBEAN_NAME` 属性定义将为此运行状况检查生成的mbean的名称。

1. 创建运行状况检查后，需要创建新的配置节点，以便在“操作”仪表板界面中访问该节点。 对于此步骤，必须知道运行状况检查的JMX Mbean名称(属 `MBEAN_NAME` 性)。 要为运行状况检查创建配置，请打开CRXDE，并在以下路径下添加新节点( **nt:unstructured**)类型： `/apps/settings/granite/operations/hc`

   新节点上应设置以下属性：

   * **名称:** `sling:resourceType`

      * **类型:** `String`
      * **值：** `granite/operations/components/mbean`
   * **名称:** `resource`

      * **类型:** `String`
      * **值：** `/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck/exampleHealthCheck`

   >[!NOTE]
   >
   >上面的资源路径按如下方式创建： 如果运行状况检查的mbean名称为“test”，则在路径末尾添加“test” `/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck`
   >
   >因此，最终的路径是：
   >
   >`/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck/test`

   >[!NOTE]
   >
   >确保路径 `/apps/settings/granite/operations/hc` 的以下属性设置为true:
   >
   >
   >`sling:configCollectionInherit`
   >
   >`sling:configPropertyInherit`
   >
   >
   >这将告知配置管理器将新配置与现有配置合并 `/libs`。

### 创建复合运行状况检查 {#creating-a-composite-health-check}

综合运行状况检查的作用是聚合多个共享一组常见功能的独立运行状况检查。 例如，安全组合运行状况检查将执行与安全相关验证的所有单个运行状况检查组合在一起。 创建复合检查的第一步是添加新的OSGI配置。 要使其显示在“操作”仪表板中，需要添加新的配置节点，这与我们对简单检查所做的相同。

1. 转到OSGI控制台中的Web配置管理器。 您可以通过访问 `https://serveraddress:port/system/console/configMgr`
1. 搜索名为Apache Sling Composite **Health Check的条目**。 找到它后，请注意已有两种配置可用： 一个用于系统检查，另一个用于安全检查。
1. 通过按配置右侧的“+”按钮创建新配置。 将出现一个新窗口，如下所示：

   ![chlimage_1-23](assets/chlimage_1-23.jpeg)

1. 创建配置并保存。 将使用新配置创建Mbean。

   每个配置属性的用途如下：

   * **名称(hc.name):** 复合运行状况检查的名称。 建议使用有意义的名称。
   * **标记(hc.tags):** 此运行状况检查的标记。 如果此复合运行状况检查是另一个复合运行状况检查的一部分（如在运行状况检查的层次结构中），请添加此复合健康检查与之相关的标记。
   * **MBean名称(hc.mbean.name):** 此复合运行状况检查的JMX MBean将指定给的Mbean的名称。
   * **筛选标记(filter.tags):** 这是特定于复合运行状况检查的属性。 这些是合成应聚合的标记。 复合运行状况检查将聚合其组下的所有运行状况检查，这些检查具有与此复合的任何过滤器标签匹配的任何标签。 例如，具有过滤器测试和检查的 **复合运行状况检查** 将聚合所有具 **有测试** 和检查 **标签属性(** PH)的 ****`hc.tags`单独和复合运行状况检查。

   >[!NOTE]
   >
   >将为Apache Sling Composite Health Check的每个新配置创建一个新的JMX Mbean。**

1. 最后，需要在“操作仪表板”配置节点中添加刚刚创建的复合运行状况检查的条目。 此过程与单个运行状况检查的过程相同： 需要在 **下创建nt** :unstructured类型的节点 `/apps/settings/granite/operations/hc`。 节点的资源属性将由OSGI配置中 **hc.mean.name的值** 定义。

   例如，如果您创建了配置并将hc. **mbean.name值设置****为diskusage**，则配置节点将如下所示：

   * **名称:** `Composite Health Check`

      * **类型:** `nt:unstructured`

   使用以下属性：

   * **名称:** `sling:resourceType`

      * **类型:** `String`
      * **值：** `granite/operations/components/mbean`
   * **名称:** `resource`

      * **类型:** `String`
      * **值：** `/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck/diskusage`

   >[!NOTE]
   >
   >如果您创建逻辑上属于复合检查的单个运行状况检查(默认情况下，该复合检查在仪表板中已存在)，它们将自动捕获并分组在相应的复合检查下。 因此，无需为这些检查创建新的配置节点。
   >
   >例如，如果您创建单个安全运行状况检查，您只需将其分配为“**security**”标记，它就会安装，它将自动显示在“操作”仪表板的“安全检查”组合检查下。

### AEM附带的运行状况检查 {#health-checks-provided-with-aem}

<table>
 <tbody>
  <tr>
   <td><strong>zHealthcheck名称</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>查询性能</td>
   <td><p>此运行状况检查在AEM <strong>6.4中已得</strong>到简化 <code>Oak QueryStats</code> ，现在可以检查最近重构的 <code>SlowQueries </code>MBean，更确切地说是属性。 如果统计数据包含任何慢速查询，运行状况检查将返回警告。 否则，返回“确定”状态。<br /> </p> <p>此运行状况检查的 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DqueriesStatus%2Ctype%3DHealthCheck">MBean为org.apache.sling.healthcheck:name=querysStatus,type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>观察队列长度</td>
   <td><p>观察队列长度迭代所有事件监听器和背景观察器，将其与 <code>queueSize </code>其和 <code>maxQueueSize</code> :</p>
    <ul>
     <li>如果值超过值 <code>queueSize</code> (即事件 <code>maxQueueSize</code> 将被删除时)，则返回关键状态</li>
     <li>返回警告， <code>queueSize</code> 如果值超 <code>maxQueueSize * WARN_THRESHOLD</code> 过（默认值为0.75） </li>
    </ul> <p>每个队列的最大长度来自不同的配置（Oak和AEM），不能通过此运行状况检查进行配置。 此运行状况检查的 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DObservationQueueLengthHealthCheck%2Ctype%3DHealthCheck">MBean为org.apache.sling.healthcheck:name=OpercationQueueLengthHealthCheck,type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>查询遍历限制</td>
   <td><p>查询遍历限制检 <code>QueryEngineSettings</code> 查MBean，更确切地 <code>LimitInMemory</code> 检查 <code>LimitReads</code> MBean和属性，并返回以下状态：</p>
    <ul>
     <li>如果其中一个限制等于或高于 <code>Integer.MAX_VALUE</code></li>
     <li>如果某个限制低于10000，则返回“警告”状态（Oak的推荐设置）</li>
     <li>如果无法检索限制或 <code>QueryEngineSettings</code> 任何限制，则返回“关键”状态</li>
    </ul> <p>此运行状况检查的 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DqueryTraversalLimitsBundle%2Ctype%3DHealthCheck">Mbean为org.apache.sling.healthcheck:name=queryTraversalLimitsBundle,type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>同步的时钟</td>
   <td><p>此检查仅与文档节点 <a href="https://github.com/apache/sling-old-svn-mirror/blob/4df9ab2d6592422889c71fa13afd453a10a5a626/bundles/extensions/discovery/oak/src/main/java/org/apache/sling/discovery/oak/SynchronizedClocksHealthCheck.java">存储群集相关</a>。 它返回以下状态：</p>
    <ul>
     <li>当实例时钟不同步并超出预定的低阈值时，返回“警告”状态</li>
     <li>当实例时钟不同步并超过预定义的高阈值时返回“关键”状态</li>
    </ul> <p>此运行状况检查的 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DslingDiscoveryOakSynchronizedClocks%2Ctype%3DHealthCheck">Mbean为org.apache.sling.healthcheck:name=slingDiscoveryOakSynchronizedCloks,type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>异步索引</td>
   <td><p>异步索引检查：</p>
    <ul>
     <li>如果至少一个索引通道出现故障，则返回关键状态</li>
     <li>检查所有 <code>lastIndexedTime</code> 索引通道，并：
      <ul>
       <li>如果超过2小时前返回关键状态 </li>
       <li>如果在2小时到45分钟之前，返回警告状态 </li>
       <li>如果45分钟前不到，则返回“OK”状态 </li>
      </ul> </li>
     <li>如果没有满足这些条件，则返回“确定”状态</li>
    </ul> <p>“严重”和“警告”状态阈值均可配置。 此运行状况检查的 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DasyncIndexHealthCheck%2Ctype%3DHealthCheck">Mbean为org.apache.sling.healthcheck:name=asyncIndexHealthCheck,type=HealthCheck</a>。</p> <p><strong>注意： </strong>此运行状况检查在AEM 6.4中可用，并已支持到AEM 6.3.0.1。</p> </td>
  </tr>
  <tr>
   <td>大型 Lucene 索引</td>
   <td><p>此检查使用MBean公开的数 <code>Lucene Index Statistics</code> 据来标识大索引并返回：</p>
    <ul>
     <li>如果有超过10亿文档的指数，则警告状态</li>
     <li>如果有超过15亿文档的指数，则处于关键状态</li>
    </ul> <p>可以配置阈值，运行状况检查的MBean <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DlargeIndexHealthCheck%2Ctype%3DHealthCheck">为org.apache.sling.healthcheck:name=largeIndexHealthCheck,type=HealthCheck。</a></p> <p><strong>注意： </strong>此检查在AEM 6.4中可用，并已支持到AEM 6.3.2.0。</p> </td>
  </tr>
  <tr>
   <td>系统维护</td>
   <td><p>系统维护是一个复合检查，如果所有维护任务都按配置运行，则返回“确定”。 请记住：</p>
    <ul>
     <li>每个维护任务都伴有相关的运行状况检查</li>
     <li>如果任务未添加到维护窗口，其运行状况检查将返回“关键”</li>
     <li>您需要配置“审核日志”和“工作流清除”维护任务，或者以其他方式从维护窗口中删除它们。 如果未配置，这些任务在首次尝试运行时将失败，因此系统维护检查将返回“关键”状态。</li>
     <li><strong>在AEM 6.4中</strong>，还检查Lucene二进制文 <a href="/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks">件维护任务</a></li>
     <li>在AEM 6.2和更低版本上，系统维护检查会在启动后立即返回警告状态，因为任务从不运行。 从6.3开始，如果尚未到达第一个维护窗口，他们将返回“OK（正常）”。</li>
    </ul> <p>此运行状况检查的 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3Dsystemchecks%2Ctype%3DHealthCheck">MBean为org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>复制队列</td>
   <td><p>此检查重复复制代理并查看其队列。 对于队列顶部的项，检查代理重试复制的次数。 如果代理重试的复制次数超过参数 <code>numberOfRetriesAllowed</code> 的值，则返回警告。 该参 <code>numberOfRetriesAllowed</code> 数是可配置的。 </p> <p>此运行状况检查的 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DreplicationQueue%2Ctype%3DHealthCheck" target="_blank">MBean为org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>Sling 作业</td>
   <td>
    <div>
      Sling Jobs检查在JobManager中排队的作业数，将其与阈值 <code>maxNumQueueJobs</code> 比较，并：
    </div>
    <ul>
     <li>如果队列中的数量 <code>maxNumQueueJobs</code> 超过，则返回严重</li>
     <li>如果存在长时间运行的活动作业超过1小时，则返回关键</li>
     <li>如果存在排队的作业，并且上次完成的作业时间早于1小时，则返回关键</li>
    </ul> <p>只能配置排队作业参数的最大数量，其默认值为1000。</p> <p>此运行状况检查的 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DslingJobs%2Ctype%3DHealthCheck" target="_blank">MBean为org.apache.sling.healthcheck:name=slingJobs,type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>请求性能</td>
   <td><p>此检查将查看Sling <code>granite.request.metrics.timer</code> 指 <a href="http://localhost:4502/system/console/slingmetrics" target="_blank">标 </a>和：</p>
    <ul>
     <li>如果第75百分点值超过临界阈值（默认值为500毫秒），则返回临界值</li>
     <li>返回当第75百分点值超过警告阈值时发出警告（默认值为200毫秒）</li>
    </ul> <p>此运行状况检查的<em></em><a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DrequestsStatus%2Ctype%3DHealthCheck" target="_blank">MBean为org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>日志错误</td>
   <td><p>如果日志中存在错误，此检查将返回“警告”状态。</p> <p>此运行状况检查的 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DlogErrorHealthCheck%2Ctype%3DHealthCheck" target="_blank">MBean为org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>磁盘空间</td>
   <td><p>磁盘空间检查会查 <code>FileStoreStats</code> 看MBean，检索节点存储的大小和节点存储分区上的可用磁盘空间量，以及：</p>
    <ul>
     <li>如果可用磁盘空间与存储库大小比小于警告阈值（默认值为10），则返回警告</li>
     <li>如果可用磁盘空间与存储库大小比小于关键阈值（默认值为2），则返回关键值</li>
    </ul> <p>这两个阈值都可配置。 该检查仅适用于具有区段存储的实例。</p> <p>此运行状况检查 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DDiskSpaceHealthCheck%2Ctype%3DHealthCheck" target="_blank">的MBean为org.apache.sling.healthcheck:name=DiskSpaceHealthCheck,type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>计划程序运行状况检查</td>
   <td><p>如果实例的Quartz作业运行时间超过60秒，此检查将返回警告。 可配置可接受的持续时间阈值。</p> <p>此运行状况检查的 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DslingCommonsSchedulerHealthCheck%2Ctype%3DHealthCheck" target="_blank">MBean为org.apache.sling.healthcheck:name=slingCommonsSchedulerHealthCheck,type=HealthCheck</a><em>。</em></p> </td>
  </tr>
  <tr>
   <td>安全检查</td>
   <td><p>安全检查是一个组合，它聚合多个与安全相关的检查的结果。 这些单独的运行状况检查可解决与安全清单文档页上提供的安全清 <a href="/help/sites-administering/security-checklist.md">单不同的问题。</a> 该检查在实例启动时可用作安全烟雾测试。 </p> <p>此运行状况检查的 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3Dsecuritychecks%2Ctype%3DHealthCheck" target="_blank">MBean为org.apache.sling.healthcheck:name=</a><a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3Dsecuritychecks%2Ctype%3DHealthCheck" target="_blank"></a><a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3Dsecuritychecks%2Ctype%3DHealthCheck" target="_blank"></a><a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3Dsecuritychecks%2Ctype%3DHealthCheck" target="_blank">securitychecks,type=HealthCheck</a></p> </td>
  </tr>
  <tr>
   <td>活动包</td>
   <td><p>活动包检查所有包的状态，并：</p>
    <ul>
     <li>返回“警告”状态（如果任何包未激活）或(以延迟激活开始)</li>
     <li>它忽略忽略忽略列表中包的状态</li>
    </ul> <p>可以配置忽略列表参数。</p> <p>此运行状况检查的 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DinactiveBundles%2Ctype%3DHealthCheck" target="_blank">MBean为org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>代码缓存检查</td>
   <td><p>这是一个运行状况检查，它验证几个JVM条件，这些条件可以触发Java 7中存在的CodeCache错误：</p>
    <ul>
     <li>在启用代码缓存刷新的情况下，返回在Java 7上运行实例时发出警告</li>
     <li>返回警告，如果实例在Java 7上运行，且保留代码缓存大小小于最小阈值（默认值为90MB）</li>
    </ul> <p>阈值 <code>minimum.code.cache.size</code> 是可配置的。 有关该错误的详细信息，请 <a href="https://bugs.java.com/bugdatabase/view_bug.do?bug_id=8012547">查看</a><a href="https://bugs.java.com/bugdatabase/view_bug.do?bug_id=8012547"></a><a href="https://bugs.java.com/bugdatabase/view_bug.do?bug_id=8012547"></a><a href="https://bugs.java.com/bugdatabase/view_bug.do?bug_id=8012547"> 本页</a>。</p> <p>此运行状况检查的 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DcodeCacheHealthCheck%2Ctype%3DHealthCheck" target="_blank">MBean为org.apache.sling.healthcheck:name=codeCacheHealthCheck,type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>资源搜索路径错误</td>
   <td><p>检查路径中是否有任何资源， <code>/apps/foundation/components/primary</code> 并：</p>
    <ul>
     <li>返回警告：如果存在子节点 <code>/apps/foundation/components/primary</code></li>
    </ul> <p>此运行状况检查的 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DresourceSearchPathErrorHealthCheck%2Ctype%3DHealthCheck" target="_blank">MBean为org.apache.sling.healthcheck:name=resourceSearchPathErrorHealthCheck,type=HealthCheck</a>。</p> </td>
  </tr>
 </tbody>
</table>

## 使用Nagios进行监视 {#monitoring-with-nagios}

运行状况检查仪表板可以通过Granite JMX Mbeans与Nagios集成。 以下示例说明如何在运行AEM的服务器上添加一个检查，其中显示已使用的内存。

1. 在监视服务器上安装和安装Nagios。
1. 然后，安装Nagios Remote Plugin Executor(NRPE)。

   >[!NOTE]
   >
   >有关如何在系统上安装Nagios和NRPE的详细信息，请查阅Nagios [文档](https://library.nagios.com/library/products/nagioscore/manuals/)。

1. 为AEM服务器添加主机定义。 这可以通过Nagios XI Web界面使用配置管理器来完成：

   1. 打开浏览器并指向Nagios服务器。
   1. 按顶 **部菜** 单中的“配置”按钮。
   1. 在左窗格中，按“Advanced Configuration(高 **级配置)”下** 的“Core **Config Manager（核心配置管理器）**”。
   1. 按“监 **视** ”部分下 **的Hosts** 链接。
   1. 添加主机定义：

   ![chlimage_1-118](assets/chlimage_1-118.png)

   以下是主机配置文件的示例，如果您使用的是Nagios Core:

   ```xml
   define host {
      address 192.168.0.5
      max_check_attempts 3
      check_period 24x7
      check-command check-host-alive
      contacts admin
      notification_interval 60
      notification_period 24x7
   }
   ```

1. 在AEM服务器上安装Nagios和NRPE。
1. 在两台 [服务器上安装check_http](https://github.com/phrawzty/check_http_json) _json插件。
1. 在两台服务器上定义通用JSON检查命令：

   ```xml
   define command{
   
       command_name    check_http_json-int
   
       command_line    /usr/lib/nagios/plugins/check_http_json --user "$ARG1$" --pass "$ARG2$" -u 'https://$HOSTNAME$:$ARG3$/$ARG4$' -e '$ARG5$' -w '$ARG6$' -c '$ARG7$'
   
   }
   ```

1. 在AEM服务器上添加已用内存的服务：

   ```xml
   define service {
   
       use generic-service
   
       host_name my.remote.host
   
       service_description AEM Author Used Memory
   
       check_command  check_http_json-int!<cq-user>!<cq-password>!<cq-port>!system/sling/monitoring/mbeans/java/lang/Memory.infinity.json!{noname}.mbean:attributes.HeapMemoryUsage.mbean:attributes.used.mbean:value!<warn-threshold-in-bytes>!<critical-threshold-in-bytes>
   
       }
   ```

1. 检查您的Nagios仪表板以了解新创建的服务：

   ![chlimage_1-119](assets/chlimage_1-119.png)

## Diagnosis tools {#diagnosis-tools}

操作仪表板还提供对诊断工具的访问，这些工具可以帮助查找和排除来自运行状况检查仪表板的警告的根本原因，并为系统操作员提供重要的调试信息。

其最重要的功能包括：

* 日志消息分析器
* 能够访问堆和线程转储
* 请求和查询性能分析器

您可以从AEM欢迎屏幕转到工具- **操作——诊断，来进入** “诊断工具”屏幕。 您还可以通过直接访问以下URL来访问屏幕： `https://serveraddress:port/libs/granite/operations/content/diagnosis.html`

![chlimage_1-120](assets/chlimage_1-120.png)

### 日志消息 {#log-messages}

默认情况下，日志消息用户界面将显示所有ERROR消息。 如果要显示更多日志消息，您需要配置具有相应日志级别的记录器。

日志消息使用内存日志附加器，因此与日志文件无关。 另一个结果是更改此UI中的日志级别不会更改传统日志文件中记录的信息。 在此UI中添加和删除记录程序只会影响内存记录程序。 另外，请注意，更改记录器配置将反映在内存记录器的将来——已记录且不再相关的条目不会被删除，但类似条目将来不会记录。

您可以通过在UI中从左上角的齿轮按钮提供记录器配置来配置记录内容。 您可以在此添加、删除或更新记录器配置。 记录器配置由日志级 **别** (WARN / INFO / DEBUG)和过滤器 **名称组成**。 筛 **选器名** 称具有筛选日志消息源的角色。 或者，如果记录器应捕获指定级别的所有日志消息，则过滤器名称应为“**root**”。 设置记录器的级别将触发所有消息的捕获，其级别等于或高于指定的级别。

示例：

* 如果您计划捕获所有 **ERROR** 消息——无需配置。 默认情况下，会捕获所有ERROR消息。
* 如果您计划捕获所 **有ERROR**、 **WARN****和** INFO消息——记录器名称应设置为： “**root**”和记录器级别： **信息**。

* 如果您计划捕获来自特定包的所有消息（例如com.adobe.granite）-记录器名称应设置为： “com.adobe.granite”和记录器级别： **调试** (这将捕获所 **有ERROR**、WARN **、** INFO **和DEBUG消息****** )，如下图所示。

![chlimage_1-121](assets/chlimage_1-121.png)

>[!NOTE]
>
>无法设置记录器名称以通过指定的过滤器仅捕获ERROR消息。 默认情况下，会捕获所有ERROR消息。

>[!NOTE]
>
>日志消息用户界面不反映实际错误日志。 除非您在UI中配置其他类型的日志消息，否则将只显示错误消息。 有关如何显示特定日志消息，请参阅上面的说明。

>[!NOTE]
>
>诊断页面中的设置不会影响记录到日志文件的内容，反之亦然。 因此，尽管错误日志可能会捕获INFO消息，但您可能在日志消息UI中看不到这些消息。 此外，通过UI，可以从某些包中捕获DEBUG消息，而不会影响错误日志。 有关如何配置日志文件的详细信息，请参 [阅日志](/help/sites-deploying/configure-logging.md)。

>[!NOTE]
>
>**在AEM 6.4中**，维护任务在INFO级别以更多信息丰富格式注销。 这允许更好地了解维护任务的状态。
>
>如果您使用第三方工具（如Splunk）来监视和维护任务活动并做出响应，则可以使用以下日志语句：

```
Log level: INFO
DATE+TIME [MaintanceLogger] Name=<MT_NAME>, Status=<MT_STATUS>, Time=<MT_TIME>, Error=<MT_ERROR>, Details=<MT_DETAILS>
```

### 请求性能 {#request-performance}

“请求性能”页允许分析处理的最慢页面请求。 此页面上仅注册内容请求。 具体而言，将捕获以下请求：

1. 访问资源的请求 `/content`
1. 访问资源的请求 `/etc/design`
1. 具有扩展的请 `".html"` 求

![chlimage_1-122](assets/chlimage_1-122.png)

此时将显示页面：

* 发出请求的时间
* URL和请求方法
* 持续时间（以毫秒为单位）

默认情况下，会捕获最慢的20个页面请求，但可以在配置管理器中修改此限制。

### 查询性能 {#query-performance}

“查询性能”页允许分析系统执行的最慢查询。 此信息由JMX Bean中的存储库提供。 在Jackrabbit中， `com.adobe.granite.QueryStat` JMX Mbean提供此信息，而在Oak存储库中，它由 `org.apache.jackrabbit.oak.QueryStats.`

此时将显示页面：

* 制作查询的时间
* 查询语
* 发布查询的次数
* 查询声明
* 持续时间（以毫秒为单位）

![chlimage_1-123](assets/chlimage_1-123.png)

### 说明查询 {#explain-query}

对于任何给定查询,Oak都会尝试根据存储库中oak:index节点下定义的Oak索引找到最 **佳执行方** 法。 根据查询,Oak可以选择不同的索引。 了解Oak如何执行查询是优化查询的第一步。

Explain查询是一个工具，用于说明Oak如何执行查询。 可以从AEM欢迎屏幕转 **到工具——操作** -诊断，然后单击 **查询性能** ，并切换到解 **释查询选项卡** 。

**功能**

* 支持Xpath、JCR-SQL和JCR-SQL2查询语言
* 报告提供查询的实际执行时间
* 检测速度较慢的查询并警告可能速度较慢的查询
* 报告用于执行查询的Oak索引
* 显示实际Oak查询引擎说明
* 提供慢速和流行查询的点击加载列表

进入“解释查询UI”后，只需输入查询并按“解释”按钮即可 **使用** :

![chlimage_1-124](assets/chlimage_1-124.png)

“查询说明”部分中的第一个条目是实际说明。 说明将显示用于执行查询的索引类型。

第二项是执行计划。

在运行 **查询之前** ，勾选“包括执行时间”框还将显示查询的执行时间，以便获得更多可用于优化应用程序或部署索引的信息。

![chlimage_1-125](assets/chlimage_1-125.png)

### 索引管理器 {#the-index-manager}

索引管理器的目的是便于索引管理，如维护索引或查看其状态。

可以从欢迎屏幕转到**工具——操作——诊断**，然后单击索引管理器按 **钮访问** 。

也可以通过以下URL直接访问它： `https://serveraddress:port/libs/granite/operations/content/diagnosistools/indexManager.html`

![screen-shot_2019-06-18at154754](assets/screen-shot_2019-06-18at154754.png)

UI可用于通过在屏幕左上角的搜索框中键入筛选条件来筛选表中的索引。

### 下载状态ZIP {#download-status-zip}

这将触发下载包含有关系统状态和配置的有用信息的zip文件。 该归档文件包含实例配置、捆绑包列表、OSGI、Sling指标和统计信息，这可能会生成大文件。 您可以使用“下载状态ZIP”窗口来减少大型状 **态文件的**&#x200B;影响。 窗口可从以下位置访问：**AEM >工具>操作>诊断>下载状态ZIP。**

在此窗口中，您可以选择要导出的内容（日志文件和线程转储）以及下载中包含的相对于当前日期的日志天数。

![download_status_zip](assets/download_status_zip.png)

### 下载线程转储 {#download-thread-dump}

这将触发下载包含系统中线程相关信息的zip文件。 提供了有关每个线程的信息，如其状态、类加载器和堆栈跟踪。

### 下载堆转储 {#download-heap-dump}

您还可以下载堆的快照，以便稍后分析它。 请注意，这将触发以数百兆字节的顺序下载大型文件。

## 自动维护任务 {#automated-maintenance-tasks}

“自动维护任务”页是一个位置，您可以在该页视图和跟踪计划定期执行的推荐维护任务。 任务与运行状况检查系统集成。 任务也可以从界面手动执行。

要转到“操作”仪表板的“维护”页，您需要从AEM欢迎屏幕转 **到“工具”-“操作”-“仪表板”** -“维护”，或直接转到以下链接：

`https://serveraddress:port/libs/granite/operations/content/maintenance.html`

以下任务在“操作”仪表板中可用：

1. “Revision **Clean Uptask(修**&#x200B;订清理升级任务)”位于“Daily Maintenance Window(每 **日维护窗口)** ”菜单下。
1. Lucene **Binaries Cleanup** 任务，位于Daily Maintenance Window **（每日维护窗口）菜单** 下。
1. 工作 **流清除任务** ，位于“每周维护 **窗口”菜单下** 。
1. “数 **据存储垃圾收集** ”任务，位于“每周 **维护窗口”菜单** 。
1. “Audit **Log Maintenance** (审核日志维护 **)”任务，位于“Weekly Maintenance(每周** 维护)窗口”菜单下。
1. “ **Version Purge Maintenance** (版本清除维护 **)”任务，位于“Weekly Maintenance Window(每** 周维护窗口)”菜单下。

每日维护窗口的默认时间是凌晨2点到5点。 配置为在每周维护窗口中运行的任务将在星期六的上午1点到2点之间执行。

您还可以通过按任意两个维护卡上的齿轮图标来配置时间：

![chlimage_1-126](assets/chlimage_1-126.png)

>[!NOTE]
>
>自AEM 6.1起，还可以将现有维护窗口配置为每月运行一次。

### 修订清理 {#revision-clean-up}

有关执行修订清理的详细信息，请 [参阅此专用文章](/help/sites-deploying/revision-cleanup.md)。

### Lucene 二进制文件清理 {#lucene-binaries-cleanup}

通过使用Lucene二进制清除任务，可以清除lucene二进制文件并减少正在运行的数据存储大小要求。 这是因为lucene的二进制服务器服务器服务器将每天重新申请，而不是以前对成功运行数据存储 [垃圾收集的依赖](/help/sites-administering/data-store-garbage-collection.md) 。

虽然开发维护任务是为了减少与Lucene相关的修改垃圾，但运行任务时总体效率有所提高：

* 每周执行数据存储垃圾收集任务将更快完成
* 它还可以略微提高AEM的整体性能

您可以从以下位置访问Lucene二进制文件清除任务: **AEM >工具>操作>维护>每日维护窗口> Lucene二进制文件清理**。

### 数据存储垃圾收集 {#data-store-garbage-collection}

有关数据存储垃圾收集的详细信息，请参阅专用 [文档页](/help/sites-administering/data-store-garbage-collection.md)。

### Workflow purge {#workflow-purge}

工作流也可以从维护仪表板中清除。 要运行“工作流清除”任务，您需要：

1. 单击“每周 **维护窗口** ”页。
1. 在下一页中，单击“工 **作流** ”清除卡 **中的“播放** ”按钮。

>[!NOTE]
>
> 有关工作流维护的详细信息，请参 [阅此页](/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances)。

### 审核日志维护 {#audit-log-maintenance}

有关审核日志维护，请参阅单 [独的文档页面。](/help/sites-administering/operations-audit-log.md)

### 版本清除 {#version-purge}

您可以计划“版本清除”维护任务，以自动删除旧版本。 因此，这会最大限度地减少手动使用版本清 [除工具的需求](/help/sites-deploying/version-purging.md)。 您可以通过访问“工具”>“操作”>“维护”>“每周维 **护窗口”并执行以下步骤来计划和配置“版本清除** ”任务，具体方法如下：

1. 单击“添 **加** ”按钮。
1. 从 **下拉菜单** 中选择版本清除。

   ![version_purge_maintenancetask](assets/version_purge_maintenancetask.png)

1. 要配置“版本清除”任务，请单击新 **创建** “版本清除”维护卡上的齿轮图标。

   ![version_purge_taskconfiguration](assets/version_purge_taskconfiguration.png)

**在AEM 6.4中**，您可以按如下方式停止版本清除维护任务:

* 自动——如果计划的维护窗口在任务完成之前关闭，任务会自动停止。 下次维护窗口打开时，它将恢复。
* 手动——要手动停止任务，请在“版本清除”维护卡上单击“停 **止** ”图标。 下次执行时，任务将安全恢复。

>[!NOTE]
>
>停止维护任务意味着暂停其执行，而不丢失对已进行作业的跟踪。

>[!CAUTION]
>
>要优化存储库大小，您应经常运行版本清除任务。 任务应在业务时间以外安排，当流量有限时。

## 自定义维护任务 {#custom-maintenance-tasks}

自定义维护任务可以作为OSGi服务实现。 由于维护任务基础结构基于Apache Sling的作业处理，因此维护任务必须实现java接口 ` [org.apache.sling.event.jobs.consumer.JobExecutor](https://sling.apache.org/apidocs/sling7/org/apache/sling/event/jobs/consumer/JobExecutor.html)`。 此外，它必须声明若干服务注册属性作为维护任务进行检测，如下所示：

<table>
 <tbody>
  <tr>
   <td><strong>服务属性名称</strong><br /> </td>
   <td><strong>描述</strong></td>
   <td><strong>示例</strong><br /> </td>
   <td><strong>类型</strong></td>
  </tr>
  <tr>
   <td>granite.maintenance.isStoppable</td>
   <td>布尔属性，用于定义用户是否可以停止任务。 如果任务声明其可停止，则必须在执行过程中检查其是否已停止，然后相应地执行。 默认值为false。</td>
   <td>true</td>
   <td>可选</td>
  </tr>
  <tr>
   <td>granite.maintenance.mandatory</td>
   <td>布尔属性，用于定义任务是否为必填项并且必须定期运行。 如果任务是强制计划，但当前不在任何活动的窗口中，运行状况检查会将此报告为错误。 默认值为false。</td>
   <td>true</td>
   <td>可选</td>
  </tr>
  <tr>
   <td>granite.maintenance.name</td>
   <td>任务的唯一名称——此名称用于引用任务。 这通常是一个简单的名称。</td>
   <td>MyMaintenanceTask</td>
   <td>必填</td>
  </tr>
  <tr>
   <td>granite.maintenance.title</td>
   <td>此任务显示的标题</td>
   <td>我的特殊维护任务</td>
   <td>必填</td>
  </tr>
  <tr>
   <td>job.topics</td>
   <td>这是维护任务的一个独特主题。<br /> Apache Sling作业处理将完全开始具有此主题的作业以执行维护任务，并在为此主题注册任务时执行该主题。<br /> 主题必须与 <i>com/adobe/granite/maintenance/job/开始</i></td>
   <td>com/adobe/granite/maintenance/job/MyMaintenanceTask</td>
   <td>必填</td>
  </tr>
 </tbody>
</table>

除了上述服务属性外， `process()` 还需要 `JobConsumer` 通过添加应为维护任务执行的代码来实现接口的方法。 提供的 `JobExecutionContext` 状态信息可用于输出状态信息，检查用户是否停止了作业并创建结果（成功或失败）。

如果维护任务不应在所有安装上运行（例如，仅在发布实例上运行），则可以通过添加使服务需要配置才能处于活动状态 `@Component(policy=ConfigurationPolicy.REQUIRE)`。 然后，您可以根据配置将其标记为运行模式（取决于存储库中的模式）。 有关详细信息，请参 [阅配置OSGi](/help/sites-deploying/configuring-osgi.md#creating-the-configuration-in-the-repository)。

下面是一个自定义维护任务的示例，该自定义维护操作从可配置的临时目录中删除文件，这些临时目录在过去24小时内已被修改：

src/main/java/com/adobe/granite/samples/maintenance/impl/DeleteTempFilesTask.java

<table>
 <tbody>
  <tr>
   <td><p> </p> <p><code>/*</code></p> <p><code> * #%L</code></p> <p><code> * sample-maintenance-task</code></p> <p><code> * %%</code></p> <p><code> * Copyright (C) 2014 Adobe</code></p> <p><code> * %%</code></p> <p><code> * Licensed under the Apache License, Version 2.0 (the "License");</code></p> <p><code> * you may not use this file except in compliance with the License.</code></p> <p><code> * You may obtain a copy of the License at</code></p> <p><code> * </code></p> <p><code> * <a href="https://www.apache.org/licenses/LICENSE-2.0">https://www.apache.org/licenses/LICENSE-2.0</a></code></p> <p><code> * </code></p> <p><code> * Unless required by applicable law or agreed to in writing, software</code></p> <p><code> * distributed under the License is distributed on an "AS IS" BASIS,</code></p> <p><code> * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.</code></p> <p><code> * See the License for the specific language governing permissions and</code></p> <p><code> * limitations under the License.</code></p> <p><code> * #L%</code></p> <p><code> */</code></p> <p><code> </code></p> <p><code>package com.adobe.granite.samples.maintenance.impl;</code></p> <p><code> </code></p> <p><code>import java.io.File;</code></p> <p><code>import java.util.Calendar;</code></p> <p><code>import java.util.Collection;</code></p> <p><code>import java.util.Map;</code></p> <p><code> </code></p> <p><code>import org.apache.commons.io.FileUtils;</code></p> <p><code>import org.apache.commons.io.filefilter.IOFileFilter;</code></p> <p><code>import org.apache.commons.io.filefilter.TrueFileFilter;</code></p> <p><code>import org.apache.felix.scr.annotations.Activate;</code></p> <p><code>import org.apache.felix.scr.annotations.Component;</code></p> <p><code>import org.apache.felix.scr.annotations.Properties;</code></p> <p><code>import org.apache.felix.scr.annotations.Property;</code></p> <p><code>import org.apache.felix.scr.annotations.Service;</code></p> <p><code>import org.apache.sling.commons.osgi.PropertiesUtil;</code></p> <p><code>import org.apache.sling.event.jobs.Job;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobConsumer;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobExecutionContext;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobExecutionResult;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobExecutor;</code></p> <p><code>import org.slf4j.Logger;</code></p> <p><code>import org.slf4j.LoggerFactory;</code></p> <p><code> </code></p> <p><code>import com.adobe.granite.maintenance.MaintenanceConstants;</code></p> <p><code> </code></p> <p><code>@Component(metatype = true,</code></p> <p><code> label = "Delete Temp Files Maintenance Task",</code></p> <p><code> description = "Maintatence Task which deletes files from a configurable temporary directory which have been modified in the last 24 hours.")</code></p> <p><code>@Service</code></p> <p><code>@Properties({</code></p> <p><code> @Property(name = MaintenanceConstants.PROPERTY_TASK_NAME, value = "DeleteTempFilesTask", propertyPrivate = true),</code></p> <p><code> @Property(name = MaintenanceConstants.PROPERTY_TASK_TITLE, value = "Delete Temp Files", propertyPrivate = true),</code></p> <p><code> @Property(name = JobConsumer.PROPERTY_TOPICS, value = MaintenanceConstants.TASK_TOPIC_PREFIX</code></p> <p><code> + "DeleteTempFilesTask", propertyPrivate = true) })</code></p> <p><code>public class DeleteTempFilesTask implements JobExecutor {</code></p> <p><code> </code></p> <p><code> private static final Logger log = LoggerFactory.getLogger(DeleteTempFilesTask.class);</code></p> <p><code> </code></p> <p><code> @Property(label = "Temporary Directory", description="Temporary Directory. Defaults to the java.io.tmpdir system property.")</code></p> <p><code> private static final String PROP_TEMP_DIR = "temp.dir";</code></p> <p><code> </code></p> <p><code> private File tempDir;</code></p> <p><code> </code></p> <p><code> @Activate</code></p> <p><code> private void activate(Map&lt;string, object=""&gt; properties) {</code></p> <p><code> this.tempDir = new File(PropertiesUtil.toString(properties.get(PROP_TEMP_DIR),</code></p> <p><code> System.getProperty("java.io.tmpdir")));</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> @Override</code></p> <p><code> public JobExecutionResult process(Job job, JobExecutionContext context) {</code></p> <p><code> log.info("Deleting old temp files from {}.", tempDir.getAbsolutePath());</code></p> <p><code> Collection&lt;file&gt; files = FileUtils.listFiles(tempDir, new LastModifiedBeforeYesterdayFilter(),</code></p> <p><code> TrueFileFilter.INSTANCE);</code></p> <p><code> int counter = 0;</code></p> <p><code> for (File file : files) {</code></p> <p><code> log.debug("Deleting file {}.", file.getAbsolutePath());</code></p> <p><code> counter++;</code></p> <p><code> file.delete();</code></p> <p><code> // TODO - capture the output of delete() and do something useful with it</code></p> <p><code> }</code></p> <p><code> return context.result().message(String.format("Deleted %s files.", counter)).succeeded();</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> /**</code></p> <p><code> * IOFileFilter which filters out files which have been modified in the last 24 hours.</code></p> <p><code> *</code></p> <p><code> */</code></p> <p><code> private static class LastModifiedBeforeYesterdayFilter implements IOFileFilter {</code></p> <p><code> </code></p> <p><code> private final long minTime;</code></p> <p><code> </code></p> <p><code> private LastModifiedBeforeYesterdayFilter() {</code></p> <p><code> Calendar cal = Calendar.getInstance();</code></p> <p><code> cal.add(Calendar.DATE, -1);</code></p> <p><code> this.minTime = cal.getTimeInMillis();</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> @Override</code></p> <p><code> public boolean accept(File dir, String name) {</code></p> <p><code> // this method is never actually called.</code></p> <p><code> return false;</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> @Override</code></p> <p><code> public boolean accept(File file) {</code></p> <p><code> return file.lastModified() <= this.minTime;</code></p> <p><code> }</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code>}</code></p> <p><code>&lt;file&gt;&lt;/string,&gt;</code></p> <p> </p> </td>
  </tr>
 </tbody>
</table>

[experiencemanager-java-maintenancetask-sample](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-maintenancetask-sample)- [src/main/java/com/adobe/granite/samples/maintenance/impl/DeleteTempFilesTask.java](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-maintenancetask-sample/blob/master/src/main/java/com/adobe/granite/samples/maintenance/impl/DeleteTempFilesTask.java)

部署服务后，它将暴露在“操作”仪表板UI中。 您可以将其添加到可用的维护计划之一：

![chlimage_1-127](assets/chlimage_1-127.png)

这将在/apps/granite/operations/config/maintenance/`schedule`//添加相应资源`taskname`。 如果任务依赖于运行模式，则需要在该节点上设置granite.operations.conditions.runmode属性，其值必须为此维护任务的活动运行模式。

## 系统概览 {#system-overview}

“ **系统概述** ”仪表板显示AEM实例的配置、硬件和运行状况的高级概述。 这意味着系统运行状况是透明的，所有信息都会聚集到一个仪表板中。

>[!NOTE]
>
>您还可以观 [看此视频](https://video.tv.adobe.com/v/21340?captions=chi_hans) ，了解“系统概述”仪表板。

### 如何访问 {#how-to-access}

要访问“系统概述”仪表板，请导航到 **工具>操作>系统概述**。

![system_overview_仪表板](assets/system_overview_dashboard.png)

### 系统概述仪表板说明 {#system-overview-dashboard-explained}

下表描述了“系统概述”仪表板中显示的所有信息。 请记住，当没有要显示的相关信息（例如，备份尚未进行，没有关键的运行状况检查）时，相应的部分将显示“无条目”消息。

您还可以通过单 `JSON` 击仪表板右上角的“ **下载** ”按钮来下载汇总仪表板信息的文件。端点是 `JSON``/libs/granite/operations/content/systemoverview/export.json` ，可用于外部监 `curl` 视的脚本中。

<table>
 <tbody>
  <tr>
   <td><strong>区域</strong></td>
   <td><strong>显示哪些信息</strong></td>
   <td><strong>什么时候关键</strong></td>
   <td><strong>链接到</strong></td>
  </tr>
  <tr>
   <td>运行状况检查</td>
   <td>
    <ul>
     <li>处于“关键”状态的列表检查</li>
     <li>处于“警告”状态的列表检查</li>
    </ul> </td>
   <td>可视指示：<br />
    <ul>
     <li>关键检查的红色标签</li>
     <li>警告检查的橙色标签</li>
    </ul> </td>
   <td>
    <ul>
     <li>运行状况报告页面</li>
    </ul> </td>
  </tr>
  <tr>
   <td>维护任务</td>
   <td>
    <ul>
     <li>一列表失败的任务</li>
     <li>列表当前运行的任务</li>
     <li>一列表任务在上一轮选举中成功</li>
     <li>一列表任务从未跑过</li>
     <li>未计划的列表任务</li>
    </ul> </td>
   <td><p>可视指示：</p>
    <ul>
     <li>失败任务的红色标记</li>
     <li>用于运行任务的橙色标签（因为它们可能影响性能）</li>
     <li>其他状态均为灰色标记</li>
    </ul> </td>
   <td>
    <ul>
     <li>维护任务页</li>
    </ul> </td>
  </tr>
  <tr>
   <td>系统</td>
   <td>
    <ul>
     <li>操作系统和操作系统版本（例如，Mac OS X）</li>
     <li>系统负载平均值，从OperatingSystemMXBeanusable中检 <a href="https://docs.oracle.com/javase/8/docs/api/java/lang/management/OperatingSystemMXBean.html#getSystemLoadAverage--">索</a></li>
     <li>磁盘空间（在主目录所在的分区上）</li>
     <li>最大堆，由MemoryMXBean返 <a href="https://docs.oracle.com/javase/8/docs/api/java/lang/management/MemoryMXBean.html#getHeapMemoryUsage--">回</a></li>
    </ul> </td>
   <td>不适用</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>实例</td>
   <td>
    <ul>
     <li>AEM版本</li>
     <li>列表运行模式</li>
     <li>实例开始的日期</li>
    </ul> </td>
   <td>不适用</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>存储库</td>
   <td>
    <ul>
     <li>Oak版</li>
     <li>节点存储类型(段Tar或文档)
      <ul>
       <li>如果类型是文档，则显示文档存储的类型（RDB或Mongo）</li>
      </ul> </li>
     <li>如果存在自定义数据存储：
      <ul>
       <li>对于文件数据存储，将显示路径</li>
       <li>对于S3数据存储，将显示S3存储段的名称</li>
       <li>对于共享的S3数据存储，将显示S3存储段的名称</li>
       <li>对于Azure数据存储，将显示容器</li>
      </ul> </li>
     <li>如果没有自定义外部数据存储，则显示一条消息，指明此情况</li>
    </ul> </td>
   <td>不适用</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>分发代理</td>
   <td>
    <ul>
     <li>列表队列被阻止的代理</li>
     <li>列表配置错误的代理（“配置错误”）</li>
     <li>队列处理暂停的代理列表</li>
     <li>一列表闲置代理</li>
     <li>运行代理的列表（当前正在处理条目）</li>
    </ul> </td>
   <td><p>可视指示：</p>
    <ul>
     <li>被阻止的代理或配置错误的红色标记</li>
     <li>暂停的代理的橙色标签</li>
     <li>暂停、空闲或正在运行的代理的灰色标记<br /> </li>
    </ul> </td>
   <td>分发页<br /> </td>
  </tr>
  <tr>
   <td>复制代理</td>
   <td>
    <ul>
     <li>列表队列被阻止的代理</li>
     <li>一列表闲置代理</li>
     <li>运行代理的列表（当前正在处理条目）</li>
    </ul> </td>
   <td><p>可视指示：<br /> </p>
    <ul>
     <li>被阻止的代理的红色标签</li>
     <li>暂停代理的灰色标记</li>
    </ul> </td>
   <td>复制页</td>
  </tr>
  <tr>
   <td>工作流</td>
   <td>
    <ul>
     <li>工作流作业：
      <ul>
       <li>失败的工作流作业数（如果有）</li>
       <li>已取消的工作流作业数（如果有）</li>
      </ul> </li>
    </ul>
    <ul>
     <li>工作流计数——处于给定状态的工作流数（如果有）:
      <ul>
       <li>运行</li>
       <li>失败</li>
       <li>暂停</li>
       <li>中止</li>
      </ul> </li>
    </ul> <p>对于以上显示的每种状态，将执行查询，限制为400毫秒。 在400毫秒时，将显示截至该点获取的条目数。</p> </td>
   <td><p>未解释：</p>
    <ul>
     <li>用户应调查是否存在意外状态的工作流和作业。</li>
    </ul> </td>
   <td>“工作流失败”页</td>
  </tr>
  <tr>
   <td>Sling 作业</td>
   <td><p>Sling作业计数——处于给定状态的作业数（如果有）:</p>
    <ul>
     <li>失败</li>
     <li>排队</li>
     <li>已取消</li>
     <li>活动</li>
    </ul> </td>
   <td><p>未解释：</p>
    <ul>
     <li>用户应调查哪些作业处于意外状态或计数较高。</li>
    </ul> </td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>预计节点计数</td>
   <td><p>估计数量：</p>
    <ul>
     <li>页</li>
     <li>资产</li>
     <li>标记</li>
     <li>可创作</li>
     <li>节点总数<br /> </li>
    </ul> <p>节点总数从nodeCounterMBean获取，其余统计信息则从IndexInfoService获取。</p> </td>
   <td>不适用</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>备份</td>
   <td>如果出现这种情况，则显示“正在进行联机备份”。</td>
   <td>不适用</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>索引</td>
   <td><p>显示:</p>
    <ul>
     <li>"正在进行索引"</li>
     <li>"正在进行查询"</li>
    </ul> <p>如果在线程转储中存在索引或查询线程。</p> </td>
   <td>不适用</td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

