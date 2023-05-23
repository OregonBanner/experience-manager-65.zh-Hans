---
title: 無法還原適用於JEE叢集伺服器的損毀CRX存放庫
description: 還原損毀CRX存放庫的步驟
exl-id: 212f61f1-360f-4abe-b874-055ec65454c7
source-git-commit: c4f776b08cb8cc8c6eea78a3757735e063bec20c
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 2%

---

# 無法還原損毀的CRX存放庫 {#unable-to-restore-corrupt-crx-repository}

## 问题 {#issue}

對於使用關聯式資料庫的JEE版AEM Forms，主控AEM Forms和關聯式資料庫的電腦時間應一律絕對同步。 如果這些電腦上的時間不同步，JEE伺服器上AEM Forms的CRX存放庫可能會變得無法存取。 它可能已損毀，且無法透過URL存取。 此 `AuthenticationsupportService missing` 錯誤已記錄。

## 前提条件 {#prerequisites}

在執行下列步驟之前，請先備份CRX存放庫。

## 解决方案 {#solution}

執行以下步驟以解決問題：
1. 转到  `https://[AEM Forms Server]:[port]/system/console/bundles`.

1. 找到 `oak-core` 套件組合併檢查其是否正在執行。

1. 重新啟動 `oak-core` 套件組合未執行時套用。 若  ![暫停按鈕](/help/forms/using/assets/stop.png) 圖示出現在 `oak-core` 束，則表示該束處於執行狀態。

1. 如果問題仍未解決，請從備份中從CRX存放庫還原，或在備份不可用時重建CRX存放庫。


## 套用至 {#applies-to}

此解決方案適用於：

* JEE叢集上的AEM Forms