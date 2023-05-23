---
title: 管理具有參考資料和多頁面的複合資產
description: 瞭解如何從內建立數位資產的參考 [!DNL Adobe InDesign]， [!DNL Adobe Illustrator]、和 [!DNL Adobe Photoshop]. 使用「頁面檢視器」功能可檢視多頁檔案的個別子資產頁面，例如PDF、INDD、PPT、PPTX和AI檔案。
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: 1ea9d8fe-602c-452b-9a24-4125b705aedf
source-git-commit: 79d8b5896f5f8eb7a22dccea81acf0656d435f2b
workflow-type: tm+mt
source-wordcount: '1424'
ht-degree: 0%

---

# 管理複合和多頁資產 {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] 可識別上傳的檔案是否包含已存在於存放庫中的資產參考。 此功能僅適用於支援的檔案格式。 如果上傳的資產包含任何參考 [!DNL Experience Manager] 資產，則會在上傳和參照的資產之間建立雙向連結。

除了消除備援外，請參考中的資產 [!DNL Adobe Creative Cloud] 應用程式可加強協同合作，並提升使用者的效率和生產力。

[!DNL Experience Manager Assets] 支援雙向參照。 您可以在上傳檔案的資產詳細資訊頁面中找到引用的資產。 此外，您還可以在參照資產的資產詳細資訊頁面中檢視參照檔案。

參照是根據參照資產的路徑、檔案ID和執行個體ID來解析。

## [!DNL Adobe Illustrator]：新增數位資產作為參考 {#refai}

您可以從中參考現有的數位資產 [!DNL Adobe Illustrator] 檔案。

1. 使用 [[!DNL Experience Manager] 案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)，在本機檔案系統上擷取數位資產。 導覽至您要參考之資產的檔案系統位置。
1. 將資產從本機資料夾拖曳至 [!DNL Illustrator] 檔案。

