---
title: 性能测试的最佳实践
seo-title: 性能测试的最佳实践
description: 本文概述了用于性能测试的总体战略和方法，以及一些可用于协助测试的工具。
seo-description: 本文概述了用于性能测试的总体战略和方法，以及一些可用于协助测试的工具。
uuid: ab8720d6-b864-4d00-9e07-2e1699cfe7db
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 669018a0-f6ef-42b2-9c6f-83d7dd5a7095
exl-id: fcac75e1-15c1-4a37-8d43-93c95267b903
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1925'
ht-degree: 0%

---

# 性能测试最佳实践{#best-practices-for-performance-testing}

## 简介 {#introduction}

性能测试是任何AEM部署的重要部分。 根据客户要求，可以对发布实例、创作实例或两者执行性能测试。

本文档将概述执行性能测试的总体战略和方法，以及Adobe为协助该过程而提供的一些工具。 最后，我们将从代码分析和系统配置角度分析AEM 6中可用的一些工具，以帮助进行性能调整。

### 模拟现实{#simulating-reality}

执行性能测试时，最重要的是确保尽可能地模拟生产环境。 虽然这通常很困难，但必须确保这些测试的准确性。 在设计性能测试时，必须考虑以下几点：

* 类似于生产的内容

AEM中的许多性能测量（如查询响应时间）可能会受系统中内容大小的影响。 务必确保测试环境尽可能接近生产数据的副本。

* 生产代码

生产中部署的AEM版本和修补程序在测试环境中应该相同。 此外，还必须测试部署到生产环境的代码版本。

* 类似生产的硬件和网络配置

如果没有与生产环境尽可能相似的环境，测试将毫无意义。 理想情况下，硬件规范、网络接口、负载平衡器和CDN应与测试环境中的生产环境相同。

* 生产负载

在系统负载过重之前，不会看到许多性能问题。 良好的性能测试应该模拟生产系统在其高峰时所受的负载。

### 设置目标{#setting-goals}

在开始性能测试之前，必须设置非功能要求以指定负载和响应时间。 如果您从现有系统迁移，请确保响应时间与当前生产值类似。 对于负载，最好采用当前峰值负载，将其加倍。 这将确保网站能够在增长时继续正常运行。

### 工具 {#tools}

市场上有许多商品化的性能测试工具。 运行负载生成工具时，必须确保正在执行测试的计算机具有足够的网络带宽。 否则，一旦测试机达到其连接限制，将不会在被测试的环境中产生额外负载。

#### 测试工具{#testing-tools}

* Adobe的&#x200B;**Tough Day**&#x200B;工具可用于在AEM实例上生成负载并收集性能数据。 Adobe的AEM工程团队实际上使用该工具对AEM产品本身进行负载测试。 在艰难时刻执行的脚本是通过属性文件和JMX XML文件配置的。 有关更多信息，请参阅[艰难日期文档](/help/sites-developing/tough-day.md)。

