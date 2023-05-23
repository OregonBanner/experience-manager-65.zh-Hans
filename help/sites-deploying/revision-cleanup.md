---
title: 修订版清理
seo-title: Revision Cleanup
description: 瞭解如何使用AEM 6.5中的修訂清除功能。
seo-description: Learn how to use the Revision Cleanup functionality in AEM 6.5.
uuid: 321f5038-44b0-4f1e-a1aa-2d29074eed70
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: f03ebe60-88c0-4fc0-969f-949490a8e768
feature: Configuring
exl-id: e53c4c81-f62e-4b6d-929a-6649c8ced23c
source-git-commit: 24a64e603d460c659467c7679934bbdfd381aaa8
workflow-type: tm+mt
source-wordcount: '5903'
ht-degree: 0%

---

# 修订版清理{#revision-cleanup}

## 简介 {#introduction}

存放庫的每次更新都會建立新的內容修訂版本。 因此，每次更新後，存放庫的大小都會增加。 舊版修訂需要清理以釋放磁碟資源 — 這對於避免不受控制的存放庫成長非常重要。 此維護功能稱為「版本清理」。 自AEM 6.0起，即已可作為離線常式使用。

在AEM 6.3及更高版本中，引進了此功能的線上版本，稱為「線上修訂清除」。 與必須關閉AEM執行個體的離線修訂清除相比，可以在AEM執行個體上線時執行線上修訂清除。 線上修訂清除預設為開啟，建議使用此方式執行修訂清除。

**注意**： [觀看影片](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/revision-cleanup-technical-video-use.html) 瞭解如何使用「線上修訂清除」的簡介。

修訂清除處理包含三個階段： **預估**， **壓縮** 和 **clean up**. 預估會根據可能收集到的垃圾數量來決定是否執行下一個階段（壓縮）。 在壓縮階段期間，區段和tar檔案會被重寫，而遺漏任何未使用的內容。 清理階段隨後會移除舊區段，包括這些區段可能包含的任何垃圾。 離線模式通常可以回收更多空間，因為線上模式需要考慮AEM工作集，這樣才能保留額外區段不被收集。

如需有關「修訂清除」的詳細資訊，請參閱下列連結：

* [如何執行線上修訂清除](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup)
* [線上修訂清除常見問題](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions)
* [如何執行離線修訂清除](/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup)

此外，您也可以閱讀 [Oak官方檔案。](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html)

### 何時使用線上修訂清除，而非離線修訂清除？ {#when-to-use-online-revision-cleanup-as-opposed-to-offline-revision-cleanup}

**線上修訂清除是執行修訂清除的建議方式。** 離線修訂清除只能在例外情況下使用 — 例如，在移轉至新儲存格式之前，或是Adobe客戶服務要求您這麼做時。

## 如何執行線上修訂清除 {#how-to-run-online-revision-cleanup}

線上修訂清除預設會設定為每天在AEM Author和Publish執行個體上自動執行一次。 您只需在使用者活動最少的時段期間定義維護時段。 您可以依照下列方式設定「線上修訂清除」工作：

1. 在AEM主視窗中，前往 **工具 — 作業 — 控制面板 — 維護** 或將瀏覽器指向： `https://serveraddress:serverport/libs/granite/operations/content/maintenance.html`

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. 暫留在 **每日維護期間** 並按一下 **設定** 圖示。

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. 輸入所需的值（週期性、開始時間、結束時間），然後按一下 **儲存**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

或者，如果要手動執行修訂清除工作，您可以：

1. 前往 **工具 — 作業 — 控制面板 — 維護** 或直接瀏覽至 `https://serveraddress:serverport/libs/granite/operations/content/maintenance.html`
1. 按一下 **每日維護期間**.
1. 將游標暫留在 **修訂清除** 圖示。
1. 按一下 **執行**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

### 在離線修訂清除後執行線上修訂清除 {#running-online-revision-cleanup-after-offline-revision-cleanup}

修訂清除程式會依層代回收舊修訂版本。 這表示每次您執行修訂清除時，都會建立新一代並保留在磁碟上。 不過，兩種修訂清除型別之間有差異：離線修訂清除會保留一代版本，而線上修訂清除則會保留兩代版本。 因此，當您執行線上修訂清除 **晚於** 離線修訂清除會發生下列情況：

1. 在第一次線上修訂清除執行後，存放庫的大小將會加倍。 發生此狀況是因為磁碟目前保留了兩代磁碟。
1. 在後續執行期間，存放庫會在建立新世代時暫時增大，然後穩定到第一次執行後的大小，因為線上修訂清除程式會回收先前的世代。

此外，請記住，根據認可型別和數量的不同，每一代都可以和上一代相比有不同的大小，因此最終大小會因執行而異。

因此，建議將磁碟大小至少比最初估計的存放庫大小大兩到三倍。

## 完整和尾部壓縮模式  {#full-and-tail-compaction-modes}

**AEM 6.5** 介紹 **兩種新模式** 的 **壓縮** 線上版次清除處理的階段：

