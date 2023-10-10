---
title: 优化 GraphQL 查询
description: 了解在Adobe Experience Manager as a Cloud Service中筛选、分页和排序内容片段以进行Headless内容投放时，如何优化GraphQL查询。
exl-id: 47d0570b-224e-4109-b94e-ccc369d7ac5f
source-git-commit: c0570d6c0d624d950ddbb5c0d2ce38ff7c3756a4
workflow-type: tm+mt
source-wordcount: '1935'
ht-degree: 60%

---

# 优化 GraphQL 查询 {#optimizing-graphql-queries}

>[!NOTE]
>
>在应用这些优化推荐之前，请考虑 [在GraphQL筛选中更新用于分页和排序的内容片段](/help/sites-developing/headless/graphql-api/graphql-optimized-filtering-content-update.md) 以获得最佳性能。

提供这些准则是为了帮助防止GraphQL查询出现性能问题。

## GraphQL核对清单 {#graphql-checklist}

以下核对清单旨在帮助您在Adobe Experience Manager (AEM)as a Cloud Service中优化GraphQL的配置和使用。

### 首要原则 {#first-principles}

#### 使用持久GraphQL查询 {#use-persisted-graphql-queries}

**推荐**

强烈建议使用持久GraphQL查询。

持久的GraphQL查询利用内容交付网络(CDN)帮助降低查询执行性能。 客户端应用程序请求持久查询，GET请求快速边缘启用执行。

**进一步参考**

请参阅：

* [持久 GraphQL 查询](/help/sites-developing/headless/graphql-api/persisted-queries.md).
* [了解如何将 GraphQL 与 AEM 结合使用 – 示例内容和查询](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md)

#### 安装GraphQL索引包 {#install-graphql-index-package}

**推荐**

使用GraphQL的客户 *必须* 使用GraphQL索引包安装Experience Manager内容片段。 这样，您就可以根据实际使用的功能添加所需的索引定义。 无法安装此包可能会导致GraphQL查询缓慢或失败。