* AEM提供开箱即用的工具，可快速查看有问题的查询、请求和错误消息。 有关更多信息，请参阅操作仪表板文档的[诊断工具](/help/sites-administering/operations-dashboard.md#diagnosis-tools)部分。
* Apache提供了名为&#x200B;**JMeter**&#x200B;的产品，可用于性能和负载测试以及功能行为。 它是开源软件，可免费使用，但其功能集比企业产品要小，学习曲线也更陡峭。 JMeter可在Apache的网站上找到，网址为[https://jmeter.apache.org/](https://jmeter.apache.org/)

* **Load Runner** 是企业级负载测试产品。提供了免费的评估版本。 有关更多信息，请访问[https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview](https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview)

* 还可以使用基于云的负载测试工具，如[Neustar](https://www.neustar.biz/services/web-performance/load-testing)。
* 在测试移动或响应式网站时，需要使用一组单独的工具。 它们通过限制网络带宽来工作，模拟较慢的移动连接（如3G或EDGE）。 使用范围更广的工具包括：

   * **[网络链接调节器](https://nshipster.com/network-link-conditioner/)**  — 它提供易于使用的UI，在网络堆栈上工作级别较低。其中包括OS X和iOS版本；[](https://nshipster.com/network-link-conditioner/)
   * [**Charles**](https://www.charlesproxy.com/)  — 一种Web调试代理应用程序，除了其他多种用途外，还提供网络限制。提供了适用于Windows、OS X和Linux的版本。[](https://www.charlesproxy.com/)

#### 优化工具{#optimization-tools}

**监测**

[监控性能](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance)文档是工具和方法的有用资源，可用于诊断问题和确定调整区域的精确位置。

**触屏UI中的开发人员模式**

AEM 6触屏UI中的新增功能之一是开发人员模式。 正如作者可以在编辑模式和预览模式之间切换一样，开发人员也可以在创作UI中切换到开发人员模式，以查看页面上每个组件的渲染时间以及查看任何错误的堆栈跟踪。 有关开发人员模式的更多信息，请参阅此[CQ Gems演示文稿](https://docs.adobe.com/content/ddc/en/gems/aem-6-0-developer-mode.html)。

**使用rlog.jar读取请求日志**

要更全面地分析AEM系统上的请求日志，可使用`rlog.jar`搜索AEM生成的`request.log`文件并对其进行排序。 `/crx-quickstart/opt/helpers`文件夹中的AEM安装中包含此jar文件。 有关日志工具和请求日志的一般信息，请参阅[监视和维护](/help/sites-deploying/monitoring-and-maintaining.md)文档。

**解释查询工具**

ACS AEM Tools中的[Explain Query Tool](/help/sites-administering/operations-dashboard.md#explain-query)可用于查看运行查询时使用的索引。 这在优化慢速运行的查询时非常有用。

**PageSpeed工具**

Google的PageSpeed工具提供了站点分析，以便遵循页面性能的最佳实践，并且还提供了可与Apache实例上的调度程序一起安装的插件，以进行其他优化。 有关更多信息，请参阅[PageSpeed Tools网站](https://developers.google.com/speed/pagespeed/)。

## 创作环境 {#author-environment}

### 执行测试{#performing-tests}

要在创作环境中进行性能测试，必须模拟生产作者的体验。 这意味着作者安装必须包含您为生产作者实例就地的所有组件、OSGi包、UI自定义、自定义索引以及任何其他添加内容。

有许多自动化框架可供使用，专为性能和负载测试而设计。 可以在这些工具中记录自定义脚本，然后进行回放，以模拟同时执行类似内容创建和激活活动的作者数量达到峰值。 建议您使用“艰难时刻”工具来模拟上传数千个资产或激活大量页面等活动。

对于需要大量资产加载或页面创作的环境类型，必须使用诸如艰难时刻之类的工具，以确保环境在峰值负载下能够高效运行。 [](/help/sites-administering/webdav-access.md) WebDAV是一款无需编写脚本的工具，也可用于加载大量资产。

#### MongoDB特定步骤{#mongodb-specific-steps}

在具有MongoDB后端的系统上， AEM提供了多个[JMX](/help/sites-administering/jmx-console.md) MBean，在执行负载或性能测试时需要监控这些JMX MBean:

* **统一缓存统计信息** MBean。 通过转到：

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

对于名为&#x200B;**Document-Diff**&#x200B;的缓存，点击率应大于`.90`。 如果点击率低于90%，则可能需要修改`DocumentNodeStoreService`配置。 Adobe产品支持可以为您的环境推荐最佳设置。

* **Oak存储库统计数据** Mbean。 通过转到：

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

**ObservationQueueMaxLength**&#x200B;部分将显示Oak观察队列中在最近几小时、几分钟、几秒和几周内的事件数。 在“每小时”部分中查找最大事件数。 需要将此数字与`oak.observation.queue-length`设置进行比较，该设置可在[OSGi控制台](/help/sites-deploying/web-console.md)的&#x200B;**SlingRepositoryManager**&#x200B;组件中找到。 如果观察队列显示的最大数量超过`queue-length`设置，请联系Adobe支持部门以获取有关提高该设置的帮助。 默认设置为1,000，但大多数部署通常需要将其增加到20,000或50,000。

## 发布环境 {#publish-environment}

### 执行测试{#performing-tests-1}

部署中需要进行加载测试的最重要部分是面向最终用户的发布或调度程序环境。

第三方自动化测试工具可用于测试网站的性能。 利用这些工具，可记录用户将在网站上完成的步骤，并同时运行其中的许多会话，以模拟生产网站的典型负载。

大多数生产网站都实施了优化，如调度程序缓存和内容交付网络就位。 测试时，您需要确保这些优化也适用于测试环境。 除了监控最终用户的响应时间之外，您还需要监控发布服务器和调度程序上的系统量度，以确保系统不受硬件资源的限制。

在不需要高级别个性化的系统上，调度程序应缓存大多数请求。 因此，发布实例的负载应保持相对平缓。 如果需要高级别的个性化，建议对个性化内容使用iFrame或AJAX请求等技术，以便允许尽可能多的调度程序缓存。

对于基本测试，Apache Bench可用于测量Web服务器响应时间，并帮助创建负载以测量内存泄漏等内容。 有关详细信息，请参阅[监控文档](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench)中的示例。

## 性能问题疑难解答{#troubleshooting-performance-issues}

在创作实例上运行性能测试后，需要调查、诊断和解决任何问题。 在执行分析和解决问题时，您可以使用多种工具和技术：

* 您可以在操作仪表板中检查[请求性能日志](/help/sites-administering/operations-dashboard.md#request-performance)。 此工具可用于识别页面速度缓慢的请求
* 使用[查询性能工具](/help/sites-administering/operations-dashboard.md#query-performance)分析慢速运行的查询

* 观看错误列表，查看错误或警告。 有关更多信息，请参阅[日志记录](/help/sites-deploying/configure-logging.md)
* 监视系统硬件资源，如内存和CPU利用率、磁盘I/O或网络I/O。这些资源通常是性能瓶颈的根源
* 优化页面的架构和页面的寻址方式，以最大限度地减少URL参数的使用，从而尽可能多地执行缓存
* 请参阅[性能优化](/help/sites-deploying/configuring-performance.md)和[性能调整提示](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)文档

* 如果在创作实例上编辑某些页面或组件时出现问题，请使用触屏UI开发人员模式来检查相关页面。 这将提供页面上每个内容区域的划分及其加载时间
* 缩小网站上的所有JS和CSS。 有关如何执行此操作的详细信息，请参阅此[博客文章](https://blogs.adobe.com/foxes/enable-js-and-css-minification/)。
* 从组件中消除嵌入的CSS和JS。 这些请求应随客户端库一起包含和缩小，以最大限度地减少呈现页面所需的请求数
* 使用诸如Chrome的“网络”选项卡之类的浏览器工具来检查服务器请求，并查看哪些请求花费的时间最长。

确定问题区域后，可以检查应用程序代码以优化性能。 任何性能不佳的开箱即用AEM功能均可通过Adobe支持解决。
