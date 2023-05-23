---
title: 建立表單入口網站頁面
seo-title: Creating a forms portal page
description: Forms入口網站為網頁開發人員配備元件，以便在使用Adobe Experience Manager (AEM)編寫的網站上建立和自訂表單入口網站。
seo-description: Forms Portal equips Web Developers with components to create and customize a forms portal on websites authored using Adobe Experience Manager (AEM).
uuid: a5017de5-616c-4ce4-81aa-f28c741f8e8f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 8fff78cb-9ef9-426e-8b30-d70b4f26887f
docset: aem65
feature: Forms Portal
exl-id: 22d7c24e-7a77-4324-afdf-74c1fbf15773
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1641'
ht-degree: 1%

---

# 建立表單入口網站頁面{#creating-a-forms-portal-page}

Forms入口網站元件可讓Web開發人員在使用Adobe Experience Manager (AEM)編寫的網站上建立和自訂表單入口網站。 如需表單入口網站的快速總覽，請參閱 [在入口網站上發佈表單的簡介](../../forms/using/introduction-publishing-forms.md).

## 前提条件 {#prerequisites}

Forms入口網站元件預設無法使用。 請確定已啟用下清單單入口網站元件類別，如所述 [啟用表單入口網站元件](/help/forms/using/enabling-forms-portal-components.md).

**檔案服務** 包含搜尋與清單製作者、連結，以及草稿與提交元件。

**檔案服務述詞** 包括日期述詞、全文檢索述詞、屬性述詞和標籤述詞元件。 這些元件可用來設定「搜尋和清單程式」元件中的搜尋。

在AEM網站頁面上啟用這些元件類別後，您就可以在元件瀏覽器中使用這些元件類別。

![元件瀏覽器中的AEM Forms入口網站元件](assets/component-categories.png)

Forms入口網站元件類別

## 搜尋和清單產生器元件 {#search-amp-lister-component}

Document Services元件類別底下提供的Search &amp; Lister元件可用於列出頁面上的表單，以及在列出的表單上實施搜尋。 元件包含兩個窗格：

* 列出表單的清單窗格。
* 新增搜尋功能的搜尋窗格。

您可以將Search &amp; Lister元件從元件瀏覽器中的Document Services元件類別拖放到頁面上。 新增元件後，其外觀會類似於以下內容。

![頁面中的Search &amp; Lister元件](assets/fp-grid-viw.png)

使用格線版面配置的頁面中的「搜尋和清單程式」元件

### 清單窗格 {#list-pane}

「清單」窗格是列出表單的區域。 Search &amp; Lister元件提供各種組態選項，可用來控制List窗格中表單的顯示。

若要設定「清單」窗格，請點選「搜尋並製表器」元件，然後點選 ![settings_icon](assets/settings_icon.png). 此 **[!UICONTROL 編輯元件]** 對話方塊開啟。

![編輯模式下的清單窗格](assets/edit-list.png)

編輯模式下的清單窗格

此 **編輯** 對話方塊包含數個提供設定選項的標籤，如下表所述。 點選 **確定** 以儲存設定（完成時）。

