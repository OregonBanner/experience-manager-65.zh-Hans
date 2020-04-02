---
title: 开发报告
seo-title: 开发报告
description: AEM根据报告框架提供一系列标准报告
seo-description: AEM根据报告框架提供一系列标准报告
uuid: 1b406d15-bd77-4531-84c0-377dbff5cab2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 50fafc64-d462-4386-93af-ce360588d294
translation-type: tm+mt
source-git-commit: ea6da2b75cce4052211fb8f0793f1f380eb85a20

---


# 开发报告{#developing-reports}

AEM提供了一系列标 [准报告](/help/sites-administering/reporting.md) ，其中大多数报告基于报告框架。

使用该框架，您可以扩展这些标准报告，或开发您自己的全新报告。 该报告框架与现有的CQ5概念和原则紧密集成，以便开发人员能够将他们现有的CQ5知识用作开发报告的跳板。

对于随AEM一起提供的标准报表：

* 这些报告构建在报告框架上：

   * [组件报告](/help/sites-administering/reporting.md#component-report)
   * [页面活动报告](/help/sites-administering/reporting.md#page-activity-report)
   * [用户报告](/help/sites-administering/reporting.md#user-report)
   * [工作流实例报告](/help/sites-administering/reporting.md#workflow-instance-report)

* 以下报告基于个别原则，因此不能延期：

   * [磁盘使用情况](/help/sites-administering/reporting.md#disk-usage)
   * [运行状况检查](/help/sites-administering/reporting.md#health-check)
   * [工作流报告](/help/sites-administering/reporting.md#workflow-report)

>[!NOTE]
>
>教程“ [创建您自己的报告——示例](#creating-your-own-report-an-example) ”还显示了可以使用以下原则的数量。
>
>您还可以参阅标准报告，查看其他实施示例。

>[!NOTE]
>
>在下面的示例和定义中，使用了以下记号：
>
>* 每行定义一个节点或一个属性，其中：
   >
   >  
* `N:<name> [<nodeType>]`
   >
   >     
   描述名称为和节点类 `<*name*>` 型为的节点 `<*nodeType*>`*。*
   >
   >  
* `P:<name> [<propertyType]`
   >
   >     
   描述名称为的属性 `<*name*>` 和属性类型为 `<*propertyType*>`。
   >
   >  
* `P:<name> = <value>`
   >
   >     
   描述必须 `<name>` 设置为的值的属性 `<value>`。
   >
   >
* 缩进显示节点之间的层次依赖关系。
>* 以|表示列表可能的项目；例如，类型或名称：
>
>  
例如 `String|String[]` ，表示该属性可以是String或String[]。
>
>* `[]` 描述数组；如字符串[] ，或查询定义中的节点 [数组](#query-definition)。
>
>
除非另有说明，否则默认类型为：
>
>* 节点- `nt:unstructured`
>* 属性 - `String`


## 报告框架 {#reporting-framework}

报告框架遵循以下原则：

* 它完全基于由CQ5 QueryBuilder执行的查询返回的结果集。
* 结果集定义报告中显示的数据。 结果集中的每一行对应于报表的表格视图中的一行。
* 可在结果集上执行的操作类似于RDBMS概念；主要 *是分组**和聚合*。

* 大多数数据检索和处理都是在服务器端完成的。
* 客户单独负责显示预处理的数据。 客户端仅执行次要处理任务（例如，在单元格内容中创建链接）。

报告框架（由标准报告的结构说明）使用由处理队列提供的以下构件块：

![chlimage_1-248](assets/chlimage_1-248.png)

### 报告页面 {#report-page}

报告页面：

* 是标准CQ5页面。
* 基于为报 [告配置的标准CQ5模板](#report-template)。

### 报告库 {#report-base}

该组 [ 件构成了任何报表的基础 `reportbase`](#report-base-component) :

* 保留提供基础 [数据](#the-query-and-data-retrieval) 结果集的查询的定义。

* 是一个经过调整的段落系统，它将包含添加到报 `columnbase`表的所有列()。
* 定义哪些图表类型可用以及哪些当前处于活动状态。
* 定义编辑对话框，该对话框允许用户配置报表的某些方面。

### 列基 {#column-base}

每列都是组件的一个实 [ 例， `columnbase` 它](#column-base-component) :

* 是段落，由各个报表的parsys( `reportbase`)使用。
* 定义指向基础结 [果集的链接](#the-query-and-data-retrieval);例如，定义在此结果集中引用的特定数据以及处理它的方式。
* 包含其他定义；如可用的聚合和过滤器以及任何默认值。

### 查询与数据检索 {#the-query-and-data-retrieval}

查询:

* 定义为组件的一 [`reportbase`](#report-base) 部分。
* 基于 [CQ QueryBuilder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html)。
* 检索用作报告基础的数据。 结果集（表）的每行都绑定到由查询返回的节点。 然后，从此 [数据集中提](#column-base-component) 取各列的特定信息。

* 通常由以下组成：

   * 根路径。

      它指定要搜索的存储库的子树。

      为帮助将性能影响降至最低，建议（尝试）将查询限制到存储库的特定子树。 根路径可以在报告模板中预 [定义](#report-template) ，也可以由用户在“配置(编 [辑)”对话框中设置](#configuration-dialog)。

   * [一个或多个条件](#query-definition)。

      这些是为了产生（初始）结果集；例如，这些限制包括对节点类型或属性约束的限制。

**这里的关键点是，查询结果集中返回的每个节点都用于在报表上生成单行（因此为1:1关系）。**

开发人员必须确保为报表定义的查询返回适合该报表的节点集。 但是，节点本身不需要保存所有必需的信息，这也可以从父节点和／或子节点派生。 例如，用于“用户报告”的 [查询](/help/sites-administering/reporting.md#user-report) ，会根据节点类型选择节点(在本例中为 `rep:user`)。 但是，此报告中的大多数列不会直接从这些节点获取其数据，而是从子节点获取 `profile`。

### 处理队列 {#processing-queue}

该 [查询](#the-query-and-data-retrieval) ，返回要作为行显示在报表上的数据集。 在将结果集中的每一行传输到客户端以在报 [告上显示之前](#phases-of-the-processing-queue)，将在多个阶段中处理（服务器端）。

这允许：

* 从基础结果集提取和导出值。

   例如，它允许您通过计算两个属性值之间的差值，将两个属性值作为单个值进行处理。

* 解析提取的值；这可以通过多种方式实现。

   例如，路径可以映射到标题(如各个 *jcr:title属性中更易于阅读的内容* )。

* 在不同点应用过滤器。
* 根据需要创建复合值。

   例如，由显示给用户的文本、用于排序的值和用于创建链接的其他URL（在客户端）组成。

#### 处理队列的工作流 {#workflow-of-the-processing-queue}

以下工作流表示处理队列：

![chlimage_1-249](assets/chlimage_1-249.png)

#### 处理队列的阶段 {#phases-of-the-processing-queue}

其中包括以下详细步骤和元素：

1. 使用值提取器将初始 [查询（报表库）返回的结果转换](#query-definition) 到基本结果集中。

   根据列类型自动选择值提 [取器](#column-specific-definitions)。 它们用于从基础JCR查询读取值并从中创建结果集；之后，可以应用进一步的处理。 例如，对于类 `diff` 型，值提取器读取两个属性，计算随后添加到结果集的单个值。 无法配置值提取器。

1. 对于包含原始数据的初始结果集，应 [用初始过滤](#column-specific-definitions) (*原始相位* )。

1. 值已预先 [处理](#processing-queue);如应用阶段所 *定义* 。

1. [对预处理值](#column-specific-definitions) (指定给预处 *理阶段* )执行过滤。

1. 值已解析；根据定义的解 [析器](#processing-queue)。
1. [对已解析](#column-specific-definitions) 的值执行筛选( *分配给已解析* 的阶段)。

1. 数据是分 [组和聚集的](#column-specific-definitions)。
1. 通过将数组数据转换为（基于字符串的）列表来解析它。

   这是一个隐式步骤，它将多值结果转换为可显示的列表;它是基于多值JCR属性的（未聚集）单元格值所必需的。

1. 值再次被预 [处理](#processing-queue);为afterApply阶段 *定义* 。

1. 数据被排序。
1. 处理后的数据被传送到客户端。

>[!NOTE]
>
>返回基本数据结果集的初始查询在组件上被定 `reportbase` 义。
>
>处理队列的其他元素在组件上被定 `columnbase` 义。

## 报告构建和配置 {#report-construction-and-configuration}

构建和配置报告时需要满足以下条件：

* 报 [表组件的定义位置](#location-of-report-components)
* 组 [`reportbase` 件](#report-base-component)
* 一个或多个 [ 组 `columnbase` 件](#column-base-component)
* 页面 [组件](#page-component)
* 报 [告设计](#report-design)
* 报告 [模板](#report-template)

### 报表组件的位置 {#location-of-report-components}

默认报告组件位于下方 `/libs/cq/reporting/components`。

但是，强烈建议您不要更新这些节点，而是在或更合适的情况下创建自己 `/apps/cq/reporting/components` 的组件节点 `/apps/<yourProject>/reports/components`。

其中（例如）:

```
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
```

在此下面，您为报表创建根，在此下面，报表基础组件和列基础组件：

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

报表页面必须使用 `sling:resourceType` 的 `/libs/cq/reporting/components/reportpage`。

自定义的页面组件不应是必需的（在大多数情况下）。

## 报表基础组件 {#report-base-component}

每个报告类型都需要一个派生自的容器组件 `/libs/cq/reporting/components/reportbase`。

此组件充当整个报告的容器，并提供以下信息：

* 查询 [定义](#query-definition)。
* 用于 [配置报表的(可选](#configuration-dialog) )对话框。
* 在报 [告中集](#chart-definitions) 成的任何Charts。

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

   可用于将结果集限制为具有具有特定值的特定属性的节点。 如果指定了多个约束，则节点必须满足所有约束（AND运算）。

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

   将返回用 `textimage` 户上次修改的所有组 `admin` 件。

* `nodeTypes`

   用于将结果集限制为指定的节点类型。 可以指定多个节点类型。

* `mandatoryProperties`

   可用于将结果集限制为具有所有指定属 *性* 的节点。 属性的值不会被考虑在内。

所有选项都是可选的，并且可以根据需要组合，但您必须至少定义其中一个。

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

      由于可以定义多个设置，因此您可以使用它定义当前处于活动状态的设置。 这些节点由一组节点定义(这些节点没有强制命名约定，但标准报告通常使用 `0`, `1`.. `x`)，每个属性具有以下属性：

      * `id`

         活动图表的标识。 这必须与其中一个图表的id匹配 `definitions`。

* `definitions`

   定义可能可用于报表的图表类型。 将 `definitions` 由设置指定要使用的 `active` 内容。

   定义是使用节点数组指定的(通常也称为 `0`, `1`... `x`)，每个属性具有以下属性：

   * `id`

      图表标识。

   * `type`

      可用图表的类型。 选择自：

      * `pie`
饼图。 仅从当前数据生成。

      * `lineseries`
一系列线（连接表示实际快照的点）。 仅从历史数据生成。
   * 其他属性可用，具体取决于图表类型：

      * 对于图表类型 `pie`:

         * `maxRadius` ( `Double/Long`)

            饼图允许的最大半径；因此，图表允许的最大大小（无图例）。 如果已定义， `fixedRadius` 则忽略。

         * `minRadius` ( `Double/Long`)

            饼图允许的最小半径。 如果已定义， `fixedRadius` 则忽略。

         * `fixedRadius` ( `Double/Long`)为饼图定义固定半径。
      * 对于图表类型 [`lineseries`](/help/sites-administering/reporting.md#display-limits):

         * `totals` ( `Boolean`)

            如果应当显示显示“ **Total** ”的其他行，则为true。
默认: `false`

         * `series` ( `Long`)

            要显示的行数／序列数。
默认：(这也 `9` 是允许的最大值)

         * `hoverLimit` ( `Long`)

            将显示弹出窗口的最大聚合快照数（每条水平线上显示的点表示不同值），即当用户将鼠标悬停在图表图例中的不同值或相应标签上时。

            默认：( `35` 即，如果当前图表设置的不同值超过35个，则不显示任何弹出窗口)。

            另外，限制10个弹出窗口可以并行显示（当将鼠标悬停在图例文本上时，可显示多个弹出窗口）。



### 配置对话框 {#configuration-dialog}

每个报告都可以有一个配置对话框，允许用户为报告指定各种参数。 打开报告页面时，可通过 **“编辑** ”按钮访问该对话框。

此对话框是标准的CQ [对话框](/help/sites-developing/components-basics.md#dialogs) ，可进行相应配置(请参阅 [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog) ，了解详细信息)。

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

提供了多个预配置组件；可以在对话框中使用值为 `xtype` 的属性引用这些属性 `cqinclude`:

* **`title`**

   `/libs/cq/reporting/components/commons/title`

   用于定义报表标题的文本字段。

* **`description`**

   `/libs/cq/reporting/components/commons/description`

   文本区域以定义报表描述。

* **`processing`**

   `/libs/cq/reporting/components/commons/processing`

   报告的处理模式的选择器（手动／自动加载数据）。

* **`scheduling`**

   `/libs/cq/reporting/components/commons/scheduling`

   为历史图表安排快照的选择器。

>[!NOTE]
>
>引用的组件必须使用后缀 `.infinity.json` 包含在内（请参阅上例）。

### 根路径 {#root-path}

此外，还可以为报告定义根路径：

* **`rootPath`**

   这会将报告限制在存储库的某个部分（树或子树），建议您这样做以便进行性能优化。 根路径由每个报告页面的节 `rootPath` 点的属性指 `report` 定（创建页面时从模板获取）。

   它可以由以下人员指定：

   * 报告 [模板](#report-template) （作为固定值或作为配置对话框的默认值）。
   * 用户（使用此参数）

## 列基础组件 {#column-base-component}

每个列类型都需要从派生的组件 `/libs/cq/reporting/components/columnbase`。

列组件定义以下组合：

* 特定于 [列的查询配置](#column-specific-query) 。
* 分辨率 [和预处理](#resolvers-and-preprocessing)。
* 列 [特定定义](#column-specific-definitions) (如过滤器和聚合;子 `definitions` 节点)。
* [列默认值](#column-default-values)。
* 客户 [端过滤器](#client-filter) ，用于从服务器返回的数据中提取要显示的信息。
* 此外，列组件必须提供适当的实例 `cq:editConfig`。 定义所需 [的事件和操作](#events-and-actions) 。
* 通用列的 [配置](#generic-columns)。

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

另请参阅 [定义新报表](#defining-your-new-report)。

### 列特定查询 {#column-specific-query}

这定义了在单个列中使用的特 [定数据提取(来自报表数据结果集](#the-query-and-data-retrieval))。

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

   如果属性定义为String[] ，则扫描多个属性（按顺序）以查找实际值。

   例如，在以下情况下：

   `property = [ "jcr:lastModified", "jcr:created" ]`

   相应的值提取器（此处控制）将：

   * 检查是否有jcr:lastModified属性可用，如果有，请使用它。
   * 如果没有jcr:lastModified属性可用，则将改用jcr:created的内容。

* `subPath`

   如果结果不位于由查询返回的节点上，则定义 `subPath` 该属性的实际位置。

* `secondaryProperty`

   定义另一个属性，该属性还必须用于计算实际单元格值；这将仅用于某些列类型（差异和可排序）。

   例如，对于“工作流实例报告”，指定的属性用于存储开始和结束时间之间的时间差的实际值（以毫秒为单位）。

* `secondarySubPath`

   与subPath类似， `secondaryProperty` 使用时。

在大多数情况下，只 `property` 会使用。

### 客户端过滤器 {#client-filter}

客户端过滤器从服务器返回的数据中提取要显示的信息。

>[!NOTE]
>
>在应用整个服务器端处理后，将执行此过滤器客户端。

```xml
N:definitions
    N:data
        P:clientFilter [String]
```

`clientFilter` 定义为一个JavaScript函数，该函数：

* 作为输入，接收一个参数；从服务器返回的数据（因此完全预处理）
* 作为输出，返回已过滤（已处理）的值；从输入信息中提取或派生的数据

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

### 分辨率和预处理 {#resolvers-and-preprocessing}

处理 [队列定义各种解析器](#processing-queue) ，并配置预处理：

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

   定义要使用的解析程序。 可使用以下解析器：

   * `const`

      将值映射到其他值；例如，它用于解析常量，如 `en` 到其等效值 `English`

   * `default`

      默认解析程序。 这是一个虚拟解析程序，它实际上不会解决任何问题。

   * `page`

      解析相应页面路径的路径值；更准确地说，是到相应节 `jcr:content` 点的。 例如， `/content/.../page/jcr:content/par/xyz` 解析为 `/content/.../page/jcr:content`。

   * `path`

      通过（可选）附加子路径并从已解析路径处的节点属性（由定义）中获取实际值来解析路径 `resolverConfig`值。 例如，可以 `path` 将 `/content/.../page/jcr:content` 其中一个解析为属性内容，这 `jcr:title` 意味着页面路径解析为页面标题。

   * `pathextension`

      通过预定路径并从已解析路径的节点的属性中获取实际值来解析值。 例如，某个值 `de` 可能以路径为前缀，如从属性中取值 `/libs/wcm/core/resources/languages`，将国家／地区代码解析 `language`为语言说明 `de``German`。

* `resolverConfig`

   提供解析程序的定义；可用的选项取决于所选 `resolver` 选项：

   * `const`

      使用属性指定要解析的常量。 属性名称定义要解析的常数；属性的值定义已解析的值。

      例如， **Name**=和Value `1` 的属性将解析为1 ****`=One` 到1。

   * `default`

      没有可用的配置。

   * `page`

      * `propertyName` （可选）

         定义应用于解析值的属性的名称。 如果未指定，则使用 *jcr:title* （页面标题）的默认值；对于解 `page` 析程序，这意味着首先将路径解析为页面路径，然后进一步解析为页面标题。
   * `path`

      * `propertyName` （可选）

         指定用于解析值的属性的名称。 如果未指定，则使用默 `jcr:title` 认值。

      * `subPath` （可选）

         此属性可用于指定在解析值之前附加到路径的后缀。
   * `pathextension`

      * `path` (mandatory)

         定义要前置的路径。

      * `propertyName` (mandatory)

         定义实际值所在的已解析路径上的属性。

      * `i18n` (可选；类型Boolean)

         确定解析的值是否应 *国际化* (即使用 [CQ5的国际化服务](/help/sites-administering/tc-manage.md))。



* `preprocessing`

   预处理是可选的，可以（单独）绑定到处理阶段 *应用**或应用* After:

   * `apply`

      初始预处理阶段([处理队列表示中的步骤3](#processing-queue))。

   * `applyAfter`

      在预处理后应用([处理队列的表示中的步骤9](#processing-queue))。

#### 分辨率 {#resolvers}

解析器用于提取所需的信息。 各种解析器的示例有：

**康斯特**

下面将解析字符串的 `VersionCreated` contant值 `New version created`。

See `/libs/cq/reporting/components/auditreport/typecol/definitions/data`.

```xml
N:data
    P:resolver=const
    N:resolverConfig
        P:VersionCreated="New version created"
```

**页面**

解析对应页面的jcr:content(child)节点上jcr:description属性的路径值。

See `/libs/cq/reporting/components/compreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=page
    N:resolverConfig
        P:propertyName="jcr:description"
```

**路径**

以下代码解析了属 `/content/.../page` 性内容的路径，这 `jcr:title` 意味着页面路径解析到页面标题。

See `/libs/cq/reporting/components/auditreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=path
    N:resolverConfig
        P:propertyName="jcr:title"
        P:subPath="/jcr:content"
```

**路径扩展**

以下代码使用路 `de` 径扩展为值 `/libs/wcm/core/resources/languages`附加前缀，然后从属性中获取值 `language`，将国家／地区代码解析 `de` 为语言描述 `German`。

See `/libs/cq/reporting/components/userreport/languagecol/definitions/data`.

```xml
N:data
    P:resolver=pathextension
    N:resolverConfig
        P:path="/libs/wcm/core/resources/languages"
        P:propertyName="language"
```

#### 预处理 {#preprocessing}

该定 `preprocessing` 义可应用于以下任一项：

* 原始值：

   原始值的预处理定义在和／或 `apply` 直接指定 `applyAfter` 。

* 值：

   如果需要，可以为每个聚合提供单独的定义。

   要指定聚合值的显式预处理，预处理定义必须驻留在相应的子 `aggregated` 节点( `apply/aggregated`, `applyAfter/aggregated`)上。 如果需要对不同聚合进行显式预处理，则预处理定义位于具有相应聚合名称的子节点(例如，或其 `apply/aggregated/min/max` 他聚合)上。

您可以指定以下任一选项以在预处理过程中使用：

* [查找并替](#preprocessing-find-and-replace-patterns)换模式发现后，指定的模式(定义为常规表达式)被另一个模式替换；例如，这可用于提取原始文件的子字符串。

* [数据类型格式化程序](#preprocessing-data-type-formatters)

   将数字值转换为相对字符串；例如，表示1小时时差的值“”将解析为字符串，如 `1:24PM (1 hour ago)`。

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

#### 预处理——查找和替换图案 {#preprocessing-find-and-replace-patterns}

对于预处理，您可以指 `pattern` 定(定义为正则表达式 [或正则表达式](https://en.wikipedia.org/wiki/Regular_expression) )，然后用模式进行 `replace` 替换：

* `pattern`

   用于定位子字符串的常规表达式。

* `replace`

   将用作原始字符串的替换的字符串或字符串的表示形式。 通常，这表示由常规表达式定位的字符串的子字符串 `pattern`。

示例替换可分为：

* 对于具有以下 `definitions/data/preprocessing/apply` 两个属性的节点：

   * `pattern`: `(.*)(/jcr:content)(/|$)(.*)`
   * `replace`: `$1`

* 字符串的形式为：

   * `/content/geometrixx/en/services/jcr:content/par/text`

* 将分为四个部分：

   * `$1` - `(.*)` - `/content/geometrixx/en/services`
   * `$2` - `(/jcr:content)` - `/jcr:content`
   * `$3` - `(/|$)` - `/`
   * `$4` - `(.*)` - `par/text`

* 并替换为以下代码表示的字符串 `$1`:

   * `/content/geometrixx/en/services`

#### 预处理——数据类型格式化程序 {#preprocessing-data-type-formatters}

这些格式化程序将数字值转换为相对字符串。

例如，这可用于允许和聚合的时 `min`间 `avg` 列 `max` 。 As `min`/ `avg`/ `max` 聚合显示为时 *间差* (例如， `10 days ago`)，它们需要数据格式化程序。 为此，格 `datedelta` 式化器被应用于 `min`/ `avg`/聚 `max` 合值。 如果 `count` 聚合也可用，则不需要格式设置程序，原始值也不需要。

当前可用的数据类型格式化程序包括：

* `format`

   数据类型格式化程序：

   * `duration`

      持续时间是两个定义日期之间的时间跨度。 例如，工作流操作的开始和结束，该操作耗时1小时，从2/13/11 11:23h开始，1小时后于2/13/11 12:23h结束。

      它将一个数值（解释为毫秒）转换为持续时间字符串；例如， `30000` 格式化为* `30s`.*

   * `datedelta`

      Datadelta是过去某个日期到“现在”的时间跨度（因此，如果在以后某个时间点查看报告，则其结果会有所不同）。

      它将数字值（解释为以天为单位的时差）转换为相对日期字符串。 例如，1的格式设置为1天前。

以下示例定义 `datedelta` 了格式 `min` 和 `max` 聚合:

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

特定于列的定义定义了该列的可用过滤器和聚合。

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

      用于提取汇总所需日期的部分部分（例如，按年分组以获取每年的汇总数据）。

   * `sortable`

      用于使用不同值（从不同属性取）进行排序和显示的值。
   此外， 以上任意一个可定义为多值；例如，定 `string[]` 义字符串数组。

   值提取器由列类型选择。 如果某个值提取器可用于某列类型，则使用该提取器。 否则，使用默认值提取器。

   类型可以（可选）采用参数。 例如，从 `timeslot:year` 日期字段提取年份。 类型及其参数：

   * `timeslot` -这些值与相应的常数比较 `java.utils.Calendar`。

      * `timeslot:year` - `Calendar.YEAR`
      * `timeslot:month-of-year` - `Calendar.MONTH`
      * `timeslot:week-of-year` - `Calendar.WEEK_OF_YEAR`
      * `timeslot:day-of-month` - `Calendar.DAY_OF_MONTH`
      * `timeslot:day-of-week` - `Calendar.DAY_OF_WEEK`
      * `timeslot:day-of-year` - `Calendar.DAY_OF_YEAR`
      * `timeslot:hour-of-day` - `Calendar.HOUR_OF_DAY`
      * `timeslot:minute-of-hour` - `Calendar.MINUTE`


* `groupable`

   定义报表是否可以按此列分组。

* `filters`

   过滤器定义。

   * `filterType`

      可用过滤器包括：

      * `string`

         基于字符串的过滤器。
   * `id`

      过滤器标识符。

   * `phase`

      可用阶段：

      * `raw`

         过滤器应用于原始数据。

      * `preprocessed`

         对预处理的数据应用过滤器。

      * `resolved`

         过滤器应用于已解析的数据。


* `aggregates`

   聚合定义。

   * `text`

      聚合的文本名称。 如 `text` 果未指定，则采用默认的聚合描述；例如， `minimum` 将用于该 `min` 聚合。

   * `type`

      聚合类型。 可用聚合包括：

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

         提供所有值的和。

      * `median`

         提供中值。

      * `percentile95`

         采用所有值的第95百分位数。

### 列默认值 {#column-default-values}

用于定义列的默认值：

```xml
N:defaults
    P:aggregate
```

* `aggregate`

   有 `aggregate` 效值与下的值相同 `type` ( `aggregates` 请参阅列特定定定 [义(定义-过滤器/聚合)](#column-specific-definitions) )。

### 事件和操作 {#events-and-actions}

“编辑配置”定义监听器检测的必要事件以及这些事件发生后要应用的操作。 有关背景 [信息，请参阅组件开发](/help/sites-developing/components.md) 的介绍。

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

### 常规列 {#generic-columns}

通用列是一个扩展，其中（大多数）列定义存储在列节点（而非组件节点）的实例上。

它们使用一个（标准）对话框，您可以为单个通用组件自定义该对话框。 该对话框允许报表用户在报表页面上定义通用列的列属性(使用菜单选项列 **属性……**)。

例如，用 **户报** 告的“通 **用”列**;请参 `/libs/cq/reporting/components/userreport/genericcol`阅。

要使列成为通用列，请执行以下操作：

* 将列 `type` 节点的属性设 `definition` 置为 `generic`。

   See `/libs/cq/reporting/components/userreport/genericcol/definitions`

* 在列的节点下指定（标准）对话框定 `definition` 义。

   See `/libs/cq/reporting/components/userreport/genericcol/definitions/dialog`

   * 对话框的字段必须引用与相应组件属性相同的名称（包括其路径）。

      例如，如果要使通过对话框配置通用列的类型，请使用名称为的字段 `./definitions/type`。

   * 使用UI/对话框定义的属性优先于组件上定义的属 `columnbase` 性。

* 定义编辑配置。

   See `/libs/cq/reporting/components/userreport/genericcol/cq:editConfig`

* 使用标准AEM方法来定义（其他）列属性。

   请注意，对于在组件实例和列实例上定义的属性，列实例上的值优先。

   通用列的可用属性包括：

   * `jcr:title` -列名称
   * `definitions/aggregates` -聚合
   * `definitions/filters` -过滤器
   * `definitions/type`-列的类型（必须在对话框中定义，使用选择器／组合框或隐藏字段）
   * `definitions/data/resolver` 和 `definitions/data/resolverConfig` (但不 `definitions/data/preprocessing` 是或 `.../clientFilter`)-解析程序和配置
   * `definitions/queryBuilder` -查询构建器配置
   * `defaults/aggregate` -默认聚合
   如果用户报告上通用列的新实例 **** ，则使用对话框定义的属性将保留在以下位置：

   `/etc/reports/userreport/jcr:content/report/columns/genericcol/settings/generic`

## 报告设计 {#report-design}

设计定义了可用于创建报告的列类型。 它还定义了向其添加列的段落系统。

强烈建议您为每个报告创建单独的设计。 这确保了完全的灵活性。 另请参阅 [定义新报表](#defining-your-new-report)。

默认报告组件位于下方 `/etc/designs/reports`。

报告的位置取决于组件所在的位置：

* `/etc/designs/reports/<yourReport>` 如果报告位于更低的位置，则适合 `/apps/cq/reporting`

* `/etc/designs/<yourProject>/reports/<*yourReport*>` 对于使用模式的报 `/apps/<yourProject>/reports` 告

必需的设计属性在上 `jcr:content/reportpage/report/columns` 注册(例如 `/etc/designs/reports/<reportName>/jcr:content/reportpage/report/columns`):

* `components`

   报表中允许的任何组件和／或组件组。

* `sling:resourceType`

   具有值的属 `cq/reporting/components/repparsys`性。

示例设计代码片断（取自组件报告的设计）是：

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

不需要为各个列指定设计。 可在设计模式下定义可用列。

>[!NOTE]
>
>建议不要对标准报告设计进行任何更改。 这是为了确保在升级或安装修补程序时不会丢失任何更改。
>
>如果要自定义标准报告，请复制报告及其设计。

>[!NOTE]
>
>创建报告时，可以自动创建默认列。 模板中指定了这些值。

## 报告模板 {#report-template}

每个报告类型都必须提供一个模板。 这些是标 [准CQ模板](/help/sites-developing/templates.md) ，可以这样配置。

模板必须：

* 设置 `sling:resourceType` 为 `cq/reporting/components/reportpage`

* 指示要使用的设计
* 通过 `report` 属性创建引用容器( `reportbase`)组件的子节点 `sling:resourceType`

示例模板片段（取自组件报表模板）是：

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

显示根路径（取自用户报告模板）的定义的示例模板片断是：

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

默认报告模板位于下方 `/libs/cq/reporting/templates`。

但是，强烈建议您不要更新这些节点，而是在或更合适的情况下创建自己 `/apps/cq/reporting/templates` 的组件节点 `/apps/<yourProject>/reports/templates`。

其中，例如(另请参阅报 [表组件的位置](#location-of-report-components)):

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
```

在此下，您可以为模板创建根：

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
                N:<reportname> [sling:Folder]
```

## 创建您自己的报告——示例 {#creating-your-own-report-an-example}

### 定义新报表 {#defining-your-new-report}

要定义新报表，您必须创建并配置：

1. 报表组件的根。
1. 报表基础组件。
1. 一个或多个列基组件。
1. 报告设计。
1. 报表模板的根目录。
1. 报表模板。

为了说明这些步骤，以下示例定义了一个报告，该报告列表了存储库中的所有OSGi配置；即节点的所有实 `sling:OsgiConfig` 例。

>[!NOTE]
>
>复制现有报告，然后自定义新版本是一种替代方法。

1. 为新报表创建根节点。

   例如，在 `/apps/cq/reporting/components/osgireport`。

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:components [sling:Folder]
               N:osgireport [sling:Folder]
   ```

1. 定义报表库。 例如， `osgireport[cq:Component]` 在 `/apps/cq/reporting/components/osgireport`下。

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

   这定义了一个报表基本组件，它：

   * 搜索类型的所有节点 `sling:OsgiConfig`
   * 显示两 `pie` 者和图 `lineseries` 表
   * 为用户提供了配置报告的对话框

1. 定义您的第一列（列库）组件。 例如， `bundlecol[cq:Component]` 在 `/apps/cq/reporting/components/osgireport`下。

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

   这定义了列基组件，它：

   * 搜索并返回从服务器接收的值；在这种情况下，每个节 `jcr:path` 点的属 `sling:OsgiConfig` 性
   * 提供了 `count` 聚合
   * 不可分组
   * 具有标 `Bundle` 题（表中的列标题）
   * 在Sidekick组中 `OSGi Report`
   * 在指定事件上刷新
   >[!NOTE]
   >
   >在此示例中，没有和的定 `N:data` 义 `P:clientFilter`。 这是因为从服务器收到的值是按1:1返回的——这是默认行为。
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

1. 定义报告设计。 例如， `osgireport[cq:Page]` 在 `/etc/designs/reports`下。

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

   例如，在 `/apps/cq/reporting/templates/osgireport`。

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:templates [sling:Folder]
               N:osgireport [cq:Template]
   ```

1. 定义您的报表模板。 例如， `osgireport[cq:Template]` 在 `/apps/cq/reporting/templates`下。

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

   * 为生成 `allowedPaths` 的报告定义——在上述情况下，位于 `/etc/reports`
   * 提供模板的标题和说明
   * 提供在模板列表中使用的缩略图图像（上面未列出此节点的完整定义——最容易从现有报表复制thumbnail.png实例）。

### 创建新报表的实例 {#creating-an-instance-of-your-new-report}

现在可以创建新报告的实例：

1. Open the **Tools** console.

1. 在 **左侧窗格** 中选择“报告”。
1. 然 **后新……** 中。 定义标 **题和名** 称 **，从模板列表中选择新的报表类型(** OSGi报表模板 **)，然后单击******&#x200B;创建。
1. 您的新报告实例将显示在列表中。 多次-单击此图标可打开。
1. 从Sidekick中拖动组件( **例如，** OSGi Report **组中的Bundle** )以创建第一列并 [开始报表定义](/help/sites-administering/reporting.md#the-basics-of-report-customization)。

   >[!NOTE]
   >
   >由于此示例没有任何可分组列，因此图表将不可用。 要查看图表，请将其 `groupable` 设置为 `true`:
   >
   >
   ```
   >N:osgireport [sling:Folder]
   > N:bundlecol [cq:Component]
   > N:definitions [nt:unstructured]
   > P:groupable [Boolean] = true
   >```

## 配置Report Framework Services {#configuring-the-report-framework-services}

本节介绍用于实现报告框架的OSGi服务的高级配置选项。

可以使用Web控制台的“配置”菜单查看这些组件(例如，在 `http://localhost:4502/system/console/configMgr`)。 When working with AEM there are several methods of managing the configuration settings for such services; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

### 基本服务(第CQ天报告配置) {#basic-service-day-cq-reporting-configuration}

* **时区** 定义为其创建时区历史数据。 这是为了确保历史图表显示全球每个用户的相同数据。
* **区域设置** ，定义要与历史数据的时区一起使 **用的区域设置** 。 区域设置用于确定某些特定于区域设置的日历设置（例如，一周的第一天是星期日还是星期一）。

* **快照路径** ，定义存储历史图表快照的根路径。
* **报告路径** ，定义报告所在的路径。 快照服务使用它确定报表以实际为其拍摄快照。
* **每日快照** ，定义每日快照拍摄时间。 指定的小时位于服务器的本地时区中。
* **每小时快照** ，定义每小时拍摄每小时快照的分钟数。
* **行（最大）** 定义每个快照所存储的最大行数。 应当合理选择该值；如果它太高，将影响存储库的大小，如果太低，则数据可能不准确，因为历史数据的处理方式。
* **假数据**，启用后，利用选择器即可创建假历史数 `fakedata` 据；如果禁用，则使用选择 `fakedata` 器将引发异常。

   由于数据是假的，它只 *能用* 于测试和调试目的。

   使用选 `fakedata` 择器将隐式完成报告，因此所有现有数据都将丢失；数据可以手动恢复，但这可能是一个耗时的过程。

* **快照用户** ，定义可用于拍摄快照的可选用户。

   基本上，快照是为完成报告的用户拍摄的。 可能存在以下情况（例如，在发布系统中，此用户不存在，因为其帐户尚未复制），您希望指定一个使用的备用用户。

   此外，指定用户可能会带来安全风险。

* **强制使用快照用户**，如果启用，则所有快照都将与在“快照”用户下指定的用 *户一起拍摄*。 如果处理不当，这可能会造成严重的安全影响。

### 缓存设置(Day CQ报告缓存) {#cache-settings-day-cq-reporting-cache}

* **启用** ，允许您启用或禁用报告数据的缓存。 启用报告缓存后，将在多个请求期间将报告数据保留在内存中。 这可能会提高性能，但会导致内存消耗增加，在极端情况下可能导致内存不足。
* **TTL** 定义缓存报告数据的时间（以秒为单位）。 数量越大，性能越好，但如果数据在时间段内发生变化，则返回的数据可能也不准确。
* **最大条目数** ，可定义每次要缓存的最大报告数。

>[!NOTE]
>
>每个用户和语言的报告数据可能不同。 因此，按报告、用户和语言缓存报告数据。 这意味着， **Max entries值** ，实际 `2` 缓存以下任一数据：
>
>* 针对不同语言设置的两个用户的一个报告
>* 一个用户和两个报告
>



