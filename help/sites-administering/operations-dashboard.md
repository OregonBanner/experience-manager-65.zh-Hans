---
title: 操作控制板
seo-title: 操作控制板
description: 了解如何使用Operations Dashboard。
seo-description: 了解如何使用Operations Dashboard。
uuid: ef24813f-a7a8-4b26-a496-6f2a0d9efef6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: b210f5d7-1d68-49ee-ade7-667c6ab11d2b
docset: aem65
translation-type: tm+mt
source-git-commit: 3dd3f700cd473570889f8d4ced09281a577e2ef8

---


# 操作控制板 {#operations-dashboard}

## 简介 {#introduction}

AEM 6中的操作控制板可帮助系统操作员一览监控AEM系统运行状况。 它还提供有关AEM相关方面的自动生成的诊断信息，并允许配置和运行自包含的维护自动化，从而显着减少项目操作和支持案例。 操作控制板可以扩展，并包含自定义运行状况检查和维护任务。 此外，操作控制板数据可通过JMX从外部监视工具访问。

**操作控制板：**

* 是一键式系统状态，可帮助运营部门提高效率
* 在一个集中的位置提供系统运行状况概述
* 缩短查找、分析和修复问题的时间
* 提供自带维护自动化功能，有助于显着降低项目运营成本

可以通过从AEM欢迎屏幕转 **到工具** - **操作** ，来访问它。

>[!NOTE]
>
>要能够访问操作控制板，登录用户必须是“操作员”用户组的一部分。 有关详细信息，请参阅有关用户、 [组和访问权限管理的文档](/help/sites-administering/user-group-ac-admin.md)。

## 健康报表 {#health-reports}

运行状况报告系统通过Sling Health Checks提供AEM实例运行状况的相关信息。 这可以通过OSGI、JMX、HTTP请求（通过JSON）或通过触控UI来完成。 它提供某些可配置计数器的度量值和阈值，在某些情况下，将提供有关如何解决该问题的信息。

它具有以下几个功能。

## 运行状况检查 {#health-checks}

健康 **状况报告** (Health Reports)是一种卡系统，用于指示特定产品区域的健康状况是否良好。 这些卡是Sling Health Checks的可视化功能，它可以从JMX和其他源收集数据，并再次以MBean的身份显示处理过的信息。 这些MBean还可以在 [JMX web控制台中](/help/sites-administering/jmx-console.md)，在 **org.apache.sling.healthcheck域下进行检查** 。

可以通过AEM欢迎屏幕上的“工具 **** -操作 **-运行状** 况报告 **** ”菜单，或直接通过以下URL访问健康报告界面：

`https://<serveraddress>:port/libs/granite/operations/content/healthreports/healthreportlist.html`

![chlimage_1-116](assets/chlimage_1-116.png)

卡系统显示三种可能的状态：确 **定**, **警告** , **严重**。 这些状态是规则和阈值的结果，可以通过将鼠标悬停在卡上并单击操作栏中的齿轮图标来配置规则和阈值：

![chlimage_1-117](assets/chlimage_1-117.png)

### 运行状况检查类型 {#health-check-types}

AEM 6中有两种类型的运行状况检查：

1. 个人运行状况检查
1. 综合运行状况检查

单 **个运行状况检查** (Individual Health Check)是与状态卡对应的单个运行状况检查。 单个运行状况检查可以配置规则或阈值，并且它们可以提供一个或多个提示和链接以解决已识别的健康问题。 让我们以“日志错误”检查为例：如果实例日志中有ERROR条目，您将在运行状况检查的详细信息页面上找到它们。 在页面顶部，您将在“诊断工具”部分看到指向“日志消息”分析器的链接，该链接使您能够更详细地分析这些错误并重新配置记录器。

综合 **运行状况检查** (Composite Health Check)是一种检查，可从多个单独的检查中收集信息。

复合健康检查是利用过滤器标签 **配置的**。 本质上，具有相同过滤器标签的所有单个检查都将被分组为复合运行状况检查。 仅当综合运行状况检查所有单个检查也都具有“确定”状态时，其状态才为“确定”。

### 如何创建运行状况检查 {#how-to-create-health-checks}

在“操作控制板”中，您可以可视化单个和复合运行状况检查的结果。

### 创建单个运行状况检查 {#creating-an-individual-health-check}

创建单个运行状况检查涉及两个步骤：实施Sling Health check并在控制面板的配置节点中为运行状况检查添加一个条目。

