---
title: 实施Analytics的服务器端页面命名
seo-title: Implementing Server-Side Page Naming for Analytics
description: Adobe Analytics使用s.pageName属性来唯一标识页面，并关联为页面收集的数据
seo-description: Adobe Analytics uses the s.pageName property to uniquely identify pages and to associate the data that is collected for the pages
uuid: 37b92099-0cce-4b2d-b55c-928f636dbd7e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: be2aa297-5b78-4b1d-8ff1-e6a585a177dd
exl-id: 17a4e4dc-804e-44a9-9942-c37dbfc8016f
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 0%

---

# 实施Analytics的服务器端页面命名{#implementing-server-side-page-naming-for-analytics}

Adobe Analytics使用 `s.pageName` 属性，用于唯一标识页面并关联为页面收集的数据。 通常，您需要在AEM中执行以下任务，为AEM发送到Analytics的此属性分配一个值：

* 使用Analytics云服务框架将CQ变量映射到Analytics `s.pageName` 属性。 (请参阅 [将组件数据映射到Adobe Analytics属性](/help/sites-administering/adobeanalytics-mapping.md).)

* 设计页面组件，使其包含映射到的CQ变量 `s.pageName` 属性。 (请参阅 [为自定义组件实施Adobe Analytics跟踪](/help/sites-developing/extending-analytics-components.md).)

要在“站点”控制台和“内容分析”中显示Analytics报表数据，AEM需要 `s.pageName` 属性。 AEM Analytics Java API定义 `AnalyticsPageNameProvider` 您为提供站点控制台和内容分析而实施的界面，其值为 `s.pageName` 属性。 您的 `AnaltyicsPageNameProvider` 服务解析服务器上的pageName属性以用于生成报告，因为它可以在客户端上使用JavaScript动态设置以用于跟踪目的。

## 默认的Analytics页面名称提供程序服务 {#the-default-analytics-page-name-provider-service}

此 `DefaultPageNameProvider` service是默认服务，用于确定 `s.pageName` 用于检索页面的Analytics数据的属性。 该服务可与AEM foundation page组件( `/libs/foundation/components/page`)。 此页面组件定义以下旨在映射到的CQ变量 `s.pageName` 属性：

* `pagedata.path`：该值设置为页面路径。
* `pagedata.title`：该值设置为页面标题。
* `pagedata.navTitle`：该值设置为页面导航标题。

此 `DefaultPageNameProvider` 服务确定哪些CQ变量已映射到 `s.pageName` 属性。 然后，该服务确定用于检索Analytics报表数据的相应页面属性：

* `pagedata.path`：服务使用 `page.getPath()`

* `pagedata.title`：服务使用 `page.getTitle()`

* `pagedata.navTitle`：服务使用 `page.getNavigationTitle()`

此 `page` 对象是 [`com.day.cq.wcm.api.Page`](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/com/day/cq/wcm/api/Page.html) 页面的Java对象。

如果不将CQ变量映射到 `s.pageName` 框架中的属性，的值 `s.pageName` 是从页面路径生成的。 例如，路径为 `/content/geometrixx/en` 使用值 `content:geometrixx:en` 对象 `s.pageName`.

>[!NOTE]
>
>DefaultPageNameProvider服务使用的服务等级为100。

## 维护Analytics报表的连续性 {#maintaining-continuity-in-analytics-reporting}

要维护页面的分析数据的完整历史记录，需要用于页面的s.pageName属性的值永不更改。 但是，可以轻松更改基础页面组件定义的analytics属性。 例如，移动页面会更改 `pagedata.path` 和中断了报告历史记录的连续性：

* 为上一路径收集的数据不再与页面关联。
* 如果其他页面使用另一个页面曾经使用的路径，则其他页面会继承该路径的数据。

为确保报告连续性，将 `s.pageName` 应具有以下特征：

* 唯一.
* 稳定。
* 人类看得懂的。

例如，自定义页面组件可以包含页面属性，作者可使用它为页面指定唯一ID，以将其用作的值 `s.pageProperties` 属性：

* 页面包含一个analytics变量，该变量设置为存储在页面属性中的唯一ID的值。
* Analytics变量将映射到 `s.pageProperties` 属性。
* AnalyticsPageNameProvider接口的实施将检索用于查询页面Analytics数据的页面属性的值。

>[!NOTE]
>
>请咨询您的Analytics顾问，以寻求帮助，为您的 `s.pageName` 值。

### 实施Analytics页面名称提供程序服务 {#implementing-an-analytics-page-name-provider-service}

实施 `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider` 界面作为OSGi服务，用于自定义检索 `s.pageName` 属性值。 “站点”页面分析和内容分析使用此服务从Analytics中检索报表数据。

AnalyticsPageNameProvider接口定义了必须实施的两种方法：

* `getPageName`：返回 `String` 值，表示要用作 `s.pageName` 属性。

* `getResource`：返回 `org.apache.sling.api.resource.Resource` 表示与关联的页面的对象 `s.pageName` 属性。

这两种方法都需要 `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext` 对象作为参数。 此 `AnalyticsPageNameContext` 类提供了有关analytics调用上下文的信息：

* 页面资源的基本路径。
* 此 `Framework` Analytics云服务配置的对象。
* 此 `Resource` 页面对象。
* 此 `ResourceResolver` 页面对象。

类还为页面名称提供setter。

### 示例AnalyticsPageNameProvider实施 {#example-analyticspagenameprovider-implementation}

以下示例 `AnalyticsPageNameProvider` 实施支持自定义页面组件：

* 该组件扩展了基础页面组件。
* 该对话框包括一个字段，作者使用该字段指定 `s.pageName` 属性。
* 属性值存储在的pageName属性中 `jcr:content`页面实例的节点。
* 存储 `s.pageName` 属性名为 `pagedata.pagename`. 此属性已映射到 `s.pageName` 属性。

以下实施的 `getPageName` 如果框架映射配置正确，则方法会返回pageName节点属性的值：

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

getResource方法的以下实施返回该页的Resource对象：

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

以下代码表示整个类，包括配置服务的SCR注释。 请注意，服务排名是200，它覆盖了默认服务。

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
