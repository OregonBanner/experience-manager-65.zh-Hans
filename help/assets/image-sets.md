---
title: 图像集
description: 瞭解如何在Dynamic Media中使用影像集
uuid: ca2fd5b0-656e-4960-b10c-f0ec3d418760
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: ccc4eb23-934c-4e67-860b-a6faa2bcaafc
docset: aem65
feature: Image Sets,Asset Management
role: User, Admin
exl-id: 2a536745-fa13-4158-8761-2ac5b6e1893e
source-git-commit: d83a647d8ac5466ba09230c584d5d501aab55274
workflow-type: tm+mt
source-wordcount: '2184'
ht-degree: 7%

---

# 图像集 {#image-sets}

影像集為使用者提供整合式檢視體驗，使用者可透過選取縮圖影像來檢視專案的不同檢視。 「影像集」可讓您呈現專案的替代檢視，而檢視器則提供縮放工具，讓您更密切地檢查影像。

影像集由帶有單字的橫幅指定 `IMAGESET`. 此外，如果图像集已发布，则横幅上会显示由 **[!UICONTROL World]** 图标指示的发布日期以及由铅笔图标指示的上次修改日期 **** 。

![图像集](assets/chlimage_1-339.png)

在「影像集」中，您也可以建立「影像集」並新增縮圖，以建立色票。

當您想要以不同的顏色、圖樣或成品顯示專案時，此應用程式非常有用。 若要建立包含色票的「影像集」，您需要為要呈現給使用者的每個不同顏色、圖樣或完成使用一個影像。 您還需要一個顏色、圖樣或精加工色票，用於每一個顏色、圖樣或精加工。

例如，假設您想要呈現不同顏色的紙幣的帽子影像；紙幣為紅色、綠色和藍色。 在此情況下，您需要三個相同帽子的鏡頭。 您需要一張紅底片、一張綠底片以及一張藍底片。 您也需要紅色、綠色和藍色色票。 顏色色票可作為縮圖，供使用者在色票集檢視器中選取，以檢視紅色計費、綠色計費或藍色計費上限。

>[!NOTE]
>
>如需Assets使用者介面的詳細資訊，請參閱 [管理資產](/help/assets/manage-assets.md).

建立影像集時，Adobe會建議下列最佳作法並強制實行下列限制：

| 限制型別 | 最佳實務 | 強制限制 |
| --- | --- | --- |
| 每個集的重複資產數量 | 無重複專案 | 20 |
| 每組影像的最大數量 | 每組5至10個影像 | 1000 |

另請參閱 [Dynamic Media限制](/help/assets/limitations.md).

## 快速入門：影像集 {#quick-start-image-sets}

**快速上手並執行：**

