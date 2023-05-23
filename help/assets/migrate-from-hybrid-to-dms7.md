---
title: 從Dynamic Media — 混合模式移轉至Dynamic Media - S7模式
description: 瞭解如何將Dynamic Media — 混合模式執行個體移轉至Dynamic Media - S7模式
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
feature: Scene7 Mode,Hybrid Mode
exl-id: 07f0803c-4ec4-4745-8214-63370e9d0282
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 2%

---

# 關於從Dynamic Media-Hybrid移至Dynamic Media-Scene7 {#about-migrating}

Dynamic Media-Hybrid是Dynamic Media與Adobe Experience Manager整合的舊版本。 混合式版本最初是在Adobe Experience Manager 6.1中引入。雖然Adobe持續支援混合模式，但不是首選模式；首選使用Dynamic Media-Scene7模式。 混合模式也不支援智慧型裁切和全景影像等新功能，而Dynamic Media-Scene7則支援。

Dynamic Media-Hybrid和Dynamic Media-Scene7之間的其他主要差異包括：

* URL的結構。
* 影片擷取。
* 影像轉譯的建立和儲存。
* 雲端設定和認證（布建）。

從Dynamic Media-Hybrid移至Dynamic Media-Scene7時，有兩個選項可供使用。 第一個選項是直接在Experience Manager上布建新的Dynamic Media-Scene7執行個體。 第二個選項是將您現有的Dynamic Media-Hybrid執行個體移轉至Dynamic Media-Scene7。 此選項在下方以表格形式概述您在移動過程中要採取的步驟和考量事項。

>[!IMPORTANT]
>
>Adobe建議您不要在即時生產執行個體上將Dynamic Media-Hybrid實作移轉至Dynamic Media-Scene7。

## 選項1 — 在Experience Manager上布建新的Dynamic Media-Scene7執行個體 {#provision-new-dms7}

請考慮在Adobe Experience Manager上使用Dynamic Media-Scene7布建的全新例項，從頭開始。 除了透過Dynamic MediaCloud Service來擷取和處理資產外，強烈建議對資產使用情況、工作流程和元件進行Adobe稽核。 通常，您可以使用較新、現成可用的功能來取代自訂元件和工作流程。

## 選項2 — 將您現有的Dynamic Media-Hybrid執行個體移轉至Dynamic Media-Scene7 {#process-for-migrating}

| 步骤 | 任务 | 注意事项 |
|---|---|---|
| 1 | 複製Dynamic Media — 混合式製作例項。 | 維護您現有的Dynamic Media-Hybrid Author例項以供遞補用途，直到此移轉程式中的其餘步驟成功完成為止。 |
| 2 | 在Dynamic Media-Scene7模式中開始復製作者執行個體。 |  |
| 3 | 在Adobe Experience ManagerCloud Services中，使用Dynamic Media-Scene7憑證設定Dynamic Media。 | Adobe必須核准Dynamic Media-Scene7布建。 因此，您同時擁有受Adobe支援的Dynamic MediaM-Hybrid和Dynamic Media-Scene7環境，但僅限於有限時間。 |
| 4 | 建立移轉套裝，以便您視需要內嵌資產。<br>刪除初始擷取至Dynamic Media-Hybrid期間建立的本機PTIFF。 | 如果所有資產目前都可在Dynamic Media — 混合式執行個體中使用，則複製的已包含所有資產。 因此，不需要組合。 |
| 5 | 執行資產更新工作流程，讓您可以將資產同步至Dynamic MediaCloud Service。 | Adobe建議您以批次方式執行更新工作流程，以允許壓縮。 |
| 6 | 移轉檢視器、影像和視訊預設集。 |  |
| 7 | 瀏覽每個網頁內容管理參考的資產，並更新其關聯的URL。 |  |
| 8 | 移轉您要支援新Dynamic Media-Scene7模式的任何自訂工作流程（手動更新）。 |  |
| 9 | 驗證您的Web內容管理上傳和設定。 |  |
| 10 | 驗證後，取得停用Dynamic Media-Hybrid Author （以備援形式維護）的核准。 |  |
| 11 | 在成功使用Dynamic Media-Scene7約一個月後，刪除Dynamic Media-Hybrid Author例項。 |  |
