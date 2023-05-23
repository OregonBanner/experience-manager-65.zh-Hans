---
title: 混合媒体集
description: 瞭解如何在Dynamic Media中使用混合媒體集
uuid: cecad772-ed05-46f6-ba44-107195866b0d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: ed84157a-e6b4-4dde-af2e-a1e0b6259628
docset: aem65
feature: Mixed Media Sets,Asset Management
role: User, Admin
exl-id: 70a72fb9-a289-4eda-abcc-300edf9f1961
source-git-commit: 7b29fc96768dc2238ebf9596b136ec10fa71aca9
workflow-type: tm+mt
source-wordcount: '1493'
ht-degree: 14%

---

# 混合媒体集{#mixed-media-sets}

混合媒體集可讓您在單一簡報中提供影像、影像集、迴轉集和視訊的混合。

混合媒体集由带有MixedMediaSet字样的横幅 **[!UICONTROL 指定]**。 此外，如果混合媒体集已发布，则横幅上会显示发布日期(由 **[!UICONTROL World]** 图标指示)以及上次修改日期(由 **** Pencil图标指示)。

![chlimage_1-137](assets/chlimage_1-348.png)

>[!NOTE]
>
>如需Assets使用者介面的詳細資訊，請參閱 [管理資產](/help/assets/manage-assets.md).

## 快速入門：混合媒體集 {#quick-start-mixed-media-sets}

若要快速啟動並執行混合媒體集，請遵循下列步驟：

