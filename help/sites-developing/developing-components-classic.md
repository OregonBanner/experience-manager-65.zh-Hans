---
title: 開發AEM元件（傳統UI）
seo-title: Developing AEM Components (Classic UI)
description: 傳統UI會使用ExtJS建立提供元件外觀的Widget。 HTL不是AEM的建議指令碼語言。
seo-description: The classic UI uses ExtJS to create widgets that provide the look-and-feel of the components. HTL is not the recommended scripting language for AEM.
uuid: ed53d7c6-5996-4892-81a4-4ac30df85f04
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: c68f724f-f9b3-4018-8d3a-1680c53d73f8
legacypath: /content/docs/en/aem/6-2/develop/components/components-classic
exl-id: 3f078139-73fd-4913-9d67-264fb2515f8a
source-git-commit: 43a30b5ba76ea470cc50a962d4f04b4a1508964d
workflow-type: tm+mt
source-wordcount: '2392'
ht-degree: 1%

---

# 開發AEM元件（傳統UI）{#developing-aem-components-classic-ui}

傳統UI會使用ExtJS建立提供元件外觀的Widget。 由於這些Widget的性質，元件與傳統UI的互動方式與 [觸控式UI](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>元件開發的許多方面對於傳統UI和觸控式UI都是通用的，因此 **您必須閱讀 [AEM元件 — 基本知識](/help/sites-developing/components-basics.md) 早於** 此頁面會說明傳統UI的詳細資訊。

>[!NOTE]
>
>雖然HTML範本語言(HTL)和JSP都可用於開發傳統UI的元件，此頁面說明了使用JSP進行開發。 這完全是因為在傳統UI中使用JSP的歷史記錄。
>
>HTL現在是AEM的建議指令碼語言。 另請參閱 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) 和 [開發AEM元件](/help/sites-developing/developing-components.md) 以比較方法。

## 结构 {#structure}

