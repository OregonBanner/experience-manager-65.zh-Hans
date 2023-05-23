---
title: 将 Dynamic Media 资源添加到页面
description: 若要將Dynamic Media功能新增至您在網站上使用的資產，您可以直接在頁面上新增Dynamic Media或互動式媒體元件。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
exl-id: d2ebfca5-19f9-4fa5-b142-b978f46a912f
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '1668'
ht-degree: 3%

---

# 将 Dynamic Media 资源添加到页面{#adding-dynamic-media-assets-to-pages}

若要將Dynamic Media功能新增至您在網站上使用的資產，您可以新增 **[!UICONTROL Dynamic Media]** 或 **[!UICONTROL 互動媒體]** 元件直接在頁面上。 輸入 **[!UICONTROL 設計]** 模式並啟用Dynamic Media元件。 然后，您可以将这些组件添加到页面，并将资产添加到该组件。 Dynamic Media和互動式媒體元件是智慧型的，可得知您是新增影像還是視訊，而可用的選項也會隨之變更。

如果您使用Dynamic Media做為WCM，請直接將Adobe Experience Manager資產新增至頁面。

>[!NOTE]
>
>可立即用於輪播橫幅的影像地圖。

## 將Dynamic Media元件新增至頁面 {#adding-a-dynamic-media-component-to-a-page}

新增 [!UICONTROL Dynamic Media] 或 [!UICONTROL 互動媒體] 將元件新增至頁面與將元件新增至任何頁面相同。 此 [!UICONTROL Dynamic Media] 和 [!UICONTROL 互動媒體] 以下各節將詳細說明元件。

若要將Dynamic Media元件/檢視器新增至頁面：

1. 在Experience Manager中，開啟您要新增Dynamic Media元件的頁面。
1. 如果沒有可用的Dynamic Media元件，請選取 [!UICONTROL Sidekick] 以輸入 **[!UICONTROL 設計]** 模式。
1. 選取 **[!UICONTROL 編輯]** parsys。
1. 選取 **[!UICONTROL Dynamic Media]** 以便Dynamic Media元件可供使用。

   >[!NOTE]
   >
   >另請參閱 [在設計模式中設定元件](/help/sites-authoring/default-components-designmode.md) 以取得詳細資訊。

