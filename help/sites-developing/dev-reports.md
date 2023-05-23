---
title: 開發報表
seo-title: Developing Reports
description: AEM根據報告架構提供一系列標準報告
seo-description: AEM provides a selection of standard reports based on a reporting framework
uuid: 1b406d15-bd77-4531-84c0-377dbff5cab2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 50fafc64-d462-4386-93af-ce360588d294
exl-id: 3891150e-9972-4bbc-ad61-7f46a1f9bbb4
source-git-commit: 071bc0e36ed2d8eb4ce7bd0ba46823adc0e43095
workflow-type: tm+mt
source-wordcount: '5238'
ht-degree: 0%

---


# 開發報表 {#developing-reports}

AEM提供以下選項 [標準報表](/help/sites-administering/reporting.md) 其中大部分都以報告架構為基礎。

使用框架，您可以擴充這些標準報表，或開發您自己的全新報表。 報告架構與現有的CQ5概念和原則緊密整合，因此開發人員可以利用他們現有的CQ5知識作為開發報告的跳板。

對於透過AEM傳送的標準報表：

* 這些報表是以報表架構為基礎：

   * [组件报告](/help/sites-administering/reporting.md#component-report)
   * [页面活动报告](/help/sites-administering/reporting.md#page-activity-report)
   * [用户报告](/help/sites-administering/reporting.md#user-report)
   * [工作流实例报告](/help/sites-administering/reporting.md#workflow-instance-report)

* 下列報表是根據個別原則，因此無法擴充：

   * [磁盘使用情况](/help/sites-administering/reporting.md#disk-usage)
   * [健康情況檢查](/help/sites-administering/reporting.md#health-check)
   * [工作流程報告](/help/sites-administering/reporting.md#workflow-report)

>[!NOTE]
>
>教學課程 [建立您自己的報表 — 範例](#creating-your-own-report-an-example) 也會顯示以下原則中可供使用的數量。
>
>您也可以參閱標準報表，檢視其他實作範例。

>[!NOTE]
>
>在下列範例和定義中使用下列標籤法：
>
>* 每一行會定義一個節點或屬性，其中：
   >  `N:<name> [<nodeType>]` ：說明名稱為「 」的節點 `<*name*>` 和節點型別 `<*nodeType*>`*.*
   >  `P:<name> [<propertyType]` ：說明名稱為「 」的屬性 `<*name*>` 和的屬性型別 `<*propertyType*>`.
   >  `P:<name> = <value>` ：說明屬性 `<name>` ，此值必須設定為 `<value>`.
>
>* 縮排顯示節點之間的階層式相依性。
>* 專案分隔方式 |代表可能專案的清單；例如，型別或名稱；例如。 `String|String[]` 表示屬性可以是字串或字串[].
>
>* `[]` 描述陣列；例如String[] 或節點陣列，如 [查詢定義](#query-definition).
>
>除非另有說明，否則預設型別為：
>
>* 節點 —  `nt:unstructured`
>* 属性 - `String`


## 報告框架 {#reporting-framework}

報告架構遵循下列原則：

* 它完全以CQ5 QueryBuilder執行的查詢所傳回的結果集為基礎。
* 結果集定義了報告中顯示的資料。 結果集中的每一列都對應到報告表格檢視中的某一列。
* 可在結果集上執行的操作類似於RDBMS概念；主要是 *分組* 和 *彙總*.

* 大部分的資料擷取與處理作業都於伺服器端進行。
* 使用者端應自行負責顯示預先處理的資料。 使用者端只會執行次要的處理工作（例如在儲存格內容中建立連結）。

報表架構（以標準報表的結構說明）會使用以下建置區塊，由處理佇列饋送：

![chlimage_1-248](assets/chlimage_1-248.png)

### 報告頁面 {#report-page}

報告頁面：

* 是標準CQ5頁面。
* 是根據 [為報表設定的標準CQ5範本](#report-template).

### 報表基礎 {#report-base}

此 [ `reportbase` 元件](#report-base-component) 構成任何報表的基礎，如下所示：

* 保留 [查詢](#the-query-and-data-retrieval) 提供基礎的結果資料集。

* 是經過調整的段落系統，將包含所有欄( `columnbase`)已新增至報表。
* 定義哪些圖表型別可用以及哪些目前作用中。
* 定義「編輯」對話方塊，供使用者設定報表的某些層面。

### 欄基底 {#column-base}

每欄都是 [ `columnbase` 元件](#column-base-component) 即：

* 是一個段落，由parsys ( `reportbase`)。
* 定義連結至 [基礎結果集](#the-query-and-data-retrieval)；亦即定義此結果集中參照的特定資料，及其處理方式。
* 保留其他定義；例如可用的彙總和篩選以及任何預設值。

### 查詢與資料擷取 {#the-query-and-data-retrieval}

查詢：

* 定義為 [ `reportbase`](#report-base) 元件。
* 根據 [CQ QueryBuilder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html).
* 擷取用來作為報表基礎的資料。 結果集（表格）的每一列都會繫結至查詢傳回的節點。 特定資訊 [個別欄](#column-base-component) 然後會從此資料集擷取。

* 通常包含：

   * 根路徑。

      這會指定要搜尋之存放庫的子樹狀結構。

      為了協助將效能影響降至最低，建議（嘗試）將查詢限制在存放庫的特定子樹狀結構。 根路徑可在 [報告範本](#report-template) 或由使用者在 [設定（編輯）對話方塊](#configuration-dialog).

   * [一或多個條件](#query-definition).

      這些條件是為了產生（初始）結果集而強制執行；例如，它們包括對節點型別的限制或屬性限制。

**這裡的關鍵點是，查詢結果集中傳回的每個單一節點都用於在報表上產生單一列（所以是1:1關係）。**

開發人員必須確保為報表定義的查詢傳回適合該報表的節點集。 但是，節點本身不需要保留所有必要的資訊，這也可以從父節點和/或子節點衍生。 例如，查詢用於 [使用者報告](/help/sites-administering/reporting.md#user-report) 根據節點型別選取節點（在此例中） `rep:user`)。 不過，此報表上的大部分欄並非直接從這些節點取得資料，而是從子節點取得 `profile`.

### 處理佇列 {#processing-queue}

此 [查詢](#the-query-and-data-retrieval) 傳回要在報表中顯示為列的結果資料集。 結果集中的每一列都會經過處理（伺服器端），位於 [幾個階段](#phases-of-the-processing-queue)，然後傳輸到使用者端以在報表上顯示。

這允許：

* 從基礎結果集擷取和衍生值。

   例如，它可讓您計算兩個屬性值之間的差異，將兩個屬性值處理為單一值。

* 解析擷取的值；這可以透過多種方式完成。

   例如，路徑可以對應到標題（如在對應內容中人類看得懂的內容） *jcr：title* 屬性)。

* 在不同點套用篩選器。
* 視需要建立複合值。

   例如，由對使用者顯示的文字、要用於排序的值以及用於建立連結的其他URL （在使用者端）組成。

#### 處理佇列的工作流程 {#workflow-of-the-processing-queue}

以下工作流程代表處理佇列：

![chlimage_1-249](assets/chlimage_1-249.png)

#### 處理佇列的階段 {#phases-of-the-processing-queue}

其中詳細步驟和元素為：

1. 轉換傳回的結果 [初始查詢(reportbase)](#query-definition) 使用值擷取器輸入基本結果集。

   系統會根據 [欄型別](#column-specific-definitions). 它們用於從基礎JCR查詢讀取值，並從這些值建立結果集；之後可以應用進一步處理。 例如，對於 `diff` 型別，值擷取器會讀取兩個屬性，並計算之後新增至結果集的單一值。 無法設定值擷取器。

1. 對於包含原始資料的初始結果集， [初始篩選](#column-specific-definitions) (*原始* 階段)。

1. 值包括 [已預先處理](#processing-queue)；如 *套用* 階段。

1. [篩選](#column-specific-definitions) (指派給 *已預先處理* 階段)。

1. 值會根據 [已定義的解析器](#processing-queue).
1. [篩選](#column-specific-definitions) (指派給 *已解決* 階段)。

1. 資料為 [分組和彙總](#column-specific-definitions).
1. 陣列資料可透過將其轉換為（字串型）清單來解析。

   此隱含步驟會將多值結果轉換為可以顯示的清單；此為基於多值JCR屬性的（未彙總）儲存格值的必要步驟。

1. 值再次為 [已預先處理](#processing-queue)；如 *afterApply* 階段。

1. 資料已排序。
1. 已處理的資料會傳輸到使用者端。

>[!NOTE]
>
>傳回基礎資料結果集的初始查詢是在 `reportbase` 元件。
>
>處理佇列的其他元素定義於 `columnbase` 元件。

## 報告建構和設定 {#report-construction-and-configuration}

建構和設定報表需要下列專案：

* a [定義報表元件的位置](#location-of-report-components)
* a [ `reportbase` 元件](#report-base-component)
* 一或多個， [ `columnbase` 元件](#column-base-component)
* a [頁面元件](#page-component)
* a [報告設計](#report-design)
* a [報告範本](#report-template)

### 報表元件的位置 {#location-of-report-components}

預設報告元件儲存在 `/libs/cq/reporting/components`.

不過，強烈建議您不要更新這些節點，而是在下建立自己的元件節點 `/apps/cq/reporting/components` 或者，如果更合適 `/apps/<yourProject>/reports/components`.

其中（例如）：

```
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
```

您可以在此下建立報表的根，並在其下建立報表基底元件和欄基底元件：

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

報告頁面必須使用 `sling:resourceType` 之 `/libs/cq/reporting/components/reportpage`.

在大多數情況下，自訂的頁面元件不是必要的。

## 報表基礎元件 {#report-base-component}

每種報表型別都需要衍生自下列專案的容器元件： `/libs/cq/reporting/components/reportbase`.

此元件可作為整個報表的容器，並提供下列專案的資訊：

* 此 [查詢定義](#query-definition).
* 一個 [（選擇性）對話方塊](#configuration-dialog) 以設定報表。
* 任何 [圖表](#chart-definitions) 已整合至報表。

```
N:<reportname> [cq:Component]
    P:sling:resourceSuperType = "cq/reporting/components/reportbase"
    N:charting
    N:dialog [cq:Dialog]
    N:queryBuilder
```

### 查詢定義 {#query-definition}

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

   可用來將結果集限制在具有特定值的特定屬性的節點內。 如果指定了多個限制，則節點必須滿足所有限制（AND作業）。

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

   將傳回所有 `textimage` 上次由修改的元件 `admin` 使用者。

* `nodeTypes`

   用於將結果集限製為指定的節點型別。 可以指定多個節點型別。

* `mandatoryProperties`

   可用於將結果集限製為具有 *全部* 指定的屬性。 未考慮屬性的值。

所有專案都是選用專案，可視需要加以合併，但您至少必須定義其中一個。

### 圖表定義 {#chart-definitions}

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

   保留使用中圖表的定義。

   * `active`

      由於可以定義多個設定，因此您可以使用此項來定義哪些設定目前處於活動狀態。 這些是由節點陣列所定義(這些節點沒有強制性的命名慣例，但標準報告通常會使用 `0`， `1`.. `x`)，則每個屬性都如下所示：

      * `id`

         使用中圖表的識別。 這必須符合其中一個圖表的ID `definitions`.

* `definitions`

   定義報表可能可用的圖表型別。 此 `definitions` 要使用的將由 `active` 設定。

   使用節點陣列（通常也命名為）來指定定義 `0`， `1`.. `x`)，則每個檔案都有以下屬性：

   * `id`

      圖表識別。

   * `type`

      可用的圖表型別。 從下列專案選取：

      * `pie`
圓形圖。 僅從目前的資料產生。

      * `lineseries`
一系列線（代表實際快照的連線點）。 僅從歷史資料產生。
   * 檢視表型別而定，可使用其他屬性：

      * 適用於圖表型別 `pie`：

         * `maxRadius` ( `Double/Long`)

            圓餅圖允許的最大半徑，因此圖表允許的大小上限（沒有圖例）。 忽略條件 `fixedRadius` 已定義。

         * `minRadius` ( `Double/Long`)

            圓餅圖允許的最小半徑。 忽略條件 `fixedRadius` 已定義。

         * `fixedRadius` ( `Double/Long`)定義圓形圖的固定半徑。
      * 適用於圖表型別 [`lineseries`](/help/sites-administering/reporting.md#display-limits)：

         * `totals` ( `Boolean`)

            如果額外的一行顯示 **總計** 應該會顯示。
默认: `false`

         * `series` ( `Long`)

            要顯示的行數/系列數。
預設： `9` （這也是允許的最大值）

         * `hoverLimit` ( `Long`)

            要顯示快顯視窗的彙總快照數上限（在每個水平線上顯示的點，代表不同的值），亦即當使用者將滑鼠移到圖表圖例中的不同值或對應標籤上時。

            預設： `35` （也就是說，如果超過35個不同的值適用於目前的圖表設定，則完全不會顯示快顯視窗）。

            此外還有10個同時顯示的快顯視窗限制（將滑鼠移到圖例文字上方時，可以顯示多個快顯視窗）。



### 設定對話方塊 {#configuration-dialog}

每個報告都可以有一個設定對話方塊，允許使用者為報告指定各種引數。 此對話方塊可透過 **編輯** 按鈕。

此對話方塊為標準CQ [對話方塊](/help/sites-developing/components-basics.md#dialogs) 且可依此設定(請參閱 [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog) 以取得詳細資訊)。

範例對話方塊如下所示：

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

提供了數個預先設定的元件；可在對話方塊中使用 `xtype` 屬性值為的屬性 `cqinclude`：

* **`title`**

   `/libs/cq/reporting/components/commons/title`

   用於定義報表標題的文字欄位。

* **`description`**

   `/libs/cq/reporting/components/commons/description`

   用於定義報表說明的文字區域。

* **`processing`**

   `/libs/cq/reporting/components/commons/processing`

   報表處理模式的選擇器（手動/自動載入資料）。

* **`scheduling`**

   `/libs/cq/reporting/components/commons/scheduling`

   用於排程歷史圖表快照的選擇器。

>[!NOTE]
>
>參照的元件必須包含在內，使用 `.infinity.json` 尾碼（請參閱上述範例）。

### 根路径 {#root-path}

此外，可以為報表定義根路徑：

* **`rootPath`**

   這會將報表限制在存放庫的特定區段（樹狀結構或子樹狀結構），建議用於效能最佳化。 根路徑由 `rootPath` 的屬性 `report` 每個報告頁面的節點（在建立頁面時取自範本）。

   可透過以下方式指定：

   * 此 [報告範本](#report-template) （作為固定值或作為設定對話方塊的預設值）。
   * 使用者（使用此引數）

## 欄基本元件 {#column-base-component}

每個欄型別都需要衍生自的元件 `/libs/cq/reporting/components/columnbase`.

欄元件會定義下列專案的組合：

* 此 [欄特定查詢](#column-specific-query) 設定。
* 此 [解析器與預先處理](#resolvers-and-preprocessing).
* 此 [欄特定定義](#column-specific-definitions) (例如篩選和彙總； `definitions` 子節點)。
* [欄預設值](#column-default-values).
* 此 [使用者端篩選器](#client-filter) 從伺服器傳回的資料中擷取要顯示的資訊。
* 此外，欄元件必須提供適當的例項 `cq:editConfig`. 以定義 [事件與動作](#events-and-actions) 必填。
* 的設定 [泛型欄](#generic-columns).

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

另請參閱 [定義您的新報告](#defining-your-new-report).

### 欄特定查詢 {#column-specific-query}

這會定義特定的資料擷取(從 [報告資料結果集](#the-query-and-data-retrieval))以便在個別欄中使用。

```xml
N:definitions
    N:queryBuilder
        P:property [String|String[]]
        P:subPath
        P:secondaryProperty [String|String[]]
        P:secondarySubPath
```

* `property`

   定義用於計算實際儲存格值的屬性。

   如果屬性定義為字串[] 系統會依序掃描多個屬性以找出實際值。

   例如，在下列情況下：

   `property = [ "jcr:lastModified", "jcr:created" ]`

   對應的值擷取器（在這裡是控制對象）將：

   * 檢查是否有可用的jcr：lastModified屬性，如果有的話，請使用它。
   * 如果沒有可用的jcr：lastModified屬性，將改用jcr：created的內容。

* `subPath`

   如果結果不在查詢傳回的節點上， `subPath` 會定義屬性的實際位置。

* `secondaryProperty`

   定義另一個屬性，該屬性也必須用於計算實際儲存格值；這僅用於特定欄型別（diff和sortable）。

   例如，若是「工作流程例項報表」，則指定的屬性會用於儲存開始與結束時間之間時間差的實際值（以毫秒為單位）。

* `secondarySubPath`

   與subPath類似，當 `secondaryProperty` 已使用。

在大多數情況下，僅 `property` 將會使用。

### 使用者端篩選器 {#client-filter}

使用者端篩選器會從伺服器傳回的資料中擷取要顯示的資訊。

>[!NOTE]
>
>套用整個伺服器端處理之後，會在使用者端執行此篩選。

```xml
N:definitions
    N:data
        P:clientFilter [String]
```

`clientFilter` 定義為JavaScript函式，該函式：

* 作為輸入，會接收一個引數；從伺服器傳回的資料（如此已完成預先處理）
* 作為輸出，傳回篩選（已處理）值；從輸入資訊擷取或衍生的資料

下列範例會從元件路徑中擷取對應的頁面路徑：

```
function(v) {
    var sepPos = v.lastIndexOf('/jcr:content');
    if (sepPos < 0) {
        return v;
    }
    return v.substring(sepPos + '/jcr:content'.length, v.length);
}
```

### 解析器與預先處理 {#resolvers-and-preprocessing}

此 [處理佇列](#processing-queue) 定義各種解析器並設定預先處理：

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

   定義要使用的解析器。 下列解析器可供使用：

   * `const`

      將值對應至其他值；例如，這可用來解析常數，例如 `en` 至其同等值 `English`.

   * `default`

      預設解析器。 這是虛擬解析程式，實際上不會解析任何內容。

   * `page`

      將路徑值解析為適當頁面的路徑；更準確地說，解析為對應的 `jcr:content` 節點。 例如， `/content/.../page/jcr:content/par/xyz` 解析為 `/content/.../page/jcr:content`.

   * `path`

      解析路徑值，方法是選擇性附加子路徑並從節點的屬性中取得實際值（如所定義） `resolverConfig`)。 例如， `path` 之 `/content/.../page/jcr:content` 可解析為的內容 `jcr:title` 屬性，這表示頁面路徑會解析為頁面標題。

   * `pathextension`

      藉由在路徑前面加上並從解析路徑處節點的屬性中取得實際值來解析值。 例如，值 `de` 前面可能會附加一個路徑，例如 `/libs/wcm/core/resources/languages`，從屬性取得值 `language`，解析國家/地區代碼 `de` 至語言說明 `German`.

* `resolverConfig`

   提供解析程式的定義；可用的選項取決於 `resolver` 已選取：

   * `const`

      使用屬性來指定要解析的常數。 屬性的名稱會定義要解析的常數；屬性的值會定義解析的值。

      例如，屬性具有 **名稱**= `1` 和 **值** `=One` 將解析1到1。

   * `default`

      沒有可用的設定。

   * `page`

      * `propertyName` （選擇性）

         定義用於解析值的屬性名稱。 若未指定，預設值為 *jcr：title* （頁面標題）會使用；用於 `page` 解析程式，這表示先將路徑解析為頁面路徑，然後進一步解析為頁面標題。
   * `path`

      * `propertyName` （選擇性）

         指定用於解析值的屬性名稱。 若未指定，預設值為 `jcr:title` 已使用。

      * `subPath` （選擇性）

         此屬性可用於指定要在解析值之前附加至路徑的字尾。
   * `pathextension`

      * `path` （必要）

         定義要在前面附加的路徑。

      * `propertyName` （必要）

         定義實際值所在解析路徑上的屬性。

      * `i18n` （選用；輸入布林值）

         決定是否應將解析的值設為 *國際化* (即使用 [CQ5的國際化服務](/help/sites-administering/tc-manage.md))。



* `preprocessing`

   前置處理是選擇性的，可以繫結至處理階段（單獨繫結） *套用* 或 *applyAfter*：

   * `apply`

      初始前置處理階段([處理佇列表示中的步驟3](#processing-queue))。

   * `applyAfter`

      在預先處理之後套用([處理佇列表示中的步驟9](#processing-queue))。

#### 解析器 {#resolvers}

解析器可用來擷取所需的資訊。 各種解析器的範例包括：

**常數**

以下內容將解析下列專案的常數值： `VersionCreated` 至字串 `New version created`.

请参阅 `/libs/cq/reporting/components/auditreport/typecol/definitions/data`.

```xml
N:data
    P:resolver=const
    N:resolverConfig
        P:VersionCreated="New version created"
```

**页面**

將路徑值解析為對應頁面之jcr：content （子項）節點上的jcr：description屬性。

请参阅 `/libs/cq/reporting/components/compreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=page
    N:resolverConfig
        P:propertyName="jcr:description"
```

**路径**

以下解析路徑 `/content/.../page` 至的內容 `jcr:title` 屬性，這表示頁面路徑會解析為頁面標題。

请参阅 `/libs/cq/reporting/components/auditreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=path
    N:resolverConfig
        P:propertyName="jcr:title"
        P:subPath="/jcr:content"
```

**路徑副檔名**

下列內容會在值前加上 `de` 以路徑副檔名 `/libs/wcm/core/resources/languages`，則會從屬性中取得值 `language`，解析國家/地區代碼 `de` 至語言說明 `German`.

请参阅 `/libs/cq/reporting/components/userreport/languagecol/definitions/data`.

```xml
N:data
    P:resolver=pathextension
    N:resolverConfig
        P:path="/libs/wcm/core/resources/languages"
        P:propertyName="language"
```

#### 正在預先處理 {#preprocessing}

此 `preprocessing` 定義可套用至以下任一專案：

* 原始值：

   原始值的預先處理定義指定於 `apply` 和/或 `applyAfter` 直接。

* 彙總狀態的值：

   如有必要，可以為每個彙總提供個別的定義。

   若要指定彙總值的明確預先處理，預先處理定義必須位於個別的 `aggregated` 子節點( `apply/aggregated`， `applyAfter/aggregated`)。 如果需要明確預先處理不同的彙總，則預先處理定義會位於具有個別彙總名稱的子節點上(例如 `apply/aggregated/min/max` 或其他彙總)。

您可以指定下列任一項要在預先處理期間使用：

* [尋找和取代圖樣](#preprocessing-find-and-replace-patterns)
找到時，指定的模式（定義為規則運算式）會被其他模式取代；例如，這可用於擷取原始模式的子字串。

* [資料型別格式化程式](#preprocessing-data-type-formatters)

   將數值轉換為相對字串；例如，「代表1小時時間差的值」會解析為字串，例如 `1:24PM (1 hour ago)`.

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

#### 預先處理 — 尋找和取代模式 {#preprocessing-find-and-replace-patterns}

針對預先處理，您可以指定 `pattern` (定義為 [規則運算式](https://en.wikipedia.org/wiki/Regular_expression) 或規則運算式)，然後由 `replace` 模式：

* `pattern`

   用來尋找子字串的規則運算式。

* `replace`

   將用來取代原始字串的字串或字串表示法。 這通常代表規則運算式所在字串的子字串 `pattern`.

取代範例可劃分為：

* 針對節點 `definitions/data/preprocessing/apply` 具有以下兩個屬性：

   * `pattern`: `(.*)(/jcr:content)(/|$)(.*)`
   * `replace`: `$1`

* 字串的到達方式：

   * `/content/geometrixx/en/services/jcr:content/par/text`

* 將分成四個區段：

   * `$1` - `(.*)` - `/content/geometrixx/en/services`
   * `$2` - `(/jcr:content)` - `/jcr:content`
   * `$3` - `(/|$)` - `/`
   * `$4` - `(.*)` - `par/text`

* 並取代為所代表的字串 `$1`：

   * `/content/geometrixx/en/services`

#### 預先處理 — 資料型別格式化程式 {#preprocessing-data-type-formatters}

這些格式化程式會將數值轉換為相對字串。

例如，這可用於時間欄，其允許 `min`， `avg` 和 `max` 彙總。 作為 `min`/ `avg`/ `max` 彙總會顯示為 *時間差異* (例如： `10 days ago`)，則需使用資料格式器。 針對此， `datedelta` 格式化程式已套用至 `min`/ `avg`/ `max` 彙總值。 若為 `count` 彙總也可供使用，因此這不需要格式化程式，原始值也不需要。

目前可用的資料型別格式化程式包括：

* `format`

   資料型別格式化程式：

   * `duration`

      期間是兩個已定義日期之間的時間範圍。 例如，工作流程動作的開始和結束時間為1小時，從2011年2月13日11:23時開始，1小時後於2011年2月13日12:23時結束。

      它將數值（解譯為毫秒）轉換為持續時間字串；例如， `30000` 格式為* `30s`.*

   * `datedelta`

      Datadelta是過去某個日期到「現在」之間的時間範圍（因此，如果在之後的某個時間點檢視報表，會有不同的結果）。

      它會將數值（解譯為以天為單位的時間差異）轉換為相對日期字串。 例如，1的格式為1天前。

以下範例定義 `datedelta` 格式設定 `min` 和 `max` 彙總：

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

### 欄特定定義 {#column-specific-definitions}

欄特定定義會定義該欄可用的篩選器和彙總。

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

   下列專案可作為標準選項使用：

   * `string`
   * `number`
   * `int`
   * `date`
   * `diff`
   * `timeslot`

      用於擷取彙總所需的日期部分（例如，依年分組，以取得每年彙總的資料）。

   * `sortable`

      用於使用不同值（如從不同屬性取得的）進行排序和顯示的值。
   此外。 以上任何專案皆可定義為多個值，例如， `string[]` 會定義字串陣列。

   值擷取器由欄型別選擇。 如果值擷取器可用於欄型別，則會使用此擷取器。 否則，會使用預設值擷取器。

   型別可以（選擇性）接受引數。 例如， `timeslot:year` 從日期欄位中擷取年份。 型別及其引數：

   * `timeslot`  — 值會與的對應常數比較， `java.utils.Calendar`.

      * `timeslot:year` - `Calendar.YEAR`
      * `timeslot:month-of-year` - `Calendar.MONTH`
      * `timeslot:week-of-year` - `Calendar.WEEK_OF_YEAR`
      * `timeslot:day-of-month` - `Calendar.DAY_OF_MONTH`
      * `timeslot:day-of-week` - `Calendar.DAY_OF_WEEK`
      * `timeslot:day-of-year` - `Calendar.DAY_OF_YEAR`
      * `timeslot:hour-of-day` - `Calendar.HOUR_OF_DAY`
      * `timeslot:minute-of-hour` - `Calendar.MINUTE`


* `groupable`

   定義報表是否可依此欄分組。

* `filters`

   篩選器定義。

   * `filterType`

      可用的篩選器包括：

      * `string`

         字串型篩選器。
   * `id`

      篩選器識別碼。

   * `phase`

      可用階段：

      * `raw`

         篩選器已套用至原始資料。

      * `preprocessed`

         篩選條件套用於已預先處理的資料。

      * `resolved`

         篩選器已套用到已解析的資料。


* `aggregates`

   彙總定義。

   * `text`

      彙總的文字名稱。 若 `text` 未指定，則會採用彙總的預設說明；例如， `minimum` 將用於 `min` 彙總。

   * `type`

      彙總型別。 可用的彙總包括：

      * `count`

         計算列數。

      * `count-nonempty`

         計算非空白列的數量。

      * `min`

         提供最小值。

      * `max`

         提供最大值。

      * `average`

         提供平均值。

      * `sum`

         提供所有值的總和。

      * `median`

         提供中間值。

      * `percentile95`

         採用所有值的第95個百分位數。

### 欄預設值 {#column-default-values}

這可用來定義欄的預設值：

```xml
N:defaults
    P:aggregate
```

* `aggregate`

   有效 `aggregate` 值與的相同 `type` 在 `aggregates` (請參閱 [欄特定定義（定義 — 篩選器/彙總）](#column-specific-definitions) )。

### 事件與動作 {#events-and-actions}

編輯設定會定義監聽器偵測的必要事件，以及這些事件發生後要套用的動作。 請參閱 [元件開發簡介](/help/sites-developing/components.md) 以取得背景資訊。

必須定義下列值，以確保滿足所有必要的動作：

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

### 一般資料行 {#generic-columns}

Generic欄是擴充功能，其中（大部分）欄定義儲存在欄節點的例項上（而非元件節點）。

它們使用您自訂的（標準）對話方塊來代表個別類屬元件。 此對話方塊可讓報告使用者定義報告頁面上一般欄的欄屬性（使用功能表選項） **欄屬性……**)。

範例為 **通用** 的欄 **使用者報告**；請參閱 `/libs/cq/reporting/components/userreport/genericcol`.

若要將欄設為類屬，請執行下列動作：

* 設定 `type` 欄的屬性 `definition` 節點至 `generic`.

   请参阅 `/libs/cq/reporting/components/userreport/genericcol/definitions`

* 在欄的底下指定（標準）對話方塊定義 `definition` 節點。

   请参阅 `/libs/cq/reporting/components/userreport/genericcol/definitions/dialog`

   * 對話方塊的欄位必須參照與對應元件屬性（包括其路徑）相同的名稱。

      例如，如果要使類屬欄的型別可透過對話方塊來設定，請使用名稱為的欄位 `./definitions/type`.

   * 使用UI/對話方塊定義的屬性優先於 `columnbase` 元件。

* 定義「編輯組態」。

   请参阅 `/libs/cq/reporting/components/userreport/genericcol/cq:editConfig`

* 使用標準AEM方法定義（其他）欄屬性。

   請注意，對於元件和欄實體上定義的屬性，優先使用欄實體上的值。

   一般資料行可用的屬性包括：

   * `jcr:title`  — 欄名稱
   * `definitions/aggregates`  — 彙總
   * `definitions/filters`  — 篩選器
   * `definitions/type` — 欄的型別（這必須在對話方塊中定義，使用選取器/下拉式方塊或隱藏欄位）
   * `definitions/data/resolver` 和 `definitions/data/resolverConfig` (但不是 `definitions/data/preprocessing` 或 `.../clientFilter`) — 解析程式和設定
   * `definitions/queryBuilder`  — 查詢產生器設定
   * `defaults/aggregate`  — 預設彙總

   若是上的類屬資料行有新例項 **使用者報告** 使用對話方塊定義的屬性會儲存在：

   `/etc/reports/userreport/jcr:content/report/columns/genericcol/settings/generic`

## 報表設計 {#report-design}

設計會定義哪些欄型別可用於建立報告。 它也會定義要新增欄的段落系統。

強烈建議您為每個報告建立個別設計。 這可確保完全的彈性。 另請參閱 [定義您的新報告](#defining-your-new-report).

預設報告元件儲存在 `/etc/designs/reports`.

報表的位置取決於元件所在的位置：

* `/etc/designs/reports/<yourReport>` 適用於報表位於下方的情況 `/apps/cq/reporting`

* `/etc/designs/<yourProject>/reports/<*yourReport*>` 對於使用 `/apps/<yourProject>/reports` 圖樣

必要的設計屬性註冊於 `jcr:content/reportpage/report/columns` (例如， `/etc/designs/reports/<reportName>/jcr:content/reportpage/report/columns`)：

* `components`

   報表上允許的任何元件和/或元件群組。

* `sling:resourceType`

   具有值的屬性 `cq/reporting/components/repparsys`.

以下是範例設計程式碼片段（取自元件報表的設計）：

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

不需要為個別資料行指定設計。 可用欄可在設計模式中定義。

>[!NOTE]
>
>建議您不要對標準報表設計進行任何變更。 這是為了確保升級或安裝Hotfix時不會遺失任何變更。
>
>如果您想要自訂標準報表，請複製報表及其設計。

>[!NOTE]
>
>建立報表時，可自動建立預設欄。 這些是在範本中指定的。

## 報告範本 {#report-template}

每個報表型別都必須提供範本。 這些是標準 [CQ範本](/help/sites-developing/templates.md) 且可依此設定。

範本必須：

* 設定 `sling:resourceType` 至 `cq/reporting/components/reportpage`

* 指示要使用的設計
* 建立 `report` 參考容器的子節點( `reportbase`)元件，使用 `sling:resourceType` 屬性

範本片段範例（取自元件報告範本）為：

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

範本片段範例顯示根路徑（取自使用者報表範本）的定義，如下所示：

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

預設報表範本儲存在 `/libs/cq/reporting/templates`.

不過，強烈建議您不要更新這些節點，而是在下建立自己的元件節點 `/apps/cq/reporting/templates` 或者，如果更合適 `/apps/<yourProject>/reports/templates`.

其中，作為範例(另請參閱 [報表元件的位置](#location-of-report-components))：

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
```

您可以在此下建立範本的根目錄：

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
                N:<reportname> [sling:Folder]
```

## 建立您自己的報表 — 範例 {#creating-your-own-report-an-example}

### 定義您的新報告 {#defining-your-new-report}

若要定義新報告，您必須建立並設定：

1. 報表元件的根目錄。
1. 報表基礎元件。
1. 一或多個欄基本元件。
1. 報表設計。
1. 報表範本的根目錄。
1. 報表範本。

為了說明這些步驟，以下範例會定義一個報表，其中列出存放庫內的所有OSGi設定；即 `sling:OsgiConfig` 節點。

>[!NOTE]
>
>複製現有報表，然後自訂新版本，是替代方法。

1. 為您的新報告建立根節點。

   例如，在 `/apps/cq/reporting/components/osgireport`.

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:components [sling:Folder]
               N:osgireport [sling:Folder]
   ```

1. 定義您的報表基礎。 例如 `osgireport[cq:Component]` 在 `/apps/cq/reporting/components/osgireport`.

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

   這會定義報表基礎元件，該元件：

   * 搜尋型別為的所有節點 `sling:OsgiConfig`
   * 顯示兩者 `pie` 和 `lineseries` 圖表
   * 提供對話方塊，供使用者設定報表

1. 定義您的第一欄（欄基底）元件。 例如 `bundlecol[cq:Component]` 在 `/apps/cq/reporting/components/osgireport`.

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

   這會定義一個資料行基礎元件，該元件：

   * 會搜尋並傳回從伺服器收到的值；在此案例中是屬性 `jcr:path` 代表每 `sling:OsgiConfig` 節點
   * 提供 `count` 彙總
   * 不可分組
   * 具有標題 `Bundle` （表格中的欄標題）
   * 在sidekick群組中 `OSGi Report`
   * 重新整理指定的事件

   >[!NOTE]
   >
   >在此範例中，沒有定義 `N:data` 和 `P:clientFilter`. 這是因為從伺服器收到的值是以1:1為傳回基準，這是預設行為。
   >
   >這與定義相同：
   >
   >
   ```
   >N:data [nt:unstructured]
   >   P:clientFilter [String] = "function(v) { return v; }"
   >```
   >
   >其中函式只會傳回收到的值。

1. 定義您的報表設計。 例如 `osgireport[cq:Page]` 在 `/etc/designs/reports`.

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

1. 為您的新報告範本建立根節點。

   例如，在 `/apps/cq/reporting/templates/osgireport`.

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:templates [sling:Folder]
               N:osgireport [cq:Template]
   ```

1. 定義您的報表範本。 例如 `osgireport[cq:Template]` 在 `/apps/cq/reporting/templates`.

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

   這會定義符合以下條件的範本：

   * 定義 `allowedPaths` 用於產生的報表 — 在上述案例中，位於 `/etc/reports`
   * 提供範本的標題和說明
   * 提供用於範本清單中的縮圖影像（上面未列出此節點的完整定義 — 最簡單的做法是複製現有報表中的thumbnail.png例項）。

### 建立新報告的例項 {#creating-an-instance-of-your-new-report}

您現在可以建立新報告的例項：

1. 開啟 **工具** 主控台。

1. 選取 **報表** 在左側窗格中。
1. 則 **新增……** （從工具列）。 定義 **標題** 和 **名稱**，選取您的新報表型別( **OSGi報表範本**)，然後按一下「 」 **建立**.
1. 您的新報告執行個體會出現在清單中。 連按兩下以開啟。
1. 拖曳元件(例如， **組合** 在 **OSGi報表** 群組)，以建立第一欄和 [啟動報表定義](/help/sites-administering/reporting.md#the-basics-of-report-customization).

   >[!NOTE]
   >
   >由於此範例沒有任何可分組的欄，因此圖表將不可用。 若要檢視圖表，請設定 `groupable` 至 `true`：
   >
   >
   ```
   >N:osgireport [sling:Folder]
   > N:bundlecol [cq:Component]
   > N:definitions [nt:unstructured]
   > P:groupable [Boolean] = true
   >```

## 設定Report Framework服務 {#configuring-the-report-framework-services}

本節說明實作報表架構之OSGi服務的進階設定選項。

這些可透過Web主控台的「設定」功能表檢視(例如 `http://localhost:4502/system/console/configMgr`)。 使用AEM時，有數種方法可管理此類服務的組態設定；請參閱 [設定OSGi](/help/sites-deploying/configuring-osgi.md) 以取得詳細資訊和建議作法。

### 基本服務（Day CQ報告設定） {#basic-service-day-cq-reporting-configuration}

* **時區** 會定義為其建立歷史資料的時區。 這是為了確保歷史圖表可顯示全球每位使用者的相同資料。
* **地區設定** 定義要搭配使用的地區設定 **時區** 以取得歷史資料。 地區設定是用來決定某些地區設定的特定行事曆設定（例如，一週的第一天是星期日還是星期一）。

* **快照路徑** 定義儲存歷史圖表快照的根路徑。
* **報表路徑** 定義報表所在的路徑。 這由快照服務用來決定要實際製作快照的報表。
* **每日快照** 定義每天拍攝快照的時間。 指定的小時是伺服器的本機時區。
* **每小時快照** 會定義每小時擷取快照時每小時的分鐘數。
* **列（最大值）** 定義每個快照所儲存的最大列數。 此值應合理選擇；如果太高，這將影響存放庫的大小；如果太低，資料可能會因為歷史資料的處理方式而不準確。
* **偽造資料**，如果已啟用，則可以使用以下專案建立虛假歷史資料： `fakedata` 選擇器；如果停用，則使用 `fakedata` 選取器會擲回例外狀況。

   由於資料是假的，因此它必須 *僅限* 用於測試和偵錯。

   使用 `fakedata` 選擇器將會以隱含的方式完成報表，因此所有現有資料都會遺失；資料可以手動還原，但此程式可能相當耗時。

* **快照使用者** 定義可用來建立快照的選用使用者。

   基本上，系統會為完成報表的使用者建立快照。 在某些情況下（例如在發佈系統上，由於尚未復寫此使用者的帳戶，因此該使用者並不存在），您可能會想要指定替代使用的後援使用者。

   此外，指定使用者可能會帶來安全性風險。

* **強制快照使用者**，如果已啟用，則會使用下列專案中指定的使用者來建立所有快照： *快照使用者*. 如果處理不當，可能會帶來嚴重的安全性影響。

### 快取設定（Day CQ報告快取） {#cache-settings-day-cq-reporting-cache}

* **啟用** 可讓您啟用或停用報表資料的快取。 在數個請求期間，啟用報表快取會將報表資料保留在記憶體中。 這可能會提高效能，但會導致更高的記憶體耗用量，並且在極端情況下可能會導致記憶體不足。
* **TTL** 定義快取報告資料的時間（以秒為單位）。 較高的數字會提升效能，但如果資料在時段內變更，也可能傳回不正確的資料。
* **最大專案數** 會定義一次要快取的報告數量上限。

>[!NOTE]
>
>每個使用者和語言的報表資料可能不同。 因此，會根據報表、使用者和語言，快取報表資料。 這表示 **最大專案數** 值 `2` 實際上快取下列任一專案的資料：
>
>* 一個報表，供具有不同語言設定的兩個使用者使用
>* 一個使用者和兩個報告
>

