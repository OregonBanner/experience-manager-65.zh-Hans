---
title: 互動式通訊編寫UI簡介
seo-title: An introduction to the various user interface elements you can use to author Interactive Communication
description: 介紹您可以用來編寫互動式通訊的各種使用者介面元素
seo-description: An introduction to the various user interface elements you can use to author Interactive Communication
uuid: e8c5b1e8-b2bb-46b4-b42e-1f343192641a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications
discoiquuid: 5855d21b-340c-4139-aabe-c3a534cedb98
docset: aem65
feature: Interactive Communication
exl-id: 3d15a723-df6c-4b4a-992e-a6636f4cf3dc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 14%

---

# 互動式通訊編寫UI簡介{#introduction-to-interactive-communication-authoring-ui}

用於編寫的使用者介面 [互動式通訊](/help/forms/using/interactive-communications-overview.md) 直覺化，並提供下列內容以製作互動式通訊的列印與Web channel：

* 所見即所得拖放檔案編輯器
* 整合式資產存放庫 — 您可透過互動式通訊編寫介面的資產瀏覽器，使用上傳至伺服器並在其上建立的資產

當您 [建立新的互動式通訊或編輯現有的互動式通訊](../../forms/using/create-interactive-communication.md)，您會使用下列使用者介面元素：

