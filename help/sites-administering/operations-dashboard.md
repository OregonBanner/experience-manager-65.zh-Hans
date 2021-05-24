---
title: 操作仪表板
seo-title: 操作仪表板
description: 了解如何使用操作仪表板。
seo-description: 了解如何使用操作仪表板。
uuid: ef24813f-a7a8-4b26-a496-6f2a0d9efef6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: b210f5d7-1d68-49ee-ade7-667c6ab11d2b
docset: aem65
exl-id: f9a88156-91a2-4c85-9bc9-8f23700c2cbd
feature: 运营
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '6199'
ht-degree: 2%

---

# 操作功能板{#operations-dashboard}

## 简介 {#introduction}

AEM 6中的“操作功能板”可帮助系统操作员一目了然地监控AEM系统运行状况。 它还提供有关AEM相关方面的自动生成的诊断信息，并允许配置和运行自包含的维护自动化，以显着减少项目操作和支持案例。 操作功能板可通过自定义运行状况检查和维护任务进行扩展。 此外，操作功能板数据可通过JMX从外部监控工具访问。

**操作功能板：**

* 是一键式系统状态，可帮助运营部门提高效率
* 在一个集中的位置提供系统运行状况概述
* 减少查找、分析和修复问题的时间
* 提供自带维护自动化功能，有助于显着降低项目运营成本

可以从AEM欢迎屏幕中转到&#x200B;**Tools** - **Operations**，以访问该工具。

>[!NOTE]
>
>要能够访问“操作功能板”，登录用户必须是“操作员”用户组的一部分。 有关更多信息，请参阅[用户、组和访问权限管理](/help/sites-administering/user-group-ac-admin.md)中的文档。

## 健康报表 {#health-reports}

运行状况报告系统通过Sling运行状况检查提供有关AEM实例运行状况的信息。 这可以通过OSGI、JMX、HTTP请求（通过JSON）或通过触屏UI来完成。 它提供某些可配置计数器的测量值和阈值，在某些情况下，将提供有关如何解决该问题的信息。

它具有以下几项功能：

## 运行状况检查 {#health-checks}

**健康报告**&#x200B;是一个卡系统，用于指示特定产品区域的健康状况是否良好。 这些卡片是Sling运行状况检查的可视化图表，用于聚合来自JMX和其他源的数据，并再次将处理的信息显示为MBean。 也可以在[JMX Web控制台](/help/sites-administering/jmx-console.md)的&#x200B;**org.apache.sling.healthcheck**&#x200B;域下检查这些MBean。

可以通过AEM欢迎屏幕上的&#x200B;**工具** - **操作** - **运行状况报告**&#x200B;菜单访问“运行状况报告”界面，也可以直接通过以下URL访问：

`https://<serveraddress>:port/libs/granite/operations/content/healthreports/healthreportlist.html`

![chlimage_1-116](assets/chlimage_1-116.png)

卡系统会公开三种可能的状态：**OK**、**警告**&#x200B;和&#x200B;**关键**。 状态是规则和阈值的结果，可通过将鼠标悬停在卡上，然后单击操作栏中的齿轮图标来配置它们：

![chlimage_1-117](assets/chlimage_1-117.png)

### 运行状况检查类型{#health-check-types}

AEM 6中有两种类型的运行状况检查：

1. 单个运行状况检查
1. 复合运行状况检查

**单个运行状况检查**&#x200B;是与状态卡对应的单个运行状况检查。 单个运行状况检查可以配置规则或阈值，并且它们可以提供一个或多个提示和链接以解决已识别的运行状况问题。 让我们以“日志错误”检查为例：如果实例日志中存在ERROR条目，则将在运行状况检查的详细信息页面上找到它们。 在页面顶部，您将在诊断工具部分看到指向“日志消息”分析器的链接，该链接将使您能够更详细地分析这些错误并重新配置日志记录器。

**复合运行状况检查**&#x200B;是一种检查，用于聚合来自多个单独检查的信息。

复合运行状况检查是使用&#x200B;**filter tags**&#x200B;的辅助配置的。 实质上，具有相同过滤器标记的所有单个检查都将分组为复合运行状况检查。 仅当聚合的所有单个检查也具有“OK”状态时，复合运行状况检查才具有“OK”状态。

### 如何创建运行状况检查{#how-to-create-health-checks}

在“操作功能板”中，您可以显示单个和复合运行状况检查的结果。

### 创建单个运行状况检查{#creating-an-individual-health-check}

创建单个运行状况检查涉及两个步骤：实施Sling运行状况检查并在功能板的配置节点中为运行状况检查添加一个条目。

