---
title: 進階URL設定
description: 瞭解如何自訂產品和類別頁面的URL。 這可讓實作將搜尋引擎的URL最佳化並促進探索。
sub-product: Commerce
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
exl-id: 0125021a-1c00-4ea3-b7fb-1533b7b9f4f2
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 6%

---

# 進階URL設定 {#url}

>[!NOTE]
>
>搜索引擎优化 (SEO) 已成为许多营销人员关注的重点。因此，許多AEM專案需要解決SEO問題。 請閱讀 [SEO和URL管理最佳作法](https://experienceleague.adobe.com/docs/experience-manager-65/managing/managing-further-reference/seo-and-url-management.html) 以取得其他資訊。

[AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components) 提供進階設定，以便自訂產品和類別頁面的URL。 許多實施會針對搜尋引擎最佳化(SEO)目的自訂這些URL。 以下影片詳細說明如何設定 `UrlProvider` 的服務與功能 [Sling對應](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) 自訂產品和類別頁面的URL。

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 配置 {#configuration}

若要設定 `UrlProvider` 服務必須根據SEO需求和需求提供「CIF URL提供者設定」的OSGI設定。

>[!NOTE]
>
>自AEM CIF核心元件2.0.0版以來，「URL提供者」設定僅提供預先定義的url格式，而非1.x版所擁有的自由文字可設定格式。 此外，使用選取器在URL中傳遞資料的做法已更換為尾碼。

### 產品頁面URL格式 {#product}

這會設定產品頁面的URL，並支援下列選項：

* `{{page}}.html/{{sku}}.html#{{variant_sku}}`（默认）
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`

若為 [Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)：

* `{{page}}` 將取代為 `/content/venia/us/en/products/product-page`
* `{{sku}}` 將由產品的sku取代，例如 `VP09`
* `{{url_key}}` 將由產品的 `url_key` 屬性，例如 `lenora-crochet-shorts`
* `{{url_path}}` 將由產品的 `url_path`，例如 `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` 將由目前選取的變體取代，例如 `VP09-KH-S`

由於 `url_path` 已過時，預先定義的產品URL格式會使用產品的 `url_rewrites` 並挑選路徑分段最多的路徑作為替代路徑，如果 `url_path` 無法使用。

在上述範例資料中，使用預設URL格式的產品變體URL看起來會像 `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`.

### 類別頁面URL格式 {#product-list}

這會設定類別或產品清單頁面的URL，並支援下列選項：

* `{{page}}.html/{{url_path}}.html`（默认）
* `{{page}}.html/{{url_key}}.html`

若為 [Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)：

* `{{page}}` 將取代為 `/content/venia/us/en/products/category-page`
* `{{url_key}}` 將由類別的 `url_key` 屬性
* `{{url_path}}` 將由類別的 `url_path`

在上述範例資料中，使用預設URL格式化的類別頁面URL看起來會像 `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`.

>[!NOTE]
> 
>此 `url_path` 是以下專案的串連： `url_keys` 產品或類別的祖先以及產品或類別的 `url_key` 分隔方式 `/` slash。

### 特定類別 — /產品頁面 {#specific-pages}

可以建立 [多個類別和產品頁面](multi-template-usage.md) 僅用於目錄的特定類別或產品子集。

此 `UrlProvider` 已預先設定，可在作者層級例項上產生這些頁面的深層連結。 這對編輯者很有用，他們可使用預覽模式瀏覽網站、導覽至特定產品或類別頁面，然後切換回編輯模式以編輯頁面。

另一方面，在發佈層級執行個體上，目錄頁面URL應保持穩定，以免失去搜尋引擎排名之類的評分。 因此，根據預設，發佈層執行個體不會轉譯特定目錄頁面的深層連結。 若要變更此行為， _CIF URL提供者特定頁面策略_ 可設定為一律產生特定頁面url。

## 自訂URL格式 {#custom-url-format}

若要提供自訂URL格式，專案可實作 [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) 或 [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) 服務介面，並將實作註冊為OSGI服務。 這些實施（如果可用）將取代已設定的預先定義格式。 如果註冊了多個實作，則服務排名較高的實作會取代服務排名較低的實作。

自訂URL格式實作必須實作一組方法，以便從指定引數建立URL，並剖析URL以分別傳回相同的引數。

## 與Sling對應結合 {#sling-mapping}

除了 `UrlProvider`，也可以設定 [Sling對應](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) 以便重寫及處理URL。 AEM原型專案也提供 [設定範例](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) 為連線埠4503 （發佈）和80 （排程程式）設定一些Sling對應。

## 與AEM Dispatcher結合 {#dispatcher}

也可以使用AEM Dispatcher HTTP伺服器搭配 `mod_rewrite` 模組。 此 [AEM專案原型](https://github.com/adobe/aem-project-archetype) 提供已包含基本設定的AEM Dispatcher參考設定 [重寫規則](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) 所產生的大小。

## 示例

此 [Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia) project包含示範產品和類別頁面使用自訂URL的設定範例。 這可讓每個專案根據其SEO需求，為產品和類別頁面設定個別URL模式。 CIF組合 `UrlProvider` 和Sling對應（如上所述）則會使用。

>[!NOTE]
>
>此設定必須使用專案使用的外部網域進行調整。 Sling對應是根據主機名稱和網域來運作。 因此，此設定預設為停用，必須在部署之前啟用。 若要這麼做，請重新命名Sling對應 `hostname.adobeaemcloud.com` 資料夾位於 `ui.content/src/main/content/jcr_root/etc/map.publish/https` 根據使用的網域名稱，並透過新增以啟用此設定 `resource.resolver.map.location="/etc/map.publish"` 至 `JcrResourceResolver` 專案的設定。

## 其他资源

* [Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)
* [AEM資源對應](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Sling對應](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
