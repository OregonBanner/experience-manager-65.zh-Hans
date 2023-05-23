---
title: 管理Dynamic Media影像預設集
description: 瞭解Dynamic Media影像預設集，並瞭解如何建立、修改和管理影像預設集。
uuid: 3e9a7af6-bf49-4cff-b516-0a3ee9765391
mini-toc-levels: 3
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: cc1111c4-6e24-4570-9ac7-97c25cf24ede
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/image-presets
feature: Image Presets
role: User, Admin
exl-id: 556b99fe-91c3-441f-ba81-22cb8c10ef7f
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '3839'
ht-degree: 7%

---

# 管理Dynamic Media影像預設集{#managing-image-presets}

影像預設集可讓Adobe Experience Manager資產以動態方式傳送不同大小、不同格式或其他動態產生影像屬性的影像。 每個影像預設集代表預先定義的一組大小調整與格式設定指令，用於顯示影像。 建立影像預設集時，您可以選擇影像傳送的大小。 您也可以選擇格式化指令，以便在傳送影像供檢視時最佳化影像的外觀。

管理員可以建立預設集來匯出資產。 使用者可以在匯出影像時選擇預設集，這樣也會將影像重新格式化為管理員指定的規格。

您也可以建立回應式影像預設集。 如果您將回應式影像預設集套用至資產，預設集會隨著檢視資產的裝置或熒幕大小而改變。 您可以將影像預設集設定為除了RGB或灰階之外，還可以在色域中使用CMYK。

本節說明如何建立、修改及一般管理影像預設集。 您可以隨時將影像預設集套用至影像預覽。 另請參閱 [套用影像預設集](/help/assets/image-presets.md).

>[!NOTE]
>
>智慧型影像處理可搭配您現有的影像預設集運作，並在傳送的最後毫秒內運用智慧功能，根據瀏覽器或網路連線速度，進一步縮減影像檔案大小。 另請參閱 [智慧型影像](/help/assets/imaging-faq.md) 以取得詳細資訊。

## 瞭解Dynamic Media影像預設集 {#understanding-image-presets}

如同巨集，「影像預設集」是預先定義的名稱下儲存的調整大小和格式指令集合。 若要瞭解影像預設集如何運作，假設您的網站要求每個產品影像以不同大小、不同格式和壓縮率顯示，以用於案頭和行動傳送。

>[!NOTE]
>
>在Dynamic Media - Scene7模式中，影像預設集僅支援影像資產。

您可以建立兩個影像預設集：一個是500 x 500畫素（適用於案頭版）和150 x 150畫素（適用於行動版）。 您可以建立兩個影像預設集，其中一個稱為 `Enlarge` 以500x500畫素顯示影像，且其中一個影像稱為 `Thumbnail` 以150 x 150畫素顯示影像。 若要將影像傳送至 `Enlarge` 和 `Thumbnail` 大小，Experience Manager會尋找放大影像預設集和縮圖影像預設集的定義。 然後Experience Manager會根據每個影像預設集的大小和格式規格，以動態方式產生影像。

動態傳送影像時若影像大小減少，可能會失去銳利度和細節。 因此，每個影像預設集都包含格式化控制項，可在影像以特定大小傳送時最佳化影像。 這些控制項可確保您的影像在傳送至您的網站或應用程式時清晰銳利。

管理員可以建立影像預設集。 若要建立影像預設集，您可以從頭開始，也可以從現有的影像預設集開始，然後以新名稱儲存。

## 管理Dynamic Media影像預設集 {#managing-image-presets-1}

您可以點選或按一下Experience Manager標誌來存取全域導覽主控台，然後點選或按一下「工具」圖示並導覽至，以管理Experience Manager的影像預設集 **[!UICONTROL 「資產」>「影像預設集」]**.

![6_5_tools-assets-imagepresets](assets/6_5_tools-assets-imagepresets.png)

