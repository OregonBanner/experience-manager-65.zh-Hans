---
title: 如何使用 Headless 应用程序上线
description: 在AEM Headless开发人员历程的这一部分中，了解如何实时部署无头应用程序。
exl-id: ec3356ef-9e60-4151-984d-3ebdab593b96
source-git-commit: 71842228dd3cb1ce3b79728912e8333d25fccefc
workflow-type: tm+mt
source-wordcount: '1846'
ht-degree: 50%

---

# 如何使用 Headless 应用程序上线 {#go-live}

在 [AEM Headless开发人员历程](overview.md)，了解如何实时部署无头应用程序。

## 迄今为止的故事 {#story-so-far}

在 AEM Headless 历程的上一个文档[如何通过 AEM Assets API 更新您的内容](update-your-content.md)中，您已了解如何通过 API 在 AEM 中更新现有 Headless 内容，您现在应该：

* 了解 AEM Assets HTTP API。

本文基于这些基础知识编写，以便您了解如何准备您自己的 AEM Headless 项目以上线。

## 目标 {#objective}

本文档可帮助您了解 AEM Headless 发布管道，以及在通过您的应用程序上线之前必须了解的性能注意事项。

* 了解AEM SDK和所需的开发工具
* 设置本地开发运行时以在上线之前模拟内容
* 了解AEM内容复制和缓存基础知识
* 在启动前保护和扩展您的应用程序
* 监控性能和调试问题

## AEM SDK {#the-aem-sdk}

AEM SDK 用于构建和部署自定义代码。它是您在上线之前必须开发和测试无头应用程序的主要工具。 它包含以下构件：

* 快速入门 jar – 可用于设置创作和发布实例的可执行的 jar 文件
* 调度程序工具 — Dispatcher模块及其对基于Windows和UNIX的系统的依赖项
* Java™ API Jar – Java™ Jar/Maven 依赖项，公开了所有允许的 Java™ API，它们可用于针对 AEM 进行开发
* Javadoc jar – Java™ API jar 的 javadoc

## 其他开发工具 {#additional-development-tools}

除了AEM SDK之外，您还需要其他工具，以便在本地开发和测试代码和内容：

* Java™
* Git
* Apache Maven
* Node.js 库
* 您选择的 IDE

由于AEM是Java™应用程序，因此您必须安装Java™和Java™ SDK才能支持AEMas a Cloud Service的开发。

Git 可用于管理源代码管理和签入对 Cloud Manager 的更改，然后将它们部署到生产实例。

AEM 使用 Apache Maven 构建从 AEM Maven 项目原型生成的项目。所有主要 IDE 都提供对 Maven 的集成支持。

Node.js是一个JavaScript运行时环境，用于处理AEM项目的前端资产 `ui.frontend` 子项目。 Node.js与npm一起分发，npm是事实上的Node.js包管理器，用于管理JavaScript依赖项。

## AEM 系统组件概览 {#components-of-an-aem-system-at-a-glance}

接下来，让我们看看 AEM 环境的组成部分。

完整的 AEM 环境由创作、发布和 Dispatcher 构成。这些相同的组件在本地开发运行时中可用，以便您在上线前更轻松地预览代码和内容。

* **Author 服务**&#x200B;是内部用户创建、管理和预览内容的地方。

* **发布服务** 被视为“实时”环境，通常是最终用户与之交互的环境。 内容在创作服务上进行编辑和批准后，会分发（复制）到发布服务。 AEM Headless 应用程序最常见的部署模式是将应用程序的生产版本连接到 AEM Publish 服务。

* **Dispatcher** 是一个通过 AEM Dispatcher 模块增强的静态 Web 服务器。它缓存由发布实例生成的网页以提高性能。

## 本地开发工作流 {#the-local-development-workflow}

本地开发项目基于 Apache Maven 构建，并使用 Git 进行源代码管理。要更新项目，开发人员可以使用他们首选的集成开发环境，例如Eclipse、Visual Studio代码或IntelliJ等。

