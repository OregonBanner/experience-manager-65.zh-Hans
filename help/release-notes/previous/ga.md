---
title: 的常规发行说明 [!DNL Adobe Experience Manager] 6.5
description: '"[!DNL Adobe Experience Manager] 6.5发行说明，其中概述了发行信息、新增功能、安装方式和详细的更改列表。”'
exl-id: b3d4a527-44ca-4eb6-b393-f3e8117cf1a6
source-git-commit: e3caa3e3067cf5e29cfcdf4286047eb346aefa23
workflow-type: tm+mt
source-wordcount: '4697'
ht-degree: 42%

---

# 的常规发行说明 [!DNL Adobe Experience Manager] 6.5{#general-release-notes-for-adobe-experience-manager}

## 版本信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] |
|---|---|
| 版本 | 6.5 |
| 类型 | 主要版本 |
| 公开发行日期 | 2019 年 4 月 8 日 |
| 推荐的更新 | 请参阅 [AEM近期更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=en). |

### 相关事项 {#trivia}

此版本的发布周期 [!DNL Adobe Experience Manager] 从2018年4月4日开始，经过23次质量保证和错误修复，于2019年3月28日结束。 此版本中修复的与客户相关的问题（包括增强功能和新增功能）总数为1345。

[!DNL Adobe Experience Manager] 6.5自2019年4月8日起正式发布。

![AEM 6.5 登录屏幕](/help/assets/assets/aem65-login-v4.png)

## 新增功能 {#what-s-new}

[!DNL Adobe Experience Manager] 6.5是的升级版本 [!DNL Adobe Experience Manager] 6.4代码库。 它提供了新增和增强功能、关键客户修复、高优先级客户增强功能，以及面向产品稳定性的一般错误修复。 它还包括 [!DNL Adobe Experience Manager] 6.4 Service Pack最多发布SP4。

下面的列表提供了概述 — 而后续页面则列出了完整的详细信息。

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

平台 [!DNL Adobe Experience Manager] 6.5基于基于OSGi的框架（Apache Sling和Apache Felix）和Java™内容存储库的更新版本而构建：阿帕奇·杰克拉布特橡1.10.2。

快速入门使用 Eclipse Jetty 9.4.15 作为 servlet 引擎。

#### Java™支持  {#java-support}

* 新增了对Java™ 11的支持，以及已支持的Java™ 8。
* 为获取最佳性能，请使用其他值覆盖默认的 GC 值。有关更多信息，请参阅 [安装和更新](/help/sites-deploying/custom-standalone-install.md) 中。
* Java™ 11和Java™ 8维护更新由Adobe分发，以便客户在与AEM相关的项目中使用(如果未从Oracle中公开提供)。

#### Java™开发 {#java-development}

* 现在有 [Uberjar的两个版本](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies)、具有未标记为弃用的公共界面的推荐版本，以及包含标记为弃用的界面的版本。

#### 用户界面 {#user-interface}

对 UI 进行了各种增强，使其更高效，更易于使用。

