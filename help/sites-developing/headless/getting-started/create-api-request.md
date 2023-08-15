---
title: 访问和交付内容片段Headless快速入门指南
description: 了解如何使用AEM Assets REST API管理内容片段，以及如何使用GraphQL API无头交付内容片段内容。
exl-id: 4664b3a4-4873-4f42-b59d-aadbfaa6072f
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 47%

---

# 访问和交付内容片段Headless快速入门指南 {#accessing-delivering-content-fragments}

了解如何使用AEM Assets REST API管理内容片段，以及如何使用GraphQL API无头交付内容片段内容。

## 什么是 GraphQL 和 Assets REST API？ {#what-are-the-apis}

[现在您已经创建了一些内容片段，](create-content-fragment.md)您可以使用 AEM 的 API 以 Headless 的方式投放它们。

* [GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) 允许您创建请求来访问和投放内容片段。
   * 要使用它， [必须在AEM中定义和启用端点](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#enabling-graphql-endpoint)，如有必要， [已安装GraphiQL接口](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#installing-graphiql-interface).
* [Assets REST API](/help/assets/assets-api-content-fragments.md) 允许您创建和修改内容片段（和其他资源）。

本指南的剩余部分侧重于 GraphQL 访问和内容片段投放。

## 如何使用GraphQL投放内容片段 {#how-to-deliver-a-content-fragment}

信息架构师必须为其渠道端点设计查询才能交付内容。 每个模型的每个端点只需考虑一次这些查询。 对于本指南快速入门，您只需要创建一个。

1. 登录AEM并访问 [GraphiQL接口](/help/sites-developing/headless/graphql-api/graphiql-ide.md)：
   * 例如：`http://<host>:<port>/aem/graphiql.html`。

1. GraphiQL 是用于 GraphQL 的浏览器中查询编辑器。您可以使用它来构建查询，以检索内容片段，并将它们作为JSON无意识地交付。
   * 左侧面板允许您构建查询。
   * 右侧窗格显示结果。
   * 查询编辑器具备代码完成和热键功能，可以轻松地执行查询。
     ![GraphiQL 编辑器](assets/graphiql.png)

1. 假定您创建的模型名为 `person`，带有字段 `firstName`、`lastName` 和 `position`，您可以构建简单的查询来检索内容片段的内容。

   ```text
   query 
   {
     personList {
       items {
         _path
         firstName
         lastName
         position
       }
     }
   }
   ```

1. 在左侧面板中输入查询。
<!--
   ![GraphiQL query](assets/graphiql-query.png)
-->

1. 单击 **执行查询** （向右箭头）图标或使用 `Ctrl-Enter` 热键和结果以JSON格式显示在右侧面板中。
   ![GraphiQL 结果](assets/graphiql-results.png)

1. 单击:
   * **文档** 以显示in-context文档，帮助您构建适应您自己的模型的查询。
   * **历史记录** 顶部工具栏中显示之前的查询。
   * **另存为** 和 **保存** 以保存查询，之后可以从以下位置列出和检索查询： **持久查询** 面板和 **Publish**.
     ![GraphiQL 文档](assets/graphiql-documentation.png)

GraphQL 启用结构化查询，不仅针对特定数据集或者单独的数据对象，而且还可以提供对象的特定元素，嵌套结果，提供查询变量支持，以及诸多功能。

GraphQL可以避免迭代API请求和过度投放。 相反，它允许作为对单个API查询的响应，批量精确投放所需呈现的内容。 生成的 JSON 可用于向其他站点或应用程序提供数据。

## 后续步骤 {#next-steps}

就是这样！现在，您已对 AEM 中的 Headless 内容管理有了基本了解。其中还有很多资源供您深入研究，以全面了解可用的功能。

* **[配置浏览器](create-configuration.md)**  — 有关AEM配置浏览器的详细信息
* **[内容片段](/help/assets/content-fragments/content-fragments.md)** – 提供有关创建和管理内容片段的详细信息
* **[GraphiQL IDE](/help/sites-developing/headless/graphql-api/graphiql-ide.md)** 有关使用GraphiQL IDE的更多详细信息
* **[持久查询](/help/sites-developing/headless/graphql-api/persisted-queries.md)** 有关持久查询的更多详细信息
* **[AEM Assets HTTP API 中的内容片段支持](/help/assets/assets-api-content-fragments.md)** – 提供直接通过 HTTP API 使用 CRUD 操作（创建、读取、更新、删除）访问 AEM 内容的详细信息
* **[GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)** – 提供有关如何以 Headless 方式投放内容片段的详细信息
