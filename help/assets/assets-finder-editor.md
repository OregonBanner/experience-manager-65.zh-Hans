---
title: 建立和設定Asset Editor頁面
description: 瞭解如何建立自訂Asset Editor頁面並同時編輯多個資產。
contentOwner: AG
role: User, Admin
feature: Developer Tools,Asset Management
exl-id: 53e310a9-c511-447a-91bd-8c5b2760dc03
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '2125'
ht-degree: 1%

---

# 建立和設定Asset Editor頁面 {#creating-and-configuring-asset-editor-pages}

本檔案說明下列各項：

* 為什麼要建立自訂的Asset Editor頁面。
* 如何建立和自訂Asset Editor頁面，這些頁面為WCM頁面，可讓您檢視和編輯中繼資料，以及執行資產動作。
* 如何同時編輯多個資產。

<!-- TBD: Add UICONTROL tags. Need PM review. Flatten the structure a bit. Re-write to remove Geometrixx mentions and to adhere to 6.5 default samples. -->

>[!NOTE]
>
>資產共用可作為開放原始碼參考實作。 另請參閱 [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/). 未正式支援。

## 為何要建立和設定Asset Editor頁面？ {#why-create-and-configure-asset-editor-pages}

數位資產管理正在越來越多的案例中使用。 從專為受過專業訓練的使用者群體（例如攝影師或分類學家）提供的小型解決方案，轉移至更大且更多樣化的使用者群組（例如商業使用者、WCM作者、記者等）時，強大的 [!DNL Adobe Experience Manager Assets] 若是專業使用者，可能會提供太多資訊，而利害關係人會開始請求特定的使用者介面或應用程式，以存取與他們相關的數位資產。

這些以資產為中心的應用程式，可以是內部網路中的簡易像片收藏館，員工可以透過商業展覽造訪或公開網站上的新聞中心上傳像片。 以資產為中心的應用程式也可以延伸至完整的解決方案，包括購物車、結帳和驗證程式。

建立以資產為中心的應用程式，在很大程度上會變成不需要編碼的設定程式，只需要使用者群組及其需求的知識，以及所使用中繼資料的知識。 以資產為中心的應用程式，建立於 [!DNL Assets] 可擴充：透過適度編碼投入，可建立可重複使用的元件，用於搜尋、檢視和修改資產。

以資產為中心的應用程式 [!DNL Experience Manager] 包含一個Asset Editor頁面，可用來取得特定資產的詳細檢視。 如果存取資產的使用者擁有必要許可權，資產編輯器頁面也允許編輯中繼資料。

<!--
## Create and configure an Asset Share page {#creating-and-configuring-an-asset-share-page}

You customize the DAM Finder functionality and create pages that have all the functionality you require, which are called Asset Share pages. To create a new Asset Share page, you add the page using the Geometrixx Asset Share template and then you customize the actions users can perform on that page, determine how viewers see the assets, and decide how users can build their queries.

Here are some use cases for creating a customized Asset Share page:

* Press Center for Journalists.
* Image Search Engine for internal business users.
* Image Database for website users.
* Media Tagging Interface for metadata editors.

### Create an Asset Share page {#creating-an-asset-share-page}

To create a new Asset Share page, you can either create it when you are working on web sites or from the digital asset manager.

>[!NOTE]
>
>By default, when you create an Asset Share page from **New** in the digital asset manager, an Asset viewer and Asset editor are automatically created for you.

To create an new Asset Share page in the **Websites** console:

1. In the **Websites** tab, navigate to the place where you want to create an asset share page and click **New**.

1. Select the **Asset Share** page and click **Create**. The new page is created and the asset share page is listed in the **Websites** tab.

![dam8](assets/dam8.png)

The basic page created using the Geometrixx DAM Asset Share template looks as follows:

![screen_shot_2012-04-18at115456am](assets/screen_shot_2012-04-18at115456am.png)

To customize your Asset Share page, you use elements from the sidekick and you also edit query builder properties. The page **Geometrixx Press Center** is a customized version of a page based on this template:

![screen_shot_2012-04-19at123048pm](assets/screen_shot_2012-04-19at123048pm.png)

To create a new asset share page via the digital asset manager:

1. In the digital asset manager, in **New**, select **New Asset Share**.
1. In the **Title**, enter the name of the asset share page. If desired, enter a name for the URL.

   ![screen_shot_2012-04-19at23626pm](assets/screen_shot_2012-04-19at23626pm.png)

1. Double-click the asset share page to open it and configure the page.

   ![screen_shot_2012-04-19at24114pm](assets/screen_shot_2012-04-19at24114pm.png)

   By default, when you create an Asset Share page from **New**, an Asset viewer and Asset editor are automatically created for you.

#### Customize actions {#customizing-actions}

You can determine what actions users can perform on selected digital assets from a selection of predefined actions.

To add actions to the Asset Share page:

1. In the Asset Share page that you want to customize, click **Actions** in the sidekick.

The following actions are available:

 | Action | Description |
 |---|---|
 | [!UICONTROL Delete Action] | Users can delete the selected assets. |
 | [!UICONTROL Download Action] | Lets users download selected assets to their computers. |
 | [!UICONTROL Lightbox Action] | Saves assets to a "lightbox"   where you can perform other actions on them. This comes in handy when working   with assets across multiple pages. The lightbox can also be used as a   shopping cart for assets. |
 | [!UICONTROL Move Action] | Users can move the asset to another   location |
 | [!UICONTROL Tags Action] | Lets users add tags to selected assets |
 | [!UICONTROL View Asset Action] | Opens the asset in the Asset editor for   user manipulation. |

1. Drag the appropriate action to the **Actions** area on the page. Doing so creates a button that is used to execute that action.

![chlimage_1-159](assets/chlimage_1-387.png)

#### Determine how search results are presented {#determining-how-search-results-are-presented}

You determine how results are displayed from a predefined list of lenses.

To change how search results are viewed:

1. In the Asset Share page that you want to customize, click Search.

![chlimage_1](assets/assetshare3.png)

1. Drag the appropriate lens to the top center of the page. In the Press Center, the lenses are already available. Users press the appropriate lens icon to display search results as desired.

The following lenses are available:

| Lens | Description |
|---|---|
| **[!UICONTROL List Lens]** |Presents the assets in a list fashion with details. |
| **[!UICONTROL Mosaic Lens]** |Presents assets in a mosaic fashion. |

#### Mosaic Lens {#mosaic-lens}

![chlimage_1-160](assets/chlimage_1-388.png)

#### List Lens {#list-lens}

![chlimage_1-161](assets/chlimage_1-389.png)

#### Customize the Query Builder {#customizing-the-query-builder}

The query builder lets you enter search terms and create content for the Asset Share page. When you edit the query builder, you also get to determine how many search results are displayed per page, which asset editor opens when you double-click an asset, the path the query searches, and customizes nodetypes.

To customize the query builder:

1. In the Asset Share page that you want to customize, click **Edit** in the Query Builder. By default, the **General** tab opens.
1. Select the number of results per page, the path of the asset editor (if you have a customized asset editor) and the Actions title.

![screen_shot_2012-04-23at15055pm](assets/screen_shot_2012-04-23at15055pm.png)

1. Click the **Paths** tab. Enter a path or multiple paths that the search will run. These paths are overwritten if the user uses the Paths predicate.

![screen_shot_2012-04-23at15150pm](assets/screen_shot_2012-04-23at15150pm.png)

1. Enter another node type, if desired.

1. In the **Query Builder URL** field, you can override or wrap the query builder and enter the new servlet URLs with the existing query builder component. In the **Feed URL** field, you can override the Feed URL as well.

![screen_shot_2012-04-23at15313pm](assets/screen_shot_2012-04-23at15313pm.png)

1. In the **Text** field, enter the text you want to appear for results and page numbers of results. Click **OK** when finished making changes.

