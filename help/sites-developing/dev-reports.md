---
title: 开发报告
description: Adobe Experience Manager (AEM)根据报表框架提供了一系列标准报表
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 3891150e-9972-4bbc-ad61-7f46a1f9bbb4
source-git-commit: b66ec42c35b5b60804015d340b8194bbd6ef3e28
workflow-type: tm+mt
source-wordcount: '5182'
ht-degree: 0%

---


# 开发报告 {#developing-reports}

Adobe Experience Manager (AEM)提供了一系列 [标准报表](/help/sites-administering/reporting.md) 其中大多数都基于报告框架。

利用框架，您可以扩展这些标准报表，或开发您自己的新报表。 报告框架与现有CQ5概念和原则紧密集成，以便开发人员可以使用他们对CQ5的现有知识作为开发报告的跳板。

对于通过AEM交付的标准报表：

* 这些报告基于报告框架：

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
>教程 [创建您自己的报表 — 示例](#creating-your-own-report-an-example) 还显示了可以使用多少条以下原则。
>
>您还可以参阅标准报表以查看其他实施示例。

>[!NOTE]
>
>在下面的示例和定义中，使用以下表示法：
>
>* 每行定义一个节点或属性，其中：
>  `N:<name> [<nodeType>]` ：描述名称为 `<*name*>` 和节点类型 `<*nodeType*>`*.*
>  `P:<name> [<propertyType]` ：描述名称为 `<*name*>` 和属性类型 `<*propertyType*>`.
>  `P:<name> = <value>` ：描述属性 `<name>` 必须设置为的值 `<value>`.
>
>* 缩进显示节点之间的分层依赖关系。
>* 项目分隔方式 |表示可能项目的列表；例如，类型或名称；例如， `String|String[]` 表示该属性可以是字符串或字符串[].
>
>* `[]` 描述数组；如String[] 或节点数组，如 [查询定义](#query-definition).
>
>除非另有说明，否则默认类型为：
>
>* 节点 —  `nt:unstructured`
>* 属性 - `String`

## 报告框架 {#reporting-framework}

报告框架遵循以下原则：

* 它完全基于CQ5 QueryBuilder执行的查询返回的结果集。
* 结果集定义报告中显示的数据。 结果集中的每一行对应于报告表格视图中的一行。
* 可用于对结果集执行的操作类似于RDBMS概念；主要是 *分组* 和 *聚合*.

* 大多数数据检索和处理都在服务器端完成。
* 客户端单独负责显示预处理后的数据。 客户端仅执行次要的处理任务（例如，在单元格内容中创建链接）。

报告框架（由标准报表的结构图示）使用以下构建块，由处理队列提供：

![chlimage_1-248](assets/chlimage_1-248.png)

### 报告页面 {#report-page}

报告页面为：

* 标准CQ5页面。
* 基于 [为报告配置的标准CQ5模板](#report-template).

### 报表库 {#report-base}

此 [`reportbase` 组件](#report-base-component) 构成任何报表的基础，因为它：

* 保留 [查询](#the-query-and-data-retrieval) 提供数据的底层结果集。

* 它是一个经过调整的段落系统，包含所有列( `columnbase`)已添加到报表。
* 定义哪些图表类型可用以及哪些图表类型当前处于活动状态。
* 定义“编辑”对话框，该对话框允许用户配置报告的某些方面。

### 列基数 {#column-base}

每列都是 [`columnbase` 组件](#column-base-component) 即：

* 是一个段落，由parsys ( `reportbase`)。
* 定义指向的链接 [基础结果集](#the-query-and-data-retrieval). 即，它定义此结果集中引用的特定数据及其处理方式。
* 保留其他定义；例如可用的聚合和筛选器以及任何默认值。

### 查询与数据检索 {#the-query-and-data-retrieval}

查询：

* 定义为 [`reportbase`](#report-base) 组件。
* 基于 [CQ QueryBuilder](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/search/QueryBuilder.html).
* 检索用作报表基础的数据。 结果集（表）的每一行都绑定到查询返回的节点。 的特定信息 [单个列](#column-base-component) 然后从该数据集提取。

* 通常包括：

   * 根路径。

     这会指定要搜索的存储库的子树。

     为了帮助将性能影响降至最低，建议（尝试）将查询限制在存储库的特定子树中。 根路径可在 [报告模板](#report-template) 或由用户在 [配置（编辑）对话框](#configuration-dialog).

   * [一个或多个标准](#query-definition).

     这些条件用来生成（初始）结果集；例如，它们包括对节点类型的限制或属性约束。

**这里的关键点是，查询结果集中返回的每个单个节点都用于在报表上生成一行（因此是1:1关系）。**

开发人员必须确保为报告定义的查询返回适合该报告的节点集。 但是，节点本身不需要保存所有必需的信息，这也可以从父节点和/或子节点派生。 例如，用于 [用户报告](/help/sites-administering/reporting.md#user-report) 根据节点类型选择节点（在本例中） `rep:user`)。 但是，此报表中的大多数列并非直接从这些节点获取其数据，而是从子节点获取数据 `profile`.

### 正在处理队列 {#processing-queue}

此 [查询](#the-query-and-data-retrieval) 返回在报表中作为行显示的数据的结果集。 结果集中的每一行都将被处理（服务器端），位于 [多个阶段](#phases-of-the-processing-queue)，然后传输到客户端以在报表中显示。

这允许：

* 从基础结果集中提取和派生值。

  例如，通过它计算两个属性值的差异，可以将两个属性值处理为单个值。

* 解析提取的值；这可以通过多种方式完成。

  例如，路径可以映射到标题（在各自更易于用户阅读的内容中） *jcr：title* 属性)。

* 在不同点应用过滤器。
* 创建复合值（如有必要）。

  例如，由向用户显示的文本、用于排序的值以及用于创建链接的附加URL（在客户端）组成。

#### 处理队列的工作流 {#workflow-of-the-processing-queue}

以下工作流表示处理队列：

![chlimage_1-249](assets/chlimage_1-249.png)

#### 处理队列的阶段 {#phases-of-the-processing-queue}

其中详细步骤和元素包括：

1. 转换返回的结果 [初始查询(reportbase)](#query-definition) 使用值提取器将转换为基本结果集。

   根据以下条件自动选择值提取器 [列类型](#column-specific-definitions). 它们用于从基础JCR查询中读取值并从这些值中创建结果集；之后，可以应用进一步处理。 例如，对于 `diff` 类型，值提取器读取两个属性，计算单个值，然后将该值添加到结果集中。 无法配置值提取器。

1. 对于包含原始数据初始结果集， [初始滤波](#column-specific-definitions) (*原始* （阶段）。

1. 值包括 [已预处理](#processing-queue)；如为 *应用* 阶段。

1. [正在筛选](#column-specific-definitions) (分配给 *已预处理* 阶段)。

1. 值会得到解析；根据 [定义的解析程序](#processing-queue).
1. [正在筛选](#column-specific-definitions) (分配给 *已解决* 阶段)。

1. 数据是 [分组和汇总](#column-specific-definitions).
1. 数组数据通过将它转换为（基于字符串的）列表来解析。

   这是一个隐式步骤，用于将多值结果转换为可以显示的列表；基于多值JCR属性的（未聚合）单元格值需要此步骤。

1. 值再次为 [已预处理](#processing-queue)；如为 *afterApply* 阶段。

1. 数据按顺序排序。
1. 处理过的数据被传输到客户端。

>[!NOTE]
>
>返回基础数据结果集的初始查询定义于 `reportbase` 组件。
>
>处理队列的其他元素定义在 `columnbase` 组件。

## 报告构建和配置 {#report-construction-and-configuration}

构建和配置报告需要以下各项：

* a [用于定义报表组件的位置](#location-of-report-components)
* a [`reportbase` 组件](#report-base-component)
* 一个或多个， [`columnbase` 组件](#column-base-component)
* a [页面组件](#page-component)
* a [报告设计](#report-design)
* a [报告模板](#report-template)

### 报表组件的位置 {#location-of-report-components}

默认报表组件保存在 `/libs/cq/reporting/components`.

但是，建议您不要更新这些节点，而是在下创建自己的组件节点 `/apps/cq/reporting/components` 或者，如果更合适 `/apps/<yourProject>/reports/components`.

其中（例如）：

```
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
```

在此下，您将创建报表的根，并在其下，创建报表基组件和列基组件：

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

报表页面必须使用 `sling:resourceType` 之 `/libs/cq/reporting/components/reportpage`.

（通常）不需要自定义页面组件。

## 报表基础组件 {#report-base-component}

每种报表类型都需要一个派生自 `/libs/cq/reporting/components/reportbase`.

此组件充当整个报表的容器，并提供以下信息：

* 此 [查询定义](#query-definition).
* An [（可选）对话框](#configuration-dialog) 以配置报表。
* 任何 [图表](#chart-definitions) 与报告集成的内容。

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

  将结果集限制为具有特定属性（含特定值）的节点。 如果指定了多个约束，则节点必须满足所有约束（AND操作）。

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

  将返回所有 `textimage` 上次由修改的组件 `admin` 用户。

* `nodeTypes`

  用于将结果集限制为指定的节点类型。 可以指定多个节点类型。

* `mandatoryProperties`

  将结果集限制为具有 *所有* 指定的属性。 未考虑属性的值。

所有变量都是可选的，可以根据需要进行组合，但您必须至少定义其中一个。

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

  保留活动图表的定义。

   * `active`

     由于可以定义多个设置，因此您可以使用此项来定义哪些设置当前处于活动状态。 它们由节点数组定义(这些节点没有强制的命名约定，但标准报告通常使用 `0`， `1`.. `x`)，则每个属性都如下所示：

      * `id`

        活动图表的标识。 此名称必须匹配某个图表的ID `definitions`.

* `definitions`

  定义可用于报表的图表类型。 此 `definitions` 要使用的由 `active` 设置。

  定义是使用节点数组(通常也命名为 `0`， `1`.. `x`)，则每个配置文件具有以下属性：

   * `id`

     图表的标识。

   * `type`

     可用的图表类型。 选择自：

      * `pie`
饼图。 仅从当前数据生成。

      * `lineseries`
一系列线（表示实际快照的连接点）。 仅从历史数据生成。

   * 还有其他可用的属性，具体取决于图表类型：

      * 对于图表类型 `pie`：

         * `maxRadius` ( `Double/Long`)

           饼图允许的最大半径；因此图表允许的最大大小（无图例）。 忽略条件 `fixedRadius` 已定义。

         * `minRadius` ( `Double/Long`)

           饼图允许的最小半径。 忽略条件 `fixedRadius` 已定义。

         * `fixedRadius` ( `Double/Long`)定义饼图的固定半径。

      * 对于图表类型 [`lineseries`](/help/sites-administering/reporting.md#display-limits)：

         * `totals` ( `Boolean`)

           如果额外的一行显示 **总计** 应该显示。
默认: `false`

         * `series` ( `Long`)

           要显示的行数/系列数。
默认： `9` （这也是允许的最大值）

         * `hoverLimit` ( `Long`)

           要显示弹出窗口的聚合快照（在每个水平线上显示的圆点，表示不同值）的最大数量。 也就是说，当用户在图表图例中将鼠标悬停在不同的值或对应的标签上时。

           默认： `35` （即，如果超过35个不同的值适用于当前的图表设置，则根本不会显示弹出窗口）。

           对于可以并行显示的弹出窗口，还有十个额外的限制（当在图例文本上悬停鼠标时，可以显示多个弹出窗口）。

### 配置对话框 {#configuration-dialog}

每个报告都可以有一个配置对话框，允许用户为报告指定各种参数。 此对话框可通过 **编辑** 按钮。

此对话框是一个标准CQ [对话框](/help/sites-developing/components-basics.md#dialogs) 并且可以按此方式配置(请参阅 [CQ.Dialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Dialog) 了解更多信息)。

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

提供了多个预配置的组件；可在对话框中使用 `xtype` 值为的属性 `cqinclude`：

* **`title`**

  `/libs/cq/reporting/components/commons/title`

  用于定义报告标题的文本字段。

* **`description`**

  `/libs/cq/reporting/components/commons/description`

  用于定义报表说明的文本区域。

* **`processing`**

  `/libs/cq/reporting/components/commons/processing`

  报表处理模式的选择器（手动/自动加载数据）。

* **`scheduling`**

  `/libs/cq/reporting/components/commons/scheduling`

  用于为历史图表计划快照的选择器。

>[!NOTE]
>
>必须使用 `.infinity.json` 后缀（请参阅以上示例）。

### 根路径 {#root-path}

此外，还可以为报告定义根路径：

* **`rootPath`**

  这会将报表限制在存储库的特定部分（树或子树）中，这是为优化性能而建议的。 根路径由 `rootPath` 的属性 `report` 每个报表页面的节点（在创建页面时从模板中获取）。

  可以通过以下方式指定：

   * 该 [报告模板](#report-template) （作为固定值或作为配置对话框的默认值）。
   * 用户（使用此参数）

## 列基本组件 {#column-base-component}

每个列类型都需要一个派生自 `/libs/cq/reporting/components/columnbase`.

列组件定义了以下各项的组合：

* 此 [列特定查询](#column-specific-query) 配置。
* 此 [解析器和预处理](#resolvers-and-preprocessing).
* 此 [列特定的定义](#column-specific-definitions) (如过滤器和聚合； `definitions` 子节点)。
* [列默认值](#column-default-values).
* 此 [客户端筛选器](#client-filter) 从服务器返回的数据中提取信息以供显示。
* 此外，列组件必须提供适当的实例 `cq:editConfig`. 以定义 [事件和操作](#events-and-actions) 必需。
* 的配置 [通用列](#generic-columns).

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

另请参阅 [定义新报告](#defining-your-new-report).

### 列特定查询 {#column-specific-query}

这会定义特定的数据提取(从 [报表数据结果集](#the-query-and-data-retrieval))，以便在单独的列中使用。

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

  如果属性被定义为字符串[]，则会（按顺序）扫描多个属性以查找实际值。

  例如，如果存在：

  `property = [ "jcr:lastModified", "jcr:created" ]`

  相应的值提取器（在此处进行控制）：

   * 检查是否有jcr：lastModified属性可用，如果已可用，则使用它。
   * 如果没有可用的jcr：lastModified属性，则改用jcr：created的内容。

* `subPath`

  如果结果不在查询返回的节点上， `subPath` 定义资产的位置。

* `secondaryProperty`

  必须用于计算实际单元格值的第二个属性。 此定义仅用于某些列类型（差异和可排序）。

  例如，如果存在工作流实例报表，则指定的属性用于存储开始时间和结束时间之间时间差的实际值（以毫秒为单位）。

* `secondarySubPath`

  与subPath类似，当 `secondaryProperty` 已使用。

通常，仅 `property` 已使用。

### 客户端筛选器 {#client-filter}

客户端过滤器从服务器返回的数据中提取要显示的信息。

>[!NOTE]
>
>在应用整个服务器端处理之后，在客户端运行此过滤器。

```xml
N:definitions
    N:data
        P:clientFilter [String]
```

此 `clientFilter` 是一个JavaScript函数，该函数：

* 作为输入，接收一个参数；从服务器返回的数据（如此完全预处理）
* 作为输出，返回滤波（已处理）值；从输入信息提取或导出的数据

以下示例从组件路径中提取对应的页面路径：

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

此 [处理队列](#processing-queue) 定义各种解析器并配置预处理：

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

  定义要使用的解析程序。 可以使用以下解析器：

   * `const`

     将值映射到其他值；例如，这用于解析常量，如 `en` 到它的等效值 `English`.

   * `default`

     默认解析程序。 这是一个虚拟解析器，实际上不会解析任何内容。

   * `page`

     将路径值解析为相应页面的路径；更准确地说，解析为相应的 `jcr:content` 节点。 例如， `/content/.../page/jcr:content/par/xyz` 已解析为 `/content/.../page/jcr:content`.

   * `path`

     解析路径值，方法是（可选）附加子路径并从节点的属性中获取实际值（如所定义） `resolverConfig`)。 例如， `path` 之 `/content/.../page/jcr:content` 可以解析为的内容 `jcr:title` 属性，这意味着页面路径解析为页面标题。

   * `pathextension`

     通过在路径前面添加并从已解析路径上节点的属性中获取实际值来解析值。 例如，值 `de` 前面可能会附加一个路径，例如 `/libs/wcm/core/resources/languages`，获取属性的值 `language`，解析国家/地区代码 `de` 到语言描述 `German`.

* `resolverConfig`

  提供解析程序的定义。 可用的选项取决于 `resolver` 已选定：

   * `const`

     使用属性指定要解析的常量。 属性的名称定义要解析的常量；属性的值定义解析的值。

     例如，属性具有 **名称**= `1` 和 **值** `=One` 解析1到1。

   * `default`

     无配置可用。

   * `page`

      * `propertyName` （可选）

        定义用于解析值的属性的名称。 如果未指定，则默认值 *jcr：title* （页面标题）来表示；对于 `page` 解析程序，这意味着首先路径解析为页面路径，然后进一步解析为页面标题。

   * `path`

      * `propertyName` （可选）

        指定用于解析值的属性的名称。 如果未指定，则默认值 `jcr:title` 已使用。

      * `subPath` （可选）

        此属性可用于指定在解决值之前附加到路径的后缀。

   * `pathextension`

      * `path` （必填）

        定义要在前面添加的路径。

      * `propertyName` （必填）

        定义实际值所在的已解析路径上的属性。

      * `i18n` （可选；键入布尔值）

        确定解析的值是否应为 *国际化* (即，使用 [CQ5的国际化服务](/help/sites-administering/tc-manage.md))。

* `preprocessing`

  预处理是可选的，可以绑定（单独绑定）到处理阶段 *应用* 或 *applyAfter*：

   * `apply`

     初始预处理阶段([处理队列表示中的步骤3](#processing-queue))。

   * `applyAfter`

     预处理后应用([处理队列表示的步骤9](#processing-queue))。

#### 解析程序 {#resolvers}

解析器用于提取所需的信息。 各种解析器的示例包括：

**常量**

下面解析一个常量值 `VersionCreated` 到字符串 `New version created`.

请参阅 `/libs/cq/reporting/components/auditreport/typecol/definitions/data`.

```xml
N:data
    P:resolver=const
    N:resolverConfig
        P:VersionCreated="New version created"
```

**页面**

解析相应页面的jcr：content（子）节点上jcr：description属性的路径值。

请参阅 `/libs/cq/reporting/components/compreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=page
    N:resolverConfig
        P:propertyName="jcr:description"
```

**路径**

以下解析了 `/content/.../page` 的内容 `jcr:title` 属性，这意味着页面路径解析为页面标题。

请参阅 `/libs/cq/reporting/components/auditreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=path
    N:resolverConfig
        P:propertyName="jcr:title"
        P:subPath="/jcr:content"
```

**路径扩展**

以下内容在值前面加上 `de` 带有路径扩展名 `/libs/wcm/core/resources/languages`，然后从属性中获取值 `language`，解析国家/地区代码 `de` 到语言描述 `German`.

请参阅 `/libs/cq/reporting/components/userreport/languagecol/definitions/data`.

```xml
N:data
    P:resolver=pathextension
    N:resolverConfig
        P:path="/libs/wcm/core/resources/languages"
        P:propertyName="language"
```

#### 预处理 {#preprocessing}

此 `preprocessing` 定义可以应用于以下任一项：

* 原始值：

  在上指定原始值的预处理定义 `apply` 和/或 `applyAfter` 直接。

* 处于聚合状态的值：

  如有必要，可以为每个聚合提供单独的定义。

  要为聚合值指定显式预处理，预处理定义必须驻留在各自的上 `aggregated` 子节点( `apply/aggregated`， `applyAfter/aggregated`)。 如果需要对不同的聚合进行显式预处理，则预处理定义位于具有相应聚合名称的子节点上(例如 `apply/aggregated/min/max` 或其他聚合)。

您可以指定预处理期间使用的以下任一选项：

* [查找和替换模式](#preprocessing-find-and-replace-patterns)
找到后，指定的模式（定义为正则表达式）会被其他模式替换；例如，这可用于提取原始模式的子字符串。

* [数据类型格式化程序](#preprocessing-data-type-formatters)

  将数值转换为相对字符串；例如，“表示一小时时间差的值”将解析为字符串，如 `1:24PM (1 hour ago)`.

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

对于预处理，您可以指定 `pattern` (定义为 [正则表达式](https://en.wikipedia.org/wiki/Regular_expression) 或正则表达式)，然后由 `replace` 模式：

* `pattern`

  用于查找子字符串的正则表达式。

* `replace`

  用作原始字符串的替换的字符串或字符串表示形式。 通常，它表示由正则表达式定位的字符串的子字符串 `pattern`.

示例替换可划分为：

* 对于节点 `definitions/data/preprocessing/apply` 具有以下两个属性：

   * `pattern`：`(.*)(/jcr:content)(/|$)(.*)`
   * `replace`：`$1`

* 一个字符串以：

   * `/content/geometrixx/en/services/jcr:content/par/text`

* 分为四个部分：

   * `$1` - `(.*)` - `/content/geometrixx/en/services`
   * `$2` - `(/jcr:content)` - `/jcr:content`
   * `$3` - `(/|$)` - `/`
   * `$4` - `(.*)` - `par/text`

* 替换为表示的字符串。 `$1`：

   * `/content/geometrixx/en/services`

#### 预处理 — 数据类型格式化程序 {#preprocessing-data-type-formatters}

这些格式化程序将数值转换为相对字符串。

例如，这可用于时间列，它允许 `min`， `avg` 和 `max` 聚合。 作为 `min`/ `avg`/ `max` 聚合显示为 *时差* (例如， `10 days ago`)，则需要数据格式化程序。 对于此， `datedelta` 格式化程序应用于 `min`/ `avg`/ `max` 聚合值。 如果 `count` 聚合也可用，它不需要格式器，原始值也不需要。

目前可用的数据类型格式化程序包括：

* `format`

  数据类型格式化程序：

   * `duration`

     持续时间是两个已定义日期之间的时间范围。 例如，某个工作流操作的开始和结束时间为1小时，从2/13/11 11:23h开始，1小时后于2/13/11 12:23h结束。

     它将数值（解释为毫秒）转换为持续时间字符串；例如， `30000` 格式为* `30s`.*

   * `datedelta`

     Datadelta是过去日期到“现在”之间的时间范围（因此，如果在以后的某个时间点查看报表，则结果不同）。

     它将数字值（解释为以天为单位的时间差异）转换为相对日期字符串。 例如，1的格式为1天前。

以下示例定义 `datedelta` 格式化 `min` 和 `max` 聚合：

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

### 列特定的定义 {#column-specific-definitions}

特定于列的定义定义定义了该列可用的过滤器和聚合。

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

  以下选项可用作标准选项：

   * `string`
   * `number`
   * `int`
   * `date`
   * `diff`
   * `timeslot`

     用于提取聚合所需日期的各个部分（例如，按年分组，以获取每年聚合的数据）。

   * `sortable`

     用于使用不同值（从不同属性获取）进行排序和显示的值。

  此外，以上任何一种都可以定义为多值，例如， `string[]` 定义字符串数组。

  值提取器由列类型选择。 如果值提取器可用于列类型，则使用此提取器。 否则，使用默认值提取器。

  类型可以（可选）采用参数。 例如， `timeslot:year` 从日期字段中提取年份。 类型及其参数：

   * `timeslot`  — 这些值与对应的常量具有可比性， `java.utils.Calendar`.

      * `timeslot:year` - `Calendar.YEAR`
      * `timeslot:month-of-year` - `Calendar.MONTH`
      * `timeslot:week-of-year` - `Calendar.WEEK_OF_YEAR`
      * `timeslot:day-of-month` - `Calendar.DAY_OF_MONTH`
      * `timeslot:day-of-week` - `Calendar.DAY_OF_WEEK`
      * `timeslot:day-of-year` - `Calendar.DAY_OF_YEAR`
      * `timeslot:hour-of-day` - `Calendar.HOUR_OF_DAY`
      * `timeslot:minute-of-hour` - `Calendar.MINUTE`

* `groupable`

  定义是否可按此列对报告进行分组。

* `filters`

  筛选器定义。

   * `filterType`

     可用的过滤器包括：

      * `string`

        基于字符串的过滤器。

   * `id`

     筛选器标识符。

   * `phase`

     可用阶段：

      * `raw`

        该过滤器应用于原始数据。

      * `preprocessed`

        该过滤器应用于预处理数据。

      * `resolved`

        该过滤器应用于已解析的数据。

* `aggregates`

  聚合定义。

   * `text`

     聚合的文本名称。 如果 `text` 如果未指定，则它采用聚合的默认描述。 例如， `minimum` 用于 `min` 聚合。

   * `type`

     聚合类型。 可用的聚合包括：

      * `count`

        计算行数。

      * `count-nonempty`

        计算非空行的数量。

      * `min`

        它提供最小值。

      * `max`

        它提供最大值。

      * `average`

        它提供平均值。

      * `sum`

        它提供所有值的总和。

      * `median`

        它提供中间值。

      * `percentile95`

        使用所有值的第95百分位数。

### 列默认值 {#column-default-values}

定义列的默认值：

```xml
N:defaults
    P:aggregate
```

* `aggregate`

  有效 `aggregate` 值与的值相同 `type` 下 `aggregates` (请参阅 [列特定的定义（定义 — 过滤器/聚合）](#column-specific-definitions) )。

### 事件和操作 {#events-and-actions}

编辑配置定义监听程序检测到的必要事件以及发生这些事件后要应用的操作。 请参阅 [组件开发简介](/help/sites-developing/components.md) 了解背景信息。

必须定义以下值以确保满足所有必需操作：

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

通用列是一种扩展，其中（大部分）列定义存储在列节点的实例（而不是组件节点）上。

它们使用（标准）对话框，您可以为单个类属元件定制该对话框。 此对话框允许报告用户定义报告页面上通用列的列属性（使用菜单选项） **列属性……**)。

示例为 **通用** 列 **用户报告**. 请参阅 `/libs/cq/reporting/components/userreport/genericcol`.

要将列设为通用列，请执行以下操作：

* 设置 `type` 列的属性 `definition` 节点至 `generic`.

  请参阅 `/libs/cq/reporting/components/userreport/genericcol/definitions`

* 在列的下方指定（标准）对话框定义 `definition` 节点。

  请参阅 `/libs/cq/reporting/components/userreport/genericcol/definitions/dialog`

   * 对话框的字段必须引用与相应组件属性（包括其路径）相同的名称。

     例如，如果要通过对话框配置类属列的类型，请使用名称为的字段 `./definitions/type`.

   * 使用UI/对话框定义的属性优先于 `columnbase` 组件。

* 定义编辑配置。

  请参阅 `/libs/cq/reporting/components/userreport/genericcol/cq:editConfig`

* 使用标准AEM方法定义（其他）列属性。

  对于在组件和列实例上定义的属性，列实例上的值优先。

  通用列的可用属性包括：

   * `jcr:title`  — 列名称
   * `definitions/aggregates`  — 聚合
   * `definitions/filters`  — 过滤器
   * `definitions/type` — 列的类型（必须在对话框中通过使用选择器/组合框或隐藏字段定义）
   * `definitions/data/resolver` 和 `definitions/data/resolverConfig` (但没有 `definitions/data/preprocessing` 或 `.../clientFilter`) — 解析程序和配置
   * `definitions/queryBuilder`  — 查询生成器配置
   * `defaults/aggregate`  — 默认聚合

  如果类属列的新实例位于 **用户报告**，则通过对话框定义的属性将保留在下：

  `/etc/reports/userreport/jcr:content/report/columns/genericcol/settings/generic`

## 报告设计 {#report-design}

设计会定义哪些列类型可用于创建报告。 它还定义了向其中添加列的段落系统。

Adobe建议您为每个报告创建单独的设计。 这样做可确保完全的灵活性。 请参阅 [定义新报告](#defining-your-new-report).

默认报表组件保存在 `/etc/designs/reports`.

报表的位置取决于组件的位置：

* `/etc/designs/reports/<yourReport>` 适用于报告位于 `/apps/cq/reporting`

* `/etc/designs/<yourProject>/reports/<*yourReport*>` 对于使用 `/apps/<yourProject>/reports` 模式

必需的设计属性注册于 `jcr:content/reportpage/report/columns` (例如， `/etc/designs/reports/<reportName>/jcr:content/reportpage/report/columns`)：

* `components`

  报表中允许的任何组件和/或组件组。

* `sling:resourceType`

  带值的属性 `cq/reporting/components/repparsys`.

一个设计代码片段示例（摘自组件报表的设计）为：

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

不需要为各个列指定设计。 可用列可在设计模式下定义。

>[!NOTE]
>
>Adobe建议您不要更改标准报表设计。 这是为了确保您在升级或安装修补程序时不会丢失任何更改。
>
>如果要自定义标准报表，请复制报表及其设计。

>[!NOTE]
>
>创建报告时，可以自动创建默认列。 这些在模板中指定。

## 报表模板 {#report-template}

每种报表类型都必须提供一个模板。 这些是标准的 [CQ模板](/help/sites-developing/templates.md) 并且可以按此方式配置。

模板必须：

* 设置 `sling:resourceType` 到 `cq/reporting/components/reportpage`

* 指示要使用的设计
* 创建 `report` 引用容器的子节点( `reportbase`)组件使用 `sling:resourceType` 属性

模板片段的示例（取自组件报表模板）为：

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

一个示例模板片段显示了根路径（取自用户报表模板）的定义，如下所示：

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

默认报表模板保留在 `/libs/cq/reporting/templates`.

但是，Adobe建议您不要更新这些节点。 请改为在下创建自己的组件节点 `/apps/cq/reporting/templates` 或者，如果更合适 `/apps/<yourProject>/reports/templates`.

其中，作为示例(另请参阅 [报表组件的位置](#location-of-report-components))：

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
```

在此下，创建模板的根：

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
                N:<reportname> [sling:Folder]
```

## 创建您自己的报表 — 示例 {#creating-your-own-report-an-example}

### 定义新报告 {#defining-your-new-report}

要定义报表，请创建和配置：

1. 报表组件的根。
1. 报表基础组件。
1. 一个或多个列基本组件。
1. 报告设计。
1. 报表模板的根。
1. 报表模板。

为了说明这些步骤，以下示例定义了一个报表，其中列出了存储库中的所有OSGi配置。 也就是说， `sling:OsgiConfig` 节点。

>[!NOTE]
>
>复制现有报表，然后自定义新版本是一种替代方法。

1. 为新报表创建根节点。

   例如，在 `/apps/cq/reporting/components/osgireport`.

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:components [sling:Folder]
               N:osgireport [sling:Folder]
   ```

1. 定义您的报表库。 例如， `osgireport[cq:Component]` 下 `/apps/cq/reporting/components/osgireport`.

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

   这将定义一个报表基组件，该组件可以：

   * 搜索类型为的所有节点 `sling:OsgiConfig`
   * 显示两者 `pie` 和 `lineseries` 图表
   * 为用户配置报告提供了一个对话框

1. 定义您的第一列(columnbase)组件。 例如， `bundlecol[cq:Component]` 下 `/apps/cq/reporting/components/osgireport`.

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

   这将定义一个具有以下特征的列基组件：

   * 搜索并返回它从服务器收到的值；在本例中，属性为 `jcr:path` 每隔 `sling:OsgiConfig` 节点
   * 提供 `count` 总计
   * 不可分组
   * 具有标题 `Bundle` （表中的列标题）
   * 在副手组里 `OSGi Report`
   * 在指定事件上刷新

   >[!NOTE]
   >
   >在此示例中，没有定义 `N:data` 和 `P:clientFilter`. 这是因为从服务器收到的值是以1:1为基数返回的 — 这是默认行为。
   >
   >这与定义相同：
   >
   >```
   >N:data [nt:unstructured]
   >   P:clientFilter [String] = "function(v) { return v; }"
   >```
   >
   >其中，函数仅返回它收到的值。

1. 定义报告设计。 例如， `osgireport[cq:Page]` 下 `/etc/designs/reports`.

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

   例如，在 `/apps/cq/reporting/templates/osgireport`.

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:templates [sling:Folder]
               N:osgireport [cq:Template]
   ```

1. 定义报表模板。 例如， `osgireport[cq:Template]` 下 `/apps/cq/reporting/templates`.

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

   这将定义一个模板，该模板：

   * 定义 `allowedPaths` 对于生成的报表 — 在上例中，位于下的任意位置 `/etc/reports`
   * 提供模板的标题和描述
   * 提供用于模板列表的缩略图图像（上面未列出此节点的完整定义 — 最简单的方法是从现有报表复制thumbnail.png的实例）。

### 创建新报告的实例 {#creating-an-instance-of-your-new-report}

现在可以创建新报告的实例：

1. 打开 **工具** 控制台。

1. 选择 **报表** 在左窗格中。
1. 则 **新建……** 工具栏中。 定义 **标题** 和 **名称**，选择您的新报表类型( **OSGi报表模板**)，然后单击 **创建**.
1. 您的新报表实例随即会显示在列表中。 双击以打开。
1. 拖动组件(例如， **捆绑** 在 **OSGi报表** 组)创建第一列和 [启动报表定义](/help/sites-administering/reporting.md#the-basics-of-report-customization).

   >[!NOTE]
   >
   >由于此示例没有任何可分组的列，因此图表不可用。 要查看图表，请设置 `groupable` 到 `true`：
   >
   >```
   >N:osgireport [sling:Folder]
   > N:bundlecol [cq:Component]
   > N:definitions [nt:unstructured]
   > P:groupable [Boolean] = true
   >```
   >

## 配置报表框架服务 {#configuring-the-report-framework-services}

此部分介绍用于实施报表框架的OSGi服务的高级配置选项。

可以使用Web控制台的配置菜单(位于 `http://localhost:4502/system/console/configMgr`例如)。 使用AEM时，可通过多种方法管理此类服务的配置设置；请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以了解更多详细信息和建议的做法。

### 基本服务（Day CQ报告配置） {#basic-service-day-cq-reporting-configuration}

* **时区** 定义为其创建历史数据的时区。 这是为了确保历史图表显示全球每个用户的相同数据。
* **区域设置** 定义要使用的区域设置 **时区** 用于历史数据。 区域设置用于确定某些特定于区域设置的日历设置（例如，一周的第一天是星期日还是星期一）。

* **快照路径** 定义存储历史图表快照的根路径。
* **报表路径** 定义报告所在的路径。 快照服务使用此选项来确定要为其实际生成快照的报表。
* **每日快照** 定义每天生成每日快照的小时。 指定的小时位于服务器的本地时区中。
* **每小时快照** 定义在生成每小时快照时每小时的分钟数。
* **行（最大值）** 定义为每个快照存储的最大行数。 应合理选择此值。 如果它太高，则会影响存储库的大小；如果太低，则数据可能因为处理历史数据的方式而不准确。
* **虚假数据**，如果启用，则可以使用创建虚假历史数据 `fakedata` 选择器；如果禁用，则使用 `fakedata` 选择器引发异常。

  因为数据是假的，所以必须 *仅限* 用于测试和调试目的。

  使用 `fakedata` 选择器隐式完成报表，因此所有现有数据都会丢失。 数据可以手动恢复，但这是一个非常耗时的过程。

* **快照用户** 定义可用于生成快照的可选用户。

  基本上，会为完成报告的用户拍摄快照。 在某些情况下（例如，在发布系统上，此用户不存在，因为其帐户尚未复制），您可能会需要指定替代使用的回退用户。

  此外，指定用户可能会带来安全风险。

* **强制快照用户**，如果启用，则所有快照都将使用下指定的用户来创建 *快照用户*. 如果处理不当，这可能会造成严重的安全影响。

### 缓存设置(Day CQ Reporting Cache) {#cache-settings-day-cq-reporting-cache}

* **启用** 允许您启用或禁用报表数据的缓存。 启用报表缓存会在多个请求期间将报表数据保留在内存中。 这可能会提高性能，但会导致内存消耗增加，并且在极端情况下可能会导致内存不足的情况。
* **TTL** 定义缓存报表数据的时间（以秒为单位）。 较高的数字可以提高性能，但如果数据在某个时间段内发生更改，则也可能返回不准确的数据。
* **最大条目数** 定义在任意时间要缓存的报表的最大数量。

>[!NOTE]
>
>每个用户和语言的报告数据可能不同。 因此，按照报表、用户和语言，会缓存报表数据。 这意味着 **最大条目数** 值 `2` 实际缓存以下任一项的数据：
>
>* 一个报表，用于具有不同语言设置的两个用户
>* 一个用户和两个报告
>
