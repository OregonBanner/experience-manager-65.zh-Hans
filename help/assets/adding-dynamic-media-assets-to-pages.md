---
title: 將Dynamic Media資產新增至頁面
description: 如何將Dynamic Media元件新增至Adobe Experience Manager中的頁面。
uuid: b5e982f5-fa1c-478a-bcb3-a1ef980df201
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 97a5f018-8255-4b87-9d21-4a0fdf740e4d
docset: aem65
role: User, Admin
exl-id: 62d4a38c-2873-4560-8d58-ad172288764d
feature: Components,Publishing
source-git-commit: 5dcea82acdc33c5c2b9e32af412554acd2571281
workflow-type: tm+mt
source-wordcount: '3262'
ht-degree: 5%

---

# 将 Dynamic Media 资源添加到页面{#adding-dynamic-media-assets-to-pages}

若要將Dynamic Media功能新增至您在網站上使用的資產，您可以新增 **Dynamic Media**， **互動媒體**， **全景媒體**，或 **360度影片媒體** 元件直接在頁面上。 若要新增元件，請進入「版面」模式並啟用Dynamic Media元件。 然后，您可以将这些组件添加到页面，并将资产添加到该组件。 Dynamic media组件是智能的——它们知道您添加的是图像还是视频，可用的配置选项会相应地发生更改。

如果您使用Dynamic Media做為WCM，請直接將Adobe Experience Manager資產新增至頁面。 如果您使用協力廠商來處理WCM，請 [連結](/help/assets/linking-urls-to-yourwebapplication.md) 或 [內嵌](/help/assets/embed-code.md) 您的資產。 有关响应式第三方网站，请参阅[将优化的图像交付到响应式网站](/help/assets/responsive-site.md)。

>[!NOTE]
>
>在將資產新增至Experience Manager頁面之前，請務必先發佈資產。 另請參閱 [發佈Dynamic Media資產](/help/assets/publishing-dynamicmedia-assets.md).

## 將Dynamic Media元件新增至頁面 {#adding-a-dynamic-media-component-to-a-page}

新增3D媒體、Dynamic Media、互動媒體、全景媒體、智慧型裁切視訊或360度視訊媒體元件至頁面，與新增元件至任何頁面相同。 以下各節將說明Dynamic Media元件。

**若要將Dynamic Media元件新增至頁面：**

