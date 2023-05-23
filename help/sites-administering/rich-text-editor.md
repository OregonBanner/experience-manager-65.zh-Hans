---
title: 設定RTF編輯器以在Adobe Experience Manager中編寫內容。
description: 瞭解如何設定Adobe Experience Manager RTF編輯器，以在Adobe Experience Manager中編寫內容。
contentOwner: AG
exl-id: 2e7ec22f-0856-44c4-bb15-1086dae0b85a
source-git-commit: 53a18ec48331f1c25c15e8f7a59bd57e95639895
workflow-type: tm+mt
source-wordcount: '2924'
ht-degree: 1%

---

# 設定RTF編輯器 {#configure-the-rich-text-editor}

RTF編輯器(RTE)為作者提供廣泛的功能來編輯其文字內容。 提供圖示、選取方塊、工具列和選單以提供「所見即所得」文字編輯體驗。

若要瞭解如何使用RTE功能進行編寫，請參閱 [使用RTF編輯器進行編寫](/help/sites-authoring/rich-text-editor.md). RTE可以設定為啟用、停用及擴充編寫元件中可用的功能。 下列工作流程說明在Experience Manager中完成RTE設定工作的建議順序。

![瞭解如何設定RTE的一系列步驟](assets/rte_workflow_v1.png)

*圖：瞭解如何設定RTE的步驟順序*

## 瞭解觸控式UI和傳統UI {#understand-touch-enabled-ui-and-classic-ui}

觸控式UI是Experience Manager的標準使用者介面。 Adobe推出觸控式UI，包含 [回應式設計](/help/sites-authoring/responsive-layout.md) 用於製作環境。 觸控式UI專為觸控和桌上型裝置而設計。 介面與原始傳統UI有很大差異。

![觸控式使用者介面中的RTF編輯器工具列](assets/chlimage_1-35.png)

*圖：觸控式UI中的RTF編輯器工具列*

![傳統UI中的RTF編輯器工具列](assets/rtedefault.png)

*圖：傳統UI中的RTF編輯器工具列*

