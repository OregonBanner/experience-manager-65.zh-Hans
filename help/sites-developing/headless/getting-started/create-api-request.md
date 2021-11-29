---
title: 访问和传送内容片段无头快速入门指南
description: 了解如何使用AEM Assets REST API管理内容片段和GraphQL API来无头地交付内容片段内容。
exl-id: 2b72f222-2ba5-4a21-86e4-40c763679c32
source-git-commit: 6c75af3957c319c38177cd62c90e781a982ba91b
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 1%

---

# 访问和传送内容片段无头快速入门指南 {#accessing-delivering-content-fragments}

了解如何使用AEM Assets REST API管理内容片段和GraphQL API来无头地交付内容片段内容。

## 什么是GraphQL和资产REST API? {#what-are-the-apis}

[现在，您已创建了一些内容片段，](create-content-fragment.md) 您可以使用AEM API无头地提供它们。

* [GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md) 允许您创建访问和交付内容片段的请求。
   * 要使用此功能， [端点需要在AEM中定义和启用](/help/assets/content-fragments/graphql-api-content-fragments.md#enabling-graphql-endpoint)，如果需要， [已安装GraphiQL界面](/help/assets/content-fragments/graphql-api-content-fragments.md#installing-graphiql-interface).
* [资产REST API](/help/assets/assets-api-content-fragments.md) 允许您创建和修改内容片段（和其他资产）。

本指南的其余部分将重点介绍GraphQL访问和内容片段交付。

## 如何使用GraphQL交付内容片段 {#how-to-deliver-a-content-fragment}

信息架构师需要为其渠道端点设计查询才能交付内容。 通常，每个模型的每个端点只需要考虑一次这些查询。 在本快速入门指南中，我们只需创建一个。

1. 登录AEM并访问GraphiQL界面：
   * 例如: `https://<host>:<port>/content/graphiql.html`.

1. GraphiQL是GraphQL的浏览器内查询编辑器。 您可以使用它来构建查询以检索内容片段，以JSON形式直接交付它们。
   * 利用左侧面板，可构建查询。
   * 右侧面板会显示结果。
   * 查询编辑器具有代码完成和热键功能，可轻松执行查询。
      ![GraphiQL编辑器](../assets/graphiql.png)

1. 假设我们创建的模型名为 `person` 带字段 `firstName`, `lastName`和 `position`，我们可以构建一个简单查询，以检索内容片段的内容。

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
   ![GraphiQL查询](../assets/graphiql-query.png)

1. 单击 **执行查询** 按钮或使用 `Ctrl-Enter` 热键和结果在右侧面板中显示为JSON。
   ![GraphiQL结果](../assets/graphiql-results.png)

1. 单击:
   * **文档** 页面右上角以显示上下文文档，以帮助您构建可自行调整模型的查询。
   * **历史** 来显示以前的查询。
      ![GraphiQL文档](../assets/graphiql-documentation.png)

GraphQL支持结构化查询，这些查询不仅可以定向特定数据集或单个数据对象，还可以提供对象的特定元素、嵌套结果、支持查询变量等。

GraphQL可以避免迭代API请求和过度交付，相反，允许批量交付呈现为单个API查询响应所需的确切内容。 生成的JSON可用于将数据交付到其他网站或应用程序。

## 后续步骤 {#next-steps}

就是这样！现在，您对AEM中的无外设内容管理有了基本的了解。 当然，您还可以使用更多资源来更深入地了解可用功能。

* **[配置浏览器](create-configuration.md)**  — 有关AEM配置浏览器的详细信息
* **[内容片段](/help/assets/content-fragments/content-fragments.md)**  — 有关创建和管理内容片段的详细信息
* **[AEM Assets HTTP API中的内容片段支持](/help/assets/assets-api-content-fragments.md)**  — 有关通过CRUD操作（创建、读取、更新、删除）直接通过HTTP API访问AEM内容的详细信息
* **[GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)**  — 有关如何无头提交内容片段的详细信息