1. 返回至 **[!UICONTROL 編輯]** 模式，方法是按一下 [!UICONTROL Sidekick].
1. 拖曳 **[!UICONTROL Dynamic Media]** 或 **[!UICONTROL 互動媒體]** 元件來自 **[!UICONTROL 其他]** 在sidekick中群組至頁面所需位置。
1. 選取 **[!UICONTROL 編輯]** 元件隨即開啟。
1. [編輯元件](#dynamic-media-component) 視需要而定。
1. 選取 **[!UICONTROL 確定]** 以儲存您的變更。

## Dynamic Media Components {#dynamic-media-components}

[!UICONTROL Dynamic Media] 和 [!UICONTROL 互動媒體] 可從以下網址取得： [!UICONTROL Sidekick] 在 **[!UICONTROL Dynamic Media]**. 您使用 **[!UICONTROL 互動媒體]** 任何互動式資產的元件，例如互動式視訊、互動式影像或轉盤集。 對於所有其他Dynamic Media元件，請使用 **[!UICONTROL Dynamic Media]** 元件。

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>預設不會提供這些元件，且必須在使用之前在設計模式中選取這些元件。 [在「設計」模式中可供使用之後](/help/sites-authoring/default-components-designmode.md)時，您可以像新增任何其他Experience Manager元件一樣將元件新增至頁面。

### Dynamic Media元件 {#dynamic-media-component}

Dynamic Media元件是智慧型的 — 視您新增影像或視訊而定，您有各種選項。 元件支援影像預設集、影像型檢視器（例如影像集、迴轉集、混合媒體集和視訊）。 此外，檢視器會回應。 也就是說，熒幕大小會根據熒幕大小自動變更。 所有檢視器都是以HTML5為基礎的檢視器。

>[!NOTE]
>
>當您新增 [!UICONTROL Dynamic Media] 元件，以及 **[!UICONTROL Dynamic Media設定]** 為空白或無法正確新增資產，請檢查下列專案：
>
>* 您有 [已啟用Dynamic Media](/help/assets/config-dynamic.md). Dynamic Media預設為停用。
>* 影像具有金字塔tiff檔案。 在啟用Dynamic Media之前匯入的影像沒有金字塔tiff檔案。
>


#### 使用影像時 {#when-working-with-images}

此 [!UICONTROL Dynamic Media] 元件可讓您新增動態影像，包括影像集、迴轉集和混合媒體集。 您可以放大、縮小旋轉集內的影像，或是從其他型別的旋轉集中選取影像（如果適用）。

您也可以直接在元件中設定檢視器預設集、影像預設集或影像格式。 若要使影像具有回應性，您可以設定中斷點或套用回應性影像預設集。

![chlimage_1-72](assets/chlimage_1-72a.png)

您可以按一下「 」，編輯下列Dynamic Media設定 **[!UICONTROL 編輯]** ，然後按一下 **[!UICONTROL Dynamic Media設定]** 標籤。

![chlimage_1-73](assets/chlimage_1-73a.png)

>[!NOTE]
>
>默认情况下，Dynamic media图像组件是自适应的。 如果要使其成為固定大小，請在 **[!UICONTROL 進階]** 以tab鍵定位 **[!UICONTROL 寬度]** 和 **[!UICONTROL 高度]** 屬性。

**[!UICONTROL 檢視器預設集]**  — 從下拉式選單中選取現有的檢視器預設集。 如果您要尋找的檢視器預設集不可見，您必須使其可見。 另請參閱 [管理檢視器預設集](/help/assets/managing-viewer-presets.md). 如果您使用影像預設集，則無法選取檢視器預設集，反之亦然。

只有當您檢視影像集、迴轉集或混合媒體集時，才可使用此選項。 顯示的檢視器預設集是智慧型的。 也就是說，只會顯示相關的檢視器預設集。

**[!UICONTROL 影像預設集]**  — 從下拉式選單中選取現有的影像預設集。 如果您要尋找的影像預設集不可見，您必須使其可見。 另請參閱 [管理影像預設集](/help/assets/managing-image-presets.md). 如果您使用影像預設集，則無法選取檢視器預設集，反之亦然。

如果您檢視影像集、迴轉集或混合媒體集，則此選項不可用。

**[!UICONTROL 影像修飾元]**  — 您可以提供其他影像指令來變更影像效果。 這些指令的說明請參閱 [管理影像預設集](/help/assets/managing-viewer-presets.md) 和 [命令參考](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html).

如果您檢視影像集、迴轉集或混合媒體集，則此選項不可用。

**[!UICONTROL 中斷點]**  — 如果您在回應式網站上使用此資產，必須新增頁面中斷點。 影像中斷點以逗號(，)分隔。 影像預設集中未定義高度或寬度時，此選項即會運作。

如果您檢視影像集、迴轉集或混合媒體集，則此選項不可用。

您可以編輯下列專案 [!UICONTROL 進階設定] 按一下 **[!UICONTROL 編輯]** 在元件中。

**[!UICONTROL 標題]**  — 變更影像的標題。

**[!UICONTROL 替代文字]**  — 為已關閉圖形的使用者新增影像標題。

如果您檢視影像集、迴轉集或混合媒體集，則此選項不可用。

**[!UICONTROL URL，開啟位置]**  — 您可以從設定資產以開啟連結。 設定 **[!UICONTROL URL]** 和 **[!UICONTROL 開啟方式]** 以指出您想要在相同視窗或新視窗中開啟該視窗。

如果您檢視影像集、迴轉集或混合媒體集，則此選項不可用。

**[!UICONTROL 寬度和高度]**  — 如果您希望影像為固定大小，請輸入畫素值。 將這些值保留空白可讓資產適應新情況。

#### 使用視訊時 {#when-working-with-video}

使用 **[!UICONTROL Dynamic Media]** 新增動態視訊至網頁的元件。 編輯元件時，您可以選擇使用預先定義的視訊檢視器預設集在頁面上播放視訊。

![chlimage_1-74](assets/chlimage_1-74a.png)

您可以編輯下列專案 [!UICONTROL Dynamic Media設定] 按一下 **[!UICONTROL 編輯]** 在元件中。

>[!NOTE]
>
>依預設，Dynamic Media視訊元件是自我調整的。 如果要使其成為固定大小，請在元件中設定它，並使用 **[!UICONTROL 寬度]** 和 **[!UICONTROL 高度]** 在 **[!UICONTROL 進階]** 標籤。

**[!UICONTROL 檢視器預設集]**  — 從下拉式選單中選取現有的視訊檢視器預設集。 如果您要尋找的檢視器預設集不可見，您必須使其可見。 另請參閱 [管理檢視器預設集](/help/assets/managing-viewer-presets.md).

您可以編輯下列專案 [!UICONTROL 進階] 設定(按一下 **[!UICONTROL 編輯]** 在元件中。

**[!UICONTROL 標題]**  — 變更視訊標題。

**[!UICONTROL 寬度和高度]**  — 如果要讓視訊大小固定，請輸入畫素值。 將這些值保留為空白可使其最適化。

#### 傳送安全視訊 {#how-to-delivery-secure-video}

在Experience Manager6.2中，當您安裝 [FP-13480](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq620/featurepack/cq-6.2.0-featurepack-13480)時，您可以控制視訊是透過安全SSL連線(HTTPS)還是不安全連線(HTTP)傳送。 依預設，視訊傳送通訊協定會自動繼承自內嵌網頁的通訊協定。 如果網頁是透過HTTPS載入，影片也會透過HTTPS傳送。 反之，如果網頁位於HTTP上，則會透過HTTP傳送影片。 通常，此預設行為是正常的，不需要進行任何設定變更。 不過，您可以覆寫此預設行為。 附加 `VideoPlayer.ssl=on` 到URL路徑的結尾或內嵌程式碼片段中其他檢視器設定引數的清單。 這兩個動作都會強制進行安全的視訊傳送。

如需安全視訊傳送和使用的詳細資訊， `VideoPlayer.ssl` configuration attribute （在URL路徑中），請參閱 [安全視訊傳送](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-viewer-20-securevideodelivery.html) 在檢視器參考指南中。 除了視訊檢視器之外，安全視訊傳送也可用於混合媒體檢視器和互動式視訊檢視器。

### 互動媒體元件 {#interactive-media-component}

互動式媒體元件適用於具有互動性的資產，例如熱點或影像地圖。 如果您有互動式影像、互動式視訊或輪播橫幅，請使用 **[!UICONTROL 互動媒體]** 元件。

此 [!UICONTROL 互動媒體] 元件是智慧型的 — 根據您新增影像或視訊，您有各種選項。 此外，檢視器會回應。 也就是說，熒幕大小會根據熒幕大小自動變更。 所有檢視器都是以HTML5為基礎的檢視器。

![chlimage_1-75](assets/chlimage_1-75a.png)

您可以編輯下列專案 **[!UICONTROL 一般]** 設定(按一下 **[!UICONTROL 編輯]** 在元件中。

**[!UICONTROL 檢視器預設集]**  — 從下拉式選單中選取現有的檢視器預設集。 如果您要尋找的檢視器預設集不可見，您必須使其可見。 檢視器預設集必須先發佈，然後才能使用。 另請參閱 [管理檢視器預設集](/help/assets/managing-viewer-presets.md).

**[!UICONTROL 標題]**  — 變更視訊標題。

**[!UICONTROL 寬度和高度]**  — 如果要讓視訊大小固定，請輸入畫素值。 將這些值保留為空白可使其最適化。

您可以編輯下列專案 **[!UICONTROL 加入購物車]** 設定(按一下 **[!UICONTROL 編輯]** 在元件中。

**[!UICONTROL 顯示產品資產]**  — 預設會選取此值。 產品資產會依商務模組中的定義顯示產品影像。 清除核取記號即可不顯示產品資產。

**[!UICONTROL 顯示產品價格]**  — 預設會選取此值。 產品價格會顯示「商務」模組中定義的專案價格。 清除核取記號即可不顯示產品價格。

**[!UICONTROL 顯示產品表單]**  — 預設不會選取此值。 產品表單包含任何產品變體，例如大小和顏色。 清除核取記號即可不顯示產品變體。