要测试由无头应用程序摄取的代码或内容更新，请将更新部署到本地AEM运行时。 这些实例包括AEM创作和发布服务的本地实例。

请务必记下本地 AEM 运行时中每个组件之间的区别，因为在更新最起作用的位置测试更新是非常重要的。例如，在创作实例上测试内容更新或在发布实例上测试新代码。

在生产系统中，Dispatcher 和 http Apache 服务器将始终位于 AEM 发布实例的前面。它们为 AEM 系统提供缓存和安全服务，因此，针对 Dispatcher 测试代码和内容更新也至为重要。

## 使用本地开发环境在本地预览您的代码和内容 {#previewing-your-code-and-content-locally-with-the-local-development-environment}

要为启动做好AEM无头项目准备，请确保项目的所有组成部分都正常运行。

为此，您必须将所有内容整合在一起：代码、内容和配置，并在本地开发环境中测试它，以便进行上线准备。

地方发展环境主要由三个方面组成：

1. AEM项目 — 包含AEM开发人员将要处理的所有自定义代码、配置和内容
1. 本地 AEM 运行时 – 本地版本的 AEM 创作和发布服务，用于从 AEM 项目部署代码
1. 本地 Dispatcher 运行时 – 包含 Dispatcher 模块的 Apache httpd Web 服务器的本地版本

设置本地开发环境后，您可以通过在本地部署静态节点服务器来模拟向React应用程序提供内容的过程。

要更深入地了解设置本地开发环境以及内容预览所需的所有依赖关系，请参阅 [生产部署文档](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/overview.html?lang=en).

## 准备AEM Headless应用程序上线 {#prepare-your-aem-headless-application-for-golive}

<!-- Start of CDN Review -->

现在，是时候按照下面概述的最佳实践，为启动您的AEM无头应用程序做好准备了。

### 在启动之前保护无头应用程序 {#secure-and-scale-before-launch}

1. 准备 [身份验证](/help/sites-developing/headless/graphql-api/graphql-authentication-content-fragments.md) 针对GraphQL请求

### 模型结构与 GraphQL 输出 {#structure-vs-output}

* 避免创建输出超过15 KB JSON（gzip压缩）的查询。 长 JSON 文件是客户端应用程序要分析的资源密集型文件。
* 避免超过五个嵌套级别的片段层级。其他级别会使内容作者难以考虑其更改产生的影响。
* 使用多对象查询而不是在模型中使用依赖项层级对查询进行建模。这样，在重构JSON输出方面就具有更大的长期灵活性，而无需进行许多内容更改。

### 最大程度地提高 CDN 缓存命中率 {#maximize-cdn}

* 不要使用直接 GraphQL 查询，除非您从表面请求实时内容。
   * 尽可能使用持久查询。
   * 提供CDN TTL（超过600秒），以便CDN可以缓存它们。
   * AEM 可以计算模型更改对现有查询的影响。
* 在低内容更改率和高内容更改率之间拆分JSON文件/GraphQL查询，以减少客户端到CDN的流量并分配更高的TTL。 这样可最大限度地减少CDN使用源服务器重新验证JSON的情况。
* 要主动使CDN中的内容失效，请使用软清除。 这样，CDN便可重新下载内容，而不会导致缓存丢失。

