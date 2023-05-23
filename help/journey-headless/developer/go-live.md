---
title: 如何使用 Headless 应用程序上线
description: 在AEM Headless開發人員歷程的這一部分，瞭解如何即時部署Headless應用程式。
exl-id: ec3356ef-9e60-4151-984d-3ebdab593b96
source-git-commit: 71842228dd3cb1ce3b79728912e8333d25fccefc
workflow-type: tm+mt
source-wordcount: '1846'
ht-degree: 50%

---

# 如何使用 Headless 应用程序上线 {#go-live}

在這部分中 [AEM Headless開發人員歷程](overview.md)，瞭解如何即時部署Headless應用程式。

## 迄今为止的故事 {#story-so-far}

在 AEM Headless 历程的上一个文档[如何通过 AEM Assets API 更新您的内容](update-your-content.md)中，您已了解如何通过 API 在 AEM 中更新现有 Headless 内容，您现在应该：

* 了解 AEM Assets HTTP API。

本文基于这些基础知识编写，以便您了解如何准备您自己的 AEM Headless 项目以上线。

## 目标 {#objective}

本文档可帮助您了解 AEM Headless 发布管道，以及在通过您的应用程序上线之前必须了解的性能注意事项。

* 瞭解AEM SDK和所需的開發工具
* 設定本機開發執行階段以在上線之前模擬您的內容
* 瞭解AEM內容復寫和快取基本概念
* 在启动前保护和扩展您的应用程序
* 监控性能和调试问题

## AEM SDK {#the-aem-sdk}

AEM SDK 用于构建和部署自定义代码。這是您上線前必須開發和測試Headless應用程式的主要工具。 它包含以下构件：

* 快速入门 jar – 可用于设置创作和发布实例的可执行的 jar 文件
* Dispatcher工具 — 適用於Windows和UNIX系統的Dispatcher模組及其相依性
* Java™ API Jar – Java™ Jar/Maven 依赖项，公开了所有允许的 Java™ API，它们可用于针对 AEM 进行开发
* Javadoc jar – Java™ API jar 的 javadoc

## 其他开发工具 {#additional-development-tools}

除了AEM SDK，您還需要其他工具，協助您在本機開發和測試程式碼和內容：

* Java™
* Git
* Apache Maven
* Node.js 库
* 您选择的 IDE

由於AEM是Java™應用程式，您必須安裝Java™和Java™ SDK以支援AEMas a Cloud Service的開發。

Git 可用于管理源代码管理和签入对 Cloud Manager 的更改，然后将它们部署到生产实例。

AEM 使用 Apache Maven 构建从 AEM Maven 项目原型生成的项目。所有主要 IDE 都提供对 Maven 的集成支持。

Node.js是JavaScript執行階段環境，用來處理AEM專案的前端資產 `ui.frontend` 子專案。 Node.js隨npm分佈，後者是實際的Node.js封裝管理員，用於管理JavaScript相依性。

## AEM 系统组件概览 {#components-of-an-aem-system-at-a-glance}

接下来，让我们看看 AEM 环境的组成部分。

完整的 AEM 环境由创作、发布和 Dispatcher 构成。這些相同的元件在本機開發執行階段中可供使用，讓您更容易在上線前預覽程式碼和內容。

* **Author 服务**&#x200B;是内部用户创建、管理和预览内容的地方。

* **Publish服務** 視為「即時」環境，通常是使用者與之互動的對象。 在Author服務上編輯和核准後的內容會分發（復寫）到Publish服務。 AEM Headless 应用程序最常见的部署模式是将应用程序的生产版本连接到 AEM Publish 服务。

* **Dispatcher** 是一个通过 AEM Dispatcher 模块增强的静态 Web 服务器。它缓存由发布实例生成的网页以提高性能。

## 本地开发工作流 {#the-local-development-workflow}

本地开发项目基于 Apache Maven 构建，并使用 Git 进行源代码管理。若要更新專案，開發人員可以使用他們偏好的整合式開發環境，例如Eclipse、Visual Studio Code或IntelliJ等。

若要測試Headless應用程式擷取的程式碼或內容更新，請將更新部署至本機AEM執行階段。 其中包括AEM作者和發佈服務的本機執行個體。

请务必记下本地 AEM 运行时中每个组件之间的区别，因为在更新最起作用的位置测试更新是非常重要的。例如，在创作实例上测试内容更新或在发布实例上测试新代码。

在生产系统中，Dispatcher 和 http Apache 服务器将始终位于 AEM 发布实例的前面。它们为 AEM 系统提供缓存和安全服务，因此，针对 Dispatcher 测试代码和内容更新也至为重要。

## 使用本地开发环境在本地预览您的代码和内容 {#previewing-your-code-and-content-locally-with-the-local-development-environment}

若要準備AEM Headless專案以準備啟動，請確定專案的所有組成部份皆正常運作。

為此，您必須將所有內容（程式碼、內容和設定）整合在一起，並在本機開發環境中測試其上線準備程度。

本機開發環境由三個主要區域組成：

