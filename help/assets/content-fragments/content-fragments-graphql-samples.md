---
title: 了解如何将 GraphQL 与 AEM 结合使用 – 示例内容和查询
description: 通过探索示例内容和查询，了解如何将 GraphQL 与 AEM 结合使用，以 Headless 方式提供内容。
feature: Content Fragments,GraphQL API
exl-id: 91c5f61c-9c15-4d72-9b9b-0c23f31e7cdc
source-git-commit: 1a3d5a6b3b4f7af67d6a62cdaab484daa536cb63
workflow-type: tm+mt
source-wordcount: '1416'
ht-degree: 100%

---

# 了解如何将 GraphQL 与 AEM 结合使用 – 示例内容和查询 {#learn-graphql-with-aem-sample-content-queries}

通过探索示例内容和查询，了解如何将 GraphQL 与 AEM 结合使用，以 Headless 方式提供内容。

>[!NOTE]
>
>本页面应该与下列内容一起阅读：
>
>* [内容片段](/help/assets/content-fragments/content-fragments.md)
>* [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)
>* [用于内容片段的 AEM GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)


要开始了解 GraphQL 查询以及它们如何与 AEM 内容片段结合使用，看一些具体的示例会有所帮助。

有关这方面的帮助，请查看：

* 一个[示例内容片段结构](#content-fragment-structure-graphql)

* 以及一些[示例 GraphQL 查询](#graphql-sample-queries)，基于示例内容片段结构（内容片段模型以及相关的内容片段）。


## GraphQL – 使用示例内容片段结构的示例查询 {#graphql-sample-queries-sample-content-fragment-structure}

查看这些示例查询，以了解创建查询的说明以及示例结果。

>[!NOTE]
>
>根据您的实例，您可以直接访问 [AEM GraphQL API 中包含的 GraphiQL 接口](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface)，用于提交和测试查询。
>
>例如：`http://localhost:4502/content/graphiql.html`

>[!NOTE]
>
>示例查询基于[用于 GraphQL 的示例内容片段结构](#content-fragment-structure-graphql)

### 示例查询 – 所有可用架构和数据类型 {#sample-all-schemes-datatypes}

这会返回所有可用架构的所有 `types`。

**示例查询**

```xml
{
  __schema {
    types {
      name
      description
    }
  }
}
```

**示例结果**

```xml
{
  "data": {
    "__schema": {
      "types": [
        {
          "name": "AdventureModel",
          "description": null
        },
        {
          "name": "AdventureModelArrayFilter",
          "description": null
        },
        {
          "name": "AdventureModelFilter",
          "description": null
        },
        {
          "name": "AdventureModelResult",
          "description": null
        },
        {
          "name": "AdventureModelResults",
          "description": null
        },
        {
          "name": "AllFragmentModels",
          "description": null
        },
        {
          "name": "ArchiveRef",
          "description": null
        },
        {
          "name": "ArrayMode",
          "description": null
        },
        {
          "name": "ArticleModel",
          "description": null
        },

...more results...

        {
          "name": "__EnumValue",
          "description": null
        },
        {
          "name": "__Field",
          "description": null
        },
        {
          "name": "__InputValue",
          "description": null
        },
        {
          "name": "__Schema",
          "description": "A GraphQL Introspection defines the capabilities of a GraphQL server. It exposes all available types and directives on the server, the entry points for query, mutation, and subscription operations."
        },
        {
          "name": "__Type",
          "description": null
        },
        {
          "name": "__TypeKind",
          "description": "An enum describing what kind of type a given __Type is"
        }
      ]
    }
  }
}
```

### 示例查询 – 关于所有城市的所有信息 {#sample-all-information-all-cities}

要检索有关所有城市的所有信息，您可以使用非常基本的查询：
**示例查询**

```xml
{
  cityList {
    items
  }
}
```

在执行时，系统将自动扩展查询以包含所有字段：

```xml
{
  cityList {
    items {
      _path
      name
      country
      population
    }
  }
}
```

**示例结果**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "_path": "/content/dam/sample-content-fragments/cities/basel",
          "name": "Basel",
          "country": "Switzerland",
          "population": 172258
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/berlin",
          "name": "Berlin",
          "country": "Germany",
          "population": 3669491
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/bucharest",
          "name": "Bucharest",
          "country": "Romania",
          "population": 1821000
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/san-francisco",
          "name": "San Francisco",
          "country": "USA",
          "population": 883306
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/san-jose",
          "name": "San Jose",
          "country": "USA",
          "population": 1026350
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/stuttgart",
          "name": "Stuttgart",
          "country": "Germany",
          "population": 634830
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/zurich",
          "name": "Zurich",
          "country": "Switzerland",
          "population": 415367
        }
      ]
    }
  }
}
```

### 示例查询 – 所有城市的名称 {#sample-names-all-cities}

这是一个直接的查询，返回 `city` 架构中所有条目的 `name`。

**示例查询**

```xml
query {
  cityList {
    items {
      name
    }
  }
}
```

**示例结果**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "Basel"
        },
        {
          "name": "Berlin"
        },
        {
          "name": "Bucharest"
        },
        {
          "name": "San Francisco"
        },
        {
          "name": "San Jose"
        },
        {
          "name": "Stuttgart"
        },
        {
          "name": "Zurich"
        }
      ]
    }
  }
}
```

