---
title: 性能优化
seo-title: 性能优化
description: 了解如何配置AEM的某些方面以优化性能。
seo-description: 了解如何配置AEM的某些方面以优化性能。
uuid: a4d9fde4-a4c7-4ee5-99b6-29b0ee7dc35b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 80118cd1-73e1-4675-bbdf-85d66d150abc
translation-type: tm+mt
source-git-commit: 7f1ae2d4ab361bc039c1098daa0ef944ec9df639
workflow-type: tm+mt
source-wordcount: '6648'
ht-degree: 1%

---


# 性能优化{#performance-optimization}

>[!NOTE]
>
>有关性能的一般准则，请阅读[性能准则](/help/sites-deploying/performance-guidelines.md)页。
>
>有关故障排除和修复性能问题的详细信息，另请参阅[性能树](/help/sites-deploying/performance-tree.md)。
>
>此外，您还可以查看有关[性能调整提示的知识库文章。](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)

关键问题是您的网站响应访客请求所花费的时间。 尽管此值会因每个请求而异，但可以定义平均目标值。 一旦这一价值被证明是可实现的和可维护的，它就可以用于监控网站的性能并指示潜在问题的发展。

您将针对的响应时间在创作和发布环境上会有所不同，反映目标受众的不同特征：

## 创作环境 {#author-environment}

此环境供输入和更新内容的作者使用。 更新内容页面和这些页面上的单个元素时，它必须满足每个用户生成大量性能密集型请求的少数用户的需求。

## 发布环境 {#publish-environment}

此环境包含您提供给用户的内容。 在这里，请求数量更多，速度也同样重要，但由于请求的性质不太动态，因此可以应用额外的性能增强机制；如缓存内容或负载平衡。

>[!NOTE]
>
>* 在配置性能优化后，请按照[Tough Day](/help/sites-developing/tough-day.md)中的步骤测试重载下的环境。
>* 另请参阅[性能调整提示。](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)


## 性能优化方法{#performance-optimization-methodology}

AEM项目的性能优化方法可以归纳为五个非常简单的规则，这些规则可以遵循，以避免开始的性能问题：

