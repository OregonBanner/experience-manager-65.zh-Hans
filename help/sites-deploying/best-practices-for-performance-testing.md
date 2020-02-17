---
title: 性能测试的最佳实践
seo-title: 性能测试的最佳实践
description: 本文概述了用于性能测试的总体战略和方法，以及可用于协助该过程的一些工具。
seo-description: 本文概述了用于性能测试的总体战略和方法，以及可用于协助该过程的一些工具。
uuid: ab8720d6-b864-4d00-9e07-2e1699cfe7db
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 669018a0-f6ef-42b2-9c6f-83d7dd5a7095
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 性能测试的最佳实践{#best-practices-for-performance-testing}

## 简介 {#introduction}

性能测试是任何AEM部署的重要部分。 根据客户要求，可以对发布实例、作者实例或两者执行性能测试。

本文档将概述执行性能测试的总体战略和方法，以及Adobe为协助执行该过程而提供的一些工具。 最后，我们将从代码分析和系统配置角度分析AEM 6中提供的一些工具，以帮助进行性能调整。

### 模拟现实 {#simulating-reality}

执行性能测试时最重要的是确保您尽可能地模仿生产环境。 虽然这通常很困难，但必须确保这些测试的准确性。 在设计性能测试时，必须考虑以下几点：

* 类似生产的内容

AEM中的许多性能度量值（如查询响应时间）可能会受系统中内容大小的影响。 务必确保测试环境尽可能接近生产数据的副本。

* 生产代码

在测试环境中，生产中部署的AEM版本和修补程序应相同。 测试部署到生产的代码版本也很重要。

* 类似生产的硬件和网络配置

如果没有尽可能接近生产环境，这些测试将毫无意义。 理想情况下，硬件规范、网络接口、负载平衡器和CDN应与测试环境中的生产完全相同。

* 生产负载

许多性能问题只有在系统负载较重时才会出现。 良好的性能测试应模拟生产系统在其高峰期所受的负载。

### 设置目标 {#setting-goals}

在开始性能测试之前，必须设置非功能要求以指定负载和响应时间。 如果您是从现有系统迁移的，请确保响应时间与当前生产值类似。 对于负载，最好采用当前峰值负载，将其加倍。 这将确保网站能够继续良好地运行。

### 工具 {#tools}

市场上有许多商业上可用的性能测试工具。 运行负载生成工具时，务必确保执行测试的计算机具有足够的网络带宽。 否则，一旦测试机达到其连接极限，将不会在测试环境中产生额外的负载。

#### 测试工具 {#testing-tools}

* Adobe的“ **艰难日** ”工具可用于为AEM实例生成负载并收集性能数据。 Adobe的AEM工程团队实际上使用该工具对AEM产品本身进行负载测试。 在艰难时刻执行的脚本是通过属性文件和JMX XML文件配置的。 有关详细信息，请参阅 [艰难日文档](/help/sites-developing/tough-day.md)。

* AEM提供开箱即用的工具，可快速查看有问题的查询、请求和错误消息。 有关详细信息，请参 [阅Operations Dashboard文档的“诊断工具](/help/sites-administering/operations-dashboard.md#diagnosis-tools) ”部分。
* Apache提供了一个名为 **JMeter的产品** ，它可用于性能和负载测试以及功能行为。 它是开放源软件，可免费使用，但功能集比企业产品小，学习曲线也更陡。 JMeter可在Apache的网站https://jmeter.apache.org/上找 [到](https://jmeter.apache.org/)

* **Load Runner** 是企业级负载测试产品。 提供免费评估版。 有关更多信息，请访 [问https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview](https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview)

* 还可以使用基于云的负 [载测试工具](https://www.neustar.biz/services/web-performance/load-testing) （如Neustar）。
* 在测试移动或响应式网站时，需要使用一组单独的工具。 它们通过限制网络带宽来工作，模拟3G或EDGE等较慢的移动连接。 使用范围更广的工具包括：

   * **[Network Link Condition](https://nshipster.com/network-link-conditioner/)**—— 它提供易于使用的UI，并且在网络堆栈上工作级别较低。 它包括OS x和iOS的版本；[](https://nshipster.com/network-link-conditioner/)
   * [**Charles **](https://www.charlesproxy.com/)—— 一个Web调试代理应用程序，除了几个其他用途外，还提供网络限制。 提供适用于Windows、OS x和Linux的版本。[](https://www.charlesproxy.com/)

#### 优化工具 {#optimization-tools}

**监测**

“监 [控性能](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance) ”文档是工具和方法的好资源，可用于诊断问题和找准调整的区域。

**触屏UI中的开发人员模式**

AEM 6触屏UI中的新增功能之一是开发人员模式。 正如作者可以在编辑模式和预览模式之间切换一样，开发人员可以在创作UI中切换到开发人员模式，查看页面上每个组件的渲染时间以及查看任何错误的堆栈跟踪。 有关开发者模式的更多信息，请参阅此 [CQ Gems演示文稿](https://docs.adobe.com/content/ddc/en/gems/aem-6-0-developer-mode.html)。

**使用rlog.jar读取请求日志**

要对AEM系统上的请求日志进行更全面的分析，可 `rlog.jar` 以使用搜索功能对AEM生成的文件进行 `request.log` 排序。 此jar文件随AEM安装一起包含在文件夹 `/crx-quickstart/opt/helpers` 中。 有关记录工具和一般请求日志的详细信息，请参阅监 [控和维护文档](/help/sites-deploying/monitoring-and-maintaining.md) 。

**Explain Query Tool**

ACS AEM [](/help/sites-administering/operations-dashboard.md#explain-query) Tools中的“解释查询”工具可用于查看运行查询时使用的索引。 这在优化运行缓慢的查询时非常有用。

**PageSpeed工具**

Google的PageSpeed工具提供了站点分析功能，以符合页面性能的最佳实践，并提供了一个插件，该插件可以与Apache实例上的调度程序一起安装，以进行其他优化。 有关详细信息，请参阅 [PageSpeed Tools网站](https://developers.google.com/speed/pagespeed/)。

## 创作环境 {#author-environment}

### 执行测试 {#performing-tests}

为了在创作环境中进行性能测试，您必须模拟制作作者的体验。 这意味着作者安装必须包含您为生产作者实例准备的所有组件、OSGi捆绑包、UI自定义、自定义索引和任何其他附加内容。

有许多自动化框架可用于性能和负载测试。 可以在这些工具中记录自定义脚本，然后回放以模拟同时执行类似内容创建和激活活动的作者的高峰数量。 建议您使用“艰难日”工具模拟上传数千个资产或激活大量页面等活动。

对于需要大量资产加载或页面创作的环境类型，必须使用“艰难日”等工具，以确保该环境在峰值负载下高效运行。 [WebDAV是一种无需脚本编写的工具](/help/sites-administering/webdav-access.md) ，也可用于加载大量资源。

#### MongoDB特定步骤 {#mongodb-specific-steps}

在具有MongoDB后端的系统上，AEM提供了在执行负载或性能测试时需要监视的几个 [JMX](/help/sites-administering/jmx-console.md) MBean:

* 统一 **的缓存统计信息** MBean。 可以通过转到：

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

对于名为 **Document-Diff的缓存**，点击率应结束 `.90`。 如果点击率低于90%，您可能需要修改配 `DocumentNodeStoreService` 置。 Adobe产品支持可以为您的环境推荐最佳设置。

* Oak库 **统计数据** Mbean。 可以通过转到：

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

OvertationQueueMaxLength **** 部分将显示Oak观察队列中在过去几小时、几分钟、几秒和几周内的事件数。 在“每小时”部分查找最大的活动数。 需要将此数字与OSGi控制台 `oak.observation.queue-length` 中 **SlingRepositoryManager组件中的设** 置进行比较 [](/help/sites-deploying/web-console.md)。 如果观察队列显示的最大数量超过设置，请 `queue-length` 与Adobe支持部门联系，以获得有关提高设置的帮助。 默认设置为1,000，但大多数部署通常需要将其提高到20,000或50,000。

## 发布环境 {#publish-environment}

### 执行测试 {#performing-tests-1}

部署中需要经受负载测试的最重要部分是面向最终用户的发布或调度程序环境。

第三方自动测试工具可用于测试网站的性能。 这些工具允许您记录用户将在站点上完成的步骤，并同时运行其中的许多会话以模拟生产网站的典型负载。

大多数生产网站都进行了优化，如调度程序缓存和内容交付网络就位。 测试时，您需要确保这些优化也适用于测试环境。 除了监视最终用户的响应时间之外，您还需要监视发布服务器和调度程序上的系统指标，以确保系统不受硬件资源的限制。

在不需要高级别个性化的系统上，调度程序应缓存大多数请求。 因此，发布实例的负载应保持相对平坦。 如果需要高级别的个性化，建议对个性化内容使用iFrames或AJAX请求等技术，以便允许尽可能多的调度程序缓存。

对于基本测试，Apache Bench可用于测量Web服务器响应时间并帮助创建用于测量内存泄漏等内容的负载。 有关详细信息，请参阅监视文档 [中的示例](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench)。

## 性能问题疑难解答 {#troubleshooting-performance-issues}

在创作实例上运行性能测试后，需要调查、诊断和解决所有问题。 在执行分析和解决问题时，可以使用多种工具和技术：

* 您可以检查“操 [作控制板](/help/sites-administering/operations-dashboard.md#request-performance) ”中的“请求性能”日志。 此工具可用于识别页面请求缓慢
* 使用“查询性能”工具分析运行 [缓慢的查询](/help/sites-administering/operations-dashboard.md#query-performance)

* 观看错误列表以查看错误或警告。 有关详细信息，请参阅记 [录](/help/sites-deploying/configure-logging.md)
* 监视系统硬件资源，如内存和CPU使用率、磁盘I/O或网络I/O。这些资源通常是导致性能瓶颈的原因
* 优化页面的架构及其寻址方式，以最大限度地减少URL参数的使用，从而尽可能多地缓存
* 按照性能优 [化和性能](/help/sites-deploying/configuring-performance.md) 调 [整提示文档操作](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html) 。

* 如果在创作实例上编辑某些页面或组件时出现问题，请使用TouchUI开发人员模式检查相关页面。 这将提供对页面上每个内容区域的细分及其加载时间
* 精简站点上的所有JS和CSS。 有关如何执行此操作的详细信息，请参阅此博 [客文章](https://blogs.adobe.com/foxes/enable-js-and-css-minification/)。
* 从组件中消除嵌入的CSS和JS。 应将它们包含在客户端库中并与其进行缩小，以最大限度地减少呈现页面所需的请求数
* 使用浏览器工具（如Chrome的“网络”选项卡）检查服务器请求并查看哪些请求占用的时间最长。

识别问题区域后，可检查应用程序代码以进行性能优化。 Adobe支持可以解决任何开箱即用的AEM功能，这些功能无法正常执行。
