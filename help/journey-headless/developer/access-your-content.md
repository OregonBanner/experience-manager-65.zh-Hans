---
title: 如何通过AEM交付API访问您的内容
description: 在AEM无头开发人员历程的这一部分中，了解如何使用GraphQL查询访问内容片段内容。
exl-id: 44f85d00-a958-470a-8a6e-e2ae1580525a
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 17%

---

# 如何通过AEM交付API访问您的内容 {#access-your-content}

在 [AEM Headless开发人员历程,](overview.md) 您可以了解如何使用GraphQL查询访问内容片段的内容并将其馈送到您的应用程序（无头交付）。

## 迄今为止的故事 {#story-so-far}

在AEM无头历程的上一个文档中， [如何对内容进行建模](model-your-content.md) 您学习了AEM中内容建模的基础知识，因此现在应该了解如何对内容结构进行建模，然后使用AEM内容片段模型和内容片段来实现该结构：

* 识别与内容建模相关的概念和术语。
* 了解为何需要内容建模才能交付无头内容。
* 了解如何使用AEM内容片段模型（以及包含内容片段的创作内容）实现此结构。
* 了解如何对内容进行建模；原则和基本样本。

本文基于这些基础知识，以便您了解如何使用AEM GraphQL API在AEM中访问现有的无标题内容。

* **受众**:初学者
* **目标**:了解如何使用AEM GraphQL查询访问内容片段的内容：
   * 引入GraphQL和AEM GraphQL API。
   * 深入了解AEM GraphQL API的详细信息。
   * 请查看一些示例查询，以了解实际操作方式。

## 您想访问您的内容吗？ {#so-youd-like-to-access-your-content}

所以……您拥有所有这些内容，其结构清晰（位于内容片段中），只需等待您的新应用程序提供信息。 问题是，如何实现它？

您需要一种方法来定位特定内容，选择您需要的内容，并将其返回给应用程序以进行进一步处理。

借助Adobe Experience Manager(AEM)，您可以使用AEM GraphQL API有选择地访问内容片段，以仅返回所需的内容。 这意味着您可以实现结构化内容的无头交付，以供在应用程序中使用。

>[!NOTE]
>
>AEM GraphQL API是一种基于标准GraphQL API规范的自定义实施。

## GraphQL — 简介 {#graphql-introduction}

GraphQL是一种开源规范，它提供：

* 一种查询语言，用于从结构化对象中选择特定内容。
* 用于对结构化内容执行这些查询的运行时。

GraphQL是 *强烈* 键入的API。 这意味着 *全部* 必须按类型清晰地构建和组织内容，以便GraphQL *理解* 访问内容和操作方式。 数据字段在GraphQL架构中定义，该架构用于定义内容对象的结构。

然后，GraphQL端点提供响应GraphQL查询的路径。

所有这些都意味着您的应用程序能够准确、可靠、高效地选择所需的内容 — 这正是您与AEM一起使用时需要的内容。

>[!NOTE]
>
>请参阅 *GraphQL*.org和 *GraphQL*.com。

<!--
## AEM and GraphQL {#aem-graphql}

GraphQL is used in various locations in AEM; for example:

* Content Fragments
  * A customized API has been developed for this use-case (Headless Delivery to your app).
    * This is the AEM GraphQL API.
* Commerce
  * AEM Commerce consumes data from a Commerce platform via GraphQL.
  * There are GraphQL integrations between AEM and various third-party commerce solutions, used with the extension hooks provided by the CIF Core Components.
    * This does not use the AEM GraphQL API.

>[!NOTE]
>
>This step of the Headless Journey is only concerned with the AEM GraphQL API and Content Fragments.
-->

## AEM GraphQL API {#aem-graphql-api}

AEM GraphQL API是基于标准GraphQL API规范的自定义版本，专门配置为允许您对内容片段执行（复杂）查询。

由于内容是根据内容片段模型构建的，因此会使用内容片段。 这满足了GraphQL的基本要求。

