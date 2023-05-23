---
title: 搜尋表單和資產
seo-title: Searching for forms and assets
description: 您可以使用AEM搜尋來搜尋AEM例項中的表單和資產。 基本和進階搜尋可讓您快速找到資產。
seo-description: You can search forms and assets in your AEM instance using AEM search. Basic and advanced search allows you to quickly locate your assets.
uuid: 0928a453-3dc4-448b-9320-dcbf20606dd9
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: e65925ff-1fbf-4da6-bf09-0cf056c86e5a
docset: aem65
role: Admin
exl-id: 1f4f49b7-5f32-47dd-9dc7-a6974faf2bdf
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 3%

---

# 搜尋表單和資產{#searching-for-forms-and-assets}

您可以使用文字字串或文字字串以及萬用字元來搜尋您的表單或表單資產。 您也可以使用「搜尋」面板中各種類別所提供的條件來縮小搜尋範圍。

當您選取一或多個條件並指定文字字串時，文字和條件的交集會以搜尋結果傳回。 搜尋結果與提供的表單和資產中繼資料一樣好。

按一下 ![aem6forms_search](assets/aem6forms_search.png)，可顯示或隱藏搜尋面板。

## 基本搜尋 {#basic-search}

基本搜尋是預設的搜尋，執行時不會指定任何篩選器。 AEM Forms會針對中繼資料屬性進行全文檢索搜尋。

若要執行基本搜尋，請在文字欄位中輸入搜尋查詢，然後按一下傳回。 您也可以輸入萬用字元(&#42;)以符合任意數目的字元。

Adobe Experience Manager會在中繼資料屬性中搜尋輸入的文字，並傳回對應的結果。 如果您輸入多個字詞，搜尋作業會比對要搜尋的完整文字。

請注意下列有關基本搜尋的要點：

* 使用表單和資產中繼資料屬性進行搜尋。
* 如果您輸入多個字詞，搜尋作業會比對要搜尋的完整文字。
* 搜尋不區分大小寫。 例如，當您輸入 `geometrixx`，具有標題的資產 `Geometrixx`， `GEOMETRIXX`、和 `GeoMetRixx` 會顯示在搜尋結果中。

* 不支援字詞的部分相符專案。 若要使用部分字串進行搜尋，請使用 &#42; 萬用字元。 不過，如果搜尋查詢符合完整的字詞，則會顯示對應的表單或資產。
* 搜尋時會考慮額外的空格，且不會進行修剪。 例如， `My form` 不是相同的搜尋查詢 `My form`.

* 如果中繼資料屬性中欄位的資料和顯示值不同，則無法使用顯示值作為搜尋引數。 例如，您無法根據「已修改」或「已發佈」等狀態進行搜尋，因為這些屬性是以不同格式儲存的。

## 進階搜尋 {#advanced-search}

在搜尋條件中，除了查詢之外，您還可以指定一些搜尋引數，使基本搜尋更有效率，更集中。

![AEM表單和資產搜尋的搜尋欄位和引數或篩選器](assets/search_forms_assets.png)

AEM表單和資產搜尋的搜尋欄位和引數或篩選器

### 资产路径 {#asset-path}

透過使用資產路徑篩選，您可以將搜尋結果限制在目前的目錄。 如果未選取「在目前目錄中搜尋」選項，則搜尋結果會包含基底目錄中的資產。 如果目前頁面不是目錄，且已選取「搜尋目前目錄」選項，則搜尋會傳回存在於父目錄中的資產。

### 资产修改 {#asset-modification}

選取下列其中一個選項，以搜尋在特定時段內修改的所有資產。

| **选项** | **描述** |
|---|---|
| 2 小时前 | 搜尋過去兩小時內修改過的所有資產。 |
| 1 个星期前 | 搜尋過去一週內修改的所有資產。 |
| 1 个月前 | 搜尋過去一個月內修改過的所有資產。 |
| 1 年前 | 搜尋所有在過去一年內修改的資產。 |

### 资产状态 {#asset-status}

您可以使用下列其中一種狀態來搜尋資產：

* **已發佈**：搜尋所有已發佈且在發佈後未修改的資產。

* **已取消發佈**：搜尋所有從未發佈的資產。

* **修改時間**：搜尋發佈後已修改或取消發佈的所有資產。

### 资产类型 {#asset-type}

您可以選取任意數量的資產型別。 搜尋會傳回所有選定資產型別的聯合。

<table>
 <tbody>
  <tr>
   <th>选项</th> 
   <th>描述</th> 
  </tr>
  <tr>
   <td>表單範本<br /> </td> 
   <td>搜尋所有表單範本。<br /> </td> 
  </tr>
  <tr>
   <td>PDF表單</td> 
   <td>搜尋所有PDF檔案。</td> 
  </tr>
  <tr>
   <td>文档</td> 
   <td>搜尋所有檔案。</td> 
  </tr>
  <tr>
   <td>最適化表單<br /> </td> 
   <td>搜尋所有最適化表單。</td> 
  </tr>
  <tr>
   <td>资源</td> 
   <td>搜尋所有資源。<br /> </td> 
  </tr>
 </tbody>
</table>

### 标记 {#tags}

標籤是附加至資產以供識別的標籤。 搜尋時，請從下拉式清單中選取任意數量的標籤，或視需要新增自訂標籤。 搜尋結果包含所選標籤的交集。
