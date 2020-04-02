---
title: 内容属性和节点
seo-title: 内容属性和节点
description: 可查看本页以了解内容属性和节点。
seo-description: 可查看本页以了解内容属性和节点。
uuid: 2dad52c8-5b6c-4b90-8498-62217a9a27fc
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: f5721ddc-df5c-496c-be61-38d1cab63ad4
translation-type: tm+mt
source-git-commit: 50c0bdfc3203410d392e53536bc7cd00245406e5

---


# 内容属性和节点 {#content-properties-and-nodes}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

文章、横幅和集合在AEM中表示为cq:Pages。

除了下面显示的代表Adobe Experience Manager(AEM)Mobile On-Demand Services元数据和集成支持属性的其他几个属性外，这些属性还共享任何cq:Page中的相同公用属性。

下表描述了内容属性和节点。

## 常见集成属性 {#common-integration-properties}

| **属性名称** | **类型** | **默认值或预期值** | **描述** |
|---|---|---|---|
| dps-id | 字符串 |  | AEM Mobile分配的AEM，在上传到AEM Mobile或从AEM Mobile导入后由AEM存储 |
| dps-resourceType | 字符串 | dps:Article | dps:Banner | dps:Collection | 实体类型属性 |
| dps-version | 字符串 |  | AEM Mobile实体的版本（也包含在完整的aemm-id中） |
| dps-lastSynced | 日期 |  | 上次同步／从AEM Mobile导入AEM的日期 |
| dps-lastUploaded | 日期 |  | 上次从AEM上传到AEM Mobile的日期 |
| dps-lastUploadedBy | 字符串：userid |  | 执行从AEM到AEM Mobile的上次上传请求的ID用户 |

## 核心元数据属性 {#core-metadata-properties}

| 属性名称 | 类型 | 默认值或预期值 |
|--- |--- |--- |
| dps-title | 字符串 |  |
| dps-shortTitle | 字符串 |  |
| dps-abstract | 字符串 |  |
| dps-shortAbstract | 字符串 |  |
| dps-department | 字符串 |  |
| dps-类别 | 字符串 |  |
| dps-keywords | String[] |  |
| dps-internalKeywords | String[] |  |
| dps-imprositance | String[] | 重要性来自{&quot;low&quot;、&quot;normal&quot;、&quot;high&quot;} |

### 文章 {#articles}

| **属性名称** | **类型** | **默认值或预期值** |
|---|---|---|
| dps-author | 字符串 |  |
| dps-authorURL | 字符串 |  |
| dps-hideFromBrowsePage | 布尔型 |  |
| dps-access | 字符串 | ProtectedAccess from {&quot;protected&quot;, &quot;metered&quot;, &quot;free&quot;} |
| **Social** |  |  |
| dps-socialShareURL | 字符串 |  |
| dps-articleText | 字符串 |  |
| dps-url | 字符串 |  |

### 横幅 {#banners}

| **属性名称** | **类型** | **默认值或预期值** |
|---|---|---|
| dps-tapAction |  | 从{webLink}点按操作 |
| dps-tapActionUrl |  |  |

### 收藏集 {#collections}

| 属性名称 | 类型 | 默认值或预期值 |
|--- |--- |--- |
| dps-productId | 字符串 |  |
| dps-readingPosition | 字符串 | 从{&quot;reset&quot;,&quot;retain&quot;} |
| dps-horizontalSwipe | 布尔型 |  |
| dps-allow下载 | 布尔型 |  |
| dps-openDefault | 字符串 | from {&quot;browsePage&quot;,&quot;contentView&quot;} |
| dps-layout | 字符串 |  |

## 内容节点 {#content-nodes}

### 常见节点 {#common-nodes}

| 节点名称 | 类型 | 默认值或预期值 | 描述 |
|--- |--- |--- |--- |
| 图像 | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |

### 实体 {#entities}

#### 文章 {#articles-1}

| 节点名称 | 类型 | 预期值的默认值 | 描述 |
|--- |--- |--- |--- |
| 社交共享图像 |  | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |

#### 横幅 {#banners-1}

| 节点名称 | 类型 | 预期值的默认值 | 描述 |
|---|---|---|---|
| NA |  |  |  |

#### 收藏集 {#collections-1}

| 节点名称 | 类型 | 预期值的默认值 | 描述 |
|--- |--- |--- |--- |
| 背景图像 | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |
