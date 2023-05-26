---
title: 内容属性和节点
seo-title: Content Properties and Nodes
description: 按照此页面了解内容属性和节点。
seo-description: Follow this page to learn about content properties and nodes.
uuid: 2dad52c8-5b6c-4b90-8498-62217a9a27fc
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: f5721ddc-df5c-496c-be61-38d1cab63ad4
exl-id: 05c8c846-69cc-4075-9149-33890b3d1e08
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 21%

---

# 内容属性和节点 {#content-properties-and-nodes}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md).

在AEM中，文章、横幅和收藏集表示为cq：Pages。

除了下面显示的几个其他属性之外，它们还共享在任何cq：Page中找到的相同常用属性，这些属性表示Adobe Experience Manager (AEM) Mobile On-Demand Services元数据和支持属性的集成。

下表描述了内容属性和节点。

## 常见集成属性 {#common-integration-properties}

| **属性名称** | **类型** | **默认值或预期值** | **描述** |
|---|---|---|---|
| dps-id | 字符串 |  | 上传至AEM Mobile或从AEM Mobile导入后，由AEM Mobile分配并由AEM存储 |
| dps-resourceType | 字符串 | dps:Article | dps:Banner | dps:Collection | 实体类型属性 |
| dps-version | 字符串 |  | AEM Mobile实体的版本（也包含在完整aemm-id中） |
| dps-lastSynced | 日期 |  | 上次从AEM Mobile同步/导入AEM的日期 |
| dps-lastUploaded | 日期 |  | 上次从AEM上传到AEM Mobile的日期 |
| dps-lastUploadedBy | String：userid |  | 执行了从AEM到AEM Mobile的上次上传请求的id用户 |

## 核心元数据属性 {#core-metadata-properties}

| 属性名称 | 类型 | 默认值或预期值 |
|--- |--- |--- |
| dps-title | 字符串 |  |
| dps-shortTitle | 字符串 |  |
| dps-abstract | 字符串 |  |
| dps-shortAbstract | 字符串 |  |
| dps-department | 字符串 |  |
| dps-category | 字符串 |  |
| dps-keywords | 字符串[] |  |
| dps-internalKeywords | 字符串[] |  |
| dps-importance | 字符串[] | 重要性来自{“低”、“正常”、“高”} |

### 文章 {#articles}

| **属性名称** | **类型** | **默认值或预期值** |
|---|---|---|
| dps-author | 字符串 |  |
| dps-authorURL | 字符串 |  |
| dps-hideFromBrowsePage | 布尔值 |  |
| dps-access | 字符串 | 来自{&quot;protected&quot;、&quot;metered&quot;、&quot;free&quot;}的ProtectedAccess |
| **Social** |  |  |
| dps-socialShareURL | 字符串 |  |
| dps-articleText | 字符串 |  |
| dps-url | 字符串 |  |

### 横幅 {#banners}

| **属性名称** | **类型** | **默认值或预期值** |
|---|---|---|
| dps-tapAction |  | 来自{webLink}的TapAction |
| dps-tapActionUrl |  |  |

### 收藏集 {#collections}

| 属性名称 | 类型 | 默认值或预期值 |
|--- |--- |--- |
| dps-productId | 字符串 |  |
| dps-readingPosition | 字符串 | 从{&quot;reset&quot;，&quot;retain&quot;} |
| dps-horizontalSwipe | 布尔值 |  |
| dps-allowDownload | 布尔值 |  |
| dps-openDefault | 字符串 | 从{&quot;browsePage&quot;，&quot;contentView&quot;} |
| dps-layout | 字符串 |  |

## 内容节点 {#content-nodes}

### 公共节点 {#common-nodes}

| 节点名称 | 类型 | 默认值或预期值 | 描述 |
|--- |--- |--- |--- |
| 图像 | jcr：primaryType=nt：unstructured <br> sling：resourceType=foundation/components/image |  |  |

### 实体 {#entities}

#### 文章 {#articles-1}

| 节点名称 | 类型 | 预期值的默认值 | 描述 |
|--- |--- |--- |--- |
| social-share-image |  | jcr：primaryType=nt：unstructured <br> sling：resourceType=foundation/components/image |  |

#### 横幅 {#banners-1}

| 节点名称 | 类型 | 预期值的默认值 | 描述 |
|---|---|---|---|
| NA |  |  |  |

#### 收藏集 {#collections-1}

| 节点名称 | 类型 | 预期值的默认值 | 描述 |
|--- |--- |--- |--- |
| background-image | jcr：primaryType=nt：unstructured <br> sling：resourceType=foundation/components/image |  |  |
