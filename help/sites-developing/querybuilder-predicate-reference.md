---
title: 查询 Builder谓词引用
seo-title: 查询 Builder谓词引用
description: 完整的谓词引用，用于查询 Builder API。
seo-description: 完整的谓词引用，用于查询 Builder API。
uuid: af0e269e-7d52-4032-b22e-801c7b5dccfa
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: 94a05894-743a-4ace-a292-bfee90ba9068
translation-type: tm+mt
source-git-commit: 571a48790c4977e97abec24fe88407b5b6376108
workflow-type: tm+mt
source-wordcount: '2323'
ht-degree: 3%

---


# 查询 Builder谓词引用{#query-builder-predicate-reference}

## 常规 {#general}

* [根](#root)
* [组](#group)
* [orderby](#orderby)

## 谓词{#predicates}

* [boolproperty](/help/sites-developing/querybuilder-predicate-reference.md#boolproperty)
* [contentfragment](/help/sites-developing/querybuilder-predicate-reference.md#contentfragment)
* [dateComparison](/help/sites-developing/querybuilder-predicate-reference.md#datecomparison)
* [达特朗格](/help/sites-developing/querybuilder-predicate-reference.md#daterange)
* [excludepath](/help/sites-developing/querybuilder-predicate-reference.md#excludepaths)
* [全文](/help/sites-developing/querybuilder-predicate-reference.md#fulltext)
* [hasPermission](/help/sites-developing/querybuilder-predicate-reference.md#haspermission)
* [语言](/help/sites-developing/querybuilder-predicate-reference.md#language)
* [mainasset](/help/sites-developing/querybuilder-predicate-reference.md#mainasset)
* [memberOf](/help/sites-developing/querybuilder-predicate-reference.md#memberof)
* [诺登](/help/sites-developing/querybuilder-predicate-reference.md#nodename)
* [notexpired](/help/sites-developing/querybuilder-predicate-reference.md#notexpired)
* [路径](/help/sites-developing/querybuilder-predicate-reference.md#path)
* [属性](/help/sites-developing/querybuilder-predicate-reference.md#property)
* [牧场属](/help/sites-developing/querybuilder-predicate-reference.md#rangeproperty)
* [相对](/help/sites-developing/querybuilder-predicate-reference.md#relativedaterange)
* [savedquery](/help/sites-developing/querybuilder-predicate-reference.md#savedquery)
* [相似](/help/sites-developing/querybuilder-predicate-reference.md#similar)
* [标签](/help/sites-developing/querybuilder-predicate-reference.md#tag)
* [tagid](/help/sites-developing/querybuilder-predicate-reference.md#tagid)
* [tagsearch](/help/sites-developing/querybuilder-predicate-reference.md#tagsearch)
* [类型](/help/sites-developing/querybuilder-predicate-reference.md#type)

### boolproperty {#boolproperty}

JCR BOOLEAN属性上的匹配。 仅接受值&quot; `true`&quot;和&quot; `false`&quot;。 如果是“`false`”，则如果属性的值为“ `false`”，或者该属性根本不存在，则匹配项。 这对于检查仅在启用时设置的布尔标志非常有用。

继承的“ `operation`”参数没有含义。

支持facet提取。 将为每个`true`或`false`值提供存储段，但仅为现有属性提供。

#### 属性 {#properties}

* ****
boolproperty相对于属性的路径，例如 
`myFeatureEnabled` 或 `jcr:content/myFeatureEnabled`

* ****
用于检查属性的值， &quot; 
`true`&quot; 或 &quot; `false`&quot;

### contentfragment {#contentfragment}

将结果限制为内容片段。

不支持筛选。

不支持facet提取。

#### 属性 {#properties-1}

* ****
contentfragment它可以与任何值一起使用来检查内容片段。

### dateComparison {#datecomparison}

将两个JCR DATE属性相互比较。 可以测试它们是否相等、不等、是否大于或等于。

这是仅筛选谓词，无法利用搜索索引。

#### 属性 {#properties-2}

* **property1**

   第一个日期属性的路径

* **property2**

   路径到第二个日期属性

* **操作**

   &quot; `equals`&quot;表示精确匹配，&quot; `!=`&quot;表示不相等比较，&quot; `greater`&quot;表示属性1大于属性2,&quot; `>=`&quot;表示属性1大于或等于属性2。 默认值为 &quot; `equals`&quot;.

### daterange {#daterange}

根据日期/时间间隔匹配JCR DATE属性。 它使用ISO8601
格式(`YYYY-MM-DDTHH:mm:ss.SSSZ`)，并允许部分表示，如`YYYY-MM-DD`。 或者，时间戳可以以1970年以来的毫秒数形式提供，以UTC时区（unix时间格式）表示。

您可以在两个时间戳之间查找任何内容，即任何比给定日期更新或更旧的内容，还可以在包含时间间隔和打开时间间隔之间进行选择。

支持facet提取。 将提供“今天”、“本周”、“本月”、“过去3个月”、“今年”、“去年”和“比去年更早”的时段。

不支持筛选。

#### 属性 {#properties-3}

* **属性**

   `DATE`属性的相对路径，例如`jcr:lastModified`

* **lowerBound**

   lower date bound to check属性，例如`2014-10-01`

* **lowerOperation**

   &quot; `>`&quot;（较新）或&quot; `>=`&quot;（at或较新）适用于`lowerBound`。 默认为 &quot; `>`&quot;.

* **上界**

   检查属性（例如`2014-10-01T12:15:00`）

* **upperOperation**

   &quot; `<`&quot;（旧）或&quot; `<=`&quot;（或旧）适用于`upperBound`。 默认为 &quot; `<`&quot;.

* **timeZone**

   未作为ISO-8601日期字符串给定时要使用的时区ID。 默认值是系统的默认时区。

### excludepaths {#excludepaths}

从其路径与常规表达式匹配的结果中排除节点。

这是仅筛选谓词，无法利用搜索索引。

不支持facet提取。

#### 属性 {#properties-4}

* **excludepath**

   常规表达式与结果路径匹配，从结果中排除匹配路径。

### 全文{#fulltext}

在全文索引中搜索词。

不支持筛选。

不支持facet提取。

#### 属性 {#properties-5}

* **全文**

   全文搜索词

* **relPath**

   要在属性或子节点中搜索的相对路径。 此属性是可选的。

### 组 {#group}

允许构建嵌套条件。 组可以包含嵌套组。 querybuilder查询中的所有内容都隐式地位于根组中，根组中也可以有`p.or`和`p.not`参数。

将两个属性中的任何一个与一个值匹配的示例：

```
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

从概念上讲，这是`(1_property`或`2_property)`。

嵌套用户组的示例：

```
fulltext=Management
group.p.or=true
group.1_group.path=/content/geometrixx/en
group.1_group.type=cq:Page
group.2_group.path=/content/dam/geometrixx
group.2_group.type=dam:Asset
```

这将搜索`/content/geometrixx/en`中的页面或`/content/dam/geometrixx`中的资产中的术语“**Management**”。

从概念上讲，这是`fulltext AND ( (path AND type) OR (path AND type) )`。 请注意，此类OR连接需要良好的性能索引。

#### 属性 {#properties-6}

* **p.or**

   如果设置为“`true`”，则组中只能有一个谓词匹配。 此默认值为“ `false`”，表示所有项必须匹配

* **p.not**

   如果设置为“ `true`”，则会对组进行重新排序（默认为“ `false`”）

* **&lt;predicate>**

   添加嵌套谓词

* **N_&lt;predicate>**

   添加多个同时嵌套的谓词，如`1_property, 2_property, ...`

### hasPermission {#haspermission}

将结果限制为当前会话具有指定[JCR权限的项目。](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

这是仅筛选谓词，无法利用搜索索引。 它不支持facet提取。

#### 属性 {#properties-7}

* **hasPermission**

   当前用户会话必须具有的以逗号分隔的JCR权限，对于所讨论的节点，ALL必须具有该权限；例如`jcr:write`, `jcr:modifyAccessControl`

### 语言 {#language}

查找特定语言的CQ页面。 这会查看页面语言属性和页面路径，页面路径通常包括顶级站点结构中的语言或区域设置。

这是仅筛选谓词，无法利用搜索索引。

支持facet提取。 将为每个唯一语言代码提供存储段。

#### 属性 {#properties-8}

* **语言**

   ISO语言代码，例如&quot; `de`&quot;

### mainasset {#mainasset}

检查节点是DAM主资产还是子资产。 这基本上是不在“子资产”节点内的每个节点。 请注意，这不会检查`dam:Asset`节点类型。 要使用此谓词，只需设置“ `mainasset=true`”或“ `mainasset=false`”，就不再有其他属性。

这是仅筛选谓词，无法利用搜索索引。

支持facet提取。 将为主资产和子资产提供2个存储段。

#### 属性 {#properties-9}

* **mainasset**

   布尔值，“ `true`”（对于主资产），“ `false`”（对于子资产）

### memberOf {#memberof}

查找特定[sling资源集合](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/resource/collection/ResourceCollection.html)的成员项目。

这是仅筛选谓词，无法利用搜索索引。 不支持facet提取。

#### 属性 {#properties-10}

* **memberOf**

   Sling资源收集路径

### nodename {#nodename}

JCR节点名称上的匹配项。

支持facet提取。 将为每个唯一节点名称（文件名）提供存储段。

#### 属性 {#properties-11}

* **诺登**

   允许通配符的节点名模式：`*` =任意或无字符，`?` =任意字符，`[abc]` =仅在括号中有字符

### notextpired {#notexpired}

通过检查JCR DATE属性是否大于或等于当前服务器时间来匹配项。 这可用于检查“`expiresAt`”类似日期属性，并仅限于尚未过期(`notexpired=true`)或已过期(`notexpired=false`)的属性。

不支持筛选。

支持彩块化提取，方式与更改谓词相同。

#### 属性 {#properties-12}

* **notexpired**

   布尔值，&quot; `true`&quot;表示尚未过期（将来或等于的日期），&quot; `false`&quot;表示过期（过去的日期）（必需）

* **属性**

   要检查的`DATE`属性的相对路径（必需）

### orderby {#orderby}

允许对结果进行排序。 如果需要按多个属性排序，则需要使用数字前缀多次添加此谓词，如`1_orderby=first`、`2_oderby=second`。

#### 属性 {#properties-13}

* **orderby**

   JCR属性名称由行距@（例如`@jcr:lastModified`或`@jcr:content/jcr:title`）指示，或者查询中的另一个谓词（例如`2_property`）指示，要对其进行排序

* **排序**

   排序方向，降序为&quot; `desc`&quot;，升序为&quot; `asc`&quot;（默认）

* **案**

   如果设置为“`ignore`”，则排序不区分大小写，表示“a”在“B”之前；如果为空或未排除，则排序区分大小写，即“B”排在“a”之前

### 路径 {#path}

在给定路径内搜索。

不支持facet提取。

#### 属性 {#properties-14}

* **路径**

   路径模式；根据具体情况，整个子树将匹配（如在xpath中附加`//*`，但请注意，这不包括基本路径）（exact=false，默认）或仅匹配精确路径(可以包括通配符(`*`));如果设置为“自我”，则将搜索包含基节点的整个子树

* **精确**

   如果`exact`为true/on，则精确路径必须匹配，但它可以包含简单的通配符(`*`)，这些通配符与名称匹配，但不能包含&quot; `/`&quot;;如果为false（默认），则包括所有子项（可选）

* **平**

   仅搜索直接子项（如xpath中附加“ `/*`”）（仅在“ `exact`”不为true时使用，可选）

* **self**

   搜索子树，但包括作为路径给定的基节点（无通配符）

### 属性 {#property}

匹配JCR属性及其值。

支持facet提取。 将为结果中的每个唯一属性值提供存储段。

#### 属性 {#properties-15}

* **属性**

   属性的相对路径，例如`jcr:title`

* **选定**

   值以检查属性；跟在JCR属性类型到字符串转换之后

* **N_value**

   使用`1_value`、`2_value`、...检查多个值（默认情况下与`OR`组合，如果为`AND`且为true）（自5.3起）

* **和**

   设置为true，将多个值(`N_value`)与AND（自5.3开始）组合

* **操作**

   “ `equals`”(对于exactmatch(default))，“ `unequals`”（对于不相等的比较），“ `like`”（对于使用`jcr:like` xpath函数），“ `not`”（对于不匹配），“ ”(例如 &quot; `not(@prop)`&quot;（在xpath中，值参数将被忽略）或&quot; `exists`&quot;（用于存在检查）（值可以为true — 属性，默认值 — 或false — 与&quot; `not`&quot;相同）

* **深度**

   属性/相对路径可存在的通配符级别数（例如，`property=size depth=2`将检查节点/大小、node/&amp;ast;/size和node/&amp;ast;/&amp;ast;/size）

### rangeproperty {#rangeproperty}

将JCR属性与间隔匹配。 这适用于线性类型（如`LONG`、`DOUBLE`和`DECIMAL`）的属性。 对于`DATE`，请参阅已优化日期格式输入的更改谓词。

您可以定义下界和上界，也可以只定义其中一个。 操作(例如 也可为下界和上界分别指定“小于”或“小于或等于”)。

不支持facet提取。

#### 属性 {#properties-16}

* **属性**

   属性的相对路径

* **lowerBound**

   下界检查属性

* **lowerOperation**

   &quot; `>`&quot;（默认）或&quot; `>=`&quot;应用于`lowerValue`

* **上界**

   上界检查属性

* **upperOperation**

   &quot; `<`&quot;（默认）或&quot; `<=`&quot;应用于`lowerValue`

* **小数**

   &quot; `true`&quot;（如果选中的属性类型为Decimal）

### 相对变量{#relativedaterange}

使用相对于当前服务器时间的时间偏移将`JCR DATE`属性与日期/时间间隔匹配。 您可以使用毫秒值或bugzilla语法`1s 2m 3h 4d 5w 6M 7y`（一秒钟、两分钟、三小时、四天、五周、六个月、七年）来指定`lowerBound`和`upperBound`。 前缀为&quot; `-`&quot;，表示当前时间之前的负偏移。 如果仅指定`lowerBound`或`upperBound`，则另一个将默认为0，表示当前时间。

例如：

* `upperBound=1h` (并且不 `lowerBound`会)将在下一小时内选择任何内容
* `lowerBound=-1d` (并且不 `upperBound`会)在过去24小时内选择任何内容
* `lowerBound=-6M` 选 `upperBound=-3M` 择任何6个月到3个月
* `lowerBound=-1500` 并 `upperBound=5500` 且选择过去1500毫秒和将来5500毫秒之间的任何内容
* `lowerBound=1d` 然 `upperBound=2d` 后在后天选择任何

请注意，考虑时间不是多年，所有月份都是30天。

不支持筛选。

支持彩块化提取，方式与更改谓词相同。

#### 属性 {#properties-17}

* **上界**

   相对于当前服务器时间，以毫秒为界或`1s 2m 3h 4d 5w 6M 7y`（一秒、二分钟、三小时、四天、五周、六个月、七年）

* **lowerBound**

   相对于当前服务器时间的较低日期范围（毫秒）或`1s 2m 3h 4d 5w 6M 7y`（一秒、二分钟、三小时、四天、五周、六个月、七年），使用“ — ”表示负偏移

### 根{#root}

根谓词组。 支持组的所有功能并允许设置全局查询参数。

名称“root”从未在查询中使用，它是隐式的。

#### 属性 {#properties-18}

* **p.offset**

   表示结果页面开始的数字，即要跳过的项目数

* **p.limit**

   指示页面大小的数字

* **p.guessTotal**

   建议：避免计算全部结果总和，代价高昂；一个数字，表示最大总计计算（例如1000，一个数字，它为用户提供了对粗略大小和精确数字的足够反馈，以便获得较小的结果），另一个数字是&quot; `true`&quot;，以仅计算最小必要值`p.offset` + `p.limit`

* **p.exper**

   如果设置为“`true`”，则在结果中包含全文摘录

* **p.hits**

   （仅适用于JSON servlet）选择将点击写入JSON的方式，使用这些标准点击（可通过ResultHitWriter服务扩展）：

   * **简单**:

      诸如`path`、`title`、`lastmodified`、`excerpt`（如果已设置）等最小项

   * **全部**:

      节点的sling JSON渲染，`jcr:path`指示点击路径：默认情况下，仅列表节点的直接属性，包含一个包含`p.nodedepth=N`的更深层树，0表示整个无限子树；添加`p.acls=true`以包含当前会话对给定结果项的JCR权限(映射：`create` = `add_node`, `modify` = `set_property`, `delete` = `remove`

   * **选定属性**:

      仅在`p.properties`中指定的属性，即相对路径的空格分隔列表（在URL中使用&quot;+&quot;）；如果相对路径深度大于1，则这些路径将表示为子对象；特殊的jcr:path属性包括点击的路径

### savedquery {#savedquery}

作为子组谓词，将持续的QueryBuilder查询的所有谓词包含到当前查询中。

请注意，这不会执行额外的查询，而是扩展当前查询。

查询可以使用`QueryBuilder#storeQuery()`以编程方式持久。 格式可以是多行String属性，也可以是`nt:file`节点，该节点将查询作为Java属性格式的文本文件包含。

不支持保存提取的谓词的facet查询。

#### 属性 {#properties-19}

* **savedquery**

   保存的查询的路径（String属性或`nt:file`节点）

### 类似{#similar}

使用JCR XPath的`rep:similar()`进行相似性搜索。

不支持筛选。 不支持facet提取。

#### 属性 {#properties-20}

* **要**
查找相似节点的节点的相似绝对路径

* **到**
子节点或 
`.` 对于当前节点(可选，默认值为“ `.`”)

### 标签{#tag}

通过指定标签标题路径，搜索带有一个或多个标签的内容。

支持facet提取。 将使用每个唯一标签的当前标签标题路径为其提供桶。

#### 属性 {#properties-21}

* **标签**

   要查找的标记标题路径，例如“资产属性：方向/横向”

* **N_value**

   使用`1_value`、`2_value`、...检查多个标签（默认情况下与`OR`组合，如果为`AND`且为true）（自5.6起）

* **属性**

   要查看的属性（或属性的相对路径）（默认为&quot; `cq:tags`&quot;）

### tagid {#tagid}

通过指定标记ID，搜索带有一个或多个标记的内容。

支持facet提取。 将使用每个唯一标记的当前标记ID为其提供存储段。

#### 属性 {#properties-22}

* **tagid**

   要查找的标记id，例如&quot; `properties:orientation/landscape`&quot;

* **N_value**

   使用`1_value`、`2_value`、...检查多个标签（默认情况下与`OR`组合，如果为`AND`且为true）（自5.6起）

* **属性**

   要查看的属性（或属性的相对路径）（默认为&quot; `cq:tags`&quot;）

### tagsearch {#tagsearch}

通过指定关键字，搜索带有一个或多个标签的内容。 这将首先搜索标题中包含这些关键字的标记，然后将结果限制为仅包含这些关键字标记的项目。

不支持facet提取。

#### 属性 {#Properties-1}

* **tagsearch**

   用于在标记标题中搜索的关键字

* **属性**

   要查看的属性（或属性的相对路径）（默认为&quot; `cq:tags`&quot;）

* **朗**

   仅搜索特定的本地化标记标题(例如，&quot; `de`&quot;

* **全部**

   (bool)搜索整个标签全文，即所有标题、描述等。 （优先于&quot;l `ang`&quot;）

### 类型 {#type}

将结果限制为特定的JCR节点类型，主节点类型或混合类型。 这也将查找该节点类型的子类型。 请注意，存储库搜索索引需要涵盖节点类型，以便有效执行。

支持facet提取。 将为结果中的每个唯一类型提供存储段。

#### 属性 {#Properties-2}

* **类型**

   要搜索的节点类型或混合名称，例如`cq:Page`