<table>
 <tbody>
  <tr>
   <th>制表符</th>
   <th>配置</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>资源文件夹</strong></code></td>
   <td>添加项目</td>
   <td>設定使用AEM Forms UI上傳資產的資料夾。 依預設，它會列出所有上傳的資產。 如需AEM Forms UI的詳細資訊，請參閱 <a href="../../forms/using/introduction-managing-forms.md" target="_blank">管理表單簡介</a>.</td>
  </tr>
  <tr>
   <td><p><span class="uicontrol"><strong>显示器</strong></code></p> </td>
   <td>标题文本</td>
   <td>搜尋和清單元件的標題。 預設標題為 <strong>Forms入口網站。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>版面配置範本</td>
   <td>資產的配置。 </td>
  </tr>
  <tr>
   <td> </td>
   <td>停用進階搜尋</td>
   <td>啟用時，會隱藏進階搜尋圖示。</td>
  </tr>
  <tr>
   <td> </td>
   <td>停用文字搜尋</td>
   <td>啟用時，會隱藏全文檢索搜尋列。</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>结果</strong></code></td>
   <td>每頁結果數</td>
   <td>設定您要在頁面上顯示的表單數目上限。</td>
  </tr>
  <tr>
   <td> </td>
   <td>结果文本</td>
   <td><p>設定結果文字（例如，601的1-12） <strong>結果</strong>)。 預設值為 <strong>結果</strong>.</p> <p>例如，如果您指定 <strong>Forms </strong>在此欄位中，共有601個表單，結果文字會變更為601個表單中的1-12個 <strong>Forms。</strong></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>页面文本</td>
   <td><p>設定頁面文字(例如， <strong>頁面 </strong>1/51)。 預設值為 <strong>頁面</strong>.</p> <p>例如，如果您指定 <strong>申請表 </strong>在此欄位中有51頁，頁面文字會變更為 <strong>申請表 </strong>1/51。</p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Of 文本</td>
   <td><p>取代單字 <strong>之</strong> 具有指定文字（第1頁） <strong>之 </strong>51)。 預設值為 <strong>之</strong>.</p> <p>例如，如果您指定 <strong>/ </strong>在此欄位中，文字會變更為第1頁 <strong>/ </strong>51.</p> </td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>表單連結</strong></code></td>
   <td>呈现类型</td>
   <td>根據指定的轉譯器型別控制表單清單。 可用的選項有PDF和HTML。 例如，如果您選取「僅HTML」作為轉譯器型別，則會篩選掉PDF forms。</td>
  </tr>
  <tr>
   <td> </td>
   <td>HTML設定檔</td>
   <td>設定用於轉譯的HTML設定檔。 下拉式清單中會列出所有可用的設定檔。</td>
  </tr>
  <tr>
   <td> </td>
   <td>提交URL</td>
   <td><p>設定表單資料提交位置的servlet。</p> <p><strong>注意：</strong> <em>表單的提交URL可在數個位置指定，其優先順序如下：</em></p>
    <ol>
     <li><em>表單中內嵌的提交URL （在提交按鈕中）具有最高優先順序。</em></li>
     <li><em>AEM Forms UI中提到的提交URL具有第二高的優先順序。</em></li>
     <li><em>Forms Portal中提到的提交URL優先順序最低。</em></li>
    </ol> </td>
  </tr>
  <tr>
   <td> </td>
   <td>HTML演算動作工具提示</td>
   <td>設定工具提示的文字，當游標停留在上方時，會顯示工具提示 <img height="16" src="assets/aem6forms_panel-html.png" width="13" /> (HTML5圖示)。</td>
  </tr>
  <tr>
   <td> </td>
   <td>PDF演算動作工具提示</td>
   <td>設定工具提示的文字，當游標停留在上方時，會顯示工具提示 <img height="16" src="assets/aem6forms_panel-pdf.png" width="14" /> (PDF圖示)。</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>样式</strong></code></td>
   <td>樣式型別</td>
   <td>可讓您指定 <strong>無樣式，預設樣式</strong>，或 <strong>自訂樣式 </strong>以列出表格。</td>
  </tr>
  <tr>
   <td> </td>
   <td>自訂樣式路徑</td>
   <td>如果您選取「自訂」作為「樣式型別」，請瀏覽以指定自訂CSS的路徑，否則請選取「預設」。</td>
  </tr>
 </tbody>
</table>

### 搜尋窗格 {#search-pane}

「搜尋」窗格可讓您從AEM Sidekick的「檔案服務述詞」類別中新增「日期述詞」、「全文檢索述詞」、「屬性述詞」和「標籤述詞」元件。 這些元件會實施搜尋功能，讓使用者在列出的表單上執行搜尋。

**秘訣：** *您可以根據預設條件控制表單入口網站上顯示的表單清單，並隱藏一般使用者的搜尋功能。 若要控制表單清單，請使用述詞元件來套用搜尋篩選器。 您也可以指定預設篩選值，並從「編輯元件」對話方塊的「顯示」標籤中停用搜尋。*

![具有日期、全文、屬性和標籤述詞的搜尋面板](assets/search-with-predicates.png)

具有日期、全文、屬性和標籤述詞的搜尋面板

#### 日期谓词 {#date-predicate}

新增日期述詞元件時，可讓您搜尋在指定期間內修改過的列出表單。

若要設定日期述詞元件：

1. 點選元件，然後點選 ![settings_icon](assets/settings_icon.png). 「編輯」對話方塊開啟。
1. 指定下列專案：

   * **型別：** 唯一可用的選項是 **上次修改日期**

   * **文字：** 日期述詞元件的標籤或註解。 預設值為 **上次修改日期。**

   * **開始日期標籤：** 開始日期欄位的標籤或標題
   * **結束日期標籤：** 結束日期欄位的標籤或標題
   * **隱藏：** 若要強制預設日期篩選條件以列出表單

1. 點選 **確定**

#### 全文檢索述詞 {#full-text-predicate}

全文檢索述詞元件對表單資料（例如名稱和說明）實施全文檢索搜尋。 使用者可以搜尋任何文字字串，以傳回包含其名稱或說明中的文字的表單。

設定全文檢索述詞元件：

1. 點選元件，然後點選 ![settings_icon](assets/settings_icon.png). 「編輯」對話方塊開啟。
1. 在中指定標題 **主要標題** 欄位。
1. 點選 **確定**