![screen_shot_2012-04-23at15300pm](assets/screen_shot_2012-04-23at15300pm.png)

#### Add predicates {#adding-predicates}

Experience Manager Assets includes a number of predicates that you can add to the Asset Share page. These let your users further narrow searches. In some cases, they may override a query builder parameter (for example, the Path parameter).

To add predicates:

1. In the Asset Share page that you want to customize, click **Search**.

![assetshare3](assets/assetshare3.png)

1. Drag the appropriate predicates to the Asset Share page underneath the query builder. Doing so creates the appropriate fields.

![assetshare4](assets/assetshare4.png)

The following predicates are available:

| Predicate | Description |
|---|---|
| **[!UICONTROL Date Predicate]** |Lets users search for assets that were modified before and after certain dates. |
| **[!UICONTROL Options Predicate]** |The site owner can specify a property to search for (as in the property predicate, for example cq:tags) and a content tree to populate the options from (for example the tag tree). Doing so generates a list of options where the users can select the values (tags) that the selected property (tag property) should have. This predicate lets you build list controls like the list of tags, file types, image orientations, and so on. It is great for a fixed set of options. |
| **[!UICONTROL Path Predicate]** |Lets users define the path and subfolders, if desired. |
| **[!UICONTROL Property Predicate]** |The site owner specifies a property to search for, e.g. tiff:ImageLength and the user can then enter a value, e.g. 800. This returns all images that are 800 pixels high. Useful predicate if your property can have arbitrary values. |

For more information, see the [predicate Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/package-summary.html).

1. To configure the predicate further, double-click it. For example, when you open the Path Predicate, you need to assign the root path.

![screen_shot_2012-04-23at15640pm](assets/screen_shot_2012-04-23at15640pm.png)
-->

## 建立和設定Asset Editor頁面 {#creating-and-configuring-an-asset-editor-page}

您可以自訂資產編輯器，以決定使用者如何檢視和編輯數位資產。 要執行此操作，您需要建立新的Asset Editor頁面，然後自訂使用者可在該頁面上執行的檢視和動作。

>[!NOTE]
>
>如果您想要將自訂欄位新增到DAM資產編輯器，請新增 `cq:Widget` 節點至 `/apps/dam/content/asseteditors.`

### 建立資產編輯器頁面 {#creating-the-asset-editor-page}

建立Asset Editor頁面時，最佳做法是直接在Asset Share頁面的下方建立頁面。

若要建立Asset Editor頁面：

1. 在 **[!UICONTROL 網站]** 索引標籤上，導覽至您要建立資產編輯器頁面的位置，然後按一下 **新增**.
1. 選取 **Geometrixx資產編輯器** 並按一下 **建立**. 隨即會建立新頁面，且頁面會列於 **網站** 標籤。

![screen_shot_2012-04-23at15858pm](assets/screen_shot_2012-04-23at15858pm.png)

使用GeometrixxAsset Editor範本建立的基本頁面如下所示：

![assetshare5](assets/assetshare5.png)

若要自訂您的Asset Editor頁面，請使用sidekick中的元素。 可從存取的Asset Editor頁面 **Geometrixx新聞中心** 是根據此範本自訂的頁面版本：

![assetshare6](assets/assetshare6.png)

#### 設定Asset Editor以從資產共用頁面開啟 {#setting-which-asset-editor-opens-from-an-asset-share-page}

建立自訂的Asset Editor頁面後，您需要確保連按兩下資產時，您所建立的自訂資產共用會在自訂的編輯器頁面中開啟資產。

若要設定Asset Editor頁面：

1. 在資產共用頁面中，按一下 **編輯** ，位於「查詢產生器」旁。

![screen_shot_2012-04-23at20123pm](assets/screen_shot_2012-04-23at20123pm.png)

1. 按一下 **一般** 標籤（如果尚未選取）。

1. 在 **Asset Editor路徑** 欄位中，輸入資產編輯器的路徑，以便「資產共用」頁面在中開啟資產，然後按一下 **確定**.

