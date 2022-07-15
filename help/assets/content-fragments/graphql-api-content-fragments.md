---
title: 用于内容片段的 AEM GraphQL API
description: 了解如何将Adobe Experience Manager(AEM)中的内容片段与AEM GraphQL API结合使用来交付无头内容。
feature: Content Fragments,GraphQL API
exl-id: beae1f1f-0a76-4186-9e58-9cab8de4236d
source-git-commit: 6f3f88ea0f07c97fa8d7ff3bdd1c89114d12a8a1
workflow-type: tm+mt
source-wordcount: '3986'
ht-degree: 89%

---

# 用于内容片段的 AEM GraphQL API {#graphql-api-for-use-with-content-fragments}

了解如何将Adobe Experience Manager(AEM)中的内容片段与AEM GraphQL API结合使用来交付无头内容。

与内容片段一起使用的 AEM GraphQL API 很大程度上依赖于标准的开源 GraphQL API。

在 AEM 中使用 GraphQL API 可以在 Headless CMS 实施中，高效地将内容片段投放到 JavaScript 客户端：

* 避免 REST 中的迭代 API 请求，
* 确保将投放限制到特定要求，
* 允许作为对单个 API 查询的响应，批量精确投放所需呈现的内容。

>[!NOTE]
>
>GraphQL当前用于Adobe Experience Manager(AEM)中的两个（单独）方案：
>
>* [AEM Commerce 通过 GraphQL 使用来自 Commerce 平台的数据](/help/commerce/cif/integrating/magento.md)。
>* AEM 内容片段与 AEM GraphQL API（一种自定义实施，基于标准 GraphQL）配合使用，提供结构化内容用于您的应用程序。


## GraphQL API {#graphql-api}

GraphQL 是：

