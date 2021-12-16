---
title: 如何使用您的无头应用程序
description: 在AEM Headless开发人员历程的这一部分中，了解如何实时部署无头应用程序。
source-git-commit: 20d46a7c37663dac36e6af9582d569a7f782eab7
workflow-type: tm+mt
source-wordcount: '1903'
ht-degree: 0%

---

# 如何使用您的无头应用程序 {#go-live}

在 [AEM Headless开发人员历程](overview.md)，了解如何实时部署无头应用程序。

## 迄今为止的故事 {#story-so-far}

在AEM无头历程的上一个文档中， [如何通过AEM Assets API更新您的内容](update-your-content.md) 您学习了如何通过API在AEM中更新现有无头内容，现在应该：

* 了解AEM Assets HTTP API。

本文基于这些基础知识，以便您了解如何准备自己的AEM无头项目以投入使用。

## 目标 {#objective}

本文档可帮助您了解AEM无头发布管道以及在使用应用程序之前需要注意的性能注意事项。

* 了解AEM SDK和所需的开发工具
* 设置本地开发运行时以在上线之前模拟内容
* 了解AEM内容复制和缓存基础知识
* 在启动之前保护并扩展您的应用程序
* 监视性能和调试问题

## AEM SDK {#the-aem-sdk}

AEM SDK用于构建和部署自定义代码。 它是您开发和测试无头应用程序之前所需的主要工具。 它包含以下工件：

* 快速入门jar — 一个可执行的jar文件，可用于设置创作实例和发布实例
* 调度程序工具 — Dispatcher模块及其对基于Windows和UNIX的系统的依赖项
* Java API Jar - Java Jar/Maven依赖项，它公开了可用于针对AEM进行开发的所有允许的Java API
* Javadoc jar - Java API Jar的javadoc

## 其他开发工具 {#additional-development-tools}

除了AEM SDK之外，您还需要其他工具，以便在本地开发和测试代码和内容：

* Java
* Git
* 阿帕奇·马文
* Node.js库
* 您选择的IDE

由于AEM是一个Java应用程序，因此您需要安装Java和Java SDK才能支持AEMas a Cloud Service的开发。

您将使用Git来管理源控件，以及将更改签入到Cloud Manager中，然后将其部署到生产实例。

AEM使用Apache Maven来构建从AEM Maven项目原型生成的项目。 所有主要IDE都为Maven提供集成支持。

Node.js是一个JavaScript运行时环境，用于处理AEM项目的前端资产 `ui.frontend` 子项目。 Node.js与npm一起分发，npm是事实上的Node.js包管理器，用于管理JavaScript依赖项。

## AEM系统组件概览 {#components-of-an-aem-system-at-a-glance}

接下来，让我们看一下AEM环境的组成部分。

完整的AEM环境由创作、发布和调度程序组成。 这些相同的组件将在本地开发运行时中提供，以便您在上线之前更轻松地预览代码和内容。

* **创作服务** 是内部用户创建、管理和预览内容的位置。

* **发布服务** 被视为“实时”环境，通常是最终用户与之交互的环境。 内容在创作服务上进行编辑和批准后，会分发（复制）到发布服务。 AEM无头应用程序的最常见部署模式是，将应用程序的生产版本连接到AEM发布服务。

* **调度程序** 是一种随AEM dispatcher模块一起增强的静态web服务器。 它会缓存由发布实例生成的网页，以提高性能。

## 本地开发工作流 {#the-local-development-workflow}

本地开发项目是基于Apache Maven构建的，并且使用Git进行源代码管理。 为了更新项目，开发人员可以使用他们首选的集成开发环境，例如Eclipse、Visual Studio代码或IntelliJ等。

要测试将由您的无头应用程序摄取的代码或内容更新，您需要将更新部署到本地AEM运行时，其中包括AEM创作和发布服务的本地实例。

请务必注意本地AEM运行时中每个组件之间的差异，因为在最重要的位置测试更新非常重要。 例如，在创作时测试内容更新或在发布实例中测试新代码。

在生产系统中，调度程序和http Apache服务器将始终位于AEM发布实例之前。 它们为AEM系统提供缓存和安全服务，因此测试针对调度程序的代码和内容更新至关重要。

## 使用本地开发环境在本地预览代码和内容 {#previewing-your-code-and-content-locally-with-the-local-development-environment}

要为启动您的AEM无头项目做好准备，您需要确保项目的所有组成部分都正常运行。

为此，您需要将所有内容整合在一起：代码、内容和配置，并在本地开发环境中测试它，以便进行上线准备。

地方发展环境由三个主要领域组成：

1. AEM项目 — 其中将包含AEM开发人员将要处理的所有自定义代码、配置和内容
1. 本地AEM运行时 — AEM创作和发布服务的本地版本，将用于从AEM项目部署代码
1. 本地Dispatcher运行时 — Apache httpd Web服务器的本地版本，其中包含Dispatcher模块

设置本地开发环境后，您可以通过在本地部署静态节点服务器来模拟向React应用程序提供内容的过程。

