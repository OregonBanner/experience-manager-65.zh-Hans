---
title: 將Dynamic Media Classic (Scene7)功能新增至您的頁面
description: Adobe Dynamic Media Classic (Scene7)是託管式解決方案，用於管理、增強和發佈多媒體資產，並將其傳遞至網路、行動裝置、電子郵件和網際網路連線的顯示和列印。
uuid: dc463e2d-a452-490e-88af-f79bdaa3b089
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: dc0191d0-f181-4e1e-b3f4-73427aa22073
docset: aem65
exl-id: bc9c864b-8bc3-42b4-ba25-6c5108be4f65
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '3511'
ht-degree: 0%

---

# 將Dynamic Media Classic (Scene7)功能新增至您的頁面{#adding-scene-features-to-your-page}

[Adobe Dynamic Media Classic (Scene7)](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/home.html) 是託管解決方案，用於管理、增強和發佈多媒體資產，並將其交付至網路、行動裝置、電子郵件和網際網路連線的顯示和列印。

您可以在多種檢視器中檢視Dynamic Media Classic (Scene7)中發佈的Experience Manager資產：

* 缩放
* 彈出
* 视频
* 图像模板
* 图像

您可以直接從Experience Manager將數位資產發佈到Dynamic Media Classic (Scene7)，也可以從Dynamic Media Classic (Scene7)將數位資產發佈到Experience Manager。

本檔案說明如何從Experience Manager將數位資產發佈到Dynamic Media Classic (Scene7)，反之亦然。 也詳細說明檢視器。 如需為Dynamic Media Classic (Scene7)設定Experience Manager的詳細資訊，請參閱 [將Dynamic Media Classic (Scene7)與Experience Manager整合](/help/sites-administering/scene7.md).

另請參閱 [新增影像地圖](/help/assets/image-maps.md).

如需搭配Experience Manager使用視訊元件的詳細資訊，請參閱下列內容：

* [视频](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)