* 内容片段模型由一个或多个字段组成。
   * 根据数据类型定义每个字段。
* 内容片段模型用于生成相应的AEM GraphQL架构。

要实际访问AEM的GraphQL（和内容），可使用端点提供访问路径。

通过AEM GraphQL API返回的内容随后可供应用程序使用。

为了帮助您直接输入和测试查询，标准GraphiQL界面的实施还可与AEM GraphQL一起使用(这可以与AEM一起安装)。 它提供了语法突出显示、自动完成、自动建议等功能，以及历史记录和在线文档。

>[!NOTE]
>
>AEM GraphQL API 实施基于 GraphQL Java 库。

<!--
### Use Cases for Author and Publish Environments {#use-cases-author-publish-environments}

The use cases for the AEM GraphQL API can depend on the type of AEMenvironment:

* Publish environment; used to: 
  * Query content for JS application (standard use-case)

* Author environment; used to: 
  * Query content for "content management purposes":
    * GraphQL in AEM is currently a read-only API.
    * The REST API can be used for CR(u)D operations.
-->

## 用于 AEM GraphQL API 的内容片段 {#content-fragments-use-with-aem-graphql-api}

内容片段可用作AEM架构和查询的GraphQL的基础，如下所示：

* 它们使您能够设计、创建、策划和发布可无缝交付的独立于页面的内容。
* 它们基于内容片段模型，内容片段模型使用一系列数据类型预先定义结果片段的结构。
* 可使用定义模型时可用的片段引用数据类型实现其他结构层。

### 内容片段模型 {#content-fragments-models}

这些内容片段模型：

* 一旦&#x200B;**启用**，用于生成模式。
* 提供 GraphQL 所需的数据类型和字段。 它们确保您的应用程序仅请求可能的内容，并接收预期内容。
* 数据类型&#x200B;**片段引用**&#x200B;可在模型中使用来引用其他内容片段，因此可引入其他级别的结构。

### 片段引用 {#fragment-references}

**片段引用**：

* 是在定义内容片段模型时可用的特定数据类型。
* 引用另一个片段，具体取决于特定的内容片段模型。
* 允许您创建并检索结构化数据。

   * 定义为&#x200B;**多源**，则主片段可以引用（检索）多个子片段。

### JSON 预览 {#json-preview}

为帮助设计和开发内容片段模型，您可以在内容片段编辑器中预览JSON输出。

![JSON预览](assets/cfm-model-json-preview.png "JSON预览")

<!--
## GraphQL Schema Generation from Content Fragments {#graphql-schema-generation-content-fragments}

GraphQL is a strongly typed API, which means that content must be clearly structured and organized by type. The GraphQL specification provides a series of guidelines on how to create a robust API for interrogating content on a certain instance. To do this, a client needs to fetch the Schema, which contains all the types necessary for a query. 

For Content Fragments, the GraphQL schemas (structure and types) are based on **Enabled** Content Fragment Models and their data types.

>[!CAUTION]
>
>All the GraphQL schemas (derived from Content Fragment Models that have been **Enabled**) are readable through the GraphQL endpoint.
>
>This means that you need to ensure that no sensitive content is available, to ensure that no sensitive data is exposed via GraphQL endpoints; for example, this includes information that could be present as field names in the model definition.

For example, if a user created a Content Fragment Model called `Article`, then AEM generates the object `article` that is of a type `ArticleModel`. The fields within this type correspond to the fields and data types defined in the model.

1. A Content Fragment Model:

   ![Content Fragment Model for use with GraphQL](assets/graphqlapi-cfmodel.png "Content Fragment Model for use with GraphQL")

