---
title: Cloud Service 配置
seo-title: Cloud Service Configurations
description: 您可以擴充現有執行個體以建立自己的設定
seo-description: You can extend the existing instances to create your own configurations
uuid: 9d20c3a4-2a12-4d3c-80c3-fcac3137a675
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d25c03bf-6eaa-45f4-ab60-298865935a62
exl-id: 20a19ee5-7113-4aca-934a-a42c415a8d93
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 3%

---

# Cloud Service 配置{#cloud-service-configurations}

設定旨在提供儲存服務設定的邏輯和結構。

您可以擴充現有執行個體來建立自己的設定。

## 概念 {#concepts}

開發設定時採用的原則以以下概念為基礎：

* 服務/配接器用於擷取組態。
* 設定（例如屬性/段落）繼承自父項。
* 依路徑從Analytics節點參照。
* 易於擴充。
* 具備彈性以因應更複雜的設定，例如 [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics).
* 支援相依性(例如 [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) 外掛程式需要 [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) configuration)。

## 结构 {#structure}

設定的基本路徑為：

`/etc/cloudservices`。

對於每種組態型別，都會提供範本和元件。如此一來，設定範本就能在自訂之後滿足大部分的需求。

若要提供新服務的設定，您需要：

* 在中建立服務區段

   `/etc/cloudservices`

* 在此底下：

   * 設定範本
   * 設定元件

範本和元件必須繼承 `sling:resourceSuperType` 從基本範本：

`cq/cloudserviceconfigs/templates/configpage`

或基礎元件

`cq/cloudserviceconfigs/components/configpage`

服務提供者也應提供服務頁面：

`/etc/cloudservices/<service-name>`

### 模板 {#template}

您的範本將會擴充基本範本：

`cq/cloudserviceconfigs/templates/configpage`

並定義 `resourceType` 指向自訂元件。

```xml
/libs/cq/analytics/templates/sitecatalyst
sling:resourceSuperType = cq/cloudserviceconfigs/templates/configpage
allowedChildren = /libs/cq/analytics/templates/sitecatalyst
allowedPaths = /etc/cloudservices/analytics/*, /etc/cloudservices/analytics/.*
componentReference = cq/analytics/components/sitecatalyst
jcr:content/
cq:designPath = /etc/designs/cloudservices
sling:resourceType = cq/analytics/components/sitecatalystpage

/libs/cq/analytics/templates/generictracker
sling:resourceSuperType = cq/cloudservices/templates/configpage
allowedChildren = /libs/cq/analytics/templates/generictracker
allowedPaths = /etc/cloudservices/analytics/*, /etc/cloudservices/analytics/.*
jcr:content/
cq:designPath = /etc/designs/cloudservices
sling:resourceType = cq/analytics/components/generictrackerpage
```

### 组件 {#components}

您的元件應擴充基本元件：

`cq/cloudserviceconfigs/templates/configpage`

```xml
/libs/cq/analytics/components/sitecatalystpage

/libs/cq/analytics/components/generictrackerpage
```

設定範本和元件後，您可以在下方新增子頁面來新增設定：

`/etc/cloudservices/<service-name>`

### 内容模型 {#content-model}

內容模型儲存為 `cq:Page` 在：

`/etc/cloudservices/<service-name>(/*)`

```xml
/etc/cloudservices
/etc/cloudservices/service-name
/etc/cloudservices/service-name/config
/etc/cloudservices/service-name/config/inherited-config
```

設定會儲存在子節點下 `jcr:content`.

* 在對話方塊中定義的固定屬性應儲存在 `jcr:node` 直接。
* 動態元素(使用 `parsys` 或 `iparsys`)使用子節點來儲存元件資料。

```xml
/etc/cloudservices/service/config/jcr:content as nt:unstructured
propertyname
*
par/component/ as cq:Component
propertyname
*
```

### API {#api}

如需有關API的參考檔案，請參閱 [com.day.cq.wcm.webservicesupport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/webservicesupport/package-summary.html).

### AEM整合 {#aem-integration}

可用的服務列於 **Cloud Services** 的標籤 **頁面屬性** 對話方塊（任何繼承自的頁面） `foundation/components/page` 或 `wcm/mobile/components/page`)。

索引標籤也提供：

* 您可以啟用服務之位置的連結
* 從路徑欄位選擇設定（服務的子節點）

#### 密碼加密 {#password-encryption}

儲存服務的使用者認證時，所有密碼都應加密。

您可以新增隱藏的表單欄位來達成此目的。 此欄位應該有註解 `@Encrypted` 在屬性名稱中；亦即 `password` 欄位名稱將寫成：

`password@Encrypted`

然後，該屬性將自動加密(使用 `CryptoSupport` service)，由 `EncryptionPostProcessor`.

>[!NOTE]
>
>這類似標準 ` [SlingPostServlet](https://sling.apache.org/site/manipulating-content-the-slingpostservlet-servletspost.html)` 註解。

>[!NOTE]
>
>根據預設 `EcryptionPostProcessor` 僅加密 `POST` 向提出要求 `/etc/cloudservices`.

#### 服務頁面的其他屬性jcr：content節點 {#additional-properties-for-service-page-jcr-content-nodes}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>componentreference</td>
   <td>要自動包含在頁面中的元件的參照路徑。<br /> 這會用於其他功能和JS包含。<br /> 這包括頁面上的元件，其中<br /> <code> cq/cloudserviceconfigs/components/servicecomponents</code><br /> 包含(通常早於 <code>body</code> 標籤)。<br /> 若是Analytics和Target，我們會使用這個包含其他功能，例如追蹤訪客行為的JavaScript呼叫。</td>
  </tr>
  <tr>
   <td>说明</td>
   <td>服務的簡短說明。<br /> </td>
  </tr>
  <tr>
   <td>descriptionExtended</td>
   <td>服務的延伸說明。</td>
  </tr>
  <tr>
   <td>排名</td>
   <td>用於清單中的服務排名。</td>
  </tr>
  <tr>
   <td>selectableChildren</td>
   <td>用於在頁面屬性對話方塊中顯示設定的篩選器。</td>
  </tr>
  <tr>
   <td>serviceUrl</td>
   <td>服務網站的URL。</td>
  </tr>
  <tr>
   <td>serviceUrlLabel</td>
   <td>服務URL標籤。</td>
  </tr>
  <tr>
   <td>thumbnailPath</td>
   <td>服務的縮圖路徑。</td>
  </tr>
  <tr>
   <td>可見</td>
   <td>頁面屬性對話方塊中的可見性；預設為可見（選擇性）</td>
  </tr>
 </tbody>
</table>

### 使用案例 {#use-cases}

預設會提供下列服務：

* [追蹤器代碼片段](/help/sites-administering/external-providers.md) (Google、WebTrends等)
* [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)
* [Test&amp;Target](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-target)

<!-- Search&Promote is end of life as of September 1, 2022 * [Search&Promote](/help/sites-administering/marketing-cloud.md#integrating-with-search-promote) -->
* [Dynamic Media](/help/sites-administering/marketing-cloud.md#integrating-with-scene)

>[!NOTE]
>
>另請參閱 [建立自訂Cloud Service](/help/sites-developing/extending-cloud-config-custom-cloud.md).
