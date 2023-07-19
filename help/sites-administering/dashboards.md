---
title: 功能板
seo-title: Dashboards
description: 了解如何创建、配置和开发新的AEM功能板。
seo-description: Learn how to create, configure and develop new AEM dashboards.
uuid: 3eadbba2-0ce1-41be-a9f8-e6cafa109893
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 40560e06-2508-45a4-a648-39629ed54f28
exl-id: 5b934e3a-f554-46ec-a913-8d570abb1503
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 3%

---

# 功能板{#dashboards}

在使用AEM时，您可以管理大量不同类型的内容（例如，页面、资产）。 AEM功能板提供了一种易于使用且可自定义的方式，来定义显示合并数据的页面。

>[!NOTE]
>
>AEM功能板是按用户创建的，因此用户只能访问自己的功能板。
>
>但是， [功能板模板](#creating-a-dashboard-template) 可用于共享通用配置和功能板布局。

![chlimage_1-22](assets/chlimage_1-22.jpeg)

## 管理功能板 {#administering-dashboards}

### 创建功能板 {#creating-a-dashboard}

要创建新功能板，请按照以下步骤操作：

1. 在 **工具** 部分，单击 **配置控制台**.
1. 在树中，双击 **仪表板**.
1. 单击 **新建仪表板**.
1. 键入 **标题** （例如，“我的仪表板”）和 **名称**.
1. 单击&#x200B;**创建**。

### 克隆功能板 {#cloning-a-dashboard}

您可能希望具有多个功能板，以便从不同视图快速查看有关您的内容的信息。 为了帮助您创建新功能板，AEM提供了一个克隆功能，您可以使用它来复制现有功能板。 要克隆功能板，请按照以下步骤操作：

1. 在 **工具** 部分，单击 **配置控制台**.

1. 在树中，单击 **仪表板**.
1. 单击要克隆的功能板。

1. 单击 **克隆**.

1. 键入 **名称** 新仪表板的。

### 删除功能板 {#removing-a-dashboard}

1. 在 **工具** 部分，单击 **配置控制台**.

1. 在树中，单击 **仪表板**.
1. 单击要删除的仪表板。

1. 单击&#x200B;**删除**。

1. 单击&#x200B;**是**&#x200B;以确认。

## 功能板组件 {#dashboard-components}

### 概述 {#overview}

功能板组件只是常规组件 [AEM组件](/help/sites-developing/developing-components-samples.md). 本节介绍AEM附带的报表组件。

### 网站分析报表组件 {#web-analytics-reporting-components}

AEM附带一组组件，这些组件渲染您的多个量度 [SiteCatalyst](/help/sites-administering/adobeanalytics.md) 数据。 这些组件在Sidekick中列在 **仪表板** 部分。

每个报表组件至少提供三个选项卡：

* **基本**：包含主配置。

* **报告：** 包含每个报表的特定配置。
* **样式**：包含样式配置，如图表大小和边距。

报表组件使用默认配置进行初始化，可帮助您快速设置功能板。

#### 基本配置 {#basic-configuration}

此 **基本** 选项卡提供对以下配置条目的访问：

**标题** 仪表板上显示的标题。

**请求类型** 请求数据的方式。

**SiteCatalyst配置（可选）** 要用于连接到SiteCatalyst的配置。 如果未提供，则假定已在功能板页面（通过页面属性）上配置配置。

**报表包ID（可选）** 要用于生成图形的SiteCatalyst报表包。

#### 报告配置 {#report-configuration}

为了显示Web统计信息，您需要定义要编辑的数据的日期范围。 此 **报告** 选项卡提供了两个字段来定义该范围。

>[!NOTE]
>
>设置较大的日期范围可能会降低仪表板的响应能力。

**起始日期** 从中获取数据的绝对或相对日期。

**结束日期** 获取数据的绝对或相对日期。

每个组件还定义特定的设置。

#### 超时报表 {#overtime-report}

![chlimage_1-26](assets/chlimage_1-26a.png)

**日期粒度** X轴的时间单位（例如，天、小时）。

**量度** 要显示的事件列表。

**元素** 划分图形中量度数据的元素列表。

#### 排名列表报表 {#ranked-list-report}

![chlimage_1-27](assets/chlimage_1-27a.png)

**元素** 在图形中划分量度数据的元素。

**量度** 要显示的事件。

**否. 排名最前的项目** 报表显示的项目数。

#### 排名报表 {#ranked-report}

![chlimage_1-28](assets/chlimage_1-28a.png)

**量度** 要显示的事件。

**元素** 在图形中划分量度数据的元素。

#### 顶级网站区域报表 {#top-site-section-report}

此组件显示一个图形，其中根据以下配置显示网站的访问次数最多的部分。

![chlimage_1-29](assets/chlimage_1-29a.png)

**否. 排名最前的项目** 报告中显示的节数。

#### 趋势报表 {#trended-report}

![chlimage_1-30](assets/chlimage_1-30a.png)

**日期粒度** X轴的时间单位（例如，天、小时）。

**量度** 要显示的事件。

**元素** 在图形中划分量度数据的元素。

## 扩展功能板 {#extending-dashboard}

### 概述 {#overview-1}

功能板是普通页面( `cq:Page`)，因此可以使用任何组件来组装功能板。

有一个默认的组件组 `Dashboard` 包含默认在模板上启用的analytics报表组件。

### 创建功能板模板 {#creating-a-dashboard-template}

模板定义新功能板的默认内容。 您可以使用多个模板来创建不同类型的功能板。

功能板模板与其他页面模板一样创建，只是它们存储在 `/libs/cq/dashboards/templates/`. 请参阅 [正在创建Contentpage模板](/help/sites-developing/website.md#creating-the-contentpage-template) 部分。

>[!NOTE]
>
>仪表板模板在用户之间共享。

### 开发功能板组件 {#developing-a-dashboard-component}

开发功能板组件包括创建常规AEM组件。 此部分介绍了显示前10个贡献者的组件的示例。

![chlimage_1-31](assets/chlimage_1-31a.png)

顶级创作组件存储在存储库中的 `/apps/geometrixx-outdoors/components/reporting` 并由：

1. a `jsp` 读取jcr数据并定义 `html` 占位符。

1. 包含客户端库的客户端库 `js` 文件，用于获取和排序数据，然后填充 `html` 占位符。

![chlimage_1-32](assets/chlimage_1-32a.png)

以下JavaScript文件是在 `geout.reporting.topauthors` [客户端库](/help/sites-developing/clientlibs.md) 作为组件本身的子项。

此 [Querybuilder](/help/sites-developing/querybuilder-api.md) 用于查询要读取的存储库 `cq:AuditEvent` 节点。 查询结果是一个JSON对象，从中可提取作者贡献。

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

此 `JSP` 包括两者 `global.jsp` 和 `clientlib`.

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
