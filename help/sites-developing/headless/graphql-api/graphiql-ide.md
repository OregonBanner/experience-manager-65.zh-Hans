---
title: 在 AEM 中使用 GraphiQL IDE
description: 了解如何在 Adobe Experience Manager 中使用 GraphiQL IDE。
exl-id: d4b01485-658b-4245-b2e6-04be8abc8ecf
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 93%

---

# 使用 GraphiQL IDE {#graphiql-ide}

标准的实施 [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) IDE可以与Adobe Experience Manager (AEM)的GraphQL API一起使用。

>[!NOTE]
>
>GraphiQL 包含在 AEM 的所有环境中（但只有在配置端点时才可访问/显示）。
>
>在以前的版本中，安装 GraphiQL IDE 时需要软件包。 如果您已安装此软件，现可将其移除。

>[!NOTE]
>在使用 GraphiQL IDE 之前，您必须在[配置浏览器](/help/assets/content-fragments/content-fragments-configuration-browser.md)中[配置您的端点](/help/sites-developing/headless/graphql-api/graphql-endpoint.md)。

**GraphiQL** 工具允许您测试和调试 GraphQL 查询，方法是：

* 选择适用于您要用于查询的 Sites 配置的&#x200B;**端点**
* 直接输入新查询
* 创建并访问&#x200B;**[持久查询](/help/sites-developing/headless/graphql-api/persisted-queries.md)**
* 运行查询以立即查看结果
* 管理&#x200B;**查询变量**
* 保存并管理&#x200B;**持久查询**
* 发布或取消发布&#x200B;**持久查询**（例如，到/从 `dev-publish`）
* 请参阅之前查询的&#x200B;**历史记录**
* 使用&#x200B;**文档资源管理器**&#x200B;访问文档；帮助您学习和理解可用的方法。

您可以通过以下任一方式访问查询编辑器：

* **工具** -> **常规** -> **GraphQL 查询编辑器**
* 直接；例如，`http://localhost:4502/aem/graphiql.html`

![GraphiQL 接口](assets/cfm-graphiql-interface.png "GraphiQL 接口")

