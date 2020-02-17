---
title: Query builder谓词引用
seo-title: Query builder谓词引用
description: 完整的Query Builder API谓词引用。
seo-description: 完整的Query Builder API谓词引用。
uuid: af0e269e-7d52-4032-b22e-801c7b5dccfa
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: 94a05894-743a-4ace-a292-bfee90ba9068
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Query builder谓词引用{#query-builder-predicate-reference}

## 常规 {#general}

* [根](#root)
* [组](#group)
* [orderby](#orderby)

## 谓词 {#predicates}

* [boolproperty](/help/sites-developing/querybuilder-predicate-reference.md#boolproperty)
* [contentfragment](/help/sites-developing/querybuilder-predicate-reference.md#contentfragment)
* [dateComparision](/help/sites-developing/querybuilder-predicate-reference.md#datecomparison)
* [达朗日](/help/sites-developing/querybuilder-predicate-reference.md#daterange)
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
* [相对变化](/help/sites-developing/querybuilder-predicate-reference.md#relativedaterange)
* [savedquery](/help/sites-developing/querybuilder-predicate-reference.md#savedquery)
* [类似](/help/sites-developing/querybuilder-predicate-reference.md#similar)
* [标签](/help/sites-developing/querybuilder-predicate-reference.md#tag)
* [tagid](/help/sites-developing/querybuilder-predicate-reference.md#tagid)
* [tagsearch](/help/sites-developing/querybuilder-predicate-reference.md#tagsearch)
* [类型](/help/sites-developing/querybuilder-predicate-reference.md#type)

### boolproperty {#boolproperty}

在JCR BOOLEAN属性上匹配。 仅接受值“ `true`”和“ `false`”。 对于“ `false`”，如果属性具有值“ `false`”或该属性根本不存在，则匹配。 这对于检查仅在启用时设置的布尔标志很有用。

继承的“ `operation`”参数没有含义。

支持facet提取。 将为每个或值提供 `true` 时段， `false` 但仅为现有属性提供时段。

#### 属性 {#properties}

* **boolproperty**&#x200B;属性到属性的相对路径， `myFeatureEnabled` 例如 `jcr:content/myFeatureEnabled`

* **值**&#x200B;用于检查属性、“ `true`”或“ `false`”

### contentfragment {#contentfragment}

将结果限制为内容片段。

不支持筛选。

不支持facet提取。

#### 属性 {#properties-1}

* **contentfragment**&#x200B;它可与任何值一起使用以检查内容片段。

### dateComparision {#datecomparison}

比较两个JCR DATE属性。 可以测试它们是否相等、不等、是否大于或大于等。

这是一个仅筛选谓词，无法利用搜索索引。

#### 属性 {#properties-2}

* **property1**

   第一个日期属性的路径

* **property2**

   第二个日期属性的路径

* **操作**

   “ `=`”表示精确匹配，“ `!=`”表示不相等比较，“ `>`”表示属性1大于属性2,“ `>=`”表示属性1大于或等于属性2。 默认值为 &quot; `=`&quot;.

### 达朗日 {#daterange}

将JCR DATE属性与日期／时间间隔匹配。 它对日期和时间( `YYYY-MM-DDTHH:mm:ss.SSSZ`)使用ISO8601格式，并允许部分表示，如 `YYYY-MM-DD`。 或者，时间戳可以以UTC时区（UNIX时间格式）自1970年以来的毫秒数提供。

您可以查找两个时间戳之间的任何内容（任何比给定日期更新或更旧的内容），还可以在包含时间间隔和打开时间间隔之间进行选择。

支持facet提取。 将提供“今天”、“本周”、“本月”、“过去3个月”、“今年”、“去年”和“比去年更早”的时段。

不支持筛选。

#### 属性 {#properties-3}

* **属性**

   属性的相对路 `DATE` 径，例如 `jcr:lastModified`

* **lowerBound**

   lower date bound to check property for，例如 `2014-10-01`

* **lowerOperation**

   “ `>`”（新）或“ `>=`”（新）适用于 `lowerBound`。 默认为 &quot; `>`&quot;.

* **upperBound**

   检查属性的上限，例如 `2014-10-01T12:15:00`

* **upperOperation**

   “ `<`”（旧）或“ `<=`”（旧）适用于 `upperBound`。 默认为 &quot; `<`&quot;.

* **timeZone**

   未作为ISO-8601日期字符串提供时要使用的时区ID。 默认值是系统的默认时区。

### 排除路径 {#excludepaths}

从其路径与正则表达式匹配的结果中排除节点。

这是一个仅筛选谓词，无法利用搜索索引。

不支持facet提取。

#### 属性 {#properties-4}

* **排除路径**

   与结果路径匹配的正则表达式，从结果中排除匹配的表达式。

### fulltext {#fulltext}

在全文索引中搜索词。

不支持筛选。

不支持facet提取。

#### 属性 {#properties-5}

* **全文**

   全文搜索词

* **relPath**

   要在属性或子节点中搜索的相对路径。 此属性是可选的。

### 组 {#group}

允许构建嵌套条件。 组可以包含嵌套组。 querybuilder查询中的所有内容都隐式地位于根组中，根组中也 `p.or` 可以有 `p.not` 和参数。

将两个属性中的任何一个与值匹配的示例：

```
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

从概念上讲，这 `(1_property` 是或 `2_property)`。

嵌套用户组的示例：

```
fulltext=Management
group.p.or=true
group.1_group.path=/content/geometrixx/en
group.1_group.type=cq:Page
group.2_group.path=/content/dam/geometrixx
group.2_group.type=dam:Asset
```

这会在中或资产&#x200B;**中**，搜索页 `/content/geometrixx/en` 面中的术语“管理” `/content/dam/geometrixx`。

从概念上讲 `fulltext AND ( (path AND type) OR (path AND type) )`, 请注意，此类OR连接需要良好的性能索引。

#### 属性 {#properties-6}

* **p.or**

   如果设置为“ `true`”，则组中只有一个谓词必须匹配。 此默认值为“ `false`”，表示所有内容必须匹配

* **p.not**

   如果设置为“ `true`”，则会否定该组(默认为“ `false`”)

* **&lt;谓词>**

   添加嵌套谓词

* **N_&lt;谓词>**

   添加多个同时嵌套的谓词，如 `1_property, 2_property, ...`

### hasPermission {#haspermission}

将结果限制为当前会话具有指定 [JCR权限的项目。](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

这是一个仅筛选谓词，无法利用搜索索引。 它不支持facet提取。

#### 属性 {#properties-7}

* **hasPermission**

   当前用户会话必须全部具有的以逗号分隔的JCR权限，以用于相关节点；例如 `jcr:write`, `jcr:modifyAccessControl`

### 语言 {#language}

查找特定语言的CQ页面。 这会查看页面语言属性和页面路径，它们通常包括顶级站点结构中的语言或区域设置。

这是一个仅筛选谓词，无法利用搜索索引。

支持facet提取。 将为每个唯一语言代码提供时段。

#### 属性 {#properties-8}

* **语言**

   ISO语言代码，例如“ `de`”

### mainasset {#mainasset}

检查节点是DAM主资产还是子资产。 这基本上是不在“子资产”节点内的每个节点。 请注意，这并不检查节点 `dam:Asset` 类型。 要使用此谓词，只需设置“” `mainasset=true`或“ `mainasset=false`”，就不再有其他属性。

这是一个仅筛选谓词，无法利用搜索索引。

支持facet提取。 将为主资产和子资产提供2个存储段。

#### 属性 {#properties-9}

* **mainasset**

   boolean, &quot; `true`&quot;（对于主资产）, &quot; `false`&quot;（对于子资产）

### memberOf {#memberof}

查找特定sling资源集合的成 [员项目](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/resource/collection/ResourceCollection.html)。

这是一个仅筛选谓词，无法利用搜索索引。 不支持facet提取。

#### 属性 {#properties-10}

* **memberOf**

   Sling资源收集路径

### nodename {#nodename}

在JCR节点名称上匹配。

支持facet提取。 将为每个唯一节点名称（文件名）提供存储段。

#### 属性 {#properties-11}

* **nodename**

   允许通配符的节点名模式： `*` =任意或无字符， `?` =任意字符， `[abc]` =只有括号中的字符

### notexpired {#notexpired}

通过检查JCR DATE属性是否大于或等于当前服务器时间来匹配项。 这可用于检查“ `expiresAt`”类日期属性，并仅限于尚未过期( `notexpired=true`)或已过期( `notexpired=false`)的属性。

不支持筛选。

支持以与更改谓词相同的方式进行facet提取。

#### 属性 {#properties-12}

* **notexpired**

   boolean, &quot; `true`&quot; for not expired yet(date in ture or equal), &quot; `false`&quot; for expired(date in last)（必填）

* **属性**

   要检查的属 `DATE` 性的相对路径（必需）

### orderby {#orderby}

允许对结果进行排序。 如果需要按多个属性排序，则需要使用数字前缀多次添加此谓词， `1_orderby=first`如 `2_oderby=second`。

#### 属性 {#properties-13}

* **orderby**

   JCR属性名称由前导@（例如，或） `@jcr:lastModified` 表示 `@jcr:content/jcr:title`，或查询中的另一个谓词(例如，对其排序 `2_property`)表示

* **排序**

   排序方向，“” `desc`表示降序，“”表示升 `asc`序（默认）

* **case**

   如果设置为“ `ignore`”，则排序将不区分大小写，即“a”在“B”之前；如果为空或遗漏，则排序区分大小写，即“B”在“a”之前

### 路径 {#path}

在给定路径内搜索。

不支持facet提取。

#### 属性 {#properties-14}

* **路径**

   路径模式；根据具体情况，整个子树将匹配(如附加在 `//*` xpath中，但请注意，这不包括基本路径)（exact=false，默认值）或仅精确的路径匹配(可包括通配符( `*`));如果设置了自身，则将搜索包括基节点的整个子树

* **精确**

   如果 `exact` 为true/on，则精确路径必须匹配，但它可以包含简单的通配符( `*`)，该通配符名称匹配，但不能是“ `/`”;如果为false（默认），则包括所有子代（可选）

* **扁平**

   仅搜索直接子项(如在xpath中附加“ `/*`”)(仅在“ `exact`”不是true时使用，可选)

* **self**

   搜索子树，但包括作为路径给定的基节点（无通配符）

### 属性 {#property}

匹配JCR属性及其值。

支持facet提取。 将为结果中的每个唯一属性值提供时段。

#### 属性 {#properties-15}

* **属性**

   属性相对路径，例如 `jcr:title`

* **value**

   值以检查属性；遵循JCR属性类型到字符串转换

* **N_value**

   使 `1_value`用， `2_value`, ...检查多个值(默认情况下 `OR` 与if `AND` and=true结合)（自5.3起）

* **和**

   设置为true，将多个值( `N_value`)与AND（自5.3开始）组合

* **操作**

   “ `equals`”表示精确匹配（默认）,“ `unequals`”表示不相等比较，“ `like`”表示使用xpath函数（可选）,“ `jcr:like``not`”表示不匹配(例如 xpath中 `not(@prop)`的“ ”，值参数将被忽略)或“ `exists`”用于存在性检查(value can be true - properties must exist, default - or false - as &quot; `not`&quot;)

* **深度**

   属性／相对路径可存在的通配符级别数(例如， `property=size depth=2` 将检查节点／大小、节点/&amp;ast;/size和node/&amp;ast;/&amp;ast;/ast;/size)

### rangeproperty {#rangeproperty}

将JCR属性与间隔匹配。 这适用于线性类型（如、和） `LONG`的 `DOUBLE` 属性 `DECIMAL`。 有关 `DATE` 信息，请参阅已优化日期格式输入的日期谓词。

您可以定义下界和上界，也可以只定义下界和上界中的一个。 操作(例如 “小于”或“小于或等于”)也可单独为下界和上界指定。

不支持facet提取。

#### 属性 {#properties-16}

* **属性**

   属性的相对路径

* **lowerBound**

   下界检查属性

* **lowerOperation**

   “ `>`”（默认）或“ `>=`”应用于 `lowerValue`

* **upperBound**

   上界检查属性

* **upperOperation**

   “ `<`”（默认）或“ `<=`”应用于 `lowerValue`

* **小数点**

   “ `true`”（如果选中的属性类型为Decimal）

### 相对变化 {#relativedaterange}

使用 `JCR DATE` 相对于当前服务器时间的时间偏移，将属性与日期／时间间隔匹配。 您可以指 `lowerBound` 定并使 `upperBound``1s 2m 3h 4d 5w 6M 7y` 用毫秒值或bugzilla语法（一秒、两分钟、三小时、四天、五周、六个月、七年）。 前缀为“ `-`”，表示当前时间之前的负偏移。 如果仅指定或 `lowerBound` ，则另 `upperBound`一个将默认为0，表示当前时间。

例如：

* `upperBound=1h` (并且不 `lowerBound`)将在下一小时内选择任何内容
* `lowerBound=-1d` (并且不 `upperBound`会)会在过去24小时内选择任何内容
* `lowerBound=-6M` 选 `upperBound=-3M` 择6个月到3个月的
* `lowerBound=-1500` 并 `upperBound=5500` 且选择过去1500毫秒到将来5500毫秒之间的任何内容
* `lowerBound=1d` 然 `upperBound=2d` 后在后天选择任何

请注意，不需要考虑闰年，所有月份都是30天。

不支持筛选。

支持以与更改谓词相同的方式进行facet提取。

#### 属性 {#properties-17}

* **upperBound**

   相对于当前服务器时间限制的上限日期（以毫秒为单位）或 `1s 2m 3h 4d 5w 6M 7y` （1秒、2分钟、3小时、4天、5周、6个月、7年），使用“-”表示负偏移

* **lowerBound**

   相对于当前服务器时间限定的较低日期（以毫秒为单位）或 `1s 2m 3h 4d 5w 6M 7y` （一秒、二分钟、三小时、四天、五周、六个月、七年），使用“-”表示负偏移

### root {#root}

根谓词组。 支持组的所有功能并允许设置全局查询参数。

名称“root”从未在查询中使用，它是隐式的。

#### 属性 {#properties-18}

* **p.offset**

   表示结果页面开始的数字，即要跳过的项目数

* **p.limit**

   指示页面大小的数字

* **p.guessTotal**

   建议：避免计算可能代价高昂的全部结果；表示最大总数最多计数的数字（例如1000，该数字为用户提供了对粗略大小和精确数量的足够反馈，以获得较小的结果）或“ `true`”仅计数最小必需 `p.offset` + `p.limit`

* **p.excepter**

   如果设置为“ `true`”，则在结果中包含全文摘录

* **p.hits**

   （仅针对JSON servlet）选择将点击写入JSON的方式，使用这些标准点击（可通过ResultHitWriter服务扩展）:

   * **简单**:

      最小项 `path`目， `title`如 `lastmodified`、 `excerpt` 、（如果已设置）

   * **全部**:

      sling JSON呈现节点， `jcr:path` 指示点击路径：默认情况下，只列出节点的直接属性，包含一个更深的树，其中 `p.nodedepth=N`0表示整个无限子树；添 `p.acls=true` 加以包含当前会话对给定结果项的JCR权限(映射： `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`)

   * **选定属性**:

      仅在中指定的 `p.properties`属性，即相对路径列表中以空格分隔的（在URL中使用“+”）;如果相对路径的深度大于1，则这些路径将表示为子对象；特殊的jcr:path属性包括点击的路径

### savedquery {#savedquery}

作为子组谓词，将持久化的querybuilder查询的所有谓词包含到当前查询中。

请注意，这不会执行额外的查询，而是扩展当前查询。

查询可以使用以编程方式持久 `QueryBuilder#storeQuery()`。 该格式可以是多行字符串属性，也可以是包含查询 `nt:file` 的节点，查询以Java属性格式作为文本文件。

不支持对保存的查询的谓词进行facet提取。

#### 属性 {#properties-19}

* **savedquery**

   保存的查询的路径(字符串属性或节 `nt:file` 点)

### 类似 {#similar}

使用JCR XPath的相似性搜索 `rep:similar()`。

不支持筛选。 不支持facet提取。

#### 属性 {#properties-20}

* **类**&#x200B;似要查找相似节点的节点的绝对路径

* **本**&#x200B;地到子节点或当前节点的 `.` 相对路径(可选，默认为“ `.`”)

### tag {#tag}

通过指定标记标题路径搜索用一个或多个标记标记的内容。

支持facet提取。 将使用每个唯一标记的当前标记标题路径为其提供时段。

#### 属性 {#properties-21}

* **标签**

   要查找的标记标题路径，例如“资产属性：方向／横向”

* **N_value**

   使 `1_value`用， `2_value`, ...检查多个标记(默认情 `OR` 况下与if `AND` and=true结合)（自5.6起）

* **属性**

   要查看的属性（或属性的相对路径）(默认为“ `cq:tags`”)

### tagid {#tagid}

通过指定标记ID搜索用一个或多个标记标记的内容。

支持facet提取。 将使用每个唯一标记的当前标记ID为其提供存储段。

#### 属性 {#properties-22}

* **tagid**

   要查找的标记id，例如“ `properties:orientation/landscape`”

* **N_value**

   使 `1_value`用， `2_value`, ...检查多个标签(默认情 `OR` 况下，与if `AND` and=true结合)（自5.6起）

* **属性**

   要查看的属性（或属性的相对路径）(默认为“ `cq:tags`”)

### tagsearch {#tagsearch}

通过指定关键字搜索用一个或多个标记标记的内容。 这将首先搜索标题中包含这些关键字的标记，然后将结果限制为仅包含这些关键字标记的项目。

不支持facet提取。

#### 属性 {#Properties-1}

* **tagsearch**

   用于在标记标题中搜索的关键字

* **属性**

   要查看的属性（或属性的相对路径）(默认为“ `cq:tags`”)

* **lang**

   仅搜索特定本地化的标记标题(例如，&quot; `de`&quot;)

* **全部**

   (bool)搜索整个标签全文，即所有标题、说明等。 (优先于“l `ang`”)

### 类型 {#type}

将结果限制为特定的JCR节点类型，主节点类型或混合类型。 此操作还将查找该节点类型的子类型。 请注意，存储库搜索索引需要涵盖节点类型，以便有效执行。

支持facet提取。 将为结果中的每个唯一类型提供时段。

#### 属性 {#Properties-2}

* **类型**

   要搜索的节点类型或混合名称，例如 `cq:Page`