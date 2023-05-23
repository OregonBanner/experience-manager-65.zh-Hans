---
title: 资源映射
seo-title: Resource Mapping
description: 瞭解如何使用資源對應為AEM定義重新導向、虛名URL和虛擬主機。
seo-description: Learn how to define redirects, vanity URLs and virtual hosts for AEM by using resource mapping.
uuid: 2ca2d0e4-6f90-4ecc-82db-26991f08c66f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 3582a4d8-a47b-467a-9e25-cb45f969ec93
docset: aem65
feature: Configuring
exl-id: 3eebdd38-da5b-4c38-868a-22c3c7a97b66
source-git-commit: 7c24379c01f247f5ad45e3ecd40f3edef4ac3cfb
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 3%

---

# 资源映射{#resource-mapping}

資源對應可用來定義AEM的重新導向、虛名URL和虛擬主機。

例如，您可以使用這些對應來：

* 所有請求的前置詞為 `/content` 以便對網站的訪客隱藏內部結構。
* 定義重新導向，讓所有要求到 `/content/en/gateway` 您的網站頁面會重新導向至 `https://gbiv.com/`.

一個可能的HTTP對應會將所有請求加上前置詞 `localhost:4503` 替換為 `/content`. 像這樣的對應可用於在允許的情況下對網站的訪客隱藏內部結構：

`localhost:4503/content/we-retail/en/products.html`

以透過以下方式存取：

`localhost:4503/we-retail/en/products.html`

因為對應會自動新增前置詞 `/content` 至 `/we-retail/en/products.html`.

>[!CAUTION]
>
>虛名URL不支援規則運算式模式。

>[!NOTE]
>
>請參閱Sling檔案，以及 [資源解析的對應](https://sling.apache.org/site/resources.html) 和 [資源](https://sling.apache.org/site/mappings-for-resource-resolution.html) 以取得進一步資訊。

## 檢視對應定義 {#viewing-mapping-definitions}

JCR資源解析器評估（由上而下）以尋找相符專案的對應表單有兩個清單。

這些清單可在「 」下方檢視（連同設定資訊） **JCR ResourceResolver** Felix主控台的選項；例如， `https://<*host*>:<*port*>/system/console/jcrresolver`：

* 組態顯示目前的組態（為下列專案所定義）： [Apache Sling資源解析程式](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver))。

* 設定測試這可讓您輸入URL或資源路徑。 按一下 **解決** 或 **地圖** 以確認系統如何轉換專案。

* **解析器對應專案**
ResourceResolver.resolve方法用來將URL對應至資源的專案清單。

* **對應對應專案**
ResourceResolver.map方法用來將資源路徑對應至URL的專案清單。

這兩個清單會顯示各種專案，包括應用程式定義為預設值的專案。 這些功能的目的通常是簡化使用者的URL。

清單會配對 **圖樣**，此規則運算式與請求相符，且具有一個 **替代** 定義要強制的重新導向。

例如：

**圖樣** `^[^/]+/[^/]+/welcome$`

將觸發：

**替代** `/libs/cq/core/content/welcome.html`.

若要重新導向請求：

`https://localhost:4503/welcome` ``

到:

`https://localhost:4503/libs/cq/core/content/welcome.html`

新的對應定義會在存放庫中建立。

>[!NOTE]
>
>有許多資源可協助說明如何定義規則運算式，例如 [https://www.regular-expressions.info/](https://www.regular-expressions.info/).

### 在AEM中建立對應定義 {#creating-mapping-definitions-in-aem}

在AEM的標準安裝中，您可以找到資料夾：

`/etc/map/http`

這是定義HTTP通訊協定對應時使用的結構。 其他資料夾( `sling:Folder`)可建立於 `/etc/map` 任何其他要對應的通訊協定。

#### 設定內部重新導向至/content {#configuring-an-internal-redirect-to-content}

建立為https://localhost:4503/的任何請求加上前置詞的對映 `/content`：

1. 使用CRXDE導覽至 `/etc/map/http`.

1. 建立新節點：

   * **型別** `sling:Mapping`
此節點型別適用於此類對應，不過其使用並非強制性。

   * **名称** `localhost_any`

1. 按一下 **全部儲存**.
1. **新增** 此節點的下列屬性：

   * **名称** `sling:match`

      * **类型** `String`

      * **值** `localhost.4503/`
   * **名称** `sling:internalRedirect`

      * **类型** `String[]`

      * **值** `/content/`


1. 按一下 **全部儲存**.

這將處理如下請求：
`localhost:4503/geometrixx/en/products.html`
就好像：
`localhost:4503/content/geometrixx/en/products.html`
已要求。

>[!NOTE]
>
>另請參閱 [資源](https://sling.apache.org/site/mappings-for-resource-resolution.html) Sling檔案中，以取得有關可用sling屬性及其設定方式的進一步資訊。

>[!NOTE]
>
>您可以使用 `/etc/map.publish` 以保留發佈環境的設定。 然後必須複製這些專案，並且新位置( `/etc/map.publish`)設定的 **對應位置** 的 [Apache Sling資源解析程式](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver) 發佈環境的。