您可以在系统上使用 GraphiQL，以便您的客户端应用程序可以使用 GET 请求来请求查询，并发布查询。 对于生产使用，您可以[将查询移动到生产环境](/help/sites-developing/headless/graphql-api/persisted-queries.md#transfer-persisted-query-production)。 最初是移至生产作者环境，以供通过查询来验证新撰写的内容，最后移至生产发布环境，以供实时使用。

## 选择您的端点 {#selecting-endpoint}

第一步，您需要选择您想用于查询的&#x200B;**[端点](/help/sites-developing/headless/graphql-api/graphql-endpoint.md)**。该端点适用于您要用于查询的 Sites 配置。

这可以从右上角的下拉列表中获得。

## 创建并持久新查询 {#creating-new-query}

您可以在编辑器中输入新查询，该编辑器位于左中面板的 GraphiQL 徽标正下方。

>[!NOTE]
>
>如果您已经选择了一个持久查询，并显示在编辑器面板中，请选择`+`（在&#x200B;**持久查询**&#x200B;旁边）清空编辑器，为新查询做好准备。

只要开始输入，编辑器还会：

* 使用鼠标悬停显示有关元素的其他信息
* 提供语法突出显示、自动完成、自动建议等功能

>[!NOTE]
>
>GraphQL 查询通常以`{`字符开头。
>
>以`#`开头的行会被忽略。

使用&#x200B;**另存为**&#x200B;来保存新查询。

## 正在更新您的持久查询 {#updating-persisted-query}

从&#x200B;**[持久查询](/help/sites-developing/headless/graphql-api/persisted-queries.md)**&#x200B;面板（最左边）的列表中选择要更新的查询。

查询将显示在编辑器面板中。进行任何需要的更改，然后使用&#x200B;**保存**&#x200B;将更新提交到持久查询。

## 正在运行查询 {#running-queries}

您可以立即运行新查询，或者加载并运行持久查询。要加载持久查询，请从列表中选择它，查询将显示在编辑器面板中。

在两种情况下，编辑器面板中显示的查询都是在以下情况下执行的查询：

* 点击/点按&#x200B;**“执行查询”**&#x200B;图标
* 使用键盘组合`Control-Enter`

## 查询变量 {#query-variables}

<!-- more details needed here? -->

GraphiQL IDE 还允许您管理[查询变量](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#graphql-variables)。

例如：

![GraphQL 变量](assets/cfm-graphqlapi-03.png "GraphQL 变量")

<!--
## Managing cache for your persisted queries {#managing-cache}

[Persisted queries](/help/headless/graphql-api/persisted-queries.md) are recommended as they can be cached at the dispatcher and CDN layers, ultimately improving the performance of the requesting client application. By default AEM will invalidate the Content Delivery Network (CDN) cache based on a default Time To Live (TTL).

>[!NOTE]
>
>Custom rewrite rules on the Dispatcher might override defaults from AEM publish. 
>
>In the case that you are sending TTL-based cache-control headers from the dispatcher, based on a location match pattern, then, if necessary, you might want to exclude `/graphql/execute.json/*` from the matches.

Using GraphQL you can configure the HTTP Cache Headers  to control these parameters for your individual persisted query.

1. The **Headers** option is accessible via the three vertical dots to the right of the persisted query name (far left panel):

   ![Persisted Query HTTP Cache Headers](assets/cfm-graphqlapi-headers-01.png "Persisted Query HTTP Cache Headers")

1. Selecting this will open the **Cache Configuration** dialog:

   ![Persisted Query HTTP Cache Header Settings](assets/cfm-graphqlapi-headers-02.png "Persisted Query HTTP Cache Header Settings")

1. Select the appropriate parameter, then adjust the value as required:

   * **cache-control** - **max-age**
     Caches can store this content for specified number of seconds. Typically this is the browser TTL (Time To Live).
   * **surrogate-control** - **s-maxage**
     Same as max-age but applies specifically to proxy caches.
   * **surrogate-control** - **stale-while-revalidate**
     Caches may continue to serve a cached response after it becomes stale, for up to the specified number of seconds.
   * **surrogate-control** - **stale-if-error**
     Caches may continue to serve a cached response in case of or origin error, for up to the specified number of seconds.

1. Select **Save** to persist the changes.
-->

## 正在发布持久查询 {#publishing-persisted-queries}

选择您的 [持久查询](/help/sites-developing/headless/graphql-api/persisted-queries.md) 从列表（左侧面板）中，您可以使用 **Publish** 和 **取消发布** 操作。 这会将它们激活到您的发布环境（例如，`dev-publish`），以便您的应用程序在测试时轻松访问。

>[!NOTE]
>
>持久查询缓存`Time To Live` {&quot;cache-control&quot;:&quot;parameter&quot;:value} 定义的默认值为 2 小时（7200 秒）。

## 复制 URL 以直接访问查询 {#copy-url}

**“复制 URL”**&#x200B;选项允许您通过复制用于直接访问持久查询并查看结果的 URL 来模拟查询。然后可以将其用于测试；例如，通过在浏览器中访问：

<!--
  >[!NOTE]
  >
  >The URL will need [encoding before using programmatically](/help/headless/graphql-api/persisted-queries.md#encoding-query-url).
  >
  >The target environment might need adjusting, depending on your requirements.
-->

例如：

`http://localhost:4502/graphql/execute.json/global/article-list-01`

通过在浏览器中使用此 URL，可以确认结果：

![GraphiQL – 复制 URL ](assets/cfm-graphiql-copy-url.png "GraphiQL – 复制 URL")

**“复制 URL”**&#x200B;选项可通过持久查询名称右侧的三个垂直点访问（最左侧面板）：

![GraphiQL – 复制 URL ](assets/cfm-graphiql-persisted-query-options.png "GraphiQL – 复制 URL")

## 正在删除持久查询 {#deleting-persisted-queries}

**“删除”**&#x200B;选项也可通过持久查询名称右侧的三个垂直点访问（最左侧面板）：

<!-- what happens if you try to delete something that is still published? -->


## 正在生产环境中安装您的持久查询 {#installing-persisted-query-production}

在使用 GraphiQL 开发和测试您的持久查询之后，最终目标是将其[转移到生产环境](/help/sites-developing/headless/graphql-api/persisted-queries.md#transfer-persisted-query-production)中，供应用程序使用。

## 键盘快捷键 {#keyboard-shortcuts}

有多种键盘快捷键可供直接访问 IDE 中的操作图标：

* 美化查询：`Shift-Control-P`
* 合并查询：`Shift-Control-M`
* 执行查询：`Control-Enter`
* 自动完成：`Control-Space`

>[!NOTE]
>
>在一些键盘上，该`Control`键被标记为`Ctrl`。
