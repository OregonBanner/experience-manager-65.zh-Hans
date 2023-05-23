---
title: 疑難排解Adobe Experience Manager
description: 瞭解AEM的疑難排解問題。
uuid: 72379531-915c-45d0-ba70-42b212665272
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6346cd93-1ca3-4510-9c31-a74c41017ddb
docset: aem65
exl-id: d2d351e7-87a5-4895-b4ec-391fb0b66798
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 4%

---

# 疑難排解Adobe Experience Manager {#troubleshooting-aem}

以下章節涵蓋您在使用AEM (Adobe Experience Manager)時可能會遇到的一些問題，以及有關如何疑難排解這些問題的建議。

>[!NOTE]
>
>如果您正在疑難排解AEM中的撰寫問題，請參閱 [作者的疑難排解。](/help/sites-authoring/troubleshooting.md)

>[!NOTE]
>
>如果發生問題，也值得檢查清單 [已知問題](/help/release-notes/release-notes.md) （發行版本和Service Pack）。

## 針對管理員的疑難排解案例 {#troubleshooting-scenarios-for-administrators}

下表提供管理員可疑難排解之問題的概觀：

<table>
 <tbody>
  <tr>
   <td><strong>角色</strong></td>
   <td><strong>問題 </strong></td>
  </tr>
  <tr>
   <td>系统管理员</td>
   <td><p>連按兩下Quickstart jar沒有任何效果，或使用其他程式（例如archive manager）開啟jar檔案</p> </td>
  </tr>
  <tr>
   <td><p>系统管理员</p> </td>
   <td><p>在CRX上執行的應用程式擲回記憶體不足錯誤</p> </td>
  </tr>
  <tr>
   <td><p>系统管理员</p> </td>
   <td><p>連按兩下AEM CM Quickstart後，瀏覽器中不會顯示AEM歡迎畫面</p> </td>
  </tr>
  <tr>
   <td><p>系统管理员</p> <p>管理員使用者</p> </td>
   <td><p>建立執行緒傾印</p> </td>
  </tr>
  <tr>
   <td><p>系统管理员</p> <p>管理員使用者</p> </td>
   <td><p>檢查未關閉的JCR工作階段</p> </td>
  </tr>
 </tbody>
</table>

## 安裝問題 {#installation-issues}

另請參閱 [常見安裝問題](/help/sites-deploying/troubleshooting.md#common-installation-issues) 有關下列疑難排解情況的資訊：

* 連按兩下Quickstart jar或其他程式（例如archive manager）的JAR檔案沒有任何效果。
* 在CRX上執行的應用程式會擲回記憶體不足錯誤。
* 連按兩下AEM Quickstart後，瀏覽器中不會顯示AEM歡迎畫面。

## 疑難排解分析的方法 {#methods-for-troubleshooting-analysis}

### 建立執行緒傾印 {#making-a-thread-dump}

對話串傾印是目前作用中的所有Java™對話串的清單。 如果AEM沒有正確回應，執行緒傾印可以幫助您識別死鎖或其他問題。

### 使用Sling對話串傾印器 {#using-sling-thread-dumper}

1. 開啟 **AEM Web Console**；例如， `https://localhost:4502/system/console/`.
1. 選取 **執行緒**&#x200B;在&#x200B;**狀態** 標籤。

![screen_shot_2012-02-13at43925pm](assets/screen_shot_2012-02-13at43925pm.png)

### 使用jstack （命令列） {#using-jstack-command-line}

1. 尋找AEM Java™例項的PID （處理序ID）。

   例如，您可以使用 `ps -ef` 或 `jps`.

1. 运行:

   `jstack <pid>`

1. 顯示執行緒傾印。

>[!NOTE]
>
>您可以使用將對話串傾印附加至記錄檔案 `>>` 輸出重新導向：
>
>`jstack <pid> >> /path/to/logfile.log`

請參閱 [如何從JVM進行對話串傾印](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17452.html?lang=zh-Hans) 說明檔案以取得詳細資訊

### 檢查未關閉的JCR工作階段 {#checking-for-unclosed-jcr-sessions}

開發AEM WCM的功能時，可能會開啟JCR工作階段（相當於開啟資料庫連線）。 如果開啟的工作階段從未關閉，您的系統可能會遇到以下症狀：

* 系統變慢。
* 您可以看到許多CacheManager： resizeAll entries in the log file；下列數字(size=&lt;x>)顯示快取數目，每個工作階段會開啟數個快取。
* 系統時常會用盡記憶體（在數小時、數天或數週後，視嚴重程度而定）。

若要分析未關閉的工作階段並找出哪個程式碼未關閉工作階段，請參閱知識庫文章 [分析未關閉的工作階段](https://helpx.adobe.com/experience-manager/kb/AnalyzeUnclosedSessions.html).

### 使用Adobe Experience Manager Web Console {#using-the-adobe-experience-manager-web-console}

OSGi套件組合的狀態也能及早指出可能的問題。

1. 開啟 **AEM Web Console**；例如， `https://localhost:4502/system/console/`.
1. 選取 **套裝** 在 **OSGI** 標籤。
1. 检查:

   * 套件組合的狀態。 如果有任何「非使用中」或「不滿意」，請嘗試停止並重新啟動該套件。 如果問題仍然存在，請使用其他方法進一步調查。
   * 是否有任何套件組合缺少相依性。 按一下個別套件名稱（這是一個連結，以下範例沒有任何問題）即可檢視此類詳細資料：

![screen_shot_2012-02-13at44706pm](assets/screen_shot_2012-02-13at44706pm.png)
