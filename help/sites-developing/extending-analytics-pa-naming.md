---
title: 實作Analytics的伺服器端頁面命名
seo-title: Implementing Server-Side Page Naming for Analytics
description: Adobe Analytics會使用s.pageName屬性來唯一識別頁面，並針對頁面所收集的資料建立關聯
seo-description: Adobe Analytics uses the s.pageName property to uniquely identify pages and to associate the data that is collected for the pages
uuid: 37b92099-0cce-4b2d-b55c-928f636dbd7e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: be2aa297-5b78-4b1d-8ff1-e6a585a177dd
exl-id: 17a4e4dc-804e-44a9-9942-c37dbfc8016f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 0%

---

# 實作Analytics的伺服器端頁面命名{#implementing-server-side-page-naming-for-analytics}

Adobe Analytics使用 `s.pageName` 屬性，用來唯一識別頁面及關聯為頁面收集的資料。 您通常會在AEM中執行下列工作，為AEM傳送至Analytics的這個屬性指派值：

* 使用Analytics雲端服務框架將CQ變數對應至Analytics `s.pageName` 屬性。 (請參閱 [將元件資料與Adobe Analytics屬性對應](/help/sites-administering/adobeanalytics-mapping.md).)

* 設計頁面元件，使其包含您對應至的CQ變數 `s.pageName` 屬性。 (請參閱 [對自訂元件實作Adobe Analytics追蹤](/help/sites-developing/extending-analytics-components.md).)

若要在Sites主控台和內容分析中公開Analytics報表資料，AEM需要 `s.pageName` 屬性。 AEM Analytics Java API會定義 `AnalyticsPageNameProvider` 您實作以提供Sites主控台和內容深入分析之值的介面， `s.pageName` 屬性。 您的 `AnaltyicsPageNameProvider` 服務會解析伺服器上的pageName屬性以用於報表用途，因為它可以在使用者端上使用Javascript動態設定以用於追蹤用途。

## 預設Analytics頁面名稱提供者服務 {#the-default-analytics-page-name-provider-service}

此 `DefaultPageNameProvider` service為預設服務，可決定 `s.pageName` 用於擷取頁面之Analytics資料的屬性。 此服務可與AEM foundation頁面元件( `/libs/foundation/components/page`)。 此頁面元件會定義下列意在對應至的CQ變數 `s.pageName` 屬性：

* `pagedata.path`：值會設定為頁面路徑。
* `pagedata.title`：值會設定為頁面標題。
* `pagedata.navTitle`：值會設定為頁面導覽標題。

此 `DefaultPageNameProvider` 此服務會判斷哪些CQ變數對應至 `s.pageName` Analytics雲端服務框架中的屬性。 然後，服務會決定用於擷取Analytics報表資料的適當頁面屬性：

* `pagedata.path`：此服務使用 `page.getPath()`

* `pagedata.title`：此服務使用 `page.getTitle()`

* `pagedata.navTitle`：此服務使用 `page.getNavigationTitle()`

此 `page` 物件是 [ `com.day.cq.wcm.api.Page`](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/com/day/cq/wcm/api/Page.html) 頁面的Java物件。

如果您未將CQ變數對應至 `s.pageName` 屬性，的值 `s.pageName` 從頁面路徑產生。 例如，路徑為的頁面 `/content/geometrixx/en` 使用值 `content:geometrixx:en` 的 `s.pageName`.

>[!NOTE]
>
>DefaultPageNameProvider服務使用100的服務排名。

## 維護Analytics報表的連續性 {#maintaining-continuity-in-analytics-reporting}

若要維護頁面的完整分析資料歷史記錄，用於頁面的s.pageName屬性值永不變更。 不過，可以輕鬆變更Foundation Page元件定義的Analytics屬性。 例如，移動頁面會變更 `pagedata.path` 和會中斷報告歷程記錄的連續性：

* 針對先前路徑所收集的資料不再與頁面相關聯。
* 如果不同頁面使用另一個頁面曾經使用的路徑，則不同頁面會繼承該路徑的資料。

為確保報告持續性， `s.pageName` 應具備下列特性：

* 唯一.
* 穩定。
* 人類看得懂的。

例如，自訂頁面元件可以包含頁面屬性，作者可使用它來指定作為下列專案值的頁面的唯一ID： `s.pageProperties` 屬性：

* 頁面包含分析變數，該變數會設定為儲存在頁面屬性中之唯一ID的值。
* 分析變數會對應至 `s.pageProperties` Analytics框架中的屬性。
* 您實作的AnalyticsPageNameProvider介面會擷取頁面屬性的值，以用於查詢頁面Analytics資料。

>[!NOTE]
>
>請向您的Analytics顧問尋求協助，為您的制定有效的策略 `s.pageName` 值。

### 實作Analytics頁面名稱提供者服務 {#implementing-an-analytics-page-name-provider-service}

實作 `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider` 介面作為OSGi服務，用於自訂擷取 `s.pageName` 屬性值。 網站頁面分析和內容分析會使用此服務從Analytics擷取報表資料。

