---
title: 硬件大小调整准则
description: 这些大小调整指南提供了部署AEM项目所需硬件资源的大致情况。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing
content-type: reference
docset: aem65
exl-id: 5837ef4f-d4e0-49d7-a671-87d5547e0d98
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2798'
ht-degree: 1%

---

# 硬件大小调整准则{#hardware-sizing-guidelines}

这些大小调整指南提供了部署AEM项目所需硬件资源的大致情况。 规模估计取决于项目的体系结构、解决方案的复杂性、预期流量和项目要求。 本指南可帮助您确定特定解决方案的硬件需求，或查找硬件需求的上下限估计。

要考虑的基本因素包括（按此顺序）：

* **网络速度**

   * 网络延迟
   * 可用带宽

* **计算速度**

   * 缓存效率
   * 预期流量
   * 模板、应用程序和组件的复杂性
   * 并发作者
   * 创作操作的复杂性（简单内容编辑、MSM转出等）

* **I/O性能**

   * 文件或数据库存储的性能和效率

* **硬盘**

   * 至少比存储库大小大两到三倍

* **内存**

   * 网站的大小（内容对象、页面和用户的数量）
   * 同时处于活动状态的用户/会话数

## 架构 {#architecture}

典型的AEM设置包括创作环境和发布环境。 这些环境对底层硬件大小和系统配置有不同的要求。 有关这两种环境的详细注意事项，请参见 [创作环境](/help/managing/hardware-sizing-guidelines.md#author-environment-specific-calculations) 和 [发布环境](/help/managing/hardware-sizing-guidelines.md#publish-environment-specific-calculations) 部分。

在典型项目设置中，您有多个环境可在其上暂存项目阶段：

* **开发环境**
开发新功能或进行重大更改。 最佳实践是为每个开发人员使用开发环境（在其个人系统上本地安装）。

* **创作测试环境**
验证更改。 测试环境的数量因项目要求而异（例如，QA、集成测试或用户验收测试不同）。

* **发布测试环境**
主要用于测试Social Collaboration用例和/或作者与多个发布实例之间的交互。

* **创作生产环境**
供作者编辑内容。

* **发布生产环境**
用于提供已发布的内容。

此外，环境可能有所不同，从运行AEM的单服务器系统和应用程序服务器，到高度扩展的多服务器、多CPU群集实例集。 Adobe建议您为每个生产系统使用单独的计算机，并且不要在这些计算机上运行其他应用程序。

## 一般硬件大小调整注意事项 {#generic-hardware-sizing-considerations}

以下各节提供了有关如何计算硬件需求的指导，其中将考虑各种因素。 对于大型系统，Adobe建议您在参考配置上执行一组简单的内部基准测试。

性能优化是一项基本任务，在完成特定项目的基准测试之前需要执行这项任务。 请务必遵循 [性能优化文档](/help/sites-deploying/configuring-performance.md) 执行任何基准测试并将其结果用于任何硬件大小计算之前。

高级用例的硬件规模要求需要基于对项目的详细性能评估。 需要卓越硬件资源的高级用例的特性包括以下组合：

* 高内容有效负荷/吞吐量
* 广泛使用自定义代码、自定义工作流或第三方软件库
* 与不受支持的外部系统集成

### 磁盘空间/硬盘 {#disk-space-hard-drive}

所需的磁盘空间在很大程度上取决于Web应用程序的卷和类型。 计算时应考虑以下因素：

* 页面、资产和其他存储库存储的实体（如工作流、配置文件等）的数量和大小。
* 估计的内容更改频率，从而创建内容版本
* 将生成的DAM资源演绎版数量
* 随着时间的推移，内容的总体增长

在“联机”和“脱机”版本清理期间，会持续监视磁盘空间。 如果可用磁盘空间下降到临界值以下，则该过程将取消。 关键值是存储库当前磁盘占用空间的25%，无法对其进行配置。 Adobe建议磁盘大小至少比存储库大小（包括预计增长量）大两到三倍。

考虑设置独立磁盘冗余阵列（例如RAID10）以实现数据冗余。

>[!NOTE]
>
>生产实例的临时目录应至少具有6 GB可用空间。

#### 虚拟化 {#virtualization}

AEM在虚拟化环境中运行良好，但可能存在CPU或I/O等无法直接等同于物理硬件的因素。 建议选择更高的I/O速度（通常），因为这是关键因素。 设定环境基准对于准确了解所需资源是必不可少的。

#### AEM实例的并行化 {#parallelization-of-aem-instances}

**失败安全性**

一个防故障的网站至少部署在两个独立的系统上。 如果一个系统发生故障，另一个系统可以接管并补偿系统故障。

**系统资源可扩展性**

当所有系统都在运行时，可以增强计算性能。 这种额外性能不一定与群集节点数量成线性关系，因为这种关系在很大程度上取决于技术环境。 请参阅 [群集文档](/help/sites-deploying/recommended-deploys.md) 以了解更多信息。

根据特定Web项目的基本要求和具体用例，估计需要多少簇节点：

* 从故障安全的角度来看，必须根据群集节点恢复所需的时间来确定所有环境的严重故障程度以及故障补偿时间。
* 在可扩展性方面，写操作的数量基本上是最重要的因素；请参见 [作者并行工作](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel) 创作环境和 [Social Collaboration](/help/managing/hardware-sizing-guidelines.md#socialcollaborationspecificconsiderations) （发布环境）。 可以为仅访问系统的操作建立负载平衡，以处理读取操作；请参阅 [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hans) 以了解详细信息。

## 创作环境特定的计算 {#author-environment-specific-calculations}

为了进行基准测试，Adobe开发了一些用于独立创作实例的基准测试。

* **基准测试1**
计算某个加载配置文件的最大吞吐量，在该配置文件中，用户在300个具有类似性质的现有页面的基础负载之上执行简单的创建页面练习。 所涉及的步骤包括：登录网站，创建包含SWF和图像/文本的页面，添加标记云，然后激活页面。

   * **结果**
发现上述简单页面创建操作（视为一个事务）的最大吞吐量为每小时1730个事务。

* **基准测试2**
当加载配置文件混用创建新页面(10%)、修改现有页面(80%)以及连续创建和修改页面(10%)时，计算最大吞吐量。 页面的复杂性与基准测试1的配置文件中相同。 页面的基本修改是通过添加图像和修改文本内容来完成的。 同样，该练习是在基准测试1中定义的具有相同复杂性的300页基础负载的基础上执行的。

   * **结果**
发现此类混合操作场景的最大吞吐量为每小时3252个事务。

>[!NOTE]
>
>吞吐率不区分负载配置文件中的事务类型。 用于测量吞吐量的方法确保每个事务类型的固定比例包含在工作负载中。

以上两个测试清楚地表明，吞吐率随操作类型而变化。 使用环境上的活动作为调整系统大小的基础。 通过诸如修改之类的不太密集的操作（这也比较常见），您将获得更好的吞吐量。

### 缓存 {#caching}

在创作环境中，缓存效率通常要低得多，因为对网站的更改更频繁，并且内容高度交互性和个性化。 使用Dispatcher，您可以缓存AEM库、JavaScript、CSS文件和布局图像。 这样可以加快创作过程的某些方面。 通过配置Web服务器，还可以在这些资源上设置用于浏览器缓存的标头，从而减少HTTP请求的数量，从而提高系统响应速度，就像作者所体验的那样。

### 作者并行工作 {#authors-working-in-parallel}

在作者环境中，并行工作的作者数量和他们交互作用添加到系统的负载是主要限制因素。 因此，Adobe建议您根据共享数据吞吐量来扩展系统。

对于此类情况，Adobe在创作实例的双节点非共享集群上运行基准测试。

* **基准测试1a**
使用包含2个创作实例的active-active shared-nothing集群，使用负载配置文件计算最大吞吐量，其中用户在300个现有页面（所有页面都具有类似性质）的基本负载的基础上执行简单的创建页面练习。

   * **结果**
一个简单的页面创建练习（如上面的）（视为一个事务）的最大吞吐量是2016事务/小时。 与同一基准测试的独立创作实例相比，大约提高了16%。

* **基准测试2b**
使用2个创作实例的active-active shared-nothing集群，计算当加载配置文件混合创建新页面创建(10%)、修改现有页面(80%)以及连续创建和修改页面(10%)时的最大吞吐量。 页面的复杂性与基准测试1的配置文件中相同。 页面的基本修改是通过添加图像和修改文本内容来完成的。 同样，该练习是在具有300个复杂度的基本负载之上执行的，这些复杂度的定义与基准测试1中的定义相同。

   * **结果**
发现这种混合操作方案的最大吞吐量为每小时6288个事务。 与同一基准测试的独立创作实例相比，大约提高了93%。

>[!NOTE]
>
>吞吐率不区分负载配置文件中的事务类型。 用于测量吞吐量的方法确保每个事务类型的固定比例包含在工作负载中。

以上两项测试清楚地表明，对于使用AEM执行基本编辑操作的作者，AEM可以很好地扩展。 通常，AEM在缩放读取操作方面最有效。

在典型的网站上，大多数创作都是在项目阶段进行的。 网站上线后，并行工作的作者数量通常降至较低（操作模式）的平均值。

您可以按如下方式计算创作环境所需的计算机（或CPU）数量：

`n = numberOfParallelAuthors / 30`

当作者使用AEM执行基本操作时，此公式可用作缩放CPU的常规准则。 它假定系统和应用程序已优化。 但是，公式对于MSM或Assets等高级功能不成立（请参阅以下部分）。

另请参阅 [并行化](/help/managing/hardware-sizing-guidelines.md#parallelization-of-aem-instances) 和 [性能优化](/help/sites-deploying/configuring-performance.md).

### 硬件Recommendations {#hardware-recommendations}

通常，您可以按照为发布环境推荐的方式，对创作环境使用相同的硬件。 通常，创作系统上的网站流量要低得多，但缓存效率也较低。 但是，这里的基本因素是并行工作的作者数量以及对系统采取的操作类型。 一般来说，（创作环境的）AEM聚类在缩放读取操作方面最有效；换句话说，AEM聚类与执行基本编辑操作的作者一起缩放效果较好。

Adobe时的基准测试是使用Red Hat® 5.5操作系统进行的，该操作系统运行于Hewlett-Packard ProLiant DL380 G5硬件平台，具有以下配置：

* 两个四核英特尔至强® X5450 CPU，3.00 GHz
* 8 GB RAM
* Broadcom NetXtreme II BCM5708千兆以太网
* HP智能阵列RAID控制器，256 MB高速缓存
* 两个146 GB 10,000-RPM SAS磁盘配置为RAID0条带集
* SPEC CINT2006费率基准得分是110

AEM实例运行时的最小栈大小为256M，最大栈大小为1024M。

## 发布特定于环境的计算 {#publish-environment-specific-calculations}

### 缓存效率和流量 {#caching-efficiency-and-traffic}

缓存效率对于网站运行速度至关重要。 下表显示了优化的AEM系统每秒可以使用反向代理（如Dispatcher）处理的页面数：

| 缓存比率 | 页数/秒（峰值） | 百万页/天（平均） |
|---|---|---|
| 100% | 1000-2000 | 35-70 |
| 99% | 910 | 32 |
| 95% | 690 | 25 |
| 90% | 520 | 18 |
| 60% | 220 | 8 |
| 0% | 100 | 3.5 |

>[!CAUTION]
>
>免责声明：这些数字基于默认硬件配置，可能会因使用的特定硬件而异。

缓存比率是Dispatcher在无需访问AEM的情况下可以返回的页面百分比。 100%表示Dispatcher应答所有请求，0%表示AEM计算每个页面。

### 模板和应用程序的复杂性 {#complexity-of-templates-and-applications}

如果您使用复杂的模板，AEM将需要更多时间来渲染页面。 从缓存中获取的页面不受此影响，但在考虑整体响应时间时，页面大小仍然相关。 渲染复杂页面所花费的时间很容易比渲染简单页面多十倍。

### 公式 {#formula}

使用以下公式，您可以计算AEM解决方案总体复杂性的估计值：

`complexity = applicationComplexity + ((1-cacheRatio) * templateComplexity)`

根据复杂性，您可以确定发布环境所需的服务器（或CPU内核）数量，如下所示：

`n = (traffic * complexity / 1000 ) * activations`

此方程式中的变量如下：

<table>
 <tbody>
  <tr>
   <td>流量</td>
   <td>预计的每秒峰值流量。 您可以将其估计为每日页面点击数除以35,000。</td>
  </tr>
  <tr>
   <td>应用程序复杂性</td>
   <td><p>对于简单应用程序，请使用1；对于复杂应用程序，请使用2；对于中间值，请使用：</p>
    <ul>
     <li>1 — 完全匿名、以内容为导向的网站</li>
     <li>1.1 — 完全匿名、以内容为导向的站点，具有客户端/Target个性化</li>
     <li>1.5 — 面向内容的网站，具有匿名部分和登录部分，客户端/Target个性化</li>
     <li>1.7 — 面向内容的网站，具有匿名登录部分、客户端/Target个性化以及一些用户生成的内容</li>
     <li>2 — 当整个站点需要登录时，广泛使用用户生成的内容和各种个性化技术</li>
    </ul> </td>
  </tr>
  <tr>
   <td>cacheRatio</td>
   <td>从Dispatcher缓存中传出的页面的百分比。 如果所有页面都来自缓存，则使用1；如果每个页面都由AEM计算，则使用0。</td>
  </tr>
  <tr>
   <td>templateComplex</td>
   <td>使用1到10之间的值表示模板的复杂性。 数字越大表示模板越复杂，值1表示每页平均包含10个组件的网站，值5表示平均包含40个组件的页面，值10表示平均包含100多个组件的网站。</td>
  </tr>
  <tr>
   <td>激活次数</td>
   <td>每小时的平均激活次数（平均大小页面和资产从创作层到发布层的复制）除以x，其中x是在系统上完成的激活次数，对系统处理的其他任务没有性能负面影响。 您还可以预定义悲观的初始值，如x = 100。<br /> </td>
  </tr>
 </tbody>
</table>

如果您拥有更复杂的网站，那么还需要功能更强大的Web服务器，以便AEM能够在可接受的时间内响应请求。

* 复杂性低于4：
   * 1024 MB JVM RAM&#42;
   * 中低性能CPU

* 复杂性从4到8：
   * 2048 MB JVM RAM&#42;
   * 中高性能CPU

* 复杂性高于8：
   * 4096 MB JVM RAM&#42;
   * 高端到高端性能CPU

>[!NOTE]
>
>&#42; 除了JVM所需的内存之外，还可为操作系统保留足够的RAM。

## 其他特定于用例的计算 {#additional-use-case-specific-calculations}

除了计算默认Web应用程序外，您可能需要考虑以下用例的特定因素。 计算值将添加到默认计算中。

### 特定于资产的注意事项 {#assets-specific-considerations}

广泛处理数字资产需要优化的硬件资源，最相关的因素是图像大小和已处理图像的峰值吞吐量。

分配至少16GB的栈并配置 [!UICONTROL DAM更新资产] 使用的工作流 [Camera Raw包](/help/assets/camera-raw.md) 用于摄取原始图像。

>[!NOTE]
>
>较高的图像吞吐量意味着计算资源需要能够跟上系统I/O的速度，反之亦然。 例如，如果通过导入图像来启动工作流，则通过WebDAV上传许多图像可能会导致工作流积压。
>
>为TarPM、数据存储和搜索索引使用单独的磁盘有助于优化系统I/O行为（但是，通常将搜索索引保留在本地是有意义的）。

>[!NOTE]
>
>另请参阅 [Assets性能指南](/help/sites-deploying/assets-performance-sizing.md).

### 多站点管理器 {#multi-site-manager}

在创作环境中使用AEM MSM时的资源消耗在很大程度上取决于特定用例。 基本因素包括：

* 活动副本数
* 转出的周期
* 要转出的内容树大小
* 转出操作的已连接功能

使用具有代表性的内容摘录测试计划的用例，可以帮助您更好地了解资源消耗。 如果使用计划吞吐量推断结果，则可以评估AEM MSM所需的其他资源。

此外，还应说明并行工作的作者。 如果AEM MSM用例消耗的资源多于计划的资源，则他们会感觉到性能副作用。

### AEM Communities大小调整注意事项 {#aem-communities-sizing-considerations}

包含AEM Communities功能的AEM站点（社区站点）会在发布环境中与站点访客（成员）进行高级别的交互。

社区站点的规模调整考虑因素取决于社区成员预期的交互，以及页面内容的最佳性能是否更加重要。

用户生成的内容(UGC)提交的成员与页面内容分开存储。 虽然AEM平台使用将站点内容从创作复制到发布的节点存储区，但AEM Communities使用单个通用存储区来存储从未复制的UGC。

对于UGC存储，需要选择一个影响所选部署的存储资源提供程序(SRP)。
请参阅

* [社区内容存储](/help/communities/working-with-srp.md)
* [推荐的社区拓扑](/help/communities/topologies.md)
