---
title: 在Dynamic Media中使用3D資產
description: 瞭解如何在Dynamic Media中使用3D資產
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
feature: 3D Assets,Asset Management
role: User, Admin
exl-id: 01c96f1e-c0e6-497d-bd7a-c0fd547a34da
source-git-commit: 787c0c25da2258f234d3c821038d62bf8ef68932
workflow-type: tm+mt
source-wordcount: '2358'
ht-degree: 3%

---

# 在Dynamic Media中使用3D資產 {#working-with-three-d-assets-dm}

Dynamic Media可讓您上傳、管理、檢視及傳遞3D資產，以盡情享受身臨其境的體驗。

* 一鍵式發佈(使用 **[!UICONTROL 快速發佈]** （在工具列上）以產生URL。
* 透過由Adobe Dimension提供支援的高品質互動式Dimensional檢視器預設集，針對檢視3D資產提供最佳化支援。
* 3D Media WCM元件可讓您輕鬆將3D資產新增至Adobe Experience Manager Sites頁面。

在Dynamic Media中使用3D資產不需要額外的設定。

![3d鞋子](/help/assets/assets-dm/3d-dimensional-viewer-quickpublish-url-embed2.png) *立體鞋的詳細資訊頁面。*

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Dynamic Media支援的3D格式 {#supported-three-d-file-formats-in-dm}

Dynamic Media支援下列3D格式。

另請參閱 [支援的3D格式](/help/assets/assets-formats.md).

| 3D副檔名 | 檔案格式 | MIME型別 | 注释 |
|---|---|---|---|
| GLB | 二進位GL傳輸 | model/gltf-binary | 將材質和紋理納入為單一資產。 |
| 物件 | WaveFront 3D物件檔案 | application/x-tgif |  |
| STL | 立體光刻 | application/vnd.ms-pki.stl |  |
| USDZ | Universal Scene說明Zip封存 | model/vnd.usdz+zip | *僅支援內嵌；不提供檢視或互動。* USDZ是專屬的3D格式，可供Safari和iOS裝置原生檢視。 |

>[!NOTE]
>
>資產「詳細資訊」頁面上的3D Media WCM元件和3D預覽版與最新版Chrome (97.x)不相容。 若要使用3D資產，請使用Firefox或Safari，或使用舊版Chrome (96.x)。

## 快速入門：Dynamic Media中的3D資產 {#quick-start-three-d}

下列逐步工作流程說明可協助您在Dynamic Media - Scene7模式中快速啟動和執行3D資產。

>[!IMPORTANT]
>
>Dynamic Media — 混合模式不支援3D資產。

在Dynamic Media中使用3D資產之前，請確定您的Experience Manager管理員已在Dynamic Media - Scene7模式下啟用並設定Dynamic MediaCloud Services。

另請參閱 [設定Dynamic MediaCloud Services](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services) 在設定Dynamic Media - Scene7模式和 [疑難排解Dynamic Media - Scene7模式](/help/assets/troubleshoot-dms7.md).

1. **上傳3D資產**

   * [上傳您的3D資產以用於Dynamic Media](/help/assets/manage-assets.md#uploading-assets).
   * [Dynamic Media支援的上傳3D檔案格式](#supported-three-d-file-formats-in-dm).

1. **管理立體資產**

   * 組織和搜尋3D資產

      * [組織數位資產](/help/assets/organize-assets.md#organize-digital-assets).
      * [搜尋三維資產](/help/assets/search-assets.md).
      * [使用自訂述詞來篩選搜尋結果](/help/assets/search-assets.md#custompredicates).
   * 檢視三維資產

      * [檢視及與3D資產互動](#viewing-three-d-assets).
      * [管理維度檢視器預設集](/help/assets/managing-viewer-presets.md).
   * 使用3D資產中繼資料

      * [管理數位資產的中繼資料](/help/assets/metadata.md).
      * [元数据架构](/help/assets/metadata-schemas.md).



1. **發佈3D資產**

   * [發佈靜態Dynamic Media 3D資產](#publishing-three-d-assets)
   * [使用維度檢視器發佈Dynamic Media 3D資產的替代方法](#alternate-publish-methods)

## 關於檢視和與3D資產互動 {#viewing-three-d-assets}

本節說明如何以兩種不同的方式檢視3D資產並與其互動：在資產詳細資訊頁面內以及在Experience Manager Sites的3D媒體元件內。

互動式3D檢視器包含一系列互動式相機控制項，可供您環繞、縮放和平移3D資產。

在「資產詳細資訊」頁面檢視中開啟3D資產所需的時間取決於幾個因素。 這些因素包括：

* 伺服器的頻寬。
* 伺服器的延遲
* 影像的複雜性。

此外，使用者端電腦的功能（例如工作站、筆記型電腦或行動觸控裝置）也是您以互動方式操作相機時也必須考量的重要因素。 功能相當強大、圖形功能良好的系統，可讓互動式3D觀賞體驗更順暢、更理想。

>[!TIP]
>
>您可以在檢視器預設集編輯器中開啟維度檢視器預設集，以練習導覽3D資產，而無需先上傳任何3D檔案。 維度檢視器預設集內建了3D資產，可供您互動。
>
>另請參閱 [管理檢視器預設集](/help/assets/managing-viewer-presets.md).

## 從資產詳細資訊頁面檢視3D資產並與其互動 {#viewing-three-d-assets-from-asset-details-page}

另請參閱 [使用軟體介面預覽資產](/help/assets/previewing-assets.md).

**若要從資產詳細資訊頁面檢視3D資產並與其互動：**

1. 請確定您已將3D資產上傳至Experience Manager。

   另請參閱 [上傳您的3D資產以用於Dynamic Media](/help/assets/manage-assets.md#uploading-assets).

1. 從Experience Manager，在 **[!UICONTROL 導覽]** 頁面，前往 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**.
1. 在頁面的右上角附近，從 **[!UICONTROL 檢視]** 下拉式清單，選取 **[!UICONTROL 卡片檢視]**.
1. 導覽至您要檢視的3D資產。
1. 選取3D資產的卡片。
1. 在3D資產的詳細資訊檢視頁面上，執行下列任一項作業：

   | 查看 | 描述 | 滑鼠動作 | 觸控熒幕動作 |
   | --- | --- | --- | --- |
   | **轉動相機** | 围绕 3D 场景和对象旋转视图。 | 按一下左鍵+拖曳。 | 單指按下+拖曳。 |
   | **平移相機** | 向左、向右、向上或向下平移檢視。 | 按一下滑鼠右鍵+拖曳。 | 兩指按下+拖曳。 |
   | **縮放相機** | 在3D場景中移入和移出區域。 | 滾輪。 | 兩指捏合。 |
   | **重新將相機置中** | 將相機重新置中至3D場景中物件上的一點。 | 按兩下。 | 點兩下。 |
   | **重置** | 在頁面的右下角附近，選取「重設」圖示，將檢視目標點恢復到3D資產的中心。 重設也會將相機移到更近或更遠的位置，以完整的方式顯示資產，並維持合理的檢視大小。 |  |  |
   | **全屏模式** | 若要進入全熒幕模式，請在頁面的右下角，選取「全熒幕」圖示。 |  |  |

1. 在頁面的右上角，選取 **[!UICONTROL 關閉]** 返回「資產」頁面。

## 在3D媒體元件中檢視3D資產並與之互動 {#interacting-with-asset-inside-three-d-media-component}

當網頁位於 **[!UICONTROL 編輯]** 模式，無法與3D資產互動。 若要讓資產具有互動式，您可以使用 **[!UICONTROL 預覽]** 可在頁面編輯器中檢視網頁的功能，並可完整存取3D媒體元件的功能。

>[!IMPORTANT]
>
>您必須先將3D媒體元件新增至網頁並指派3D資產至元件，才能完成此工作。 另請參閱 [將3D媒體元件新增至網頁](#adding-the-three-d-media-component-to-a-web-page) 和 [為3D媒體元件指派3D資產](#assigning-a-three-d-asset-to-the-component).

另請參閱 [使用軟體介面預覽資產](/help/assets/previewing-assets.md).

**若要在3D媒體元件中檢視3D資產並與其互動：**

1. 當網頁位於 **[!UICONTROL 編輯]** 模式，執行下列任一項作業：

   * 在頁面的右上角附近，選取 **[!UICONTROL 預覽]** 以輸入 **[!UICONTROL 預覽]** 模式。
   * 刪除 `/editor.html` 從瀏覽器中的頁面URL。

完全互動的3D資產，顯示於    ![3D資產顯示在3D媒體元件內](/help/assets/assets-dm/3d-asset-in-3d-media.png)
完全互動的3D資產，顯示於 **[!UICONTROL 預覽]** 模式。

1. 當在 **[!UICONTROL 預覽]** 模式，執行下列任一項作業：

   | 查看 | 描述 | 滑鼠動作 | 觸控熒幕動作 |
   | --- | --- | --- | --- |
   | **轉動相機** | 围绕 3D 场景和对象旋转视图。 | 按一下左鍵+拖曳。 | 單指按下+拖曳。 |
   | **平移相機** | 向左、向右、向上或向下平移檢視。 | 按一下滑鼠右鍵+拖曳。 | 兩指按下+拖曳。 |
   | **縮放相機** | 在3D場景中移入和移出區域。 | 滾輪。 | 兩指捏合。 |
   | **重新將相機置中** | 將相機重新置中至3D場景中物件上的一點。 | 按兩下。 | 點兩下。 |
   | **重置** | 在頁面的右下角附近，選取「重設」圖示，將檢視目標點恢復到3D資產的中心。 重設也會將相機移到更近或更遠的位置，以完整的方式顯示資產，並維持合理的檢視大小。 |  |  |
   | **全屏模式** | 若要進入全熒幕模式，請在頁面的右下角，選取「全熒幕」圖示。 |  |  |

## 關於使用3D媒體元件 {#working-with-three-d-media-component}

Dynamic Media內含Dynamic Media 3D Media元件，您可以在Adobe Experience Manager Sites中使用，在網頁上以互動方式檢視3D模型。

* [將3D媒體元件新增至頁面範本](#adding-three-d-media-component-to-page-template)
* [將3D媒體元件新增至網頁](#adding-the-three-d-media-component-to-a-web-page)
   * [可選 — 設定3D媒體元件](#configuring-the-three-d-component)
* [將3D資產指派給3D媒體元件](#assigning-a-three-d-asset-to-the-component)

## 將3D媒體元件新增至頁面範本 {#adding-three-d-media-component-to-page-template}

1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 範本]**.
1. 導覽至您要啟用3D元件的頁面範本，然後選取範本。
1. 選取 **[!UICONTROL 編輯]** 以便您開啟範本。
1. 在頁面的右上角附近，在下拉式選單中選取 **[!UICONTROL 結構]** 模式（如果尚未啟用）。

   ![3d-media-component-structure](/help/assets/assets-dm/3d-media-component-structure.png)

1. 選取一個空白區域 **[!UICONTROL 配置容器]** 區域，讓您選取它並開啟其關聯的工具列。
1. 在工具列上，選取 **[!UICONTROL 原則]** 圖示以開啟 **[!UICONTROL 原則編輯器]**.
1. 在 **[!UICONTROL 屬性]** 區段，在 **[!UICONTROL 允許的元件]** 標籤，捲動至 **[!UICONTROL Dynamic Media]**，然後展開清單並勾選 **[!UICONTROL 3D媒體]**.
1. 選取 **[!UICONTROL 完成]** 以儲存變更並關閉 **[!UICONTROL 原則編輯器]**.

   您現在可以將Dynamic Media 3D媒體元件放置在使用此範本的所有頁面上。

## 在網頁上新增3D媒體元件 {#adding-the-three-d-media-component-to-a-web-page}

如果您使用Experience Manager作為網頁內容管理系統，您可以透過3D媒體元件將3D資產新增至網頁。

另請參閱 [在頁面上新增Dynamic Media資產](/help/assets/adding-dynamic-media-assets-to-pages.md).

**若要在網頁上新增3D媒體元件：**

1. 開啟Experience Manager Sites並選取您要新增Dynamic Media 3D媒體元件的網頁。
1. 選取 **[!UICONTROL 編輯]** （鉛筆）圖示，讓您可以在頁面編輯器中開啟頁面。 請確定 **[!UICONTROL 編輯]** 模式會選取在頁面右上角附近。

   ![3d-media-component-add](/help/assets/assets-dm/3d-media-component-edit.png)

1. 在工具列上，選取「側面板」圖示以切換或「開啟」面板的顯示。

1. 在側面板中，選取加號圖示以開啟 **[!UICONTROL 元件]** 清單。

   ![3d-media-component-drag-drop](/help/assets/assets-dm/3d-assets-filter.png)

1. 拖曳 **[!UICONTROL 3D媒體]** 元件來自 **[!UICONTROL 元件]** 列出要在頁面上顯示3D檢視器的位置。

您現在已準備好為元件指派3D資產。

另請參閱 [將3D資產指派給3D媒體元件](#assigning-a-three-d-asset-to-the-component).

### 可選 — 設定3D媒體元件 {#configuring-the-three-d-component}

1. 在Experience Manager Sites頁面編輯器中，選取 **[!UICONTROL 3D媒體檢視器]** 先前新增至頁面的元件。
1. 選取 **[!UICONTROL 設定]** 圖示（扳手）以開啟「元件組態」對話方塊。

   ![3d-media-component-config](/help/assets/assets-dm/3d-media-component-config.png)

1. 在「3D媒體」對話方塊中，從「檢視器預設集」下拉式清單中選取 **[!UICONTROL 維度]** 將「維度」檢視器預設集指派給元件。

   ![3d-media-component-edit-config](/help/assets/assets-dm/3d-media-component-edit-config.png)

1. 在右上角，選取核取記號以儲存變更。

## 將3D資產指派給3D媒體元件 {#assigning-a-three-d-asset-to-the-component}

將3D媒體元件新增至網頁後，即可為其指派3D資產。

另請參閱 [將3D媒體元件新增至網頁](#adding-the-three-d-media-component-to-a-web-page).

**若要將3D資產指派給3D媒體元件：**

1. 在Experience Manager Sites頁面編輯器中，選取 **[!UICONTROL 資產]** 圖示以開啟 **[!UICONTROL 資產]** 於側面板中。
1. 在下拉式清單中，選取 **[!UICONTROL 三維]** 以僅顯示3D資產檔案型別。
1. 在側面板中，搜尋或捲動至您要在編輯的頁面上檢視的3D資產。
1. 從「資產」側面板拖曳3D資產，並將其拖放至 **[!UICONTROL 3D媒體]** 先前新增至頁面的元件。

   ![將3D資產指派給3D媒體元件](/help/assets/assets-dm/3d-asset-add.png)

>[!NOTE]
>
>當網頁位於Experience Manager Sites中時 **[!UICONTROL 編輯]** 模式，「3D媒體」元件會顯示3D資產，但無法與資產互動。 若要讓資產具有互動式，您可以使用 **[!UICONTROL 預覽]** 可在頁面編輯器中檢視網頁的功能，並可完整存取3D媒體元件的功能。

## 發佈靜態Dynamic Media 3D資產 {#publishing-three-d-assets}

Dynamic Media接受以下支援的各種3D檔案格式 *靜態內容* 在Dynamic Media中。 靜態內容表示您可以上傳和發佈3D資產，但不支援 *變數影像* 或與3D資產相關聯的影像重新調整。 原因在於Dynamic Media Imaging Server無法辨識3D格式。 因此，在Dynamic Media中發佈3D資產後，您就可以立即複製URL。 3D資產的URL會遵循一般的Dynamic Media URL結構。 不過，與Dynamic Media中的傳統影像資產不同，您無法編輯資產URL中的任何引數。

另請參閱 [取得靜態資產的URL](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset).

在 **[!UICONTROL 卡片檢視]**，資產名稱正下方及其日期和時間左側會出現一個小地球圖示，指出資產已發佈。 在&#x200B;**[!UICONTROL 列表视图]**&#x200B;中，**[!UICONTROL 已发布]**&#x200B;列显示已发布的资产和未发布的资产。

如果您使用Experience Manager做為WCM，請使用此發佈方法直接在網頁上新增Dynamic Media 3D資產。

另請參閱 [發佈Dynamic Media資產](publishing-dynamicmedia-assets.md).

另請參閱 [發佈頁面](/help/sites-authoring/publishing-pages.md).

**若要發佈靜態Dynamic Media 3D資產：**

1. 開啟3D資產（GLB、OBJ或STL檔案格式），以便在資產詳細資訊頁面中檢視它。
1. 在工具列上，選取 **[!UICONTROL 快速發佈]**.

   ![3d-asset-quick-publish](/help/assets/assets-dm/3d-asset-quick-publish.png)

1. 選取 **[!UICONTROL 關閉]** 以結束對話方塊並返回資產詳細資訊頁面。
1. 從3D資產檔案名稱左側的下拉式清單中，選取 **[!UICONTROL 轉譯]**.

   ![3d-asset-renditions](/help/assets/assets-dm/3d-asset-renditions.png)

1. 選取 **[!UICONTROL 原始]**. 發佈（或「啟動」）3D資產時， **[!UICONTROL URL]** 如果符合下列3D資產條件，按鈕會出現在頁面左下角附近：
   * 3D資產是支援的格式（GLB、OBJ、STL和USDZ）。
   * 3D資產已內嵌至Dynamic Media Image Production System (IPS)。
   * 3D資產隨即發佈。

   ![3d-asset-url](/help/assets/assets-dm/3d-asset-url.png)

1. 選取 **[!UICONTROL URL]** 以便顯示3D資產的直接生產URL，供您在網頁上複製和使用。

### 使用維度檢視器發佈Dynamic Media 3D資產的替代方法 {#alternate-publish-methods}

若要發佈Dynamic Media 3D資產，請使用下列兩種方法 *not* 使用Experience Manager做為WCM。

* **[!UICONTROL URL]**  — 使用 **[!UICONTROL URL]** 如果您使用協力廠商網頁內容管理系統，且想使用「維度」檢視器將Dynamic Media 3D資產連結至網頁。

   另請參閱 [將URL連結至您的網頁應用程式](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset).

* **[!UICONTROL 內嵌]**  — 使用 **[!UICONTROL 內嵌]** 當您想要使用「維度」檢視器來檢視內嵌在網頁上的Dynamic Media 3D資產時。 将嵌入代码复制到剪贴板，以便将其粘贴到网页中。 中不允許編輯程式碼 **[!UICONTROL 內嵌]** 對話方塊。

   另請參閱 [將Dynamic Media視訊、影像檢視器或維度檢視器內嵌在網頁上](/help/assets/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page).