1. [上傳您的主要來源影像以供多個檢視](#uploading-assets-in-image-sets).

   首先，上傳影像集的影像。 當您選擇影像時，請記得您的客戶可以在影像集檢視器中放大影像。 請確定影像在最大尺寸中至少為2000畫素，以獲得最佳縮放細節。 Dynamic Media可轉譯每個高達2500萬畫素(megapixel)的影像。 例如，您可以使用5000 x 5000 MP影像或任何其他大小組合，最大可達25 MP。

   另請參閱 [Dynamic Media — 支援的點陣影像格式](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media) 以取得「影像集」支援的格式清單。

<!--    Adobe Experience Manager Assets supports many image file formats, but lossless TIFF, PNG, and EPS images are recommended. -->

1. [建立影像集](#creating-image-sets).

   在「影像集」中，使用者可在「影像集檢視器」中選取縮圖影像。

   若要在「資產」中建立影像集，請前往 **[!UICONTROL 建立]** > **[!UICONTROL 影像集]**. 然後，新增影像並選取 **[!UICONTROL 儲存]**.

   您也可以透過自動建立影像集 [批次集預設集](/help/assets/config-dms7.md).
   >[!IMPORTANT]
   >
   >批次集由IPS (Image Production System)建立，作為資產擷取的一部分，僅適用於Dynamic Media - Scene7模式。

   另請參閱 [準備影像集資產以上傳和上傳您的檔案](#uploading-assets-in-image-sets).

   另請參閱 [使用選取器](/help/assets/working-with-selectors.md).

1. 新增 [影像集檢視器預設集](/help/assets/managing-viewer-presets.md)，視需要而定。

   管理員可以建立或修改影像集檢視器預設集。 若要檢視含有檢視器預設集的影像集，請選取「影像集」，然後在左側導軌下拉式選單中選取 **[!UICONTROL 檢視者]**.

   導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 檢視器預設集]** 如果您想要建立或編輯檢視器預設集。

1. （可選） [檢視影像集](/help/assets/image-sets.md#viewing-image-sets) 使用批次集預設集建立的。
1. [預覽影像集](/help/assets/previewing-assets.md).

   選取「影像集」，即可預覽。 選取縮圖圖示，以便在選取的檢視器中檢查影像集。 您可以從以下選擇不同的檢視器 **[!UICONTROL 檢視者]** 功能表，可從左側邊欄下拉式功能表取得。

1. [發佈影像集](/help/assets/publishing-dynamicmedia-assets.md).

   發佈影像集時會啟用URL和內嵌程式碼。 此外，您必須 [發佈任何自訂檢視器預設集](/help/assets/managing-viewer-presets.md) 您已建立的。 現成的檢視器預設集已發佈。

1. [將URL連結至您的網頁應用程式](/help/assets/linking-urls-to-yourwebapplication.md) 或 [內嵌視訊或影像檢視器](/help/assets/embed-code.md).

   Experience Manager Assets會為影像集建立URL呼叫，並在您發佈影像集後將其啟用。 您可以在預覽資產時複製這些URL。 或者，您也可以將它們內嵌在網站上。

   选择图像集，然后在左边栏下拉菜单中选择&#x200B;**[!UICONTROL 查看器]**。

   另請參閱 [將影像集連結至網頁](/help/assets/linking-urls-to-yourwebapplication.md) 和 [內嵌視訊或影像檢視器](/help/assets/embed-code.md).

若要編輯影像集，請參閱 [編輯影像集](#editing-image-sets). 此外，您也可以檢視和編輯 [影像集屬性](/help/assets/manage-assets.md#editing-properties).

如果您無法建立集合，請參閱影像和集合，位置如下： [疑難排解Dynamic Media - Scene7模式](/help/assets/troubleshoot-dms7.md#images-and-sets).

## 上傳影像集中的資產 {#uploading-assets-in-image-sets}

首先，上傳影像集的影像。 當您選擇影像時，請記得您的客戶可以在影像集檢視器中放大影像。 确保图像的最大尺寸至少为2000像素。影像集支援許多影像檔案格式，但建議使用不失真TIFF、PNG和EPS影像。

您可以依原樣上傳影像集的影像 [上傳資產中的任何其他資產](/help/assets/manage-assets.md#uploading-assets).

另請參閱 [Dynamic Media — 支援的點陣影像格式](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media) 以取得「影像集」支援的格式清單。

### 準備影像集資產以供上傳 {#preparing-image-set-assets-for-upload}

在建立影像集之前，請確定影像的大小和格式正確。

若要建立多檢視影像集，您需要顯示不同檢視點專案的影像，或顯示同一專案的不同方面。 目標是要強調專案的重要功能，讓檢視者能完整瞭解專案外觀或作用。

由於使用者可以在「影像集」中縮放影像，因此請確定影像在最大維度中至少為2000畫素。 <!-- Assets support many image file formats, but lossless TIFF, PNG, and EPS images are recommended. -->

>[!NOTE]
>
>此外，如果您使用縮圖來表示產品色票，則必須執行下列動作：
>
>您需要相同影像的暈映或不同快照，以不同的顏色、圖樣或完成顯示影像。 您還需要對應不同顏色、圖樣或筆畫的縮圖檔案。 例如，若要呈現縮圖，且「影像集」以黑色、棕色和綠色顯示相同夾克，您需要：
>
>* 同一件夾克的黑色、棕色和綠色照片。
>* 黑色、棕色和綠色的縮圖。


## 建立影像集 {#creating-image-sets}

您可以透過使用者介面或API建立影像集。 本節說明如何在UI中建立影像集。

>[!NOTE]
>
>您也可以透過自動建立影像集 [批次集預設集](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets).
>**重要：** 批次集由IPS (Image Production System)建立，作為資產擷取的一部分，僅適用於Dynamic Media - Scene7模式。

當您將資產新增至集時，資產會自動以英數字元順序新增。 在新增資產後，您可以手動重新排序或排序資產。

>[!NOTE]
>
>檔案名稱中有「，」（逗號）的資產不支援影像集。

建立影像集時，Adobe會建議下列最佳作法並強制實行下列限制：

| 限制型別 | 最佳實務 | 強制限制 |
| --- | --- | --- |
| 每個集的重複資產數量 | 無重複專案 | 20 |
| 每組影像的最大數量 | 每組5至10個影像 | 1000 |

另請參閱 [Dynamic Media限制](/help/assets/limitations.md).

**若要建立影像集：**

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台，然後前往 **[!UICONTROL 導覽]** > **[!UICONTROL 資產]**. 導覽至您要建立影像集的位置，然後前往 **[!UICONTROL 建立]** > **[!UICONTROL 影像集]** 以開啟「影像集編輯器」頁面。

   您还可以从包含资产的文件夹中创建旋转集。

   ![6_5_imagesets-createpulldown](assets/6_5_imagesets-createpulldown.png)

1. 在「影像集編輯器」頁面的 **[!UICONTROL 標題]** 欄位，輸入影像集的名稱。 該名稱會出現在影像集的橫幅中。 選擇性地輸入說明。

   ![6_5_imageset-creatingnewset](assets/6_5_imageset-creatingnewset.png)

1. 執行下列任一項作業：

   * 在「影像集編輯器」頁面的左上角附近，選取 **[!UICONTROL 新增資產]**.

   * 在「影像集編輯器」頁面中間附近，選取 **[!UICONTROL 點選以開啟資產選擇器]**.
   選取您要包含在影像集中的資產。 选定资产上有一个复选标记图标。完成後，在頁面的右上角附近，選取 **[!UICONTROL 選取]**.

   借助资产选择器，您可以通过键入关键字并点按或单击&#x200B;**[!UICONTROL 返回]**&#x200B;来搜索资产。您还可以应用过滤器来优化搜索结果。您可以按路径、收藏集、文件类型和标记进行过滤。選取篩選，然後選取 **[!UICONTROL 篩選]** 圖示加以檢視。 点按“视图”图标并选择&#x200B;**[!UICONTROL 列视图]**、**[!UICONTROL 卡片视图]**&#x200B;或&#x200B;**[!UICONTROL 列表视图]**&#x200B;可更改视图。

   另請參閱 [使用選取器](/help/assets/working-with-selectors.md).

   ![6_5_imageset-addingassets](assets/6_5_imageset-addingassets.png)

1. 當您將資產新增至集時，資產會自動以英數字元順序新增。 在新增資產後，您可以手動重新排序或排序資產。

   如有必要，請將資產的「重新排序」圖示拖曳至資產檔案名稱的右側，以將影像重新排序至集清單的上方或下方。

   ![6_5_imageset-reorderassets](assets/6_5_imageset-reorderassets.png)

   如果您想要變更縮圖或色票，請選取 **+** **縮圖** 圖示並導覽至您想要的縮圖或色票。 選取完所有影像後，請選取 **[!UICONTROL 儲存]**.

1. （可選）執行下列任一項作業：

   * 若要刪除影像，請選取該影像，然後選取 **[!UICONTROL 刪除資產]**.

   * 若要套用預設集，在頁面右上角附近，選取 **[!UICONTROL 預設集]**，然後選取要一次套用至所有資產的預設集。
   >[!NOTE]
   >
   >建立影像集時，您可以變更影像集縮圖，或允許Experience Manager根據影像集中的資產自動選取縮圖。 若要選取縮圖，請選取 **[!UICONTROL 變更縮圖]** 在「影像集編輯器」頁面的「標題」欄位上方，然後選取任何影像（您也可以導覽至其他資料夾以尋找影像）。 如果您已選取縮圖，然後決定要讓Experience Manager從影像集產生縮圖，請選取 **[!UICONTROL 切換至]** > **[!UICONTROL 自動縮圖]**.

1. 选择&#x200B;**[!UICONTROL 保存]**。您新建立的影像集會顯示在您建立它的資料夾中。

## 檢視影像集 {#viewing-image-sets}

您可以在使用者介面中建立影像集，或自動使用 [批次集預設集](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets).

>[!IMPORTANT]
>
>批次集由IPS建立 [影像生產系統] 做為資產擷取的一部分，僅適用於Dynamic Media - Scene7模式。)

不過，使用批次集預設集建立的集可以 *not* 顯示在使用者介面中。 您可以使用三種不同的方式檢視這些集合。 （即使您在使用者介面中建立了影像集，這些方法仍可使用）。

* 開啟個別資產的屬性。 屬性會指出所選資產被參考或為其成員的設定。 如果要檢視整個集合，請選取集合的名稱。

   ![6_5_imageset-assetproperties](assets/6_5_imageset-assetproperties2.png)

* 来自任何集的成员图像。選取 **[!UICONTROL 集合]** 功能表，以顯示資產所屬的集合。

   ![6_5_imageset-setspulldownmenu](assets/6_5_imageset-setspulldownmenu.png)

* 在搜尋中，您可以選取 **[!UICONTROL 篩選]**，然後展開 **[!UICONTROL Dynamic Media]** 並選取 **[!UICONTROL 集合]**.

   搜尋會傳回在UI中手動建立或通過批次集預設集自動建立的相符集。 對於自動化集，搜尋查詢會使用「開頭為」搜尋條件來執行，這不同於以使用「包含」搜尋條件為基礎的Experience Manager搜尋。 將篩選設定為 **[!UICONTROL 集合]** 搜尋自動化集合的唯一方法。

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>您可以透過使用者介面檢視集合，如中所述 [編輯影像集](#editing-image-sets).

## 編輯影像集 {#editing-image-sets}

您可以對「影像集」執行各種編輯工作，例如：

* 將影像新增至影像集。
* 重新排序影像集中的影像。
* 刪除影像集中的資產。
* 套用檢視器預設集。
* 刪除影像集。

**若要編輯影像集：**

1. 執行下列任一項作業：

   * 暫留在影像集資產上，然後選取 **[!UICONTROL 編輯]** （鉛筆圖示）。
   * 將滑鼠指標暫留在影像集資產上，選取 **[!UICONTROL 選取]** （勾選圖示），然後選取 **[!UICONTROL 編輯]** （在工具列上）。
   * 在影像集資產上選取，然後選取「 」 **[!UICONTROL 編輯]** （鉛筆圖示）。

1. 若要編輯「影像集」中的影像，請執行下列任一項作業：

   * 若要重新排序資產，請將影像拖曳至新位置（選取重新排序圖示以移動專案）。
   * 若要依遞增或遞減順序排序專案，請選取欄標題。
   * 若要新增資產或更新現有資產，請選取 **[!UICONTROL 新增資產]**. 導覽至資產，選取該資產，然後選取 **[!UICONTROL 選取]** 靠近頁面的右上角。

      >[!NOTE]
      >
      >如果您以其他影像取代來刪除Experience Manager用於縮圖的影像，則原始資產仍會顯示。
   * 若要刪除資產，請選取該資產並選取 **[!UICONTROL 刪除資產]**.
   * 若要套用預設集，在頁面右上角附近，選取 **[!UICONTROL 預設集]**，然後選取檢視器預設集。
   * 若要新增或變更縮圖，請選取資產右側旁的縮圖圖示。 導覽至新的縮圖或色票資產，選取該資產，然後選取 **[!UICONTROL 選取]**.
   * 若要刪除整個影像集，請導覽至影像集，選取影像集，然後選取 **[!UICONTROL 刪除]**.

   >[!NOTE]
   >
   >您可以導覽至影像集，選取 **[!UICONTROL 設定成員]** ，然後選取個別資產上的「鉛筆」圖示以開啟編輯視窗。

1. 選取 **[!UICONTROL 儲存]** 完成編輯時。

## 預覽影像集 {#previewing-image-sets}

另請參閱 [預覽資產](/help/assets/previewing-assets.md).

## 發佈影像集 {#publishing-image-sets}

另請參閱 [發佈資產](/help/assets/publishing-dynamicmedia-assets.md).
