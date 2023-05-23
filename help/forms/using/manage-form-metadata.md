---
title: 管理表單中繼資料
seo-title: Manage form metadata
description: 中繼資料可讓您更輕鬆地分類及組織資產，並協助尋找特定資產的使用者。
seo-description: Metadata allows for easier categorization and organization of assets and helps users who are looking for a specific asset.
uuid: d982df6f-a256-4bad-868f-74fcd08350f8
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: ba571f8e-8bd3-48eb-82e1-c93b14ffe44a
docset: aem65
role: Admin
exl-id: f82bbd39-b655-47a9-bca9-21d7cd30c082
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1972'
ht-degree: 1%

---

# 管理表單中繼資料{#manage-form-metadata}

## 概述  {#overview-nbsp}

中繼資料可讓您更輕鬆地分類及組織資產，並協助尋找特定資產的使用者。

AEM Forms預設會為每種資產型別提供一組已定義的中繼資料。 除了預設中繼資料外，您還可以將自訂中繼資料新增到每個資產型別。 AEM Forms也為您提供正確的方法，以有效率地建立、管理和交換表單的所有中繼資料。

如果您是開發人員或網站擁有者，您可以自訂Forms Portal (AEM Forms的一般使用者介面)，以反映您在組織中使用的中繼資料。 如需Forms入口網站的詳細資訊，請參閱 [在入口網站上發佈表單的簡介](../../forms/using/introduction-publishing-forms.md).

## AEM Forms中的中繼資料 {#metadata-in-aem-forms}

在AEM Forms中，與資產相關聯的中繼資料屬性清單取決於其型別。 此外，如果您新增任何自訂中繼資料屬性，則會將該屬性新增至新增自訂中繼資料之型別的所有資產。

### 資產型別 {#asset-types}

AEM Forms支援下列資產型別：

* 表單範本（XFA表單）
* PDF forms
* 檔案(平面PDF)
* 自适应表单
* 资源
* XFS

#### 廣泛的中繼資料清單 {#extensive-list-of-metadata}

以下是AEM Forms支援的中繼資料屬性詳盡清單：

