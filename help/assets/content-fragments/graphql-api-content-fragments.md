---
title: AEM GraphQL API，用于内容片段
description: 了解如何将Adobe Experience Manager(AEM)中的内容片段与AEM GraphQL API结合使用来交付无头内容。
feature: Content Fragments,GraphQL API
exl-id: beae1f1f-0a76-4186-9e58-9cab8de4236d
source-git-commit: b5cf18d8e83786a23005aadf8aafe43d006a2e67
workflow-type: tm+mt
source-wordcount: '3919'
ht-degree: 1%

---

# AEM GraphQL API，用于内容片段 {#graphql-api-for-use-with-content-fragments}

了解如何将Adobe Experience Manager(AEM)中的内容片段与AEM GraphQL API结合使用来交付无头内容。

与内容片段一起使用的AEM GraphQL API在很大程度上基于标准的开源GraphQL API。

在AEM中使用GraphQL API，可以在无头CMS实施中高效地将内容片段交付到JavaScript客户端：

* 避免像使用REST一样使用迭代API请求，
* 确保投放仅限于特定要求，
* 允许批量交付作为单个API查询的响应渲染所需的确切内容。

>[!NOTE]
>
>GraphQL当前用于Adobe Experience Manager(AEM)中的两个（单独）方案：
>
>* [AEM Commerce通过GraphQL从商务平台使用数据](/help/commerce/cif/integrating/magento.md)。
>* AEM内容片段可与AEM GraphQL API（一种基于标准GraphQL的自定义实施）一起使用，来提供结构化内容以供在您的应用程序中使用。


## GraphQL API {#graphql-api}

GraphQL是：