>[!NOTE]
>
>預覽或傳遞資產時，您所建立的任何影像預設集也可作為動態轉譯使用。
>
>在 *Dynamic Media - Scene7模式*，您可以 *not* 需要發佈影像預設集，因為影像預設集會自動發佈。
>
>在 *Dynamic Media — 混合模式*，您必須手動發佈影像預設集。
>
>另請參閱 [發佈影像預設集](#publishing-image-presets).

>[!NOTE]
>
>當您選取時，系統會顯示各種轉譯 **[!UICONTROL 轉譯]** 在資產的「詳細資料檢視」中。 您可以增加或減少顯示的影像預設集數目。 另請參閱 [增加顯示的影像預設集數目](#increasing-or-decreasing-the-number-of-image-presets-that-display).

### 智慧型裁切、Adobe Illustrator (AI)、Postscript (EPS)和PDF檔案格式 {#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats}

>[!NOTE]
>
>本主題僅適用於Dynamic Media — 混合模式。

如果您想要支援AI、EPS和PDF檔案的擷取，以便產生這些檔案格式的動態轉譯，在建立影像預設集之前請先檢閱下列資訊。

Adobe Illustrator的檔案格式是PDF的變體。 在Experience Manager Assets的情境下，主要差異如下：

* Adobe Illustrator檔案由單一頁面組成，其中包含多個圖層。 每個圖層都會擷取為主要Illustrator資產下的PNG子資產。
* PDF檔案包含一或多個頁面。 每個頁面都會擷取為主要多頁PDF檔案下的單一頁面PDF子資產。

子資產是由 `Create Sub Asset process` 整體中的元件 `DAM Update Asset` 工作流程。 若要在工作流程中檢視此程式元件，請點選 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]** > **[!UICONTROL DAM更新資產]** > **[!UICONTROL 編輯]**.

另請參閱 [檢視多頁檔案的頁面](/help/assets/managing-linked-subassets.md#view-pages-of-a-multi-page-file).

您可以在開啟資產時檢視子資產或頁面，點選「內容」功能表，然後選取 **[!UICONTROL 子資產]** 或 **[!UICONTROL 頁面]**. 子資產是真正的資產。 也就是說，系統會擷取PDF頁面， `Create Sub Asset` 工作流程元件。 然後會儲存為 `page1.pdf`， `page2.pdf`，依此類推，位於主要資產下方。 儲存後， `DAM Update Asset` 工作流程會處理它們。

若要使用Dynamic Media來預覽和產生AI、EPS或PDF檔案的動態轉譯，需執行下列處理步驟：

1. 在 `DAM Update Asset` 工作流程， `Rasterize PDF/AI Image Preview Rendition` process元件會使用設定的解析度，將原始資產的第一個頁麵點陣化成 `cqdam.preview.png` 轉譯。

1. 此 `cqdam.preview.png` 然後，轉譯會由 `Dynamic Media Process Image Assets` 工作流程中的程式元件。

>[!NOTE]
>
>在 [!UICONTROL DAM更新資產] 工作流程， **[!UICONTROL EPS縮圖]** 步驟會產生EPS檔案的縮圖。

#### PDF/AI/EPS資產中繼資料屬性 {#pdf-ai-eps-asset-metadata-properties}

| **中繼資料屬性** | **描述** |
|---|---|
| `dam:Physicalwidthininches` | 檔案寬度（以英吋為單位）。 |
| `dam:Physicalheightininches` | 檔案高度，以英吋為單位。 |

您存取 `Rasterize PDF/AI Image Preview Rendition` 處理元件選項的方式 `DAM Update Asset` 工作流程。

點選左上方的Adobe Experience Manager，導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**. 在「工作流程模型」頁面上，選擇 **[!UICONTROL DAM更新資產]**，然後在工具列點選 **[!UICONTROL 編輯]**. 於 [!UICONTROL DAM更新資產] 工作流程頁面，點兩下 `Rasterize PDF/AI Image Preview Rendition` 處理元件，以開啟其「步驟屬性」對話方塊。

#### 點陣化PDF/AI影像預覽轉譯選項 {#rasterize-pdf-ai-image-preview-rendition-options}

![點陣化PDF或AI工作流程的引數](assets/rasterize_pdf_ai_image_preview.png)

點陣化PDF或AI工作流程的引數

<table>
 <tbody>
  <tr>
   <td><strong>程式引數</strong></td>
   <td><strong>預設設定</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>Mime 类型</td>
   <td><p>application/pdf</p> <p>application/postscript</p> <p>application/illustrator<br /> </p> </td>
   <td>視為PDF或Illustrator檔案的檔案mime型別清單。<br /> </td>
  </tr>
  <tr>
   <td>最大宽度</td>
   <td>2048</td>
   <td>產生的預覽轉譯的最大寬度（畫素）。<br /> </td>
  </tr>
  <tr>
   <td>最大高度</td>
   <td>2048</td>
   <td>所產生預覽轉譯的最大高度（畫素）。<br /> </td>
  </tr>
  <tr>
   <td>解决方法</td>
   <td>72</td>
   <td>點陣化第一頁的解析度，以ppi （每英吋畫素）為單位。</td>
  </tr>
 </tbody>
</table>

使用預設的處理引數，PDF/AI檔案的第一頁點陣化為72 ppi，而產生的預覽影像大小為2048 x 2048畫素。 對於一般部署，您可能想要將解析度增加至至少150 ppi或更高。 例如，300 ppi的美國字母大小檔案分別需要最大寬度和高度2550 x 3300畫素。

「最大寬度」和「最大高度」會限制點陣化的解析度。 例如，如果最大值保持不變，且「解析度」設定為300 ppi，則「美國信件」檔案會以186 ppi點陣化。 也就是說，檔案是1581 x 2046畫素。

此 `Rasterize PDF/AI Image Preview Rendition` 程式元件已定義一個最大值，以確保它不會在記憶體中建立過大的影像。 如此大型的影像可能會使提供給JVM (Java™虛擬機器器)的記憶體溢位。 必須注意為JVM提供足夠的記憶體來管理設定的並行工作流程數量，每個工作流程都有可能以設定的最大大小建立影像。

### InDesign(INDD)檔案格式 {#indesign-indd-file-format}

如果您想要支援INDD檔案的擷取，以便產生此檔案格式的動態轉譯，您可能想要在建立影像預設集之前先檢閱下列資訊。

對於InDesign檔案，只有在Adobe InDesign Server與Experience Manager整合時，才會擷取子資產。 參照的資產會根據其中繼資料進行連結。 連結不需要InDesign Server。 不過，在處理InDesign檔案之前，參考資產必須存在於Experience Manager中，才能在InDesign檔案和參考資產之間建立連結。

另請參閱 [將Experience Manager Assets與InDesign Server整合](/help/assets/indesign.md).

中的媒體提取程式元件 `DAM Update Asset` 工作流程會執行數個預先設定的擴充指令碼來處理InDesign檔案。

![媒體提取程式引數中的ExtendScript路徑](assets/6_5_mediaextractionprocess.png)

中的媒體提取程式元件引數中的ExtendScript路徑 [!UICONTROL DAM更新資產] 工作流程。

Dynamic Media整合會使用下列指令碼：

<table>
 <tbody>
  <tr>
   <td><strong>ExtendScript名稱</strong></td>
   <td><strong>默认</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>ThumbnailExport.jsx</td>
   <td>是</td>
   <td>產生300-ppi <code>thumbnail.jpg</code> 已最佳化並轉換為PTIFF轉譯的轉譯 <code>Dynamic Media Process Image Assets</code> 程式元件。<br /> </td>
  </tr>
  <tr>
   <td>JPEGPagesExport.jsx</td>
   <td>是</td>
   <td>為每個頁面產生300 PPIJPEG子資產。 JPEG子資產是儲存在InDesign資產下的實際資產。 它也會經過最佳化，並由 <code>DAM Update Asset</code> 工作流程。<br /> </td>
  </tr>
  <tr>
   <td>PDFPagesExport.jsx</td>
   <td>否</td>
   <td>為每個頁面產生PDF子資產。 系統會如前所述處理PDF子資產。 由於PDF僅包含單一頁面，因此不會產生任何子資產。<br /> </td>
  </tr>
 </tbody>
</table>

## 設定影像縮圖大小 {#configuring-image-thumbnail-size}

您可以透過以下專案中的設定來設定縮圖的大小： **[!UICONTROL DAM更新資產]** 工作流程。 工作流程有兩個步驟，您可以在其中設定影像資產的縮圖大小。 雖然(**[!UICONTROL Dynamic Media程式影像資產]**)用於動態影像資產，以及(**[!UICONTROL 程式縮圖]**)用於靜態縮圖產生，或當所有其他程式無法產生縮圖時， *兩者* 必須有相同的設定。

在 **[!UICONTROL Dynamic Media 流程图像资产]**&#x200B;步骤中，缩略图由图像服务器生成，此配置与应用于&#x200B;**[!UICONTROL 流程缩略图]**&#x200B;步骤的配置无关。通过&#x200B;**[!UICONTROL 流程缩略图]**&#x200B;步骤生成缩略图是创建缩览图最耗时、内存占用最多的方法。

縮圖大小會以下列格式定義： **[!UICONTROL 寬度:height:居中]**，例如 `80:80:false`. 寬度和高度會決定縮圖的大小（以畫素為單位）。 中心值為false或true，若設為true，表示縮圖影像大小與設定中指定的大小完全相同。 如果調整大小的影像較小，它會在縮圖內居中。

>[!NOTE]
>
>* EPS檔案的縮圖大小設定於 **[!UICONTROL EPS縮圖]** 步驟，在 **[!UICONTROL 引數]** 標籤中的「縮圖」。
>
>* 視訊的縮圖大小設定於 **[!UICONTROL FFmpeg縮圖]** 步驟，在 **[!UICONTROL 程式]** 標籤下的 **[!UICONTROL 引數]**.
>


**若要設定影像縮圖大小：**

1. 點選 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]** > **[!UICONTROL DAM更新資產]** > **[!UICONTROL 編輯]**.
1. 點選 **[!UICONTROL Dynamic Media程式影像資產]** 逐步並點選或按一下 **[!UICONTROL 縮圖]** 標籤。 根据需要更改缩略图大小，然后点按&#x200B;**[!UICONTROL 确定]**。

   ![6_5_dynamicmediaprocessimageassets-thumbnailstab](assets/6_5_dynamicmediaprocessimageassets-thumbnailstab.png)

1. 点按&#x200B;**[!UICONTROL 流程缩略图]**&#x200B;步骤，然后点按&#x200B;**[!UICONTROL 缩略图]**&#x200B;选项卡。根据需要更改缩略图大小，然后点按&#x200B;**[!UICONTROL 确定]**。

   >[!NOTE]
   >
   >**[!UICONTROL 流程缩略图]**&#x200B;步骤的缩略图参数中的值必须与 **[!UICONTROL Dynamic Media 流程图像资产]**&#x200B;步骤中的缩略图参数相匹配。

1. 點選 **[!UICONTROL 儲存]** 以儲存對工作流程所做的變更。

### 增加或減少顯示的Dynamic Media影像預設集數目 {#increasing-or-decreasing-the-number-of-image-presets-that-display}

預覽資產時，您建立的影像預設集可用作動態轉譯。 從檢視資產時，Experience Manager會顯示各種動態轉譯 **[!UICONTROL 詳細資料檢視>轉譯]**. 您可以增加或減少顯示的轉譯限制。

**增加或減少顯示的Dynamic Media影像預設集數目：**

1. 導覽至CRXDE Lite([https://localhost:4502/crx/de](https://localhost:4502/crx/de))。
1. 導覽至影像預設集清單節點，位置為 `/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist`

   ![increase_decreasethenumberofimagepresetsthatdisplay](assets/increase_decreasethenumberofimagepresetsthatdisplay.png)

1. 在 **[!UICONTROL limit]** 属性中，将默认设 **[!UICONTROL 置为15的Value]**（值）更改为所需的数字。
1. 導覽至影像預設集資料來源，網址為 `/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist/datasource`

   ![chlimage_1-495](assets/chlimage_1-495.png)

1. 在limit屬性中，將數字變更為所需的數字，例如 `{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`
1. 點選 **[!UICONTROL 全部儲存]**.

## 建立Dynamic Media影像預設集 {#creating-image-presets}

建立Dynamic Media影像預設集可讓您在預覽或發佈時，將這些設定套用至任何影像。

>[!NOTE]
>
>如果使用Internet Explorer 9，建立預設集不會在儲存後立即出現在預設集清單中。 若要解決此問題，請停用IE9的快取。

如果您想要支援AI、PDF和EPS檔案的擷取，以便產生這些檔案格式的動態轉譯，在建立影像預設集之前請先檢閱下列資訊。
另請參閱 [Adobe Illustrator (AI)、Postscript (EPS)和PDF檔案格式](#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats).

如果您想要支援INDD檔案的擷取，以便產生此檔案格式的動態轉譯，您可能想要在建立影像預設集之前先檢閱下列資訊。
另請參閱 [InDesign(INDD)檔案格式](#indesign-indd-file-format).

>[!NOTE]
>
>若要建立Dynamic Media影像預設集，您必須擁有Experience Manager管理員或Admin Console管理員的許可權。

**若要建立Dynamic Media影像預設集：**

1. 在Experience Manager中，點選Experience Manager標誌以存取全域導覽主控台，然後點選 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 影像預設集]**.
1. 单击&#x200B;**[!UICONTROL 创建]**。此 **[!UICONTROL 編輯影像預設集]** 視窗隨即開啟。

   ![chlimage_1-496](assets/chlimage_1-496.png)

   >[!NOTE]
   >
   >要使此图像预设具有响应性，请擦除&#x200B;**[!UICONTROL 宽度]**&#x200B;和&#x200B;**[!UICONTROL 高度]**&#x200B;字段中的值，并将其留空。

1. 根据需要，在&#x200B;**[!UICONTROL 基本]**&#x200B;和&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡中输入值，包括名称。图像预设选项中概 [述了这些选项](#image-preset-options)。 预设显示在左窗格中，并可以与其他资产一起动态使用。

   ![6_5_imagepreset-edit](assets/6_5_imagepreset-edit.png)

1. 单击“**[!UICONTROL 保存]**”。

## 建立回應式影像預設集 {#creating-a-responsive-image-preset}

若要建立回應式影像預設集，請執行以下步驟： [建立影像預設集](#creating-image-presets). 在中輸入高度和寬度時 **[!UICONTROL 編輯影像預設集]** 視窗，拭除值並保留空白。

將其保留為空白會告知Experience Manager此影像預設集有回應。 您可以適當地調整其他值。



>[!NOTE]
>
>為了檢視 **[!UICONTROL URL]** 和 **[!UICONTROL RESS]** 按鈕將影像預設集套用至資產時，必須發佈資產。
>
>![chlimage_1-79](assets/chlimage_1-498.png)
>
>在Dynamic Media - Scene7模式中，影像預設集和影像資產會自動發佈。
>
>在Dynamic Media — 混合模式中，您必須手動發佈影像預設集和影像資產。

### 影像預設集選項 {#image-preset-options}

當您建立或編輯影像預設集時，您會有本節中所述的選項。 此外，Adobe建議開始選擇這些「最佳實務」選項：

* **[!UICONTROL 格式]** (**[!UICONTROL 基本]** 索引標籤) — 選取 **[!UICONTROL JPEG]** 或其他符合您需求的格式。 所有 Web 浏览器都支持 JPEG 图像格式；它可以在小文件大小和图像质量之间实现良好的平衡。但是，JPEG 格式图像使用有损压缩方案，如果压缩设置太低，则会引入不需要的图像伪影。因此，Adobe 建议将压缩质量设置为 75。此设置在图像质量和小文件大小之间提供了良好的平衡。

* **[!UICONTROL 启用简单锐化]** - 请勿选择&#x200B;**[!UICONTROL 启用简单锐化]**（此锐化滤镜提供的控制度低于“钝化蒙版”设置）。

* **[!UICONTROL 銳利化：重新取樣模式]**  — 選取 **[!UICONTROL 銳利化2]**.

#### 基本索引標籤選項 {#basic-tab-options}

<table>
 <tbody>
  <tr>
   <td><strong>字段</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td><strong>名称</strong></td>
   <td>輸入描述性名稱，不含任何空格。 在名稱中包含影像大小規格，以協助使用者識別此影像預設集。</td>
  </tr>
  <tr>
   <td><strong>宽度和高度</strong></td>
   <td>輸入遞送影像的畫素大小。 寬度和高度必須大於0畫素。 如果任一值為0，則不會建立預設集。 如果兩個值都為空白，則會建立回應式影像預設集。</td>
  </tr>
  <tr>
   <td><strong>格式</strong></td>
   <td><p>從選單中選擇格式。</p> <p>選擇 <strong>JPEG</strong> 提供下列其他選項：</p>
    <ul>
     <li><strong>品質</strong>  — 控制JPEG壓縮等級。 此設定會影響檔案大小和影像品質。 JPEG品質比例為1-100。 當您拖曳滑桿時，「縮放」是可見的。</li>
     <li><strong>啟用JPG色度縮減取樣</strong>  — 由於眼睛對高頻色彩資訊的敏感度低於高頻亮度，因此JPEG影像會將影像資訊劃分為亮度和色彩分量。 壓縮JPEG影像時，明度分量會保留為完整解析度，而色彩分量會透過平均畫素群組來縮減取樣。 縮減取樣可將資料量減少一半或三分之一，幾乎不影響感知品質。 縮減取樣不適用於灰階影像。 此技術會減少高對比影像（例如文字重疊的影像）適用的壓縮量。</li>
    </ul>
    <div>
      選擇
     <strong>GIF</strong> 或
     <strong>含Alpha的GIF</strong> 提供這些額外的
     <strong>GIF色彩量化</strong> 選項：
    </div>
    <ul>
     <li><strong>型別 </strong> — 選取 <strong>最適化</strong> （預設）， <strong>Web</strong>，或 <strong>Macintosh</strong>. 如果您選取 <strong>含Alpha的GIF</strong>，無法使用Macintosh選項。</li>
     <li><strong>遞色</strong>  — 選取 <strong>擴散</strong> 或 <strong>關閉</strong>.</li>
     <li><strong>色彩數量 </strong> — 輸入從2到256的數字。</li>
     <li><strong>色彩清單</strong>  — 輸入逗號分隔的清單。 例如，對於白色、灰色和黑色，請輸入 <code>000000,888888,ffffff</code>.</li>
    </ul>
    <div>
      選擇
     <strong>PDF</strong>，
     <strong>TIFF</strong>，或
     <strong>含Alpha的TIFF</strong> 提供此額外選項：
    </div>
    <ul>
     <li><strong>壓縮</strong>  — 選取壓縮演演算法。 PDF的演演算法選項包括 <strong>無</strong>， <strong>Zip</strong>、和 <strong>Jpeg</strong>；若要TIFF，選項為 <strong>無</strong>， <strong>LZW</strong>， <strong>Jpeg</strong>、和 <strong>Zip</strong>；而含Alpha的TIFF則為 <strong>無</strong>， <strong>LZW</strong>、和 <strong>Zip</strong>.</li>
    </ul> <p>選擇 <strong>PNG</strong>， <strong>含Alpha的PNG，</strong> 或 <strong>EPS</strong> 不提供其他選項。</p> </td>
  </tr>
  <tr>
   <td><strong>锐化</strong></td>
   <td>選取 <strong>啟用簡單銳利化</strong> 在發生所有縮放之後，將基本銳利化濾鏡套用至影像的選項。銳利化有助於彌補以不同大小顯示影像時可能產生的模糊。 </td>
  </tr>
 </tbody>
</table>

#### 進階索引標籤選項 {#advanced-tab-options}

<table>
 <tbody>
  <tr>
   <td><strong>字段</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td><strong>色彩空间</strong></td>
   <td>選取 <strong>RGB、CMYK、</strong> 或 <strong>灰階</strong> 色彩空間的。</td>
  </tr>
  <tr>
   <td><strong>颜色配置文件</strong></td>
   <td>如果資產與正在處理的設定檔不同，請選取資產應轉換為的輸出色域設定檔。</td>
  </tr>
  <tr>
   <td><strong>渲染方法</strong></td>
   <td>您可以覆寫預設的演算比對方式。 演算意圖會決定無法在目標色彩設定檔（超出色域）中重現的色彩會發生什麼情況。 如果「演算比對方式」與ICC設定檔不相容，則會予以忽略。
    <ul>
     <li>選取 <strong>可感知</strong> 當原始影像中的一個或多個顏色超出目的地色域的範圍時，將總色域從一個色域壓縮到另一個色域。</li>
     <li>選取 <strong>相對比色</strong> 當目前色域的顏色超出目標色域的色域時。 而且，您想要將其對應到目標色域中可能最接近的顏色，而不影響任何其他顏色。 </li>
     <li>選取 <strong>飽和度</strong> 如果您想要在轉換為目標色域時重現原始影像色彩飽和度。 </li>
     <li>選取 <strong>絕對比色</strong> 以完全符合顏色，而不調整會改變影像亮度的白點或黑點。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>黑场补偿</strong></td>
   <td>如果輸出設定檔支援此功能，請選取此選項。 如果黑點補償與指定的ICC設定檔不相容，則會忽略黑點補償。</td>
  </tr>
  <tr>
   <td><strong>仿色</strong></td>
   <td>選取此選項可避免或減少色階誤差。 </td>
  </tr>
  <tr>
   <td><strong>銳利化型別</strong></td>
   <td><p>選取 <strong>無</strong>， <strong>銳利化</strong>，或 <strong>不銳利化遮色片</strong>. </p>
    <ul>
     <li>選取 <strong>無</strong> 如果您要停用銳利化。</li>
     <li>選取 <strong>銳利化</strong> 如果您想要在執行所有縮放之後套用基本銳利化濾鏡。 銳利化有助於彌補以不同大小顯示影像時可能產生的模糊。 </li>
     <li>選取<strong> 不銳利化遮色片</strong> 如果您想要微調最終縮減取樣影像的銳利化濾鏡效果。 您可以控制效果的強度、效果半徑（以畫素測量），以及忽略的對比度臨界值。 此效果使用與Photoshop的「遮色片銳利化」濾鏡相同的選項。</li>
    </ul> <p>在 <strong>不銳利化遮色片</strong>，您有以下選項：</p>
    <ul>
     <li><strong>數量</strong>  — 控制套用至邊緣畫素的對比量。 預設實數值為1.0。若是高解析度影像，最高可增加到5.0。將「數量」視為濾鏡強度的量度。</li>
     <li><strong>半徑</strong>  — 決定邊緣畫素周圍影響銳利化的畫素數量。 對於高解析度的影像，請輸入從1到2的實數。 低值只會銳利化邊緣畫素；高值會銳利化較寬的畫素範圍。 正確的值取決於影像的大小。</li>
     <li><strong>臨界值</strong>  — 決定套用遮色片銳利化調整濾鏡時要忽略的對比範圍。 換言之，此選項會決定銳利化的畫素與周圍區域必須有多大的差異，才會被視為邊緣畫素並予以銳利化。 為避免引入雜訊，請嘗試使用2到20的整數值。 </li>
     <li><strong>套用至</strong>  — 決定取消銳利化會套用至每個顏色或亮度。</li>
    </ul>
    <div>
      銳利化的說明請參閱
     <a href="https://experienceleague.adobe.com/docs/experience-manager-65/assets/sharpening_images.pdf">銳利化影像</a>.
    </div> </td>
  </tr>
  <tr>
   <td><strong>重新取样模式</strong></td>
   <td>選取 <strong>重新取樣模式</strong> 選項。 這些選項會在縮減取樣影像時銳利化影像：
    <ul>
     <li><strong>雙線性</strong>  — 最快速的重新取樣方法。會產生一些明顯的鋸齒狀不自然感。</li>
     <li><strong>雙立方式</strong>  — 增加CPU使用量，但產生較銳利的影像，且鋸齒狀不自然感較不明顯。</li>
     <li><strong>銳利化2</strong>  — 可以產生比兩次立方稍微銳利的結果，但成本更高。</li>
     <li><strong>Bi-Sharp</strong>  — 選取Photoshop預設的重新取樣器以縮減影像大小，稱為 <strong>雙立方體銳利化</strong> 在Adobe Photoshop中。</li>
     <li><strong>每種顏色</strong> 和 <strong>亮度</strong>  — 每種方法都可依據色彩或亮度而定。 依預設 <strong>每種顏色</strong> 「 」已選取。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>列印解析度</strong></td>
   <td>選取列印此影像的解析度；預設為72畫素。</td>
  </tr>
  <tr>
   <td><strong>图像修饰符</strong></td>
   <td><p>除了UI中可用的常見影像設定外，Dynamic Media還支援許多進階影像修改，您可在 <strong>影像修飾元</strong> 欄位。 這些引數定義於 <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html#image-serving-api">影像伺服器通訊協定命令參考</a>.</p> <p>重要：不支援API中列出的以下功能：</p>
    <ul>
     <li>基本範本和文字演算指令： <code>text= textAngle= textAttr= textFlowPath= textFlowXPath= textPath=</code> 和 <code>textPs=</code></li>
     <li>本地化命令： <code>locale=</code> 和 <code>req=xlate</code></li>
     <li><code>req=set</code> 無法用於一般用途。</li>
     <li><code>req=mbrset</code></li>
     <li><code>req=saveToFile</code></li>
     <li><code>req=targets</code></li>
     <li><code>template=</code></li>
     <li>非核心Dynamic Media服務：SVG、影像演算和網頁印刷</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 使用影像修飾元定義影像預設集選項 {#defining-image-preset-options-with-image-modifiers}

除了「基本」和「進階」標籤中可用的選項外，您還可以定義影像修飾元，以便在定義影像預設集時為您提供更多選項。 影像演算仰賴影像演算API，其定義詳見於 [HTTP通訊協定參考](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html#image-serving-api).

以下是您可以使用影像修飾元進行的一些基本範例。

>[!NOTE]
>
>部分影像修飾元 [無法用於Experience Manager](#advanced-tab-options).

* [op_invert](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-invert.html#image-serving-api)  — 反轉每個顏色元件以產生負影像效果。

   ```xml
   &op_invert=1
   ```

   ![6_5_imagepreset-edit-invert](assets/6_5_imagepreset-edit-invert.png)

* [op_blur](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-blur.html#image-serving-api)  — 將模糊濾鏡套用至影像。

   ```xml
   &op_blur=7
   ```

   ![6_5_imagepreset-edit-blur](assets/6_5_imagepreset-edit-blur.png)

* 組合命令 — op_blur和逆反

   ```xml
   &op_invert=1&op_blur=7
   ```

   ![chlimage_1-80](assets/chlimage_1-501.png)

* [op_brightness](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-brightness.html#image-serving-api)  — 減少或增加亮度。

   ```xml
   &op_brightness=58
   ```

   ![6_5_imagepreset-edit-brightness](assets/6_5_imagepreset-edit-brightness.png)

* [opac](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-opac.html#image-serving-api)  — 調整影像不透明度。 可讓您降低前景不透明度。

   ```xml
   opac=29
   ```

   ![6_5_imagepreset-edit-opacity](assets/6_5_imagepreset-edit-opacity.png)

## 編輯影像預設集 {#modifying-image-presets}

1. 在Experience Manager中，點選Experience Manager標誌以存取全域導覽主控台，然後點選 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 影像預設集]**.

   ![6_5_imagepreset-editpreset](assets/6_5_imagepreset-editpreset.png)

1. 選取預設集，然後按一下 **[!UICONTROL 編輯]**. 此 **[!UICONTROL 編輯影像預設集]** 視窗隨即開啟。
1. 進行變更並按一下 **[!UICONTROL 儲存]** 儲存變更或 **[!UICONTROL 取消]** 以取消您的變更。

## 發佈Dynamic Media影像預設集 {#publishing-image-presets}

如果您正在執行Dynamic Media — 混合模式，您必須手動發佈影像預設集。

(如果您執行Dynamic Media - Scene7模式，影像預設集會自動為您發佈；您不需要完成這些步驟。)

**若要在Dynamic Media — 混合模式中發佈影像預設集：**

1. 在Experience Manager中，點選或按一下Experience Manager標誌以存取全域導覽主控台，然後點選或按一下「工具」圖示並導覽至 **[!UICONTROL 資產]** > **[!UICONTROL 影像預設集]**.
1. 從影像預設集清單中選取影像預設集或多個影像預設集，然後按一下或點選 **[!UICONTROL 發佈]**.
1. 影像預設集發佈後，狀態會從未發佈變更為已發佈。

   ![chlimage_1-81](assets/chlimage_1-505.png)

## 刪除Dynamic Media影像預設集 {#deleting-image-presets}

1. 在Experience Manager中，點選或按一下Experience Manager標誌以存取全域導覽主控台。
1. 點選 **[!UICONTROL 工具]** 圖示，然後導覽至 **[!UICONTROL 資產]** > **[!UICONTROL 影像預設集]**.
1. 選取預設集，然後按一下 **[!UICONTROL 刪除]**. Dynamic Media會確認您要刪除它。 點選 **[!UICONTROL 刪除]** 刪除或點選 **[!UICONTROL 取消]** 以中止。