* [侧栏](#sidebar)
* [页面工具栏](#page-toolbar)
* [组件工具栏](#component-toolbar)
* 内容区域

![互動式通訊編寫使用者介面](assets/form-editor.png)

**答：** 側欄 **B.** 頁面工具列 **C.** 內容區域

## 侧栏 {#sidebar}

![侧栏](assets/sidebar-comps-2.png)

**答：** 頻道瀏覽器 **B.** 內容瀏覽器 **C.** 屬性瀏覽器 **D.** 資產瀏覽器 **E.** 元件瀏覽器 **F.** 資料來源瀏覽器 — 資料模型 **G.** 資料來源瀏覽器 — 主要內容

<!-- Click to enlarge

![sidebar-comps-3](assets/sidebar-comps-3.png)-->

側邊欄包含下列內容：

* **頻道瀏覽器**

Channel瀏覽器可協助您在互動式通訊的列印與Web通道之間切換。 根據您在管道瀏覽器中選取的管道，「內容」和「元件」等瀏覽器會顯示選項。

* **內容瀏覽器**
在內容瀏覽器中，您可以看到所選管道之檔案的物件階層。 作者可以點選檔案物件樹狀結構中的特定元素，以導覽至該元件。 作者可以在Web Channel中搜尋物件，並從此樹狀結構重新排列物件。

* **属性浏览器**

   可让您编辑组件的属性。屬性會根據元件而變更。 例如，若要檢視檔案容器的屬性：選取元件，然後點選 ![欄位層級](assets/field-level.png) > **檔案容器**，然後點選 ![cmppr](assets/cmppr.png).

* **資產瀏覽器**
區隔不同型別的內容，例如佈局片段、影像、檔案、頁面、影片。 作者可以將資產拖放至互動式通訊中。

* **元件瀏覽器**
包含可用來建置檔案的列印和Web管道的元件。 您可以將元件拖曳至互動式通訊以新增元素，並依需求設定新增的元素。 下表說明「元件」瀏覽器中列出的列印和Web管道元件：

| **Component** | **打印渠道** | **Web 渠道** | **功能** |
|---|---|---|---|
| 图表 | ✓ | ✓ | 新增可在互動式通訊中使用的圖表，以視覺化呈現從表單資料模型集合專案中擷取的二維資料。 |
| 文档片段 | ✓ | ✓ | 可讓您新增可重複使用的元件、文字、清單或條件至互動式通訊。 您新增至互動式通訊的可重複使用元件，可以是表單資料模型式元件，也可以不使用表單資料模型。 |
| 图像 | ✓ | ✓ | 可让您插入图像。 |
| 面板 | - | ✓ | Panel元件是將其他元件分組在一起的預留位置，可控制一組元件在互動式通訊中的配置方式。 面板元件也可讓您讓一組元件對一般使用者可重複，例如在填寫教育憑證所需的多個專案中。 同時，對於具有多個標籤的互動式通訊標籤，最好為每個標籤使用面板。 |
| 表 | &#42; | ✓ | 添加表格以便按行和列整理数据。 |
| 目标区域 | &#42;&#42; | ✓ | 在Web Channel中插入目標區域，以整理Web Channel專用元件。 |
| 文本 | - | ✓ | 新增文字至互動式通訊的Web channel。 文字可利用表單資料模型物件來讓內容成為動態的。 |

&#42; 在列印管道中使用版面片段來新增表格。

&#42;&#42; 在Print channel中，目標區域是在XDP/print範本中預先定義的。 您無法使用互動式通訊編寫UI新增目標區域。

* **資料來源瀏覽器**
資料來源瀏覽器會以您在建立互動式通訊時選取的表單資料模型顯示可用的資料來源。

### 使用元件的關鍵點 {#key-points-for-working-with-components}

使用互動式通訊元件時的要點如下：

* 每個元件都有相關的屬性，這些屬性控制其外觀和功能。 若要設定元件的屬性，請點選元件並點選 ![cmppr](assets/cmppr.png) 以在「屬性」瀏覽器中開啟元件屬性。
* 元件以其元素名稱識別。 點選時 ![cmppr](assets/cmppr.png)，您可以變更屬性瀏覽器中的元素名稱欄位值來變更元件名稱。 「元素名稱」欄位僅接受字母、數字、連字型大小(-)和底線(_)。 不允許使用其他特殊字元，元素名稱應以字母開頭。
* 只要互動式通訊的標題可見，您就可以在編輯器中修改內嵌互動式通訊元件的Title屬性，而無需開啟Properties瀏覽器。 若要這麼做：

   1. 點選以選取具有Title屬性且已停用Hide title屬性的元件。
   1. 點選 ![aem_6_3_edit](assets/aem_6_3_edit.png) 讓標題可編輯。

   1. 修改標題並點選Return鍵，或點選元件之外的任意位置以儲存變更。 點選Esc鍵以捨棄變更。

## 组件工具栏 {#component-toolbar}

![元件工具列標籤](do-not-localize/component_toolbar_labels_new.png)

選取元件時，您會看到可讓您使用它的工具列。 您可以获得用于剪切、粘贴、移动和指定组件属性的选项。您的选项包括：

A. **配置**：在点按&#x200B;**配置**&#x200B;时，组件属性将显示在侧栏中。

B.**編輯規則**：點選「編輯規則」時，會出現「規則編輯器」，您可在此編輯和建立所選元件的規則。 在規則編輯器中，您也可以選取其他表單物件（元件）並編輯/建立這些表單物件的規則。

C.**複製**：您可以使用複製選項來複製元件，並將其貼到互動式通訊的其他位置。

D.**剪下**：您可以使用剪下選項在互動式通訊中將元件從一個位置移動到另一個位置。

E. **刪除**：可讓您從互動式通訊中刪除元件。

F. **插入元件**：可讓您在選取的元件上方插入元件。

G. **貼上**：可讓您貼上使用上述選項剪下或複製的元件。

H. **分组**：可让您选择多个组件（如果要剪切、复制或粘贴多个组件）。

I **父项**：可让您选择组件的父项。

J. **檢視SOM運算式：** 可讓您檢視 [SOM運算式](../../forms/using/using-som-expressions-adaptive-forms.md) 用於元件。

K： **面板中的群組物件：** 可讓您將元件群組在面板中，以便同時對這些元件執行操作。 如需詳細資訊，請參閱 [面板中的群組物件](create-interactive-communication.md#groupobjectspanel).

L. **新增子面板** （僅適用於面板）：可讓您將子面板新增至面板。

M： **新增面板工具列** （僅適用於面板）：可讓您新增面板元件的工具列。 您接著可以在工具列上執行進一步的動作。

此外， **Replace** 工具列上的選項可讓您以替代元件取代現有元件。 選項不適用於面板元件。

## 页面工具栏 {#page-toolbar}

上方的「頁面」工具列提供可讓您預覽互動式通訊並變更其屬性的選項。 您可以在編寫互動式通訊時加以預覽，並據以變更。 在页面工具栏中，您会看到：

* 切换侧面板![toggle-side-panel](assets/toggle-side-panel.png)：可让您显示或隐藏侧栏。
* 頁面資訊 ![pageinformationad](assets/pageinformationad.png)：可讓您檢視頁面屬性。
* 模擬器 ![尺標](assets/ruler.png)：可讓您針對不同的顯示器大小（例如平板電腦和手機），模擬互動式通訊的外觀。
* 编辑：可让您选择其他模式，例如：编辑、样式、开发人员和设计。

   * 編輯：可讓您編輯互動式通訊及其元件的屬性。 例如，添加组件、删除图像和指定必填字段。
   * 樣式：可讓您為互動式通訊的元件外觀設定樣式。 例如，在样式模式下，您可以选择一个面板并指定其背景颜色。
   * 开发人员：可让开发人员：

      * 探索互動式通訊由哪些部分組成。
      * 调试何时何地发生的情况，这反过来有助于解决问题。
   * Target：可讓您啟用或停用自訂元件，或是未列在側欄中的現成可用元件。


* 預覽：可讓您預覽互動式通訊在發佈時的外觀。