AnalyticsPageNameProvider介面會定義您必須實作的兩種方法：

* `getPageName`：傳回 `String` 代表要用作 `s.pageName` 屬性。

* `getResource`：傳回 `org.apache.sling.api.resource.Resource` 物件，代表與關聯的頁面 `s.pageName` 屬性。

兩種方法都需要 `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext` 物件作為引數。 此 `AnalyticsPageNameContext` class提供有關analytics呼叫內容的資訊：

* 頁面資源的基本路徑。
* 此 `Framework` Analytics雲端服務設定的物件。
* 此 `Resource` 頁面物件。
* 此 `ResourceResolver` 頁面物件。

類別也會提供頁面名稱的setter。

### AnalyticsPageNameProvider實作範例 {#example-analyticspagenameprovider-implementation}

以下範例 `AnalyticsPageNameProvider` 實作支援自訂頁面元件：

* 此元件會延伸基礎頁面元件。
* 對話方塊中包含一個欄位，作者可使用該欄位指定 `s.pageName` 屬性。
* 屬性值會儲存在的pageName屬性中 `jcr:content`頁面執行個體的節點。
* 儲存「 」的「 」分析屬性 `s.pageName` 屬性已呼叫 `pagedata.pagename`. 此屬性已對應至 `s.pageName` Analytics框架中的屬性。

下列實作 `getPageName` 如果框架對應已正確設定，則方法會傳回pageName節點屬性的值：

```java
public String getPageName(AnalyticsPageNameContext context) {
        String pageName = null;

        Framework framework = context.getFramework();
        Resource resource = context.getResource();

        if (resource != null && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            Page page = resource.adaptTo(Page.class);
            if (cqVar.equals("pagedata.pagename")) {
                pageName = page.getProperties().get("pageName",null);
            }
        }
        return pageName;
    }
```

下列getResource方法實作會傳回頁面的Resource物件：

```java
     public Resource getResource(AnalyticsPageNameContext context) {
        Resource res = null;

        Framework framework = context.getFramework();
        ResourceResolver resolver = context.getResourceResolver();
        String pageName = context.getPageName();
        String basePath = context.getBasePath();

        if (pageName != null && basePath != null && resolver != null
                && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            if (cqVar.equals("pagedata.pagename")) {
             Iterator<Resource>
             hits = resolver.findResources(createQuery(pageName, basePath, "pagename"), Query.JCR_SQL2);
             if (hits.hasNext()) {
              res = hits.next();
              res = res.getParent();
             }
            }
        }
        return res;
    }

    private String createQuery(String pageName, String basePath, String propName) {
        return "SELECT * FROM [cq:PageContent] WHERE ISDESCENDANTNODE(["
                + basePath + "]) and [" + propName + "] = \"" + pageName + "\"";
    }
```

下列程式碼代表整個類別，包括設定服務的SCR註解。 請注意，服務排名是200，會覆寫預設服務。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2019 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.day.cq.analytics.sitecatalyst;

import java.util.Iterator;

import javax.jcr.query.Query;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceResolver;
import org.osgi.framework.Constants;
import org.osgi.service.component.annotations.Component;

import com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext;
import com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider;
import com.day.cq.analytics.sitecatalyst.Framework;
import com.day.cq.wcm.api.Page;

import static com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext.S_PAGE_NAME;

/**
 * Default implementation of {@link AnalyticsPageNameProvider} that resolves
 * page title, path or navTitle if mapped in {@link Framework}.
 */
@Component(
    service = { AnalyticsPageNameProvider.class },
    property = {
        Constants.SERVICE_DESCRIPTION + "=Example Page Name Resolver implementation",
        Constants.SERVICE_RANKING + ":Integer=200"
    }
)
public class ExamplePageNameProvider implements AnalyticsPageNameProvider {
    public String getPageName(AnalyticsPageNameContext context) {
        String pageName = null;

        Framework framework = context.getFramework();
        Resource resource = context.getResource();

        if (resource != null && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            Page page = resource.adaptTo(Page.class);
            if (cqVar.equals("pagedata.path")) {
                pageName = page.getProperties().get("pageName",null);
            }
        }
        return pageName;
    }

    public Resource getResource(AnalyticsPageNameContext context) {
        Resource res = null;

        Framework framework = context.getFramework();
        ResourceResolver resolver = context.getResourceResolver();
        String pageName = context.getPageName();
        String basePath = context.getBasePath();

        if (pageName != null && basePath != null && resolver != null
                && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            if (cqVar.equals("pagedata.pagename")) {
                Iterator<Resource>
                hits = resolver.findResources(createQuery(pageName, basePath, "pagename"), Query.JCR_SQL2);
                if (hits.hasNext()) {
                    res = hits.next();
                    res = res.getParent();
                }
            }
        }
        return res;
    }

    private String createQuery(String pageName, String basePath, String propName) {
        return "SELECT * FROM [cq:PageContent] WHERE ISDESCENDANTNODE(["
                + basePath + "]) and [" + propName + "] = \"" + pageName + "\"";
    }
}
```