#### 屬性述詞 {#properties-predicate}

屬性述詞元件會根據表單屬性（例如標題、作者和說明）實施表單搜尋。

若要設定「屬性述詞」元件：

1. 點選元件，然後點選 ![settings_icon](assets/settings_icon.png). 「編輯」對話方塊開啟。
1. 在「一般」標籤中，指定搜尋標籤。 預設值為 **屬性**

1. 在「選項」標籤中，點選 **新增專案。**
1. 從下拉式清單中選取屬性，並在下拉式清單下方的欄位中指定其搜尋標籤。
1. 重複步驟4以新增更多屬性。 您也可以指定預設篩選值，以根據指定的條件列出表單，並隱藏屬性以供一般使用者搜尋。 選取屬性的「隱藏」核取方塊，並指定預設篩選值。
例如，如果您想要顯示在其標題中包含「旅行」的表單，請選取「標題」屬性旁的「隱藏」。 此外，在預設篩選值文字方塊中指定Travel。

1. 點選 **確定**

#### 标记谓词 {#tags-predicate}

標籤述詞元件會根據Forms Manager中定義的標籤來實施表單搜尋。

若要設定「標籤述詞」元件：

1. 點選元件，然後點選 ![settings_icon](assets/settings_icon.png). 「編輯」對話方塊開啟。
1. 點選「標籤」欄位旁的向下箭頭按鈕。
1. 選取適當的標籤
1. 點選 **確定**

選取的標籤會連同選取的核取方塊一起出現在「搜尋」窗格中。 使用者現在可以根據標籤縮小搜尋範圍。

## 在頁面上列出表單 {#list-forms-on-a-page-br}

若要在頁面上列出表單，請新增 **[!UICONTROL 搜尋和製表人]** 元件至頁面並設定 **[!UICONTROL 清單窗格]**. 若要讓一般使用者搜尋包含日期、文字和標籤的表單，請新增 **[!UICONTROL 搜尋窗格]** 元件。

若要從頁面上的任何位置連結表單，請使用連結元件。 如需連結元件的詳細資訊，請參閱 [將連結元件內嵌在頁面中](../../forms/using/embedding-link-component-page.md).

若要列出處於草稿狀態的表單和已提交的表單，請使用 **[!UICONTROL 草稿和提交]** 元件。 如需詳細資訊，請參閱 [自訂草稿與提交元件](../../forms/using/draft-submission-component.md).

## 行動裝置便利性 {#mobile-device-friendliness}

Forms Portal搜尋與清單元件適合行動裝置使用，並據此調整。 所有三個預設檢視：格線、卡片、根據開啟網站的裝置重新佈局面板，而且網頁也會隨之調整。 簡單的事實是，「搜尋和製表器」只是元件，不會控管頁面層級樣式。

以下影像說明在行動裝置上開啟搜尋與清單程式元件時：

![「搜尋並製表器」元件的熒幕擷圖](assets/search_lister.png)

搜尋和清單產生器元件

## 自訂表單入口網站頁面 {#customizing-a-forms-portal-page-br}

您可以自訂表單入口網站頁面，為頁面提供獨特的外觀。 您也可以新增中繼資料以改善搜尋體驗、變更頁面版面以及新增自訂CSS樣式。 如需詳細資訊，請參閱 [自訂Forms Portal元件的範本](../../forms/using/customizing-templates-forms-portal-components.md).

AEM Forms UI可讓您將自訂中繼資料新增至表單。 自訂中繼資料適用於為一般使用者提供清單和搜尋表單體驗。 如需自訂中繼資料的詳細資訊，請參閱 [自訂Forms Portal元件的範本](../../forms/using/customizing-templates-forms-portal-components.md).

Forms Portal可立即提供轉譯動作。 您可以自訂表單入口網站以新增更多動作。 如需詳細資訊，請參閱 [新增表單製作者專案的自訂動作。](../../forms/using/add-custom-action-form-lister.md)

## 相关文章

* [啟用表單入口網站元件](/help/forms/using/enabling-forms-portal-components.md)
* [建立表單入口網站頁面](/help/forms/using/creating-form-portal-page.md)
* [使用API的網頁上列出表單](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交元件](/help/forms/using/draft-submission-component.md)
* [自訂草稿和已提交表單的儲存](/help/forms/using/draft-submission-component.md)
* [將草稿和提交元件與資料庫整合的範例](/help/forms/using/integrate-draft-submission-database.md)
* [自訂表單入口網站元件的範本](/help/forms/using/customizing-templates-forms-portal-components.md)
* [在入口網站上發佈表單的簡介](/help/forms/using/introduction-publishing-forms.md)
