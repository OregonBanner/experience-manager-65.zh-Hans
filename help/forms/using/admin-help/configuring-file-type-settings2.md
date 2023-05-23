---
title: 正在設定檔案型別設定
seo-title: Configuring file type settings
description: 瞭解如何設定檔案型別設定。
seo-description: Learn how to configure file type settings.
uuid: d01f430b-9637-4a5f-b3a7-d5ef3e5ecbc5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: adbe8416-c8d7-4581-940b-df62eadf0e26
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '6167'
ht-degree: 0%

---


# 正在設定檔案型別設定 {#configuring-file-type-settings}

在PDF產生器中，您可以為支援的檔案型別設定應用程式設定。 在Windows上，您可以為每個支援的檔案型別設定應用程式設定。 在UNIX和Linux上，您可以為HTML對PDF和OpenOffice設定應用程式設定。

您可以在「檔案型別設定值」頁面執行下列工作：

* [建立或編輯檔案型別設定](#create-or-edit-file-type-settings)
* 指定預設使用的檔案型別設定(請參閱 [匯入和匯出PDF產生器組態檔](https://helpx.adobe.com/aem-forms/6-2/admin-help/importing-exporting-pdf-generator-configuration.html))
* [變更預設設定](/help/forms/using/admin-help/configuring-file-type-settings2.md#change-the-default-settings)
* [啟用PDF/A支援](https://helpx.adobe.com/aem-forms/6-2/admin-help/enable-pdf-a-support.html)
* [刪除檔案型別設定](https://helpx.adobe.com/aem-forms/6-2/admin-help/enable-pdf-a-support.html)

>[!NOTE]
>
>後援轉換程式(例如Acrobat用於HTML至PDF轉換、Microsoft PowerPoint、Microsoft Word和Microsoft Excel)無法使用檔案型別設定。

## 建立或編輯檔案型別設定 {#create-or-edit-file-type-settings}

建立或編輯檔案型別設定，以指定應用程式如何處理受支援檔案型別的轉換。 在Windows上，您可以為每個支援的檔案型別設定應用程式設定。 在UNIX和Linux上，您可以為HTML對PDF和OpenOffice設定應用程式設定。

1. 在管理控制檯中，按一下 **[!UICONTROL 服務]** > **[!UICONTROL PDF產生器]** > **[!UICONTROL 檔案型別設定]**.
1. 按一下「新增」或按一下設定的名稱。
1. 在「副檔名」方塊中，輸入此應用程式接受的檔案型別的副檔名（以逗號分隔）。 請勿包含擴充功能之前的句點或空格。 默认为 `bmp,gif,jpeg,jpg,tif,tiff,png`。
1. （可選）若要在圖形或影像中使用文字的光學程式碼辨識(OCR)，請選取「使用OCR」並設定下列選項：

**主要OCR語言：** 用於識別字元的OCR引擎語言。 預設值為英文（美國）。

**PDF輸出樣式：** 選取「可搜尋的影像」，在前景中擁有頁面的點陣圖影像，並在下方不可見的圖層上擁有掃描的文字。 頁面的外觀不會變更，但文字會變成可選取且可讀取。 選取「格式化文字和圖形」，使用可識別的文字、字型、圖片和其他圖形元素來重新建構原始頁面。 預設為「可搜尋影像」(Searchable Image) （精確）。

**縮減取樣影像：** 減少彩色、灰階和單色影像的畫素數量。 在OCR完成之後執行掃描影像的縮減取樣。 預設值為最低(600 dpi)。 如果您將PDF輸出樣式設定為「可搜尋的影像（精確）」，則此選項不可用。

1. 完成以下章節中的必要資訊：

   [匯入和匯出PDF產生器組態檔](https://helpx.adobe.com/aem-forms/6-2/admin-help/importing-exporting-pdf-generator-configuration.html)

[Adobe PDF匯出設定（僅限Windows）](#adobe-pdf-export-settings-windows-only)

[HTML對PDF設定](#html-to-pdf-settings)

[將視訊Flash至PDF設定](#flash-videos-to-pdf-settings)

[XPS至PDF設定](#xps-to-pdf-settings)

[PDF最佳化工具設定](#pdf-optimizer-settings)

[Microsoft Excel設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings2.md#microsoft-excel-settings-windows-only)

[Microsoft PowerPoint設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings2.md#microsoft-powerpoint-settings-windows-only)

[Microsoft專案設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings2.md#microsoft-project-settings-windows-only)

[Microsoft Word設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings2.md#microsoft-word-settings-windows-only)

[Microsoft Visio設定（僅限Windows）](#visio)

[Microsoft Publisher設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings2.md#microsoft-publisher-settings-windows-only)

[AutoCAD設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings2.md#autocad-settings-windows-only)

[OpenOffice設定](/help/forms/using/admin-help/configuring-file-type-settings2.md#openoffice-settings)

[其他應用程式的設定（僅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings2.md#other-applications-settings-windows-only)

   若要移至其他區段，請按一下其在網頁上的連結，或使用**[!UICONTROL 下一個]**或 **[!UICONTROL 上一個]** 按鈕。

1. 完成所有區段後，按一下 **[!UICONTROL 儲存]** 或 **[!UICONTROL 另存為]** 並提供設定的名稱。

可自訂對各種檔案型別的支援。 (請參閱&quot; [新增對其他原生檔案格式的支援](https://help.adobe.com/en_US/AEMForms/6.1/ProgramLC/WS624e3cba99b79e12e69a9941333732bac8-7756.2.html)中的「」 [使用AEM表單程式設計](https://www.adobe.com/go/learn_lc_programming_11).)

## 變更預設設定 {#change-the-default-settings}

您可以變更適用於新建立來源的Adobe PDF設定、安全性設定和檔案型別設定的預設值。 變更預設值不會影響現有來源的設定。

1. 在管理控制檯中，按一下 **[!UICONTROL 服務>PDF產生器]**.
1. 於 **[!UICONTROL Adobe PDF設定]**， **[!UICONTROL 檔案型別設定]**，或 **[!UICONTROL 安全性設定]** 頁面，按一下 **[!UICONTROL 設定預設設定]**.
1. 選取您偏好的預設設定。 「設定預設值」頁面提供下列一或多個設定：

   **[!UICONTROL Adobe PDF設定]**：原始預設為「標準」(Acrobat 6)。

   **[!UICONTROL 安全性設定]**：原始預設為「無安全性(Acrobat 5)」。

   **[!UICONTROL 檔案型別設定]**：原始預設為「標準」。

1. 单击“**[!UICONTROL 保存]**”。

## 刪除檔案型別設定 {#delete-a-file-type-setting}

您可以刪除不再使用的檔案型別設定。

1. 在管理控制檯中，按一下 **[!UICONTROL 「服務」>「PDF產生器」>「檔案型別設定」]**.
1. 選取要刪除的設定旁的核取方塊。 您可以選取多個來源。 旁邊沒有核取方塊的設定一律會包含在PDF產生器中，且無法刪除。
1. 按一下 **[!UICONTROL 刪除]** 然後，在「刪除確認」頁面上，按一下 **[!UICONTROL 刪除]**.

## 影像至PDF設定 {#image-to-pdf-settings}

下列選項決定如何將影像檔案轉換為PDF。 如需存取這些設定的相關指示，請參閱 [建立或編輯檔案型別設定](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**副檔名：** 可轉換的副檔名清單（以逗號分隔）。

**嘗試遞補轉換器：** PDF產生器可以使用Java™或Acrobat將影像檔案轉換為PDF。 當選取此選項且轉換失敗或達到指定的逾時限制時，PDF產生器會使用替代方法嘗試轉換。 如果替代方法失敗或達到指定的逾時限制，則會將例外狀況寫入記錄檔。

>[!NOTE]
>
>JPEG2000檔案只能使用Acrobat進行轉換。

**使用OCR：** 指定是否將OCR （光學字元辨識）套用至PDF。 OCR軟體可讓您搜尋、修正和複製PDF中的文字。

***注意&#x200B;**：只有Microsoft Windows支援OCRPDF(可搜尋PDF)功能。*

**主要OCR語言：** 指定OCR引擎用來識別字元的語言。

**PDF輸出樣式：** 決定要產生的PDF型別。 所有格式都會將OCR和字型與頁面辨識套用至文字影像，並將它們轉換為一般文字。

**可搜尋的影像：** 確保文字可搜尋且可供選取。 此選項會保留原始影像、視需要傾斜影像，並在影像上放置不可見的文字圖層。 「縮減取樣影像」選項決定影像是否縮減取樣以及縮減取樣到何種程度。

**可搜尋的影像（精確）：** 確保文字可搜尋且可供選取。 此選項會保留原始影像，並在其上放置不可見的文字圖層。 建議在需要原始影像的最大精確度的情況下使用。

**清除掃描：** 會合成與原始字型相近的新Type 3字型，並使用低解析度復本保留頁面背景。

**縮減取樣影像：** 在OCR完成之後，減少彩色、灰階和單色影像的畫素數。 選擇要套用的縮減取樣程度。 編號較高的選項會減少縮減取樣，產生更高解析度的PDF。

## Adobe PDF匯出設定（僅限Windows） {#adobe-pdf-export-settings-windows-only}

Adobe PDF匯出設定區段中的「匯出檔案型別」設定可用來將PDF檔案轉換為其他格式。 預設為HTML4.01搭配階層式樣式表(CSS) 1.0 (*.htm， *.html)。

如需存取此設定的相關指示，請參閱 [建立或編輯檔案型別設定](configuring-file-type-settings.md#create-or-edit-file-type-settings).

## HTML對PDF設定 {#html-to-pdf-settings}

以下選項決定HTML檔案如何轉換為PDF。 如需有關存取這些選項的指示，請參閱 [建立或編輯檔案型別設定](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**嘗試遞補轉換器：** PDF產生器可以使用Java™或Acrobat將HTML檔案轉換為PDF。 當選取此選項且轉換失敗或達到指定的逾時限制時，PDF產生器會使用替代方法嘗試轉換。 如果替代方法失敗或達到指定的逾時限制，則會將例外狀況寫入記錄檔。

**預設編碼：** 從作業系統和字母的功能表設定檔案文字的輸入編碼。 只有在HTML來源檔案未指定編碼型別時，才會使用「預設編碼」選項中顯示的選取範圍。

**強制選取的編碼：** 忽略HTML來源檔案中指定的任何編碼，並使用預設編碼選項中顯示的選項。

### 網路串流設定 {#spidering-settings}

*串流* 掃描網頁，尋找其他網頁的連結。 遇到另一個網頁的連結時，會擷取目的地頁面，並將其包含在產生的PDF檔案中。 啟用這些選項來設定要擷取並轉換成PDF的層級數目：

**僅取得X層級：** 從基本頁面URL編目並轉換頁面，直到指定層級的深度。 值1隻會轉換提供的URL。

**取得整個網站：** 從提供的URL開始，轉換整個網站。

**維持相同的路徑：** 在串流期間，指向與基礎URL不在相同相對路徑上的頁面的任何連結都不會被轉換。

**停留在相同的伺服器上：** 在串流期間，指向不同伺服器上頁面的任何連結都不會被轉換。 系統只會轉換指向與指定URL相同伺服器的連結。

### 頁面轉換設定 {#page-conversion-settings}

啟用這些選項可指定如何轉換HTML頁面。 寬度、高度和邊界值會根據頁面大小相應地調整。

**頁面大小：** 選擇自訂並指定寬度和高度，或選取預先定義的尺寸。

**方向：** 選取已轉換PDF檔案的直向或橫向。

**邊界：** 指定產生的PDF檔案中的邊界（上、下、左和右）。

**新增書籤至PDF：** 將書籤新增至PDF檔案。

**啟用標籤PDF：** 在PDF檔案中嵌入標籤。

**設定初始檢視設定：** 可讓您設定檔案選項、視窗選項和使用者介面選項。 這些設定會決定內容的初始顯示方式。

### 檔案選項 {#document-options}

啟用這些選項以指定如何顯示內容、如何在PDF檔案中顯示頁面，以及如何指定放大等級：

**顯示：** 選取開啟PDF檔案時要在Acrobat中開啟的窗格。

**頁面配置：** 選取PDF檔案的版面配置型別。

**顯示比例：** 選擇PDF檔案初始檢視的預設放大比例，或選取自訂值。 選擇預設設定表示將使用預設的Acrobat放大率。

**開啟頁碼：** 指定PDF開啟的頁碼。

### 視窗選項 {#window-options}

啟用這些選項以指定視窗的大小和顯示方式。

**將視窗大小調整為初始頁面：** 將Acrobat視窗大小調整為初始頁面大小。

**熒幕上的中央視窗：** 在熒幕中央開啟視窗。

**以全熒幕模式開啟：** 以全熒幕模式開啟視窗。

**顯示：** 在視窗中顯示檔案標題或檔案名稱。

### 使用者介面選項 {#user-interface-options}

啟用這些選項以指定視窗外觀：

**隱藏功能表列：** 隱藏PDF檔案中的功能表列。

**隱藏工具列：** 隱藏PDF檔案中的工具列。

**隱藏視窗控制項：** 隱藏PDF檔案中的視窗控制項。

## 將視訊Flash至PDF設定 {#flash-videos-to-pdf-settings}

PDF產生器支援提交視訊以進行AdobeFlash(SWF或FLV檔案)，以及建立PDF檔案的功能，其中包含用於AdobeFlash的視訊。 此轉換不需要在表單伺服器上安裝AdobeFlash Player。 如需存取此選項的說明，請參閱 [建立或編輯檔案型別設定](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**副檔名：** 可轉換的副檔名清單（以逗號分隔）。

## XPS至PDF設定 {#xps-to-pdf-settings}

XML紙張規格(XPS)用於Windows印表機器。 這是一種Microsoft格式，可從任何Microsoft Office應用程式建立。 AEM表單提供轉換XPS檔案PDF的功能。

**副檔名：** 可轉換之所有XPS副檔名的逗號分隔清單。 目前有一種格式： .xps。

## PDF最佳化工具設定 {#pdf-optimizer-settings}

PDF產生器支援縮小PDF檔案大小的功能。 是否使用所有這些設定或僅使用幾個設定，取決於您打算如何使用檔案以及檔案必須具備的基本屬性。 在大多數情況下，預設設定適合發揮最大效率 — 透過移除嵌入字型、壓縮影像以及從檔案中移除不再需要的專案來節省空間。

>[!NOTE]
>
>最佳化數位簽署的檔案會移除數位簽章，並使其失效。

如需存取此設定的相關指示，請參閱 [建立或編輯檔案型別設定](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**目標PDF版本：** 指定PDF相容的Acrobat版本。

### 字型 {#fonts}

1. 選取 **字型。**
1. 選取下列其中一個選項：

   **取消嵌入所有字型：** 取消嵌入所有嵌入字型。

   **不要取消嵌入任何字型：** 不會取消嵌入任何字型。

   **取消嵌入某些字型：** 僅取消嵌入指定的字型。 請依照下列步驟指定要取消嵌入的字型：

   * 如有必要，請從 **字型來源** 下拉式功能表。 此下拉式功能表會列出中指定的字型目錄 **首頁>設定>核心系統>核心設定**.
   * 從「 」中選取一或多個字型 **可用字型** 清單並按一下 **新增**. 這些字型會新增至 **要取消嵌入的字型** 清單。
   * 如果要取消嵌入表單伺服器上不存在的某些字型，請在 **新增字型以取消嵌入** 方塊。 按一下 **新增**.

   >[!NOTE]
   >
   >*如果要取消嵌入某些字型（其子集已嵌入檔案中），請在字型名稱前面加上+號。 例如，「+Helvetica」。*

1. 如果您只想嵌入使用中的嵌入字型子集，請選取 **將所有內嵌字型設為子集**.

   >[!NOTE]
   >
   >*如果您要搭配使用此選項&#x200B;**取消嵌入某些字型**，中的字型&#x200B;**新增字型以取消嵌入**清單仍完全未內嵌。*

   >[!NOTE]
   >
   >*字型子集設定是僅內嵌字型的一部分的技巧。 字型子集僅包含檔案中使用的字元。*

### 透明度 {#transparency}

如果您的PDF檔案包含包含包含透明度的圖稿，您可以使用「PDF最佳化工具」設定來平面化透明度並降低檔案大小。

>[!NOTE]
>
>如果選取Acrobat 4.0和更新版本作為TargetPDF版本，則所有透明物件都會平面化。 對於其他TargetPDF版本，透明度受到支援，而且您可以設定透明度設定。

選取 **透明度** 在最佳化PDF檔案時進行透明度設定。

**透明度層級** 指定要保留的向量資訊量。 較高的設定會保留較多向量物件，而較低的設定則會點陣化較多向量物件；中間的設定會保留向量形式的簡單區域，並將複雜區域點陣化。 選取最低設定以點陣化所有圖稿。

>[!NOTE]
>
>點陣化的發生量取決於頁面的複雜性及重疊物件的型別。

**線條圖與文字** 所有物件（包括影像、向量圖稿、文字和漸層）點陣化的解析度。 支援的值為1畫素/英吋(ppi)至9600 ppi。

>[!NOTE]
>
>「線條藝術和文字」解析度通常應設定為600-1200 ppi，以提供高品質點陣化，尤其是襯線或小型點尺寸文字。

**漸層和網紋** 漸層和網格點陣化的解析度。 支援的值為1 ppi至1200 ppi。

>[!NOTE]
>
>漸層和網紋解析度通常應設為150-300 ppi，因為漸層、下落陰影和羽毛的品質無法透過較高的解析度改善，但列印時間和檔案大小會增加。

**將所有文字轉換為外框** 將所有文字物件（點文字、區域文字和路徑文字）轉換成外框，並捨棄包含透明度的頁面上的所有文字字元資訊。 此選項可確保文字寬度在平面化期間保持一致。 請注意，在Acrobat中檢視或在低解析度的桌上型印表機上列印時，啟用此選項會讓小型字型顯得稍微厚一些。 它不會影響列印在高解析度印表機或照排機上的型別品質。

**將所有筆畫轉換為外框** 在包含透明度的頁面上，將所有筆畫轉換為簡單的填色路徑。 這個選項可確保在平面化期間筆畫的寬度保持一致。 請注意，啟用此選項會導致細筆畫顯得稍微加厚，而且可能會降低平面化效能。

**裁剪複雜區域** 確保向量圖稿與點陣化圖稿之間的邊界沿著物件路徑排列。 此選項可減少當屬於某個OG的一部分時所產生的拼接成品

<!--
NOTE to WRITER: Unfinished sentence above.
-->

>[!NOTE]
>
>有些列印驅動程式處理點陣圖與向量圖的方式不同，有時會導致色彩拼接。 您可以停用某些列印驅動程式特定的色彩管理設定，將銜接問題降到最低。 這些設定會因每個印表機而異，請參閱印表機隨附的檔案以取得詳細資料。

保留疊印：將透明圖稿的顏色與背景顏色混合，以建立疊印效果。

下表顯示常見的印表機型別及其以dpi計量的解析度、以每英吋線數(lpi)計量的預設熒幕刻度，以及以每英吋畫素數(ppi)計量的影像重新取樣解析度。 例如，如果您要列印到600 dpi的雷射印表機，您應該輸入170作為重新取樣影像的解析度。

**影像** 選取「影像」以指定彩色、灰階和單色影像的壓縮和重新取樣選項。 您可能想要嘗試這些選項，以找出檔案大小與影像品質之間的適當平衡。彩色與灰階影像的解析度設定應該為列印檔案時網線的1.5到2倍。 單色影像的解析度應與輸出裝置相同，但請注意，以高於1500 dpi的解析度儲存單色影像會增加檔案大小，而不會明顯改善影像品質。 要放大的影像（例如地圖）可能需要更高的解析度。

>[!NOTE]
>
>重新取樣單色影像可能會產生非預期的檢視結果，例如沒有影像顯示。 如果發生這種情況，請關閉重新取樣，然後再次轉換檔案。 次取樣最可能發生此問題，縮減取樣則最不可能發生此問題。

<table>
 <tbody>
  <tr>
   <th><p><strong>印表機解析度</strong></p> </th>
   <th><p><strong>預設線條畫面</strong></p> </th>
   <th><p><strong>影像解析度</strong></p> </th>
  </tr>
  <tr>
   <td><p>300 dpi （雷射印表機）</p> </td>
   <td><p>60 lpi</p> </td>
   <td><p>120 ppi</p> </td>
  </tr>
  <tr>
   <td><p>600 dpi （雷射印表機）</p> </td>
   <td><p>85 lpi</p> </td>
   <td><p>170 ppi</p> </td>
  </tr>
  <tr>
   <td><p>1200 dpi （影像輸出機）</p> </td>
   <td><p>120 lpi</p> </td>
   <td><p>240 ppi</p> </td>
  </tr>
  <tr>
   <td><p>2400 dpi （影像輸出機）</p> </td>
   <td><p>150 lpi</p> </td>
   <td><p>300 ppi</p> </td>
  </tr>
 </tbody>
</table>

#### 捨棄物件 {#discard-objects}

* 選取 **捨棄物件** 指定要從PDF中移除的物件，以及最佳化CAD工程圖中的曲線。
* **捨棄所有表單提交、匯入和重設動作**：停用與提交或匯入表單資料相關的所有動作，並重設表單欄位。 此選項會保留動作連結到的表單物件。
* **捨棄所有JavaScript動作**：從PDF中移除任何使用JavaScript的動作。
* **捨棄內嵌的頁面縮圖**：移除內嵌的頁面縮圖。 此選項適用於大型檔案，按一下「頁面」按鈕後，這類檔案可能需要很長時間才能繪製頁面縮圖。
* **將平滑線條轉換為曲線**：減少用來在CAD工程圖中建立曲線的控制點數目，從而使PDF檔案更小，熒幕上呈現的速度更快。
* **捨棄內嵌的列印設定**：從檔案中移除內嵌的列印設定，例如頁面縮放比例和雙工模式。
* **捨棄書籤**：從檔案移除所有書籤。
* **平面化表單欄位**：造成表單欄位無法使用，而不變更其外觀。 表單資料會與頁面合併，成為頁面內容。
* **捨棄所有替代影像**：移除除了預定要在熒幕上檢視的版本以外的所有影像版本。 有些PDF包含同一影像的多個版本，用於不同的用途，例如低解析度的熒幕檢視和高解析度的列印。
* **捨棄檔案標籤**：從檔案中移除標籤，也會移除文字的協助工具及重排功能。
* **偵測及合併影像片段**：尋找分割成細分割的影像或遮色片，並嘗試將分割合併為單一影像或遮色片。
* **捨棄內嵌搜尋索引**：移除內嵌的搜尋索引，這會減少檔案大小。

#### 捨棄使用者資料 {#discard-user-data}

選取 **捨棄使用者資料** 移除您不想散佈或與其他使用者共用的任何個人資訊。

* **捨棄所有註解、Forms和多媒體**：從PDF中移除所有註解、表單、表單欄位和多媒體。
* **捨棄所有物件資料**：從PDF中移除所有物件。
* **捨棄外部互動參照**：移除其他檔案的連結。 跳至PDF內其他位置的連結不會移除。
* **捨棄隱藏圖層內容並平面化可見圖層**：減少檔案大小。 最佳化的檔案看起來像原始PDF，但不包含圖層資訊。
* **捨棄檔案資訊和中繼資料**：移除檔案資訊字典和所有中繼資料串流中的資訊。 (使用「另存新檔」指令將中繼資料串流還原為PDF的復本。)
* **捨棄檔案附件**：移除所有檔案附件，包括新增至PDF作為註解的附件。 (PDF最佳化程式不會最佳化附加的檔案。)
* **捨棄其他應用程式的私人資料**：從PDF檔案中移除僅對建立檔案的應用程式有用的資訊。 此設定不會影響PDF的功能，但會減少檔案大小。

### 清理 {#clean-up}

選取 **清理** 以移除檔案中不必要的專案。
這些專案包括已過時或不必要用於檔案預期用途的元素。 移除某些元素可能會嚴重影響PDF的功能。 依預設，只會選取不影響功能的元素。 如果您不確定移除其他選項的影響，請使用預設選取專案。

**压缩**

從下拉式選單中選取下列任一「浮雕壓縮」選項：

* 壓縮整個檔案
* 壓縮檔案結構
* 移除壓縮
* 保持壓縮不變

**使用Flate來編碼未編碼的資料流**：將Flate壓縮套用至所有未編碼的資料流。

**捨棄無效的書籤**：移除指向檔案中已刪除頁面的書籤。

**捨棄未參考的已命名目的地**：從PDF檔案中移除未在內部參考的已命名目的地。 此選項不會檢查其他PDF檔案或網站的連結。

**最佳化快速Web檢視的PDF**：重新建構PDF檔案，以便從Web伺服器逐頁下載（位元組服務）。

**在使用LZW編碼的資料流中，請改用Flate**：將Flate壓縮套用至使用LZW編碼的所有內容串流和影像。

**捨棄無效的連結**：移除跳至無效目的地的連結。

**最佳化頁面內容**：將所有行尾字元轉換為空格字元，可改善Flate壓縮。

## Microsoft Excel設定（僅限Windows） {#microsoft-excel-settings-windows-only}

這些選項決定Microsoft Excel檔案的轉換方式。 如需有關存取這些選項的指示，請參閱 [建立或編輯檔案型別設定](#create-or-edit-file-type-settings).

**嘗試OpenOffice做為遞補轉換器**：選取此選項且使用Microsoft Excel的轉換失敗或達到指定的逾時限制時，PDF產生器會嘗試使用OpenOffice進行轉換。 如果使用OpenOffice的轉換失敗或達到指定的逾時限制，則會將例外狀況寫入記錄檔。

**副檔名**：指定此應用程式接受的檔案型別的副檔名（以逗號分隔）。 默认为 `xls,xlsx`。請勿在擴充功能前加上句點或空格。

**建立PDF/A-1a相容檔案**：強制使用PDF/A-1b：2005RGBAdobe PDF設定。

**將書籤新增至Adobe PDF**：將Excel工作表名稱轉換為書籤。 依預設，會選取此選項。

**將工作表調整至單一頁面**：縮小文字大小以符合單一頁面上的工作表。

**轉換整個活頁簿**：轉換Excel檔案中的所有工作表。 如果未選取此選項，則只會轉換目前頁面。

**自動執行巨集**：在轉換檔案之前執行Excel檔案中的任何巨集（例如插入目前時間的巨集）。

**轉換檔案資訊**：根據來源檔案中的檔案資訊新增PDF檔案屬性。 這包括檔案標題、作者、主旨和關鍵字等資訊。

**新增Adobe PDF連結**：將來源檔案中的超連結轉換為PDF檔案中的超連結。

**將來源檔案附加至Adobe PDF**：選取此選項時，會將原始Excel試算表作為附件插入產生的PDF檔案中。

**啟用協助工具及具有標籤Adobe PDF的Reflow**：將標籤內嵌於PDF檔案中，以啟用協助工具及重排。

**要載入的Excel增益集清單**：根據預設（基於安全考量），當Excel檔案轉換為PDF時，不會執行任何Excel增益集。 若要允許某些Excel增益集在轉換期間執行，請提供以逗號分隔的增益集名稱清單。

**要轉換的工作表清單**：此方塊空白時，Excel試算表中的所有工作表都會包含在產生的PDF中。 若要選擇性地轉換工作表子集，請提供以逗號分隔的工作表名稱清單。

## Microsoft PowerPoint設定（僅限Windows） {#microsoft-powerpoint-settings-windows-only}

這些選項決定Microsoft PowerPoint檔案的轉換方式。 如需有關存取這些選項的指示，請參閱 [建立或編輯檔案型別設定](/help/forms/using/admin-help/configuring-file-type-settings2.md#create-or-edit-file-type-settings).

**[!UICONTROL 嘗試OpenOffice做為遞補轉換器]**：選取此選項且使用Microsoft PowerPoint的轉換失敗或達到指定的逾時限制時，PDF產生器會嘗試使用OpenOffice進行轉換。 如果使用OpenOffice的轉換失敗或達到指定的逾時限制，則會將例外狀況寫入記錄檔。

**[!UICONTROL 副檔名]**：指定此應用程式接受的檔案型別的副檔名（以逗號分隔）。 預設值為ppt，pptx。 請勿在擴充功能前加上句點或空格。

**[!UICONTROL 轉換檔案資訊]**：從來源檔案的「屬性」對話方塊新增檔案資訊，包括標題、主旨、作者、關鍵字、經理、公司、類別和註解。 依預設，會選取此選項。

**[!UICONTROL 將書籤新增至Adobe PDF]**：將PowerPoint標題轉換為書籤。 依預設，會選取此選項。

**[!UICONTROL 將來源檔案附加至Adobe PDF]**：將來源檔案作為附件新增至PDF檔案。 此選項預設為取消選取。

**[!UICONTROL 啟用協助工具及具有標籤Adobe PDF的Reflow]**：將標籤內嵌至PDF檔案。 此選項預設為取消選取。

**[!UICONTROL 將多媒體轉換為PDF多媒體]**：儘可能將多媒體轉換為PDF多媒體。 依預設，會選取此選項。

**[!UICONTROL 轉換演講者備註]**：將演講者備註轉換為PDF。

**[!UICONTROL 自動執行巨集]**：在轉換檔案之前執行PowerPoint檔案中的任何巨集（例如插入目前時間的巨集）。

**[!UICONTROL 以PowerPoint印表機設定為基礎的PDF配置]**：使用PowerPoint印表機設定來配置PDF檔案的版面。

**[!UICONTROL 新增Adobe PDF連結]**：轉換檔案時保留現有連結。 連結的外觀通常不會改變。 只有同時選取「啟用協助工具」選項時，才能建立連結。 此選項預設為取消選取。

**[!UICONTROL 在Adobe PDF中儲存投影片切換]**：轉換投影片轉場。 依預設，會選取此選項。

**[!UICONTROL 在Adobe PDF中儲存動畫]**：將轉換後的動畫儲存在PDF檔案中。

**[!UICONTROL 將隱藏的幻燈片轉換為PDF頁面]**：轉換隱藏的幻燈片。

**[!UICONTROL 建立PDF/A-1a相容檔案]**：強制使用PDF/A-1b：2005RGBAdobe PDF設定。 產生PDF檔案時，有些PowerPoint功能並未轉換。 如果PowerPoint轉變在Acrobat中沒有對等轉變，則會取代類似的轉變。 如果同一張投影片中有多個動畫效果，則會使用單一效果。 轉換頁面切換效果及專案符號飛入。

## Microsoft專案設定（僅限Windows） {#microsoft-project-settings-windows-only}

這些選項決定Microsoft專案檔案的轉換方式。 如需有關存取這些選項的指示，請參閱 [建立或編輯檔案型別設定](#create-or-edit-file-type-settings).

1. **[!UICONTROL 副檔名：]** 指定此應用程式接受的檔案型別的副檔名（以逗號分隔）。 默认为 `mpp`。請勿在擴充功能前加上句點或空格。

1. **[!UICONTROL 轉換檔案資訊]**：從來源檔案的「屬性」對話方塊新增檔案資訊，包括標題、主旨、作者、關鍵字、經理、公司、類別和註解。 依預設，會選取此選項。
1. **[!UICONTROL 將來源檔案附加至Adobe PDF]**：將來源檔案作為附件新增至PDF檔案。
1. **[!UICONTROL 建立PDF/A-1a相容檔案]**：強制使用PDF/A-1b：2005RGBAdobe PDF設定。
1. **[!UICONTROL 自動執行巨集]**：在轉換檔案之前執行Microsoft專案檔案中的任何巨集（例如插入目前時間的巨集）。

## Microsoft Word設定（僅限Windows） {#microsoft-word-settings-windows-only}

這些選項決定Microsoft Word檔案的轉換方式。 如需有關存取這些選項的指示，請參閱 [建立或編輯檔案型別設定](#create-or-edit-file-type-settings).

**[!UICONTROL 嘗試OpenOffice做為遞補轉換器]**：選取此選項且使用Microsoft Word的轉換失敗或達到指定的逾時限制時，PDF產生器會嘗試使用OpenOffice進行轉換。 如果使用OpenOffice的轉換失敗或達到指定的逾時限制，則會將例外狀況寫入記錄檔。

**[!UICONTROL 副檔名]**：指定此應用程式接受的檔案型別的副檔名（以逗號分隔）。 默认为 `doc,docx,rtf,txt`。請勿在擴充功能前加上句點或空格。

**[!UICONTROL 轉換檔案資訊]**：從來源檔案的「屬性」對話方塊新增檔案資訊，包括標題、主旨、作者、關鍵字、經理、公司、類別和註解。 依預設，會選取此選項。

**[!UICONTROL 將書籤新增至Adobe PDF]**：將標題轉換為書籤。 依預設，會選取此選項。

**[!UICONTROL 將來源檔案附加至Adobe PDF]**：將來源檔案作為附件新增至PDF檔案。

**[!UICONTROL 將交叉引用和目錄轉換為連結]**：將所有互動參照和目錄專案轉換為連結。 依預設，會選取此選項。

**[!UICONTROL 啟用協助工具及具有標籤Adobe PDF的Reflow]**：將標籤內嵌至PDF檔案。 依預設，會選取此選項。

**[!UICONTROL 建立PDF/A-1a相容檔案]**：如果選取，會強制使用PDF/A-1b：2005RGBAdobe PDF設定。

**[!UICONTROL 自動執行巨集]**：在轉換檔案之前執行Word檔案中的任何巨集（例如插入目前時間的巨集）。

**[!UICONTROL 在Adobe PDF中保留檔案標籤]**：將Word檔案中的標籤轉換為PDF檔案中的註釋。

**[!UICONTROL 新增Adobe PDF連結]**：將來源檔案中的超連結轉換為PDF檔案中的超連結。

**[!UICONTROL 轉換註腳和註腳連結]**：從PDF檔案中的註腳和註尾引用來建立註腳連結。

**[!UICONTROL 在Adobe PDF中將顯示的註解轉換為註解]**：將Word檔案中的註解轉換為PDF檔案中的文字註解。

**[!UICONTROL 啟用進階標籤]**：新增進階標籤以增強協助工具。

**[!UICONTROL 將所有樣式轉換為書籤]**：將Word檔案中的所有樣式轉換為PDF檔案中的書籤。

**[!UICONTROL 具層級的樣式]**：指定Word檔案中的哪些樣式會轉換為PDF檔案中的書籤。 也會指定書籤的層級。 若要使用此功能，請取消選取 **[!UICONTROL 將所有樣式轉換為書籤]** 選項並以下列格式指定樣式名稱：

styleName1=level1[，styleName2=level2...]

如果Microsoft Word樣式名稱包含逗號(，)或等號(=)，請在特殊字元前加上逸出字元(&quot;\_)。 例如，將名為「標題，1」的樣式指定為標題\，1。

## Microsoft Visio設定（僅限Windows） {#visio}

**轉換檔案資訊**：從來源檔案的「屬性」對話方塊新增檔案資訊，包括標題、主旨、作者、關鍵字、經理、公司、類別和註解。 依預設，會選取此選項。 此選項預設為啟用。

**新增Adobe PDF連結**：保留所有連結。 依預設，會選取此選項。

**將書籤新增至Adobe PDF**：將標題轉換為書籤。 依預設，會選取此選項。

**將來源檔案附加至Adobe PDF**：將來源檔案作為附件新增至PDF檔案。

**在Adobe PDF中一律平面化圖層**：將所有Visio圖層平面化。

**轉換所有頁面**：轉換Visio檔案的所有頁面。

**在Adobe Acrobat中檢視時開啟「圖層」面板**：如果Visio圖層未平面化，會開啟一個視窗，您可以在其中指定使用Acrobat開啟時保留在PDF檔案中的圖層。 依預設，會選取此選項。

**建立PDF/A-1b相容檔案**：強制使用Adobe PDF設定PDF/A-1b：2005 (RGB)。

**將註解轉換為Adobe PDF註解**：將Visio備註轉換為PDF註解。

## Microsoft Publisher設定（僅限Windows） {#microsoft-publisher-settings-windows-only}

這些選項決定Microsoft Publisher檔案的轉換方式。 如需有關存取這些選項的指示，請參閱 [建立或編輯檔案型別設定](#create-or-edit-file-type-settings).

**[!UICONTROL 副檔名]**：指定此應用程式接受的檔案型別的副檔名（以逗號分隔）。 默认为 `pub`。請勿在擴充功能前加上句點或空格。

## AutoCAD設定（僅限Windows） {#autocad-settings-windows-only}

這些選項決定AutoCAD檔案的轉換方式。 如需有關存取這些選項的指示，請參閱 [建立或編輯檔案型別設定](/help/forms/using/admin-help/configuring-file-type-settings2.md#create-or-edit-file-type-settings).

**[!UICONTROL 副檔名]**：指定此應用程式接受的檔案型別的副檔名（以逗號分隔）。 默认为 `dwg`。請勿在擴充功能前加上句點或空格。

**[!UICONTROL 轉換檔案資訊]**：從來源檔案的「屬性」對話方塊新增檔案資訊，包括標題、主旨、作者、關鍵字、經理、公司、類別和註解。 依預設，會選取此選項。

**[!UICONTROL 將書籤新增至Adobe PDF]**：將標題轉換為書籤。

**[!UICONTROL 在Adobe PDF中一律平面化圖層]**：將所有AutoCAD圖層平面化。

**[!UICONTROL 在Adobe Acrobat中檢視時開啟「圖層」窗格]**：在Acrobat中開啟PDF時顯示圖層結構。

**[!UICONTROL 建立符合PDF/E-1規範的檔案]**：建立符合PDF/E-1的檔案。 PDF/E是用於交換工程和技術檔案的ISO標準。 如需PDF/E-1的詳細資訊，請參閱 [Adobe和業界標準](https://www.adobe.com/enterprise/standards/index.html).

**[!UICONTROL 轉換所有版面]**：包含PDF中的所有版面。

**[!UICONTROL 將模型空間轉換為3D]**：選取後，模型空間配置會轉換為PDF中的3D註釋。

**[!UICONTROL 新增Adobe PDF連結]**：如果選取，會保留所有連結。

**[!UICONTROL 將來源檔案附加至Adobe PDF]**：將來源檔案作為附件新增至PDF檔案。

**[!UICONTROL 建立PDF/A-1b相容檔案]**：強制使用PDF/A-1b Adobe PDF設定。

**[!UICONTROL 轉換所有圖層]**：根據預設，PDF產生器僅會將AutoCAD檔案的預設圖層轉換為PDF，而非檔案中的所有圖層。 選取此選項可轉換檔案的所有圖層。

**[!UICONTROL 內嵌規模資訊]**：保留工程圖比例資訊。

**[!UICONTROL 轉換目前的版面]**：僅包含PDF中的目前版面。

**[!UICONTROL 要轉換的AutoCAD配置清單]**：AutoCAD工程圖可以有多個版面。 當此方塊為空白時，AutoCAD工程圖中的所有版面都會包含在產生的PDF檔案中。 若要有選擇地轉換配置子集，請提供以逗號分隔的配置名稱清單。

## OpenOffice設定 {#openoffice-settings}

這些選項決定OpenOffice檔案的轉換方式。 如需有關存取這些選項的指示，請參閱 [建立或編輯檔案型別設定](/help/forms/using/admin-help/configuring-file-type-settings2.md#create-or-edit-file-type-settings).

**試用PDFMaker作為後援轉換器**：選取此選項且使用OpenOffice的轉換失敗或達到指定的逾時限制時，PDF產生器會嘗試使用PDFMaker進行轉換。 如果使用PDFMaker的轉換失敗或達到指定的逾時限制，則會將例外狀況寫入記錄檔。

**副檔名**：指定此應用程式接受的檔案型別的副檔名（以逗號分隔）。 默认为 `odt,odp,ods,odg,odf,sxw,sxi,sxd`。請勿在擴充功能前加上句點或空格。

**範圍**：轉換所有頁面或指定特定頁面或頁面範圍。 如果未定義頁面範圍，則會轉換所有頁面。 若要匯出一定範圍的頁面，請使用格式3-6。 若要匯出單一頁面，請使用格式7；9；11。 您可以使用3-6；8；10；12等格式匯出頁面範圍和單一頁面的組合。

**頁面方向**：僅適用於純文字檔案，請為轉換後的PDF檔案選取直向或橫向。

**影像**：設定影像的轉換方式。 內嵌預覽的EPS影像隻會匯出為預覽。 沒有內嵌預覽的EPS影像會匯出為空白的預留位置。 使用影像的無失真壓縮，會保留所有畫素。 藉由影像的JPEG壓縮和高品質等級，幾乎所有畫素都會保留。 若是低品質層級，部分畫素會遺失且產生不自然感，但檔案大小會減少。

**一般**：啟用轉換標籤PDF或將Writer和FormCalc檔案註記、Impress投影片切換效果或空白頁面匯出到PDF的選項。 匯出標籤時，檔案大小可能會大幅增加。 有些匯出的標籤為目錄、超連結和控制項。

您也可以指定提交表單的方式。 選項有XML、FDF、PDF或HTML。 此設定會覆寫您在檔案中設定的控制項URL屬性。 只能為PDF檔案選取一個通用設定：

* PDF（傳送整個檔案）
* FDF （傳送控制內容）
* HTML
* XML

**標籤PDF**：啟用從OpenOffice檔案建立標籤PDF的功能。 已標籤的PDF包含有關檔案內容結構的資訊。 當檔案顯示在不同熒幕的裝置上，以及使用熒幕助讀程式軟體時，這項功能會有所幫助。 它還有助於協助工具軟體對PDF檔案執行各種有用的操作，例如朗讀PDF檔案的內容。

**匯出附註**：將OpenOffice檔案中的附註轉換為產生的PDF檔案中的附註。

**使用切換效果**：將OpenOffice簡報中的投影片切換效果轉換為對應的PDF切換效果。

**以格式提交Forms**：建立可由PDF檔案使用者填寫和列印的PDF表單。

**匯出自動插入的空白頁面**：選取此選項時，自動插入的空白頁面會包含在產生的PDF檔案中。 如果要雙面列印PDF檔案，這會很有用。 例如，書冊可以設定為章節的第一頁一律從奇數頁開始。 如果上一章結尾是奇數頁，OpenOffice會插入空白偶數頁。 此選項控制是否在產生的PDF中包含偶數頁面。

## 其他應用程式設定（僅限Windows） {#other-applications-settings-windows-only}

您無法透過Administration Console變更其他應用程式的設定；它們會顯示支援的檔案型別的副檔名。 如需存取這些設定的相關指示，請參閱 [建立或編輯檔案型別設定](https://help.adobe.com/en_US/AEMForms/6.1/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7e42.2.html).

* Corel WordPerfect： `wpd`
* AdobePageMaker： `pmd, pm6, p65, pm`
* Adobe FrameMaker： `fm`
* Adobe Photoshop: `psd`

可能需要自訂對這些檔案型別的支援。 如需詳細資訊，請參閱以下的「新增對其他原生檔案格式的支援」： [使用AEM表單程式設計](https://www.adobe.com/go/learn_aemforms_programming_62).

如需設定PDFG網路印表機的說明，請參閱 [設定PDFG網路印表機（僅限Windows）](/help/forms/using/admin-help/setting-pdfg-network-printer-windows.md).