<table>
 <tbody> 
  <tr> 
   <td><strong>属性名称</strong></td> 
   <td><strong>资源类型</strong></td> 
   <td><strong>描述</strong><br /> </td> 
  </tr> 
  <tr> 
   <td>标题</td> 
   <td>除了資源以外的所有專案</td> 
   <td>表單的顯示名稱。<br /> </td> 
  </tr> 
  <tr> 
   <td>描述</td> 
   <td>除了資源以外的所有專案</td> 
   <td>表單說明。 使用者可以指定此值。<br /> </td> 
  </tr> 
  <tr> 
   <td>类型</td> 
   <td>所有</td> 
   <td><p>指定資產型別的唯讀值。 它可以有下列其中一個值：</p> 
    <ul> 
     <li>表單範本</li> 
     <li>PDF表單、PDF表單(Acroform)或PDF表單（已簽署）</li> 
     <li>檔案，檔案（已簽署）</li> 
     <li>自适应表单</li> 
     <li>资源</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>创建时间</td> 
   <td>所有</td> 
   <td>指定資產建立時間的唯讀值。</td> 
  </tr> 
  <tr> 
   <td>上次修改日期</td> 
   <td>所有</td> 
   <td>指定上次修改資產時間的唯讀值。</td> 
  </tr> 
  <tr> 
   <td>创作</td> 
   <td>除了資源以外的所有專案</td> 
   <td><p>根據表單型別自動計算的唯讀值。</p> 
    <ul> 
     <li>PDF/表單範本/檔案 — 從上傳的二進位檔案中擷取。</li> 
     <li>最適化表單 — 建立表單時登入的使用者。</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>状态</td> 
   <td>除了資源以外的所有專案</td> 
   <td><p> 唯讀值，定義表單的下列狀態之一：</p> 
    <ul> 
     <li>無值：如果表單未曾發佈。</li> 
     <li>已發佈：表單發佈時。</li> 
     <li>已修改：表單發佈一次後修改的時間。</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>上次發佈日期</td> 
   <td>除了資源以外的所有專案</td> 
   <td>指定上次發佈表單時間的唯讀值。</td> 
  </tr> 
  <tr> 
   <td>發佈開啟/關閉時間</td> 
   <td>除了資源以外的所有專案</td> 
   <td><p>排定自動發佈/取消發佈表單的時間。 使用者在編輯中繼資料時設定此值。</p> 
    <ul> 
     <li>發佈開啟和關閉時間都應在目前日期以後。 </li> 
     <li>發佈關閉時間應在發佈開啟時間之後。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>提交URL</td> 
   <td><p>表單範本</p> <p>PDF表單</p> </td> 
   <td><p>設定使用者指定的URL以將表單資料提交至servlet。</p> <p>您可以使用下列任一方法來設定提交URL （依優先順序排列）：</p> 
    <ul> 
     <li>在AEM Forms Designer中建立XFA表單時，使用HTTP提交按鈕直接在表單範本中指定提交URL。</li> 
     <li>在AEM Forms UI中，選取表單並在編輯中繼資料屬性時指定提交URL。</li> 
     <li>在Forms Portal中，編輯「搜尋和製表器」元件，並在「表單連結」索引標籤下指定提交URL。</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>HTML演算設定檔</td> 
   <td>表單範本</td> 
   <td>以HTML格式轉譯表單範本時使用的HTML轉譯器設定檔。</td> 
  </tr> 
  <tr> 
   <td>演算格式</td> 
   <td><p>表單範本</p> <p>自适应表单</p> </td> 
   <td><p>此選項可讓使用者在發佈表單時指定表單的轉譯格式：</p> 
    <ul> 
     <li>HTML</li> 
     <li>PDF</li> 
     <li> 双向</li> 
    </ul> <p>此選項僅用於限制一般使用者可在表單入口網站上看到表單的呈現格式。</p> </td> 
  </tr> 
  <tr> 
   <td>标记</td> 
   <td>除了資源以外的所有專案</td> 
   <td>與表單關聯的標籤有助於快速輕鬆的搜尋。</td> 
  </tr> 
  <tr> 
   <td>引用</td> 
   <td><p>自适应表单</p> <p>表單範本</p> <p>资源</p> </td> 
   <td><p>與此表單相關的資產（其他表單或資源）清單。 這些資產可能分為以下兩個類別：</p> 
    <ul> 
     <li>參照：目前表單參照的資產。</li> 
     <li>引用者：引用目前資產的資產。</li> 
    </ul> <p>這些資產會顯示為連結，而您可以按一下連結，直接存取其中繼資料。<br /> </p> </td> 
  </tr> 
  <tr> 
   <td>表單模型(XDP/XSD)選擇</td> 
   <td>自适应表单</td> 
   <td><p>指定在製作最適化表單時使用的表單模型。 此屬性可以有下列值：</p> 
    <ul> 
     <li>表單範本：從存放庫中的現有表單範本中選取表單範本。 此值可更新。</li> 
     <li>XML結構描述：已上傳XSD檔案。 此值可更新。</li> 
     <li>无</li> 
    </ul> 
    <div>
      表單模型一旦選取便可以更新，但不能移除。 
    </div> </td> 
  </tr> 
 </tbody> 
</table>

## 檢視表單中繼資料 {#view-form-metadata}

資產具有現有的屬性值，可在唯讀模式下檢視。 此中繼資料源自表單上傳或表單建立時。

1. 導覽至您要檢視中繼資料的資產位置。

1. 使用下列其中一種方式開啟屬性頁面：

   1. 按一下檢視屬性 ![e_reviewmode_properties_n](assets/e_reviewmode_properties_n.png) 圖示加以檢視。

      >[!NOTE]
      >
      >「快速動作」是在滑鼠懸停時顯示在縮圖上的動作專案。

   1. 選取表單並按一下「檢視屬性」 ![e_reviewmode_properties_n](assets/e_reviewmode_properties_n.png) 圖示顯示。
   1. 若未處於選取模式，請按一下表單縮圖，導覽至表單詳細資訊頁面。 現在，按一下 ![aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png) 右上角的眼睛圖示，然後按一下下方清單中的「屬性」 。

1. 開啟的屬性頁面會顯示只包含中繼資料屬性（包含某些值）的綱要。

   屬性頁面有一個包含兩個動作圖示的工具列：

   * 編輯： ![aem6forms_edit](assets/aem6forms_edit.png) 編輯中繼資料屬性值
   * 檢視： ![aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png) 導覽至表單詳細資訊頁面，該頁面會在預覽模式下開啟表單。

   內容部分分為兩個部分：

   * 左側面板包含表單的縮圖
   * 右側面板包含唯讀模式的中繼資料屬性，並分佈於各種索引標籤中。


## 新增/更新表單中繼資料值 {#add-update-form-metadata-values}

您可以編輯現有中繼資料屬性的值，或向現有中繼資料屬性欄位新增值（例如，當中繼資料欄位空白時）。

### 更新中繼資料屬性值 {#update-metadata-property-values}

1. 依照上一節所述的步驟，開啟屬性頁面，您可在此檢視所選表單的現有中繼資料。

1. 在工具列中按一下編輯圖示 ![aem6forms_edit](assets/aem6forms_edit.png) 將頁面的模式從唯讀變更為讀取/寫入。

1. 開啟的屬性頁面包含混合了可編輯輸入欄位和靜態文字的結構描述。

1. 靜態文字中顯示的屬性是您無法編輯的屬性。

1. 您可以導覽至其他標籤，以尋找置於其下的中繼資料屬性的輸入欄位。

   此頁面有一個工具列，其中包含兩個與檢視模式不同的動作圖示：

   * 取消： ![aem6forms_close](assets/aem6forms_close.svg_w24.png) 取消目前對中繼資料屬性值所做的任何變更
   * 完成： ![aem6forms_check](assets/aem6forms_check.png) 儲存目前對中繼資料屬性值所做的所有變更

   這兩個動作都會將使用者引導回包含更新值的屬性頁面的唯讀模式。

### 更新表單縮圖 {#update-the-form-thumbnail}

屬性頁面中的左側面板會顯示表單的縮圖。 依預設，顯示的縮圖是建立表單（最適化表單）時或上傳表單時產生的縮圖。

對於所有表單型別，您可以選擇按一下「 」以上傳影像 **[!UICONTROL 上傳影像]** 和從本機目錄瀏覽影像檔案。 選取的影像會用作縮圖，而非預設的縮圖。

針對調適型表單，提供其他功能，可讓使用者產生縮圖，作為目前調適型表單預覽的快照。 由於AEM Forms也支援撰寫調適型表單，每次您變更調適型表單時，調適型表單的預覽可能會變更。 此功能可產生縮圖，協助您根據目前的預覽狀態，為最適化表單取得新的縮圖。 按一下 **[!UICONTROL 產生預覽]** 以執行此動作。

>[!NOTE]
>
>* 縮圖使用正方形影像。 當您使用非正方形影像並在清單檢視中檢視縮圖時，縮圖會以裁剪方式顯示。
>* 上傳或產生新影像後，縮圖就會被此影像取代，且無法重設為上一個影像。
>


## 新增自訂中繼資料 {#add-custom-metadata}

除了現成可用的中繼資料外，AEM Forms也支援新的自訂中繼資料。