1. 在Experience Manager中，開啟您要新增Dynamic Media元件的頁面。
1. 在頁面左側的面板中（如有必要，請切換側面板的顯示），選取 **[!UICONTROL 元件]** 圖示。
1. 在 **[!UICONTROL 元件]** 標題，在下拉式清單中，選取 **[!UICONTROL Dynamic Media]**.

   如果沒有可用的Dynamic Media元件清單，您必須啟用您要使用的Dynamic Media元件。 另請參閱 [啟用Dynamic Media元件](#enabling-dynamic-media-components).

   ![6_5_360video_wcmcomponent](/help/assets/assets/6_5_360video_wcmcomponent.png)

1. 拖曳 **[!UICONTROL Dynamic Media]** 您要使用的元件，並將其拖曳至頁面上的所需位置。

1. 將滑鼠指標直接停留在元件上。 當元件被藍色方塊包圍時，選取一次以顯示元件的工具列。 選取 **[!UICONTROL 設定（扳手）]** 圖示。

   ![6_5_360video_wcmcomponentconfigure](/help/assets/assets/6_5_360video_wcmcomponentconfigure.png)

1. 視您放置在頁面上的Dynamic Media元件而定，設定對話方塊隨即開啟。 [設定元件的選項](/help/assets/adding-dynamic-media-assets-to-pages.md#dynamic-media-components) 視需要而定。

   以下範例顯示Dynamic Media **[!UICONTROL 360度影片媒體]** 元件對話方塊，以及「檢視器預設集」下拉式清單中可用的選項。

   ![360度影片媒體元件](assets/6_5_360video_wcmcomponentviewerpreset.png)

   Dynamic Media 360度影片媒體元件。

1. 完成後，在對話方塊的右上角，選取核取記號以儲存變更。

### 啟用Dynamic Media元件 {#enabling-dynamic-media-components}

如果沒有可供新增至頁面的Dynamic Media元件，可能表示您必須先啟用您要使用的元件。

**若要啟用Dynamic Media元件：**

1. 在Experience Manager中，開啟您要新增Dynamic Media元件的頁面。
1. 在靠近頁面頂端的工具列左側，選取「頁面資訊」圖示，然後選取 **[!UICONTROL 編輯範本]** 下拉式清單中的。

   ![edit-template](/help/assets/assets-dm/edit-template.png)

1. 在靠近頁面頂端的工具列右側，從下拉式清單中選取 **[!UICONTROL 結構]**.

   ![策略](/help/assets/assets-dm/structure-mode.png)

1. 在頁面底部附近，選取 **[!UICONTROL 配置容器]** 若要開啟其工具列，請選取原則圖示。
1. 於 **[!UICONTROL 配置容器]** 頁面，在 **[!UICONTROL 屬性]** 標題，確認 **[!UICONTROL 允許的元件]** 標籤已選取。

   ![允許的元件](/help/assets/assets-dm/allowed-components.png)

1. 捲動直到您看到 **[!UICONTROL Dynamic Media]**.
1. 選取左側的>圖示 **[!UICONTROL Dynamic Media]** 以便展開清單，然後選取您要啟用的Dynamic Media元件。

   ![Dynamic Media元件清單](/help/assets/assets-dm/dm-components-select.png)

1. 在右上角附近 **[!UICONTROL 配置容器]** 頁面中，選取「完成」 （勾號）圖示。

1. 在靠近頁面頂端的工具列右側，從下拉式清單中選取 **[!UICONTROL 初始內容]**，則 [將Dynamic Media元件新增至頁面](#adding-a-dynamic-media-component-to-a-page) 一如既往。

## 本地化Dynamic Media元件 {#localizing-dynamic-media-components}

您可以透過下列兩種方式之一將Dynamic Media元件當地語系化：

* 在“站点”的网页中，打开“属 **[!UICONTROL 性]** ”，然后选择“ **[!UICONTROL 高级]** ”选项卡。 选择所需的本地化语言。

   ![chlimage_1-172](assets/chlimage_1-538.png)

* 從網站選擇器中，選取所需的頁面或頁面群組。 選取 **[!UICONTROL 屬性]** 並選取 **[!UICONTROL 進階]** 標籤。 选择所需的本地化语言。

   >[!NOTE]
   >
   >並非所有語言都可在 **[!UICONTROL 語言]** 功能表目前有指派的權杖。

## Dynamic Media Components {#dynamic-media-components}

選取「 」時，可使用Dynamic Media元件 **[!UICONTROL 元件]** 圖示，然後篩選 **[!UICONTROL Dynamic Media]**.

可用的Dynamic Media元件包括：

* **[!UICONTROL Dynamic Media]** - 用于图像、视频、电子目录和旋转集等资产。
* **[!UICONTROL 互動媒體]**  — 用於任何互動式資產，例如互動式視訊、互動式影像或轉盤集。
* **[!UICONTROL 全景媒體]**  — 用於全景影像或全景VR影像資產。
* **[!UICONTROL 360度影片媒體]**  — 用於360視訊和360 VR視訊資產。

>[!NOTE]
>
>預設不會提供這些元件；您必須透過範本編輯器提供這些元件，才能使用它們。 [在可供使用之後，請](/help/sites-authoring/templates.md#editing-templates-template-authors)在範本編輯器中，您可以將元件新增至頁面，就像新增任何其他Experience Manager元件一樣。

![6_5_dynamicmediawcmcomponents](assets/6_5_dynamicmediawcmcomponents.png)

### Dynamic Media元件 {#dynamic-media-component}

Dynamic Media元件是智慧型的。 無論您新增影像或影片，都有各種選項。 元件支援影像預設集、影像型檢視器（例如影像集、迴轉集、混合媒體集和視訊）。 此外，檢視器會回應 — 熒幕大小會自動根據熒幕大小變更。 所有檢視器皆為HTML5檢視器。

>[!NOTE]
>
>如果您的網頁有以下內容：
>
>* 相同頁面上使用了多個Dynamic Media元件例項。
>* 每個例項都使用相同的資產型別。
>
>不支援為該頁面上的每個Dynamic Media元件指派不同的檢視器預設集。
>
>不過，您可以在頁面內，為所有使用相同型別資產的Dynamic Media元件使用相同的檢視器預設集。

新增Dynamic Media元件時，以及 **[!UICONTROL Dynamic Media設定]** 為空白或無法正確新增資產，請檢查下列專案：

* 您有 [已啟用Dynamic Media](/help/assets/config-dynamic.md). Dynamic Media預設為停用。
* 影像具有金字塔tiff檔案。 啟用Dynamic Media之前匯入的影像沒有金字塔tiff檔案。

#### 使用影像時 {#when-working-with-images}

Dynamic Media元件可讓您新增動態影像，包括影像集、迴轉集及混合媒體集。 您可以放大、縮小旋轉集內的影像，或是從其他型別的旋轉集中選取影像（如果適用）。

您也可以直接在元件中設定檢視器預設集、影像預設集或影像格式。 若要使影像具有回應性，您可以設定中斷點或套用回應性影像預設集。

選取「 」，編輯下列Dynamic Media設定 **[!UICONTROL 編輯]** 圖示，然後 **[!UICONTROL Dynamic Media設定]**.

![dm-settings-image-preset](assets/dm-settings-image-preset.png)

>[!NOTE]
>
>默认情况下，Dynamic media图像组件是自适应的。 如果要使其变为固定大小，请在“高级”选项卡的组件中设置 **[!UICONTROL 它]** ，并使用“宽度”和“高 **** 度” ****。

* **[!UICONTROL 檢視器預設集]**  — 從下拉式選單中選取現有的檢視器預設集。 如果您要尋找的檢視器預設集不可見，您必須使其可見。 另請參閱 [管理檢視器預設集](/help/assets/managing-viewer-presets.md). 如果您使用影像預設集，則無法選取檢視器預設集，反之亦然。

   只有當您檢視影像集、迴轉集或混合媒體集時，才能使用此選項。 顯示的檢視器預設集是智慧型的 — 只會顯示相關的檢視器預設集。

* **[!UICONTROL 檢視器修飾元]**  — 檢視器修飾元採用name=value搭配&amp;分隔字元的形式，可讓您依照《檢視器參考指南》中的概述變更檢視器。 檢視器修飾元的範例為 `posterimage=img.jpg&caption=text.vtt,1` 這會為視訊縮圖設定不同的影像，並將隱藏式字幕/字幕檔案與視訊建立關聯。

* **[!UICONTROL 影像預設集]**  — 從下拉式選單中選取現有的影像預設集。 如果您要尋找的影像預設集不可見，您必須使其可見。 請參閱管理影像預設集。 如果您使用影像預設集，則無法選取檢視器預設集，反之亦然。

   如果您檢視影像集、迴轉集或混合媒體集，則此選項不可用。

* **[!UICONTROL 影像修飾元]**  — 您可以透過提供其他影像指令來套用影像效果。 這些效果在「影像預設集」和「影像伺服命令」參考中進行了說明。

   如果您檢視影像集、迴轉集或混合媒體集，則此選項不可用。

* **[!UICONTROL 中斷點]**  — 如果您在回應式網站上使用此資產，必須新增影像中斷點。 影像中斷點以逗號(，)分隔。 影像預設集中未定義高度或寬度時，此選項即會運作。

   如果您檢視影像集、迴轉集或混合媒體集，則此選項不可用。

   您可以選取「 」，編輯下列進階設定 **[!UICONTROL 編輯]** 在元件中。

* **[!UICONTROL 針對更高解析度的裝置最佳化]**  — 選取（預設）核取方塊以允許DPR （裝置畫素比率）最佳化。

   此 **[!UICONTROL 針對更高解析度的裝置最佳化]** 選項僅在下列為true時顯示：

   * 在「預設集型別」下， **[!UICONTROL 影像預設集]** 「 」已選取，並且 **[!UICONTROL RESS_IP]** 是從 **[!UICONTROL 影像預設集]** 下拉式清單。

   ![影像預設集的裝置畫素比設定](/help/assets/assets-dm/dpr-ress-ip.png)

   另請參閱 [關於裝置畫素比最佳化](/help/assets/imaging-faq.md#dpr). 任何Adobe Experience Manager Dynamic Media智慧型影像DPR值都會被忽略。

* **[!UICONTROL 標題]**  — 變更影像的標題。

* **[!UICONTROL 替代文字]**  — 為已關閉圖形的使用者新增影像標題。

   如果您檢視影像集、迴轉集或混合媒體集，則此選項不可用。

* **[!UICONTROL URL，開啟位置]**  — 您可以設定資產以開啟連結。 設定URL，並在「開啟」中指定您要在同一個視窗或新視窗中開啟。

   如果您檢視影像集、迴轉集或混合媒體集，則此選項不可用。

* **[!UICONTROL 寬度]**  — 如果您希望影像為固定大小，請輸入畫素值。 將此值保留空白可讓資產適應新情況。

* **[!UICONTROL 高度]**  — 如果您希望影像為固定大小，請輸入畫素值。 將此值保留空白可讓資產適應新情況。

#### 使用視訊時 {#when-working-with-video}

使用Dynamic Media元件將動態視訊新增至您的網頁。 編輯元件時，您可以選擇使用預先定義的視訊檢視器預設集在頁面上播放視訊。

![chlimage_1-173](assets/chlimage_1-540.png)

選取「 」，編輯下列Dynamic Media設定 **[!UICONTROL 編輯]** 在元件中。

>[!NOTE]
>
>依預設，Dynamic Media視訊元件是自我調整的。 如果要使其成為固定大小，請在元件中設定它，並使用 **[!UICONTROL 寬度]** 和 **[!UICONTROL 高度]** 在 **[!UICONTROL 進階]** 標籤。

* **[!UICONTROL 檢視器預設集]**  — 從下拉式選單中選取現有的視訊檢視器預設集。 如果您要尋找的檢視器預設集不可見，您必須使其可見。 另請參閱 [管理檢視器預設集](/help/assets/managing-viewer-presets.md).

* **[!UICONTROL 檢視器修飾元]**  — 檢視器修飾元採用名稱=值配對及&amp;分隔字元的形式，可讓您依照Adobe檢視器參考指南中的概述變更檢視器。 檢視器修飾元的範例為 `posterimage=img.jpg&caption=text.vtt,1`

   例如，您可以使用檢視器修飾元執行下列動作：

   * 將註解檔案與視訊建立關聯： [註解](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-caption.html)
   * 將導覽檔案與視訊建立關聯： [導覽](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-navigation.html)

      您可以選取「 」，編輯下列進階設定 **[!UICONTROL 編輯]** 在元件中。

* **[!UICONTROL 標題]**  — 變更視訊標題。

* **[!UICONTROL 寬度]**  — 如果您希望影像為固定大小，請輸入畫素值。 將此值保留空白可讓資產適應新情況。

* **[!UICONTROL 高度]**  — 如果您希望影像為固定大小，請輸入畫素值。 將此值保留空白可讓資產適應新情況。

#### 使用智慧型裁切時 {#when-working-with-smart-crop}

使用Dynamic Media元件將智慧型裁切影像資產新增至您的網頁。 編輯元件時，您可以選擇使用預先定義的視訊檢視器預設集在頁面上播放視訊。

另請參閱 [影像設定檔](/help/assets/image-profiles.md).

![dm-settings-smart-crop](assets/dm-settings-smart-crop.png)

選取以編輯下列Dynamic Media設定 **[!UICONTROL 編輯]** 在元件中。

>[!NOTE]
>
>默认情况下，Dynamic media图像组件是自适应的。 如果要使其变为固定大小，请在“高级”选项卡的组件中设置 **[!UICONTROL 它]** ，并使用“宽度”和“高 **** 度” ****。

* **[!UICONTROL 影像修飾元]**  — 您可以透過提供其他影像指令來套用影像效果。 這些效果在「影像預設集」和「影像伺服命令」參考中進行了說明。

   如果您檢視影像集、迴轉集或混合媒體集，則此選項不可用。

   您可以選取「 」，編輯下列進階設定 **[!UICONTROL 編輯]** 在元件中。

* **[!UICONTROL 啟用長寬比相符]**  — 若要讓Dynamic Media挑選外觀比例最符合原始影像外觀比例的智慧型裁切轉譯，請選取此選項。

* **[!UICONTROL 針對更高解析度的裝置最佳化]**  — 選取（預設）核取方塊以允許DPR （裝置畫素比率）最佳化。

   此 **[!UICONTROL 針對更高解析度的裝置最佳化]** 選項僅在下列為true時顯示：

   * 在「預設集型別」下， **[!UICONTROL 智慧型裁切]** 選項時才會選擇此選項。

   ![智慧型裁切的裝置畫素比設定](/help/assets/assets-dm/dpr-smartcrop.png)

   另請參閱 [關於裝置畫素比最佳化](/help/assets/imaging-faq.md#dpr). 任何Adobe Experience Manager Dynamic Media智慧型影像DPR值都會被忽略。

* **[!UICONTROL 標題]**  — 變更智慧型裁切影像的標題。

* **[!UICONTROL 替代文字]**  — 為已關閉圖形的使用者新增標題至智慧型裁切影像。

   如果您檢視影像集、迴轉集或混合媒體集，則此選項不可用。

* **[!UICONTROL URL，開啟位置]**  — 您可以設定資產以開啟連結。 設定URL，並在「開啟」中指定您要在同一個視窗或新視窗中開啟。

   如果您檢視影像集、迴轉集或混合媒體集，則此選項不可用。

* **[!UICONTROL 寬度]**  — 如果您希望影像為固定大小，請輸入畫素值。 將此值保留空白可讓資產適應新情況。

* **[!UICONTROL 高度]**  — 如果您希望影像為固定大小，請輸入畫素值。 將此值保留空白可讓資產適應新情況。

### 互動媒體元件 {#interactive-media-component}

互動式媒體元件適用於具有互動性的資產，例如熱點或影像地圖。 如果您有互動式影像、互動式視訊或輪播橫幅，請使用 **[!UICONTROL 互動媒體]** 元件。

互動媒體元件是智慧型的。 無論您新增影像或影片，都有各種選項。 此外，檢視器會回應 — 熒幕大小會自動根據熒幕大小變更。 所有檢視器皆為HTML5檢視器。

>[!NOTE]
>
>如果您的網頁有以下內容：
>
>* 在相同頁面上使用的多個互動式媒體元件例項。
>* 每個例項都使用相同的資產型別。
>
>不支援為該頁面上的每個互動媒體元件指派不同的檢視器預設集。
>
>不過，您可以對頁面內使用相同型別資產的所有互動式媒體元件使用相同的檢視器預設集。

![chlimage_1-174](assets/chlimage_1-541.png)

您可以編輯下列專案 **[!UICONTROL 一般]** 設定，方法是選取 **[!UICONTROL 編輯]** 在元件中。

* **[!UICONTROL 檢視器預設集]**  — 從下拉式選單中選取現有的檢視器預設集。 如果您要尋找的檢視器預設集不可見，您必須使其可見。 檢視器預設集必須先發佈，然後才能使用。 請參閱管理檢視器預設集。

* **[!UICONTROL 標題]**  — 變更視訊標題。

* **[!UICONTROL 寬度]**  — 如果您希望影像為固定大小，請輸入畫素值。 將此值保留空白可讓資產適應新情況。

* **[!UICONTROL 高度]**  — 如果您希望影像為固定大小，請輸入畫素值。 將此值保留空白可讓資產適應新情況。

   您可以編輯下列專案 **[!UICONTROL 加入購物車]** 設定，方法是選取 **[!UICONTROL 編輯]** 在元件中。

* **[!UICONTROL 顯示產品資產]**  — 預設會選取此值。 產品資產會依商務模組中的定義顯示產品影像。 清除核取記號即可不顯示產品資產。

* **[!UICONTROL 顯示產品價格]**  — 預設會選取此值。 產品價格會顯示「商務」模組中定義的專案價格。 清除核取記號即可不顯示產品價格。

* **[!UICONTROL 顯示產品表單]**  — 預設不會選取此值。 產品表單包含任何產品變體，例如大小和顏色。 清除核取記號即可不顯示產品變體。

### 全景媒體元件 {#panoramic-media-component}

全景媒體元件適用於球面全景影像的資產。 這類影像可提供360度的房間、屬性、位置或橫向觀賞體驗。 若要讓影像符合球面全景的條件，它必須具備下列其中一項（或）兩項：

* 外觀比例為2:1。
* 以關鍵字標籤 `equirectangular` 或(`spherical` + `panorama`)或(`spherical` + `panoramic`)。 另請參閱 [使用標籤](/help/sites-authoring/tags.md).

纵横比和关键字条件都适用于资产详细信息页面和&#x200B;**[!UICONTROL 全景媒体]** WCM 组件的全景资产。

>[!NOTE]
>
>如果您的網頁有以下內容：
>
>* 的多個執行個體 **[!UICONTROL 全景媒體]** 在相同頁面上使用的元件。
>* 每個例項都使用相同的資產型別。
>
>指派不同的檢視器預設集給每個檢視器 **[!UICONTROL 全景媒體]** 不支援該頁面上的元件。
>
>不過，您可以對頁面內使用相同資產型別的所有「全景媒體」元件，使用相同的檢視器預設集。

![panoramic-media-viewer-preset](assets/panoramic-media-viewer-preset.png)

您可以選取「 」，編輯下列設定 **[!UICONTROL 設定]** 在元件中。

* **[!UICONTROL 檢視器預設集]**  — 從「檢視器預設集」下拉式選單中選取現有的檢視器。

如果您要尋找的檢視器預設集不可見，請檢查以確保其已發佈。 請先發佈檢視器預設集，然後再使用。 另請參閱 [管理檢視器預設集](/help/assets/managing-viewer-presets.md).

### 360度影片媒體元件 {#video-media-component}

使用 **[!UICONTROL 360度影片媒體]** 此元件可在網頁上呈現等角視訊，以提供房間、屬性、位置、橫向或醫療程式的沈浸式檢視體驗。

在平面顯示器上播放期間，使用者可以控制視角；行動裝置上的播放通常使用其內建的陀螺儀控制項。

檢視器包含原生支援，可傳送360個視訊資產。 依預設，檢視或播放不需要額外的設定。 您會使用標準視訊副檔名（例如.mp4、.mkv和.mov）來傳送360視訊。 最常見的轉碼器是H.264。

![6_5_360video_wcmcomponent-1](assets/6_5_360video_wcmcomponent-1.png)

您可以選取「 」，編輯下列設定 **[!UICONTROL 設定]** 在元件中。

* **[!UICONTROL 檢視器預設集]**  — 從「檢視器預設集」下拉式選單中選取現有的檢視器。 使用Video360VR的使用者若使用虛擬實境眼鏡，即可使用。 包含基本視訊播放控制項和社群媒體功能。 使用包含基本視訊播放控制項的Video360_social。 視訊演算是以立體聲模式完成。 手動視點控制已關閉，但陀螺儀控制已開啟。 沒有社群媒體功能。

如果您要尋找的檢視器預設集不可見，請檢查以確保其已發佈。 使用檢視器預設集之前，請務必先發佈檢視器預設集。 另請參閱 [管理檢視器預設集](/help/assets/managing-viewer-presets.md).

### 使用HTTP/2傳遞Dynamic Media資產 {#using-http-to-delivery-dynamic-media-assets}

HTTP/2是新的、更新的Web通訊協定，可改善瀏覽器和伺服器的通訊方式。 它提供更快速的資訊傳輸，並減少所需的處理能力。 Dynamic Media資產的傳送現在可透過HTTP/2進行，以提供更佳的回應和載入時間。

另請參閱 [HTTP2傳送內容](/help/assets/http2.md) 以取得開始使用HTTP/2與Dynamic Media帳戶的完整詳細資訊。

>[!MORELIKETHIS]
>
>* [在Experience ManagerDynamic Media中使用視訊播放器](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/video/dynamic-media-video-player-feature-video-use.html)
>* [搭配使用互動式視訊與Experience ManagerDynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/video/dynamic-media-interactive-video-feature-video-use.html)
>* [透過Experience ManagerDynamic Media瞭解資產檢視器](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/viewers/dynamic-media-viewer-feature-video-understand.html)
>* [透過Experience ManagerDynamic Media使用自訂視訊縮圖](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/video/dynamic-media-video-thumbnails-feature-video-use.html)
>* [透過Experience ManagerDynamic Media瞭解色彩管理](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-color-management-technical-video-setup.html)
>* [搭配Experience ManagerDynamic Media使用影像銳利化](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-image-sharpening-feature-video-use.html)

