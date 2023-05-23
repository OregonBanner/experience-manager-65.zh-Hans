---
title: 內容屬性和節點
seo-title: Content Properties and Nodes
description: 請依照本頁面瞭解內容屬性和節點。
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

# 內容屬性和節點 {#content-properties-and-nodes}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

在AEM中，文章、橫幅和集合以cq：Pages表示。

除了下面顯示的幾個其他屬性以外，他們還共用在任何cq：Page中找到的相同通用屬性，這些屬性代表Adobe Experience Manager (AEM) Mobile On-Demand Services中繼資料和整合支援屬性。

下表說明內容屬性和節點。

## 常見整合屬性 {#common-integration-properties}

| **属性名称** | **类型** | **預設值或預期值** | **描述** |
|---|---|---|---|
| dps-id | 字符串 |  | 上傳至AEM Mobile或從AEM Mobile匯入後，由AEM Mobile指派並由AEM儲存 |
| dps-resourceType | 字符串 | dps:Article | dps:Banner | dps:Collection | 實體型別屬性 |
| dps-version | 字符串 |  | AEM Mobile實體版本（也包含在完整aemm-id中） |
| dps-lastSynced | 日期 |  | 上次從AEM Mobile同步/匯入至AEM的日期 |
| dps-lastUploaded | 日期 |  | 上次從AEM上傳至AEM Mobile的日期 |
| dps-lastUploadedBy | String：userid |  | 執行上次從AEM到AEM Mobile上傳請求的id使用者 |

## 核心中繼資料屬性 {#core-metadata-properties}

| 属性名称 | 类型 | 預設值或預期值 |
|--- |--- |--- |
| dps-title | 字符串 |  |
| dps-shortTitle | 字符串 |  |
| dps-abstract | 字符串 |  |
| dps-shortAbstract | 字符串 |  |
| dps-department | 字符串 |  |
| dps-category | 字符串 |  |
| dps-keywords | 字符串[] |  |
| dps-internalKeywords | 字符串[] |  |
| dps-importance | 字符串[] | 重要性來自{&quot;low&quot;、&quot;normal&quot;、&quot;high&quot;} |

### 文章 {#articles}

| **属性名称** | **类型** | **預設值或預期值** |
|---|---|---|
| dps-author | 字符串 |  |
| dps-authorURL | 字符串 |  |
| dps-hideFromBrowsePage | 布尔值 |  |
| dps-access | 字符串 | ProtectedAccess來自{&quot;protected&quot;， &quot;metered&quot;， &quot;free&quot;} |
| **Social** |  |  |
| dps-socialShareURL | 字符串 |  |
| dps-articleText | 字符串 |  |
| dps-url | 字符串 |  |

### 横幅 {#banners}

| **属性名称** | **类型** | **預設值或預期值** |
|---|---|---|
| dps-tapAction |  | 來自{webLink}的TapAction |
| dps-tapActionUrl |  |  |

### 收藏集 {#collections}

| 属性名称 | 类型 | 預設值或預期值 |
|--- |--- |--- |
| dps-productId | 字符串 |  |
| dps-readingPosition | 字符串 | 從{&quot;reset&quot;，&quot;retain&quot;} |
| dps-horizontalSwipe | 布尔值 |  |
| dps-allowDownload | 布尔值 |  |
| dps-openDefault | 字符串 | 從{&quot;browsePage&quot;，&quot;contentView&quot;} |
| dps-layout | 字符串 |  |

## 內容節點 {#content-nodes}

### 通用節點 {#common-nodes}

| 节点名称 | 类型 | 預設值或預期值 | 描述 |
|--- |--- |--- |--- |
| 图像 | jcr：primaryType=nt：unstructured <br> sling：resourceType=foundation/components/image |  |  |

### 实体 {#entities}

#### 文章 {#articles-1}

| 节点名称 | 类型 | 預期值的預設值 | 描述 |
|--- |--- |--- |--- |
| social-share-image |  | jcr：primaryType=nt：unstructured <br> sling：resourceType=foundation/components/image |  |

#### 横幅 {#banners-1}

| 节点名称 | 类型 | 預期值的預設值 | 描述 |
|---|---|---|---|
| NA |  |  |  |

#### 收藏集 {#collections-1}

| 节点名称 | 类型 | 預期值的預設值 | 描述 |
|--- |--- |--- |--- |
| background-image | jcr：primaryType=nt：unstructured <br> sling：resourceType=foundation/components/image |  |  |
