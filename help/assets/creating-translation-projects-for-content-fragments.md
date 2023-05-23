---
title: 建立內容片段的翻譯專案
seo-title: Creating Translation Projects for Content Fragments
description: 瞭解如何翻譯內容片段。
seo-description: Learn how to translate content fragments.
uuid: 23176e70-4003-453c-af25-6499a5ed3f6d
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: managing-assets
content-type: reference
discoiquuid: d2decc31-a04b-4a8e-bb19-65f21cf7107e
feature: Content Fragments
role: User, Admin
exl-id: 19bb58da-8220-404e-bddb-34be94a3a7d7
source-git-commit: 53c39e4aa250b18d4fae0327b313b18901677f2c
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 0%

---

# 建立內容片段的翻譯專案 {#creating-translation-projects-for-content-fragments}

除了資產外，Adobe Experience Manager (AEM) Assets還支援以下專案的語言複製工作流程： [內容片段](/help/assets/content-fragments/content-fragments.md) （包括變數）。 對內容片段執行語言複製工作流程不需要其他最佳化。 在每個工作流程中，會傳送整個內容片段以供翻譯。

您可以在內容片段上執行的工作流程型別與您為資產執行的工作流程型別完全類似。 此外，每個工作流程型別中可用的選項，與資產對應工作流程型別下可用的選項相符。

您可以在內容片段上執行下列型別的語言複製工作流程：

**创建并翻译**

在此工作流程中，要翻譯的內容片段會複製到您要翻譯之語言的語言根目錄。 此外，根據您選擇的選項，還會在專案主控台中為內容片段建立翻譯專案。 根據設定，翻譯專案可以手動啟動，或允許在建立翻譯專案後立即自動執行。

**更新语言副本**

更新或修改來源內容片段時，對應的地區設定/語言特定內容片段需要重新翻譯。 更新語言副本工作流程會翻譯額外的內容片段群組，並將其納入特定地區設定的語言副本中。 在這種情況下，翻譯的內容片段會新增到已經包含先前翻譯的內容片段的目標資料夾。

## 建立及翻譯工作流程 {#create-and-translate-workflow}

建立及翻譯工作流程包含下列選項。 與每個選項相關的程式步驟類似於與資產的相應選項相關的程式步驟。

