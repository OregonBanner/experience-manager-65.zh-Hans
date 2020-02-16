---
title: 为Analytics实施服务器端页面命名
seo-title: 为Analytics实施服务器端页面命名
description: Adobe Analytics使用s.pageName属性唯一标识页面并关联为页面收集的数据
seo-description: Adobe Analytics使用s.pageName属性唯一标识页面并关联为页面收集的数据
uuid: 37b92099-0cce-4b2d-b55c-928f636dbd7e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: be2aa297-5b78-4b1d-8ff1-e6a585a177dd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 为Analytics实施服务器端页面命名{#implementing-server-side-page-naming-for-analytics}

Adobe Analytics使用该属 `s.pageName` 性唯一标识页面并关联为页面收集的数据。 通常，您在AEM中执行以下任务，以向AEM发送给Analytics的此属性分配一个值：

* 使用Analytics云服务框架将CQ变量映射到Analytics属 `s.pageName` 性。 (请参 [阅使用Adobe Analytics属性映射组件数据](/help/sites-administering/adobeanalytics-mapping.md)。)

* 设计页面组件，使其包含您映射到属性的CQ变 `s.pageName` 量。 (请参 [阅为自定义组件实施Adobe Analytics跟踪](/help/sites-developing/extending-analytics-components.md)。)

要在站点控制台和内容分析中显示Analytics报告数据，AEM要求每个页面的 `s.pageName` 属性值。 AEM Analytics Java API定义您实施的界 `AnalyticsPageNameProvider` 面，以向站点控制台和内容分析提供属性的 `s.pageName` 值。 您的 `AnaltyicsPageNameProvider` 服务会为报告目的解析服务器上的pageName属性，因为可以使用客户端上的Javascript动态设置它以用于跟踪目的。

## 默认分析页面名称提供者服务 {#the-default-analytics-page-name-provider-service}

服务 `DefaultPageNameProvider` 是默认服务，它确定用于检索页面 `s.pageName` 的Analytics数据的属性值。 该服务与AEM基础页面组件( `/libs/foundation/components/page`)结合使用。 此页面组件定义要映射到属性的以下CQ变 `s.pageName` 量：

* `pagedata.path`:该值设置为页面路径。
* `pagedata.title`:该值将设置为页面标题。
* `pagedata.navTitle`:该值设置为页面导航标题。

服 `DefaultPageNameProvider` 务确定将这些CQ变量中的哪个映射到 `s.pageName` Analytics云服务框架中的属性。 然后，该服务确定用于检索分析报告数据的相应页面属性：

* `pagedata.path`:服务使用 `page.getPath()`

* `pagedata.title`:服务使用 `page.getTitle()`

* `pagedata.navTitle`:服务使用 `page.getNavigationTitle()`

对 `page` 象是页面的 [`com.day.cq.wcm.api.Page`](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/com/day/cq/wcm/api/Page.html) Java对象。

如果不将CQ变量映射到框架 `s.pageName` 中的属性，则页面路径将 `s.pageName` 生成该值。 例如，具有路径的页面 `/content/geometrixx/en` 使用的 `content:geometrixx:en` 值 `s.pageName`。

>[!NOTE]
>
>DefaultPageNameProvider服务使用100的服务等级。

## 保持分析报告的连续性 {#maintaining-continuity-in-analytics-reporting}

为页面维护分析数据的完整历史记录要求用于页面的s.pageName属性的值不会更改。 但是，可以轻松更改基础页面组件定义的分析属性。 例如，移动页面会更改报告历史 `pagedata.path` 记录的值并中断报告历史记录的连续性：

* 为上一路径收集的数据不再与页面关联。
* 如果其他页面使用其他页面曾经使用的路径，则其他页面会继承该路径的数据。

为确保报告的连续性，其价 `s.pageName` 值应具有以下特征：

* 唯一.
* 稳定。
* 易于阅读。

例如，自定义页面组件可以包括作者用来为用作属性值的页面指定唯一ID的页面属 `s.pageProperties` 性：

* 该页面包括一个分析变量，该变量设置为存储在页面属性中的唯一ID的值。
* 分析变量将映射到Analytics框 `s.pageProperties` 架中的属性。
* 您对AnalyticsPageNameProvider界面的实现会检索页面属性的值，以用于查询页面分析数据。

>[!NOTE]
>
>请咨询您的Analytics顾问，以获得开发有效价值战略的 `s.pageName` 帮助。

### 实施分析页面名称提供者服务 {#implementing-an-analytics-page-name-provider-service}

将接 `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider` 口作为OSGi服务实现，以自定义检索属性值 `s.pageName` 的逻辑。 “站点”页面分析和内容分析使用该服务从Analytics检索报告数据。

AnalyticsPageNameProvider接口定义了必须实现的两种方法：

* `getPageName`:返回 `String` 一个值，它表示要用作属性的 `s.pageName` 值。

* `getResource`:返回一 `org.apache.sling.api.resource.Resource` 个对象，它表示与属性关联的页 `s.pageName` 面。

这两种方法都 `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext` 将对象作为参数。 该 `AnalyticsPageNameContext` 类提供有关分析调用的上下文的信息：

* 页面资源的基本路径。
* Analytics `Framework` 云服务配置的对象。
* 页 `Resource` 面的对象。
* 页 `ResourceResolver` 面的对象。

该类还为页面名称提供setter。

### 示例AnalyticsPageNameProvider实施 {#example-analyticspagenameprovider-implementation}

以下示例实 `AnalyticsPageNameProvider` 现支持自定义页面组件：

* 该组件扩展了基础页面组件。
* 该对话框包括作者用来指定属性值的字 `s.pageName` 段。
* 属性值存储在页面实例的节 `jcr:content`点的pageName属性中。
* 存储该属性的分析 `s.pageName` 属性被调用 `pagedata.pagename`。 此属性将映射到Analytics框 `s.pageName` 架中的属性。

如果框架映射配 `getPageName` 置正确，则以下方法实现将返回pageName节点属性的值：

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

getResource方法的以下实现返回页面的Resource对象：

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

以下代码表示整个类，包括配置服务的SCR注释。 请注意，服务等级为200，它将覆盖默认服务。

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

