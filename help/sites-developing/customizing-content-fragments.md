---
title: 自定义和扩展内容片段
seo-title: Customizing and Extending Content Fragments
description: 內容片段可擴充標準資產。
seo-description: A content fragment extends a standard asset.
topic-tags: extending-aem
content-type: reference
docset: aem65
exl-id: 08c88e70-4df9-4627-8a66-1fabe3aee50b
source-git-commit: 9ad531738ac5e3c9d888f685b47c8b322712a89e
workflow-type: tm+mt
source-wordcount: '2778'
ht-degree: 2%

---


# 自定义和扩展内容片段{#customizing-and-extending-content-fragments}

內容片段可擴充標準資產；請參閱：

* [建立和管理內容片段](/help/assets/content-fragments/content-fragments.md) 和 [使用內容片段編寫頁面](/help/sites-authoring/content-fragments.md) 以取得有關內容片段的進一步資訊。

* [管理資產](/help/assets/manage-assets.md) 和 [自訂和擴充資產](/help/assets/extending-assets.md) 以取得標準資產的詳細資訊。

## 架构 {#architecture}

基本 [組成部分](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 的內容片段包括：

* A *內容片段，*
* 由一或多個 *內容元素* s，
* 而且可以有一或多個 *內容變數* s.

視片段型別而定，也會使用模型或範本：

>[!CAUTION]
>
>[內容片段模型](/help/assets/content-fragments/content-fragments-models.md) 建議用於建立所有新片段。
>
>內容片段模型用於WKND中的所有範例。

>[!NOTE]
>
>在AEM 6.3之前，內容片段是根據範本而非模型建立的。
>
>內容片段範本現已棄用。 它們仍可用於建立片段，但建議改用內容片段模型。 片段範本不會新增任何新功能，而會在未來版本中移除。

* 内容片段模型:

   * 用於定義儲存結構化內容的內容片段。
   * 內容片段模型會在建立內容片段時定義其結構。
   * 片段會參考模型；因此對模型的變更可能會/將會影響任何相依片段。
   * 模型是資料型別的建置模型。
   * 新增新變數的函式等必須相應地更新片段。

   >[!CAUTION]
   >
   >對現有內容片段模式所做的任何變更都可能影響相依片段，都可能導致這些片段中出現孤立屬性。

* 內容片段範本：

   * 用於定義簡單內容片段。
   * 範本會在建立內容片段時定義內容片段的（基本、僅限文字）結構。
   * 範本會在建立時複製到片段，因此對範本的進一步變更將不會反映在現有片段中。
   * 新增新變數的函式等必須相應地更新片段。
   * [內容片段範本](/help/sites-developing/content-fragment-templates.md) 以與AEM生態系統內其他範本機制（例如頁面範本等）不同的方式運作。 因此，應分別予以考慮。
   * 根據範本時，內容的MIME型別是根據實際內容管理的；這表示每個元素和變數可以有不同的MIME型別。

### 與Assets整合 {#integration-with-assets}

內容片段管理(CFM)是AEM Assets的一部分，如下所示：

* 內容片段為資產。
* 他們使用現有的Assets功能。
* 它們與Assets （管理主控台等）完全整合。

#### 將結構化內容片段對應至資產 {#mapping-structured-content-fragments-to-assets}

![片段至資產結構化](assets/fragment-to-assets-structured.png)

具有結構化內容（即根據內容片段模型）的內容片段對應至單一資產：

* 所有內容都儲存在 `jcr:content/data` 資產節點：

   * 元素資料儲存在主子節點下：
      `jcr:content/data/master`

   * 變數會儲存在具有變數名稱的子節點下：例如 `jcr:content/data/myvariation`

   * 每個元素的資料都會以元素名稱的屬性儲存在個別子節點中，例如element的內容 `text` 儲存為屬性 `text` 於 `jcr:content/data/master`

* 中繼資料和相關內容儲存在下方 `jcr:content/metadata`
除了標題和說明之外，這些不會視為傳統中繼資料並儲存在 
`jcr:content`

#### 將簡單內容片段對應至資產 {#mapping-simple-content-fragments-to-assets}

![chlimage_1-90](assets/chlimage_1-90.png)

簡單內容片段（根據範本）對應至由主要資產和（選用）子資產組成的複合：

* 片段的所有非內容資訊（例如標題、說明、中繼資料、結構）都只在主要資產上管理。
* 片段第一個元素的內容對應至主要資產的原始轉譯。

   * 第一個元素的變數（如果有的話）會對應至主要資產的其他轉譯。

* 其他元素（如果存在）會對應至主要資產的子資產。

   * 這些額外元素的主要內容對應至個別子資產的原始轉譯。
   * 任何其他元素的其他變數（如果適用）對應至個別子資產的其他轉譯。

#### 資產位置 {#asset-location}

與標準資產一樣，內容片段位於下方：

`/content/dam`

#### 資產許可權 {#asset-permissions}

如需詳細資訊，請參閱 [內容片段 — 刪除考量事項](/help/assets/content-fragments/content-fragments-delete.md).

#### 功能整合 {#feature-integration}

* 內容片段管理(CFM)功能以Assets核心為基礎，但應儘可能獨立於此。
* CFM針對卡片/欄/清單檢視中的專案提供自己的實作；這些外掛程式會插入現有的Assets內容演算實作中。
* 已擴充多個Assets元件，以符合內容片段。

### 在頁面中使用內容片段 {#using-content-fragments-in-pages}

>[!CAUTION]
>
>此 [內容片段核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=zh-Hans) 現在建議使用。 另請參閱 [開發核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html) 以取得更多詳細資料。

內容片段可以從AEM頁面參照，就像任何其他資產型別一樣。 AEM提供 [**內容片段** 核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=zh-Hans) - a [可讓您在頁面上包含內容片段的元件](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page). 您也可以擴充 **內容片段** 核心元件。

* 元件使用 `fragmentPath` 屬性以參考實際內容片段。 此 `fragmentPath` 屬性的處理方式與其他資產型別的類似屬性相同；例如，當內容片段移動到另一個位置時。

* 元件可讓您選取要顯示的變數。
* 此外，可以選取段落範圍來限制輸出；例如，這可用於多欄輸出。
* 元件允許 [中間內容](/help/sites-developing/components-content-fragments.md#in-between-content)：

   * 元件可讓您在此處放置其他資產（影像等） 位於參考片段的段落之間。
   * 對於中間內容，您需要：

      * 請注意不穩定參考的可能性；中間內容（製作頁面時新增）與其旁邊段落沒有固定的關係，在中間內容位置前插入新段落（在內容片段編輯器中）可能會失去相對位置
      * 請考慮其他引數（例如變數和段落篩選器）以避免搜尋結果中出現誤判

>[!NOTE]
>
>**内容片段模型:**
>
>使用以頁面上的內容片段模型為基礎的內容片段時，會參考模型。 這表示如果您在發佈頁面時尚未發佈模型，系統會標籤此模型，並將模型新增至要與頁面一起發佈的資源。
>
>**內容片段範本：**
>
>使用已根據頁面上的內容片段範本的內容片段時，沒有參考在建立片段時複製了範本。

#### 使用OSGi主控台進行設定 {#configuration-using-osgi-console}

例如，內容片段的後端實作負責讓頁面上使用的片段例項可供搜尋，或負責管理混合媒體內容。 此實作需要知道哪些元件用於轉譯片段，以及轉譯如何引數化。

此專案的引數可在以下位置設定： [網頁主控台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)，適用於OSGi套件組合 **內容片段元件設定**.

* **資源型別**
清單 
`sling:resourceTypes` 可定義用於轉譯內容片段以及背景處理應套用到的位置的元件。

* **參考屬性**
屬性清單可設定為指定針對個別元件儲存片段參照的位置。

>[!NOTE]
>
>屬性和元件型別之間沒有直接對應。
>
>AEM只會採用可以在段落上找到的第一個屬性。 因此，您應謹慎選擇屬性。

![screenshot_2019-03-18at100941](assets/screenshot_2019-03-18at100941.png)

您仍然必須遵循一些准則，以確保您的元件與內容片段背景處理相容：

* 定義要轉譯之元素之屬性的名稱必須是 `element` 或 `elementNames`.

* 定義要轉譯之變數的屬性名稱必須是 `variation` 或 `variationName`.

* 如果支援多個元素的輸出(透過 `elementNames` 指定多個元素)，實際顯示模式由屬性定義 `displayMode`：

   * 如果值為 `singleText` （而且僅設定一個元素），則元素會呈現為具有中間內容、版面配置支援等的文字。 這是僅呈現一個元素的片段的預設。
   * 否則，會使用更簡單的方法（可以稱為「表單檢視」），其中不支援中間內容，而片段內容會依「原樣」呈現。

* 如果片段呈現給 `displayMode` == `singleText` （隱含或明確）下列額外屬性會發揮作用：

   * `paragraphScope` 定義是否應呈現所有段落，或僅呈現某個範圍的段落(值： `all` 與 `range`)

   * 如果 `paragraphScope` == `range` 然後屬性 `paragraphRange` 定義要呈現的段落範圍

### 與其他架構整合 {#integration-with-other-frameworks}

內容片段可以與：

* **翻譯**

   內容片段已完全與整合 [AEM翻譯工作流程](/help/sites-administering/tc-manage.md). 在架構層級，這表示：

   * 內容片段的個別翻譯實際上是個別的片段；例如：

      * 它們位於不同的語言根下：

         `/content/dam/<path>/en/<to>/<fragment>`

         與

         `/content/dam/<path>/de/<to>/<fragment>`

      * 但它們共用語言根目錄下的完全相同的相對路徑：

         `/content/dam/<path>/en/<to>/<fragment>`

         與

         `/content/dam/<path>/de/<to>/<fragment>`
   * 除了規則型路徑以外，內容片段的不同語言版本之間沒有進一步的連線；這些版本會作為兩個獨立的片段處理，雖然UI提供了在語言變體之間導覽的方法。
   >[!NOTE]
   >
   >AEM翻譯工作流程適用於 `/content`：
   >
   >* 由於內容片段模型存放在 `/conf`，這些不會包含在這類翻譯中。 您可以 [國際化UI字串](/help/sites-developing/i18n-dev.md).
   >
   >* 系統會複製範本以建立片段，因此這是隱含的。


* **元数据架构**

   * 內容片段（重新）使用 [中繼資料結構](/help/assets/metadata-schemas.md)，可使用標準資產定義。
   * CFM提供專屬的特定結構描述：

      `/libs/dam/content/schemaeditors/forms/contentfragment`

      如有需要，可加以擴充。

   * 個別結構表單已與片段編輯器整合。

## 內容片段管理API — 伺服器端 {#the-content-fragment-management-api-server-side}

您可以使用伺服器端API來存取您的內容片段；請參閱：

[com.adobe.cq.dam.cfm](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/package-summary.html)

>[!CAUTION]
>
>強烈建議使用伺服器端API，而非直接存取內容結構。

### 重要介面 {#key-interfaces}

下列三個介面可作為入口點：

* **片段範本** ([片段範本](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html))

   使用 `FragmentTemplate.createFragment()` 用於建立新片段。

   ```
   Resource templateOrModelRsc = resourceResolver.getResource("...");
   FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
   ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
   ```

   此介面代表：

   * 要從中建立內容片段的內容片段模型或內容片段範本，
   * 以及（建立後）該片段的結構資訊

   此資訊可包括：

   * 存取基本資料（標題、說明）
   * 存取片段元素的範本/模型：

      * 清單元素範本
      * 取得指定元素的結構資訊
      * 存取元素範本(請參閱 `ElementTemplate`)
   * 存取片段變數的範本：

      * 清單變數範本
      * 取得指定變數的結構資訊
      * 存取變數範本(請參閱 `VariationTemplate`)
   * 取得初始關聯內容

   代表重要資訊的介面：

   * `ElementTemplate`

      * 取得基本資料（名稱、標題）
      * 取得初始元素內容
   * `VariationTemplate`

      * 取得基本資料（名稱、標題、說明）






* **內容片段** ([內容片段](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

   此介面可讓您以抽象方式處理內容片段。

   >[!CAUTION]
   >
   >強烈建議透過此介面存取片段。 應避免直接變更內容結構。

   介面可讓您執行下列動作：

   * 管理基本資料（例如取得名稱、取得/設定標題/說明）
   * 存取中繼資料
   * 存取元素：

      * 清單元素
      * 依名稱取得元素
      * 建立新元素(請參閱 [注意事項](#caveats))

      * 存取元素資料(請參閱 `ContentElement`)
   * 為片段定義的清單變數
   * 建立全域的新變數
   * 管理關聯內容：

      * 清單集合
      * 新增集合
      * 移除集合
   * 存取片段的模型或範本

   代表片段主要元素的介面包括：

   * **內容元素** ([內容元素](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * 取得基本資料（名稱、標題、說明）
      * 取得/設定內容
      * 存取元素的變數：

         * 清單變數
         * 依名稱取得變數
         * 建立新的變數(請參閱 [注意事項](#caveats))
         * 移除變數(請參閱 [注意事項](#caveats))
         * 存取變數資料(請參閱 `ContentVariation`)
      * 解決變異的捷徑（如果指定的變異不適用於某個元素，則套用一些其他實作特有的遞補邏輯）
   * **內容變數** ([ContentVariation](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * 取得基本資料（名稱、標題、說明）
      * 取得/設定內容
      * 根據上次修改資訊的簡單同步處理

   所有三個介面( `ContentFragment`， `ContentElement`， `ContentVariation`)擴充 `Versionable` 介面，新增內容片段所需的版本設定功能：

   * 建立元素的新版本
   * 列出元素的版本
   * 取得版本化元素的特定版本內容







### 調整 — 使用adaptTo() {#adapting-using-adaptto}

可調整以下內容：

* `ContentFragment` 可調整為：

   * `Resource`  — 基礎Sling資源；請注意，更新基礎 `Resource` 直接，需要重建 `ContentFragment` 物件。

   * `Asset` - DAM `Asset` 代表內容片段的抽象；請注意，更新 `Asset` 直接，需要重建 `ContentFragment` 物件。

* `ContentElement` 可調整為：

   * `ElementTemplate`  — 用於存取元素的結構資訊。

* `FragmentTemplate` 可調整為：

   * `Resource` - `Resource` 決定參照的模型或複製的原始範本；

      * 透過進行的變更 `Resource` 不會自動反映在 `FragmentTemplate`.

* `Resource` 可調整為：

   * `ContentFragment`
   * `FragmentTemplate`

### 注意事项 {#caveats}

請注意：

* 實作API是為了提供UI支援的功能。
* 整個API的設計目的是 **not** 自動保留變更（除非API JavaDoc另有說明）。 因此，您必須一律認可個別要求的資源解析器（或您實際使用的解析器）。
* 可能需要額外努力的任務：

   * 建立/移除新元素不會更新簡單片段的資料結構（根據片段範本）。
   * 建立新變數來源 `ContentElement` 不會更新資料結構(但會從下列位置建立全域資料結構： `ContentFragment` 會)。

   * 移除現有變數將不會更新資料結構。

## 內容片段管理API — 使用者端 {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>對於AEM 6.5，使用者端API是內部的。

### 附加信息 {#additional-information}

请参阅以下内容：

* `filter.xml`

   此 `filter.xml` 用於內容片段管理的設定使其不會與資產核心內容套件重疊。

## 編輯工作階段 {#edit-sessions}

當使用者在其中一個編輯器頁面中開啟內容片段時，會啟動編輯工作階段。 當使用者透過選擇以下任一專案離開編輯器時，編輯工作階段即完成 **儲存** 或 **取消**.

### 要求 {#requirements}

控制編輯工作階段的需求如下：

* 編輯內容片段可跨越多個檢視(=HTML頁面)，這應該是原子的。
* 編輯內容也應該 *異動*；在編輯工作階段結束時，必須認可（儲存）變更或復原變更（取消）。
* 邊緣案例應正確處理，包括使用者手動輸入URL或使用全域導覽離開頁面的情況。
* 應提供定期自動儲存（每x分鐘）以防止資料遺失。
* 如果兩個使用者同時編輯內容片段，他們不應覆寫彼此的變更。

#### 进程 {#processes}

相關程式包括：

* 啟動工作階段

   * 內容片段的新版本已建立。
   * 自動儲存已啟動。
   * Cookie已設定；這些會定義目前編輯的片段，且有編輯工作階段開啟。

* 完成作業階段

   * 自動儲存已停止。
   * 提交時：

      * 上次修改的資訊會更新。
      * Cookie已移除。
   * 復原時：

      * 還原在編輯工作階段啟動時建立的內容片段版本。
      * Cookie已移除。


* 编辑

   * 所有變更（包括自動儲存）都是在作用中內容片段上完成的，而不是在分隔的保護區中。
   * 因此，這些變更會立即反映在參考個別內容片段的AEM頁面上

#### 操作 {#actions}

可能的動作包括：

* 輸入頁面

   * 檢查編輯工作階段是否已存在；透過檢查個別Cookie。

      * 如果存在，請確認已針對目前編輯的內容片段啟動編輯工作階段

         * 如果目前片段，請重新建立工作階段。
         * 如果沒有，請嘗試取消編輯先前編輯的內容片段並移除Cookie （之後不會有編輯工作階段）。
      * 如果不存在編輯工作階段，請等待使用者進行第一次變更（請參閱下文）。
   * 檢查頁面上是否已參考內容片段，如果有的話，則顯示適當的資訊。



* 內容變更

   * 每當使用者變更內容且沒有編輯工作階段出現時，就會建立新的編輯工作階段(請參閱 [啟動工作階段](#processes))。

* 離開頁面

   * 如果存在編輯工作階段且變更尚未持續存在，則會顯示強制回應確認對話方塊，以通知使用者可能遺失的內容，並允許他們停留在頁面上。

## 示例 {#examples}

### 範例：存取現有的內容片段 {#example-accessing-an-existing-content-fragment}

若要達到此目的，您可以將代表API的資源調整為：

`com.adobe.cq.dam.cfm.ContentFragment`

例如：

```java
// first, get the resource
Resource fragmentResource = resourceResolver.getResource("/content/dam/fragments/my-fragment");
// then adapt it
if (fragmentResource != null) {
    ContentFragment fragment = fragmentResource.adaptTo(ContentFragment.class);
    // the resource is now accessible through the API
}
```

### 範例：建立新內容片段 {#example-creating-a-new-content-fragment}

若要以程式設計方式建立新的內容片段，您需要使用：

`com.adobe.cq.dam.cfm.ContentFragmentManager#create`

例如：

```java
Resource templateOrModelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### 範例：指定自動儲存間隔 {#example-specifying-the-auto-save-interval}

可以使用設定管理員(ConfMgr)定義自動儲存間隔（以秒為單位測量）：

* 節點： `<*conf-root*>/settings/dam/cfm/jcr:content`
* 属性名称: `autoSaveInterval`
* 类型: `Long`

* 預設： `600` （10分鐘）；此值的定義日期為 `/libs/settings/dam/cfm/jcr:content`

如果您想要將自動儲存間隔設為5分鐘，您必須在節點上定義屬性；例如：

* 節點： `/conf/global/settings/dam/cfm/jcr:content`
* 属性名称: `autoSaveInterval`

* 类型: `Long`

* 值： `300` （5分鐘等於300秒）

## 內容片段範本 {#content-fragment-templates}

另請參閱 [內容片段範本](/help/sites-developing/content-fragment-templates.md) 以取得完整資訊。

## 用於頁面編寫的元件 {#components-for-page-authoring}

如需詳細資訊，請參閱

* [核心元件 — 內容片段元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=zh-Hans) （建議）
* [內容片段元件 — 頁面製作所需元件](/help/sites-developing/components-content-fragments.md#components-for-page-authoring)