頁面上會說明元件的基本結構 [AEM元件 — 基本知識](/help/sites-developing/components-basics.md#structure)，會同時套用觸控式UI和傳統UI。 即使您不需要在新元件中使用觸控式UI的設定，在繼承現有元件時瞭解這些設定也會有所幫助。

## JSP指令碼 {#jsp-scripts}

JSP指令碼或Servlet可用於呈現元件。 根據Sling的請求處理規則，預設指令碼的名稱是：

`<*componentname*>.jsp`

## global.jsp {#global-jsp}

JSP指令碼檔案 `global.jsp` 用於提供對用於呈現元件的任何JSP指令碼檔案的特定物件的快速存取（即存取內容）。

因此 `global.jsp` 應包含在每個元件轉譯JSP指令碼中，其中一個或多個物件提供於 `global.jsp` 已使用。

預設的位置 `global.jsp` 為：

`/libs/foundation/global.jsp`

>[!NOTE]
>
>路徑 `/libs/wcm/global.jsp`CQ 5.3及舊版所使用的，現已淘汰。

### global.jsp、used API和Taglibs的功能 {#function-of-global-jsp-used-apis-and-taglibs}

以下列出預設提供的最重要物件 `global.jsp`：

摘要:

* `<cq:defineObjects />`

   * `slingRequest`  — 包裝的要求物件( `SlingHttpServletRequest`)。
   * `slingResponse`  — 包裝的回應物件( `SlingHttpServletResponse`)。
   * `resource` - Sling資源物件( `slingRequest.getResource();`)。
   * `resourceResolver` - Sling資源解析器物件( `slingRequest.getResoucreResolver();`)。
   * `currentNode`  — 請求的已解析JCR節點。
   * `log`  — 預設記錄器()。
   * `sling` - Sling指令碼協助程式。
   * `properties`  — 已定址資源的屬性( `resource.adaptTo(ValueMap.class);`)。
   * `pageProperties`  — 已定址資源的頁面屬性。
   * `pageManager`  — 用於存取AEM內容頁面的頁面管理員( `resourceResolver.adaptTo(PageManager.class);`)。
   * `component`  — 目前AEM元件的元件物件。
   * `designer`  — 用於擷取設計資訊的設計器物件( `resourceResolver.adaptTo(Designer.class);`)。
   * `currentDesign`  — 已定址資源的設計。
   * `currentStyle`  — 已定址資源的樣式。

### 存取內容 {#accessing-content}

存取AEM WCM中的內容有三種方法：

* 透過中引入的屬性物件 `global.jsp`：

   properties物件是ValueMap的例項(請參閱 [Sling API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ValueMap.html))並包含目前資源的所有屬性。

   範例： `String pageTitle = properties.get("jcr:title", "no title");` 用於頁面元件的轉譯指令碼。

   範例： `String paragraphTitle = properties.get("jcr:title", "no title");` 用於標準段落元件的轉譯指令碼。

* 透過 `currentPage` 在中引入的物件 `global.jsp`：

   此 `currentPage` 物件是頁面的例項(請參閱 [AEM API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.mhtml))。 Page類別提供一些存取內容的方法。

   示例: `String pageTitle = currentPage.getTitle();`

* Via `currentNode` 在中引入的物件 `global.jsp`：

   此 `currentNode` 物件是節點的執行個體(請參閱 [JCR API](https://jackrabbit.apache.org/api/2.16/org/apache/jackrabbit/standalone/cli/core/CurrentNode.html))。 節點屬性可透過以下方式存取： `getProperty()` 方法。

   示例: `String pageTitle = currentNode.getProperty("jcr:title");`

## JSP標籤庫 {#jsp-tag-libraries}

CQ和Sling標籤庫可讓您存取特定函式，以便在範本和元件的JSP指令碼中使用。

如需詳細資訊，請參閱檔案 [標籤庫](/help/sites-developing/taglib.md).

## 使用使用者端HTML程式庫 {#using-client-side-html-libraries}

現代網站非常依賴由複雜的JavaScript和CSS程式碼驅動的使用者端處理。 組織和最佳化此程式碼的伺服可能會是個複雜的問題。

為協助處理此問題，AEM提供 **使用者端資料庫資料夾**，可將使用者端程式碼儲存在存放庫中，將其組織成類別，並定義每個類別程式碼何時及如何提供給使用者端。 然後，使用者端程式庫系統會負責在最終網頁中產生正確的連結，以載入正確的程式碼。

檢視檔案 [使用使用者端HTML程式庫](/help/sites-developing/clientlibs.md) 以取得詳細資訊。

## 对话框 {#dialog}

您的元件需要對話方塊才能讓作者新增及設定內容。

另請參閱 [AEM元件 — 基本知識](/help/sites-developing/components-basics.md#dialogs) 以取得更多詳細資料。

## 設定編輯行為 {#configuring-the-edit-behavior}

您可以設定元件的編輯行為。 這包括元件可用的動作、就地編輯器的特性，以及與元件上事件相關的接聽程式等屬性。 此設定對觸控式與傳統UI而言都是通用的，不過會有某些特定差異。

此 [元件的編輯行為已設定](/help/sites-developing/components-basics.md#edit-behavior) 藉由新增 `cq:editConfig` 型別的節點 `cq:EditConfig` 元件節點下方(型別 `cq:Component`)，並新增特定屬性和子節點。

## 使用和擴充ExtJS Widget {#using-and-extending-extjs-widgets}

另請參閱 [使用和擴充ExtJS Widget](/help/sites-developing/widgets.md) 以取得更多詳細資料。

## 對ExtJS Widget使用xtype {#using-xtypes-for-extjs-widgets}

另請參閱 [使用xtypes](/help/sites-developing/xtypes.md) 以取得更多詳細資料。

## 開發新元件 {#developing-new-components}

本節說明如何建立您自己的元件，並將其新增至段落系統。

快速入門方法是複製現有元件，然後進行您想要的變更。

有關如何開發元件的範例詳細說明，請參閱 [擴充文字和影像元件 — 範例。](#extending-the-text-and-image-component-an-example)

### 開發新元件（調整現有元件） {#develop-a-new-component-adapt-existing-component}

若要根據現有元件為AEM開發新元件，您可以複製元件、為新元件建立JavaScript檔案，並將其儲存在AEM可存取的位置(另請參閱 [自訂元件和其他元素](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements))：

1. 使用CRXDE Lite，在中建立新的元件資料夾：

   / `apps/<myProject>/components/<myComponent>`

   像在libs中一樣重新建立節點結構，然後複製現有元件（例如Text元件）的定義。 例如，若要自訂文字元件副本：

   * 从 `/libs/foundation/components/text`
   * 到 `/apps/myProject/components/text`

1. 修改 `jcr:title` 以反映其新名稱。
1. 開啟新的元件資料夾，並進行您需要的變更。 此外，請刪除資料夾中任何無關的資訊。

   您可以進行下列變更：

   * 在對話方塊中新增欄位

      * `cq:dialog`  — 觸控式UI的對話方塊
      * `dialog`  — 傳統UI的對話方塊
   * 取代 `.jsp` 檔案（以新元件的名稱命名）
   * 或完全重工整個元件（若您需要）

   例如，如果您取得標準「文字」元件的副本，則可以在對話方塊中新增一個額外的欄位，然後更新 `.jsp` 以處理在那裡輸入的內容。

   >[!NOTE]
   >
   >的元件：
   >
   >* 觸控式UI使用 [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) 元件
   >* 傳統UI使用 [ExtJS Widget](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)


   >[!NOTE]
   >
   >為傳統UI定義的對話方塊將在觸控式UI中運作。
   >
   >為觸控式UI定義的對話方塊不會在傳統UI中運作。
   >
   >視您的執行個體和作者環境而定，您可能想要為元件定義這兩種型別的對話方塊。

1. 下列節點之一應存在且已正確初始化，新元件才能顯示：

   * `cq:dialog`  — 觸控式UI的對話方塊
   * `dialog`  — 傳統UI的對話方塊
   * `cq:editConfig`  — 元件在編輯環境中的行為（例如拖放）
   * `design_dialog`  — 設計模式對話方塊（僅限傳統UI）

1. 透過下列任一項在段落系統中啟動新元件：

   * 使用CRXDE Lite來新增值 `<path-to-component>` (例如， `/apps/geometrixx/components/myComponent`)至節點的屬性元件 `/etc/designs/geometrixx/jcr:content/contentpage/par`
   * 依照中的指示操作 [新增元件至段落系統](#adding-a-new-component-to-the-paragraph-system-design-mode)

1. 在AEM WCM中，開啟網站中的頁面，並插入您剛才建立之型別的新段落，以確保元件正常運作。

>[!NOTE]
>
>若要檢視頁面載入的計時統計資料，您可以使用Ctrl-Shift-U — 搭配 `?debugClientLibs=true` 在URL中設定。

### 新增元件至段落系統（設計模式） {#adding-a-new-component-to-the-paragraph-system-design-mode}

開發元件後，您可以將其新增至段落系統，讓作者在編輯頁面時能夠選取和使用元件。

1. 例如，存取編寫環境中使用段落系統的頁面 `<contentPath>/Test.html`.
1. 透過以下任一方式切換到設計模式：

   * 新增 `?wcmmode=design` 移至URL結尾並再次存取，例如：

      `<contextPath>/ Test.html?wcmmode=design`

   * 按一下Sidekick中的「設計」

   您現在處於設計模式，可以編輯段落系統。

1. 按一下「編輯」。

   此時會顯示屬於段落系統的元件清單。 也會列出您的新元件。

   可以啟動（或停用）元件，以決定在編輯頁面時提供給作者的元件。

1. 啟動元件，然後返回正常編輯模式以確認元件可供使用。

### 擴充文字和影像元件 — 範例 {#extending-the-text-and-image-component-an-example}

本節提供如何使用可設定的影像放置功能來擴充廣泛使用的文字和影像標準元件的範例。

文字和影像元件的擴充功能可讓編輯器使用元件的所有現有功能，另外還有一個額外選項可指定影像的位置：

* 在文字的左側（目前行為與新預設值）
* 以及在右側

延伸此元件後，您可以透過元件的對話方塊來設定影像位置。

本練習將說明下列技巧：

* 複製現有元件節點並修改其中繼資料
* 修改元件的對話方塊，包括從父對話方塊繼承Widget
* 修改元件的指令碼以實作新功能

>[!NOTE]
>
>此範例目標是傳統UI。

>[!NOTE]
>
>此範例是根據AEM不再隨附的Geometrixx範例內容，已由We.Retail取代。 檢視檔案 [We.Retail參考實作](/help/sites-developing/we-retail.md#we-retail-geometrixx) 瞭解如何下載和安裝Geometrixx。

#### 擴充現有的文字提示元件 {#extending-the-existing-textimage-component}

若要建立新元件，我們使用標準文字元件作為基礎並加以修改。 我們會將新元件儲存在GeometrixxAEM WCM範例應用程式中。

1. 從以下位置複製標準文字元素： `/libs/foundation/components/textimage` 放入Geometrixx元件資料夾中， `/apps/geometrixx/components`，使用textimage作為目標節點名稱。 （瀏覽至元件、以滑鼠右鍵按一下並選取「複製」，然後瀏覽至目標目錄，以複製元件。）

   ![chlimage_1-59](assets/chlimage_1-59a.png)

1. 若要讓此範例維持簡單，請導覽至您複製的元件，並刪除新文位元組點的所有子節點（以下子節點除外）：

   * 對話方塊定義： `textimage/dialog`
   * 元件指令碼： `textimage/textimage.jsp`
   * 編輯設定節點（允許拖放資產）： `textimage/cq:editConfig`

   >[!NOTE]
   >
   >對話方塊定義取決於UI：
   >
   >* 觸控式UI： `textimage/cq:dialog`
   >* 经典 UI: `textimage/dialog`


1. 編輯元件中繼資料：

   * 元件名稱

      * 設定 `jcr:description` 至 `Text Image Component (Extended)`
      * 設定 `jcr:title` 至 `Text Image (Extended)`
   * 群組，其中的元件列在Sidekick中（保持原樣）

      * 離開 `componentGroup` 設定為 `General`
   * 新元件的父元件（標準文字元件）

      * 設定 `sling:resourceSuperType` 至 `foundation/components/textimage`

   在此步驟後，元件節點看起來像這樣：

   ![chlimage_1-60](assets/chlimage_1-60a.png)

1. 變更 `sling:resourceType` 影像的編輯設定節點的屬性(屬性： `textimage/cq:editConfig/cq:dropTargets/image/parameters/sling:resourceType`)至 `geometrixx/components/textimage.`

   如此一來，當影像放到頁面上的元件時， `sling:resourceType` 延伸文字功能元件的屬性已設定為： `geometrixx/components/textimage.`

1. 修改元件的對話方塊以包含新選項。 新元件會繼承對話方塊中與原始元件相同的零件。 我們所做的唯一新增是擴充 **進階** 標籤，新增 **影像位置** 下拉式清單，含選項 **左側** 和 **右**：

   * 離開 `textimage/dialog`屬性未變更。

   注意操作方式 `textimage/dialog/items` 有4個子節點，從tab1到tab4，代表「文字」對話方塊的四個標籤。

   * 前兩個標籤（tab1和tab2）：

      * 將xtype變更為cqinclude （繼承自標準元件）。
      * 使用值新增路徑屬性 `/libs/foundation/components/textimage/dialog/items/tab1.infinity.json`和 `/libs/foundation/components/textimage/dialog/items/tab2.infinity.json`（分別）。
      * 移除所有其他屬性或子節點。
   * 對於tab3：

      * 保留屬性和子節點而不變更
      * 新增欄位定義至 `tab3/items`，型別的節點位置 `cq:Widget`
      * 為新的設定以下屬性（字串型別） `tab3/items/position`節點：

         * `name`： `./imagePosition`
         * `xtype`: `selection`
         * `fieldLabel`: `Image Position`
         * `type`: `select`
      * 新增子節點 `position/options` 型別 `cq:WidgetCollection` 代表兩個影像放置選項，並在其下建立兩個節點，o1和o2型別 `nt:unstructured`.
      * 針對節點 `position/options/o1` 設定屬性： `text` 至 `Left` 和 `value` 至 `left.`
      * 針對節點 `position/options/o2` 設定屬性： `text` 至 `Right` 和 `value` 至 `right`.
   * 刪除Tab4。

   影像位置會持續保留在內容中，做為 `imagePosition`節點的屬性，表示 `textimage` 段落。 執行這些步驟後，「元件」對話方塊看起來像這樣：

   ![chlimage_1-61](assets/chlimage_1-61a.png)

1. 擴充元件指令碼， `textimage.jsp`，額外處理新引數：

   ```xml
   Image image = new Image(resource, "image");
   
   if (image.hasContent() || WCMMode.fromRequest(request) == WCMMode.EDIT) {
        image.loadStyleData(currentStyle);
   ```

   我們將取代強調的程式碼片段 *%>&lt;div class=&quot;image&quot;>&lt;%* 新程式碼產生此標籤的自訂樣式。

   ```xml
   // todo: add new CSS class for the 'right image' instead of using
   // the style attribute
   String style="";
        if (properties.get("imagePosition", "left").equals("right")) {
             style = "style=\"float:right\"";
        }
        %><div <%= style %> class="image"><%
   ```

1. 將元件儲存至存放庫。 元件已準備好進行測試。

#### 檢查新元件 {#checking-the-new-component}

開發元件後，您可以將其新增至段落系統，讓作者在編輯頁面時選取並使用元件。 這些步驟可讓您測試元件。

1. 以Geometrixx（例如英文/公司）開啟頁面。
1. 按一下Sidekick中的「設計」切換至設計模式。
1. 按一下頁面中間段落系統上的「編輯」，編輯段落系統設計。 隨即顯示可放置在段落系統中的元件清單，清單中應包含新開發的元件Text Image (Extended) 。 選取它並按一下確定，為段落系統啟動它。
1. 切換回編輯模式。
1. 將文字影像（延伸）段落新增至段落系統，以範例內容初始化文字和影像。 保存更改。
1. 開啟文字和影像段落的對話方塊，並將「進階」標籤上的「影像位置」變更為「右側」，然後按一下「確定」以儲存變更。
1. 段落會以右側的影像呈現。
1. 元件現在已可供使用。

元件會將其內容儲存在公司頁面上的段落中。

### 停用影像元件的上傳功能 {#disable-upload-capability-of-the-image-component}

若要停用此功能，我們會使用標準影像元件作為基礎並加以修改。 我們會將新元件儲存在Geometrixx範例應用程式中。

1. 複製標準影像元件來源 `/libs/foundation/components/image` 放入Geometrixx元件資料夾中， `/apps/geometrixx/components`，使用影像作為目標節點名稱。

   ![chlimage_1-62](assets/chlimage_1-62a.png)

1. 編輯元件中繼資料：

   * 設定 **jcr：title** 至 `Image (Extended)`

1. 导航到 `/apps/geometrixx/components/image/dialog/items/image`。
1. 添加新属性:

   * **名称**: `allowUpload`
   * **类型**: `String`
   * **值**: `false`

   ![chlimage_1-63](assets/chlimage_1-63a.png)

1. 按一下 **全部儲存**. 元件已準備好進行測試。
1. 以Geometrixx（例如英文/公司）開啟頁面。
1. 切換到設計模式並啟動影像（延伸）。
1. 切換回編輯模式，並將其新增至段落系統。 在下一張圖片中，您可以看到原始影像元件與您剛剛建立的影像元件之間的差異。

   原始影像元件：

   ![chlimage_1-64](assets/chlimage_1-64a.png)

   您的新影像元件：

   ![chlimage_1-65](assets/chlimage_1-65a.png)

1. 元件現在已可供使用。
