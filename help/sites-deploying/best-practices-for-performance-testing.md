---
title: 性能测试最佳实践
seo-title: Best Practices for Performance Testing
description: 本文概述用于性能测试的整体策略和方法，以及在此过程中提供帮助的一些工具。
seo-description: This article outlines the overall strategies and methodologies used for performance testing as well as some of the tools that are available to assist in the process.
uuid: ab8720d6-b864-4d00-9e07-2e1699cfe7db
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 669018a0-f6ef-42b2-9c6f-83d7dd5a7095
exl-id: fcac75e1-15c1-4a37-8d43-93c95267b903
source-git-commit: e8320b1dac681fd2c9e749344e8c126487d840ba
workflow-type: tm+mt
source-wordcount: '1897'
ht-degree: 0%

---

# 性能测试最佳实践{#best-practices-for-performance-testing}

## 简介 {#introduction}

性能测试是任何AEM部署的重要组成部分。 根据客户要求，可以对发布实例、创作实例或两者执行性能测试。

本文档将概述执行性能测试的总体策略和方法，以及Adobe为协助该过程而提供的一些工具。 最后，我们将从代码分析和系统配置角度分析AEM 6中可用于帮助进行性能调整的某些工具。

### 模拟现实 {#simulating-reality}

执行性能测试时，最重要的是确保尽可能模拟生产环境。 虽然这通常很困难，但必须确保这些测试的准确性。 在设计性能测试时，必须考虑以下几点：

* 生产类内容

AEM中的许多性能衡量指标（如查询响应时间）都可能受系统上内容的大小影响。 确保测试环境尽可能接近生产数据的副本非常重要。

* 生产代码

在生产环境中部署的AEM版本和修补程序应在测试环境中相同。 在部署到生产环境的代码版本上进行测试也很重要。

* 类似生产环境的硬件和网络配置

如果没有与生产环境尽可能相似的环境，测试将毫无意义。 理想情况下，硬件规格、网络接口、负载平衡器和CDN应与测试环境中的生产环境相同。

* 生产负载

直到系统负载较重时，才会出现许多性能问题。 良好的性能测试应该模拟生产系统在其峰值下将承受的负载。

### 设置目标 {#setting-goals}

在开始性能测试之前，必须设置非功能要求以指定负载和响应时间。 如果您要从现有系统迁移，请确保响应时间与当前的生产值类似。 对于载荷，最好取当前峰值载荷，再加倍。 这将确保网站在增长时能够继续保持良好的性能。

### 工具 {#tools}

市面上有很多市面上可买到的性能测试工具。 运行负载生成工具时，必须确保执行测试的计算机具有足够的网络带宽。 否则，一旦测试计算机达到其连接的限制，则不会在受测试的环境中生成额外负载。

#### 测试工具 {#testing-tools}

* Adobe **艰难的一天** 工具可用于在AEM实例上生成负载并收集性能数据。 Adobe的AEM工程团队实际上使用该工具对AEM产品本身进行负载测试。 在Tough Day中执行的脚本通过属性文件和JMX XML文件进行配置。 欲了解更多信息，请参见 [Hearth Day文档](/help/sites-developing/tough-day.md).

