---
title: 頁面範本 — 可編輯
description: 我們引進了可編輯的範本，讓非開發人員能夠建立及編輯範本、提供可保留與使用範本建立的任何頁面的動態連線的範本，並讓頁面元件更通用
uuid: 61791960-fdef-4e49-878a-11fdf1d4f0ab
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 1099cc44-de6d-499e-8b52-f2f5811ae086
docset: aem65
exl-id: dcb66b6d-d731-493e-8936-12d529f6cbde
source-git-commit: 768576e300b655962adc3e1db20fc5ec06a5ba6c
workflow-type: tm+mt
source-wordcount: '3224'
ht-degree: 5%

---

# 頁面範本 — 可編輯 {#page-templates-editable}

可編輯的範本已引入：

* 允許專業作者進行 [建立和編輯範本](/help/sites-authoring/templates.md).

   * 這類專業作者稱為 **範本作者**
   * 範本作者必須是 `template-authors` 群組。

* 提供可保留動態連線至任何建立頁面的範本。 這麼做可確保對範本所做的任何變更都會反映在頁面本身中。
* 讓頁面元件變得更通用，以便無需自訂即可使用核心頁面元件。

使用可編輯的範本時，組成頁面的片段會隔離在元件中。 您可以在UI中設定必要的元件組合，如此一來您就不需要為每個頁面變數開發新的頁面元件。

>[!NOTE]
>
>[靜態範本](/help/sites-developing/page-templates-static.md) 也可供使用。

本文档：

* 提供建立可編輯範本的概觀

   * 如需詳細資訊，請參閱 [建立頁面範本](/help/sites-authoring/templates.md)

* 說明建立可編輯範本所需的管理員/開發人員工作
* 說明可編輯範本的技術基礎

本檔案假設您已熟悉範本的建立和編輯。 請參閱撰寫檔案 [建立頁面範本](/help/sites-authoring/templates.md)，其中會詳細說明向範本作者公開的可編輯範本的功能。

>[!NOTE]
>
>下列教學課程可能也適合在新專案中設定可編輯的頁面範本：
>[AEM Sites快速入門第2部分 — 建立基礎頁面和範本](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/pages-templates.html?lang=en)

## 建立新範本 {#creating-a-new-template}

建立可編輯的範本主要是透過完成 [範本主控台和範本編輯器](/help/sites-authoring/templates.md) 由範本作者執行。 本節提供此程式的概述，並在後面說明在技術層面上發生的情況。

如需如何在AEM專案中使用可編輯範本的詳細資訊，請參閱 [使用Lazybones建立AEM專案](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/create-aem-project-structure-using-lazybones/m-p/186478).

建立新的可編輯範本時，您可以：