1. 要创建Sling Health Check，您需要创建一个实施Sling healthCheck界面的OSGI组件。 您将此组件添加到捆绑中。 组件的属性将完全标识运行状况检查。 安装该组件后，将自动为运行状况检查创建JMX MBean。 有关详细 [信息，请参阅Sling Health Check文档](https://sling.apache.org/documentation/bundles/sling-health-check-tool.html) 。

   使用OSGI服务组件注释编写的Sling Health check组件示例：

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

1. 创建运行状况检查后，需要创建新的配置节点，以便在“操作控制板”界面中访问该节点。 对于此步骤，必须知道运行状况检查的JMX Mbean名称(属 `MBEAN_NAME` 性)。 要为运行状况检查创建配置，请打开CRXDE，并在以下路径下添加新节点( **nt:unstructured**): `/apps/settings/granite/operations/hc`

   应在新节点上设置以下属性：

   * **名称:** `sling:resourceType`

      * **类型:** `String`
      * **** 值： `granite/operations/components/mbean`
   * **名称:** `resource`

      * **类型:** `String`
      * **** 值： `/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck/exampleHealthCheck`
   >[!NOTE]
   >
   >上面的资源路径如下所示：如果运行状况检查的mbean名称为“test”，则在路径末尾添加“test” `/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck`
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

Composite Health Check的角色是汇总多个共享一组常见功能的独立Health Check。 例如，“安全复合运行状况检查”组将执行安全相关验证的所有单个运行状况检查一起进行。 创建复合检查的第一步是添加新的OSGI配置。 要使其显示在操作控制板中，需要添加新的配置节点，这与简单检查的方式相同。

1. 转到OSGI控制台中的Web配置管理器。 您可以通过访问 `https://serveraddress:port/system/console/configMgr`
1. 搜索名为 **Apache Sling Composite Health Check的条目**。 找到它后，请注意已有两种配置可用：一个用于系统检查，另一个用于安全检查。
1. 通过按配置右侧的“+”按钮创建新配置。 将显示一个新窗口，如下所示：

   ![chlimage_1-23](assets/chlimage_1-23.jpeg)

1. 创建配置并保存。 将使用新配置创建Mbean。

   每个配置属性的用途如下：

   * **** 名称(hc.name):复合运行状况检查的名称。 建议使用有意义的名称。
   * **** 标记(hc.tags):此运行状况检查的标记。 如果此复合健康检查旨在作为另一个复合健康检查的一部分（如在健康检查的层次结构中），请添加此复合所关联的标记。
   * **** MBean名称(hc.mbean.name):将提供给此复合运行状况检查的JMX MBean的Mbean的名称。
   * **** 筛选标记(filter.tags):这是特定于复合运行状况检查的属性。 这些是合成应聚合的标记。 复合健康检查将聚合到其组下所有具有与此复合的任何过滤器标签匹配的任何标签的健康检查。 例如，具有过滤器 **test** and **check的复合健康检查将汇总所有具有其标签属性(** test and check)中的任何test **and******`hc.tags`checkTags的个人健康检查和复合健康检查。
   >[!NOTE]
   >
   >为Apache Sling Composite Health Check的每个新配置创建了一个新的JMX Mbean。**

1. 最后，刚刚创建的复合运行状况检查条目需要添加到“操作控制板”配置节点中。 此过程与单个运行状况检查的过程相同：需要在下 **创建nt:unstructured** 类型的节点 `/apps/settings/granite/operations/hc`。 节点的资源属性将由OSGI配置中 **hc.mean.name的值定义** 。

   例如，如果您创建了配置并将 **hc.mbean.name** 值设置为 **diskusage**，则配置节点将如下：

   * **名称:** `Composite Health Check`

      * **类型:** `nt:unstructured`
   使用以下属性：

   * **名称:** `sling:resourceType`

      * **类型:** `String`
      * **** 值： `granite/operations/components/mbean`
   * **名称:** `resource`

      * **类型:** `String`
      * **** 值： `/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck/diskusage`
   >[!NOTE]
   >
   >如果您创建逻辑上属于复合检查的单个运行状况检查（默认情况下，该复合检查已在控制面板中显示），它们将自动捕获并分组在相应的复合检查下。 因此，无需为这些检查创建新的配置节点。
   >
   >例如，如果您创建单个安全性运行状况检查，您只需将其分配为“**security**”标记，并且它已安装，它将自动显示在“操作控制板”的“安全性检查”复合检查下。

### AEM附带的运行状况检查 {#health-checks-provided-with-aem}

<table>
 <tbody>
  <tr>
   <td><strong>zHealthcheck名称</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>查询性能</td>
   <td><p>此运行状况检查在AEM 6.4 <strong>中已得到简化</strong>，现在可以检查最近重构的 <code>Oak QueryStats</code> MBean，更确切地说是属 <code>SlowQueries </code>性。 如果统计数据包含任何慢速查询，则运行状况检查会返回警告。 否则，它将返回“确定”状态。<br /> </p> <p>此运行状况检查的MBean <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DqueriesStatus%2Ctype%3DHealthCheck">为org.apache.sling.healthcheck:name=querysStatus,type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>观察队列长度</td>
   <td><p>观察队列长度迭代所有事件监听器和背景观察器，将其与 <code>queueSize </code>其和 <code>maxQueueSize</code> :</p>
    <ul>
     <li>如果值超过该值( <code>queueSize</code> 即事件将 <code>maxQueueSize</code> 被丢弃的时间)，则返回关键状态</li>
     <li>返回警告， <code>queueSize</code> 如果该值超过 <code>maxQueueSize * WARN_THRESHOLD</code> （默认值为0.75） </li>
    </ul> <p>每个队列的最大长度来自不同的配置（Oak和AEM），不能通过此运行状况检查进行配置。 此运行状况检查的MBean为 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DObservationQueueLengthHealthCheck%2Ctype%3DHealthCheck">org.apache.sling.healthcheck:name=OpercationQueueLengthHealthCheck,type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>查询遍历限制</td>
   <td><p>查询遍历限制检 <code>QueryEngineSettings</code> 查MBean，更确切地说是检查 <code>LimitInMemory</code> MBean和 <code>LimitReads</code> 属性，并返回以下状态：</p>
    <ul>
     <li>如果其中一个限制等于或高于 <code>Integer.MAX_VALUE</code></li>
     <li>如果某个限制低于10000（Oak的推荐设置），则返回“警告”状态</li>
     <li>如果无法检索或任何限 <code>QueryEngineSettings</code> 制，则返回“严重”状态</li>
    </ul> <p>此运行状况检查的Mbean为 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DqueryTraversalLimitsBundle%2Ctype%3DHealthCheck">org.apache.sling.healthcheck:name=queryTraversalLimitsBundle,type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>同步的时钟</td>
   <td><p>此检查仅与文档节点 <a href="https://github.com/apache/sling-old-svn-mirror/blob/4df9ab2d6592422889c71fa13afd453a10a5a626/bundles/extensions/discovery/oak/src/main/java/org/apache/sling/discovery/oak/SynchronizedClocksHealthCheck.java">存储群集相关</a>。 它返回以下状态：</p>
    <ul>
     <li>当实例时钟不同步并超过预定的低阈值时，返回“警告”状态</li>
     <li>当实例时钟不同步并超过预定的高阈值时，返回“关键”状态</li>
    </ul> <p>此运行状况检查的Mbean是 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DslingDiscoveryOakSynchronizedClocks%2Ctype%3DHealthCheck">org.apache.sling.healthcheck:name=slingDiscoveryOakSynchronizedClocks,type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>异步索引</td>
   <td><p>异步索引检查：</p>
    <ul>
     <li>如果至少一个索引通道出现故障，则返回关键状态</li>
     <li>检查所 <code>lastIndexedTime</code> 有索引通道和：
      <ul>
       <li>如果超过2小时前，返回关键状态 </li>
       <li>如果警告在2小时到45分钟之前，则返回警告状态 </li>
       <li>如果在45分钟前不到，则返回“OK”状态 </li>
      </ul> </li>
     <li>如果未满足这些条件，则返回“确定”状态</li>
    </ul> <p>“严重”和“警告”状态阈值均可配置。 此运行状况检查的Mbean是 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DasyncIndexHealthCheck%2Ctype%3DHealthCheck">org.apache.sling.healthcheck:name=asyncIndexHealthCheck,type=HealthCheck</a>。</p> <p><strong>注意：此 </strong>运行状况检查在AEM 6.4中可用，并已支持到AEM 6.3.0.1。</p> </td>
  </tr>
  <tr>
   <td>大型 Lucene 索引</td>
   <td><p>此检查使用MBean公开的数据来标 <code>Lucene Index Statistics</code> 识大型索引并返回：</p>
    <ul>
     <li>如果存在包含超过10亿个文档的索引，则警告状态</li>
     <li>a如果存在包含超过15亿份文档的索引，则处于关键状态</li>
    </ul> <p>可以配置阈值，健康检查的MBean为 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DlargeIndexHealthCheck%2Ctype%3DHealthCheck">org.apache.sling.healthcheck:name=largeIndexHealthCheck,type=HealthCheck。</a></p> <p><strong>注意：此 </strong>检查在AEM 6.4中可用，并已支持到AEM 6.3.2.0。</p> </td>
  </tr>
  <tr>
   <td>系统维护</td>
   <td><p>系统维护是一个综合检查，如果所有维护任务都按配置运行，则返回“确定”。 请记住：</p>
    <ul>
     <li>每个维护任务都会伴有相关的运行状况检查</li>
     <li>如果任务未添加到维护窗口，其运行状况检查将返回“关键”</li>
     <li>您需要配置“审核日志”和“工作流清除”维护任务，或者以其他方式从维护窗口中删除它们。 如果未配置，这些任务在首次尝试运行时将失败，因此系统维护检查将返回“关键”状态。</li>
     <li><strong>在AEM 6.4中</strong>，还检查了 <a href="/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks">Lucene Binaries Maintenance</a> （Lucene二进制维护）任务</li>
     <li>在AEM 6.2及更低版本中，系统维护检查会在启动后立即返回“警告”状态，因为任务从不运行。 从6.3开始，如果尚未到达第一个维护窗口，他们将返回“OK”。</li>
    </ul> <p>此运行状况检查的MBean <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3Dsystemchecks%2Ctype%3DHealthCheck">为org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>复制队列</td>
   <td><p>此检查会重复复制代理并查看其队列。 对于队列顶部的项目，检查代理重试复制的次数。 如果代理重试的复制次数大于该参数的 <code>numberOfRetriesAllowed</code> 值，则会返回警告。 该参 <code>numberOfRetriesAllowed</code> 数是可配置的。 </p> <p>此运行状况检查的MBean <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DreplicationQueue%2Ctype%3DHealthCheck" target="_blank">为org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>Sling 作业</td>
   <td>
    <div>
      Sling Jobs检查在JobManager中排队的作业数，将其与阈值进 <code>maxNumQueueJobs</code> 行比较，并：
    </div>
    <ul>
     <li>如果队列中的队列数 <code>maxNumQueueJobs</code> 超过，则返回关键值</li>
     <li>如果存在运行时间长于1小时的活动作业，则返回关键值</li>
     <li>如果存在已排队的作业，且上次完成的作业时间大于1小时，则返回关键值</li>
    </ul> <p>只有最大数目的已排队作业参数是可配置的，其默认值为1000。</p> <p>此运行状况检查的MBean <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DslingJobs%2Ctype%3DHealthCheck" target="_blank">为org.apache.sling.healthcheck:name=slingJobs,type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>请求性能</td>
   <td><p>此检查将查看 <code>granite.request.metrics.timer</code> Sling <a href="http://localhost:4502/system/console/slingmetrics" target="_blank">指标 </a>和：</p>
    <ul>
     <li>如果第75百分点值超过关键阈值（默认值为500毫秒），则返回关键值</li>
     <li>如果第75百分点值超过警告阈值（默认值为200毫秒），则返回警告</li>
    </ul> <p>此运行状况检查的MBean为<em></em><a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DrequestsStatus%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>日志错误</td>
   <td><p>如果日志中有错误，此检查将返回“警告”状态。</p> <p>此运行状况检查的MBean为 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DlogErrorHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>磁盘空间</td>
   <td><p>“磁盘空间”检查查看 <code>FileStoreStats</code> MBean，检索节点存储的大小和节点存储分区上的可用磁盘空间量，以及：</p>
    <ul>
     <li>如果可用磁盘空间与存储库大小的比率小于警告阈值（默认值为10），则返回警告</li>
     <li>如果可用磁盘空间与存储库大小比小于关键阈值（默认值为2），则返回关键值</li>
    </ul> <p>这两个阈值都可以配置。 此检查仅适用于区段存储的实例。</p> <p>此运行状况检查的MBean为 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DDiskSpaceHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck:name=DiskSpaceHealthCheck,type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>计划程序运行状况检查</td>
   <td><p>如果实例的Quartz作业运行时间超过60秒，则此检查将返回警告。 可配置可接受的持续时间阈值。</p> <p>此运行状况检查的MBean是 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DslingCommonsSchedulerHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck:name=slingCommonsSchedulerHealthCheck,type=HealthCheck</a><em>。</em></p> </td>
  </tr>
  <tr>
   <td>安全检查</td>
   <td><p>“安全性”检查是一个组合，它聚合多个与安全性相关的检查的结果。 这些单独的运行状况检查解决了与安全清单文档页面上提供的安全清 <a href="/help/sites-administering/security-checklist.md">单不同的问题。</a> 当实例启动时，该检查可用作安全烟雾测试。 </p> <p>此运行状况检查的MBean是 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3Dsecuritychecks%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck:name=</a><a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3Dsecuritychecks%2Ctype%3DHealthCheck" target="_blank"></a><a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3Dsecuritychecks%2Ctype%3DHealthCheck" target="_blank"></a><a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3Dsecuritychecks%2Ctype%3DHealthCheck" target="_blank">securitychecks,type=HealthCheck</a></p> </td>
  </tr>
  <tr>
   <td>活动包</td>
   <td><p>活动包检查所有包的状态，并：</p>
    <ul>
     <li>如果任何包未激活或（以延迟激活开始），则返回“警告”状态</li>
     <li>它忽略忽略列表中包的状态</li>
    </ul> <p>可以配置忽略列表参数。</p> <p>此运行状况检查的MBean <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DinactiveBundles%2Ctype%3DHealthCheck" target="_blank">为org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>代码缓存检查</td>
   <td><p>这是一个运行状况检查，它验证若干JVM条件，这些条件可触发Java 7中存在的CodeCache错误：</p>
    <ul>
     <li>在启用代码缓存刷新的情况下，如果实例在Java 7上运行，则返回警告</li>
     <li>如果实例在Java 7上运行，且保留代码缓存大小小于最小阈值（默认值为90MB），则返回警告</li>
    </ul> <p>阈值 <code>minimum.code.cache.size</code> 是可配置的。 有关该错误的详细信息，请 <a href="https://bugs.java.com/bugdatabase/view_bug.do?bug_id=8012547">查看</a><a href="https://bugs.java.com/bugdatabase/view_bug.do?bug_id=8012547"></a><a href="https://bugs.java.com/bugdatabase/view_bug.do?bug_id=8012547"></a><a href="https://bugs.java.com/bugdatabase/view_bug.do?bug_id=8012547"> 此页</a>。</p> <p>此运行状况检查的MBean为 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DcodeCacheHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck:name=codeCacheHealthCheck,type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>资源搜索路径错误</td>
   <td><p>检查路径中是否有任何资源， <code>/apps/foundation/components/primary</code> 并：</p>
    <ul>
     <li>返回警告，如果子节点位于 <code>/apps/foundation/components/primary</code></li>
    </ul> <p>此运行状况检查的MBean为 <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DresourceSearchPathErrorHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck:name=resourceSearchPathErrorHealthCheck,type=HealthCheck</a>。</p> </td>
  </tr>
 </tbody>
</table>

## 使用Nagios进行监视 {#monitoring-with-nagios}

运行状况检查控制板可以通过Granite JMX Mbeans与Nagios集成。 以下示例说明如何在运行AEM的服务器上添加一个检查，其中显示已使用的内存。

1. 在监视服务器上安装和安装Nagios。
1. 然后，安装Nagios Remote Plugin Executor(NRPE)。

   >[!NOTE]
   >
   >有关如何在系统上安装Nagios和NRPE的详细信息，请参阅 [Nagios文档](https://library.nagios.com/library/products/nagioscore/manuals/)。

1. 为AEM服务器添加主机定义。 这可以通过Nagios XI web界面使用配置管理器来完成：

   1. 打开浏览器并指向Nagios服务器。
   1. 按顶部 **菜单中** “配置”按钮。
   1. 在左窗格中，按高级配 **置下的核心配置****管理器**。
   1. 按“监 **视** ”部分下的“ **主机** ”链接。
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
1. 在两台 [服务器上安装check_http_json](https://github.com/phrawzty/check_http_json) 插件。
1. 在两台服务器上定义通用JSON检查命令：

   ```xml
   define command{
   
       command_name    check_http_json-int
   
       command_line    /usr/lib/nagios/plugins/check_http_json --user "$ARG1$" --pass "$ARG2$" -u 'https://$HOSTNAME$:$ARG3$/$ARG4$' -e '$ARG5$' -w '$ARG6$' -c '$ARG7$'
   
   }
   ```

1. 在AEM服务器上为已用内存添加服务：

   ```xml
   define service {
   
       use generic-service
   
       host_name my.remote.host
   
       service_description AEM Author Used Memory
   
       check_command  check_http_json-int!<cq-user>!<cq-password>!<cq-port>!system/sling/monitoring/mbeans/java/lang/Memory.infinity.json!{noname}.mbean:attributes.HeapMemoryUsage.mbean:attributes.used.mbean:value!<warn-threshold-in-bytes>!<critical-threshold-in-bytes>
   
       }
   ```

1. 检查您的Nagios控制板以了解新创建的服务：

   ![chlimage_1-119](assets/chlimage_1-119.png)

## Diagnosis tools {#diagnosis-tools}

操作控制板还提供对诊断工具的访问，这些工具可以帮助查找和排除来自运行状况检查控制板的警告的根本原因，并为系统操作员提供重要的调试信息。

其最重要的功能包括：

* 日志消息分析器
* 能够访问堆和线程转储
* 请求和查询性能分析器

您可以从AEM欢迎屏幕转到工具- **操作——诊断** ，以进入诊断工具屏幕。 您还可以通过直接访问以下URL来访问屏幕： `https://serveraddress:port/libs/granite/operations/content/diagnosis.html`

![chlimage_1-120](assets/chlimage_1-120.png)

### 日志消息 {#log-messages}

默认情况下，日志消息用户界面将显示所有ERROR消息。 如果要显示更多日志消息，您需要配置具有相应日志级别的记录器。

日志消息使用内存日志附加器，因此与日志文件无关。 另一个结果是，更改此UI中的日志级别不会更改记录在传统日志文件中的信息。 在此UI中添加和删除记录器只会影响内存记录器。 另外，请注意，更改记录器配置将反映在内存记录器的将来——已记录且不再相关的条目不会被删除，但类似条目将来不会记录。

您可以通过在UI中的左上齿轮按钮提供记录器配置来配置记录内容。 您可以在此处添加、删除或更新记录器配置。 记录器配置由日志级 **别** (WARN / INFO / DEBUG)和过滤器名 **称组成**。 过滤 **器名称** ，具有过滤日志消息源的角色。 或者，如果记录器应捕获指定级别的所有日志消息，则过滤器名称应为“**root**”。 设置记录器的级别将触发所有消息的捕获，其级别等于或高于指定的级别。

示例:

* 如果您计划捕获所有 **ERROR** 消息，则无需配置。 默认情况下会捕获所有ERROR消息。
* 如果计划捕获所有 **ERROR**、 **WARN** 和 **INFO消息** -记录器名称应设置为：“**root**”，并且记录器级别为：信 **息**。

* 如果计划捕获来自特定包（例如com.adobe.granite）的所有消息，则记录器名称应设置为：“com.adobe.granite”和记录器级别：调 **试** (这将捕获所有 **ERROR**、 **WARN**、 ******** INFO和DEBUG消息中的DEBUG消息)，如下图所示。

![chlimage_1-121](assets/chlimage_1-121.png)

>[!NOTE]
>
>不能将记录器名称设置为通过指定的过滤器仅捕获ERROR消息。 默认情况下，将捕获所有ERROR消息。

>[!NOTE]
>
>日志消息用户界面不反映实际错误日志。 除非您在UI中配置其他类型的日志消息，否则将只显示错误消息。 有关如何显示特定日志消息的信息，请参阅上面的说明。

>[!NOTE]
>
>诊断页面中的设置不会影响记录到日志文件的内容，反之亦然。 因此，尽管错误日志可能捕获INFO消息，但您可能在日志消息UI中看不到这些消息。 此外，通过UI可以从某些包中捕获DEBUG消息，而不会影响错误日志。 有关如何配置日志文件的详细信息，请参阅记 [录](/help/sites-deploying/configure-logging.md)。

>[!NOTE]
>
>**在AEM 6.4中**，维护任务将以INFO级别的更多信息富格式从开箱即用。 这使得能够更好地查看维护任务的状态。
>
>如果您使用第三方工具（如Splunk）监视维护任务活动并对其做出响应，则可以使用以下日志语句：

```
Log level: INFO
DATE+TIME [MaintanceLogger] Name=<MT_NAME>, Status=<MT_STATUS>, Time=<MT_TIME>, Error=<MT_ERROR>, Details=<MT_DETAILS>
```

### 请求性能 {#request-performance}

通过“请求性能”页可以分析处理的最慢页面请求。 此页面上仅会注册内容请求。 具体而言，将捕获以下请求：

1. 访问资源的请求 `/content`
1. 访问资源的请求 `/etc/design`
1. 具有扩展的请 `".html"` 求

![chlimage_1-122](assets/chlimage_1-122.png)

此时会显示页面：

* 发出请求的时间
* URL和请求方法
* 持续时间（以毫秒为单位）

默认情况下，捕获最慢的20个页面请求，但可以在配置管理器中修改该限制。

### 查询性能 {#query-performance}

“查询性能”页允许分析系统执行的最慢查询。 此信息由JMX Mbean中的存储库提供。 在Jackrabbit中， `com.adobe.granite.QueryStat` JMX Mbean提供此信息，而在Oak存储库中，它由 `org.apache.jackrabbit.oak.QueryStats.`

此时会显示页面：

* 进行查询的时间
* 查询的语言
* 发出查询的次数
* 查询语句
* 持续时间（以毫秒为单位）

![chlimage_1-123](assets/chlimage_1-123.png)

### 说明查询 {#explain-query}

对于任何给定的查询，Oak都会尝试根据库中 **oak:index节点下定义的Oak索引找到最佳执行方式** 。 根据查询，Oak可能会选择不同的索引。 了解Oak如何执行查询是优化查询的第一步。

Explain Query是一个工具，用于解释Oak如何执行查询。 可以从AEM欢迎屏幕转到工具——操作——诊断 **屏幕，然后单击查询性能** ，然后切换到解释查询选项卡，以访问该 **功能****** 。

**功能**

* 支持Xpath、JCR-SQL和JCR-SQL2查询语言
* 报告所提供查询的实际执行时间
* 检测慢速查询并警告可能慢速的查询
* 报告用于执行查询的Oak索引
* 显示实际Oak查询引擎说明
* 提供“慢速”和“常用”查询的“点击加载”列表

进入“解释查询”UI后，只需输入查询并按“解释”按钮即可使用该查询 **** :

![chlimage_1-124](assets/chlimage_1-124.png)

“查询说明”部分中的第一个条目是实际说明。 说明将显示用于执行查询的索引类型。

第二项是执行计划。

在运行 **查询之前，勾选“包括执行时间** ”框还将显示查询在中执行的时间，以便获得可用于优化应用程序或部署索引的更多信息。

![chlimage_1-125](assets/chlimage_1-125.png)

### 索引管理器 {#the-index-manager}

索引管理器的目的是便于索引管理，如维护索引或查看其状态。

可以从欢迎屏幕转至**工具——操作——诊断**，然后单击索引管理器按 **钮来访问** 。

也可以通过以下URL直接访问它： `https://serveraddress:port/libs/granite/operations/content/diagnosistools/indexManager.html`

![screen-shot_2019-06-18at154754](assets/screen-shot_2019-06-18at154754.png)

UI可用于筛选表中的索引，方法是在屏幕左上角的搜索框中键入筛选条件。

### 下载状态ZIP {#download-status-zip}

这将触发下载包含系统状态和配置的有用信息的zip文件。 该归档文件包含实例配置、捆绑包列表、OSGI、Sling指标和统计信息，这可能导致文件较大。 您可以使用“下载状态ZIP”窗口来减少大型状态 **文件的**&#x200B;影响。 **该窗口可从以下位置访问：AEM >工具>操作>诊断>下载状态ZIP。**

在此窗口中，您可以选择要导出的内容（日志文件和线程转储）以及下载中包含的相对于当前日期的日志天数。

![download_status_zip](assets/download_status_zip.png)

### 下载线程转储 {#download-thread-dump}

这将触发下载包含系统中线程相关信息的zip文件。 提供了有关每个线程的信息，如其状态、类加载器和堆栈跟踪。

### 下载堆转储 {#download-heap-dump}

您还可以下载堆的快照，以便在以后分析它。 请注意，这将触发以百兆字节顺序下载的大型文件。

## 自动维护任务 {#automated-maintenance-tasks}

“自动维护任务”页是一个位置，您可以在该位置查看和跟踪为定期执行计划的推荐维护任务。 这些任务与运行状况检查系统相集成。 还可以从界面手动执行这些任务。

要转到“操作控制板”中的“维护”页，您需要从AEM欢迎屏幕转至“工具”-“操作”-“控制板” **** -“维护”，或直接单击以下链接：

`https://serveraddress:port/libs/granite/operations/content/maintenance.html`

操作功能板中提供以下任务：

1. “修 **订清理**&#x200B;更新”任务，位于“每 **日维护窗口”菜单下** 。
1. Lucene Binaries Cleanup **(** Lucene二进制清除 **)任务，位于Daily Maintenance Window(每日维护窗** 口)菜单下。
1. 工作 **流清除任务** ，位于每周维护窗 **口菜单下** 。
1. “数 **据存储垃圾收集”任务** ，位于“每周 **维护窗口”菜单下** 。
1. “审 **核日志维护** ”任务位于“每周 **维护窗口”菜单下** 。
1. “版 **本清除维护** ”任务位于“每周 **维护窗口”菜单下** 。

每日维护窗口的默认时间为2 AM到5 AM。 在每周维护窗口中配置为运行的任务将在星期六的上午1点到凌晨2点之间执行。

您还可以通过按下任意两个维护卡上的齿轮图标来配置时间：

![chlimage_1-126](assets/chlimage_1-126.png)

>[!NOTE]
>
>自AEM 6.1起，现有维护窗口也可配置为每月运行。

### 修订清理 {#revision-clean-up}

有关执行修订清理的详细信息，请参 [阅此专用文章](/help/sites-deploying/revision-cleanup.md)。

### Lucene 二进制文件清理 {#lucene-binaries-cleanup}

通过使用Lucene二进制清除任务，您可以清除lucene二进制文件并减少正在运行的数据存储大小要求。 这是因为，Lucene的二进制客户流失将每天重新申请，而不是以前对成功运行数据存储垃圾 [收集的依赖](/help/sites-administering/data-store-garbage-collection.md) 。

虽然维护任务是为了减少与Lucene相关的修改垃圾，但是运行任务时总体效率的提高是：

* 每周执行数据存储垃圾收集任务将更快地完成
* 它还可能会略微提高AEM的整体性能

您可以从以下位置访问Lucene二进制文件清除任务： **AEM >工具>操作>维护>每日维护窗口> Lucene二进制清除**。

### 数据存储垃圾收集 {#data-store-garbage-collection}

有关数据存储垃圾收集的详细信息，请参阅专用 [文档页](/help/sites-administering/data-store-garbage-collection.md)。

### Workflow purge {#workflow-purge}

还可以从维护功能板中清除工作流。 要运行“工作流清除”任务，您需要：

1. 单击“每周 **维护窗口** ”页。
1. 在下一页中，单击“工 **作流** ”清除卡 **中的“播放** ”按钮。

>[!NOTE]
>
> 有关工作流维护的更多详细信息，请参 [阅此页](/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances)。

### 审核日志维护 {#audit-log-maintenance}

有关审核日志维护，请参阅单 [独的文档页面。](/help/sites-administering/operations-audit-log.md)

### 版本清除 {#version-purge}

您可以计划“版本清除”维护任务，以自动删除旧版本。 因此，这会最大限度地减少手动使用版本清 [除工具的需求](/help/sites-deploying/version-purging.md)。 您可以通过访问工具>操作>维护>每周维护窗口，并 **按照以下步骤来计划和配置版本清除任务** :

1. 单击“添 **加** ”按钮。
1. 从下 **拉菜单中选择** “版本清除”。

   ![version_purge_maintenance_task](assets/version_purge_maintenancetask.png)

1. 要配置“版本清除”任务，请单击新创建的“版 **本清除** ”维护卡上的齿轮图标。

   ![version_purge_taskconfiguration](assets/version_purge_taskconfiguration.png)

**在AEM 6.4中**，您可以按如下方式停止版本清除维护任务：

* 自动——如果计划的维护窗口在任务完成之前关闭，则任务将自动停止。 下一个维护窗口打开时，系统将恢复运行。
* 手动——要手动停止任务，请在“版本清除”维护卡上单击“停止 **** ”图标。 下次执行时，任务将安全地恢复。

>[!NOTE]
>
>停止维护任务意味着暂停其执行，而不会丢失对已进行作业的跟踪。

>[!CAUTION]
>
>要优化存储库大小，您应经常运行版本清除任务。 当流量有限时，应在工作时间以外安排任务。

## 自定义维护任务 {#custom-maintenance-tasks}

自定义维护任务可以作为OSGi服务实现。 由于维护任务基础结构是基于Apache Sling的作业处理，因此维护任务必须实现java接口 ` [org.apache.sling.event.jobs.consumer.JobExecutor](https://sling.apache.org/apidocs/sling7/org/apache/sling/event/jobs/consumer/JobExecutor.html)`。 此外，它必须声明多个服务注册属性以作为维护任务进行检测，如下所列：

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
   <td>用于定义用户是否可以停止任务的布尔属性。 如果任务声明它是可停止的，它必须在执行过程中检查它是否已停止，然后相应地执行。 默认值为false。</td>
   <td>true</td>
   <td>可选</td>
  </tr>
  <tr>
   <td>granite.maintenance.mandatory</td>
   <td>布尔属性，用于定义任务是否为必需任务且必须定期运行。 如果某项任务是必需任务，但当前不在任何活动的计划窗口中，则运行状况检查会将此报告为错误。 默认值为false。</td>
   <td>true</td>
   <td>可选</td>
  </tr>
  <tr>
   <td>granite.maintenance.name</td>
   <td>任务的唯一名称——用于引用任务。 这通常是一个简单的名称。</td>
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
   <td>这是维护任务的一个独特主题。<br /> Apache Sling作业处理将启动具有此主题的作业以执行维护任务，并在为此主题注册任务时执行该任务。<br /> 主题必须以 <i>com/adobe/granite/maintenance/job/开头</i></td>
   <td>com/adobe/granite/maintenance/job/MyMaintenanceTask</td>
   <td>必填</td>
  </tr>
 </tbody>
</table>

除了上述服务属性之外，还 `process()` 需要通过 `JobConsumer` 为维护任务添加应执行的代码来实现接口的方法。 提供的 `JobExecutionContext` 状态信息可用于输出状态信息、检查用户是否停止了作业并创建结果（成功或失败）。

对于维护任务不应在所有安装上运行的情况（例如，仅在发布实例上运行），您可以通过添加使服务需要配置才能处于活动状态 `@Component(policy=ConfigurationPolicy.REQUIRE)`。 然后，您可以根据配置将该配置标记为运行模式（取决于存储库）。 有关详细信息，请参 [阅配置OSGi](/help/sites-deploying/configuring-osgi.md#creating-the-configuration-in-the-repository)。

以下是一个自定义维护任务的示例，该任务从可配置的临时目录中删除文件，该目录在过去24小时内进行了修改：

src/main/java/com/adobe/granite/samples/maintenance/impl/DeleteTempFilesTask.java

<table>
 <tbody>
  <tr>
   <td><p> </p> <p><code>/*</code></p> <p><code> * #%L</code></p> <p><code> * sample-maintenance-task</code></p> <p><code> * %%</code></p> <p><code> * Copyright (C) 2014 Adobe</code></p> <p><code> * %%</code></p> <p><code> * Licensed under the Apache License, Version 2.0 (the "License");</code></p> <p><code> * you may not use this file except in compliance with the License.</code></p> <p><code> * You may obtain a copy of the License at</code></p> <p><code> * </code></p> <p><code> * <a href="https://www.apache.org/licenses/LICENSE-2.0">https://www.apache.org/licenses/LICENSE-2.0</a></code></p> <p><code> * </code></p> <p><code> * Unless required by applicable law or agreed to in writing, software</code></p> <p><code> * distributed under the License is distributed on an "AS IS" BASIS,</code></p> <p><code> * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.</code></p> <p><code> * See the License for the specific language governing permissions and</code></p> <p><code> * limitations under the License.</code></p> <p><code> * #L%</code></p> <p><code> */</code></p> <p><code> </code></p> <p><code>package com.adobe.granite.samples.maintenance.impl;</code></p> <p><code> </code></p> <p><code>import java.io.File;</code></p> <p><code>import java.util.Calendar;</code></p> <p><code>import java.util.Collection;</code></p> <p><code>import java.util.Map;</code></p> <p><code> </code></p> <p><code>import org.apache.commons.io.FileUtils;</code></p> <p><code>import org.apache.commons.io.filefilter.IOFileFilter;</code></p> <p><code>import org.apache.commons.io.filefilter.TrueFileFilter;</code></p> <p><code>import org.apache.felix.scr.annotations.Activate;</code></p> <p><code>import org.apache.felix.scr.annotations.Component;</code></p> <p><code>import org.apache.felix.scr.annotations.Properties;</code></p> <p><code>import org.apache.felix.scr.annotations.Property;</code></p> <p><code>import org.apache.felix.scr.annotations.Service;</code></p> <p><code>import org.apache.sling.commons.osgi.PropertiesUtil;</code></p> <p><code>import org.apache.sling.event.jobs.Job;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobConsumer;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobExecutionContext;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobExecutionResult;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobExecutor;</code></p> <p><code>import org.slf4j.Logger;</code></p> <p><code>import org.slf4j.LoggerFactory;</code></p> <p><code> </code></p> <p><code>import com.adobe.granite.maintenance.MaintenanceConstants;</code></p> <p><code> </code></p> <p><code>@Component(metatype = true,</code></p> <p><code> label = "Delete Temp Files Maintenance Task",</code></p> <p><code> description = "Maintatence Task which deletes files from a configurable temporary directory which have been modified in the last 24 hours.")</code></p> <p><code>@Service</code></p> <p><code>@Properties({</code></p> <p><code> @Property(name = MaintenanceConstants.PROPERTY_TASK_NAME, value = "DeleteTempFilesTask", propertyPrivate = true),</code></p> <p><code> @Property(name = MaintenanceConstants.PROPERTY_TASK_TITLE, value = "Delete Temp Files", propertyPrivate = true),</code></p> <p><code> @Property(name = JobConsumer.PROPERTY_TOPICS, value = MaintenanceConstants.TASK_TOPIC_PREFIX</code></p> <p><code> + "DeleteTempFilesTask", propertyPrivate = true) })</code></p> <p><code>public class DeleteTempFilesTask implements JobExecutor {</code></p> <p><code> </code></p> <p><code> private static final Logger log = LoggerFactory.getLogger(DeleteTempFilesTask.class);</code></p> <p><code> </code></p> <p><code> @Property(label = "Temporary Directory", description="Temporary Directory. Defaults to the java.io.tmpdir system property.")</code></p> <p><code> private static final String PROP_TEMP_DIR = "temp.dir";</code></p> <p><code> </code></p> <p><code> private File tempDir;</code></p> <p><code> </code></p> <p><code> @Activate</code></p> <p><code> private void activate(Map&lt;string, object=""&gt; properties) {</code></p> <p><code> this.tempDir = new File(PropertiesUtil.toString(properties.get(PROP_TEMP_DIR),</code></p> <p><code> System.getProperty("java.io.tmpdir")));</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> @Override</code></p> <p><code> public JobExecutionResult process(Job job, JobExecutionContext context) {</code></p> <p><code> log.info("Deleting old temp files from {}.", tempDir.getAbsolutePath());</code></p> <p><code> Collection&lt;file&gt; files = FileUtils.listFiles(tempDir, new LastModifiedBeforeYesterdayFilter(),</code></p> <p><code> TrueFileFilter.INSTANCE);</code></p> <p><code> int counter = 0;</code></p> <p><code> for (File file : files) {</code></p> <p><code> log.debug("Deleting file {}.", file.getAbsolutePath());</code></p> <p><code> counter++;</code></p> <p><code> file.delete();</code></p> <p><code> // TODO - capture the output of delete() and do something useful with it</code></p> <p><code> }</code></p> <p><code> return context.result().message(String.format("Deleted %s files.", counter)).succeeded();</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> /**</code></p> <p><code> * IOFileFilter which filters out files which have been modified in the last 24 hours.</code></p> <p><code> *</code></p> <p><code> */</code></p> <p><code> private static class LastModifiedBeforeYesterdayFilter implements IOFileFilter {</code></p> <p><code> </code></p> <p><code> private final long minTime;</code></p> <p><code> </code></p> <p><code> private LastModifiedBeforeYesterdayFilter() {</code></p> <p><code> Calendar cal = Calendar.getInstance();</code></p> <p><code> cal.add(Calendar.DATE, -1);</code></p> <p><code> this.minTime = cal.getTimeInMillis();</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> @Override</code></p> <p><code> public boolean accept(File dir, String name) {</code></p> <p><code> // this method is never actually called.</code></p> <p><code> return false;</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> @Override</code></p> <p><code> public boolean accept(File file) {</code></p> <p><code> return file.lastModified() <= this.minTime;</code></p> <p><code> }</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code>}</code></p> <p><code>&lt;file&gt;&lt;/string,&gt;</code></p> <p> </p> </td>
  </tr>
 </tbody>
</table>

[experiencemanager-java-maintenancetask-sample](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-maintenancetask-sample)- [src/main/java/com/adobe/granite/samples/maintenance/impl/DeleteTempFilesTask.java](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-maintenancetask-sample/blob/master/src/main/java/com/adobe/granite/samples/maintenance/impl/DeleteTempFilesTask.java)

部署服务后，它会显示在操作控制板UI中。 您可以将其添加到某个可用的维护计划中：

![chlimage_1-127](assets/chlimage_1-127.png)

这将在/apps/granite/operations/config/maintenance/`schedule`//中添加相应的资源`taskname`。 如果任务与运行模式相关，则需要在该节点上设置granite.operations.conditions.runmode属性，并设置运行模式的值，这些值需要为此维护任务处于活动状态。

## 系统概览 {#system-overview}

系 **统概述控制板** ，显示AEM实例的配置、硬件和运行状况的高级概述。 这意味着系统运行状况是透明的，所有信息都会汇总到单个仪表板中。

>[!NOTE]
>
>您还可以观 [看此视频](https://video.tv.adobe.com/v/21340?captions=chi_hans) ，了解系统概述控制板的简介。

### 如何访问 {#how-to-access}

要访问“系统概述”控制板，请导航到“工 **具”>“操作”>“系统概述”**。

![system_overview_dashboard](assets/system_overview_dashboard.png)

### 系统概述功能板说明 {#system-overview-dashboard-explained}

下表描述了系统概述功能板中显示的所有信息。 请记住，当没有要显示的相关信息（例如，备份尚未进行，没有关键的运行状况检查）时，相应的部分将显示“无条目”消息。

您还可以通过单 `JSON` 击功能板右上角的 **Download** （下载）按钮来下载汇总功能板信息的文件。端点是 `JSON` ，它可用于外部监 `/libs/granite/operations/content/systemoverview/export.json``curl` 视的脚本中。

<table>
 <tbody>
  <tr>
   <td><strong>区域</strong></td>
   <td><strong>显示哪些信息</strong></td>
   <td><strong>什么时候是关键</strong></td>
   <td><strong>链接到</strong></td>
  </tr>
  <tr>
   <td>运行状况检查</td>
   <td>
    <ul>
     <li>处于关键状态的检查列表</li>
     <li>处于“警告”状态的检查列表</li>
    </ul> </td>
   <td>以可视方式指示：<br />
    <ul>
     <li>关键检查的红色标签</li>
     <li>用于警告检查的橙色标签</li>
    </ul> </td>
   <td>
    <ul>
     <li>运行状况报告页</li>
    </ul> </td>
  </tr>
  <tr>
   <td>维护任务</td>
   <td>
    <ul>
     <li>失败的任务列表</li>
     <li>当前正在运行的任务列表</li>
     <li>上次运行中成功的任务列表</li>
     <li>从未运行的任务列表</li>
     <li>未计划的任务列表</li>
    </ul> </td>
   <td><p>以可视方式指示：</p>
    <ul>
     <li>失败任务的红色标记</li>
     <li>用于运行任务的橙色标记（因为它们可能影响性能）</li>
     <li>其他状态均为灰色标记</li>
    </ul> </td>
   <td>
    <ul>
     <li>“维护任务”页</li>
    </ul> </td>
  </tr>
  <tr>
   <td>系统</td>
   <td>
    <ul>
     <li>操作系统和操作系统版本（例如，Mac OS X）</li>
     <li>系统负载平均值，从OperatingSystemMXBeanable检索 <a href="https://docs.oracle.com/javase/8/docs/api/java/lang/management/OperatingSystemMXBean.html#getSystemLoadAverage--">到</a></li>
     <li>磁盘空间（在主目录所在的分区上）</li>
     <li>最大堆，由 <a href="https://docs.oracle.com/javase/8/docs/api/java/lang/management/MemoryMXBean.html#getHeapMemoryUsage--">MemoryMXBean返回</a></li>
    </ul> </td>
   <td>不适用</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>实例</td>
   <td>
    <ul>
     <li>AEM版本</li>
     <li>运行模式列表</li>
     <li>启动实例的日期</li>
    </ul> </td>
   <td>不适用</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>存储库</td>
   <td>
    <ul>
     <li>Oak版</li>
     <li>节点存储的类型（段Tar或文档）
      <ul>
       <li>如果类型是文档，则显示文档存储的类型（RDB或Mongo）</li>
      </ul> </li>
     <li>如果存在自定义数据存储：
      <ul>
       <li>对于文件数据存储，将显示路径</li>
       <li>对于S3数据存储，将显示S3存储段的名称</li>
       <li>对于共享的S3数据存储，将显示S3存储段的名称</li>
       <li>对于Azure Data Store，将显示容器</li>
      </ul> </li>
     <li>如果没有自定义外部数据存储，则显示指示此情况的消息</li>
    </ul> </td>
   <td>不适用</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>分发代理</td>
   <td>
    <ul>
     <li>具有被阻止队列的代理的列表</li>
     <li>配置错误的代理列表（“配置错误”）</li>
     <li>队列处理暂停的代理列表</li>
     <li>空闲代理的列表</li>
     <li>正在运行的代理的列表（当前是处理条目）</li>
    </ul> </td>
   <td><p>以可视方式指示：</p>
    <ul>
     <li>被阻止的代理或配置错误的红色标记</li>
     <li>暂停的代理的橙色标签</li>
     <li>暂停、空闲或正在运行的代理的灰色标记<br /> </li>
    </ul> </td>
   <td>分发页面<br /> </td>
  </tr>
  <tr>
   <td>复制代理</td>
   <td>
    <ul>
     <li>具有被阻止队列的代理的列表</li>
     <li>空闲代理的列表</li>
     <li>正在运行的代理的列表（当前是处理条目）</li>
    </ul> </td>
   <td><p>以可视方式指示：<br /> </p>
    <ul>
     <li>被阻止代理的红色标签</li>
     <li>暂停的代理的灰色标记</li>
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
       <li>已中止</li>
      </ul> </li>
    </ul> <p>对于上面显示的每个状态，将执行查询，限制为400毫秒。 在400毫秒时，将显示截至该点所获取的条目数。</p> </td>
   <td><p>未解释：</p>
    <ul>
     <li>当存在处于意外状态的工作流和作业时，用户应进行调查。</li>
    </ul> </td>
   <td>“工作流失败”页</td>
  </tr>
  <tr>
   <td>Sling 作业</td>
   <td><p>Sling作业计数——处于给定状态的作业数（如果有）:</p>
    <ul>
     <li>失败</li>
     <li>已排队</li>
     <li>已取消</li>
     <li>活动</li>
    </ul> </td>
   <td><p>未解释：</p>
    <ul>
     <li>当存在意外状态或计数较高的作业时，用户应进行调查。</li>
    </ul> </td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>预计节点计数</td>
   <td><p>估计人数：</p>
    <ul>
     <li>页</li>
     <li>资产</li>
     <li>标记</li>
     <li>可授权</li>
     <li>节点总数<br /> </li>
    </ul> <p>从nodeCounterMBean获取节点总数，而从IndexInfoService获取其余统计信息。</p> </td>
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
    </ul> <p>如果线程转储中存在索引或查询线程。</p> </td>
   <td>不适用</td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

