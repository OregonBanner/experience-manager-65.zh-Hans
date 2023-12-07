---
title: 性能测试的最佳实践
description: 了解用于性能测试的整体策略和方法，以及可用于帮助此过程的一些工具。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: fcac75e1-15c1-4a37-8d43-93c95267b903
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1790'
ht-degree: 0%

---

# 性能测试的最佳实践{#best-practices-for-performance-testing}

## 简介 {#introduction}

性能测试是任何AEM部署的重要组成部分。 根据客户要求，可以对发布实例、创作实例或两者执行性能测试。

本文档概述了执行性能测试的总体策略和方法，以及Adobe为帮助该过程而提供的一些工具。 最后，从代码分析和系统配置的角度阅读AEM 6中可用于帮助进行性能调整的工具分析。

### 模拟现实 {#simulating-reality}

进行性能测试时，请确保尽可能模拟生产环境。 虽然此类任务通常比较困难，但必须确保这些测试的准确性。 在设计性能测试时，必须考虑以下几点：

* 生产类内容

AEM中的许多性能度量（如查询响应时间）都可能会受系统上内容的大小影响。 确保测试环境尽可能接近生产数据的副本很重要。

* 生产代码

在生产环境中部署的AEM版本和修补程序应该与测试环境中相同。 在部署到生产环境的代码版本上进行测试也很重要。

* 生产类硬件和网络配置

如果没有与生产环境尽可能相似的环境，这些测试就毫无意义。 理想情况下，硬件规格、网络接口、负载平衡器和CDN应与测试环境中的生产环境相同。

* 生产负载

在系统负载较重之前，不会出现许多性能问题。 良好的性能测试应该模拟生产系统在峰值时的负荷。

### 设置目标 {#setting-goals}

开始性能测试之前，必须设置非功能要求以指定加载和响应时间。 如果您要从现有系统迁移，请确保响应时间与当前的生产值类似。 对于负载，最好取当前峰值负载并将其加倍。 这样做可以确保网站在增长过程中能够继续保持良好的性能。

### 工具 {#tools}

市场上有许多市售的性能测试工具。 运行负载生成工具时，必须确保执行测试的计算机具有足够的网络带宽。 否则，一旦测试计算机达到其连接的限制，则不会在受测试的环境中生成额外负载。

#### 测试工具 {#testing-tools}

* Adobe **艰难的一天** 工具可用于在AEM实例上生成负载并收集性能数据。 Adobe的AEM工程团队实际上使用该工具来对AEM产品本身进行负载测试。 在“困难日”中执行的脚本通过属性文件和JMX XML文件进行配置。 欲了解更多信息，请参见 [Touch Day文档](/help/sites-developing/tough-day.md).

