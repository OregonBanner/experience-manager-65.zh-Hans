---
title: 微調健康狀態監視器效能
seo-title: Fine-tuning Health Monitor performance
description: 瞭解如何微調健康狀態監視器效能
seo-description: Learn how to fine-tune Health Monitor performance
uuid: 770b10cb-065f-41b5-9594-a291e4311151
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b8f8bddc-0d38-4d5e-b33f-978f04bc16c6
exl-id: 41042e08-5e14-4809-89b7-16d98a72d1b4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 1%

---

# 微調健康狀態監視器效能{#fine-tuning-health-monitor-performance}

收集系統統計資料以填入「健康情況監視」會對您的AEM Forms環境的效能造成一些影響。 若要控制此影響，請在應用程式伺服器中設定下列的Java選項。

<table>
 <thead>
  <tr>
   <th><p>属性</p></th>
   <th><p>用途</p></th>
   <th><p>預設值</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>adobe.healthmonitor.enabled</p></td>
   <td><p>開啟或關閉健康情況監視器執行緒</p></td>
   <td><p>true</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.statistics-enabled</p></td>
   <td><p>開啟或關閉Gemfire快取</p></td>
   <td><p>true</p></td>
  </tr>
  <tr>
   <td><p>adobe.healthmonitor.refresh-interval</p></td>
   <td><p>健康情況監視執行緒收集統計資料的間隔（毫秒）</p></td>
   <td><p>10分鐘（600,000毫秒）</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.multicast-port</p></td>
   <td><p>用來與分散式系統的其他成員通訊的多點傳送連線埠。 如果設為0，會停用成員探索和散發的多點傳送。 </p><p>注意：請為不同的分散式系統選取不同的多點傳送位址和連線埠。 請勿僅使用不同的地址。</p></td>
   <td><p>無預設值。 有效值的範圍介於0到65535之間。</p></td>
  </tr>
  <tr>
   <td><p>statistic-sample-rate</p></td>
   <td><p>統計資料取樣速率（毫秒）。 作業系統統計資料只會在取得範例時更新。</p></td>
   <td><p>600000</p></td>
  </tr>
  <tr>
   <td><p>adobe.workmanager.healthmonitor.enabled</p></td>
   <td><p>此屬性可啟用或停用Work Manager統計資料集合，例如工作或工作專案計數。</p></td>
   <td><p>true</p></td>
  </tr>
 </tbody>
</table>

## 將Java選項新增至JBoss {#add-java-options-to-jboss}

1. 停止JBoss應用程式伺服器。
1. 開啟 *[appserver根目錄]*/bin/run.bat (Windows)或run.sh （Linux或UNIX），並視需要新增任何Java選項。
1. 重新啟動伺服器。

## 將Java選項新增至WebLogic {#add-java-options-to-weblogic}

1. 輸入https://以啟動WebLogic管理主控台[主機名稱]：&#39;port&#39;/console （在網頁瀏覽器的URL行中）。
1. 輸入您為WebLogic Server網域建立的使用者名稱和密碼，然後按一下「變更中心」下的「記錄」，再按一下「鎖定與編輯」。
1. 在「網域結構」下，按一下「環境>伺服器」，然後在右窗格中按一下Managed伺服器名稱。
1. 在下一個畫面中，按一下「設定」標籤>「伺服器啟動」標籤。
1. 在「引數」方塊中，將所需的引數附加至目前內容的結尾。 例如，新增 —  `Dadobe.healthmonitor.enabled=false` 停用健康情況監視。
1. 按一下儲存，然後按一下啟用變更。
1. 重新啟動WebLogic管理的伺服器。

## 將Java選項新增至WebSphere {#add-java-options-to-websphere}

1. 在「WebSphere管理主控台」導覽樹狀結構中，對您的應用程式伺服器執行下列動作：

   (WebSphere 6.x)按一下「伺服器>應用程式伺服器」

   (WebSphere 7.x)按一下「伺服器>伺服器型別> WebSphere應用程式伺服器」

1. 在右窗格中，按一下伺服器名稱。
1. 在「伺服器基礎結構」下，按一下「Java和表單工作流程>程式定義」。
1. 在「其他屬性」下，按一下「Java虛擬機器器」。
1. 在「一般JVM引數」方塊中，輸入所需的引數。
1. 按一下「確定」或「套用」，然後按一下「直接儲存至主組態」。