1. [上傳您的資產](#uploading-assets).

   首先为混合媒体集上传图像和视频。 如有必要，请创 [建图像集](/help/assets/image-sets.md)[和旋转集](/help/assets/spin-sets.md)。 由於使用者可以在混合媒體集檢視器中放大影像，因此請謹慎選擇影像。 确保图像的最大尺寸至少为2000像素。

   另請參閱 [Dynamic Media — 支援的點陣影像格式](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media) 以取得混合媒體集支援的格式清單。

1. [建立混合媒體集](#creating-mixed-media-sets).

   若要建立混合媒體集，請從「資產」頁面中選取 **[!UICONTROL 建立]** > **[!UICONTROL 混合媒體集]** 然後命名該集合、選擇資產，並選擇影像的顯示順序。

   另請參閱 [使用選取器](/help/assets/working-with-selectors.md).

1. 設定 [混合媒體檢視器預設集](/help/assets/managing-viewer-presets.md)，視需要而定。

   管理员可以创建或修改混合媒体集查看器预设。要查看带有查看器预设的混合媒体，请选择混合媒体集，然后在左边栏下拉菜单中，选择&#x200B;**[!UICONTROL 查看器]**。

   若要建立或編輯檢視器預設集，請參閱 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 檢視器預設集]**.

   另請參閱 [新增和編輯檢視器預設集](/help/assets/managing-viewer-presets.md).

1. [預覽混合媒體集](#previewing-mixed-media-sets).

   選取「混合媒體集」，即可預覽。 選取縮圖圖示，以便在選取的檢視器中檢查您的混合媒體集。 您可以從以下選擇不同的檢視器 **[!UICONTROL 檢視者]** 功能表，可從左側邊欄下拉式功能表取得。

1. [發佈混合媒體集](#publishing-mixed-media-sets).

   發佈混合媒體集時會啟用URL和內嵌字串。 此外，您必須 [發佈檢視器預設集](/help/assets/managing-viewer-presets.md#publishing-viewer-presets).

1. [將URL連結至您的網頁應用程式](/help/assets/linking-urls-to-yourwebapplication.md) 或 [內嵌視訊或影像檢視器](/help/assets/embed-code.md).

   Adobe Experience Manager資產會為混合媒體集建立URL呼叫，並在您發佈混合媒體集後將其啟用。 您可以在預覽資產時複製這些URL。 或者，您也可以將它們內嵌在網站上。

   選取「混合媒體集」，然後在左側導軌下拉式選單中選取 **[!UICONTROL 檢視者]**.

   另請參閱 [將混合媒體集連結至網頁](/help/assets/linking-urls-to-yourwebapplication.md) 和 [內嵌視訊或影像檢視器](/help/assets/embed-code.md).

如有需要，您可以編輯 [混合媒體集](#editing-mixed-media-sets). 此外，您也可以檢視和修改 [混合媒體集屬性](/help/assets/manage-assets.md#editing-properties).

>[!NOTE]
>
>如果您在建立集合時發生問題，請參閱 [疑難排解Dynamic Media - Scene7模式](/help/assets/troubleshoot-dms7.md).

## 上传资产 {#uploading-assets}

首先为混合媒体集上传图像和视频。 由於使用者可以在混合媒體集檢視器中放大影像，因此請謹慎選擇影像。 确保图像的最大尺寸至少为2000像素。

此外，如果您想要將迴轉集或影像集新增至混合媒體集，也請建立這些集合。

另請參閱 [Dynamic Media — 支援的點陣影像格式](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media) 以取得混合媒體集支援的格式清單。

## 建立混合媒體集 {#creating-mixed-media-sets}

您可以將影像、影像集、迴轉集和視訊新增至混合媒體集。 將檔案、影像集和迴轉集新增至混合媒體集之前，請確定檔案和影像集已可發佈。

當您將資產新增至集時，資產會自動以英數字元順序新增。 在新增資產後，您可以手動重新排序或排序資產。

**若要建立混合媒體集：**

1. 在「資產」中，導覽至您要建立混合媒體集的位置，然後選取「 」 **[!UICONTROL 建立]**，並選取 **[!UICONTROL 混合媒體集]**. 您还可以从包含资产的文件夹中创建旋转集。此时将显示混合媒体集编辑器。

   ![chlimage_1-138](assets/chlimage_1-349.png)

1. 在混合媒體集編輯器中，在 **[!UICONTROL 標題]**，輸入混合媒體集的名稱。 此名稱會出現在混合媒體集的橫幅中。 選擇性地輸入說明。

   ![chlimage_1-139](assets/chlimage_1-350.png)

   >[!NOTE]
   >
   >建立混合媒體集時，您可以變更混合媒體集縮圖，或允許Experience Manager根據混合媒體集中的資產自動選取縮圖。 若要選取縮圖，請選取 **[!UICONTROL 變更縮圖]** 並選取任何影像（您也可以導覽至其他資料夾以尋找影像）。 如果您已選取縮圖，然後決定要讓Experience Manager從混合媒體集產生縮圖，請選取「 」 **[!UICONTROL 切換到自動縮圖]**.

1. 選取「資產選擇器」，即可選取要納入混合媒體集的資產。 選取它們，然後選取 **[!UICONTROL 選取]**.

   借助资产选择器，您可以通过键入关键字并点按&#x200B;**[!UICONTROL 返回]**&#x200B;来搜索资产。您还可以应用过滤器来优化搜索结果。您可以按路径、收藏集、文件类型和标记进行过滤。選取篩選，然後選取 **[!UICONTROL 篩選]** 圖示加以檢視。 选择&#x200B;**[!UICONTROL 视图]**&#x200B;图标，然后选择&#x200B;**[!UICONTROL 列表视图]**、**[!UICONTROL 列视图]**&#x200B;或&#x200B;**[!UICONTROL 卡片视图]**&#x200B;以更改视图。

   另請參閱 [使用選取器](/help/assets/working-with-selectors.md).

   ![chlimage_1-140](assets/chlimage_1-383.png)

1. 將資產向上或向下拖曳至清單，以重新排序資產(必須選取 **[!UICONTROL 重新排序]** 圖示)。

   ![chlimage_1-141](assets/chlimage_1-352.png)

   如果您想要新增縮圖，請選取 **+** **[!UICONTROL 縮圖]** 圖示並導覽至您想要的縮圖。 選取完所有縮圖影像後，請選取 **[!UICONTROL 儲存]**.

   >[!NOTE]
   >
   >如果您想要新增資產，請選取「 」 **[!UICONTROL 新增資產]**.

1. 若要刪除資產，請選取對應的核取方塊並選取 **[!UICONTROL 刪除資產]**.
1. 若要套用預設集，請選取 **[!UICONTROL 預設集]** 並選取要套用至資產的預設集。
1. 选择&#x200B;**[!UICONTROL 保存]**。您新建立的混合媒體集會顯示在您建立它的資料夾中。

## 編輯混合媒體集 {#editing-mixed-media-sets}

您可以直接在使用者介面中針對混合媒體集中的資產執行各種編輯任務 [如同Assets中的任何資產](/help/assets/manage-assets.md). 您也可以在「混合媒體集」中執行下列動作：

* 將資產新增至混合媒體集。
* 重新排序混合媒體集中的資產。
* 刪除混合媒體集中的資產。
* 套用檢視器預設集。
* 變更預設縮圖。

**若要編輯混合媒體集：**

1. 執行下列任一項作業：

   * 暫留在混合媒體集資產上，然後選取「 」 **[!UICONTROL 編輯]** （鉛筆圖示）。
   * 將滑鼠懸停在混合媒體集資產上，選取 **[!UICONTROL 選取]** （勾選圖示），然後選取 **[!UICONTROL 編輯]** （在工具列上）。

   * 選取混合媒體集資產，然後選取 **[!UICONTROL 編輯]** （鉛筆圖示）。

1. 在混合媒體集編輯器中，執行下列任一項作業：

   * 若要重新排序資產 — 在左側面板中，選取 **[!UICONTROL 資產]** （圖片圖示），將資產拖曳至新位置。
   * 若要新增資產 — 在工具列上，選取 **[!UICONTROL 新增資產]**. 導覽至資產。 針對您要新增的每個資產，將滑鼠指標暫留在資產的影像（而非資產名稱）上，然後選取核取記號圖示。 在右上角，選取 **[!UICONTROL 選取]**.

   * 若要刪除資產 — 在左側面板中，選取 **[!UICONTROL 資產]** （圖片圖示），然後選取資產。 在工具列上，選取 **[!UICONTROL 刪除資產]**.

   * 若要依名稱遞增或遞減順序排序資產，請在左側面板中選取 **[!UICONTROL 資產]** （圖片圖示）。 右側 **[!UICONTROL 資產]** 標題中，選取向上或向下插入號圖示。

      >[!NOTE]
      >
      >* 若要從任何檢視模式(例如 **[!UICONTROL 卡片檢視]** 或 **[!UICONTROL 欄檢視]**)導覽至混合媒體集。 將滑鼠指標暫留在資產上，並選取核取標籤圖示，讓您選取它。 按下 **[!UICONTROL 退格字元]** 或選取「 」 **[!UICONTROL 更多]** （三個點），然後選取 **[!UICONTROL 刪除]**.
      >
      >* 您可以導覽至混合媒體集，然後按一下「 」，編輯混合媒體集中的資產 **[!UICONTROL 設定成員]** 在左側邊欄中。 選取 **[!UICONTROL 鉛筆]** 圖示來開啟，以便在編輯視窗中開啟。


1. 選取 **[!UICONTROL 儲存]** 完成編輯時。

   >[!NOTE]
   >
   >* 若要編輯混合媒體集中的資產 — 導覽至混合媒體集。 點選（不要選取）集，使其在「Experience Manager集預覽」頁面中開啟。 在左側邊欄中，選取向下插入號以開啟下拉式清單，然後選取 **[!UICONTROL 設定成員]**. 在「設定成員」頁面中，暫留在資產上，然後選取「 」 **[!UICONTROL 編輯]** （鉛筆圖示）以開啟編輯頁面。
   >
   >* 要刪除整個混合媒體集 — 從任何檢視模式（例如卡片檢視或欄檢視），導覽至混合媒體集。 暫留在集合上，然後選取 **選取** （勾選圖示）。 按下 **[!UICONTROL 退格字元]** 或選取「 」 **[!UICONTROL 更多]** （三點列），然後選取 **[!UICONTROL 刪除]**.


## 預覽混合媒體集 {#previewing-mixed-media-sets}

另請參閱 [預覽資產](/help/assets/previewing-assets.md) 以取得有關如何預覽混合媒體集的詳細資訊。

## 發佈混合媒體集 {#publishing-mixed-media-sets}

另請參閱 [發佈資產](/help/assets/publishing-dynamicmedia-assets.md) 有關如何發佈混合媒體集的詳細資訊。

>[!NOTE]
>
>如果混合媒體集在第一次發佈時並未完全進入傳送服務，請再次發佈混合媒體集。