* AEM提供了开箱即用的工具，用于快速查看有问题的查询、请求和错误消息。 欲了解更多信息，请参见 [诊断工具](/help/sites-administering/operations-dashboard.md#diagnosis-tools) 部分（位于操作仪表板文档中）。
* Apache提供了一个名为的产品 **JMet** 可用于性能和负载测试以及功能行为。 它是开源软件，使用起来很自由，但功能集比企业产品更小，学习曲线也更陡峭。 您可以在Apache的网站上找到JMeter，网址为 [https://jmeter.apache.org/](https://jmeter.apache.org/)

* **加载运行程序** 是一种企业级负载测试产品。 提供了免费评估版。 欲知更多信息，请访问 [https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview](https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview)

* 基于云的负载测试工具，如 [Neustar](https://www.neustar.biz/services/web-performance/load-testing) 也可以使用。
* 在测试移动或响应式网站时，需要使用一组单独的工具。 它们的工作方式是限制网络带宽，模拟速度较慢的移动连接，如3G或EDGE。 使用范围更广的工具包括：

   * **[网络链路调节器](https://nshipster.com/network-link-conditioner/)**  — 它提供易于使用的UI，在网络栈栈中以相当低的级别工作。 它包括OS X和iOS的版本；
   * [**Charles**](https://www.charlesproxy.com/)  — 一个Web调试代理应用程序，除了若干其他用途外，还提供网络调节。 提供了适用于Windows、OS X和Linux的版本。

#### 优化工具 {#optimization-tools}

**监测**

此 [监控性能](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance) 文档是有关工具和方法的有用资源，可用于诊断问题并查明需要调整的区域。

**触屏UI中的开发人员模式**

AEM 6触屏UI中的一项新增功能是开发人员模式。 就像作者可以在编辑和预览模式之间切换一样，开发人员可以在作者UI中切换到开发人员模式，以查看页面上每个组件的渲染时间并查看任何错误的栈栈跟踪。 有关开发人员模式的更多信息，请参阅此 [CQ Gems演示](https://docs.adobe.com/content/ddc/en/gems/aem-6-0-developer-mode.html).

**使用rlog.jar读取请求日志**

要更全面地分析AEM系统上的请求日志，请执行以下操作 `rlog.jar` 可用于搜索和排序 `request.log` AEM生成的文件。 此jar文件包含在中的AEM安装中 `/crx-quickstart/opt/helpers` 文件夹。 有关rlog工具和一般请求日志的更多信息，请参阅 [监控和维护](/help/sites-deploying/monitoring-and-maintaining.md) 文档。

**Explain查询工具**

此 [说明查询工具](/help/sites-administering/operations-dashboard.md#explain-query) 在ACS中，AEM工具可用于查看运行查询时使用的索引。 在优化运行缓慢的查询时，这可能非常有用。

**PageSpeed工具**

Google的PageSpeed工具提供网站分析，以符合页面性能最佳实践，并提供一个插件，可与Dispatcher一起安装在Apache实例上以进行其他优化。 欲了解更多信息，请参见 [PageSpeed Tools网站](https://developers.google.com/speed/pagespeed/).

## 创作环境 {#author-environment}

### 执行测试 {#performing-tests}

要在创作环境中执行性能测试，必须模拟生产作者的体验。 这意味着创作安装必须包含所有组件、OSGi包、UI自定义、自定义索引以及您为生产创作实例设置的任何其他附加内容。

有许多为性能和负载测试而设计的自动化框架。 自定义脚本可以记录在这些工具中，然后回放以模拟同时执行类似内容创建和激活活动的作者数量峰值。 建议您使用“困难日”工具来模拟上传数千个资产或激活大量页面等活动。

对于需要大量资产加载或页面创作的环境类型，必须使用Tough Day等工具，以确保环境在峰值负载下高效运行。 [WebDAV](/help/sites-administering/webdav-access.md) 是一种不需要编写脚本的工具，也可用于加载大量资产。

#### MongoDB特定步骤 {#mongodb-specific-steps}

在具有MongoDB后端的系统上，AEM提供了多个 [JMX](/help/sites-administering/jmx-console.md) 执行负载或性能测试时需要监视的MBean：

* 此 **已整合的缓存统计信息** MBean。 可以通过以下位置直接访问它：

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

对于命名的缓存 **Document-Diff**，则命中率应大于 `.90`. 如果点击率低于90%，您可能需要修改您的 `DocumentNodeStoreService` 配置。 Adobe产品支持可为您的环境推荐最佳设置。

* 此 **Oak存储库统计数据** Mbean。 可以通过以下位置直接访问它：

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

此 **ObservationqueueMaxLength** 部分将显示Oak观察队列中过去小时、分钟、秒和周的事件数。 在“每小时”部分中查找事件的最大数量。 此数字需要与 `oak.observation.queue-length` 设置。 如果为观察队列显示的最高数量超过 `queue-length` 设置：

1. 创建名为的文件： `com.adobe.granite.repository.impl.SlingRepositoryManager.cfg` 包含参数 `oak.observation.queue‐length=50000`
1. 将其放置在/crx--quickstart/install文件夹下。

>[!NOTE]
>另请参阅知识库文章，网址为 [AEM 6.x |性能调整提示](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)

默认设置为10,000，但大多数部署通常需要将其增加到20,000或50,000。

## 发布环境 {#publish-environment}

### 执行测试 {#performing-tests-1}

部署中需要接受负载测试的最重要部分是面向最终用户的Publish或Dispatcher环境。

可以使用第三方自动化测试工具来测试网站的性能。 这些工具允许您记录用户在网站上将执行的步骤，并同时运行多个会话，以模拟生产网站的典型负载。

大多数生产网站都实施了优化，例如Dispatcher缓存和已建立的内容交付网络。 在测试时，您需要确保这些优化对测试环境也可用。 除了监控最终用户的响应时间之外，您还需要监控发布服务器和调度程序上的系统指标，以确保系统不受硬件资源的限制。

在不要求高级别个性化的系统上，Dispatcher应缓存大多数请求。 因此，发布实例上的负载应保持相对平坦。 如果需要高级别的个性化，建议对个性化内容使用iFrame或AJAX请求等技术，以便允许尽可能多的Dispatcher缓存。

对于基本测试，Apache Bench可用于测量Web服务器的响应时间，并帮助创建负载以测量内存泄漏等情况。 有关更多信息，请参阅 [监控文档](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench).

## 性能问题疑难解答 {#troubleshooting-performance-issues}

在创作实例上运行性能测试后，需要对任何问题进行调查、诊断和解决。 在执行分析和解决问题时，可以使用多种工具和技术：

* 您可以检查 [请求性能日志](/help/sites-administering/operations-dashboard.md#request-performance) 操作功能板中的。 此工具可用于识别较慢的页面请求
* 使用分析运行缓慢的查询 [查询性能工具](/help/sites-administering/operations-dashboard.md#query-performance)

* 观察错误日志中的错误或警告。 有关更多信息，请参阅 [日志记录](/help/sites-deploying/configure-logging.md)
* 监视系统硬件资源，如内存和CPU利用率、磁盘I/O或网络I/O。这些资源通常是性能瓶颈的原因
* 优化页面的架构以及如何寻址页面，以最大限度地减少URL参数的使用，从而允许尽可能多的缓存
* 请遵循 [性能优化](/help/sites-deploying/configuring-performance.md) 和 [性能调整提示](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html) 文档

* 如果编辑创作实例上的某些页面或组件时出现问题，请使用TouchUI开发人员模式检查有问题的页面。 这将提供页面上每个内容区域的划分及其加载时间
* 缩小站点上的所有JS和CSS。 有关如何执行此操作的更多信息，请参阅此 [博客帖子](https://blogs.adobe.com/foxes/enable-js-and-css-minification/).
* 从组件中消除嵌入的CSS和JS。 它们应该包含在客户端库中，并与客户端库一起缩小，以最大程度地减少渲染页面所需的请求数
* 使用诸如Chrome的“网络”选项卡之类的浏览器工具来检查服务器请求，并查看哪些请求花费的时间最长。

一旦识别出问题区域，就可以检查应用程序代码以优化性能。 任何开箱即用的AEM功能无法正确执行，都可以通过Adobe支持来解决。