1. The corresponding GraphQL schema (output from GraphiQL automatic documentation):
   ![GraphQL Schema based on Content Fragment Model](assets/graphqlapi-cfm-schema.png "GraphQL Schema based on Content Fragment Model")

   This shows that the generated type `ArticleModel` contains several [fields](#fields). 
   
   * Three of them have been controlled by the user: `author`, `main` and `referencearticle`.

   * The other fields were added automatically by AEM, and represent helpful methods to provide information about a certain Content Fragment; in this example, `_path`, `_metadata`, `_variations`. These [helper fields](#helper-fields) are marked with a preceding `_` to distinguish between what has been defined by the user and what has been auto-generated.

1. After a user creates a Content Fragment based on the Article model, it can then be interrogated through GraphQL. For examples, see the Sample Queries.md#graphql-sample-queries) (based on a sample Content Fragment structure for use with GraphQL.

In GraphQL for AEM, the schema is flexible. This means that it is auto-generated each and every time a Content Fragment Model is created, updated or deleted. The data schema caches are also refreshed when you update a Content Fragment Model.

The Sites GraphQL service listens (in the background) for any modifications made to a Content Fragment Model. When updates are detected, only that part of the schema is regenerated. This optimization saves time and provides stability.

So for example, if you:

1. Install a package containing `Content-Fragment-Model-1` and `Content-Fragment-Model-2`:
 
   1. GraphQL types for `Model-1` and `Model-2` will be generated.

1. Then modify `Content-Fragment-Model-2`:

   1. Only the `Model-2` GraphQL type will get updated.

   1. Whereas `Model-1` will remain the same. 

>[!NOTE]
>
>This is important to note in case you want to do bulk updates on Content Fragment Models through the REST api, or otherwise.

The schema is served through the same endpoint as the GraphQL queries, with the client handling the fact that the schema is called with the extension `GQLschema`. For example, performing a simple `GET` request on `/content/cq:graphql/global/endpoint.GQLschema` will result in the output of the schema with the Content-type: `text/x-graphql-schema;charset=iso-8859-1`.

### Schema Generation - Unpublished Models {#schema-generation-unpublished-models}

When Content Fragments are nested it can happen that a parent Content Fragment Model is published, but a referenced model is not.

>[!NOTE]
>
>The AEM UI prevents this happening, but if publishing is made programmatically, or with content packages, it can occur.

When this happens, AEM generates an *incomplete* Schema for the parent Content Fragment Model. This means that the Fragment Reference, which is dependent on the unpublished model, is removed from the schema.

## AEM GraphQL Endpoints {#aem-graphql-endpoints}

An endpoint is the path used to access GraphQL for AEM. Using this path you (or your app) can:

* access the GraphQL schemas,
* send your GraphQL queries,
* receive the responses (to your GraphQL queries).

AEM allows for:

* A global endpoint - available for use by all sites.
* Endpoints for specific Sites configurations - that you can configure (in the Configuration Browser), specific to a specified site/project.

## Permissions {#permissions}

The permissions are those required for accessing Assets.

## The AEM GraphiQL Interface {#aem-graphiql-interface}

To help you directly input, and test queries, an implementation of the standard GraphiQL interface is available for use with AEM GraphQL. This can be installed with AEM.

>[!NOTE]
>
>GraphiQL is bound the global endpoint (and does not work with other endpoints for specific Sites configurations).

It provides features such as syntax-highlighting, auto-complete, auto-suggest, together with a history and online documentation.

![GraphiQL Interface](assets/graphiql-interface.png "GraphiQL Interface")
-->

## 实际使用AEM GraphQL API {#actually-using-aem-graphiql}

### 初始设置 {#initial-setup}

在开始查询内容之前，您需要：

* 启用您的端点
   * 使用工具 — >资产 — > GraphQL
   * [启用 GraphQL 端点](/help/assets/content-fragments/graphql-api-content-fragments.md#enabling-graphql-endpoint)

* 安装GraphiQL（如果需要）
   * 安装为专用包
   * [安装AEM GraphiQL界面](/help/assets/content-fragments/graphql-api-content-fragments.md#installing-graphiql-interface)

### 示例结构 {#sample-structure}

要在查询中实际使用AEM GraphQL API，我们可以使用两个非常基本的内容片段模型结构：

* 公司
   * 名称 — 文本
   * 首席执行官（人员） — 片段参考
   * 员工（人员） — 片段参考
* 人员
   * 姓名 - 文本
   * 名字 — 文本

如您所见，CEO和Employees字段引用“人员”片段。

将使用片段模型：

* 在内容片段编辑器中创建内容时
* 生成要查询的GraphQL架构

### 在何处测试查询 {#where-to-test-your-queries}

查询可以在GraphiQL界面中输入，例如：

* `http://localhost:4502/content/graphiql.html`

![GraphiQL 接口](assets/graphiql-interface.png "GraphiQL 接口")

### 查询入门 {#getting-Started-with-queries}

简单的查询是返回公司架构中所有条目的名称。 在此，您需要列出所有公司名称：

```xml
query {
  companyList {
    items {
      name
    }
  }
}
```

更复杂的查询是选择所有没有“Jobs”名称的人员。 这将过滤所有名称不为Jobs的人员。 这是通过EQUALS_NOT运算符实现的（还有更多）：

```xml
query {
  personList(filter: {
    name: {
      _expressions: [
        {
          value: "Jobs"
          _operator: EQUALS_NOT
        }
      ]
    }
  }) {
    items {
      name
      firstName
    }
  }
}
```

您还可以构建更复杂的查询。 例如，查询至少拥有一名员工且其名称为“Smith”的所有公司。 此查询说明了对名为“Smith”的任意人员的筛选，以及从嵌套片段返回的信息：

```xml
query {
  companyList(filter: {
    employees: {
      _match: {
        name: {
          _expressions: [
            {
              value: "Smith"
            }
          ]
        }
      }
    }
  }) {
    items {
      name
      ceo {
        name
        firstName
      }
      employees {
        name
        firstName
      }
    }
  }
}
```

<!-- need code / curl / cli examples-->

有关使用AEM GraphQL API以及配置必需元素的完整详细信息，可以引用：

* 了解如何将GraphQL与AEM结合使用
* 示例内容片段结构
* 了解如何将 GraphQL 与 AEM 结合使用 – 示例内容和查询

## 下一步 {#whats-next}

现在，您已了解如何使用AEM GraphQL API访问和查询无头内容，您现在可以 [了解如何使用REST API访问和更新内容片段的内容](update-your-content.md).

## 其他资源 {#additional-resources}

* [GraphQL.org](https://graphql.org)
   * [架构](https://graphql.org/learn/schema/)
   * [变量](https://graphql.org/learn/queries/#variables)
   * [GraphQL Java库](https://graphql.org/code/#java)
* [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql)
* [了解如何将GraphQL与AEM结合使用](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * [启用 GraphQL 端点](/help/assets/content-fragments/graphql-api-content-fragments.md#enabling-graphql-endpoint)
   * [安装AEM GraphiQL界面](/help/assets/content-fragments/graphql-api-content-fragments.md#installing-graphiql-interface)
* [示例内容片段结构](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)
* [了解如何将 GraphQL 与 AEM 结合使用 – 示例内容和查询](/help/assets/content-fragments/content-fragments-graphql-samples.md)
   * [示例查询 – 一个特定城市片段](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)
   * [元数据的示例查询 – 列出标题为 GB 的奖项的元数据](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb)
   * [示例查询 – 具有指定变体的所有城市](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation)
* [在配置浏览器中启用内容片段功能](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)
* [使用内容片段](/help/assets/content-fragments/content-fragments.md)
   * [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)
   * [JSON 输出](/help/assets/content-fragments/content-fragments-json-preview.md)
* [了解跨源资源共享(CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=en#understand-cross-origin-resource-sharing-(cors))
* [AEM Headless快速入门](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)  — 一个简短的视频教程系列概述了如何使用AEM无标题功能，包括内容建模和GraphQL。

<!--
* [Generating Access Tokens for Server Side APIs](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)
-->