为了更深入地了解如何设置本地开发环境以及内容预览所需的所有依赖关系，请参阅 [生产部署文档](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/production-deployment.html?lang=en#prerequisites).

## 准备AEM Headless应用程序上线 {#prepare-your-aem-headless-application-for-golive}

<!-- Start of CDN Review -->

现在，是时候按照下面概述的最佳实践，为启动您的AEM无头应用程序做好准备了。

### 在启动之前保护无头应用程序 {#secure-and-scale-before-launch}

1. 准备 [身份验证](/help/assets/content-fragments/graphql-authentication-content-fragments.md) GraphQL请求

### 模型结构与GraphQL输出 {#structure-vs-output}

* 避免创建输出超过15kb JSON（gzip压缩）的查询。 较长的JSON文件是需要大量资源才能解析客户端应用程序。
* 避免片段层级的嵌套级别超过5个。 其他级别使内容作者很难考虑其更改的影响。
* 使用多对象查询，而不是在模型内使用依赖关系层次结构建模查询。 这样，在重构JSON输出方面就具有了更大的长期灵活性，而无需进行大量内容更改。

### 最大化CDN缓存点击率 {#maximize-cdn}

* 除非您从表面请求实时内容，否则请勿使用直接GraphQL查询。
   * 尽可能使用持久查询。
   * 为CDN提供超过600秒的CDN TTL，以便CDN进行缓存。
   * AEM可以计算模型更改对现有查询的影响。
* 在低内容更改率和高内容更改率之间拆分JSON文件/GraphQL查询，以减少客户端对CDN的流量并分配更高的TTL。 这样可以最大限度地减少CDN使用源服务器重新验证JSON的情况。
* 要主动使来自CDN的内容失效，请使用软清除。 这样，CDN便可重新下载内容，而不会导致缓存丢失。

>[!NOTE]
>
>请参阅 [其他资源](#additional-resources) 有关CDN和缓存的更多信息。

### 缩短下载无头内容的时间 {#improve-download-time}

* 确保HTTP客户端使用HTTP/2。
* 确保HTTP客户端接受gzip的标头请求。
* 最大限度地减少用于托管JSON和引用对象的域数。
* 利用 `Last-modified-since` 刷新资源。
* 使用 `_reference` JSON文件中的输出，以便开始下载资产，而无需解析完整的JSON文件。

<!-- End of CDN Review -->

## 部署到生产环境 {#deploy-to-production}

部署到生产环境取决于您是否具有 *传统* 使用Maven进行部署或位于Adobe Managed Services(AMS)上，因此使用Cloud Manager的AEM实例。

## 使用Maven部署到生产环境 {#deploy-to-production-maven}

对于 *传统* 使用Maven部署（非AMS）时，您可以看到 [WKND教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/project-setup.html?lang=en#build) ，以查看概述。

## 使用Cloud Manager部署到生产环境 {#deploy-to-production-cloud-manager}

如果您是使用Cloud Manager的AMS客户，则在确保所有内容均已测试并正常运行后，您便可以将代码更新推送到 [Cloud Manager中的集中式Git存储库](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html).

将更新上传到Cloud Manager后，可以使用将这些更新部署到AEM [Cloud Manager的CI/CD管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html).

<!-- Can't find a parallel link -->
<!--
You can start deploying your code by leveraging the Cloud Manager CI/CD pipeline, which is covered extensively [here](/help/implementing/deploying/overview.md).
-->

## 性能监控 {#performance-monitoring}

为了让用户在使用AEM无头应用程序时获得最佳体验，您务必要监控关键性能量度，如下所述：

* 验证应用程序的预览和生产版本
* 验证AEM状态页面以了解当前服务可用性状态
* 访问性能报告
   * 交付性能
      * 源服务器 — 调用数、错误率、CPU负载、负载流量
   * 创作性能
      * 检查用户数、请求数和加载数
* 访问特定于应用程序和空间的性能报表
   * 服务器启动后，检查常规量度是否为绿色/橙色/红色，然后确定特定的应用程序问题
   * 打开上面按应用程序或空间过滤的相同报表(例如Photoshop桌面版、付费专区)
   * 使用Splunk日志API访问服务和应用程序性能
   * 如果存在其他问题，请联系客户支持。

## 疑难解答 {#troubleshooting}

### 调试 {#debugging}

按照以下最佳实践作为调试的一般方法：

* 使用应用程序的预览版本验证功能和性能
* 使用应用程序的生产版本验证功能和性能
* 使用内容片段编辑器的JSON预览进行验证
* Inspect客户端应用程序中的JSON，以检查客户端应用程序或交付问题是否存在
* Inspect使用GraphQL检查是否存在与缓存内容或AEM相关的问题

### 记录支持的错误 {#logging-a-bug-with-support}

为了在您需要进一步帮助时，通过支持部门高效地记录错误，请执行以下步骤：

* 如有必要，请拍摄问题的屏幕截图
* 记录重现问题的方法
* 记录问题所重现的内容
* 通过具有相应优先级的AEM支持门户记录问题

## 历程结束了？ {#journey-ends}

恭喜！ 您已完成AEM Headless开发人员历程! 您现在应该了解：

* 无头内容和有头内容交付之间的区别。
* AEM无头功能。
* 如何组织和AEM Headless项目。
* 如何在AEM中创建无标题内容。
* 如何在AEM中检索和更新无标题内容。
* 如何使用AEM Headless项目进行实时。
* 上线后怎么办。

您已经启动了您的第一个AEM Headless项目，或者现在掌握了执行此操作所需的所有知识。 干得好！

### 浏览单页应用程序 {#explore-spa}

不过，AEM中的无头店不需要停在这里。 您可能记得 [入门指南部分](getting-started.md#integration-levels) 我们简要讨论了AEM如何不仅支持无头交付和传统的全栈模型，而且还支持结合两者优点的混合模型。

如果您的项目需要这种灵活性，请继续进行历程的可选附加部分， [如何使用AEM创建单页应用程序(SPA)。](create-spa.md)

## 其他资源 {#additional-resources}

* [AEM Developing指南](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/the-basics.html?lang=en)

* [WKND教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en)

* [Cloud Manager for AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=en)

* CDN缓存

   * [控制CDN缓存](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html#controlling-a-cdn-cache)

   * 配置 [CDN重写程序](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/osgi-configuration-settings.html) (*搜索CDN重写程序*)
