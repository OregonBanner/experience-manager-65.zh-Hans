---
title: 叠加
seo-title: Overlays
description: AEM使用覆蓋原則，可讓您擴充和自訂主控台和其他功能
seo-description: AEM uses the principle of overlays to allow you to extend and customize the consoles and other functionality
uuid: d14c08fe-04c0-4925-8c99-c6644357919d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0470b74c-2c34-4327-afed-b95eefb1d521
exl-id: e57a6971-6a6f-427b-a8cd-a2f2e8cdf9e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 0%

---

# 叠加{#overlays}

AEM （在此之前，CQ）一直使用覆蓋原則，好讓您擴充和自訂 [主控台](/help/sites-developing/customizing-consoles-touch.md) 和其他功能(例如， [頁面製作](/help/sites-developing/customizing-page-authoring-touch.md))。

覆蓋是可用於許多內容的字詞。 在此上下文中(擴充AEM)，覆蓋表示採用預先定義的功能並將您自己的定義強加於此功能（以自訂標準功能）。

在標準例項中，預先定義的功能儲存在 `/libs` 而且建議您在下定義覆蓋（自訂） `/apps` 分支。 AEM會使用搜尋路徑來尋找資源，先搜尋 `/apps` 分支，然後 `/libs` 分支( [可以設定搜尋路徑](#configuring-the-search-paths))。 此機制表示您的覆蓋（以及其中定義的自訂）將具有優先權。

自AEM 6.0起，實施及使用覆蓋圖的方式已有所變更：

* AEM 6.0以後 — for [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) — 相關覆蓋圖（即觸控式UI）

   * 方法

      * 重新建構適當的 `/libs` 結構於 `/apps`.

         這不需要一對一的副本， [Sling資源合併](/help/sites-developing/sling-resource-merger.md) 用於互動參照所需的原始定義。 Sling Resource Merger透過差異（差異）機制提供存取和合併資源的服務。

      * 進行任何變更 `/apps`.
   * 优点

      * 更健全，可適應以下變更 `/libs`.
      * 僅重新定義實際需要的專案。


* AEM 6.0之前的非Granite覆蓋圖和覆蓋圖

   * 方法

      * 複製內容來源 `/libs` 至 `/apps`

         您需要複製整個子分支，包括屬性。

      * 進行任何變更 `/apps`.
   * 缺点

      * 雖然您的變更不會因為下方的某些專案變更而遺失 `/libs`，您可能必須重新建立下覆蓋圖中所發生的特定變更 `/apps`.


>[!CAUTION]
>
>此 [Sling資源合併](/help/sites-developing/sling-resource-merger.md) 並且相關方法只能用於 [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). 這表示建立具有骨架結構的覆蓋圖僅適用於標準觸控式UI。
>
>其他區域（包括傳統UI）的覆蓋涉及複製適當的節點和整個子結構，然後進行必要的變更。

針對許多變更，建議使用覆蓋圖，例如 [設定您的主控台](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) 或 [在側面板中的資產瀏覽器中建立您的選取範圍類別](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) （用於編寫頁面）。 需有下列變數：

* 您 ***不得* 變更 `/libs` 分支&#x200B;**您所做的任何變更都可能遺失，因為每當您：

   * 在您的執行個體上升級
   * 套用hotfix
   * 安裝Feature Pack

* 它們會將您的變更集中在一個位置；讓您更輕鬆地追蹤、移轉、備份及/或視需要偵錯變更。

## 設定搜尋路徑 {#configuring-the-search-paths}

對於覆蓋圖，傳送的資源是擷取的資源和屬性的彙總，取決於可定義的搜尋路徑：

* 資源 **解析程式搜尋路徑** 如 [OSGi設定](/help/sites-deploying/configuring-osgi.md) 的 **Apache Sling資源解析器工廠**.

   * 搜尋路徑的由上而下的順序表示其各自的優先順序。
   * 在標準安裝中，主要預設值為 `/apps`， `/libs`  — 所以內容屬於 `/apps` 的優先順序高於 `/libs` (亦即 *覆蓋* it)。

* 兩個服務使用者需要有JCR：READ存取權來存取指令碼儲存的位置。 這些使用者是： components-search-service (由com.day.cq.wcm.coreto用於存取/快取元件)和sling-scripting （由org.apache.sling.servlets.resolver用於尋找servlet）。
* 下列設定也必須根據您放置指令碼的位置（在此範例中位於/etc、/libs或/apps下）進行設定。

   ```
   PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
   resource.resolver.searchpath=["/etc","/apps","/libs"]
   resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
   ```

* 最後，也必須設定Servlet Resolver （在此範例中也是為了新增/etc）

   ```
   PID = org.apache.sling.servlets.resolver.SlingServletResolver
   servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
   ```

## 使用範例 {#example-of-usage}

以下說明部分範例：

* [自訂主控台](/help/sites-developing/customizing-consoles-touch.md)
* [自訂頁面製作](/help/sites-developing/customizing-page-authoring-touch.md)
