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
source-git-commit: 9a4ae73c08657195da2741cccdb196bd7f7142c9
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 4%

---


# Search Essentials {#search-essentials}

## 概述 {#overview}

搜索功能是AEM Communities的一个基本特征。 除了[AEM平台搜索](../../help/sites-deploying/queries-and-indexing.md)功能外，AEM Communities还提供[UGC搜索API](#ugc-search-api)以搜索用户生成的内容(UGC)。 UGC具有唯一属性，因为输入该属性时，它会与其他AEM内容和用户数据分开存储。

对于Communities，通常搜索的两件事情是：

* 社区成员发布的内容

   * 使用AEM Communities的UGC搜索API。

* 用户和用户组（用户数据）

   * 使用AEM平台搜索功能。

文档的本节内容对创建创建或管理UGC的自定义组件的开发人员很有兴趣。

## 安全和阴影节点{#security-and-shadow-nodes}

对于自定义组件，必须使用[SocialResourceUtilities](socialutils.md#socialresourceutilities-package)方法。 创建和搜索UGC的实用程序方法将建立所需的[阴影节点](srp.md#about-shadow-nodes-in-jcr)，并确保成员对请求具有正确的权限。

未通过SRP实用程序管理的是与仲裁相关的属性。

有关用于访问UGC和ACL阴影节点的实用程序方法的信息，请参见[ SRP和UGC Essentials](srp-and-ugc.md)。

## UGC搜索API {#ugc-search-api}

[UGC公用存储区](working-with-srp.md)由各种存储资源提供者(SRP)之一提供，每个提供者可能具有不同的本机查询语言。 因此，无论选择何种SRP，自定义代码都应使用[UGC API包](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html)(*com.adobe.cq.social.ugc.api*)中的方法，这些方法将调用适用于所选SRP的查询语言。

### ASRP搜索{#asrp-searches}

对于[ASRP](asrp.md),UGC存储在Adobe云中。 虽然UGC在CRX中不可见，但[仲裁](moderate-ugc.md)在作者和发布环境中均可用。 使用[UGC搜索API](#ugc-search-api)对ASRP的作用与对其他SRP的作用相同。

目前不存在用于管理ASRP搜索的工具。

创建可搜索的自定义属性时，必须符合[命名要求](#naming-of-custom-properties)。

### MSRP搜索{#msrp-searches}

对于[MSRP](msrp.md),UGC存储在配置为使用Solr进行搜索的MongoDB中。 UGC在CRX中不可见，但[仲裁](moderate-ugc.md)在作者和发布环境中均可用。

关于MSRP和Solr:

* AEM平台的嵌入式Solr不用于MSRP。
* 如果将远程Solr用于AEM平台，则可以与MSRP共享它，但它们应使用不同的集合。
* Solr可配置为标准搜索或多语言搜索(MLS)。
* 有关配置详细信息，请参阅MSRP的[Solr Configuration](msrp.md#solr-configuration)。

自定义搜索功能应使用[UGC搜索API](#ugc-search-api)。

创建可搜索的自定义属性时，必须符合[命名要求](#naming-of-custom-properties)。

### JSRP搜索{#jsrp-searches}

对于[JSRP](jsrp.md),UGC存储在[Oak](../../help/sites-deploying/platform.md)中，并且仅在输入它的AEM作者或发布实例的存储库中可见。

由于UGC通常在发布环境中输入，对于多发布者生产系统，必须配置[发布群集](topologies.md)，而不是发布场，这样输入的内容就可以从所有发布者中看到。

对于JSRP，在发布环境中输入的UGC在创作环境中将不可见。 因此，所有[协调](moderate-ugc.md)任务都发生在发布环境中。

自定义搜索功能应使用[UGC搜索API](#ugc-search-api)。

#### Oak索引{#oak-indexing}

虽然Oak索引不是为AEM平台搜索自动创建的，但从AEM 6.2开始，它们已经为AEM Communities添加，以提高性能，并在呈现UGC搜索结果时提供分页支持。

如果自定义属性正在使用，且搜索速度慢，则需要为自定义属性创建其他索引，以提高其性能。 要保持可移植性，在创建可搜索的自定义属性时，请遵循[命名要求](#naming-of-custom-properties)。

要修改现有索引或创建自定义索引，请参阅[Oak查询和索引](../../help/sites-deploying/queries-and-indexing.md)。

[Oak索引管理器](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html)可从ACS AEM Commons获取。 它提供：

* 现有索引的视图。
* 启动重新索引的能力。

要视图[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)中的现有Oak索引，位置为：

* `/oak:index/socialLucene`

![社交露西](assets/social-lucene.png)

## 索引搜索属性{#indexed-search-properties}

### 默认搜索属性{#default-search-properties}

以下是用于各种社区功能的一些可搜索属性：

| **属性** | **数据类型** |
|---|---|
| isFlaged | *布尔型* |
| isSpam | *布尔型* |
| 读 | *布尔型* |
| 影响 | *布尔型* |
| 附件 | *布尔型* |
| 情感 | *长整型* |
| 已标记 | *布尔型* |
| 已添加 | *日期* |
| modifiedDate | *日期* |
| 状态 | *String* |
| userIdentifier | *字符串* |
| 回复 | *长整型* |
| jcr:title | *字符串* |
| jcr:description | *字符串* |
| sling:resourceType | *字符串* |
| allowThreadedReply | *布尔型* |
| isDraft | *布尔型* |
| publishDate | *日期* |
| publishJobId | *字符串* |
| 已回复 | *布尔型* |
| 乔森纳 | *布尔型* |
| 标签 | *字符串* |
| cq：标记 | *字符串* |
| author_display_name | *字符串* |
| location_t | *字符串* |
| parentPath | *字符串* |
| parentTitle | *字符串* |

### 自定义属性的命名{#naming-of-custom-properties}

添加自定义属性时，为了使这些属性对使用[UGC搜索API](#ugc-search-api)创建的排序和搜索可见，必须&#x200B;*为属性名称添加后缀。*

后缀是使用查询语的模式语：

* 它将属性标识为可搜索。
* 它标识数据类型。

Solr是使用查询语的模式语的示例。

| **后缀** | **数据类型** |
|---|---|
| _b | *布尔型* |
| _dt | *日历* |
| _d | *双精度型* |
| _tl | *长整型* |
| _s | *字符串* |
| _t | *文本* |

**注释:**

* ** 文本是标记字符串， ** 字符串不是。使用&#x200B;*文本*&#x200B;进行模糊搜索（更类似于此）。

* 对于多值类型，请在后缀中添加“s”，例如：

   * `viewDate_dt`:单日期属性
   * `viewDates_dts`:列表日期属性

## 筛选器 {#filters}

包含[注释系统](essentials-comments.md)的组件支持将过滤器参数添加到其端点。

AND和OR逻辑的过滤器语法如下所示（在进行URL编码前显示）:

* 要指定OR，请使用一个以逗号分隔的值的筛选器参数：

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* 要指定AND，请使用多个筛选器参数：

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

[搜索组件](search.md)的默认实现使用此语法，如[社区组件指南](components-guide.md)中打开搜索结果页的URL中所示。 要进行试验，请浏览至[http://localhost:4503/content/community-components/en/search.html](http://localhost:4503/content/community-components/en/search.html)。

过滤器运算符有：

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
* 不正确：论坛页面
   * `/content/community-components/en/forum.social.json`

## SRP工具{#srp-tools}

有一个Adobe Marketing CloudGitHub项目，其中包含：

[AEM CommunitiesSRP工具](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

此存储库包含用于管理SRP中数据的工具。

目前，有一个servlet提供从任何SRP删除所有UGC的功能。

例如，要删除ASRP中的所有UGC:

```shell
curl -X POST http://localhost:4502/services/social/srp/cleanup?path=/content/usergenerated/asi/cloud -uadmin:admin
```

## 疑难解答 {#troubleshooting}

### Solr查询{#solr-query}

要帮助解决Solr查询的问题，请启用

`com.adobe.cq.social.srp.impl.SocialSolrConnector`。

实际的Solr查询将显示在调试日志中编码的URL:

查询至solr是：`sort=timestamp+desc&bl=en&pl=en&start=0&rows=10 &q=%2Btitle_t:(hello)+%2Bprovider_id:\/content/usergenerated/asi/mongo/content/+%2Bresource_type_s:&df=provider_id&trf=verbatim&fq={!cost%3D100}report_suite:mongo`

`q`参数的值是查询。 解码URL编码后，查询可以传递到Solr Admin查询工具以进一步调试。

## 相关资源 {#related-resources}

* [社区内容存储](working-with-srp.md) -讨论UGC公用商店的可用SRP选项。
* [存储资源提供者概述](srp.md) -简介和存储库使用概述。
* [使用SRP编码准则](accessing-ugc-with-srp.md) 访问UGC。
* [SocialUtils重构](socialutils.md) -替换SocialUtils的SRP的实用程序方法。
* [搜索和搜索结果组件](search.md) -将UGC搜索功能添加到模板。

