---
title: 性能优化
seo-title: Performance Optimization
description: 了解如何配置AEM的某些方面以优化性能。
seo-description: Learn how to configure certain aspects of AEM to optimize performance.
uuid: a4d9fde4-a4c7-4ee5-99b6-29b0ee7dc35b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 80118cd1-73e1-4675-bbdf-85d66d150abc
feature: Configuring
exl-id: 5b0c9a8c-0f5f-46ee-a455-adb9b9d27270
source-git-commit: 4fc42469e4b97f2f2c5d7489837012d31c63f86d
workflow-type: tm+mt
source-wordcount: '6645'
ht-degree: 14%

---

# 性能优化 {#performance-optimization}

>[!NOTE]
>
>有关性能的一般准则，请阅读 [性能准则](/help/sites-deploying/performance-guidelines.md) 页面。
>
>有关疑难解答和修复性能问题的更多信息，另请参阅 [性能树](/help/sites-deploying/performance-tree.md).
>
>此外，您还可以在 [性能调整提示。](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)

一个关键问题是您的网站响应访客请求所花费的时间。 尽管该值会因每个请求而异，但可以定义平均目标值。 一旦该价值被证明是可实现的且可维护的，便可用于监控网站的性能并指示潜在问题的发展。

在创作和发布环境中，您要针对的响应时间将有所不同，这反映了目标受众的不同特征：

## 创作环境 {#author-environment}

作者可使用此环境输入和更新内容。 更新内容页面和这些页面上的各个元素时，必须满足少数用户的需求，这些用户均会生成大量性能密集型请求。

## 发布环境 {#publish-environment}

此环境包含可供用户使用的内容。 在这里，请求数量更多，速度也同样重要，但由于请求的性质不那么动态，因此可以应用额外的性能提升机制；例如缓存内容或负载平衡。

>[!NOTE]
>
>* 配置以优化性能后，请按照 [艰难的一天](/help/sites-developing/tough-day.md) 来测试环境。
>* 另请参阅 [性能调整提示。](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)


## 性能优化方法 {#performance-optimization-methodology}

AEM项目的性能优化方法可以归纳为五个非常简单的规则，可以遵循这些规则以避免从一开始就出现性能问题：

