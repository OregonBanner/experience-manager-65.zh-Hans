---
title: 的常规发行说明 [!DNL Adobe Experience Manager] 6.5
description: ”[!DNL Adobe Experience Manager] 6.5说明概述了版本信息、新增功能、安装方法和详细的更改列表。”
exl-id: b3d4a527-44ca-4eb6-b393-f3e8117cf1a6
source-git-commit: a51a863a4edf7e8b951a8361c5c7f0517b09f12a
workflow-type: tm+mt
source-wordcount: '4675'
ht-degree: 6%

---

# 的常规发行说明 [!DNL Adobe Experience Manager] 6.5{#general-release-notes-for-adobe-experience-manager}

## 版本信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] |
|---|---|
| 版本 | 6.5 |
| 类型 | 主要版本 |
| 正式发布日期 | 2019 年 4 月 8 日 |
| 建议的更新 | 参见 [AEM最近更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=zh-Hans). |

### Trivia {#trivia}

此版本的发布周期 [!DNL Adobe Experience Manager] 自2018年4月4日起，经过23次质量保证和错误修复迭代，结束于2019年3月28日。 此版本中修复的客户相关问题（包括增强功能和新功能）总数为1345。

[!DNL Adobe Experience Manager] 6.5自2019年4月8日起正式推出。

![AEM 6.5 Login屏幕](/help/assets/assets/aem65-login-v4.png)

## 新增功能 {#what-s-new}

[!DNL Adobe Experience Manager] 6.5是 [!DNL Adobe Experience Manager] 6.4代码库。 它提供新功能和增强功能、关键客户修复、高优先级客户增强功能以及面向产品稳定性的常规错误修复。它还包括 [!DNL Adobe Experience Manager] 6.4 Service Pack发行至SP4。

以下列表提供了概述，而后续页面列出了完整的详细信息。

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

的平台 [!DNL Adobe Experience Manager] 6.5在基于OSGi的框架的更新版本（Apache Sling和Apache Felix）和Java™内容存储库(Apache Jackrabbit Oak 1.10.2)的基础上构建。

快速入门使用Eclipse Jetty 9.4.15作为Servlet引擎。

#### Java™支持  {#java-support}

* 新增对Java™ 11和已支持的Java™ 8的支持。
* 为获得最佳性能，请用其他值覆盖默认GC值。 欲了解更多信息，请参见 [安装和更新](/help/sites-deploying/custom-standalone-install.md) 部分。
* Java™ 11和Java™ 8维护更新按Adobe分发，以供客户在AEM相关项目中使用(如果未从Oracle公开提供)。

#### Java™开发 {#java-development}

* 现在有 [两个版本的Uberjar](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies)，这是一个推荐版本，其中包含未标记为弃用的公共接口，另一个版本包含标记为弃用的接口。

#### 用户界面 {#user-interface}

对UI进行了各种增强，使其更高效、更易于使用。