>[!NOTE]
>
>请参阅 [其他资源](#additional-resources) 有关CDN和缓存的更多信息。

### 缩短下载 Headless 内容的时间 {#improve-download-time}

* 确保 HTTP 客户端使用 HTTP/2。
* 确保 HTTP 客户端接受 gzip 的标头请求。
* 最大程度地减少用于托管 JSON 的域和引用的构件的数量。
* 使用 `Last-modified-since` 刷新资源。
* 使用 JSON 文件中的 `_reference` 输出开始下载资产，而无需分析完整的 JSON 文件。

<!-- End of CDN Review -->

## 部署到生产 {#deploy-to-production}

部署到生产环境取决于您是否具有 *传统* 使用Maven进行部署或位于Adobe Managed Services(AMS)上，因此使用Cloud Manager的AEM实例。

## 使用Maven部署到生产环境 {#deploy-to-production-maven}

对于 *传统* 使用Maven部署（非AMS），请参阅 [WKND教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/project-setup.html?lang=en#build) ，以查看概述。

## 使用Cloud Manager部署到生产环境 {#deploy-to-production-cloud-manager}

如果您是使用Cloud Manager的AMS客户，则在确保所有内容都经过测试并正常运行后，您可以将代码更新推送到 [Cloud Manager中的集中式Git存储库](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/git-integration.html).

将更新上传到Cloud Manager后，请使用将其部署到AEM [Cloud Manager的CI/CD管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-deployment.html).

<!-- Can't find a parallel link -->
<!--
You can start deploying your code by leveraging the Cloud Manager CI/CD pipeline, which is covered extensively [here](/help/implementing/deploying/overview.md).
-->

## 性能监控 {#performance-monitoring}

要让用户在使用 AEM Headless 应用程序时获得最佳体验，请务必监控关键性能指标，详情如下：

* 验证应用程序的预览版和生产版
* 验证当前服务可用性状态的 AEM 状态页面
* 访问性能报告
   * 交付性能
      * 源服务器 – 调用次数、错误率、CPU 负载、负载流量
   * 创作性能
      * 检查用户、请求和加载的数量
* 访问特定于应用程序和空间的性能报表
   * 在服务器启动后，检查一般指标是否为绿色/橙色/红色，然后识别具体的应用程序问题
   * 打开上面过滤到应用程序或空间的相同报告（例如，Photoshop 桌面、付费专区）
   * 使用 Splunk 日志 API 访问服务和应用程序性能
   * 如果还有其他问题，请联系客户支持。

## 疑难解答 {#troubleshooting}

### 调试 {#debugging}

将这些最佳实践用作常规调试方法：

* 使用应用程序的预览版本验证功能和性能
* 使用应用程序的生产版本验证功能和性能
* 使用内容片段编辑器的 JSON 预览版进行验证
* 要检查是否存在客户端应用程序或交付问题，请检查客户端应用程序中的JSON
* 要检查是否存在与缓存内容或AEM相关的问题，请使用GraphQL检查JSON

### 借助支持记录错误 {#logging-a-bug-with-support}

要通过支持部门高效记录错误，如果您需要进一步的帮助，请完成以下步骤：

* 如有必要，可拍摄问题屏幕快照
* 记录重现问题的方法
* 记录问题重现的内容
* 通过 AEM 支持门户以适当的优先级记录问题

## 历程结束 - 是吗？ {#journey-ends}

恭喜！您已完成 AEM Headless 开发人员历程！您现在应了解以下内容：

* Headless 和 Headful 内容交付之间的区别。
* AEM 的 Headless 功能。
* 如何编排 AEM Headless 项目。
* 如何在 AEM 中创建 Headless 内容。
* 如何在 AEM 中检索和更新 Headless 内容。
* 如何使用 AEM Headless 项目上线。
* 上线完成后要执行的操作。

您已经启动了您的第一个AEM Headless项目，或者现在已具备执行此操作的所有知识。 做得好！

### 探究单页应用程序 {#explore-spa}

不过，无需停止AEM中的无头存储。 在 [入门指南部分](getting-started.md#integration-levels)，它讨论了AEM不仅支持无头交付和传统的全栈模型，还支持结合两者优势的混合模型。

如果您需要这种灵活性来完成项目，请继续进行历程中的可选其他部分， [如何使用AEM创建单页应用程序(SPA)。](create-spa.md)

## 其他资源 {#additional-resources}

* [AEM Developing指南](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/the-basics.html?lang=en)

* [WKND教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en)

* [Cloud Manager for AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=zh-Hans)

* CDN缓存

   * [控制CDN缓存](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html#controlling-a-cdn-cache)

   * 配置 [CDN重写程序](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/osgi-configuration-settings.html) (*搜索CDN重写程序*)