![screen_shot_2012-04-23at21653pm](assets/screen_shot_2012-04-23at21653pm.png)

#### 新增Asset Edit元件 {#adding-asset-editor-components}

您可以將元件新增至頁面，藉此決定資產編輯器具備哪些功能。

若要新增資產編輯器元件：

1. 在要自訂的Asset Editor頁面中，選取 **資產編輯器** 在sidekick。 所有可用的Asset Editor元件都會顯示。

>[!NOTE]
>
>您可以自訂的內容取決於可用的元件。 若要啟用元件，請前往「設計」模式並選取需要啟用的元件。

1. 將元件從Sidekick拖曳至資產編輯器，並在元件對話方塊中進行任何修改。 這些元件如下表所述，並詳見以下詳細說明。

>[!NOTE]
>
>設計資產編輯器頁面時，您可以建立唯讀或可編輯的元件。 使用者知道如果鉛筆影像出現在元件中，可以編輯欄位。 依預設，大部分元件都設定為唯讀。

| 组件 | 描述 |
|---|---|
| **[!UICONTROL 中繼資料表單] 和 [!UICONTROL 中繼資料文字欄位]** | 可讓您新增其他中繼資料至資產，以及對該資產執行動作（例如提交）。 |
| **[!UICONTROL 子资产]** | 可讓您自訂子資產。 |
| **标记** | 可讓使用者選取標籤並將其新增至資產。 |
| **[!UICONTROL 缩略图]** | 顯示資產的縮圖及其檔案名稱，並可讓您新增替代文字。 您也可以在這裡新增資產編輯器動作。 |
| **[!UICONTROL 标题]** | 顯示可自訂的資產標題。 |

![screen_shot_2012-04-23at22743pm](assets/screen_shot_2012-04-23at22743pm.png)

#### 中繼資料表單和文字欄位 — 設定檢視中繼資料元件 {#metadata-form-and-text-field-configuring-the-view-metadata-component}