* 新的用户和组权限管理UI。
* 列视图现在也仅加载屏幕上可见的条目，并且仅在用户开始滚动时才加载更多条目。 列表和卡片视图自6.0之后便已执行该操作（在6.4中进行了改进）。
* 列视图现在包含页面/资产的工作流状态（如果适用）。
* 此 [全选](/help/sites-authoring/basic-handling.md#select-all) 操作是一种对同一文件夹中的所有页面/资产执行操作的快速方法。
* 此 [全选](/help/sites-authoring/basic-handling.md#select-all) 操作会尝试对所有页面/资产执行该操作，而不仅仅是加载的内容。 如果操作未升级为处理批量操作，则会显示警告对话框。

>[!CAUTION]
>
>Adobe不打算进一步增强经典UI。 AEM 6.5包含经典UI，从早期版本升级的客户可以继续按原样使用它。 经典UI在弃用后仍得到完全支持。 [了解更多](/help/sites-deploying/ui-recommendations.md).

#### 搜索和编制索引 {#indexing-and-search}

* Oak中的搜索现在支持动态Facet。 例如，资源搜索中的筛选边栏显示估计的结果数。
* 扩展了QueryBuilder以提供带有动态Facet的结果。

#### 升级 {#upgrade}

* 运行AEM 6.2、6.3和6.4的客户支持直接就地升级到AEM 6.5。使用5.x或6.0/6.1且希望使用就地升级的客户需要先升级到6.4。 然后，升级到6.5，或通过直接将实例之间的内容传输到AEM 6.5的方式进行升级。
* 升级程序在6.5中大致保持不变。
* 我们将继续支持6.4中引入的向后兼容性、升级复杂性评估和可持续升级功能。根据需要对这些区域进行了特定于版本的更新。
* Pattern Detector封装现已简化。 有一个程序包可用于评估可用源版本是否升级到6.5。
* 有关升级过程的详细信息，请参见 [升级文档](/help/sites-deploying/upgrade.md).

#### 项目和工作流 {#projects-and-workflows}

* 6.4中引入的新工作流模型编辑器已得到改进，现包括更多操作，如复制和发布、工作流步骤中的变量支持以及增强功能 `OR` 和 `AND` 拆分。

#### 存储库 {#repository}

* Adobe Experience Manager 6.5的基础基于基于OSGi的框架的更新版本（Apache Sling和Apache Felix）和Java™ Content Repository： Apache Jackrabbit Oak 1.10.2.
* 有关已修复问题的概述，请参阅 [Apache Jackrabbit Oak Jira版本1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt)， [Apache Jackrabbit Oak Jira版本1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) 和 [Apache Jackrabbit Oak Jira版本1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt).

>[!CAUTION]
>
>自AEM 6.3以来一直存在的Oak区段Tar的新版本要求迁移存储库。 如果您从旧版TarMK升级，或者希望从其他类型的持久性中切换新的Segment Tar，则必须执行此步骤。 有关新区段Tar的益处的更多信息，请参阅 [迁移到Oak区段Tar常见问题解答](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar).

#### OSGI {#osgi}

* 添加了OSGi Promises和Converter实用程序库。

#### 安全性 {#security}

* 添加了管理员用户的密码过期时间。

#### Web 服务器 {#web-server}

* 快速入门分发使用Eclipse Jetty 9.4.15作为Servlet引擎(随9.3.22提供的AEM 6.4)。

### [!DNL Experience Manager] Sites {#experience-manager-sites}

#### 受管的单页应用程序 {#managed-single-page-apps}

页面编辑器添加了在客户端渲染体验（也称为）中的上下文内编辑内容和撰写/布局的功能 [作为SPA编辑器](/help/sites-developing/spa-architecture.md))。 现有的使用JavaScript框架构建的单页应用程序React或Angular可以使用AEM SJ SDK进行扩展，以使从业人员可编辑。

首次作为AEM 6.4 SP2的一部分提供，对于AEM 6.5，SPA支持将获得以下功能：

* 使用模板编辑器编辑和配置SPA的AEM可编辑部分
* 使用多站点管理创建国家/地区、特许经营或白标的SPA体验

#### Headless内容管理 {#headless-content-management}

AEM能够以各种格式和从栈栈的各个级别提供内容。 有些从2008年起就一直使用 [SlingGET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) 和 [POSTServlet](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html). 内容服务([Sling模型导出程序](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=en))在AEM 6.3中引入，是AEM SJ SDK用于对单页应用程序进行水合的方法。 此 [HTTP API for Assets](/help/assets/mac-api-assets.md) 是适用于AEM 6.5扩展的CRUD API。

新的HTTP API功能：

* 已添加 [对HTTP API for Assets的内容片段支持](/help/assets/assets-api-content-fragments.md) 创建、更新、读取和删除片段。
* 使用内容服务公开内容片段列表 [内容片段列表核心组件](https://www.aemcomponents.dev).
* [核心组件库](https://www.aemcomponents.dev) 其中显示了每个组件的默认Content Services JSON输出

#### Screens加载项 {#screens-add-on}

在所有数字显示器（从交互式信息亭到数字标牌）上高效地设计、交付和优化体验。

* 通过改进的内容重用跨数字和店内统一体验和内容
* 支持启动项的简化创作和批准/发布工作流程
* 使用SPA编辑器编辑并提供丰富的交互式体验
* 使用启动项规划标牌内容的未来内容更改
* 序列渠道中的计量的播放
* 使用源文件（如Excel工作表）自动创建项目结构
* 通过强大的在线和离线操作(Smart Sync)扩展了媒体播放器支持，甚至可以扩展到最大的标牌网络。
* 使用动态占位符按位置或配置数据触发的内容进行个性化。
* 由Adobe Analytics集成到AEM Screens Player中的统一见解

有关AEM Screens更改的更多详细信息 — 请参阅 [AEM Screens用户指南](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=zh-Hans).

#### 组件和模板开发 {#component-amp-template-development}

* 对于新项目，请参阅Maven项目原型18+ [GitHub发行说明](https://github.com/adobe/aem-project-archetype/releases).
* 有关新项目的单页应用程序Maven项目原型1.0.6+，请参阅 [GitHub发行说明](https://github.com/adobe/aem-spa-project-archetype/releases).
* HTL版本1.4，请参见 [GitHub发行说明](https://github.com/adobe/htl-spec/releases/tag/1.4).

   * 用于字符串、数组和对象的“in”运算符：

      ```html
      ${'a' in 'abc'}
      ${100 in myArray}
      ${'a' in myObject}
      ```

   * 具有data-sly-set的变量声明：
      `<sly data-sly-set.title="${currentPage.title}"/>${title}`

   * 列出并重复控制参数：开始、步骤、结束：
      `<h2 data-sly-repeat="${currentPage.listChildren @ begin = 1, step=2}">${item.title}</h2>`

   * 用于data-sly-unwrap的标识符：

      ```html
      <div data-sly-unwrap.isUnwrapped="${myCondition || myOtherCondition}">
      text <span data-sly-test="${isUnwrapped}>is unwrapped</code>
      </div>
      ```

   * 支持负数

* 核心组件2.3.2+，请参阅 [GitHub发行说明](https://github.com/adobe/aem-core-wcm-components/releases).
* 布局容器的网格系统，请参见 [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid).
* Clientlib管理器：将Google Closure Compiler默认为JavaScript clientlibs的缩小（旧默认为Yahoo YUI），并将Google Closure Compiler更新为版本v20190121
* 模板编辑器和策略

   * 为使用JS SDK(也称为SPA编辑器)的单页应用程序创建和编辑模板

* 引用站点We.Retail 4.0，请参阅 [GitHub发行说明](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases).
* 升级现有站点以使用最新编辑器功能的工具包，请参见 [GitHub存储库](https://github.com/adobe/aem-modernize-tools)

>[!CAUTION]
>
>AEM包含1.12.4版本的jQuery库，可提供与现有自定义代码的最大兼容性。 Adobe已做出修改以解决已知安全问题。

#### 站点管理 {#site-administration}

* 此 [引用](/help/sites-authoring/author-environment-tools.md#references) 边栏有一个新部分，用于列出指向所选页面的内部链接。 在计划使页面脱机或删除时，这非常有用 — 可查看在使页面脱机之前需要调整哪些页面。
* 此 [列表视图](/help/sites-authoring/basic-handling.md#list-view) 有一个新的工作流列，当页面处于工作流中时，该列会显示状态。
* 在 [页面属性](/help/sites-authoring/editing-page-properties.md)，现在可以在为页面分配缩略图（缩略图选项卡）时浏览现有资源。

#### 页面编辑器 {#page-editor}

* 允许对使用JS SDK(也称为SPA编辑器)的React和Angular客户端组件构建的单页应用程序体验进行上下文内编辑和合成
* 仅当页面配置了基架页面时，才会显示基架模式。

#### 内容片段和编辑器 {#content-fragments-amp-editor}

* 新 [批注](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations) 内容片段编辑器中的边栏，用于发表常规评论并查看在文本中发表的评论（也会显示在时间轴边栏中）
* 能够设置中多行文本元素的默认内容类型 [内容片段模型](/help/assets/content-fragments/content-fragments-models.md) 转换为简单文本、富文本或标记
* 添加 [注释/批注](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment) 通过在RTE（全屏视图）中选择文本
* [比较版本](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) 通过参考边栏并排的内容片段
* 资产下载报表现在相应地显示内容片段
* 添加 [对资产HTTP API的内容片段支持](/help/assets/assets-api-content-fragments.md) 通过/api.json. 有用于创建、更新、读取和删除内容片段的API。

#### 体验片段 {#experience-fragments}

* 改进了的索引 [体验片段](/help/sites-authoring/experience-fragments.md)，因此可在搜索正在使用它们的页面中找到它们的内容。
* 此 [导出到Target](/help/sites-administering/experience-fragments-target.md) 选项现在允许您以JSON(默认为HTML)或两者的形式发送体验片段。

#### 翻译 {#translation}

* 通过使用项目母版简化翻译项目的创建。
* 通过将翻译作业设置为默认批准状态，简化翻译项目的执行。
* 允许更新第三方翻译记忆库中具有更改的已翻译页面。
* 允许以JSON格式导出翻译作业。
* 更新Microsoft®翻译集成以使用V3 API。

#### 多站点管理(MSM) {#multi-site-management-msm}

* 对于使用PushOnModify的转出配置，更好地处理页面移动操作以避免不一致状态。
* 默认情况下，在LiveCopy结构中创建页面将创建一个独立页面。
* 在使用JS SDK(也称为SPA编辑器)的单页应用程序中使用MSM功能

#### 启动项 {#launches}

* 适用于启动项的新审核和批准工作流，以及仅提升已批准的启动页面的功能
* 已添加 [UI中的选项，用于选择在提升步骤之后立即删除启动项](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)

#### 内容定位和模拟 {#content-targeting-simulation}

* ContextHub数据层和客户端规则引擎JavaScript已更新，默认使用jQuery 3。

#### AEM和Adobe Target {#aem-amp-adobe-target}

>[!CAUTION]
>
>当前：
>
>* 仅 `at.js 1.x` 如果您在AEM Activities控制台中使用Adobe Target作为定位引擎，则支持。
>
>* 两者 `at.js. 1.x` 和 `at.js 2.x` 如果您使用体验片段导出到Target并在Target控制台中运行活动，则支持。


* Adobe Target集成现在使用Target Standard API。 早期版本的AEM使用Target Classic HTTP API，该API现已弃用。
* Adobe Target `mbox.js` 包括版本63。 Adobe强烈建议您将实施切换为 `at.js` v1.x.
* `at.js` 现已包含版本1.5.0。 Adobe建议您使用 [Adobe Experience Platform Launch](https://business.adobe.com/products/experience-platform/launch.html) 预配 `at.js` 将v1.x添加到站点中。

#### AEM和Adobe Analytics {#aem-amp-adobe-analytics}

* `s_code.js` 包括H.27.5。 Adobe建议您将实施切换到 `AppMeasurement.js`
* `AppMeasurement.js` 包括v1.8.0。 Adobe建议您使用 [Adobe Experience Platform Launch](https://business.adobe.com/products/experience-platform/launch.html) 将AppMeasurement.js预配到站点中。

#### AEM和Commerce {#aem-commerce}

Commerce Integration Framework的改进自AEM 6.4以来采用了更快的发行周期。 [在此处了解详情](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/integrations/magento.html).

#### Communities加载项 {#communities-add-on}

要获取最新版本，请参阅 [部署社区](/help/communities/deploy-communities.md) 部分。

##### 社区参与方面的增强 {#enhancements-to-community-engagement}

**@Mentions支持**
AEM Communities现在允许注册用户在用户生成的内容中标记（提及）其他注册会员以引起他们的注意。 随后会通知已标记（提及）的成员，并包含指向相应的用户生成内容的深层链接。 但是，用户可以选择禁用/启用Web和电子邮件通知。

![At mentions支持](/help/release-notes/assets/at-mentions.png)

社区用户无需搜索其名字、姓氏或用户名即可查看是否有人联系过他们或需要他们关注。 此外，它允许UGC作者从能够最好地解决该问题并添加输入的特定注册用户那里寻求响应。

社区管理员需要 **启用提及功能** ，以允许注册用户使用这些组件上的功能。

**组消息传递**

注册的社区成员现在可以通过单个电子邮件组合将私信批量发送到群组，而不是单独将相同的消息发送给群组成员。 允许 [群组消息](/help/communities/configure-messaging.md)，启用两个实例 [消息传送操作服务](/help/communities/messaging.md#group-messaging).

![组消息](/help/release-notes/assets/group-messaging.png)

##### 对批量审核的增强 {#enhancements-to-bulk-moderation}

批量审核中的自定义筛选条件

[自定义筛选条件](/help/communities/moderation.md#custom-filters) 现在可以开发并添加到批量审核UI中。

A [示例项目](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) 中提供了用于演示通过标记进行过滤的示例 [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter). 此项目可用作开发类似自定义筛选器的基础。

![自定义筛选条件](/help/release-notes/assets/custom-tag-filter.png)

**批量审核中的列表视图**

批量审核提供了具有改进UI的新列表视图，以显示用户生成的内容条目。

![列表视图中的批量审阅](/help/release-notes/assets/list-view-moderation.png)

##### 站点和组管理的增强功能 {#enhancements-to-site-and-group-management}

**作者端站点和组管理员**

从AEM 6.5开始，Communities允许分散管理（和管理）不同的社区站点和组/嵌套组。 托管多个社区站点和嵌套组的组织现在可以在创建站点（和组）时为作者端的管理员角色选择成员。

![站点管理员](/help/release-notes/assets/site-admin.png)

站点管理员可以在任何层次结构级别创建组并成为默认管理员。 这些管理员以后可由其他组管理员删除。 组管理员可以管理其组G1并创建嵌套在G1下的子组。

##### 增强功能 {#enhancements-to-enablement}

**SCORM 2017.1支持**

AEM 6.5 Communities的启用功能支持可共享内容对象引用模型 [(SCORM) 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) 引擎。

* 启用组件上的键盘导航支持
* AEM Communities中的启用组件（例如目录和课程播放、任务、文件库）支持键盘导航以提高可访问性。

##### 其他增强功能 {#other-enhancements}

* Solr 7支持
* 在设置MSRP和DSRP时，AEM 6.5社区支持搜索平台的Apache Solr 7.0版本。

### [!DNL Experience Manager Assets] {#experience-manager-assets}

AEM 6.5引入了以下功能和增强功能，以提高AEM用户、DAM角色以及相关创意和营销角色的生产效率。

#### 与集成 [!DNL Adobe Creative Cloud] 和创意工作流 {#integration-with-adobe-creative-cloud-and-creative-workflows}

[!DNL Adobe Experience Manager] 提供了多种方法来与集成 [!DNL Adobe Creative Cloud] 和共享资产，以便在创意和营销团队或业务团队密切协作的工作流中使用。 [!DNL Experience Manager] 6.5继续改进整合，进一步精简整合，以发掘更多机会，精简现有方法。

请阅读并了解的特定功能和集成 [!DNL Experience Manager] 6.5，您可以使用该版本以最好地支持您的content velocity用例。

##### Adobe Asset Link {#aal}

[!DNL Adobe Asset Link] 在内容创建过程中加强创意人员和营销人员之间的协作。 创意人员可以访问中存储的内容 [!DNL Experience Manager Assets]，而不离开他们最熟悉的应用程序。 创意人员可以使用中的应用程序内面板无缝浏览、搜索、签出和签入资产 [!DNL Adobe Photoshop]， [!DNL Adobe Illustrator]、和 [!DNL Adobe InDesign] 应用程序。

[!DNL Adobe Asset Link] 是的一部分 [企业Creative Cloud](https://www.adobe.com/cn/creativecloud/business/enterprise.html) 主动出击。 有关该集成的详细信息，包括 [!DNL Experience Manager] 部署，请参见 [Adobe资源链接](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html).

![在Adobe Photoshop中搜索资源](/help/release-notes/assets/asset_search_photoshop.png)

##### [!DNL Adobe Stock] 集成 {#stock}

您的组织可以使用其 [!DNL Adobe Stock] 内的企业计划 [!DNL Experience Manager Assets] 确保许可资产可广泛用于您的创意和营销项目。 您可以快速查找、预览和许可 [!DNL Adobe Stock] 使用DAM的强大功能以Experience Manager保存的资源 [!DNL Experience Manager].

[!DNL Adobe Stock] 该服务使设计人员和企业能够为其所有创意项目访问数百万张高质量、精选且免版税的照片、矢量、插图、视频、模板和3D资产。

有关更多信息，请参阅 [在Experience Manager Assets中使用Adobe Stock资源](/help/assets/aem-assets-adobe-stock.md).

![从Experience Manager Assets中预览Adobe Stock图像和许可证](/help/release-notes/assets/stock_image_preview_license_options.png)

*图：预览 [!DNL Adobe Stock] 中的图像和许可证 [!DNL Experience Manager Assets].*

![在Experience Manager中搜索和筛选许可的Adobe Stock图像](/help/release-notes/assets/aem-search-filters2.jpg)

*图：搜索和筛选许可的 [!DNL Adobe Stock] 中的图像 [!DNL Experience Manager].*

##### 中的动态引用 [!DNL Adobe InDesign] {#dynamic-references-in-indesign}

[!DNL Experience Manager Assets] 使用位置 [!DNL Adobe InDesign] 文件是动态的。 如果引用的资产在存储库中移动，引用会自动更新。 有关更多信息，请参阅 [如何管理复合资产](/help/assets/managing-linked-subassets.md).

#### Brand Portal功能 {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal] 帮助您轻松获取、有效控制并安全地跨设备向外部供应商/机构和内部业务用户分发经批准的资产。 它有助于提高资产共享效率，加快资产上市速度，并消除不合规使用和未经授权访问的风险。

有关更多信息，请参阅 [Brand Portal的新增功能](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=zh-Hans).

#### 连接的资源 {#connectedassets}

在大型企业中，可以分发创建网站所需的基础架构。 有时，网站创建功能和所需的数字资产位于不同的小仓库中。

[!DNL Experience Manager Sites] 提供创建网页和 [!DNL Experience Manager Assets] 是数字资产管理(DAM)系统，为网站提供所需的资产。 [!DNL Experience Manager] 现在通过集成支持上述用例 [!DNL Sites] 和 [!DNL Assets]. 参见 [如何配置和使用“连接的资产”功能](/help/assets/use-assets-across-connected-assets-instances.md).

![将资源从 [!DNL Experience Manager] 部署 [!DNL Sites] 其他项的页面 [!DNL Experience Manager] 部署](/help/release-notes/assets/connected-assets-drag-and-drop-only.gif)

*图：从拖动资产 [!DNL Experience Manager] 部署 [!DNL Sites] 页面上的其他 [!DNL Experience Manager] 部署。*

#### Dynamic Media {#dynamic-media}

[!DNL Dynamic Media] 在中提供增强的富媒体创作和交付 [!DNL Experience Manager Assets] 推动引人入胜的个性化前沿体验。 通过上传单个高质量的主要资源并使用Adobe的高级云渲染和查看器，您可以动态提供演绎版的任意组合，以支持贵组织的媒体策略。

有关新增的详细信息 [!DNL Dynamic Media] 功能，请参见 [Dynamic Media发行说明](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/release-notes/s7rn2017.html).

##### 360视频支持 {#video-support}

直接在中管理您的360视频文件 [!DNL Experience Manager] 使用先进的查看器为台式机、移动设备和VR耳机提供VR体验。 有关更多信息，请参阅 [使用360视频](/help/assets/360-video.md).

##### 自定义视频缩略图 {#custom-video-thumbnails}

您现在可以使用视频本身的帧或存储在DAM中的其他内容来自定义视频资产的缩略图。 有关其他说明，请参阅 [关于视频缩略图](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

##### 辅助功能增强功能 {#accessibility-enhancements}

[!DNL Dynamic Media] 查看器现在支持增强的辅助功能，如Aria支持、屏幕阅读器和替换文本。 有关其他详细信息，请参阅 [查看器参考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/homeviewers.html).

#### 搜索体验增强功能 {#experience-enhancement-for-searching}

[!DNL Experience Manager] 6.5以后，营销人员可以从搜索结果页面中更快地发现所需的资产。 即使在应用搜索过滤器之前，搜索彩块化也会更新为资源数。 查看筛选器的预期计数有助于用户有效地在搜索结果中导航。 有关更多信息，请参阅 [在Experience Manager中搜索资源](/help/assets/search-assets.md).

![在搜索彩块化中查看未筛选搜索结果的资产数量](/help/assets/assets/asset_search_results_in_facets_filters.png)

*图：在搜索Facet中查看未筛选搜索结果的资产数量。*

#### 可用性增强 {#usability-enhancement}

现在，您可以一次性选择文件夹中所有已加载的资产，或从搜索结果中选择所需的资产。 它可帮助您快速管理多个资产。 该复选框会选择符合场景的所有资源（如搜索结果），而不仅仅是中可见的资源 [!DNL Experience Manager] 界面。

![使用“全选”选项，只需单击一下即可选择所有加载的资源。](/help/release-notes/assets/select-all-in-aem-assets.gif)

*图：使用“全选”选项，只需单击一下即可选择所有加载的资源。*

#### 元数据增强功能 {#metadata-enhancements}

[!DNL Assets] 允许您为资源文件夹创建元数据架构，这些文件夹定义文件夹属性页面中显示的布局和元数据。 您现在可以将文件夹元数据架构分配给现有文件夹或在创建文件夹时。 有关更多信息，请参阅 [文件夹元数据架构](/help/assets/metadata-config.md#folder-metadata-schema).

指定级联元数据时，可在运行时从JSON文件加载选项，而不是在表单中手动键入。 有关更多信息，请参阅 [级联元数据](/help/assets/metadata-schemas.md#cascading-metadata).

#### 报告增强功能 {#reporting-enhancements}

内容片段和链接共享现已包含在下载的报表中。 有关更多信息，请参阅 [Assets报表](/help/assets/asset-reports.md).

### [!DNL Adobe Experience Manager Forms] {#experience-manager-forms}

AEM 6.5 Forms引入了几项新功能和增强功能。 这些亮点包括：

* 用于跟踪已提交表单、已处理文档和已渲染文档数量的交易报表
* 改进了交互式通信的可用性
* 自适应表单中基于云的数字签名
* 将自适应表单和交互式通信嵌入到AEM Sites单页应用程序(SPA)中。
* 在AEM Workflow中支持变量
* 交互式通信中的数据显示模式支持
* 对自适应表单和交互式通信表进行排序
* 自动验证表单数据模型中的输入数据

请参阅 [AEM 6.5 Forms的新增功能和增强功能摘要](/help/forms/using/whats-new.md) 有关新增功能和改进功能的信息以及文档资源。

### 使用以客户为中心的开发 {#leverage-customer-focused-development}

Adobe使用以客户为中心的开发模型，允许客户在开发过程的各个阶段（规范、开发和测试期间）做出贡献。 在此过程中，我们感谢所有参与的客户和合作伙伴。

Adobe已制定相关程序和流程，以便能够收集、划分优先顺序和跟踪以客户为中心的错误解决和增强请求开发。 此 [Experience Manager支持门户](https://experienceleague.adobe.com/?support-solution=Experience+Manager#support) 与Adobe增强和缺陷跟踪系统集成。 客户问题由客户支持团队尽可能确定和解决。 上报到研发部门后，将捕获所有客户信息，并用于优先顺序和报告目的。 在开发中优先考虑付费支持、被担保人问题和客户付费的增强功能。

这一优先顺序确定过程产生了750多项以客户为中心的更改，这些更改在AEM 6.5中得以修复。

## 属于发行版的文件列表 {#list-of-files-that-are-part-of-the-release}

**Foundation**

* 独立快速入门： `cq-quickstart-6.5.0.jar`.
* 应用程序服务器快速启动： `cq-quickstart-6.5.0.war`.
* 适用于各种Web服务器和平台的Dispatcher 4.3.2或更高版本。 参见 [下载链接](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html)
* 适用于Eclipse IDE的插件([阅读更多信息并下载](/help/sites-developing/aem-eclipse.md))

* Brackets代码编辑器扩展([阅读更多信息并下载](/help/sites-developing/aem-brackets.md))
* Maven/Gradle依赖项([下载链接](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.0/))

**Sites**

* 核心组件([GitHub项目](https://github.com/adobe/aem-core-wcm-components))
* We.Retail参考实施([了解更多](/help/sites-developing/we-retail.md))
* Maven项目原型：

   * 对于全栈站点： [GitHub项目](https://github.com/adobe/aem-project-archetype)
   * 对于使用React/Angular的单页应用程序： [GitHub项目](https://github.com/adobe/aem-spa-project-archetype)

* 适用于各种目标平台的AEM Screens Player ([下载](https://download.macromedia.com/screens/))

* 智能内容语言模型。 已预装英语 — 可以下载更多语言

   * [德语](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [西班牙语](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [意大利语](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [法语](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)

* AEM现代化工具套件，例如，对话框转换工具。 ([GitHub项目](https://github.com/adobe/aem-modernize-tools))

**Assets**

* 用于添加增强型PDF光栅器的包([了解更多](/help/assets/aem-pdf-rasterizer.md))
* 用于添加扩展RAW映像支持的包([了解更多](/help/assets/camera-raw.md))

**Forms**

* [AEM Forms功能包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [AEM Forms OSGi客户端SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/)

## 语言 {#languages}

用户界面提供以下语言版本：

* 英语
* 德语
* 法语
* 西班牙语
* 意大利语
* 巴西葡萄牙语
* 日语
* 简体中文
* 繁体中文（有限支持）
* 朝鲜语

[!DNL Experience Manager] 6.5已通过GB18030-2005 CITS使用中文编码标准的认证。

## 安装和更新 {#install-update}

有关设置要求，请参阅 [安装说明](/help/sites-deploying/custom-standalone-install.md).

有关详细说明，请参阅 [升级文档](/help/sites-deploying/upgrade.md).

## 支持的平台 {#supported-platforms}

查找支持的平台的完整列表，包括 [AEM 6.5技术要求](/help/sites-deploying/technical-requirements.md).

>[!NOTE]
>
>oracle已转为使用OracleJava™ SE产品的长期支持(LTS)模型。 Java™ 9和10是按Oracle划分的非LTS版本。 参见 [oracleJava™ SE支持路线图](https://www.oracle.com/technetwork/java/eol-135779.html). Adobe支持LTS版本的Java™，以便仅在生产中运行AEM。 推荐将Java™ 11与AEM 6.5一起使用。

## 已弃用和已删除的功能 {#deprecated-and-removed-features}

Adobe会持续评估产品功能，不断使用更强大的版本替换旧功能，也可能决定重新推出部分组件，以满足未来的期望或扩展要求。

对象 [!DNL Adobe Experience Manager] 6.5， [阅读已弃用和已删除的功能的列表](/help/release-notes/deprecated-removed-features.md). 该页面还包含未来变化的预告以及对从先前版本更新的客户的重要通知。

## 已知问题 {#known-issues}

### Platform {#platform}

* 报告了一个问题，其中删除了CRX-Quickstart及其内容。

   在每个此类操作中，确保属性 `htmllibmanager.fileSystemOutputCacheLocation` 不是空字符串：

   1. 呼叫 `/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`.
   2. 升级到AEM 6.5。
   3. 在AEM 6.5上执行“延迟内容迁移”。

   A [知识库](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) 提供了相关文章，其中提供了有关此问题的更多详细信息和解决方法。

* 如果将JDK 11与AEM 6.5实例一起使用，则在部署某些包后，某些页面可能会显示为空白。 日志文件中显示以下错误消息：

   ```java
   *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
   java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
   ```

要解决此错误，请执行以下操作：

1. 停止AEM实例。 转到 `<aem_server_path_on_server>crx-quickstart\conf` 然后打开 `sling.properties` 文件。 Adobe建议对此文件进行备份。

1. 搜索 `org.osgi.framework.bootdelegation=`. 添加 `jdk.internal.reflect,jdk.internal.reflect.*` 属性以将结果显示为。

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. 保存文件并重新启动AEM实例。

### Sites {#sites}

* **使用页面版本**： [如果页面已移动，您将无法再对移动之前创建的任何版本执行预览](/help/sites-authoring/working-with-page-versions.md#previewing-a-version).

### Assets {#assets}

* **搜索：** 如果搜索字符串包含前导空格([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **文件夹元数据架构**：添加选择按钮后，ID和值字段未按预期呈现，并且删除功能不起作用。 (CQ-4261144)
* 重命名资源时，资源名称中不能使用空格。 (CQ-4266403)

### Forms {#forms}

* 在Linux®操作系统上安装AEM Forms时， Digital Signature with Hardware Security Module不起作用。 (CQ-4266721)
* (仅限WebSphere上的AEM Forms®) **Forms Workflow** > **任务搜索** 选项在搜索 **管理员** 替换为 **用户名** 作为搜索条件。 (CQ-4266457)

* AEM Forms无法将经过JPEG压缩的TIF和TIFF文件转换为PDF文档。 (CQ-4265972)
* 此 **AEM Forms Assets扫描程序** 和 **书信到交互式通信迁移** 选项在 **AEM Forms迁移** 页面。 (CQ-4266572)

* (仅限JBoss® 7)当您从以前的版本升级到AEM 6.5 Forms时，如果以前的版本具有创建和使用了默认提交或默认渲染进程的副本的进程(.lca)，则使用此类进程(.lca)的HTML5 Forms无法执行所需的操作。 (CQ-4243928)
* 在自适应源中，当从规则编辑器调用表单数据模型服务以动态更新图像选择组件的值时，图像选择组件的值未更新。 (CQ-4254754)
* AEM Forms Designer安装程序需要32位版本的 [Visual C++可再发行运行时包2012](https://docs.microsoft.com/en-US/cpp/windows/latest-supported-vc-redist?view=msvc-170) 和 [Visual C++可再发行运行时包2013](https://support.microsoft.com/en-us/topic/update-for-visual-c-2013-and-visual-c-redistributable-package-5b2ac5ab-4139-8acc-08e2-9578ec9b2cf1). 在开始安装之前，请确保已安装前面提到的可再发行运行时包。 (CQ-4265668)

* PDF生成器不支持基于智能卡的身份验证。 当管理员启用组策略时 `Interactive Logon: Require Smart card` 在Windows服务器上，所有现有的PDF生成器用户都将失效。

* 当自适应表单配置为动态更新组件的值，并且通过Dispatcher访问承载表单的发布实例时，动态更新字段值的功能停止工作。 要解决此问题，请在发布实例上打开CRXDE，导航到 `/libs/fd/af/runtime/clientlibs/guideChartReducer`，并创建下面列出的资产。

   * 名称： allowProxy
   * 类型：布尔值
   * 值： true
   * 受保护：假
   * 必需：假
   * 多个：False
   * 自动创建： False

   利用属性，运行时文件夹下的客户端库可以访问代理。 (CQ-4268679)

* 启动AEM Forms时， `SAX Security Manager could not be setup` 出现警告。
* 在运行20.10.00版Adobe Acrobat Reader的Apple iOS或iPadOS上打开受AEM Forms Document Security保护的PDF时
* 在从 Apple iOS 设备提交包含标准 HTML 上传字段的表单时，有时不会发送文件内容，而在另一端会收到一个 0 字节的文件。Apple iOS 15.1 修复了此问题。

## 产品下载和支持（受限制的站点） {#product-download-and-support-restricted-sites}

以下网站仅供客户使用。 如果您是客户并且需要访问权限，请联系您的Adobe客户经理。

* [产品下载：licensing.adobe.com](https://licensing.adobe.com/).

* 产品更新、修补程序和软件包，用于 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).

* [通过Admin Console提供客户支持](https://adminconsole.adobe.com/). 有关更多信息，请参阅 [新的Adobe客户支持体验](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en).