### 示例查询 – 一个特定城市片段 {#sample-single-specific-city-fragment}

此查询返回存储库中特定位置的单个片段条目的详细信息。

**示例查询**

```xml
{
  cityByPath (_path: "/content/dam/sample-content-fragments/cities/berlin") {
    item {
      _path
      name
      country
      population
     categories
    }
  }
}
```

**示例结果**

```xml
{
  "data": {
    "cityByPath": {
      "item": {
        "_path": "/content/dam/sample-content-fragments/cities/berlin",
        "name": "Berlin",
        "country": "Germany",
        "population": 3669491,
        "categories": [
          "city:capital",
          "city:emea"
        ]
      }
    }
  }
}
```

### 示例查询 – 具有指定变体的所有城市 {#sample-cities-named-variation}

如果您创建新的变体，命名为“柏林中心”(`berlin_centre`)，则对于 `city` 柏林，您可以使用查询返回变体的详细信息。

**示例查询**

```xml
{
  cityList (variation: "berlin_center") {
    items {
      _path
      name
      country
      population
      categories
    }
  }
}
```

**示例结果**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "_path": "/content/dam/sample-content-fragments/cities/berlin",
          "name": "Berlin",
          "country": "Germany",
          "population": 3669491,
          "categories": [
            "city:capital",
            "city:emea"
          ]
        }
      ]
    }
  }
}
```

### 示例查询 – 公司的 CEO 和员工的完整详细信息 {#sample-full-details-company-ceos-employees}

使用嵌套片段的结构，此查询返回公司的 CEO 及其所有员工的完整详细信息。

**示例查询**

```xml
query {
  companyList {
    items {
      name
      ceo {
        _path
        name
        firstName
        awards {
        id
          title
        }
      }
      employees {
       name
        firstName
       awards {
         id
          title
        }
      }
    }
  }
}
```

**示例结果**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "Apple Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/steve-jobs",
            "name": "Jobs",
            "firstName": "Steve",
            "awards": []
          },
          "employees": [
            {
              "name": "Marsh",
              "firstName": "Duke",
              "awards": []
            },
            {
              "name": "Caulfield",
              "firstName": "Max",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                }
              ]
            }
          ]
        },
        {
          "name": "Little Pony, Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/adam-smith",
            "name": "Smith",
            "firstName": "Adam",
            "awards": []
          },
          "employees": [
            {
              "name": "Croft",
              "firstName": "Lara",
              "awards": [
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            },
            {
              "name": "Slade",
              "firstName": "Cutter",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                },
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            }
          ]
        },
        {
          "name": "NextStep Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/steve-jobs",
            "name": "Jobs",
            "firstName": "Steve",
            "awards": []
          },
          "employees": [
            {
              "name": "Smith",
              "firstName": "Joe",
              "awards": []
            },
            {
              "name": "Lincoln",
              "firstName": "Abraham",
              "awards": []
            }
          ]
        }
      ]
    }
  }
}
```

### 示例查询 – 所有名为“Jobs”或“Smith”的人 {#sample-all-persons-jobs-smith}

这将筛选出名为 `Jobs` 或 `Smith` 的所有 `persons`。

**示例查询**

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

**示例结果**

```xml
{
  "data": {
    "personList": {
      "items": [
        {
          "name": "Smith",
          "firstName": "Adam"
        },
        {
          "name": "Smith",
          "firstName": "Joe"
        },
        {
          "name": "Jobs",
          "firstName": "Steve"
        }
      ]
    }
  }
}
```