* AEM提供了开箱即用的工具，用于快速查看有问题的查询、请求和错误消息。 欲了解更多信息，请参见 [诊断工具](/help/sites-administering/operations-dashboard.md#diagnosis-tools) 部分。
* Apache提供了一个名为的产品 **JMet** 可用于性能和负载测试，以及功能行为。 它是一款开源软件，可以免费使用，但功能集比企业产品更小，学习曲线也更陡峭。 您可以在Apache网站上找到JMeter，网址为 [https://jmeter.apache.org/](https://jmeter.apache.org/)

* **加载运行程序** 是企业级负载测试产品。 提供了免费的评估版。 欲知更多信息，请访问 [https://www.microfocus.com/en-us/portfolio/performance-engineering/overview](https://www.microfocus.com/en-us/portfolio/performance-engineering/overview)

* 网站负载测试工具，如 [韦尔卡拉](https://vercara.com/website-performance-management) 也可以使用。
* 测试移动或响应式网站时，必须使用一组单独的工具。 它们通过调节网络带宽来工作，模拟速度较慢的移动连接，如3G或EDGE。 使用范围更广的工具包括：

   * **[网络链路调节器](https://nshipster.com/network-link-conditioner/)**  — 它提供了易于使用的UI，并且在网络栈栈上以相当低的级别工作。 它包括OS X和iOS的版本；
   * [**Charles**](https://www.charlesproxy.com/)  — 一个Web调试代理应用程序，除了若干其他用途外，还提供网络调节。 为Windows、OS X和Linux®提供了版本。

#### 优化工具 {#optimization-tools}

**监控**

此 [监控性能](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance) 文档是有关工具和方法的有用资源，可用于诊断问题并查明需要调整的区域。

**触屏UI中的开发人员模式**

AEM 6触控UI中的一项新增功能是开发人员模式。 就像作者可以在编辑和预览模式之间切换一样，开发人员也可以在作者UI中切换到开发人员模式。 这样，您就可以查看页面上每个组件的渲染时间，并查看任何错误的栈栈跟踪。 有关开发人员模式的更多信息，请参阅此 [CQ Gems演示](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2014/aem-developer-mode.html?lang=en).

**使用rlog.jar读取请求日志**

要更全面地分析AEM系统上的请求日志， `rlog.jar` 可用于搜索和排序 `request.log` AEM生成的文件。 此jar文件包含在中的AEM安装 `/crx-quickstart/opt/helpers` 文件夹。 有关rlog工具和请求登录常规的详细信息，请参阅 [监控和维护](/help/sites-deploying/monitoring-and-maintaining.md) 文档。

**Explain查询工具**

此 [说明查询工具](/help/sites-administering/operations-dashboard.md#explain-query) 在ACS中，AEM工具可用于查看运行查询时使用的索引。 此工具在优化运行缓慢的查询时很有用。

**PageSpeed Tools**

Google的PageSpeed工具提供网站分析，以遵守页面性能最佳实践，并提供可与Apache实例上的Dispatcher一起安装的插件，以进行其他优化。
请参阅 [PageSpeed Tools网站](https://developers.google.com/speed).

## 创作环境 {#author-environment}

### 执行测试 {#performing-tests}

要在创作环境中执行性能测试，必须模拟生产作者的体验。 即，创作安装必须包含所有组件、OSGi包、UI自定义、自定义索引以及您为生产创作实例设置的任何其他附加内容。

有许多可用于性能和负载测试的自动化框架。 自定义脚本可以记录在这些工具中，然后回放以模拟同时执行类似内容创建和激活活动的作者数量峰值。 建议您使用“Touch Day”工具来模拟上传数千个资产或激活大量页面等活动。

对于需要大量资产加载或页面创作的环境类型，必须使用“Touch Day”等工具。 这样做可确保环境在峰值负载下高效运行。 [WebDAV](/help/sites-administering/webdav-access.md) 是一种不需要编写脚本的工具，也可用于加载大量资产。

#### MongoDB特定步骤 {#mongodb-specific-steps}

在具有MongoDB后端的系统上，AEM提供了多个 [JMX](/help/sites-administering/jmx-console.md) 执行负载或性能测试时必须监视的MBean：

* 此 **已整合的缓存统计数据** MBean。 可以通过以下位置直接访问它：

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

对于命名的缓存 **Document-Diff**，则命中率应大于 `.90`. 如果点击率降至90%以下，您可能需要编辑 `DocumentNodeStoreService` 配置。 Adobe产品支持可为您的环境推荐最佳设置。

* 此 **Oak存储库统计数据** Mbean。 可以通过以下位置直接访问它：

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

此 **ObservationqueueMaxLength** 部分显示Oak的观察队列中在过去小时、分钟、秒和周内的事件数。 在“每小时”部分中查找事件的最大数量。 将此数字与 `oak.observation.queue-length` 设置。 如果为观察队列显示的最大数量超过 `queue-length` 设置：

1. 创建名为的文件： `com.adobe.granite.repository.impl.SlingRepositoryManager.cfg` 包含参数 `oak.observation.queue‐length=50000`
1. 将其放在/crx-quickstart/install文件夹下。

>[!NOTE]
>请参阅 [AEM 6.x |性能调整提示](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=en)

默认设置为10,000，但大多数部署都必须将其增加到20,000或50,000。

## 发布环境 {#publish-environment}

### 执行测试 {#performing-tests-1}

部署中必须接受负载测试的最重要部分是面向最终用户的发布或Dispatcher环境。

可以使用第三方自动化测试工具来测试网站的性能。 这些工具允许您记录用户在网站上执行的步骤，并同时运行其中的许多会话，以模拟生产网站的典型负载。

大多数生产网站都已实施优化，例如Dispatcher缓存和内容交付网络。 测试时，请确保这些优化也适用于测试环境。 除了监控最终用户的响应时间，还要监控发布服务器和调度程序上的系统指标，以确保系统不受硬件资源的限制。

在不要求高级别个性化的系统上，Dispatcher应缓存大多数请求。 因此，发布实例上的负载应保持相对平坦。 如果需要高级别的个性化，则建议对个性化内容使用iFrame或AJAX请求等技术，以尽可能多地允许Dispatcher缓存。

对于基本测试，Apache Bench可用于测量Web服务器的响应时间，并帮助创建负载以测量内存泄漏等情况。 请参阅以下示例中的 [监控文档](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench).

## 性能问题疑难解答 {#troubleshooting-performance-issues}

在创作实例上运行性能测试后，必须调查、诊断和解决任何问题。 在执行分析和解决问题时，您可以使用多种工具和技术：

* 您可以检查 [请求性能日志](/help/sites-administering/operations-dashboard.md#request-performance) 操作功能板中的。 此工具可用于识别较慢的页面请求
* 使用分析运行缓慢的查询 [查询性能工具](/help/sites-administering/operations-dashboard.md#query-performance)

* 观察错误日志中是否有错误或警告。 有关更多信息，请参阅 [记录](/help/sites-deploying/configure-logging.md).
* 监视系统硬件资源，如内存和CPU利用率、磁盘I/O或网络I/O。这些资源通常是造成性能瓶颈的原因。
* 优化页面的架构以及如何寻址页面，以最大限度地减少URL参数的使用，从而尽可能多地允许缓存。
* 请遵循 [性能优化](/help/sites-deploying/configuring-performance.md) 和 [性能调整提示](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=en) 文档。

* 如果在创作实例上编辑某些页面或组件时出现问题，请使用TouchUI开发人员模式检查有问题的页面。 这样做可划分页面上的每个内容区域及其加载时间。
* 缩小网站上的所有JS和CSS。 查看此 [博客帖子](https://blogs.adobe.com/foxes/enable-js-and-css-minification/).
* 从组件中消除嵌入的CSS和JS。 它们应当包含在客户端库中并对其进行缩小，以最大限度地减少呈现页面所需的请求数。
* 要检查服务器请求并查看哪些请求占用的时间最长，请使用Chrome的“网络”选项卡等浏览器工具。

一旦识别出问题区域，就可以检查应用程序代码以优化性能。 任何无法正常执行的现成AEM功能都可以通过Adobe支持来解决。
