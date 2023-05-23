---
title: 工作管理員和節流
seo-title: Work Manager and throttling
description: 本檔案提供Work Manager的背景資訊，以及設定Work Manager節流選項的指示。
seo-description: This document provides background information on Work Manager, and provides instructions on configuring Work Manager throttling options.
uuid: b90998bc-e3d4-493a-9371-55ccb44da20d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9a8b4e3a-f416-4dc6-a90a-9018df5c844e
exl-id: 1f765de2-1362-4318-9302-c5036e6fa7d6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 0%

---

# 工作管理員和節流{#work-manager-and-throttling}

AEM forms （及舊版）使用JMS佇列來非同步執行操作。 在AEM表單中，JMS佇列已由工作管理員取代。 本檔案提供Work Manager的背景資訊，以及設定Work Manager節流選項的指示。

## 關於長期（非同步）操作 {#about-long-lived-asynchronous-operations}

在AEM Forms中，服務執行的作業可能是短期（同步）或長期（非同步）。 短期作業會在從中叫用作業的相同執行緒上同步完成。 這些作業會等待回應，再繼續進行。

長期作業可能跨越系統，甚至延伸至組織以外，例如客戶必須完成並提交貸款申請表，作為整合多個自動化和人為作業的較大解決方案的一部分。 在等待回應的同時，這類作業必須繼續。 長期作業會以非同步方式執行其基礎工作，允許資源在等待完成時進行其他作業。 與短期作業不同，工作管理員在叫用長期作業時，不會認為該作業已完成。 必須發生外部觸發程式才能完成操作，例如系統請求對相同服務執行其他操作，或是使用者提交表單。

## 關於工作管理員 {#about-work-manager}

AEM forms （及舊版）使用JMS佇列來非同步執行操作。 AEM Forms會使用工作管理員，透過受管理的執行緒排程及執行非同步作業。

非同步操作的處理方式如下：

1. 工作管理員會收到要執行的工作專案。
1. 「工作管理員」會將工作專案儲存在資料庫表格中，並將唯一識別碼指派給工作專案。 資料庫記錄包含執行工作專案所需的所有資訊。
1. 當對話串變成可用狀態時，工作管理器對話串會拉入工作專案。 在提取工作專案之前，執行緒可以檢查需要的服務是否已啟動、是否有足夠的棧積大小可提取下一個工作專案，以及是否有足夠的CPU週期可處理工作專案。 在排程工作專案的執行時，「工作管理員」也會評估工作專案的屬性（例如其優先順序）。

AEM Forms管理員可以使用「健康情況監視器」來檢查Work Manager統計資料，例如佇列中的工作專案數量及其狀態。 您也可以使用「健全狀態監視」來暫停、繼續、重試或刪除工作專案。 (請參閱 [檢視與工作管理員相關的統計資料](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)

## 設定Work Manager節流選項 {#configuring-work-manager-throttling-options}

您可以為工作管理員設定節流，以便只有在有足夠的可用記憶體資源時才會排程工作專案。 您可在應用程式伺服器中設定下列JVM選項，以設定節流。

<table>
 <thead>
  <tr>
   <th><p>属性</p></th>
   <th><p>描述</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><code> adobe.work-manager.queue-refill-interval</code></td>
   <td><p>指定Work Manager檢查其佇列中新專案時使用的時間間隔（以毫秒為單位）。</p><p>此選項的值是整數。 預設值為 <code>1000</code> 毫秒（1秒）。 </p><p>如果非同步叫用的數量很低，您可以增加此值。 例如，您可以將其增加到2000到5000之間（2到5秒）。 </p><p>如果非同步叫用的數量很高，預設值應該就足夠了，但您可以視需要使用較低的值。 過多地減少這個值（例如，低於50，這會導致輪詢頻率為每秒20次）會對系統造成大量負荷。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.debug-mode-enabled</code></td>
   <td><p>將此選項設為 <code>true</code> 啟用偵錯模式，或設為false停用偵錯模式。 </p><p>在偵錯模式中，會記錄有關Work Manager原則違規和Work Manager暫停/恢復動作的訊息。 只有在疑難排解時才會將此選項設定為true。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.enabled</code></td>
   <td><p>將此選項設為 <code>true</code> 根據下列記憶體控制設定啟用節流，或是 <code>false</code> 以停用節流。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.high-limit</code></td>
   <td><p>指定在工作管理員限制傳入工作之前，可以使用的最大記憶體百分比。</p><p>此選項的預設值為 <code>95</code>. 這個值對於大多數系統應該都可以。 只有在您的系統需要推進到最大容量時才增加容量。 但請注意，隨著您增加此值，記憶體不足問題的風險也會增加。</p><p>如果您在叢集環境中執行AEM表單，您可能想要在叢集的不同節點上以不同方式設定記憶體控制限制設定。 例如，節點A和B的上限可能較低，這些節點會在您的負載平衡器中設定以進行互動式工作。 而且，您可以在節點C和D上設定較高的上限，負載平衡器不會使用這些節點，而是將其保留以用於非同步工作。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.low-limit</code></td>
   <td><p>指定工作管理員停止節流傳入工作之前，可使用的最大記憶體百分比。</p><p>此選項的預設值為 <code>20</code>. 這個值對於大多數系統應該都可以。</p></td>
  </tr>
  <tr>
   <td><code>Dadobe.workmanager.allocate.max-batch-size</code></td>
   <td><p>指定Workmanager的批次大小上限。 預設批次大小為10。</p><p>如果即使在任務完成後，Workmanager中的流程狀態也沒有更新，則將批次大小設定為1。</p></td>
  </tr>
 </tbody>
</table>

**將Java選項新增至JBoss**

1. 停止JBoss應用程式伺服器。
1. 開啟 *[appserver根目錄]*/bin/run.bat (Windows)或run.sh （Linux或UNIX），並視需要以格式新增任何Java選項 `-Dproperty=value`.
1. 重新啟動伺服器。

**將Java選項新增至WebLogic**

1. 輸入「 」以啟動WebLogic管理主控台 `https://[host name]:[port]/console` 在網頁瀏覽器中。
1. 輸入您為WebLogic Server網域建立的使用者名稱和密碼，然後按一下「變更中心」下的「記錄」，再按一下「鎖定與編輯」。
1. 在「網域結構」下，按一下「環境>伺服器」，然後在右窗格中按一下Managed伺服器名稱。
1. 在下一個畫面中，按一下「設定」標籤>「伺服器啟動」標籤。
1. 在「引數」方塊中，將所需的引數附加至目前內容的結尾。 例如，若要停用「健康情況監視」，請新增：

   `-Dadobe.healthmonitor.enabled=false` 停用健康情況監視。

1. 按一下儲存，然後按一下啟用變更。
1. 重新啟動WebLogic管理的伺服器。

**將Java選項新增至WebSphere**

1. 在「WebSphere管理主控台」導覽樹狀結構中，按一下「伺服器」>「伺服器型別」>「WebSphere應用程式伺服器」。
1. 在右窗格中，按一下伺服器名稱。
1. 在「伺服器基礎結構」下，按一下「Java和表單工作流程>程式定義」。
1. 在「其他屬性」下，按一下「Java虛擬機器器」。
1. 在「一般JVM引數」方塊中，輸入所需的引數。
1. 按一下「確定」或「套用」，然後按一下「直接儲存至主組態」。