### 示例查询 – 所有名字不是“Jobs”的人 {#sample-all-persons-not-jobs}

这将筛选出名为 `Jobs` 或 `Smith` 的所有 `persons`。

**示例查询**

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

**示例结果**

```xml
{
  "data": {
    "personList": {
      "items": [
        {
          "name": "Lincoln",
          "firstName": "Abraham"
        },
        {
          "name": "Smith",
          "firstName": "Adam"
        },
        {
          "name": "Slade",
          "firstName": "Cutter"
        },
        {
          "name": "Marsh",
          "firstName": "Duke"
        },
        {
          "name": "Smith",
          "firstName": "Joe"
        },
        {
          "name": "Croft",
          "firstName": "Lara"
        },
        {
          "name": "Caulfield",
          "firstName": "Max"
        }
      ]
    }
  }
}
```

### 示例查询 – 其 `_path` 以特定前缀开头的所有冒险 {#sample-wknd-all-adventures-cycling-path-filter}

其 `_path` 以特定前缀 (`/content/dam/wknd/en/adventures/cycling`) 开头的所有 `adventures`。

**示例查询**

```xml
query {
  adventureList(
    filter: {
      _path: {
        _expressions: [
        {
          value: "/content/dam/wknd/en/adventures/cycling"
         _operator: STARTS_WITH
        }]
       }
    })
    {
    items {
      _path
    }
  }
}
```

**示例结果**

```xml
{
  "data": {
    "adventureList": {
      "items": [
        {
          "_path": "/content/dam/wknd/en/adventures/cycling-southern-utah/cycling-southern-utah"
        },
        {
          "_path": "/content/dam/wknd/en/adventures/cycling-tuscany/cycling-tuscany"
        }
      ]
    }
  }
}
```

### 示例查询 – 位于德国或瑞士且人口在 400000 到 999999 之间的所有城市。 {#sample-all-cities-d-ch-population}

以下是筛选的字段组合：使用 `AND`（隐式）来选择 `population` 范围，使用 `OR`（显式）来选择所需的城市。

**示例查询**

```xml
query {
  cityList(filter: {
    population: {
      _expressions: [
        {
          value: 400000
          _operator: GREATER_EQUAL
        }, {
          value: 1000000
          _operator: LOWER
        }
      ]
    },
    country: {
      _logOp: OR
      _expressions: [
        {
          value: "Germany"
        }, {
          value: "Switzerland"
        }
      ]
    }
  }) {
    items {
      name
      population
      country
    }
  }
}
```

**示例结果**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "Stuttgart",
          "population": 634830,
          "country": "Germany"
        },
        {
          "name": "Zurich",
          "population": 415367,
          "country": "Switzerland"
        }
      ]
    }
  }
}
```

### 示例查询 – 名称中包含 SAN 的所有城市，不考虑大小写 {#sample-all-cities-san-ignore-case}

此查询查找名称中包含 `SAN` 的所有城市，不考虑大小写。

**示例查询**

```xml
query {
  cityList(filter: {
    name: {
      _expressions: [
        {
          value: "SAN"
          _operator: CONTAINS
          _ignoreCase: true
        }
      ]
    }
  }) {
    items {
      name
      population
      country
    }
  }
}
```

**示例结果**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA"
        },
        {
          "name": "San Jose",
          "population": 1026350,
          "country": "USA"
        }
      ]
    }
  }
}
```

### 示例查询 – 筛选数组中必须至少出现一次的项 {#sample-array-item-occur-at-least-once}

此查询筛选数组中必须至少出现一次的项 (`city:na`)。

**示例查询**

```xml
query {
  cityList(filter: {
    categories: {
      _expressions: [
        {
          value: "city:na"
          _apply: AT_LEAST_ONCE
        }
      ]
    }
  }) {
    items {
      name
      population
      country
      categories
    }
  }
}
```

**示例结果**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA",
          "categories": [
            "city:beach",
            "city:na"
          ]
        },
        {
          "name": "San Jose",
          "population": 1026350,
          "country": "USA",
          "categories": [
            "city:na"
          ]
        }
      ]
    }
  }
}
```

### 示例查询 – 根据精确的数组值筛选 {#sample-array-exact-value}

此查询筛选一个精确的数组值。

**示例查询**

```xml
query {
  cityList(filter: {
    categories: {
      _expressions: [
        {
          values: [
            "city:beach",
            "city:na"
          ]
        }
      ]
    }
  }) {
    items {
      name
      population
      country
      categories
    }
  }
}
```

**示例结果**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA",
          "categories": [
            "city:beach",
            "city:na"
          ]
        }
      ]
    }
  }
}
```

