---
title: 自訂AEM表單工作區簡介
seo-title: Introduction to Customizing AEM form workspace
description: 提供概念和技術資訊的快速介紹，用於自訂流程管理的LiveCycleAEM Forms工作區。
seo-description: A quick introduction, with conceptual and technical information, to customize LiveCycle AEM Forms workspace for process management.
uuid: 38759071-e6b8-4976-8b06-909ad7a786cd
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 021c6606-8cd3-472c-a80b-b1bcace7e87f
docset: aem65
exl-id: b183d42f-343c-4acb-bc73-f80ad72e54df
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1763'
ht-degree: 0%

---

# 自訂AEM表單工作區簡介{#introduction-to-customizing-aem-form-workspace}

AEM表單工作區提供修改其介面的呈現語意和功能的功能。 以下說明用於變更樣式、版面、格式設定、品牌和核心功能的自訂型別。

![cu_customized_workspace_example](assets/cu_customized_workspace_example.png)

自訂工作區的範例

## 自訂型別 {#types-of-customizations}

AEM Forms工作區支援各種自訂，以更新使用者介面的版面、外觀、功能等。 自訂涉及更新下列一或多個專案：

* 使用者介面的外觀
* 使用語意自訂的功能
* 在其他應用程式中重複使用HTML元件

### 使用者介面變更 {#user-interface-changes}

您可以變更AEM Forms工作區的外觀、版面配置和其他呈現語意。 透過自訂CSS、HTML範本和JavaScript™檔案來變更工作區。 預設安裝會提供所有預設檔案。

最常用的步驟包含在 [AEM Forms工作區自訂的一般步驟](../../forms/using/generic-steps-html-workspace-customization.md). 如需此類自訂的特定範例，包括詳細步驟，請參閱本文結尾的相關文章。

#### 瞭解樣式表 {#understanding-the-style-sheet}

在自訂工作區之前，請熟悉AEM Forms所提供的預設樣式表，網址為/libs/ws/css/style.css。

若要自訂工作區，建議您熟悉位於/libs/ws/css資料夾中的現有樣式表style.css。 以下說明一些顯著元件。

<table>
 <tbody>
  <tr>
   <th><p>CSS元素</p> </th>
   <th><p>使用者介面元件已修改</p> </th>
  </tr>
  <tr>
   <td><p>#标题</p> </td>
   <td><p>AEM Forms工作區的標頭</p> </td>
  </tr>
  <tr>
   <td><p>.categoryList</p> </td>
   <td><p>類別清單</p> </td>
  </tr>
  <tr>
   <td><p>.categoryList .header</p> </td>
   <td><p>類別清單的標題</p> </td>
  </tr>
  <tr>
   <td><p>.category， .filters</p> </td>
   <td><p>類別清單下方的空間</p> </td>
  </tr>
  <tr>
   <td><p>.category， .filter</p> </td>
   <td><p>类别</p> </td>
  </tr>
  <tr>
   <td><p>.category：hover， .category.selected， .filter：hover， .filter.selected</p> </td>
   <td><p>選取的類別並將滑鼠移到類別樣式上</p> </td>
  </tr>
  <tr>
   <td><p>categoryListBar .tool， categoryListBar .content</p> </td>
   <td><p>開始程式頁面（已關閉的類別清單）</p> </td>
  </tr>
  <tr>
   <td><p>filterListBar .tool， filterListBar .content</p> </td>
   <td><p>待辦事項頁面（已關閉的篩選器清單）</p> </td>
  </tr>
  <tr>
   <td><p>processNameListBar .tool， processNameListBar .content</p> </td>
   <td><p>追蹤頁面（已關閉的流程名稱清單）</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList， .tasklist</p> </td>
   <td><p>起點清單或任務清單</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList .header， .tasklist .header</p> </td>
   <td><p>起點清單或任務清單的標題</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected， .task.selected</p> </td>
   <td><p>選取的起點或任務</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected .description， .task.selected .description</p> </td>
   <td><p>所選起點或任務的描述</p> </td>
  </tr>
  <tr>
   <td><p>#taskarea</p> </td>
   <td><p>工作區域</p> </td>
  </tr>
  <tr>
   <td><p>#header .dropdown</p> </td>
   <td><p>標題中的使用者下拉式清單</p> </td>
  </tr>
  <tr>
   <td><p>.sortDrop dd ul</p> </td>
   <td><p>排序任務下拉式清單</p> </td>
  </tr>
 </tbody>