请参阅适用于您的Service Pack的版本的发行说明。 例如，有关最新的Service Pack，请参阅 [安装用于Experience Manager内容片段的GraphQL索引包](/help/release-notes/release-notes.md#install-aem-graphql-index-add-on-package) .

>[!NOTE]
>
>每个实例仅安装此包一次；无需随每个Service Pack一起重新安装。

**进一步参考**
请参阅：

* [安装用于Experience Manager内容片段的GraphQL索引包](/help/release-notes/release-notes.md#install-aem-graphql-index-add-on-package)

### 缓存策略 {#cache-strategy}

还可以使用各种缓存方法进行优化。

#### 启用AEM Dispatcher缓存 {#enable-aem-dispatcher-caching}

**推荐**

[AEM调度程序](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html) 是AEM服务中的第一级缓存，在CDN缓存之前。

**进一步参考**

请参阅：

* [GraphQL 持久化查询 - 在 Dispatcher 中启用缓存](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#graphql-persisted-queries-enabling-caching-dispatcher)

#### 使用内容交付网络(CDN) {#use-cdn}

**推荐**

如果定位为，则可以缓存GraphQL查询及其JSON响应。 `GET` 使用CDN时的请求。 相比之下，未缓存的请求可能非常（资源）昂贵且处理缓慢，有可能对源头资源造成进一步的有害影响。

**进一步参考**

请参阅：

* [在AEM中使用CDN](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hans#using-dispatcher-with-a-cdn)

#### 设置HTTP缓存控制标头 {#set-http-cache-control-headers}

**推荐**

在将GraphQL持久查询与CDN结合使用时，建议设置适当的HTTP缓存控制标头。

每个持久查询可以有自己的一组特定的缓存控制标头。 标头可设置在 [GRAPHQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md).

<!-- or the [AEM GraphiQL IDE](/help/sites-developing/headless/graphql-api/graphiql-ide.md#managing-cache). 
-->

**进一步参考**

请参阅：

* [正在缓存您的持久查询](/help/sites-developing/headless/graphql-api/persisted-queries.md#caching-persisted-queries)
<!--
* [Managing cache for your persisted queries](/help/sites-developing/headless/graphql-api/graphiql-ide.md#managing-cache)
-->

<!--
#### Use AEM GraphQL pre-caching {#use-aem-graphql-pre-caching}

**Recommendation**

This capability allows AEM to further cache content within the scope of GraphQL queries that can then be assembled as blocks in JSON output rather than line by line. 

**Further Reference**

Please contact Adobe to enable this capability for your AEM Cloud Service program and environments. 
-->

### GraphQL查询优化 {#graphql-query-optimization}

在具有大量共享同一模型的内容片段的 AEM 实例上，GraphQL 列表查询的成本可能会较高（就资源而言）。

这是因为&#x200B;*所有*&#x200B;共享将在 GraphQL 查询中使用的模型的片段都必须加载到内存中。这将消耗较多的时间和内存。只能在将整个结果集加载到内存中&#x200B;**后**，再应用筛选（它可能会减少最终结果集中的项目数）。

这可能会给人留下一种印象，那就是，即使较小的结果集也会导致性能不佳。然而，实际上这种缓慢是由初始结果集的大小引起的，因为必须先内部处理此情况，之后才能应用筛选。

要减少性能和内存问题，必须使该初始结果集尽可能的小。

AEM 提供了两种方法来优化 GraphQL 查询：

* [混合筛选](#use-aem-graphql-hybrid-filtering)
* [分页](#use-aem-graphql-pagination)

   * [排序](#use-graphql-sorting)与优化没有直接关系，而与分页有关

每种方法都有自己的用例和限制。本节提供有关混合过滤和分页的信息，以及一些 [最佳实践](#best-practices) 以用于优化GraphQL查询。

#### 使用AEM GraphQL混合筛选 {#use-aem-graphql-hybrid-filtering}

**推荐**

混合筛选结合了 JCR 筛选和 AEM 筛选。

它在将结果集加载到内存中以进行 AEM 筛选之前应用 JCR 筛选（采用查询约束的形式）。这是为了减少加载到内存中的结果集，因为 JCR 筛选会在此之前删除多余的结果。

>[!NOTE]
>
>出于技术原因（例如灵活性、片段嵌套），AEM 无法将整个筛选工作委派给 JCR。

此技术保留了 GraphQL 筛选提供的灵活性，同时将尽可能多的筛选工作委派给 JCR。

>[!NOTE]
>
>AEM混合筛选需要更新现有的内容片段

**进一步参考**

请参阅：

* [在GraphQL筛选中更新用于分页和排序的内容片段](/help/sites-developing/headless/graphql-api/graphql-optimized-filtering-content-update.md)
* [按 _tags ID 过滤并排除变体的示例查询](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-filtering-tag-not-variations)

#### 使用GraphQL分页 {#use-aem-graphql-pagination}

**推荐**

通过使用分页(一种GraphQL标准)将响应分段为块，可以改进具有大型结果集的复杂查询的响应时间。

AEM 中的 GraphQL 支持两种类型的分页：

* [基于限制/偏移的分页](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#list-offset-limit)
此分页用于列表查询；它们以`List` 结尾；例如 `articleList`。
要使用它，您必须提供要返回的第一个项目的位置 (`offset`) 和要返回的项目数（`limit` 或页面大小）。

* [基于光标的分页](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#paginated-first-after)（由 `first` 和 `after` 表示）
这将为每个项目提供一个唯一 ID；也称为光标。
在查询中，您指定上一页的最后一项的光标，以及页面大小（要返回的项目的最大数量）。

  由于基于光标的分页不适合基于列表的查询的数据结构，因此，AEM 引入了 `Paginated` 查询类型；例如 `articlePaginated`。所使用的数据结构和参数遵循 [GraphQL 光标连接规范](https://relay.dev/graphql/connections.htm)。

  >[!NOTE]
  >
  >AEM 目前支持前向分页（使用 `after`/`first` 参数）。
  >
  >后向分页（使用 `before`/`last` 参数）不受支持。

**进一步参考**

请参阅：

* [使用“先”和“后”的示例分页查询](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-pagination-first-after)

#### 使用GraphQL排序 {#use-graphql-sorting}

**推荐**

作为GraphQL标准，排序使客户端能够按排序的顺序接收JSON内容。 这可以降低在客户端上执行进一步处理的需要。

仅在所有排序条件都与顶级片段相关时，排序才有效。

如果排序顺序包括某个嵌套片段上的一个或多个字段，则必须将所有共享顶级模型的片段加载到内存中。这会对性能产生负面影响。

>[!NOTE]
>
>对顶级字段进行排序也会对性能产生（虽然很小）影响。

**进一步参考**

请参阅：

* [示例查询，按_tags ID筛选并排除变体，并按名称排序](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-filtering-tag-not-variations)

## 最佳实践 {#best-practices}

所有优化推荐的主要目标是减少初始结果集。 此处列出的最佳实践提供了多种方法来实现此目的。可以（也应该）将它们结合使用。

### 仅筛选顶级属性 {#filter-top-level-properties-only}

目前，JCR 级别的筛选仅适用于顶级片段。

如果筛选处理嵌套片段的字段，则 AEM 必须回退以将所有共享基础模型的片段加载到内存中。

您仍可以使用 [AND 运算符](#logical-operations-in-filter-expressions)将顶级片段字段上的筛选表达式和嵌套片段字段上的筛选表达式组合起来，从而优化此类 GraphQL 查询。

### 使用内容结构 {#use-content-structure}

在 AEM 中，通常考虑的最佳实践是，使用存储库结构来缩小要处理的内容范围。

此方法也将应用于 GraphQL 查询。

这可以通过在顶级片段的 `_path` 字段上应用筛选来完成：

```graphql
{
  someList(filter: {
    _path: {
      _expressions: [ 
        {
          value: "/content/dam/some/sub/path/",
          _operator: STARTS_WITH
        }
      ]
    }
  }) {
    items {
      # ...
    }
  }
}
```

>[!NOTE]
>
>需要 `value` 上的尾随 `/` 来实现最佳性能。

### 使用分页 {#use-paging}

您还可以使用分页来减小初始结果集；特别是在您的请求不使用任何筛选和排序的情况下。

如果您对嵌套片段进行筛选或排序，分页查询可能仍然很慢，因为 AEM 可能仍需要将大量片段加载到内存中。因此，如果将筛选和分页结合使用，请考虑筛选规则（如上所述）。

对于分页，排序同样重要，因为分页的结果始终是已排序的 - 无论是通过显式还是隐式方式。

如果您主要只对检索前几页感兴趣，则使用 `...List` 或 `...Paginated` 查询之间没有显著区别。不过，如果您的应用程序不只是想阅读一两页，则应考虑 `...Paginated` 查询，因为此查询在阅读后续页面时的性能更佳。

### 筛选表达式中的逻辑运算 {#logical-operations-in-filter-expressions}

如果在嵌套片段上进行筛选，则仍可以通过提供使用 `AND` 运算符的顶级字段的附加筛选来利用 JCR 筛选。

一个典型用例是，对顶级片段的 `_path` 字段使用筛选器来限制查询的范围，然后筛选可能位于顶级或嵌套片段上的其他字段。

在此示例中，将使用 `AND` 组合不同的筛选表达式。因此，对 `_path` 进行筛选可以有效地限制初始结果集的大小。对顶级字段进行的所有其他筛选也可以帮助减小初始结果集 - 前提是使用 `AND` 将它们组合使用。

如果涉及嵌套的片段，则无法优化使用 `OR` 组合使用的筛选表达式。仅在&#x200B;*不*&#x200B;涉及嵌套片段的情况下，可以优化 `OR` 表达式。

### 避免筛选多行文本字段 {#avoid-filtering-multiline-textfields}

无法通过 JCR 查询筛选多行文本字段的字段（html、markdown、plaintext、json），因为必须即时计算这些字段的内容。

如果您仍需要筛选多行文本字段，请考虑通过添加额外的筛选表达式来限制初始结果集的大小，并使用 `AND` 将它们组合使用。通过筛选 `_path` 字段来限制范围也是一个好方法。

### 避免筛选虚拟字段 {#avoid-filtering-virtual-fields}

虚拟字段（大多数字段以 `_` 开始）是在执行 GraphQL 查询时计算的，因此不在基于 JCR 的筛选的范围内。

一个重要的例外是 `_path` 字段，可使用该字段有效地减小初始结果集 - 如果相应地构建了内容（请参阅[使用内容结构](#use-content-structure)）。

### 筛选：排除 {#filtering-exclusions}

还存在几种无法在 JCR 级别计算筛选表达式的情况（因此，应避免这些情况以实现最佳性能）：

* 使用 `_sensitiveness` 筛选选项的基于 `Float` 值的筛选表达式，其中 `_sensitiveness` 设置为 `0.0` 之外的任何值。

* 使用 `_ignoreCase` 筛选选项的基于 `String` 值的筛选表达式。

* 基于 `null` 值的筛选。

* 使用 `_apply: ALL_OR_EMPTY` 的基于数组的筛选。

* 使用 `_apply: INSTANCES` 和 `_instances: 0` 的基于数组的筛选。

* 使用 `CONTAINS_NOT` 运算符的筛选表达式。

* 使用 `NOT_AT` 运算符的基于 `Calendar`、`Date` 或 `Time` 值的筛选表达式。

### 最小化内容片段嵌套 {#minimize-content-fragment-nesting}

嵌套内容片段是生成自定义内容结构模型的好方法。 您甚至可以具有一个带有嵌套片段的片段，该片段具有一个嵌套片段，该片段具有……等等。

但是，如果创建的结构级别过多，可能会增加GraphQL查询的处理时间，因为GraphQL必须遍历所有嵌套内容片段的整个层次结构。

深度嵌套还会对内容治理产生不利影响。 一般情况下，建议将内容片段嵌套限制在五或六个级别以下。

### 不输出所有格式（多行文本元素） {#do-not-output-all-formats}

AEM GraphQL可以返回文本，文本创作于 **[多行文本](/help/assets/content-fragments/content-fragments-models.md#data-types)** 数据类型，采用多种格式：富文本、简单文本和Markdown。

输出所有三种格式会将JSON中文本输出的大小增大三倍。 再加上来自非常宽泛查询的通常较大的结果集，可能会产生非常大的JSON响应，因此需要很长时间才能计算。 最好将输出限制为仅呈现内容所需的文本格式。

### 修改内容片段 {#modifying-content-fragments}

使用AEM UI或API仅修改内容片段及其资源。 请勿直接在JCR中进行修改。

### 测试查询 {#test-your-queries}

处理GraphQL查询与处理搜索查询类似，并且比简单的包含所有内容的GETAPI请求要复杂得多。

在生产中使用时，在受控的非生产环境中仔细规划、测试和优化查询是以后取得成功的关键。