* &quot;*...API的查询语言以及用于使用现有数据执行这些查询的运行时。 GraphQL提供了API中数据的完整且可理解的描述，使客户能够准确地询问自己需要的内容，无需再做任何事情，更便于随着时间的推移改进API，并支持功能强大的开发人员工具。*&quot;

   请参阅[GraphQL.org](https://graphql.org)

* &quot;*...灵活API层的开放规范。 将GraphQL置于现有后端上，以比以往更快的速度构建产品…….*&quot;。

   请参阅[浏览GraphQL](https://www.graphql.com)。

* *&quot;。..一种数据查询语言和规范，由Facebook于2012年在内部开发，后于2015年公开开放。它为基于REST的体系结构提供了替代方案，目的是提高开发人员的工作效率并最大限度地减少数据传输量。 GraphQL由数百个大小各异的组织在生产中使用……&quot;*

   请参阅[GraphQL Foundation](https://foundation.graphql.org/)。

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all of the tools they need to understand and adopt GraphQL.*". 
-->

有关GraphQL API的更多信息，请参阅以下部分（包括许多其他资源）：

* 在[graphql.org](https://graphql.org):

   * [GraphQL简介](https://graphql.org/learn)

   * [GraphQL规范](http://spec.graphql.org/)

* 在[graphql.com](https://graphql.com):

   * [指南](https://www.graphql.com/guides/)

   * [教程](https://www.graphql.com/tutorials/)

   * [案例研究](https://www.graphql.com/case-studies/)

用于AEM的GraphQL实施基于标准的GraphQL Java库。 请参阅：

* [graphQL.org - Java](https://graphql.org/code/#java)

* [GitHub上的GraphQL Java](https://github.com/graphql-java)

### GraphQL术语 {#graphql-terminology}

GraphQL使用以下代码：

* **[查询](https://graphql.org/learn/queries/)**

* **[架构和类型](https://graphql.org/learn/schema/)**:

   * 架构由AEM基于内容片段模型生成。
   * 使用您的架构，GraphQL显示GraphQL for AEM实施允许的类型和操作。

* **[字段](https://graphql.org/learn/queries/#fields)**

* **[GraphQL端点](#graphql-aem-endpoint)**
   * AEM中响应GraphQL查询并提供对GraphQL架构的访问权限的路径。

   * 有关更多详细信息，请参阅[启用GraphQL端点](#enabling-graphql-endpoint)。

请参阅[(GraphQL.org)GraphQL](https://graphql.org/learn/)简介，以了解详细信息，包括[最佳实践](https://graphql.org/learn/best-practices/)。

### GraphQL查询类型 {#graphql-query-types}

通过GraphQL，您可以执行查询以返回以下任一值：

* **单个条目**

* **[条目列表](https://graphql.org/learn/schema/#lists-and-non-null)**

您还可以执行以下操作：

* [已缓存的持久化查询](#persisted-queries-caching)

>[!NOTE]
>可以使用[GraphiQL IDE](#graphiql-interface)测试和调试GraphQL查询。

## 用于AEM端点的GraphQL {#graphql-aem-endpoint}

端点是用于访问GraphQL for AEM的路径。 使用此路径，您（或您的应用程序）可以：

* 访问GraphQL模式，
* 发送GraphQL查询，
* 接收响应（对您的GraphQL查询）。

AEM中有两种类型的端点：

* 全局
   * 可供所有站点使用。
   * 此端点可以使用所有站点配置（在[配置浏览器](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)中定义）中的所有内容片段模型。
   * 如果有任何内容片段模型应在站点配置之间共享，则应在全局站点配置下创建这些模型。
* 站点配置：
   * 对应于在[配置浏览器](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)中定义的站点配置。
   * 特定于指定的站点/项目。
   * 特定于站点配置的端点将使用该特定站点配置中的内容片段模型以及全局站点配置中的内容片段模型。

>[!CAUTION]
>
>内容片段编辑器允许一个站点配置的内容片段引用另一个站点配置的内容片段（通过策略）。
>
>在这种情况下，并非所有内容都可以使用特定于Sites配置的端点进行检索。
>
>内容作者应控制此情景；例如，考虑将共享的内容片段模型置于全局站点配置下可能会非常有用。

用于AEM全局端点的GraphQL的存储库路径是：

`/content/cq:graphql/global/endpoint`

您的应用程序可以在请求URL中对其使用以下路径：

`/content/_cq_graphql/global/endpoint.json`

要为AEM启用GraphQL的端点，您需要：

* [启用GraphQL端点](#enabling-graphql-endpoint)
* [发布GraphQL端点](#publishing-graphql-endpoint)

### 启用GraphQL端点 {#enabling-graphql-endpoint}

要启用GraphQL端点，您首先需要具有适当的配置。 请参阅[内容片段 — 配置浏览器](/help/assets/content-fragments/content-fragments-configuration-browser.md)。

>[!CAUTION]
>
>如果[对内容片段模型的使用尚未启用](/help/assets/content-fragments/content-fragments-configuration-browser.md)，则&#x200B;**创建**&#x200B;选项将不可用。

要启用相应的端点，请执行以下操作：

1. 导航到&#x200B;**工具**、**资产**，然后选择&#x200B;**GraphQL**。
1. 选择&#x200B;**创建**。
1. 将打开&#x200B;**新建GraphQL端点**&#x200B;对话框。 您可以在此指定：
   * **名称**:端点名称；您可以输入任何文本。
   * **使用**&#x200B;提供的GraphQL模式：使用下拉菜单选择所需的站点/项目。

   >[!NOTE]
   >
   >对话框中显示以下警告：
   >
   >* *如果不对 GraphQL 端点仔细管理，则可能会带来数据安全和性能问题。请确保在创建端点后设置适当的权限。*


1. 使用&#x200B;**创建**&#x200B;进行确认。
1. **后续步骤**&#x200B;对话框将提供指向安全控制台的直接链接，以便您能够确保新创建的端点具有适当的权限。

   >[!CAUTION]
   >
   >每个人都可以访问该端点。 这可能会（尤其是在发布实例上）带来安全问题，因为GraphQL查询可能会给服务器带来沉重的负载。
   >
   >您可以在端点上设置与用例相应的ACL。

### 发布GraphQL端点 {#publishing-graphql-endpoint}

选择新端点和&#x200B;**Publish**&#x200B;以使其在所有环境中都完全可用。

>[!CAUTION]
>
>每个人都可以访问该端点。
>
>在发布实例上，这可能会引起安全问题，因为GraphQL查询可能会给服务器带来沉重的负载。
>
>您必须在端点上设置与用例相适的ACL。

## GraphiQL接口 {#graphiql-interface}

标准[GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql)接口的实现可与AEM GraphQL一起使用。 这可以是[与AEM](#installing-graphiql-interface)一起安装的。

>[!NOTE]
>
>GraphiQL已绑定全局端点（并且不适用于特定Sites配置的其他端点）。

此界面允许您直接输入和测试查询。

例如：

* `http://localhost:4502/content/graphiql.html`

这提供了语法突出显示、自动完成、自动建议等功能，以及历史记录和在线文档：

![GraphiQL接](assets/cfm-graphiql-interface.png "口GraphiQL接口")

### 安装AEM GraphiQL界面 {#installing-graphiql-interface}

<!-- 6.5.10.0??? -->

GraphiQL用户界面可以通过专用包安装在AEM上：[GraphiQL内容包v0.0.6(2021.3)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-graphql/graphiql-0.0.6.zip)包。

>[!NOTE]
>
>提供的包与AEM 6.5.10.0和AEM as a A A Device完全兼容。

## 创作和发布环境的用例 {#use-cases-author-publish-environments}

用例取决于AEM环境的类型：

* 发布环境；用于：
   * JS应用程序的查询数据（标准用例）

* 创作环境；用于：
   * 查询数据以用于“内容管理目的”：
      * AEM中的GraphQL当前是只读API。
      * REST API可用于CR(u)D操作。

## 权限 {#permission}

访问资产所需的权限。

## 模式生成 {#schema-generation}

GraphQL是一种强类型API，这意味着数据必须按类型清晰地结构和组织。

GraphQL规范提供了一系列关于如何创建用于查询特定实例上数据的强大API的准则。 要实现此目的，客户端需要获取[Schema](#schema-generation)，其中包含查询所需的所有类型。

对于内容片段，GraphQL架构（结构和类型）基于&#x200B;**Enabled** [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)及其数据类型。

>[!CAUTION]
>
>所有GraphQL架构（从已&#x200B;**Enabled**&#x200B;的内容片段模型派生）均可通过GraphQL端点读取。
>
>这意味着您需要确保没有可用的敏感数据，因为这些数据可能会以这种方式泄露；例如，这包括模型定义中可以显示为字段名称的信息。

例如，如果用户创建了名为`Article`的内容片段模型，则AEM会生成类型为`ArticleModel`的对象`article`。 此类型中的字段对应于模型中定义的字段和数据类型。

1. 内容片段模型：

   ![与GraphQLContent片段模型一起使](assets/cfm-graphqlapi-01.png "用的内容片段模型与GraphQL一起使用")

1. 相应的GraphQL模式（从GraphiQL自动文档中输出）：
   ![基于内容片段的GraphQL模式基于](assets/cfm-graphqlapi-02.png "内容片段模型的GraphQL模式")

   这表示生成的类型`ArticleModel`包含多个[字段](#fields)。

   * 其中三个受用户控制：`author`、`main`和`referencearticle`。

   * 其他字段由AEM自动添加，它们代表了提供特定内容片段相关信息的有用方法；在此示例中，`_path`、`_metadata`、`_variations`。 这些[帮助程序字段](#helper-fields)标有前面的`_`，以区分用户定义的内容和自动生成的内容。

1. 用户根据文章模型创建内容片段后，可以通过GraphQL查询该内容片段。 有关示例，请参阅[示例查询](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries)（基于[示例内容片段结构，以与GraphQL](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)一起使用）。

在用于AEM的GraphQL中，架构是灵活的。 这意味着每次创建、更新或删除内容片段模型时，都会自动生成该模型。 更新内容片段模型时，数据架构缓存也会刷新。

站点GraphQL服务监听（在后台）对内容片段模型所做的任何修改。 检测到更新后，只会重新生成模式的该部分。 这种优化节省了时间并提供了稳定性。

例如，如果您：

1. 安装包含`Content-Fragment-Model-1`和`Content-Fragment-Model-2`的包：

   1. 将生成`Model-1`和`Model-2`的GraphQL类型。

1. 然后，修改`Content-Fragment-Model-2`:

   1. 只有`Model-2` GraphQL类型会更新。

   1. 而`Model-1`将保持不变。

>[!NOTE]
>
>如果您想要通过REST API或其他方式对内容片段模型进行批量更新，请务必注意这一点。

该架构通过与GraphQL查询相同的端点提供，客户端会处理使用扩展`GQLschema`调用该架构的事实。 例如，对`/content/cq:graphql/global/endpoint.GQLschema`执行简单的`GET`请求，将导致输出具有Content-type的架构：`text/x-graphql-schema;charset=iso-8859-1`。

### 架构生成 — 未发布的模型 {#schema-generation-unpublished-models}

嵌套内容片段后，可能会发布父内容片段模型，但未发布引用的模型。

>[!NOTE]
>
>AEM UI可阻止发生这种情况，但如果以编程方式或通过内容包进行发布，则可能会发生这种情况。

发生此情况时，AEM会为父内容片段模型生成一个&#x200B;*不完整的*&#x200B;架构。 这意味着从架构中删除依赖于未发布模型的片段引用。

## 字段 {#fields}

架构内有两个基本类别的单个字段：

* 生成的字段。

   选择的[字段类型](#field-types)用于根据您配置内容片段模型的方式创建字段。 字段名称取自&#x200B;**数据类型**&#x200B;的&#x200B;**属性名称**&#x200B;字段。

   * 还需要考虑&#x200B;**Render As**&#x200B;属性，因为用户可以配置某些数据类型；例如，作为单行文本或多字段。

* AEM的GraphQL还会生成许多[帮助程序字段](#helper-fields)。

   这些参数用于标识内容片段，或获取有关内容片段的更多信息。

### 字段类型 {#field-types}

用于AEM的GraphQL支持类型列表。 所有支持的内容片段模型数据类型和相应的GraphQL类型均表示：

| 内容片段模型 — 数据类型 | GraphQL类型 | 描述 |
|--- |--- |--- |
| 单行文本 | 字符串， [字符串] |  用于简单字符串，如作者名称、位置名称等。 |
| 多行文本 | 字符串 |  用于输出文本，如文章的正文 |
| 数字 |  浮点， [浮点] | 用于显示浮点数和正则数 |
| 布尔型 |  布尔型 |  用于显示复选框→简单true/false语句 |
| 日期和时间 | 日历 |  用于以ISO 8086格式显示日期和时间。 根据所选类型，AEM GraphQL中可以使用三种类型：`onlyDate`、`onlyTime`、`dateTime` |
| 枚举 |  String |  用于显示在模型创建时定义的选项列表中的选项 |
|  标记 |  [String] |  用于显示表示AEM中所用标记的字符串列表 |
| 内容引用 |  字符串 |  用于在AEM中显示指向其他资产的路径 |
| 片段引用 |  *模型类型* |  用于引用在创建模型时定义的特定模型类型的另一个内容片段 |

### 帮助程序字段 {#helper-fields}

除了用户生成字段的数据类型之外，AEM的GraphQL还会生成许多&#x200B;*帮助程序*&#x200B;字段，以帮助识别内容片段，或提供有关内容片段的其他信息。

#### 路径 {#path}

路径字段用作GraphQL中的标识符。 它表示内容片段资产在AEM存储库中的路径。 我们选择了此作为内容片段的标识符，因为它：

* 在AEM中是唯一的，
* 很容易被取走。

以下代码将显示之前基于内容片段模型`Person`创建的所有内容片段的路径。

```xml
{
  personList {
    items {
      _path
    }
  }
}
```

要检索特定类型的单个内容片段，还需要先确定其路径。 例如：

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

请参阅[示例查询 — 单个特定城市片段](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)。

#### 元数据 {#metadata}

AEM还通过GraphQL公开内容片段的元数据。 元数据是描述内容片段的信息，例如内容片段的标题、缩略图路径、内容片段的描述、创建日期等。

由于元数据是通过架构编辑器生成的，因此没有特定结构，因此实施了`TypedMetaData` GraphQL类型以公开内容片段的元数据。 `TypedMetaData` 公开按以下标量类型分组的信息：

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

每个标量类型表示单个名称值对或名称值对数组，其中该对的值是其分组的类型。

例如，如果您要检索内容片段的标题，我们知道此属性是字符串属性，因此我们将查询所有字符串元数据：

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

如果查看生成的GraphQL架构，则可以查看所有元数据GraphQL类型。 所有型号类型具有相同的`TypedMetaData`。

>[!NOTE]
>
>**正常元数据和数组元数据之间的差异**
>请记住，`StringMetadata`和`StringArrayMetadata`都引用存储库中存储的内容，而不是如何检索它们。
>
>因此，例如，通过调用`stringMetadata`字段，您将收到存储库中存储的`String`所有元数据的数组，如果调用`stringArrayMetadata` ，您将收到存储库中存储的`String[]`所有元数据的数组。

请参阅[元数据查询示例 — 列出标题为GB](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb)的奖项的元数据。

#### 变量 {#variations}

`_variations`字段已实施，以简化对内容片段所包含变量的查询。 例如：

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _variations
    }
  }
}
```

请参阅[示例查询 — 具有命名变体的所有城市](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation)。

<!--
## Security Considerations {#security-considerations}
-->

## GraphQL变量 {#graphql-variables}

GraphQL允许将变量置于查询中。 有关更多信息，请参阅[GraphQL variables](https://graphql.org/learn/queries/#variables)文档。

例如，要获取具有特定变量的`Article`类型的所有内容片段，可以在GraphiQL中指定变量`variation`。

![GraphQL变](assets/cfm-graphqlapi-03.png "量GraphQL变量")

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

## GraphQL指令 {#graphql-directives}

在GraphQL中，可以根据变量更改查询，称为GraphQL指令。

例如，您可以在查询中基于变量`includePrice`包含所有`AdventureModels`的`adventurePrice`字段。

![GraphQL指](assets/cfm-graphqlapi-04.png "令GraphQL指令")

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

您还可以在GraphQL查询中使用过滤来返回特定数据。

过滤使用基于逻辑运算符和表达式的语法。

例如，以下（基本）查询过滤名称为`Jobs`或`Smith`的所有人员：

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

* 用于AEM扩展的[GraphQL的详细信息](#graphql-extensions)

* [使用此示例内容和结构的示例查询](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries-sample-content-fragment-structure)

   * 和准备用于示例查询的[示例内容和结构](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)

* [基于WKND项目的示例查询](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-queries-using-wknd-project)

## GraphQL for AEM — 扩展摘要 {#graphql-extensions}

使用AEM的GraphQL查询的基本操作符合标准的GraphQL规范。 对于使用AEM的GraphQL查询，有以下扩展：

* 如果需要单个结果：
   * 使用模型名称；eg city

* 如果您希望得到结果列表：
   * 将`List`添加到模型名称；例如，`cityList`
   * 请参阅[示例查询 — 有关所有城市的所有信息](#sample-all-information-all-cities)

* 如果要使用逻辑OR:
   * use ` _logOp: OR`
   * 请参阅[示例查询 — 名称为“Jobs”或“Smith”](#sample-all-persons-jobs-smith)的所有人员

* 逻辑AND也存在，但是（通常）是隐式的

* 您可以查询与内容片段模型中的字段对应的字段名称
   * 请参阅[示例查询 — 公司CEO和员工的完整详细信息](#sample-full-details-company-ceos-employees)

* 除了模型中的字段之外，还有一些系统生成的字段（前面有下划线）：

   * 对于内容：

      * `_locale` :揭露语言；基于语言管理器
         * 请参阅[示例查询，以了解给定区域设置的多个内容片段](#sample-wknd-multiple-fragments-given-locale)
      * `_metadata` :显示片段的元数据
         * 请参阅[元数据查询示例 — 列出标题为GB](#sample-metadata-awards-gb)的奖项的元数据
      * `_model` :允许查询内容片段模型（路径和标题）
         * 请参阅[模型](#sample-wknd-content-fragment-model-from-model)中内容片段模型的示例查询
      * `_path` :存储库中内容片段的路径
         * 请参阅[示例查询 — 单个特定城市片段](#sample-single-specific-city-fragment)
      * `_reference` :显示引用；包括富文本编辑器中的内联引用
         * 请参阅[有关具有预取引用的多个内容片段的示例查询](#sample-wknd-multiple-fragments-prefetched-references)
      * `_variation` :以显示内容片段中的特定变量
         * 请参阅[示例查询 — 具有命名变体的所有城市](#sample-cities-named-variation)
   * 操作：

      * `_operator` :应用特定的运算符； `EQUALS`,  `EQUALS_NOT`,  `GREATER_EQUAL`,  `LOWER`,  `CONTAINS`  `STARTS_WITH`
         * 请参阅[示例查询 — 所有名称不为“Jobs”](#sample-all-persons-not-jobs)的人员
         * 请参阅[示例查询 — `_path`以特定前缀](#sample-wknd-all-adventures-cycling-path-filter)开头的所有冒险
      * `_apply` :适用特定条件；例如，   `AT_LEAST_ONCE`
         * 请参阅[示例查询 — 对具有项目且必须至少出现一次的数组进行筛选](#sample-array-item-occur-at-least-once)
      * `_ignoreCase` :在查询时忽略大小写
         * 请参阅[示例查询 — 名称中包含SAN的所有城市，而不考虑大小写](#sample-all-cities-san-ignore-case)









* 支持GraphQL并集类型：

   * 使用`... on`
      * 请参阅[有关具有内容引用的特定模型的内容片段的示例查询](#sample-wknd-fragment-specific-model-content-reference)

## 持久查询（缓存） {#persisted-queries-caching}

在准备包含POST请求的查询后，可以使用可由HTTP缓存或CDN缓存的GET请求执行该查询。

这是必需的，因为POST查询通常不会缓存，如果将GET与查询一起用作参数，则很有可能会使参数对HTTP服务和中间产品而言变得过大。

持久化查询必须始终使用与[相应Sites配置](#graphql-aem-endpoint)相关的端点；这样，它们就可以同时使用或同时使用这两种方法：

* 全局配置和端点
查询有权访问所有内容片段模型。
* 特定Sites配置和端点
为特定站点配置创建持久查询时，需要相应的特定于站点配置的端点（以提供对相关内容片段模型的访问）。
例如，要专门为WKND Sites配置创建持久查询，必须提前创建相应的WKND特定Sites配置和WKND特定端点。

>[!NOTE]
>
>有关更多详细信息，请参阅配置浏览器中的[启用内容片段功能](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser) 。
>
>需要启用&#x200B;**GraphQL持久性查询**，才能进行相应的站点配置。

例如，如果存在一个名为`my-query`的特定查询，该查询使用站点配置`my-conf`中的模型`my-model`:

* 您可以使用`my-conf`特定端点创建查询，然后该查询将保存如下：
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* 您可以使用`global`端点创建同一查询，但随后该查询将保存如下：
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>这两个查询是保存在不同路径下的不同查询。
>
>他们恰巧使用了相同的模型，但是通过不同的端点。


以下是保留给定查询所需的步骤：

1. 通过将查询发送到新端点URL `/graphql/persist.json/<config>/<persisted-label>`来准备查询。

   例如，创建一个持久查询：

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

1. 此时，请检查响应。

   例如，检查成功与否：

   ```xml
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. 然后，您可以通过获取URL `/graphql/execute.json/<shortPath>`来重播保留的查询。

   例如，使用持久查询：

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. 通过POSTing将持久查询更新为现有查询路径。

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

1. 创建封装的纯查询。

   例如：

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. 使用缓存控制创建封装的纯查询。

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

   * 使用POST进行复制：

      ```xml
      $curl -X POST   http://localhost:4502/bin/replicate.json \
        -H 'authorization: Basic YWRtaW46YWRtaW4=' \
        -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
        -F cmd=activate
      ```

   * 使用包：
      1. 创建新的包定义。
      1. 包括配置（例如`/conf/wknd/settings/graphql/persistentQueries`）。
      1. 构建包。
      1. 复制包。
   * 使用复制/分发工具。
      1. 转到分发工具。
      1. 为配置选择树激活（例如`/conf/wknd/settings/graphql/persistentQueries`）。
   * 使用工作流（通过工作流启动器配置）：
      1. 定义工作流启动器规则，用于执行将在不同事件上复制配置的工作流模型（例如，创建、修改等）。



1. 发布查询配置后，同样的原则适用，只需使用发布端点即可。

   >[!NOTE]
   >
   >对于匿名访问，系统假定ACL允许“每个人”有权访问查询配置。
   >
   >如果情况并非如此，它将无法执行。

   >[!NOTE]
   >
   >需要对URL中的任何分号(&quot;;&quot;)进行编码。
   >
   >例如，与执行持久查询的请求一样：
   >
   >
   ```xml
   >curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   >```

## 从外部网站查询GraphQL端点 {#query-graphql-endpoint-from-external-website}

要从外部网站访问GraphQL端点，您需要配置：

* [CORS过滤器](#cors-filter)
* [反向链接过滤器](#referrer-filter)

### CORS过滤器 {#cors-filter}

>[!NOTE]
>
>有关AEM中CORS资源共享策略的详细概述，请参阅[了解跨域资源共享(CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html#understand-cross-origin-resource-sharing-(cors))。

要访问GraphQL端点，必须在客户Git存储库中配置CORS策略。 这是通过为所需端点添加相应的OSGi CORS配置文件来完成的。

此配置必须指定必须向其授予访问权限的受信任网站源`alloworigin`或`alloworiginregexp`。

例如，要授予对`https://my.domain`的GraphQL端点和持久查询端点的访问权，您可以使用：

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

如果为端点配置了虚路径，则还可以在`allowedpaths`中使用该路径。

### 反向链接过滤器 {#referrer-filter}

除了CORS配置之外，还必须配置反向链接过滤器，以允许从第三方主机访问。

这是通过添加相应的OSGi反向链接过滤器配置文件来完成的，该配置文件：

* 指定可信网站主机名；`allow.hosts`或`allow.hosts.regexp`,
* 授予对此主机名的访问权限。

例如，要授予使用反向链接`my.domain`的请求的访问权限，您可以：

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
>客户仍有责任：
>
>* 仅授予对受信任域的访问权限
>* 确保不泄露任何敏感信息
>* 不使用通配符[*]语法；这将禁用对GraphQL端点的经过身份验证的访问，并向全世界展示该端点。


>[!CAUTION]
>
>所有GraphQL [架构](#schema-generation)（从已&#x200B;**启用**&#x200B;的内容片段模型派生）均可通过GraphQL端点读取。
>
>这意味着您需要确保没有可用的敏感数据，因为这些数据可能会以这种方式泄露；例如，这包括模型定义中可以显示为字段名称的信息。

## 身份验证 {#authentication}

请参阅[对内容片段的远程AEM GraphQL查询的身份验证](/help/assets/content-fragments/graphql-authentication-content-fragments.md)。

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

1. **问**:“AEM的GraphQL API与查询生成器API有何不同？**”

   * **答**:“*AEM GraphQL API提供了对JSON输出的完全控制，是用于查询内容的行业标准。接下来，AEM计划投资于AEM GraphQL API。*&quot;

## 教程 — AEM Headless和GraphQL快速入门 {#tutorial}

正在查找动手实践教程？ 请参阅[AEM无头和GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)端到端入门教程，其中演示了如何在无头CMS方案中使用AEM GraphQL API构建和公开内容，以及如何使用外部应用程序使用的内容。
