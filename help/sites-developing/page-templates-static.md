---
title: 頁面範本 — 靜態
seo-title: Page Templates - Static
description: 範本可用來建立頁面，並定義哪些元件可以在所選範圍內使用
seo-description: A Template is used to create a Page and defines which components can be used within the selected scope
uuid: 7a473c19-9565-476e-9e54-ab179da04d71
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: cfd90e8f-9b9b-4d0b-be31-828469b961de
docset: aem65
exl-id: b934ac41-78b9-497f-ba95-b05ef1e5660e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1626'
ht-degree: 1%

---

# 頁面範本 — 靜態{#page-templates-static}

範本可用來建立頁面，並定義可在所選範圍內使用的元件。 範本是節點的階層，其結構與要建立的頁面相同，但沒有任何實際內容。

每個範本都會提供您一系列可供使用的元件。

* 範本的建置方式 [元件](/help/sites-developing/components.md)；
* 元件會使用並允許存取Widget，而這些元件會用於轉譯內容。

>[!NOTE]
>
>[可編輯的範本](/help/sites-developing/page-templates-editable.md) 也可供使用，並且是提供最大彈性和最新功能的建議範本型別。

## 範本的屬性和子節點 {#properties-and-child-nodes-of-a-template}

範本是cq：Template型別的節點，具有以下屬性和子節點：

<table>
 <tbody>
  <tr>
   <td><strong>名称 <br /> </strong></td>
   <td><strong>类型 <br /> </strong></td>
   <td><strong>描述 <br /> </strong></td>
  </tr>
  <tr>
   <td>. <br /> </td>
   <td> cq:Template</td>
   <td>目前的範本。 範本為節點型別cq：Template。<br /> </td>
  </tr>
  <tr>
   <td> allowedChildren </td>
   <td> 字符串[]</td>
   <td>允許作為此範本之子範本的範本路徑。<br /> </td>
  </tr>
  <tr>
   <td> allowedParents</td>
   <td> 字符串[]</td>
   <td>允許作為此範本之父範本的範本路徑。<br /> </td>
  </tr>
  <tr>
   <td> allowedPaths</td>
   <td> 字符串[]</td>
   <td>允許以此範本為基礎的頁面路徑。<br /> </td>
  </tr>
  <tr>
   <td> jcr:created</td>
   <td> 日期</td>
   <td>建立範本的日期。<br /> </td>
  </tr>
  <tr>
   <td> jcr：description</td>
   <td> 字符串</td>
   <td>範本的說明。<br /> </td>
  </tr>
  <tr>
   <td> jcr:title</td>
   <td> 字符串</td>
   <td>範本的標題。<br /> </td>
  </tr>
  <tr>
   <td> 排名</td>
   <td> 长整型</td>
   <td>範本的排名。 用於在使用者介面中顯示範本。<br /> </td>
  </tr>
  <tr>
   <td> jcr：content</td>
   <td> cq:PageContent</td>
   <td>包含範本內容的節點。<br /> </td>
  </tr>
  <tr>
   <td> thumbnail.png</td>
   <td> nt：file</td>
   <td>範本的縮圖。<br /> </td>
  </tr>
  <tr>
   <td> icon.png</td>
   <td> nt：file</td>
   <td>範本的圖示。<br /> </td>
  </tr>
 </tbody>
</table>

範本是頁面的基礎。

若要建立頁面，必須複製範本（節點樹） `/apps/<myapp>/template/<mytemplate>`)中的對應位置：如果頁面是使用 **網站** 標籤。

此複製動作也會提供頁面的初始內容（通常是僅限頂層內容）和屬性sling：resourceType，也就是用來轉譯頁面的頁面元件路徑（子節點jcr：content中的所有專案）。

## 範本的結構方式 {#how-templates-are-structured}

需要考慮兩個方面：

* 範本本身的結構
* 使用範本時產生的內容結構

### 範本的結構 {#the-structure-of-a-template}

範本會在型別的節點下建立 **cq：Template**.

![screen_shot_2012-02-13at63646pm](assets/screen_shot_2012-02-13at63646pm.png)

您可以設定各種屬性，特別是：

* **jcr：title**  — 範本的標題；建立頁面時顯示在對話方塊中。
* **jcr：description**  — 範本的說明；建立頁面時顯示在對話方塊中。

此節點包含jcr：content (cq：PageContent)節點，可作為產生頁面之內容節點的基礎；此節點會使用sling：resourceType參照要用於呈現新頁面之實際內容的元件。

![screen_shot_2012-02-13at64010pm](assets/screen_shot_2012-02-13at64010pm.png)