>[!MORELIKETHIS]
>
>* [UI建議](/help/sites-deploying/ui-recommendations.md)
>* 關於淘汰傳統UI，請參閱 [Experience Manager 6.5發行說明](/help/release-notes/deprecated-removed-features.md)
>* 如需UI之間的差異，請參閱 [Touch UI和Classic UI](https://aemcq5pedia.wordpress.com/2018/01/05/touch-enabled-ui-aem6-3/)
>* 若要深入瞭解觸控式UI，請參閱 [Experience Manager觸控式UI的概念](/help/sites-developing/touch-ui-concepts.md)


## 各種編輯模式 {#editingmodes}

作者可以使用不同的元件模式，在Experience Manager中建立和編輯文字內容。 製作和格式化內容的工具列選項，以及不同編輯模式下RTE啟用元件的使用者體驗，會因RTE設定而異。

| 編輯模式 | 編輯區域 | 建議啟用的功能 | 触屏 UI | 经典 UI |
|--- |--- |--- |--- |--- |
| 内嵌 | 就地編輯以進行快速、次要的編輯；格式化而不開啟對話方塊 | 最少的RTE功能 | Y | Y |
| RTE全熒幕 | 涵蓋整個頁面 | 所有必要的RTE功能 | Y | N |
| 对话框 | 對話方塊位於頁面內容上方，但不涵蓋整個頁面 | 傳統UI中的所有必要RTE功能；謹慎地在觸控式UI中啟用功能 | Y | Y |
| 對話方塊全熒幕 | 與全熒幕模式相同；包含對話方塊的欄位以及RTE | 所有必要的RTE功能 | Y | N |

>[!NOTE]
>
>觸控式UI中的內嵌編輯模式無法使用來源編輯功能。 您無法在全熒幕模式中拖曳影像。 所有其他功能在所有模式中皆可運作。

### 內嵌編輯 {#inline-editing}

開啟時（緩慢點選/按一下），可在頁面內編輯內容。 將顯示包含非常基本選項的精簡工具列。

![觸控式UI中使用基本工具列的內嵌編輯](assets/chlimage_1-36.png)

*圖：觸控式UI中使用基本工具列的內嵌編輯*

在傳統UI中，只要在元件上緩慢連按兩下，即可內嵌編輯，橘色外框會反白顯示內容。 如果「內容尋找器」已開啟，視窗頂端會顯示具有可用RTE格式選項的工具列。 如果「內容尋找器」未開啟，則格式選項不會顯示，而且您只能編輯基本文字。

### 全熒幕編輯 {#full-screen-editing}

Experience Manager元件可在全熒幕檢視中開啟，以隱藏頁面內容並佔用可用熒幕。 請考慮全熒幕編輯內嵌編輯的詳細版本，因為它提供最多的編輯選項。 按一下「 」即可開啟 ![rte_fullscreen](assets/rte_fullscreen.png)，使用內聯編輯模式時可從壓縮工具列移除。

在對話方塊全熒幕模式以及詳細的RTE工具列中，對話方塊中可用的選項和元件也可用。 它僅適用於包含RTE以及其他元件的對話方塊。

![在觸控式UI中以全熒幕模式編輯時的詳細RTE工具列](assets/chlimage_1-37.png)

*圖：在觸控式UI中以全熒幕模式編輯時的詳細RTE工具列*

### 對話方塊編輯 {#dialog-editing}

連按兩下元件時，會開啟對話方塊以編輯內容。 對話方塊會在現有頁面上方開啟。 在某些特定情況下，對話方塊會以快顯視窗開啟。 例如，當文字元件屬於多欄頁面配置中的欄時，可用於對話方塊的區域較少。

![觸控式UI中的對話方塊編輯模式](assets/dialog_editing_modetouchui.png)

*圖：觸控式UI中的對話方塊編輯模式*

![傳統UI中的對話方塊，其中包含用於編輯的詳細工具列](assets/chlimage_1-38.png)

*圖：傳統UI中的對話方塊，其中包含用於編輯的詳細工具列*

## 關於RTE外掛程式和相關功能 {#aboutplugins}

此功能透過一系列外掛程式提供，每個外掛程式具有：

* A `features` 屬性：

   * 用於啟動或停用該外掛程式的基本功能
   * 可使用標準化的程式進行設定

* 適當時，需要專門設定的其他屬性和選項。

RTE的基本功能會由的值啟用或停用 `features` 屬性（在適當的外掛程式特定的節點上）。

下表列出目前的外掛程式，其中顯示：

* 包含API檔案連結的外掛程式ID。 ID在下列情況下會作為節點名稱使用： [啟用外掛程式](/help/sites-administering/configure-rich-text-editor-plug-ins.md#activateplugin).
* 允許的值 `features` 屬性。
* 外掛程式所提供功能的說明。

| 外掛程式ID | 功能 | 描述 |
|--- |--- |--- |
| 编辑 | 剪下copy paste-default paste-plaintext paste-wordhtml | [剪下、複製和三種貼上模式](/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles). |
| findreplace | 尋找取代 | 查找并替换. |
| 格式 | 粗斜體底線 | [基本文字格式](/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles). |
| 图像 | 图像 | 基本影像支援（從內容或內容尋找器拖曳）。 根據瀏覽器的不同，支援對作者有不同的行為 |
| 金鑰 |  | 若要定義此值，請參閱 [索引標籤大小](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tabsize). |
| 左右對齊 | justifyleft justifycenter justifyright | 段落對齊方式。 |
| 連結 | modifylink取消連結錨點 | [超連結和錨點](/help/sites-administering/configure-rich-text-editor-plug-ins.md#linkstyles). |
| 清單 | 已排序的無序縮排縮排 | 此外掛程式會同時控制兩者 [縮排和清單](/help/sites-administering/configure-rich-text-editor-plug-ins.md#indentmargin)；包括巢狀清單。 |
| misctools | specialchars sourceedit | 其他工具可讓作者輸入 [特殊字元](/help/sites-administering/configure-rich-text-editor-plug-ins.md#spchar) 或編輯HTML來源。 此外，您也可以新增整個 [特殊字元範圍](/help/sites-administering/configure-rich-text-editor-plug-ins.md#definerangechar) 如果您想要定義自己的清單。 |
| 引數格式 | 引數格式 | 預設段落格式為段落、標題1、標題2和標題3 (`<p>`， `<h1>`， `<h2>`、和 `<h3>`)。 您可以 [新增更多段落格式](/help/sites-administering/configure-rich-text-editor-plug-ins.md#paraformats) 或擴充清單。 |
| 拼字檢查 | 核取文字 | [語言感知拼字檢查程式](/help/sites-administering/configure-rich-text-editor-plug-ins.md#adddict). |
| 樣式 | 樣式 | 支援使用CSS類別設定樣式。 [新增文字樣式](/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles) 如果您想要新增（或擴充）自己的樣式範圍，以便與文字搭配使用。 |
| 下標 | 下標上標 | 基本格式的擴充功能，可新增子指令碼和超級指令碼。 |
| 表格 | 表格removetable insertrow removerow insertcolumn removecolumn cellprops mergecells splitcell selectrow selectcolumns | 另請參閱 [設定表格樣式](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tablestyles)，如果您想要為整個表格或個別儲存格新增自己的樣式。 |
| 撤消 | 復原重做 | 歷史記錄大小 [還原和重做](/help/sites-administering/configure-rich-text-editor-plug-ins.md#undohistory) 作業。 |

>[!NOTE]
>
>對話方塊模式不支援全熒幕外掛程式。 使用 `dialogFullScreen` 設定以設定全熒幕模式的工具列。

## 瞭解設定路徑和位置 {#understand-the-configuration-paths-and-locations}

此 [RTE編輯模式（和UI）](#editingmodes) 由您提供給作者的資料，在您決定組態詳細資訊的位置 [啟用RTE外掛程式](/help/sites-administering/configure-rich-text-editor-plug-ins.md#activateplugin)：

| 編輯模式 | 觸控式UI的位置 | 傳統UI的位置 |
|---|---|---|
| 内嵌 | `cq:editConfig/cq:inplaceEditing` | `cq:editConfig/cq:inplaceEditing` |
| 全熒幕 | `cq:editConfig/cq:inplaceEditing` | 不适用 |
| 对话框 | `cq:dialog` | `dialog` |
| 全熒幕對話方塊 | `cq:dialog` | 不适用 |

>[!NOTE]
>
>不要將節點命名為 `cq:inplaceEditing` 作為 `config`. 開啟 `cq:inplaceEditing` 節點，定義下列屬性：
>* **名称**: `configPath`
>* **类型**: `String`
>* **值**：包含實際設定的節點路徑
>
>不要將RTE設定節點命名為 `config`. 否則，RTE設定只會對管理員生效，而不會對群組中的使用者生效 `content-author`.

設定以下屬性，這些屬性只適用於觸控式UI中的對話方塊編輯模式：

* `useFixedInlineToolbar`：設定此RTE節點上定義的布林值屬性(具有sling：resourceType= `cq/gui/components/authoring/dialog/richtext`)至 `True`，以使RTE工具列固定，而非浮動。

   此屬性為true時，RTF編輯預設會在「foundation-contentloaded」事件上啟動。

   若要防止此情況，請設定屬性 `customStart` 至 `True`並觸發&#39;rte-start&#39;事件以開始RTE編輯。 當此屬性為「true」時，預設行為（按一下即啟動rte）無法運作。

* `customStart`：將此在RTE節點上定義的布林值屬性設定為 `True`，以透過觸發事件來控制何時開始RTE `rte-start`.

* `rte-start`：在上觸發此事件 `contenteditable-div` RTE時，開始編輯RTE的時間。 此設定僅適用於 `customStart` 已設定為true。

在觸控式對話方塊中使用RTE時，請設定屬性 `useFixedInlineToolbar` 為true是避免問題的必要專案。

## 自訂就地編輯 {#customizing-in-place-editing}

您可以透過設定以下屬性來定義文字編輯器從哪個HTML選擇器開始：

* **`editElementQuery`**  — 定義於 `cq:InplaceEditingConfig`，此屬性用於指定會在其上開始文字元件內嵌編輯的HTML元素選取器。 如果未指定，內嵌編輯會直接在文字元件HTML上啟動。
* **`textPropertyName`**  — 定義於 `cq:InplaceEditingConfig`，此屬性用於指定將儲存在內容節點上的屬性名稱，其中文字元件的HTML值將在內聯編輯後持續存在。

對話方塊模式的對應屬性為 `name`.

## 透過啟用外掛程式來啟用RTE功能 {#enable-rte-functionalities-by-activating-plug-ins}

RTE功能可透過一系列外掛程式提供，每個外掛程式都具備功能屬性。 您可以設定features屬性，以啟用或停用每個外掛程式的各種功能。

如需RTE外掛程式的詳細設定，請參閱 [如何啟動和設定RTE外掛程式](/help/sites-administering/configure-rich-text-editor-plug-ins.md).

**範例**：下載 [此範例設定](/help/sites-administering/assets/rte-sample-all-features-enabled-10.zip) 說明如何設定RTE。 在此套件中，所有功能皆已啟用。

>[!NOTE]
>
>此 [核心元件文字元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html?lang=en#the-text-component-and-the-rich-text-editor) 可讓範本編輯器在GUI中設定許多RTE外掛程式作為內容原則，而不需要技術設定。 內容原則可搭配使用RTE UI設定，如本檔案所述。
>
>如需詳細資訊，請參閱 [RTE UI設定和內容原則](/help/sites-administering/rich-text-editor.md) 以及本檔案的區段 [建立頁面範本](/help/sites-authoring/templates.md) 和 [核心元件開發人員檔案](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html).

>[!NOTE]
>
>為了方便參考，您可以在下列位置找到預設文字元件（作為標準安裝的一部分提供）：
>
>* `/libs/wcm/foundation/components/text`
>* `/libs/foundation/components/text`
>
>若要建立自己的文字元件，請複製上述元件，而非編輯這些元件。

## 設定RTE工具列 {#dialogfullscreen}

AEM可讓您針對不同的編輯模式，以不同方式設定RTF編輯器的介面。 以下提供預設設定。 您可以根據需求覆寫這些預設值。 您只需自訂要提供給作者的工具列功能。 您不需要指定所有工具列設定。

若要設定工具列 `dialogFullScreen`，使用下列範例設定。

```java
<uiSettings jcr:primaryType="nt:unstructured">
  <cui jcr:primaryType="nt:unstructured">
    <inline
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,#justify,#lists,links#modifylink,links#unlink,#paraformat]">
      <popovers jcr:primaryType="nt:unstructured">
        <justify
          jcr:primaryType="nt:unstructured"
          items="[justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify]"
          ref="justify"/>
        <lists
          jcr:primaryType="nt:unstructured"
          items="[lists#unordered,lists#ordered,lists#outdent,lists#indent]"
          ref="lists"/>
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </inline>
    <dialogFullScreen
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify,lists#unordered,lists#ordered,lists#outdent,lists#indent,links#modifylink,links#unlink,table#createoredit,#paraformat,image#imageProps]">
      <popovers jcr:primaryType="nt:unstructured">
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </dialogFullScreen>
    <tableEditOptions
      jcr:primaryType="nt:unstructured"
      toolbar="[table#insertcolumn-before,table#insertcolumn-after,table#removecolumn,-,table#insertrow-before,table#insertrow-after,table#removerow,-,table#mergecells-right,table#mergecells-down,table#mergecells,table#splitcell-horizontal,table#splitcell-vertical,-,table#selectrow,table#selectcolumn,-,table#ensureparagraph,-,table#modifytableandcell,table#removetable,-,undo#undo,undo#redo,-,table#exitTableEditing,-]">
    </tableEditOptions>
  </cui>
</uiSettings>
```

內嵌模式和全熒幕模式會使用不同的UI設定。 toolbar屬性用於指定工具列的按鈕。

例如，如果按鈕本身是功能(例如， `Bold`)，則指定為 `PluginName#FeatureName` (例如， `links#modifylink`)。

如果按鈕是彈出視窗（包含外掛程式的部分功能），則會指定為 `#PluginName` (例如， `#format`)。

分隔符號(`|`)之間，您可以透過以下方式指定： `-`.

內嵌或全熒幕模式下的彈出式節點包含所使用的彈出視窗清單。 「彈出視窗」節點下的每個子節點都會以外掛程式（例如格式）命名。 其屬性「items」包含外掛程式的功能清單（例如format#bold）。

## RTE使用者介面設定和內容原則 {#rtecontentpolicies}

管理員可以使用內容原則來控制RTE選項，而不是如上所述進行設定。 內容原則在作為元件的一部分使用時，會定義元件的設計屬性 [可編輯的範本](/help/sites-authoring/templates.md). 例如，如果使用RTE的文字元件搭配可編輯的範本使用，則內容原則可定義粗體選項可供使用，而一些段落格式選項可供使用。 內容原則可重複使用，並可套用至多個範本。

RTE中可用的選項會從使用者介面設定向下流向內容原則。

* 使用者介面組態設定會定義哪些選項可供內容原則使用。
* 如果RTE的使用者介面設定已移除或未啟用專案，則內容原則無法進行設定。
* 作者只能存取使用者介面設定和內容原則所提供的功能。

例如，您可以看到 [文字核心元件檔案](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/text.html?lang=en#the-text-component-and-the-rich-text-editor).

## 自訂工具列圖示和命令之間的對應 {#iconstoolbar}

您可以自訂RTE工具列上顯示的Coral圖示與可用指令之間的對應。 除了Coral圖示以外，您無法使用任何其他圖示。

1. 建立名為的節點 `icons` 在 `uiSettings/cui`.

1. 為下方的個別圖示建立節點。
1. 在每個圖示節點上，指定Coral圖示和對應至圖示的命令。

以下是將命令Bold對應到Coral圖示（命名為）的範常式式碼片段 `textItalic`.

```java
<text jcr:primaryType="nt:unstructured" sling:resourceType="cq/gui/components/authoring/dialog/richtext" name="./text" useFixedInlineToolbar="{Boolean}true">
    <rtePlugins jcr:primaryType="nt:unstructured">
        <format jcr:primaryType="nt:unstructured" features="bold,italic"/>
    </rtePlugins>
    <uiSettings jcr:primaryType="nt:unstructured">
        <cui jcr:primaryType="nt:unstructured">
            <inline jcr:primaryType="nt:unstructured"
                toolbar="[format#bold,format#italic,format#underline,links#modifylink,links#unlink]">
            </inline>
            <icons jcr:primaryType="nt:unstructured">
                <bold jcr:primaryType="nt:unstructured"
                    command="format#bold"
                    icon="textItalic"/>
            </icons>
        </cui>
    </uiSettings>
</text>
```

## 切換至CoralUI 2 RTF編輯器 {#switch-to-coralui-rich-text-editor}

在頁面上，您可以包含CoralUI 2 RTE clientlib或CoralUI 3 RTE clientlib。 依預設，RTF編輯器包含CoralUI 3 RTE clientlib。 若要切換至CoralUI 2 RTE，請執行下列步驟。

>[!NOTE]
>
>Adobe不建議將此作為最佳實務。 最後選擇切換至CoralUI 2 RTE。 如果外掛程式不依賴RTE內部元件（例如類別），CoralUI 2 RTE的自訂外掛程式可搭配CoralUI 3 RTE使用。
>
>如果您使用CoralUI3 RTE的自訂外掛程式，請使用 `rte.coralui3` 資料庫。


1. 覆蓋節點 `/libs/cq/gui/components/authoring/editors/clientlibs/core` 在 `/apps`，並執行下列動作：

   * Replace `rte.coralui3` 替換為 `rte.coralui2` 相依性屬性的。
   * Replace `cq.authoring.editor.core.inlineediting.rte.coralui3` 替換為 `cq.authoring.editor.core.inlineediting.rte.coralui2` （內嵌屬性）。
   * Replace `cq.authoring.rte.coralui3` 替換為 `cq.authoring.rte.coralui2` （內嵌屬性）。

1. 覆蓋節點 `/libs/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui3` 和 `/libs/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui2` 在 `/apps`.

   移除類別 `cq.authoring.dialog` 從 `/apps/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui3` 並將其新增至 `/apps/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui2`.

1. 從變更要包含在頁面上的任何其他相依性 `rte.coralui3` 至 `rte.coralui2`. 例如，重疊節點之後 `/libs/mcm/campaign/components/touch-ui/clientlibs/rte` 在 `/apps`，從變更任何相依性 `rte.coralui3` 至 `rte.coralui2`.

1. 覆蓋節點 `cq/ui/widgets` 在 `/apps`. 取代相依性 `cq.rte` 在節點 `/apps/cq/ui/widgets` 替換為 `cq.coralui2.rte`.

>[!NOTE]
>
>CoralUI 2 RTE使用Handlebars範本來進行外掛程式對話。 因此，CoralUI 2 RTE clientlib依賴handlebars clientlib。 CoralUI 3 RTE不使用Handlebars範本，且沒有任何關聯的相依性。 如果您的自訂外掛程式使用handlebars範本，請在網頁中包含handlebars clientlib。

## 更多信息 {#further-information}

如需設定RTE的詳細資訊，請參閱 [AEM Widget API](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.RichText) 參考資料。

具體來說，若要檢視外掛程式和可用的相關選項：

* 此 [CQ.form.Rtf](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.RichText) 元件提供表單欄位，用於編輯樣式化文字資訊(RTF)。 若要瞭解RTF表單可用的所有引數，請參閱設定選項。
* RTF元件使用下列外掛程式提供多種功能 [CQ.form.rte.plugins.Plugin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin). 對於每個外掛程式：

   * 如需可啟用（或停用）功能的詳細資訊，請參閱功能
   * 如需適當外掛程式的詳細設定資訊，請參閱所有可用引數的設定選項

* 您也可以參閱連結的HTML規則詳細資訊。

這些資料可用於擴充和自訂您自己的RTE。 例如，若要在建立連結時列出頁面中可用的錨點，您可以提供自己的實施 `LinkPlugin`.

## 已知限制 {#known-limitations}

AEM RTE功能有下列限制：

* 只有AEM元件對話方塊才支援RTE功能。 精靈或類似的Foundation表單不支援RTE [頁面屬性](/help/sites-developing/page-properties-views.md) 和 [支架](/help/sites-authoring/scaffolding.md) 觸控式UI上。

* AEM無法運作 [混合式裝置](/help/release-notes/release-notes.md).

* 不要命名RTE設定節點 `config`. 否則，RTE設定只會對管理員生效，而不會對群組中的使用者生效 `content-author`.

* RTE不支援內嵌內容的內嵌框架或iframe。

## 最佳作法和秘訣 {#best-practices-and-tips}

* 僅啟用浮動對話方塊的外掛程式，而不使用快顯視窗。 沒有快顯視窗的外掛程式尺寸較小，最適合用於浮動對話方塊。
* 透過較大的快顯視窗啟用外掛程式，例如 `Paste` 外掛程式，僅適用於全熒幕對話方塊模式或全熒幕模式。 具有大型快顯視窗的外掛程式需要更多熒幕空間，以提供良好的撰寫體驗。
* 如果您使用CoralUI3 RTE的自訂外掛程式，請使用 `rte.coralui3` 資料庫。

## 疑難排解RTE的常見問題 {#troubleshoot-issues-with-aem-rich-text-editor}

**如何選取多個表格儲存格？**

若要選取表格中的多個儲存格，請按 `Ctrl` 或 `Cmd` 鍵，然後逐一按一下表格儲存格。

現在對選取範圍執行操作，例如設定所選儲存格的屬性。

**使用「設定」按鈕編輯元件時超連結遺失**

使用「設定」按鈕編輯文字元件，以新增超連結。 再次編輯超連結並再次驗證超連結時，您可能會遺失超連結。

因應措施是在第二次顯示「編輯」對話方塊時按一下文字元件，然後執行連結驗證。

此問題已在AEM 6.3及更高版本中解決。

**在來源編輯模式中新增的HTML內容會遺失**

請勿新增易發XSS的HTML。 AEM而非RTE可能會移除一些HTML內容，以遵守XSS反霧狀規則。

若要確認已貼上的HTML是否已儲存，請檢查CRXDE中儲存的內容（在內容節點中）。

如果未儲存，則HTML必須已由RTE移除，因為它不符合RTE的規則。

如果儲存在CRXDE中但未在頁面上轉譯(若要檢查轉譯，請參閱頁面的 [預覽](/help/sites-authoring/editing-content.md#preview-mode)，則會被AEM XSS規則移除。

**多欄位元件未按預期運作**

若要建立多欄位元件，請專門使用CoralUI 3。 請勿使用CoralUI 2元件對話方塊。

此外，請確認您的多欄位實作程式碼和節點結構正確。

**作者無法取得管理員可用的設定**

如果反映管理員的介面設定更新，但不反映作者帳戶的介面設定更新，請確保未命名設定節點 `config`. 使用 [`configPath` 屬性](/help/sites-developing/components-basics.md#cq-inplaceediting).

>[!MORELIKETHIS]
>
>* [設定RTE外掛程式](configure-rich-text-editor-plug-ins.md)
>* [使用RTF編輯器進行編寫](../sites-authoring/rich-text-editor.md)
>* [為可存取的網站設定RTE](rte-accessible-content.md)
>* [Touch UI和Classic UI功能比較](../release-notes/touch-ui-features-status.md)
>* [建立複合多欄位元件的教學課程範例](https://experience-aem.blogspot.com/2019/05/aem-65-touchui-composite-multifield-with-coral3-rte-rich-text.html)