1. [优化计划](#planning-for-optimization)
1. [模拟现实](#simulate-reality)
1. [确立坚实的目标](#establish-solid-goals)
1. [保持相关性](#stay-relevant)
1. [灵活迭代循环](#agile-iteration-cycles)

这些规则在很大程度上适用于Web项目，与项目经理和系统管理员相关，以确保其项目在启动时不会面临性能挑战。

### 优化计划{#planning-for-optimization}

![chlimage_1-3](assets/chlimage_1-3.jpeg)

大约10%的项目工作应计划用于性能优化阶段。 当然，实际的性能优化要求将取决于项目的复杂性水平和开发团队的经验。 虽然您的项目可能（最终）不需要所有分配的时间，但最好始终在建议区域规划性能优化。

在可能的情况下，首先应将项目软启动到有限受众，以收集实际体验并进行进一步优化，而无需在发布完整公告后承受额外压力。

“实时”后，性能优化不会结束。 这是您体验系统上“真实”负载的时间点。 计划在启动后进行其他调整很重要。

由于系统负载发生变化，并且系统的性能用户档案会随时间推移而改变，因此应以6-12个月的时间间隔安排性能“调整”或“运行状况检查”。

### 模拟现实{#simulate-reality}

![chlimage_1-4](assets/chlimage_1-4.jpeg)

如果您与某个网站一起上线，并在启动后发现您遇到性能问题，则只有一个原因：负载和性能测试不能充分模拟现实。

模拟现实是困难的，而您合理地希望投入多少精力来实现“真实”取决于您项目的性质。 “真实”不仅指“真实代码”和“真实流量”，还指“真实内容”，特别是关于内容大小和结构的内容。 请记住，根据存储库的大小和结构，模板的行为可能会完全不同。

### 确立坚实的目标{#establish-solid-goals}

![chlimage_1-5](assets/chlimage_1-5.jpeg)

正确制定业绩目标的重要性不容低估。 通常，一旦人们开始关注特定的绩效目标，就很难在以后改变这些目标，即使这些目标是基于疯狂的假设。

建立良好、稳健的业绩目标确实是最棘手的领域之一。 通常最好从类似网站（例如新网站的前身）收集真实生活日志和基准。

### 保持相关{#stay-relevant}

![chlimage_1-6](assets/chlimage_1-6.jpeg)

一次优化一个瓶颈很重要。 如果您尝试并行操作而未验证一次优化的影响，您将无法跟踪哪个优化衡量标准实际上起到了帮助。

### 灵活迭代循环{#agile-iteration-cycles}

![chlimage_1-7](assets/chlimage_1-7.jpeg)

性能调整是一个迭代过程，它涉及测量、分析、优化和验证，直到达到目标。 为了正确考虑这一方面，在优化阶段实施灵活的验证过程，而不是在每次迭代后执行更繁重的权重测试过程。

这在很大程度上意味着实施优化的开发者应该能够快速判断优化是否已达到目标。 这是宝贵的信息，因为当达到目标时，优化就结束了。

## 基本性能指南{#basic-performance-guidelines}

通常，将未缓存的html请求保持在100毫秒以内。 更具体地说，以下内容可作为指导：

* 70%的页面请求应在100毫秒内得到答复。
* 25%的页面请求应在100ms-300ms内得到响应。
* 4%的页面请求应在300ms-500ms内得到响应。
* 1%的页面请求应在500ms-1000ms内得到响应。
* 任何页面的响应速度都不应低于1秒。

上述数字假设以下条件：

* 在发布时衡量(没有与创作环境相关的间接费用)
* 在服务器上测量（无网络开销）
* 未缓存(没有AEM输出缓存，没有调度程序缓存)
* 仅适用于具有多个依赖关系(HTML、JS、PDF...)的复杂项目
* 系统上没有其他负载

有些问题经常导致性能问题。 主要围绕：

* 调度程序缓存效率低下
* 在普通显示模板中使用查询。

JVM和操作系统级别调整通常不会导致性能的大幅提升，因此应在优化周期的最后阶段执行。

内容存储库的结构方式也会影响性能。 为获得最佳性能，附加到内容存储库中单个节点的子节点数不应超过1,000（作为一般规则）。

在通常的性能优化练习中，您的最好朋友是：

* 不为目标组件考虑 `request.log`
* 基于组件的计时
* 最后，但不是最后一个Java概要分析器。

### 加载和编辑数字资产时的性能{#performance-when-loading-and-editing-digital-assets}

由于加载和编辑数字资产时涉及大量数据，因此性能可能成为一个问题。

以下两点会影响性能：

* CPU —— 多核允许在转码时更流畅地工作
* 硬盘——并行RAID磁盘实现相同

要提高性能，您可以考虑以下事项：

* 每天要上传多少个资产？ 最佳估计可基于：

![chlimage_1-77](assets/chlimage_1-77.png)

* 进行编辑的时间范围（通常为工作日的时长，对于国际操作则更多）。
* 上传的图像的平均大小（以及每个图像生成的演绎版的大小）(MB)。
* 确定平均数据率：

![chlimage_1-78](assets/chlimage_1-78.png)

* 80%的编辑将在20%的时间内完成，因此在高峰时间，您的数据率将是平均数据率的4倍。 这是您的绩效目标。

## 性能监视{#performance-monitoring}

性能（或缺乏性能）是用户首先注意到的事情之一，因此与任何具有用户界面的应用程序一样，性能至关重要。 要优化AEM安装的性能，您需要监视实例的各种属性及其行为。

有关如何执行性能监视的信息，请参见[监视性能](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance)。

导致性能问题的问题通常很难跟踪，即使它们的效果很容易看到。

一个基本的出发点是，当系统正常运行时，对系统有很好的了解。 除非您知道环境在正常运行时的“外观”和“行为”，否则在性能恶化时很难找到问题所在。 这意味着您应花一些时间调查系统在平稳运行时的运行情况，并确保收集性能信息是持续的任务。 这将为您提供在性能受到影响时进行比较的基础。

下图说明AEM内容请求可采用的路径，因此说明影响性能的不同元素的数量。

![chlimage_1-79](assets/chlimage_1-79.png)

性能也是卷和容量之间的平衡：

* **Volume**  —系统处理和传送的输出量。
* **容量** -系统交付卷的能力。

这可以在整个Web链的不同位置进行说明。

![chlimage_1-80](assets/chlimage_1-80.png)

有几个功能方面通常负责影响性能：

* 缓存
* 应用程序（您的项目）代码
* 搜索功能

### 性能{#basic-rules-regarding-performance}的基本规则

在优化性能时，应牢记某些规则：

* 性能调整&#x200B;*必须*&#x200B;是每个项目的一部分。
* 不要在开发周期的早期进行优化。
* 性能仅与最弱环节一样好。
* 始终考虑容量与容量。
* 首先优化重要事项。
* 没有&#x200B;*现实*&#x200B;目标，永远不要进行优化。

>[!NOTE]
>
>请记住，您用于衡量绩效的机制通常会影响您尝试衡量的内容。 你应该努力解决这些差异，尽可能消除它们的影响；尤其是应尽可能取消激活浏览器插件。

## 性能{#configuring-for-performance}配置

可以配置AEM（和／或基础存储库）的某些方面以优化性能。 以下是可能性和建议，在进行更改之前，您必须确定是否或如何使用相关功能。

>[!NOTE]
>
>有关详细信息，请参阅[KB文章](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)。

### 搜索索引{#search-indexing}

从AEM 6.0开始，Adobe Experience Manager使用基于Oak的存储库体系结构。

您可以在以下网址找到更新的索引信息：

* [查询和索引的最佳实践](/help/sites-deploying/best-practices-for-queries-and-indexing.md)
* [查询和索引](/help/sites-deploying/queries-and-indexing.md)

### 并发工作流处理{#concurrent-workflow-processing}

限制并发运行的工作流进程数以提高性能。 默认情况下，工作流引擎处理的工作流数与Java VM可用的处理器数相同。 当工作流步骤需要大量处理资源（RAM或CPU）时，并行运行这些工作流中的若干个可能会对可用服务器资源提出高要求。

例如，当上传图像（或通常为DAM资产）时，工作流会自动将图像导入DAM。 图像通常是高分辨率的，并且处理时可轻松消耗数百MB的堆。 并行处理这些图像会给存储子系统和垃圾收集器带来高负载。

工作流引擎使用Apache Sling作业队列来处理和计划工作项处理。 默认情况下，已从Apache Sling作业队列配置服务工厂创建以下作业队列服务以处理工作流作业：

* Granite工作流队列：大多数工作流步骤（如处理DAM资产的步骤）都使用Granite工作流队列服务。
* Granite工作流外部进程作业队列：此服务用于特殊的外部工作流步骤，这些步骤通常用于联系外部系统和轮询结果。 例如，InDesign媒体提取流程步骤将作为外部流程实施。 工作流引擎使用外部队列处理轮询。 (请参阅[com.day.cq.workflow.exec.WorkflowExternalProcess](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkflowExternalProcess.html)。)

配置这些服务以限制并发运行的工作流进程的最大数量。

>[!NOTE]
>
>配置这些作业队列会影响所有工作流，除非您为特定工作流模型创建了作业队列（请参阅下面的[为特定工作流模型配置队列](/help/sites-deploying/configuring-performance.md#configure-the-queue-for-a-specific-workflow)）。

#### 存储库{#configuration-in-the-repo}中的配置

如果您使用sling:OsgiConfig节点](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)配置服务[，您需要找到现有服务的PID，例如：org.apache.sling.事件.jobs.QueueConfiguration.370aad73-d01b-4a0b-abe4-20198d85f705。 您可以使用Web控制台发现PID。

您需要配置名为`queue.maxparallel`的属性。

#### Web控制台{#configuration-in-the-web-console}中的配置

要使用Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)配置这些服务[，请在Apache Sling作业队列配置服务工厂下找到现有配置项。

您需要配置名为“最大并行作业”的属性。

### 为特定工作流{#configure-the-queue-for-a-specific-workflow}配置队列

为特定工作流模型创建作业队列，以便您可以为该工作流模型配置作业处理。 这样，您的配置会影响特定工作流的处理，而默认的Granite工作流队列的配置则控制其他工作流的处理。

当工作流模型执行时，它们会为特定主题创建Sling作业。 默认情况下，该主题与为常规Granite工作流队列或Granite工作流外部进程作业队列配置的主题相匹配：

* `com/adobe/granite/workflow/job*`
* `com/adobe/granite/workflow/external/job*`

工作流模型生成的实际作业主题包括模型特定后缀。 例如，**DAM更新资产**&#x200B;工作流模型生成具有以下主题的作业：

`com/adobe/granite/workflow/job/etc/workflow/models/dam/update_asset/jcr_content/model`

因此，您可以为主题创建与工作流模型的作业主题匹配的作业队列。 配置队列的性能相关属性只影响生成与队列主题匹配的作业的工作流模型。

以下过程以&#x200B;**DAM更新资产**&#x200B;工作流为例，为工作流创建作业队列。

1. 执行要为其创建作业队列的工作流模型，以生成主题统计信息。 例如，向资产中添加一个图像以执行&#x200B;**DAM更新资产**&#x200B;工作流。
1. 打开Sling作业控制台(`https://<host>:<port>/system/console/slingevent`)。
1. 在控制台中发现与工作流相关的主题。 对于DAM更新资产，可找到以下主题：

   * `com/adobe/granite/workflow/external/job/etc/workflow/models/dam/update_asset/jcr_content/model`
   * `com/adobe/granite/workflow/job/etc/workflow/models/dam/update_asset/jcr_content/model`
   * `com/adobe/granite/workflow/job/etc/workflow/models/dam-xmp-writeback/jcr_content/model`

1. 为每个主题创建一个作业队列。 要创建作业队列，请为Apache Sling作业队列工厂服务创建工厂配置。

   工厂配置与[并发工作流处理](/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing)中描述的Granite工作流队列相似，但“主题”属性与工作流作业的主题匹配。

### AEM DAM资产同步服务{#cq-dam-asset-synchronization-service}

`AssetSynchronizationService`用于同步来自装载式存储库（包括LiveLink、Documentum等）的资产。 默认情况下，每300秒（5分钟）进行一次定期检查，因此，如果您不使用挂载式资料库，则可以禁用此服务。

通过[配置OSGi服务](/help/sites-deploying/configuring-osgi.md) **CQ DAM资产同步服务**，将&#x200B;**同步周期**(`scheduler.period`)设置为（最低为）1年（以秒为单位）。

### 多个DAM实例{#multiple-dam-instances}

部署多个DAM实例有助于在以下情况下实现性能：

* 由于为作者环境定期上传大量资产，因此负载较高；此处，可以专门为作者提供服务的单独DAM实例。
* 您在世界各地拥有多个团队（例如美国、欧洲、亚洲）。

其他注意事项包括：

* 在发布时将作者的“在创作中的作品”与“最终作品”分开
* 将创作时的内部用户与发布时的外部访客/用户（例如代理、新闻代表、客户、学生等）相分离。

## 质量保证最佳实践{#best-practices-for-quality-assurance}

性能对您的发布环境至关重要。 因此，在实施项目时，您需要仔细计划和分析将针对发布环境进行的性能测试。

本节旨在对在&#x200B;*publish*&#x200B;环境上为性能测试专门定义测试概念时涉及的问题进行标准化概述。 这主要是QA工程师、项目经理和系统管理员感兴趣的。

下面介绍了在&#x200B;*Publish*&#x200B;环境上对AEM应用程序进行性能测试的标准化方法。 这涉及以下5个阶段：

* [知识验证](#verification-of-knowledge)
* [范围定义](#scope-definition)
* [测试方法](#test-methodologies)
* [绩效目标的定义](#defining-the-performance-goals)
* [优化](#optimization)

控制是一个额外的、包罗万象的过程——必需但不限于测试。

### 知识验证{#verification-of-knowledge}

第一步是文档您需要了解的基础信息，然后才能开始测试：

* 测试环境的架构
* 详细列出需要测试的内部元素的应用程序图（隔离和组合）

#### 测试架构{#test-architecture}

您应明确文档用于性能测试的测试环境的架构。

您需要复制计划内的生产发布环境以及调度程序和负载平衡器。

#### 应用程序映射{#application-map}

要获得清晰的概述，您可以创建整个应用程序的映射(您很可能已通过“作者”环境上的测试获得该映射)。

应用程序内部元素的图表表示，可以提供测试要求的概述；通过颜色编码，它还可以作为报告的基础。

### 范围定义{#scope-definition}

应用程序通常会有一些用例。 有些将非常重要，有些则不那么重要。

要将性能测试的范围集中在发布上，建议您定义：

* 最重要的业务使用案例
* 最关键的技术使用案例

用例数量由您决定，但应限制为易于管理的数量（如5到10）。

一旦选择了关键用例，就可以为每个案例定义关键绩效指标(KPI)和用于衡量它们的工具。 常见KPI示例包括：

* 端到端响应时间
* Servlet响应时间
* 单个组件的响应时间
* 服务的响应时间
* 线程池中的空闲线程数
* 免费连接数
* 系统资源，如CPU和I/O访问

### 测试方法{#test-methodologies}

此概念有4种用于定义和测试性能目标的方案：

* 单个组件测试
* 组合组件测试
* *Going* Livescenario
* 错误方案

根据以下原则。

#### 组件断点{#component-breakpoints}

* 每个组件在与性能相关时都有一个特定的断点。 这意味着组件在达到特定点之前可以显示良好的性能，之后性能会迅速下降。
* 要获得应用程序的完整概述，您必须首先验证您的组件以确定何时到达每个断点。
* 要查找断点，您可以执行负载测试，在一段时间内，增加用户数以创建不断增加的负载。 通过监视此负载和组件的响应，您将在到达组件的断点时遇到特定的性能行为。 该积分可以按每秒并发事务处理数以及并发用户数来限定（如果组件对此KPI敏感）。
* 然后，此信息可以作为改进的基准，指示所使用的度量的效率，并帮助定义测试方案。

#### 事务{#transactions}

* 术语事务用于表示整个网页的请求，包括页面本身和所有后续调用；例如，页面请求、任何AJAX调用、图像和其他对象。**请求向下钻取**
* 要完全分析每个请求，您可以表示调用堆栈的每个元素，然后合计每个请求的平均处理时间。

### 定义绩效目标{#defining-the-performance-goals}

定义范围和相关KPI后，即可设置特定绩效目标。 这包括设计测试方案以及目标值。

您需要在平均和峰值条件下测试性能。 此外，您还需要“开始使用”方案测试，以确保在网站首次发布时能够满足更多网站需求。

您从现有网站收集的任何经验或统计信息，在确定未来目标时也会很有用；例如来自您实时网站的热门流量。

#### 单个组件测试{#single-component-tests}

关键组件需要在平均和峰值条件下进行测试。

在这两种情况下，当预定义的用户数使用系统时，您都可以定义每秒的预期事务处理数。

| 组件 | 测试类型 | 否. 用户数 | Tx/秒（预期） | Tx/秒（已测试） | 描述 |
|---|---|---|---|---|---|
| 主页单用户 | 平均 | 1 | 1 |  |  |
|  | 峰 | 1 | 3 |  |  |
| 主页100个用户 | 平均 | 100 | 1 |  |  |
|  | 峰 | 100 | 1 |  |

#### 组合组件测试{#combined-component-tests}

组合测试组件可更仔细地反映应用程序行为。 同样，必须测试平均和峰值条件。

| 方案 | 组件 | 否. 用户数 | Tx/秒（预期） | Tx/秒（已测试） | 描述 |
|---|---|---|---|---|---|
| 混合平均 | 主页 | 10 | 1 |  |  |
|  | 搜索 | 10 | 3 |  |  |
|  | 新闻 | 10 | 2 |  |  |
|  | 事件 | 10 | 1 |  |  |
|  | 激活 | 10 | 1 |  | 创作行为模拟。 |
| 混合峰 | 主页 | 100 | 5 |  |  |
|  | 搜索 | 50 | 5 |  |  |
|  | 新闻 | 100 | 10 |  |  |
|  | 事件 | 100 | 10 |  |  |
|  | 激活 | 20 | 20 |  | 创作行为模拟。 |

#### 正在进行实时测试{#going-live-tests}

在网站发布后的头几天，您会发现兴趣级别会提高。 这可能比您测试的峰值还要大。 强烈建议测试“开始使用”场景，以确保系统能够满足此情况。

| 方案 | 测试类型 | 否. 用户数 | Tx/秒（预期） | Tx/秒（已测试） | 描述 |
|---|---|---|---|---|---|
| 向实时峰值迈进 | 主页 | 200 | 20 |  |  |
|  | 搜索 | 100 | 10 |  |  |
|  | 新闻 | 200 | 20 |  |  |
|  | 事件 | 200 | 20 |  |  |
|  | 激活 | 20 | 20 |  | 创作行为模拟。 |

#### 错误方案测试{#error-scenario-tests}

还必须测试错误情景，以确保系统能正确、适当地反应。 不仅在于错误本身的处理方式，还在于它可能对性能的影响。 例如：

* 当用户尝试在搜索框中输入无效搜索词时会发生什么情况
* 当搜索词过于笼统以致返回过多结果时会发生什么情况

在设计这些测试时，应记住并非所有方案都会定期发生。 但是，它们对整个系统的影响很重要。

| 错误方案 | 错误类型 | 否. 用户数 | Tx/秒（预期） | Tx/秒（已测试） | 描述 |
|---|---|---|---|---|---|
| 搜索组件过载 | 搜索全局通配符（星号） | 10 | 1 |  | 仅&amp;ast;&amp;ast;&amp;ast;。 |
|  | 停止单词 | 20 | 2 |  | 搜索停止词。 |
|  | 空字符串 | 10 | 3 |  | 搜索空字符串。 |
|  | 特殊字符 | 10 | 1 |  | 搜索特殊字符。 |

#### 耐力测试{#endurance-tests}

系统连续运行一段时间后才会遇到某些问题；不管是几个小时，甚至几天。 使用耐久性测试来测试在所需时间段内的恒定平均载荷。 然后可以分析任何性能退化。

| 方案 | 测试类型 | 否. 用户数 | Tx/秒（预期） | Tx/秒（已测试） | 描述 |
|---|---|---|---|---|---|
| 耐力测试（72小时） | 主页 | 10 | 1 |  |  |
|  | 搜索 | 10 | 3 |  |  |
|  | 新闻 | 20 | 2 |  |  |
|  | 事件 | 10 | 1 |  |  |
|  | 激活 | 1 | 3 |  | 创作行为模拟。 |

### 优化{#optimization}

在实施的后期阶段，您需要优化应用程序以实现／最大化性能目标。

必须测试所做的任何优化，以确保它们具有：

* 不影响功能
* 已通过负载测试进行验证，然后才能发布

提供一系列工具，帮助您进行负载生成、性能监控和／或结果分析:

* [JMeter](https://jakarta.apache.org/jmeter/)
* [加载运行器](https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview)
* [DetermyneInsideApps](https://www.determyne.com/) 
* [InfraRED](https://www.infraredsoftware.com/)
* [Java交互式用户档案](https://jiprof.sourceforge.net/)
* 更多...

优化后，您需要再次测试以确认影响。

### 报告 {#reporting}

需要持续的报告，以便让所有人了解状态，如之前在颜色编码中提到的，架构图可用于此。

完成所有测试后，您将要报告：

* 遇到任何严重错误
* 仍需进一步调查的非关键问题
* 在测试过程中作出的任何假设
* 测试中的任何建议

## 使用调度程序{#optimizing-performance-when-using-the-dispatcher}时优化性能

[调度程序](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)是Adobe的缓存和／或负载平衡工具。 使用Dispatcher时，您应考虑优化网站以实现缓存性能。

>[!NOTE]
>
>调度程序版本独立于AEM，但调度程序文档嵌入在AEM文档中。 请始终使用文档中嵌入的用于最新版AEM的Dispatcher文档。
>
>如果单击以前版本 AEM 文档中嵌入的 Dispatcher 文档链接，可能会重定向到此页面。

调度程序优惠了许多内置机制，您可以在网站利用这些机制时使用它们来优化性能。 本节将告诉您如何设计网站，以最大化缓存的优势。

>[!NOTE]
>
>它可能有助于您记住，调度程序将缓存存储在标准Web服务器上。 这意味着您：
>
>* 可以缓存所有可以存储为页面并使用URL请求的内容
>* 无法存储其他内容，如cookie、会话数据和表单数据。

>
>
通常，许多缓存策略都涉及选择好的URL，而不依赖这些附加数据。
>
>在Dispatcher版本4.1.11中，您还可以缓存响应头，请参阅[缓存HTTP响应头](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache)。


### 计算调度程序缓存比率{#calculating-the-dispatcher-cache-ratio}

缓存比率公式估计高速缓存处理的请求在进入系统的请求总数中所占的百分比。 要计算缓存比率，您需要：

* 请求总数。 Apache `access.log`中提供此信息。 有关详细信息，请参阅[官方Apache文档](https://httpd.apache.org/docs/2.4/logs.html#accesslog)。

* Publish实例提供的请求数。 此信息在实例的`request.log`中可用。 有关详细信息，请参阅[解释request.log](/help/sites-deploying/monitoring-and-maintaining.md#interpreting-the-request-log)和[查找日志文件](/help/sites-deploying/monitoring-and-maintaining.md#finding-the-log-files)。

计算缓存比率的公式为：

* （请求总数&#x200B;**减**&#x200B;发布上的请求数）**除以**&#x200B;的请求总数。

例如，如果请求总数为129491，而Publish实例所服务的请求数为58959，则缓存比率为：**(129491 - 58959)/129491= 54.5%**。

如果您没有一对一的发布程序／调度程序配对，您需要将所有调度程序和发布程序的请求添加到一起，以获得准确的度量。 另请参阅[建议的部署](/help/sites-deploying/recommended-deploys.md)。

>[!NOTE]
>
>为获得最佳性能，Adobe建议缓存比率为90%到95%。

#### 使用一致的页面编码{#using-consistent-page-encoding}

使用Dispatcher版本4.1.11，您可以缓存响应头。 如果不在Dispatcher上缓存响应标头，则如果在标头中存储页面编码信息，则可能会出现问题。 在这种情况下，当Dispatcher从缓存中提供页面时，将使用Web服务器的默认编码进行页面编码。 有两种方法可以避免此问题：

* 如果只使用一种编码，请确保Web服务器上使用的编码与AEM网站的默认编码相同。
* 使用HTML `head`部分的`<META>`标记设置编码，如以下示例所示：

```xml
        <META http-equiv="Content-Type" content="text/html; charset=EUC-JP">
```

#### 避免URL参数{#avoid-url-parameters}

如果可能，请避免要缓存的页面的URL参数。 例如，如果您有图片库，则不会缓存以下URL（除非调度程序已相应地配置[](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache)）:

```xml
www.myCompany.com/pictures/gallery.html?event=christmas&amp;page=1
```

但是，您可以按如下方式将这些参数放入页面URL:

```xml
www.myCompany.com/pictures/gallery.christmas.1.html
```

>[!NOTE]
>
>此URL调用与`gallery.html`相同的页面和模板。 在模板定义中，您可以指定呈现页面的脚本，也可以对所有页面使用相同的脚本。

#### 按URL{#customize-by-url}进行自定义

如果允许用户更改字体大小（或任何其他布局自定义），请确保URL中反映不同的自定义。

例如，Cookies不进行缓存，因此如果您将字体大小存储在Cookie（或类似机制）中，则缓存页面的字体大小不会保留。 因此，Dispatcher会随机返回任何字体大小的文档。

在URL中包含字体大小作为选择器可避免此问题：

```xml
www.myCompany.com/news/main.large.html
```

>[!NOTE]
>
>对于大多数布局方面，也可以使用样式表和／或客户端脚本。 通常，这些功能在缓存方面非常有效。
>
>这对于打印版本也很有用，在打印版本中，您可以使用URL，例如：
>
>`www.myCompany.com/news/main.print.html`
>
>使用模板定义的脚本覆盖，您可以指定用于呈现打印页的单独脚本。

#### 用作标题{#invalidating-image-files-used-as-titles}的图像文件无效

如果您以图片形式呈现页面标题或其他文本，则建议存储这些文件，以便在页面上的内容更新时删除它们：

1. 将图像文件放在与页面相同的文件夹中。
1. 对图像文件使用以下命名格式：

   `<page file name>.<image file name>`

例如，可以在`file myPage.title.gif`中存储页面`myPage.html`的标题。 如果页面已更新，则会自动删除此文件，因此对页面标题所做的任何更改都会自动反映在缓存中。

>[!NOTE]
>
>映像文件在AEM实例上不一定存在。 您可以使用动态创建图像文件的脚本。 然后，调度程序将文件存储在Web服务器上。

#### 导航{#invalidating-image-files-used-for-navigation}所使用的映像文件无效

如果将图片用于导航条目，则方法与标题基本相同，只是稍微复杂一些。 将所有导航图像与目标页面一起存储。 如果您使用两张图片作为正常和活动，则可以使用以下脚本：

* 正常情况下显示页面的脚本。
* 处理“.normal”请求并返回正常图片的脚本。
* 处理“.active”请求并返回已激活图片的脚本。

使用与页面相同的命名句柄创建这些图片非常重要，这样，内容更新会删除这些图片以及页面。

对于未修改的页面，图片仍保留在缓存中，尽管页面本身通常自动失效。

#### 个性化 {#personalization}

建议您将个性化限制在必要的位置。 说明原因：

* 如果您使用可自由自定义的开始页，则每次用户请求该页面时，都必须合成该页面。
* 相反，如果优惠10个不同的开始页，则可以缓存每个页，从而提高性能。

>[!TIP]
>有关配置Dispatcher缓存的更多详细信息，请参见[AEM Dispatcher缓存教程](https://experienceleague.adobe.com/docs/experience-manager-learn/dispatcher-tutorial/overview.html)及其[缓存受保护内容一节。](https://experienceleague.adobe.com/docs/experience-manager-learn/dispatcher-tutorial/chapter-1.html#dispatcher-tips-and-tricks)

如果您对每个页面进行个性化设置（例如，将用户的姓名放入标题栏），则会影响性能。

>[!TIP]
>有关缓存安全内容的信息，请参阅调度程序指南中的[缓存安全内容](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html)。

关于将受限内容和公开内容混合到一页上，您可能希望考虑一种策略，该策略利用Dispatcher中的服务器端包括，或通过浏览器中的Ajax在客户端包括。

>[!TIP]
>
>有关处理混合的公共和受限内容，请参阅[设置Sling Dynamic Include。](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-sling-dynamic-include.html)

#### 粘性连接{#sticky-connections}

[粘](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html#the-benefits-of-load-balancing) 性连接确保一个用户的文档都在同一台服务器上组成。如果用户离开此文件夹，稍后又返回到该文件夹，则连接仍然保持。 定义一个文件夹以保存要求网站具有粘性连接的所有文档。 尽量不要有其他文档。 如果您使用个性化的页面和会话数据，这会影响负载平衡。

#### MIME类型{#mime-types}

浏览器可以通过两种方式确定文件类型：

1. 通过其扩展(例如，`.html`、`.gif`、`.jpg`等。)
1. 按服务器随文件发送的MIME类型。

对于大多数文件，MIME类型隐含在文件扩展名中。 i.e.:

1. 通过其扩展(例如，`.html`、`.gif`、`.jpg`等。)
1. 按服务器随文件发送的MIME类型。

如果文件名没有扩展名，则显示为纯文本。

使用Dispatcher版本4.1.11，您可以缓存响应头。 如果未在Dispatcher上缓存响应头，请注意MIME类型是HTTP头的一部分。 因此，如果AEM应用程序返回的文件没有可识别的文件结尾，而是依赖MIME类型，则这些文件可能会错误地显示。

要确保正确缓存文件，请遵循以下准则：

* 确保文件始终具有正确的扩展名。
* 避免使用具有`download.jsp?file=2214`等URL的通用文件服务脚本。 重写脚本以使用包含文件规范的URL。 对于上一个示例，此值为`download.2214.pdf`。

## 备份性能{#backup-performance}

本节介绍一系列基准测试，用于评估AEM备份的性能以及备份活动对应用程序性能的影响。 AEM备份在运行时对系统造成很大负载，我们会测量这一情况，以及尝试调制这些效果的备份延迟设置的影响。 其目标是优惠一些参考数据，这些参考数据是关于实际配置和生产数据量中备份的预期性能，并就如何估计计划系统的备份时间提供指导。

### 引用环境{#reference-environment}

#### 物理系统{#physical-system}

此文档中报告的结果是从参考环境下运行的基准中获得的，该基准具有以下配置。 此配置设计为类似于数据中心中的典型生产环境:

* H-P ProLiant DL380 G6,8个CPU x 2.533 GHz
* 串行连接SCSI 300GB 10,000RPM驱动器
* 硬件RAID控制器；RAID0+5阵列中有8个驱动器
* VMware映像CPU x 2英特尔至强E5540 @ 2.53GHz
* RedHat Linux 2.6.18-194.el5;Java 1.6.0_29
* 单作者实例

此服务器上的磁盘子系统速度很快，它代表可能用于生产服务器的高性能RAID配置。 备份性能对磁盘性能可能很敏感，而此环境的结果反映了在非常快速的RAID配置上的性能。 VMWare映像配置为在RAID阵列上具有物理驻留在本地磁盘存储中的单个大磁盘卷。

AEM配置将存储库和数据存储放在同一逻辑卷上，并与所有操作系统和AEM软件一起放置。 备份的目标目录也位于此逻辑文件系统中。

#### 数据卷{#data-volumes}

下表说明了备份基准中使用的数据卷的大小。 首先安装初始基准内容，然后添加额外的已知数据量以增加备份内容的大小。 备份将以特定增量创建，以代表内容和一天内可能产生的内容的大幅增加。 内容（页面、图像、标记）的分发大致基于逼真的制作资产组合。 页面、图像和标记最多限制为800个子页面。 每个页面将包括标题、Flash、文本／图像、视频、幻灯片、表单、表、云和传送组件。 图像将从400个大小从37 kB到594 kB的唯一文件池上传。

|内容|节点|页面|图像|标记|
|---|---|---|---|---|
|基本安装|69 610|562|256|237|
|用于增量备份的小内容||+100|+2|+2|
|用于完整备份的大内容||+10 000|+100|+100||

每次重复时添加的附加内容集会重复备份基准。

#### 基准方案{#benchmark-scenarios}

备份基准测试涵盖两种主要情况：在系统处于大负荷时进行备份，在系统空闲时进行备份。 尽管一般建议在AEM尽可能空闲时执行备份，但在某些情况下，必须在系统负载不足时运行备份。

* **空闲状态** -在AEM上执行备份时不使用其他活动。
* **在“Load** - Backups（负载——备份）”下，当系统从联机进程负载不足80%时执行备份。备份延迟会有所不同，因此会看到对负载的影响。

备份时间和结果备份的大小从AEM服务器日志中获取。 通常建议在AEM空闲时（如半夜）安排非时备份。 此方案代表建议的方法。

加载将由页面创建／删除、遍历和查询组成，其中大部分加载来自页面遍历和查询。 添加和删除过多页面会不断增大工作区大小并阻止备份完成。 脚本将使用的加载分布为75%的页面遍历、24%的查询和1%的页面创建（单个级别没有嵌套子页面）。 在空闲系统上，每秒的峰值平均事务数是通过4个并发线程实现的，这是在负载下测试备份时使用的。

负载对备份性能的影响可以通过此应用程序负载时和不时的性能差异来估计。 通过比较每小时事务处理中的方案吞吐量，以及在进行并发备份时，以及在使用不同的“备份延迟”设置时，备份对应用程序吞吐量的影响，可以发现备份对应用程序吞吐量的影响。

* **延迟设置** -对于多种情况，我们还使用10毫秒（默认）、1毫秒和0毫秒的值来更改备份延迟设置，以了解此设置对备份性能的影响。
* **备份类型** -所有备份都是存储库的外部备份，存储库创建到备份目录时不创建zip文件，但在比较中，tar命令直接使用的情况除外。由于增量备份不能创建到zip文件，或者以前的完全备份是zip文件，因此备份目录方法在生产情况下最常使用。

### 结果摘要{#summary-of-results}

#### 备份时间和吞吐量{#backup-time-and-throughput}

这些基准测试的主要结果是显示备份时间随着备份类型和数据总量的不同而如何变化。 下图显示了使用默认备份配置获得的备份时间，它是页总数的函数。

![chlimage_1-81](assets/chlimage_1-81.png)

空闲实例的备份时间相当一致，无论是完整备份还是增量备份，平均为0.608 MB/s（请参见下图）。 备份时间只是备份数据量的函数。 完成完整备份的时间会随着页面总数的增加而明显增加。 完成增量备份的时间也会随着页面总数而增加，但速度要低得多。 由于备份的数据量相对较少，完成增量备份所花费的时间要短得多。

备份的大小是完成备份所花费时间的主要决定因素。 下图显示了作为最终备份大小的函数所用的时间。

![chlimage_1-82](assets/chlimage_1-82.png)

此图表说明增量备份和完整备份都遵循简单的大小与时间模式，我们可以将其作为吞吐量来衡量。 空闲实例的备份时间相当一致，平均为0.61 MB/秒，而不管基准环境上的完整备份或增量备份。

#### 备份延迟{#backup-delay}

提供备份延迟参数以限制备份可能干扰生产工作负载的范围。 该参数指定等待时间（以毫秒为单位），该等待时间会逐个地分散到备份操作中。 整体效果部分取决于受影响的文件的大小。 以MB/秒为单位衡量备份性能提供了一种比较延迟对备份的影响的合理方法。

* 与常规应用程序负载同时运行备份将对常规负载的吞吐量产生负面影响。
* 影响可能很小（只有5%）或非常显着，导致吞吐量下降75%，这可能比任何情况都更取决于应用程序。
* 备份对CPU的负载并不大，因此与I/O密集型工作负载相比，对CPU密集型生产工作负载的影响更小。

![chlimage_1-83](assets/chlimage_1-83.png)

为了比较使用文件系统备份（使用“tar”）来备份同一存储库文件的吞吐量。 tar的性能相当，但略高于将延迟设置为零的备份。 即使是小延迟也会大大降低备份吞吐量，而默认延迟10毫秒也会大大降低吞吐量。 如果备份可能在应用程序整体使用率很低或应用程序完全空闲时进行，则可能需要将延迟减少到默认值以下，以便允许备份更快地进行。

当前备份的应用程序吞吐量的实际影响取决于应用程序和基础架构详细信息。 延迟值的选择应通过应用程序的经验分析进行，但应尽可能小，以便能够尽快完成备份。 由于选择延迟值与对应用程序吞吐量的影响之间只存在微弱的关联，因此选择延迟应有利于缩短总体备份时间，以最大限度地减少备份的总体影响。 完成备份需要8小时，但吞吐量影响为-20% ，与完成备份需要2小时相比，备份的总体影响可能更大，但吞吐量影响为-30%。

### 引用 {#references}

* [管理——备份和恢复](/help/sites-administering/backup-and-restore.md)
* [管理——容量和卷](/help/managing/best-practices-further-reference.md#capacity-and-volume)