建立新頁面時，此元件可用來定義內容的結構和設計。

![screen_shot_2012-02-13at64137pm](assets/screen_shot_2012-02-13at64137pm.png)

### 範本產生的內容 {#the-content-produced-by-a-template}

範本是用來建立型別的頁面 `cq:Page` （如前所述，頁面是一種特殊型別的元件）。 每個AEM頁面都有一個結構化節點 `jcr:content`. 此功能：

* 屬於cq：PageContent型別
* 是儲存已定義內容定義的結構化節點型別
* 具有屬性 `sling:resourceType` 以參考儲存用於轉譯內容的sling指令碼的元件

### 預設範本 {#default-templates}

AEM隨附許多立即可用的預設範本。 在某些情況下，您可能會想要依原樣使用範本。 在此情況下，您需要確保範本可用於您的網站。

例如，AEM隨附多個範本，包括內容頁面和首頁。

| **标题** | **Component** | **位置** | **用途** |
|---|---|---|---|
| 主页 | homepage | geometrixx | Geometrixx首頁範本。 |
| 内容页 | contentpage | geometrixx | Geometrixx內容頁面範本。 |

#### 顯示預設範本 {#displaying-default-templates}

若要檢視存放庫中所有範本的清單，請依照下列步驟進行：

1. 在CRXDE Lite中，開啟 **工具** 功能表並按一下 **查詢**.

1. 在「查詢」索引標籤中
1. 作為 **型別**，選取 **XPath**.

1. 在 **查詢** 輸入欄位，輸入下列字串：//element(&#42;， cq：Template)

1. 按一下 **執行**. 清單會顯示在結果方塊中。

