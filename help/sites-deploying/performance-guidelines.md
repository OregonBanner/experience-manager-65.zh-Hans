---
title: 性能准则
description: 本文提供了有关如何优化AEM部署性能的一般准则。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
feature: Configuring
exl-id: 5a305a5b-0c3d-413b-88c1-1f5abf7e1579
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2935'
ht-degree: 4%

---

# 性能准则{#performance-guidelines}

本页提供了有关如何优化AEM部署性能的一般准则。 如果您是AEM的新用户，请在开始阅读性能准则之前阅读以下页面：

* [AEM基本概念](/help/sites-deploying/deploy.md#basic-concepts)
* [AEM中的存储概述](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [建议的部署](/help/sites-deploying/recommended-deploys.md)
* [技术要求](/help/sites-deploying/technical-requirements.md)

下图显示了可用于AEM的部署选项（滚动查看所有选项）：

<table>
 <tbody>
  <tr>
   <td><p><strong>AEM</strong></p> <p><strong>产品</strong></p> </td>
   <td><p><strong>拓扑</strong></p> </td>
   <td><p><strong>操作系统</strong></p> </td>
   <td><p><strong>应用程序服务器</strong></p> </td>
   <td><p><strong>JRE</strong></p> </td>
   <td><p><strong>安全性</strong></p> </td>
   <td><p><strong>微内核</strong></p> </td>
   <td><p><strong>数据存储</strong></p> </td>
   <td><p><strong>索引</strong></p> </td>
   <td><p><strong>Web 服务器</strong></p> </td>
   <td><p><strong>浏览器</strong></p> </td>
   <td><p><strong>Experience Cloud</strong></p> </td>
  </tr>
  <tr>
   <td><p>Sites</p> </td>
   <td><p>非HA</p> </td>
   <td><p>Windows</p> </td>
   <td><p>CQSE</p> </td>
   <td><p>oracle</p> </td>
   <td><p>LDAP</p> </td>
   <td><p>Tar</p> </td>
   <td><p>市场细分</p> </td>
   <td><p>属性</p> </td>
   <td><p>Apache</p> </td>
   <td><p>Edge</p> </td>
   <td><p>目标</p> </td>
  </tr>
  <tr>
   <td><p>资源</p> </td>
   <td><p>Publish-HA</p> </td>
   <td><p>Solaris™</p> </td>
   <td><p>WebLogic</p> </td>
   <td><p>IBM®</p> </td>
   <td><p>SAML</p> </td>
   <td><p>MongoDB</p> </td>
   <td><p>文件</p> </td>
   <td><p>Lucene</p> </td>
   <td><p>IIS</p> </td>
   <td><p>IE</p> </td>
   <td><p>分析</p> </td>
  </tr>
  <tr>
   <td><p>社区</p> </td>
   <td><p>Author-CS</p> </td>
   <td><p>Red Hat®</p> </td>
   <td><p>WebSphere®</p> </td>
   <td><p>HP</p> </td>
   <td><p>Oauth</p> </td>
   <td><p>RDB/Oracle</p> </td>
   <td><p>S3/Azure</p> </td>
   <td><p>Solr</p> </td>
   <td><p>iPlanet</p> </td>
   <td><p>FireFox</p> </td>
   <td><p>营销活动</p> </td>
  </tr>
  <tr>
   <td><p>Forms</p> </td>
   <td><p>Author-Offload</p> </td>
   <td><p>HP-UX</p> </td>
   <td><p>Tomcat</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB/DB2</p> </td>
   <td><p>MongoDB</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>铬黄</p> </td>
   <td><p>Social</p> </td>
  </tr>
  <tr>
   <td><p>移动设备</p> </td>
   <td><p>Author-Cluster</p> </td>
   <td><p>IBM® AIX®</p> </td>
   <td><p>JBoss®</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB/MySQL</p> </td>
   <td><p>RDBMS</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Safari</p> </td>
   <td><p>受众</p> </td>
  </tr>
  <tr>
   <td><p>多站点</p> </td>
   <td><p>ASRP</p> </td>
   <td><p>SUSE®</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB/SQLServer</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>资源</p> </td>
  </tr>
  <tr>
   <td><p>商务</p> </td>
   <td><p>MSRP</p> </td>
   <td><p>Apple操作系统</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>激活</p> </td>
  </tr>
  <tr>
   <td><p>Dynamic Media</p> </td>
   <td><p>JSRP</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>移动设备</p> </td>
  </tr>
  <tr>
   <td><p>Brand Portal</p> </td>
   <td><p>J2E</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>AoD</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>LiveFyre</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>Screens</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>文档安全</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>流程管理</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>桌面应用程序</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>性能准则主要适用于AEM Sites。

## 何时使用性能准则 {#when-to-use-the-performance-guidelines}

在以下情况下使用性能准则：

* **首次部署**：在计划首次部署AEM Sites或Assets时，了解可用的选项很重要。 特别是在配置微内核、节点存储和数据存储时（与默认设置相比）。 例如，将TarMK的“数据存储”的默认设置更改为“文件数据存储”。
* **升级到新版本**：在升级到新版本时，了解与运行环境相比的性能差异很重要。 例如，从AEM 6.1升级到6.2，或从AEM 6.0 CRX2升级到6.2 OAK。
* **响应时间慢**：当所选的Nodestore架构不满足您的要求时，了解与其他拓扑选项相比的性能差异非常重要。 例如，部署TarMK而不是MongoMK，或使用文件数据存储而不是Amazon S3或Microsoft® Azure数据存储。
* **添加更多作者**：当推荐的TarMK拓扑不符合性能要求并且扩展创作节点的大小已达到可用的最大容量时，请了解性能差异。 请比较是否将MongoMK与三个或更多创作节点一起使用。 例如，部署MongoMK而不是TarMK。
* **添加更多内容**：如果推荐的数据存储架构不符合您的要求，请务必了解与其他数据存储选项相比的性能差异。 示例：使用Amazon S3或Microsoft®Azure数据存储，而不是文件数据存储。

## 简介 {#introduction}

本章概述AEM架构及其最重要的组件。 它还提供了开发准则，并描述了TarMK和MongoMK基准测试中使用的测试场景。

### AEM平台 {#the-aem-platform}

AEM平台包含以下组件：

![chlimage_1](assets/chlimage_1a.png)

有关AEM平台的更多信息，请参阅 [什么是AEM](/help/sites-deploying/deploy.md#what-is-aem).

### AEM架构 {#the-aem-architecture}

AEM部署有三个重要的构建块。 此 **创作实例** 内容作者、编辑者和批准者使用此功能创建和审阅内容。 内容获得批准后，将发布到名为的第二个实例类型 **发布实例** 从最终用户访问的位置。 第三个构建基块是 **Dispatcher** 是一个处理缓存和URL过滤的模块，安装在Web服务器上。 有关AEM架构的其他信息，请参阅 [典型部署方案](/help/sites-deploying/deploy.md#typical-deployment-scenarios).

![chlimage_1-1](assets/chlimage_1-1a.png)

### 微内核 {#micro-kernels}

微内核在AEM中充当持久性管理器。 AEM使用三种类型的微内核：TarMK、MongoDB和关系数据库（受限制支持）。 根据您的需要，如何选择一种解决方案取决于实例的用途和您考虑的部署类型。 有关微型内核的其他信息，请参见 [建议的部署](/help/sites-deploying/recommended-deploys.md) 页面。

![chlimage_1-2](assets/chlimage_1-2a.png)

### Nodestore {#nodestore}

在AEM中，二进制数据可以独立于内容节点进行存储。 存储二进制数据的位置称为 **数据存储**，而内容节点和属性的位置称为 **节点存储**.

>[!NOTE]
>
>Adobe建议将TarMK作为客户用于AEM创作实例和发布实例的默认持久性技术。

>[!CAUTION]
>
>关系数据库微内核的支持受限。 联系人 [Adobe客户关怀](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home#support) 使用这种类型的微内核之前。

![chlimage_1-3](assets/chlimage_1-3a.png)

### 数据存储 {#data-store}

在处理大量二进制文件时，建议您使用外部数据存储而不是默认节点存储来最大化性能。 例如，如果您的项目需要许多媒体资产，将它们存储在File或Azure/S3数据存储区下，则访问这些媒体资产的速度会比直接将它们存储在MongoDB中更快。

有关可用配置选项的更多详细信息，请参阅 [配置节点和数据存储](/help/sites-deploying/data-store-config.md).

>[!NOTE]
>
>Adobe建议您选择使用AdobeManaged Services在Azure或Amazon Web Services (AWS)上部署AEM的选项。 客户将受益于具有在这些云计算环境中部署和操作AEM的经验和技能的团队。 请参阅 [有关AdobeManaged Services的其他文档](https://business.adobe.com/products/experience-manager/managed-services.html?aemClk=t).
>
>有关如何在AdobeManaged Services之外的Azure或AWS上部署AEM的建议，Adobe建议直接与云提供商合作。 或者，与在您选择的云环境中支持AEM部署的Adobe合作伙伴之一合作。 选定的云提供商或合作伙伴负责其支持的架构的规模规格、设计和实施，以满足您的特定性能、负载、可扩展性和安全要求。
>
>>另请参阅 [技术要求](/help/sites-deploying/technical-requirements.md#supported-platforms) 页面。

### 搜索 {#search-features}

本节中列出了与AEM一起使用的自定义索引提供程序。 要了解有关索引的更多信息，请参阅 [Oak查询和索引](/help/sites-deploying/queries-and-indexing.md).

>[!NOTE]
>
>对于大多数部署，Adobe建议使用Lucene索引。 在专业且复杂的部署中，仅使用Solr实现可扩展性。

![chlimage_1-4](assets/chlimage_1-4a.png)

### 开发准则 {#development-guidelines}

针对AEM目标进行开发 **性能和可扩展性**. 以下是您可以遵循的最佳实践：

**DO**

* 应用演示文稿、逻辑和内容的分离
* 使用现有AEM API（例如：Sling）和工具（例如：复制）
* 在实际内容的上下文中开发
* 开发以获得最佳可缓存性
* 最大程度地减少保存次数（例如：使用临时工作流）
* 确保所有HTTP端点均为RESTful
* 限制JCR观察的范围
* 请注意异步线程

**不要**

* 如果可以，请不要直接使用JCR API
* 请勿更改/libs，而是使用叠加
* 尽量不要使用查询
* 请勿使用Sling绑定在Java™代码中获取OSGi服务，而是使用：

   * DS组件中的@Reference
   * 在Sling模型中@Inject用
   * Sightly Use类中的sling.getService()
   * JSP中的sling.getService()
   * ServiceTracker
   * 直接访问OSGi服务注册表

有关在AEM上进行开发的更多详细信息，请阅读 [开发 — 基础知识](/help/sites-developing/the-basics.md). 有关其他最佳实践，请参阅 [开发最佳实践](/help/sites-developing/best-practices.md).

### 设定方案基准 {#benchmark-scenarios}

>[!NOTE]
>
>此页面上显示的所有基准测试均已在实验室环境中执行。

下面详述的测试场景用于TarMK、MongoMk和TarMK与MongoMk章节的基准部分。 要查看哪个方案用于特定基准测试，请阅读中的方案字段 [技术规范](/help/sites-deploying/performance-guidelines.md#tarmk-performance-benchmark) 表格。

**单个产品方案**

AEM Assets：

* 用户交互：浏览资源/搜索资源/下载资源/读取资源元数据/更新资源元数据/上传资源/运行上传资源工作流
* 执行模式：并发用户，每个用户单次交互

**混合产品方案**

AEM Sites +资产：

* 站点用户交互：读取文章页面/读取页面/创建段落/编辑段落/创建内容页面/激活内容页面/作者搜索
* 资源用户交互：浏览资源/搜索资源/下载资源/读取资源元数据/更新资源元数据/上传资源/运行上传资源工作流
* 执行模式：并发用户，每个用户的混合交互

**垂直用例方案**

媒体：

* `Read Article Page (27.4%), Read Page (10.9%), Create Session (2.6%), Activate Content Page (1.7%), Create Content Page (0.4%), Create Paragraph (4.3%), Edit Paragraph (0.9%), Image Component (0.9%), Browse Assets (20%), Read Asset Metadata (8.5%), Download Asset (4.2%), Search Asset (0.2%), Update Asset Metadata (2.4%), Upload Asset (1.2%), Browse Project (4.9%), Read Project (6.6%), Project Add Asset (1.2%), Project Add Site (1.2%), Create Project (0.1%), Author Search (0.4%)`
* 执行模式：并发用户，每个用户的混合交互

## tarmk {#tarmk}

本章提供了TarMK的一般性能准则，用于指定最低架构要求和设置配置。 还提供了基准测试，以进一步澄清。

Adobe建议将TarMK作为客户在所有部署场景中使用的默认持久性技术，适用于AEM创作实例和发布实例。

有关TarMK的详细信息，请参见 [部署方案](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) 和 [Tar存储](/help/sites-deploying/storage-elements-in-aem-6.md#tar-storage).

### TarMK最低架构准则 {#tarmk-minimum-architecture-guidelines}

>[!NOTE]
>
>下面介绍的最低架构准则适用于生产环境和高流量站点。 这些准则包括 **非** 该 [最低规范](/help/sites-deploying/technical-requirements.md#prerequisites) 运行AEM。

要在使用TarMK时建立良好的性能，您应该从以下架构开始：

* 一个创作实例
* 两个发布实例
* 两个Dispatcher

以下说明了AEM sites和AEM Assets的架构准则。

>[!NOTE]
>
>应关闭无二进制复制 **开启** 如果文件数据存储已共享。

**AEM Sites的Tar架构准则**

![chlimage_1-5](assets/chlimage_1-5a.png)

**AEM Assets的Tar架构准则**

![chlimage_1-6](assets/chlimage_1-6a.png)

### TarMK设置指南 {#tarmk-settings-guideline}

要获得良好的性能，您应该遵循下面提供的设置指南。 有关如何更改设置的说明， [查看此页面](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=en).

<table>
 <tbody>
  <tr>
   <td><strong>设置</strong></td>
   <td><strong>参数</strong></td>
   <td><strong>价值</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>Sling作业队列</td>
   <td><code>queue.maxparallel</code></td>
   <td>将值设置为CPU核心数的一半。 </td>
   <td>默认情况下，每个作业队列的并发线程数等于CPU核心数。</td>
  </tr>
  <tr>
   <td>Granite Transient工作流队列</td>
   <td><code>Max Parallel</code></td>
   <td>将值设置为CPU核心数的一半</td>
   <td> </td>
  </tr>
  <tr>
   <td>JVM参数</td>
   <td><p><code>Doak.queryLimitInMemory</code></p> <p><code>Doak.queryLimitReads</code></p> <p><code>Dupdate.limit</code></p> <p><code>Doak.fastQuerySize</code></p> </td>
   <td><p>500000</p> <p>100000</p> <p>250000</p> <p>True</p> </td>
   <td>要防止扩展查询使系统过载，请在AEM启动脚本中添加这些JVM参数。</td>
  </tr>
  <tr>
   <td>Lucene索引配置</td>
   <td><p><code>CopyOnRead</code></p> <p><code>CopyOnWrite</code></p> <p><code>Prefetch Index Files</code></p> </td>
   <td><p>启用</p> <p>启用</p> <p>启用</p> </td>
   <td>有关可用参数的更多详细信息，请参阅 <a href="https://jackrabbit.apache.org/oak/docs/query/lucene.html">此页面</a>.</td>
  </tr>
  <tr>
   <td>数据存储= S3数据存储</td>
   <td><p><code>maxCachedBinarySize</code></p> <p><code>cacheSizeInMB</code></p> </td>
   <td><p>1048576 (1 MB)或更小</p> <p>最大栈大小的2-10%</p> </td>
   <td>另请参阅 <a href="/help/sites-deploying/data-store-config.md#data-store-configurations">数据存储配置</a>.</td>
  </tr>
  <tr>
   <td>DAM更新资产工作流</td>
   <td><code>Transient Workflow</code></td>
   <td>已选中</td>
   <td>此工作流用于管理资产的更新。</td>
  </tr>
  <tr>
   <td>DAM元数据写回</td>
   <td><code>Transient Workflow</code></td>
   <td>已选中</td>
   <td>此工作流用于管理XMP对原始二进制文件的回写，并设置JCR中的上次修改日期。</td>
  </tr>
 </tbody>
</table>

### TarMK性能基准 {#tarmk-performance-benchmark}

#### 技术规范 {#technical-specifications}

基准测试按以下规范执行：

| | **作者节点** |
|---|---|
| 服务器 | 裸机硬件(HP) |
| 操作系统 | Red Hat® Linux® |
| CPU/内核 | Intel(R) Xeon(R) CPU E5-2407 @2.40GHz，8核 |
| RAM | 32 GB |
| 磁盘 | 磁性 |
| Java™ | oracleJRE版本8 |
| JVM栈 | 16 GB |
| 产品 | AEM 6.2 |
| Nodestore | tarmk |
| 数据存储 | 文件DS |
| 方案 | 单个产品：资产/ 30个并发线程 |

#### 性能基准结果 {#performance-benchmark-results}

>[!NOTE]
>
>下面显示的数字已标准化为1作为基线，而不是实际的吞吐量数字。

![chlimage_1-7](assets/chlimage_1-7a.png) ![chlimage_1-8](assets/chlimage_1-8a.png)

## MongoMK {#mongomk}

与TarMK相比，选择MongoMK持久性后端的主要原因是要水平缩放实例。 此功能意味着始终运行两个或多个活动的创作实例，并使用MongoDB作为持久性存储系统。 运行多个创作实例的需要通常是由于单个服务器的CPU和内存容量（支持所有并发创作活动）不再可持续。

有关TarMK的详细信息，请参见 [部署方案](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) 和 [Mongo存储](/help/sites-deploying/storage-elements-in-aem-6.md#mongo-storage).

### MongoMK最低架构准则 {#mongomk-minimum-architecture-guidelines}

要在使用MongoMK时建立良好的性能，您应该从以下架构开始：

* 三个作者实例
* 两个发布实例
* 三个MongoDB实例
* 两个Dispatcher

>[!NOTE]
>
>在生产环境中， MongoDB始终用作具有主副本集和两个辅助副本集的副本集。 读取和写入操作将转到主数据库，读取操作将转到辅助数据库。 如果存储不可用，可以使用仲裁器替换其中一个辅助副本，但MongoDB副本集必须始终由奇数实例组成。

>[!NOTE]
>
>应关闭无二进制复制 **开启** 如果文件数据存储已共享。

![chlimage_1-9](assets/chlimage_1-9a.png)

### MongoMK设置准则 {#mongomk-settings-guidelines}

要获得良好的性能，您应该遵循下面提供的设置指南。 有关如何更改设置的说明， [查看此页面](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=en).

<table>
 <tbody>
  <tr>
   <td><strong>设置</strong></td>
   <td><strong>参数</strong></td>
   <td><strong>值（默认）</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>Sling作业队列</td>
   <td><code>queue.maxparallel</code></td>
   <td>将值设置为CPU核心数的一半。 </td>
   <td>默认情况下，每个作业队列的并发线程数等于CPU核心数。</td>
  </tr>
  <tr>
   <td>Granite Transient工作流队列</td>
   <td><code>Max Parallel</code></td>
   <td>将值设置为CPU核心数的一半。</td>
   <td> </td>
  </tr>
  <tr>
   <td>JVM参数</td>
   <td><p><code>Doak.queryLimitInMemory</code></p> <p><code>Doak.queryLimitReads</code></p> <p><code>Dupdate.limit</code></p> <p><code>Doak.fastQuerySize</code></p> <p><code>Doak.mongo.maxQueryTimeMS</code></p> </td>
   <td><p>500000</p> <p>100000</p> <p>250000</p> <p>True</p> <p>60000</p> </td>
   <td>要防止扩展查询使系统过载，请在AEM启动脚本中添加这些JVM参数。</td>
  </tr>
  <tr>
   <td>Lucene索引配置</td>
   <td><p><code>CopyOnRead</code></p> <p><code>CopyOnWrite</code></p> <p><code>Prefetch Index Files</code></p> </td>
   <td><p>启用</p> <p>启用</p> <p>启用</p> </td>
   <td>有关可用参数的更多详细信息，请参阅 <a href="https://jackrabbit.apache.org/oak/docs/query/lucene.html">此页面</a>.</td>
  </tr>
  <tr>
   <td>数据存储= S3数据存储</td>
   <td><p><code>maxCachedBinarySize</code></p> <p><code>cacheSizeInMB</code></p> </td>
   <td><p>1048576 (1 MB)或更小</p> <p>最大栈大小的2-10%</p> </td>
   <td>另请参阅 <a href="/help/sites-deploying/data-store-config.md#data-store-configurations">数据存储配置</a>.</td>
  </tr>
  <tr>
   <td>DocumentNodeStoreService</td>
   <td><p><code>cache</code></p> <p><code>nodeCachePercentage</code></p> <p><code>childrenCachePercentage</code></p> <p><code>diffCachePercentage</code></p> <p><code>docChildrenCachePercentage</code></p> <p><code>prevDocCachePercentage</code></p> <p><code>persistentCache</code></p> </td>
   <td><p>2048</p> <p>35 (25)</p> <p>20 (10)</p> <p>30 (5)</p> <p>10 (3)</p> <p>4 (4)</p> <p>。/cache，size=2048，binary=0，-compact，-compress</p> </td>
   <td><p>缓存的默认大小设置为256 MB。</p> <p>会影响执行缓存失效所需的时间。</p> </td>
  </tr>
  <tr>
   <td>oak-observation</td>
   <td><p><code>thread pool</code></p> <p><code>length</code></p> </td>
   <td><p>最小值和最大值= 20</p> <p>50000</p> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### MongoMK性能基准 {#mongomk-performance-benchmark}

### 技术规范 {#technical-specifications-1}

基准测试按以下规范执行：

| | **创作节点** | **MongoDB节点** |
|---|---|---|
| 服务器 | 裸机硬件(HP) | 裸机硬件(HP) |
| 操作系统 | Red Hat® Linux® | Red Hat® Linux® |
| CPU/内核 | Intel(R) Xeon(R) CPU E5-2407 @2.40GHz，8核 | Intel(R) Xeon(R) CPU E5-2407 @2.40GHz，8核 |
| RAM | 32 GB | 32 GB |
| 磁盘 | 磁性 — 1k IOPS以上 | 磁性 — 1k IOPS以上 |
| Java™ | oracleJRE版本8 | 不适用 |
| JVM栈 | 16 GB | 不适用 |
| 产品 | AEM 6.2 | MongoDB 3.2 WiredTiger |
| Nodestore | MongoMK | 不适用 |
| 数据存储 | 文件DS | 不适用 |
| 方案 | 单个产品：资产/ 30个并发线程 | 单个产品：资产/ 30个并发线程 |

### 性能基准结果 {#performance-benchmark-results-1}

>[!NOTE]
>
>下面显示的数字已标准化为1作为基线，而不是实际的吞吐量数字。

![chlimage_1-10](assets/chlimage_1-10a.png) ![chlimage_1-11](assets/chlimage_1-11a.png)

## TarMK对MongoMK {#tarmk-vs-mongomk}

在两者之间进行选择时，需要考虑的基本规则是TarMK是针对性能而设计的，而MongoMK则是用于可扩展性。 Adobe建议将TarMK作为客户在所有部署场景中使用的默认持久性技术，适用于AEM创作实例和发布实例。

与TarMK相比，选择MongoMK持久性后端的主要原因是要水平缩放实例。 此功能意味着始终运行两个或多个活动的创作实例，并使用MongoDB作为持久性存储系统。 运行多个创作实例的需要通常是由于单个服务器的CPU和内存容量（支持所有并发创作活动）不再可持续。

有关TarMK与MongoMK的更多详细信息，请参阅 [建议的部署](/help/sites-deploying/recommended-deploys.md#microkernels-which-one-to-use).

### TarMK与MongoMk准则 {#tarmk-vs-mongomk-guidelines}

**TarMK的优势**

* 专门为内容管理应用程序构建
* 文件始终保持一致，可以使用任何基于文件的备份工具进行备份
* 提供故障转移机制 — 请参阅 [冷备用](/help/sites-deploying/tarmk-cold-standby.md) 了解更多详细信息
* 以最低的操作开销提供高性能、可靠的数据存储
* 降低TCO（总体拥有成本）

**选择MongoMK的标准**

* 一天中连接的指定用户数：千或更多
* 并发用户数：以百计或更多
* 每天的资产摄取量：数十万或更多
* 每天页面编辑量：数十万或更多
* 每天的搜索量：以万或更多

### TarMK与MongoMK基准 {#tarmk-vs-mongomk-benchmarks}

>[!NOTE]
>
>下面显示的数字已标准化为1作为基线，而不是实际的吞吐量数字。

### 方案1技术规范 {#scenario-technical-specifications}

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>创作OAK节点</strong></td>
   <td><strong>MongoDB节点</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td>服务器</td>
   <td>裸机硬件(HP)</td>
   <td>裸机硬件(HP)</td>
   <td> </td>
  </tr>
  <tr>
   <td>操作系统</td>
   <td>Red Hat® Linux®</td>
   <td>Red Hat® Linux®</td>
   <td> </td>
  </tr>
  <tr>
   <td>CPU/内核</td>
   <td>Intel(R) Xeon(R) CPU E5-2407 @2.40GHz，8核</td>
   <td>Intel(R) Xeon(R) CPU E5-2407 @2.40GHz，8核</td>
   <td> </td>
  </tr>
  <tr>
   <td>RAM</td>
   <td>32 GB</td>
   <td>32 GB</td>
   <td> </td>
  </tr>
  <tr>
   <td>磁盘</td>
   <td>磁性 — 1k IOPS以上</td>
   <td>磁性 — 1k IOPS以上</td>
   <td> </td>
  </tr>
  <tr>
   <td>Java™</td>
   <td>oracleJRE版本8</td>
   <td>不适用</td>
   <td> </td>
  </tr>
  <tr>
   <td>JVM栈16GB</td>
   <td>16 GB</td>
   <td>不适用</td>
   <td> </td>
  </tr>
  <tr>
   <td>产品 </td>
   <td>AEM 6.2</td>
   <td>MongoDB 3.2 WiredTiger</td>
   <td> </td>
  </tr>
  <tr>
   <td>Nodestore</td>
   <td>tarmk或MongoMK</td>
   <td>不适用</td>
   <td> </td>
  </tr>
  <tr>
   <td>数据存储</td>
   <td>文件DS </td>
   <td>不适用</td>
   <td> </td>
  </tr>
  <tr>
   <td>方案</td>
   <td><p><br /> 单个产品：资产/每次运行30个并发线程</p> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 场景1性能基准结果 {#scenario-performance-benchmark-results}

![chlimage_1-12](assets/chlimage_1-12a.png)

### 方案2技术规范 {#scenario-technical-specifications-1}

>[!NOTE]
>
>要使用MongoDB启用与使用一个TarMK系统相同数量的作者，您需要具有两个AEM节点的集群。 与一个TarMK实例相比，四个节点的MongoDB群集可以处理1.8倍的“作者”数量。 8节点MongoDB群集处理的作者数是单个TarMK实例的2.3倍。

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>创作TarMK节点</strong></td>
   <td><strong>创作MongoMK节点</strong></td>
   <td><strong>MongoDB节点</strong></td>
  </tr>
  <tr>
   <td>服务器</td>
   <td>AWS c3.8xlarge</td>
   <td>AWS c3.8xlarge</td>
   <td>AWS c3.8xlarge</td>
  </tr>
  <tr>
   <td>操作系统</td>
   <td>Red Hat® Linux®</td>
   <td>Red Hat® Linux®</td>
   <td>Red Hat® Linux®</td>
  </tr>
  <tr>
   <td>CPU/内核</td>
   <td>32</td>
   <td>32</td>
   <td>32</td>
  </tr>
  <tr>
   <td>RAM</td>
   <td>60 GB</td>
   <td>60 GB</td>
   <td>60 GB</td>
  </tr>
  <tr>
   <td>磁盘</td>
   <td>固态硬盘 — 10,000IOPS</td>
   <td>固态硬盘 — 10,000IOPS</td>
   <td>固态硬盘 — 10,000IOPS</td>
  </tr>
  <tr>
   <td>Java™</td>
   <td>oracleJRE版本8</td>
   <td><br /> oracleJRE版本8</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>JVM栈16GB</td>
   <td>30 GB</td>
   <td>30 GB</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>产品 </td>
   <td>AEM 6.2</td>
   <td>AEM 6.2</td>
   <td><br /> MongoDB 3.2 WiredTiger</td>
  </tr>
  <tr>
   <td>Nodestore</td>
   <td>tarmk </td>
   <td>MongoMK</td>
   <td><br /> 不适用</td>
  </tr>
  <tr>
   <td>数据存储</td>
   <td>文件DS </td>
   <td><br /> 文件DS</td>
   <td><br /> 不适用</td>
  </tr>
  <tr>
   <td>方案</td>
   <td><p><br /> <br /> 垂直使用案例：媒体/ 2000个并发线程</p> </td>
   <td></td>
   <td></td>
  </tr>
 </tbody>
</table>

### 场景2性能基准结果 {#scenario-performance-benchmark-results-1}

![chlimage_1-13](assets/chlimage_1-13a.png)

### AEM Sites和Assets的架构可扩展性准则 {#architecture-scalability-guidelines-for-aem-sites-and-assets}

![chlimage_1-14](assets/chlimage_1-14a.png)

## 性能准则摘要  {#summary-of-performance-guidelines}

此页面上提供的准则可概括如下：

* **带有文件数据存储的TarMK**  — 为大多数客户推荐的体系结构：

   * 最小拓扑：一个创作实例、两个发布实例、两个Dispatcher
   * 如果文件数据存储是共享的，则启用无二进制复制

* **具有文件数据存储的MongoMK**  — 为创作层的水平可扩展性推荐的体系结构：

   * 最小拓扑：三个创作实例、三个MongoDB实例、两个发布实例、两个Dispatcher
   * 如果文件数据存储是共享的，则启用无二进制复制

* **Nodestore**  — 存储在本地磁盘上，而不是网络连接存储(NAS)
* 使用时 **Amazon S3**：

   * Amazon S3数据存储区在创作层和发布层之间共享
   * 必须打开无二进制复制
   * 数据存储垃圾收集要求首先在所有创作和发布节点上运行一次，然后在创作节点上再运行一次

* **除了开箱即用索引之外，还应创建自定义索引**  — 基于最常见的搜索

   * Lucene索引应该用于自定义索引

* **自定义工作流可以显着提高性能**  — 删除“更新资产”工作流中的视频步骤，禁用未使用的监听器等。

欲知更多详情，另请参阅 [建议的部署](/help/sites-deploying/recommended-deploys.md) 页面。