</table>

#### CSS {#css}

AEM Forms工作區的外觀會從CSS借用其外觀。 透過自訂CSS，您可以變更工作區的表現語意，例如字型、顏色、品牌和版面。

CSS自訂的頂層步驟為：

* 建立CSS檔案。
* 將樣式專案新增至此CSS。 如需詳細資訊，請參閱瞭解CSS樣式。
* 更新其參照 `html.jsp`.

如需進行這些自訂的確切步驟，請參閱 [AEM Forms工作區自訂的一般步驟](../../forms/using/generic-steps-html-workspace-customization.md). AEM Forms工作區隨附的CSS檔案位於/libs/ws/css/。 對於CSS相關的自訂，請使用 [出貨套件](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p). 如需CSS相關自訂的特定範例，請參閱本文結尾的相關說明主題。

#### 图像 {#image}

您可以自訂AEM Forms工作區，以新增使用者的頭像或新增組織的標誌。 對於這些自訂，請使用 [出貨套件](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p).

影像自訂的最上層步驟為：

* 安裝及設定WebDAV。
* 新增影像。
* 新增與新增的影像對應的新樣式。
* 連結至中的新CSS檔案 `html.jsp` 檔案。

若要開始在AEM Forms工作區中自訂影像，請遵循 [AEM Forms工作區自訂的一般步驟](../../forms/using/generic-steps-html-workspace-customization.md). 如需影像相關自訂的特定範例，請參閱本文結尾的相關說明主題。

#### HTML範本 {#html-template}

HTML範本有助於定義工作區使用者介面的外觀和版面。 透過更新預設HTML範本，您可以自訂配置預設使用者介面。

HTML範本自訂的最上層步驟為：

* 在使用者建立的資料夾中，複製所需的預設檔案。
* 在使用者定義的資料夾中新增範本。
* 對複製的檔案進行相關更新，例如新範本的路徑。

如需此類自訂的特定範例，請參閱本文結尾提供的說明主題。 選擇 [出貨套件](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p) 或 [開發封裝](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)，視要自訂的範本而定。

### 語意變更 {#semantic-changes}

若要修改AEM Forms工作區功能，請變更JavaScript原始程式碼。 核心功能中的修改專案會標示為語意變更。 您可以修改提供為AEM Forms工作區原始程式碼一部分的模型、檢視和範本。

進行語意變更以修改AEM Forms工作區功能的頂層步驟如下：

* 在使用者建立的資料夾中，複製適當的預設檔案。
* 在使用者定義的資料夾中新增模型和檢視。
* 進行相關更新，例如更新預設JavaScript檔案中新新增的模型和檢視的路徑。
* 將套件最小化，以最佳化效能。

如需原始程式碼中元件的詳細概念資訊，請參閱 [可重複使用元件的說明](/help/forms/using/description-reusable-components.md). 對於這些自訂，請使用開發套件。

### 可重複使用的元件 {#reusable-components}

由於AEM Forms工作區是以元件為基礎的軟體，因此可輕鬆自訂及重複使用。 您可以輕鬆地將工作區元件與Web應用程式整合。

如需更多概念資訊，請參閱 [可重複使用元件的說明](/help/forms/using/description-reusable-components.md) 如需有關使用元件的指示，請參閱 [在網頁應用程式中整合AEM Forms工作區元件](/help/forms/using/description-reusable-components.md).

## 建立AEM Forms工作區程式碼 {#building-html-workspace-code}

### SDK套件 {#sdk-package}

