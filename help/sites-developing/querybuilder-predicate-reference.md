---
title: 查询生成器谓词参考
seo-title: Query Builder Predicate Reference
description: 查询生成器API的完整谓词引用。
seo-description: Complete predicate reference for the Query Builder API.
uuid: af0e269e-7d52-4032-b22e-801c7b5dccfa
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: 94a05894-743a-4ace-a292-bfee90ba9068
exl-id: 54b942f9-5dd9-4826-9a0a-028f2d7b8e41
source-git-commit: f97eb2e028263016131b0c86be5a0508ae4def9b
workflow-type: tm+mt
source-wordcount: '2371'
ht-degree: 3%

---

# 查询生成器谓词参考{#query-builder-predicate-reference}

>[!CAUTION]
>
>此页面上的信息并不详尽。
>
>有关完整信息，请参阅 **可用谓词** （在查询生成器调试器控制台上）；例如，在：
>* [http://localhost:4502/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)
>
>例如，请参阅：
>
>* [http://localhost:4502/system/console/services?filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29](http://localhost:4502/system/console/services?filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29)


## 常规 {#general}

* [根](#root)
* [组](#group)
* [orderby](#orderby)

## 谓语 {#predicates}

* [布尔属性](/help/sites-developing/querybuilder-predicate-reference.md#boolproperty)
* [contentfragment](/help/sites-developing/querybuilder-predicate-reference.md#contentfragment)
* [dateComparison](/help/sites-developing/querybuilder-predicate-reference.md#datecomparison)
* [达特朗日](/help/sites-developing/querybuilder-predicate-reference.md#daterange)
* [排除路径](/help/sites-developing/querybuilder-predicate-reference.md#excludepaths)
* [全文](/help/sites-developing/querybuilder-predicate-reference.md#fulltext)
* [hasPermission](/help/sites-developing/querybuilder-predicate-reference.md#haspermission)
* [语言](/help/sites-developing/querybuilder-predicate-reference.md#language)
* [主资产](/help/sites-developing/querybuilder-predicate-reference.md#mainasset)
* [memberOf](/help/sites-developing/querybuilder-predicate-reference.md#memberof)
* [nodename](/help/sites-developing/querybuilder-predicate-reference.md#nodename)
* [notexpired](/help/sites-developing/querybuilder-predicate-reference.md#notexpired)
* [路径](/help/sites-developing/querybuilder-predicate-reference.md#path)
* [属性](/help/sites-developing/querybuilder-predicate-reference.md#property)
* [rangproperty](/help/sites-developing/querybuilder-predicate-reference.md#rangeproperty)
* [相对变量](/help/sites-developing/querybuilder-predicate-reference.md#relativedaterange)
* [savedquery](/help/sites-developing/querybuilder-predicate-reference.md#savedquery)
* [相似](/help/sites-developing/querybuilder-predicate-reference.md#similar)
* [标记](/help/sites-developing/querybuilder-predicate-reference.md#tag)
* [tagid](/help/sites-developing/querybuilder-predicate-reference.md#tagid)
* [tagsearch](/help/sites-developing/querybuilder-predicate-reference.md#tagsearch)
* [类型](/help/sites-developing/querybuilder-predicate-reference.md#type)

### 布尔属性 {#boolproperty}

在JCR布尔属性上匹配。 仅接受值“ `true`&quot;和&quot; `false`&quot; 如果为“ `false`“，则当属性具有值“ `false`“或者，如果它根本不存在。 这可用于检查仅在启用时设置的布尔标记。

继承的“ `operation`&quot;参数没有意义。

支持Facet提取。 将为每个 `true` 或 `false` 值，但仅适用于现有属性。

#### 属性 {#properties}

* **布尔属性**
相对于属性的路径，例如 
`myFeatureEnabled` 或 `jcr:content/myFeatureEnabled`

* **值**
用于检查属性的值， &quot; 
`true`&quot; 或 &quot; `false`&quot;

### contentfragment {#contentfragment}

将结果限制为内容片段。

不支持过滤。

不支持面提取。

#### 属性 {#properties-1}

* **contentfragment**
它可与任何值一起使用来检查内容片段。

### dateComparison {#datecomparison}

比较两个JCR DATE属性。 可以测试它们是否相等、不等、是否大于或等于。

这是仅限过滤的谓词，无法利用搜索索引。

#### 属性 {#properties-2}

* **属性1**

   首次日期属性的路径

* **属性2**

   第二个日期属性的路径

* **操作**

   &quot; `equals`&quot;表示精确匹配， &quot; `!=`&quot;表示不相等比较， &quot; `greater`&quot;表示属性1大于属性2, &quot; `>=`&quot;表示属性1大于或等于属性2。 默认值为 &quot; `equals`&quot;.

### 达特朗日 {#daterange}

根据日期/时间间隔匹配JCR DATE属性。 日期和时间采用ISO8601格式( `YYYY-MM-DDTHH:mm:ss.SSSZ`)，并允许部分表示，例如 `YYYY-MM-DD`. 或者，时间戳可以以自1970年以来（UTC时区，UNIX时间格式）的毫秒数提供。

您可以查找两个时间戳之间的任何内容，即比给定日期晚或早的任何内容，也可以在包含时间戳和打开时间戳之间进行选择。

支持Facet提取。 将提供“今天”、“本周”、“本月”、“最近3个月”、“今年”、“去年”和“比去年早”时段。

不支持过滤。

#### 属性 {#properties-3}

* **属性**

   相对路径 `DATE` 属性，例如 `jcr:lastModified`

* **下界**

   例如，用于检查属性的下限 `2014-10-01`

* **lowerOperation**

   &quot; `>`&quot;（较新）或&quot; `>=`“（at或更高版本）”适用于 `lowerBound`. 默认为 &quot; `>`&quot;.

* **上界**

   例如，检查属性的上限 `2014-10-01T12:15:00`

* **upperOperation**

   &quot; `<`&quot;（旧）或&quot; `<=`“（在或更早版本） `upperBound`. 默认为 &quot; `<`&quot;.

* **timeZone**

   未作为ISO-8601日期字符串提供时要使用的时区ID。 默认时区是系统的默认时区。

### 排除路径 {#excludepaths}

从其路径与正则表达式匹配的结果中排除节点。

这是仅限过滤的谓词，无法利用搜索索引。

不支持面提取。

#### 属性 {#properties-4}

* **排除路径**

   与结果路径匹配的正则表达式，从结果中排除匹配的路径。

### 全文 {#fulltext}

在全文索引中搜索术语。

不支持过滤。

不支持面提取。

#### 属性 {#properties-5}

* **全文**

   全文搜索词

* **relPath**

   属性或子节点中要搜索的相对路径。 此属性是可选的。

### 组 {#group}

用于生成嵌套条件。 组可以包含嵌套组。 查询生成器查询中的所有内容都会隐式置于根组中，根组可能具有 `p.or` 和 `p.not` 参数。

将两个属性中的任一属性与值匹配的示例：

```
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

从概念上讲 `(1_property` 或 `2_property)`.

嵌套群组的示例：

```
fulltext=Management
group.p.or=true
group.1_group.path=/content/geometrixx/en
group.1_group.type=cq:Page
group.2_group.path=/content/dam/geometrixx
group.2_group.type=dam:Asset
```

这会搜索术语“**管理**“” `/content/geometrixx/en` 或 `/content/dam/geometrixx`.

从概念上讲 `fulltext AND ( (path AND type) OR (path AND type) )`. 请注意，此类OR连接需要良好的索引才能获得性能。

#### 属性 {#properties-6}

* **p.or**

   如果设置为“ `true`“，组中只能有一个谓词匹配。 这默认为“ `false`&quot;表示必须匹配

* **p.not**

   如果设置为“ `true`&quot;，则它否定组(默认为“ `false`&quot;)

* **&lt;predicate>**

   添加嵌套谓词

* **N_&lt;predicate>**

   添加多个同时的嵌套谓词，如 `1_property, 2_property, ...`

### hasPermission {#haspermission}

将结果限制为当前会话具有指定 [JCR权限。](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

这是仅限过滤的谓词，无法利用搜索索引。 它不支持面提取。

#### 属性 {#properties-7}

* **hasPermission**

   以逗号分隔的JCR权限，当前用户会话必须对相关节点具有ALL权限；例如 `jcr:write`, `jcr:modifyAccessControl`

### 语言 {#language}

查找使用特定语言的CQ页面。 这会同时查看页面语言属性和页面路径，页面路径通常包括顶级站点结构中的语言或区域设置。

这是仅限过滤的谓词，无法利用搜索索引。

支持Facet提取。 将为每个唯一语言代码提供存储段。

#### 属性 {#properties-8}

* **语言**

   ISO语言代码，例如“ `de`&quot;

### 主资产 {#mainasset}

检查节点是DAM主资产还是子资产。 这基本上是“子资产”节点内部的每个节点。 请注意，这不会检查 `dam:Asset` 节点类型。 要使用此谓词，只需将“ `mainasset=true`&quot;或&quot; `mainasset=false`“，则没有其他属性。

这是仅限过滤的谓词，无法利用搜索索引。

支持Facet提取。 将为主资产和子资产提供2个存储段。

#### 属性 {#properties-9}

* **主资产**

   布尔值， &quot; `true`“ ” `false`“ ”（子资产）

### memberOf {#memberof}

查找属于特定 [sling资源收集](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

这是仅限过滤的谓词，无法利用搜索索引。 不支持面提取。

#### 属性 {#properties-10}

* **memberOf**

   Sling资源收集的路径

### nodename {#nodename}

在JCR节点名称上匹配。

支持Facet提取。 将为每个唯一节点名称（文件名）提供存储段。

#### 属性 {#properties-11}

* **nodename**

   允许使用通配符的节点名称模式： `*` =任何字符或无字符， `?` =任意字符， `[abc]` =仅在括号中显示字符

### notexpired {#notexpired}

通过检查JCR DATE属性是否大于或等于当前服务器时间来匹配项目。 这可用于检查“ `expiresAt`“称赞日期属性，并仅限于尚未过期的属性( `notexpired=true`)或已过期( `notexpired=false`)。

不支持过滤。

支持以与更改谓词相同的方式进行面提取。

#### 属性 {#properties-12}

* **notexpired**

   布尔值， &quot; `true`&quot;表示尚未过期（未来日期或等于日期）， &quot; `false`”(表示过期（过去的日期）（必需）

* **属性**

   相对路径 `DATE` 要检查的属性（必需）

### orderby {#orderby}

允许对结果进行排序。 如果需要按多个属性进行排序，则需要使用数字前缀多次添加此谓词，例如 `1_orderby=first`, `2_oderby=second`.

#### 属性 {#properties-13}

* **orderby**

   例如，由前导@指示的JCR属性名称 `@jcr:lastModified` 或 `@jcr:content/jcr:title`，或查询中的其他谓词，例如 `2_property`，排序对象

* **排序**

   排序方向，或&quot; `desc`&quot;表示降序或&quot; `asc`“表示升序（默认）

* **案例**

   如果设置为“ `ignore`&quot;将使排序不区分大小写，即“a”在“B”之前出现；如果为空或忽略，则排序区分大小写，这意味着“B”在“a”之前

### 路径 {#path}

在给定路径内搜索。

不支持面提取。

#### 属性 {#properties-14}

* **路径**

   路径模式；根据具体情况，整个子树将匹配(例如，附加 `//*` 在xpath中，但请注意，这不包括基本路径)（exact=false，默认值），或者只有精确的路径匹配项，该匹配项可以包含通配符( `*`);如果设置了自身，则将搜索包含基节点的整个子树

* **精确**

   if `exact` 为true/on，则精确路径必须匹配，但可以包含简单的通配符( `*`)，匹配名称，但不匹配“ `/`“；如果为false（默认），则包含所有子代（可选）

* **平整**

   仅搜索直接子项(例如附加“ `/*`&quot;(仅在&#39; `exact`&#39;不为true，可选)

* **self**

   搜索子树，但包含作为路径给定的基节点（无通配符）

### 属性 {#property}

与JCR属性及其值匹配。

支持Facet提取。 将为结果中的每个唯一属性值提供存储段。

#### 属性 {#properties-15}

* **属性**

   相对于属性的路径，例如 `jcr:title`

* **选定**

   值来检查属性；将JCR属性类型跟踪到字符串转化

* **N_value**

   use `1_value`, `2_value`,...检查多个值(与 `OR` 默认情况下，使用 `AND` if and=true)（自5.3起）

* **和**

   对于组合多个值，设置为true( `N_value`)和（从5.3开始）

* **操作**

   &quot;`equals`&quot;表示精确匹配（默认）， &quot; `unequals`&quot;表示不相等比较， &quot; `like`” `jcr:like` xpath函数（可选）， &quot; `not`“ ”(例如 &quot;`not(@prop)`&quot;在xpath中，值参数将被忽略)或&quot; `exists`“ for existence check(value can be true - property mest exist， default - or false - same as &quot; `not`&quot;)

* **深度**

   属性/相对路径可存在的通配符级别数(例如， `property=size depth=2` 将检查节点/大小、节点/&amp;ast;/size和node/&amp;ast;/&amp;ast;/&amp;ast;/size

### rangproperty {#rangeproperty}

将JCR属性与间隔匹配。 这适用于具有线性类型(如 `LONG`, `DOUBLE` 和 `DECIMAL`. 对于 `DATE` 请参阅具有优化日期格式输入的日期范围谓词。

您可以定义下限和上限，或者只定义其中一个。 操作(例如 也可以单独为下界和上界指定“小于”或“小于或等于”)。

不支持面提取。

#### 属性 {#properties-16}

* **属性**

   属性的相对路径

* **下界**

   下限检查的属性

* **lowerOperation**

   &quot; `>`&quot;（默认）或&quot; `>=`“，适用于 `lowerValue`

* **上界**

   上界检查属性

* **upperOperation**

   &quot; `<`&quot;（默认）或&quot; `<=`“，适用于 `lowerValue`

* **小数**

   &quot; `true`&quot;（如果选中的属性类型为“小数”）

### 相对变量 {#relativedaterange}

匹配 `JCR DATE` 使用相对于当前服务器时间的时间偏移对日期/时间间隔进行属性。 您可以指定 `lowerBound` 和 `upperBound` 使用毫秒值或bugzilla语法 `1s 2m 3h 4d 5w 6M 7y` （一秒、二分钟、三小时、四天、五个星期、六个月、七年）。 前缀为“ `-`&quot;表示当前时间之前的负偏移。 如果仅指定 `lowerBound` 或 `upperBound`，另一个将默认为0，这表示当前时间。

例如：

* `upperBound=1h` （否） `lowerBound`)会在下一小时内选择任何内容
* `lowerBound=-1d` （否） `upperBound`)会选择过去24小时内的任何内容
* `lowerBound=-6M` 和 `upperBound=-3M` 选择任何6个月到3个月的内容
* `lowerBound=-1500` 和 `upperBound=5500` 会选择过去1500毫秒到将来5500毫秒之间的任何值
* `lowerBound=1d` 和 `upperBound=2d` 会在后天选择任何东西

请注意，考虑时间不需要多年，所有月份都为30天。

不支持过滤。

支持以与更改谓词相同的方式进行面提取。

#### 属性 {#properties-17}

* **上界**

   以毫秒或以毫秒为单位的上限日期范围 `1s 2m 3h 4d 5w 6M 7y` （1秒、2分钟、3小时、4天、5周、6个月、7年）相对于当前服务器时间，使用“ — ”作为负偏移

* **下界**

   以毫秒或以毫秒为单位的下限日期 `1s 2m 3h 4d 5w 6M 7y` （1秒、2分钟、3小时、4天、5周、6个月、7年）相对于当前服务器时间，使用“ — ”作为负偏移

### 根 {#root}

根谓词组。 支持组的所有功能，并允许设置全局查询参数。

查询中从未使用名称“root”，它是隐式的。

#### 属性 {#properties-18}

* **p.offset**

   表示结果页面开始的数字，即要跳过的项目数

* **p.limit**

   表示页面大小的数字

* **p.guessTotal**

   建议：避免计算可能代价高昂的全部结果总数；一个数字，表示最多计数的总数（例如1000，表示用户对粗细大小和精确数字有足够的反馈，以获得较小的结果），或者“ `true`“ ”，以仅计算所需的最低值 `p.offset` + `p.limit`

* **p.摘录**

   如果设置为“ `true`“，在结果中包含全文摘录

* **p.hits**

   （仅适用于JSON Servlet）选择点击以JSON形式写入的方式，并使用这些标准点击（可通过ResultHitWriter服务扩展）：

   * **简单**:

      最小项目， `path`, `title`, `lastmodified`, `excerpt` （如果已设置）

   * **全部**:

      节点的SLING JSON渲染(带 `jcr:path` 指示点击的路径：默认情况下，仅列出节点的直接属性，包括包含更深层的树，其中包含 `p.nodedepth=N`，其中0表示整个无限子树；添加 `p.acls=true` 在给定结果项上包含当前会话的JCR权限(映射： `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`)

   * **选定属性**:

      仅指定 `p.properties`，这是相对路径的空格分隔（在URL中使用“+”）列表；如果相对路径的深度大于1，则表示为子对象；特殊的jcr:path属性包括点击的路径

### savedquery {#savedquery}

将持久化查询生成器查询的所有谓词作为子组谓词包含到当前查询中。

请注意，这不会执行额外的查询，而是扩展当前查询。

查询可以使用以编程方式持久保留 `QueryBuilder#storeQuery()`. 格式可以是多行String属性，也可以是 `nt:file` 节点，该节点将查询作为Java属性格式的文本文件。

不支持对保存查询的谓词进行分面提取。

#### 属性 {#properties-19}

* **savedquery**

   保存查询的路径(字符串属性或 `nt:file` node)

### 相似 {#similar}

使用JCR XPath的相似度搜索 `rep:similar()`.

不支持过滤。 不支持面提取。

#### 属性 {#properties-20}

* **相似**
要查找相似节点的节点的绝对路径

* **本地**
到子节点或 
`.` 对于当前节点(可选，默认值为“ `.`&quot;)

### 标记 {#tag}

通过指定标签标题路径，搜索带有一个或多个标签的内容。

支持Facet提取。 将使用每个唯一标记的当前标记标题路径为其提供分段。

#### 属性 {#properties-21}

* **标记**

   标记标题路径以查找，例如“资产属性：方向/横向”

* **N_value**

   use `1_value`, `2_value`,...检查多个标记(与 `OR` 默认情况下，使用 `AND` if and=true)（自5.6起）

* **属性**

   要查看的属性（或属性的相对路径）(默认为“ `cq:tags`&quot;)

### tagid {#tagid}

通过指定标记ID，搜索带有一个或多个标记的内容。

支持Facet提取。 将使用每个唯一标记的当前标记ID为其提供分段。

#### 属性 {#properties-22}

* **tagid**

   要查找的标记id，例如“ `properties:orientation/landscape`&quot;

* **N_value**

   use `1_value`, `2_value`,...检查多个标记(与 `OR` 默认情况下，使用 `AND` if and=true)（自5.6起）

* **属性**

   要查看的属性（或属性的相对路径）(默认为“ `cq:tags`&quot;)

### tagsearch {#tagsearch}

通过指定关键字，搜索带有一个或多个标记的内容。 这将首先在其标题中搜索包含这些关键词的标记，然后将结果限制为仅包含这些关键词的项目。

不支持面提取。

#### 属性 {#Properties-1}

* **tagsearch**

   在标记标题中搜索的关键词

* **属性**

   要查看的属性（或属性的相对路径）(默认为“ `cq:tags`&quot;)

* **朗**

   仅在特定本地化的标记标题中搜索(例如，&quot; `de`&quot;)

* **全部**

   （布尔）搜索整个标记全文，即所有标题、描述等。 (优先于&quot;l&quot; `ang`&quot;)

### 类型 {#type}

将结果限制为特定的JCR节点类型（主节点类型或混合类型）。 此外，还会查找该节点类型的子类型。 请注意，为了高效执行，存储库搜索索引需要涵盖节点类型。

支持Facet提取。 将为结果中的每个唯一类型提供存储段。

#### 属性 {#Properties-2}

* **类型**

   要搜索的节点类型或混合名称，例如 `cq:Page`
