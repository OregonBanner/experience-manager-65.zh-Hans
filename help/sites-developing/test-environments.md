---
title: 需要哪些測試環境？
seo-title: Which Test Environments are needed?
description: 在測試中應考慮幾個環境
seo-description: Several environments should be considered as part of testing
uuid: bb725e50-edae-4c20-8107-d1c8df2e60e2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: db528b9b-3407-462d-8254-20b3cc2c3ccf
exl-id: 05f7a513-5ee7-4870-a691-4a0602e0cbb2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# 需要哪些測試環境？{#which-test-environments-will-be-needed}

若要定義要測試的設定，您應考量下列事項：

**開發**  — 適用於單位和某些整合測試。

**測試**  — 適用於大部分測試。

**即時**  — 進行最終效能與壓力測試。 也用於和客戶進行驗收測試。

您還需要決定您將在何處需要哪些執行個體（通常是所有測試層級至少各一個）：

**作者**  — 此例項可讓作者輸入及發佈內容。

**發佈**  — 此例項會以已發佈的形式顯示網站，以供訪客存取。

應結合Dispatcher進行測試。

最後，必須考量實際的硬體 — 任何效能測試都應在儘可能接近最終上線環境的設定上進行。 因此，我們也建議將Project Launch分割為：

**軟啟動**  — 減少可用性；可在實際生產環境中進行效能測試、調校和最佳化。

**硬式啟動**  — 完整可用性。