此套件包含AEM Forms工作區的原始碼。 套件位於 `[LC root]\sdk\html-workspace\adobe-lc-workspace-src.zip`.

此範本主要用於自訂，因為它提供產生以下專案的功能：

* 出貨、偵錯和開發設定檔的CRX套件(如下所述 [CRX套件](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p))。
* 自訂程式碼的縮製版本（用於語意變更）。

#### WS內容 {#ws-content}

* client-pkg：

   * src — 包含建立CRX節點所需的成品。
   * pom.xml — 為各種設定檔建置部署套件的指令碼WS-Deploy套裝

* client-html：

   * 元件 — 包含指令碼用來建立AEM Forms工作區SDK的zip.xml。
   * src/main/webapp -

      * css — 包含AEM Forms工作區的樣式表。
      * 影像 — 包含AEM Forms工作區中使用的影像。
      * js：

         * libs — 包含AEM Forms工作區中使用的所有第三方程式庫。
         * licenses — 包含HTML和JS檔案的授權，以及這些授權在各自原始檔中加上前置詞的程式碼。
         * minifier — 用於組合、縮制和升級customizedJavaScript程式碼。
         * resourcejs_optimizer — 用於JavaScript來源的組合、縮制和升級。
         * resource_generator — 用於產生register.js和modelcontrollerpath.js。
         * 執行階段：

            * 初始設定式 — 包含用於初始化AEM Forms工作區中使用的骨幹檢視和模型的initializer.js。
            * 模型 — 包含AEM Forms工作區中所有元件的主幹模型。
            * 路由 — 包含JavaScript檔案和HTML檔案，可在AEM Forms工作區中載入啟動程式、待辦事項、追蹤和偏好設定。
            * 服務 — 包含AEM Forms工作區中使用的service.js。 所有伺服器呼叫都是透過service.js進行。
            * 範本 — 包含所有範本，即AEM Forms workspace中所有檢視的HTML檔案。
            * util — 包含在AEM Forms工作區中使用的所有公用程式檔案(javascript)。
            * 檢視 — 包含AEM Forms工作區中所有元件的主幹檢視。
         * main.js
         * router.js
      * libs/ws： pdf.html和pluginPing.pdf用於載入AEM Forms工作區中的PDF forms，而WSNextAdapter.swf用於載入AEM Forms工作區中的SWF表單和參考線。
      * 地區設定：

         * de-DE — 包含德文的translation.json。
         * en-US — 包含英文的translation.json。
         * fr-FR — 包含法文的translation.json。
         * ja-JP — 包含日文的translation.json。
         * html.jsp — 包含可找出目前瀏覽器地區設定的程式碼。
      * html.jsp
      * GET.jsp




### CRX套件 {#crx-package}

CRX套件可部署在CRX™存放庫上。 此函式位於 `[LC root]\crx-repository\install\adobe-lc-workspace-pkg.zip`.

此套件可使用下述的三個設定檔來建置。

| **配置文件** | **描述** | **使用** |
|---|---|---|
| 出貨設定檔 | 此設定檔會使用縮制來建立可能大小最小的CRX套件。 此套件最有效率。 所有JavaScript™檔案會合併並縮製為單一JS檔案。 | 當JS檔案中不需要進一步語意變更時，請使用此設定檔。 |
| 偵錯設定檔 | 此設定檔會建立中等效率的CRX套件。 封裝的大小略大於使用「出貨設定檔」建立的封裝。 此套件已將大部分JavaScript檔案合併至單一JS檔案中。 | 使用此設定檔進行偵錯。 |
| 開發設定檔 | 此設定檔會建立最大可能大小的CRX套件。 所有JavaScript檔案都可單獨使用，因為它們位於SDK套件中。 | 在合併語意變更時使用此設定檔。 |

#### 出貨設定檔 {#ship-profile}

#### 命令 {#command}

* mvn clean -P將安裝傳送至使用者端之來源封裝的client-pkg資料夾上。
* Ship profile命令僅能在64位元JVM上執行。

