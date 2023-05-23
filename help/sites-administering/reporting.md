---
title: 报告
seo-title: Reporting
description: 瞭解如何在AEM中使用報告。
seo-description: Learn how to work with Reporting in AEM.
uuid: eee4befd-5fa9-4ebc-8eea-56e1534a6b9b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 7e2b30a3-75ff-4735-8038-5c5391ac36f3
docset: aem65
exl-id: 2a0bf59d-8829-4142-9cb4-dcef90f53ae9
source-git-commit: 429f3ee859477fb38938fd6b9706c8006623eb03
workflow-type: tm+mt
source-wordcount: '2806'
ht-degree: 4%

---

# 报告 {#reporting}

為協助您監控及分析執行個體的狀態，AEM提供一系列預設報表，您可依個別需求加以設定：

* [组件报告](#component-report)
* [磁盘使用情况](#disk-usage)
* [健康情況檢查](#health-check)
* [页面活动报告](#page-activity-report)
* [用户生成的内容报告](#user-generated-content-report)
* [用户报告](#user-report)
* [工作流实例报告](#workflow-instance-report)
* [工作流程報告](#workflow-report)

>[!NOTE]
>
>這些報表僅適用於Classic UI。 如需新式UI中的系統監控和報告，請參閱 [操作控制面板。](/help/sites-administering/operations-dashboard.md)

所有報表都可從以下網址存取： **工具** 主控台。 選取 **報表** 然後，在左側窗格中連按兩下右側窗格中的必要報表，以開啟報表以供檢視和/或設定。

報表的新例項也可從以下網址建立： **工具** 主控台。 選取 **報表** 在左側窗格中，然後 **新增……** （從工具列）。 定義 **標題** 和 **名稱**，選取您需要的報表型別，然後按一下 **建立**. 您的新報告執行個體會出現在清單中。 連按兩下以開啟，然後從Sidekick拖曳元件以建立第一欄並開始報表定義。

>[!NOTE]
>
>除了現成可用的標準AEM報表之外，您還可以 [開發您自己的（全新）報告](/help/sites-developing/dev-reports.md).

## 報表自訂的基本概念 {#the-basics-of-report-customization}

有多種可用的報告格式。 下列報表都使用可自訂的欄，詳見以下章節：

* [组件报告](#component-report)
* [页面活动报告](#page-activity-report)
* [用户生成的内容报告](#user-generated-content-report)
* [用户报告](#user-report)
* [工作流实例报告](#workflow-instance-report)

>[!NOTE]
>
>以下各報表具有各自的格式和自訂：
>
>
>* [健康情況檢查](#health-check) 使用選取欄位來指定您要報告的資料。
>* [磁碟使用量](#disk-usage) 會使用連結來向下鑽研存放庫結構。
>* [工作流程報告](/help/sites-administering/reporting.md#workflow-report) 提供執行個體上執行的工作流程概觀。
>
>因此，下列欄設定程式並不適用。 如需詳細資訊，請參閱個別報表的說明。

### 選取和定位資料欄 {#selecting-and-positioning-the-data-columns}

欄可以在任何報表中新增、重新放置或移除（無論是標準報表還是自訂報表）。

此 **元件** Sidekick的索引標籤（可在報告頁面上取得）列出了可選取為欄的所有資料類別。

若要變更資料選取範圍：

* 若要新增欄，請從sidekick拖曳所需元件，然後放置於您想要的位置

   * 綠色勾號表示位置何時有效，而一對箭頭則表示位置將放置的確切位置
   * 位置無效時，紅色的no-go符號會指示出來

* 若要移動欄，請按住標題並拖曳至新位置
* 若要移除欄，請按住欄標題，然後向上拖曳至報表標題區域（紅色減號表示位置無效）；放開滑鼠按鈕，「刪除元件」對話方塊會要求確認您確實要刪除欄。

### 欄下拉式功能表 {#column-drop-down-menu}

報表中的每一欄都有一個下拉式功能表。 當滑鼠游標移到欄標題儲存格上時，這會變得可見。

箭頭標頭會出現在標題儲存格的最右側(請勿與標題文字右側的箭頭標頭混淆，後者指出 [目前的排序機制](#sorting-the-data))。

![reportcolumn排序](assets/reportcolumnsort.png)

功能表上的可用選項將取決於欄的設定（如專案開發期間所做），任何無效選項都將呈現灰色。

### 排序資料 {#sorting-the-data}

資料可以根據特定欄排序，方法如下：

* 按一下適當的欄標題；排序會在遞增和遞減之間切換，由標題文字旁邊的箭頭標頭指示
* 使用 [欄的下拉式功能表](#column-drop-down-menu) 以明確選取 **升序排序** 或 **降序排序**；同樣地，這將在標題文字旁邊以箭頭表示

### 群組與目前資料圖表 {#groups-and-the-current-data-chart}

您可以在適當的欄上選取 **依此欄分組** 從 [欄的下拉式功能表](#column-drop-down-menu). 這將會根據該欄中每個不同的值來分組資料。 您可以選取多個要分組的欄。 當欄中的資料不適當時（例如，每個專案都不同且獨特，因此無法形成任何群組，例如使用者報表的使用者ID欄），選項會變灰。

將至少一個欄分組後，圓形圖會顯示 **目前資料** 將會根據此分組產生。 如果有多欄分組，圖表上也會指出這點。

![報告使用者](assets/reportuser.png)

將游標移至圓形圖上會顯示適當區段的彙總值。 這會使用目前為欄定義的彙總；例如count、minimum、average等。

### 篩選和彙總 {#filters-and-aggregates}

您也可以在適當的欄上設定 **篩選器設定** 和/或 **彙總** 從 [欄的下拉式功能表](#column-drop-down-menu).

#### 过滤器 {#filters}

篩選設定可讓您指定要顯示的專案條件。 可用的運運算元包括：

* `contains`
* `equals`

![reportfilter](assets/reportfilter.png)

若要設定篩選：

1. 從下拉式清單中選取您想要的運運算元。
1. 輸入要篩選的文字。
1. 按一下 **套用**.

若要停用篩選器：

1. 移除篩選文字。
1. 按一下 **套用**.

#### 彙總 {#aggregates}

您也可以選取聚總方法（視選取的欄位而定）：

![reportaggregate](assets/reportaggregate.png)

### 列属性 {#column-properties}

此選項僅適用於 [通用欄](#generic-column) 已用於 [使用者報告](#user-report).

### 历史数据 {#historic-data}

您可以在下方看到資料隨時間變化的圖表 **歷史資料**. 這是從定期拍攝的快照衍生而來。

資料為：

* 收集者（如果有的話）是第一個已排序欄，否則是第一個（非群組）欄
* 依適當的欄分組

可以產生報表：

1. 設定 **分組** 在必要欄上。
1. **編輯** 定義快照建立頻率的設定；每小時或每天。
1. **完成……** 啟動快照集集合的定義。

   左上方的紅色/綠色滑桿按鈕表示快照的收集時間。

產生的圖表會顯示在右下方：

![reporttrends](assets/reporttrends.png)

開始收集資料後，您可以選取：

* **时间段**

   您可以選擇要顯示報表資料的開始和結束日期。

* **间隔**

   您可以選取月、周、日、小時來縮放與彙總報表。

   例如，如果2011年2月有每日快照可用：

   * 如果間隔設定為 `Day`，每個快照都會顯示為圖表中的單一值。
   * 如果間隔設定為 `Month`，所有2月的快照都會彙總為單一值（在圖表中顯示為單一「點」）。

選取您的需求，然後按一下 **前往** 以將其套用至報表。 若要在進一步建立快照後更新顯示，請按一下 **前往** 再來一次。

![chlimage_1-43](assets/chlimage_1-43.png)

收集快照時，您可以：

* 使用 **完成……** 以重新初始化集合。

   **完成** 「凍結」報告的結構（即指派給報告的欄，以及分組、排序、篩選的欄等） 並開始製作快照。

* 開啟 **編輯** 要選取的對話方塊 **無資料快照** 終止集合，直到需要為止。

   **編輯** 只有開啟或關閉快照的製作。 如果再次開啟快照製作，則會使用報表上次完成時的狀態，以製作進一步的快照。

>[!NOTE]
>
>快照會儲存在 `/var/reports/...` 其中路徑的其餘部分映象了報告完成時建立的各個報告的路徑和ID。
>
>
>如果您完全確定不再需要這些執行個體，可以手動清除舊快照。

>[!NOTE]
>
>預先設定的報表不會耗費大量效能，但仍建議在生產環境中使用每日快照。 如有可能，請在網站上活動較少時執行這些每日快照；這可以透過定義 `Daily snapshots (repconf.hourofday)` 的引數 **Day CQ報告設定**；請參閱 [OSGI設定](/help/sites-deploying/configuring-osgi.md) 瞭解更多有關如何設定此專案的詳細資訊。

#### 顯示限制 {#display-limits}

歷史資料報表的外觀也會因為可設定的限制（根據所選期間的結果數量）而稍微改變。

每一條水平線都稱為一個序列（對應於圖表圖例中的一個專案），每一條垂直的點欄代表彙總的快照。

![chlimage_1-44](assets/chlimage_1-44.png)

若要讓圖表在較長時間內保持乾淨，可設定限制。 對於標準報表，這些報表包括：

* 水準數列 — 預設值與系統最大值均為 `9`

* 垂直彙總快照 — 預設為 `35` （每個水準系列）

因此，當超出（適當的）限制時：

* 將不會顯示點
* 歷史資料圖表的圖例可能會顯示與目前資料圖表不同的專案數

![chlimage_1-45](assets/chlimage_1-45.png)

自訂報表也可顯示 **總計** 所有序列的值。 這會顯示為序列（圖例中的水平線和輸入專案）。

>[!NOTE]
>
>對於自訂報表，限制可以不同設定。

### 編輯（報告） {#edit-report}

此 **編輯** 按鈕開啟 **編輯報告** 對話方塊。

這是收集快照的期間所在的位置 [歷史資料](#historic-data) 已定義，但也可以定義各種其他設定：

![reportedit](assets/reportedit.png)

* **标题**

   您可以定義自己的標題。

* **描述**

   您可以定義自己的說明。

* **根路徑** (*僅對特定報告有效*)

   使用此選項可將報表限制在存放庫的（子）區段。

* **報表處理**

   * **自动刷新数据**

      每次更新報告定義時，報告資料都會重新整理。

   * **手动刷新数据**

      當資料量很大時，此選項可用來防止自動重新整理作業造成的延遲。

      選取此項表示當報表設定的任何方面已變更時，必須手動重新整理報表資料。 這也表示一旦您變更設定的任何方面，報告表格就會變成空白。

      選取此選項時 **[載入資料](#load-data)** 按鈕將會顯示(在 **編輯** （于報表中）。 **載入資料** 將會載入資料，並重新整理顯示的報表資料。

* **快照**
您可以定義建立快照的頻率；每天、每小時或根本不建立快照。

### 加载数据 {#load-data}

此 **載入資料** 按鈕只有在 **手動重新整理資料** 已從中選取 **[編輯](#edit-report)**.

![chlimage_1-46](assets/chlimage_1-46.png)

按一下 **載入資料** 將重新載入資料並更新顯示的報表。

選取以手動重新整理資料表示：

1. 一旦您變更報告設定，報告資料表就會被清除。

   例如，如果您變更欄的排序機制，將不會顯示資料。

1. 如果您想要再次顯示報表資料，您必須按一下 **載入資料** 以重新載入資料。

### 完成（報表） {#finish-report}

當您 **完成** 報告：

* 報表定義 *截至該時間點* 將用於拍攝快照（之後，您可以繼續處理報表定義，因為它與快照分開）。
* 任何現有的快照都會被移除。
* 系統會為收集新的快照 [歷史資料](#historic-data).

您可以在此對話方塊定義或更新產生之報告的標題和說明。

![reportfinish](assets/reportfinish.png)

## 報表型別 {#report-types}

### 组件报告 {#component-report}

元件報表提供網站如何使用元件的相關資訊。

[資訊欄](#selecting-and-positioning-the-data-columns) 關於：

* 创作
* 组件路径
* 组件类型
* 上次修改时间
* 页面

舉例來說，表示您可以看到：

* 哪些元件用於何處。

   很有用，例如，在測試時。

* 特定元件的例項分佈方式。

   如果特定頁面（即「繁重頁面」）發生效能問題，這可能很有趣。

* 識別網站有頻繁/較少變更的部分。
* 瞭解頁面內容如何隨著時間發展。

所有元件都包含在產品標準和專案特定中。 使用 **編輯** 對話方塊使用者也可設定 **根路徑** 會定義報表的起點 — 報表會考慮該根下的所有元件。

![reportcomponent](assets/reportcomponent.png) ![reportcompentall](assets/reportcompentall.png)

### 磁盘使用情况 {#disk-usage}

「磁碟使用量」報表顯示儲存於存放庫中之資料的相關資訊。

報表會從存放庫的根( / )開始；按一下特定分支即可在存放庫中向下展開（目前路徑將反映在報表標題中）。

![reportdiskusage](assets/reportdiskusage.png)

### 健康情況檢查 {#health-check}

此報表會分析目前的請求記錄：

`<cq-installation-dir>/crx-quickstart/logs/request.log`
協助您識別特定期間內最貴的要求。

若要產生報表，您可以指定：

* **期間（小時）**

   要分析的時數（過去）。

   默认: `24`

* **最大. 结果**

   最大輸出行數。

   默认: `50`

* **最大. 请求**

   要分析的請求數上限。

   預設： `-1` （全部）

* **电子邮件地址**

   將結果傳送至電子郵件地址。

   可選；預設：空白

* **每日執行於(hh：mm)**

   指定每天自動執行報表的時間。

   可選；預設：空白

![reporthealth](assets/reporthealth.png)

### 页面活动报告 {#page-activity-report}

頁面活動報告會列出頁面以及在頁面執行的動作。

[資訊欄](#selecting-and-positioning-the-data-columns) 關於：

* 页面
* 用时
* 类型
* 用户

表示您可以監視：

* 最新的修改。
* 在特定頁面上工作的作者。
* 最近未修改的頁面，因此可能需要採取行動。
* 變更最多/最不頻繁的頁面。
* 最多/最不活躍的使用者。

頁面活動報告會從稽核記錄中擷取其所有資訊。 依預設，根路徑會設定為稽核記錄，位於 `/var/audit/com.day.cq.wcm.core.page`.

![報告頁面活動](assets/reportpageactivity.png)

### 用户生成的内容报告 {#user-generated-content-report}

此報表提供有關使用者產生內容的資訊；無論是評論、評等或論壇。

[資訊欄](#selecting-and-positioning-the-data-columns) 於：

* 日期
* IP 地址
* 页面
* 引用
* 类型
* 用户标识符

允許您：

* 檢視哪些頁面收到的評論最多。
* 取得特定網站訪客正在離開的所有評論的概觀，可能是相關問題。
* 透過監視何時在頁面上產生評論來判斷新內容是否引起評論。

![報告使用者內容](assets/reportusercontent.png)

### 用户报告 {#user-report}

此報表提供有關已註冊帳戶和/或設定檔的所有使用者的資訊；這可以包括組織內的作者和外部訪客。

[資訊欄](#selecting-and-positioning-the-data-columns) （可用時）關於：

* 年龄
* 国家/地区
* 域
* 电子邮件
* 姓氏
* 性别
* [通用](#generic-column)
* 名字
* 信息
* 关注
* 语言
* NTLM 哈希码
* 用户 ID

允許您：

* 檢視使用者的人口統計分佈。
* 報告您新增至設定檔的自訂欄位。

![reportusercanned](assets/reportusercanned.png)

#### 通用欄 {#generic-column}

此 **通用** 欄可在使用者報告中使用，因此您可以存取自訂資訊，通常是從 [使用者設定檔](/help/sites-administering/identity-management.md#profiles-and-user-accounts)；例如， [新增欄位至設定檔定義底下所詳述的最愛顏色](/help/sites-administering/identity-management.md#adding-fields-to-the-profile-definition).

當您執行以下任一操作時，「一般」欄對話方塊將會開啟：

* 將Generic元件從Sidekick拖曳至報表。
* 選取現有「一般」欄的「欄屬性」。

![reportusrgenericcolm](assets/reportusrgenericcolm.png)

從 **定義** 標籤，您可以定義：

* **标题**

   您自己的通用欄標題。

* **属性**

   儲存在存放庫中的屬性名稱，通常在使用者的設定檔中。

* **路径**

   屬性通常取自 `profile`.

* **类型**

   選取欄位型別 `String`， `Number`， `Integer`， `Date`.

* **預設彙總**

   如果欄在至少有一個分組欄的報告中取消分組，這會定義預設使用的彙總。 從以下專案選取所需的彙總： `Count`， `Minimum`， `Average`， `Maximum`， `Sum`.

   例如， *計數* 對於 `String` 欄位表示相異的數量 `String` 值會針對處於彙總狀態的欄顯示。

在 **延伸** 索引標籤您也可以定義可用的彙總和篩選器：

![reportusrgenericcolmextented](assets/reportusrgenericcolmextented.png)

### 工作流实例报告 {#workflow-instance-report}

這可為您提供簡短的概觀，提供關於個別工作流程例項（包括執行中及已完成的）的資訊。

[資訊欄](#selecting-and-positioning-the-data-columns) 關於：

* 已完成
* 持续时间
* 发起者
* 模型
* 有效负荷
* 启动时间
* 状态

表示您可以：

* 監視工作流程的平均持續時間；如果定期發生此情況，則可強調工作流程的問題。

![reportworkflowinstance](assets/reportworkflowintance.png)

### 工作流程報告 {#workflow-report}

這提供有關執行個體上執行的工作流程的重要統計資料。

![報告工作流程](assets/reportworkflow.png)

## 在發佈環境中使用報表 {#using-reports-in-a-publish-environment}

一旦您將報表設定為符合特定需求，您可以將其啟動以將設定傳輸到發佈環境。

>[!CAUTION]
>
>如果您需要 **歷史資料** （對於發佈環境），則 **完成** 啟動頁面之前的作者環境報告。

之後，您便可在下方存取適當的報表：

`/etc/reports`

例如，「使用者產生的內容」報告位於以下位置：

`http://localhost:4503/etc/reports/ugcreport.html`

現在會回報從發佈環境收集到的資料。

由於發佈環境中不允許報表設定， **編輯** 和 **完成** 按鈕無法使用。 不過，您可以選取 **期間** 和 **間隔** 的 **歷史資料** 報告是否正在收集快照。

![reportsucgpublish](assets/reportsucgpublish.png)

>[!CAUTION]
>
>存取這些報告可能是安全問題；因此，建議您設定Dispatcher，以便 `/etc/reports` 外部訪客無法使用。 請參閱 [安全性檢查清單](security-checklist.md) 以取得更多詳細資料。

## 執行報告所需的許可權 {#permissions-needed-for-running-reports}

所需的許可權取決於動作：

* 報表資料基本上是使用目前使用者的許可權來收集。
* 歷史資料是使用完成報表之使用者的許可權收集的。

在標準AEM安裝中，報表會預設下列許可權：

* **用户报告**

   `user administrators`  — 讀取和寫入

* **页面活动报告**

   `contributors`  — 讀取和寫入

* **组件报告**

   `contributors`  — 讀取和寫入

* **用户生成的内容报告**

   `contributors`  — 讀取和寫入

* **工作流实例报告**

   `workflow-users`  — 讀取和寫入

所有成員 `administrators` 群組擁有建立新報告的必要許可權。