1. 儲存 [!DNL Illustrator] 檔案到掛載的磁碟機，或 [上傳](/help/assets/manage-assets.md#uploading-assets) 至 [!DNL Experience Manager] 存放庫。

1. 工作流程完成後，前往資產的資產詳細資訊頁面。 現有數位資產的參考資料列於 **[!UICONTROL 相依性]** 在 **[!UICONTROL 引用]** 欄。

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. 顯示在下方的參考資產 **[!UICONTROL 相依性]** 也可以由目前檔案以外的檔案參照。 若要檢視資產的參考檔案清單，請按一下下方中的資產 **[!UICONTROL 相依性]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. 按一下 **[!UICONTROL 檢視屬性]** （從工具列）。 在 [!UICONTROL 屬性] 頁面，參照目前資產的檔案清單會出現在 **[!UICONTROL 引用]** 中的欄 **[!UICONTROL 基本]** 標籤。

   ![在資產詳細資訊的「參考」欄中檢視Experience Manager Assets的參考](assets/asset-references.png)

   *圖：資產詳細資料中的資產參考。*

## [!DNL Adobe InDesign]：新增數位資產作為參考 {#add-aem-assets-as-references-in-adobe-indesign}

若要從內部參照數位資產 [!DNL InDesign] 檔案，將資產拖曳至 [!DNL InDesign] 檔案或匯出 [!DNL InDesign] 壓縮封存檔的檔案。

引用的資產已存在於 [!DNL Experience Manager Assets]. 您可以透過以下方式擷取子資產： [設定InDesign Server](indesign.md). 中的內嵌資產 [!DNL InDesign] 檔案會擷取為子資產。

>[!NOTE]
>
>如果 [!DNL InDesign Server] 已代理， [!DNL InDesign] 檔案的XMP中繼資料中內嵌其預覽。 在此情況下，不會明確要求縮圖擷取。 但是，如果 [!DNL InDesign Server] 並未進行代理，必須明確擷取縮圖 [!DNL InDesign] 檔案。

上傳INDD檔案時，會透過查詢具有以下特徵的資產來擷取參考： `xmpMM:InstanceID` 和 `xmpMM:DocumentID` 屬性存放庫中。

### 透過拖曳資產建立引用 {#create-references-by-dragging-aem-assets}

此程式類似於 [在Adobe Illustrator中新增數位資產作為參考](#refai).

### 透過匯出ZIP檔案來建立資產的參考 {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. 執行以下步驟： [建立工作流程模型](/help/sites-developing/workflows-models.md) 以建立新的工作流程。
1. 使用 [封裝功能](https://helpx.adobe.com/indesign/how-to/indesign-package-files-for-handoff.html) 之 [!DNL Adobe InDesign] 以匯出檔案。 [!DNL Adobe InDesign] 可將檔案和連結的資產匯出為套件。 在此案例中，匯出的資料夾包含 `Links` 包含子資產的資料夾 [!DNL InDesign] 檔案。 此 `Links` 資料夾與INDD檔案位於相同的資料夾中。
1. 建立ZIP檔案並將其上傳至 [!DNL Experience Manager] 存放庫。
1. 開始 `Unarchiver` 工作流程。
1. 工作流程完成時，連結資料夾中的參照會自動參照為子資產。 若要檢視引用的資產清單，請導覽至 [!DNL InDesign] 資產並關閉 [邊欄](/help/sites-authoring/basic-handling.md#rail-selector).

## [!DNL Adobe Photoshop]：新增數位資產作為參考 {#refps}

1. 使用 [!DNL Experience Manager] 要存取的案頭應用程式 [!DNL Experience Manager Assets]. 下載並顯示本機檔案系統上的資產。 使用 [!UICONTROL 置入已連結] 中的功能 [!DNL Adobe Photoshop]. 另請參閱 [將資產放入案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents).

1. 儲存於 [!DNL Photoshop] 檔案到已掛載的磁碟機或 [上傳](/help/assets/manage-assets.md#uploading-assets) 至 [!DNL Experience Manager] 存放庫。
1. 工作流程完成後，參考至現有的 [!DNL Experience Manager] 資產會列在資產詳細資訊頁面中。

   若要檢視參照的資產，請關閉 [邊欄](/help/sites-authoring/basic-handling.md#rail-selector) （在資產詳細資訊頁面中）。

1. 引用的資產也包含從中引用它們的資產清單。 若要檢視參照的資產清單，請導覽至資產詳細資訊頁面並關閉 [邊欄](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>複合資產中的資產也可以根據其檔案ID和例項ID進行引用。 此功能適用於 [!DNL Adobe Illustrator] 和 [!DNL Adobe Photoshop] 僅限版本。 對於其他人，會根據主要複合資產中連結資產的相對路徑進行引用，如同在舊版中做的那樣 [!DNL Experience Manager].

## 建立子資產 {#generate-subassets}

對於支援的多頁格式資產 — PDF檔案、AI檔案、 [!DNL Microsoft PowerPoint] 和 [!DNL Apple Keynote] 檔案，和 [!DNL Adobe InDesign] 檔案 —  [!DNL Experience Manager] 可以產生與原始資產的每個個別頁面相對應的子資產。 這些子資產連結至 *父級* 資產並加速多頁檢視。 至於所有其他用途，會將子資產視為中的一般資產 [!DNL Experience Manager].

子資產產生功能預設為停用。 若要啟用子資產產生功能，請遵循下列步驟：

1. 登入 [!DNL Experience Manager] 作為管理員。 存取 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**.
1. 選取 **[!UICONTROL DAM更新資產]** 工作流程與點按 **[!UICONTROL 編輯]**.
1. 按一下 **[!UICONTROL 切換側面板]** 並找到 **[!UICONTROL 建立子資產]** 步驟。 將步驟新增至工作流程。 单击&#x200B;**[!UICONTROL 同步]**。

若要產生子資產，請執行下列任一項作業：

* 新資產： [!UICONTROL DAM更新資產] 工作流程會在任何上傳至的新資產上執行 [!DNL Experience Manager]. 系統會自動為新多頁資產產生子資產。
* 現有的多頁資產：手動執行 [!UICONTROL DAM更新資產] 工作流程會遵循下列任一步驟：

   * 選取資產並按一下 [!UICONTROL 時間表] 以開啟左側面板。 或者，使用鍵盤快速鍵 `alt + 3`. 按一下 [!UICONTROL 開始工作流程]，選取 [!UICONTROL DAM更新資產]，按一下 [!UICONTROL 開始]，然後按一下 [!UICONTROL 繼續].
   * 選取資產並按一下 [!UICONTROL 建立] > [!UICONTROL 工作流程] （從工具列）。 在快顯對話方塊中，選取 [!UICONTROL DAM更新資產] 工作流程，按一下 [!UICONTROL 開始]，然後按一下 [!UICONTROL 繼續].

特別是對於Microsoft Word檔案，請執行 **[!UICONTROL DAM剖析Word檔案]** 工作流程。 它會產生 `cq:Page` Microsoft Word檔案內容中的元件。 從檔案擷取的影像會參照自 `cq:Page` 元件。 即使停用子資產產生，也會擷取這些影像。

>[!NOTE]
>
>在 [!UICONTROL 建立子資產程式 — 步驟屬性] 在 [!UICONTROL 程式引數]，您可以指定達到以下條件的子資產數量： [!DNL Experience Manager] 會產生。 默认值为 5。若要產生所有子資產，請將此欄位留空。 如果欄位包含負值，則不會產生任何子資產。

## 檢視子資產 {#viewing-subassets}

只有在產生子資產且可用於所選的多頁資產時，才會顯示子資產。 若要檢視產生的子資產，請開啟多頁資產。 在頁面的左上角區域，按一下 ![開啟左側邊欄的選項](assets/do-not-localize/aem_leftrail_contentonly.png) 並按一下 **[!UICONTROL 子資產]** 從清單中。 當您選取 **[!UICONTROL 子資產]** 從清單中。 或者，使用鍵盤快速鍵 `alt + 5`.

![檢視多頁資產的子資產](assets/view_subassets_simulation.gif)

## 檢視多頁檔案的頁面 {#view-pages-of-a-multi-page-file}

您可以使用以下的「頁面檢視器」功能來檢視多頁檔案，例如PDF、INDD、PPT、PPTX和AI檔案： [!DNL Experience Manager Assets]. 開啟多頁資產並按一下 **[!UICONTROL 檢視頁面]** 從頁面的左上角。 開啟的頁面檢視器會顯示資產的頁面，以及用來瀏覽和縮放每個頁面的控制項。

![檢視和檢視多頁資產的頁面](assets/view_multipage_asset_fmr.gif)

對象 [!DNL InDesign]，您可以使用以下專案擷取頁面： [!DNL InDesign Server]. 如果頁面的預覽是在以下期間儲存： [!DNL InDesign] 建立檔案，然後 [!DNL InDesign Server] 不須用於頁面擷取。

工具列、左側邊欄及「頁面檢視器」控制項中有以下選項：

* **[!UICONTROL 案頭動作]** 若要開啟或顯示特定子資產，請使用 [!DNL Experience Manager] 案頭應用程式。 瞭解如何 [設定案頭動作](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2) 如果您使用 [!DNL Experience Manager] 案頭應用程式。

* **[!UICONTROL 屬性]** 選項會開啟 [!UICONTROL 屬性] 特定子資產的頁面。

* **[!UICONTROL 註釋]** 選項可讓您為特定子資產加上註釋。 您用於個別子資產的註解會在父資產開啟以供檢視時一起收集和顯示。

* **[!UICONTROL 頁面概觀]** 選項會同時顯示所有子資產。

* **[!UICONTROL 時間表]** 選項（在按一下後從左側邊欄選取） ![開啟左側邊欄的選項](assets/do-not-localize/aem_leftrail_contentonly.png) 顯示檔案的活動資料流。

## 最佳作法和限制 {#best-practice-limitation-tips}

* 在任何專案上，產生子資產可能會耗費大量資源 [!DNL Experience Manager] 部署。 如果您在上傳複雜資產時產生子資產，請在「DAM更新資產」工作流程中新增步驟。 如果您要隨選產生子資產，請建立個別的工作流程以產生子資產。 專用工作流程可讓您略過DAM更新資產工作流程中的其他步驟，並儲存運算資源。

>[!MORELIKETHIS]
>
>* [使用Adobe Experience Manager案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [在Adobe Experience Manager中設定案頭動作](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [在Adobe Photoshop中建立連結智慧物件](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [在Adobe InDesign中置入圖形](https://helpx.adobe.com/indesign/using/placing-graphics.html)