* “*...一种用于 API 和运行时的查询语言，使用您的现有数据满足这些查询。GraphQL 提供了 API 中数据的完整且可理解的描述，使客户端能够精确地请求所需要的数据，避免其他多余内容，让 API 更容易随时间演进，并提供了强大的开发人员工具。*”

   请参阅 [GraphQL.org](https://graphql.org)。

* “*...一种面向灵活 API 层的开发规格。将 GraphQL 放在现有后端之上，相比从前能够更快地构建产品...*”

   请参阅[探索 GraphQL](https://www.graphql.com)。

* *“...一种数据查询语言和规范，由 Facebook 在 2012 年内部开发，然后在 2015 年公开开源发布。它提供了对基于 REST 的架构的替代，其目的是为了提高开发人员的工作效率并尽可能减少传输的数据量。GraphQL 已由各种规模的数百家组织用于生产环境中...”*

   请参阅 [GraphQL 基础](https://foundation.graphql.org/)。

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all of the tools they need to understand and adopt GraphQL.*". 
-->

有关 GraphQL API 的更多信息，请参阅以下部分（以及多种其他资源）：

* 位于 [graphql.org](https://graphql.org)：

   * [GraphQL 简介](https://graphql.org/learn)

   * [GraphQL 规范](https://spec.graphql.org/)

* 位于 [graphql.com](https://graphql.com)：

   * [ 指南](https://www.graphql.com/guides/)

   * [教程](https://www.graphql.com/tutorials/)

   * [案例研究](https://www.graphql.com/case-studies/)

GraphQL for AEM 实施基于标准 GraphQL Java 库。请参阅：

* [graphQL.org - Java](https://graphql.org/code/#java)

* [GitHub 上的 GraphQL Java](https://github.com/graphql-java)

### GraphQL 术语 {#graphql-terminology}

GraphQL 使用以下对象：

* **[查询](https://graphql.org/learn/queries/)**

* **[架构和类型](https://graphql.org/learn/schema/)**：

   * AEM 基于内容片段模型来生成架构。
   * 使用您的架构，GraphQL 呈现允许用于 GraphQL for AEM 实施的类型和操作。

* **[字段](https://graphql.org/learn/queries/#fields)**

* **[GraphQL 端点](#graphql-aem-endpoint)**
   * AEM 中的路径，对应于 GraphQL 查询，提供对 GraphQL 架构的访问。

   * 有关更多详细信息，请参阅[启用 GraphQL 端点](#enabling-graphql-endpoint)。

请参阅 [(GraphQL.org) GraphQL 简介](https://graphql.org/learn/)获取全面的详细信息，包括[最佳实践](https://graphql.org/learn/best-practices/)。

### GraphQL 查询类型 {#graphql-query-types}

使用 GraphQL，您可以执行查询以返回：

* **单个条目**

* **[条目列表](https://graphql.org/learn/schema/#lists-and-non-null)**

您还可以执行：

* [缓存的持久查询](#persisted-queries-caching)

>[!NOTE]
>您可以使用 [GraphiQL IDE](#graphiql-interface) 测试和调试 GraphQL 查询。

## 用于AEM端点的GraphQL {#graphql-aem-endpoint}

端点是 AEM 用于访问 GraphQL 的路径。您（或您的应用程序）可以使用此路径来：

* 访问 GraphQL 架构，
* 发送 GraphQL 查询，
* 接收（对您 GraphQL 查询的）响应。

AEM 中有两种类型的端点：

* 全局
   * 可供所有站点使用。
   * 此端点可以使用所有 Sites 配置的所有内容片段模型（在[配置浏览器](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)中定义）。
   * 如果有任何应该在 Sites 配置中共享的内容片段模型，则这些内容应该在全局 Sites 配置下创建。
* Sites 配置：
   * 对应于 Sites 配置，如[配置浏览器](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)中的定义。
   * 特定于指定站点/项目。
   * Sites 配置特定的端点将来自特定 Sites 配置与来自全局 Sites 配置的内容片段模型结合使用。

>[!CAUTION]
>
>内容片段编辑器可以允许一个 Sites 配置的内容片段引用另一个 Sites 配置（通过策略）的内容片段。
>
>在这种情况下，所有内容将可使用 Sites 配置特定的端点检索。
>
>内容作者应控制这种情境；例如，在考虑将共享内容片段模型放在全局 Sites 配置下时，它会很有用。

AEM 全局端点的 GraphQL 的存储库路径为：

`/content/cq:graphql/global/endpoint`

对于此项，您的应用程序可以在请求 URL 中使用以下路径：

`/content/_cq_graphql/global/endpoint.json`

要为 AEM 的 GraphQL 启用端点，您需要：

* [启用 GraphQL 端点](#enabling-graphql-endpoint)
* [发布 GraphQL 端点](#publishing-graphql-endpoint)

### 启用 GraphQL 端点 {#enabling-graphql-endpoint}

要启用 GraphQL 端点，您首先需要具有合适的配置。请参阅[内容片段 - 配置浏览器](/help/assets/content-fragments/content-fragments-configuration-browser.md)。

>[!CAUTION]
>
>如果[未启用内容片段模型的使用](/help/assets/content-fragments/content-fragments-configuration-browser.md)，则&#x200B;**创建**&#x200B;选项将不可用。

要启用对应的端点，请执行以下操作：

1. 导航到&#x200B;**工具**、**资源**，然后选择 **GraphQL**。
1. 选择&#x200B;**创建**。
1. 此时将打开&#x200B;**创建新 GraphQL 端点**&#x200B;对话框。在其中可以指定：
   * **名称**：端点的名称，您可以输入任意文本。
   * **使用的 GraphQL 架构提供自**：使用下拉菜单选择所需的站点/项目。

   >[!NOTE]
   >
   >对话框中显示以下警告：
   >
   >* *如果不对 GraphQL 端点仔细管理，则可能会带来数据安全和性能问题。请确保在创建端点后设置适当的权限。*


1. 选择&#x200B;**创建**&#x200B;来确认。
1. **后续步骤**&#x200B;对话框将提供直接指向安全控制台的链接，这样您可以确保新创建的端点具有合适的权限。

   >[!CAUTION]
   >
   >端点可供所有人访问。这会带来安全问题，特别是在发布实例上，因为 GraphQL 查询会对服务器施加大量负载。
   >
   >您可在端点上设置适合您的用例的 ACL。

### 发布 GraphQL 端点 {#publishing-graphql-endpoint}

选择新端点和&#x200B;**发布**&#x200B;以使其在所有环境中完全可用。

>[!CAUTION]
>
>端点可供所有人访问。
>
>在发布实例上，这会带来安全问题，因为 GraphQL 查询会对服务器施加大量负载。
>
>您必须在端点上设置适合您的用例的 ACL。

## GraphiQL接口 {#graphiql-interface}

标准的实施 [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) 界面可与AEM GraphQL一起使用。 这可以[随 AEM 安装](#installing-graphiql-interface)。

>[!NOTE]
>
>GraphiQL 绑定全局端点（不可用于特定 Sites 配置的其他端点）。

此界面允许您直接输入和测试查询。

例如：

* `http://localhost:4502/content/graphiql.html`

这提供了诸如语法突出显示、自动完成、自动建议等功能，以及历史记录和在线文档：

![GraphiQL 接口](assets/cfm-graphiql-interface.png "GraphiQL 接口")

### 安装AEM GraphiQL界面 {#installing-graphiql-interface}

GraphiQL用户界面可以通过专用包安装在AEM上：the [GraphiQL内容包v0.0.6(2021.3)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-graphql/graphiql-0.0.6.zip) 包。

>[!NOTE]
>
>可用的包与AEM 6.5.10.0和AEMas a Cloud Service完全兼容。

## 针对创作环境和发布环境的用例 {#use-cases-author-publish-environments}

用例取决于AEM环境的类型：

* 发布环境；用于：
   * 查询 JS 应用程序的数据（标准用例）

* 创作环境；用于：
   * 查询用于“内容管理用途”的数据：
      * AEM中的GraphQL当前是只读API。
      * REST API 可用于 CR(u)D 操作。

## 权限 {#permission}

权限是访问 Assets 所需的权限。

## 架构生成 {#schema-generation}

GraphQL 是一种强类型的 API，这意味着数据必须有明确的结构并按类型整理。

GraphQL 规范提供了一系列准则，说明如何创建可靠的 API 用于询问特定实例上的数据。为执行此操作，客户端需要提取[架构](#schema-generation)，其中包含查询所需的全部类型。

对于内容片段，GraphQL 架构（结构和类型）基于&#x200B;**已启用**[内容片段模型](/help/assets/content-fragments/content-fragments-models.md)及其数据类型。

>[!CAUTION]
>
>所有 GraphQL 架构（派生自&#x200B;**已启用**&#x200B;的内容片段模型）可通过 GraphQL 端点读取。
>
>这意味着您需要确保其中没有提供敏感数据，因为这种方式可能会导致泄露；例如，这包括可能在模型定义中作为字段名称呈现的信息。

例如，如果创建内容片段模型的用户调用 `Article`，则 AEM 生成对象 `article`，其类型为 `ArticleModel`。此类型中的字段对应于在模型中定义的字段和数据类型。

1. 内容片段模型：

   ![用于 GraphQL 的内容片段模型](assets/cfm-graphqlapi-01.png "用于 GraphQL 的内容片段模型")

1. 对应的 GraphQL 架构（来自 GraphiQL 自动文档的输出）：
   ![GraphQL 架构基于内容片段模型](assets/cfm-graphqlapi-02.png "GraphQL 架构基于内容片段模型")

   这显示了生成的类型 `ArticleModel` 包含多个 [字段](#fields)。

   * 其中三个由用户控制：`author`、`main` 和 `referencearticle`。

   * 其他字段由 AEM 自动添加，表示用于提供有关特定内容片段的有用方法，在本例中为 `_path`、`_metadata`、`_variations`。这些[帮助程序字段](#helper-fields)使用前缀 `_` 标记，用于区分哪些字段由用户定义，哪些字段为自动生成。

1. 用户基于 Article 模型创建内容片段之后，可以通过 GraphQL 询问该模型。例如，请参阅[示例查询](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries)（基于[用于 GraphQL 的示例内容片段结构](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)）。

在 GraphQL for AEM 中，架构是灵活的。这意味着每次在创建、更新或删除内容片段模型时会自动生成架构。数据架构缓存还可在更新内容片段模型时刷新。

Sites GraphQL 服务监听（在后台）对内容片段模型所作的任何更改。检测到更新时，仅重新生成架构的该部分。此优化可节省时间并提供稳定性。

例如，如果您：

1. 安装包含 `Content-Fragment-Model-1` 和 `Content-Fragment-Model-2` 的软件包：

   1. 将生成用于 `Model-1` 和 `Model-2` 的 GraphQL 类型。

1. 然后修改 `Content-Fragment-Model-2`：

   1. 将只更新 `Model-2` GraphQL 类型。

   1. 而 `Model-1` 将保持不变。

>[!NOTE]
>
>在您需要通过 REST api 或以其他方式批量更新内容片段模型时，这一点务必要注意。

架构通过与 GraphQL 查询相同的端点提供，客户端处理使用扩展 `GQLschema` 调用架构的实际情况。例如，在 `/content/cq:graphql/global/endpoint.GQLschema` 上执行简单的 `GET` 请求将导致架构的输出带有内容类型：`text/x-graphql-schema;charset=iso-8859-1`。

### 架构生成 - 未发布的模型 {#schema-generation-unpublished-models}

当内容片段嵌套时，可能会出现的情况是发布了父内容片段模型，但未发布引用的模型。

>[!NOTE]
>
>AEM UI 可以防止出现这种情况，但是，如果以编程方式进行发布，或者使用内容包发布，则可能出现这种情况。

出现这种情况时，AEM 为父内容片段模型生成&#x200B;*不完整的*&#x200B;架构。这意味着依赖于未发布模型的片段引用会从架构中删除。

## 字段 {#fields}

在架构中有两个基本类别的单独字段：

* 您生成的字段。

   使用选择的一组[字段类型](#field-types)，根据您配置内容片段模型的方式来创建字段。字段名称获取自&#x200B;**数据类型**&#x200B;的&#x200B;**属性名称**&#x200B;字段。

   * 其中还有&#x200B;**渲染为**&#x200B;属性需要考虑，因为用户可以配置特定数据类型；例如，作为单行文本或多行文本。

* GraphQL for AEM 还生成多个[帮助程序字段](#helper-fields)。

   这些用于标识内容片段，或者获取有关内容片段的更多信息。

### 字段类型 {#field-types}

GraphQL for AEM 支持一个类型列表。所有支持的内容片段模型数据类型和对应的 GraphQL 类型呈现如下：

| 内容片段模型 - 数据类型 | GraphQL 类型 | 描述 |
|--- |--- |--- |
| 单行文本 | 字符串，[字符串] | 用于简单字符串，例如作者姓名、位置名称等 |
| 多行文本 | 字符串 | 用于输出文本，例如文章的正文 |
| 数值 | 浮点，[浮点] | 用于显示浮点数和常规数字 |
| 布尔型 |  布尔型 | 用于显示复选框 → 简单的 true/false 语句 |
| 日期和时间 | 日历 | 用于显示日期和时间，使用 ISO 8086 格式。根据选择的类型，有三种风格可用于 AEM GraphQL 中：`onlyDate`、`onlyTime`、`dateTime` |
| 枚举 | 字符串 | 用于显示在模型创建时定义的选项列表中的选项 |
| 标记 | [字符串] | 用于显示表示在 AEM 中所用标记的字符串列表 |
| 内容引用 | 字符串 | 用于显示指向 AEM 中其他资源的路径 |
| 片段引用 | *模型类型* | 用于引用特定模型类型的其他内容片段，在创建模型时定义 |

### 帮助程序字段 {#helper-fields}

在用户生成的字段数据类型之外，GraphQL for AEM 还生成了多种&#x200B;*帮助程序* 字段，用于帮助标识内容片段，或者提供有关内容片段的额外信息。

#### 路径 {#path}

路径字段用作 GraphQL 中的标识符。它代表 AEM 存储库中内容片段资源的路径。我们选择此项作为内容片段的标识符是因为它：

* 在 AEM 中唯一
* 可以轻松地提取

以下代码将显示根据内容片段模型 `Person` 创建的所有内容片段的路径。

```xml
{
  personList {
    items {
      _path
    }
  }
}
```

要检索特定类型的单个内容片段，您还需要先确定其路径。例如：

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      firstName
      name
    }
  }
}
```

请参阅[示例查询 - 一个特定城市片段](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)。

#### 元数据 {#metadata}

通过 GraphQL，AEM 还可以公开内容片段的元数据。元数据是描述内容片段的信息，例如内容片段的标题、缩略图路径、内容片段的描述、创建日期等等。

由于元数据通过架构编辑器生成，因此没有特定结构，所以实施了 `TypedMetaData` GraphQL 类型以公开内容片段的元数据。`TypedMetaData` 公开按以下标量类型分组的信息：

| 字段 |
|--- |
| `stringMetadata:[StringMetadata]!` |
| `stringArrayMetadata:[StringArrayMetadata]!` |
| `intMetadata:[IntMetadata]!` |
| `intArrayMetadata:[IntArrayMetadata]!` |
| `floatMetadata:[FloatMetadata]!` |
| `floatArrayMetadata:[FloatArrayMetadata]!` |
| `booleanMetadata:[BooleanMetadata]!` |
| `booleanArrayMetadata:[booleanArrayMetadata]!`  |
| `calendarMetadata:[CalendarMetadata]!` |
| `calendarArrayMetadata:[CalendarArrayMetadata]!` |

每个标量类型表示一个名称-值对或者名称-值对数组，而该对的值是它所分组到的类型。

例如，如果您希望检索内容片段的标题，我们知道此属性是字符串属性，因此我们将查询所有字符串元数据：

要查询元数据，请执行以下操作：

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      _metadata {
        stringMetadata {
          name
          value
        }
      }
    }
  }
}
```

如果您查看生成的 GraphQL 架构，可以查看所有元数据 GraphQL 类型。所有模型类型具有相同的 `TypedMetaData`。

>[!NOTE]
>
>**普通和数组元数据之间的不同**
>请记住，`StringMetadata` 和 `StringArrayMetadata` 均引用存储在存储库中的内容，而非您如何检索它们。
>
>举例而言，通过调用 `stringMetadata` 字段，您应该以 `String` 的形式收到存储在存储库中所有元数据的数组，如果您调用 `stringArrayMetadata`，则会以 `String[]` 的形式收到存储在存储库中所有元数据的数组。

请参阅[元数据的示例查询 - 列出标题为 GB 的奖励的元数据](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb)。

#### 变量 {#variations}

`_variations` 字段已实施以简化查询内容片段具有的变体。例如：

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _variations
    }
  }
}
```

请参阅[示例查询 - 具有指定变体的所有城市](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation)。

>[!NOTE]
>
>如果内容片段不存在给定的变量，则主控变量将作为（回退）默认值返回。

<!--
## Security Considerations {#security-considerations}
-->

## GraphQL 变量 {#graphql-variables}

GraphQL 允许在查询中放入变量。有关详细信息，请参阅 [GraphQL 的变量文档](https://graphql.org/learn/queries/#variables)。

例如，要获取具有特定变体的类型为 `Article` 的所有内容片段，您可以在 GraphiQL 中指定变量 `variation`。

![GraphQL 变量](assets/cfm-graphqlapi-03.png "GraphQL 变量")

```xml
### query
query GetArticlesByVariation($variation: String!) {
    articleList(variation: $variation) {
        items {
            _path
            author
        }
    }
}
 
### in query variables
{
    "variation": "uk"
}
```

## GraphQL 指令 {#graphql-directives}

在 GraphQL 中，可以更改基于变量的查询，这称为 GraphQL 指令。

例如，您可在针对所有 `AdventureModels`、基于变量 `includePrice` 的查询中包含 `adventurePrice` 字段。

![GraphQL 指令](assets/cfm-graphqlapi-04.png "GraphQL 指令")

```xml
### query
query GetAdventureByType($includePrice: Boolean!) {
  adventureList {
    items {
      adventureTitle
      adventurePrice @include(if: $includePrice)
    }
  }
}
 
### in query variables
{
    "includePrice": true
}
```

## 筛选 {#filtering}

您还可以筛选 GraphQL 查询以返回特定数据。

筛选使用基于逻辑运算符和表达式的语法。

例如，以下（基本）查询筛选名为 `Jobs` 或 `Smith` 的所有人员：

```xml
query {
  personList(filter: {
    name: {
      _logOp: OR
      _expressions: [
        {
          value: "Jobs"
        },
        {
          value: "Smith"
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

有关更多示例，请参阅：

* [GraphQL for AEM 扩展](#graphql-extensions)的详细信息

* [使用此示例内容和结构的示例查询](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries-sample-content-fragment-structure)

   * 以及准备用于示例查询的[示例内容和结构](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)

* [基于 WKND 项目的示例查询](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-queries-using-wknd-project)

## GraphQL for AEM - 执行摘要 {#graphql-extensions}

使用 GraphQL for AEM 的查询基本操作遵循标准 GraphQL 规范。对于用于 AEM 的 GraphQL 查询，有几个扩展：

* 如果您需要单个结果：
   * 使用模型名称，例如 city

* 如果您需要结果列表：
   * 将 `List` 添加到模型名称；例如，`cityList`
   * 请参阅[示例查询 - 关于所有城市的所有信息](#sample-all-information-all-cities)

* 如果您希望使用逻辑 OR：
   * 使用 ` _logOp: OR`
   * 请参阅[示例查询 - 所有名为“Jobs”或“Smith”的人](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-all-persons-jobs-smith)

* 逻辑 AND 也可使用，不过（通常）是隐式的

* 您可以查询与内容片段模型中字段对应的字段名称
   * 请参阅[示例查询 - 公司的 CEO 和员工的完整详细信息](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-full-details-company-ceos-employees)

* 除了来自您模型的字段以外，还有一些系统生成的字段（以下划线为前缀）：

   * 对于内容：

      * `_locale`：用于显示语言；基于语言管理器
         * 请参阅[给定区域设置的多个内容片段的示例查询](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-multiple-fragments-given-locale)
      * `_metadata`：用于显示片段的元数据
         * 请参阅[元数据的示例查询 - 列出标题为 GB 的奖励的元数据](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb)
      * `_model`：允许查询内容片段模型（路径和标题）
         * 请参阅[来自模型的内容片段模型的示例查询](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-content-fragment-model-from-model)
      * `_path`：存储库中内容片段的路径
         * 请参阅[示例查询 - 一个特定城市片段](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)
      * `_reference`：用于显示引用，包括富文本编辑器中的内联引用
         * 请参阅[具有预获取引用的多个内容片段的示例查询](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-multiple-fragments-prefetched-references)
      * `_variation`：用于显示内容片段中的特定变体

         >[!NOTE]
         >
         >如果内容片段不存在给定的变量，则主控变量将作为（回退）默认值返回。

         * 请参阅[示例查询 - 具有指定变体的所有城市](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation)
   * 以及操作：

      * `_operator`：应用特定运算符；`EQUALS`、`EQUALS_NOT`、`GREATER_EQUAL`、`LOWER`、`CONTAINS`、`STARTS_WITH`
         * 请参阅[示例查询 - 所有名字不是“Jobs”的人](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-all-persons-not-jobs)
         * 请参阅[示例查询 - `_path` 以特定前缀开头的所有冒险](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-all-adventures-cycling-path-filter)
      * `_apply`：用于应用特定条件，例如 `AT_LEAST_ONCE`
         * 请参阅[示例查询 - 筛选数组中必须至少出现一次的项](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-array-item-occur-at-least-once)
      * `_ignoreCase`：在查询时忽略大小写
         * 请参阅[示例查询 - 名称中包含 SAN 的所有城市，不考虑大小写](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-all-cities-san-ignore-case)









* 支持 GraphQL 合并类型：

   * 使用 `... on`
      * 请参阅[具有内容引用的特定模型的内容片段示例查询](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-fragment-specific-model-content-reference)

* 在查询嵌套片段时回退：

   * 如果请求的变量在嵌套片段中不存在，则 **主控** 将返回变量。

## 持久查询（缓存） {#persisted-queries-caching}

在准备包含POST请求的查询后，可以使用可由HTTP缓存或CDN缓存的GET请求执行该查询。

这是必需的，因为POST查询通常不会缓存，如果将GET与查询一起用作参数，则很有可能会使参数对HTTP服务和中间产品而言变得过大。

持久查询必须始终使用与[相应 Sites 配置](#graphql-aem-endpoint)相关的端点，因此它们可以使用以下项之一或全部：

* 全球配置和端点
查询具有对所有内容片段模型的访问权限。
* 特定 Sites 配置和端点
为特定 Sites 配置创建持久查询需要对应的 Sites 配置特定的端点（用于提供对相关内容片段模型的访问权限）。
例如，要创建特定于 WKND Sites 配置的持久查询，必须预先创建对应的 WKND 特定的端点。

>[!NOTE]
>
>有关更多详细信息，请参阅[在配置浏览器中启用内容片段功能](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)。
>
>**GraphQL 持久查询**&#x200B;需要为对应的 Sites 配置启用。

例如，如果存在名为 `my-query` 的特定查询，使用来自 Sites 配置 `my-conf` 的模型 `my-model`：

* 您可以使用 `my-conf` 特定的端点创建查询，然后查询将保存如下：
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* 您可以使用 `global` 端点创建相同的查询，但然后查询将保存如下：
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>这里有两种不同的查询，保存在不同的路径中。
>
>它们只是正好使用了相同的模型，但通过不同的端点。


以下是保留给定查询所需的步骤：

1. 使用 PUT 操作将查询放入新端点 URL `/graphql/persist.json/<config>/<persisted-label>` 来准备查询。

   例如，创建持久查询：

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
       }
     }
   }'
   ```

1. 此时，检查响应。

   例如，检查是否成功：

   ```xml
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. 然后，您可以通过获取URL来重播保留的查询 `/graphql/execute.json/<shortPath>`.

   例如，使用持久查询：

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. 通过将持久查询 POST 到已经存在的查询路径来更新持久查询。

   例如，使用持久查询：

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
         referencearticle {
           _path
         }
       }
     }
   }'
   ```

1. 创建打包的简单查询。

   例如：

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. 使用缓存控制创建打包的简单查询。

   例如：

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. 使用参数创建持久查询：

   例如：

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-parameters" \
       -d \
   'query GetAsGraphqlModelTestByPath($apath: String!, $withReference: Boolean = true) {
     articleByPath(_path: $apath) {
       item {
         _path
           author
           main {
           plaintext
           }
           referencearticle @include(if: $withReference) {
           _path
           }
         }
       }
     }'
   ```

1. 使用参数执行查询。

   例如：

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   
   $ curl -X GET \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   ```

1. 要在发布时执行查询，需要复制相关的持久树

   * 使用 POST 进行复制：

      ```xml
      $curl -X POST   http://localhost:4502/bin/replicate.json \
        -H 'authorization: Basic YWRtaW46YWRtaW4=' \
        -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
        -F cmd=activate
      ```

   * 使用包：
      1. 创建新的包定义。
      1. 包括配置（例如，`/conf/wknd/settings/graphql/persistentQueries`）。
      1. 构建包。
      1. 复制包。
   * 使用复制/分发工具。
      1. 转到分发工具。
      1. 为配置选择树激活（例如，`/conf/wknd/settings/graphql/persistentQueries`）。
   * 使用工作流（通过工作流启动器配置）：
      1. 定义工作流启动器规则，用于执行将在不同事件上复制配置的工作流模型（例如，创建、修改及其他）。



1. 发布查询配置后，同样的原则适用，只需使用发布端点即可。

   >[!NOTE]
   >
   >对于匿名访问，系统假设 ACL 允许“所有人”可以访问查询配置。
   >
   >如果不是这种情况，它将无法执行。

   >[!NOTE]
   >
   >URL 中的任何分号（“;”）需要编码。
   >
   >例如，在请求中执行持久查询：
   >
   >
   ```xml
   >curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   >```

## 从外部网站查询 GraphQL 端点 {#query-graphql-endpoint-from-external-website}

要从外部网站访问 GraphQL 端点，您需要配置：

* [CORS 筛选条件](#cors-filter)
* [反向链接筛选条件](#referrer-filter)

### CORS 筛选条件 {#cors-filter}

>[!NOTE]
>
>有关 AEM 中 CORS 资源共享策略的详细概述，请参阅[了解跨源资源共享 (CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=zh-Hans#understand-cross-origin-resource-sharing-(cors))。

要访问GraphQL端点，必须在客户Git存储库中配置CORS策略。 此操作可通过为所需端点添加相应的 OSGi CORS 配置文件来完成。

此配置必须指定受信任的网站源 `alloworigin` 或 `alloworiginregexp` 必须授予其访问权限。

例如，要授予对 GraphQL 端点  的访问权限，以及对 `https://my.domain` 的持久查询端点的访问权限，您可以使用：

```xml
{
  "supportscredentials":true,
  "supportedmethods":[
    "GET",
    "HEAD",
    "POST"
  ],
  "exposedheaders":[
    ""
  ],
  "alloworigin":[
    "https://my.domain"
  ],
  "maxage:Integer":1800,
  "alloworiginregexp":[
    ""
  ],
  "supportedheaders":[
    "Origin",
    "Accept",
    "X-Requested-With",
    "Content-Type",
    "Access-Control-Request-Method",
    "Access-Control-Request-Headers"
  ],
  "allowedpaths":[
    "/content/_cq_graphql/global/endpoint.json",
    "/graphql/execute.json/.*"
  ]
}
```

如果您已为端点配置虚名路径，还可以在 `allowedpaths` 中使用它。

### 反向链接筛选条件 {#referrer-filter}

除了CORS配置之外，还必须配置反向链接过滤器，以允许从第三方主机访问。

这是通过添加相应的OSGi反向链接过滤器配置文件来完成的，该配置文件：

* 指定了可信的网站主机名；可以为 `allow.hosts` 或 `allow.hosts.regexp`。
* 授予了对此主机名的访问权限。

例如，要授予反向链接 `my.domain` 的请求的访问权限，您可以：

```xml
{
    "allow.empty":false,
    "allow.hosts":[
      "my.domain"
    ],
    "allow.hosts.regexp":[
      ""
    ],
    "filter.methods":[
      "POST",
      "PUT",
      "DELETE",
      "COPY",
      "MOVE"
    ],
    "exclude.agents.regexp":[
      ""
    ]
}
```

>[!CAUTION]
>
>客户仍然有下列责任：
>
>* 仅向可信域授予访问权限
>* 确保未公开敏感信息
>* 不使用通配符 [*] 语法，这不仅会禁用对 GraphQL 端点的经过身份验证的访问，还会将其向全世界公开。


>[!CAUTION]
>
>所有 GraphQL [架构](#schema-generation)（派生自&#x200B;**已启用**&#x200B;的内容片段模型）可通过 GraphQL 端点读取。
>
>这意味着您需要确保其中没有提供敏感数据，因为这种方式可能会导致泄露；例如，这包括可能在模型定义中作为字段名称呈现的信息。

## 身份验证 {#authentication}

请参阅[对内容片段的远程 AEM GraphQL 查询的身份验证](/help/assets/content-fragments/graphql-authentication-content-fragments.md)。

<!-- to be addressed later -->

<!--
## Sorting {#sorting}
-->

<!-- to be addressed later -->

<!--
## Paging {#paging}
-->

## 常见问题解答 {#faqs}

出现的问题：

1. **问**：*适用于 AEM 的 GraphQL API 与查询生成器 API 有何不同？*

   * **答**：
*AEM GraphQL API 提供了对 JSON 输出的全面控制，是用于查询内容的行业标准。
接下来，AEM 计划投资于 AEM GraphQL API。*

## 教程 - AEM Headless 和 GraphQL 快速入门 {#tutorial}

正在寻找实践教程？请查看 [AEM Headless 和 GraphQL 快速入门](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=zh-Hans)端到端教程，其中说明了在 Headless CMS 场景中，如何使用 AEM GraphQL API 构建和公开内容并由外部应用程序使用。