1. [优化计划](#planning-for-optimization)
1. [模拟现实](#simulate-reality)
1. [确立坚实的目标](#establish-solid-goals)
1. [保持相关性](#stay-relevant)
1. [敏捷迭代周期](#agile-iteration-cycles)

这些规则在很大程度上适用于Web项目，并且与项目经理和系统管理员相关，可确保其项目在启动时不会面临性能挑战。

### 优化计划 {#planning-for-optimization}

![chlimage_1-3](assets/chlimage_1-3.jpeg)

在性能优化阶段，应计划大约10%的项目工作。 当然，实际的性能优化要求将取决于项目的复杂性级别和开发团队的经验。 虽然您的项目可能（最终）不需要所有分配的时间，但最好始终在建议的区域中规划性能优化。

在可能的情况下，首先应向有限的受众软启动项目，以收集实际体验并进一步优化，而无需在发布完整公告后承受额外压力。

“实时”后，性能优化就不会结束。 这是您在系统上体验到“实际”负载的时间点。 在启动后计划进一步调整很重要。

由于系统负载发生变化，并且系统的性能配置文件会随时间而改变，因此应安排6-12个月的时间间隔来进行性能“调整”或“运行状况检查”。

### 模拟现实 {#simulate-reality}

![chlimage_1-4](assets/chlimage_1-4.jpeg)

如果您通过网站上线并在启动后发现遇到性能问题，则只有一个原因：您的负载和性能测试没有足够地模拟现实。

模拟现实是困难的，而您在获得“真实”方面有多大的投入，取决于您项目的性质。 “真实”不仅表示“真实代码”和“真实流量”，还表示“真实内容”，尤其是有关内容大小和结构的内容。 请记住，您的模板可能会因存储库的大小和结构而有完全不同的行为。

### 确立坚实的目标 {#establish-solid-goals}

![chlimage_1-5](assets/chlimage_1-5.jpeg)

正确制定业绩目标的重要性不容低估。 通常，一旦人们专注于具体的绩效目标，就很难在以后改变这些目标，即使这些目标是基于疯狂的假设。

建立良好、稳健的绩效目标确实是最棘手的领域之一。 通常最好从可比较的网站（例如新网站的前身）收集真实生活日志和基准。

### 保持相关性 {#stay-relevant}

![chlimage_1-6](assets/chlimage_1-6.jpeg)

一次优化一个瓶颈很重要。 如果您尝试在不验证某个优化的影响的情况下并行执行某些操作，您将无法跟踪哪个优化措施实际上有帮助。

### 敏捷迭代周期 {#agile-iteration-cycles}

![chlimage_1-7](assets/chlimage_1-7.jpeg)

性能调整是一个迭代过程，包括测量、分析、优化和验证，直到达到目标。 为了正确考虑这一方面，在优化阶段实施灵活的验证过程，而不是在每次迭代后执行更重的测试过程。

这在很大程度上意味着实施优化的开发人员应该能够快速判断优化是否已达到目标。 这是有价值的信息，因为当达到目标时，优化就会结束。

## 基本性能准则 {#basic-performance-guidelines}

通常，将未缓存的html请求保留在100毫秒以下。 更具体地说，以下内容可能是准则：

* 70%的页面请求应在100毫秒内答复。
* 25%的页面请求应在100毫秒至300毫秒内得到响应。
* 4%的页面请求应在300ms-500ms内得到响应。
* 1%的页面请求应在500ms-1000ms内收到响应。
* 任何页面的响应速度都不应低于1秒。

上述数字假定满足以下条件：

* 在发布时测量（没有与创作环境相关的间接费用）
* 在服务器上测量（无网络开销）
* 未缓存(无AEM输出缓存，无Dispatcher缓存)
* 仅适用于具有许多依赖项的复杂项目(HTML、JS、PDF...)
* 系统上没有其他负载

有些问题经常导致性能问题。 这主要围绕：

* 调度程序缓存效率低下
* 在普通显示模板中使用查询。

JVM和操作系统级别的调整通常不会导致性能的大幅提升，因此应在优化周期的最后阶段执行。

内容存储库的结构方式也会影响性能。 为获得最佳性能，附加到内容存储库中各个节点的子节点数不应超过1,000个（作为一般规则）。

在通常的性能优化练习中，您的好友包括：

* 不为目标组件考虑 `request.log`
* 基于组件的计时
* 最后，但不是最后一个Java探查器。

### 加载和编辑数字资产时的性能 {#performance-when-loading-and-editing-digital-assets}

由于加载和编辑数字资产时涉及大量数据，因此性能可能成为一个问题。

以下两点会影响性能：

* CPU — 多个内核使转码时的工作更顺畅
* 硬盘 — 并行RAID磁盘实现相同

要提高性能，您可以考虑以下事项：

* 每天要上传多少个资产？ 您可以基于以下数据做出合理估计：

![chlimage_1-77](assets/chlimage_1-77.png)

* 将进行编辑的时间范围（通常是工作日的时长，对于国际操作而言更多）。
* 上传图像的平均大小（以及每个图像生成的演绎版的大小）(MB)。
* 确定平均数据率：

![chlimage_1-78](assets/chlimage_1-78.png)

* 80%的编辑将在20%的时间内完成，因此在峰值时间，您的数据率将是平均数据率的4倍。 这是您的绩效目标。

## 性能监控 {#performance-monitoring}

性能（或者缺乏性能）是用户首先注意到的事情之一，因此，与任何具有用户界面的应用程序一样，性能至关重要。 要优化AEM安装的性能，您需要监控实例的各种属性及其行为。

有关如何执行性能监控的信息，请参阅 [监控性能](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance).

导致性能问题的问题通常很难跟踪，即使它们的效果很容易看到。

基本起点是系统正常运行时对系统的良好了解。 除非您知道环境在正常运行时“外观”和“行为”如何，否则在性能恶化时，很难找到问题。 这意味着，在系统正常运行时，您应该花一些时间来调查系统，并确保收集性能信息是一项持续的任务。 这将为您提供在性能受到影响时进行比较的基础。

下图说明了AEM内容请求可采用的路径，从而说明了可能影响性能的不同元素的数量。

![chlimage_1-79](assets/chlimage_1-79.png)

性能也是卷和容量之间的平衡：

* **卷**  — 系统处理和传送的输出量。
* **容量**  — 系统传送卷的能力。

这可以在整个Web链的不同位置进行说明。

![chlimage_1-80](assets/chlimage_1-80.png)

有几个功能领域通常负责影响性能：

* 缓存
* 应用程序（您的项目）代码
* 搜索功能

### 性能基本规则 {#basic-rules-regarding-performance}

在优化性能时，应牢记以下某些规则：

* 性能调整 *必须* 成为每个项目的一部分。
* 请勿在开发周期的早期进行优化。
* 性能仅与最薄弱的环节一样好。
* 请始终考虑容量与容量。
* 首先优化重要事项。
* 不优化 *现实* 目标。

>[!NOTE]
>
>请记住，用于衡量绩效的机制通常会影响您尝试衡量的内容。 您应始终努力解决这些差异，并尽可能消除其影响；特别是，应尽可能取消激活浏览器插件。

## 性能配置 {#configuring-for-performance}

可以对AEM的某些方面（和/或基础存储库）进行配置以优化性能。 以下是各种可能性和建议，您必须确保在进行更改之前是否或如何使用相关功能。

>[!NOTE]
>
>有关其他信息，请参阅 [知识库文章](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html).

### 搜索索引 {#search-indexing}

从AEM 6.0开始，Adobe Experience Manager使用基于Oak的存储库架构。

您可以在此处找到更新的索引信息：

* [有关查询和索引的最佳实践](/help/sites-deploying/best-practices-for-queries-and-indexing.md)
* [查询和索引](/help/sites-deploying/queries-and-indexing.md)

### 并发工作流处理 {#concurrent-workflow-processing}

限制同时运行的工作流进程的数量以提高性能。 默认情况下，工作流引擎会并行处理任意数量的工作流，只要有可用于Java VM的处理器。 当工作流步骤需要大量处理资源（RAM或CPU）时，并行运行其中几个工作流可能会对可用的服务器资源提出很高要求。

例如，在上传图像（或通常为DAM资产）时，工作流会自动将图像导入DAM。 图像通常是高分辨率的，并且处理时容易消耗数百MB的堆。 并行处理这些图像会给存储子系统和垃圾收集器带来高负载。

工作流引擎使用Apache Sling作业队列来处理和计划工作项处理。 默认情况下，已从Apache Sling作业队列配置服务工厂创建以下作业队列服务，以处理工作流作业：

* Granite工作流队列：大多数工作流步骤（例如处理DAM资产的步骤）都使用Granite工作流队列服务。
* Granite工作流外部进程作业队列：此服务用于特殊的外部工作流步骤，通常用于联系外部系统和轮询结果。 例如，InDesign媒体提取流程步骤将作为外部流程实施。 工作流引擎使用外部队列处理轮询。 (请参阅 [com.day.cq.workflow.exec.WorkflowExternalProcess](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkflowExternalProcess.html).)

配置这些服务以限制并发运行的工作流进程的最大数量。

>[!NOTE]
>
>配置这些作业队列会影响所有工作流，除非您为特定的工作流模型创建了作业队列(请参阅 [为特定工作流模型配置队列](/help/sites-deploying/configuring-performance.md#configure-the-queue-for-a-specific-workflow) )。

#### 存储库中的配置 {#configuration-in-the-repo}

如果要配置服务 [使用sling:OsgiConfig节点](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)，则需要查找现有服务的PID，例如：org.apache.sling.event.jobs.QueueConfiguration.370aad73-d01b-4a0b-abe4-20198d85f705。 您可以使用Web控制台发现PID。

您需要配置名为 `queue.maxparallel`.

#### Web控制台中的配置 {#configuration-in-the-web-console}

配置这些服务 [使用Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)，找到Apache Sling作业队列配置服务工厂下的现有配置项。

您需要配置名为“最大并行作业数”的属性。

### 为特定工作流配置队列 {#configure-the-queue-for-a-specific-workflow}

为特定工作流模型创建作业队列，以便您可以配置该工作流模型的作业处理。 这样，您的配置就会影响特定工作流的处理，而默认Granite工作流队列的配置则控制其他工作流的处理。

执行工作流模型时，他们会为特定主题创建Sling作业。 默认情况下，该主题与为常规Granite工作流队列或Granite工作流外部进程作业队列配置的主题相匹配：

* `com/adobe/granite/workflow/job*`
* `com/adobe/granite/workflow/external/job*`

工作流模型生成的实际作业主题包括特定于模型的后缀。 例如， **DAM更新资产** 工作流模型会生成具有以下主题的作业：

`com/adobe/granite/workflow/job/etc/workflow/models/dam/update_asset/jcr_content/model`

因此，您可以为主题创建与工作流模型的作业主题匹配的作业队列。 配置队列的性能相关属性仅影响生成与队列主题匹配的作业的工作流模型。

以下过程使用 **DAM更新资产** 工作流的示例。

1. 执行要为其创建作业队列的工作流模型，以便生成主题统计信息。 例如，向资产中添加图像以执行 **DAM更新资产** 工作流。
1. 打开Sling作业控制台(`https://<host>:<port>/system/console/slingevent`)。
1. 在控制台中探索与工作流相关的主题。 对于DAM更新资产，找到以下主题：

   * `com/adobe/granite/workflow/external/job/etc/workflow/models/dam/update_asset/jcr_content/model`
   * `com/adobe/granite/workflow/job/etc/workflow/models/dam/update_asset/jcr_content/model`
   * `com/adobe/granite/workflow/job/etc/workflow/models/dam-xmp-writeback/jcr_content/model`

1. 为每个主题创建一个作业队列。 要创建作业队列，请为Apache Sling作业队列工厂服务创建工厂配置。

   工厂配置与 [并发工作流处理](/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing)，但主题属性与工作流作业的主题匹配除外。

### AEM DAM资产同步服务 {#cq-dam-asset-synchronization-service}

的 `AssetSynchronizationService` 用于同步来自装载存储库（包括LiveLink 、 Documentum等）的资产。 默认情况下，每300秒（5分钟）进行一次定期检查，因此如果不使用挂载的存储库，则可以禁用此服务。

此操作由 [配置OSGi服务](/help/sites-deploying/configuring-osgi.md) **CQ DAM资产同步服务** 设置 **同步期** ( `scheduler.period`)至（最少为）1年（以秒为单位定义）。

### 多个DAM实例 {#multiple-dam-instances}

例如，部署多个DAM实例有助于提高性能：

* 由于为创作环境定期上传大量资产，因此负载较高；此处，可以专门为作者提供单独的DAM实例。
* 您在全球各地（例如，美国、欧洲、亚洲）拥有多个团队。

其他注意事项包括：

* 在发布时将作者的“在制品”与“最终”分开
* 将创作上的内部用户与发布上的外部访客/用户（例如代理、新闻代表、客户、学生等）分开。

## 质量保证最佳实践 {#best-practices-for-quality-assurance}

性能对发布环境至关重要。 因此，您需要仔细规划和分析在实施项目时将针对发布环境进行的性能测试。

本节旨在对定义专门用于您的性能测试的测试概念所涉及的问题进行标准化概述 *发布* 环境。 这主要是QA工程师、项目经理和系统管理员感兴趣的。

下面介绍了对上的AEM应用程序进行性能测试的标准化方法 *发布* 环境。 这涉及以下5个阶段：

* [知识验证](#verification-of-knowledge)
* [范围定义](#scope-definition)
* [测试方法](#test-methodologies)
* [绩效目标的定义](#defining-the-performance-goals)
* [优化](#optimization)

控制是一个额外的、涵盖所有内容的过程，是必要的，但不限于测试。

### 知识验证 {#verification-of-knowledge}

第一步是记录在开始测试之前您需要了解的基本信息：

* 测试环境的架构
* 详细描述需要测试的内部元素的应用程序图（隔离和组合）

#### 测试架构 {#test-architecture}

您应该清楚地记录用于性能测试的测试环境的架构。

您需要复制计划的生产发布环境以及调度程序和负载平衡器。

#### 应用程序图 {#application-map}

要获得清晰的概述，您可以创建整个应用程序的映射（您很可能已在创作环境的测试中获得该映射）。

应用程序内部元素的图表表示，可以提供测试要求的概述；通过颜色编码，还可以用作报告的基础。

### 范围定义 {#scope-definition}

应用程序通常会有一系列用例。 有些将非常重要，有些则不那么重要。

要将性能测试的范围集中在发布上，我们建议您定义：

* 最重要的业务用例
* 最关键的技术用例

用例的数量由您来决定，但应该限制为一个易于管理的数字（例如，在5到10之间）。

选择关键用例后，便可以为每个案例定义关键绩效指标(KPI)和用于衡量这些指标的工具。 常见KPI的示例包括：

* 端到端响应时间
* Servlet响应时间
* 单个组件的响应时间
* 服务的响应时间
* 线程池中的空闲线程数
* 可用连接数
* 系统资源，如CPU和I/O访问

### 测试方法 {#test-methodologies}

此概念有4种用于定义和测试性能目标的方案：

* 单组件测试
* 组合组件测试
* *上线* 方案
* 错误方案

根据以下原则。

#### 组件断点 {#component-breakpoints}

* 每个组件在与性能相关时都有一个特定的中断点。 这意味着组件在达到特定点之前会显示良好的性能，在达到该点之后，性能会迅速下降。
* 要获取应用程序的完整概述，您必须首先验证组件以确定何时到达每个断点。
* 要查找断点，您可以执行负载测试，其中在一段时间内，您需要增加用户数量以创建不断增加的负载。 通过监控此负载和组件的响应，您将在到达组件的断点时遇到特定的性能行为。 该点可以按每秒并发事务数以及并发用户数（如果组件对此KPI敏感）来进行鉴别。
* 然后，此信息可作为改进的基准，指示所使用度量的效率，并帮助定义测试情景。

#### 交易 {#transactions}

* 术语事务用于表示完整网页的请求，包括页面本身和所有后续调用；例如，页面请求、任何AJAX调用、图像和其他对象。**请求向下钻取**
* 要充分分析每个请求，您可以表示调用堆栈的每个元素，然后总计每个请求的平均处理时间。

### 定义绩效目标 {#defining-the-performance-goals}

定义范围和相关KPI后，可以设置特定的绩效目标。 这包括设计测试方案和目标值。

您需要在平均和峰值条件下测试性能。 此外，您还需要上线方案测试，以确保在网站首次可用时能够满足客户对网站日益浓厚的兴趣。

您从现有网站收集的任何体验或统计信息也可用于确定未来目标；例如，来自您实时网站的热门流量。

#### 单个组件测试 {#single-component-tests}

关键组件需要在平均和峰值条件下进行测试。

在这两种情况下，您都可以定义当预定义数量的用户使用系统时每秒的预期事务处理数。

| 组件 | 测试类型 | 否. 用户数 | Tx/秒（预期） | Tx/秒（已测试） | 描述 |
|---|---|---|---|---|---|
| 主页单用户 | 平均 | 1 | 1 |  |  |
|  | 峰值 | 1 | 3 |  |  |
| 主页100个用户 | 平均 | 100 | 3 |  |  |
|  | 峰值 | 100 | 3 |  |

#### 组合组件测试 {#combined-component-tests}

通过组合测试组件，可以更深入地反映应用程序行为。 同样，必须测试平均和峰值条件。

| 方案 | 组件 | 否. 用户数 | Tx/秒（预期） | Tx/秒（已测试） | 描述 |
|---|---|---|---|---|---|
| 混合平均值 | 主页 | 10 | 1 |  |  |
|  | 搜索 | 10 | 1 |  |  |
|  | 新闻 | 10 | 2 |  |  |
|  | 事件 | 10 | 1 |  |  |
|  | 激活 | 10 | 3 |  | 创作行为模拟。 |
| 混合峰 | 主页 | 100 | 5 |  |  |
|  | 搜索 | 50 | 5 |  |  |
|  | 新闻 | 100 | 10 |  |  |
|  | 事件 | 100 | 10 |  |  |
|  | 激活 | 20 | 20 |  | 创作行为模拟。 |

#### 上线测试 {#going-live-tests}

在您的网站发布后的最初几天，您可能会有更高的兴趣级别。 这可能比您测试的峰值还要大。 强烈建议测试上线方案，以确保系统能够满足此情况。

| 方案 | 测试类型 | 否. 用户数 | Tx/秒（预期） | Tx/秒（已测试） | 描述 |
|---|---|---|---|---|---|
| 上线高峰 | 主页 | 200 | 20 |  |  |
|  | 搜索 | 100 | 10 |  |  |
|  | 新闻 | 200 | 20 |  |  |
|  | 事件 | 200 | 20 |  |  |
|  | 激活 | 20 | 20 |  | 创作行为模拟。 |

#### 错误方案测试 {#error-scenario-tests}

还必须测试错误情景，以确保系统能正确、适当地反应。 不仅在于错误本身的处理方式，还在于它可能对性能的影响。 例如：

* 当用户尝试在搜索框中输入无效搜索词时会发生什么情况
* 当搜索词非常一般，以致返回过多的结果时会发生什么情况

在设计这些测试时，应记住并非所有情景都会定期发生。 但是，它们对整个系统的影响很重要。

| 错误方案 | 错误类型 | 否. 用户数 | Tx/秒（预期） | Tx/秒（已测试） | 描述 |
|---|---|---|---|---|---|
| 搜索组件过载 | 搜索全局通配符（星号） | 10 | 1 |  | 仅&amp;ast;&amp;ast;&amp;ast;搜索。 |
|  | 停止字 | 20 | 2 |  | 正在搜索一个停止词。 |
|  | 空字符串 | 10 | 1 |  | 搜索空字符串。 |
|  | 特殊字符 | 10 | 1 |  | 搜索特殊字符。 |

#### 耐力测试 {#endurance-tests}

系统连续运行一段时间后，才会遇到某些问题；不管是几个小时，甚至几天。 使用耐久性测试来测试在所需时间段内的恒定平均负载。 然后可以分析任何性能下降。

| 方案 | 测试类型 | 否. 用户数 | Tx/秒（预期） | Tx/秒（已测试） | 描述 |
|---|---|---|---|---|---|
| 耐力测试（72小时） | 主页 | 10 | 1 |  |  |
|  | 搜索 | 10 | 1 |  |  |
|  | 新闻 | 20 | 2 |  |  |
|  | 事件 | 10 | 1 |  |  |
|  | 激活 | 1 | 3 |  | 创作行为模拟。 |

### 优化 {#optimization}

在实施的后续阶段，您需要优化应用程序以实现/最大化性能目标。

必须对所做的任何优化进行测试，以确保它们具有：

* 不影响功能
* 已通过负载测试验证后才能发布

有一系列工具可帮助您进行负载生成、性能监控和/或结果分析：

* [JMeter](https://jakarta.apache.org/jmeter/)
* [加载运行程序](https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview)
* [德特米内](https://www.determyne.com/) InsideApps
* [红外线](https://www.infraredsoftware.com/)
* [Java交互式配置文件](https://jiprof.sourceforge.net/)
* 更多...

优化后，您需要再次测试以确认影响。

### 报告 {#reporting}

需要持续报告才能让每个人都知道状态，如之前在对体系结构图进行颜色编码时所述。

完成所有测试后，您将需要报告：

* 遇到任何严重错误
* 非关键问题，仍需进一步调查
* 测试期间所作之任何假设
* 测试中要提出的任何建议

## 使用Dispatcher时优化性能 {#optimizing-performance-when-using-the-dispatcher}

的 [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) 是Adobe的缓存和/或负载平衡工具。 使用Dispatcher时，您应考虑优化网站以提高缓存性能。

>[!NOTE]
>
>虽然 Dispatcher 版本独立于 AEM，但 Dispatcher 文档会嵌入到 AEM 文档中。始终使用嵌入到最新版本的 AEM 文档中的 Dispatcher 文档。
>
>您可能是在单击以前版本的 AEM 文档中嵌入的 Dispatcher 文档链接后重定向到此页面。

Dispatcher提供了许多内置机制，在您的网站利用这些机制时，您可以使用这些机制来优化性能。 此部分介绍了如何设计您的网站以最大限度地提高缓存优势。

>[!NOTE]
>
>Dispatcher 将缓存存储在标准 Web 服务器上，记住这一点可能会对您有所帮助。这意味着您：
>
>* 可以使用URL缓存可存储为页面和请求的所有内容
>* 无法存储其他内容，如Cookie、会话数据和表单数据。
>
>通常，许多缓存策略涉及选择完好的 URL，并且不依赖此类额外数据。
>
>使用Dispatcher版本4.1.11，您还可以缓存响应标头，请参阅 [缓存HTTP响应头](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache).

### 计算调度程序缓存比率 {#calculating-the-dispatcher-cache-ratio}

缓存比率公式估计缓存处理的请求在进入系统的请求总数中所占的百分比。 要计算缓存比率，您需要满足以下条件：

* 请求总数。 此信息在Apache中提供 `access.log`. 有关更多详细信息，请参阅 [官方Apache文档](https://httpd.apache.org/docs/2.4/logs.html#accesslog).

* 发布实例提供的请求数。 此信息可在 `request.log` 实例。 有关更多详细信息，请参阅 [解释request.log](/help/sites-deploying/monitoring-and-maintaining.md#interpreting-the-request-log) 和 [查找日志文件](/help/sites-deploying/monitoring-and-maintaining.md#finding-the-log-files).

计算缓存比率的公式为：

* (请求总数 **减号** 发布时的请求数) **划分** 按请求总数计算。

例如，如果请求总数为129491，而Publish实例提供的请求数为58959，则缓存比率为： **(129491 - 58959)/129491= 54.5%**.

如果您没有一对发布者/调度程序配对，则需要将所有调度程序和发布者的请求添加到一起，以获得准确的测量。 另请参阅 [推荐的部署](/help/sites-deploying/recommended-deploys.md).

>[!NOTE]
>
>为获得最佳性能，Adobe建议将缓存比率设为90%到95%。

#### 使用一致的页面编码 {#using-consistent-page-encoding}

使用Dispatcher版本4.1.11，您可以缓存响应标头。 如果不在Dispatcher上缓存响应标头，则如果在标头中存储页面编码信息，则可能会出现问题。 在此情况下，当 Dispatcher 从缓存中提供一个页面时，Web 服务器的默认编码将用于该页面。可通过两种方式避免此问题：

* 如果您只使用一种编码，请确保 Web 服务器上使用的编码与 AEM 网站的默认编码相同。
* 使用 HTML `head` 部分中的 `<META>` 标记设置编码，如以下示例所示：

```xml
        <META http-equiv="Content-Type" content="text/html; charset=EUC-JP">
```

#### 消除 URL 参数 {#avoid-url-parameters}

如果可能，请消除要缓存的页面的 URL 参数。例如，如果您有一个图片库，则绝不会缓存以下 URL（除非对 Dispatcher 进行[相应配置](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache)）：

```xml
www.myCompany.com/pictures/gallery.html?event=christmas&amp;page=1
```

不过，您可以将这些参数放入页面 URL 中，如下所示：

```xml
www.myCompany.com/pictures/gallery.christmas.1.html
```

>[!NOTE]
>
>此URL会调用与相同的页面和模板 `gallery.html`. 在模板定义中，您可以指定用于渲染页面的脚本，也可以对所有页面使用同一脚本。

#### 按 URL 进行自定义  {#customize-by-url}

如果您允许用户更改字体大小（或任何其他版面自定义设置），请确保各种自定义设置都反映在 URL 中。

例如，由于不会缓存 cookie，因此如果您将字体大小存储在 cookie（或类似机制）中，则不会为缓存的页面保留字体大小。因此，Dispatcher 会随机返回任意字体大小的文档。

在 URL 中包含字体大小作为选择器可避免出现此问题：

```xml
www.myCompany.com/news/main.large.html
```

>[!NOTE]
>
>对于大多数版面，也可以使用样式表和/或客户端脚本。它们通常可以很好地与缓存配合使用。
>
>这对于打印版本也很有用，您可以在其中使用 URL，例如：
>
>`www.myCompany.com/news/main.print.html`
>
>通过使用模板定义的脚本通配，您可以指定单独的脚本来渲染打印页面。

#### 使用作标题的图像文件失效 {#invalidating-image-files-used-as-titles}

如果您将页面标题或其他文本渲染为图片，建议您存储文件，以便在更新页面内容时将其删除：

1. 将图像文件放入与页面相同的文件夹中。
1. 对图像文件使用以下命名格式：

   `<page file name>.<image file name>`

例如，您可以存储页面的标题 `myPage.html` 在 `file myPage.title.gif`. 由于此文件会在页面更新时自动被删除，因此对页面标题进行的任何更改都会自动反映在缓存中。

>[!NOTE]
>
>图像文件不一定会实际存在于 AEM 实例上。您可以使用动态创建图像文件的脚本。随后，Dispatcher 会将文件存储在 Web 服务器上。

#### 使用于导航的图像文件失效 {#invalidating-image-files-used-for-navigation}

如果将图片用于导航条目，则采用的方法与标题的大致相同，只不过会稍微复杂一些。将所有导航图像与目标页面一起存储。如果将两张图片用于一般或活动场景，则可以使用以下脚本：

* 一个正常显示页面的脚本。
* 一个处理“.normal”请求并返回正常图片的脚本。
* 一个处理“.active”请求并返回活动图片的脚本。

请务必使用与页面相同的命名句柄创建这些图片，以确保内容更新将删除这些图片以及页面。

对于未修改的页面，图片仍保留在缓存中，但页面本身通常会自动失效。

#### 个性化 {#personalization}

建议您将个性化限制为必要时。 原因如下：

* 如果您使用可随意自定义的开始页面，则用户每次请求该页面时都必须对它进行编辑。
* 相反，如果您有 10 个不同的开始页面可供选择，则可以缓存其中的每个页面，从而提高性能。

>[!TIP]
>有关配置Dispatcher缓存的更多详细信息，请参阅 [AEM Dispatcher缓存教程](https://experienceleague.adobe.com/docs/experience-manager-learn/dispatcher-tutorial/overview.html) 和 [缓存受保护的内容。](https://experienceleague.adobe.com/docs/experience-manager-learn/dispatcher-tutorial/chapter-1.html#dispatcher-tips-and-tricks)

如果您个性化每个页面（例如，将用户名称置于标题栏中），则可能会对性能产生影响。

>[!TIP]
>有关缓存安全内容的信息，请参阅 [缓存安全内容](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html) 中的“调度程序”指南。

关于在一个页面上混合使用受限内容和公共内容，您可能需要考虑一种策略，该策略可利用Dispatcher中的服务器端包含，或者通过浏览器中的Ajax的客户端包含。

>[!TIP]
>
>有关处理混合的公共和受限内容的信息，请参阅 [设置Sling动态包含。](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-sling-dynamic-include.html)

#### 粘性连接 {#sticky-connections}

[粘性连接](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html#the-benefits-of-load-balancing)可确保同一个用户的文档全部在同一服务器上撰写。如果用户在退出此文件夹不久后返回，则此连接仍保持粘性。定义一个文件夹来保存所有需要网站的粘性连接的文档。尽量不要在该文件夹中放入其他文件。如果您使用个性化的页面和会话数据，这将影响负载平衡。

#### MIME 类型 {#mime-types}

浏览器可通过两种方式确定文件的类型：

1. 扩展(例如 `.html`, `.gif`, `.jpg`等)
1. 按服务器随文件一起发送的 MIME 类型。

对于大多数文件，MIME 类型隐含在文件扩展名中。即：

1. 扩展(例如 `.html`, `.gif`, `.jpg`等)
1. 按服务器随文件一起发送的 MIME 类型。

如果文件名没有扩展名，则以纯文本形式显示。

使用Dispatcher版本4.1.11，您可以缓存响应标头。 如果不缓存Dispatcher上的响应标头，请注意，MIME类型是HTTP标头的一部分。 因此，如果AEM应用程序返回的文件没有可识别的文件结尾，而是依赖MIME类型，则这些文件可能会被错误地显示。

要确保正确缓存文件，请遵循以下准则：

* 确保文件始终具有正确的扩展名。
* 避免使用通用文件服务脚本，这些脚本具有URL，例如 `download.jsp?file=2214`. 重写脚本以使用包含文件规范的URL。对于上一个示例，这将是 `download.2214.pdf`.

## 备份性能 {#backup-performance}

本节介绍一系列用于评估AEM备份性能和备份活动对应用程序性能的影响的基准。 AEM备份在系统运行时对系统造成很大负载，我们测量了这一情况，以及尝试调制这些影响的备份延迟设置的影响。 其目标是提供一些参考数据，说明实际配置中备份的预期性能和生产数据的数量，并就如何估算计划系统的备份时间提供指导。

### 参考环境 {#reference-environment}

#### 物理系统 {#physical-system}

本文档中报告的结果是从参考环境中运行的基准获得的，其配置如下。 此配置设计为类似于数据中心中的典型生产环境：

* H-P ProLiant DL380 G6,8 CPU x 2.533 GHz
* 串行连接SCSI 300GB 10,000RPM驱动器
* 硬件RAID控制器；RAID0+5阵列中有8个驱动器
* VMware映像CPU x 2英特尔至强E5540,2.53GHz
* RedHat Linux 2.6.18-194.el5;Java 1.6.0_29
* 单个创作实例

此服务器上的磁盘子系统速度相当快，代表了可能在生产服务器中使用的高性能RAID配置。 备份性能对磁盘性能很敏感，此环境中的结果反映了在非常快速的RAID配置上的性能。 VMWare映像配置为在RAID阵列上具有物理驻留在本地磁盘存储中的单个大磁盘卷。

AEM配置将存储库和数据存储放在同一逻辑卷上，以及所有操作系统和AEM软件。 备份的目标目录也位于此逻辑文件系统上。

#### 数据卷 {#data-volumes}

下表说明了备份基准中使用的数据卷的大小。 首先安装初始基准内容，然后添加额外的已知数据量以增加备份内容的大小。 将以特定增量创建备份，以表示内容和一天内可能产生的内容大幅增加。 内容（页面、图像、标记）的分发大致将基于逼真的生产资产组合。 页面、图像和标记最多将限制为800个子页面。 每个页面都将包含标题、Flash、文本/图像、视频、幻灯片、表单、表格、云和轮播组件。 将从400个唯一文件的池中上传图像，大小从37千字节到594千字节不等。

| 内容 | 节点 | 页面 | 图像 | 标记 |
|---|---|---|---|---|
| 基本安装 | 69 610 | 562 | 256 | 237 |
| 用于增量备份的小内容 |  | +100 | +2 | +2 |
| 用于完全备份的大内容 |  | +10 000 | +100 | +100 |

备份基准会重复，每次重复时都会添加其他内容集。

#### 基准方案 {#benchmark-scenarios}

备份基准包括两种主要情形：在系统处于应用程序大负载时进行备份，在系统空闲时进行备份。 虽然一般建议在AEM尽可能空闲时执行备份，但在某些情况下，必须在系统负载不足时运行备份。

* **空闲状态**  — 在AEM上执行备份时没有其他活动。
* **在加载下**  — 在系统从联机进程负载不足80%时执行备份。 备份延迟会有所不同，以查看对负载的影响。

从AEM服务器日志获取备份时间和生成备份的大小。 通常建议在AEM空闲时（如在午夜）将备份安排为非时间备份。 这种情况代表了建议的方法。

加载将由页面创建/删除、遍历和查询组成，其中大多数加载来自页面遍历和查询。 添加和删除过多页面会不断增大工作区大小，并阻止备份完成。 脚本将使用的加载分布为75%的页面遍历、24%的查询和1%的页面创建（单个级别没有嵌套子页面）。 在空闲系统上，每秒的峰值平均事务量是通过4个并发线程实现的，这是测试负载下备份时所使用的。

负载对备份性能的影响可以通过此应用程序负载时和不时的性能差异来估计。 备份对应用程序吞吐量的影响可通过比较每小时事务中的方案吞吐量（包括和不包括持续的并发备份）和备份以不同的“备份延迟”设置运行时的情况吞吐量来发现。

* **延迟设置**  — 对于某些情况，我们还使用10毫秒（默认值）、1毫秒和0毫秒的值来更改备份延迟设置，以了解此设置如何影响备份性能。
* **备份类型**  — 所有备份都是将存储库外部备份到备份目录而不创建zip ，但是在比较时，tar命令直接使用。 由于增量备份不能创建到zip文件，或者当以前的完全备份是zip文件时，备份目录方法在生产情况中最常使用。

### 结果摘要 {#summary-of-results}

#### 备份时间和吞吐量 {#backup-time-and-throughput}

这些基准的主要结果是显示备份时间随备份类型和总数据量的变化情况。 下图显示了使用默认备份配置获得的备份时间，它是页总数的函数。

![chlimage_1-81](assets/chlimage_1-81.png)

空闲实例上的备份时间相当一致，无论是完整备份还是增量备份，平均为0.608 MB/s（请参阅下图）。 备份时间只是备份数据量的函数。 完成完整备份的时间会随着页面总数的增加而明显增加。 完成增量备份的时间也会随着页面总数而增加，但速度要低得多。 由于备份的数据量相对较小，完成增量备份所花费的时间要短得多。

备份的大小是完成备份所花费的时间的主要决定因素。 下图显示了作为最终备份大小的函数所需的时间。

![chlimage_1-82](assets/chlimage_1-82.png)

此图表说明，增量备份和完整备份都遵循一种简单的大小与时间模式，我们可以将此模式作为吞吐量进行衡量。 空闲实例上的备份时间相当一致，平均为0.61 MB/秒，而不考虑基准环境中的完整或增量备份。

#### 备份延迟 {#backup-delay}

提供备份延迟参数以限制备份可能干扰生产工作负载的程度。 参数指定的等待时间（以毫秒为单位），将逐个文件插入到备份操作中。 整体效果部分取决于受影响文件的大小。 以MB/秒为单位测量备份性能为比较延迟对备份的影响提供了一种合理的方法。

* 与常规应用程序负载同时运行备份将对常规负载的吞吐量产生负面影响。
* 影响可能很小（只有5%），或者可能非常显着，导致吞吐量下降75%，这可能比任何情况都更取决于应用程序。
* 备份在CPU上并不是负载过重，因此与I/O密集型工作负载相比，CPU密集型生产工作负载受备份影响较小。

![chlimage_1-83](assets/chlimage_1-83.png)

为了比较使用文件系统备份（使用“tar”）备份同一存储库文件时获得的吞吐量。 tar的性能相当，但略高于将延迟设置为零的备份。 即使设置小的延迟也会大大降低备份吞吐量，而默认延迟为10毫秒会大大降低吞吐量。 如果在总体应用程序使用率很低或应用程序完全空闲时可能安排备份，则可能需要将延迟降低到默认值以下，以便允许备份更快地进行。

持续备份的应用程序吞吐量的实际影响取决于应用程序和基础架构的详细信息。 延迟值的选择应通过对应用程序的经验分析来完成，但应尽可能选择小的延迟值，以便能够尽快完成备份。 由于选择延迟值与对应用程序吞吐量的影响之间只存在微弱的关联，因此选择延迟应该有利于缩短总体备份时间，以最大限度地减少备份的整体影响。 备份需要8小时才能完成，但吞吐量影响为–20%的备份，其总体影响可能比完成需要2小时而吞吐量影响为–30%的备份大。

### 引用 {#references}

* [管理 — 备份和恢复](/help/sites-administering/backup-and-restore.md)
* [管理 — 容量和卷](/help/managing/best-practices-further-reference.md#capacity-and-volume)
