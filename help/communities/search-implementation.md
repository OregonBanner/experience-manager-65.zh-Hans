---
title: Search Essentials
seo-title: Search Essentials
description: 在社区中搜索
seo-description: 在社区中搜索
uuid: 5f35a033-2069-499e-9cdb-db25781312f0
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 300aa9f3-596f-42bc-8d46-e535f2bc4379
translation-type: tm+mt
source-git-commit: 6d425dcec4fab19243be9acb41c25b531a84ea74

---


# Search Essentials {#search-essentials}

## 概述 {#overview}

搜索功能是AEM Communities的一个基本功能。 除了 [AEM平台搜索功能外](../../help/sites-deploying/queries-and-indexing.md) ,AEM Communities还提供 [UGC搜索API](#ugc-search-api) ，用于搜索用户生成的内容(UGC)。 UGC具有唯一属性，因为输入该属性后，该属性会与其他AEM内容和用户数据分开存储。

对于“社区”，通常搜索的两件事是：

* 社区成员发布的内容

   * 使用AEM Communities的UGC搜索API。

* 用户和用户组（用户数据）

   * 使用AEM平台搜索功能。

文档的本节内容对创建创建或管理UGC的自定义组件的开发人员很有兴趣。

## 安全性和阴影节点 {#security-and-shadow-nodes}

对于自定义组件，必须使用 [SocialResourceUtilities方法](socialutils.md#socialresourceutilities-package) 。 创建和搜索UGC的实用程序方法将建立所需的 [阴影节点](srp.md#about-shadow-nodes-in-jcr) ，并确保成员对请求具有正确的权限。

未通过SRP实用程序管理的是与仲裁相关的属性。

有关 [用于访问UGC和ACL阴影节点的实用程序方法的信息，请参阅SRP和UGC Essentials](srp-and-ugc.md) 。

## UGC搜索API {#ugc-search-api}

该 [UGC公共存储由多种存储资源提供者](working-with-srp.md) (SRP)之一提供，每个SRP可能具有不同的本机查询语言。 因此，无论选择何种SRP，自定义代码都应使用 [UGC API包](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) (*com.adobe.cq.social.ugc.api*)中的方法，该方法将调用适用于所选SRP的查询语言。

### ASRP搜索 {#asrp-searches}

对于 [ASRP](asrp.md),UGC存储在Adobe云中。 虽然UGC在CRX中不可见，但 [审核功能](moderate-ugc.md) 从创作和发布环境中均可用。 使用 [UGC搜索API](#ugc-search-api) 与使用其他SRP一样适用于ASRP。

目前不存在用于管理ASRP搜索的工具。

创建可搜索的自定义属性时，必须符合命名 [要求](#naming-of-custom-properties)。

### MSRP搜索 {#msrp-searches}

对 [于MSRP](msrp.md),UGC存储在配置为使用Solr进行搜索的MongoDB中。 UGC在CRX中不可见，但 [仲裁](moderate-ugc.md) 可从作者和发布环境中获取。

关于MSRP和Solr:

* AEM平台的嵌入式Solr不用于MSRP。
* 如果将远程Solr用于AEM平台，则可能会与MSRP共享它，但它们应使用不同的集合。
* Solr可配置为标准搜索或多语言搜索(MLS)。
* 有关配置详细信息，请参 [阅MSRP的Solr配置](msrp.md#solr-configuration) 。

自定义搜索功能应使 [用UGC搜索API](#ugc-search-api)。

创建可搜索的自定义属性时，必须符合命名 [要求](#naming-of-custom-properties)。

### JSRP搜索 {#jsrp-searches}

对 [于JSRP](jsrp.md),UGC存储在 [](../../help/sites-deploying/platform.md) Oak中，并且仅在输入AEM作者或发布实例的存储库中可见。

由于UGC通常在发布环境中输入，对于多发布者生产系统，必须配置发布群集 [](topologies.md)，而不是发布群集，这样输入的内容在所有发布者中都可见。

对于JSRP，在发布环境中输入的UGC在创作环境中永远不可见。 因此，所 [有协调任务](moderate-ugc.md) 都会在发布环境中进行。

自定义搜索功能应使 [用UGC搜索API](#ugc-search-api)。

#### Oak索引 {#oak-indexing}

虽然Oak索引不会自动为AEM平台搜索创建，但从AEM 6.2开始，已为AEM Communities添加这些索引，以在呈现UGC搜索结果时提高性能并提供分页支持。

如果自定义属性正在使用，且搜索速度较慢，则需要为自定义属性创建其他索引，以提高其性能。 要保持可移植性，请在创建可搜索 [的自定义属性](#naming-of-custom-properties) 时遵循命名要求。

要修改现有索引或创建自定义索引，请参阅 [Oak查询和索引](../../help/sites-deploying/queries-and-indexing.md)。

Oak Index Manager [](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html) ，可从ACS AEM Commons获得。 它提供：

* 现有索引的视图。
* 启动重新索引的能力。

要视图 [CRXDE Lite中的现有Oak索引](../../help/sites-developing/developing-with-crxde-lite.md)，位置为：

* `/oak:index/socialLucene`

![chlimage_1-235](assets/chlimage_1-235.png)

## 索引搜索属性 {#indexed-search-properties}

### 默认搜索属性 {#default-search-properties}

以下是用于各种Communities功能的一些可搜索属性：

| **属性** | **数据类型** |
|---|---|
| isFlaged | *布尔型* |
| isSpam | *布尔型* |
| 阅读 | *布尔型* |
| 影响 | *布尔型* |
| 附件 | *布尔型* |
| 情感 | *长整型* |
| 已标记 | *布尔型* |
| 已添加 | *日期* |
| modifiedDate | *日期* |
| 状态 | *String* |
| userIdentifier | *String* |
| 回复 | *长整型* |
| jcr:title | *String* |
| jcr:description | *String* |
| sling:resourceType | *String* |
| allowThreadedReply | *布尔型* |
| isDraft | *布尔型* |
| publishDate | *日期* |
| publishJobId | *String* |
| 已回复 | *布尔型* |
| 选择已回答 | *布尔型* |
| 标签 | *String* |
| cq：标记 | *String* |
| author_display_name | *String* |
| location_t | *String* |
| parentPath | *String* |
| parentTitle | *String* |

### 自定义属性的命名 {#naming-of-custom-properties}

添加自定义属性时，为了使这些属性对使用 [UGC搜索API创建的排序和搜索可见](#ugc-search-api)，必须 ** 为属性名添加后缀。

后缀是使用查询的模式语：

* 它将属性标识为可搜索。
* 它标识数据类型。

Solr是使用查询语的模式语的示例。

| **后缀** | **数据类型** |
|---|---|
| _b | *布尔型* |
| _dt | *日历* |
| _d | *双精度型* |
| _tl | *长整型* |
| _s | *String* |
| _t | *文本* |

**注释:**

* *Text* 是标记字符串， *String* 不是。 使用 *文本* （更像这样）进行模糊搜索。

* 对于多值类型，请向后缀添加“s”，例如：

   * `viewDate_dt`:单日期属性
   * `viewDates_dts`:列表日期属性

## 筛选器 {#filters}

包括注释系统的组 [件支持在](essentials-comments.md) 其端点之外添加过滤器参数。

AND和OR逻辑的过滤器语法如下所示（在对URL进行编码之前显示）:

* 要指定OR，请使用一个以逗号分隔的值的筛选器参数：

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* 要指定AND，请使用多个过滤器参数：

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

搜索组件的默认实 [施使用此语法](search.md) ，如在“社区组件”指南中打开“搜索结果”页面的URL中所 [示](components-guide.md)。 要进行试验，请浏览 [http://localhost:4503/content/community-components/en/search.html](http://localhost:4503/content/community-components/en/search.html)。

过滤器操作符有：

| EQ | 等于 |
|---|---|
| NE | 等于 |
| LT | 小于 |
| LTE | 小于或等于 |
| GE | 大于 |
| GTE | 大于或等于 |
| LIKE | 模糊匹配 |

URL引用社区组件（资源），而不是放置组件的页面，这一点很重要：

* 正确：论坛组件
   * `/content/community-components/en/forum/jcr:content/content/forum.social.json`
* 错误：论坛页面
   * `/content/community-components/en/forum.social.json`

## SRP工具 {#srp-tools}

有一个Adobe Marketing Cloud GitHub项目，其中包含：

[AEM Communities SRP工具](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

此存储库包含用于管理SRP中数据的工具。

目前，有一个Servlet，它提供从任何SRP中删除所有UGC的功能。

例如，要删除ASRP中的所有UGC，请执行以下操作：

```shell
curl -X POST http://localhost:4502/services/social/srp/cleanup?path=/content/usergenerated/asi/cloud -uadmin:admin
```

## 疑难解答 {#troubleshooting}

### 索尔查询 {#solr-query}

要帮助解决Solr查询的问题，请为

`com.adobe.cq.social.srp.impl.SocialSolrConnector`。

实际的Solr查询将显示调试日志中编码的URL:

查询是： `sort=timestamp+desc&bl=en&pl=en&start=0&rows=10 &q=%2Btitle_t:(hello)+%2Bprovider_id:\/content/usergenerated/asi/mongo/content/+%2Bresource_type_s:&df=provider_id&trf=verbatim&fq={!cost%3D100}report_suite:mongo`

参数的值 `q` 是查询。 解码URL编码后，该查询可以传递到Solr Admin查询工具以进一步调试。

## 相关资源 {#related-resources}

* [社区内容存储](working-with-srp.md) -讨论UGC公用商店的可用SRP选项。
* [存储资源提供者概述](srp.md) -简介和存储库使用概述。
* [使用SRP](accessing-ugc-with-srp.md) —— 编码准则访问UGC。
* [SocialUtils重构](socialutils.md) -用于替换SocialUtils的SRP的实用程序方法。
* [搜索和搜索结果组件](search.md) -将UGC搜索功能添加到模板。

