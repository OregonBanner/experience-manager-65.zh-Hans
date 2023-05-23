---
title: 管理檢視器預設集
description: 如何在Dynamic Media中建立、編輯和管理檢視器預設集。
uuid: 64fcf16a-7c4a-435b-bf1a-f27b8b39a715
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: cf7823f4-82c2-4e36-9b65-3c58359b8104
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/viewer-presets
feature: Viewer Presets
role: User, Admin
exl-id: 0899e497-88e9-4fc3-a6be-b3a149fb5b32
source-git-commit: a95255594ec03c152cd96df48597ced5fce4b315
workflow-type: tm+mt
source-wordcount: '4519'
ht-degree: 8%

---

# 管理檢視器預設集{#managing-viewer-presets}

檢視器預設集是設定集合，可決定使用者在其電腦熒幕和行動裝置上檢視多媒體資產的方式。 如果您是管理員，可以建立檢視器預設集。 設定可供一系列檢視器組態選項使用。 例如，您可以變更檢視器顯示大小或縮放行為。

如需建立和自訂您自己的HTML5檢視器預設集的指示，請參閱AdobeDynamic Media *HTML5檢視器SDK API檔案*. SDK內嵌於SDK本身的IS發佈伺服器上，可供使用。 每個程式庫版本都有各自的SDK檔案。

路径: `<scene7_domain>/s7sdk/<library_version>/docs/jsdocs/index.html`.\
例如，3.10 SDK： [https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html)

另請參閱 [AdobeDynamic Media檢視器參考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html).

本節說明如何建立、編輯及管理檢視器預設集。 您可以隨時將檢視器預設集套用至資產預覽。 另請參閱 [套用檢視器預設集](#applying-a-viewer-preset-to-an-asset).

>[!NOTE]
>
>編輯任何 *預先定義的現成檢視器預設集* 不是支援的情況。 如果您嘗試編輯現成的檢視器預設集，系統會提示您使用新名稱儲存檢視器預設集。

## 檢視器的鍵盤協助工具 {#keyboard-accessibility-for-viewers}

所有開箱即用的檢視器都支援鍵盤協助功能。

另請參閱 [鍵盤協助工具與導覽](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html).

## 管理檢視器預設集 {#managing-viewer-presets-1}

您可以點選，在Adobe Experience Manager中新增、編輯、刪除、發佈、取消發佈和預覽檢視器預設集 **[!UICONTROL 工具]** （槌子圖示） > **[!UICONTROL 資產]** > **[!UICONTROL 檢視器預設集]**.

![6_5_tools-assets-viewerpresets](assets/6_5_tools-assets-viewerpresets.png)

>[!NOTE]
>
>依預設，當您在資產的詳細資料檢視中選取「檢視器」時，系統會顯示15個檢視器預設集。 您可以提高此限制。请参阅[增加显示的查看器预设数量](#increasing-the-number-of-viewer-presets-that-display)。

### 回應式設計網頁的檢視器支援 {#viewer-support-for-responsive-designed-web-pages}

不同的網頁有不同的需求。 例如，有時您會想要一個網頁，提供可在個別瀏覽器視窗中開啟HTML5檢視器的連結。 在其他情況下，您可能需要直接將HTML5檢視器內嵌在託管頁面上。 在後一種情況下，網頁可能具有靜態配置。 或者，它可能會是「回應式」的，且在不同裝置或不同瀏覽器視窗大小中顯示的方式會有所不同。 為了滿足這些需求，Dynamic Media隨附的所有預先定義、現成可用的HTML5檢視器都支援靜態網頁和回應式設計的網頁。

另請參閱 [Responsive影像資料庫](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/responsive-static-image-library/c-about-responsive-static-image-library.html) 瞭解更多有關如何將回應式檢視器內嵌至網頁的資訊。

>[!NOTE]
>
>在第一次使用現成可用的檢視器之前，請先發佈這些檢視器。
>另請參閱 [發佈檢視器預設集].(#publishing-viewer-presets)

### 檢視器預設集系統相容性 {#viewer-preset-system-compatibility}

Dynamic Media隨附的所有現成可用的檢視器預設集都與下列系統完全相容：

* 桌上型
* Apple iPhone
* Apple iPad
* Android™智慧型手機
* Android™平板電腦
* 視訊額外支援MP4播放，適用於 [BlackBerry®](https://developer.blackberry.com/devzone/develop/supported_media/bb_media_support_at_a_glance.html#kba1328730952678) 和 [Windows Phone](https://learn.microsoft.com/en-us/windows/uwp/audio-video-camera/supported-codecs).

### 檢視器預設集的多媒體型別 {#rich-media-types-for-viewer-presets}

建立檢視器預設集時，管理員可以新增和自訂以下多媒體型別。

<table>
 <tbody>
  <tr>
   <td><strong>轮播集</strong><br /> </td>
   <td><p>熱點、影像地圖、或兩者都會新增至一連串的兩個或多個影像中。 客戶可以將影像向左或向右平移，然後在影像上選取熱點，以取得更多詳細資訊或直接從網站的類別、首頁或登陸頁面購買。</p> </td>
  </tr>
  <tr>
   <td><strong>尺寸</strong><br /> </td>
   <td><p>顯示可讓您旋轉、平移、縮放或重新置入相機的3D場景。</p> </td>
  </tr>
  <tr>
   <td><strong>弹出缩放</strong></td>
   <td><p>在原始影像旁顯示縮放區域的第二個影像。 沒有要使用的控制項 — 使用者將選取範圍移動到他們想要檢視的區域。</p> <p>判斷此檢視器的完整頻寬使用量時，請考量檢視器中會同時提供主要影像和彈出式影像。 主要影像大小（「舞台寬度」和「高度」）和「縮放因數」會決定彈出式影像大小。 若要避免彈出式檔案變得太大，請平衡這兩個值：如果您有大的主要影像大小，請降低「縮放因數」值。 （「彈出式寬度」和「彈出式高度」會決定彈出式視窗的大小，但不會決定提供給檢視器的彈出式影像的大小。）</p> <p>例如，如果您的主要影像大小為350 x 350畫素，縮放係數為3，則產生的彈出式影像為1050 x 1050畫素。 如果您的主要影像大小為300 x 300畫素，縮放係數為4，則彈出式影像為1200 x 1200畫素。 根據JPEG品質設定（建議的設定介於80到90之間），您可以大幅減少檔案大小。 建議縮放因數為2.5至4，視您主影像的大小而定。</p> </td>
  </tr>
  <tr>
   <td><strong>內嵌縮放</strong></td>
   <td>在原始檢視器中顯示縮放區域的影像。 沒有要使用的控制項。 也就是說，使用者會將選取範圍移動到他們想要檢視的區域上。</td>
  </tr>
  <tr>
   <td><strong>图像集</strong></td>
   <td>在「影像集」檢視器中，使用者可以透過選取縮圖影像來檢視專案的不同檢視或顏色變化。 此檢視器還提供縮放工具，以便更密切地檢查影像。</td>
  </tr>
  <tr>
   <td><strong>交互式图像</strong></td>
   <td>連結區會新增至影像的某些部分，然後客戶可以選取這些部分以取得其他詳細資訊，或直接從網站的類別、首頁或登入頁面進行購買。</td>
  </tr>
  <tr>
   <td><strong>交互式视频</strong></td>
   <td>縮圖會新增至影片中的時間軸區段，然後客戶可選取該區段以取得其他詳細資訊，或直接從網站的類別、首頁或登入頁面進行購買。</td>
  </tr>
  <tr>
   <td><strong>混合媒体</strong></td>
   <td>在一個檢視器中顯示不同型別的媒體。 您可以包含迴轉集、影像集、影像和視訊。</td>
  </tr>
  <tr>
   <td><strong>全景图像</strong></td>
   <td><p>「全景影像」和「全景VR」檢視器可呈現球面全景影像，讓使用者沈浸在房間、屬性、位置或橫向的360度檢視體驗中。</p> <p>若要讓上傳的影像符合球面全景的條件，它必須具備下列其中一項或兩項條件：</p>
    <ul>
     <li>外觀比例為2:1。</li>
     <li>以關鍵字標籤 <code>equirectangular</code>，或 <code>spherical</code> 和 <code>panorama</code>，或 <code>spherical </code>和 <code>panoramic</code>. 另請參閱 <a href="/help/sites-authoring/tags.md">使用標籤</a>.</li>
    </ul> <p>外觀比例和關鍵字條件都適用於資產詳細資訊頁面和「全景媒體」WCM元件的全景資產。</p> <p><strong>重要</strong>：此檢視器僅適用於Dynamic Media - Scene7模式。</p> </td>
  </tr>
  <tr>
   <td><strong>智能裁剪视频</strong><br /> </td>
   <td><p>使用此檢視器可自動偵測並裁切至任何視訊中的焦點。</p> </td>
  </tr>
  <tr>
   <td><strong>旋转集</strong></td>
   <td>提供影像的多個檢視，讓使用者可以轉動物件來檢查不同的側邊和角度。</td>
  </tr>
  <tr>
   <td><strong>360度影片</strong></td>
   <td><p>使用360/VR視訊檢視器可呈現等矩形的視訊，以沈浸式地檢視房間、屬性、位置、橫向或醫療程式。</p> <p>在平面顯示器上播放期間，使用者可以控制視角；在行動裝置上播放通常會套用其內建的陀螺儀控制項。</p> <p>檢視器包含原生支援，可傳送360個視訊資產。 依預設，檢視或播放不需要額外的設定。 您會使用標準視訊副檔名（例如.mp4、.mkv和.mov）來傳送360視訊。 最常見的轉碼器是H.264。</p> <p><strong>重要</strong>：此檢視器僅適用於Dynamic Media - Scene7模式。</p> </td>
  </tr>
  <tr>
   <td><strong>视频</strong></td>
   <td><p>使用漸進式或自我調整位元速率串流播放視訊。 最適化位元速率串流會自動執行裝置和頻寬偵測，以正確的格式提供正確的品質視訊。</p> </td>
  </tr>
  <tr>
   <td><strong>垂直縮放</strong></td>
   <td><p>垂直縮放檢視器可讓您最大化產品影像檢視體驗，讓使用者以最佳方式呈現產品。 色票的垂直位置會執行下列動作：</p>
    <ul>
     <li>確保色票「高於摺頁」。<br/> 對於水準色票，視使用者的案頭熒幕大小而定，直到使用者向下捲動頁面才會顯示。 將色票垂直放置在檢視器中，可確保無論使用者的熒幕大小如何，都能看到色票。</li>
     <li>最大化主要影像大小。<br /> 使用水準色票時，必須在頁面上保留空間，以確保可看見色票。 此定位縮小了主要影像的大小。 不過，如果是垂直色票版面配置，則不需要配置此空間。 因此，您可以將主要影像大小最大化。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>缩放</strong></td>
   <td>可讓使用者透過選取區域來放大該區域。 使用者可以選取控制項來放大、縮小影像，以及將影像重設為預設大小。</td>
  </tr>
 </tbody>
</table>

### 現成可用的檢視器預設集清單 {#list-of-out-of-the-box-viewer-presets}

下表列出Dynamic Media隨附的所有預先定義、立即可用的檢視器預設集。

另請參閱 [即時示範](https://landing.adobe.com/zh-Hans/na/dynamic-media/ctir-2755/live-demos.html).

如需有關檢視器支援的網頁瀏覽器和作業系統版本的資訊，您可以檢閱「檢視器發行說明」。

請參閱目錄中的「檢視器發行說明」。 [檢視器參考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html).

>[!NOTE]
>
>Dynamic Media中的所有現成可用的檢視器預設集都已啟動（開啟），但您必須發佈它們。
>另請參閱 [發佈檢視器預設集](#publishing-viewer-presets).
>
>您建立和新增的任何新檢視器預設集都必須啟動*和*已發佈。
>另請參閱 [啟用或停用檢視器預設集](#activating-or-deactivating-viewer-presets) 和 [發佈檢視器預設集](#publishing-viewer-presets).

<table>
 <tbody>
  <tr>
   <td><strong>檢視器預設集標題</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>CSS 文件名称</strong><br /> </td>
  </tr>
  <tr>
   <td>Carousel_Dotted_dark</td>
   <td>Carusel_Set</td>
   <td><code>html5_carouselviewer_dotted_dark.css</code></td>
  </tr>
  <tr>
   <td>Carousel_Dotted_light</td>
   <td>Carusel_Set</td>
   <td><code>html5_carouselviewer_dotted_light.css</code></td>
  </tr>
  <tr>
   <td>Carousel_Numeric_dark</td>
   <td>Carusel_Set</td>
   <td><code>html5_carouselviewer_numeric_dark.css</code></td>
  </tr>
  <tr>
   <td>Carousel_Numeric_light</td>
   <td>Carusel_Set</td>
   <td><code>html5_carouselviewer_numeric_light.css</code></td>
  </tr>
  <tr>
   <td>尺寸</td>
   <td>尺寸</td>
   <td><code>html5_dimensionalviewer.css</code></td>
  </tr>
  <tr>
   <td>彈出</td>
   <td>Flyout_Zoom</td>
   <td><code>html5_flyoutviewer.css</code></td>
  </tr>
  <tr>
   <td>ImageSet_dark</td>
   <td>图像集</td>
   <td><code>html5_zoomviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>ImageSet_light</td>
   <td>图像集</td>
   <td><code>html5_zoomviewer_light.css</code></td>
  </tr>
  <tr>
   <td>InlineMixedMedia_dark</td>
   <td>混合媒體</td>
   <td><code>html5_inlinemixedmediaviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>InlineMixedMedia_light</td>
   <td>混合媒體</td>
   <td><code>html5_inlinemixedmediaviewer_light.css</code></td>
  </tr>
  <tr>
   <td>InlineZoom</td>
   <td>Flyout_Zoom</td>
   <td><code>html5_inlinezoomviewer.css</code></td>
  </tr>
  <tr>
   <td>MixedMedia_dark</td>
   <td>混合媒體</td>
   <td><code>html5_mixedmediaviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>MixedMedia_light</td>
   <td>混合媒體</td>
   <td><code>html5_mixedmediaviewer_light.css</code></td>
  </tr>
  <tr>
   <td>全景影像</td>
   <td>Panoramic_Image</td>
   <td><code>html5_panoramicimage.css</code></td>
  </tr>
  <tr>
   <td>PanoramicImageVR</td>
   <td>Panoramic_Image</td>
   <td><code>html5_panoramicimage.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Banner</td>
   <td>Interactive_Image</td>
   <td><code>html5_interactiveimage.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Video_dark</td>
   <td>互動視訊</td>
   <td><code>html5_interactivevideoviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Video_light</td>
   <td>互動視訊</td>
   <td><code>html5_interactivevideovewer_light.css</code></td>
  </tr>
  <tr>
   <td>SmartCropVideo</td>
   <td>Smart_Crop_Video</td>
   <td><code>html5_smartcropvideoviewer.css</code></td>
  </tr>
  <tr>
   <td>SmartCropVideo_social</td>
   <td>Smart_Crop_Video</td>
   <td><code>html5_smartcropvideoviewersocial.css</code></td>
  </tr>
  <tr>
   <td>SpinSet_dark</td>
   <td>迴轉集</td>
   <td><code>html5_spinviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>SpinSet_light</td>
   <td>迴轉集</td>
   <td><code>html5_spinviewer_light.css</code></td>
  </tr>
  <tr>
   <td><p>视频</p> <p>（包含隱藏式字幕支援）</p> </td>
   <td>视频</td>
   <td><code>html5_videoviewer.css</code></td>
  </tr>
  <tr>
   <td><p>Video360_social</p> <p>（包括基本視訊播放控制、視訊演算在立體聲模式下完成、手動視點控制關閉但陀螺控制開啟，以及無社群媒體功能）</p> </td>
   <td>Video_360</td>
   <td><code>html5_video360viewersocial.css</code></td>
  </tr>
  <tr>
   <td><p>Video360VR</p> <p>(專為使用虛擬現實眼鏡的使用者所設計。 包含基本視訊播放控制項和社群媒體功能)</p> </td>
   <td>Video_360</td>
   <td><code>html5_video360viewer.css</code></td>
  </tr>
  <tr>
   <td><p>Video_social</p> <p>（包括隱藏式字幕和社群媒體的支援）</p> </td>
   <td>视频</td>
   <td><code>html5_videoviewersocial.css</code></td>
  </tr>
  <tr>
   <td>Zoom_dark<br /> </td>
   <td>缩放<br /> </td>
   <td><code>html5_basiczoomviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>Zoom_light<br /> </td>
   <td>缩放</td>
   <td><code>html5_basiczoomviewer_light.css</code></td>
  </tr>
  <tr>
   <td>ZoomVertical_dark<br /> </td>
   <td>Vertical_Zoom</td>
   <td><code>html5_zoomverticalviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>ZoomVertical_light</td>
   <td>Vertical_Zoom</td>
   <td><code>html5_zoomverticalviewer_light.css</code></td>
  </tr>
 </tbody>
</table>

### 支援的行動檢視器手勢矩陣 {#supported-mobile-viewers-gestures-matrix}

下表識別iOS、Android™ 2.x和Android™ 3.x裝置支援的行動檢視器手勢。

<table>
 <tbody>
  <tr>
   <td><strong>手勢</strong></td>
   <td><strong>弹出缩放</strong></td>
   <td><strong>缩放</strong></td>
   <td><strong>旋转</strong></td>
  </tr>
  <tr>
   <td><p><strong>拖曳</strong></p> </td>
   <td><p>Pans</p> </td>
   <td><p>Pans</p> </td>
   <td><p>Pans</p> </td>
  </tr>
  <tr>
   <td><p><strong>选择</strong></p> </td>
   <td><p>顯示彈出式視窗</p> </td>
   <td><p>顯示或隱藏使用者介面</p> </td>
   <td><p>顯示或隱藏使用者介面</p> </td>
  </tr>
  <tr>
   <td><p><strong>點兩下</strong></p> </td>
   <td><p>不適用</p> </td>
   <td><p>放大或重設</p> </td>
   <td><p>放大或重設</p> </td>
  </tr>
  <tr>
   <td><p><strong>捏合開啟</strong></p> </td>
   <td><p>不適用</p> </td>
   <td><p>放大(僅限iOS和Android™ 3x)</p> </td>
   <td><p>放大(僅限iOS和Android™ 3x)</p> </td>
  </tr>
  <tr>
   <td><p><strong>捏合關閉</strong></p> </td>
   <td><p>不適用</p> </td>
   <td><p>縮小顯示(僅限iOS和Android™ 3x)</p> </td>
   <td><p>縮小顯示(僅限iOS和Android™ 3x)</p> </td>
  </tr>
  <tr>
   <td><p><strong>轻扫</strong></p> </td>
   <td><p>捲動色票列</p> </td>
   <td><p>捲動影像</p> </td>
   <td><p>旋轉</p> </td>
  </tr>
  <tr>
   <td><p><strong>輕觸</strong></p> </td>
   <td><p>捲動色票列</p> </td>
   <td><p>捲動影像</p> </td>
   <td><p>旋轉</p> </td>
  </tr>
 </tbody>
</table>

## 增加顯示的檢視器預設集數目 {#increasing-the-number-of-viewer-presets-that-display}

Experience Manager在檢視資產時會顯示各種不同的檢視器預設集 **[!UICONTROL 詳細資料檢視]** > **[!UICONTROL 檢視者]**. 您可以增加或減少顯示的檢視器數量。

**增加顯示的檢視器預設集數目：**

1. 導覽至CRXDE Lite([https://localhost:4502/crx/de](https://localhost:4502/crx/de))。
1. 導覽至檢視器預設集清單節點，位置如下：

   `/libs/dam/gui/coral/content/commons/sidepanels/viewerpresets/viewerpresetslist`

   ![chlimage_1-221](assets/chlimage_1-221.png)

1. 在 **[!UICONTROL limit]** 属性中，将默认设 **[!UICONTROL 置为15的Value]**（值）更改为所需的数字。
1. 導覽至檢視器預設集資料來源，網址為 `/libs/dam/gui/coral/content/commons/sidepanels/viewerpresets/viewerpresetslist/datasource`

   ![chlimage_1-222](assets/chlimage_1-222.png)

1. 在limit屬性中，將數字變更為所需的數字，例如 `{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`
1. 選取 **[!UICONTROL 全部儲存]**.

## 建立檢視器預設集 {#creating-a-new-viewer-preset}

建立檢視器預設集可讓您套用各種設定來檢視資產並與之互動。 不過，您不需要建立檢視器預設集。 您也可以選擇使用AEM Assets隨附的預設現成檢視器預設集。

如果您選擇建立檢視器預設集，在儲存後，檢視器的狀態會自動啟動(設為 **[!UICONTROL 開啟]**)。 此狀態表示只要您預覽影像或視訊，就能在Dynamic Media元件和互動式媒體元件中看到它。

有些檢視器預設集具有獨佔設定，可能會影響檢視器的使用方式和整體行為。 根據您建立的檢視器預設集，您可能會想要瞭解這些特殊考量。

另請參閱 [建立互動式檢視器預設集的特殊考量事項](#special-considerations-for-creating-an-interactive-viewer-preset).

另請參閱 [建立轉盤橫幅檢視器預設集的特殊考量事項](#special-considerations-for-creating-a-carousel-banner-viewer-preset).

**若要建立檢視器預設集：**

1. 在Experience Manager的左上角，選取Experience Manager標誌，然後在左側邊欄中選取 **[!UICONTROL 工具]** （槌子圖示） > **[!UICONTROL 資產] > [!UICONTROL 檢視器預設集]**.

   ![6_5_viewerpresets](assets/6_5_viewerpresets.png)

1. 在「檢視器預設集」頁面的工具列上，選取 **[!UICONTROL 建立]**.
1. 在 **[!UICONTROL 新增檢視器預設集]** 對話方塊，在 **[!UICONTROL 預設集名稱]** 欄位中，輸入新預設集的名稱。 請謹慎選擇名稱 — 在您選取後，這些名稱將不可編輯 **[!UICONTROL 建立]**.

   當您稍後在這些步驟中儲存預設集時，該名稱會出現在「檢視器預設集」頁面的「預設集標題」欄標題下。

1. 在「多媒體型別」下拉式功能表中，選取您要建立的檢視器預設集型別，然後在頁面的右上角選取 **[!UICONTROL 建立]**.

   另請參閱 [檢視器預設集的多媒體型別](#rich-media-types-for-viewer-presets).

1. 在「檢視器預設集編輯器」頁面上，選取 **[!UICONTROL 外觀]** 標籤。
1. 执行下列操作之一：

   * 在 **[!UICONTROL 選取的型別]** 下拉式選單，選取您要自訂其視覺設計的元件。 或者，您可以在檢視器中選取任何視覺元素，以選取它進行設定。

      視覺化編輯器可讓您檢視特定屬性對樣式有何影響。 使用編輯器左側的範例來設定或調整任何屬性，以立即檢視其對檢視器有何影響。

      如需每種檢視器預設集型別的CSS樣式屬性，請參閱自訂 *`<viewer name>`* 檢視器」中的說明主題 [檢視器參考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html). 例如，如果您要建立的檢視器預設集型別為 `Mixed_Media`，請參閱 [自訂混合媒體檢視器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/mixed-media/customing-mixed-media/c-html5-mixedmedia-viewer-customizingviewer.html) 以取得每個屬性的清單和說明。

   * 如果您已在個別的CSS檔案中定義樣式設定，則可將CSS檔案上傳至AEM Assets。 選取 **[!UICONTROL 匯入CSS]** 在 **[!UICONTROL 選取的型別]** 下拉式選單（如有必要，請向上捲動視覺編輯器以檢視它），以便您可以找到上傳的CSS檔案並將其與檢視器預設集相關聯。

      匯入CSS檔案時，視覺化編輯器會檢查CSS是否使用正確的檢視器標籤。 例如，如果您要建立縮放檢視器，則必須使用檢視器類別名稱來定義所有匯入的CSS規則 `.s7mixedmediaviewer` 定義於父檢視器元素上。

      您可以匯入任意的手工製作CSS，只要它為特定檢視器正確定義CSS標籤即可。 (CSS標籤在任何「自訂」一節中有說明。 *&lt;viewer name=&quot;&quot;>* 檢視器」中的說明主題 [檢視器參考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html). 例如，如果您想閱讀縮放檢視器的CSS標籤，請參閱 [自訂縮放檢視器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/zoom/customizing-zoom/c-html5-20-zoom-viewer-customizingviewer.html).) 不過，視覺化編輯器可能並不瞭解某些CSS值。 在這種情況下，視覺化編輯器會嘗試覆寫錯誤，讓CSS仍可運作。
   >[!NOTE]
   >
   >如果您偏好直接以原始格式編輯CSS，請選取「 」 **[!UICONTROL 顯示/隱藏CSS]** 在「選取型別」(Selected Type)下拉式選單下方（如有必要，請向上捲動視覺編輯器以檢視它）。
   >如同視覺化編輯器，直接在CSS中變更屬性時，您會立即看到屬性對檢視器範例有何影響。 而且，在視覺化編輯器中，相同的屬性會同時自動更新。 因此，您可以使用原始CSS編輯器或視覺化編輯器，也可以交替使用兩者。

   >[!NOTE]
   >
   >對於按鈕圖稿，請選擇2x影像並上傳高解析度圖稿。 使用互動式影像和可購物橫幅時，您也可以選取各種現成的熱點按鈕。

1. （可選）在「編輯檢視器預設集」頁面頂端附近，選取「 」 **[!UICONTROL 案頭]**， **[!UICONTROL 平板電腦]**，或 **[!UICONTROL 電話]** 為不同的裝置和熒幕型別唯一定義視覺樣式。
1. 在「檢視器預設集編輯器」頁面上，選取 **[!UICONTROL 行為]** 標籤。 或者，您可以在檢視器中選取任何視覺元素，以選取它進行設定。
例如，對於 *videoplayer* 型別，在下 **[!UICONTROL 修飾元]** > **[!UICONTROL 播放]**，您可以從三個最適化位元速率串流選項中選取：

   * **[!UICONTROL 虛線]**  — 視訊資料流僅以短劃線顯示。 不過，在Safari/iOS裝置上，您必須選取 **[!UICONTROL hls]** 做為型別。
   * **[!UICONTROL hls]**  — 視訊資料流僅以HLS形式。
   * **[!UICONTROL 自動]**  — 最佳做法。 建立DASH和HLS資料流時，會最佳化儲存空間。 因此，Adobe建議您一律選取 **[!UICONTROL 自動]** 做為播放型別。 視訊串流為虛線、hls或漸進式，如下列播放順序所示：
      * 如果瀏覽器支援DASH，則會先使用DASH串流。
      * 如果瀏覽器不支援DASH，則會使用HLS資料流，第二個。
      * 如果瀏覽器不支援DASH或HLS，則最後會使用漸進式播放。

   >[!NOTE]
   >
   >若要檢視並使用 **[!UICONTROL 虛線]** 選項，必須先由您帳戶上的Adobe技術支援啟用。 另請參閱 [在您的帳戶上啟用DASH](/help/assets/video.md#enable-dash).

1. 从&#x200B;**[!UICONTROL 选定类型]**&#x200B;下拉菜单中，选择要更改其行为的组件。

   視覺化編輯器中的許多元件都有與其相關的詳細說明。 展開元件以顯示其相關引數時，這些說明會顯示在藍色方塊中。

   有些“查看器类型”具有的组件允许您在 **[!UICONTROL IS 命令]**&#x200B;文本字段中指定“图像提供”命令。有关可使用的命令列表，请参阅[图像提供 API 参考](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-is-home.html)。

   >[!NOTE]
   >
   >**如果您使用觸控裝置，例如手機或平板電腦……**
   >
   >
   >在文字欄位中輸入值後，選取使用者介面中的其他位置以提交變更並關閉虛擬鍵盤。 如果您選取Enter，則不會發生任何動作。

1. 在頁面的右上角附近，選取 **[!UICONTROL 儲存]**.
1. 發佈您的新檢視器預設集，以便用於您的網站。

   另請參閱 [發佈檢視器預設集](#publishing-viewer-presets).

   >[!IMPORTANT]
   >
   >對於使用最適化位元速率串流設定檔的舊影片，URL會持續如常播放（透過HLS串流），直到您離開 [重新處理視訊資產](/help/assets/processing-profiles.md#reprocessing-assets). 重新處理之後，相同的URL仍會繼續運作，但現在透過 *兩者* DASH和HLS串流已啟用。

### 建立互動式檢視器預設集的特殊考量事項 {#special-considerations-for-creating-an-interactive-viewer-preset}

**關於面板中影像縮圖的顯示模式**

當您建立或編輯互動式視訊檢視器預設集時，可以選擇在選取時使用的「顯示模式」設定 `InteractiveSwatches` 從 **[!UICONTROL 選取的元件]** 功能表下的 **[!UICONTROL 行為]** 標籤。 您選擇的顯示模式會影響縮圖在視訊播放時的顯示方式和時間。 您可以選擇 `segment`顯示模式（預設）或 `continuous` 顯示模式。

<table>
 <tbody>
  <tr>
   <td><strong>显示模式</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>市场细分</td>
   <td><p><code>Segment </code>是現成互動式視訊檢視器預設集的預設顯示模式 <code>Shoppable_Video_light</code> 和 <code>Shoppable_Video_dark</code> 以及您自行建立的任何互動式視訊檢視器預設集。</p> <p>在此模式中，當指派給視訊區段的縮圖數量少於顯示面板中的可見點數時。 此外，下一個或上一個子區段的縮圖也有 <i>not </i>拉入以填滿面板中的任何空白點。 也就是說，它可以保留指定給特定視訊區段的色票顯示。</p> </td>
  </tr>
  <tr>
   <td>連續</td>
   <td><p>在 <code>continuous </code>顯示模式：如果區段中的縮圖數目少於面板中顯示的數目，則檢視器會自動包含顯示下一個區段的縮圖。 或者，檢視器會自動包含先前區段的縮圖顯示（若顯示的是最後一個縮圖）。</p> <p>此 <a href="/help/assets/interactive-videos.md">此主題中的影片</a> 是 <code>continuous </code>顯示模式。</p> </td>
  </tr>
 </tbody>
</table>

**關於互動式視訊檢視器中的自動捲動行為**

互動式視訊檢視器中縮圖的自動捲動行為獨立於您選擇的顯示模式。

创建或编辑交互式视频查看器预设时，您可以从“行为”选项卡访问“自动滚动”。在行為標籤中，從 **[!UICONTROL 選取的元件]** 下拉式功能表，選取 **[!UICONTROL 互動色票]**. “自动滚动”复选框列在“IS 命令”文本字段的下方。

如果在查看器预设中禁用&#x200B;**[!UICONTROL 自动滚动]**（清除复选框），则在用户播放视频时，该面板仅显示整个视频长度的第一个缩略图。但是，如果需要，用户可以使用向上和向下箭头图标手动滚动缩略图。

在查看器预设中启用（选择）**[!UICONTROL 自动滚动]**&#x200B;后，在视频播放过程中，分配给视频区段的缩略图图像会在区段开始时滚动到视图中。但是，在某些情况下，区段内某些缩略图的显示时间是其之前或之后缩略图显示时间的两倍。发生此行为的原因是区段中缩略图的数量大于面板中可见缩略图的数量，且不可平均分割。

舉例說明，假設您有一個30秒的視訊區段。 此外，在30秒內總共會顯示九個縮圖。 您瀏覽器的大小調整方式決定了顯示面板中有四個可見的縮圖位置。 30秒的視訊時間區段分為三個子區段。 下表顯示指定時間子區段所顯示縮圖的劃分：

| **視訊子區段** | **子區段時間（以秒為單位）** | **面板中可見的縮圖** |
|---|---|---|
| 1 | 0-10 | 1, 2, 3, 4 |
| 2 | 10-20 | 4, 5, 6, 7 |
| 3 | 20-30 | 6, 7, 8, 9 |

視訊子區段3的延伸範圍不會超過指派給它的縮圖。 另外也請注意，在面板中顯示的縮圖4、6和7比其他縮圖長兩倍。

根據可用位置數量，檢視器用於面板中顯示縮圖數目的邏輯如下：

* 子區段數=向上舍入至下一個子區段（縮圖數/縮圖面板中的可見位置數，根據瀏覽器視窗大小而定）。
以上表為例，9個縮圖/ 4個槽= 2.25；檢視器邏輯將其四捨五入為三個子區段。

* 縮圖數目=四捨五入至下一個縮圖（縮圖數目/視訊子區段數目）。
以上表為例，9個縮圖/ 3個視訊子區段= 3個縮圖。

* 子區段的持續時間=影片總持續時間/影片子區段數量。
以上表範例為例，30秒/ 3視訊子區段=每個視訊子區段顯示10秒。

#### 建立轉盤橫幅檢視器預設集的特殊考量事項 {#special-considerations-for-creating-a-carousel-banner-viewer-preset}

建立「轉盤橫幅」檢視器預設集時，可以依照以下步驟存取變更連結區樣式：

|  | **描述** | **操作** |
|---|---|---|
| **[!UICONTROL 熱點圖示]** | 變更用於連結區的圖示 | 若要變更熱點圖示影像，請在以下位置輸入： **[!UICONTROL 外觀]** 標籤，在 **[!UICONTROL 選取的元件]**，選取 **[!UICONTROL ImageMapEffect]**. 下 **[!UICONTROL 圖示]**，選取 **[!UICONTROL 背景]** 和 **[!UICONTROL 影像]** 欄位導覽至您想要的背景影像。 |

## 啟用或停用檢視器預設集 {#activating-or-deactivating-viewer-presets}

使用者介面中可用的檢視器預設集取決於在作者模式下活動的檢視器預設集。 依預設，建立檢視器預設集後會變成「開啟」。 如果您關閉預設集，在「作者」模式中看不到。 如果預設集已發佈，則無論預設集是否已切換，都會發佈預設集。 如果清單變得太笨重，或者您不希望檢視器預設集可供使用，您可能會想要停用檢視器預設集。

**若要啟用或停用檢視器預設集：**

1. 在Experience Manager的左上角，選取Experience Manager標誌，然後在左側邊欄中選取 **[!UICONTROL 工具]** （槌子圖示） > **[!UICONTROL 資產]** > **[!UICONTROL 檢視器預設集]**.
1. 在「檢視器預設集」頁面的 **[!UICONTROL 州]** 欄標題，選取切換即可啟用或停用檢視器預設集。

   已啟用的檢視器預設集會在右側內藍色方塊中顯示切換按鈕；已停用的檢視器預設集會在左側淺灰色方塊內顯示切換按鈕。

## 發佈檢視器預設集 {#publishing-viewer-presets}

啟用（或開啟「檢視器預設集」）狀態表示檢視器預設集會顯示在Dynamic Media元件、互動媒體元件中，以及您檢視資產時的狀態。

但是，到 *deliver* 若資產具有檢視器預設集，則檢視器預設集也必須發佈。 必須啟用所有檢視器預設集 *和* 發佈以取得資產的URL或內嵌程式碼。 請務必啟動並發佈Dynamic Media隨附的所有現成可用的檢視器預設集。 您创建和添加的自定义查看器预设将自动激活，但也必须发布。

另請參閱 [啟用或停用檢視器預設集](#activating-or-deactivating-viewer-presets).

另請參閱 [預覽資產](/help/assets/previewing-assets.md).

**若要發佈檢視器預設集：**

1. 在Experience Manager的左上角，選取Experience Manager標誌，然後在左側邊欄中選取 **[!UICONTROL 工具]** （槌子圖示） > **[!UICONTROL 資產]** > **[!UICONTROL 檢視器預設集]**.
1. 選取一或多個您要發佈的檢視器預設集。
1. 在工具列上，選取 **[!UICONTROL 發佈]** 圖示。

## 排序檢視器預設集 {#sorting-viewer-presets}

1. 在Experience Manager的左上角，選取Experience Manager標誌，然後在左側邊欄中選取 **[!UICONTROL 工具]** （槌子圖示） > **[!UICONTROL 資產]** > **[!UICONTROL 檢視器預設集]**.
1. 選取 **[!UICONTROL 預設集標題]**， **[!UICONTROL 型別]**， **[!UICONTROL 已發佈]**，或 **[!UICONTROL 州]** 以依該欄標題排序。 例如，選取 **[!UICONTROL 型別]**  以字母或反向字母順序排序檢視器預設集型別。

## 編輯檢視器預設集 {#editing-viewer-presets}

編輯任何 *預先定義的現成檢視器預設集* 不是支援的情況。 如果您編輯現成的檢視器預設集，系統會提示您以新名稱儲存它。

**若要編輯檢視器預設集：**

1. 在Experience Manager的左上角，選取Experience Manager標誌，然後在左側邊欄中選取 **[!UICONTROL 工具]** （槌子圖示） > **[!UICONTROL 資產]** > **[!UICONTROL 檢視器預設集]**.
1. 勾選檢視器預設集標題左側的方塊，選取預設集。
1. 在工具列上，選取 **[!UICONTROL 編輯]**.
1. 於 **[!UICONTROL 檢視器預設集編輯器]** 頁面上，使用「 」選單中的選項，對檢視器預設集進行您想要的變更 **[!UICONTROL 外觀]** 和 **[!UICONTROL 行為]** 索引標籤。

   從 **[!UICONTROL 外觀]** 索引標籤中，在「檢視器預設集編輯器」頁面的左上角附近，選取 **[!UICONTROL 案頭]**， **[!UICONTROL 平板電腦]**，或 **[!UICONTROL 電話]** 以變更資產的簡報模式。

1. 在頁面的右上角附近，執行下列任一項作業：

   * 選取 **[!UICONTROL 儲存]** 以儲存您的變更並返回「檢視器預設集」頁面。
   * 選取 **[!UICONTROL 取消]** 使所做的任何變更無效，並返回「檢視器預設集」頁面。

## 刪除自訂檢視器預設集 {#deleting-custom-viewer-presets}

您可以刪除已建立並新增至Dynamic Media的檢視器預設集。

**若要刪除自訂檢視器預設集：**

1. 在Experience Manager的左上角，選取Experience Manager標誌，然後在左側邊欄中選取 **[!UICONTROL 工具]** （槌子圖示） **[!UICONTROL 資產]** > **[!UICONTROL 檢視器預設集]**.
1. 在「檢視器預設集」頁面上，核取「預設集標題」，然後選取 **[!UICONTROL 垃圾桶]** 圖示。
1. 选择&#x200B;**[!UICONTROL 删除]**。

## 將檢視器預設集套用至資產 {#applying-a-viewer-preset-to-an-asset}

如果已发布资产和选定的查看器，则在选择查看器预设后 **[!UICONTROL 将显示]** “ **[!UICONTROL URL]** ”和“嵌入”按钮。

**若要將檢視器預設集套用至資產：**

1. 開啟資產，並在頁面的左上角附近，選取下拉式功能表，然後選取 **[!UICONTROL 檢視者]**.

   >[!NOTE]
   >
   >如果已发布资产和选定的查看器，则在选择查看器预设后 **[!UICONTROL 将显示]** “ **[!UICONTROL URL]** ”和“嵌入”按钮。

1. 從左窗格選取檢視器預設集，以便將其套用至資產。

   您可以 [複製要共用的URL](/help/assets/linking-urls-to-yourwebapplication.md) 與其他使用者整合。

## 使用檢視器預設集傳遞資產 {#delivering-assets-with-viewer-presets}

若要取得檢視器預設集的URL，請參閱 [將URL連結至您的Web應用程式](/help/assets/linking-urls-to-yourwebapplication.md). 另請參閱 [將Video Viewer內嵌在網頁上](/help/assets/embed-code.md).

如果您使用Experience Manager作為WCM，您可以直接在頁面上使用檢視器預設集新增資產。 另請參閱 [將Dynamic Media資產新增至頁面](/help/assets/adding-dynamic-media-assets-to-pages.md).