1. 建立 [範本的資料夾](#template-folders). 此資料夾不是強制性的，但建議使用最佳實務。
1. 選取 [範本型別](#template-type). 此型別會複製以建立 [範本定義](#template-definitions).

   >[!NOTE]
   >
   >現成提供一系列範本型別。 您也可以 [建立您自己的網站特定範本型別](/help/sites-developing/page-templates-editable.md#creating-template-types)，如有必要。

1. 設定新範本的結構、內容原則、初始內容和版面配置。

   **结构**

   * 結構可讓您定義範本的元件和內容。
   * 無法在產生的頁面上移動範本結構中所定義的元件，也無法將其從任何產生的頁面中刪除。

      * 如果您是在「 」以外的自訂資料夾中建立範本 `We.Retail` 範例內容，您可以選擇Foundation元件或使用 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=zh-Hans).
   * 如果您希望頁面作者能夠新增和移除元件，請將段落系統新增至範本。
   * 可以解锁组件，然后再将其锁定，以便定义初始内容。

   如需範本作者如何定義結構的詳細資訊，請參閱 [建立頁面範本](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

   如需結構的技術詳細資訊，請參閱 [結構](/help/sites-developing/page-templates-editable.md#structure) 於本檔案中。

   **策略**

   * 內容原則會定義元件的設計屬性。

      * 例如，可用的元件或最小/最大尺寸。
   * 這些原則適用於範本（以及使用範本建立的頁面）。

   如需範本作者如何定義原則的詳細資訊，請參閱 [建立頁面範本](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

   如需原則的技術詳細資訊，請參閱 [內容原則](/help/sites-developing/page-templates-editable.md#content-policies) 於本檔案中。

   **初始内容**

   * 初始內容會定義根據範本首次建立頁面時顯示的內容。
   * 然後，頁面作者可以編輯初始內容。

   如需範本作者如何定義結構的詳細資訊，請參閱 [建立頁面範本](/help/sites-authoring/templates.md#editing-a-template-initial-content-author).

   如需初始內容的技術細節，請參閱 [初始內容](/help/sites-developing/page-templates-editable.md#initial-content) 於本檔案中。

   **布局**

   * 您可以为各种设备定义模板布局。
   * 模板的响应式布局与页面创作时的响应式布局功能相同。

   如需範本作者如何定義範本配置的詳細資訊，請參閱 [建立頁面範本](/help/sites-authoring/templates.md#editing-a-template-layout-template-author).

   如需範本配置的技術詳細資訊，請參閱 [版面](/help/sites-developing/page-templates-editable.md#layout) 於本檔案中。

1. 啟用範本，然後允許其用於特定內容樹狀結構。

   * 您可以啟用或停用範本，讓頁面作者可以使用或無法使用此範本。
   * 可以使模板可用于或不可用于某些页面分支。

   如需範本作者如何啟用範本的詳細資訊，請參閱 [建立頁面範本](/help/sites-authoring/templates.md#enabling-and-allowing-a-template-template-author).

   如需啟用範本的技術詳細資訊，請參閱 [為我們啟用和允許範本](/help/sites-developing/page-templates-editable.md#enabling-and-allowing-a-template-for-use)e在此檔案中

1. 使用它來建立內容頁面。

   * 使用範本建立頁面時，靜態範本與可編輯範本之間沒有可見的差異，也沒有任何指示。
   * 對於頁面作者，程式是透明的。

   如需頁面作者如何使用範本建立頁面的詳細資訊，請參閱 [建立及組織頁面](/help/sites-authoring/managing-pages.md#templates).

   如需使用可編輯的範本建立頁面的技術詳細資訊，請參閱 [結果內容頁面](/help/sites-developing/page-templates-editable.md#resultant-content-pages) 於本檔案中。

>[!TIP]
>
>切勿在範本中輸入任何必須國際化的資訊。 基於內部化的目的， [核心元件的本地化功能](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html) 建議使用。

>[!NOTE]
>
>模板是简化页面创建工作流的强大工具。不过，太多的模板会让作者不知所措，并使页面创建变得混乱。一个好的经验法则是将模板的数量保持在 100 个以内。
>
>由于潜在的性能影响，Adobe 建议不要使用超过 1000 个模板。

>[!NOTE]
>
>編輯器使用者端程式庫假設存在 `cq.shared` 內容頁面中的名稱空間。 如果不存在，則會導致JavaScript錯誤 `Uncaught TypeError: Cannot read property 'shared' of undefined`.
>
>所有範例內容頁面都包含 `cq.shared`，因此任何以它們為基礎的內容都會自動包含 `cq.shared`. 但是，如果您決定從頭開始建立自己的內容頁面，而不是以範例內容為基礎，則必須確保包含 `cq.shared` 名稱空間。
>
>另請參閱 [使用使用者端資料庫](/help/sites-developing/clientlibs.md) 以取得進一步資訊。

## 範本資料夾 {#template-folders}

若要組織範本，您可以使用下列資料夾：

* **全局**
* 網站特定您建立用來組織範本的網站特定資料夾，是以具有管理員許可權的帳戶所建立。

>[!NOTE]
>
>即使您可以巢狀內嵌資料夾，當使用者在 **範本** 主控台以平面結構呈現。

在標準AEM執行個體中， **全域** 資料夾存在於範本主控台中。 此資料夾會保留預設範本，並在目前資料夾中找不到原則及/或範本型別時作為備援。 您可以將預設範本新增至此資料夾或建立資料夾（建議選項）。

>[!NOTE]
>
>最佳實務是建立資料夾以存放自訂範本，而不是使用全域資料夾。

>[!CAUTION]
>
>資料夾必須由使用者建立，具有 `admin` 權利。

範本型別和原則會根據下列優先順序繼承至所有資料夾：

1. 目前的資料夾。
1. 目前資料夾的父系或父系。
1. `/conf/global`
1. `/apps`
1. `/libs`

將會建立所有允許專案的清單。 如果任何設定重疊( `path`/ `label`)，則只會向使用者顯示最接近目前資料夾的執行個體。

若要建立資料夾，請執行下列動作：

* 以程式設計方式或CRXDE Lite
* 使用設定瀏覽器

## 使用 CRXDE Lite {#using-crxde-lite}

1. 可以程式設計方式或CRXDE Lite方式為您的執行個體建立新資料夾（在/conf下）。

   必須使用下列結構：

   ```xml
   /conf
       <your-folder-name> [sling:Folder]
           settings [sling:Folder]
               wcm [cq:Page]
                   templates [cq:Page]
                   policies [cq:Page]
   ```

1. 然後，您可以在資料夾根節點上定義下列屬性：

   `<your-folder-name> [sling:Folder]`

   名称: `jcr:title`

   * 类型: `String`

   * 值：您要在「 」中顯示的「 」資料夾標題 **範本** 主控台。

1. 在 *增加* 至標準編寫許可權和許可權(例如， `content-authors`)、指派群組並定義作者所需的存取許可權(ACL)，以便在新資料夾中建立範本。

   此 `template-authors` group是必須指派的預設群組。 請參閱下列章節 [ACL和群組](/help/sites-developing/page-templates-editable.md#acls-and-groups) 以取得詳細資訊。

   另請參閱 [存取許可權管理](/help/sites-administering/user-group-ac-admin.md#access-right-management) 以取得有關管理和指派存取許可權的完整詳細資訊。

### 使用設定瀏覽器 {#using-the-configuration-browser}

1. 前往 **全域導覽** -> **工具** > **設定瀏覽器**.

   現有資料夾會列在左側，包括 **全域** 資料夾。

1. 单击&#x200B;**创建**。
1. 在 **建立設定** 對話方塊中，必須設定下列欄位：

   * **標題**：提供設定資料夾的標題
   * **可編輯的範本**：選取以允許在此資料夾中使用可編輯的範本

1. 按一下 **建立**

>[!NOTE]
>
>在設定瀏覽器中，您可以編輯全域資料夾並啟動 **可編輯的範本** 選項（如果要在此資料夾中建立範本）。 不過，不建議使用此作法。
>
>請參閱 [設定瀏覽器](/help/sites-administering/configurations.md) 說明檔案以取得詳細資訊。

### ACL和群組 {#acls-and-groups}

建立範本資料夾後（透過CRXDE或使用組態瀏覽器），必須為範本資料夾的適當群組定義ACL，以確保適當的安全性。

的範本資料夾 [`We.Retail` 參考實作](/help/sites-developing/we-retail.md) 可作為範例。

#### 範本 — 作者群組 {#the-template-authors-group}

此 `template-authors` group是用來管理範本存取的群組，且隨附於AEM，但為空白。 必須將使用者新增至專案/網站的群組。

>[!CAUTION]
>
>此 `template-authors` 群組為 *僅限* 適用於必須能夠建立範本的使用者。
>
>編輯範本的功能強大，若未正確完成，現有範本可能會損毀。 因此，此角色應著重於且僅包含合格使用者。

下表詳細說明範本編輯的必要許可權。

<table>
 <tbody>
  <tr>
   <th>路径</th>
   <th>角色/群組</th>
   <th>权限<br /> </th>
   <th>描述</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>範本作者<br /> </td>
   <td>讀取、寫入、復寫</td>
   <td>在網站特定中建立、讀取、更新、刪除和復寫範本的範本作者 <code>/conf</code> 空間</td>
  </tr>
  <tr>
   <td>匿名Web使用者</td>
   <td>讀取</td>
   <td>匿名Web使用者在轉譯頁面時必須讀取範本</td>
  </tr>
  <tr>
   <td>内容作者</td>
   <td>復寫</td>
   <td>replicateContent作者在啟動頁面時必須啟動頁面的範本</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>讀取、寫入、復寫</td>
   <td>在網站特定中建立、讀取、更新、刪除和復寫範本的範本作者 <code>/conf</code> 空間</td>
  </tr>
  <tr>
   <td>匿名Web使用者</td>
   <td>讀取</td>
   <td>匿名Web使用者在轉譯頁面時必須讀取原則</td>
  </tr>
  <tr>
   <td>内容作者</td>
   <td>復寫</td>
   <td>內容作者在啟用頁面時必須啟用頁面範本的原則</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>範本作者</td>
   <td>讀取</td>
   <td>範本作者會根據其中一個預先定義的範本型別建立範本。</td>
  </tr>
  <tr>
   <td>匿名Web使用者</td>
   <td>无</td>
   <td>匿名Web使用者不得存取範本型別</td>
  </tr>
 </tbody>
</table>

此預設值 `template-authors` 群組僅涵蓋專案設定，其中所有 `template-authors` 允許成員存取及編寫所有範本。 對於更複雜的設定，需要多個範本作者群組來分隔範本的存取許可權，則必須建立更多自訂範本作者群組。 不過，範本作者群組的許可權仍會相同。

#### /conf/global下的舊版範本 {#legacy-templates-under-conf-global}

不要將範本儲存在 `/conf/global`. 但是，對於某些舊版安裝，此位置可能仍存在範本。 *僅限* 在此等舊式情況下，應 `/conf/global` 路徑必須明確設定。

<table>
 <tbody>
  <tr>
   <th>路径</th>
   <th>角色/群組</th>
   <th>权限<br /> </th>
   <th>描述</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/templates</code></td>
   <td>範本作者</td>
   <td>讀取、寫入、復寫</td>
   <td>在中建立、讀取、更新、刪除和復寫範本的範本作者 <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>匿名Web使用者</td>
   <td>讀取</td>
   <td>匿名Web使用者在轉譯頁面時必須讀取範本</td>
  </tr>
  <tr>
   <td>内容作者</td>
   <td>復寫</td>
   <td>內容作者在啟用頁面時必須啟用頁面的範本</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>讀取、寫入、復寫</td>
   <td>在中建立、讀取、更新、刪除和復寫範本的範本作者 <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>匿名Web使用者</td>
   <td>讀取</td>
   <td>匿名Web使用者在轉譯頁面時必須讀取原則</td>
  </tr>
  <tr>
   <td>内容作者</td>
   <td>復寫</td>
   <td>內容作者在啟用頁面時必須啟用頁面範本的原則</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/global/settings/wcm/template-types</code></td>
   <td>範本作者</td>
   <td>讀取</td>
   <td>範本作者會根據預先定義的範本型別之一建立範本</td>
  </tr>
  <tr>
   <td>匿名Web使用者</td>
   <td>无</td>
   <td>匿名Web使用者不得存取範本型別</td>
  </tr>
 </tbody>
</table>

## 範本型別 {#template-type}

建立範本時，請指定範本型別：

* 範本型別可有效提供範本的範本。 建立範本時，會使用所選範本型別的結構和初始內容來建立範本。

   * 範本型別會複製以建立範本。
   * 複製一旦發生，範本和範本型別之間的唯一連線是靜態參考，以供參考。

* 範本型別可讓您定義：

   * 頁面元件的資源型別。
   * 根節點的原則，定義範本編輯器中允許的元件。
   * Adobe建議您為回應式格線定義中斷點，並在範本型別上設定行動模擬器。 此步驟為選用，因為組態也可以在個別範本上定義(請參閱 [範本型別和行動裝置群組](/help/sites-developing/page-templates-editable.md#p-template-type-and-mobile-device-groups-br-p))。

* AEM提供少量現成可用的範本型別，例如「HTML5頁面」和「最適化表單頁面」。

   * 提供其他範例作為的一部分 [`We.Retail`](/help/sites-developing/we-retail.md) 範例內容。

* 範本型別通常由開發人員定義。

現成的範本型別儲存在下列位置：

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>請勿變更 `/libs` 路徑。 原因是因為內容屬於 `/libs` 下次升級執行個體時會被覆寫（並在套用hotfix或feature pack時可能被覆寫）。

您的網站特定範本型別應儲存在類似位置：

* `/apps/settings/wcm/template-types`

自訂範本型別的定義應儲存在使用者定義的資料夾中（建議使用），或是儲存在 `global`. 例如：

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>範本型別必須遵循正確的資料夾結構(即 `/settings/wcm/...`)，否則找不到範本型別。

### 範本型別和行動裝置群組 {#template-type-and-mobile-device-groups-br}

此 [裝置群組](/help/sites-developing/mobile.md#device-groups) 用於可編輯的範本（設定為屬性的相對路徑） `cq:deviceGroups`)定義哪些行動裝置可在中作為模擬器 [版面模式](/help/sites-authoring/responsive-layout.md) 頁面製作的「 」。 此值可在兩個位置設定：

* 在可編輯的範本型別上
* 在可編輯的範本上

建立新的可編輯範本時，值會從範本型別複製到個別範本。 如果型別上未設定值，可在範本上設定它。 建立範本後，就沒有任何型別繼承到範本。

>[!CAUTION]
>
>的值 `cq:deviceGroups` 必須設定為相對路徑，例如 `mobile/groups/responsive` 而不是絕對路徑，例如 `/etc/mobile/groups/responsive`.

>[!NOTE]
>
>替換為 [靜態範本](/help/sites-developing/page-templates-static.md)，的值 `cq:deviceGroups` 可設定於網站的根目錄。
>
>若使用可編輯的範本，此值現在會儲存在範本層級，而不支援在頁面根層級。

### 建立範本型別 {#creating-template-types}

如果您已建立可作為其他範本基礎的範本，則可以複製此範本作為範本型別。

1. 建立範本，就像建立任何可編輯的範本一樣 [如此處的紀錄](/help/sites-authoring/templates.md#creating-a-new-template-template-author)，可作為範本型別的基礎。
1. 使用CRXDE Lite，複製新建立的範本 `templates` 節點至 `template-types` 下的節點 [範本資料夾](/help/sites-developing/page-templates-editable.md#template-folders).
1. 從刪除範本 `templates` 下的節點 [範本資料夾](/help/sites-developing/page-templates-editable.md#template-folders).
1. 在範本的副本中，位於 `template-types` 節點，全部刪除 `cq:template` 和 `cq:templateType` 全部屬性 `jcr:content` 節點。

您也可以使用GitHub提供的範例可編輯範本作為基礎，來開發自己的範本型別。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-sites-example-custom-template-type專案](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* 將專案下載為 [ZIP檔案](https://codeload.github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/zip/refs/heads/master)

## 範本定義 {#template-definitions}

可編輯範本的定義已儲存 [使用者定義的資料夾](/help/sites-developing/page-templates-editable.md#template-folders) （建議使用）或選擇使用 `global`. 例如：

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

範本的根節點為型別 `cq:Template` 骨架結構為：

```xml
<template-name>
  initial
    jcr:content
      root
        <component>
        ...
        <component>
  jcr:content
    @property status
  policies
    jcr:content
      root
        @property cq:policy
        <component>
          @property cq:policy
        ...
        <component>
          @property cq:policy
  structure
    jcr:content
      root
        <component>
        ...
        <component>
      cq:responsive
        breakpoints
  thumbnail.png
```

主要元素包括：

* `<template-name>`

   * ` [initial](#initial-content)`
   * `jcr:content`
   * ` [structure](#structure)`
   * ` [policies](#policies)`
   * `thumbnail.png`

### jcr：content {#jcr-content}

此節點保留範本的屬性：

* **名称**: `jcr:title`

* **名称**: `status`

   * **类型**: `String`

   * **值**： `draft`， `enabled`，或 `disabled`

### 结构 {#structure}

定義結果頁面的結構：

* 與初始內容合併( `/initial`)建立頁面時。
* 對結構所做的變更會反映在使用範本建立的任何頁面中。
* 此 `root` ( `structure/jcr:content/root`)節點會定義產生頁面中可用的元件清單。

   * 範本結構中定義的元件無法在任何結果頁面上移動或刪除。
   * 解鎖元件後， `editable` 屬性已設定為 `true`.

   * 解鎖已包含內容的元件後，此內容會移至 `initial` 分支。

* 此 `cq:responsive` 節點保留回應式佈局的定義。

### 初始内容 {#initial-content}

定義建立新頁面時的初始內容：

* 包含 `jcr:content` 複製到任何新頁面的節點。
* 與結構合併( `/structure`)建立頁面時。
* 如果在建立後變更初始內容，則會更新任何現有頁面。
* 此 `root` node會儲存元件清單，以定義結果頁面中可用的元件。
* 如果在結構模式下將內容新增到元件，且元件稍後解除鎖定（或反之），則此內容會用作初始內容。

### 布局 {#layout}

時間 [編輯範本時，您可以定義版面](/help/sites-authoring/templates.md)，此實務會使用 [標準回應式佈局](/help/sites-authoring/responsive-layout.md) 也可以 [已設定](/help/sites-administering/configuring-responsive-layout.md).

### 內容原則 {#content-policies}

內容（或設計）原則會定義元件的設計屬性，例如元件的可用性或最小/最大維度。 這些原則適用於範本（以及使用範本建立的頁面）。 可在範本編輯器中建立和選取內容原則。

* 屬性 `cq:policy`，位於 `root` 節點
   `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
提供頁面段落系統內容原則的相對參照。

* 屬性 `cq:policy`，於下的元件明確節點上 `root`，提供個別元件原則的連結。

* 實際原則定義儲存在下列位置：
   `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>原則定義的路徑取決於元件的路徑。 此 `cq:policy` 保留組態本身的相對參照。

>[!NOTE]
>
>從可編輯範本建立的頁面不會在頁面編輯器中提供設計模式。
>
>此 `policies` 可編輯範本的樹狀結構與下列靜態範本的設計模式組態有相同的階層：
>
>`/etc/designs/<my-site>/jcr:content/<component-name>`
>
>靜態範本的設計模式設定是按頁面元件定義的。

### 页面策略 {#page-policies}

頁面原則可讓您定義 [內容原則](#content-policies) 頁面（主要parsys）的範本或結果頁面中。

### 啟用和允許使用範本 {#enabling-and-allowing-a-template-for-use}

1. **啟用範本**

   在使用範本之前，必須透過以下任一方式啟用它：

   * [啟用範本](/help/sites-authoring/templates.md#enablingatemplateauthor) 從 **範本** 主控台。

   * 在上設定狀態屬性 `jcr:content` 節點。

      * 例如，在：
         `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * 定義屬性：

         * 名稱：狀態
         * 型別：字串
         * 价值: `enabled`

1. **允许的模板**

   * [在上定義允許的範本路徑 **頁面屬性**](/help/sites-authoring/templates.md#allowing-a-template-author) 子分支的適當頁面或根頁面的。
   * 設定屬性：
      `cq:allowedTemplates`
於 
`jcr:content` 必要分支的節點。
   例如，其值為：

   `/conf/<your-folder>/settings/wcm/templates/.*`

## 結果內容頁面 {#resultant-content-pages}

從可編輯範本建立的頁面：

* 使用合併的子樹狀結構建立 `structure` 和 `initial` 在範本中

* 具有範本和範本型別中所儲存資訊的參考。 您可以透過 `jcr:content` 具有下列屬性的節點：

   * `cq:template`
提供實際範本的動態參考；讓範本的變更反映在實際頁面上。

   * `cq:templateType`
提供範本型別的參考。

![chlimage_1-71](assets/chlimage_1-71.png)

上圖顯示範本、內容和元件如何相互關聯：

* 控制器 —  `/content/<my-site>/<my-page>`
參照範本的結果頁面。 內容會控制整個程式。 根據定義，它會存取適當的範本和元件。

* 設定 —  `/conf/<my-folder>/settings/wcm/templates/<my-template>`
此 [範本和相關內容原則](#template-definitions) 定義頁面設定。

* 模型 — OSGi套件組合 [OSGI套件組合](/help/sites-deploying/osgi-configuration-settings.md) 實作功能。

* 檢視 —  `/apps/<my-site>/components`
在製作和發佈環境中，內容的轉譯者為 [元件](/help/sites-developing/components.md).

轉譯頁面時：

* **模板**:

   * 此 `cq:template` 其屬性 `jcr:content` 會參照節點，以存取對應至該頁面的範本。

* **组件**:

   * 頁面元件會合併 `structure/jcr:content` 範本的樹狀結構，具有 `jcr:content` 頁面的樹狀結構。

   * 頁面元件僅可讓作者編輯已標籤為可編輯的範本結構節點（以及任何子系）。
   * 在頁面上呈現元件時，該元件的相對路徑會取自 `jcr:content` 節點；下方的相同路徑 `policies/jcr:content` 接著會搜尋範本的節點。

      * 此 `cq:policy` 此節點的屬性指向實際內容原則（也就是說，它儲存該元件的設計設定）。

      * 此功能可讓您擁有重複使用相同內容原則設定的多個範本。