在大多數情況下，您將取得現有範本並開發新的範本供您自己使用。 另請參閱 [開發頁面範本](#developing-page-templates) 以取得詳細資訊。

若要啟用您網站的現有範本，並且希望範本顯示在 **建立頁面** 建立頁面時的對話方塊 **網站** 從 **網站** 主控台，將範本節點的allowedPaths屬性設定為： **/content(/.&#42;)？**

## 範本設計的套用方式 {#how-template-designs-are-applied}

使用在UI中定義樣式時 [設計模式](/help/sites-authoring/default-components-designmode.md)，則設計會持續保留在定義樣式的內容節點的確切路徑上。

>[!CAUTION]
>
>Adobe建議僅套用設計至 [設計模式](/help/sites-authoring/default-components-designmode.md).
>
>例如，在CRX DE中修改設計不是最佳做法，此類設計的應用可能與預期行為不同。

如果設計僅使用「設計模式」套用，則下列各節 [設計路徑解析](/help/sites-developing/page-templates-static.md#design-path-resolution)， [決策樹](/help/sites-developing/page-templates-static.md#decision-tree)，以及 [範例](/help/sites-developing/page-templates-static.md#example) 不適用。

### 設計路徑解析 {#design-path-resolution}

根據靜態範本呈現內容時，AEM會嘗試根據內容階層的周遊情況，將最相關的設計和樣式套用至內容。

AEM會依下列順序決定內容節點最相關的樣式：

* 如果內容節點的完整和確切路徑有設計（當設計在「設計」模式中定義時），則使用該設計。
* 如果父系的內容節點有設計，則使用該設計。
* 如果內容節點的路徑上有任何節點的設計，則使用該設計。

在後兩種情況下，如果有多個適用的設計，請使用最接近內容節點的設計。

### 決策樹 {#decision-tree}

此為下列專案的圖形表示： [設計路徑解析](/help/sites-developing/page-templates-static.md#design-path-resolution) 邏輯。

![design_path_resolution](assets/design_path_resolution.png)

### 示例 {#example}

請考量下列簡單內容結構，其中設計可套用至任何節點：

`/root/branch/leaf`

下表說明AEM如何選擇設計。

<table>
 <tbody>
  <tr>
   <td><strong>尋找設計<br /> </strong></td>
   <td><strong>存在以下專案的設計：<br /> </strong></td>
   <td><strong>已選擇設計<br /> </strong></td>
   <td><strong>注释</strong></td>
  </tr>
  <tr>
   <td><code class="code">leaf
      </code></td>
   <td><p><code>root</code></p> <p><code>branch</code></p> <p><code>leaf</code></p> </td>
   <td><code>leaf</code></td>
   <td>一律會採用最精確的相符項。<br /> </td>
  </tr>
  <tr>
   <td><code>leaf</code></td>
   <td><p><code>root</code></p> <p><code>branch</code></p> </td>
   <td><code>branch</code></td>
   <td>回復到樹狀結構中最接近的匹配項。</td>
  </tr>
  <tr>
   <td><code>leaf</code></td>
   <td><code>root</code></td>
   <td><code>root</code></td>
   <td>如果其他所有操作失敗，則採取剩餘的部分。<br /> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><code>branch</code></td>
   <td><code>branch</code></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><p><code>branch</code></p> <p><code class="code">leaf
       </code></p> </td>
   <td><code>branch</code></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><p><code>root</code></p> <p><code class="code">branch
       </code></p> </td>
   <td><code>branch</code></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><p><code>root</code></p> <p><code class="code">leaf
       </code></p> </td>
   <td><code>root</code></td>
   <td><p>如果沒有完全相符的專案，請取樹狀結構中較低的一個。</p> <p>假設這永遠適用，但樹狀結構往上可能太具體。<br /> </p> </td>
  </tr>
 </tbody>
</table>

## 開發頁面範本 {#developing-page-templates}

AEM頁面範本只是用來建立新頁面的模型。 視需要它們可以包含儘可能少或儘可能多的初始內容，其角色是建立正確的初始節點結構，並將所需的屬性（主要是sling：resourceType）設定為允許編輯和呈現。

### 建立新範本（根據現有範本） {#creating-a-new-template-based-on-an-existing-template}

不用說，新範本可以從頭開始完全建立，但現有範本通常會經過複製和更新，以節省您的時間和精力。 例如，Geometrixx中的範本可以用來協助您開始使用。

若要根據現有範本建立新範本，請執行下列動作：

1. 將現有範本（最好使用儘可能接近您要達到的定義）複製到新節點。

   範本通常儲存在 **/apps/&lt;website-name>/templates/&lt;template-name>**.

   >[!NOTE]
   >
   >可用範本的清單取決於新頁面的位置及每個範本中指定的版位限制。 另請參閱 [範本可用性](#templateavailibility).

1. 變更 **jcr：title** ，以反映其新角色。 您也可以更新 **jcr：description** 視情況而定。 請務必視需要變更頁面的範本可用性。

   >[!NOTE]
   >
   >如果您希望範本顯示在 **建立頁面** 建立頁面時的對話方塊 **網站** 從 **網站** 主控台，設定 `allowedPaths` 範本節點的屬性至： `/content(/.*)?`

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. 複製範本所依據的元件(這由 **sling：resourceType** 的屬性 **jcr：content** 節點)，以建立新執行個體。

   元件通常儲存在 **/apps/&lt;website-name>/components/&lt;component-name>**.

1. 更新 **jcr：title** 和 **jcr：description** 新元件的ID。
1. 如果您想要在範本選取範圍清單中顯示新的縮圖圖片（大小為128 x 98畫素），請取代thumbnail.png。
1. 更新 **sling：resourceType** 範本的 **jcr：content** 節點來參照新元件。
1. 對範本及/或其基礎元件的功能或設計進行任何進一步的變更。

   >[!NOTE]
   >
   >對所做的變更 **/apps/&lt;website>/templates/&lt;template-name>** 節點將會影響範本例項（如選取專案清單中所示）。
   對所做的變更 **/apps/&lt;website>/components/&lt;component-name>** 節點會影響使用範本時建立的內容頁面。

   您現在可以使用新範本在您的網站中建立頁面。

>[!NOTE]
編輯器使用者端程式庫假設存在 `cq.shared` 名稱空間時，如果不存在，則會發生JavaScript錯誤 `Uncaught TypeError: Cannot read property 'shared' of undefined` 將產生。
所有範例內容頁面都包含 `cq.shared`，因此任何以它們為基礎的內容都會自動包含 `cq.shared`. 但是，如果您決定從頭開始建立自己的內容頁面，而不是以範例內容為基礎，則必須確保包含 `cq.shared` 名稱空間。
另請參閱 [使用使用者端資料庫](/help/sites-developing/clientlibs.md) 以取得進一步資訊。

## 讓現有範本可供使用 {#making-an-existing-template-available}

此範例說明如何允許範本用於特定內容路徑。 建立新頁面時可供頁面作者使用的範本由中定義的邏輯決定 [範本可用性](/help/sites-developing/templates.md#template-availability).

1. 在CRXDE Lite中，導覽至您要用於頁面的範本，例如Newsletter範本。
1. 變更 `allowedPaths` 屬性及其他用於下列專案的屬性： [範本可用性](/help/sites-developing/templates.md#template-availability). 例如， `allowedPaths`： `/content/geometrixx-outdoors/[^/]+(/.*)?` 表示此範本允許位於下的任何路徑中 `/content/geometrixx-outdoors`.

   ![chlimage_1-89](assets/chlimage_1-89.png)