### 嵌套内容片段的示例查询 – 至少有一位员工名为“Smith”的所有公司 {#sample-companies-employee-smith}

此查询演示了筛选 `name` 为“Smith”的任意 `person`，跨两个嵌套片段返回结果：`company` 和 `employee`。

**示例查询**

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

**示例结果**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "NextStep Inc.",
          "ceo": {
            "name": "Jobs",
            "firstName": "Steve"
          },
          "employees": [
            {
              "name": "Smith",
              "firstName": "Joe"
            },
            {
              "name": "Lincoln",
              "firstName": "Abraham"
            }
          ]
        }
      ]
    }
  }
}
```

### 嵌套内容片段的示例查询 – 所有员工赢得了“Gamestar”奖项的所有公司 {#sample-all-companies-employee-gamestar-award}

此查询演示了跨三个嵌套片段筛选：`company`、`employee` 和 `award`。

**示例查询**

```xml
query {
  companyList(filter: {
    employees: {
      _apply: ALL
      _match: {
        awards: {
          _match: {
            id: {
              _expressions: [
                {
                  value: "GS"
                  _operator:EQUALS
                }
              ]
            }
          }
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
        awards {
          id
          title
        }
      }
    }
  }
}
```

**示例结果**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "Little Pony, Inc.",
          "ceo": {
            "name": "Smith",
            "firstName": "Adam"
          },
          "employees": [
            {
              "name": "Croft",
              "firstName": "Lara",
              "awards": [
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            },
            {
              "name": "Slade",
              "firstName": "Cutter",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                },
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            }
          ]
        }
      ]
    }
  }
}
```

### 元数据的示例查询 – 列出标题为 GB 的奖项的元数据 {#sample-metadata-awards-gb}

此查询演示了跨三个嵌套片段筛选：`company`、`employee` 和 `award`。

**示例查询**

```xml
query {
  awardList(filter: {
      id: {
        _expressions: [
          {
            value:"GB"
          }
        ]
    }
  }) {
    items {
      _metadata {
        stringMetadata {
          name,
          value
        }
      }
      id
      title
    }
  }
}
```

**示例结果**

```xml
{
  "data": {
    "awardList": {
      "items": [
        {
          "_metadata": {
            "stringMetadata": [
              {
                "name": "title",
                "value": "Gameblitz Award"
              },
              {
                "name": "description",
                "value": ""
              }
            ]
          },
          "id": "GB",
          "title": "Gameblitz"
        }
      ]
    }
  }
}
```

## 使用 WKND 项目的示例查询 {#sample-queries-using-wknd-project}

这些示例查询基于 WKND 项目。它具有：

* 在以下位置提供的内容片段模型：
   `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* 在以下位置提供的内容片段（和其他内容）：
   `http://<hostname>:<port>/assets.html/content/dam/wknd/en`

>[!NOTE]
>
>由于结果可能会很庞大，此处不再复述。

### 具有指定属性的特定模型的所有内容片段示例查询 {#sample-wknd-all-model-properties}

此示例查询查找：

* 类型为 `article` 的所有内容片段
* 具有 `path` 和 `author` 属性。

**示例查询**

```xml
{
  articleList {
    items {
      _path
      author
    }
  }
}
```

### 元数据的示例查询 {#sample-wknd-metadata}

此查询查找：

* 类型为 `adventure` 的所有内容片段
* 元数据

**示例查询**

```xml
{
  adventureList {
    items {
      _path,
      _metadata {
        stringMetadata {
          name,
          value
        }
        stringArrayMetadata {
          name,
          value
        }
        intMetadata {
          name,
          value
        }
        intArrayMetadata {
          name,
          value
        }
        floatMetadata {
          name,
          value
        }
        floatArrayMetadata {
          name,
          value
        }
        booleanMetadata {
          name,
          value
        }
        booleanArrayMetadata {
          name,
          value
        }
        calendarMetadata {
          name,
          value
        }
        calendarArrayMetadata {
          name,
          value
        }
      }
    }
  }
}
```

### 给定模型的单个内容片段的示例查询 {#sample-wknd-single-content-fragment-of-given-model}

此示例查询查找：

* 特定路径下类型为 `article` 的单个内容片段
   * 在其中，所有下列格式的内容：
      * HTML
      * Markdown
      * 纯文本
      * JSON

**示例查询**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/alaska-adventure/alaskan-adventures") {
    item {
        _path
        author
        main {
          html
          markdown
          plaintext
          json
        }
    }
  }
}
```

### 来自模型的内容片段模型的示例查询 {#sample-wknd-content-fragment-model-from-model}

此示例查询查找：

* 单个内容片段
   * 底层内容片段模型的详细信息

**示例查询**

```xml
{
  adventureByPath(_path: "/content/dam/wknd/en/adventures/riverside-camping-australia/riverside-camping-australia") {
    item {
      _path
      adventureTitle
      _model {
        _path
        title
      }
    }
  }
}
```

### 嵌套内容片段的示例查询 – 单个模型类型{#sample-wknd-nested-fragment-single-model}

此查询查找：

* 特定路径下类型为 `article` 的单个内容片段
   * 在其中，引用（嵌套）片段的路径和作者

>[!NOTE]
>
>字段 `referencearticle` 具有数据类型 `fragment-reference`。

**示例查询**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/skitouring/skitouring") {
    item {
        _path
        author
        referencearticle {
          _path
          author
      }
    }
  }
}
```

