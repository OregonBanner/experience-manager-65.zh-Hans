---
title: 使用客户端库
seo-title: Using Client-Side Libraries
description: AEM提供使用者端程式庫資料夾，可讓您將使用者端程式碼儲存在存放庫中、將其組織成類別，並定義每個類別程式碼何時及如何提供給使用者端
seo-description: AEM provides Client-side Library Folders, which allow you to store your client-side code in the repository, organize it into categories, and define when and how each category of code is to be served to the client
uuid: f12b13cc-6651-4c9a-9c52-19a22bb82b28
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 3d14837d-41a8-480a-83ba-392e32f84c65
docset: aem65
exl-id: 408ac30c-60ab-4d6c-855c-d544af8d5cf9
source-git-commit: 7ceee6819618d785f04029b9ac1c6f763995b3ac
workflow-type: tm+mt
source-wordcount: '2861'
ht-degree: 1%

---

# 使用客户端库{#using-client-side-libraries}

現代網站非常依賴由複雜的JavaScript和CSS程式碼驅動的使用者端處理。 組織和最佳化此程式碼的伺服可能會是個複雜的問題。

為協助處理此問題，AEM提供 **使用者端資料庫資料夾**，可將使用者端程式碼儲存在存放庫中，將其組織成類別，並定義每個類別程式碼何時及如何提供給使用者端。 然後，使用者端程式庫系統會負責在最終網頁中產生正確的連結，以載入正確的程式碼。

## 使用者端程式庫在AEM中的運作方式 {#how-client-side-libraries-work-in-aem}

在頁面的HTML中包含使用者端資料庫（即JS或CSS檔案）的標準方式是僅包含 `<script>` 或 `<link>` 標籤（包含相關檔案的路徑）。 例如，

```xml
...
<head>
   ...
   <script type="text/javascript" src="/etc/clientlibs/granite/jquery/source/1.8.1/jquery-1.8.1.js"></script>
   ...
</head>
...
```

雖然此方法在AEM中有效，但當頁面及其組成元件變得複雜時，可能會導致問題。 在這種情況下，最終HTML輸出中可能會包含同一JS程式庫的多份副本，這是很危險的。 若要避免此問題，並允許AEM使用的使用者端程式庫的邏輯組織 **使用者端資料庫資料夾**.