* 僅建立結構：如需程式步驟，請參閱 [僅建立資產的結構](translation-projects.md#create-structure-only).
* 建立新的翻譯專案：如需程式步驟，請參閱 [建立資產的新翻譯專案](translation-projects.md#create-a-new-translation-project).
* 新增至現有翻譯專案：如需程式步驟，請參閱 [新增至資產的現有翻譯專案](translation-projects.md#add-to-existing-translation-project).

## 更新語言副本工作流程 {#update-language-copies-workflow}

更新語言副本工作流程包含以下選項。 與每個選項相關的程式步驟類似於與資產的相應選項相關的程式步驟。

* 建立新的翻譯專案：如需程式步驟，請參閱 [建立資產的新翻譯專案](translation-projects.md#create-a-new-translation-project) （更新工作流程）。
* 新增至現有翻譯專案：如需程式步驟，請參閱 [新增至資產的現有翻譯專案](translation-projects.md#add-to-existing-translation-project) （更新工作流程）。

您也可以建立片段的臨時語言副本，其方式與建立資產的臨時副本類似。 如需詳細資訊，請參閱 [建立資產的臨時語言副本](translation-projects.md#creating-temporary-language-copies).

## 翻譯混合媒體片段 {#translating-mixed-media-fragments}

AEM可讓您翻譯包含各種媒體資產和集合型別的內容片段。 如果您翻譯包含內嵌資產的內容片段，這些資產的翻譯副本會儲存在目標語言根下。

如果內容片段包含集合，則集合中的資產會與內容片段一起翻譯。 資產的翻譯復本會儲存在適當的目標語言根目錄中，且位置與來源語言根目錄下來源資產的實體位置相符。

若要能夠翻譯包含混合媒體的內容片段，請先編輯預設翻譯框架以啟用與內容片段相關聯的內嵌資產和集合的翻譯。

1. 按一下/點選AEM標誌，然後導覽至 **[!UICONTROL 「工具>部署>Cloud Services」]**.
1. 尋找 **[!UICONTROL 翻譯整合]** 在 **[!UICONTROL Adobe Marketing Cloud]**，然後按一下/點選 **[!UICONTROL 顯示設定]**.

   ![chlimage_1-444](assets/chlimage_1-444.png)

1. 在可用設定清單中，按一下/點選 **[!UICONTROL 預設設定（翻譯整合設定）]** 以開啟 **[!UICONTROL 預設設定]** 頁面。

   ![chlimage_1-445](assets/chlimage_1-445.png)

1. 按一下 **[!UICONTROL 編輯]** 以顯示 **[!UICONTROL 翻譯設定]** 對話方塊。

   ![chlimage_1-446](assets/chlimage_1-446.png)

1. 導覽至 **[!UICONTROL 資產]** 標籤，然後選擇 **[!UICONTROL 內嵌媒體資產和關聯的集合]** 從 **[!UICONTROL 翻譯內容片段資產]** 清單。 按一下/點選 **[!UICONTROL 確定]** 以儲存變更。

   ![chlimage_1-447](assets/chlimage_1-447.png)

1. 從英文根資料夾中，開啟內容片段。

   ![chlimage_1-448](assets/chlimage_1-448.png)

1. 按一下/點選 **[!UICONTROL 插入資產]** 圖示。

   ![chlimage_1-449](assets/chlimage_1-449.png)

1. 將資產插入內容片段。

   ![將資產插入內容片段](assets/column-view.png)

1. 按一下/點選 **[!UICONTROL 關聯內容]** 圖示。

   ![chlimage_1-451](assets/chlimage_1-451.png)

1. 按一下/點選 **[!UICONTROL 關聯內容]**.

   ![chlimage_1-452](assets/chlimage_1-452.png)

1. 選取一個集合併將其包含到內容片段中。 按一下/點選 **[!UICONTROL 儲存]**.

   ![chlimage_1-453](assets/chlimage_1-453.png)

1. 選取內容片段，然後按一下/點選 **[!UICONTROL GlobalNav]** 圖示。
1. 選取 **[!UICONTROL 引用]** 以顯示 **[!UICONTROL 引用]** 窗格。

   ![chlimage_1-454](assets/chlimage_1-454.png)

1. 按一下/點選 **[!UICONTROL 語言副本]** 在 **[!UICONTROL 份數]** 以顯示語言副本。

   ![chlimage_1-455](assets/chlimage_1-455.png)

1. 按一下/點選 **[!UICONTROL 建立並翻譯]** 從面板底部以顯示 **[!UICONTROL 建立並翻譯]** 對話方塊。

   ![chlimage_1-456](assets/chlimage_1-456.png)

1. 從中選擇目標語言 **[!UICONTROL 目標語言]** 清單。

   ![chlimage_1-457](assets/chlimage_1-457.png)

1. 從中選擇翻譯專案型別 **[!UICONTROL 專案]** 清單。

   ![chlimage_1-458](assets/chlimage_1-458.png)

1. 在中指定專案標題 **[!UICONTROL 專案標題]** 方塊，然後按一下/點選 **建立**.

   ![chlimage_1-459](assets/chlimage_1-459.png)

1. 導覽至 **[!UICONTROL 專案]** 控制檯中，並開啟您建立之翻譯專案的專案資料夾。

   ![chlimage_1-460](assets/chlimage_1-460.png)

1. 按一下/點選專案拼貼，以開啟專案詳細資訊頁面。

   ![chlimage_1-461](assets/chlimage_1-461.png)

1. 在「翻譯工作」動態磚中，驗證要翻譯的資產數量。
1. 從 **[!UICONTROL 翻譯工作]** 圖磚，開始翻譯工作。

   ![chlimage_1-462](assets/chlimage_1-462.png)

1. 按一下「翻譯工作」圖磚底部的省略符號，以顯示翻譯工作的狀態。

   ![chlimage_1-463](assets/chlimage_1-463.png)

1. 按一下/點選內容片段以檢查已翻譯關聯資產的路徑。

   ![chlimage_1-464](assets/chlimage_1-464.png)

1. 在「集合」控制檯中檢閱集合的語言副本。

   ![chlimage_1-465](assets/chlimage_1-465.png)

   請注意，只會翻譯集合的內容。 集合本身不會翻譯。

1. 導覽至翻譯的相關資產路徑。 請注意，翻譯的資產會儲存在目標語言根目錄下。

   ![chlimage_1-466](assets/chlimage_1-466.png)

1. 導覽至集合中隨內容片段一起翻譯的資產。 請注意，資產的翻譯副本會儲存在適當的目標語言根目錄中。

   ![chlimage_1-467](assets/chlimage_1-467.png)

   >[!NOTE]
   >
   >將內容片段新增至現有專案或執行更新工作流程的程式與資產的對應程式類似。 如需這些程式的指引，請參閱資產所述的程式。
