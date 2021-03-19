---
title: 性能指南
seo-title: 性能指南
description: 本文提供有关如何优化AEM部署性能的一般准则。
seo-description: 本文提供有关如何优化AEM部署性能的一般准则。
uuid: 38cf8044-9ff9-48df-a843-43f74b0c0133
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 9ccbc39e-aea7-455e-8639-9193abc1552f
feature: 配置
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2994'
ht-degree: 5%

---


# 性能指南{#performance-guidelines}

本页提供有关如何优化AEM部署性能的一般准则。 如果您是初次接触AEM，请浏览以下页面，然后开始阅读性能指南：

* [AEM Basic Concepts](/help/sites-deploying/deploy.md#basic-concepts)
* [AEM中的存储概述](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [建议的部署](/help/sites-deploying/recommended-deploys.md)
* [技术要求](/help/sites-deploying/technical-requirements.md)

以下说明了可用于AEM的部署选项(滚动以视图所有选项):

<table>
 <tbody>
  <tr>
   <td><p><strong>AEM</strong></p> <p><strong>产品</strong></p> </td>
   <td><p><strong>拓扑</strong></p> </td>
   <td><p><strong>操作系统</strong></p> </td>
   <td><p><strong>应用程序服务器</strong></p> </td>
   <td><p><strong>JRE</strong></p> </td>
   <td><p><strong>安全</strong></p> </td>
   <td><p><strong>微内核</strong></p> </td>
   <td><p><strong>数据存储</strong></p> </td>
   <td><p><strong>索引</strong></p> </td>
   <td><p><strong>Web 服务器</strong></p> </td>
   <td><p><strong>浏览器</strong></p> </td>
   <td><p><strong>Marketing Cloud</strong></p> </td>
  </tr>
  <tr>
   <td><p>站点</p> </td>
   <td><p>非HA</p> </td>
   <td><p>Windows</p> </td>
   <td><p>CQSE</p> </td>
   <td><p>Oracle</p> </td>
   <td><p>LDAP</p> </td>
   <td><p>Tar</p> </td>
   <td><p>区段</p> </td>
   <td><p>属性</p> </td>
   <td><p>Apache</p> </td>
   <td><p>Edge</p> </td>
   <td><p>Target</p> </td>
  </tr>
  <tr>
   <td><p>资产</p> </td>
   <td><p>Publish-HA</p> </td>
   <td><p>Solaris</p> </td>
   <td><p>WebLogic</p> </td>
   <td><p>IBM</p> </td>
   <td><p>SAML</p> </td>
   <td><p>MongoDB</p> </td>
   <td><p>文件</p> </td>
   <td><p>Lucene</p> </td>
   <td><p>IIS</p> </td>
   <td><p>IE</p> </td>
   <td><p>Analytics</p> </td>
  </tr>
  <tr>
   <td><p>社区</p> </td>
   <td><p>Author-CS</p> </td>
   <td><p>红帽</p> </td>
   <td><p>WebSphere</p> </td>
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
   <td><p>表单</p> </td>
   <td><p>作者卸载</p> </td>
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
   <td><p>作者群集</p> </td>
   <td><p>IBM AIX</p> </td>
   <td><p>JBoss</p> </td>
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
   <td><p>SUSE</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB/SQLServer</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>资产</p> </td>
  </tr>
  <tr>
   <td><p>商务</p> </td>
   <td><p>MSRP</p> </td>
   <td><p>Apple OS</p> </td>
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
   <td><p>奥德</p> </td>
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
   <td><p>屏幕</p> </td>
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
   <td><p>文档安全性</p> </td>
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
   <td><p>进程管理</p> </td>
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
>性能指南主要适用于AEM Sites。

## 何时使用性能指南{#when-to-use-the-performance-guidelines}

您应在以下情况下使用性能准则：

* **首次部署**:首次计划部署AEM Sites或资产时，请务必了解配置微内核、节点存储和数据存储时可用的选项（与默认设置相比）。例如，将TarMK的数据存储的默认设置更改为文件数据存储。
* **升级到新版本**:升级到新版本时，了解与运行环境相比的性能差异非常重要。例如，从AEM 6.1升级到6.2，或从AEM 6.0 CRX2升级到6.2 OAK。
* **响应时间很慢**:当选定的Nodestore体系结构不满足您的要求时，了解与其他拓扑选项相比的性能差异非常重要。例如，部署TarMK而不是MongoMK，或者使用文件数据存储而不是Amazon S3或Microsoft Azure数据存储。
* **添加更多作者**:当建议的TarMK拓扑不满足性能要求并且向上调整Author节点已达到可用的最大容量时，了解与将MongoMK与三个或更多作者节点一起使用相比的性能差异非常重要。例如，部署MongoMK而不是TarMK。
* **添加更多内容**:当建议的数据存储体系结构不符合您的要求时，了解与其他数据存储选项相比的性能差异非常重要。示例：使用Amazon S3或Microsoft Azure数据存储而不是文件数据存储。

## 简介 {#introduction}

本章概述了AEM体系结构及其最重要的组件。 它还提供开发指南，并描述TarMK和MongoMK基准测试中使用的测试方案。

### AEM平台{#the-aem-platform}

AEM平台由以下组件组成：

![chlimage_1](assets/chlimage_1a.png)

有关AEM平台的详细信息，请参阅[什么是AEM](/help/sites-deploying/deploy.md#what-is-aem)。

### AEM体系架构{#the-aem-architecture}

AEM部署有三个重要的构建块。 内容作者、编辑者和批准者使用的&#x200B;**作者实例**&#x200B;创建和审阅内容。 内容获得批准后，将发布到最终用户从中访问的名为&#x200B;**发布实例**&#x200B;的第二个实例类型。 第三个构建块是&#x200B;**Dispatcher**，它是一个模块，用于处理缓存和URL过滤，并安装在Web服务器上。 有关AEM体系架构的其他信息，请参阅[典型部署方案](/help/sites-deploying/deploy.md#typical-deployment-scenarios)。

![chlimage_1-1](assets/chlimage_1-1a.png)

### 微内核{#micro-kernels}

在AEM中，Micro Kernel充当持久管理器。 与AEM一起使用的微内核有三种类型：TarMK、MongoDB和关系数据库（受限支持）。 请根据您的实例目的和所考虑的部署类型，选择符合您需求的部署。有关微内核的其他信息，请参阅[建议部署](/help/sites-deploying/recommended-deploys.md)页。

![chlimage_1-2](assets/chlimage_1-2a.png)

### Nodestore {#nodestore}

在AEM中，二进制数据可以独立于内容节点存储。 存储二进制数据的位置称为&#x200B;**数据存储**，而内容节点和属性的位置称为&#x200B;**节点存储**。

>[!NOTE]
>
>Adobe建议TarMK作为客户用于AEM作者实例和发布实例的默认持久性技术。

>[!CAUTION]
>
>关系数据库微内核受到限制支持。 在使用此类型的微内核之前，请与[Adobe客户关怀](https://helpx.adobe.com/cn/marketing-cloud/contact-support.html)联系。

![chlimage_1-3](assets/chlimage_1-3a.png)

### 数据存储{#data-store}

在处理大量二进制文件时，建议使用外部数据存储而不是默认节点存储，以便最大化性能。 例如，如果您的项目需要大量媒体资源，则将这些资源存储在File或Azure/S3 Data Store下比直接存储在MongoDB中更快地访问它们。

有关可用配置选项的更多详细信息，请参阅[配置节点和数据存储](/help/sites-deploying/data-store-config.md)。

>[!NOTE]
>
>Adobe建议选择使用Adobe Managed Services在Azure或Amazon Web Services(AWS)上部署AEM的选项，在该选项中，客户将从具备在这些云计算环境中部署和操作AEM的经验和技能的团队受益。 请参阅我们的[有关Adobe Managed Services](https://www.adobe.com/marketing-cloud/enterprise-content-management/managed-services-cloud-platform.html?aemClk=t)的其他文档。
>
>有关如何在Azure或AWS上部署AEM的建议，我们强烈建议在Adobe Managed Services之外直接与云提供商或我们的合作伙伴之一合作，支持在您选择的云环境中部署AEM。 选定的云提供商或合作伙伴负责规模规范、设计和实施他们将支持的架构，以满足您的特定性能、负载、可扩展性和安全要求。
>
>有关其他详细信息，另请参阅[技术要求](/help/sites-deploying/technical-requirements.md#supported-platforms)页。

### 搜索 {#search-features}

本节中列出的是与AEM一起使用的自定义索引提供程序。 要了解有关索引的更多信息，请参阅[Oak查询和索引](/help/sites-deploying/queries-and-indexing.md)。

>[!NOTE]
>
>对于大多数部署，Adobe建议使用Lucene索引。 您只应将Solr用于特殊和复杂部署中的可伸缩性。

![chlimage_1-4](assets/chlimage_1-4a.png)

### 开发指南{#development-guidelines}

您应针对AEM开发以&#x200B;**性能和可伸缩性**&#x200B;为目标。 以下是您可以遵循的许多最佳实践：

**DO**

* 应用表示、逻辑和内容的分离
* 使用现有AEM API(例如：Sling)和工具(例如：复制)
* 根据实际内容进行开发
* 优化可缓存性
* 最大程度地减少保存次数(例如：使用临时工作流)
* 确保所有HTTP端点都是RESTful
* 限制JCR观测范围
* 注意异步线程

**不要**

* 如果可以，请不要直接使用JCR API
* 不要更改/libs，而是使用叠加
* 不要尽可能使用查询
* 不要使用Sling Bindings获取Java代码中的OSGi服务，而应使用：

   * @Reference in a DS component
   * @Inject in a Sling Model
   * sling.getService()Sightly Use类
   * sling.getService()
   * 服务跟踪器
   * 直接访问OSGi服务注册表

有关在AEM上进行开发的更多详细信息，请阅读[开发 — 基础知识](/help/sites-developing/the-basics.md)。 有关其他最佳实践，请参阅[开发最佳实践](/help/sites-developing/best-practices.md)。

### 基准方案{#benchmark-scenarios}

>[!NOTE]
>
>此页上显示的所有基准测试都已在实验室设置中执行。

下面详述的测试方案用于TarMK、MongoMk和TarMK与MongoMk章节的基准部分。 要查看特定基准测试使用的方案，请阅读[技术规范](/help/sites-deploying/performance-guidelines.md#tarmk-performance-benchmark)表中的方案字段。

**单个产品方案**

AEM Assets:

* 用户交互：浏览资产/搜索资产/下载资产/读取资产元数据/更新资产元数据/上传资产/运行上传资产工作流
* 执行模式：并发用户，每个用户一次交互

**混合产品方案**

AEM Sites +资产：

* 站点用户交互：阅读文章页面/阅读页面/创建段落/编辑段落/创建内容页面/激活内容页面/作者搜索
* 资产用户交互：浏览资产/搜索资产/下载资产/读取资产元数据/更新资产元数据/上传资产/运行上传资产工作流
* 执行模式：并发用户，每用户混合交互

**垂直用例方案**

媒体:

* 阅读文章页面(27.4%)、阅读页面(10.9%)、创建会话(2.6%)、激活内容页面(1.7%)、创建内容页面(0.4%)、创建段落(4.3%)、编辑段落(0.9%)、图像组件(0.9%)、资产(20%)、阅读资产元数据(8.5%)、下载资产(4.2%)、搜索资产(0.2%)、更新资产元数据(2.4%)、上传资产(1.2%)、浏览项目(4.9%)、阅读项目(6.6%)、项目添加资产(1.2%)%)、项目添加站点(1.2%)、创建项目(0.1%)、作者搜索(0.4%)
* 执行模式：并发用户，每用户混合交互

## TarMK {#tarmk}

本章为TarMK提供了一般性能指南，指定最低体系结构要求和设置配置。 还提供了基准测试以供进一步说明。

Adobe建议TarMK作为客户在所有部署方案（对于AEM作者实例和Publish实例）中使用的默认持久性技术。

有关TarMK的详细信息，请参阅[部署方案](/help/sites-deploying/recommended-deploys.md#deployment-scenarios)和[Tar存储](/help/sites-deploying/storage-elements-in-aem-6.md#tar-storage)。

### TarMK最低体系结构准则{#tarmk-minimum-architecture-guidelines}

>[!NOTE]
>
>下面介绍的最低体系结构指南针对生产环境和高流量站点。 这些是运行AEM所需的[最低规格](/help/sites-deploying/technical-requirements.md#prerequisites)**不**。

要在使用TarMK时确立良好的性能，您应从以下架构进行开始:

* 一个作者实例
* 两个发布实例
* 两个调度程序

以下是AEM站点和AEM Assets的架构指南。

>[!NOTE]
>
>如果共享文件数据存储，应将无二进制复制转为&#x200B;**ON**。

**AEM Sites的Tar架构指南**

![chlimage_1-5](assets/chlimage_1-5a.png)

**AEM Assets的Tar架构指南**

![chlimage_1-6](assets/chlimage_1-6a.png)

### TarMK设置指南{#tarmk-settings-guideline}

为了获得良好性能，您应遵循以下设置指南。 有关如何更改设置的说明，请参阅此页](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)。[

<table>
 <tbody>
  <tr>
   <td><strong>设置</strong></td>
   <td><strong>参数</strong></td>
   <td><strong>值</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>Sling作业队列</td>
   <td><code>queue.maxparallel</code></td>
   <td>将值设置为CPU核心数的一半。 </td>
   <td>默认情况下，每个作业队列的并发线程数等于CPU核心数。</td>
  </tr>
  <tr>
   <td>Granite临时工作流队列</td>
   <td><code>Max Parallel</code></td>
   <td>将值设置为CPU核心数的一半</td>
   <td> </td>
  </tr>
  <tr>
   <td>JVM参数</td>
   <td><p><code>Doak.queryLimitInMemory</code></p> <p><code>Doak.queryLimitReads</code></p> <p><code>Dupdate.limit</code></p> <p><code>Doak.fastQuerySize</code></p> </td>
   <td><p>500000</p> <p>100000</p> <p>250000</p> <p>True</p> </td>
   <td>在AEM 开始脚本中添加这些JVM参数，以防止扩展查询使系统过载。</td>
  </tr>
  <tr>
   <td>Lucene索引配置</td>
   <td><p><code>CopyOnRead</code></p> <p><code>CopyOnWrite</code></p> <p><code>Prefetch Index Files</code></p> </td>
   <td><p>启用</p> <p>启用</p> <p>启用</p> </td>
   <td>有关可用参数的详细信息，请参阅<a href="https://jackrabbit.apache.org/oak/docs/query/lucene.html">此页</a>。</td>
  </tr>
  <tr>
   <td>数据存储= S3数据存储</td>
   <td><p><code>maxCachedBinarySize</code></p> <p><code>cacheSizeInMB</code></p> </td>
   <td><p>1048576(1MB)或更小</p> <p>最大堆大小的2-10%</p> </td>
   <td>另请参阅<a href="/help/sites-deploying/data-store-config.md#data-store-configurations">数据存储配置</a>。</td>
  </tr>
  <tr>
   <td>DAM更新资产工作流</td>
   <td><code>Transient Workflow</code></td>
   <td>已选中</td>
   <td>此工作流用于管理资产的更新.</td>
  </tr>
  <tr>
   <td>DAM元数据写回</td>
   <td><code>Transient Workflow</code></td>
   <td>已选中</td>
   <td>此工作流管理XMP对原始二进制文件的回写，并设置JCR中上次修改的日期。</td>
  </tr>
 </tbody>
</table>

### TarMK性能基准{#tarmk-performance-benchmark}

#### 技术规范{#technical-specifications}

对以下规范执行了基准测试：

|  | **作者节点** |
|---|---|
| 服务器 | 裸机硬件(HP) |
| 操作系统 | RedHat Linux |
| CPU/核心 | 英特尔®至强® CPU E5-2407 @2.40GHz，8核 |
| RAM | 32 GB |
| 磁盘 | 磁性 |
| Java | Oracle JRE版本8 |
| JVM堆 | 16 GB |
| 产品 | AEM 6.2 |
| Nodestore | TarMK |
| 数据存储 | 文件DS |
| 方案 | 单个产品：资产/30个并发线程 |

#### 性能基准结果{#performance-benchmark-results}

>[!NOTE]
>
>以下数字已标准化为1作为基准，而不是实际吞吐量数。

![chlimage_1-7](assets/chlimage_1-7a.png) ![chlimage_1-8](assets/chlimage_1-8a.png)

## MongoMK {#mongomk}

选择MongoMK持久性后端而不是TarMK的主要原因是水平缩放实例。 这意味着有两个或多个活动的作者实例始终运行，并将MongoDB用作持久存储系统。 需要运行多个创作实例通常是因为单台服务器的CPU和内存容量(支持所有并发创作活动)不再可持续。

有关TarMK的详细信息，请参阅[部署方案](/help/sites-deploying/recommended-deploys.md#deployment-scenarios)和[ Mongo 存储](/help/sites-deploying/storage-elements-in-aem-6.md#mongo-storage)。

### MongoMK最低体系结构准则{#mongomk-minimum-architecture-guidelines}

要在使用MongoMK时获得良好性能，您应从以下架构进行开始:

* 三个作者实例
* 两个发布实例
* 三个MongoDB实例
* 两个调度程序

>[!NOTE]
>
>在生产环境中，MongoDB将始终用作具有主和两个辅助节点的复制副本集。 读和写操作将转到主节点，读操作可转到辅助节点。 如果存储不可用，可以用仲裁程序替换其中一个辅助节点，但MongoDB副本集必须始终由奇数的实例组成。

>[!NOTE]
>
>如果共享文件数据存储，应将无二进制复制转为&#x200B;**ON**。

![chlimage_1-9](assets/chlimage_1-9a.png)

### MongoMK设置指南{#mongomk-settings-guidelines}

为了获得良好性能，您应遵循以下设置指南。 有关如何更改设置的说明，请参阅此页](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)。[

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
   <td>Granite临时工作流队列</td>
   <td><code>Max Parallel</code></td>
   <td>将值设置为CPU核心数的一半。</td>
   <td> </td>
  </tr>
  <tr>
   <td>JVM参数</td>
   <td><p><code>Doak.queryLimitInMemory</code></p> <p><code>Doak.queryLimitReads</code></p> <p><code>Dupdate.limit</code></p> <p><code>Doak.fastQuerySize</code></p> <p><code>Doak.mongo.maxQueryTimeMS</code></p> </td>
   <td><p>500000</p> <p>100000</p> <p>250000</p> <p>True</p> <p>60000</p> </td>
   <td>在AEM 开始脚本中添加这些JVM参数，以防止扩展查询使系统过载。</td>
  </tr>
  <tr>
   <td>Lucene索引配置</td>
   <td><p><code>CopyOnRead</code></p> <p><code>CopyOnWrite</code></p> <p><code>Prefetch Index Files</code></p> </td>
   <td><p>启用</p> <p>启用</p> <p>启用</p> </td>
   <td>有关可用参数的详细信息，请参阅<a href="https://jackrabbit.apache.org/oak/docs/query/lucene.html">此页</a>。</td>
  </tr>
  <tr>
   <td>数据存储= S3数据存储</td>
   <td><p><code>maxCachedBinarySize</code></p> <p><code>cacheSizeInMB</code></p> </td>
   <td><p>1048576(1MB)或更小</p> <p>最大堆大小的2-10%</p> </td>
   <td>另请参阅<a href="/help/sites-deploying/data-store-config.md#data-store-configurations">数据存储配置</a>。</td>
  </tr>
  <tr>
   <td>DocumentNodeStoreService</td>
   <td><p><code>cache</code></p> <p><code>nodeCachePercentage</code></p> <p><code>childrenCachePercentage</code></p> <p><code>diffCachePercentage</code></p> <p><code>docChildrenCachePercentage</code></p> <p><code>prevDocCachePercentage</code></p> <p><code>persistentCache</code></p> </td>
   <td><p>2048</p> <p>35(25)</p> <p>20(10)</p> <p>30(5)</p> <p>10(3)</p> <p>4(4)</p> <p>./cache，size=2048,binary=0,-compact，-compress</p> </td>
   <td><p>缓存的默认大小设置为256 MB。</p> <p>对执行缓存失效所花费的时间产生影响。</p> </td>
  </tr>
  <tr>
   <td>橡树观察</td>
   <td><p><code>thread pool</code></p> <p><code>length</code></p> </td>
   <td><p>最小和最大= 20</p> <p>50000</p> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### MongoMK性能基准{#mongomk-performance-benchmark}

### 技术规范{#technical-specifications-1}

对以下规范执行了基准测试：

|  | **作者节点** | **MongoDB节点** |
|---|---|---|
| 服务器 | 裸机硬件(HP) | 裸机硬件(HP) |
| 操作系统 | RedHat Linux | RedHat Linux |
| CPU/核心 | 英特尔®至强® CPU E5-2407 @2.40GHz，8核 | 英特尔®至强® CPU E5-2407 @2.40GHz，8核 |
| RAM | 32 GB | 32 GB |
| 磁盘 | 磁性 — 超过1k IOPS | 磁性 — 超过1k IOPS |
| Java | Oracle JRE版本8 | 不适用 |
| JVM堆 | 16 GB | 不适用 |
| 产品 | AEM 6.2 | MongoDB 3.2 WiredTiger |
| Nodestore | MongoMK | 不适用 |
| 数据存储 | 文件DS | 不适用 |
| 方案 | 单个产品：资产/30个并发线程 | 单个产品：资产/30个并发线程 |

### 性能基准结果{#performance-benchmark-results-1}

>[!NOTE]
>
>以下数字已标准化为1作为基准，而不是实际吞吐量数。

![chlimage_1-10](assets/chlimage_1-10a.png) ![chlimage_1-11](assets/chlimage_1-11a.png)

## TarMK与MongoMK {#tarmk-vs-mongomk}

在两者之间进行选择时，需要考虑的基本规则是TarMK是为性能而设计的，而MongoMK是用于可扩展性的。 Adobe建议TarMK作为客户在所有部署方案（对于AEM作者实例和Publish实例）中使用的默认持久性技术。

选择MongoMK持久性后端而不是TarMK的主要原因是水平缩放实例。 这意味着有两个或多个活动的作者实例始终运行，并将MongoDB用作持久存储系统。 需要运行多个创作实例通常是因为单个服务器的CPU和内存容量(支持所有并发创作活动)不再可持续。

有关TarMK与MongoMK的更多详细信息，请参阅[建议部署](/help/sites-deploying/recommended-deploys.md#microkernels-which-one-to-use)。

### TarMK与MongoMk准则{#tarmk-vs-mongomk-guidelines}

**TarMK的优势**

* 专门为内容管理应用程序构建
* 文件始终一致，并且可以使用任何基于文件的备份工具进行备份
* 提供故障转移机制 — 有关更多详细信息，请参阅[冷备用](/help/sites-deploying/tarmk-cold-standby.md)
* 提供高性能、可靠的数据存储，并将运营开销降至最低
* 更低的总体拥有成本（总体拥有成本）

**选择MongoMK的标准**

* 一天内连接的指定用户数：成千上万
* 并发用户数：数百或更多
* 每天资产摄取的量：数十万甚至更多
* 每天的页面编辑量：数十万甚至更多
* 每天的搜索量：数万甚至更多

### TarMK与MongoMK基准测试{#tarmk-vs-mongomk-benchmarks}

>[!NOTE]
>
>以下数字已标准化为1作为基准，而不是实际吞吐量数。

### 方案1技术规范{#scenario-technical-specifications}

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
   <td>RedHat Linux</td>
   <td>RedHat Linux</td>
   <td> </td>
  </tr>
  <tr>
   <td>CPU/核心</td>
   <td>英特尔®至强® CPU E5-2407 @2.40GHz，8核</td>
   <td>英特尔®至强® CPU E5-2407 @2.40GHz，8核</td>
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
   <td>磁性 — 超过1k IOPS</td>
   <td>磁性 — 超过1k IOPS</td>
   <td> </td>
  </tr>
  <tr>
   <td>Java</td>
   <td>Oracle JRE版本8</td>
   <td>不适用</td>
   <td> </td>
  </tr>
  <tr>
   <td>JVM堆16GB</td>
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
   <td>TarMK或MongoMK</td>
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

### 方案1性能基准结果{#scenario-performance-benchmark-results}

![chlimage_1-12](assets/chlimage_1-12a.png)

### 方案2技术规范{#scenario-technical-specifications-1}

>[!NOTE]
>
>要使MongoDB的作者数与使用一个TarMK系统的作者数相同，您需要一个包含两个AEM节点的群集。 四个节点MongoDB群集可以处理1.8倍于一个TarMK实例的作者数。 八个节点MongoDB群集可处理的作者数是一个TarMK实例的2.3倍。

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>作者TarMK节点</strong></td>
   <td><strong>作者MongoMK节点</strong></td>
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
   <td>RedHat Linux</td>
   <td>RedHat Linux</td>
   <td>RedHat Linux</td>
  </tr>
  <tr>
   <td>CPU/核心</td>
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
   <td>SSD - 10k IOPS</td>
   <td>SSD - 10k IOPS</td>
   <td>SSD - 10k IOPS</td>
  </tr>
  <tr>
   <td>Java</td>
   <td>Oracle JRE版本8</td>
   <td><br /> Oracle JRE版本8</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>JVM堆16GB</td>
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
   <td>TarMK </td>
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
   <td><p><br /> <br /> 垂直用例：媒体/ 2000个并发线程</p> </td>
   <td></td>
   <td></td>
  </tr>
 </tbody>
</table>

### 方案2性能基准结果{#scenario-performance-benchmark-results-1}

![chlimage_1-13](assets/chlimage_1-13a.png)

### AEM Sites和资产的架构可伸缩性指导原则{#architecture-scalability-guidelines-for-aem-sites-and-assets}

![chlimage_1-14](assets/chlimage_1-14a.png)

## 性能指南摘要{#summary-of-performance-guidelines}

本页所载准则概述如下：

* **TarMK with File Datastore是** 大多数客户建议的架构：

   * 最小拓扑：一个作者实例、两个Publish实例、两个Dispatcher
   * 如果共享文件数据存储，则启用无二进制复制

* **MongoMK with File Datastore** 是建议的创作层水平可伸缩性的架构：

   * 最小拓扑：三个作者实例、三个MongoDB实例、两个Publish实例、两个Dispatcher
   * 如果共享文件数据存储，则启用无二进制复制

* **Nodestore应** 存储在本地磁盘上，而不是网络连接存储(NAS)上
* 使用&#x200B;**Amazon S3**&#x200B;时：

   * Amazon S3数据存储在作者层和发布层之间共享
   * 必须启用无二进制复制
   * Datastore Garbage Collection要求在所有“作者”和“发布”节点上先运行一次，然后在“作者”节点上再运行一次

* **除了基于大多数常见搜索的开箱即用索引外，还应** 创建自定义索引

   * Lucene索引应用于自定义索引

* **自定义工作流可以大幅提高性能**，例如，删除“更新资产”工作流中的视频步骤，禁用未使用的侦听器，等等。

有关详细信息，请阅读[建议的部署](/help/sites-deploying/recommended-deploys.md)页。
