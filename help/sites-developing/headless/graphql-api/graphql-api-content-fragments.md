---
title: 用于内容片段的 AEM GraphQL API
description: 了解如何在Adobe Experience Manager (AEM)中将内容片段与AEM GraphQL API用于Headless内容投放。
feature: Content Fragments,GraphQL API
exl-id: beae1f1f-0a76-4186-9e58-9cab8de4236d
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '4774'
ht-degree: 62%

---

# 用于内容片段的 AEM GraphQL API {#graphql-api-for-use-with-content-fragments}

了解如何在Adobe Experience Manager (AEM)中将内容片段与AEM GraphQL API用于Headless内容投放。

与内容片段一起使用的AEM GraphQL API很大程度上依赖于标准的开源GraphQL API。

在 AEM 中使用 GraphQL API 可以在 Headless CMS 实施中，高效地将内容片段投放到 JavaScript 客户端：

* 避免 REST 中的迭代 API 请求，
* 确保将投放限制到特定要求，
* 允许作为对单个 API 查询的响应，批量精确投放所需呈现的内容。

>[!NOTE]
>
>GraphQL在Adobe Experience Manager (AEM)中使用两种（不同的）方案：
>
>* [AEM Commerce 通过 GraphQL 使用来自 Commerce 平台的数据](/help/commerce/cif/integrating/magento.md)。
>* AEM 内容片段与 AEM GraphQL API（一种自定义实施，基于标准 GraphQL）配合使用，提供结构化内容用于您的应用程序。

## 前提条件 {#prerequisites}