* 此 **完全壓縮** 模式會重寫整個存放庫中的所有區段和tar檔案。 因此，後續的清理階段可以移除存放庫中的最大垃圾量。 由於完全壓縮會影響整個存放庫，因此需要相當多的系統資源和時間才能完成。 完全壓縮對應至AEM 6.3中的壓縮階段。
* 此 **尾部壓縮** 模式只會重寫存放庫中最近的區段和tar檔案。 最近的區段和tar檔案是自上次執行完整或尾部壓縮以來新增的區段。 因此，後續的清理階段只能移除存放庫最近部分中所包含的垃圾。 由於尾部壓縮只會影響存放庫的一部分，因此完成所需的系統資源和時間比完全壓縮要少得多。

這些壓真實模式構成效率和資源消耗之間的權衡：尾端壓實效率較低，對正常系統作業的影響也較小。 相較之下，完全壓縮的效果較佳，但對正常系統作業的影響較大。

AEM 6.5在壓縮期間也引進了更有效率的內容重複資料刪除機制，進一步減少了存放庫在磁碟上的空間。

以下兩張圖表呈現內部實驗室測試的結果，說明與AEM 6.3相比，AEM 6.5的平均執行時間和平均磁碟空間佔用減少：

![onrc-duration-6_4vs63](assets/onrc-duration-6_4vs63.png) ![segmentstore-6_4vs63](assets/segmentstore-6_4vs63.png)

### 如何設定完全和尾部壓縮 {#how-to-configure-full-and-tail-compaction}

預設設定會在週日執行尾部壓縮，並在星期日執行完全壓縮。 預設設定可使用新設定值變更 `full.gc.days` 的 `RevisionCleanupTask` [維護任務](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup).

當您設定 `full.gc.days` 值請注意，完全壓縮會在值中定義的日子執行，而尾部壓縮會在值中未定義的日子執行。 例如，如果您設定完全壓縮在星期日執行，則尾部壓縮將在星期一到星期六執行。 例如，如果您將完全壓縮設定為一週中的每一天執行，則尾部壓縮將完全不執行。

此外，請考量以下事項：

* **尾部壓縮** 效率較低，對正常系統作業的影響也較小。 因此，此函式會在營業日執行。
* **完全壓縮** 更有效率，但對一般系統作業的影響也更大。 因此，此函式適用於非工作日。
* 尾部壓縮和完全壓縮都應該排程在非尖峰時段執行。

### 疑难解答 {#troubleshooting}

使用新的壓縮模式時，請記住以下事項：

* 您可以監視輸入/輸出(I/O)活動，例如：I/O作業、等待IO的CPU、認可佇列大小。 這有助於判斷系統是否受到I/O限制，且需要升級。
* 此 `RevisionCleanupTaskHealthCheck` 表示「線上修訂清除」的整體健康狀態。 其運作方式與AEM 6.3相同，且無法區分完整和尾部壓縮。
* 記錄訊息包含有關壓縮模式的相關資訊。 例如，當「線上修訂清除」啟動時，對應的記錄訊息將指示壓縮模式。 此外，在某些轉角案例中，當排定執行尾部壓縮時，系統將恢復為完全壓縮，而記錄訊息將指示此變更。 下列記錄檔範例指出壓縮模式，以及從尾部到完全壓縮的變更：

```
TarMK GC: running tail compaction
TarMK GC: no base state available, running full compaction instead
```

### 已知限制 {#known-limitations}

在某些情況下，在尾部模式和完全壓縮模式之間切換會延遲清理過程。 更準確地說，完全壓縮後，存放庫會成長（大小會加倍）。 當存放庫下降到完全壓縮前的大小下方時，額外的空間將在後續的尾部壓縮中回收。 也應避免執行平行維護任務。

**建議磁碟大小至少比最初估計的存放庫大小大兩到三倍。**

## 線上修訂清除常見問題 {#online-revision-cleanup-frequently-asked-questions}

### AEM 6.5升級注意事項 {#aem-upgrade-considerations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td>问题 </td>
   <td>答案</td>
  </tr>
  <tr>
   <td>升級至AEM 6.5時應該注意什麼？</td>
   <td><p>TarMK的持續性格式將隨AEM 6.5而改變。這些變更不需要主動移轉步驟。 現有存放庫將進行滾動式移轉，這對使用者而言是透明的。 移轉程式會在AEM 6.5 （或相關工具）首次存取存放庫時啟動。</p> <p><strong>一旦開始移轉至AEM 6.5持續性格式，存放庫就無法恢復為之前的AEM 6.3持續性格式。</strong></p> </td>
  </tr>
 </tbody>
</table>