#### WS內容 {#ws-content-1}

* css — 包含style.css、ie.css和jquery-ui.css。
* 影像 — 包含所有影像。
* js：

   * 程式庫：

      * require - Contains require.js.
      * jqueryui — 包含jquery.ui.datepicker.ja.js。
   * 執行階段：

      * 範本 — 包含所有範本，即AEM Forms workspace中所有元件的HTML檔案。
   * main.js （合併、縮小和醜化）。
   * registry.js



* 程式庫：

   * ws — 包含pluginPing.pdf、pdf.html和WSNextAdapter.swf。

* 地區設定 — 包含.content.xml。
* 地區設定：

   * de-DE — 包含德文的translation.json。
   * en-US — 包含英文的translation.json。
   * fr-FR — 包含法文的translation.json。
   * ja-JP — 包含日文的translation.json。
   * html.jsp — 包含可找出目前瀏覽器地區設定的程式碼。

* 索引 — 包含.content.xml
* 設定檔 — 包含offline.jsp。
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### 偵錯設定檔 {#debug-profile}

#### 命令 {#command-1}

* mvn clean -P在client-pkg上偵錯安裝
* 偵錯設定檔命令執行僅適用於64位元JVM。

#### WS內容 {#ws-content-2}

* css — 包含style.css、ie.css和jqueri-ui.css。
* 影像 — 包含所有影像。
* js：

   * 程式庫：

      * require - Contains require.js.
      * jqueryui — 包含jquery.ui.datepicker.ja.js。
   * 執行階段：

      * 範本 — 包含所有範本，即AEM Forms workspace中所有元件的HTML檔案。
   * main.js （合併）。
   * registry.js



* 程式庫：

   * ws — 包含pluginPing.pdf、pdf.html和WSNextAdapter.swf。

* 地區設定 — 包含.content.xml。
* 地區設定：

   * de-DE — 包含德文的translation.json。
   * en-US — 包含英文的translation.json。
   * fr-FR — 包含法文的translation.json。
   * ja-JP — 包含日文的translation.json。
   * html.jsp — 包含可找出目前瀏覽器地區設定的程式碼。

* 索引 — 包含.content.xml
* 設定檔 — 包含offline.jsp。
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### 開發設定檔 {#dev-profile}

#### 命令 {#command-2}

mvn clean — 在client-pkg上安裝P Dev

#### WS內容 {#ws-content-3}

* css — 包含style.css、ie.css和jqueri-ui.css。
* 影像 — 包含所有影像。
* js：

   * libs — 包含AEM Forms工作區中使用的所有程式庫。
   * require — 包含require.js
   * jqueryui — 包含jquery.ui.datepicker.ja.js
   * 執行階段：

      * 初始設定式 — 包含初始設定式.js和modelcontrollerpath.js。
      * 模型 — 包含AEM Forms工作區中所有元件的模型。
      * 路由 — 包含JavaScript檔案和HTML檔案，可在AEM Forms工作區中載入啟動程式、待辦事項、追蹤和偏好設定。
      * 服務 — 包含AEM Forms工作區中使用的service.js。
      * 範本 — 包含所有範本，即AEM Forms workspace中所有元件的HTML檔案。
      * util — 包含在AEM Forms工作區中使用的所有公用程式檔案(JavaScript)。
      * 檢視 — 包含AEM Forms工作區中所有元件的檢視。
   * main.js
   * registry.js
   * router.js


* 程式庫：

   * ws — 包含pluginPing.pdf、pdf.html和WSNextAdapter.swf。

* 地區設定 — 包含.content.xml。
* 地區設定：

   * de-DE — 包含德文的translation.json。
   * en-US — 包含英文的translation.json。
   * fr-FR — 包含法文的translation.json。
   * ja-JP — 包含日文的translation.json。
   * html.jsp — 包含可找出目前瀏覽器地區設定的程式碼。

* 索引 — 包含.content.xml
* 設定檔 — 包含offline.jsp。
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml
