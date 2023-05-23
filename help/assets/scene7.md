---
title: 將Dynamic Media Classic功能新增至頁面
description: 如何將Dynamic Media Classic功能和元件新增至Adobe Experience Manager中的頁面。
uuid: aa5a4735-bfec-43b8-aec0-a0c32bff134f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
topic-tags: managing-assets
discoiquuid: e7b95732-a571-48e8-afad-612059cdbde7
feature: Dynamic Media Classic
role: User, Admin
mini-toc-levels: 3
exl-id: 815f577d-4774-4830-8baf-0294bd085b83
source-git-commit: d947bd98b3a0f6fd79cde5b5b2fca23487077da3
workflow-type: tm+mt
source-wordcount: '2845'
ht-degree: 0%

---

# 將Dynamic Media Classic功能新增至頁面 {#adding-scene-features-to-your-page}

[Adobe Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/home.html) 是託管解決方案，用於管理、增強和發佈多媒體資產，並將其交付至網路、行動裝置、電子郵件和網際網路連線的顯示和列印。

您可以在多種檢視器中檢視Dynamic Media Classic中發佈的Experience Manager資產：

* 缩放
* 彈出
* 视频
* 图像模板
* 图像

您可以直接從Experience Manager將數位資產發佈到Dynamic Media Classic，也可以從Dynamic Media Classic將數位資產發佈到Experience Manager。

本檔案說明如何將數位資產從Experience Manager發佈至Dynamic Media Classic，反之亦然。 也詳細說明檢視器。 如需為Dynamic Media Classic設定Experience Manager的詳細資訊，請參閱 [將Dynamic Media Classic與Experience Manager整合](/help/sites-administering/scene7.md).

另請參閱 [新增影像地圖](image-maps.md).

如需搭配Experience Manager使用視訊元件的詳細資訊，請參閱 [視訊](video.md).

>[!NOTE]
>
>如果Dynamic Media Classic資產無法正確顯示，請確定Dynamic Media已 [已停用](config-dynamic.md#disabling-dynamic-media) 然後重新整理頁面。

## 從資產手動發佈至Dynamic Media Classic {#manually-publishing-to-scene-from-assets}

您可以將數位資產發佈至Dynamic Media Classic，如下所示：

* [在Assets控制檯的傳統使用者介面中](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-the-assets-console)
* [在資產的傳統使用者介面中](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-an-asset)
* [在CQ Target資料夾外部的傳統使用者介面中](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-assets-from-outside-the-cq-target-folder)

>[!NOTE]
>
>Experience Manager以非同步方式發佈至Dynamic Media Classic。 在您選取之後 **[!UICONTROL 發佈]**，您的資產發佈至Dynamic Media Classic需要幾秒鐘的時間。

## Dynamic Media Classic元件 {#scene-components}

下列Dynamic Media Classic元件為Experience Manager所提供：

* 缩放
* 彈出（縮放）
* 图像模板
* 图像
* 视频

>[!NOTE]
>
>預設不會提供這些元件，必須選取於 **[!UICONTROL 設計]** 模式。

在中提供這些變數後 **[!UICONTROL 設計]** 模式，您可以像任何其他Experience Manager元件一樣，將元件新增至頁面。 如果在同步資料夾或頁面上，或使用Dynamic Media Classic雲端設定，會將尚未發佈至Dynamic Media Classic的資產發佈至Dynamic Media Classic。

>[!NOTE]
>
>如果您要建立及開發自訂檢視器並使用「內容尋找器」，則必須明確新增 `allowfullscreen` 引數。

### Flash 查看器生命周期终止通知 {#flash-viewers-end-of-life-notice}

自2017年1月31日起，Adobe Dynamic Media Classic不再支援Flash檢視器平台。

### 將Dynamic Media Classic (Scene7)元件新增至頁面 {#adding-a-scene-component-to-a-page}

將Dynamic Media Classic (Scene7)元件新增至頁面，與將元件新增至任何頁面相同。 以下各節將詳細說明Dynamic Media Classic元件。

**若要將Dynamic Media Classic (Scene7)元件新增至頁面：**

1. 在Experience Manager中，開啟您要新增的頁面 **[!UICONTROL Dynamic Media Classic (Scene7)]** 元件。

1. 如果沒有可用的Dynamic Media Classic元件，請選取「 」 **[!UICONTROL 設計]** 模式，選取任何具有藍色邊框的元件，然後選取 **[!UICONTROL 父級]** 圖示，然後按一下 **[!UICONTROL 設定]** 圖示。 在 **[!UICONTROL Parsys （設計）]**，選取所有Dynamic Media Classic元件以開放使用，然後選取 **[!UICONTROL 確定]**.

   ![chlimage_1-224](assets/chlimage_1-224.png)

1. 選取 **[!UICONTROL 編輯]** 以便返回 **[!UICONTROL 編輯]** 模式。

1. 將元件從Sidekick中的Dynamic Media Classic群組拖曳到頁面上的所需位置。

1. 選取 **[!UICONTROL 設定]** 圖示以開啟元件。

1. 視需要編輯元件並選取 **[!UICONTROL 確定]** 以儲存變更。
1. 將影像或視訊從內容瀏覽器拖曳至您新增至頁面的Dynamic Media Classic元件。

   >[!NOTE]
   >
   >僅限觸控式UI中，您必須將影像或視訊拖放至您放在頁面上的Dynamic Media Classic元件上。 不支援選取和編輯Dynamic Media Classic元件，然後選取資產。

### 新增互動式檢視體驗至回應式網站 {#adding-interactive-viewing-experiences-to-a-responsive-website}

資產的回應式設計表示您的資產會根據顯示位置進行調整。 透過回應式設計，相同的資產能夠有效地顯示在多個裝置上。

另請參閱 [網頁的回應式設計](/help/sites-developing/responsive.md).

**若要在回應式網站中新增互動式檢視體驗：**

1. 登入Experience Manager，並確認您擁有 [已設定的Adobe Dynamic Media ClassicCloud Services](/help/sites-administering/scene7.md#configuring-scene-integration) 以及Dynamic Media Classic元件是否可供使用。

   >[!NOTE]
   >
   >如果Dynamic Media Classic元件無法使用，請確定 [以設計模式啟用它們](/help/sites-authoring/default-components-designmode.md).

1. 在具有 **[!UICONTROL Dynamic Media Classic]** 啟用元件，拖曳 **[!UICONTROL 影像]** 元件至頁面。
1. 選取元件並選取設定圖示。
1. 在 **[!UICONTROL Dynamic Media Classic設定]** 標籤，調整中斷點。

   ![chlimage_1-225](assets/chlimage_1-225.png)

1. 確認檢視器是否以回應式方式調整大小，以及所有互動是否針對桌上型電腦、平板電腦和行動裝置進行最佳化。

### 所有Dynamic Media Classic元件的通用設定 {#settings-common-to-all-scene-components}

雖然組態選項不盡相同，但下列專案是所有使用者共有的 [!UICONTROL Dynamic Media Classic] 元件：

* **[!UICONTROL 檔案參考]**  — 瀏覽至您要參照的檔案。 檔案參考會顯示資產URL，不一定是完整的Dynamic Media Classic URL，包括URL命令和引數。 您無法在此欄位中新增Dynamic Media Classic URL命令和引數。 而是透過元件中對應的功能來新增它們。
* **[!UICONTROL 寬度]**  — 可讓您設定寬度。
* **[!UICONTROL 高度]**  — 可讓您設定高度。

您可以開啟（按兩下）Dynamic Media Classic元件來設定這些設定選項，例如，當您開啟 **[!UICONTROL 縮放]** 元件：

![chlimage_1-226](assets/chlimage_1-226.png)

### 缩放 {#zoom}

按下HTML5縮放元件時，會顯示較大的影像。 **[!UICONTROL +]** 按鈕。

資產底部有縮放工具。 選取 **[!UICONTROL +]** 如果要放大，請選取 **[!UICONTROL -]** 如果您想要減少。 點選 **[!UICONTROL x]** 或重設縮放箭頭會將影像帶回匯入的原始大小。 選取對角線箭頭，使其變成全熒幕。 選取 **[!UICONTROL 編輯]** 以便設定元件。 使用此元件，您可以設定 [所有使用者通用的設定 [!UICONTROL Dynamic Media Classic] 元件](#settings-common-to-all-scene-components).

![chlimage_1-227](/help/assets/assets/do-not-localize/chlimage_1-227.png)

### 彈出 {#flyout}

在HTML中5 **[!UICONTROL 彈出]** 元件時，資產會以拆分畫面顯示；將資產左移為指定大小；右側會顯示縮放部分。 選取 **[!UICONTROL 編輯]** 以便設定元件。 使用此元件，您可以設定 [所有Dynamic Media Classic元件的通用設定](#settings-common-to-all-scene-components).

>[!NOTE]
>
>若您的 **[!UICONTROL 彈出]** 元件使用自訂大小，然後會使用該自訂大小，並停用元件的回應式設定。
>
>若您的 **[!UICONTROL 彈出]** 元件使用預設大小，如中所設定 **[!UICONTROL 設計檢視]**，則會使用預設大小，元件會延伸以配合啟用元件的回應式設定的頁面版面大小。 元件的回應式設定存在限制。 當您使用 **[!UICONTROL 彈出]** 元件若有回應式設定，請勿將其用於完整頁面延伸。 否則， **[!UICONTROL 彈出]** 超出頁面的右邊框。

![chlimage_1-228](assets/chlimage_1-228.png)

### 图像 {#image}

Dynamic Media Classic **[!UICONTROL 影像]** 元件可讓您將Dynamic Media Classic功能新增至影像，例如Dynamic Media Classic修飾元、影像或檢視器預設集，以及銳利化。 Dynamic Media Classic **[!UICONTROL 影像]** 元件類似於Experience Manager中的其他影像元件，具有特殊的Dynamic Media Classic功能。 在此範例中，影像有Dynamic Media Classic URL修飾元， `&op_invert=1` 已套用。

![chlimage_1-229](assets/chlimage_1-229.png)

**[!UICONTROL 標題，替代文字]**  — 在 **[!UICONTROL 進階]** 標籤，為已關閉圖形的使用者新增標題和替代文字。

**[!UICONTROL URL，開啟位置]**  — 您可以從設定資產以開啟連結。 設定 **[!UICONTROL URL]** 和 **[!UICONTROL 開啟方式]** 指出您想要在同一個視窗或新視窗中開啟它。

![chlimage_1-230](assets/chlimage_1-230.png)

**[!UICONTROL 檢視器預設集]**  — 從下拉式選單中選取現有的檢視器預設集。 如果您要尋找的檢視器預設集不可見，您必須使其可見。 另請參閱 [管理檢視器預設集](/help/assets/managing-viewer-presets.md). 如果您使用影像預設集，則無法選取檢視器預設集，反之亦然。

**[!UICONTROL Dynamic Media Classic設定]**  — 選取您要用來從SPS擷取作用中影像預設集的Dynamic Media Classic設定。

**[!UICONTROL 影像預設集]**  — 從下拉式選單中選取現有的影像預設集。 如果您要尋找的影像預設集不可見，您必須使其可見。 另請參閱 [管理影像預設集](/help/assets/managing-image-presets.md). 如果您使用影像預設集，則無法選取檢視器預設集，反之亦然。

**[!UICONTROL 輸出格式]**  — 選取影像的輸出格式，例如jpeg。 視您選取的輸出格式而定，會有其他設定選項。 另請參閱 [影像預設集最佳作法](/help/assets/managing-image-presets.md#image-preset-options).

**[!UICONTROL 銳利化]**  — 選取您要如何銳利化影像。 詳細說明銳利化，請參閱 [影像預設集最佳作法](/help/assets/managing-image-presets.md#image-preset-options) 和 [強化最佳實務](/help/assets/assets/sharpening_images.pdf).

**[!UICONTROL URL修飾元]**  — 您可以透過提供其他Dynamic Media Classic影像指令來變更影像效果。 這些指令的說明請參閱 [影像預設集](/help/assets/managing-image-presets.md) 和 [命令參考](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html).

**[!UICONTROL 中斷點]**  — 如果您的網站有回應，您想要調整中斷點。 中斷點必須以逗號( 、 )分隔。

### 图像模板 {#image-template}

[Dynamic Media Classic影像範本](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/template-basics/quick-start-template-basics.html) 是匯入至Dynamic Media Classic的分層Photoshop內容，其中內容和屬性已引數化為可變性。 此 **[!UICONTROL 影像範本]** 元件可讓您匯入影像並動態變更Experience Manager文字。 此外，您可以設定 **[!UICONTROL 影像範本]** 元件來使用來自使用者端內容的值，讓每個使用者都能透過個人化的方式體驗影像。

選取 **[!UICONTROL 編輯]** 如果您想要設定元件。 您可以設定 [所有Dynamic Media Classic元件的通用設定](#settings-common-to-all-scene-components) 以及本節中說明的其他設定。

![chlimage_1-231](assets/chlimage_1-231.png)

**[!UICONTROL 檔案參照、寬度、高度]**  — 檢視所有ScDynamic Media Classicene7元件的通用設定。

>[!NOTE]
>
>Dynamic Media Classic URL命令和引數無法直接新增至檔案參考URL。 它們只能在的元件UI中定義 **[!UICONTROL 引數]** 面板。

**[!UICONTROL 標題，替代文字]**  — 在「Dynamic Media Classic影像範本」索引標籤中，為已關閉圖形的使用者新增影像標題和替代文字。

**[!UICONTROL URL，開啟位置]**  — 您可以從設定資產以開啟連結。 設定URL，並在「開啟」中指定您要在同一個視窗或新視窗中開啟。

![chlimage_1-232](assets/chlimage_1-232.png)

**[!UICONTROL 引數面板]**  — 匯入影像時，引數會預先填入影像中的資訊。 如果沒有可動態變更的內容，則此視窗為空白。

![chlimage_1-233](assets/chlimage_1-233.png)

#### 動態變更文字 {#changing-text-dynamically}

若要動態變更文字，請在欄位中輸入新文字，然後選取 **[!UICONTROL 確定]**. 在此範例中， **[!UICONTROL 價格]** 現在為$50，運費為99美分。

![chlimage_1-234](assets/chlimage_1-234.png)

影像中的文字會變更。 您可以點選文字，將文字重設為原始值 **[!UICONTROL 重設]** 欄位旁邊。

![chlimage_1-235](assets/chlimage_1-235.png)

#### 變更文字以反映使用者端內容值的值 {#changing-text-to-reflect-the-value-of-a-client-context-value}

若要將欄位連結至使用者端內容值，請選取 **[!UICONTROL 選取]** 若要開啟使用者端內容功能表，請選取使用者端內容，然後選取 **[!UICONTROL 確定]**. 在此範例中，名稱會隨著在設定檔中將「名稱」與格式化名稱連結而變更。

![chlimage_1-236](assets/chlimage_1-236.png)

此文字會反映目前登入使用者的名稱。 您可以按一下「 」，將文字重設為原始值 **[!UICONTROL 重設]** 欄位旁邊。

![chlimage_1-237](assets/chlimage_1-237.png)

#### 將Dynamic Media Classic影像範本設為連結 {#making-the-scene-image-template-a-link}

1. 在具有Dynamic Media Classic的頁面上 **[!UICONTROL 影像範本]** 元件，選取 **[!UICONTROL 編輯]**.
1. 在 **[!UICONTROL URL]** 欄位中，輸入使用者點選影像時前往的URL。 在 **[!UICONTROL 開啟方式]** 欄位中，選取是否要開啟目標（新視窗或相同視窗）。

   ![chlimage_1-238](assets/chlimage_1-238.png)

1. 選取 **[!UICONTROL 確定]**.

### 視訊元件 {#video-component}

Dynamic Media Classic **[!UICONTROL 視訊]** 元件(可在sidekick的Dynamic Media Classic區段取得)使用裝置和頻寬偵測將正確的視訊提供給每個畫面。 此元件是HTML5視訊播放程式；它是可跨頻道使用的單一檢視器。

它可用於自我調整視訊集、單一MP4視訊或單一F4V視訊。

另請參閱 [視訊](s7-video.md) 如需影片如何與Dynamic Media Classic整合搭配使用的詳細資訊。 此外，請參閱 [Dynamic Media Classic視訊元件與Foundation視訊元件](s7-video.md).

![chlimage_1-239](assets/chlimage_1-239.png)

### 視訊元件的已知限制 {#known-limitations-for-the-video-component}

AdobeDAM和WCM會顯示是否上傳了主要來源影片。 它們不會顯示這些Proxy資產：

* Dynamic Media Classic編碼的轉譯
* Dynamic Media Classic最適化視訊集

搭配Dynamic Media Classic視訊元件使用自我調整視訊集時，您必須調整元件大小以符合視訊的尺寸。

## Dynamic Media Classic內容瀏覽器 {#scene-content-browser}

Dynamic Media Classic內容瀏覽器可讓您直接在Experience Manager中檢視Dynamic Media Classic的內容。 若要存取內容瀏覽器，請在 **[!UICONTROL 內容尋找器]**，選取 **[!UICONTROL Dynamic Media Classic]** 在觸控最佳化的使用者介面或 **[!UICONTROL S7]** 圖示加以存取。 兩個使用者介面之間的功能相同。

如果您有多個組態，依預設，「Experience Manager」會顯示 [預設設定](/help/sites-administering/scene7.md#configuring-a-default-configuration). 您可以直接在Dynamic Media Classic內容瀏覽器的下拉式選單中選取不同的設定。

>[!NOTE]
>
>* 隨選資料夾中的資產不會出現在Dynamic Media Classic內容瀏覽器中。
>* 時間 [已啟用安全預覽](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)，Dynamic Media Classic上已發佈和未發佈的資產都會出現在Dynamic Media Classic內容瀏覽器中。
>* 如果您沒有看見 **[!UICONTROL Dynamic Media Classic]** 或 **[!UICONTROL S7]** 圖示作為內容瀏覽器中的選項，您必須 [設定Dynamic Media Classic以搭配Experience Manager使用](/help/sites-administering/scene7.md).
>* 對於視訊，Dynamic Media Classic內容瀏覽器支援：
   >
   >   * 最適化視訊集：包含跨多個熒幕無縫播放所需的所有視訊轉譯的容器
   >   * 單一MP4視訊
   >   * 單一F4V視訊


### 在觸控最佳化的UI中瀏覽內容 {#browsing-content-in-the-touch-optimized-ui}

您可以在觸控最佳化或傳統UI中存取內容瀏覽器。 目前，觸控最佳化有下列限制：

* 不支援來自Dynamic Media Classic的FXG和Flash資產。

瀏覽Dynamic Media Classic資產，方法是選取 **[!UICONTROL Dynamic Media Classic]** 從第三個下拉式功能表。 如果您尚未設定Dynamic Media Classic/Experience Manager整合，Dynamic Media Classic就不會出現在清單中。

>[!NOTE]
>
>* Dynamic Media Classic內容瀏覽器會載入約100個資產，並依名稱排序。
>* 如果您已設定安全預覽伺服器，瀏覽器會使用該預覽伺服器來轉譯縮圖和資產。
>


![chlimage_1-240](assets/chlimage_1-240.png)

此外，您可以將滑鼠游標停留在瀏覽器中的資產上，以瀏覽解析度資訊、大小、修改後的天數以及檔案名稱。

![chlimage_1-241](assets/chlimage_1-241.png)

* 針對最適化視訊集和範本，不會產生縮圖的大小資訊。
* 若為最適化視訊集，縮圖不會產生解析度。

### 使用內容瀏覽器搜尋Dynamic Media Classic資產 {#searching-for-scene-assets-with-the-content-browser}

在Dynamic Media Classic中搜尋資產類似於在Experience Manager Assets中搜尋資產。 不過，當您搜尋時，您實際上會在Dynamic Media Classic系統中看到資產的遠端檢視，而不是直接將資產匯入Experience Manager。

您可以使用傳統UI或觸控最佳化UI來檢視和搜尋資產。 依介面而定，搜尋方式會稍微有些不同。

在任何一個UI中搜尋時，您可以依下列條件進行篩選（如觸控最佳化UI中所示）：

**[!UICONTROL 輸入關鍵字]**  — 您可以依名稱搜尋資產。 搜尋時，您輸入的關鍵字是檔案名稱的開頭。 例如，輸入「swimming」會尋找任何以那個順序開頭字母的資產檔案名稱。 輸入字詞以尋找資產後，請務必按Enter鍵。

![chlimage_1-242](assets/chlimage_1-242.png)

**[!UICONTROL 資料夾/路徑]**  — 看到的資料夾名稱是根據您選取的設定而定。 您可以點選資料夾圖示並選取子資料夾，然後點選核取記號來選取它，以向下鑽研至較低層級。

如果您輸入關鍵字並選取資料夾，Experience Manager會搜尋該資料夾及任何子資料夾。 但是，如果您在搜尋時未輸入任何關鍵字，則選取該資料夾只會顯示該資料夾中的資產，不包含任何子資料夾。

根據預設，Experience Manager會搜尋選取的資料夾和所有子資料夾。

![chlimage_1-243](assets/chlimage_1-243.png)

**[!UICONTROL 資產型別]**  — 選取 **[!UICONTROL Dynamic Media Classic]** 以瀏覽Dynamic Media Classic內容。 此選項僅在Dynamic Media Classic已設定後才可用。

![chlimage_1-244](assets/chlimage_1-244.png)

**[!UICONTROL 設定]**  — 如果您在中定義了多個Dynamic Media Classic設定 [!UICONTROL Cloud Services]，您可以在這裡選取。 因此，資料夾會根據您選擇的設定而變更。

![chlimage_1-245](assets/chlimage_1-245.png)

**[!UICONTROL 資產型別]**  — 在Dynamic Media Classic瀏覽器中，您可以篩選結果以包含下列任一專案：影像、範本、視訊和自我調整視訊集。 如果您未選取任何資產型別，預設情況下，Experience Manager會搜尋所有資產型別。

![chlimage_1-246](assets/chlimage_1-246.png)

>[!NOTE]
>
>* 在傳統UI中，您也可以搜尋 **Flash** 和 **FXG**. 不支援在觸控最佳化UI中篩選這些型別。
>
>* 搜尋視訊時，您會搜尋單一轉譯。 結果會傳回原始轉譯（僅限&amp;ast；.mp4）和編碼的轉譯。
>* 搜尋最適化視訊集時，您會搜尋資料夾和所有子資料夾，但前提是您已新增關鍵字至搜尋。 如果您尚未新增關鍵字，Experience Manager不會搜尋子資料夾。
>


**[!UICONTROL 發佈狀態]**  — 您可以根據發佈狀態來篩選資產： **[!UICONTROL 已取消發佈]** 或 **[!UICONTROL 已發佈]**. 如果您未選取任何 **[!UICONTROL 發佈狀態]**，Experience Manager預設會搜尋所有發佈狀態。

![chlimage_1-247](assets/chlimage_1-247.png)