### 移轉至Oak區段Tar {#migrating-to-oak-segment-tar}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>问题</strong></td>
   <td><strong>答案</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>為什麼我需要移轉存放庫？</strong></td>
   <td><p>在AEM 6.3中，需要變更儲存格式，尤其是為了改善線上修訂清除的效能和功效。 這些變更無法回溯相容，且使用舊版Oak區段(AEM 6.2及舊版)建立的存放庫必須移轉。</p> <p>變更儲存格式的其他優點：</p>
    <ul>
     <li>更優異的擴充性（最佳化的區段大小）。</li>
     <li>更快 <a href="/help/sites-administering/data-store-garbage-collection.md" target="_blank">資料存放區垃圾收集</a>.<br /> </li>
     <li>未來增強功能的基礎。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>是否仍支援舊版的Tar格式？</strong></td>
   <td>AEM 6.3或更新版本僅支援新的Oak區段Tar。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>內容移轉是否一律為強制性？</strong></td>
   <td>是。除非您以新的執行個體開始，否則永遠必須移轉內容。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>我可以升級至6.3或更新版本並在稍後執行移轉（例如，使用另一個維護時段）嗎？</strong></td>
   <td>否，如上所述，內容移轉是強制性的。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>移轉時可避免停機嗎？</strong></td>
   <td>否. 這是一次性的工作，無法在執行中的執行個體上完成。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果我意外執行了錯誤的存放庫格式，會發生什麼情況？</strong></td>
   <td>如果您嘗試對oak-segment-tar存放庫執行oak-segment模組（反之亦然），啟動將失敗 <em>IllegalState例外狀況</em> 並顯示「無效區段格式」訊息。 不會發生資料損毀。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>是否需要重新索引搜尋索引？</strong></td>
   <td>否. 從Oak-segment移轉至Oak-segment-tar會導致容器格式發生變更。 包含的資料不受影響，也不會被修改。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何以最佳方式計算移轉期間和之後所需的預期磁碟空間？</strong></td>
   <td>移轉等同於以新格式重新建立區段存放區。 這可用來估計移轉期間所需的額外磁碟空間。 移轉後，可以刪除舊區段存放區以回收空間。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何以最佳方式估計移轉的持續時間？</strong></td>
   <td>遷移效能可大幅提升，如果 <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup">離線修訂清除</a> 會在移轉前執行。 建議所有客戶在升級程式的先決條件執行它。 一般而言，移轉的持續時間應與離線修訂清除工作的持續時間類似（假設離線修訂清除工作已在移轉之前執行）。</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 正在執行線上修訂清除 {#running-online-revision-cleanup}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>问题</strong></td>
   <td><strong>答案</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>線上修訂清除應該多久執行一次？</strong></td>
   <td>每日一次. 這是「操作控制面板」中的預設設定。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何設定線上修訂清除維護任務的開始時間？</strong></td>
   <td>請參閱 <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">如何執行線上修訂清除</a> 區段。 </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>是否有線上修訂清除不應超過的最大頻率？</strong></td>
   <td>建議每天執行一次線上修訂清除，如同預設設定。<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>決定線上修訂清除執行頻率的關鍵指標是什麼？</strong></td>
   <td>無需判斷頻率，因為「線上修訂清除」已設定為維護任務，且每天自動執行。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>第一次執行線上修訂清除時，為何不會回收任何空間？</strong></td>
   <td>線上修訂清除會依層代回收舊修訂版本。 每次執行修訂清除時，都會產生新的產生。 只有至少兩代的內容才會回收，這表示在第一次執行時沒有任何可回收的內容。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>為什麼第一次線上修訂清除在離線修訂清除後執行時，不會回收任何空間？</strong></td>
   <td><p>離線修訂清除正在回收除了最新一代以外的所有內容，而線上修訂清除則使用最新兩代。 若是新的存放庫，「線上修訂清除」在離線修訂清除後第一次執行時，不會回收任何空間，因為沒有足夠舊的層代可回收。</p> <p>此外，請閱讀的「離線修訂清除後執行線上修訂清除」一節。 <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">本章節</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Author和Publish通常會有不同的線上修訂清除視窗嗎？</strong></td>
   <td>這取決於營業時間和客戶線上狀態的流量模式。 維護時段應在主要生產時間以外設定，以實現最佳清理功效。 若為多個AEM發佈執行個體（TarMK陣列），線上修訂清除的維護時段應分批進行。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>執行線上修訂清除之前是否有任何先決條件？</strong></td>
   <td><p>線上修訂清除僅適用於AEM 6.3及更高版本。 此外，如果您使用舊版AEM，則需要移轉至新版 <a href="/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar">Oak區段Tar</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>決定「線上修訂清除」持續時間的因素為何？</strong></td>
   <td>因素包括：<br />
    <ul>
     <li>存放庫大小</li>
     <li>在系統上載入（每分鐘請求數，特別是寫入作業）</li>
     <li>活動模式（讀取與寫入）</li>
     <li>硬體規格（CPU效能、記憶體、IOPS）</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>執行「線上修訂清除」時，作者是否仍可繼續工作？</strong></td>
   <td>是，「線上修訂清除」可處理同時寫入。 不過，「線上版次清理」可以更快更有效率地運作，而不需要同時執行寫入異動。 建議將「線上修訂清除」維護工作排程在相對安靜的時間，不會有太多流量。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>執行線上修訂清除時，磁碟空間和棧積記憶體的最低需求為何？</strong></td>
   <td><p>線上上修訂清除期間，會持續監視磁碟空間。 如果可用磁碟空間下降到關鍵值以下，則會取消此程式。 關鍵值是存放庫目前磁碟空間的25%，且無法設定。</p> <p><strong>建議磁碟大小至少比最初估計的存放庫大小大兩到三倍。</strong></p> <p>在清理程式期間，會持續監控可用棧積空間。 如果可用棧積空間下降到關鍵值以下，則會取消此程式。 臨界值是透過org.apache.jackrabbit.oak.segment.SegmentNodeStoreService#MEMORY_THRESHOLD設定。 預設值為15%。</p> <p>Recommendations提供最小壓縮棧積大小，但並未與AEM記憶體大小調整建議分開。 一般規則： <strong>如果AEM執行個體的大小足以應付使用案例和預期上的裝載，則清理程式將獲得足夠的記憶體。</strong></p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>執行「線上修訂清除」時，預期的效能影響為何？</strong></td>
   <td>線上修訂清除」是背景程式，可同時讀取和寫入存放庫以進行正常的系統作業。 尤其是，它可能需要在短時間內獨佔存取存放庫，以防止其他對話串寫入存放庫。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>線上修訂清除預計執行多久？</strong></td>
   <td>根據我們在內部執行的最新效能測試，執行時間不應超過2小時。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果線上修訂清除需要更長的時間，應該怎麼做？</strong></td>
   <td>
    <ul>
     <li>請確定每天都執行。<br /> </li>
     <li>確保透過在操作儀表板中相應地設定維護視窗，在最小儲存庫活動期間執行它。</li>
     <li>擴充系統資源（CPU、記憶體、I/O）。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果線上修訂清除超過設定的維護期間會發生什麼情況？</strong></td>
   <td>請確定其他維護任務沒有延遲執行。 如果在相同的維護時段內執行比「線上修訂清除」更多的維護任務，就可能會發生這種情況。 請注意，維護任務會依序執行，而不會有可設定的順序。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>為何略過修訂垃圾收藏集？</strong></td>
   <td><p>修訂清除依賴估計階段來判斷是否有足夠的垃圾要清除。 估算程式會比較目前大小與上次壓縮後存放庫的大小。 如果大小超過設定的差異，將會執行清理。 大小差異設定為1 GB。 這實際上意味著，如果存放庫大小自上次清除執行以來未增加1 GB，則會略過新的修訂版清除反複專案。 </p> <p>以下是估算階段的相關記錄專案：</p>
    <ul>
     <li>修訂GC將會執行： <em>大小差異為N%或N/N （N/N位元組），因此執行壓縮</em></li>
     <li>修訂GC將 <strong>not</strong> 執行： <em>大小差異為N%或N/N （N/N位元組），因此現在會略過壓縮</em></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果效能影響太大，是否可以安全地中止自動壓縮？</strong></td>
   <td>是。自AEM 6.3起，您可以透過「操作控制面板」內的「維護工作視窗」或透過JMX安全地停止它。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果AEM執行個體在排定的清理工作期間關閉，處理程式是否會安全地中止，或是在壓縮完成前封鎖關機？</strong></td>
   <td>修訂清除將中斷，存放庫將安全關閉。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>當系統線上上修訂清除期間當機時，會發生什麼情況？</strong></td>
   <td>在這種情況下，沒有資料損毀的風險。 後續執行將清理垃圾剩餘。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>未執行線上修訂清除會產生什麼影響？</strong></td>
   <td>效能會隨著時間而降低。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>正在收集哪些修訂版本？</strong></td>
   <td>依預設，「線上修訂清除」只會收集至少24小時之前的修訂版本。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果同時寫入存放庫的干擾太大，會發生什麼情況？</strong></td>
   <td><p>如果系統上有寫入並行，線上修訂清除可能需要獨佔寫入存取權，才能在壓縮週期結束時認可變更。 系統將會進入 <strong>forceCompact模式</strong>，詳情請參閱 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html" target="_blank">Oak檔案</a>. 在強制壓縮期間，會取得獨佔寫入鎖定，以最終認可變更，而不會同時干擾寫入。 若要限制對回應時間的影響，可定義逾時值。 此值預設為1分鐘，這表示如果強制壓縮未在1分鐘內完成，壓縮流程將中止，以支援同時認可。</p> <p>強制壓縮的持續時間取決於以下因素：</p>
    <ul>
     <li>硬體：尤其是IOPS。 持續時間會隨著IOPS的增加而縮短。</li>
     <li>區段存放區大小：持續時間會隨著區段存放區的大小而增加。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>線上修訂清除在待命執行個體上如何執行？</strong></p> </td>
   <td><p>在冷待命設定中，只需要將主要執行個體設定為執行「線上修訂清除」。 在待命執行個體上，不需要特別排定「線上修訂清除」。</p> <p>待命執行個體上的對應操作是「自動清理」 — 這對應於「線上修訂清理」的清理階段。 在主要執行個體上執行「線上修訂清除」之後，在待命執行個體上執行「自動清除」。</p> <p>預估和壓縮階段不會在待命執行個體上執行。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>離線修訂清除是否比線上修訂清除能釋放更多磁碟空間？</strong></td>
   <td><p>離線修訂清除可以立即移除舊修訂版本，而線上修訂清除需要說明應用程式棧疊仍在參考的舊修訂版本。 因此，前者比後者能更積極地移除垃圾，其效果會在幾個垃圾收集週期內攤銷。</p> <p>此外，請閱讀的「離線修訂清除後執行線上修訂清除」一節。 <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">本章節</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>有關記憶體對應檔案作業的任何考量事項？</td>
   <td>
    <ul>
     <li><strong>在Windows環境中</strong>，會一律強制執行一般檔案存取，以免使用記憶體對應存取。 一般建議將所有可用的RAM配置給棧集，並增加segmentCache大小。 您可以將segmentCache.size選項新增至org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config (例如segmentCache.size=20480)以增加segmentCache。 請記得為作業系統和其他處理序省略一些RAM。</li>
     <li><strong>在非Windows環境中</strong>，增加實體記憶體大小以改善存放庫的記憶體對應。</li>
    </ul> </td>
   <td>
    <ul>
     <li> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 監視線上修訂清除 {#monitoring-online-revision-cleanup}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>線上修訂清除期間需要監控哪些專案？</strong></td>
   <td>
    <ul>
     <li>啟用[線上修訂清除]時，應該監視磁碟空間。 當磁碟空間不足時，將不會執行或會先佔終止清理。</li>
     <li>檢查線上修訂清除的完成時間記錄。 此過程不應超過2小時。</li>
     <li>查核點數目。 如果在壓縮執行時有超過3個查核點，建議清除查核點。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何檢查線上修訂清除是否成功完成？</strong></td>
   <td><p>您可以檢查記錄檔來檢查線上修訂清除是否成功完成。</p> <p>例如，「<code>TarMK GC #{}: compaction completed in {} ({} ms), after {} cycles</code>「表示壓縮步驟成功完成，除非在訊息前面」<code>TarMK GC #{}: compaction gave up compacting concurrent commits after {} cycles</code>「」，這表示有太多同時負載。</p> <p>相應地，還有一則訊息「<code>TarMK GC #{}: cleanup completed in {} ({} ms</code>」以成功完成清理步驟。</p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><strong>我們可以在哪裡找到上次線上修訂清除執行的統計資料？</strong></td>
   <td><p>狀態、進度和統計資料會透過JMX (<code>SegmentRevisionGarbageCollection</code> MBean)。 如需更多關於 <code>SegmentRevisionGarbageCollection</code> MBean，請閱讀 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">跟隨段落</a>.</p> <p>進度可透過 <code>EstimatedRevisionGCCompletion</code> 的屬性 <code>SegmentRevisionGarbageCollection MBean.</code></p> <p>您可以使用取得MBean的參照 <code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection"</code>.</p> <p>請注意，統計資料僅自上次系統啟動後提供。 可運用外部監控工具，讓資料超出AEM運作時間。 另請參閱 <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios" target="_blank">將健康情況檢查附加至Nagios的AEM檔案，作為外部監控工具的範例</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>哪些是相關的記錄專案？</strong></td>
   <td>
    <ul>
     <li>線上修訂清除已開始/停止
      <ul>
       <li>線上修訂清除由三個階段組成：估計、壓縮和清除。 如果存放庫未包含足夠的垃圾，估算可能會強制略過壓縮和清理。 在最新版AEM中，訊息為「<code>TarMK GC #{}: estimation started</code>「會標籤預估的開頭， 」<code>TarMK GC #{}: compaction started, strategy={}</code>」會標籤壓縮的開頭，而「T」<code>arMK GC #{}: cleanup started. Current repository size is {} ({} bytes</code>」會標籤清除的開始。</li>
      </ul> </li>
     <li>修訂清除所取得的磁碟空間
      <ul>
       <li>只有在清除階段完成時，才會回收空間。 清理階段的完成會以記錄訊息「T」標示<code>arMK GC #{}: cleanup completed in {} ({} ms</code>「。 後續清理大小為{} （{}位元組），已回收空間{} （{}位元組）。 壓縮地圖寬度/深度為{}/{} （{}位元組/{}）。」</li>
      </ul> </li>
     <li>修訂清除期間發生問題
      <ul>
       <li>有許多失敗情況，所有情況都標示為以「TarMK GC」開頭的WARN或ERROR記錄訊息。</li>
      </ul> </li>
    </ul> <p>另請參閱 <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">根據錯誤訊息進行疑難排解</a> 區段底下。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何檢查完成線上修訂清除後回收了多少空間？</strong></td>
   <td>清理週期結束時的記錄檔中有一則訊息："<code>TarMK GC #3: cleanup completed</code>「包括存放庫大小和回收的垃圾量。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>線上修訂清除完成後，如何檢查存放庫的完整性？</strong></td>
   <td><p>線上修訂清除後不需要檢查存放庫完整性。 </p> <p>不過，您可以執行下列動作，在清除後檢查存放庫狀態：</p>
    <ul>
     <li>存放庫 <a href="/help/sites-deploying/consistency-check.md" target="_blank">周遊檢查</a></li>
     <li>在清除程式完成後，使用Oak-run工具來檢查不一致之處。 如需如何執行此動作的詳細資訊，請檢視 <a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">Apache檔案。</a> 您不需要關閉AEM即可執行工具。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何偵測線上修訂清除是否失敗，以及要復原的步驟為何？</strong></td>
   <td>失敗情況會以「TarMK GC」開頭的WARN或ERROR記錄訊息標示。 另請參閱 <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">根據錯誤訊息進行疑難排解</a> 區段底下。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>修訂清除健康情況檢查中會公開哪些資訊？ 它們如何以及何時對顏色編碼狀態層級作出貢獻？ </strong></td>
   <td><p>修訂清理健康情況檢查是 <a href="/help/sites-administering/operations-dashboard.md#health-reports" target="_blank">操作控制面板</a>.<br /> </p> <p>狀態將為 <strong>綠色</strong> 如果「線上修訂清除」維護任務的最後一次執行成功完成。</p> <p>將會是 <strong>黃色</strong> 如果「線上版次清理」維護作業已取消一次。<br /> </p> <p>將會是 <strong>紅色</strong> 如果「線上版次清理」維護作業連續取消三次。 <strong>在此情況下，需要手動互動</strong> 或「線上修訂清除」可能再次失敗。 如需詳細資訊，請閱讀 <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-online-revision-cleanup">疑難排除</a> 區段底下。<br /> </p> <p>另請注意，系統重新啟動後，將會重設健康情況檢查狀態。 因此，新重新啟動的執行個體會在修訂清除健康情況檢查中顯示綠色狀態。 可運用外部監控工具，讓資料超出AEM運作時間。 另請參閱 <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios">將健康情況檢查附加至Nagios的AEM檔案，作為外部監控工具的範例</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>如何在待命執行個體上監視自動清除？</strong></p> </td>
   <td><p>透過JMX使用公開狀態、進度和統計資料 <code>SegmentRevisionGarbageCollection</code> MBean。 另請參閱下列內容 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">Oak檔案</a>. </p> <p>您可以使用取得MBean的參照 <code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection"</code>.</p> <p>請注意，統計資料僅自上次系統啟動後可用。 可運用外部監控工具，讓資料超出AEM運作時間。 另請參閱 <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios" target="_blank">將健康情況檢查附加至Nagios的AEM檔案，作為外部監控工具的範例</a>.</p> <p>記錄檔也可用來檢查自動清理的狀態、進度和統計資料。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>在待命執行個體的自動清除期間，需要監視哪些專案？</strong></p> </td>
   <td>
    <ul>
     <li>執行「自動清理」時，應監視磁碟空間。</li>
     <li>完成時間（透過記錄檔）以確保不會超過2小時。</li>
     <li>執行自動清理後的區段存放區大小。 待命執行個體上的區段存放區大小應該與主要執行個體上的區段存放區大小大致相同。</li>
    </ul> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 疑難排解線上修訂清除 {#troubleshooting-online-revision-cleanup}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>如果不執行線上修訂清除，可能會發生什麼最壞的情況？</strong></td>
   <td>AEM執行個體的磁碟空間將會用盡，進而導致生產中斷。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>在發佈執行個體上執行線上修訂清除時，高使用者流量是否有問題？</strong></td>
   <td>高使用者流量會影響壓縮階段是否能夠成功完成。<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>根據「狀況檢查」與記錄專案，「線上修訂清除」連續三次未順利完成。 需要什麼才能讓線上修訂清除順利完成？</strong></td>
   <td>您可以採取幾個步驟來尋找和修正問題：<br />
    <ul>
     <li>首先，檢查記錄專案<br /> </li>
     <li>根據記錄檔中的資訊，採取適當的動作：
      <ul>
       <li>如果紀錄顯示五個錯過的壓縮週期和一個逾時 <code>forceCompact</code> 週期，將維護期間排程為存放庫寫入量低時的安靜時間。 您可以在存放庫度量監視工具中檢視存放庫寫入，該工具位於 <em>https://serveraddress:serverport/libs/granite/operations/content/monitoring/page.html</em></li>
       <li>如果清理在維護時段結束時停止，請確定維護任務使用者介面中的維護時段設定足夠大</li>
       <li>如果可用的棧積記憶體不足，請確定執行個體有足夠的記憶體。</li>
       <li>如果反應延遲，區段存放區可能會增長太多，線上修訂清除甚至無法在較長的維護時段內完成。 例如，如果上週未成功完成線上修訂清除，則建議規劃離線維護並執行離線修訂清除，以將區段存放區恢復到可管理的大小。</li>
      </ul> </li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Healthcheck警示開啟後需要做什麼？</strong></td>
   <td>請參閱上一個點。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果「線上修訂清除」在排程的維護期間逾時，會發生什麼情況？</strong></td>
   <td>將取消線上修訂清除，並將移除剩餘的專案。 下次排定維護時段時，它會重新開始。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>原因 <code>SegmentNotFoundException</code> 要登入的例項 <code>error.log</code> 如何復原？</strong></td>
   <td><p>A <code>SegmentNotFoundException</code> 當TarMK嘗試存取其找不到之儲存單位（區段）時會由TarMK記錄。 有三種情況可能會導致此問題：</p>
    <ol>
     <li>一種應用程式，可規避建議的存取機制（例如Sling和JCR API），並使用較低層級的API/SPI來存取存放庫，然後超過區段的保留時間。 也就是說，它會保留實體參照，保留時間超過線上修訂清除所允許的保留時間（預設為24小時）。 此案例為暫時性，不會導致資料損毀。 若要復原，應使用Oak-run工具來確認例外狀況的暫時性（Oak-run檢查不應回報任何錯誤）。 若要這麼做，需要讓執行個體離線並稍後重新啟動。</li>
     <li>外部事件造成磁碟上的資料損毀。 這可能是磁碟故障、磁碟空間不足或意外修改所需資料檔案所致。 在此情況下，需要離線執行個體，並使用Oak-run檢查來修復。 如需如何執行Oak-run檢查的詳細資訊，請閱讀以下內容 <a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">Apache檔案</a>.</li>
     <li>所有其他事件應透過 <a href="https://helpx.adobe.com/cn/marketing-cloud/contact-support.html" target="_blank">Adobe客戶服務</a>.</li>
    </ol> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 根據錯誤訊息進行疑難排解 {#troubleshooting-based-on-error-messages}

如果線上上修訂清除程式期間發生事件，error.log將會是詳細的。 以下矩陣旨在說明最常見的訊息並提供可能的解決方案：

<!---| **Phase** |**Log Messages** |**Explanation** |**Next Steps** |
|---|---|---|---|
|   |  |  |  |
| Estimation |TarMK GC #2: estimation skipped because compaction is paused |The estimation phase is skipped when compaction is disabled on the system by configuration. |Enable Online Revision Cleanup. |
|   |TarMK GC #2: estimation interrupted: ${REASON}. Skipping compaction. |The estimation phase terminated prematurely. Some examples of events that could interrupt the estimation phase: not enough memory or disk space on the host system. |Depends on the given reason. |
| Compaction |TarMK GC #2: compaction paused |As long as the compaction phase is paused by configuration, neither the estimation phase nor the compaction phase will be executed. |Enable online revision cleanup. |
|   |TarMK GC #2: compaction cancelled: ${REASON}. |The compaction phase terminated prematurely. Some examples of events that could interrupt the compaction phase: not enough memory or disk space on the host system. Moreover, compaction can also be cancelled by shutting down the system or by explicitly cancelling it via administrative interfaces such as the Maintenance Window within the Operations Dashobard. |Depends on the given reason. |
|   |TarMK GC #2: compaction failed in 32.902 min (1974140 ms), after 5 cycles |This message doesn’t mean that there was an unrecoverable error, but only that compaction was terminated after a certain amount of attempts. Also, read the [following paragraph](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes). |Read the following [Oak documentation](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes), and the last question of the [Running Online Revision Cleanup](/help/sites-deploying/revision-cleanup.md#running-online-revision-cleanup) section. |
| Cleanup |TarMK GC #2: cleanup interrupted |Cleanup has been cancelled by shutting down the repository. No impact on consistency is expected. Also, disk space is most likely not reclaimed to full extent. It will be reclaimed during next revision cleanup cycle. |Investigate why repository has been shut down and going forward try to avoid shutting down the repository during maintenance windows. |-->

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>階段</th>
    <th>記錄訊息</th>
    <th>解释</th>
    <th>后续步骤</th>
  </tr>  
  <tr>
    <td>預估</td>
    <td>TarMK GC #2：估算已略過，因為壓縮已暫停。</td>
    <td>當設定在系統上停用壓縮時，會略過預估階段。</td>
    <td>啟用線上修訂清除。</td>
  </td>
  </tr>
  <tr>
    <td>不适用</td>
    <td>TarMK GC #2：估計中斷： ${REASON}。 正在略過壓縮。</td>
    <td>預估階段過早結束。 可能中斷估計階段的一些事件範例：主機系統上的記憶體或磁碟空間不足。</td>
    <td>取決於特定原因。</td>
  </td>
  </tr>
  <tr>
    <td>壓縮</td>
    <td>TarMK GC #2：壓縮已暫停。</td>
    <td>只要壓縮階段由設定暫停，預估階段和壓縮階段都不會執行。</td>
    <td>啟用線上修訂清除。</td>
  </td>
  </tr>
   <tr>
    <td>不适用</td>
    <td>TarMK GC #2：壓縮已取消： ${REASON}。</td>
    <td>壓縮階段提前結束。 可能中斷壓縮階段的一些事件範例：主機系統上的記憶體或磁碟空間不足。 此外，也可以關閉系統或透過管理介面（例如「操作控制面板」內的「維護視窗」）明確取消系統，來取消壓縮。</td>
    <td>取決於特定原因。</td>
  </td>
  </tr>
  <tr>
    <td>不适用</td>
    <td>TarMK GC #2：5次循環後32.902分鐘(1974140毫秒)內壓實失敗。</td>
    <td>此訊息並不表示發生無法復原的錯誤，只表示在嘗試一段時間後壓縮已終止。 此外，請閱讀 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes">在段落之後。</a></td>
    <td>閱讀下列內容 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes">Oak檔案</a>，以及「執行線上修訂清除」區段的最後一個問題。</a></td>
  </td>
  </tr>
  <tr>
    <td>清理</td>
    <td>TarMK GC #2：清理已中斷。</td>
    <td>已透過關閉存放庫來取消清理。 一致性預期沒有影響。 此外，磁碟空間很可能無法完全回收。 它將在下一個修訂清除週期中回收。</td>
    <td>調查存放庫已關閉的原因，並繼續努力避免在維護期間關閉存放庫。</td>
  </td>
  </tr>
  </tbody>
</table>

## 如何執行離線修訂清除 {#how-to-run-offline-revision-cleanup}

>[!CAUTION]
>
>使用版本號碼（主要和次要）符合AEM安裝Oak核心版本的Oak-run工具發行版本。 例如，如果您的AEM執行個體有Oak核心版本1.22.x，您應使用最新版本的Oak-run工具1.22.x。

Adobe提供了一個工具，稱為 **Oak-run** 以執行修訂清除。 您可在下列位置下載此版本：

[https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/)

此工具是可執行的jar，可以手動執行以壓縮存放庫。 此程式稱為離線修訂清除，因為存放庫必須關閉才能正確執行工具。 請務必根據您的維護期間來規劃清理。

如需有關如何提高畫質除程式效能的秘訣，請參閱 [提高離線修訂清除的效能](/help/sites-deploying/revision-cleanup.md#increasing-the-performance-of-offline-revision-cleanup).

>[!NOTE]
>
>您也可以在進行維護之前清除舊查核點（以下程式中的步驟2和3）。 建議僅對擁有超過100個查核點的執行個體使用此選項。

1. 請一律確認您有AEM執行個體最近的備份。

   關閉AEM。

1. （選用）使用工具尋找舊查核點：

   ```xml
   java -jar oak-run.jar checkpoints install-folder/crx-quickstart/repository/segmentstore
   ```

1. （選用）然後，刪除未參考的查核點：

   ```xml
   java -jar oak-run.jar checkpoints install-folder/crx-quickstart/repository/segmentstore rm-unreferenced
   ```

1. 執行壓縮並等待它完成：

   ```xml
   java -jar -Dsun.arch.data.model=32 oak-run.jar compact install-folder/crx-quickstart/repository/segmentstore
   ```

### 提高離線修訂清除的效能 {#increasing-the-performance-of-offline-revision-cleanup}

Oak-run工具引進了多項功能，旨在提高修訂清除流程的效能，並儘可能減少維護時段。

此清單包含數個命令列引數，如下所述：

* **-mmap。** 您可以將此項設為true或false。 如果設為true，則使用記憶體對應存取。 如果設為false，則會使用檔案存取。 如果未指定，記憶體對應存取會用於64位元系統，而檔案存取則會用於32位元系統。 在Windows上，一律會強制進行一般檔案存取，而會忽略此選項。 **此引數已取代 — Dtar.memoryMapped引數。**

* **-Dupdate.limit**. 定義磁碟臨時交易排清的臨界值。 默认值为 10000。

* **-Dcompress間隔**. 壓縮目前地圖之前要保留的壓縮地圖專案數。 預設值為1000000。 如果有足夠的棧積記憶體可用，您應該將此值增加到更高的數目，以加快輸送量。 **此引數已在Oak 1.6版中移除，因此無效。**

* **-Dcompaction-progress-log**. 將記錄的壓縮節點數。 預設值為150000，這表示在操作期間將記錄前150000個壓縮的節點。 請將此選項與以下記錄的下一個引數搭配使用。

* **-Dtar.PersistCompactionMap。** 將此引數設為true可使用磁碟空間來取代棧積記憶體來維持壓縮對應。 需要Oak-run工具 **版本1.4** 和更高版本。 如需更多詳細資訊，請參閱 [離線修訂清除常見問題](/help/sites-deploying/revision-cleanup.md#offline-revision-cleanup-frequently-asked-questions) 區段。 **此引數已在Oak 1.6版中移除，因此無效。**

* **—force。** 強制壓縮並忽略不匹配的區段存放區版本。

>[!CAUTION]
>
>使用 `--force` 引數會將區段存放區升級至最新版本，此版本與舊版Oak不相容。 此外，請考量到無法降級。 一般而言，使用這些引數時請務必謹慎，且僅在您瞭解如何使用這些引數時才會使用。

使用中的引數範例：

```xml
java -Dupdate.limit=10000 -Dcompaction-progress-log=150000 -Dlogback.configurationFile=logback.xml -Xmx8g -jar oak-run-*.jar checkpoints <repository>
```

### 觸發修訂清除的其他方法 {#additional-methods-of-triggering-revision-cleanup}

除了上述方法之外，您也可以使用JMX主控台來觸發修訂清除機制，如下所示：

1. 開啟JMX主控台，方法是前往 [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)
1. 按一下 **RevisionGarbageCollection** MBean。
1. 在下一個視窗中，按一下 **startRevisionGC()** 然後 **叫用** 以啟動「修訂垃圾收集」工作。

### 離線修訂清除常見問題 {#offline-revision-cleanup-frequently-asked-questions}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>決定離線修訂清除持續時間的因素為何？</strong></td>
   <td><p>存放庫大小和需要清理的修訂數量會決定清理的持續時間。</p> </td>
  </tr>
  <tr>
   <td><strong>修訂版本和頁面版本之間有何差異？</strong></td>
   <td>
    <ul>
     <li><strong>Oak修訂版本：</strong> Oak會以大型樹狀階層來組織所有內容，該階層包含節點和屬性。 此內容樹狀結構的每個快照或修訂版本都是不可變的，而且樹狀結構的變更會以新修訂版本的順序表示。 通常，每個內容修改都會觸發新的修訂。 另請參閱 <a href="https://jackrabbit.apache.org/dev/ngp.html" target="_blank"> 關注連結</a>.</li>
     <li><strong>頁面版本：</strong> 版本設定功能會在特定時間點建立頁面的「快照」。 通常，新版本會在頁面啟動時建立。 如需詳細資訊，請參閱 <a href="/help/sites-authoring/working-with-page-versions.md" target="_blank">使用頁面版本</a>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>如果「離線修訂清除」任務未在8小時內完成，該如何加快該任務執行速度？</strong></td>
   <td>如果修訂任務未在8小時內完成，並且 <a href="/help/sites-administering/operations-dashboard.md#diagnosis-tools" target="_blank">執行緒傾印</a> 顯示主要熱點為 <code>InMemoryCompactionMap.findEntry</code>，搭配oak-run工具使用下列引數 <strong>版本1.4 </strong>或更高： <code>-Dtar.PersistCompactionMap=true</code>. 請注意 <code>-Dtar.PersistCompactionMap</code> 引數已在Oak 1.6版中移除。</td>
  </tr>
 </tbody>
</table>