提供的工具（中繼資料結構編輯器）可定義中繼資料配置的結構描述；也就是說，顯示在以下專案中的佈局： **[!UICONTROL 屬性]** 表單頁面。 中繼資料結構編輯器可讓您新增或修改資產的自訂結構。

AEM Forms會公開此工具中支援之表單型別的中繼資料結構。 如此一來，您就可以存取這些結構描述，並使用中繼資料結構描述編輯器中提供的功能來新增自訂屬性。

### 瀏覽中繼資料結構編輯器 {#navigate-the-metadata-schema-editor}

1. 導覽至 **[!UICONTROL 「工具>資產>中繼資料結構」]**.

1. 按一下 **[!UICONTROL 表單]** 從列出的結構表單。

1. 在開啟的清單中，按一下您要新增自訂中繼資料的資產型別。

   >[!NOTE]
   >
   >這些結構描述包含立即可用的中繼資料屬性，且不得變更/編輯（選取核取方塊並從工具列按一下「編輯」）以避免功能問題。

1. 任何按下的資產型別都會開啟包含 `extendedmetadata` 選項。 編輯此結構描述。

1. 選取旁邊的核取方塊 `extendedmetadata` 然後按一下編輯 ![aem6forms_edit](assets/aem6forms_edit.png) 圖示顯示。

1. AEM Forms會開啟所選資產型別的中繼資料結構編輯器/表單產生器（在此案例中是適用性表單）。

   ![最適化表單型別的中繼資料結構編輯器](assets/metadata-schema-editor-for-adaptive-form-type.png)

   中繼資料編輯器

   1. 左側面板包含放置欄位的標籤區段，右側面板顯示所有可用的UI元件和從左側面板中選取的欄位的屬性。

   1. 鎖定的區段不可編輯，並包含現成提供之所有中繼資料屬性的欄位。

   1. 您可以按一下+符號來新增其他標籤。

   1. 您可以新增所需型別的自訂欄位，方法是從 **[!UICONTROL 建置表單]** 區段切換至「綱要」頁面。
   1. 此欄位的規格可在 **[!UICONTROL 設定]** 區段。

### 在結構描述編輯器中新增自訂中繼資料屬性 {#add-custom-metadata-property-in-schema-editor}

1. 導覽至您要新增自訂屬性的標籤（現有或新增）。

1. 將所需型別的元件從 **[!UICONTROL 建置表單]** 區段至左側面板，並放置在方便的位置。

   >[!NOTE]
   >
   >您無法移動鎖定的區段，但可將元件置於任何空白處。

1. 按一下您剛才拖曳的元件。 在右側面板中開啟的「設定」標籤中，填寫下列欄位的資訊：

   1. 指定欄位標籤，這會作為顯示在結構描述中放置欄位上方的名稱（例如：Department）
   1. 在「對應至屬性」欄位下方，您可以看到預先填入的值 **&#39;./jcr：content/metadata/default&#39;**. 變更&#39;**預設**&#39;至所需的屬性名稱，用於儲存crx存放庫中的屬性(例如： &#39;。/jcr：content/metadata/department&#39;)

      >[!NOTE]
      >
      >請勿變更前置詞&#39;。/jcr：content/metadata/&#39;，因為它定義了儲存屬性的路徑。
      >
      >此外，屬性名稱必須是唯一的，以避免在存放庫的相同位置寫入兩個或更多屬性的值。 因此，建議您變更「預設」值。

   1. 根據需求填寫其他設定。 例如：如果您要將欄位設為必要欄位，請選取必要選項。
   1. 若要刪除您新增的欄位，請選取該欄位，然後按一下刪除 ![delete-1](assets/delete-1.png) 圖示。

1. 如有需要，請依照步驟1-3新增其他屬性。
1. 按一下 **完成** 完成所有變更後。

   您已成功新增自訂中繼資料屬性。

AEM Forms中的所有調適型表單現在都包含此額外的中繼資料屬性。 您可以從屬性頁面編輯它。