中繼資料表單是包含開始和結束動作的表單。 在兩者之間，輸入 **文字** 欄位。 另請參閱 [Forms](/help/sites-authoring/default-components-foundation.md#form-component) 以取得使用表單的詳細資訊。

1. 按一下「 」以建立開始動作 **編輯** 在表單的「開始」區域中。 您可以視需要輸入「方塊」標題。 根據預設，「方塊」標題為 **中繼資料**. 如果您要產生java-script使用者端代碼進行驗證，請選取「使用者端驗證」核取方塊。

![screen_shot_2012-04-23at22911pm](assets/screen_shot_2012-04-23at22911pm.png)

1. 按一下以建立「結束」動作 **編輯** 在表單的「結束」區域中。 例如，您可能想要建立 **[!UICONTROL 提交]** 允許使用者提交其中繼資料變更的選項。 或者，您也可以新增 **重設** 將中繼資料重設為其原始狀態的選項。

![screen_shot_2012-04-23at23138pm](assets/screen_shot_2012-04-23at23138pm.png)

1. 介於 **表單開始** 和 **表單結尾**，將中繼資料文字欄位拖曳至表單。 使用者會將中繼資料填入這些文字欄位中，以便提交或完成其他動作。

1. 連按兩下欄位名稱，例如， **標題** 以開啟中繼資料欄位並進行變更。 在 **一般** 的標籤 **編輯元件** 視窗，您可以定義名稱空間和欄位標籤以及型別，例如， `dc:title`.

![screen_shot_2012-04-23at23305pm](assets/screen_shot_2012-04-23at23305pm.png)

另請參閱 [自訂和擴充資產](/help/assets/extending-assets.md) 以取得有關修改中繼資料表單中可用名稱空間的資訊。

1. 按一下 **限制** 標籤。 您可以在此選取是否需要欄位，並視需要新增任何限制。

![screen_shot_2012-04-23at23435pm](assets/screen_shot_2012-04-23at23435pm.png)

1. 按一下 **顯示** 標籤。 在這裡，您可以為中繼資料欄位輸入新的寬度和列數。 選取 **欄位為唯讀** 核取方塊可讓使用者編輯中繼資料。

![screen_shot_2012-04-23at23446pm](assets/screen_shot_2012-04-23at23446pm.png)

以下是包含各種欄位的中繼資料表單範例：

![元数据](assets/chlimage_1-390.png)

然後，使用者可以在「資產編輯器」頁面的中繼資料欄位中輸入值（如果可編輯），並執行結束動作（例如，提交變更）。

#### 子资产 {#sub-assets}

子資產元件是您檢視和選取子資產的地方。 您可以決定 [主要資產](/help/assets/assets.md#what-are-digital-assets) 和子資產。

連按兩下Sub Assets元件以開啟Sub Assets對話方塊，您可以在此變更主要資產和任何子資產的標題。 預設值會顯示在對應欄位下方。

![screen_shot_2012-04-23at23907pm](assets/screen_shot_2012-04-23at23907pm.png)

以下是填入的Sub Assets元件範例：

![screen_shot_2012-04-23at24442pm](assets/screen_shot_2012-04-23at24442pm.png)

例如，如果您選取子資產，請注意元件如何顯示適當的頁面，以及「方塊」標題如何從「子資產」變更為「同層級」。

![screen_shot_2012-04-23at24552pm](assets/screen_shot_2012-04-23at24552pm.png)

#### 标记 {#tags}

標籤元件是使用者可以將現有標籤指派給資產的元件，這有助於日後的組織和擷取。 您可以將此元件設為唯讀，讓使用者無法新增標籤，但只能檢視標籤。

![screen_shot_2012-04-23at25031pm](assets/screen_shot_2012-04-23at25031pm.png)

連按兩下Tags元件以開啟Tags對話方塊，您可以在其中視需要變更Tags的標題，以及選取配置的名稱空間。 若要讓此欄位可編輯，請清除 **[!UICONTROL 隱藏編輯]** 核取方塊。 依預設，標籤是可編輯的。

![screen_shot_2012-04-23at24731pm](assets/screen_shot_2012-04-23at24731pm.png)

如果使用者可以編輯標籤，則他們可以按一下鉛筆，透過從「標籤」下拉式選單中選取標籤來新增標籤。

![screen_shot_2012-04-23at25150pm](assets/screen_shot_2012-04-23at25150pm.png)

以下是填入的Tags元件：

![screen_shot_2012-04-23at25244pm](assets/screen_shot_2012-04-23at25244pm.png)

#### 缩略图 {#thumbnail}

縮圖元件是資產顯示所選縮圖的地方（對於許多格式，縮圖會自動擷取）。 此外，元件會顯示檔案名稱，以及 [您可以修改的動作](/help/assets/assets-finder-editor.md#adding-asset-editor-actions).

![screen_shot_2012-04-23at25452pm](assets/screen_shot_2012-04-23at25452pm.png)

連按兩下縮圖元件以開啟縮圖對話方塊，您可以在此變更替代文字。 根據預設，縮圖替代文字預設為 **按一下以下載** 資產。

![screen_shot_2012-04-23at25604pm](assets/screen_shot_2012-04-23at25604pm.png)

以下是填入的Thumbnail元件範例：

![screen_shot_2012-04-23at34815pm](assets/screen_shot_2012-04-23at34815pm.png)

#### 标题 {#title}

標題元件會顯示資產的標題和說明。

預設為唯讀模式，因此使用者無法編輯它。 若要使其可編輯，請連按兩下元件並清除 **隱藏編輯按鈕** 核取方塊。 此外，輸入多個資產的標題。

![screen_shot_2012-04-23at35100pm](assets/screen_shot_2012-04-23at35100pm.png)

如果可以編輯標題，您可以按一下「鉛筆」以開啟 **資產屬性** 視窗。 此外，您可以選取日期和時間，以開啟或關閉資產。

編輯 [!UICONTROL 標題]，使用者可變更 **標題**， **說明**，並輸入 **開啟** 和 **關閉時間** 以開啟和關閉資產。

![screen_shot_2012-04-23at35241pm](assets/screen_shot_2012-04-23at35241pm.png)

以下是填入Title元件的範例：

![chlimage_1-164](assets/chlimage_1-392.png)

#### 新增資產編輯器動作 {#adding-asset-editor-actions}

您可以透過一系列預先定義的動作，決定使用者可對選取的數位資產執行哪些動作。

若要將動作新增至Asset Editor頁面：

1. 在要自訂的Asset Editor頁面中，按一下 **資產編輯器** 在sidekick。

![screen_shot_2012-04-23at35515pm](assets/screen_shot_2012-04-23at35515pm.png)

下列動作可供使用：

| 操作 | 描述 |
|---|---|
| [!UICONTROL 下载] | 可讓使用者將選取的資產下載至其電腦。 |
| [!UICONTROL 编辑器] | 可讓使用者編輯影像（互動式編輯） |
| [!UICONTROL Lightbox] | 將資產儲存至「燈箱」，您可在此對其執行其他動作。 在多個頁面中處理資產時，此功能會很實用。 |
| [!UICONTROL 鎖定] | 可讓使用者鎖定資產。 預設不會啟用此功能，需要啟用元件清單中的此功能。 |
| [!UICONTROL 引用] | 按一下此以在使用資產的頁面上顯示。 |
| [!UICONTROL 版本控制] | 可讓您建立和還原資產的版本。 |

1. 將適當的動作拖曳至 **動作** 區域。 它會建立一個選項，用來執行在頁面上拖曳的動作。

![chlimage_1-165](assets/chlimage_1-393.png)

## 使用Asset Editor頁面多重編輯資產 {#multi-editing-assets-with-the-asset-editor-page}

替換為 [!DNL Experience Manager Assets] 您可以一次變更多個資產。 選取資產後，您可以同時變更其：

* 标记
* 中繼資料

若要使用Asset Editor頁面多重編輯資產：

1. 開啟Geometrixx **新聞中心** 頁面：
   `https://localhost:4502/content/geometrixx/en/company/press.html`

1. 選取資產：

   * 在Windows上： `Ctrl + click` 每個資產。
   * 在Mac上： `Cmd + click` 每個資產。

   若要選取資產範圍：按一下第一個資產，然後 `Shift + click` 最後一個資產。

1. 按一下 **編輯中繼資料** 在 **動作** 欄位（頁面左側）。
1. Geometrixx **按下Center Asset Editor** 頁面會在新標籤中開啟。 資產的中繼資料顯示如下：

   * 標籤不會套用至所有資產，但只會套用至少數資產，會以斜體顯示。
   * 套用至所有資產的標籤會以一般字型顯示。
   * 標籤以外的中繼資料：只有在所有選定資產都相同的情況下，才會顯示欄位的值。

1. 按一下 **下載** 以下載包含資產原始轉譯的ZIP檔案。
1. 按一下旁邊的「編輯標籤」選項 **標籤** 欄位。

   * 標籤不適用於所有資產，但只有少數資產具有灰色背景。
   * 套用至所有資產的標籤都具有白色背景。

   您可以：

   * 按一下 `x` 以移除所有資產的標籤。
   * 按一下 `+` 將標籤新增至所有資產。
   * 按一下 **箭頭** 並選取標籤以將新標籤新增至所有資產。

   按一下 **確定** 將變更寫入表單。 旁的方塊 **標籤** 欄位會自動勾選。

1. 編輯說明欄位。 例如，將其設為：

   `This is a common description`

   編輯欄位時，其值會在提交表單時覆寫所選資產的現有值。

   附註：編輯欄位時，會自動勾選欄位旁邊的方塊。

1. 按一下 **更新中繼資料** 以提交表單並儲存所有資產的變更。

   注意：只會修改已核取的中繼資料。