### 嵌套内容片段的示例查询 – 多个模型类型{#sample-wknd-nested-fragment-multiple-model}

此查询查找：

* 类型为 `bookmark` 的多个内容片段
   * 带有对特定模型类型 `article` 和 `adventure` 的其他片段的片段引用

>[!NOTE]
>
>字段 `fragments` 具有数据类型 `fragment-reference`，并选择了模型 `Article`、`Adventure`。

```xml
{
  bookmarkList {
    items {
        fragments {
          ... on ArticleModel {
            _path
            author
          }
          ... on AdventureModel {
            _path
            adventureTitle
          }
        }
     }
  }
}
```

### 具有内容引用的特定模型的内容片段示例查询{#sample-wknd-fragment-specific-model-content-reference}

此查询有两种风格：

1. 用于返回所有内容引用。
1. 用于返回类型为 `attachments` 的特定内容引用。

这些查询查找：

* 类型为 `bookmark` 的多个内容片段
   * 具有对其他片段的内容引用

#### 具有预获取引用的多个内容片段的示例查询 {#sample-wknd-multiple-fragments-prefetched-references}

以下查询通过使用 `_references` 返回所有内容引用：

```xml
{
  bookmarkList {
     _references {
         ... on ImageRef {
          _path
          type
          height
        }
        ... on MultimediaRef {
          _path
          type
          size
        }
        ... on DocumentRef {
          _path
          type
          author
        }
        ... on ArchiveRef {
          _path
          type
          format
        }
    }
    items {
        _path
    }
  }
}
```

#### 具有附件的多个内容片段的示例查询 {#sample-wknd-multiple-fragments-attachments}

以下查询返回所有 `attachments` – 类型为 `content-reference` 的特定字段（子组）：

>[!NOTE]
>
>字段 `attachments` 具有数据类型 `content-reference`，并选择了多种格式。

```xml
{
  bookmarkList {
    items {
      attachments {
        ... on PageRef {
          _path
          type
        }
        ... on ImageRef {
          _path
          width
        }
        ... on MultimediaRef {
          _path
          size
        }
        ... on DocumentRef {
          _path
          author
        }
        ... on ArchiveRef {
          _path
          format
        }
      }
    }
  }
}
```

### 具有 RTE 内联引用的单个内容片段的示例查询 {#sample-wknd-single-fragment-rte-inline-reference}

此查询查找：

* 特定路径下类型为 `bookmark` 的单个内容片段
   * 在其中，具有 RTE 内联引用

>[!NOTE]
>
>RTE 内联引用在 `_references` 中水合。

**示例查询**

```xml
{
  bookmarkByPath(_path: "/content/dam/wknd/en/bookmarks/skitouring") {
    item {
      _path
      description {
        json
      }
    }
    _references {
      ... on ArticleModel {
        _path
      }
      ... on AdventureModel {
        _path
      }
      ... on ImageRef {
        _path
      }
      ... on MultimediaRef {
        _path
      }
      ... on DocumentRef {
        _path
      }
      ... on ArchiveRef {
        _path
      }
    }
  }
}
```

### 给定模型的单个内容片段变体的示例查询 {#sample-wknd-single-fragment-given-model}

