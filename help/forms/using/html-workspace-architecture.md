---
title: AEM Forms工作區架構
seo-title: AEM Forms Workspace Architecture
description: LiveCycleAEM Forms工作區架構的概念資訊和概觀。
seo-description: Conceptual information and overview of the architecture of LiveCycle AEM Forms workspace.
uuid: e1a48452-ed44-4ea7-ba38-d961c8faafa5
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c3a312fb-f684-477d-916d-2d3c99aa7607
exl-id: c6f216d4-781c-4356-b9f0-3324903a28e7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# AEM Forms工作區架構 {#aem-forms-workspace-architecture}

AEM Forms工作區是在CRX™上託管的網頁應用程式。 在瀏覽器中開啟工作區時，會存取CRX資源，並將應用程式呈現為瀏覽器中的HTML頁面。

應用程式在REST端點上存取AEM Forms伺服器，以執行下列動作：

* 擷取使用者工作、程式起點、程式歷史記錄和使用者資訊
* 對任務執行動作
* 查詢資料庫中的工作
* 更新使用者偏好設定等

AEM Forms伺服器會透過JDBC存取AEM Forms資料庫。 資料庫會儲存任務、流程及其執行個體、使用者和相關資訊。

AEM Forms工作區設計為模組化JavaScript™元件，可個別自訂並重複用於其他網頁應用程式。 這些元件以BackBone為基礎，這是JavaScript程式庫，為Web應用程式提供結構。 說明元件與BackBone互動的詳細文章為 [此處](/help/forms/using/backbone-interaction.md). CRX資料夾結構中元件的組織方式將在中討論。 [此](/help/forms/using/folder-structure.md) 文章。

為AEM Forms工作區提供的套件：

* `adobe-lc-workspace-pkg-<version>.zip`：它是CRX套件，也就是說，可以使用套件管理器在CRX中部署。
* `adobe-lc-workspace-<version>-src.zip`：此封存包含AEM Forms工作區的完整程式碼和建立部署套件的指令碼 — 出貨、除錯和開發套裝。
