---
title: 自訂錯誤處理常式顯示的頁面
seo-title: Customizing Pages shown by the Error Handler
description: AEM隨附處理HTTP錯誤的標準錯誤處理常式
seo-description: AEM comes with a standard error handler for handling HTTP errors
uuid: aaf940fd-e428-4c7c-af7f-88b1d02c17c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 63c94c82-ed96-4d10-b645-227fa3c09f4b
exl-id: d6745baa-44da-45dd-b5d5-a9b218e7e8cf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 2%

---

# 自訂錯誤處理常式顯示的頁面{#customizing-pages-shown-by-the-error-handler}

AEM隨附處理HTTP錯誤的標準錯誤處理常式；例如，顯示：

![chlimage_1-67](assets/chlimage_1-67a.png)

系統提供的指令碼存在(在 `/libs/sling/servlet/errorhandler`)以回應錯誤代碼，標準CQ例項預設提供下列內容：

* 403.jsp
* 404.jsp

>[!NOTE]
>
>AEM是以Apache Sling為基礎，所以請參閱 [https://sling.apache.org/site/errorhandling.html](https://sling.apache.org/site/errorhandling.html) 以取得有關Sling錯誤處理的詳細資訊。

>[!NOTE]
>
>在作者執行個體上， [CQ WCM偵錯篩選器](/help/sites-deploying/osgi-configuration-settings.md) 預設為啟用。 這會一律產生回應代碼200。 預設錯誤處理常式會透過將完整棧疊追蹤寫入回應來回應。
>
>在發佈執行個體上，CQ WCM偵錯篩選器為 *一律* 停用（即使設定為已啟用）。

## 如何自訂錯誤處理常式顯示的頁面 {#how-to-customize-pages-shown-by-the-error-handler}

您可以開發自己的指令碼，以便在發生錯誤時自訂錯誤處理常式顯示的頁面。 您的自訂頁面將會建立在 `/apps` 和覆蓋預設頁面(位於 `/libs`)。

>[!NOTE]
>
>另請參閱 [使用覆蓋](/help/sites-developing/overlays.md) 以取得更多詳細資料。

1. 在存放庫中，複製預設指令碼：

   * 从 `/libs/sling/servlet/errorhandler/`
   * 到 `/apps/sling/servlet/errorhandler/`

   由於目的地路徑預設不存在，因此在第一次執行此動作時，您將需要建立它。

1. 导航到 `/apps/sling/servlet/errorhandler`。您可以：

   * 編輯適當的現有指令碼，以提供所需的資訊。
   * 建立和編輯所需程式碼的新指令碼。

1. 儲存變更並測試。

>[!CAUTION]
>
>404.jsp和403.jsp處理常式是專為滿足CQ5驗證而設計，尤其是在發生這些錯誤時允許系統登入。
>
>因此，取代這兩個處理常式時應格外小心。

### 自訂HTTP 500錯誤的回應 {#customizing-the-response-to-http-errors}

HTTP 500錯誤是由伺服器端例外狀況所造成。

* **[500內部伺服器錯誤](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)**
伺服器發生未預期的情況，無法完成要求。

當請求處理導致例外狀況時，Apache Sling架構(AEM建置在其上)：

* 記錄例外狀況
* 傳回：

   * HTTP回應代碼500
   * 例外狀況棧疊追蹤

   在回應內文中。

作者： [自訂錯誤處理常式顯示的頁面](#how-to-customize-pages-shown-by-the-error-handler) a `500.jsp` 可建立指令碼。 但是，它僅用於 `HttpServletResponse.sendError(500)` 明確地執行，即從例外狀況收集器。

否則，回應代碼會設為500，但 `500.jsp` 指令碼未執行。

若要處理500個錯誤，錯誤處理常式指令碼的檔案名稱必須與exception類別（或超類別）相同。 若要處理所有此類例外，您可以建立指令碼 `/apps/sling/servlet/errorhandler/Throwable.js`p或 `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!CAUTION]
>
>在作者執行個體上， [CQ WCM偵錯篩選器](/help/sites-deploying/osgi-configuration-settings.md) 預設為啟用。 這會一律產生回應代碼200。 預設錯誤處理常式會透過將完整棧疊追蹤寫入回應來回應。
>
>對於自訂錯誤處理常式，需要程式碼為500的回應，因此 [需要停用CQ WCM偵錯篩選器](/help/sites-deploying/osgi-configuration-settings.md). 如此可確保傳回回應代碼500，而這會觸發正確的Sling錯誤處理常式。
>
>在發佈執行個體上，CQ WCM偵錯篩選器為 *一律* 停用（即使設定為已啟用）。
