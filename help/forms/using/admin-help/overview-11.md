---
title: 健康情況監視概觀
seo-title: Overview of Health Monitor
description: 本檔案提供健康情況監視器的概觀，以及有關如何存取它的詳細資訊。
seo-description: This document provides the overview of the Health monitor, and details about how you can access it.
uuid: 5934fd2d-80a5-4c6d-b3ee-882c2865705b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c303e967-944d-40b0-96ca-f91e2f42a0d0
exl-id: 05f8b430-141e-4921-98b1-a0d8f636e478
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# 健康情況監視概觀 {#overview-of-health-monitor}

健康狀態監視器提供有關AEM表單系統的重要資訊，例如伺服器資訊、記憶體使用量和處理器使用量。 也可以使用Work Manager統計資料，例如工作專案或工作在佇列中的數量及其狀態。 您可以使用「健康情況監視器」執行下列工作：

* 確認您的系統正在正確執行
* 檢視資訊以協助診斷系統問題
* 對顯示問題的工作專案或工單執行作業
* 從「工作管理員」資料庫中永久刪除過時記錄

Administration Console中的「健康情況監視」頁面有三個頁簽：

* 「系統」標籤會顯示資源監督圖表以及表單伺服器（或叢集環境中的節點）的相關資訊。 (請參閱 [檢視系統資訊](/help/forms/using/admin-help/view-system-information.md#view-system-information).)
* 「工作管理員」標籤會顯示與「工作管理員」相關的資料，例如「工作管理員」佇列中的工作專案數。 您可以使用各種條件篩選資訊，或使用作業工具管理個別工作專案。 (請參閱 [檢視與工作管理員相關的統計資料](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)
* 您可以使用「工作永久刪除排程器」頁標從「工作管理員」資料庫永久刪除過時的記錄。 (請參閱 [從「工作管理員」資料庫中清除記錄](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)

健康情況監視網頁會填入透過Gemfire API收集的統計資料。 此API會自動探索叢集中的所有節點。 它也能解決從Proxy伺服器或負載平衡器後面收集統計資料時發生的安全性問題。 Java選項可用於微調健康情況監視器，減少對AEM表單環境效能的影響。 (請參閱 [微調健康狀態監視器效能](/help/forms/using/admin-help/fine-tuning-health-monitor-performance.md#fine-tuning-health-monitor-performance).)

**存取狀況監視器**

1. 在管理控制檯中，按一下頁面右上角的「健全狀況監視器」 。