1. AEM專案 — 包含AEM開發人員將處理的所有自訂程式碼、設定和內容
1. 本地 AEM 运行时 – 本地版本的 AEM 创作和发布服务，用于从 AEM 项目部署代码
1. 本地 Dispatcher 运行时 – 包含 Dispatcher 模块的 Apache httpd Web 服务器的本地版本

設定本機開發環境後，您可以在本機部署靜態Node伺服器，模擬為React應用程式提供內容服務。

若要更深入地瞭解如何設定本機開發環境以及內容預覽所需的所有相依性，請參閱 [生產部署檔案](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/overview.html?lang=en).

## 準備您的AEM Headless應用程式上線 {#prepare-your-aem-headless-application-for-golive}

<!-- Start of CDN Review -->

現在，您可以遵循下面概述的最佳實務，讓AEM Headless應用程式做好啟動準備。

### 啟動前保護您的Headless應用程式 {#secure-and-scale-before-launch}

1. 準備 [驗證](/help/sites-developing/headless/graphql-api/graphql-authentication-content-fragments.md) (適用於您的GraphQL請求)

### 模型结构与 GraphQL 输出 {#structure-vs-output}

* 避免建立輸出超過15 KB JSON （gzip壓縮）的查詢。 长 JSON 文件是客户端应用程序要分析的资源密集型文件。
* 避免超过五个嵌套级别的片段层级。其他级别会使内容作者难以考虑其更改产生的影响。
* 使用多对象查询而不是在模型中使用依赖项层级对查询进行建模。如此一來，重新建構JSON輸出的長期彈性得以增強，且無需進行多項內容變更。

### 最大程度地提高 CDN 缓存命中率 {#maximize-cdn}

* 不要使用直接 GraphQL 查询，除非您从表面请求实时内容。
   * 尽可能使用持久查询。
   * 提供600秒以上的CDN TTL，讓CDN可以快取它們。
   * AEM 可以计算模型更改对现有查询的影响。
* 在低和高內容變更率之間分割JSON檔案/GraphQL查詢，以減少到CDN的使用者端流量並指派較高的TTL。 這麼做可將CDN使用原始伺服器重新驗證JSON的情況降至最低。
* 若要使CDN中的內容失效，請使用「軟清除」。 這麼做可讓CDN重新下載內容，而不會造成快取遺失。

>[!NOTE]
>
>另請參閱 [其他資源](#additional-resources) 以取得有關CDN和快取的詳細資訊。

### 缩短下载 Headless 内容的时间 {#improve-download-time}

* 确保 HTTP 客户端使用 HTTP/2。
* 确保 HTTP 客户端接受 gzip 的标头请求。
* 最大程度地减少用于托管 JSON 的域和引用的构件的数量。
* 使用 `Last-modified-since` 以重新整理資源。
* 使用 JSON 文件中的 `_reference` 输出开始下载资产，而无需分析完整的 JSON 文件。

<!-- End of CDN Review -->

## 部署到生产 {#deploy-to-production}

部署到生產環境取決於您是否擁有 *傳統* 使用Maven進行部署的AEM執行個體，或位於Adobe Managed Services (AMS)且因此使用Cloud Manager的執行個體。

## 使用Maven部署到生產環境 {#deploy-to-production-maven}

對於 *傳統* 使用Maven部署（非AMS），請參閱 [WKND教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/project-setup.html?lang=en#build) 以取得概覽。

## 使用Cloud Manager部署到生產環境 {#deploy-to-production-cloud-manager}

如果您是使用Cloud Manager的AMS客戶，在確保一切經過測試且正常運作後，您可以將程式碼更新推送至 [Cloud Manager中的集中Git存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/git-integration.html).

將更新上傳到Cloud Manager後，使用將它們部署到AEM [Cloud Manager的CI/CD管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-deployment.html).

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
      * 檢查使用者、請求和載入的數量
* 存取應用程式和空間專用的效能報表
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
* 若要檢查使用者端應用程式是否存在或傳送問題，請在使用者端應用程式中檢查JSON
* 若要檢查是否存在與快取內容或AEM相關的問題，請使用GraphQL檢查JSON

### 借助支持记录错误 {#logging-a-bug-with-support}

若您需要進一步協助，請完成下列步驟，以有效率地向「支援」記錄錯誤：

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
* 上線完成後該做什麼。

您已啟動您的第一個AEM Headless專案，或現在已具備執行此作業的所有知識。 做得好！

### 探究单页应用程序 {#explore-spa}

不過，沒有必要停止AEM中的Headless商店。 在 [歷程的快速入門部分](getting-started.md#integration-levels)，其中說明了AEM如何不僅支援headless傳送和傳統的全棧疊模式，也支援結合了兩者優點的混合模式。

如果專案需要這種彈性，請繼續進行歷程的額外部分（選填）， [如何使用AEM建立單頁應用程式(SPA)。](create-spa.md)

## 其他资源 {#additional-resources}

* [AEM Developing指南](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/the-basics.html?lang=en)

* [WKND教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en)

* [適用於AEM的Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=zh-Hans)

* CDN快取

   * [控制CDN快取](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html#controlling-a-cdn-cache)

   * 設定 [CDN重寫程式](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/osgi-configuration-settings.html) (*搜尋CDN重寫程式*)
