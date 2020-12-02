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
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 0%

---


# 为Analytics{#implementing-server-side-page-naming-for-analytics}实施服务器端页面命名

Adobe Analytics使用`s.pageName`属性来唯一标识页面并关联为页面收集的数据。 通常，您在AEM中执行以下任务，为AEM发送到Analytics的此属性分配值：

* 使用Analytics云服务框架将CQ变量映射到Analytics `s.pageName`属性。 (请参阅[使用Adobe Analytics属性映射组件数据](/help/sites-administering/adobeanalytics-mapping.md)。)

* 设计页面组件，使其包含您映射到`s.pageName`属性的CQ变量。 (请参阅[为自定义组件实施Adobe Analytics跟踪](/help/sites-developing/extending-analytics-components.md)。)

要在站点控制台和内容分析中显示Analytics报告数据，AEM要求每个页面的`s.pageName`属性值。 AEM Analytics Java API定义您实施的`AnalyticsPageNameProvider`接口，以向站点控制台和内容分析提供`s.pageName`属性的值。 您的`AnaltyicsPageNameProvider`服务会为报告目的解析服务器上的pageName属性，因为可以使用客户端上的Javascript动态设置该属性以用于跟踪目的。

## 默认分析页面名称提供程序服务{#the-default-analytics-page-name-provider-service}

`DefaultPageNameProvider`服务是默认服务，它确定用于检索页面的Analytics数据的`s.pageName`属性的值。 该服务与AEM基础页面组件(`/libs/foundation/components/page`)配合使用。 此页组件定义要映射到`s.pageName`属性的以下CQ变量：

* `pagedata.path`:该值设置为页面路径。
* `pagedata.title`:该值设置为页面标题。
* `pagedata.navTitle`:该值设置为页面导航标题。

`DefaultPageNameProvider`服务确定这些CQ变量中的哪个映射到Analytics云服务框架中的`s.pageName`属性。 然后，该服务确定用于检索分析报告数据的相应页面属性：

* `pagedata.path`:服务使用  `page.getPath()`

* `pagedata.title`:服务使用  `page.getTitle()`

* `pagedata.navTitle`:服务使用  `page.getNavigationTitle()`

`page`对象是页面的[ `com.day.cq.wcm.api.Page`](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/com/day/cq/wcm/api/Page.html) Java对象。

如果未将CQ变量映射到框架中的`s.pageName`属性，则会从页面路径生成`s.pageName`的值。 例如，路径为`/content/geometrixx/en`的页面使用值`content:geometrixx:en`表示`s.pageName`。

>[!NOTE]
>
>DefaultPageNameProvider服务使用100的服务等级。

## 在分析报告{#maintaining-continuity-in-analytics-reporting}中保持连续性

为页面维护分析数据的完整历史记录要求用于页面的s.pageName属性的值始终不变。 但是，可以轻松更改基础页面组件定义的分析属性。 例如，移动页面会更改`pagedata.path`的值，并中断报告历史记录的连续性：

* 为上一路径收集的数据不再与页面关联。
* 如果其他页面使用了其他页面曾经使用的路径，则其他页面会继承该路径的数据。

为确保报告连续性，`s.pageName`的值应具有以下特征：

* 唯一.
* 稳定。
* 可读。

例如，自定义页面组件可以包含一个页面属性，作者使用该属性为用作`s.pageProperties`属性值的页面指定唯一ID:

* 该页面包含一个分析变量，该变量设置为存储在页面属性中的唯一ID的值。
* 分析变量将映射到Analytics框架中的`s.pageProperties`属性。
* AnalyticsPageNameProvider接口的实现会检索用于查询页面分析数据的页面属性值。

>[!NOTE]
>
>请咨询Analytics顾问，帮助您制定`s.pageName`价值的有效战略。

### 实施分析页面名称提供程序服务{#implementing-an-analytics-page-name-provider-service}

将`com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider`接口作为OSGi服务实现，以自定义检索`s.pageName`属性值的逻辑。 站点页面分析和内容分析使用服务从Analytics检索报告数据。

AnalyticsPageNameProvider接口定义了必须实现的两种方法：

* `getPageName`:返回 `String` 表示用作属性的值的 `s.pageName` 值。

* `getResource`:返回 `org.apache.sling.api.resource.Resource` 表示与属性关联的页面的对 `s.pageName` 象。

这两种方法都以`com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext`对象作为参数。 `AnalyticsPageNameContext`类提供有关分析调用的上下文的信息：

* 页面资源的基本路径。
* Analytics云服务配置的`Framework`对象。
* 页面的`Resource`对象。
* 页面的`ResourceResolver`对象。

类还为页面名称提供setter。

### 示例AnalyticsPageNameProvider实施{#example-analyticspagenameprovider-implementation}

以下示例`AnalyticsPageNameProvider`实现支持自定义页面组件：

* 该组件扩展了基础页面组件。
* 该对话框包含一个作者用来指定`s.pageName`属性值的字段。
* 属性值存储在页面实例的`jcr:content`节点的pageName属性中。
* 存储`s.pageName`属性的分析属性称为`pagedata.pagename`。 此属性将映射到Analytics框架中的`s.pageName`属性。

如果正确配置了框架映射，则`getPageName`方法的以下实现将返回pageName节点属性的值：

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

getResource方法的以下实现为页面返回Resource对象：

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

以下代码代表整个类，包括配置服务的SCR注释。 请注意，服务等级为200，它将覆盖默认服务。

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

