---
title: 旋转集
description: 瞭解如何在Dynamic Media中使用迴轉集
uuid: 379a20a3-6a17-499a-b0f1-3a835b97aa7b
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 8e9b3815-2893-4e6b-ac41-77720b42d56b
docset: aem65
feature: Spin Sets,Asset Management
role: User, Admin
exl-id: 758ad754-15de-4e72-9b7d-ab49c51d7d4f
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1952'
ht-degree: 8%

---

# 旋转集{#spin-sets}

「迴轉集」會模擬實際動作，即轉動物件來檢查它。 「迴轉集」可讓您從任何角度檢視專案，從任何角度獲得關鍵的視覺細節。

迴轉集可模擬360度的觀賞體驗。 Dynamic Media提供單軸迴轉集，檢視器可在此旋轉專案。 此外，使用者只要按一下滑鼠幾下，即可「自由變形」縮放及平移任何檢視。 透過這種方式，使用者可以從特定觀點更密切地檢查專案。

迴轉集由橫幅指定，並加上單字 **[!UICONTROL 迴轉集]**. 此外，如果已發佈迴轉集，則發佈日期(以 **[!UICONTROL World]** 圖示和上次修改日期位於橫幅上，由以下專案指示： **[!UICONTROL 鉛筆]** 圖示顯示。

![chlimage_1-](assets/chlimage_1-380.png)

>[!NOTE]
>
>如需Assets使用者介面的詳細資訊，請參閱 [管理資產](/help/assets/manage-assets.md).

當您建立迴轉集時，Adobe會建議下列最佳作法並強制實行下列限制：

| 限制型別 | 最佳實務 | 強制限制 |
| --- | --- | --- |
| 每個2D集的最大列數/欄數 | 每組12-18個影像 | 1000 |

另請參閱 [Dynamic Media限制](/help/assets/limitations.md).

## 快速入門：迴轉集 {#quick-start-spin-sets}

若要快速啟動並執行「迴轉集」，請遵循下列步驟：

1. [上傳您的影像以進行多次檢視](#uploading-assets-for-spin-sets).

   一維「迴轉集」至少需要8-12個專案快照，二維「迴轉集」至少需要16-24個專案快照。 拍攝必須定期進行，以提供專案正在旋轉和翻轉的印象。 例如，如果一維「迴轉集」包含12個鏡頭，則每個鏡頭應將專案旋轉30° (360/12)。

   另請參閱 [Dynamic Media — 支援的點陣影像格式](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media) 以取得迴轉集支援的格式清單。

1. [建立迴轉集](#creating-spin-sets).

   若要建立迴轉集，請選取 **[!UICONTROL 建立>迴轉集]** 然後命名該集合、選擇資產，並選擇影像的顯示順序。

   另請參閱 [使用選取器](/help/assets/working-with-selectors.md).

   >[!NOTE]
   >
   >您还可以通过[批量集预设](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)自动创建旋转集。**重要：** 批次集由IPS (Image Production System)建立，作為資產擷取的一部分，僅適用於Dynamic Media - Scene7模式。

1. 設定 [迴轉集檢視器預設集](/help/assets/managing-viewer-presets.md)，視需要而定。

   管理员可以创建或修改旋转集查看器预设。要查看带有查看器预设的旋转集，请选择旋转集，然后在左边栏下拉菜单中，选择&#x200B;**查看器**。

   另請參閱 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 檢視器預設集]** 如果您想要建立或編輯檢視器預設集。

   另請參閱 [新增和編輯檢視器預設集](/help/assets/managing-viewer-presets.md).

1. [檢視迴轉集](#viewing-spin-sets).

   您可以透過三種不同的方式，檢視和存取透過批次集預設集建立的集合。 (使用批次集預設集建立的集合，可以 *not* 出現在使用者介面中。)

1. [預覽迴轉集](/help/assets/previewing-assets.md).

   選取「迴轉集」，即可預覽。 旋轉迴轉集。 您可以從以下選擇不同的檢視器 **[!UICONTROL 檢視者]** 功能表，可從左側邊欄下拉式功能表取得。

1. [發佈迴轉集](/help/assets/publishing-dynamicmedia-assets.md).

   發佈迴轉集時會啟用URL和內嵌字串。 此外，您必須 [發佈檢視器預設集](/help/assets/managing-viewer-presets.md).

1. [將URL連結至您的網頁應用程式](/help/assets/linking-urls-to-yourwebapplication.md) 或 [內嵌視訊或影像檢視器](/help/assets/embed-code.md).

   Adobe Experience Manager資產會為迴轉集建立URL呼叫，並在您發佈迴轉集後啟用。 您可以在預覽資產時複製這些URL。 或者，您也可以將它們內嵌在網站上。

   选择旋转集，然后在左边栏下拉菜单中选择&#x200B;**[!UICONTROL 查看器]**。

   另請參閱 [將迴轉集連結至網頁](/help/assets/linking-urls-to-yourwebapplication.md) 和 [內嵌視訊或影像檢視器](/help/assets/embed-code.md).

如有需要，您可以 [編輯迴轉集](#editing-spin-sets). 此外，您也可以檢視和修改 [迴轉集屬性](/help/assets/manage-assets.md#editing-properties).

## 上傳迴轉集的資產 {#uploading-assets-for-spin-sets}

一維「迴轉集」至少需要8-12個專案快照，二維「迴轉集」至少需要16-24個專案快照。 拍攝必須定期進行，以提供專案正在旋轉和翻轉的印象。 例如，如果一維「迴轉集」包含12個鏡頭，則每個鏡頭應將專案旋轉30° (360/12)。

您可以像上傳一樣上傳迴轉集的影像 [在Experience Manager Assets中上傳任何其他資產](/help/assets/manage-assets.md).

另請參閱 [Dynamic Media — 支援的點陣影像格式](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media) 以取得迴轉集支援的格式清單。

### 擷取迴轉集影像的准則 {#guidelines-for-shooting-spin-set-images}

以下是有關迴轉集影像的一些最佳實務。 一般而言，「迴轉集」中的影像越多，影像旋轉效果就越好。 不過，在集合中包含許多影像也會增加影像載入所需的時間。 Experience Manager建議您在拍攝影像以用於「迴轉集」時，遵循下列准則：

* 在一維迴轉集中至少使用8-12個影像，在二維迴轉集中至少使用16-24個影像。 至少需要8個影像才能旋轉360度。 一維迴轉集較為常見，因為建立二維迴轉集需要大量人力。
* 使用無損格式；建議使用TIFF和PNG。
* 遮罩所有影像，讓專案出現在純白色或其他高對比的背景上。 選擇性地新增陰影。
* 請確定產品詳細資料都清楚標示且受到關注。
* 使用人體模型或模特拍攝時裝的旋轉影像。 通常，人體模型會被遮罩（使用玻璃人體模型），或是樣式化的人體模型/服裝模型會顯示在影像中。 您可以定義角度數來建立模型上的迴轉集。 在地面上用膠帶標籤每個角度，這樣您就可以引導模型步進，並檢視每個拍攝的方向。

## 建立迴轉集 {#creating-spin-sets}

本節說明如何以Experience Manager建立「迴轉集」。

>[!NOTE]
>
>您还可以通过[批量集预设](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)自动创建旋转集。**重要：** 批次集由IPS (Image Production System)建立，作為資產擷取的一部分，僅適用於Dynamic Media - Scene7模式。
>
>請參閱中的「建立批次集預設集以自動生成影像集和迴轉集」 [設定Dynamic Media - Scene7模式](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets).

>[!NOTE]
>
>影像在迴轉集中出現的順序很重要。 請務必加以排序，讓旋轉呈平滑的360°檢視。

當您建立迴轉集時，Adobe會建議下列最佳作法並強制實行下列限制：

| 限制型別 | 最佳實務 | 受限強制執行 |
| --- | --- | --- |
| 每個2D集的最大列數/欄數 | 每組12-18個影像 | 1000 |

另請參閱 [Dynamic Media限制](/help/assets/limitations.md).

**若要建立迴轉集：**

1. 在「資產」中，導覽至您要建立迴轉集的位置，然後選取 **[!UICONTROL 建立]**，並選取 **[!UICONTROL 迴轉集]**. 您还可以从包含资产的文件夹中创建旋转集。此时将显示旋转集编辑器。

   ![6_5_spinset-createpulldownmenu](assets/6_5_spinset-createpulldownmenu.png)

1. 在迴轉集編輯器中，於 **[!UICONTROL 標題]** 欄位，輸入迴轉集的名稱。 名稱會出現在整個迴轉集的橫幅中。 選擇性地輸入說明。

   ![6_5_spinset-spinseteditortitle](assets/6_5_spinset-spinseteditortitle.png)

   >[!NOTE]
   >
   >建立迴轉集時，您可以變更迴轉集縮圖，或允許Experience Manager根據迴轉集中的資產自動選取縮圖。 若要選取縮圖，請選取 **[!UICONTROL 變更縮圖]** 並選取任何影像（您也可以導覽至其他資料夾以尋找影像）。 如果您已選取縮圖，然後決定要讓Experience Manager從迴轉集產生縮圖，請選取 **[!UICONTROL 切換到自動縮圖]**.

1. 執行下列任一項作業：

   * 在「迴轉集編輯器」頁面的左上角附近，選取 **[!UICONTROL 新增資產]**.

   * 在「迴轉集編輯器」頁面中間附近，選取 **[!UICONTROL 點選以開啟資產選擇器]**.
   點選以選取您要納入迴轉集的資產。 选定资产上有一个复选标记图标。完成後，在頁面的右上角附近，選取 **[!UICONTROL 選取]**.

   借助资产选择器，您可以通过键入关键字并点按&#x200B;**[!UICONTROL 返回]**&#x200B;来搜索资产。您还可以应用过滤器来优化搜索结果。您可以按路径、收藏集、文件类型和标记进行过滤。選取篩選，然後選取 **[!UICONTROL 篩選]** 圖示加以檢視。 点按“视图”图标并选择&#x200B;**[!UICONTROL 列视图]**、**[!UICONTROL 卡片视图]**&#x200B;或&#x200B;**[!UICONTROL 列表视图]**&#x200B;可更改视图。

   另請參閱 [使用選取器](/help/assets/working-with-selectors.md).

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. 當您將資產新增至集時，資產會自動以英數字元順序新增。 在新增資產後，您可以手動重新排序或排序資產。

   如有必要，請將資產的「重新排序」圖示拖曳至資產檔案名稱的右側，以將影像重新排序至集清單的上方或下方。

   ![將迴轉集內的影格11拖曳至新位置，重新排序影格11](assets/6_5_spinset-reorderassets.png).

   在迴轉集中重新排序影格11，方法是將其拖曳到新位置。

1. （可選）執行下列任一項作業：

   * 若要刪除影像，請選取該影像，然後選取 **[!UICONTROL 刪除資產]**.

   * 若要套用預設集，在頁面右上角附近，選取 **[!UICONTROL 預設集]**，然後選取要一次套用至所有資產的預設集。

1. 选择&#x200B;**[!UICONTROL 保存]**。您新建立的「迴轉集」會顯示在您建立它的資料夾中。

## 檢視迴轉集 {#viewing-spin-sets}

您可以在使用者介面中建立迴轉集，或自動使用 [批次集預設集](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets). 不過，使用批次集預設集建立的集可以 *not* 顯示在使用者介面中。 您可以透過三種不同的方式，存取透過批次集預設集建立的集合。 （即使您在使用者介面中建立了迴轉集，仍可使用這些方法）。

>[!NOTE]
>
>您也可以透過使用者介面檢視集合，如中所述 [編輯迴轉集](#editing-spin-sets).

**若要檢視迴轉集：**

1. 開啟個別資產的屬性時。 屬性會指出所選資產所屬的集合(位於 **[!UICONTROL 集的成員]**)。 選取集合名稱，以便檢視整個集合。

   ![chlimage_1-156](assets/chlimage_1-384.png)

1. 来自任何集的成员图像。選取 **[!UICONTROL 集合]** 功能表，以顯示資產所屬的集合。

   ![chlimage_1-157](assets/chlimage_1-385.png)

1. 从搜索中，您可以选择&#x200B;**[!UICONTROL 过滤器]**，然后展开 **[!UICONTROL Dynamic Media]**，并选择&#x200B;**[!UICONTROL 集]**。

   搜尋會傳回在UI中手動建立或通過批次集預設集自動建立的相符集。 對於自動化集，搜尋查詢會使用下列專案來執行： `Starts with` 搜尋條件，不同於以使用為基礎的Experience Manager搜尋 `Contains` 搜尋條件。 將篩選設定為 **[!UICONTROL 集合]** 是搜尋自動化集的唯一方法。

   ![chlimage_1-158](assets/chlimage_1-386.png)

## 編輯迴轉集 {#editing-spin-sets}

您可以在「迴轉集」上執行各種編輯工作，例如：

* 新增影像至迴轉集。
* 重新排序迴轉集中的影像。
* 刪除迴轉集中的資產。
* 套用檢視器預設集。
* 刪除迴轉集。

**若要編輯迴轉集：**

1. 執行下列任一項作業：

   * 暫留在迴轉集資產上，然後選取「 」 **[!UICONTROL 編輯]** （鉛筆圖示）。
   * 暫留在迴轉集資產上，選取 **[!UICONTROL 選取]** （勾選圖示），然後選取 **[!UICONTROL 編輯]** （在工具列上）。

   * 在迴轉集資產上選取，然後選取 **[!UICONTROL 編輯]** （鉛筆圖示）。

1. 若要編輯「迴轉集」，請執行下列任一項作業：

   * 若要重新排序影像，請將影像拖曳至新位置（選取重新排序圖示以移動專案）。
   * 若要依遞增或遞減順序排序專案，請選取欄標題。
   * 若要新增資產或更新現有資產，請選取 **[!UICONTROL 新增資產]**. 導覽至資產，選取該資產，然後選取 **[!UICONTROL 選取]** 右上角附近。
如果您以其他影像取代來刪除Experience Manager用於縮圖的影像，則原始資產仍會顯示。
   * 若要刪除資產，請選取該資產並選取 **[!UICONTROL 刪除資產]**.
   * 若要套用預設集，請選取「預設集」圖示並選取預設集。
   * 若要刪除整個迴轉集，請導覽至「迴轉集」，選取它，然後選取 **[!UICONTROL 刪除]**

   >[!NOTE]
   >
   >您可以導覽至迴轉集並選取「 」，編輯迴轉集中的影像 **[!UICONTROL 設定成員]** ，然後選取個別資產上的「鉛筆」圖示以開啟編輯視窗。

1. 選取 **[!UICONTROL 儲存]** 完成編輯時。

## 預覽迴轉集 {#previewing-spin-sets}

另請參閱 [預覽資產](/help/assets/previewing-assets.md).

## 發佈迴轉集 {#publishing-spin-sets}

另請參閱 [發佈資產](/help/assets/publishing-dynamicmedia-assets.md).