使用GraphQL的客户应安装AEM内容片段和GraphQL索引包1.0.5。请参阅 [发行说明](/help/release-notes/release-notes.md#install-aem-graphql-index-add-on-package) 以了解更多详细信息。

## GraphQL API {#graphql-api}

GraphQL 是：

* “*...一种用于 API 和运行时的查询语言，使用您的现有数据满足这些查询。GraphQL提供了API中数据的完整且可理解的描述。 它使客户端能够精确地请求所需要的信息，而不再需要其他内容，让API更容易随时间演进，并提供了强大的开发人员工具。*“。

  请参阅 [GraphQL.org](https://graphql.org)。

* “*...一种面向灵活 API 层的开发规格。将GraphQL放在现有后端之上，以便您以前所未有的速度构建产品....*“。

  请参阅[探索 GraphQL](https://graphql.com/)。

* *“……一种数据查询语言和规范，由Facebook在2012年内部开发，然后在2015年公开开源发布。 它提供了对基于 REST 的架构的替代，其目的是为了提高开发人员的工作效率并尽可能减少传输的数据量。GraphQL 已由各种规模的数百家组织用于生产环境中...”*

  请参阅 [GraphQL 基础](https://graphql.org/foundation)。

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all the tools they need to understand and adopt GraphQL.*". 
-->

有关GraphQL API的更多信息，请参阅以下部分（以及其他许多资源）：

* 位于 [graphql.org](https://graphql.org)：

   * [GraphQL 简介](https://graphql.org/learn)

   * [GraphQL 规范](https://spec.graphql.org/)

* 位于 [graphql.com](https://graphql.com)：

   * [教程](https://graphql.com/tutorials/)


GraphQL for AEM实施基于标准GraphQL Java™库。 请参阅：

* [graphQL.org – Java](https://graphql.org/code/#java)

* [GitHub上的GraphQL Java™](https://github.com/graphql-java)

### GraphQL 术语 {#graphql-terminology}

GraphQL 使用以下对象：

* **[查询](https://graphql.org/learn/queries/)**

* **[架构和类型](https://graphql.org/learn/schema/)**：

   * AEM 基于内容片段模型来生成架构。
   * 使用您的架构，GraphQL 呈现允许用于 GraphQL for AEM 实施的类型和操作。

* **[字段](https://graphql.org/learn/queries/#fields)**

* **[GraphQL 端点](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#graphql-aem-endpoint)**
   * AEM 中的路径，对应于 GraphQL 查询，提供对 GraphQL 架构的访问。

   * 有关更多详细信息，请参阅[启用 GraphQL 端点](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#enabling-graphql-endpoint)。

请参阅 [(GraphQL.org) GraphQL 简介](https://graphql.org/learn/)获取全面的详细信息，包括[最佳实践](https://graphql.org/learn/best-practices/)。

### GraphQL 查询类型 {#graphql-query-types}

使用 GraphQL，您可以执行查询以返回：

* **单个条目**

* **[条目列表](https://graphql.org/learn/schema/#lists-and-non-null)**

AEM提供了将查询（两种类型）转换为 [持久查询](/help/sites-developing/headless/graphql-api/persisted-queries.md) Dispatcher和CDN缓存的区段。

### GraphQL 查询最佳实践（Dispatcher 和 CND） {#graphql-query-best-practices}

[持久查询](/help/sites-developing/headless/graphql-api/persisted-queries.md) 建议在发布实例上使用的方法是：

* 它们被缓存
* 它们由AEM集中管理

<!-- is this fully accurate? -->
>[!NOTE]
>
>通常创作实例上没有Dispatcher/CDN，因此在那里使用持久查询不会提高性能；除了测试它们。

不建议使用 POST 请求的 GraphQL 查询，因为它们未缓存，因此在默认实例中，Dispatcher 配置为阻止此类查询。

虽然GraphQL也支持GET请求，但这些请求可能会达到限制（例如URL的长度），而使用持久查询可以避免这些限制。

有关更多详细信息，请参阅[启用持久化查询缓存](#enable-caching-persisted-queries)。

>[!NOTE]
>
>将来某个时候，执行直接查询的功能可能会被弃用。

## GraphiQL接口 {#graphiql-interface}

标准的实施 [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) 界面可与AEM GraphQL一起使用。

>[!NOTE]
>
>GraphiQL包含在AEM的所有环境中（但只有在配置端点时才能访问/显示）。
>
>在以前的版本中，安装GraphiQL IDE时需要软件包。 如果您已安装此软件包，现在可以将其删除。

利用此界面，可直接输入和测试查询。

例如：

* `http://localhost:4502/content/graphiql.html`

它提供语法突出显示、自动完成、自动建议等功能，以及历史记录和在线文档：

![GraphiQL 接口](assets/cfm-graphiql-interface.png "GraphiQL 接口")

>[!NOTE]
>
>请参阅 [使用GraphiQL IDE](/help/sites-developing/headless/graphql-api/graphiql-ide.md).

## 针对创作环境和发布环境的用例 {#use-cases-author-publish-environments}

用例可以取决于AEM环境的类型：

* 发布环境；用于：
   * 查询 JS 应用程序的数据（标准用例）

* 创作环境；用于：
   * 查询用于“内容管理用途”的数据：
      * AEM中的GraphQL是一个只读API。
      * REST API 可用于 CR(u)D 操作。

## 权限 {#permission}

访问Assets需要权限。

GraphQL查询是在基础请求的AEM用户的权限下运行的。 如果用户对某些片段（存储为资产）没有读取权限，它们将不会成为结果集的一部分。

此外，用户必须有权访问GraphQL端点才能运行GraphQL查询。

## 架构生成 {#schema-generation}

GraphQL是一种类型的API，这意味着数据必须清楚地按类型构建和组织结构。

GraphQL 规范提供了一系列准则，说明如何创建可靠的 API 用于询问特定实例上的数据。要完成这些指南，客户端必须获取 [架构](#schema-generation)，其中包含查询所需的全部类型。

对于内容片段，GraphQL 架构（结构和类型）基于&#x200B;**已启用**[内容片段模型](/help/assets/content-fragments/content-fragments-models.md)及其数据类型。

>[!CAUTION]
>
>所有 GraphQL 架构（派生自&#x200B;**已启用**&#x200B;的内容片段模型）可通过 GraphQL 端点读取。
>
>这种能力意味着您必须确保没有敏感数据可用，因为数据可能会以这种方式泄露。 例如，它包括可在模型定义中作为字段名称显示的信息。

例如，如果创建内容片段模型的用户调用 `Article`，则 AEM 生成 GraphQL 类型 `ArticleModel`。此类型中的字段对应于在模型中定义的字段和数据类型。此外，它还为操作此类型的查询创建一些入口点，例如 `articleByPath` 或 `articleList`。

1. 内容片段模型：

   ![用于 GraphQL 的内容片段模型](assets/cfm-graphqlapi-01.png "用于 GraphQL 的内容片段模型")

1. 对应的 GraphQL 架构（来自 GraphiQL 自动文档的输出）：
   ![GraphQL 架构基于内容片段模型](assets/cfm-graphqlapi-02.png "GraphQL 架构基于内容片段模型")

   此图像显示生成的类型 `ArticleModel` 包含多个 [字段](#fields).

   * 其中三个由用户控制： `author`， `main`、和 `referencearticle`.

   * 其他字段由AEM自动添加，表示用于提供有关特定内容片段的有用方法。在此示例中， [帮助程序字段](#helper-fields)) `_path`， `_metadata`， `_variations`.

1. 用户基于 Article 模型创建内容片段之后，可以通过 GraphQL 询问该模型。例如，请参阅[示例查询](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#graphql-sample-queries)（基于[用于 GraphQL 的示例内容片段结构](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#content-fragment-structure-graphql)）。

在 GraphQL for AEM 中，架构是灵活的。这种灵活性意味着每次创建、更新或删除内容片段模型时都会自动生成架构。 数据架构缓存还可在更新内容片段模型时刷新。

Sites GraphQL 服务监听（在后台）对内容片段模型所作的任何更改。检测到更新时，仅重新生成架构的该部分。此优化可节省时间并提供稳定性。

例如，如果您：

1. 安装包含 `Content-Fragment-Model-1` 和 `Content-Fragment-Model-2` 的软件包：

   1. 生成用于 `Model-1` 和 `Model-2` 的 GraphQL 类型。

1. 然后修改 `Content-Fragment-Model-2`：

   1. 仅 `Model-2` GraphQL类型已更新。

   1. 而 `Model-1` 保持不变。

>[!NOTE]
>
>此详细信息很重要，以防您通过REST API或以其他方式批量更新内容片段模型。

架构通过与 GraphQL 查询相同的端点提供，客户端处理使用扩展 `GQLschema` 调用架构的实际情况。例如，执行 `GET` 请求日期 `/content/cq:graphql/global/endpoint.GQLschema` 将生成具有内容类型的架构输出： `text/x-graphql-schema;charset=iso-8859-1`.

### 架构生成 – 未发布的模型 {#schema-generation-unpublished-models}

当内容片段嵌套时，可能会出现的情况是发布了父内容片段模型，但未发布引用的模型。

>[!NOTE]
>
>AEM用户界面可以防止出现这种情况，但是，如果以编程方式进行发布，或者使用内容包发布，则可能出现这种情况。

发生这种情况时，AEM会生成 *未完成* 父内容片段模型的架构。 这意味着依赖于未发布模型的片段引用将从架构中删除。

## 字段 {#fields}

在架构中，有两个基本类别的单独字段：

* 您生成的字段。

  使用选择的一组[数据类型](#data-types)，根据您配置内容片段模型的方式来创建字段。字段名称获取自&#x200B;**数据类型**&#x200B;的&#x200B;**属性名称**&#x200B;字段。

   * 还有 **呈现为** 设置，因为用户可以配置某些数据类型。 例如，通过选择将单行文本字段配置为包含多个单行文本 `multifield` 从下拉菜单中查找。

* GraphQL for AEM还生成了多个 [帮助程序字段](#helper-fields).

  这些字段用于标识内容片段，或获取有关内容片段的更多信息。

### 数据类型 {#data-types}

GraphQL for AEM 支持一个类型列表。所有支持的内容片段模型数据类型和对应的 GraphQL 类型呈现如下：

| 内容片段模型 – 数据类型 | GraphQL 类型 | 描述 |
|--- |--- |--- |
| 单行文本 | `String`、`[String]` |  用于简单字符串，例如作者名称和位置名称。 |
| 多行文本 | `String` | 用于输出文本，例如文章的正文 |
| 数字 |  `Float`， `[Float]` | 用于显示浮点数和常规数字 |
| 布尔型 |  `Boolean` | 用于显示复选框 → 简单的 true/false 语句 |
| 日期和时间 | `Calendar` | 用于显示日期和时间，使用 ISO 8086 格式。根据选择的类型，有三种风格可用于 AEM GraphQL 中：`onlyDate`、`onlyTime`、`dateTime` |
| 枚举 |  `String` | 用于显示在模型创建时定义的选项列表中的选项 |
| 标记 |  `[String]` | 用于显示表示在 AEM 中所用标记的字符串列表 |
| 内容引用 |  `String` | 用于显示指向 AEM 中其他资源的路径 |
| 片段引用 | *模型类型*<br><br>单个字段：`Model`-模型类型，直接引用<br><br>多字段，具有一个引用类型：`[Model]`-数组类型`Model`，直接从数组中引用<br><br>多字段，带有多个引用类型；`[AllFragmentModels]`-所有模型类型的数组，从具有合并类型的数组中引用 | 用于引用创建模型时定义的特定模型类型的一个或多个内容片段 |

{style="table-layout:auto"}

### 帮助程序字段 {#helper-fields}

除了用户生成的字段的数据类型之外，GraphQL for AEM还生成了多个 *辅助函数* 帮助标识内容片段或提供有关内容片段的附加信息的字段。

这些[帮助程序字段](#helper-fields)使用前缀 `_` 标记，用于区分哪些字段由用户定义，哪些字段为自动生成。

#### 路径 {#path}

路径字段用作 AEM GraphQL 中的标识符。它代表 AEM 存储库中内容片段资源的路径。此路径被选为内容片段的标识符，因为它：

* 在 AEM 中唯一
* 可以轻松地提取

以下代码显示基于内容片段模型创建的所有内容片段的路径 `Person`.

```graphql
{
  personList {
    items {
      _path
    }
  }
}
```

要检索特定类型的单个内容片段，您还必须先确定其路径。 例如：

```graphql
{
  authorByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      firstName
      name
    }
  }
}
```

请参阅[示例查询 – 一个特定城市片段](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)。

#### 元数据 {#metadata}

通过 GraphQL，AEM 还可以公开内容片段的元数据。元数据是描述内容片段的信息，如下所示：

* 内容片段的标题
* 缩略图路径
* 内容片段的描述
* 以及创建日期，等等。

由于元数据通过架构编辑器生成，因此没有特定结构，所以实施了 `TypedMetaData` GraphQL 类型以公开内容片段的元数据。此 `TypedMetaData` 公开按以下标量类型分组的信息：

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

例如，如果您要检索内容片段的标题，此属性是字符串属性，因此您将查询所有字符串元数据：

要查询元数据，请执行以下操作：

```graphql
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
>例如，通过调用 `stringMetadata` 字段中，您将收到一个数组，其中包含作为存储在存储库中的所有元数据 `String`. 如果你打电话 `stringArrayMetadata`，您将收到一个数组，其中包含存储在存储库中的所有元数据，其名称为 `String[]`.

请参阅[元数据的示例查询 – 列出标题为 GB 的奖励的元数据](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-metadata-awards-gb)。

#### 变体 {#variations}

`_variations` 字段已实施以简化查询内容片段具有的变体。例如：

```graphql
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _variations
    }
  }
}
```

>[!NOTE]
>
>此 `_variations` 字段不包含 `master` 变体，从技术上讲，为原始数据(称为 *母版* （在UI中）不被视为显式变量。

请参阅[示例查询 – 具有指定变体的所有城市](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-cities-named-variation)。

>[!NOTE]
>
>如果内容片段不存在给定的变量，则原始数据（也称为主控变量）会作为（回退）默认值返回。

<!--
## Security Considerations {#security-considerations}
-->

## GraphQL 变量 {#graphql-variables}

GraphQL 允许在查询中放入变量。有关详细信息，请参阅 [GraphQL 的变量文档。](https://graphql.org/learn/queries/#variables)

例如，要获取具有特定变体的类型为 `Article` 的所有内容片段，您可以在 GraphiQL 中指定变量 `variation`。

![GraphQL 变量](assets/cfm-graphqlapi-03.png "GraphQL 变量")

```graphql
### query
query GetArticlesByVariation($variation: String!) {
    articleList(variation: $variation) {
        items {
            _path
            author
            _variations
        }
    }
}
 
### in query variables
{
    "variation": "uk"
}
```

## GraphQL 指令 {#graphql-directives}

在GraphQL中，可以根据变量更改查询，这称为GraphQL指令。

例如，您可在针对所有 `AdventureModels`、基于变量 `includePrice` 的查询中包含 `adventurePrice` 字段。

![GraphQL 指令](assets/cfm-graphqlapi-04.png "GraphQL 指令")

```graphql
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

最原子的部分是可以应用于特定字段内容的单个表达式。它将字段的内容与给定的常量值进行比较。

例如，以下表达式会将字段的内容与值进行比较 `some text`，如果内容等于该值，则成功。 否则，表达式将失败。：

```graphql
{
  value: "some text"
  _op: EQUALS
}
```

以下运算符可用于将字段与特定值进行比较：

| 运算符 | 类型 | 如果...，则表达式成功 |
|--- |--- |--- |
| `EQUALS` | `String`、`ID`、`Boolean` | ...该值与该字段的内容相同 |
| `EQUALS_NOT` | `String`、`ID` | ... 该值与该字段的内容&#x200B;*不*&#x200B;完全相同 |
| `CONTAINS` | `String` | ...字段的内容包含值(`{ value: "mas", _op: CONTAINS }` 匹配 `Christmas`， `Xmas`， `master`， ...) |
| `CONTAINS_NOT` | `String` | ... 字段的内容&#x200B;*不*&#x200B;包含值 |
| `STARTS_WITH` | `ID` | ... ID以特定值开头(`{ value: "/content/dam/", _op: STARTS_WITH` 匹配 `/content/dam/path/to/fragment`，但不匹配 `/namespace/content/dam/something` |
| `EQUAL` | `Int`、`Float` | ...该值与该字段的内容相同 |
| `UNEQUAL` | `Int`、`Float` | ... 该值与该字段的内容&#x200B;*不*&#x200B;完全相同 |
| `GREATER` | `Int`、`Float` | ... 字段内容大于值 |
| `GREATER_EQUAL` | `Int`、`Float` | ... 字段的内容大于或等于值 |
| `LOWER` | `Int`、`Float` | ... 字段内容小于值 |
| `LOWER_EQUAL` | `Int`、`Float` | ... 字段的内容小于或等于值 |
| `AT` | `Calendar`, `Date`, `Time` | ...字段的内容与值相同（包括时区设置） |
| `NOT_AT` | `Calendar`、`Date`、`Time` | ... 字段的内容与值&#x200B;*不*&#x200B;完全相同 |
| `BEFORE` | `Calendar`、`Date`、`Time` | ... 值表示的时间点在字段内容表示的时间点之前 |
| `AT_OR_BEFORE` | `Calendar`、`Date`、`Time` | ... 值表示的时间点在字段内容表示的时间点之前或与之相同 |
| `AFTER` | `Calendar`、`Date`、`Time` | ... 值表示的时间点在字段内容表示的时间点之后 |
| `AT_OR_AFTER` | `Calendar`, `Date`, `Time` | ... 值表示的时间点在字段内容表示的时间点之后或与之相同 |

某些类型还允许您指定其他选项来修改表达式的计算方式：

| 选项 | 类型 | 描述 |
|--- |--- |--- |
| `_ignoreCase` | `String` | 忽略字符串的大小写，例如 `time` 匹配 `TIME`， `time`， `tImE`， ... |
| `_sensitiveness` | `Float` | 允许有一定的余地，将 `float` 值视为相同（以解决由于 `float` 值的内部表示引起的技术限制；应该避免，因为此选项可能有负面影响对性能的影响 |

表达式可以在逻辑运算符 (`_logOp`) 的帮助下组合成一个集合：

* `OR`  — 如果至少有一个表达式成功，则表达式集将成功
* `AND`  — 如果所有表达式都成功，则表达式集将成功（默认值）

每个字段都可以通过其自己的一组表达式进行过滤。过滤器参数中提到的所有字段的表达式集最终将由其自己的逻辑运算符组合。

过滤器定义（作为 `filter` 参数传递给查询）包含：

* 每个字段的子定义(可以通过其名称访问该字段，例如， `lastName` 的过滤器中的字段 `lastName` 字段类型)
* 每个子定义包含 `_expressions` 数组，提供表达式集和 `_logOp` 定义表达式应与之组合的逻辑运算符的字段
* 每个表达式由值（`value` 字段）和运算符（`_operator` 字段）定义，字段的内容应该与之进行比较

您可以省略 `_logOp` 如果要将项目与 `AND` 和 `_operator` 如果您要检查是否相等，因为这些值是默认值。

以下示例演示了一个完整的查询，该查询过滤所有 `lastName` 为 `Provo` 或包含 `sjö` 的人员，与大小写无关：

```graphql
{
  authorList(filter: {
    lastname: {
      _logOp: OR
      _expressions: [
        {
          value: "sjö",
          _operator: CONTAINS,
          _ignoreCase: true
        },
        {
          value: "Provo"
        }
      ]
    }
  }) {
    items {
      lastName
      firstName
    }
  }
}
```

虽然您也可以对嵌套字段进行筛选，但不建议这样做，因为这可能会导致性能问题。

有关更多示例，请参阅：

* [GraphQL for AEM 扩展](#graphql-extensions)的详细信息

* [使用此示例内容和结构的示例查询](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#graphql-sample-queries-sample-content-fragment-structure)

   * 以及准备用于示例查询的[示例内容和结构](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#content-fragment-structure-graphql)

* [基于 WKND 项目的示例查询](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-queries-using-wknd-project)

## 排序 {#sorting}

>[!NOTE]
>
>为获得最佳性能，请考虑 [在GraphQL筛选中更新用于分页和排序的内容片段](/help/sites-developing/headless/graphql-api/graphql-optimized-filtering-content-update.md).

此功能让您根据指定字段对查询结果进行排序。

排序标准：

* 是以逗号分隔的值列表，表示字段路径
   * 列表中的第一个字段定义主要排序顺序
      * 如果主要排序标准的两个值相等，则使用第二个字段
      * 如果前两个标准相等，则使用第三个字段，依此类推。
   * 点分符号，即field1.subfield.subfield等……
* 带有可选的订单方向
   * ASC（升序）或 DESC（降序）；作为默认 ASC 应用
   * 可以按字段指定方向；这种能力意味着您可以对一个字段按升序排序，对另一个字段按降序排序（名称、名字DESC）

例如：

```graphql
query {
  authorList(sort: "lastName, firstName") {
    items {
      firstName
      lastName
    }
  }
}
```

也可以：

```graphql
{
  authorList(sort: "lastName DESC, firstName DESC") {
    items {
        lastName
        firstName
    }
  }
}
```

您还可以使用 `nestedFragmentname.fieldname` 的格式对嵌套片段中的字段进行排序。

>[!NOTE]
>
>此格式可能会对性能产生负面影响。

例如：

```graphql
query {
  articleList(sort: "authorFragment.lastName")  {
    items {
      title
      authorFragment {
        firstName
        lastName
        birthDay
      }
      slug
    }
  }
}
```

## 分页 {#paging}

>[!NOTE]
>
>为获得最佳性能，请考虑 [在GraphQL筛选中更新用于分页和排序的内容片段](/help/sites-developing/headless/graphql-api/graphql-optimized-filtering-content-update.md).

此功能让您对返回列表的查询类型执行分页。提供了两种方法：

* 在 `List` 查询中的 `offset` 和 `limit`
* 在 `Paginated` 查询中的 `first` 和 `after`

### 列表查询 – 偏移和限制 {#list-offset-limit}

在 `...List` 查询中，您可以使用 `offset` 和 `limit` 返回特定的结果子集：

* `offset`：指定要返回的第一个数据集
* `limit`：指定返回的最大数据集数

例如，要输出最多包含五篇文章的结果页面，从&#x200B;*完整*&#x200B;结果列表中的第五篇文章开始：

```graphql
query {
   articleList(offset: 5, limit: 5) {
    items {
      authorFragment {
        lastName
        firstName
      }
    }
  }
}
```

<!-- When available link to BP and replace "JCR query level" with a more neutral term. -->

<!-- When available link to BP and replace "JCR query result set" with a more neutral term. -->

>[!NOTE]
>
>* 分页需要稳定的排序顺序才能在请求同一结果集的不同页面的多个查询中正常工作。默认情况下，它使用结果集中每个项目的存储库路径来确保顺序始终相同。 如果使用不同的排序顺序，并且无法在JCR查询级别进行排序，则会对性能产生负面影响。 原因在于，在确定页面之前，必须将整个结果集加载到内存中。
>
>* 偏移量越高，从完整的JCR查询结果集中跳过项目所需的时间就越多。 大型结果集的替代解决方案是使用带有 `first` 和 `after` 方法的分页查询。

### 分页查询 – 先和后 {#paginated-first-after}

`...Paginated` 查询类型重用了大部分 `...List` 查询类型功能（过滤、排序），但没有使用 `offset`/`limit` 参数，它使用 `first`/`after` 参数，正如 [GraphQL 光标连接规范](https://relay.dev/graphql/connections.htm)所定义。您可以在 [GraphQL 介绍](https://graphql.org/learn/pagination/#pagination-and-edges) 中找到不太正式的介绍。

* `first`：`n`要返回的第一个项目。
默认为 `50`。最大值为 `100`。
* `after`：确定请求页面开始的光标。光标所表示的项目不包含在结果集中。 项目的光标由 `cursor` 字段 `edges` 结构。

例如，输出包含最多五次冒险的结果页面，从&#x200B;*完整*&#x200B;结果列表中的给定光标项开始：

```graphql
query {
    adventurePaginated(first: 5, after: "ODg1MmMyMmEtZTAzMy00MTNjLThiMzMtZGQyMzY5ZTNjN2M1") {
        edges {
          cursor
          node {
            title
          }
        }
        pageInfo {
          endCursor
          hasNextPage
        }
    }
}
```

<!-- When available link to BP -->
<!-- Due to internal technical constraints, performance will degrade if sorting and filtering is applied on nested fields. Therefore it is recommended to use filter/sort fields stored at root level. For more information, see the [Best Practices document](link). -->

>[!NOTE]
>
>* 默认情况下，分页使用表示排序片段的存储库节点的UUID，以确保结果的顺序始终相同。 当使用 `sort` 时，隐式使用 UUID 以确保唯一排序；即使对于具有相同排序键的两个项目，也可以使用。
>
>* 由于内部技术限制，如果对嵌套字段应用排序和筛选，则性能会降低。 因此，请使用存储在根级别的筛选器/排序字段。 如果要查询大型分页结果集，也建议使用此方法。

## GraphQL 持久化查询 - 在 Dispatcher 中启用缓存 {#graphql-persisted-queries-enabling-caching-dispatcher}

>[!CAUTION]
>
>如果在 Dispatcher 中启用了缓存，则不需要 [CORS 筛选条件](#cors-filter)，并且可以忽略该部分。

默认情况下，Dispatcher 中未启用持久化查询的缓存。无法实施默认启用，因为对多个源使用 CORS（跨源资源共享）的客户需要检查并（可能需要）更新其 Dispatcher 配置。

>[!NOTE]
>
>Dispatcher 不会缓存 `Vary` 标头。
>
>可以在 Dispatcher 中启用其他 CORS 相关标头的缓存，但如果存在多个 CORS 源，则可能不够。

### 启用持久化查询的缓存 {#enable-caching-persisted-queries}

要启用持久化查询的缓存，请定义 Dispatcher 变量 `CACHE_GRAPHQL_PERSISTED_QUERIES`：

1. 将该变量添加到 Dispatcher 文件 `global.vars` 中：

   ```xml
   Define CACHE_GRAPHQL_PERSISTED_QUERIES
   ```

>[!NOTE]
>
>为了符合 [Dispatcher 对可缓存文档的要求](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/troubleshooting/dispatcher-faq.html#how-does-the-dispatcher-return-documents%3F)，Dispatcher 将后缀 `.json` 添加到所有持久化查询 URL，以便能够缓存结果。
>
>在启用持久化查询缓存后，将通过重写规则添加此后缀。

### Dispatcher 中的 CORS 配置 {#cors-configuration-in-dispatcher}

使用 CORS 请求的客户可能需要在 Dispatcher 中查看和更新其 CORS 配置。

* `Origin` 标头不得通过 Dispatcher 传递到 AEM 发布：
   * 检查 `clientheaders.any` 文件。
* 相反，必须在 Dispatcher 级别为允许的源评估 CORS 请求。此方法还可确保在所有情况下，在一个位置正确设置 CORS 相关标头。
   * 应将此类配置添加到 `vhost` 文件。下面提供了一个示例配置；为简单起见，仅提供了 CORS 相关部分。您可以根据特定用例进行调整。

  ```xml
  <VirtualHost *:80>
     ServerName "publish"
  
     # ...
  
     <IfModule mod_headers.c>
         Header add X-Vhost "publish"
  
          ################## Start of the CORS specific configuration ##################
  
          SetEnvIfExpr "req_novary('Origin') == ''"  CORSType=none CORSProcessing=false
          SetEnvIfExpr "req_novary('Origin') != ''"  CORSType=cors CORSProcessing=true CORSTrusted=false
  
          SetEnvIfExpr "req_novary('Access-Control-Request-Method') == '' && %{REQUEST_METHOD} == 'OPTIONS' && req_novary('Origin') != ''  " CORSType=invalidpreflight CORSProcessing=false
          SetEnvIfExpr "req_novary('Access-Control-Request-Method') != '' && %{REQUEST_METHOD} == 'OPTIONS' && req_novary('Origin') != ''  " CORSType=preflight CORSProcessing=true CORSTrusted=false
          SetEnvIfExpr "req_novary('Origin') -strcmatch 'https://%{HTTP_HOST}*'"  CORSType=samedomain CORSProcessing=false
  
          # For requests that require CORS processing, check if the Origin can be trusted
          SetEnvIfExpr "%{HTTP_HOST} =~ /(.*)/ " ParsedHost=$1
  
          ################## Adapt the regex to match CORS origin for your environment
          SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*.your-domain.tld(:\d+)?$)#" CORSTrusted=true
  
          # Extract the Origin header 
          SetEnvIfNoCase ^Origin$ ^https://(.*)$ CORSTrustedOrigin=https://$1
  
          # Flush If already set
          Header unset Access-Control-Allow-Origin
          Header unset Access-Control-Allow-Credentials
  
          # Trusted
          Header always set Access-Control-Allow-Credentials "true" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Origin "%{CORSTrustedOrigin}e" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Methods "GET" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Max-Age 1800 "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Headers "Origin, Accept, X-Requested-With, Content-Type, Access-Control-Request-Method, Access-Control-Request-Headers" "expr=reqenv('CORSTrusted') == 'true'"
  
          # Non-CORS or Not Trusted
          Header unset Access-Control-Allow-Credentials "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Allow-Origin "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Allow-Methods "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Max-Age "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
  
          # Always vary on origin, even if its not there.
          Header merge Vary Origin
  
          # CORS - send 204 for CORS requests which are not trusted
          RewriteCond expr "reqenv('CORSProcessing') == 'true' && reqenv('CORSTrusted') == 'false'"
          RewriteRule "^(.*)" - [R=204,L]
  
          ################## End of the CORS specific configuration ##################
  
     </IfModule>
  
     <Directory />
  
         # ...
  
     </Directory>
  
     # ...
  
  </VirtualHost>
  ```

## GraphQL for AEM – 执行摘要 {#graphql-extensions}

使用 GraphQL for AEM 的查询基本处理遵循标准 GraphQL 规范。对于使用AEM的GraphQL查询，有几个扩展：

* 如果您需要单个结果：
   * 使用模型名称；例如，city

* 如果您需要结果列表：
   * 将 `List` 添加到模型名称；例如，`cityList`
   * 请参阅[示例查询 – 关于所有城市的所有信息](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-all-information-all-cities)

  稍后您可以：

   * [对结果进行排序](#sorting)

      * `ASC` : 升序
      * `DESC` : 降序

   * 使用以下任一方法返回一页结果：

      * [带有偏移和限制的列表查询](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#list-offset-limit)
      * [带有“先”和“后”的分页查询](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#paginated-first-after)
   * 请参阅[示例查询 – 关于所有城市的所有信息](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-all-information-all-cities)

* 过滤器 `includeVariations` 包含在 `List` 查询类型。 要在查询结果中检索内容片段变体，请 `includeVariations` 筛选器必须设置为 `true`.

  >[!CAUTION]
  >过滤器 `includeVariations` 不能与系统生成的字段一起使用 `_variation`.

* 如果您希望使用逻辑 OR：
   * 使用 ` _logOp: OR`
   * 请参阅[示例查询 – 所有名为“Jobs”或“Smith”的人](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-all-persons-jobs-smith)

* 逻辑 AND 也可使用，不过（通常）是隐式的

* 您可以查询与内容片段模型中字段对应的字段名称
   * 请参阅[示例查询 – 公司的 CEO 和员工的完整详细信息](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-full-details-company-ceos-employees)

* 除了来自您模型的字段以外，还有一些系统生成的字段（以下划线为前缀）：

   * 对于内容：

      * `_locale`：用于显示语言；基于语言管理器
         * 请参阅[给定区域设置的多个内容片段的示例查询](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-wknd-multiple-fragments-given-locale)

      * `_metadata`：用于显示片段的元数据
         * 请参阅[元数据的示例查询 – 列出标题为 GB 的奖励的元数据](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-metadata-awards-gb)

      * `_model`：允许查询内容片段模型（路径和标题）
         * 请参阅[来自模型的内容片段模型的示例查询](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-wknd-content-fragment-model-from-model)

      * `_path`：存储库中内容片段的路径
         * 请参阅[示例查询 – 一个特定城市片段](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)

      * `_reference`：用于显示引用，包括富文本编辑器中的内联引用
         * 请参阅[具有预获取引用的多个内容片段的示例查询](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-wknd-multiple-fragments-prefetched-references)

      * `_variation`：用于显示内容片段中的特定变体

        >[!NOTE]
        >
        >如果内容片段不存在给定的变量，则主控变量会作为（回退）默认值返回。

        >[!CAUTION]
        >系统生成的字段 `_variation` 不能与过滤器 `includeVariations` 一起使用。

         * 请参阅[示例查询 – 具有指定变体的所有城市](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-cities-named-variation)

      * `_tags` ：用于显示包含标记的内容片段或变体的ID；此列表由一系列 `cq:tags` 标识符。

         * 请参阅[示例查询 - 标记为“城市度假”的所有城市的名称](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-names-all-cities-tagged-city-breaks)
         * 请参阅[附加了特定标签的给定模型的内容片段变体的示例查询](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-wknd-fragment-variations-given-model-specific-tag)

        >[!NOTE]
        >
        >还可以通过列出内容片段的元数据来查询标签。

   * 以及操作：

      * `_operator`：应用特定运算符；`EQUALS`、`EQUALS_NOT`、`GREATER_EQUAL`、`LOWER`、`CONTAINS`、`STARTS_WITH`
         * 请参阅[示例查询 – 所有名字不是“Jobs”的人](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-all-persons-not-jobs)
         * 请参阅[示例查询 – `_path` 以特定前缀开头的所有冒险](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-wknd-all-adventures-cycling-path-filter)

      * `_apply`：用于应用特定条件，例如 `AT_LEAST_ONCE`
         * 请参阅[示例查询 – 筛选数组中必须至少出现一次的项](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-array-item-occur-at-least-once)

      * `_ignoreCase`：在查询时忽略大小写
         * 请参阅[示例查询 – 名称中包含 SAN 的所有城市，不考虑大小写](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-all-cities-san-ignore-case)

* 支持 GraphQL 合并类型：

   * 使用 `... on`
      * 请参阅[具有内容引用的特定模型的内容片段示例查询](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-wknd-fragment-specific-model-content-reference)

* 在查询嵌套片段时回退：

   * 如果请求的变体在嵌套片段中不存在，则 **母版** 变量已返回。

### CORS 筛选条件 {#cors-filter}

>[!CAUTION]
>
>如果[已在 Dispatcher 中启用缓存](#graphql-persisted-queries-enabling-caching-dispatcher)，则不需要 CORS 筛选条件，因此可忽略此部分。

>[!NOTE]
>
>有关AEM中CORS资源共享策略的详细概述，请参阅 [了解跨源资源共享(CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=zh-Hans#understand-cross-origin-resource-sharing-(cors)).

要访问GraphQL端点，请在客户Git存储库中配置CORS策略。 此配置可通过为一个或多个所需端点添加相应的OSGi CORS配置文件来完成。

此配置必须指定可信网站来源 `alloworigin` 或 `alloworiginregexp` 必须向其授予访问权限。

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

除了CORS配置外，还必须配置反向链接筛选条件以允许从第三方主机进行访问。

此过滤器可通过添加适当的OSGi反向链接过滤器配置文件来完成，该配置文件可以：

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
>* 不使用通配符 [*] 语法；此功能禁用对GraphQL端点的经过身份验证的访问，还会将其向全世界公开。

>[!CAUTION]
>
>所有 GraphQL [架构](#schema-generation)（派生自&#x200B;**已启用**&#x200B;的内容片段模型）可通过 GraphQL 端点读取。
>
>此功能意味着您必须确保没有敏感数据可用，因为这样可能会泄露这些数据。 例如，它包括可在模型定义中作为字段名称显示的信息。

## 身份验证 {#authentication}

请参阅[对内容片段的远程 AEM GraphQL 查询的身份验证](/help/sites-developing/headless/graphql-api/graphql-authentication-content-fragments.md)。

## 常见问题解答 {#faqs}

出现的问题：

1. **问**：*适用于 AEM 的 GraphQL API 与查询生成器 API 有何不同？*

   * **答**：
*AEM GraphQL API 提供了对 JSON 输出的全面控制，是用于查询内容的行业标准。
将来，AEM计划投资于AEM GraphQL API。*&quot;

## 教程 – AEM Headless 和 GraphQL 快速入门 {#tutorial}

正在寻找实践教程？请查看 [AEM Headless 和 GraphQL 快速入门](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=zh-Hans)端到端教程，其中说明了在 Headless CMS 场景中，如何使用 AEM GraphQL API 构建和公开内容并由外部应用程序使用。