* 用户和组的新权限管理 UI.
* 列视图现在也只加载屏幕上可见的条目，并且仅在用户开始滚动时加载更多。 列表和卡片视图自6.0起便已执行该操作（在6.4中进行了改进）。
* 列视图现在包括页面/资产的工作流状态（如果适用）.
* [全选](/help/sites-authoring/basic-handling.md#select-all)操作是一种快速方法，可以对同一文件夹中的所有页面/资产执行操作.
* [全选](/help/sites-authoring/basic-handling.md#select-all)操作会尝试对所有页面/资源执行操作，而不仅仅是加载的页面/资源。如果未升级操作以处理批量操作，则会显示警告对话框。

>[!CAUTION]
>
>Adobe 不打算进一步增强经典 UI。AEM 6.5 包含经典 UI，从早期发行版升级的客户可以继续按原样使用它。经典UI在弃用时仍完全受支持。 [了解更多](/help/sites-deploying/ui-recommendations.md)。

#### 搜索和索引 {#indexing-and-search}

* 在 Oak 中搜索现在支持动态 Facet。例如，资产搜索中的过滤器边栏会显示预计的结果数。
* 扩展了 QueryBuilder 以提供包含动态 Facet 的结果.

#### 升级 {#upgrade}

* 运行AEM 6.2、6.3和6.4的客户支持直接就地升级到AEM 6.5。使用5.x或6.0/6.1且想要就地升级的客户需要首先升级到6.4。 然后，升级到6.5，或通过在实例之间直接将内容传输到AEM 6.5进行升级。
* 升级过程在 6.5 中基本保持不变。
* 我们继续支持6.4中引入的向后兼容性、升级复杂性评估和可持续升级功能。在需要时对这些方面进行了特定于版本的更新。
* 图案检测器包装现已简化。 有一个包可评估到6.5的可用源版本。
* 有关升级过程的详细信息，请参阅 [升级文档](/help/sites-deploying/upgrade.md).

#### 项目和工作流 {#projects-and-workflows}

* 6.4中引入的新工作流模型编辑器已得到改进，可包含更多操作，如复制和发布、工作流步骤中的变量支持以及增强功能 `OR` 和 `AND` 拆分。

#### 存储库 {#repository}

* Adobe Experience Manager 6.5的基础以基于OSGi的框架（Apache Sling和Apache Felix）和Java™内容存储库的更新版本为基础构建：阿帕奇·杰克拉布特橡1.10.2。
* 有关已修复问题的概述，请参阅 [Apache Jackrabbit Oak Jira诉1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt), [Apache Jackrabbit Oak Jira诉1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) 和 [Apache Jackrabbit Oak Jira诉1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt).

>[!CAUTION]
>
>自AEM 6.3起推出的新版Oak Segment Tar需要存储库迁移。 如果要从旧版本的 TarMK 升级或想要从其他类型的持久性切换新的 Tar 区段，那么必须执行此步骤。有关新区段焦油的优势的更多信息，请参阅 [迁移到Oak区段Tar常见问题解答](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar).

#### OSGI {#osgi}

* 添加了 OSGi Promises 和 Converter 实用程序库.

#### 安全性 {#security}

* 为管理员用户添加了密码过期时间。

#### Web 服务器 {#web-server}

* 快速入门分发版使用Eclipse Jetty 9.4.15作为servlet引擎(AEM 6.4随9.3.22一起提供)。

### [!DNL Experience Manager] Sites {#experience-manager-sites}

#### 托管单页应用程序 {#managed-single-page-apps}

“页面编辑器”添加了在上下文中编辑内容以及在客户端呈现的体验中撰写/布局的功能（也称为 [SPA 编辑器](/help/sites-developing/spa-architecture.md)）。使用 JavaScript 框架 React 或 Angular 构建的现有单页应用程序可以使用 AEM SJ SDK 进行扩展，以便从业人员可对其进行编辑。

SPA 支持首先作为 AEM 6.4 SP2 的一部分发布，在 AEM 6.5 中，其增加了以下功能：

* 使用“模板编辑器”来编辑和配置 SPA 的 AEM 可编辑部分
* 使用多站点管理创建国家/地区、特许经营或白标的SPA体验

#### 无头内容管理 {#headless-content-management}

AEM可以以各种格式和堆栈的不同级别提供内容。 自 2008 年以来，有些就已经使用 [Sling GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) 和 [POST Servlet](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html)。Content Services（[Sling Model 导出程序](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=en)）在 AEM 6.3 中引入，是一种 AEM SJ SDK 用于保护单页应用程序的方法。[资产的 HTTP API](/help/assets/mac-api-assets.md) 是一个 CRUD API，已针对 AEM 6.5 进行了扩展。

新的HTTP API功能：

* 添加了 [对资产HTTP API的内容片段支持](/help/assets/assets-api-content-fragments.md) 创建、更新、读取和删除片段。
* 使用[内容片段列表核心组件](https://www.aemcomponents.dev)，通过 Content Services 显示内容片段列表。
* [核心组件库](https://www.aemcomponents.dev)，可显示每个组件的默认 Content Services JSON 输出

#### Screens 加载项 {#screens-add-on}

从交互式网亭到数字标牌，高效地设计、交付和优化所有数字显示体验。

* 通过改进内容重用，将数字和存储中的体验和内容统一起来
* 通过支持启动项简化了创作和批准/发布工作流
* 使用 SPA 编辑器编辑和提供丰富的交互式体验
* 使用启动项规划标牌内容的未来内容更改
* 序列渠道中按流量计费的播放
* 使用源文件（如Excel工作表）自动创建项目结构
* 扩展的媒体播放器支持执行强大的联机和脱机操作（智能同步），甚至可以扩展到最大的标牌网络。
* 通过使用动态占位符，按照数据触发内容的位置或配置进行个性化。
* 通过将 Adobe Analytics 集成到 AEM Screens 播放器驱动的统一分析

有关对AEM Screens所做的更改的更多详细信息 — 请参阅 [AEM Screens用户指南](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=en).

#### 组件和模板开发 {#component-amp-template-development}

* 适用于新项目的Maven项目原型18+，请参阅 [GitHub（发行说明）](https://github.com/adobe/aem-project-archetype/releases).
* 适用于新项目的单页应用程序Maven项目原型1.0.6及更高版本，请参阅 [GitHub（发行说明）](https://github.com/adobe/aem-spa-project-archetype/releases).
* HTL版本1.4，请参阅 [GitHub（发行说明）](https://github.com/adobe/htl-spec/releases/tag/1.4).

   * 字符串、数组和对象的“in”运算符：

      ```html
      ${'a' in 'abc’}
      ${100 in myArray}
      ${'a' in myObject}
      ```

   * 具有data-sly-set的变量声明：
      `<sly data-sly-set.title="${currentPage.title}"/>${title}`

   * 列出和重复控制参数：开始、步骤、结束：
      `<h2 data-sly-repeat="${currentPage.listChildren @ begin = 1, step=2}">${item.title}</h2>`

   * data-sly-unwrap的标识符：

      ```html
      <div data-sly-unwrap.isUnwrapped="${myCondition || myOtherCondition}">
      text <span data-sly-test="${isUnwrapped}>is unwrapped</code>
      </div>
      ```

   * 支持负数

* 核心组件2.3.2及更高版本，请参阅 [GitHub（发行说明）](https://github.com/adobe/aem-core-wcm-components/releases).
* 布局容器的网格系统，请参阅 [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid).
* Clientlib管理器：将Google Closure Compiler默认设置为缩小JavaScript clientlibs（旧默认值为Yahoo YUI），并将Google Closure Compiler更新为版本v20190121
* 模板编辑器和策略

   * 为使用 JS SDK（也称为 SPA 编辑器）的单页应用程序创建和编辑模板

* 参考网站We.Retail 4.0，请参阅 [GitHub（发行说明）](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases).
* 用于升级现有站点以使用最新编辑器功能的工具包，请参阅 [GitHub存储库](https://github.com/adobe/aem-modernize-tools)

>[!CAUTION]
>
>AEM包含jQuery库版本1.12.4，可最大程度地与现有自定义代码兼容。 Adobe 已对其进行了修改以解决已知的安全问题。

#### 站点管理 {#site-administration}

* [引用](/help/sites-authoring/author-environment-tools.md#references)边栏中新增了一个部分，用于列出指向所选页面的内部链接。如果计划使页面处于脱机状态或删除页面，此边栏非常有用 - 可在脱机之前查看需要调整的页面。
* 的 [列表视图](/help/sites-authoring/basic-handling.md#list-view) 新增了一个工作流列，用于显示页面处于工作流中时的状态。
* 在[页面属性](/help/sites-authoring/editing-page-properties.md)中，现在可以在为页面指定缩略图（“缩略图”选项卡）时浏览现有资产。

#### 页面编辑器 {#page-editor}

* 允许对使用JS SDK的React和Angular客户端组件(也称为SPA编辑器)构建的单页应用程序体验进行上下文内编辑和组合
* 仅当页面配置了基架页面时，才会显示基架模式。

#### 内容片段和编辑器 {#content-fragments-amp-editor}

* 新建 [批注](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations) 内容片段编辑器中的边栏，以发表常规注释并查看在文本中做出的注释（也显示在时间轴边栏中）
* 能够在 [内容片段模型](/help/assets/content-fragments/content-fragments-models.md) 转换为简单文本、富文本或标记
* 可通过选择 RTE 中的文本（全屏视图）添加[评论/注释](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* 可通过“引用”边栏并排[比较各个版本的内容片段](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions)
* 资产“下载报表”现在会相应地显示内容片段
* 可通过 /api.json 将[内容片段支持添加到资产 HTTP API](/help/assets/assets-api-content-fragments.md)。有用于创建、更新、读取和删除内容片段的API。

#### 体验片段 {#experience-fragments}

* 改进了[体验片段](/help/sites-authoring/experience-fragments.md)的索引，现在可通过搜索正在使用它们的页面查找它们的内容.
* 的 [导出到Target](/help/sites-administering/experience-fragments-target.md) 选项现在允许您以JSON格式(默认为HTML)发送体验片段，或者同时将两者发送。

#### 翻译 {#translation}

* 使用项目母版简化了翻译项目创建过程.
* 通过默认将翻译作业设置为已批准状态，简化了翻译项目执行过程.
* 允许使用第三方翻译记忆库中的更改更新翻译页面.
* 允许以 JSON 格式导出翻译作业.
* 更新Microsoft®翻译集成以使用V3 API。

#### 多站点管理 (MSM) {#multi-site-management-msm}

* 对于使用 PushOnModify 的转出配置，优化了页面移动操作的处理以避免出现不一致的状态.
* 在Live Copy结构中创建页面时，默认情况下会创建一个独立页面。
* 可在使用 JS SDK（也称为 SPA 编辑器）的单页应用程序中使用 MSM 功能

#### 启动项 {#launches}

* 新增了启动项的审核和批准工作流，可仅提升已批准的启动页面
* 向 UI 中添加了[可选择在提升步骤后立即删除启动项的选项](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)

#### 内容定位和模拟 {#content-targeting-simulation}

* 已将 ContextHub 数据层和客户端规则引擎 JavaScript 更新为默认使用 jQuery 3。

#### AEM和Adobe Target {#aem-amp-adobe-target}

>[!CAUTION]
>
>当前：
>
>* 仅 `at.js 1.x` 如果您在AEM活动控制台中使用Adobe Target作为定位引擎，则支持使用此选项。
>
>* 两者兼有 `at.js. 1.x` 和 `at.js 2.x` 如果您使用将体验片段导出到Target并在Target控制台中运行活动，则支持使用此功能。


* Adobe Target集成现在使用Target Standard API。 AEM的早期版本使用Target Classic HTTP API，该API现已弃用。
* Adobe Target `mbox.js` 包含版本63。 Adobe强烈建议您将实施切换为 `at.js` v1.x。
* `at.js` 现已包含版本1.5.0。 Adobe建议您使用 [Adobe Experience Platform Launch](https://business.adobe.com/products/experience-platform/launch.html) 准备 `at.js` v1.x。

#### AEM和Adobe Analytics {#aem-amp-adobe-analytics}

* `s_code.js` 包含H.27.5。 Adobe建议您将实施切换为 `AppMeasurement.js`
* `AppMeasurement.js` 包含v1.8.0。 Adobe建议您使用 [Adobe Experience Platform Launch](https://business.adobe.com/products/experience-platform/launch.html) 将AppMeasurement.js配置到网站中。

#### AEM and Commerce {#aem-commerce}

自AEM 6.4起，对商务集成框架的改进以更快的发行周期进行。 [在此处了解更多](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/integrations/magento.html).

#### Communities 加载项 {#communities-add-on}

要获取最新版本，请参阅 [部署社区](/help/communities/deploy-communities.md) 文档的子目录访问Advertising Cloud帮助。

##### 对社区互动的增强功能 {#enhancements-to-community-engagement}

**@Mentions支持**
AEM Communities现在允许注册用户在用户生成的内容中标记（提及）其他注册成员以引起他们的注意。 然后通知标记（提及）的成员，并在通知中包含指向相应用户生成的内容的深层链接。但是，用户可以选择禁用/启用 Web 和电子邮件通知。

![@Mentions 支持](/help/release-notes/assets/at-mentions.png)

社区用户无需搜索其名字、姓氏或用户名，即可查看是否有人联系过他们或需要他们的注意。 此外，它还允许 UGC 作者寻求能够最佳解决问题并提出意见或建议的特定注册用户的答复。

社区管理员需要 **启用提及** 在社区组件上，允许注册用户在这些组件上使用功能。

**组消息传递**

现在，已注册的社区成员可以通过单个电子邮件合成将私聊信息批量发送到组，而不是将相同的邮件分别发送给组成员。要允许[组消息传递](/help/communities/configure-messaging.md)，请启用 [Messaging Operations Service](/help/communities/messaging.md#group-messaging) 的两个实例。

![组消息](/help/release-notes/assets/group-messaging.png)

##### 批量审核增强功能 {#enhancements-to-bulk-moderation}

批量审核中的自定义过滤器

[自定义过滤器](/help/communities/moderation.md#custom-filters) 现在可以开发并添加到批量审核UI中。

A [示例项目](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) 用于演示通过标记进行过滤的 [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter). 该项目可用作开发类似自定义筛选器的基础。

![自定义筛选器](/help/release-notes/assets/custom-tag-filter.png)

**批量审核中列表视图**

在批量审核中提供了一个改进了 UI 的新列表视图，用于显示用户生成的内容条目。

![列表视图中的批量审核](/help/release-notes/assets/list-view-moderation.png)

##### 站点和组管理增强功能 {#enhancements-to-site-and-group-management}

**作者端站点和组管理员**

AEM 6.5 以后的 Communities 允许对不同的社区站点和组/嵌套组进行分散式管理。托管多个社区站点和嵌套组的组织现在可以在创建站点（和组）时在作者端选择管理员角色成员。

![站点管理员](/help/release-notes/assets/site-admin.png)

站点管理员可以在任何级别的层次结构中创建组，并成为默认管理员。这些管理员稍后可被其他组管理员删除。 组管理员可以管理其组 G1 并创建嵌套在 G1 下的子组。

##### 启用增强功能 {#enhancements-to-enablement}

**SCORM 2017.1 支持**

AEM 6.5 Communities的启用功能支持可共享内容对象引用模型 [(SCORM)2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) 引擎。

* 启用组件上的键盘导航支持
* AEM Communities中的支持组件（例如“目录”和“课程播放”、“工作总揽”、“文件库”）支持键盘导航以改进辅助功能。

##### 其他增强功能 {#other-enhancements}

* Solr 7支持
* AEM 6.5 Communities在设置MSRP和DSRP时支持Apache Solr 7.0版本的搜索平台。

### [!DNL Experience Manager Assets] {#experience-manager-assets}

AEM 6.5 引入了以下功能和增强功能，以提高 AEM 用户、DAM 角色以及相关的创意和营销角色的生产力。

#### 与集成 [!DNL Adobe Creative Cloud] 和创意工作流 {#integration-with-adobe-creative-cloud-and-creative-workflows}

[!DNL Adobe Experience Manager] 提供了多种方法来与 集成并共享资产，以供在创意、营销或业务团队密切合作的工作流中使用。[!DNL Adobe Creative Cloud][!DNL Experience Manager] 6.5 将继续改进并进一步简化该集成，以提供更多商机和简化现有方法。

请阅读并了解 [!DNL Experience Manager] 6.5，以便更好地支持内容周转率用例。

##### Adobe Asset Link {#aal}

[!DNL Adobe Asset Link] 在内容创建过程中加强创意人员和营销人员之间的协作。 创意人员可以访问 [!DNL Experience Manager Assets]，而无需离开他们最熟悉的应用程序。 创意人员可以使用 [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]和 [!DNL Adobe InDesign] 应用程序。

[!DNL Adobe Asset Link] 是 [企业Creative Cloud](https://www.adobe.com/cn/creativecloud/business/enterprise.html) 服务。 有关此功能的更多信息，包括 [!DNL Experience Manager] 部署，请参阅 [Adobe资产链接](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html).

![在Adobe Photoshop中搜索资产](/help/release-notes/assets/asset_search_photoshop.png)

##### [!DNL Adobe Stock] 集成 {#stock}

贵组织可以使用 [!DNL Adobe Stock] 企业计划 [!DNL Experience Manager Assets] 以确保许可资产广泛适用于您的创意和营销项目。 您可以快速查找、预览和许可 [!DNL Adobe Stock] Experience Manager中保存的资产，使用 [!DNL Experience Manager].

[!DNL Adobe Stock] 服务为设计师和企业提供了数百万种可用于所有创意项目的高品质、精选、免版税的照片、矢量、插图、视频、模板和 3D 资产。

有关更多信息，请参阅 [在Experience Manager Assets中使用Adobe Stock资产](/help/assets/aem-assets-adobe-stock.md).

![在Experience Manager Assets中预览Adobe Stock图像和许可证](/help/release-notes/assets/stock_image_preview_license_options.png)

*图：预览 [!DNL Adobe Stock] 从内部获取图像和许可 [!DNL Experience Manager Assets].*

![在Experience Manager中搜索和过滤授权的Adobe Stock图像](/help/release-notes/assets/aem-search-filters2.jpg)

*图：搜索和过滤已授权的 [!DNL Adobe Stock] 图像 [!DNL Experience Manager].*

##### 中的动态引用 [!DNL Adobe InDesign] {#dynamic-references-in-indesign}

[!DNL Experience Manager Assets] 在 [!DNL Adobe InDesign] 文件是动态的。 如果引用的资产在存储库中移动，则引用会自动更新。 有关更多信息，请参阅 [如何管理复合资产](/help/assets/managing-linked-subassets.md).

#### Brand Portal 功能 {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal] 可帮助您轻松获取及有效控制已批准的资产，并在设备间安全地将该资产分发给外部供应商/代理商和内部企业用户。它有助于提高资产共享的效率、加快资产的上市时间，并消除不合规使用和未授权访问的风险。

有关更多信息，请参阅 [Brand Portal的新增功能](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=zh-Hans).

#### 连接的资源 {#connectedassets}

在大型企业中，可以分发创建网站所需的基础环境。有时，网站创建功能和所需的数字资产位于不同的容器中。

[!DNL Experience Manager Sites] 提供了创建网页的功能， 是为网站提供所需资产的数字资产管理 (DAM) 系统。[!DNL Experience Manager Assets][!DNL Experience Manager] 现在通过集成支持上述用例 [!DNL Sites] 和 [!DNL Assets]. 请参阅 [如何配置和使用“连接的资产”功能](/help/assets/use-assets-across-connected-assets-instances.md).

![从 [!DNL Experience Manager] 在 [!DNL Sites] 不同页面 [!DNL Experience Manager] 部署](/help/release-notes/assets/connected-assets-drag-and-drop-only.gif)

*图：从 [!DNL Experience Manager] 在 [!DNL Sites] 页面 [!DNL Experience Manager] 部署。*

#### Dynamic Media {#dynamic-media}

[!DNL Dynamic Media] 在 [!DNL Experience Manager Assets] 提供身临其境且个性化的最前沿体验。 通过上传单个高质量主资产，并使用Adobe的高级云渲染和查看器，您可以即时交付任意演绎版组合，以支持贵组织的媒体策略。

有关新 [!DNL Dynamic Media] 功能，请参阅 [Dynamic Media发行说明](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/release-notes/s7rn2017.html).

##### 360视频支持 {#video-support}

直接在 [!DNL Experience Manager] 使用最先进的查看器向台式机、移动设备和VR耳机提供VR体验。 有关更多信息，请参阅 [使用360视频](/help/assets/360-video.md).

##### 自定义视频缩略图 {#custom-video-thumbnails}

您现在可以使用视频本身的帧或存储在 DAM 中的其他内容自定义视频资产的缩略图。有关其他说明，请参阅 [关于视频缩略图](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

##### 辅助功能增强功能 {#accessibility-enhancements}

[!DNL Dynamic Media] 查看器现在支持增强的辅助功能，如Aria支持、屏幕阅读器和替代文本。 有关更多详细信息，请参阅 [查看器参考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/homeviewers.html).

#### 搜索体验增强功能 {#experience-enhancement-for-searching}

[!DNL Experience Manager] 从6.5开始，营销人员可以更快地从搜索结果页面发现所需的资产。 即使还未应用搜索筛选器，也会为搜索 Facet 更新资产数量。查看筛选后的预计计数有助于用户有效地浏览搜索结果。有关更多信息，请参阅 [在Experience Manager中搜索资产](/help/assets/search-assets.md).

![在搜索 Facet 中查看未筛选搜索结果时的资产数量](/help/assets/assets/asset_search_results_in_facets_filters.png)

*图：在搜索彩块化中查看未筛选搜索结果的资产数量。*

#### 可用性增强功能 {#usability-enhancement}

您现在可以一次从文件夹或搜索结果中选择所有加载的资产。 该功能可以帮助您快速管理多个资产。此复选框会选择适合方案（如搜索结果）的所有资产，而不只是选择 [!DNL Experience Manager] 界面。

![使用全选选项，一键选择所有加载的资产。](/help/release-notes/assets/select-all-in-aem-assets.gif)

*图：使用全选选项，一键选择所有加载的资产。*

#### 元数据增强功能 {#metadata-enhancements}

[!DNL Assets] 允许您为资产文件夹创建元数据架构，该架构定义文件夹属性页面中显示的布局和元数据。 现在，您可以将文件夹元数据架构分配给现有文件夹，或在创建文件夹时。 有关更多信息，请参阅[文件夹元数据架构](/help/assets/metadata-config.md#folder-metadata-schema)。

指定级联元数据时，可以在运行时从 JSON 文件加载选项，而不是在表单中手动键入选项。有关更多信息，请参阅 [级联元数据](/help/assets/metadata-schemas.md#cascading-metadata).

#### 报告增强功能 {#reporting-enhancements}

内容片段和链接共享现在包含在下载的报表中。 有关更多信息，请参阅 [Assets 报表](/help/assets/asset-reports.md)。

### [!DNL Adobe Experience Manager Forms] {#experience-manager-forms}

AEM 6.5 Forms引入了一些新增功能和增强功能。 主要功能包括：

* 事务报告，用于跟踪所提交表单、已处理文档和已呈现文档的数量
* 交互式通信的可用性改进
* 自适应表单中基于云的数字签名
* 在AEM Sites单页应用程序(SPA)中嵌入自适应表单和交互式通信。
* 支持 AEM 工作流中的变量
* 交互式通信中的数据显示模式支持
* 对自适应表单和交互式通信表格进行排序
* 自动验证表单数据模型中的输入数据

请参阅 [AEM 6.5 Forms中的新增功能和增强功能摘要](/help/forms/using/whats-new.md) 有关新增和改进功能及文档资源的信息。

### [!DNL Experience Manager Livefyre] {#experience-manager-livefyre}

您可以将 Livefyre 与 AEM 6.5 实例集成。请参阅 [如何将Livefyre与AEM集成](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/livefyre.html).

### 使用以客户为中心的开发 {#leverage-customer-focused-development}

Adobe使用以客户为中心的开发模型，该模型允许客户在规范、开发和测试期间对开发过程的所有阶段做出贡献。 在此过程中，我们感谢所有有贡献的客户和合作伙伴。

Adobe已制定相应的程序和流程，以便收集、确定以客户为中心的错误解决和增强请求开发的优先级并跟踪这些错误。 的 [Experience Manager支持门户](https://experienceleague.adobe.com/?support-solution=Experience+Manager#support) 与Adobe增强和缺陷跟踪系统集成。 客户问题由客户支持团队在可能的情况下识别并解决。 升级到 R&amp;D 时，将捕获所有客户信息，并将这些信息用于确定优先级和报告。在开发过程中，优先考虑付费支持、被担保人问题和客户付费增强功能。

这一确定优先级的流程已经产生了 750 多个以客户为中心的更改，并已在 AEM 6.5 中进行了修复。

## 作为发布一部分的文件列表 {#list-of-files-that-are-part-of-the-release}

**Foundation**

* 独立快速入门： `cq-quickstart-6.5.0.jar`.
* 应用程序服务器快速启动： `cq-quickstart-6.5.0.war`.
* 适用于各种Web服务器和平台的Dispatcher 4.3.2或更高版本。 请参阅 [下载链接](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html)
* 用于 Eclipse IDE 的插件（[了解更多并下载](/help/sites-developing/aem-eclipse.md)）

* 用于 Brackets 代码编辑器的扩展（[了解更多并下载](/help/sites-developing/aem-brackets.md)）
* Maven/Gradle 依赖（[下载链接](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.0/)）

**Sites**

* 核心组件（[GitHub 项目](https://github.com/adobe/aem-core-wcm-components)）
* We.Retail 参考实施（[了解更多](/help/sites-developing/we-retail.md)）
* Maven 项目原型：

   * 对于全堆栈站点：[GitHub 项目](https://github.com/adobe/aem-project-archetype)
   * 对于使用 React/Angular 的单页应用程序：[GitHub 项目](https://github.com/adobe/aem-spa-project-archetype)

* 适用于各种不同平台的 AEM Screens 播放器（[下载](https://download.macromedia.com/screens/)）

* 智能内容语言模型。预装英语 — 可下载更多语言

   * [德语](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [西班牙语](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [意大利语](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [法语](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)

* AEM现代化工具套件，例如对话框转换工具。 （[GitHub 项目](https://github.com/adobe/aem-modernize-tools)）

**Assets**

* 用于添加增强型 PDF 栅格化程序的软件包（[了解更多](/help/assets/aem-pdf-rasterizer.md)）
* 用于添加扩展 RAW 图像支持的软件包（[了解更多](/help/assets/camera-raw.md)）

**Forms**

* [用于 AEM Forms 功能的软件包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [AEM Forms OSGi客户端SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/)

## 语言 {#languages}

用户界面提供了下列语言版本：

* 英语
* 德语
* 法语
* 西班牙语
* 意大利语
* 巴西葡萄牙语
* 日语
* 简体中文
* 繁体中文（有限支持）
* 韩语

[!DNL Experience Manager] 6.5 已通过 GB18030-2005 CITS 认证，可使用中文编码标准。

## 安装和更新 {#install-update}

有关设置要求，请参阅 [安装说明](/help/sites-deploying/custom-standalone-install.md).

有关详细说明，请参阅 [升级文档](/help/sites-deploying/upgrade.md).

## 支持的平台 {#supported-platforms}

查找支持的平台的完整矩阵，包括 [AEM 6.5技术要求](/help/sites-deploying/technical-requirements.md).

>[!NOTE]
>
>Oracle已转为使用OracleJava™ SE产品的长期支持(LTS)模型。 Java™ 9和10是按Oracle列出的非LTS版本。请参阅 [OracleJava™ SE支持路线图](https://www.oracle.com/technetwork/java/eol-135779.html). Adobe支持LTS版本的Java™，以便仅在生产中运行AEM。 要与AEM 6.5一起使用，建议使用Java™ 11版本。

## 已弃用和已删除的功能 {#deprecated-and-removed-features}

Adobe会不断评估产品中的功能，并且随着时间的推移，计划使用更强大的版本替换这些功能，或者决定重新实施选定的部件，以便更好地满足未来的期望或扩展。

对于 [!DNL Adobe Experience Manager] 6.5, [阅读已弃用和已删除功能的列表](/help/release-notes/deprecated-removed-features.md). 该页面还包含未来即将发生的更改的预告，以及从以前版本更新的客户的重要通知。

## 已知问题 {#known-issues}

### 平台 {#platform}

* 报告了删除CRX快速入门及其内容的问题。

   在每个操作中，确保 `htmllibmanager.fileSystemOutputCacheLocation` 不是空字符串：

   1. 正在调用 `/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`.
   2. 升级到AEM 6.5。
   3. 在AEM 6.5中执行“延迟内容迁移”。

   A [知识库](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) 有关此问题的更多详细信息和解决方法，请参阅文章。

* 如果您正在将JDK 11与AEM 6.5实例一起使用，则在部署某些包后，某些页面可能会显示为空白。 日志文件中显示以下错误消息：

   ```java
   *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
   java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
   ```

要解决此错误，请执行以下操作：

1. 停止AEM实例。 转到 `<aem_server_path_on_server>crx-quickstart\conf` 打开 `sling.properties` 文件。 Adobe建议备份此文件。

1. 搜索 `org.osgi.framework.bootdelegation=`. 添加 `jdk.internal.reflect,jdk.internal.reflect.*` 属性来将结果显示为。

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. 保存文件并重新启动AEM实例。

### Sites {#sites}

* **使用页面版本**: [如果页面已移动，则无法再对移动前创建的任何版本执行预览](/help/sites-authoring/working-with-page-versions.md#previewing-a-version).

### Assets {#assets}

* **搜索：** 如果搜索字符串包含前导空格([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **文件夹元数据架构**：添加选择按钮后，ID 和值字段未按预期呈现，且删除功能不起作用。(CQ-4261144)
* 重命名资产时，无法在资产名称中使用空格。(CQ-4266403)

### Forms {#forms}

* 在Linux®操作系统上安装AEM Forms后，带硬件安全模块的数字签名不起作用。 (CQ-4266721)
* (仅限WebSphere上的AEM Forms®) **Forms Workflow** > **任务搜索** 如果您搜索 **管理员** with **用户名** 作为搜索标准。 (CQ-4266457)

* AEM Forms无法将具有JPEG压缩的TIF和TIFF文件转换为PDF文档。 (CQ-4265972)
* **AEM Forms 迁移**&#x200B;页面上的 **AEM Forms 资产扫描程序**&#x200B;和&#x200B;**交互式通信迁移字符**&#x200B;选项不起作用。(CQ-4266572)

* (仅限JBoss® 7)当您从以前的版本升级到AEM 6.5 Forms，并且以前的版本具有创建和使用默认提交或默认呈现过程副本的进程(.lca)时，使用此类进程(.lca)的HTML5 Forms无法执行所需的操作。 (CQ-4243928)
* 在自适应表单中，当从规则编辑器调用表单数据模型服务以动态更新图像选项组件的值时，不会更新图像选项组件的值。(CQ-4254754)
* AEM Forms Designer安装程序需要32位版本的 [Visual C++可再发行运行时包2012](https://docs.microsoft.com/en-US/cpp/windows/latest-supported-vc-redist?view=msvc-170) 和 [Visual C++可再发行运行时包2013](https://support.microsoft.com/en-us/topic/update-for-visual-c-2013-and-visual-c-redistributable-package-5b2ac5ab-4139-8acc-08e2-9578ec9b2cf1). 在开始安装之前，请确保已安装之前提到的可再发行运行时包。 (CQ-4265668)

* PDF生成器不支持基于智能卡的身份验证。 当管理员启用组策略时 `Interactive Logon: Require Smart card` 在Windows服务器上，所有现有PDF生成器用户都将失效。

* 当自适应表单配置为动态更新组件的值并通过Dispatcher访问托管表单的发布实例时，动态更新字段值的功能将停止工作。 要解决此问题，请在发布实例上打开CRXDE，导航到 `/libs/fd/af/runtime/clientlibs/guideChartReducer`，然后创建下面列出的资产。

   * 名称：allowProxy
   * 类型：布尔型
   * 值：true
   * 受保护：False
   * 必填：False
   * 多选：False
   * 自动创建：False

   该属性让运行时文件夹下的客户端库可以访问代理。(CQ-4268679)

* 启动AEM Forms时， `SAX Security Manager could not be setup` 出现警告。
* 在运行Adobe Acrobat Reader版本20.10.00的Apple iOS或iPadOS上打开受AEM Forms Document Security保护的PDF时
* 在从 Apple iOS 设备提交包含标准 HTML 上传字段的表单时，有时不会发送文件内容，而在另一端会收到一个 0 字节的文件。Apple iOS 15.1 修复了此问题。

## 产品下载和支持（受限网站） {#product-download-and-support-restricted-sites}

以下网站仅供客户使用。 如果您是客户并且需要访问，请联系您的 Adobe 客户经理。

* [产品下载：licensing.adobe.com](https://licensing.adobe.com/).

* 产品更新、修补程序和软件包，以获取 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).

* [通过Admin Console提供客户支持](https://adminconsole.adobe.com/). 有关更多信息，请参阅 [新的Adobe客户支持体验](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en).
