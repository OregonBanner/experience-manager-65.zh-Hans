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
>本页上的信息并非详尽无遗。
>
>有关完整信息，请参阅下面的列表 **可用谓词** 在Query Builder Debugger控制台上；例如，位于：
>* [http://localhost:4502/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)
>
>例如，请参阅：
>
>* [http://localhost:4502/system/console/services?filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29](http://localhost:4502/system/console/services?filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29)


## 常规 {#general}

* [根](#root)
* [组](#group)
* [orderby](#orderby)

## 谓词 {#predicates}

* [布尔属性](/help/sites-developing/querybuilder-predicate-reference.md#boolproperty)
* [contentfragment](/help/sites-developing/querybuilder-predicate-reference.md#contentfragment)
* [dateComparison](/help/sites-developing/querybuilder-predicate-reference.md#datecomparison)
* [日期范围](/help/sites-developing/querybuilder-predicate-reference.md#daterange)
* [排除路径](/help/sites-developing/querybuilder-predicate-reference.md#excludepaths)
* [全文](/help/sites-developing/querybuilder-predicate-reference.md#fulltext)
* [hasPermission](/help/sites-developing/querybuilder-predicate-reference.md#haspermission)
* [语言](/help/sites-developing/querybuilder-predicate-reference.md#language)
* [mainasset](/help/sites-developing/querybuilder-predicate-reference.md#mainasset)
* [memberOf](/help/sites-developing/querybuilder-predicate-reference.md#memberof)
* [nodename](/help/sites-developing/querybuilder-predicate-reference.md#nodename)
* [notexpired](/help/sites-developing/querybuilder-predicate-reference.md#notexpired)
* [路径](/help/sites-developing/querybuilder-predicate-reference.md#path)
* [属性](/help/sites-developing/querybuilder-predicate-reference.md#property)
* [rangeproperty](/help/sites-developing/querybuilder-predicate-reference.md#rangeproperty)
* [相对日期范围](/help/sites-developing/querybuilder-predicate-reference.md#relativedaterange)
* [savedquery](/help/sites-developing/querybuilder-predicate-reference.md#savedquery)
* [相似](/help/sites-developing/querybuilder-predicate-reference.md#similar)
* [标记](/help/sites-developing/querybuilder-predicate-reference.md#tag)
* [tagid](/help/sites-developing/querybuilder-predicate-reference.md#tagid)
* [tagsearch](/help/sites-developing/querybuilder-predicate-reference.md#tagsearch)
* [类型](/help/sites-developing/querybuilder-predicate-reference.md#type)

### 布尔属性 {#boolproperty}

匹配JCR BOOLEAN属性。 仅接受值&quot; `true`“ ”和“ ” `false`“。 如果为“ `false`“，如果属性具有值“”，则它将匹配 `false`”或者如果它根本不存在。 这对于检查仅在启用时设置的布尔标志非常有用。

继承的&quot; `operation`”参数没有意义。

支持Facet提取。 将为每个提供存储段 `true` 或 `false` 值，但仅适用于现有属性。

#### 属性 {#properties}

* **布尔属性**
属性的相对路径，例如 
`myFeatureEnabled` 或 `jcr:content/myFeatureEnabled`

* **值**
要检查属性的值， &quot; 
`true`&quot; 或 &quot; `false`&quot;

### contentfragment {#contentfragment}

将结果限制为内容片段。

不支持筛选。

不支持Facet提取。

#### 属性 {#properties-1}

* **contentfragment**
它可以与任何值一起使用来检查内容片段。

### dateComparison {#datecomparison}

将两个JCR DATE属性相互进行比较。 可以测试它们是否相等、不相等、大于或大于或等于。

这是仅用于筛选的谓词，不能利用搜索索引。

#### 属性 {#properties-2}

* **property1**

   指向第一个日期属性的路径

* **property2**

   指向第二个日期属性的路径

* **操作**

   ” `equals`“”表示完全匹配，“ `!=`“不平等比较” `greater`&quot;对于property1，大于属性2， &quot; `>=`”表示属性1大于或等于property2。 默认值为 &quot; `equals`&quot;.

### 日期范围 {#daterange}

根据日期/时间间隔匹配JCR DATE属性。 这使用ISO8601格式表示日期和时间( `YYYY-MM-DDTHH:mm:ss.SSSZ`)并允许部分表示，如 `YYYY-MM-DD`. 或者，时间戳可以按UTC时区（unix时间格式）提供自1970年以来的毫秒数。

您可以查找两个时间戳之间的任何内容，查找比给定日期更新或旧的任何内容，还可以选择包含时间间隔和未包含时间间隔。

支持Facet提取。 将提供桶“今天”、“本周”、“本月”、“过去3个月”、“今年”、“去年”和“比去年早”。

不支持筛选。

#### 属性 {#properties-3}

* **属性**

   相对路径 `DATE` 属性，例如 `jcr:lastModified`

* **下限**

   用于检查属性的下限日期，例如 `2014-10-01`

* **lowerOperation**

   ” `>`“（较新）或” `>=`“（在或更高），适用于 `lowerBound`. 默认为&quot; `>`“。

* **上限**

   检查属性的上限，例如 `2014-10-01T12:15:00`

* **upperOperation**

   ” `<`“（更早）或” `<=`“（等于或大于），适用于 `upperBound`. 默认为&quot; `<`“。

* **时区**

   未作为ISO-8601日期字符串提供时要使用的时区ID。 默认值是系统的默认时区。

### 排除路径 {#excludepaths}

从结果中排除路径与正则表达式匹配的节点。

这是仅用于筛选的谓词，不能利用搜索索引。

不支持Facet提取。

#### 属性 {#properties-4}

* **排除路径**

   正则表达式与结果路径匹配，不包括结果中的匹配路径。

### 全文 {#fulltext}

搜索全文索引中的术语。

不支持筛选。

不支持Facet提取。

#### 属性 {#properties-5}

* **全文**

   全文搜索词

* **relPath**

   在属性或子节点中搜索的相对路径。 此属性是可选的。

### 组 {#group}

允许生成嵌套条件。 组可以包含嵌套的组。 Querybuilder查询中的所有内容都隐式位于根组中，根组中可以具有 `p.or` 和 `p.not` 参数也是如此。

将两个属性之一与值匹配的示例：

```
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

这是概念上的 `(1_property` 或 `2_property)`.

嵌套组示例：

```
fulltext=Management
group.p.or=true
group.1_group.path=/content/geometrixx/en
group.1_group.type=cq:Page
group.2_group.path=/content/dam/geometrixx
group.2_group.type=dam:Asset
```

这将搜索术语&quot;**管理**“（在中的页面内） `/content/geometrixx/en` 或中的资产 `/content/dam/geometrixx`.

这是概念上的 `fulltext AND ( (path AND type) OR (path AND type) )`. 请注意，此类OR连接需要良好的性能索引。

#### 属性 {#properties-6}

* **p.or**

   如果设置为&quot; `true`“”，组中只有一个谓词必须匹配。 默认为&quot; `false`“，表示所有参数必须匹配

* **p.not**

   如果设置为&quot; `true`“”，这将使组无效(默认为“” `false`&quot;)

* **&lt;predicate>**

   添加嵌套谓词

* **N_&lt;predicate>**

   同时添加多个嵌套谓词，如 `1_property, 2_property, ...`

### hasPermission {#haspermission}

将结果限制在当前会话具有指定的项目 [JCR权限。](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

这是仅用于筛选的谓词，不能利用搜索索引。 它不支持Facet提取。

#### 属性 {#properties-7}

* **hasPermission**

   当前用户会话“全部”必须为相关节点具有的逗号分隔JCR权限；例如 `jcr:write`， `jcr:modifyAccessControl`

### 语言 {#language}

查找采用特定语言的CQ页面。 这会查看页面语言属性和页面路径，后者通常包括顶级网站结构中的语言或区域设置。

这是仅用于筛选的谓词，不能利用搜索索引。

支持Facet提取。 将为每个唯一语言代码提供存储段。

#### 属性 {#properties-8}

* **语言**

   ISO语言代码，例如“ `de`”

### mainasset {#mainasset}

检查节点是否为DAM主资产而不是子资产。 这基本上是每个不在“子资产”节点内的节点。 请注意，这不会检查 `dam:Asset` 节点类型。 要使用此谓词，只需设置“ `mainasset=true`“或” `mainasset=false`“，没有其他属性。

这是仅用于筛选的谓词，不能利用搜索索引。

支持Facet提取。 将为主资源和子资源提供2个存储段。

#### 属性 {#properties-9}

* **mainasset**

   布尔型， &quot; `true`”表示主资产，“ `false`”表示子资产

### memberOf {#memberof}

查找属于特定成员的项目 [sling资源集合](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

这是仅用于筛选的谓词，不能利用搜索索引。 不支持Facet提取。

#### 属性 {#properties-10}

* **memberOf**

   Sling资源集合的路径

### nodename {#nodename}

匹配JCR节点名称。

支持Facet提取。 将为每个唯一节点名称（文件名）提供存储段。

#### 属性 {#properties-11}

* **nodename**

   允许使用通配符的节点名称模式： `*` =任何字符或无字符， `?` =任何字符， `[abc]` =仅括号中的字符

### notexpired {#notexpired}

通过检查JCR DATE属性是否大于或等于当前服务器时间匹配项。 这可用于检查&quot; `expiresAt`”赞日期属性，并仅限尚未过期的属性( `notexpired=true`)或已过期的( `notexpired=false`)。

不支持筛选。

支持方面提取的方式与日期范围谓词相同。

#### 属性 {#properties-12}

* **notexpired**

   布尔型， &quot; `true`”表示尚未过期（将来的日期或等于），“ `false`”表示已过期（过去日期）（必需）

* **属性**

   相对路径 `DATE` 要检查的属性（必需）

### orderby {#orderby}

允许对结果进行排序。 如果需要按多个属性排序，则需要使用数字前缀多次添加此谓词，例如 `1_orderby=first`， `2_oderby=second`.

#### 属性 {#properties-13}

* **orderby**

   以@开头表示的JCR属性名称，例如 `@jcr:lastModified` 或 `@jcr:content/jcr:title`或查询中的其他谓词，例如 `2_property`，对其排序

* **排序**

   排序方向，“” `desc`”表示降序或“” `asc`“”表示升序（默认）

* **case**

   如果设置为&quot; `ignore`“ ”将使排序不区分大小写，这意味着“A”在“B”之前；如果为空或缺席，则排序区分大小写，这意味着“B”在“A”之前

### 路径 {#path}

在给定路径内搜索。

不支持Facet提取。

#### 属性 {#properties-14}

* **路径**

   路径模式；根据具体情况，整个子树都将匹配(如附加 `//*` 在xpath中，但请注意，这不包括基本路径)（exact=false，默认）或仅包括精确路径匹配，其中可以包括通配符( `*`)；如果设置了self，则将搜索包含基节点的整个子树

* **精确**

   如果 `exact` 为true/on，则确切路径必须匹配，但它可以包含简单的通配符( `*`)，名称匹配，但不匹配&quot; `/`&quot;；如果为false（默认），则包含所有后代（可选）

* **平坦**

   仅搜索直接子项(如附加&quot; `/*`在xpath中为“”)(仅在“ `exact`&#39;不为true，可选)

* **self**

   搜索子树，但包含作为路径给定的基本节点（无通配符）

### 属性 {#property}

匹配JCR属性及其值。

支持Facet提取。 将为结果中的每个唯一属性值提供存储段。

#### 属性 {#properties-15}

* **属性**

   属性的相对路径，例如 `jcr:title`

* **值**

   要检查属性的值；遵循JCR属性类型到字符串的转换

* **N_value**

   使用 `1_value`， `2_value`， ...以检查多个值(与 `OR` 默认情况下，使用 `AND` if和=true)（从5.3开始）

* **和**

   设置为true可组合多个值( `N_value`)与AND（从5.3开始）

* **操作**

   ”`equals`“”表示完全匹配（默认）， “ `unequals`“不平等比较” `like`“”，用于使用 `jcr:like` xpath函数（可选）， &quot; `not`”表示无匹配项(例如， ”`not(@prop)`“在xpath中，值参数将被忽略)或” `exists`“进行存在性检查(值可以为true — 属性必须存在，默认值 — 或false — 与”相同 `not`&quot;)

* **深度**

   属性/相对路径可以存在的通配符级别数(例如， `property=size depth=2` 将检查节点/大小、节点/&amp;ast；/大小和节点/&amp;ast；/&amp;ast；/大小)

### rangeproperty {#rangeproperty}

将JCR属性与间隔进行匹配。 这适用于具有线性类型的属性，例如 `LONG`， `DOUBLE` 和 `DECIMAL`. 对象 `DATE` 请参阅已优化日期格式输入的日期范围谓词。

您可以定义下限和上限，也可以只定义其中一个。 操作(例如 也可以为下限和上限分别指定“小于”或“小于或等于”)。

不支持Facet提取。

#### 属性 {#properties-16}

* **属性**

   属性的相对路径

* **下限**

   检查属性的下限

* **lowerOperation**

   ” `>`“（默认）或” `>=`&quot;，适用于 `lowerValue`

* **上限**

   检查属性的上限

* **upperOperation**

   ” `<`“（默认）或” `<=`&quot;，适用于 `lowerValue`

* **十进制**

   ” `true`&quot;（如果检查的属性是Decimal类型）

### 相对日期范围 {#relativedaterange}

匹配 `JCR DATE` 属性针对某个日期/时间间隔使用相对于当前服务器时间的时间偏移。 您可以指定 `lowerBound` 和 `upperBound` 使用毫秒值或bugzilla语法 `1s 2m 3h 4d 5w 6M 7y` （一秒、两分钟、三小时、四天、五周、六个月、七年）。 前缀为“ `-`”表示当前时间之前的负偏移。 如果您只指定 `lowerBound` 或 `upperBound`，则另一个将默认为0，表示当前时间。

例如：

* `upperBound=1h` (无 `lowerBound`)将选择下一小时内的任何内容
* `lowerBound=-1d` (无 `upperBound`)会选择过去24小时内的任何内容
* `lowerBound=-6M` 和 `upperBound=-3M` 会选择6个月到3个月之前的任何时间
* `lowerBound=-1500` 和 `upperBound=5500` 将选择过去1500毫秒到未来5500毫秒之间的任何值
* `lowerBound=1d` 和 `upperBound=2d` 会选择后天的任何内容

请注意，不考虑闰年，所有月份都是30天。

不支持筛选。

支持方面提取的方式与日期范围谓词相同。

#### 属性 {#properties-17}

* **上限**

   日期上限（以毫秒为单位）或 `1s 2m 3h 4d 5w 6M 7y` 相对于当前服务器时间（一秒、两分钟、三小时、四天、五周、六个月、七年），使用“ — ”表示负偏移

* **下限**

   以毫秒为单位的日期下限或 `1s 2m 3h 4d 5w 6M 7y` 相对于当前服务器时间（一秒、两分钟、三小时、四天、五周、六个月、七年），使用“ — ”表示负偏移

### 根 {#root}

根谓词组。 支持组的所有功能，并允许设置全局查询参数。

查询中从未使用名称“root”，它是隐式的。

#### 属性 {#properties-18}

* **p.offset**

   指示结果页面开始的数字，即要跳过多少项

* **p.limit**

   指示页面大小的数字

* **p.guessTotal**

   建议：避免计算完整的结果总数，因为这可能很昂贵；要么是指示要计算的最大总数的数字（例如1000，一个数字，该数字向用户提供对粗略大小和精确数字的足够反馈，以获得较小结果），要么是“ `true`”以仅计数到所需的最小值 `p.offset` + `p.limit`

* **p.excerpt**

   如果设置为&quot; `true`&quot;，在结果中包含全文摘录

* **点击**

   （仅适用于JSON servlet）选择点击作为JSON写入的方式，包括以下标准点击（可通过ResultHitWriter服务扩展）：

   * **简单**:

      最小项目，如 `path`， `title`， `lastmodified`， `excerpt` （如果已设置）

   * **全部**:

      节点的Sling JSON渲染，使用 `jcr:path` 指示点击的路径：默认情况下，仅列出节点的直接属性，包括更深的树 `p.nodedepth=N`，0表示整个、无限子树；添加 `p.acls=true` 在给定结果项上包含当前会话的JCR权限(映射： `create` = `add_node`， `modify` = `set_property`， `delete` = `remove`)

   * **选定属性**:

      仅指定属性 `p.properties`，以空格分隔（在URL中使用“+”）的相对路径列表；如果相对路径的深度大于1，则这些路径将显示为子对象；特殊的jcr：path属性包括点击的路径

### savedquery {#savedquery}

将持久查询生成器查询的所有谓词作为子组谓词包含到当前查询中。

请注意，这不会执行额外的查询，但会扩展当前查询。

可以使用以下编程方式持久查询 `QueryBuilder#storeQuery()`. 格式可以是多行字符串属性或 `nt:file` 以Java属性格式将查询作为文本文件包含的节点。

不支持对已保存查询的谓词进行Facet提取。

#### 属性 {#properties-19}

* **savedquery**

   已保存查询的路径(字符串属性或 `nt:file` 节点)

### 相似 {#similar}

使用JCR XPath的相似性搜索 `rep:similar()`.

不支持筛选。 不支持Facet提取。

#### 属性 {#properties-20}

* **相似**
要查找相似节点的节点的绝对路径

* **本地**
子节点或子节点的相对路径 
`.` （可选，默认为“”） `.`&quot;)

### 标记 {#tag}

通过指定标记标题路径，搜索使用一个或多个标记标记的内容。

支持Facet提取。 将为每个唯一标记提供存储段，使用其当前标记标题路径。

#### 属性 {#properties-21}

* **标记**

   要查找的标记标题路径，例如“资产属性：方向/横向”

* **N_value**

   使用 `1_value`， `2_value`， ...以检查多个标记(与 `OR` 默认情况下，使用 `AND` if和=true)（从5.6开始）

* **属性**

   要查看的属性（或属性的相对路径）(默认为&quot; `cq:tags`&quot;)

### tagid {#tagid}

通过指定标记ID搜索使用一个或多个标记标记的内容。

支持Facet提取。 将使用每个唯一标记的当前标记ID为其提供存储段。

#### 属性 {#properties-22}

* **tagid**

   要查找的标记ID，例如“ `properties:orientation/landscape`”

* **N_value**

   使用 `1_value`， `2_value`， ...以检查多个tagid(与 `OR` 默认情况下，使用 `AND` if和=true)（从5.6开始）

* **属性**

   要查看的属性（或属性的相对路径）(默认为&quot; `cq:tags`&quot;)

### tagsearch {#tagsearch}

通过指定关键字，搜索带有一个或多个标记的内容。 这将首先搜索其标题中包含这些关键字的标记，然后将结果限制为仅具有这些标记的项目。

不支持Facet提取。

#### 属性 {#Properties-1}

* **tagsearch**

   要在标记标题中搜索的关键字

* **属性**

   要查看的属性（或属性的相对路径）(默认为&quot; `cq:tags`&quot;)

* **lang**

   仅搜索特定本地化的标记标题(例如“ `de`&quot;)

* **全部**

   （布尔）搜索整个标记全文，即所有标题、描述等。 (优先于“l” `ang`&quot;)

### 类型 {#type}

将结果限制为特定的JCR节点类型，包括主节点类型或mixin类型。 这还将查找该节点类型的子类型。 请注意，存储库搜索索引需要包含节点类型才能有效执行。

支持Facet提取。 将为结果中的每个唯一类型提供存储段。

#### 属性 {#Properties-2}

* **类型**

   要搜索的节点类型或mixin名称，例如 `cq:Page`