使用者端程式庫資料夾是型別的存放庫節點 `cq:ClientLibraryFolder`. 其定義位於 [CND標籤法](https://jackrabbit.apache.org/node-type-notation.html) 是

```shell
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

依預設， `cq:ClientLibraryFolder` 節點可放置於 `/apps`， `/libs` 和 `/etc` 存放庫的子樹狀結構(這些預設值和其他設定可透過 **AdobeGraniteHTML程式庫管理員** 的面板 [系統主控台](https://localhost:4502/system/console/configMgr))。

每個 `cq:ClientLibraryFolder` 會填入一組JS和/或CSS檔案，以及一些支援檔案（請參閱下文）。 的屬性 `cq:ClientLibraryFolder` 的設定如下：

* `categories`：識別這個JS和/或CSS檔案集所屬的類別 `cq:ClientLibraryFolder` 秋天。 此 `categories` 屬性是多值屬性，可讓程式庫資料夾屬於多個類別（請參閱下方以瞭解其用處）。

* `dependencies`：這是此程式庫資料夾所相依的其他使用者端程式庫類別清單。 例如，假設有兩個 `cq:ClientLibraryFolder` 節點 `F` 和 `G`，如果檔案位於 `F` 需要在下列位置有另一個檔案： `G` 為了正常運作，至少一個 `categories` 之 `G` 應該屬於 `dependencies` 之 `F`.

* `embed`：用來內嵌其他程式庫中的程式碼。 如果節點F嵌入節點G和H，則產生的HTML將是來自節點G和H的內容集。
* `allowProxy`：如果使用者端程式庫位於 `/apps`，此屬性可讓您透過Proxy servlet存取它。 另請參閱 [找到使用者端程式庫資料夾並使用Proxy使用者端程式庫Servlet](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) 下方的。

## 參考使用者端程式庫 {#referencing-client-side-libraries}

由於HTL是開發AEM網站的慣用技術，因此HTL應該用來在AEM中包含使用者端程式庫。 不過，也可以使用JSP執行此操作。

### 使用HTL {#using-htl}

在HTL中，使用者端程式庫是透過AEM提供的helper範本載入，該範本可透過以下方式存取： [ `data-sly-use`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#use). 此檔案中有三個範本可用，這些範本可透過來呼叫 [ `data-sly-call`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#template-call)：

* **css**  — 僅載入參照的使用者端程式庫的CSS檔案。
* **js**  — 僅載入參照的使用者端程式庫的JavaScript檔案。
* **全部**  — 載入參照的使用者端程式庫的所有檔案（CSS和JavaScript）。

每个帮助程序模板都需要一个 `categories` 选项来引用所需的客户端库。该选项可以是字符串值的数组，也可以是包含逗号分隔值列表的字符串。

如需詳細資訊和使用範例，請參閱檔案 [開始使用HTML範本語言](https://helpx.adobe.com/experience-manager/htl/using/getting-started.html#loading-client-libraries).

### 使用JSP {#using-jsp}

新增 `ui:includeClientLib` 標籤至JSP程式碼，在產生的HTML頁面中新增使用者端程式庫的連結。 若要參照程式庫，請使用 `categories` 的屬性 `ui:includeClientLib` 節點。

```
<%@taglib prefix="ui" uri="https://www.adobe.com/taglibs/granite/ui/1.0" %>
<ui:includeClientLib categories="<%= categories %>" />
```

例如， `/etc/clientlibs/foundation/jquery` 節點屬於型別 `cq:ClientLibraryFolder` 具有值的類別屬性 `cq.jquery`. JSP檔案中的下列程式碼會參考程式庫：

```xml
<ui:includeClientLib categories="cq.jquery"/>
```

產生的HTML頁面包含下列程式碼：

```xml
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
```

如需完整資訊，包括篩選JS、CSS或主題資料庫的屬性，請參閱 [ui：includeClientLib](/help/sites-developing/taglib.md#lt-ui-includeclientlib).

>[!CAUTION]
>
>`<cq:includeClientLib>`過去常用來包含使用者端程式庫，但自AEM 5.6起已棄用。 [ `<ui:includeClientLib>`](/help/sites-developing/taglib.md#lt-ui-includeclientlib) 應改用，如上所述。

## 建立使用者端資料庫資料夾 {#creating-client-library-folders}

建立 `cq:ClientLibraryFolder` 節點來定義JavaScript和階層式樣式表程式庫，並讓它們可供HTML頁面使用。 使用 `categories` 節點的屬性，用來識別其所屬的程式庫類別。

節點包含一或多個在執行階段合併至單一JS和/或CSS檔案的來源檔案。 產生檔案的名稱是節點名稱，帶有 `.js` 或 `.css` 副檔名。 例如，程式庫節點命名為 `cq.jquery` 產生的檔案中的結果命名為 `cq.jquery.js` 或 `cq.jquery.css`.

使用者端程式庫資料夾包含下列專案：

* 要合併的JS和/或CSS來源檔案。
* 支援CSS樣式的資源，例如影像檔案。

   **注意：** 您可以使用子資料夾來組織來源檔案。
* 一 `js.txt` 檔案和/或一個 `css.txt` 可識別在產生的JS和/或CSS檔案中要合併之來源檔案的檔案。

![clientlibarch](assets/clientlibarch.png)

如需有關Widget使用者端程式庫特定需求的資訊，請參閱 [使用和擴充Widget](/help/sites-developing/widgets.md).

Web使用者端必須擁有許可權才能存取 `cq:ClientLibraryFolder` 節點。 您也可以從存放庫的安全區域公開程式庫（請參閱下方的從其他程式庫內嵌程式碼）。

### 覆寫/lib中的程式庫 {#overriding-libraries-in-lib}

位於下方的使用者端程式庫資料夾 `/apps` 優先於位置相似的同名資料夾 `/libs`. 例如， `/apps/cq/ui/widgets` 優先於 `/libs/cq/ui/widgets`. 當這些程式庫屬於相同類別時，底下的程式庫 `/apps` 已使用。

### 找到使用者端程式庫資料夾並使用Proxy使用者端程式庫Servlet {#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet}

在舊版中，使用者端程式庫資料夾位於下方 `/etc/clientlibs` 存放庫中。 系統仍支援此功能，但建議使用者端程式庫現在位於 `/apps`. 這是為了在其他指令碼附近找到使用者端程式庫，這些指令碼通常可在下方找到 `/apps` 和 `/libs`.

>[!NOTE]
>
>使用者端程式庫資料夾下方的靜態資源必須位於名為的資料夾中 *資源*. 如果您在資料夾底下沒有靜態資源（例如影像） *資源*，無法在發佈執行個體上參照。 範例如下： https://localhost:4503/etc.clientlibs/geometrixx/components/clientlibs/resources/example.gif

>[!NOTE]
>
>為了更妥善地將程式碼與內容和設定隔離開，建議在下方找到使用者端程式庫 `/apps` 並透過以下方式公開 `/etc.clientlibs` 善用 `allowProxy` 屬性。

用於下的使用者端程式庫的順序 `/apps` 為了可存取，會使用proxy servelt。 ACL仍會在使用者端程式庫資料夾上強制執行，但servlet允許透過讀取內容 `/etc.clientlibs/` 如果 `allowProxy` 屬性已設定為 `true`.

靜態資源若位於使用者端程式庫資料夾下方的資源之下，則只能透過Proxy存取。

例如：

* 您在中有clientlib `/apps/myproject/clientlibs/foo`
* 您有一個靜態影像，位於 `/apps/myprojects/clientlibs/foo/resources/icon.png`

然後您設定 `allowProxy` 屬性： `foo` 為true。

* 然後，您可以請求 `/etc.clientlibs/myprojects/clientlibs/foo.js`
* 然後，您可以透過以下方式參考影像 `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

>[!CAUTION]
>
>使用代理的使用者端程式庫時，AEM Dispatcher設定可能需要更新，以確保允許具有擴充功能clientlibs的URI。

>[!CAUTION]
>
>Adobe建議您將使用者端程式庫放置在 `/apps` 以及透過Proxy servlet來使用。 但請記住，最佳實務仍要求公用網站絕不包含直接透過提供服務的任何內容。 `/apps` 或 `/libs` 路徑。

### 建立使用者端資料庫資料夾 {#create-a-client-library-folder}

1. 在網頁瀏覽器中開啟CRXDE Lite([https://localhost:4502/crx/de](https://localhost:4502/crx/de))。
1. 選取您要找到使用者端程式庫資料夾的資料夾，然後按一下 **建立>建立節點**.
1. 輸入程式庫檔案的名稱，然後在「型別」清單中選取 `cq:ClientLibraryFolder`. 按一下 **確定** 然後按一下 **全部儲存**.
1. 若要指定程式庫所屬的類別，請選取 `cq:ClientLibraryFolder` 節點，新增以下屬性，然後按一下 **全部儲存**：

   * 名稱：類別
   * 型別：字串
   * 值：類別名稱
   * 多個：選取

1. 以任何方式將來源檔案新增至程式庫資料夾。 例如，使用WebDav使用者端來複製檔案，或建立檔案並手動編寫內容。

   **注意：** 您可以視需要在子資料夾中組織來源檔案。

1. 選取使用者端程式庫資料夾，然後按一下 **「建立」>「建立檔案」**.
1. 在「檔案名稱」方塊中，鍵入下列其中一個檔案名稱，然後按一下「確定」：

   * **`js.txt`：** 使用此檔案名稱來產生JavaScript檔案。
   * **`css.txt`：** 使用此檔案名稱來產生階層式樣式表。

1. 開啟檔案並輸入下列文字，以識別來源檔案的根路徑：

   `#base=*[root]*`

   取代* `[root]`*包含來源檔案的資料夾路徑（相對於TXT檔案）。 例如，當來源檔案與TXT檔案位於相同的資料夾時，請使用以下文字：

   `#base=.`

   下列程式碼會將根設定為名為mobile的資料夾，位於 `cq:ClientLibraryFolder` 節點：

   `#base=mobile`

1. 在以下行上 `#base=[root]`，鍵入相對於根的來源檔案路徑。 將每個檔案名稱放在單獨的一行上。
1. 按一下 **全部儲存**.

### 連結至相依性 {#linking-to-dependencies}

當使用者端程式庫資料夾中的程式碼參考其他程式庫時，請將其他程式庫識別為相依性。 在JSP中， `ui:includeClientLib` 參照使用者端程式庫資料夾的標籤會讓HTML程式碼包含所產生程式庫檔案的連結以及相依性。

相依性必須是另一個 `cq:ClientLibraryFolder`. 若要識別相依性，請將屬性新增至 `cq:ClientLibraryFolder` 具有下列屬性的節點：

* **名稱：** 相依性
* **型別：** 字串[]
* **值：** 目前程式庫資料夾所依賴之cq：ClientLibraryFolder節點的categories屬性值。

例如， / `etc/clientlibs/myclientlibs/publicmain` 有相依於 `cq.jquery` 資料庫。 參考主要使用者端程式庫的JSP會產生HTML，其中包含下列程式碼：

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### 從其他程式庫內嵌程式碼 {#embedding-code-from-other-libraries}

您可以將使用者端程式庫的程式碼內嵌到另一個使用者端程式庫中。 在執行階段中，內嵌程式庫產生的JS和CSS檔案會包含內嵌程式庫的程式碼。

內嵌程式碼對於存取儲存在存放庫的安全區域中的資料庫很有用。

#### 應用程式專屬的使用者端程式庫資料夾 {#app-specific-client-library-folders}

最佳實務是將所有應用程式相關檔案保留在以下應用程式資料夾中 `/apps`. 拒絕網站訪客存取 `/apps` 資料夾。 若要同時滿足這兩個最佳實務，請在下方建立使用者端程式庫資料夾 `/apps`，並使其可透過Proxy servlet存取，如下所述 [找到使用者端程式庫資料夾並使用Proxy使用者端程式庫Servlet](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet).

使用categories屬性來識別要內嵌的使用者端程式庫資料夾。 若要內嵌程式庫，請在內嵌中新增屬性 `cq:ClientLibraryFolder` 節點，使用下列屬性屬性：

* **名稱：** 內嵌
* **型別：** 字串[]
* **值：** 的categories屬性的值 `cq:ClientLibraryFolder` 要內嵌的節點。

#### 使用內嵌將請求最小化 {#using-embedding-to-minimize-requests}

在某些情況下，您可能會發現發佈執行個體針對典型頁面產生的最終HTML包含相對大量的 `<script>` 元素，特別是您的網站正使用使用者端內容資訊來進行分析或鎖定目標時。 例如，在非最佳化專案中，您可能會找到下列系列 `<script>` 頁面HTML中的元素：

```xml
<script type="text/javascript" src="/etc/clientlibs/granite/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/utils.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/jquery/granite.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/shared.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/personalization/kernel.js"></script>
```

在這種情況下，將所有必要的使用者端程式庫程式碼合併為單一檔案會很有用，這樣就能減少頁面載入時的來回請求數量。 若要這麼做，您可以 `embed` 必要的程式庫會使用「 」的內嵌屬性，將您的應用程式專屬的使用者端程式庫中 `cq:ClientLibraryFolder` 節點。

AEM包含下列使用者端程式庫類別。 您應僅內嵌特定網站運作所需的專案。 不過， **您應維持此處列出的順序**：

1. `browsermap.standard`
1. `browsermap`
1. `jquery-ui`
1. `cq.jquery.ui`
1. `personalization`
1. `personalization.core`
1. `personalization.core.kernel`
1. `personalization.clientcontext.kernel`
1. `personalization.stores.kernel`
1. `personalization.kernel`
1. `personalization.clientcontext`
1. `personalization.stores`
1. `cq.collab.comments`
1. `cq.collab.feedlink`
1. `cq.collab.ratings`
1. `cq.collab.toggle`
1. `cq.collab.forum`
1. `cq.cleditor`

#### CSS檔案中的路徑 {#paths-in-css-files}

內嵌CSS檔案時，產生的CSS程式碼會使用與內嵌程式庫相關的資源路徑。 例如，可公開存取的程式庫 `/etc/client/libraries/myclientlibs/publicmain` 內嵌 `/apps/myapp/clientlib` 使用者端資源庫：

![screen_shot_2012-05-29at20122pm](assets/screen_shot_2012-05-29at20122pm.png)

此 `main.css` 檔案包含下列樣式：

```xml
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

CSS檔案會 `publicmain` 節點會使用原始影像的URL產生包含以下樣式：

```xml
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

### 針對特定行動群組使用資料庫 {#using-a-library-for-specific-mobile-groups}

使用 `channels` 使用者端資料庫資料夾的屬性，用來識別使用該資料庫的行動群組。 此 `channels` 當針對不同裝置功能設計相同類別的程式庫時，屬性會很有用。

若要將使用者端程式庫資料夾與裝置群組建立關聯，請將屬性新增至 `cq:ClientLibraryFolder` 具有下列屬性的節點：

* **名稱：** 頻道
* **型別：** 字串[]
* **值：** 行動群組的名稱。 若要從群組中排除程式庫資料夾，請在名稱前面加上驚歎號(「！」)。

例如，下表列出 `channels` 屬性的每個使用者端資料庫資料夾， `cq.widgets` 類別：

| 使用者端資料庫資料夾 | 管道屬性的值 |
|---|---|
| `/libs/cq/analytics/widgets` | `!touch` |
| `/libs/cq/analytics/widgets/themes/default` | `!touch` |
| `/libs/cq/cloudserviceconfigs/widgets` | `!touch` |
| `/libs/cq/touch/widgets` | `touch` |
| `/libs/cq/touch/widgets/themes/default` | `touch` |
| `/libs/cq/ui/widgets` | `!touch` |
| `/libs/cq/ui/widgets/themes/default` | `!touch` |

<!-- Search&Promote is end of life as of September 1, 2022 | `/libs/cq/searchpromote/widgets` | `!touch` | -->
<!-- Search&Promote is end of life as of September 1, 2022 | `/libs/cq/searchpromote/widgets/themes/default` |*[no value]* -->

## 使用前置處理器 {#using-preprocessors}

AEM支援可插拔的前處理器，並隨附以下支援 [YUI壓縮程式](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) 適用於CSS和JavaScript及 [Google Closure Compiler (GCC)](https://developers.google.com/closure/compiler/) YUI設為AEM預設前置處理器的JavaScript。

可插拔的前處理器可彈性使用，包括：

* 定義可以處理指令碼來源的ScriptProcessors
* 處理器可設定選項
* 處理器可用於縮制，也可用於非縮制的情況
* clientlib可以定義要使用的處理器

>[!NOTE]
>
>依預設，AEM會使用YUI壓縮程式。 請參閱 [YUI Compressor GitHub檔案](https://github.com/yui/yuicompressor/issues) 以取得已知問題的清單。 切換至特定clientlibs的GCC壓縮程式可以解決使用YUI時觀察到的一些問題。

>[!CAUTION]
>
>請勿將縮制的程式庫放入使用者端程式庫中。 改為提供原始程式庫，如果需要縮制，請使用前置處理器的選項。

### 用途 {#usage}

您可以選擇針對每個clientlibrary或系統範圍設定前置處理器組態。

* 新增多值屬性 `cssProcessor` 和 `jsProcessor` 在clientlibrary節點上

* 或透過以下方式定義系統預設設定： **HTML程式庫管理員** OSGi設定

clientlib節點上的前置處理器設定優先於OSGI設定。

### 格式與範例 {#format-and-examples}

#### 格式 {#format}

```xml
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

#### CSS縮制的YUI壓縮程式和JS的GCC {#yui-compressor-for-css-minification-and-gcc-for-js}

```xml
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

#### 輸入指令碼以預先處理，然後使用GCC以縮小和模糊化 {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

```xml
jsProcessor: [
   "default:typescript",
   "min:typescript",
   "min:gcc;obfuscate=true"
]
```

#### 其他GCC選項 {#additional-gcc-options}

```xml
failOnWarning (defaults to "false")
languageIn (defaults to "ECMASCRIPT5")
languageOut (defaults to "ECMASCRIPT5")
compilationLevel (defaults to "simple") (can be "whitespace", "simple", "advanced")
```

如需GCC選項的詳細資訊，請參閱 [GCC檔案](https://developers.google.com/closure/compiler/docs/compilation_levels).

### 設定系統預設縮制器 {#set-system-default-minifier}

YUI已設定為AEM中的預設縮制器。 若要將此變更為GCC，請按照以下步驟操作。

1. 前往Apache Felix Config Manager，網址為 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. 尋找並編輯 **AdobeGraniteHTML程式庫管理員**.
1. 啟用 **最小化** 選項（如果尚未啟用）。
1. 設定值 **JS處理器預設設定** 至 `min:gcc`.

   如果以分號分隔，例如： `min:gcc;obfuscate=true`.

1. 按一下 **儲存** 以儲存變更。

## 偵錯工具 {#debugging-tools}

AEM提供數種用於偵錯和測試使用者端程式庫資料夾的工具。

### 請參閱內嵌檔案 {#see-embedded-files}

若要追蹤內嵌程式碼的來源，或確保內嵌使用者端程式庫產生預期的結果，您可以檢視執行階段內嵌的檔案名稱。 若要檢視檔案名稱，請附加 `debugClientLibs=true` 網頁URL的引數。 產生的程式庫包含 `@import` 陳述式，而非內嵌程式碼。

在上一個範例中 [從其他程式庫內嵌程式碼](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries) 區段， `/etc/client/libraries/myclientlibs/publicmain` client library資料夾內嵌 `/apps/myapp/clientlib` 使用者端資料庫資料夾。 將引數附加至網頁會在網頁的原始程式碼中產生下列連結：

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

開啟 `publicmain.css` file會顯示下列程式碼：

```xml
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. 在網頁瀏覽器的位址方塊中，將下列文字附加至HTML的URL：

   `?debugClientLibs=true`
1. 頁面載入時，檢視頁面來源。
1. 按一下提供為連結元素href的連結，開啟檔案並檢視原始程式碼。

### 探索使用者端資料庫 {#discover-client-libraries}

此 `/libs/cq/granite/components/dumplibs/dumplibs` 元件會產生系統上所有使用者端程式庫資料夾的資訊頁。 此 `/libs/granite/ui/content/dumplibs` 節點將元件作為資源型別。 若要開啟頁面，請使用下列URL （視需要變更主機和連線埠）：

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

資訊包括程式庫路徑和型別（CSS或JS），以及程式庫屬性的值，例如類別和相依性。 頁面上的後續表格會顯示每個類別和管道中的程式庫。

### 檢視產生的輸出 {#see-generated-output}

此 `dumplibs` 元件包含測試選擇器，顯示產生的原始程式碼 `ui:includeClientLib` 標籤之間。 此頁面包含js、css和主題屬性之不同組合的程式碼。

1. 使用下列其中一種方法開啟「測試輸出」頁面：

   * 從 `dumplibs.html` 頁面上，按一下 **按一下這裡進行輸出測試** 文字。

   * 在網頁瀏覽器中開啟下列URL （視需要使用不同的主機和連線埠）：

      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`

   預設頁面顯示沒有categories屬性值的標籤的輸出。

1. 若要檢視類別的輸出，請輸入使用者端程式庫的 `categories` 屬性並按一下 **提交查詢**.

## 設定程式庫處理以進行開發和生產 {#configuring-library-handling-for-development-and-production}

HTML程式庫管理員服務程式 `cq:ClientLibraryFolder` 標籤並在執行階段產生程式庫。 環境的型別（開發或生產）會決定應如何設定服務：

* 提高安全性：停用偵錯
* 提升效能：移除空白並壓縮程式庫。
* 提高可讀性：包含空白字元且請勿壓縮。

如需有關設定服務的資訊，請參閱 [AEMHTML庫管理員](/help/sites-deploying/osgi-configuration-settings.md#aemhtmllibrarymanager).