1. 要创建Sling运行状况检查，您需要创建一个实施Sling HealthCheck界面的OSGI组件。 将此组件添加到包中。 组件的属性将完全识别运行状况检查。 安装组件后，将自动为运行状况检查创建JMX MBean。 有关更多信息，请参阅[Sling运行状况检查文档](https://sling.apache.org/documentation/bundles/sling-health-check-tool.html)。

   Sling运行状况检查组件示例，该组件使用OSGI服务组件注释编写：

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
   >`MBEAN_NAME`属性定义将为此运行状况检查生成的mbean的名称。

1. 创建运行状况检查后，需要创建一个新的配置节点，以使其可在操作功能板界面中访问。 对于此步骤，需要知道运行状况检查的JMX Mbean名称（`MBEAN_NAME`属性）。 要为运行状况检查创建配置，请打开CRXDE并在以下路径下添加一个新节点（类型为&#x200B;**nt:unstructured**）：`/apps/settings/granite/operations/hc`

   应在新节点上设置以下属性：

   * **名称:** `sling:resourceType`

      * **类型:** `String`
      * **值：** `granite/operations/components/mbean`
   * **名称:** `resource`

      * **类型:** `String`
      * **值：** `/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck/exampleHealthCheck`

   >[!NOTE]
   >
   >上述资源路径按如下方式创建：如果运行状况检查的mbean名称为“test”，则在路径`/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck`的末尾添加“test”
   >
   >因此，最终的路径是：
   >
   >`/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck/test`

   >[!NOTE]
   >
   >确保`/apps/settings/granite/operations/hc`路径的以下属性设置为true:
   >
   >
   >`sling:configCollectionInherit`
   >
   >`sling:configPropertyInherit`
   >
   >
   >这将指示配置管理器将新配置与`/libs`中的现有配置合并。

### 创建复合运行状况检查{#creating-a-composite-health-check}

复合运行状况检查的作用是聚合多个共享一组通用功能的单独运行状况检查。 例如，安全复合运行状况检查将执行安全相关验证的所有单个运行状况检查分组在一起。 创建复合检查的第一步是添加新的OSGi配置。 要使其显示在操作功能板中，需要添加新的配置节点，这与我们进行简单检查的方式相同。

1. 转到OSGI控制台中的Web配置管理器。 您可以通过访问`https://serveraddress:port/system/console/configMgr`来执行此操作
1. 搜索名为&#x200B;**Apache Sling Composite Health Check**&#x200B;的条目。 在找到该配置后，请注意已有两种配置可用：一个用于系统检查，另一个用于安全检查。
1. 通过按配置右侧的“+”按钮创建新配置。 将显示一个新窗口，如下所示：

   ![chlimage_1-23](assets/chlimage_1-23.jpeg)

1. 创建配置并保存。 将使用新配置创建Mbean。

   每个配置属性的用途如下：

   * **名称(hc.name):** 复合运行状况检查的名称。建议使用有意义的名称。
   * **标记(hc.tags):** 用于此运行状况检查的标记。如果此复合运行状况检查旨在成为另一个复合运行状况检查的一部分（例如，在运行状况检查层次结构中），请添加此复合所关联的标记。
   * **MBean名称(hc.mbean.name):** 将给此复合运行状况检查的JMX MBean的Mbean的名称。
   * **过滤器标记(filter.tags):** 这是特定于复合运行状况检查的属性。这些是复合应聚合的标记。 复合运行状况检查将聚合到其组下所有具有与此复合的任何过滤器标记相匹配的任何标记的运行状况检查。 例如，具有过滤器标记&#x200B;**test**&#x200B;和&#x200B;**check**&#x200B;的复合运行状况检查将聚合所有具有其标记属性(`hc.tags`)中的任何&#x200B;**test**&#x200B;和&#x200B;**check**&#x200B;标记的单独和复合运行状况检查。

   >[!NOTE]
   >
   >将为Apache Sling复合运行状况检查的每个新配置创建新的JMX Mbean。**

1. 最后，需要在操作仪表板配置节点中添加刚刚创建的复合运行状况检查的条目。 此过程与单独运行状况检查的过程相同：需要在`/apps/settings/granite/operations/hc`下创建类型为&#x200B;**nt:unstructured**&#x200B;的节点。 节点的资源属性将由OSGI配置中的&#x200B;**hc.mean.name**&#x200B;值定义。

   例如，如果您创建了配置，并将&#x200B;**hc.mbean.name**&#x200B;值设置为&#x200B;**diskusage**，则配置节点将如下所示：

   * **名称:** `Composite Health Check`

      * **类型:** `nt:unstructured`

   具有以下属性：

   * **名称:** `sling:resourceType`

      * **类型:** `String`
      * **值：** `granite/operations/components/mbean`
   * **名称:** `resource`

      * **类型:** `String`
      * **值：** `/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck/diskusage`

   >[!NOTE]
   >
   >如果您创建的各个运行状况检查在逻辑上属于复合检查下（默认情况下，该复合检查已出现在功能板中），则它们将自动捕获并分组到相应的复合检查下。 因此，无需为这些检查创建新的配置节点。
   >
   >例如，如果您创建单个安全运行状况检查，则您只需为其分配“**security**”标记，并且已安装该检查，它将自动显示在“操作功能板”的“安全检查”复合检查下。

### AEM {#health-checks-provided-with-aem}提供的运行状况检查

<table>
 <tbody>
  <tr>
   <td><strong>zHealthcheck名称</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>查询性能</td>
   <td><p>在AEM 6.4</strong>中，此运行状况检查已得到简化，现在检查最近重构的<code>Oak QueryStats</code> MBean，更具体地说是<code>SlowQueries </code>属性。 <strong>如果统计数据包含任何慢速查询，则运行状况检查会返回警告。 否则，返回“确定”状态。<br /> </strong></p> <p>此运行状况检查的MBean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DqueriesStatus%2Ctype%3DHealthCheck">org.apache.sling.healthcheck:name=querysStatus，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>观察队列长度</td>
   <td><p>观察队列长度迭代所有事件侦听器和后台观察器，将其<code>queueSize </code>与其<code>maxQueueSize</code>和：</p>
    <ul>
     <li>如果<code>queueSize</code>值超过<code>maxQueueSize</code>值（即删除事件时），则返回关键状态</li>
     <li>如果<code>queueSize</code>值超过<code>maxQueueSize * WARN_THRESHOLD</code>，则返回警告（默认值为0.75） </li>
    </ul> <p>每个队列的最大长度来自单独的配置(Oak和AEM)，不能通过此运行状况检查进行配置。 此运行状况检查的MBean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DObservationQueueLengthHealthCheck%2Ctype%3DHealthCheck">org.apache.sling.healthcheck:name=ObservationQueueLengthHealthCheck，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>查询遍历限制</td>
   <td><p>查询遍历限制检查<code>QueryEngineSettings</code> MBean，更具体地说是<code>LimitInMemory</code>和<code>LimitReads</code>属性，并返回以下状态：</p>
    <ul>
     <li>如果其中一个限制等于或大于 <code>Integer.MAX_VALUE</code></li>
     <li>如果其中一个限制低于10000（Oak中的建议设置），则返回“警告”状态</li>
     <li>如果无法检索<code>QueryEngineSettings</code>或任何限制，则返回“关键”状态</li>
    </ul> <p>此运行状况检查的Mbean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DqueryTraversalLimitsBundle%2Ctype%3DHealthCheck">org.apache.sling.healthcheck:name=queryTraversLimitsBundle，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>同步的时钟</td>
   <td><p>此检查仅与<a href="https://github.com/apache/sling-old-svn-mirror/blob/4df9ab2d6592422889c71fa13afd453a10a5a626/bundles/extensions/discovery/oak/src/main/java/org/apache/sling/discovery/oak/SynchronizedClocksHealthCheck.java">文档节点存储群集</a>相关。 它会返回以下状态：</p>
    <ul>
     <li>当实例时钟不同步并超过预定义的低阈值时，返回“警告”状态</li>
     <li>当实例时钟不同步并超过预定义的高阈值时，返回“关键”状态</li>
    </ul> <p>此运行状况检查的Mbean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DslingDiscoveryOakSynchronizedClocks%2Ctype%3DHealthCheck">org.apache.sling.healthcheck:name=slingDiscoveryOakSynchronizedClocks，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>异步索引</td>
   <td><p>异步索引检查：</p>
    <ul>
     <li>如果至少有一个索引通道失败，则返回关键状态</li>
     <li>检查<code>lastIndexedTime</code>是否存在所有索引通道，并：
      <ul>
       <li>如果超过2小时，则返回关键状态 </li>
       <li>如果在2小时到45分钟之前，则返回警告状态 </li>
       <li>如果45分钟前不到，则返回“正常”状态 </li>
      </ul> </li>
     <li>如果不满足这些条件，则返回“确定”状态</li>
    </ul> <p>“严重”和“警告”状态阈值均可配置。 此运行状况检查的Mbean是<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DasyncIndexHealthCheck%2Ctype%3DHealthCheck">org.apache.sling.healthcheck:name=asyncIndexHealthCheck，type=HealthCheck</a>。</p> <p><strong>注意： </strong>此运行状况检查在AEM 6.4中可用，并已支持到AEM 6.3.0.1。</p> </td>
  </tr>
  <tr>
   <td>大型 Lucene 索引</td>
   <td><p>此检查使用<code>Lucene Index Statistics</code> MBean公开的数据来标识大索引并返回：</p>
    <ul>
     <li>a如果存在包含超过10亿份文档的索引，则显示警告状态</li>
     <li>a如果有超过15亿份文档的索引，则处于关键状态</li>
    </ul> <p>可以配置阈值，运行状况检查的MBean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DlargeIndexHealthCheck%2Ctype%3DHealthCheck">org.apache.sling.healthcheck:name=largeIndexHealthCheck，type=HealthCheck.</a></p> <p><strong>注意： </strong>此检查在AEM 6.4中可用，并且已备份到AEM 6.3.2.0。</p> </td>
  </tr>
  <tr>
   <td>系统维护</td>
   <td><p>系统维护是一个复合检查，如果所有维护任务都按配置运行，则返回“确定”。 请记住以下事项：</p>
    <ul>
     <li>每项维护任务都附带相关的运行状况检查</li>
     <li>如果任务未添加到维护窗口，则其运行状况检查将返回关键</li>
     <li>您需要配置“审核日志”和“工作流清除”维护任务，或者从维护窗口中删除这些任务。 如果未配置，这些任务在首次尝试运行时将失败，因此系统维护检查将返回“关键”状态。</li>
     <li><strong>在AEM 6.4中</strong>，还会检查Lucene二进制文 <a href="/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks">件维</a> 护任务</li>
     <li>在AEM 6.2及更低版本上，系统维护检查会在启动后立即返回警告状态，因为任务从不运行。 从6.3开始，如果尚未到达第一个维护窗口，则它们将返回“OK”。</li>
    </ul> <p>此运行状况检查的MBean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3Dsystemchecks%2Ctype%3DHealthCheck">org.apache.sling.healthcheck:name=systemchecks，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>复制队列</td>
   <td><p>此检查会遍历复制代理并查看其队列。 对于队列顶部的项目，检查代理重试复制的次数。 如果代理重试复制的次数超过<code>numberOfRetriesAllowed</code>参数的值，则会返回警告。 可配置<code>numberOfRetriesAllowed</code>参数。 </p> <p>此运行状况检查的MBean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DreplicationQueue%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck:name=replicationQueue，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>Sling 作业</td>
   <td>
    <div>
      Sling作业会检查在JobManager中排队的作业数，并将其与
     <code>maxNumQueueJobs</code>阈值和：
    </div>
    <ul>
     <li>如果队列中的值超过<code>maxNumQueueJobs</code>，则返回严重值</li>
     <li>如果有长时间运行的活动作业超过1小时，则返回关键</li>
     <li>如果存在已排队的作业，并且上次完成的作业时间早于1小时，则返回关键值</li>
    </ul> <p>只能配置已排队作业参数的最大数量，其默认值为1000。</p> <p>此运行状况检查的MBean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DslingJobs%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck:name=slingJobs，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>请求性能</td>
   <td><p>此检查将检查<code>granite.request.metrics.timer</code> <a href="http://localhost:4502/system/console/slingmetrics" target="_blank">Sling量度</a>和：</p>
    <ul>
     <li>如果第75个百分位数值超过临界阈值（默认值为500毫秒），则返回临界值</li>
     <li>如果第75个百分位数值超过警告阈值（默认值为200毫秒），则返回警告</li>
    </ul> <p>此运行状况检查的MBean为<em> </em><a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DrequestsStatus%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck:name=requestsStatus，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>日志错误</td>
   <td><p>如果日志中存在错误，此检查将返回“警告”状态。</p> <p>此运行状况检查的MBean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DlogErrorHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck:name=logErrorHealthCheck，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>磁盘空间</td>
   <td><p>磁盘空间检查检查<code>FileStoreStats</code> MBean，检索节点存储的大小和节点存储分区上的可用磁盘空间量，以及：</p>
    <ul>
     <li>如果可用磁盘空间与存储库大小的比率小于警告阈值（默认值为10），则返回警告</li>
     <li>如果可用磁盘空间与存储库大小比小于临界阈值（默认值为2），则返回临界</li>
    </ul> <p>两个阈值都可配置。 此检查仅适用于具有区段存储的实例。</p> <p>此运行状况检查的MBean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DDiskSpaceHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck:name=DiskSpaceHealthCheck，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>计划程序运行状况检查</td>
   <td><p>如果实例的Quartz作业运行时间超过60秒，则此检查会返回警告。 可接受的持续时间阈值是可配置的。</p> <p>此运行状况检查的MBean是<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DslingCommonsSchedulerHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck:name=slingCommonsSchedulerHealthCheck，type=HealthCheck</a><em>.</em></p> </td>
  </tr>
  <tr>
   <td>安全检查</td>
   <td><p>安全检查是聚合多个安全相关检查结果的组合。 这些单独的运行状况检查可解决与<a href="/help/sites-administering/security-checklist.md">安全检查表文档页面上提供的安全检查表不同的问题。</a> 在启动实例时，此检查可用作安全烟雾测试。 </p> <p>此运行状况检查的MBean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3Dsecuritychecks%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck:name=securitychecks，type=HealthCheck</a></p> </td>
  </tr>
  <tr>
   <td>活动包</td>
   <td><p>活动包检查所有包的状态，并：</p>
    <ul>
     <li>如果有任何包不处于活动状态，或者（从延迟激活开始）返回“警告”状态</li>
     <li>它会忽略忽略忽略列表中的包状态</li>
    </ul> <p>可以配置忽略列表参数。</p> <p>此运行状况检查的MBean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DinactiveBundles%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck:name=inactiveBundles，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>代码缓存检查</td>
   <td><p>这是运行状况检查，用于验证可触发Java 7中存在的CodeCache错误的多个JVM条件：</p>
    <ul>
     <li>如果实例在启用“代码缓存刷新”的情况下在Java 7中运行，则返回警告</li>
     <li>如果实例在Java 7中运行，并且保留代码缓存大小小于最小阈值（默认值为90MB），则返回警告</li>
    </ul> <p>可配置<code>minimum.code.cache.size</code>阈值。 有关该错误的更多信息，请<a href="https://bugs.java.com/bugdatabase/view_bug.do?bug_id=8012547">check</a><a href="https://bugs.java.com/bugdatabase/view_bug.do?bug_id=8012547"></a><a href="https://bugs.java.com/bugdatabase/view_bug.do?bug_id=8012547"></a><a href="https://bugs.java.com/bugdatabase/view_bug.do?bug_id=8012547">此页面</a>。</p> <p>此运行状况检查的MBean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DcodeCacheHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck:name=codeCacheHealthCheck，type=HealthCheck</a>。</p> </td>
  </tr>
  <tr>
   <td>资源搜索路径错误</td>
   <td><p>检查路径<code>/apps/foundation/components/primary</code>中是否有任何资源，并：</p>
    <ul>
     <li>返回当下存在子节点时发出警告 <code>/apps/foundation/components/primary</code></li>
    </ul> <p>此运行状况检查的MBean为<a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DresourceSearchPathErrorHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck:name=resourceSearchPathErrorHealthCheck，type=HealthCheck</a>。</p> </td>
  </tr>
 </tbody>
</table>

## 使用Nagios {#monitoring-with-nagios}进行监控

运行状况检查功能板可以通过Granite JMX Mbeans与Nagios集成。 以下示例说明如何添加检查，以显示运行AEM的服务器上已用内存。

1. 在监控服务器上设置并安装Nagios。
1. 接下来，安装Nagios远程插件执行器(NRPE)。

   >[!NOTE]
   >
   >有关如何在系统上安装Nagios和NRPE的更多信息，请参阅[Nagios文档](https://library.nagios.com/library/products/nagioscore/manuals/)。

1. 为AEM服务器添加主机定义。 这可以通过Nagios XI Web界面使用配置管理器来完成：

   1. 打开浏览器并指向Nagios服务器。
   1. 按顶部菜单中的&#x200B;**Configure**&#x200B;按钮。
   1. 在左窗格中，按&#x200B;**Advanced Configuration**&#x200B;下的&#x200B;**核心配置管理器**。
   1. 按&#x200B;**监视**&#x200B;部分下的&#x200B;**Hosts**&#x200B;链接。
   1. 添加主机定义：

   ![chlimage_1-118](assets/chlimage_1-118.png)

   以下是主机配置文件示例（如果您使用的是Nagios Core）：

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
1. 在两台服务器上安装[check_http_json](https://github.com/phrawzty/check_http_json)插件。
1. 在两台服务器上定义通用JSON check命令：

   ```xml
   define command{
   
       command_name    check_http_json-int
   
       command_line    /usr/lib/nagios/plugins/check_http_json --user "$ARG1$" --pass "$ARG2$" -u 'https://$HOSTNAME$:$ARG3$/$ARG4$' -e '$ARG5$' -w '$ARG6$' -c '$ARG7$'
   
   }
   ```

1. 为AEM服务器上的已用内存添加服务：

   ```xml
   define service {
   
       use generic-service
   
       host_name my.remote.host
   
       service_description AEM Author Used Memory
   
       check_command  check_http_json-int!<cq-user>!<cq-password>!<cq-port>!system/sling/monitoring/mbeans/java/lang/Memory.infinity.json!{noname}.mbean:attributes.HeapMemoryUsage.mbean:attributes.used.mbean:value!<warn-threshold-in-bytes>!<critical-threshold-in-bytes>
   
       }
   ```

1. 检查Nagios功能板以了解新创建的服务：

   ![chlimage_1-119](assets/chlimage_1-119.png)

## 诊断工具{#diagnosis-tools}

“操作功能板”还提供对诊断工具的访问，这些工具有助于查找和排除来自“运行状况检查功能板”的警告的根本原因，并为系统操作员提供重要的调试信息。

其最重要的功能包括：

* 日志消息分析器
* 访问堆和线程转储的功能
* 请求和查询性能分析程序

从AEM欢迎屏幕中转到&#x200B;**Tools - Operations - Diagnosis**，可以访问“诊断工具”屏幕。 您还可以通过直接访问以下URL来访问屏幕：`https://serveraddress:port/libs/granite/operations/content/diagnosis.html`

![chlimage_1-120](assets/chlimage_1-120.png)

### 日志消息{#log-messages}

默认情况下，“用户界面”将显示所有“错误”消息。 如果要显示更多日志消息，您需要配置具有相应日志级别的日志记录器。

日志消息使用内存日志附加器中的，因此与日志文件无关。 另一个结果是，更改此UI中的日志级别不会更改传统日志文件中记录的信息。 在此UI中添加和删除日志记录器将仅影响内存日志记录器中的。 另外，请注意，更改日志记录器配置将反映在内存日志记录器的将来 — 已记录且不再相关的条目不会删除，但类似条目将来不会记录。

您可以通过在UI的左上角齿轮按钮中提供日志记录器配置来配置日志记录内容。 在此，您可以添加、删除或更新日志记录器配置。 日志记录器配置由&#x200B;**日志级别**（警告/信息/调试）和&#x200B;**筛选器名称**&#x200B;组成。 **筛选器名称**&#x200B;具有筛选日志消息源的角色。 或者，如果日志记录器应捕获指定级别的所有日志消息，则筛选器名称应为“**root**”。 设置日志记录器的级别将触发所有消息的捕获，其级别等于或大于指定的级别。

示例：

* 如果您计划捕获所有&#x200B;**ERROR**&#x200B;消息，则无需配置。 默认情况下会捕获所有错误消息。
* 如果您计划捕获所有&#x200B;**ERROR**、**WARN**&#x200B;和&#x200B;**INFO**&#x200B;消息，则应将日志记录器名称设置为：&quot;**root**&quot;，日志记录器级别为：**信息**。

* 如果您计划捕获来自特定包（例如com.adobe.granite）的所有消息，则应将日志记录器名称设置为：&quot;com.adobe.granite&quot;，并且日志记录器级别为：**DEBUG**（这将捕获所有&#x200B;**ERROR**、**WARN**、**INFO**&#x200B;和&#x200B;**DEBUG**&#x200B;消息），如下图所示。

![chlimage_1-121](assets/chlimage_1-121.png)

>[!NOTE]
>
>您无法设置记录器名称来通过指定的过滤器仅捕获错误消息。 默认情况下，会捕获所有错误消息。

>[!NOTE]
>
>日志消息用户界面未反映实际错误日志。 除非您在UI中配置其他类型的日志消息，否则您将只看到错误消息。 有关如何显示特定日志消息的信息，请参阅上面的说明。

>[!NOTE]
>
>诊断页面中的设置不会影响记录到日志文件的内容，反之亦然。 因此，虽然错误日志可能会捕获信息消息，但您可能在日志消息UI中看不到它们。 此外，通过UI，可以从某些包中捕获DEBUG消息，而不会影响错误日志。 有关如何配置日志文件的更多信息，请参阅[日志记录](/help/sites-deploying/configure-logging.md)。

>[!NOTE]
>
>**在AEM 6.4**&#x200B;中，维护任务在“信息”级别以更丰富的格式记录在案。这样可更好地查看维护任务的状态。
>
>如果您使用第三方工具（如Splunk）来监视维护任务活动并对其做出反应，则可以使用以下日志语句：

```
Log level: INFO
DATE+TIME [MaintanceLogger] Name=<MT_NAME>, Status=<MT_STATUS>, Time=<MT_TIME>, Error=<MT_ERROR>, Details=<MT_DETAILS>
```

### 请求性能{#request-performance}

“请求性能”页面允许分析处理最慢的页面请求。 此页面上将仅注册内容请求。 更具体地说，将捕获以下请求：

1. 访问`/content`下的资源的请求
1. 访问`/etc/design`下的资源的请求
1. 具有`".html"`扩展的请求

![chlimage_1-122](assets/chlimage_1-122.png)

此时将显示页面：

* 发出请求的时间
* URL和请求方法
* 持续时间（以毫秒为单位）

默认情况下，会捕获最慢的20个页面请求，但可以在配置管理器中修改此限制。

### 查询性能{#query-performance}

“查询性能”页允许分析系统执行的最慢查询。 此信息由JMX Mbean中的存储库提供。 在Jackrabbit中，`com.adobe.granite.QueryStat` JMX Mbean会提供此信息，而在Oak存储库中，`org.apache.jackrabbit.oak.QueryStats.`提供此信息

此时将显示页面：

* 进行查询的时间
* 查询的语言
* 发出查询的次数
* 查询语句
* 持续时间（以毫秒为单位）

![chlimage_1-123](assets/chlimage_1-123.png)

### 说明查询 {#explain-query}

对于任何给定的查询，Oak会尝试根据存储库中&#x200B;**oak:index**&#x200B;节点下定义的Oak索引来找出最佳的执行方式。 根据查询，Oak可能会选择不同的索引。 了解Oak如何执行查询是优化查询的第一步。

Explain Query是一个工具，用于说明Oak如何执行查询。 可以从AEM欢迎屏幕中转到&#x200B;**工具 — 操作 — 诊断**，然后单击&#x200B;**查询性能**&#x200B;并切换到&#x200B;**解释查询**&#x200B;选项卡，以访问查询。

**功能**

* 支持Xpath、JCR-SQL和JCR-SQL2查询语言
* 报告提供查询的实际执行时间
* 检测慢速查询并警告可能慢速的查询
* 报告用于执行查询的Oak索引
* 显示Oak查询引擎的实际说明
* 提供慢速和热门查询的点进加载列表

进入Explain Query UI后，要使用它，您只需输入查询并按&#x200B;**Explain**&#x200B;按钮即可：

![chlimage_1-124](assets/chlimage_1-124.png)

“查询说明”部分的第一个条目是实际说明。 说明将显示用于执行查询的索引类型。

第二项是执行计划。

运行查询前，按键勾选&#x200B;**包含执行时间**&#x200B;框还将显示查询在中执行的时间，以便提供可用于优化应用程序或部署索引的更多信息。

![chlimage_1-125](assets/chlimage_1-125.png)

### 索引管理器{#the-index-manager}

索引管理器的目的是促进索引管理，如维护索引或查看其状态。

可以从欢迎屏幕中转到**工具 — 操作 — 诊断**，然后单击&#x200B;**索引管理器**&#x200B;按钮，以访问该库。

也可以通过以下URL直接访问该域：`https://serveraddress:port/libs/granite/operations/content/diagnosistools/indexManager.html`

![screenshot_2019-06-18at154754](assets/screen-shot_2019-06-18at154754.png)

UI可用于筛选表格中的索引，方法是在屏幕左上角的搜索框中键入筛选条件。

### 下载状态ZIP {#download-status-zip}

这将触发下载包含系统状态和配置有用信息的zip文件。 存档包含实例配置、包列表、OSGi、Sling量度和统计信息，这可能会生成大文件。 使用&#x200B;**下载状态ZIP**&#x200B;窗口，可以减少大型状态文件的影响。 该窗口可从以下位置访问：**AEM >工具>操作>诊断>下载状态ZIP。**

在此窗口中，您可以选择要导出的内容（日志文件和线程转储）以及下载中包含的相对于当前日期的日志天数。

![download_status_zip](assets/download_status_zip.png)

### 下载线程转储{#download-thread-dump}

这将触发下载包含系统中存在线程信息的zip文件。 提供了每个线程的信息，如其状态、类加载器和堆栈跟踪。

### 下载堆转储{#download-heap-dump}

您还能够下载堆的快照，以便在以后分析它。 请注意，这将触发大文件的下载（以百兆字节为单位）。

## 自动维护任务{#automated-maintenance-tasks}

在“自动维护任务”页面中，您可以查看和跟踪计划定期执行的推荐维护任务。 任务与运行状况检查系统集成。 任务也可以从界面手动执行。

要转到“操作”功能板中的“维护”页面，您需要从“AEM欢迎”屏幕转到&#x200B;**工具 — 操作 — 功能板 — 维护**，或直接访问以下链接：

`https://serveraddress:port/libs/granite/operations/content/maintenance.html`

操作功能板中提供以下任务：

1. **修订清理**&#x200B;任务，位于&#x200B;**每日维护窗口**&#x200B;菜单下。
1. **Lucene二进制文件清理**&#x200B;任务，位于&#x200B;**每日维护窗口**&#x200B;菜单下。
1. 位于&#x200B;**每周维护窗口**&#x200B;菜单下的&#x200B;**工作流清除**&#x200B;任务。
1. **数据存储垃圾收集**&#x200B;任务，位于&#x200B;**每周维护窗口**&#x200B;菜单下。
1. **审核日志维护**&#x200B;任务，位于&#x200B;**每周维护窗口**&#x200B;菜单下。
1. **版本清除维护**&#x200B;任务，位于&#x200B;**每周维护窗口**&#x200B;菜单下。

每日维护时段的默认时间为凌晨2点到5点。 在每周维护时段内配置的任务将在星期六凌晨1点到2点之间执行。

您还可以通过按下两个维护卡中任意一个上的齿轮图标来配置计时：

![chlimage_1-126](assets/chlimage_1-126.png)

>[!NOTE]
>
>自AEM 6.1起，还可以将现有维护窗口配置为每月运行。

### 修订清理 {#revision-clean-up}

有关执行修订清理的详细信息，请[参阅此专述文章](/help/sites-deploying/revision-cleanup.md)。

### Lucene 二进制文件清理 {#lucene-binaries-cleanup}

通过使用Lucene二进制文件清理任务，可以清除lucene二进制文件并减少正在运行的数据存储大小要求。 这是因为Lucene的二进制流失率将每天重新声明，而不是先前对成功运行[数据存储垃圾收集](/help/sites-administering/data-store-garbage-collection.md)的依赖。

虽然开发维护任务是为了减少与Lucene相关的修订垃圾，但运行该任务时总体效率上有所提高：

* 每周执行数据存储垃圾收集任务将更快地完成
* 它还可能会略微提高整体AEM性能

您可以从以下位置访问Lucene二进制文件清理任务：**AEM >工具>操作>维护>每日维护窗口> Lucene二进制文件清理**。

### 数据存储垃圾收集 {#data-store-garbage-collection}

有关数据存储垃圾收集的详细信息，请参阅专用的[文档页面](/help/sites-administering/data-store-garbage-collection.md)。

### 工作流清除{#workflow-purge}

也可以从维护功能板中清除工作流。 要运行“工作流清除”任务，您需要：

1. 单击&#x200B;**每周维护窗口**&#x200B;页面。
1. 在下一页，单击&#x200B;**工作流清除**&#x200B;卡中的&#x200B;**播放**&#x200B;按钮。

>[!NOTE]
>
>有关工作流维护的详细信息，请参阅[此页面](/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances)。

### 审核日志维护{#audit-log-maintenance}

有关审核日志维护，请参阅单独的文档页面[。](/help/sites-administering/operations-audit-log.md)

### 版本清除 {#version-purge}

您可以计划“版本清除”维护任务以自动删除旧版本。 因此，这可以最大限度地减少手动使用[版本清除工具](/help/sites-deploying/version-purging.md)的需要。 您可以通过访问&#x200B;**工具>操作>维护>每周维护窗口**&#x200B;并执行以下步骤来计划和配置版本清除任务：

1. 单击&#x200B;**Add**&#x200B;按钮。
1. 从下拉菜单中选择&#x200B;**版本清除**。

   ![version_purge_maintenancetask](assets/version_purge_maintenancetask.png)

1. 要配置“版本清除”任务，请单击新创建的“版本清除”维护卡上的&#x200B;**齿轮**&#x200B;图标。

   ![version_purge_taskconfiguration](assets/version_purge_taskconfiguration.png)

**在AEM 6.4中**，您可以按如下方式停止“版本清除”维护任务：

* 自动 — 如果计划维护窗口在任务完成之前关闭，则任务会自动停止。 在下一个维护窗口打开时，系统将恢复运行。
* 手动 — 要手动停止任务，请在版本清除维护卡上单击&#x200B;**停止**&#x200B;图标。 下次执行时，任务将安全地恢复。

>[!NOTE]
>
>停止维护任务意味着暂停其执行，而不丢失已在进行中的作业的跟踪。

>[!CAUTION]
>
>为了优化存储库大小，您应经常运行版本清除任务。 当流量有限时，应将任务安排在工作时间之外。

## 自定义维护任务{#custom-maintenance-tasks}

自定义维护任务可以作为OSGi服务实施。 由于维护任务基础架构基于Apache Sling的作业处理，因此维护任务必须实施java接口` [org.apache.sling.event.jobs.consumer.JobExecutor](https://sling.apache.org/apidocs/sling7/org/apache/sling/event/jobs/consumer/JobExecutor.html)`。 此外，它必须声明若要作为维护任务检测的多个服务注册属性，如下所示：

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
   <td>布尔属性，用于定义用户是否可以停止任务。 如果任务声明其可停止，则必须在其执行期间检查其是否已停止，然后相应地执行。 默认值为false。</td>
   <td>true</td>
   <td>可选</td>
  </tr>
  <tr>
   <td>granite.maintenance.mandatory</td>
   <td>布尔属性，用于定义任务是否是必备任务，并且必须定期运行。 如果任务是必备任务，但当前不在任何活动的计划窗口中，则运行状况检查会将此报告为错误。 默认值为false。</td>
   <td>true</td>
   <td>可选</td>
  </tr>
  <tr>
   <td>granite.maintenance.name</td>
   <td>任务的唯一名称 — 此名称用于引用任务。 这通常是一个简单的名称。</td>
   <td>MyMaintenanceTask</td>
   <td>必填</td>
  </tr>
  <tr>
   <td>granite.maintenance.title</td>
   <td>为此任务显示的标题</td>
   <td>我的特殊维护任务</td>
   <td>必填</td>
  </tr>
  <tr>
   <td>job.topics</td>
   <td>这是维护任务的一个独特主题。<br /> Apache Sling作业处理将启动一个正好具有此主题的作业，以执行维护任务，并在为此主题注册任务时执行该任务。<br /> 本主题必须以 <i>com/adobe/granite/maintenance/job/开头</i></td>
   <td>com/adobe/granite/maintenance/job/MyMaintenanceTask</td>
   <td>必填</td>
  </tr>
 </tbody>
</table>

除了上述服务属性之外，还需要通过添加维护任务应执行的代码来实现`JobConsumer`接口的`process()`方法。 提供的`JobExecutionContext`可用于输出状态信息、检查用户是否停止了作业并创建结果（成功或失败）。

如果维护任务不应在所有安装上运行（例如，仅在发布实例上运行），则可以通过添加`@Component(policy=ConfigurationPolicy.REQUIRE)`使服务需要配置才能处于活动状态。 然后，您可以根据存储库中的运行模式，将相应的配置标记为。 有关更多信息，请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md#creating-the-configuration-in-the-repository)。

下面是一个自定义维护任务的示例，该任务从过去24小时内已修改的可配置临时目录中删除文件：

src/main/java/com/adobe/granite/samples/maintenance/impl/DeleteTempFilesTask.java

<table>
 <tbody>
  <tr>
   <td><p> </p> <p><code>/*</code></p> <p><code> * #%L</code></p> <p><code> * sample-maintenance-task</code></p> <p><code> * %%</code></p> <p><code> * Copyright (C) 2014 Adobe</code></p> <p><code> * %%</code></p> <p><code> * Licensed under the Apache License, Version 2.0 (the "License");</code></p> <p><code> * you may not use this file except in compliance with the License.</code></p> <p><code> * You may obtain a copy of the License at</code></p> <p><code> * </code></p> <p><code> * <a href="https://www.apache.org/licenses/LICENSE-2.0">https://www.apache.org/licenses/LICENSE-2.0</a></code></p> <p><code> * </code></p> <p><code> * Unless required by applicable law or agreed to in writing, software</code></p> <p><code> * distributed under the License is distributed on an "AS IS" BASIS,</code></p> <p><code> * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.</code></p> <p><code> * See the License for the specific language governing permissions and</code></p> <p><code> * limitations under the License.</code></p> <p><code> * #L%</code></p> <p><code> */</code></p> <p><code> </code></p> <p><code>package com.adobe.granite.samples.maintenance.impl;</code></p> <p><code> </code></p> <p><code>import java.io.File;</code></p> <p><code>import java.util.Calendar;</code></p> <p><code>import java.util.Collection;</code></p> <p><code>import java.util.Map;</code></p> <p><code> </code></p> <p><code>import org.apache.commons.io.FileUtils;</code></p> <p><code>import org.apache.commons.io.filefilter.IOFileFilter;</code></p> <p><code>import org.apache.commons.io.filefilter.TrueFileFilter;</code></p> <p><code>import org.apache.felix.scr.annotations.Activate;</code></p> <p><code>import org.apache.felix.scr.annotations.Component;</code></p> <p><code>import org.apache.felix.scr.annotations.Properties;</code></p> <p><code>import org.apache.felix.scr.annotations.Property;</code></p> <p><code>import org.apache.felix.scr.annotations.Service;</code></p> <p><code>import org.apache.sling.commons.osgi.PropertiesUtil;</code></p> <p><code>import org.apache.sling.event.jobs.Job;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobConsumer;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobExecutionContext;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobExecutionResult;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobExecutor;</code></p> <p><code>import org.slf4j.Logger;</code></p> <p><code>import org.slf4j.LoggerFactory;</code></p> <p><code> </code></p> <p><code>import com.adobe.granite.maintenance.MaintenanceConstants;</code></p> <p><code> </code></p> <p><code>@Component(metatype = true,</code></p> <p><code> label = "Delete Temp Files Maintenance Task",</code></p> <p><code> description = "Maintatence Task which deletes files from a configurable temporary directory which have been modified in the last 24 hours.")</code></p> <p><code>@Service</code></p> <p><code>@Properties({</code></p> <p><code> @Property(name = MaintenanceConstants.PROPERTY_TASK_NAME, value = "DeleteTempFilesTask", propertyPrivate = true),</code></p> <p><code> @Property(name = MaintenanceConstants.PROPERTY_TASK_TITLE, value = "Delete Temp Files", propertyPrivate = true),</code></p> <p><code> @Property(name = JobConsumer.PROPERTY_TOPICS, value = MaintenanceConstants.TASK_TOPIC_PREFIX</code></p> <p><code> + "DeleteTempFilesTask", propertyPrivate = true) })</code></p> <p><code>public class DeleteTempFilesTask implements JobExecutor {</code></p> <p><code> </code></p> <p><code> private static final Logger log = LoggerFactory.getLogger(DeleteTempFilesTask.class);</code></p> <p><code> </code></p> <p><code> @Property(label = "Temporary Directory", description="Temporary Directory. Defaults to the java.io.tmpdir system property.")</code></p> <p><code> private static final String PROP_TEMP_DIR = "temp.dir";</code></p> <p><code> </code></p> <p><code> private File tempDir;</code></p> <p><code> </code></p> <p><code> @Activate</code></p> <p><code> private void activate(Map&lt;string, object=""&gt; properties) {</code></p> <p><code> this.tempDir = new File(PropertiesUtil.toString(properties.get(PROP_TEMP_DIR),</code></p> <p><code> System.getProperty("java.io.tmpdir")));</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> @Override</code></p> <p><code> public JobExecutionResult process(Job job, JobExecutionContext context) {</code></p> <p><code> log.info("Deleting old temp files from {}.", tempDir.getAbsolutePath());</code></p> <p><code> Collection&lt;file&gt; files = FileUtils.listFiles(tempDir, new LastModifiedBeforeYesterdayFilter(),</code></p> <p><code> TrueFileFilter.INSTANCE);</code></p> <p><code> int counter = 0;</code></p> <p><code> for (File file : files) {</code></p> <p><code> log.debug("Deleting file {}.", file.getAbsolutePath());</code></p> <p><code> counter++;</code></p> <p><code> file.delete();</code></p> <p><code> // TODO - capture the output of delete() and do something useful with it</code></p> <p><code> }</code></p> <p><code> return context.result().message(String.format("Deleted %s files.", counter)).succeeded();</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> /**</code></p> <p><code> * IOFileFilter which filters out files which have been modified in the last 24 hours.</code></p> <p><code> *</code></p> <p><code> */</code></p> <p><code> private static class LastModifiedBeforeYesterdayFilter implements IOFileFilter {</code></p> <p><code> </code></p> <p><code> private final long minTime;</code></p> <p><code> </code></p> <p><code> private LastModifiedBeforeYesterdayFilter() {</code></p> <p><code> Calendar cal = Calendar.getInstance();</code></p> <p><code> cal.add(Calendar.DATE, -1);</code></p> <p><code> this.minTime = cal.getTimeInMillis();</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> @Override</code></p> <p><code> public boolean accept(File dir, String name) {</code></p> <p><code> // this method is never actually called.</code></p> <p><code> return false;</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> @Override</code></p> <p><code> public boolean accept(File file) {</code></p> <p><code> return file.lastModified() <= this.minTime;</code></p> <p><code> }</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code>}</code></p> <p><code>&lt;file&gt;&lt;/string,&gt;</code></p> <p> </p> </td>
  </tr>
 </tbody>
</table>

[experiencemanager-java-maintenancetask-sample](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-maintenancetask-sample) -  [src/main/java/com/adobe/granite/samples/maintenance/impl/DeleteTempFilesTask.java](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-maintenancetask-sample/blob/master/src/main/java/com/adobe/granite/samples/maintenance/impl/DeleteTempFilesTask.java)

部署服务后，该服务会显示在操作功能板UI中。 您可以将其添加到一个可用的维护计划中：

![chlimage_1-127](assets/chlimage_1-127.png)

这将在/apps/granite/operations/config/maintenance/`schedule`/`taskname`添加相应的资源。 如果任务与运行模式相关，则需要在该节点上设置granite.operations.conditions.runmode属性，其中包含运行模式值，该运行模式值需要为此维护任务处于活动状态。

## 系统概览 {#system-overview}

**系统概述功能板**&#x200B;显示AEM实例的配置、硬件和运行状况的高级概述。 这意味着系统运行状况状态是透明的，所有信息都会汇总到一个仪表板中。

>[!NOTE]
>
>您还可以[观看此视频](https://video.tv.adobe.com/v/21340)，了解系统概述功能板的简介。

### 如何访问{#how-to-access}

要访问“系统概述”功能板，请导航至&#x200B;**工具>操作>系统概述**。

![system_overview_dashboard](assets/system_overview_dashboard.png)

### 系统概述功能板说明{#system-overview-dashboard-explained}

下表描述了“系统概述”功能板中显示的所有信息。 请记住，当没有可显示的相关信息（例如，备份未进行，没有关键的运行状况检查）时，相应部分将显示“无条目”消息。

您还可以通过单击功能板右上角的&#x200B;**Download**&#x200B;按钮来下载汇总功能板信息的`JSON`文件。`JSON`端点为`/libs/granite/operations/content/systemoverview/export.json`，可用于`curl`脚本中进行外部监控。

<table>
 <tbody>
  <tr>
   <td><strong>区域</strong></td>
   <td><strong>显示哪些信息</strong></td>
   <td><strong>何时至关重要</strong></td>
   <td><strong>链接到</strong></td>
  </tr>
  <tr>
   <td>运行状况检查</td>
   <td>
    <ul>
     <li>处于关键状态的检查列表</li>
     <li>处于警告状态的检查列表</li>
    </ul> </td>
   <td>直观指示：<br />
    <ul>
     <li>关键检查的红色标记</li>
     <li>用于警告检查的橙色标记</li>
    </ul> </td>
   <td>
    <ul>
     <li>运行状况报表页面</li>
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
   <td><p>直观地指示：</p>
    <ul>
     <li>失败任务的红色标记</li>
     <li>用于运行任务的橙色标记（因为它们可能会影响性能）</li>
     <li>其他每个状态均显示灰色标记</li>
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
     <li>操作系统和操作系统版本（例如Mac OS X）</li>
     <li>系统负载平均值，从<a href="https://docs.oracle.com/javase/8/docs/api/java/lang/management/OperatingSystemMXBean.html#getSystemLoadAverage--">OperatingSystemMXBeanusable</a>检索</li>
     <li>磁盘空间（在主目录所在的分区上）</li>
     <li>最大堆，由<a href="https://docs.oracle.com/javase/8/docs/api/java/lang/management/MemoryMXBean.html#getHeapMemoryUsage--">MemoryMXBean</a>返回</li>
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
     <li>实例启动的日期</li>
    </ul> </td>
   <td>不适用</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>存储库</td>
   <td>
    <ul>
     <li>Oak版本</li>
     <li>节点存储类型（区段Tar或文档）
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
     <li>如果没有自定义外部数据存储，则会显示一条消息，指示此事实</li>
    </ul> </td>
   <td>不适用</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>分发代理</td>
   <td>
    <ul>
     <li>队列被阻止的代理列表</li>
     <li>配置错误的代理的列表（“配置错误”）</li>
     <li>暂停队列处理的代理列表</li>
     <li>空闲代理的列表</li>
     <li>运行的代理（当前正在处理条目）列表</li>
    </ul> </td>
   <td><p>直观地指示：</p>
    <ul>
     <li>已阻止的代理或配置错误的红色标记</li>
     <li>暂停代理的橙色标记</li>
     <li>已暂停、空闲或正在运行的代理的灰色标记<br /> </li>
    </ul> </td>
   <td>分发页面<br /> </td>
  </tr>
  <tr>
   <td>复制代理</td>
   <td>
    <ul>
     <li>队列被阻止的代理列表</li>
     <li>空闲代理的列表</li>
     <li>运行的代理（当前正在处理条目）列表</li>
    </ul> </td>
   <td><p>直观指示：<br /> </p>
    <ul>
     <li>被阻止的代理的红色标记</li>
     <li>暂停的代理的灰色标记</li>
    </ul> </td>
   <td>“复制”页</td>
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
     <li>工作流计数 — 处于给定状态的工作流数（如果有）：
      <ul>
       <li>运行</li>
       <li>失败</li>
       <li>暂停</li>
       <li>中止</li>
      </ul> </li>
    </ul> <p>对于上面显示的每种状态，将执行查询，其时间限制为400毫秒。 在400毫秒处，将显示截至该时间点获取的条目数。</p> </td>
   <td><p>未解释：</p>
    <ul>
     <li>当存在处于意外状态的工作流和作业时，用户应当进行调查。</li>
    </ul> </td>
   <td>“工作流失败”页</td>
  </tr>
  <tr>
   <td>Sling 作业</td>
   <td><p>Sling作业计数 — 处于给定状态的作业数（如果有）：</p>
    <ul>
     <li>失败</li>
     <li>已排队</li>
     <li>已取消</li>
     <li>活动</li>
    </ul> </td>
   <td><p>未解释：</p>
    <ul>
     <li>当存在处于意外状态或计数较高的作业时，用户应进行调查。</li>
    </ul> </td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>预计节点计数</td>
   <td><p>估计数：</p>
    <ul>
     <li>页</li>
     <li>资产</li>
     <li>标记</li>
     <li>可授权</li>
     <li>节点总数<br /> </li>
    </ul> <p>节点总数从nodeCounterMBean获取，其余的统计信息则从IndexInfoService获取。</p> </td>
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
