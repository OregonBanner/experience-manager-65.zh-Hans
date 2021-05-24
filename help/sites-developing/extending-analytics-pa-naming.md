---
title: 为Analytics实施服务器端页面命名
seo-title: 为Analytics实施服务器端页面命名
description: Adobe Analytics使用s.pageName属性来唯一标识页面，并关联为页面收集的数据
seo-description: Adobe Analytics使用s.pageName属性来唯一标识页面，并关联为页面收集的数据
uuid: 37b92099-0cce-4b2d-b55c-928f636dbd7e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: be2aa297-5b78-4b1d-8ff1-e6a585a177dd
exl-id: 17a4e4dc-804e-44a9-9942-c37dbfc8016f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 0%

---

# 为Analytics{#implementing-server-side-page-naming-for-analytics}实施服务器端页面命名

Adobe Analytics使用`s.pageName`属性来唯一标识页面并关联为页面收集的数据。 通常，您会在AEM中执行以下任务，以便为AEM发送到Analytics的此属性分配一个值：

* 使用Analytics云服务框架将CQ变量映射到Analytics `s.pageName`属性。 (请参阅[将组件数据映射到Adobe Analytics属性](/help/sites-administering/adobeanalytics-mapping.md)。)

* 设计页面组件，以使其包含映射到`s.pageName`属性的CQ变量。 (请参阅[为自定义组件实施Adobe Analytics跟踪](/help/sites-developing/extending-analytics-components.md)。)

要在站点控制台和内容分析中显示Analytics报表数据， AEM要求每个页面的`s.pageName`属性值。 AEM Analytics Java API定义了您实施的`AnalyticsPageNameProvider`界面，以向站点控制台和内容分析提供`s.pageName`属性的值。 您的`AnaltyicsPageNameProvider`服务解析服务器上的pageName属性以用于报告目的，因为该属性可以使用客户端上的Javascript动态设置以用于跟踪目的。

## 默认的Analytics页面名称提供程序服务{#the-default-analytics-page-name-provider-service}

`DefaultPageNameProvider`服务是默认服务，它确定用于检索页面Analytics数据的`s.pageName`属性值。 该服务可与AEM基础页面组件(`/libs/foundation/components/page`)配合使用。 此页面组件定义了以下要映射到`s.pageName`属性的CQ变量：

* `pagedata.path`:值设置为页面路径。
* `pagedata.title`:值将设置为页面标题。
* `pagedata.navTitle`:值将设置为页面导航标题。

`DefaultPageNameProvider`服务可确定其中哪些CQ变量映射到Analytics云服务框架中的`s.pageName`属性。 然后，该服务会确定用于检索分析报表数据的相应页面属性：

* `pagedata.path`:服务使用  `page.getPath()`

* `pagedata.title`:服务使用  `page.getTitle()`

* `pagedata.navTitle`:服务使用  `page.getNavigationTitle()`

`page`对象是页面的[ `com.day.cq.wcm.api.Page`](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/com/day/cq/wcm/api/Page.html) Java对象。

如果未将CQ变量映射到框架中的`s.pageName`属性，则`s.pageName`的值将从页面路径生成。 例如，路径为`/content/geometrixx/en`的页面使用`content:geometrixx:en`的值`s.pageName`。

>[!NOTE]
>
>DefaultPageNameProvider服务使用100的服务排名。

## 在Analytics报表中维护连续性{#maintaining-continuity-in-analytics-reporting}

要维护页面分析数据的完整历史记录，需要用于页面的s.pageName属性的值永远不变。 但是，基础页面组件定义的分析属性可以轻松更改。 例如，移动页面会更改`pagedata.path`的值，并中断报表历史记录的连续性：

* 为上一路径收集的数据不再与页面关联。
* 如果其他页面使用其他页面以前使用的路径，则不同页面会继承该路径的数据。

为确保报告的连续性，`s.pageName`的值应具有以下特征：

* 唯一.
* 稳定。
* 人类可读。

例如，自定义页面组件可以包含作者用于为页面指定唯一ID的页面属性，该ID用作`s.pageProperties`属性的值：

* 该页面包含一个Analytics变量，该变量设置为存储在页面属性中的唯一ID的值。
* 分析变量会映射到Analytics框架中的`s.pageProperties`属性。
* 您对AnalyticsPageNameProvider界面的实施会检索用于查询页面分析数据的页面属性值。

>[!NOTE]
>
>请咨询您的Analytics顾问，以获取有关为`s.pageName`值制定有效策略的帮助。

### 实施Analytics页面名称提供程序服务{#implementing-an-analytics-page-name-provider-service}

将`com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider`接口作为OSGi服务实施，以自定义检索`s.pageName`属性值的逻辑。 站点页面分析和内容分析使用服务从Analytics中检索报表数据。

AnalyticsPageNameProvider界面定义了必须实施的两种方法：

* `getPageName`:返回 `String` 表示要用作属性的值的 `s.pageName` 值。

* `getResource`:返回一 `org.apache.sling.api.resource.Resource` 个对象，该对象表示与属性关联的 `s.pageName` 页面。

这两种方法都采用`com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext`对象作为参数。 `AnalyticsPageNameContext`类提供有关分析调用上下文的信息：

* 页面资源的基本路径。
* Analytics云服务配置的`Framework`对象。
* 页面的`Resource`对象。
* 页面的`ResourceResolver`对象。

类还为页面名称提供setter。

### AnalyticsPageNameProvider实施示例{#example-analyticspagenameprovider-implementation}

以下示例`AnalyticsPageNameProvider`实施支持自定义页面组件：

* 该组件扩展了基础页面组件。
* 该对话框包括作者用于指定`s.pageName`属性值的字段。
* 属性值存储在页面实例`jcr:content`节点的pageName属性中。
* 存储`s.pageName`属性的分析属性称为`pagedata.pagename`。 此属性已映射到Analytics框架中的`s.pageName`属性。

如果框架映射配置正确，则`getPageName`方法的以下实现会返回pageName节点属性的值：

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

以下代码表示整个类，包括用于配置服务的SCR注释。 请注意，服务排名为200，它覆盖默认服务。

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
