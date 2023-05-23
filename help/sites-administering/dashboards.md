---
title: 功能板
seo-title: Dashboards
description: 瞭解如何建立、設定和開發新的AEM儀表板。
seo-description: Learn how to create, configure and develop new AEM dashboards.
uuid: 3eadbba2-0ce1-41be-a9f8-e6cafa109893
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 40560e06-2508-45a4-a648-39629ed54f28
exl-id: 5b934e3a-f554-46ec-a913-8d570abb1503
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 3%

---

# 功能板{#dashboards}

使用AEM時，您可以管理許多不同型別的內容（例如頁面、資產）。 AEM儀表板提供簡單易用且可自訂的方式，來定義顯示整合資料的頁面。

>[!NOTE]
>
>AEM控制面板是根據使用者建立的，因此使用者只能存取自己的控制面板。
>
>不過， [儀表板範本](#creating-a-dashboard-template) 可用來共用一般設定和控制面板配置。

![chlimage_1-22](assets/chlimage_1-22.jpeg)

## 管理儀表板 {#administering-dashboards}

### 建立控制面板 {#creating-a-dashboard}

若要建立新的控制面板，請依照下列步驟進行：

1. 在 **工具** 區段，按一下 **設定主控台**.
1. 在樹狀結構中，按兩下 **儀表板**.
1. 按一下 **新儀表板**.
1. 輸入 **標題** (例如：我的儀表板)和 **名稱**.
1. 单击&#x200B;**创建**。

### 複製控制面板 {#cloning-a-dashboard}

您可能想要有多個控制面板，以從不同檢視快速檢視有關您內容的資訊。 為協助您建立新儀表板，AEM提供複製功能，可用來複製現有儀表板。 若要複製控制面板，請依照下列步驟進行：

1. 在 **工具** 區段，按一下 **設定主控台**.

1. 在樹狀結構中，按一下 **儀表板**.
1. 按一下您要複製的控制面板。

1. 按一下 **原地複製**.

1. 輸入 **名稱** 的新儀表板。

### 移除控制面板 {#removing-a-dashboard}

1. 在 **工具** 區段，按一下 **設定主控台**.

1. 在樹狀結構中，按一下 **儀表板**.
1. 按一下要刪除的控制面板。

1. 单击&#x200B;**删除**。

1. 单击&#x200B;**是**&#x200B;以确认。

## 儀表板元件 {#dashboard-components}

### 概述 {#overview}

儀表板元件只是一般元件 [AEM元件](/help/sites-developing/developing-components-samples.md). 本節說明AEM隨附的報告元件。

### 網站分析報表元件 {#web-analytics-reporting-components}

AEM隨附一組元件，可轉譯您的多個量度 [SiteCatalyst](/help/sites-administering/adobeanalytics.md) 資料。 這些元件列在Sidekick中的 **儀表板** 區段。

每個報表元件至少提供三個標籤：

* **基本**：包含主要設定。

* **報告：** 包含每個報表的特定設定。
* **樣式**：包含樣式設定，例如圖表大小和邊界。

報表元件會以預設設定進行初始化，以協助您快速設定儀表板。

#### 基本設定 {#basic-configuration}

此 **基本** 索引標籤提供對下列設定專案的存取：

**標題** 控制面板上顯示的標題。

**請求型別** 要求資料的方式。

**SiteCatalyst設定（選擇性）** 您要用來連線至SiteCatalyst的設定。 若未提供，則會假設已在儀表板頁面（透過頁面屬性）上設定設定。

**報表套裝ID （選用）** 您要用來產生圖表的SiteCatalyst報表套裝。

#### 報告設定 {#report-configuration}

若要顯示網頁統計資料，您必須定義要收集的資料日期範圍。 此 **報告** tab提供兩個欄位來定義該範圍。

>[!NOTE]
>
>設定較大的日期範圍可能會降低儀表板的回應能力。

**起始日期** 擷取資料的絕對或相對日期。

**結束日期** 擷取資料的絕對或相對日期。

每個元件也會定義特定設定。

#### 超时报表 {#overtime-report}

![chlimage_1-26](assets/chlimage_1-26a.png)

**日期詳細程度** X軸的時間單位（例如天、小時）。

**量度** 您要顯示的事件清單。

**元素** 可劃分圖形中量度資料的元素清單。

#### 排名列表报表 {#ranked-list-report}

![chlimage_1-27](assets/chlimage_1-27a.png)

**元素** 劃分圖形中量度資料的元素。

**量度** 您要顯示的事件。

**否. 排名最前的專案** 報表顯示的專案數。

#### 排名报表 {#ranked-report}

![chlimage_1-28](assets/chlimage_1-28a.png)

**量度** 您要顯示的事件。

**元素** 劃分圖形中量度資料的元素。

#### 顶级网站区域报表 {#top-site-section-report}

此元件會根據下列設定，顯示網站中造訪次數較多的區段的圖表。

![chlimage_1-29](assets/chlimage_1-29a.png)

**否. 排名最前的專案** 報表中顯示的區段數。

#### 趋势报表 {#trended-report}

![chlimage_1-30](assets/chlimage_1-30a.png)

**日期詳細程度** X軸的時間單位（例如天、小時）。

**量度** 您要顯示的事件。

**元素** 劃分圖形中量度資料的元素。

## 延伸控制面板 {#extending-dashboard}

### 概述 {#overview-1}

儀表板是一般頁面( `cq:Page`)，因此任何元件都可用於組裝儀表板。

有一個預設元件群組 `Dashboard` 包含依預設在範本上啟用的analytics報表元件。

### 建立控制面板範本 {#creating-a-dashboard-template}

範本會定義新控制面板的預設內容。 您可以使用數個範本來建立不同型別的儀表板。

控制面板範本的建立方式與其他頁面範本相同，只是這些範本會儲存在 `/libs/cq/dashboards/templates/`. 請參閱 [建立Contentpage範本](/help/sites-developing/website.md#creating-the-contentpage-template) 區段。

>[!NOTE]
>
>控制面板範本會在使用者之間共用。

### 開發儀表板元件 {#developing-a-dashboard-component}

開發Dashboard元件包含建立一般AEM元件。 本節說明顯示前10名貢獻者的元件範例。

![chlimage_1-31](assets/chlimage_1-31a.png)

主要作者元件儲存在存放庫中，位於 `/apps/geometrixx-outdoors/components/reporting` 和由：

1. a `jsp` 讀取jcr資料並定義 `html` 預留位置。

1. 包含資料庫的使用者端資料庫 `js` 擷取資料並加以排序的檔案，然後填入 `html` 預留位置。

![chlimage_1-32](assets/chlimage_1-32a.png)

下列Javascript檔案定義於 `geout.reporting.topauthors` [使用者端資源庫](/help/sites-developing/clientlibs.md) 作為元件本身的子項。

此 [Querybuilder](/help/sites-developing/querybuilder-api.md) 用於查詢要讀取的存放庫 `cq:AuditEvent` 節點。 查詢結果是JSON物件，系統會從中擷取作者貢獻。

#### top_authors.js {#top-authors-js}

```
$.ajax({
  url: "/bin/querybuilder.json",
  cache: false,
  data: {
       "orderby": "cq:time",
       "orderby.sort": "desc",
       "p.hits": "full",
       "p.limit": 100,
       "path": "/var/audit/com.day.cq.wcm.core.page/",
       "type": "cq:AuditEvent"
   },
  dataType: "json"
}).done(function( res ) {
    var authors = {};
    // from JSON to Object
    for(var r in res.hits) {
        var userId = res.hits[r].userId;
        if(userId == undefined) {
            continue;
        }
        var auth = authors[userId] || {userId : userId};
        auth.contrib = (auth.contrib || 0) +1;

        authors[userId] = auth;
    }

    // order by contribution
    var orderedByContrib = [];
    for(var a in authors) {
        orderedByContrib.push(authors[a]);
    }
    orderedByContrib.sort(function(a,b){return b.contrib - a.contrib});

    // produce the list
    for (var i=0, tot=orderedByContrib.length; i < tot; i++) {
        var current = orderedByContrib[i];
        $("<div> #" + (i + 1) +" "+ current.userId + " (" + current.contrib +" contrib.)</div>").appendTo("#authors-list");

    }
});
```

此 `JSP` 包含兩者 `global.jsp` 和 `clientlib`.

#### top_authors.jsp {#top-authors-jsp}

```java
<%@page session="false" contentType="text/html; charset=utf-8" %><%
%><%
%><%@include file="/libs/foundation/global.jsp" %><%
%>
<ui:includeClientLib categories="geout.reporting.topauthors" />
<%
String reportletTitle = properties.get("title", "Top Authors");
%>
<html>
     <h3><%=xssAPI.encodeForHTML(reportletTitle) %></h3>
     <div id="authors-list"></div>
</html>
```
