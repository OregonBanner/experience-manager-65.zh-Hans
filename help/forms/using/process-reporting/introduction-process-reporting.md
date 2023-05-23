---
title: 程式報告簡介
seo-title: Introduction to Process Reporting
description: AEM Forms on JEE Process Reporting的簡介和主要功能
seo-description: Introduction and key capabilities of AEM Forms on JEE Process Reporting
uuid: a7f2455b-1b09-41a7-817b-e2e7a1ff9936
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e83ed7b-3f48-4bf6-be4c-89f79949c1df
docset: aem65
exl-id: 674d28dc-7353-49de-9e12-b1998e1509c7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# 程式報告簡介{#introduction-to-process-reporting}

![程式報告](assets/process-reporting.png)

程式報告是一種基於瀏覽器的工具，可用於建立和檢視AEM Forms程式和任務的報告。

「程式報告」提供一組現成可用的報告，可讓您篩選、檢視長時間執行程式、程式持續時間和工作流程量的相關資訊。

此外，「程式報告」提供執行臨機查詢的介面，以及將自訂報告檢視整合到「程式報告」使用者介面中。

如需支援的瀏覽器清單，請參閱 [AEM Forms支援的平台](/help/forms/using/aem-forms-jee-supported-platforms.md).

程式報告會建置在符合以下條件的模組上：

* 從AEM Forms資料庫讀取程式資料
* 將程式資料發佈到內嵌的程式報告存放庫
* 提供瀏覽器式使用者介面以檢視報表

## 主要功能 {#key-capabilities}

### 永遠開啟的報表 {#always-on-reporting}

![網站管理](assets/site-management.png)

檢視長時間執行流程的清單、流程持續時間圖表，以及使用篩選器執行自訂查詢。

「程式報表」也提供將報表和查詢資料匯出為CSV格式的選項。

### 臨時報表 {#adhoc-reports}

![列印&amp; — 色彩](assets/print-&-colour.png)

使用篩選器以取得您資料的特定檢視。

您可以依ID、持續時間、開始和結束日期、流程發起者等搜尋流程或任務。

您可以結合多個篩選器以建立特定報表。

然後，您可以儲存報表篩選器，以供稍後日期或時間執行。

### 程式/任務歷史記錄 {#process-task-history}

![檔案管理](assets/file-management.png)

AEM Forms伺服器會同時執行多個程式。 這些程式會不斷從一種狀態轉換到另一種狀態。 透過定期將Forms資料發佈到Process Reporting存放庫， Process Reporting可保留AEM Forms中執行之程式的轉換資訊。

### 访问控制 {#access-control-br}

![未命名](assets/untitled.png)

「程式報告」提供對使用者介面的許可權型存取。

這表示只有具有報表許可權的使用者才能存取程式報表使用者介面。