此查询查找：

* 特定路径下类型为 `article` 的单个内容片段
   * 在其中，数据关联到变体：`variation1`

**示例查询**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/alaska-adventure/alaskan-adventures", variation: "variation1") {
    item {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

### 给定模型的多个内容片段的指定变体示例查询 {#sample-wknd-variation-multiple-fragment-given-model}

此查询查找：

* 类型为 `article` 且具有以下特定变体的内容片段：`variation1`

**示例查询**

```xml
{
  articleList (variation: "variation1") {
    items {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

### 给定区域设置的多个内容片段的示例查询 {#sample-wknd-multiple-fragments-given-locale}

此查询查找：

* `fr` 区域设置中类型为 `article` 的内容片段

**示例查询**

```xml
{ 
  articleList (_locale: "fr") {
    items {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

## 示例内容片段结构（用于 GraphQL） {#content-fragment-structure-graphql}

示例查询基于以下结构，该结构使用：

* 一个或多个[示例内容片段模型](#sample-content-fragment-models-schemas) – 构成了 GraphQL 架构的基础

* 基于以上模型的[示例内容片段](#sample-content-fragments)

### 示例内容片段模型（架构） {#sample-content-fragment-models-schemas}

对于相同的查询，我们将使用以下内容模型及其相互关系（引用 ->）：

* [公司](#model-company)
-> [人员](#model-person)
-> [奖励](#model-award)

* [城市](#model-city)

#### 公司 {#model-company}

定义公司的基本字段包括：

| 字段名 | 数据类型 | 引用 |
|--- |--- |--- |
| 公司名称 | 单行文本 |  |
| CEO | 片段引用（单个字段） | [人员](#model-person) |
| 员工 | 片段引用（多个字段） | [人员](#model-person) |

#### 人员 {#model-person}

这些字段定义人员，也可以是员工：

| 字段名 | 数据类型 | 引用 |
|--- |--- |--- |
| 名称 | 单行文本 |  |
| 名字 | 单行文本 |  |
| 奖励 | 片段引用（多个字段） | [奖励](#model-award) |

#### 奖励 {#model-award}

定义奖励的字段包括：

| 字段名 | 数据类型 | 引用 |
|--- |--- |--- |
| 简称/ID | 单行文本 |  |
| 标题 | 单行文本 |  |

#### 城市 {#model-city}

定义城市的字段包括：

| 字段名 | 数据类型 | 引用 |
|--- |--- |--- |
| 名称 | 单行文本 |  |
| 国家/地区 | 单行文本 |  |
| 人口 | 数字 |  |
| 类别 | 标记 |  |

### 示例内容片段 {#sample-content-fragments}

以下片段用于相应的模型。

#### 公司 {#fragment-company}

| 公司名称 | 首席执行官 | 员工 |
|--- |--- |--- |
| Apple | Steve Jobs | Duke Marsh<br>Max Caulfield |
| Little Pony Inc. | Adam Smith | Lara Croft<br>Cutter Slade |
| NextStep Inc. | 史蒂夫·乔布斯 | Joe Smith<br>Abe Lincoln |

#### 人员 {#fragment-person}

| 姓名 | 名字 | 奖励 |
|--- |--- |--- |
| Lincoln | Abe |  |
| Smith | Adam |   |
| Slade | Cutter | Gameblitz<br>Gamestar |
| Marsh | Duke |   |   |
| Smith | Joe |   |
| Croft | Lara | Gamestar |
| Caulfield | Max | Gameblitz |
| Jobs | Steve |   |

#### 奖励 {#fragment-award}

| 简称/ID | 标题 |
|--- |--- |
| GB | Gameblitz |
| GS | Gamestar |
| OSC | Oscar |

#### 城市 {#fragment-city}

| 名称 | 国家/地区 | 人口 | 类别 |
|--- |--- |--- |--- |
| 巴塞尔 | 瑞士 | 172258 | city:emea |
| 柏林 | 德国 | 3669491 | city:capital<br>city:emea |
| 布加勒斯特 | 罗马尼亚 | 1821000 |  city:capital<br>city:emea |
| 圣弗朗西斯科 | 美国 |  883306 |  city:beach<br>city:na |
| 圣何塞 | 美国 |  102635 | city:na |
| 斯图加特 | 德国 | 634830 | city:emea |
| 苏黎世 | 瑞士 | 415367 |  城市：资本<br>城市：emea |
