---
title: 开发报告
seo-title: 开发报告
description: AEM基于报表框架提供一系列标准报表
seo-description: AEM基于报表框架提供一系列标准报表
uuid: 1b406d15-bd77-4531-84c0-377dbff5cab2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 50fafc64-d462-4386-93af-ce360588d294
exl-id: 3891150e-9972-4bbc-ad61-7f46a1f9bbb4
source-git-commit: 071bc0e36ed2d8eb4ce7bd0ba46823adc0e43095
workflow-type: tm+mt
source-wordcount: '5252'
ht-degree: 0%

---


# 开发报告 {#developing-reports}

AEM提供了[标准报表](/help/sites-administering/reporting.md)的选项，其中大多数报表基于报表框架。

使用该框架，您可以扩展这些标准报表，或开发您自己的全新报表。 报表框架与现有CQ5概念和原则紧密集成，以便开发人员可以将其现有的CQ5知识用作开发报表的跳板。

对于随AEM一起交付的标准报表：

* 这些报告是基于报告框架构建的：

   * [组件报告](/help/sites-administering/reporting.md#component-report)
   * [页面活动报告](/help/sites-administering/reporting.md#page-activity-report)
   * [用户报告](/help/sites-administering/reporting.md#user-report)
   * [工作流实例报告](/help/sites-administering/reporting.md#workflow-instance-report)

* 以下报告以个别原则为基础，因此不能扩展：

   * [磁盘使用情况](/help/sites-administering/reporting.md#disk-usage)
   * [运行状况检查](/help/sites-administering/reporting.md#health-check)
   * [工作流报表](/help/sites-administering/reporting.md#workflow-report)

>[!NOTE]
>
>教程[创建您自己的报表 — 示例](#creating-your-own-report-an-example)还显示了可以使用以下多少项原则。
>
>您还可以参阅标准报表，以查看其他实施示例。

>[!NOTE]
>
>在以下示例和定义中，使用了以下符号：
>
>* 每行定义一个节点或属性，其中：
   >  `N:<name> [<nodeType>]` :描述名称为且节点类 `<*name*>` 型为的节 `<*nodeType*>`*点。*
   >  `P:<name> [<propertyType]` :描述名称为且属 `<*name*>` 性类型为的属 `<*propertyType*>`性。
   >  `P:<name> = <value>` :描述必 `<name>` 须设置为值的属 `<value>`性。
   >
   >
* 缩进显示节点之间的分层依赖关系。
>* 以 |表示可能项目的列表；例如，类型或名称；例如`String|String[]`表示该属性可以是String或String[]。

   >
   >
* `[]` 描述数组；例如字符串[] 或查询定义中的节点 [数组](#query-definition)。
>
>
除非另有说明，否则默认类型为：
>
>* 节点 — `nt:unstructured`
>* 属性 - `String`


## 报告框架 {#reporting-framework}

报告框架遵循以下原则：

* 它完全基于由CQ5 QueryBuilder执行的查询返回的结果集。
* 结果集定义报表中显示的数据。 结果集中的每一行都对应于报表表格视图中的一行。
* 可在结果集上执行的操作与RDBMS概念类似；主要是&#x200B;*分组*&#x200B;和&#x200B;*聚合*。

* 大多数数据检索和处理都是在服务器端完成的。
* 客户仅负责显示预处理的数据。 客户端只执行次要处理任务（例如，在单元格内容中创建链接）。

报告框架（由标准报告的结构说明）使用由处理队列提供的以下构建基块：

![chlimage_1-248](assets/chlimage_1-248.png)

### 报表页面 {#report-page}

报表页面：

* 是标准CQ5页面。
* 基于为报表](#report-template)配置的[标准CQ5模板。

### 报表库 {#report-base}

[ `reportbase`组件](#report-base-component)构成任何报表的基础，如下所示：

* 保存用于传送数据基础结果集的[查询](#the-query-and-data-retrieval)的定义。

* 是一个经过修改的段落系统，其中将包含添加到报表的所有列(`columnbase`)。
* 定义哪些图表类型可用以及哪些当前处于活动状态。
* 定义编辑对话框，该对话框允许用户配置报表的某些方面。

### 列基 {#column-base}

每列都是[ `columnbase`组件](#column-base-component)的实例，该实例：

* 是段落，由相应报表的parsys(`reportbase`)使用。
* 定义指向[基础结果集](#the-query-and-data-retrieval)的链接；例如，定义此结果集中引用的特定数据，以及其处理方式。
* 持有其他定义；例如可用的聚合和过滤器，以及任何默认值。

### 查询与数据检索 {#the-query-and-data-retrieval}

查询：

* 定义为[ `reportbase`](#report-base)组件的一部分。
* 基于[CQ QueryBuilder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html)。
* 检索用作报表基础的数据。 结果集（表）的每一行都绑定到查询返回的节点。 然后，将从此数据集中提取[单个列](#column-base-component)的特定信息。

* 通常包括：

   * 根路径。

      这会指定要搜索的存储库的子树。

      为帮助最大限度地降低对性能的影响，建议（尝试）将查询限制在存储库的特定子树中。 根路径可以在[报表模板](#report-template)中进行预定义，也可以由用户在[配置（编辑）对话框](#configuration-dialog)中设置。

   * [一个或多个标准](#query-definition)。

      这些规则被强制用于生成（初始）结果集；例如，节点类型限制或属性约束。

**这里的关键点是，查询结果集中返回的每个单个节点都用于在报表上生成一行（因此是1:1关系）。**

开发人员必须确保为报表定义的查询返回适用于该报表的节点集。 但是，节点本身不需要保存所有必需的信息，这也可以从父节点和/或子节点派生。 例如，用于[用户报表](/help/sites-administering/reporting.md#user-report)的查询会根据节点类型选择节点（在此例中为`rep:user`）。 但是，此报表上的大多数列并非直接从这些节点获取其数据，而是从子节点`profile`获取其数据。

### 处理队列 {#processing-queue}

[query](#the-query-and-data-retrieval)返回要在报表中显示为行的数据集。 在将结果集中的每一行（服务器端）在[几个阶段](#phases-of-the-processing-queue)中进行处理，然后传输到客户端，以便在报表中显示。

这允许：

* 从基础结果集提取和派生值。

   例如，它允许您通过计算两个属性值之间的差值，将两个属性值作为单个值进行处理。

* 解析提取的值；这可以通过多种方式实现。

   例如，路径可以映射到标题（如相应&#x200B;*jcr:title*&#x200B;属性中更易读的内容）。

* 在不同位置应用过滤器。
* 创建复合值（如果需要）。

   例如，由向用户显示的文本、用于排序的值以及用于（在客户端）创建链接的其他URL组成。

#### 处理队列的工作流 {#workflow-of-the-processing-queue}

以下工作流表示处理队列：

![chlimage_1-249](assets/chlimage_1-249.png)

#### 处理队列的阶段 {#phases-of-the-processing-queue}

其中，详细步骤和元素包括：

1. 使用值提取器将[初始查询(reportbase)](#query-definition)返回的结果转换为基本结果集。

   根据[列类型](#column-specific-definitions)自动选择值提取器。 它们用于从基础JCR查询中读取值并从中创建结果集；之后，可应用进一步处理。 例如，对于`diff`类型，值提取器会读取两个属性，计算随后添加到结果集中的单个值。 无法配置值提取器。

1. 对包含原始数据的初始结果集应用初始筛选](#column-specific-definitions)（*raw*&#x200B;阶段）。[

1. 值为[预处理](#processing-queue);按照为&#x200B;*apply*&#x200B;阶段定义。

1. [对预处理值执行过](#column-specific-definitions) 滤 ** （分配给预处理阶段）。

1. 值得到解析；根据[定义的resolver](#processing-queue)。
1. [对解析值执行筛选](#column-specific-definitions) ( ** 分配给解析阶段)。

1. 数据是分组和聚合的](#column-specific-definitions)。[
1. 数组数据通过将其转换为（基于字符串）列表来解析。

   这是一个隐式步骤，它将多值结果转换为可显示的列表；对于基于多值JCR属性的（未聚合）单元格值，它是必需的。

1. 值再次为[预处理](#processing-queue);为&#x200B;*afterApply*&#x200B;阶段定义。

1. 数据已排序。
1. 处理的数据被传输到客户端。

>[!NOTE]
>
>在`reportbase`组件上定义返回基本数据集的初始查询。
>
>处理队列的其他元素在`columnbase`组件上定义。

## 报表构建和配置 {#report-construction-and-configuration}

构建和配置报表时需要满足以下条件：

* [定义报表组件的位置](#location-of-report-components)
* [ `reportbase`组件](#report-base-component)
* 一个或多个[ `columnbase`组件](#column-base-component)
* [页面组件](#page-component)
* a [报表设计](#report-design)
* [报表模板](#report-template)

### 报表组件的位置 {#location-of-report-components}

默认报表组件位于`/libs/cq/reporting/components`下。

但是，强烈建议您不要更新这些节点，而是在`/apps/cq/reporting/components`下创建自己的组件节点，或者在更合适的`/apps/<yourProject>/reports/components`下创建组件节点。

其中（例如）：

```
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
```

在此下，您为报表创建根，在此下，报表基组件和列基组件：

```
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
                N:<reportname> [sling:Folder]
                        N:<reportname> [cq:Component]  // report base component
                        N:<columnname> [cq:Component]  // column base component
```

### 页面组件 {#page-component}

报表页面必须使用`/libs/cq/reporting/components/reportpage`的`sling:resourceType`。

自定义页面组件在大多数情况下不应是必需的。

## 报表库组件 {#report-base-component}

每个报表类型都需要一个从`/libs/cq/reporting/components/reportbase`派生的容器组件。

此组件用作报表整体的容器，并提供以下信息：

* [查询定义](#query-definition)。
* 用于配置报表的[（可选）对话框](#configuration-dialog)。
* 报表中集成的任何[Charts](#chart-definitions)。

```
N:<reportname> [cq:Component]
    P:sling:resourceSuperType = "cq/reporting/components/reportbase"
    N:charting
    N:dialog [cq:Dialog]
    N:queryBuilder
```

### 查询定义 {#query-definition}

```xml
N:queryBuilder
    N:propertyConstraints
    [
        N:<name> // array of nodes (name irrelevant), each with the following properties:
            P:name
            P:value
    ]
    P:nodeTypes [String|String[]]
    P:mandatoryProperties [String|String[]
  ]
```

* `propertyConstraints`

   可用于将结果集限制为具有特定属性且具有特定值的节点。 如果指定了多个约束，则节点必须满足所有约束（AND运算）。

   例如：

   ```
   N:propertyConstraints
    [
    N:0
    P:sling:resourceType
    P:foundation/components/textimage
    N:1
    P:jcr:modifiedBy
    P:admin
    ]
   ```

   将返回上次由`admin`用户修改的所有`textimage`组件。

* `nodeTypes`

   用于将结果集限制为指定的节点类型。 可以指定多个节点类型。

* `mandatoryProperties`

   可用于将结果集限制为具有指定属性&#x200B;*所有*&#x200B;的节点。 不会考虑属性的值。

所有项都是可选的，并且可以根据需要进行组合，但您必须至少定义其中一项。

### 图表定义 {#chart-definitions}

```xml
N:charting
    N:settings
        N:active [cq:WidgetCollection]
        [
            N:<name> // array of nodes, each with the following property
                P:id   // must match the id of a child node of definitions
        ]
    N:definitions [cq:WidgetCollection]
    [
        N:<name> // array of nodes, each with the following properties
            P:id
            P:type
            // additional, chart type specific configurations
    ]
```

* `settings`

   保存活动图表的定义。

   * `active`

      由于可以定义多个设置，因此您可以使用此设置定义当前处于活动状态的设置。 这些值由节点数组定义(这些节点没有强制命名约定，但标准报表通常使用`0`、`1`。 `x`)，每个资产均具有以下属性：

      * `id`

         活动图表的标识。 此ID必须匹配图表`definitions`中某个ID。

* `definitions`

   定义可能可用于报表的图表类型。 要使用的`definitions`将由`active`设置指定。

   定义使用节点数组(通常也称为`0`、`1`。 `x`)，每个属性具有以下属性：

   * `id`

      图表标识。

   * `type`

      可用的图表类型。 从以下位置选择：

      * `pie`
饼图。仅从当前数据生成。

      * `lineseries`
一系列线（表示实际快照的连接点）。仅从历史数据生成。
   * 其他属性可用，具体取决于图表类型：

      * 对于图表类型`pie`:

         * `maxRadius` ( `Double/Long`)

            饼图允许的最大半径；因此，图表允许的最大大小（无图例）。 如果定义了`fixedRadius`，则忽略。

         * `minRadius` ( `Double/Long`)

            饼图允许的最小半径。 如果定义了`fixedRadius`，则忽略。

         * `fixedRadius` ( `Double/Long`)为饼图定义固定半径。
      * 对于图表类型[`lineseries`](/help/sites-administering/reporting.md#display-limits):

         * `totals` ( `Boolean`)

            如果应显示显示&#x200B;**Total**的额外行，则为true。
默认: `false`

         * `series` ( `Long`)

            要显示的行/系列数。
默认：`9`（这也是允许的最大值）

         * `hoverLimit` ( `Long`)

            要显示弹出窗口的聚合快照的最大数量（每个水平线上显示的点，表示不同的值），即当用户将鼠标悬停在图表图例中的不同值或相应标签上时。

            默认：`35`（即，如果当前图表设置的不同值超过35个，则不显示任何弹出窗口）。

            另外，限制可以并行显示10个弹出窗口（当在图例文本上鼠标悬停时，可显示多个弹出窗口）。



### 配置对话框 {#configuration-dialog}

每个报表都可以有一个配置对话框，允许用户为报表指定各种参数。 打开报表页面时，可通过&#x200B;**编辑**&#x200B;按钮访问此对话框。

此对话框是标准CQ [对话框](/help/sites-developing/components-basics.md#dialogs)，可以按此方式进行配置（有关更多信息，请参阅[CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog)）。

示例对话框如下所示：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    jcr:primaryType="cq:Dialog"
    height="{Long}424">
    <items jcr:primaryType="cq:WidgetCollection">
        <props jcr:primaryType="cq:Panel">
            <items jcr:primaryType="cq:WidgetCollection">
                <title
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/title.infinity.json"
                    xtype="cqinclude"/>
                <description
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/description.infinity.json"
                    xtype="cqinclude"/>
                <rootPath
                    jcr:primaryType="cq:Widget"
                    fieldLabel="Root path"
                    name="./report/rootPath"
                    rootPath=""
                    rootTitle="Repository root"
                    xtype="pathfield"/>
                <processing
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/processing.infinity.json"
                    xtype="cqinclude"/>
                <scheduling
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/scheduling.infinity.json"
                    xtype="cqinclude"/>
            </items>
        </props>
    </items>
</jcr:root>
```

提供了多个预配置的组件；可以使用`xtype`属性（值为`cqinclude`）在对话框中引用这些参数：

* **`title`**

   `/libs/cq/reporting/components/commons/title`

   用于定义报表标题的文本字段。

* **`description`**

   `/libs/cq/reporting/components/commons/description`

   用于定义报表描述的文本区域。

* **`processing`**

   `/libs/cq/reporting/components/commons/processing`

   报表处理模式的选择器（手动/自动加载数据）。

* **`scheduling`**

   `/libs/cq/reporting/components/commons/scheduling`

   用于为历史图表计划快照的选择器。

>[!NOTE]
>
>引用的组件必须使用`.infinity.json`后缀包含（请参阅上面的示例）。

### 根路径 {#root-path}

此外，还可以为报表定义根路径：

* **`rootPath`**

   这会将报表限制为存储库的某个部分（树或子树），这是性能优化推荐的选项。 根路径由每个报表页面`report`节点的`rootPath`属性指定（在创建页面时从模板获取）。

   它可以由以下方式指定：

   * [报表模板](#report-template)（作为固定值或作为配置对话框的默认值）。
   * 用户（使用此参数）

## 列基组件 {#column-base-component}

每个列类型都需要一个从`/libs/cq/reporting/components/columnbase`派生的组件。

列组件定义了以下组合：

* [列特定查询](#column-specific-query)配置。
* [解析器和预处理](#resolvers-and-preprocessing)。
* [列特定定义](#column-specific-definitions)(如过滤器和聚合；`definitions`子节点)。
* [列默认值](#column-default-values)。
* [客户端筛选器](#client-filter)从服务器返回的数据中提取要显示的信息。
* 此外，列组件必须提供合适的`cq:editConfig`实例。 定义所需的[事件和操作](#events-and-actions)。
* [通用列](#generic-columns)的配置。

```
N:<columnname> [cq:Component]
    P:componentGroup
    P:jcr:title
    P:sling:resourceSuperType = "cq/reporting/components/columnbase"
    N:cq:editConfig [cq:EditConfig] // <a href="#events-and-actions">Events and Actions</a>
    N:defaults // <a href="#column-default-values">Column Default Values</a>
    N:definitions
      N:queryBuilder // <a href="#column-specific-query">Column Specific Query</a>
        P:property [String|String[]] // Column Specific Query
        P:subPath // Column Specific Query
        P:secondaryProperty [String|String[]] // Column Specific Query
        P:secondarySubPath // Column Specific Query
      N:data
        P:clientFilter [String] // <a href="#client-filter">Client Filter</a>
        P:resolver // <a href="#resolvers-and-preprocessing">Resolvers and Preprocessing</a>
        N:resolverConfig // Resolvers and Preprocessing
        N:preprocessing // Resolvers and Preprocessing
      P:type // <a href="#column-specific-definitions">Column Specific Definitions</a>
      P:groupable [Boolean] // Column Specific Definitions
      N:filters [cq:WidgetCollection] // Column Specific Definitions
      N:aggregates [cq:WidgetCollection] // Column Specific Definitions
```

另请参阅[定义新报表](#defining-your-new-report)。

### 列特定查询 {#column-specific-query}

这定义了在单个列中使用的特定数据提取（从[报表数据结果集](#the-query-and-data-retrieval)）。

```xml
N:definitions
    N:queryBuilder
        P:property [String|String[]]
        P:subPath
        P:secondaryProperty [String|String[]]
        P:secondarySubPath
```

* `property`

   定义用于计算实际单元格值的属性。

   如果属性定义为String[] ，则会扫描（按顺序）多个属性以查找实际值。

   例如，在以下情况下：

   `property = [ "jcr:lastModified", "jcr:created" ]`

   相应的值提取器（位于此处）将：

   * 检查是否有jcr:lastModified属性可用，如果可用，请使用该属性。
   * 如果没有jcr:lastModified属性可用，则将改用jcr:created的内容。

* `subPath`

   如果结果不在查询返回的节点上，则`subPath`定义属性的实际位置。

* `secondaryProperty`

   定义另一个属性，该属性还必须用于计算实际单元格值；这将仅用于某些列类型（差异和可排序）。

   例如，对于工作流实例报表，指定的属性用于存储开始时间和结束时间之间时间差的实际值（以毫秒为单位）。

* `secondarySubPath`

   与subPath类似，当使用`secondaryProperty`时。

在大多数情况下，仅使用`property`。

### 客户端过滤器 {#client-filter}

客户端过滤器从服务器返回的数据中提取要显示的信息。

>[!NOTE]
>
>在应用整个服务器端处理后，将在客户端执行此过滤器。

```xml
N:definitions
    N:data
        P:clientFilter [String]
```

`clientFilter` 定义为一个JavaScript函数，该函数：

* 作为输入，接收一个参数；从服务器返回的数据（如此经过完全预处理）
* 作为输出，返回过滤（已处理）的值；从输入信息提取或导出的数据

以下示例从组件路径中提取相应的页面路径：

```
function(v) {
    var sepPos = v.lastIndexOf('/jcr:content');
    if (sepPos < 0) {
        return v;
    }
    return v.substring(sepPos + '/jcr:content'.length, v.length);
}
```

### 解析器和预处理 {#resolvers-and-preprocessing}

[处理队列](#processing-queue)定义各种解析器并配置预处理：

```xml
N:definitions
    N:data
        P:resolver
        N:resolverConfig
        N:preprocessing
            N:apply
            N:applyAfter
```

* `resolver`

   定义要使用的解析程序。 提供了以下解析器：

   * `const`

      将值映射到其他值；例如，它用于将常量（如`en`）解析为其等效值`English`。

   * `default`

      默认解析程序。 这是一个虚拟的解析程序，它不能解决任何问题。

   * `page`

      将路径值解析为相应页面的路径；更精确地说，到相应的`jcr:content`节点。 例如，将`/content/.../page/jcr:content/par/xyz`解析为`/content/.../page/jcr:content`。

   * `path`

      解析路径值，方法是（可选）附加一个子路径，并在解析路径上从节点的属性（由`resolverConfig`定义）中获取实际值。 例如，可以将`/content/.../page/jcr:content`的`path`解析为`jcr:title`属性的内容，这表示页面路径解析为页面标题。

   * `pathextension`

      通过预挂路径并从已解析路径中的节点属性中获取实际值来解析值。 例如，值`de`可能由`/libs/wcm/core/resources/languages`之类的路径（从属性`language`中获取值）前面添加，以将国家/地区代码`de`解析为语言描述`German`。

* `resolverConfig`

   提供解析程序的定义；可用的选项取决于所选的`resolver`:

   * `const`

      使用属性指定要解析的常量。 属性的名称定义要解析的常量；属性的值定义解析的值。

      例如，具有&#x200B;**Name**= `1`和&#x200B;**Value** `=One`的属性将1解析为1。

   * `default`

      没有可用的配置。

   * `page`

      * `propertyName` （可选）

         定义应用于解析值的属性名称。 如果未指定，则使用默认值&#x200B;*jcr:title*（页面标题）；对于`page`解析程序，这意味着首先将路径解析为页面路径，然后进一步解析为页面标题。
   * `path`

      * `propertyName` （可选）

         指定应用于解析值的属性的名称。 如果未指定，则使用默认值`jcr:title`。

      * `subPath` （可选）

         此属性可用于指定在解析值之前要附加到路径的后缀。
   * `pathextension`

      * `path` (mandatory)

         定义要前置的路径。

      * `propertyName` （必填）

         在实际值所在的解析路径上定义属性。

      * `i18n` （可选）类型布尔值)

         确定解析的值是否应为&#x200B;*国际化*（即使用[CQ5的国际化服务](/help/sites-administering/tc-manage.md)）。



* `preprocessing`

   预处理是可选的，可以（单独）绑定到处理阶段&#x200B;*apply*&#x200B;或&#x200B;*applyAfter*:

   * `apply`

      初始预处理阶段（处理队列表示中的步骤3](#processing-queue)）。[

   * `applyAfter`

      在预处理后应用（处理队列的表示中的[步骤9](#processing-queue)）。

#### 解析器 {#resolvers}

解析器用于提取所需信息。 各种解析器的示例包括：

**康斯特**

以下内容会将`VersionCreated`的常量值解析为字符串`New version created`。

请参阅 `/libs/cq/reporting/components/auditreport/typecol/definitions/data`.

```xml
N:data
    P:resolver=const
    N:resolverConfig
        P:VersionCreated="New version created"
```

**页面**

解析对应页面jcr:content（子）节点上的jcr:description属性的路径值。

请参阅 `/libs/cq/reporting/components/compreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=page
    N:resolverConfig
        P:propertyName="jcr:description"
```

**路径**

下面将`/content/.../page`的路径解析为`jcr:title`属性的内容，这表示页面路径已解析为页面标题。

请参阅 `/libs/cq/reporting/components/auditreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=path
    N:resolverConfig
        P:propertyName="jcr:title"
        P:subPath="/jcr:content"
```

**路径扩展**

以下代码使用路径扩展名`/libs/wcm/core/resources/languages`预留值`de`，然后从属性`language`中获取值，以将国家/地区代码`de`解析为语言描述`German`。

请参阅 `/libs/cq/reporting/components/userreport/languagecol/definitions/data`.

```xml
N:data
    P:resolver=pathextension
    N:resolverConfig
        P:path="/libs/wcm/core/resources/languages"
        P:propertyName="language"
```

#### 预处理 {#preprocessing}

`preprocessing`定义可应用于以下任一项：

* 原始值：

   原始值的预处理定义直接在`apply`和/或`applyAfter`上指定。

* 值：

   如有必要，可为每个聚合提供单独的定义。

   要指定聚合值的显式预处理，预处理定义必须驻留在相应的`aggregated`子节点(`apply/aggregated`、`applyAfter/aggregated`)上。 如果需要对不同聚合进行显式预处理，则预处理定义位于具有相应聚合名称的子节点（例如`apply/aggregated/min/max`或其他聚合）上。

您可以指定以下任一内容，以在预处理过程中使用：

* [查找并替](#preprocessing-find-and-replace-patterns)
换模式找到时，指定的模式（定义为正则表达式）将被另一个模式替换；例如，这可用于提取原始的子字符串。

* [数据类型格式化程序](#preprocessing-data-type-formatters)

   将数值转换为相对字符串；例如，表示时间差为1小时的值“将解析为字符串，如`1:24PM (1 hour ago)`。

例如：

```xml
N:definitions
    N:data
        N:preprocessing
            N:apply|applyAfter
                P:pattern         // regex
                P:replace         // replacement for regex
                // and/or
                P:format          // data type formatter
```

#### 预处理 — 查找和替换模式 {#preprocessing-find-and-replace-patterns}

要进行预处理，您可以指定一个`pattern`（定义为[正则表达式](https://en.wikipedia.org/wiki/Regular_expression)或正则表达式），该表达式位于并随后被`replace`模式替换：

* `pattern`

   用于查找子字符串的正则表达式。

* `replace`

   将用作原始字符串替换的字符串或字符串的表示形式。 通常，它表示由正则表达式`pattern`定位的字符串的子字符串。

替换示例可划分为：

* 对于具有以下两个属性的节点`definitions/data/preprocessing/apply`:

   * `pattern`: `(.*)(/jcr:content)(/|$)(.*)`
   * `replace`:  `$1`

* 字符串将作为：

   * `/content/geometrixx/en/services/jcr:content/par/text`

* 将分为四个部分：

   * `$1` -  `(.*)` -  `/content/geometrixx/en/services`
   * `$2` -  `(/jcr:content)` -  `/jcr:content`
   * `$3` -  `(/|$)` -  `/`
   * `$4` -  `(.*)` -  `par/text`

* 并替换为由`$1`表示的字符串：

   * `/content/geometrixx/en/services`

#### 预处理 — 数据类型格式化程序 {#preprocessing-data-type-formatters}

这些格式化程序会将数值转换为相对字符串。

例如，此参数可用于允许`min`、`avg`和`max`聚合的时间列。 作为`min`/ `avg`/ `max`聚合显示为&#x200B;*时间差*(例如，`10 days ago`)，则需要使用数据格式化程序。 为此，将`datedelta`格式化程序应用于`min`/ `avg`/ `max`聚合值。 如果`count`聚合也可用，则它不需要格式化程序，原始值也不需要。

当前可用的数据类型格式化程序包括：

* `format`

   数据类型格式化程序：

   * `duration`

      持续时间是两个定义日期之间的时间跨度。 例如，工作流操作的开始和结束用了1小时，从2/13/11 11:23h开始，到1小时后2/13/11 12:23h结束。

      它将数值（解释为毫秒）转换为持续时间字符串；例如，`30000`的格式为* `30s`。*

   * `datedelta`

      Datadelta是过去某个日期到“现在”之间的时间跨度（因此，如果在稍后的时间点查看报表，则其结果会有所不同）。

      它会将数值（解释为以天为单位的时间差）转换为相对日期字符串。 例如，1的格式为1天前。

以下示例为`min`和`max`聚合定义了`datedelta`格式：

```xml
N:definitions
    N:data
        N:preprocessing
            N:apply
                N:aggregated
                    N:min
                        P:format = "datedelta"
                    N:max
                        P:format = "datedelta"
```

### 列特定定义 {#column-specific-definitions}

特定于列的定义定义该列可用的过滤器和聚合。

```xml
N:definitions
    P:type
    P:groupable [Boolean]
    N:filters [cq:WidgetCollection]
    [
        N:<name> // array of nodes (names irrelevant) with the following properties:
            P:filterType
            P:id
            P:phase
    ]
    N:aggregates [cq:WidgetCollection]
    [
        N:<name> // array of nodes (names irrelevant) with the following properties:
            P:text
            P:type
    ]
```

* `type`

   以下是标准选项：

   * `string`
   * `number`
   * `int`
   * `date`
   * `diff`
   * `timeslot`

      用于提取聚合所需日期的部分部分（例如，按年分组以获取每年的聚合数据）。

   * `sortable`

      用于使用不同值（取自不同属性）进行排序和显示的值。
   此外， 上述任一值均可定义为多值；例如，`string[]`定义字符串数组。

   值提取器由列类型选择。 如果某个值提取器可用于列类型，则使用此提取器。 否则，使用默认值提取器。

   类型可以（可选）采用参数。 例如，`timeslot:year`从日期字段提取年份。 类型及其参数：

   * `timeslot`  — 这些值可与的相应常量比较 `java.utils.Calendar`。

      * `timeslot:year` - `Calendar.YEAR`
      * `timeslot:month-of-year` -  `Calendar.MONTH`
      * `timeslot:week-of-year` -  `Calendar.WEEK_OF_YEAR`
      * `timeslot:day-of-month` -  `Calendar.DAY_OF_MONTH`
      * `timeslot:day-of-week` -  `Calendar.DAY_OF_WEEK`
      * `timeslot:day-of-year` -  `Calendar.DAY_OF_YEAR`
      * `timeslot:hour-of-day` -  `Calendar.HOUR_OF_DAY`
      * `timeslot:minute-of-hour` -  `Calendar.MINUTE`


* `groupable`

   定义报表是否可以按此列分组。

* `filters`

   过滤器定义。

   * `filterType`

      可用的过滤器包括：

      * `string`

         基于字符串的过滤器。
   * `id`

      过滤器标识符。

   * `phase`

      可用阶段：

      * `raw`

         过滤器会应用于原始数据。

      * `preprocessed`

         过滤器应用于预处理的数据。

      * `resolved`

         过滤器将应用于已解析的数据。


* `aggregates`

   聚合定义。

   * `text`

      聚合的文本名称。 如果未指定`text`，则将采用聚合的默认描述；例如，`minimum`将用于`min`聚合。

   * `type`

      聚合类型。 可用的聚合包括：

      * `count`

         计算行数。

      * `count-nonempty`

         计算非空行数。

      * `min`

         提供最小值。

      * `max`

         提供最大值。

      * `average`

         提供平均值。

      * `sum`

         提供所有值的总和。

      * `median`

         提供中间值。

      * `percentile95`

         采用所有值的第95个百分位数。

### 列默认值 {#column-default-values}

用于定义列的默认值：

```xml
N:defaults
    P:aggregate
```

* `aggregate`

   有效的`aggregate`值与`aggregates`下`type`的值相同(请参阅[列特定定义（定义 — 过滤器/聚合）](#column-specific-definitions))。

### 事件和操作 {#events-and-actions}

编辑配置定义侦听器需要检测的事件以及在这些事件发生后要应用的操作。 有关背景信息，请参阅[组件开发简介](/help/sites-developing/components.md)。

必须定义以下值，以确保满足所有必需的操作：

```xml
N:cq:editConfig [cq:EditConfig]
    P:cq:actions [String[]] = "insert", "delete"
    P:cq:dialogMode = "floating"
    P:cq:layout = "auto"
    N:cq:listeners [cq:EditListenersConfig]
        P:aftercreate = "REFRESH_INSERTED"
        P:afterdelete = "REFRESH_SELF"
        P:afteredit = "REFRESH_SELF"
        P:afterinsert = "REFRESH_INSERTED"
        P:aftermove = "REFRESH_SELF"
        P:afterremove = "REFRESH_SELF"
```

### 通用列 {#generic-columns}

通用列是扩展，其中（大多数）列定义存储在列节点（而不是组件节点）的实例中。

它们使用您自定义的（标准）对话框，用于单个通用组件。 此对话框允许报表用户在报表页面上定义通用列的列属性(使用菜单选项&#x200B;**列属性……**)。

例如，**用户报表**&#x200B;的&#x200B;**Generic**&#x200B;列；请参阅`/libs/cq/reporting/components/userreport/genericcol`。

要使列通用，请执行以下操作：

* 将列`definition`节点的`type`属性设置为`generic`。

   请参阅 `/libs/cq/reporting/components/userreport/genericcol/definitions`

* 在列的`definition`节点下指定（标准）对话框定义。

   请参阅 `/libs/cq/reporting/components/userreport/genericcol/definitions/dialog`

   * 对话框的字段必须引用与相应组件属性（包括其路径）相同的名称。

      例如，如果要通过对话框配置通用列的类型，请使用名称为`./definitions/type`的字段。

   * 使用UI/对话框定义的属性优先于在`columnbase`组件上定义的属性。

* 定义编辑配置。

   请参阅 `/libs/cq/reporting/components/userreport/genericcol/cq:editConfig`

* 使用标准AEM方法来定义（其他）列属性。

   请注意，对于在组件实例和列实例上定义的属性，列实例上的值优先。

   可用于常规列的属性包括：

   * `jcr:title`  — 列名称
   * `definitions/aggregates`  — 聚合
   * `definitions/filters`  — 过滤器
   * `definitions/type` — 列的类型（必须在对话框中定义，使用选择器/组合框或隐藏字段）
   * `definitions/data/resolver` 和( `definitions/data/resolverConfig` 但不是 `definitions/data/preprocessing` 或) `.../clientFilter` — 解析程序和配置
   * `definitions/queryBuilder`  — 查询生成器配置
   * `defaults/aggregate`  — 默认聚合

   对于&#x200B;**User Report**&#x200B;上通用列的新实例，通过对话框定义的属性将保留在下：

   `/etc/reports/userreport/jcr:content/report/columns/genericcol/settings/generic`

## 报表设计 {#report-design}

设计可定义哪些列类型可用于创建报表。 它还定义了将列添加到的段落系统。

强烈建议您为每个报表创建单个设计。 这可确保完全的灵活性。 另请参阅[定义新报表](#defining-your-new-report)。

默认报表组件位于`/etc/designs/reports`下。

报表的位置取决于组件所在的位置：

* `/etc/designs/reports/<yourReport>` 如果报告位置偏远，则此参数适用  `/apps/cq/reporting`

* `/etc/designs/<yourProject>/reports/<*yourReport*>` 对于使用模式的报 `/apps/<yourProject>/reports` 表

必需的设计属性在`jcr:content/reportpage/report/columns`上注册（例如`/etc/designs/reports/<reportName>/jcr:content/reportpage/report/columns`）：

* `components`

   报表中允许的任何组件和/或组件组。

* `sling:resourceType`

   值`cq/reporting/components/repparsys`的属性。

示例设计代码片段（取自组件报表的设计）为：

```xml
<!-- ... -->
    <jcr:content
        jcr:primaryType="nt:unstructured"
        jcr:title="Component Report"
        sling:resourceType="wcm/core/components/designer">
        <reportpage jcr:primaryType="nt:unstructured">
            <report jcr:primaryType="nt:unstructured">
                <columns
                    jcr:primaryType="nt:unstructured"
                    sling:resourceType="cq/reporting/components/repparsys"
                    components="group:Component Report"/>
            </report>
        </reportpage>
    </jcr:content>
<!-- ... -->
```

不需要为单个列指定设计。 可在设计模式下定义可用列。

>[!NOTE]
>
>建议您不要对标准报表设计进行任何更改。 这是为了确保在升级或安装修补程序时不会丢失任何更改。
>
>如果要自定义标准报表，请复制报表及其设计。

>[!NOTE]
>
>创建报表后，可自动创建默认列。 这些值在模板中指定。

## 报表模板 {#report-template}

每个报表类型必须提供一个模板。 这些是标准的[CQ模板](/help/sites-developing/templates.md)，可以这样配置。

模板必须：

* 将`sling:resourceType`设置为`cq/reporting/components/reportpage`

* 指示要使用的设计
* 创建`report`子节点，该子节点通过`sling:resourceType`属性引用容器(`reportbase`)组件

示例模板代码片段（取自组件报表模板）为：

```xml
<!-- ... -->
    <jcr:content
        cq:designPath="/etc/designs/reports/compreport"
        jcr:primaryType="cq:PageContent"
        sling:resourceType="cq/reporting/components/reportpage">
        <report
            jcr:primaryType="nt:unstructured"
            sling:resourceType="cq/reporting/components/compreport/compreport"/>
    </jcr:content>
<!-- .. -->
```

显示根路径（取自用户报表模板）定义的示例模板代码片段为：

```xml
<!-- ... -->
    <jcr:content
        cq:designPath="/etc/designs/reports/userreport"
        jcr:primaryType="cq:PageContent"
        sling:resourceType="cq/reporting/components/reportpage">
        <report
            jcr:primaryType="nt:unstructured"
            rootPath="/home/users"
            sling:resourceType="cq/reporting/components/compreport/compreport"/>
    </jcr:content>
<!-- .. -->
```

默认报告模板位于`/libs/cq/reporting/templates`下。

但是，强烈建议您不要更新这些节点，而是在`/apps/cq/reporting/templates`下创建自己的组件节点，或者在更合适的`/apps/<yourProject>/reports/templates`下创建组件节点。

例如，（另请参阅[报表组件的位置](#location-of-report-components)）：

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
```

在此下，为模板创建根：

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
                N:<reportname> [sling:Folder]
```

## 创建您自己的报表 — 示例 {#creating-your-own-report-an-example}

### 定义新报表 {#defining-your-new-report}

要定义新报表，必须创建并配置：

1. 报表组件的根。
1. 报表库组件。
1. 一个或多个列基组件。
1. 报表设计。
1. 报表模板的根。
1. 报表模板。

为了说明这些步骤，以下示例定义了一个报表，其中列出了存储库中的所有OSGi配置；即`sling:OsgiConfig`节点的所有实例。

>[!NOTE]
>
>复制现有报表，然后自定义新版本是一种替代方法。

1. 为新报表创建根节点。

   例如，在`/apps/cq/reporting/components/osgireport`下。

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:components [sling:Folder]
               N:osgireport [sling:Folder]
   ```

1. 定义报表库。 例如`/apps/cq/reporting/components/osgireport`下的`osgireport[cq:Component]`。

   ```xml
   N:osgireport [sling:Folder]
       N:osgireport [cq:Component]
           P:sling:resourceSuperType [String] = "cq/reporting/components/reportbase"
           N:charting [nt:unstructured]
               N:settings [nt:unstructured]
                   N:active [cq:WidgetCollection]
                       N:0 [nt:unstructured]
                           P:id [String] = "pie"
                       N:1 [nt:unstructured]
                           P:id [String] = "lineseries"
               N:definitions [cq:WidgetCollections]
                   N:0 [nt:unstructured]
                       P:id [String] = "pie"
                       P:maxRadius [Long] = 180
                       P:type [String] = "pie"
                   N:1 [nt:unstructured]
                       P:id [String] = "lineseries"
                       P:type [String] = "lineseries"
           N:dialog [cq:Dialog]
               P:height [Long] = 424
               N:items [cq:WidgetCollection]
                   N:props [cq:Panel]
                       N:items [cq:WidgetCollection]
                           N:title [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/title.infinity.json"
                               P:xtype [String] = "cqinclude"
                           N:description [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/description.infinity.json"
                               P:xtype [String] = "cqinclude"
                           N:rootPath [cq:Widget]
                               P:fieldLabel [String] = "Root path"
                               P:name [String] = "./report/rootPath"
                               P:xtype [String] = "pathfield"
                           N:processing [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/processing.infinity.json"
                               P:xtype [String] = "cqinclude"
                           N:scheduling [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/scheduling.infinity.json"
                               P:xtype [String] = "cqinclude"
           N:queryBuilder [nt:unstructured]
               P:nodeTypes [String[]] = "sling:OsgiConfig"
   ```

   这定义了一个报表库组件，该组件：

   * 搜索类型为`sling:OsgiConfig`的所有节点
   * 显示`pie`和`lineseries`图表
   * 为用户提供一个用于配置报表的对话框

1. 定义第一列（列基）组件。 例如`/apps/cq/reporting/components/osgireport`下的`bundlecol[cq:Component]`。

   ```xml
   N:osgireport [sling:Folder]
       N:bundlecol [cq:Component]
           P:componentGroup [String] = "OSGi Report"
           P:jcr:title = "Bundle"
           P:sling:resourceSuperType [String] = "cq/reporting/components/columnbase"
           N:cq:editConfig [cq:EditConfig]
               P:cq:actions [String[]] = "insert", "delete"
               P:cq:dialogMode [String] = "floating"
               P:cq:layout [String] = "auto"
               N:cq:listeners [cq:EditListenersConfig]
                   P:aftercreate [String] "REFRESH_INSERTED"
                   P:afterdelete [String] "REFRESH_SELF"
                   P:afteredit [String] "REFRESH_SELF"
                   P:afterinsert [String] "REFRESH_INSERTED"
                   P:aftermove [String] "REFRESH_SELF"
                   P:afterremove [String] "REFRESH_SELF"
           N:defaults [nt:unstructured]
               P:aggregate [String] = "count"
           N:definitions [nt:unstructured]
               P:groupable [Boolean] = false
               P:type [String] = "string"
               N:queryBuilder [nt:unstructured]
                   P:property [String] = "jcr:path"
   ```

   这定义了一个基于列的组件，该组件：

   * 搜索并返回从服务器接收的值；在这种情况下，每个`sling:OsgiConfig`节点的属性`jcr:path`
   * 提供`count`聚合
   * 不可分组
   * 标题`Bundle`（表中的列标题）
   * 位于sidekick组`OSGi Report`中
   * 在指定事件中刷新

   >[!NOTE]
   >
   >在本例中，没有`N:data`和`P:clientFilter`的定义。 这是因为从服务器收到的值是按1:1返回的 — 这是默认行为。
   >
   >这与定义相同：
   >
   >
   ```
   >N:data [nt:unstructured]
   >   P:clientFilter [String] = "function(v) { return v; }"
   >```
   >
   >其中，函数只返回它收到的值。

1. 定义报表设计。 例如`/etc/designs/reports`下的`osgireport[cq:Page]`。

   ```xml
   N:osgireport [cq:Page]
       N:jcr:content [nt:unstructured]
           P:jcr:title [String] = "OSGi report"
           P:sling:resourceType [String] = "wcm/core/components/designer"
           N:reportpage [nt:unstructured]
               N:report [nt:unstructured]
                   N:columns [nt:unstructured]
                       P:components [String] = "group:OSGi Report"
                       P:sling:resourceType [String] = "cq/reporting/components/repparsys"
   ```

1. 为新报表模板创建根节点。

   例如，在`/apps/cq/reporting/templates/osgireport`下。

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:templates [sling:Folder]
               N:osgireport [cq:Template]
   ```

1. 定义报表模板。 例如`/apps/cq/reporting/templates`下的`osgireport[cq:Template]`。

   ```xml
   N:osgireport [cq:Template]
       P:allowedPaths [String[]] = "/etc/reports(/.*)?"
       P:jcr:description [String] = "Use this report generator to create a new OSGi report."
       P:jcr:title [String] = "OSGi Report Template"
       P:ranking [Long] = 100
       P:shortTitle [String] = "OSGi Report"
       N:jcr:content [cq:PageContent]
           P:cq:designPath [String] = "/etc/designs/reports/osgireport"
           P:sling:resourceType [String] = "cq/reporting/components/reportpage"
           N:report [nt:unstructured]
               P:rootPath [String] = "/"
               P:sling:resourceType [String] = "cq/reporting/components/osgireport/osgireport"
       N:thumbnail.png [nt:file]
   ```

   这定义了一个模板：

   * 为生成的报告定义`allowedPaths` — 在上述`/etc/reports`下的任意位置
   * 提供模板的标题和描述
   * 提供可在模板列表中使用的缩略图图像（上面未列出此节点的完整定义 — 最简单的方法是从现有报表中复制thumbnail.png的实例）。

### 创建新报表的实例 {#creating-an-instance-of-your-new-report}

现在可以创建新报表的实例：

1. 打开&#x200B;**工具**&#x200B;控制台。

1. 在左窗格中选择&#x200B;**Reports**。
1. 然后，**新建……**。 定义&#x200B;**标题**&#x200B;和&#x200B;**名称**，从模板列表中选择新的报表类型（**OSGi报表模板**），然后单击&#x200B;**创建**。
1. 您的新报表实例将显示在列表中。 双击此图标可打开。
1. 从Sidekick中拖动组件（例如，**OSGi报表**&#x200B;组中的&#x200B;**捆绑**）以创建第一列，并启动报表定义](/help/sites-administering/reporting.md#the-basics-of-report-customization)。[

   >[!NOTE]
   >
   >由于此示例没有任何可分组列，因此图表将不可用。 要查看图表，请将`groupable`设置为`true`:
   >
   >
   ```
   >N:osgireport [sling:Folder]
   > N:bundlecol [cq:Component]
   > N:definitions [nt:unstructured]
   > P:groupable [Boolean] = true
   >```

## 配置报表框架服务 {#configuring-the-report-framework-services}

本节介绍用于实施报表框架的OSGi服务的高级配置选项。

可以使用Web控制台的“配置”菜单（例如`http://localhost:4502/system/console/configMgr`）查看这些配置。 使用AEM时，可通过多种方法来管理此类服务的配置设置；有关更多详细信息和建议的实践，请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md) 。

### 基本服务（Day CQ Reporting配置） {#basic-service-day-cq-reporting-configuration}

* **** 时区定义为其创建时区历史数据。这是为了确保历史图表能够为全球每个用户显示相同的数据。
* **** 本地化定义要与时间区一起用于历史 **** 数据的区域设置。区域设置用于确定某些特定于区域设置的日历设置（例如，一周的第一天是星期日还是星期一）。

* **快照** 路径定义存储历史图表快照的根路径。
* **报表** 路径定义报表所在的路径。快照服务使用此参数来确定要为其实际拍摄快照的报表。
* **每日** 快照定义每天拍摄每日快照的小时数。指定的小时位于服务器的本地时区中。
* **每小** 时快照定义每小时拍摄快照时的分钟数。
* **行（最大）** 定义为每个快照存储的最大行数。该值应合理选择；如果过高，则会影响存储库的大小，如果过低，则数据可能不准确，因为历史数据的处理方式。
* **假数据**，启用后，即可使用选择器创建假历史数 `fakedata` 据；如果禁用，则使用选择 `fakedata` 器将引发异常。

   由于数据是假的，因此必须仅&#x200B;**&#x200B;用于测试和调试。

   使用`fakedata`选择器将隐式完成报告，因此所有现有数据都将丢失；数据可以手动还原，但这可能是一个非常耗时的过程。

* **快照** 用户定义了可用于拍摄快照的可选用户。

   基本上，快照是为已完成报告的用户拍摄的。 可能会有这样一些情况（例如，在发布系统上，由于此用户的帐户尚未复制，因此此用户不存在），您希望指定一个替代用户。

   此外，指定用户可能会带来安全风险。

* **强制快照用户**，如果启用，则所有快照都将与在快照用户 *下指定的用户一起*&#x200B;拍摄。如果处理不正确，可能会对安全造成严重影响。

### 缓存设置(Day CQ Reporting Cache) {#cache-settings-day-cq-reporting-cache}

* **** 启用后，您可以启用或禁用报表数据的缓存。启用报告缓存会在多个请求期间将报告数据保留在内存中。 这可能会提高性能，但会导致内存消耗增加，在极端情况下可能导致内存不足。
* **** TTL定义缓存报表数据的时间（以秒为单位）。数字越高，性能越好，但如果数据在时间段内发生更改，则也可能会返回不准确的数据。
* **最大** 条目数定义每次要缓存的报表数上限。

>[!NOTE]
>
>每个用户和语言的报表数据可能不同。 因此，会根据报表、用户和语言缓存报表数据。 这意味着&#x200B;****&#x200B;值`2`实际上会缓存以下任一数据：
>
>* 具有不同语言设置的两个用户的一个报表
>* 一个用户和两个报表

>