>[!NOTE]
>
>如果Dynamic Media Classic (Scene7)資產未正確顯示，請確定Dynamic Media已 [已停用](/help/assets/config-dynamic.md#disabling-dynamic-media) 然後重新整理頁面。

## 從Assets手動發佈至Dynamic Media Classic (Scene7) {#manually-publishing-to-scene-from-assets}

您可以從傳統UI的Assets控制檯或直接從資產將數位資產發佈到Dynamic Media Classic (Scene7)。

>[!NOTE]
>
>Experience Manager以非同步方式發佈至Dynamic Media Classic (Scene7)。 在您選取之後 **[!UICONTROL 發佈]**，您的資產可能需要幾秒鐘才能發佈至Dynamic Media Classic (Scene7)。

### 從Assets控制檯發佈 {#publishing-from-the-assets-console}

如果資產位於Dynamic Media Classic (Scene7)目標資料夾，您可以從資產控制檯發佈至Dynamic Media Classic (Scene7)。

1. 在Experience Manager Classic UI中，選取 **[!UICONTROL 數位資產]** 以存取digital asset manager。

1. 從您要發佈至Dynamic Media Classic (Scene7)的目標資料夾中選取資產（或資產）或資料夾，然後按一下滑鼠右鍵並選取 **[!UICONTROL 發佈至Dynamic Media Classic (Scene7)]**. 或者，您可以選取 **[!UICONTROL 發佈至Dynamic Media Classic (Scene7)]** 從 **[!UICONTROL 工具]** 功能表。

   ![chlimage_1-48](assets/chlimage_1-48.png)

1. 前往Dynamic Media Classic (Scene7)並確認資產可供使用。

   >[!NOTE]
   >
   >如果資產不在Dynamic Media Classic (Scene7)同步處理資料夾中， **[!UICONTROL 發佈至Dynamic Media Classic (Scene7)]** 兩個功能表中皆可見，但已停用。

### 從資產發佈 {#publishing-from-an-asset}

您可以手動發佈資產，前提是該資產位於同步的Dynamic Media Classic (Scene7)資料夾內。

>[!NOTE]
>
>如果資產不在Dynamic Media Classic (Scene7)已同步資料夾中，請連結至 **[!UICONTROL 發佈至Dynamic Media Classic (Scene7)]** 未出現。

若要直接從數位資產發佈至Dynamic Media Classic (Scene7)：

1. 在Experience Manager中選取 **[!UICONTROL 數位資產]** 以存取digital asset manager。

1. 按兩下以開啟資產。

1. 在資產詳細資料窗格中，選取 **[!UICONTROL 發佈至Dynamic Media Classic (Scene7)]**.

   ![screen_shot_2012-02-22at34828pm](assets/screen_shot_2012-02-22at34828pm.png)

1. 連結變更為 **[!UICONTROL 正在發佈……]** 然後 **[!UICONTROL 已發佈]**. 前往Dynamic Media Classic (Scene7)並確認資產可供使用。

   >[!NOTE]
   >
   >如果資產未正確發佈至Dynamic Media Classic (Scene7)，連結會變更為 **[!UICONTROL 發佈失敗]**. 如果資產已發佈至Dynamic Media Classic (Scene7)，連結會顯示 **[!UICONTROL 重新發佈至Dynamic Media Classic (Scene7)]**. 重新發佈可讓您變更Experience Manager中的資產並重新發佈。

### 從CQ目標資料夾外部發佈資產 {#publishing-assets-from-outside-the-cq-target-folder}

Adobe建議您只從Dynamic Media Classic (Scene7)目標資料夾內的資產發佈資產到Dynamic Media Classic (Scene7)。 不過，如果您必須從目標資料夾以外的資料夾上傳資產，您仍然可以透過將資產上傳到Dynamic Media Classic (Scene7)上的隨選資料夾來執行此操作。 首先，針對您要顯示資產的頁面設定雲端設定。 然後新增Dynamic Media Classic (Scene7)元件至頁面，並將資產拖放至元件上。 為該頁面設定頁面屬性後， **[!UICONTROL 發佈至Dynamic Media Classic (Scene7)]** 連結會在選取觸發器上傳至Dynamic Media Classic (Scene7)時顯示。

>[!NOTE]
>
>隨選資料夾中的資產不會出現在Dynamic Media Classic (Scene7)內容瀏覽器中。

**若要從CQ目標資料夾外部發佈資產：**

1. 在傳統UI的Experience Manager中，選取 **[!UICONTROL 網站]** 並導覽至您要新增數位資產至但尚未發佈至Dynamic Media Classic (Scene7)的網頁。 （適用一般頁面繼承規則。）

1. 在sidekick中，選取 **[!UICONTROL 頁面]** 圖示並選取 **[!UICONTROL 頁面屬性]**.

1. 選取 **[!UICONTROL Cloud Services]**.
1. 選取 **[!UICONTROL 新增服務]**.
1. 選取 **[!UICONTROL Dynamic Media Classic (Scene7)]**.
1. 在 **[!UICONTROL Adobe Dynamic Media Classic (Scene7)]** 下拉式清單，選取所需的組態，然後選取 **[!UICONTROL 確定]**.

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. 在網頁上，將Dynamic Media Classic (Scene7)元件新增至頁面上所需的位置。
1. 從內容尋找器，將數位資產拖曳至元件。 您會看到以下連結至 **[!UICONTROL 檢查Dynamic Media Classic (Scene7)發佈狀態]**.

   >[!NOTE]
   >
   >如果數位資產在CQ目標資料夾中，則沒有連結到 **[!UICONTROL 檢查Dynamic Media Classic (Scene7)發佈狀態]** 出現。 資產會放置在元件中。

   ![chlimage_1-50](assets/chlimage_1-50.png)

1. 選取 **[!UICONTROL 檢查Dynamic Media Classic (Scene7)發佈狀態]**. 如果資產未發佈，Experience Manager會將資產發佈至Dynamic Media Classic (Scene7)。 上傳之後，即可在隨選資料夾中找到資產。 依預設，隨選資料夾位於 **[!UICONTROL name_of_the_company/CQ5_adhoc]**. 您可以 [視需要設定隨選資料夾](#configuringtheadhocfolder).

   >[!NOTE]
   >
   >如果資產不在Dynamic Media Classic (Scene7)同步處理資料夾中，而且沒有Dynamic Media Classic (Scene7)雲端設定與目前頁面相關聯，則上傳會失敗。

## Dynamic Media Classic (Scene7)元件 {#scene-components}

以下Dynamic Media Classic (Scene7)元件為Experience Manager版本：

* 缩放
* 彈出（縮放）
* 图像模板
* 图像
* 视频

>[!NOTE]
>
>預設不會提供這些元件，且必須在使用之前在設計模式中選取這些元件。

在「設計」模式中提供元件後，您就可以像新增任何其他Experience Manager元件一樣，將元件新增至頁面。 如果在同步資料夾或頁面上，或使用Dynamic Media Classic (Scene7)雲端設定，會將尚未發佈至Dynamic Media Classic (Scene7)的資產發佈至Dynamic Media Classic (Scene7)。

>[!NOTE]
>
>如果您要建立及開發自訂S7檢視器並使用「內容尋找器」，則必須明確新增 `allowfullscreen` 引數。

### Flash 查看器生命周期终止通知 {#flash-viewers-end-of-life-notice}

自2017年1月31日起，Adobe Dynamic Media Classic (Scene7)正式停止支援Flash檢視器平台。

### 將Dynamic Media Classic (Scene7)元件新增至頁面 {#adding-a-scene-component-to-a-page}

將Dynamic Media Classic (Scene7)元件新增至頁面，與將元件新增至任何頁面相同。 以下各節將詳細說明Dynamic Media Classic (Scene7)元件。

若要將Dynamic Media Classic (Scene7)元件/檢視器新增至傳統UI中的頁面：

1. 在Experience Manager中，開啟您要新增Dynamic Media Classic (Scene7)元件的頁面。

1. 如果沒有可用的Dynamic Media Classic (Scene7)元件，請選取Sidekick中的尺標以輸入 **設計** 模式，選取 **[!UICONTROL 編輯]** parsys，然後選取所有的 **[!UICONTROL Dynamic Media Classic (Scene7)]** 元件以利使用。

1. 返回至 **編輯** 模式，方法是選取sidekick中的鉛筆。

1. 從拖曳元件 **[!UICONTROL Dynamic Media Classic (Scene7)]** 在sidekick中群組至頁面所需位置。

1. 選取***[!UICONTROL 編輯]** 以開啟元件。

1. 視需要編輯元件並選取 **[!UICONTROL 確定]** 以儲存變更。

### 將互動式檢視體驗新增至回應式網站 {#adding-interactive-viewing-experiences-to-a-responsive-website}

資產的回應式設計意味著您的資產會根據顯示的位置進行調整。 透過回應式設計，相同的資產能夠有效地顯示在多個裝置上。

若要在傳統UI中新增互動式檢視體驗至回應式網站：

1. 登入Experience Manager，並確認您擁有 [已設定的Adobe Dynamic Media Classic (Scene7)Cloud Services](/help/sites-administering/scene7.md#configuring-scene-integration) 以及Dynamic Media Classic (Scene7)元件是否可供使用。

   >[!NOTE]
   >
   >如果Dynamic Media Classic (Scene7) WCM元件無法使用，請務必透過設計模式啟用它們。

1. 在啟用Dynamic Media Classic (Scene7)元件的網站中，拖曳 **[!UICONTROL 影像]** 檢視器移至頁面。
1. 編輯元件並調整中斷點 **[!UICONTROL Dynamic Media Classic (Scene7)設定]** 標籤。

   ![chlimage_1-51](assets/chlimage_1-51.png)

1. 確認檢視器是否以回應式方式調整大小，以及所有互動是否針對桌上型電腦、平板電腦和行動裝置進行最佳化。

### 所有Dynamic Media Classic (Scene7)元件的通用設定 {#settings-common-to-all-scene-components}

雖然設定選項不盡相同，但下列專案是所有Dynamic Media Classic (Scene7)元件的共同專案：

* **檔案參考** — 瀏覽至您要參照的檔案。 檔案參考會顯示資產URL，不一定是完整的Dynamic Media Classic (Scene7) URL，包括URL命令和引數。 您無法在此欄位中新增Dynamic Media Classic (Scene7) URL命令和引數。 相反，必須透過元件中的對應功能新增它們。
* **寬度**  — 可讓您設定寬度。
* **高度**  — 可讓您設定高度。

您可以開啟（按兩下） Dynamic Media Classic (Scene7)元件來設定這些設定選項，例如，當您開啟 **縮放** 元件：

![chlimage_1-52](assets/chlimage_1-52.png)

### 缩放 {#zoom}

按下+按鈕時，HTML5縮放元件會顯示較大的影像。

資產底部有縮放工具。 選取 **[!UICONTROL +]** 放大。 選取 **[!UICONTROL -]** 以減少。 選取 **[!UICONTROL x]** 或重設縮放箭頭會將影像帶回匯入的原始大小。 選取對角線箭頭，使其變成全熒幕。 選取 **[!UICONTROL 編輯]** 以便設定元件。 使用此元件，您可以設定 [所有Dynamic Media Classic (Scene7)元件的通用設定](#settings-common-to-all-scene-components).

![](do-not-localize/chlimage_1-3.png)

### 彈出 {#flyout}

在HTML5彈出式元件中，資產顯示為拆分畫面；將資產保留為指定大小；顯示縮放部分時會顯示為右側。 選取 **[!UICONTROL 編輯]** 以便設定元件。 使用此元件，您可以設定 [所有Dynamic Media Classic (Scene7)元件的通用設定](/help/sites-administering/scene7.md#settingscommontoallscene7components).

>[!NOTE]
>
>如果您的彈出式元件使用自訂大小，則會使用該自訂大小，並停用元件的回應式設定。
>
>如果您的彈出式元件使用預設大小（如「設計」檢視中所設定），則使用預設大小。 元件會延伸以配合啟用元件的回應式設定下的頁面版面大小。 但請注意，元件的回應式設定存在限制。 當您使用具有回應式設定的彈出式元件時，不應將其用於完整頁面延伸。 否則，彈出式視窗可能會超出頁面的右邊框。

![chlimage_1-53](assets/chlimage_1-53.png)

### 图像 {#image}

Dynamic Media Classic (Scene7)影像元件可讓您將Dynamic Media Classic (Scene7)功能新增至影像，例如Dynamic Media Classic (Scene7)修飾元、影像或檢視器預設集，以及銳利化。 Dynamic Media Classic (Scene7)影像元件類似於Experience Manager中的其他影像元件，具有特殊的Dynamic Media Classic (Scene7)功能。 在此範例中，影像有Dynamic Media Classic (Scene7) URL修飾元， `&op_invert=1` 已套用。

![](do-not-localize/chlimage_1-4.png)

**標題，替代文字**  — 在「進階」標籤中，為已關閉圖形的使用者新增標題和替代文字。

**URL，開啟位置**  — 您可以從設定資產以開啟連結。 設定URL，並在「開啟」中指定您要在同一個視窗或新視窗中開啟。

![chlimage_1-54](assets/chlimage_1-54.png)

**檢視器預設集**  — 從下拉式選單中選取現有的檢視器預設集。 如果您要尋找的檢視器預設集不可見，您必須使其可見。 請參閱管理檢視器預設集。 如果您使用影像預設集，則無法選取檢視器預設集，反之亦然。

**Dynamic Media Classic (Scene7)設定**  — 選取您要用來從SPS擷取作用中影像預設集的Dynamic Media Classic (Scene7)設定。

**影像預設集**  — 從下拉式選單中選取現有的影像預設集。 如果您要尋找的影像預設集不可見，您必須使其可見。 請參閱管理影像預設集。 如果您使用影像預設集，則無法選取檢視器預設集，反之亦然。

**輸出格式**  — 選取影像的輸出格式，例如jpeg。 根據您選取的輸出格式，您可能有其他組態選項。 請參閱影像預設集最佳實務。

**銳利化**  — 選取您要如何銳利化影像。 「影像預設集」最佳實務和「銳利化」最佳實務中會詳細說明銳利化。

**URL修飾元**  — 您可以提供其他S7影像指令來變更影像效果。 這些指令在「影像預設集」和「指令」參照中進行了說明。

**中斷點**  — 如果您的網站有回應，您想要調整中斷點。 中斷點必須以逗號(，)分隔。

### 图像模板 {#image-template}

Dynamic Media Classic (Scene7)影像範本是匯入至Dynamic Media Classic (Scene7)的分層Photoshop內容，其中的內容和屬性因可變性而引數化。 此 **[!UICONTROL 影像範本]** 元件可讓您匯入影像並動態變更Experience Manager文字。 此外，您可以設定 **[!UICONTROL 影像範本]** 元件來使用來自使用者端內容的值，讓每個使用者都能透過個人化的方式體驗影像。

選取 **[!UICONTROL 編輯]**  — 設定元件。 您可以設定 [所有Dynamic Media Classic (Scene7)元件的通用設定](/help/sites-administering/scene7.md#settingscommontoallscene7components) 以及本節中說明的其他設定。

![chlimage_1-55](assets/chlimage_1-55.png)

**檔案參照、寬度、高度**  — 請參閱 [所有Dynamic Media Classic (Scene7)元件的通用設定](/help/sites-administering/scene7.md#settingscommontoallscene7components).

>[!NOTE]
>
>Dynamic Media Classic (Scene7) URL命令和引數無法直接新增至檔案參考URL。 它們只能在的元件UI中定義 **[!UICONTROL 引數]** 面板。

**標題，替代文字**  — 在Dynamic Media Classic (Scene7)影像範本索引標籤中，為已關閉圖形的使用者新增影像標題和替代文字。

**URL，開啟位置**  — 您可以從設定資產以開啟連結。 設定URL，並在「開啟」中指定您要在同一個視窗或新視窗中開啟。

![chlimage_1-56](assets/chlimage_1-56.png)

**引數面板**  — 匯入影像時，引數會預先填入影像中的資訊。 如果沒有可動態變更的內容，則此視窗為空白。

![chlimage_1-57](assets/chlimage_1-57.png)

#### 動態變更文字 {#changing-text-dynamically}

若要動態變更文字，請在欄位中輸入新文字，然後選取 **[!UICONTROL 確定]**. 在此範例中， **價格** 現在為$50，運費為99美分。

![chlimage_1-58](assets/chlimage_1-58.png)

影像中的文字會變更。 您可以選取「 」，將文字重設為原始值 **[!UICONTROL 重設]** 欄位旁邊。

![chlimage_1-59](assets/chlimage_1-59.png)

#### 變更文字以反映使用者端內容值的值 {#changing-text-to-reflect-the-value-of-a-client-context-value}

若要將欄位連結至使用者端內容值，請選取 **[!UICONTROL 選取]** 若要開啟使用者端內容功能表，請選取使用者端內容，然後選取 **[!UICONTROL 確定]**. 在此範例中，名稱會隨著在設定檔中將「名稱」與格式化名稱連結而變更。

![chlimage_1-60](assets/chlimage_1-60.png)

此文字會反映目前登入使用者的名稱。 您可以選取「 」，將文字重設為原始值 **[!UICONTROL 重設]** 欄位旁邊。

![chlimage_1-61](assets/chlimage_1-61.png)

#### 將Dynamic Media Classic (Scene7)影像範本設為連結 {#making-the-scene-image-template-a-link}

您可以將Dynamic Media Classic (Scene7)影像範本元件設成可點按的連結。

1. 在具有Dynamic Media Classic (Scene7)影像範本元件的頁面上，選取 **[!UICONTROL 編輯]**.
1. 在 **[!UICONTROL URL]** 欄位中，輸入使用者點按影像時前往的URL。 在 **[!UICONTROL 開啟方式]** 欄位中，選取是否要開啟目標（新視窗或相同視窗）。

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. 選取 **[!UICONTROL 確定]**.

### 視訊元件 {#video-component}

Dynamic Media Classic (Scene7) **[!UICONTROL 視訊]** 元件(可在sidekick的Dynamic Media Classic (Scene7)區段中取得)使用裝置和頻寬偵測將正確的視訊提供給每個畫面。 此元件是HTML5視訊播放程式；它是可跨頻道使用的單一檢視器。

它可用於自我調整視訊集、單一MP4視訊或單一F4V視訊。

另請參閱 [視訊](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md) 如需影片如何與Dynamic Media Classic (Scene7)整合搭配使用的詳細資訊。 此外，請參閱如何 [此 **Dynamic Media Classic (Scene7)影片** 元件與基礎的比較 **視訊** 元件](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md).

![chlimage_1-63](assets/chlimage_1-63.png)

### 視訊元件的已知限制 {#known-limitations-for-the-video-component}

AdobeDAM和WCM會顯示是否上傳了主要來源影片。 它們不會顯示這些Proxy資產：

* Dynamic Media Classic (Scene7)編碼轉譯
* Dynamic Media Classic (Scene7)最適化視訊集

搭配Dynamic Media Classic (Scene7)視訊元件使用自我調整視訊集時，必須調整元件大小以符合視訊的尺寸。

## Dynamic Media Classic (Scene7)內容瀏覽器 {#scene-content-browser}

Dynamic Media Classic (Scene7)內容瀏覽器可讓您直接在Experience Manager中檢視Dynamic Media Classic (Scene7)的內容。 若要存取內容瀏覽器，請在「內容尋找器」中選取 **Dynamic Media Classic (Scene7)** 在觸控最佳化的使用者介面或 **S7** 圖示加以存取。 兩個使用者介面之間的功能相同。

如果您有多個組態，依預設，「Experience Manager」會顯示 [預設設定](/help/sites-administering/scene7.md#configuring-a-default-configuration). 您可以直接在Dynamic Media Classic (Scene7)內容瀏覽器中的下拉式選單中選取不同的設定。

>[!NOTE]
>
>* 隨選資料夾中的資產不會出現在Dynamic Media Classic (Scene7)內容瀏覽器中。
>* 時間 [已啟用安全預覽](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)，Dynamic Media Classic (Scene7)上已發佈和未發佈的資產都會出現在Dynamic Media Classic (Scene7)內容瀏覽器中。
>* 如果您沒有看見 **[!UICONTROL Dynamic Media Classic (Scene7)]** 或 **[!UICONTROL S7]** 圖示作為內容瀏覽器中的選項，您必須 [設定Dynamic Media Classic (Scene7)以使用Experience Manager](/help/sites-administering/scene7.md).
>* 對於視訊，Dynamic Media Classic (Scene7)內容瀏覽器支援：
   >   * 最適化視訊集：包含跨多個熒幕無縫播放所需的所有視訊轉譯的容器
   >   * 單一MP4視訊
   >   * 單一F4V視訊


### 浏览内容 {#browsing-content-in-the-classic-ui}

在Dynamic Media Classic (Scene7)中瀏覽內容，方法是選取 **[!UICONTROL S7]** 標籤。

您可以選取組態來變更您正在存取的組態。 資料夾會依您選取的組態而變更。

![chlimage_1-64](assets/chlimage_1-64.png)

和資產的內容尋找器一樣，您可以搜尋資產和篩選結果。 不過，與資產尋找器不同，當在 **S7** 標籤，檔案名稱 **開頭為** 您輸入的字串，而不是 **包含** 檔案名稱中的關鍵字。

依預設，資產會依檔案名稱顯示。 不過，您也可以依資產型別篩選結果。

>[!NOTE]
>
>對於視訊，WCM的Dynamic Media Classic (Scene7)內容瀏覽器支援：
>
>* 最適化視訊集：包含跨多個熒幕無縫播放所需的所有視訊轉譯的容器
>* 單一MP4視訊
>* 單一F4V視訊
>


### 使用內容瀏覽器搜尋Dynamic Media Classic (Scene7)資產 {#searching-for-scene-assets-with-the-content-browser}

搜尋Dynamic Media Classic (Scene7)資產與搜尋Experience Manager資產類似。 例外情況是，當您搜尋時，您實際上會在Dynamic Media Classic (Scene7)系統中看到資產的遠端檢視，而不是直接將資產匯入Experience Manager。

您可以使用傳統UI或觸控最佳化UI來檢視和搜尋資產。 依介面而定，搜尋方式會稍微有些不同。

在任何一個UI中搜尋時，您可以依下列條件進行篩選（如觸控最佳化UI中所示）：

**輸入關鍵字**  — 您可以依名稱搜尋資產。 搜尋關鍵字時，您會輸入檔案名稱的開頭。 例如，輸入「swimming」會尋找任何以那個順序開頭字母的資產檔案名稱。 輸入搜尋資產的辭彙後，請務必選取Enter。

![chlimage_1-65](assets/chlimage_1-65.png)

**資料夾/路徑**  — 資料夾的名稱是根據您選取的設定。 您可以選取資料夾圖示並選取子資料夾，然後選取核取記號來選取它，藉此向下展開至較低層級。

如果您輸入關鍵字並選取資料夾，Experience Manager會搜尋該資料夾及任何子資料夾。 但是，如果您在搜尋時未輸入任何關鍵字，則選取該資料夾只會顯示該資料夾中的資產，不包含任何子資料夾。

根據預設，Experience Manager會搜尋選取的資料夾和所有子資料夾。

![chlimage_1-66](assets/chlimage_1-66.png)

**資產型別**  — 選取Dynamic Media Classic (Scene7)以瀏覽Dynamic Media Classic (Scene7)內容。 此選項僅在Dynamic Media Classic (Scene7)已設定後才可用。

![chlimage_1-67](assets/chlimage_1-67.png)

**設定**  — 如果您在Cloud Services中定義了多個Dynamic Media Classic (Scene7)設定，您可以在此處選取它。 因此，資料夾會根據您選擇的設定而變更。

![chlimage_1-68](assets/chlimage_1-68.png)

**資產型別**  — 在Dynamic Media Classic (Scene7)瀏覽器中，您可以篩選結果以包含以下任一專案：影像、範本、視訊和自我調整視訊集。 如果您未選取任何資產型別，則「Experience Manager」預設會搜尋所有資產型別。

![chlimage_1-69](assets/chlimage_1-69.png)

>[!NOTE]
>
>* 在傳統UI中，您也可以搜尋 **Flash** 和 **FXG**. 不支援在觸控最佳化UI中篩選這兩個詞語。
>
>* 搜尋視訊時，您會搜尋單一轉譯。 結果會傳回原始轉譯(僅限 &#42;.mp4)和編碼的轉譯。
>* 搜尋最適化視訊集時，您會搜尋資料夾和所有子資料夾，但前提是您已新增關鍵字至搜尋。 如果您尚未新增關鍵字，Experience Manager不會搜尋子資料夾。
>


**發佈狀態**  — 您可以根據發佈狀態來篩選資產：未發佈或已發佈。 如果您未選取任何發佈狀態，則Experience Manager預設會搜尋所有發佈狀態。

![chlimage_1-70](assets/chlimage_1-70.png)
