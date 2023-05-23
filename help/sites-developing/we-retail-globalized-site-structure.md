---
title: 在We.Retail中嘗試全球化網站結構
seo-title: Trying out the Globalized Site Structure in We.Retail
description: 在We.Retail中嘗試全球化網站結構
seo-description: null
uuid: 5e5a809d-578f-4171-8226-cb65aa995754
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d674458c-d5f3-4dee-a673-b0777c02ad30
exl-id: e1de20b0-6d7a-4bda-b62f-c2808fd0af28
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---

# 在We.Retail中嘗試全球化網站結構{#trying-out-the-globalized-site-structure-in-we-retail}

We.Retail是以全球化網站結構建置，提供可即時複製至特定國家/地區網站的語言主版。 所有功能皆已開箱即用，可讓您實驗此結構和內建的翻譯功能。

## 正在試用 {#trying-it-out}

1. 從以下位置開啟網站主控台： **全域導覽 — >網站**.
1. 切換到欄檢視（如果尚未啟用）並選取We.Retail。 請注意範例國家/地區結構（瑞士、美國、法國等）以及語言母版。

   ![chlimage_1-87](assets/chlimage_1-87a.png)

1. 選取「瑞士」，並檢視該國家/地區的語言根目錄。 請注意，在這些根目錄下還沒有任何內容。

   ![chlimage_1-88](assets/chlimage_1-88a.png)

1. 切換到清單檢視，檢視國家/地區的語言副本都是即時副本。

   ![chlimage_1-89](assets/chlimage_1-89a.png)

1. 返回欄檢視，然後按一下「語言主版」，檢視含有內容的語言主版根目錄。 請注意，只有英文有內容。

   We.Retail未隨附任何翻譯內容，但結構和設定已準備就緒，可讓您示範翻譯服務。

   ![chlimage_1-90](assets/chlimage_1-90a.png)

1. 選取「英文主版」後，開啟 **引用** 邊欄並選取「 」 **語言副本**.

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. 勾選「 」旁的核取方塊 **語言副本** 標籤以選取所有語言副本。 在 **更新語言副本** 區域內，選取選項以 **建立新的翻譯專案**. 提供專案名稱，然後按一下 **更新**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. 系統會為每個語言翻譯建立一個專案。 在下檢視它們 **導覽 — >專案**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

1. 按一下德文，以檢視翻譯專案的詳細資料。 請注意，狀態顯示為 **草稿**. 若要使用Microsoft的翻譯服務開始翻譯，請按一下 **翻譯工作** 標題並選取 **開始**.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. 翻譯專案隨即開始。 按一下標示為翻譯工作的卡片底部的省略符號以檢視詳細資訊。 具有狀態的頁面 **準備好審查** 已由翻譯服務翻譯。

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. 選取清單中的其中一個頁面，然後 **在網站中預覽** 在工具列中開啟頁面編輯器中的翻譯頁面。

   ![chlimage_1-96](assets/chlimage_1-96.png)

>[!NOTE]
>
>此程式展示與Microsoft機器翻譯的內建整合。 使用 [AEM翻譯整合架構](/help/sites-administering/translation.md)，您可以整合許多標準翻譯服務，以策劃AEM的翻譯。

## 更多信息 {#further-information}

如需進一步資訊，請參閱撰寫檔案 [翻譯多語言網站的內容](/help/sites-administering/translation.md) 以取得完整的技術細節。
