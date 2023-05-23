---
title: 建立互動式通訊
seo-title: Create an Interactive Communication
description: 使用互動式通訊編輯器建立互動式通訊。 使用拖放功能來建立互動式通訊，並預覽不同裝置型別上的列印和Web輸出。
seo-description: Create an Interactive Communication using the Interactive Communication editor. Use drag-and-drop functionality to build the Interactive Communication, and preview both print and web outputs on different device types.
uuid: d524a3de-00b4-444f-b3c7-be443fa24ec8
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f4d98cb9-84d8-4735-91d2-b9ceec861e5e
docset: aem65
feature: Interactive Communication
exl-id: 1f89c3bf-e67e-4d13-9285-3367be1ac8f8
source-git-commit: 92092e1c050c9264c19e3cd9da9b240607af7bab
workflow-type: tm+mt
source-wordcount: '6178'
ht-degree: 1%

---

# 建立互動式通訊{#create-an-interactive-communication}

## 概述 {#overview}

互動式通訊可集中處理及管理個人化互動式信函的建立、集合及傳遞。 利用列印作為網頁的主通道，您可以在建立互動式通訊的網頁輸出時最小化重複工作。

### 前提条件 {#prerequisites}

建立互動式通訊的先決條件如下：

* 設定 [表單資料模型](/help/forms/using/data-integration.md) 包含測試資料或使用實際資料來源，例如Microsoft® Dynamics的例項。
* 確保您擁有 [檔案片段](/help/forms/using/document-fragments.md).
* 確定您擁有 [列印和Web Channel的範本](/help/forms/using/web-channel-print-channel.md).
* 確保您具備所需的 [主題](/help/forms/using/themes.md) （適用於web channel）。

## 创建交互式通信 {#createic}

1. 登入AEM編寫執行個體並導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 點選 **[!UICONTROL 建立]** 並選取 **[!UICONTROL 互動式通訊]**. 「建立互動式通訊」頁面隨即顯示。

   ![create-interactive-communication](assets/create-interactive-communication.png)

1. 輸入下列資訊。 : 

   * **[!UICONTROL 標題]**：輸入互動式通訊的標題。
   * **[!UICONTROL 名稱]**：互動式通訊的名稱是從您輸入的標題衍生而來。 如有需要，請加以編輯。
   * **[!UICONTROL 說明]**：輸入互動式通訊的說明。
   * **[!UICONTROL 表單資料模型]**：瀏覽並選取表單資料模型。 如需表單資料模型的詳細資訊，請參閱 [AEM Forms資料整合](/help/forms/using/data-integration.md).

   * **[!UICONTROL 預填服務]**：選取預填服務以擷取資料並預填互動式通訊。
   * **[!UICONTROL 後處理型別]**：您可以選取AEM或Forms工作流程，以便在提互動動式通訊時觸發。 選取要觸發的工作流程型別。

   * **[!UICONTROL 後處理]**：選取要觸發的工作流程名稱。 選取AEM工作流程時，請提供附件路徑、版面配置路徑、PDF路徑、列印資料路徑和網頁資料路徑。
   * **[!UICONTROL 標籤]**：選取要套用至互動式通訊的標籤。 您也可以輸入新的/自訂標簽名稱，然後按Enter建立它。
   * **[!UICONTROL 作者]**：作者名稱會自動從登入使用者的使用者名稱中取得。
   * **[!UICONTROL 發佈日期：]** 輸入發佈互動式通訊的日期。
   * **[!UICONTROL 取消發佈日期]**：輸入取消發佈互動式通訊的日期。

1. 點選 **[!UICONTROL 下一個]**. 指定列印和Web Channel詳細資訊的畫面會出現。
1. 輸入下列內容：

   * **[!UICONTROL 列印]**：選取此選項可產生互動式通訊的列印通道。
   * **[!UICONTROL 列印範本]**：瀏覽並選取XDP作為列印範本。
   * **[!UICONTROL Web]**：選取此選項可產生互動式通訊的Web channel或回應式輸出。
   * **[!UICONTROL 互動式通訊Web範本]**：瀏覽並選取Web範本。
   * **[!UICONTROL 主題]** 和 **[!UICONTROL 選取主題]**：瀏覽並選取主題，為互動式通訊的Web channel設定樣式。 如需詳細資訊，請參閱 [AEM Forms中的主題](/help/forms/using/themes.md).

   * **[!UICONTROL 針對Web Channel使用「列印為主版」]**：選取此選項可建立與列印頻道同步的網頁頻道。 使用列印頻道作為Web Channel的主版，可確保從Web Channel衍生出Web Channel的內容和資料繫結，當您點選「同步」時，在列印頻道中所做的變更會反映在Web Channel中。 不過，作者可視需要中斷Web Channel中特定元件的繼承。 如需詳細資訊，請參閱 [將Web channel與Print channel同步](../../forms/using/create-interactive-communication.md#synchronize).
如果您選取 **[!UICONTROL 針對Web Channel使用「列印為主版」]** 選項，您可以選取下列任何模式來產生Web Channel：

      * **[!UICONTROL 自動配置]**：選取此模式可自動從Print channel產生Web channel的預留位置、內容和資料繫結。
      * **[!UICONTROL 手動組織]**：選取此模式以手動選取Print channel元素，並使用 **[!UICONTROL 資料來源]** 標籤。 如需詳細資訊，請參閱 [選取「列印管道元素」以建立Web channel內容](#selectprintchannelelements).

   如需有關列印管道和網頁管道的詳細資訊，請參閱 [列印管道和網頁管道](/help/forms/using/web-channel-print-channel.md).

1. 點選 **[!UICONTROL 建立]**. 隨即建立互動式通訊，並出現警示方塊。 點選 **[!UICONTROL 編輯]** 開始建立互動式通訊的內容，如中所述 [使用互動式通訊編寫使用者介面新增內容](#step2). 或者，您也可以點選 **[!UICONTROL 完成]** 並選擇稍後編輯互動式通訊。

## 新增內容至互動式通訊 {#step2}

建立互動式通訊後，您可以使用互動式通訊編寫介面來建構其內容。

如需互動式通訊編寫介面的詳細資訊，請參閱 [互動式通訊撰寫簡介](/help/forms/using/introduction-interactive-communication-authoring.md).

1. 當您點選「編輯」時，會啟動互動式通訊編寫介面，如中所述 [建立互動式通訊](#createic). 或者，您也可以導覽至AEM上現有的互動式通訊資產，選取該資產，然後點選 **[!UICONTROL 編輯]** 以啟動互動式通訊編寫介面。

   依預設，除非互動式通訊是僅限Web-channel，否則互動式通訊的列印頻道會出現。 互動式通訊的「列印」頻道會顯示目標區域，如所選XDP/列印頻道範本中所提供。 在這些目標區域和欄位中，您可以新增元件或資產。

1. 選取列印管道後，選取 **[!UICONTROL 元件]** 標籤。 列印頻道中有以下元件：

   | **Component** | **功能** |
   |---|---|
   | 图表 | 新增可在互動式通訊中使用的圖表，以視覺化呈現從表單資料模型集合中擷取的二維資料。 如需詳細資訊，請參閱 [在互動式通訊中使用圖表](/help/forms/using/chart-component-interactive-communications.md). |
   | 文档片段 | 可讓您將可重複使用的元件（例如文字、清單或條件）新增至互動式通訊。 新增的元件能以表單資料模型為基礎，或不含表單資料模型。 |
   | 图像 | 可让您插入图像。 |

   將元件拖放至互動式通訊中，並視需要加以設定。

   您也可以在為列印和Web頻道編寫互動式通訊時，使用還原和重做操作。

   使用復原操作可捨棄最後執行的動作，而重做操作可再次納入捨棄的動作。 例如，如果您已在互動式通訊中插入影像或建立資料繫結，且需要捨棄該影像，請使用復原操作。

   ![還原重做動作](assets/undo_redo_actions_new.png)

   「還原」和「重做」選項會顯示在編寫UI頁面工具列上。 復原選項只會在執行動作後顯示。 重做選項只會在執行復原操作後顯示在頁面工具列上。 重新整理頁面時會重設這些動作。

1. 選取列印管道後，前往 **[!UICONTROL 資產]** 標籤並套用篩選器，以僅顯示您要檢視的資產。

   使用「資產」瀏覽器，您也可以直接將資產拖放至「互動式通訊」目標區域。

   ![assets-docfragments](assets/assets-docfragments.png)

1. 將檔案片段拖放至互動式通訊中。 以下是您可以在互動式通訊的列印頻道中使用的檔案片段型別。

<table>
 <tbody>
  <tr>
   <td><strong>文档片段类型</strong></td>
   <td><strong>範例用途</strong></td>
  </tr>
  <tr>
   <td><a href="/help/forms/using/texts-interactive-communications.md" target="_blank">文本</a></td>
   <td>新增地址、收件者電子郵件和信函內文的文字 </td>
  </tr>
  <tr>
   <td><a href="/help/forms/using/conditions-interactive-communications.md" target="_blank">条件</a></td>
   <td>根據原則型別將適當的頁首影像新增至通訊的條件： Standard或Premium。 <br /> </td>
  </tr>
  <tr>
   <td>列表</td>
   <td>檔案片段群組，包括文字、條件、其他清單和影像。 <br /> </td>
  </tr>
 </tbody>
</table>

您也可以使用將新片段拖放至目標區域，以取代目標區域與檔案片段之間的繫結。 **[!UICONTROL 資產]** 標籤。 拖曳片段時目標區域的藍色陰影表示檔案片段可以拖曳至目標區域。

如需檔案片段的詳細資訊，請參閱 [檔案片段](/help/forms/using/document-fragments.md).

編寫介面可讓您區分互動式通訊中未繫結和已繫結的欄位和變數。 介面會使用橘色邊框反白標示未繫結的欄位和變數。

![unbound_fields_variables_highlights_dc](assets/unbound_fields_variables_highlights_dc.jpg)

此外，當您將滑鼠停留在這些元素上時，會顯示工具提示，其中包含「欄位」(Field) （未繫結）或「變數」(Variable) （未繫結）訊息。

檔案片段中使用的未繫結變數有時可能不會顯示在編寫介面上。 這可能是由於檔案片段中的內嵌文字規則所造成，或是條件片段的情況。 在這種情況下，以藍色反白顯示的工具提示會顯示為檔案片段的一部分。 工具提示會顯示檔案片段中使用的未繫結變數數目。

![未繫結的變數](assets/df_unbound_variable_new.png)

點選檔案片段，點選 ![configure_icon](assets/configure_icon.png) （設定），然後點選 **[!UICONTROL 屬性]** 互動式通訊的副手。 此 **[!UICONTROL 變數和資料模型物件]** 區段會列出變數，包括隱藏的變數，以及檔案片段中使用的資料模型物件。 使用 ![編輯](assets/edit.svg) （編輯）圖示來編輯屬性。

1. 若要設定變數的繫結，請點選變數並選取 ![configure_icon](assets/configure_icon.png) （設定），然後在側邊欄的「屬性」面板中設定繫結屬性。

   * **無**：代理程式會填入變數的值。
   * **文字片段**：如果選取，您可以瀏覽並選取文字檔案片段，其內容會呈現在欄位中。 只有那些文字檔案片段可以繫結至內沒有變數的變數。
   * **資料模型物件**：選取其值已填入欄位中的表單資料模型屬性。
   * **預設值：** 您可以使用此欄位定義變數的預設值。 當您預覽互動式通訊或在Agent UI中時，會顯示值。
   * **顯示模式：** 您也可以定義變數的顯示格式。 從「 」中選取任何預先定義的選項 **型別** 下拉式清單，將顯示格式套用至變數。 選取 **自訂** 定義清單中不可用的顯示模式。 如需詳細資訊，請參閱 [資料顯示模式](../../forms/using/create-interactive-communication.md#datadisplaypatterns).

   導覽至 [變數和資料模型物件](../../forms/using/create-interactive-communication.md#hiddenvariables) 以設定檔案片段中隱藏變數的繫結。

   您也可以拖放資料來源元素或文字檔案片段，以設定變數的繫結。  若要建立與任何資料來源元素的繫結，請選取 **資料來源** 標籤並將元素拖放至變數名稱。 資料來源元素和變數必須是相同型別，才能成功設定繫結。 如果您將資料來源元素拖放至已繫結的變數，新元素會取代舊元素，以使用變數建立新繫結。 同樣地，選取 **資產** 定位並拖放文字檔案片段至變數名稱，以設定兩者之間的繫結。 文字檔案片段不得包含任何變數。

1. 若要在已選取列印管道的情況下新增表格，請在 **[!UICONTROL 資產]** 索引標籤套用篩選器以僅顯示佈局片段。 將所需的佈局片段拖放至互動式通訊。 佈局片段以XDP為基礎，可用於在互動式通訊中建立圖形佈局或填入動態資料的靜態和動態表格。

   範例：版面配置表，顯示舊政策與新政策的毛保費、忠誠度折扣百分比以及緊急路邊協助可用性。

   如需佈局片段的詳細資訊，請參閱 [檔案片段](/help/forms/using/document-fragments.md).

1. 選取列印管道後，在 **[!UICONTROL 資產]** 索引標籤套用濾鏡以顯示影像。 將所需的影像拖放至互動式通訊，例如公司標誌。

   此外，在互動式通訊中管理下列專案：

   * [新增和設定圖表](/help/forms/using/chart-component-interactive-communications.md)
   * [使用列印管道同步Web管道](../../forms/using/create-interactive-communication.md#synchronize)

      * 自動同步
      * 取消继承
      * 重新啟用繼承
      * 同步
   * [附件與程式庫存取權](../../forms/using/create-interactive-communication.md#attachmentslibrary)
   * [XDP/佈局欄位屬性](../../forms/using/create-interactive-communication.md#xdplayoutfieldproperties)
   * [將規則新增至元件](../../forms/using/create-interactive-communication.md#rules)


1. 切換至 **[!UICONTROL 網路頻道]**. Web channel會顯示在互動式通訊編輯器中。 當您第一次從列印管道切換至網頁管道時，會自動進行同步。 如需詳細資訊，請參閱 [從列印管道同步Web管道](../../forms/using/create-interactive-communication.md#synchronize).

   由於在此範例中，我們使用Print做為Web的主版，因此Print channel預留位置、內容和資料繫結會同步至Web channel。 不過，您可以變更和自訂網路頻道中的特定內容。 [取消繼承](#cancelinheritance) 已使用print channel產生的目標區域和變數能夠自訂內容。

   ![webchannelassets](assets/webchannelassets.png)

   點選檔案片段，點選 ![configure_icon](assets/configure_icon.png) （設定），然後點選 **[!UICONTROL 屬性]** 互動式通訊的副手。 此 **[!UICONTROL 變數和資料模型物件]** 區段會列出變數，包括隱藏的變數，以及檔案片段中使用的資料模型物件。 使用 ![編輯](assets/edit.svg) （編輯）圖示來編輯屬性。 此外，對於已 [自動產生](#synchronize) 在使用Print channel的Web channel中，使用 ![取消繼承](assets/cancelinheritance.png) （取消繼承）圖示移至每個資料模型物件和變數旁的 [取消繼承](#cancelinheritance) 以及能夠編輯它們。

1. 若要在Web channel中新增其他元件，並在選取Web channel時，點選 **[!UICONTROL 元件]**. 視需要在互動式通訊的Web channel中拖放元件，然後繼續加以設定。

   | 组件 | 功能 |
   |---|---|
   | 图表 | 新增可在互動式通訊中使用的圖表，以視覺化呈現從表單資料模型集合中擷取的二維資料。 如需詳細資訊，請參閱 [使用圖表元件](../../forms/using/chart-component-interactive-communications.md). |
   | 文档片段 | 可讓您新增可重複使用的元件、文字、清單或條件至互動式通訊。 您新增至互動式通訊的可重複使用元件，可以是表單資料模型式元件，也可以不使用表單資料模型。 |
   | 图像 | 可让您插入图像。 |
   | 面板 | 可讓您新增 [面板](../../forms/using/create-interactive-communication.md#add-panel-component-to-the-web-channel) 至互動式通訊。 |
   | 表 | 添加表格以便按行和列整理数据。 |
   | 目标区域 | 在Web Channel中插入目標區域，以整理Web Channel專用元件。 目標區域是一個普通的容器，可讓您將網頁頻道特定的元件分組。 |
   | 文本 | 將RTF文字新增至互動式通訊的Web channel。 文字也可以使用表單資料模型物件來使內容動態化。 |
   | 按钮 | 可讓您新增 [按鈕](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) 至互動式通訊。 您可以使用Button元件導覽至其他互動式通訊、最適化表單、影像或檔案片段等其他資產，或外部URL。 |
   | 分隔符 | 可讓您在互動式通訊中插入水平線。 使用此元件來區分對應中的區段。 例如，您可以使用分隔符號元件，來區分信用卡對帳單中「客戶明細」與「信用卡明細」區段。 |

1. 視需要在您的Web Channel中插入資產。

   您可以 [預覽您的互動式通訊](#previewic) 檢視互動式通訊的列印和網頁輸出外觀，並視需要繼續變更。

## 預覽互動式通訊 {#previewic}

您可以使用 **預覽選項** 評估互動式通訊的外觀。 互動式通訊的Web channel也提供模擬各種裝置互動式通訊體驗的選項。 例如，iPhone、iPad和案頭。 您可以使用兩者 **預覽** 和 **模擬器** ![尺標](assets/ruler.png) 這些選項會相互結合，以針對不同熒幕大小的裝置預覽Web輸出。 預覽中的範例資料會從指定的表單資料模型填入。

1. 選取要預覽的（列印或網頁）頻道，然後點選預覽。 此時會出現互動式通訊。

   >[!NOTE]
   >
   >預覽會填入指定的表單資料模型的範例資料。 如需使用其他資料預覽互動式通訊或使用預填服務的詳細資訊，請參閱 [使用表單資料模型](/help/forms/using/using-form-data-model.md) 和 [使用表單資料模型](/help/forms/using/work-with-form-data-model.md).

1. 對於Web Channel，請使用 ![尺標](assets/ruler.png) 以檢視互動式通訊在各種裝置上的外觀。

   ![webchannelpreview](assets/webchannelpreview.png)

此外，您還可以 [使用Agent UI準備和傳送互動式通訊](/help/forms/using/prepare-send-interactive-communication.md).

## 在互動式通訊中設定屬性  {#configure-properties-in-interactive-communication}

### 附件與程式庫存取權 {#attachmentslibrary}

在Print channel中，您可以設定附件和程式庫存取權，以允許Agent管理互動式通訊之Agent UI中的附件：

1. 在「列印」管道中，反白顯示「檔案容器」並點選 **屬性**.

   ![documentcontainerproperties](assets/documentcontainerproperties.png)

   「屬性」面板會顯示在側欄中。

   ![屬性附件](assets/propertiesattachments.png)

1. 展開 **附件** 並指定下列屬性：

   * **[!UICONTROL 允許程式庫存取]**：選取此選項可在代理程式UI中啟用代理程式的程式庫存取權。 如果啟用，Agent可以在準備互動式通訊時從資料庫新增檔案。
   * **[!UICONTROL 允許重新排序附件]**：選取此選項可讓「代理程式」透過互動式通訊重新排序附件。
   * **[!UICONTROL 附件數量上限]**：指定互動式通訊允許的附件數目上限。
   * **[!UICONTROL 要附加的檔案]**：點選 **[!UICONTROL 新增]** 和瀏覽以選取要附加的檔案，並指定下列內容：

      * **[!UICONTROL 依預設將此檔案附加至檔案]**：如果只有附件不是強制性的，您可以變更此選項。
      * **[!UICONTROL 強制：]** 代理程式將無法移除代理程式UI中的附件。

   ![附件檔案](assets/attachfiles.png)

1. 點選 **[!UICONTROL 完成]**.

### XDP/佈局欄位屬性 {#xdplayoutfieldproperties}

1. 編輯互動式通訊的列印頻道時，將滑鼠游標停留在欄位上（內建於列印頻道範本中），然後選取 ![configure_icon](assets/configure_icon.png) （設定）。

   「屬性」對話方塊會顯示在側邊欄中。

   ![data_display_patterns_fields](assets/data_display_patterns_fields.jpg)

1. 指定下列專案：

   * **[!UICONTROL 名稱]**：JCR節點名稱。
   * **[!UICONTROL 標題]**：輸入代理程式UI和檔案容器樹狀結構中的代理程式可見的標題。
   * **[!UICONTROL 繫結型別]**：為欄位選取下列其中一個繫結型別。

      * 無：代理程式會填入屬性的值。
      * 文字片段：如果選取，您可以瀏覽並選取文字檔案片段，其內容會呈現在欄位中。 或者，也可以將文字檔案片段拖放至欄位名稱，以設定兩者之間的繫結。 文字檔案片段不得包含任何變數。
      * 資料模型物件：選取其值已填入欄位中的表單資料模型屬性。 或者，選取 **資料來源** 標籤並將屬性拖放至欄位。
   * **[!UICONTROL 預設值]**：預設值可確保當指定的資料模型物件或文字片段未提供任何值時，欄位不會空白。 如果資料繫結型別是none，預設值會預先填入欄位中。
   * **[!UICONTROL 顯示模式]**：您也可以定義欄位的顯示格式。 從「 」中選取任何預先定義的選項 **型別** 下拉式清單，將顯示格式套用至欄位。 選取 **自訂** 定義清單中不可用的顯示模式。 如需詳細資訊，請參閱 [資料顯示模式](../../forms/using/create-interactive-communication.md#datadisplaypatterns)

   * **[!UICONTROL 可由Agent編輯]**：選取以允許代理程式編輯代理程式UI中欄位中的值。 如果繫結型別是文字片段，此設定不適用。
   * **[!UICONTROL 標籤]**：指定在Agent UI中向Agent顯示與欄位一起顯示的文字字串。 如果繫結型別是文字片段，此設定不適用。
   * **[!UICONTROL 工具提示]**：輸入文字字串，將滑鼠移到代理程式UI中的代理程式時可以看到此字串。 如果繫結型別是文字片段，此設定不適用。
   * **[!UICONTROL 必填]**：選取此選項可讓欄位成為代理程式的必要欄位。 如果繫結型別是文字片段，此設定不適用。
   * **[!UICONTROL 允許多行]**：選取此欄位可允許多行文字在欄位中輸入。 如果繫結型別是文字片段，此設定不適用。


1. 點選 ![done_icon](assets/done_icon.png).

### 資料顯示模式 {#datadisplaypatterns}

製作介面可讓您為欄位、變數和表單資料模型元素定義資料顯示模式，以供建立列印和Web管道的互動式通訊時使用。

若要設定資料顯示模式，請點選元素，然後選取 ![configure_icon](assets/configure_icon.png) （設定）並設定中的顯示模式 **[!UICONTROL 屬性]** 側欄中的面板。 從「 」中選取任何預先定義的選項 **[!UICONTROL 型別]** 下拉式清單，以檢視與所選型別相關聯的模式。 選取 **[!UICONTROL 自訂]** 從 **[!UICONTROL 型別]** 下拉式清單，定義清單中不可用的模式。 編輯中的值 **[!UICONTROL 圖樣]** 欄位會自動將型別修改為 **[!UICONTROL 自訂]**.

若要套用顯示模式，在「模式」欄位中定義的字元或數字數必須符合或超過欄位、變數和表單資料模型元素值中定義的字元或數字。 如需詳細資訊，請參閱 [範例](../../forms/using/create-interactive-communication.md#greaternumberofdigits).

![data_display_pattern_example](assets/data_display_patterns_ssn_new.png)

從列印管道產生Web內容後，您可以重新定義欄位、變數或表單資料模型元素的顯示模式。 因此，元素可以針對列印和Web管道定義不同的顯示模式。 如果您未定義列印管道中元素的顯示模式，且未使用列印管道自動產生Web內容，則為列印管道中的元素定義的資料繫結會定義中可用的顯示模式選項。 **[!UICONTROL 型別]** 下拉式清單。 如果沒有為元素定義繫結，則元素的資料型別會定義可用的顯示模式選項。 例如，如果您為列印管道中的元素建立Number型別的資料繫結，則可在 **[!UICONTROL 型別]** 下拉式清單屬於各種格式的「數字」型別。

切換至 **預覽** 模式或開啟Agent UI以檢視套用至這些元素的顯示模式。

下表列出設定變數的資料顯示模式後，所顯示的值範例：

| 类型 | 預設值 | 顯示模式 | 顯示值 | 描述 |
|---|---|---|---|---|
| 社会安全号码 | 123456789 | 文字{999-99-9999} | 123-45-6789 | 預設值欄位中的位數與「模式」欄位中的位數相符。 已成功顯示基於模式的值。 |
| 社会安全号码 | 1234567 | 文字{999-99-9999} | 1-23-4567 | 預設值欄位中的位數小於「模式」欄位中的位數。 模式會套用到7個可用的數字。 |
| 社会安全号码 | 1234567890 | 文字{999-99-9999} | 1234567890 | 預設值欄位中的位數大於「模式」欄位中的位數。 因此，顯示值不會變更。 |

如果沒有為變數或表單資料模型元素指定顯示模式， [全域檔案片段設定](https://helpx.adobe.com//experience-manager/6-5/forms/using/interactive-communication-configuration-properties.html) 預設為使用。

如果您沒有將顯示模式套用至數字資料型別的變數，列印預覽會根據全域檔案片段組態顯示模式。 如果您將變更套用至預設全域檔案片段設定，Agent UI仍會根據為地區設定的預設分隔符號顯示模式。

同樣地，對於欄位，如果未指定顯示模式，則建立列印範本(XDP)時定義的模式將套用至欄位。 如果在建立列印範本時沒有圖樣，則根據XFA規格的預設圖樣會套用至欄位。

此外，如果指定的顯示模式不正確或無法套用，則會將根據XFA規格的預設模式套用至欄位、變數或表單資料模型元素。

## 套用規則至互動式通訊元件 {#rules}

若要在互動式通訊中條件化元件或內容，請點選元件/內容並選取 ![createruleicon](assets/createruleicon.png) （建立規則）以啟動規則編輯器。

如需詳細資訊，請參閱：

* [规则编辑器](/help/forms/using/rule-editor.md)
* [互動式通訊撰寫簡介](/help/forms/using/introduction-interactive-communication-authoring.md)

## 使用表格 {#tables}

### 互動式通訊中的動態表格 {#dynamic-tables-in-interactive-communication}

您可以使用版面配置片段在互動式通訊中新增動態表格。 下列步驟使用信用卡陳述式的範例來說明如何使用版面片段在互動式通訊中建立動態表格。

1. 確保建立表格所需的佈局片段可在AEM中使用。
1. 在互動式通訊的列印頻道中，從資產瀏覽器將版面片段（含多欄表格）拖放至目標區域。

   ![lf_dragdrop](assets/lf_dragdrop.png)

   表格會顯示在互動式通訊配置區域中。

   ![lf_dragdrop_table](assets/lf_dragdrop_table.png)

1. 指定表格中每個儲存格的資料繫結。 若要建立可重複的列，請在屬於通用集合屬性的列中插入表單資料模型屬性。

   1. 點選表格中的儲存格並選取 ![configure_icon](assets/configure_icon.png) （設定）。

      「屬性」對話方塊會顯示在側邊欄中。

      ![lf_cell_properties](assets/lf_cell_properties.png)

   1. 設定屬性：

      * **[!UICONTROL 名稱]**：JCR節點名稱。
      * **[!UICONTROL 標題]**：輸入將顯示在互動式通訊編輯器中的標題。
      * **[!UICONTROL 繫結型別]**：為欄位選取下列其中一個繫結型別。

         * **[!UICONTROL 无]**
         * **[!UICONTROL 資料模型物件]**：表單資料模型屬性的值會填入欄位中。 或者，選取 **資料來源** 標籤並將屬性拖放至欄位。
      * **[!UICONTROL 資料模型物件]**：表單資料模型屬性，其值已填入欄位中。
      * **[!UICONTROL 預設值]**：預設值可確保指定資料模型物件未提供值時的欄位不是空的。 預設值會預先填入欄位中。

      * **[!UICONTROL 可由Agent編輯]**：選取以允許代理程式編輯代理程式UI中欄位中的值。
   1. 點選 ![done_icon](assets/done_icon.png).



1. 預覽互動式通訊，以檢視以資料呈現的表格。

   ![lf_preview](assets/lf_preview.png)

### 僅限Web-channel表格 {#webchanneltables}

在網頁範本中點選根面板，然後點選 **+** 新增 **表格** 元件至互動式通訊。 包含兩列的表格會插入互動式通訊中。 表格的第一列代表「表格」標頭。

#### 將列和欄新增至表格 {#addrowscolumnstable}

**若要新增或刪除欄：**

1. 點選表格標頭列中的預設文字方塊以檢視元件工具列。
1. 選取 **新增欄** 或 **刪除欄** 以分別新增或刪除表格欄。

![component_toolbar_table1](assets/component_toolbar_table1.png)

**若要新增或刪除列：**

1. 點選任何表格列可檢視元件工具列。 您也可以使用互動式通訊Sidekick中的內容瀏覽器來選取表格列。
1. 選取 **新增列** 或 **刪除列** 以分別新增或刪除表格列。 使用 **上移** 和 **下移** 工具列中的可用選項可重新排清單格中的列。

![组件工具栏](assets/component_toolbar_table_row_new.png)

**答：** 新增列 **B.** 刪除列 **C.** 上移 **D.** 下移

#### 新增或編輯表格儲存格中的文字 {#addedittexttable}

1. 選取表格儲存格中的預設文字方塊，然後點選 ![編輯](assets/edit.png) （編輯）。
1. 在表格儲存格中輸入文字，然後點選 ![done_icon](assets/done_icon.png) 以儲存。

#### 建立表格儲存格與資料模型物件元素之間的繫結 {#createbindingtablecells}

1. 選取表格列中的預設文字方塊並點選 ![編輯](assets/edit.png) （編輯）。
1. 點選「資料模型物件」下拉式清單，然後選取屬性。
1. 點選以儲存並建立表格儲存格與資料模型物件屬性之間的繫結。

![建立資料繫結](assets/create_data_binding_table_new.png)

#### 為表格儲存格中的文字建立超連結 {#createhyperlinktable}

1. 選取表格儲存格中的預設文字方塊，然後點選 ![編輯](assets/edit.svg) （編輯）。
1. 選取表格儲存格中的文字，然後點選「超連結」圖示。
1. 在「 」中指定URL **路徑** 欄位。
1. 點選 ![done_icon](assets/done_icon.png) 以儲存超連結屬性。

![建立超連結](assets/create_hyperlink_table_new.png)

#### 建立動態表格 {#createdynamictables}

您可以使用型別集合的資料模型屬性，在互動式通訊中建立僅限Web管道的動態表格。 這樣的表格是集合屬性的子屬性的表示法。 您只能編輯表格中各種儲存格的格式屬性。

1. 切換至Web channel，然後選擇顯示資料來源瀏覽器。
1. 將集合屬性拖放至子表單中。 系統隨即會在子表單中建立表格。
1. 在互動式通訊的Web預覽中預覽表格。

#### 排序表格中的欄 {#sortcolumns}

您可以根據互動式通訊中表格中的任何欄來排序資料。 欄中的值可以遞增或遞減順序排序。

排序可套用至包含下列專案的表格欄：

* 靜態文字
* 資料模型物件屬性
* 靜態文字與資料模型物件屬性的組合

若要啟用排序：

1. 選取表格並點選 ![configure_icon](assets/configure_icon.png) （設定）。 您也可以使用 **內容** 互動式通訊側邊欄中的瀏覽器。
1. 選取 **啟用排序。**
1. 點選 ![done_icon](assets/done_icon.png) 以儲存表格屬性。 欄標題中的排序圖示（向上和向下箭頭）表示已啟用排序。

   ![啟用排序](assets/enable_sorting_new-1.png)

1. 切換至 **預覽** 模式以檢視輸出。 表格會自動根據表格的第一個欄排序。
1. 按一下欄標題，根據欄排序值。

   具有向上箭頭的欄標題表示：

   * 表格會根據該欄排序。
   * 欄中的值會以遞增順序顯示。

   ![遞增排序](assets/sorting_ascending_new-1.png)

   同樣地，具有向下箭頭的欄標題表示欄中的值以降序顯示。

## 編輯互動式通訊屬性 {#edit-interactive-communication-properties}

建立互動式通訊後，您可在稍後階段編輯其屬性。

使用 **屬性** 頁面至：

* 編輯建立互動式通訊時指定欄位的值，例如「標題」和「說明」。
* 新增或刪除現有互動式通訊的Web channel。
* 預覽、下載或刪除互動式通訊
* 開啟 [代理程式UI](/help/forms/using/prepare-send-interactive-communication.md).

若要存取 **屬性** 頁面：

1. 登入AEM編寫執行個體並導覽至 **Adobe Experience Manager** > **Forms** > **Forms與檔案**.
1. 選取互動式通訊並點選 **屬性**.
1. 選取 **一般** 標籤以編輯 **標題** 和 **說明** 欄位。

### 新增或刪除Web管道 {#add-or-delete-the-web-channel}

執行以下步驟，為現有的互動式通訊新增Web channel：

1. 於 **屬性** 頁面，選取 **頻道** 標籤。
1. 選取 **Web** 核取方塊並選取Web頻道的範本。
1. 選取 **針對Web Channel使用列印為主版** 以啟用Web頻道與列印頻道之間的同步化。
1. 點選 **儲存並關閉** 以儲存變更。

   同樣地，您可以點選 **Web** 核取方塊 **頻道** 索引標籤以從互動式通訊中刪除Web channel。

## 新增Button元件至Web channel {#add-button-component-to-the-web-channel}

您可以將按鈕當做元件新增到互動式通訊的Web channel中。 使用定義規則 [規則編輯器](../../forms/using/rule-editor.md) 點選按鈕即可導覽至其他互動式通訊、最適化表單、影像或檔案片段等其他資產，或外部URL。

若要新增按鈕並在其上定義規則：

1. 在網頁範本中點選根面板，然後點選 **+** 新增 **按鈕** 元件至互動式通訊。
1. 點選按鈕元件並點選 ![edit-rules](assets/edit-rules.png) 以定義點選按鈕上的規則。
1. 在 **時間** 區段，選取 **已點按** 從按鈕下拉式清單的狀態。
1. 在 **則** 區段：

   1. 從下拉式清單中選取動作。 例如，選取 **導覽至** 作為動作型別。

   1. 指定互動式通訊、最適化表單、資產或網頁的URL。 例如，以下列格式指定URL以導覽至其他互動式通訊： https://&lt;server-name>：&lt;port>/editor.html/content/forms/af/&lt;interactive communication=&quot;&quot; name=&quot;&quot;>/channels/&lt;channel name=&quot;&quot; print=&quot;&quot; or=&quot;&quot; web=&quot;&quot;>.html
   1. 指定在同一個標籤、新標籤或新視窗中開啟資產的選項。
   1. 點選 **完成** 然後點選 **關閉** 以儲存規則。

   同樣地，您可以從動作型別下拉式清單中選取其他可用選項，例如「叫用服務」和「提交表單」。 如需詳細資訊，請參閱 [規則編輯器](../../forms/using/rule-editor.md).

1. 預覽互動式通訊，然後點選按鈕以檢視互動式通訊、最適化表單、資產，或步驟4(b)中指定的網頁。

## 將面板元件新增至Web Channel {#add-panel-component-to-the-web-channel}

Panel元件是將其他元件分組在一起的預留位置，可控制一組元件（例如摺疊式功能表和索引標籤）在互動式通訊中的佈局方式。 面板元件也可讓您讓一組元件對一般使用者可重複，例如在填寫教育憑證所需的多個專案中。

執行以下步驟，將面板元件新增至Web Channel：

1. 插入 **面板** 元件（使用下列任一選項）：

   * 點選元件，點選 **+** 並選取 **面板** 元件。

   * 從 **元件** 瀏覽器面板，拖放 **面板** 互動式通訊上的元件。

   * 點選 **面板** 在 **內容** 瀏覽器面板並點選 **新增子面板**. 選取 **新增子面板** 選項會顯示 **新增子面板** 對話方塊。 輸入Panel元件的標題和選擇性說明及名稱。

1. 從「 」點選面板 **內容** 瀏覽器在面板上執行其他動作，例如設定、編輯規則、複製、刪除和插入元件。

   您也可以拖放面板至 **內容** 瀏覽器，以反映右窗格中互動式通訊結構的變更。

## 將Web Channel與列印頻道同步 {#synchronize}

當您在建立互動式通訊時選取「列印為Web Channel的主版」時，Web channel會與Print channel同步建立，而Web channel的內容和資料繫結會衍生自print channel，而且當您點選「同步」時，在列印管道中所做的變更會反映在Web channel中。

不過，作者可視需要中斷Web Channel中元件的繼承。

![建立列印主版](assets/create_ic_print_master_new-1.png) ![列印主版網頁](assets/create_ic_print_master_web_new-1.png)

### 自動同步 {#autosync}

如果您選取 **[!UICONTROL 針對Web Channel使用「列印為主版」]** 選項，您可以選取下列任何模式來產生Web Channel：

* **[!UICONTROL 自動配置]**：選取此模式可自動從Print channel產生Web channel的預留位置、內容和資料繫結。
* **[!UICONTROL 手動組織]**：選取此模式可手動選取列印管道元素，並使用「資料來源」標籤中可用的主要內容將其新增至Web channel。 如需詳細資訊，請參閱 [選取「列印管道元素」以建立Web channel內容](#selectprintchannelelements).

![建立IC選項](assets/create_ic_options_updated_new.png)

>[!NOTE]
>
>同步管道只會同步從列印管道到Web管道的檔案片段、影像、條件、清單和佈局片段。 包含此類元素的子表單或父節點不會同步。

### 選取「列印管道元素」以建立Web channel內容 {#selectprintchannelelements}

如果您在建立互動式通訊時選取「列印為主版」，但未選取「自動同步」選項，您也可以將「列印色版」元素拖放至Web channel編寫介面。

導覽至 **資料來源** > **主要內容** 以檢視Print channel元素。 將目標區域、欄位或表格拖放至Web Channel編寫介面。 元素名稱旁的藍色圓圈圖示表示Print channel元素已包含在Web channel中。

![主要內容](assets/master_content.png)

### 取消继承 {#cancelinheritance}

在Web Channel中，元件會嵌入目標區域中。

將滑鼠指標暫留在Web Channel中的相關目標區域或變數上，然後選取 ![取消繼承](assets/cancelinheritance.png) （取消繼承），然後在「取消繼承」對話方塊中，點選 **[!UICONTROL 是]**.

會取消目標區域內元件的繼承，現在您可以視需要加以編輯。

### 重新启用继承 {#re-enable-inheritance}

在Web Channel中，如果您已取消元件的繼承，則可重新啟用它。 若要重新啟用繼承，請將游標停留在相關目標區域的邊界上（包括元件），然後點選 ![reenableinheritance](assets/reenableinheritance.png).

「回覆繼承」對話方塊隨即顯示。

![revertinheritance](assets/revertinheritance.png)

如有需要，請選取 **[!UICONTROL 在恢復繼承後同步頁面]**. 選取此選項可同步處理整個互動式通訊。 如果您未選取此選項，恢復繼承時只會同步相關目標區域。

點選 **[!UICONTROL 是]**.

### 同步 {#synchronize-1}

如果您使用Print as Master for Web Channel並對Print channel進行變更，則可以同步內容以將新進行的變更帶到Web channel。

1. 若要將Web channel與Print channel同步，請切換至Web channel並點選「更多選項」圖示。

   ![自動同步選項](assets/auto_sync_options_new.png)

1. 點選下列其中一項：

   * **[!UICONTROL 與列印同步]**：僅針對繼承未取消的目標區域同步內容。
   * **[!UICONTROL 重設]**：將Web channel內容與Print channel同步，並捨棄對Web channel所做的所有變更。

### 使用元件工具列對繼承的元件執行動作 {#componenttoolbar}

使用「同步」選項在Web Channel中自動產生內容後，您就可以對元件執行更多動作，而無需取消繼承。

![组件工具栏](assets/component_toolbar_inherited_web_new.png)

點選元件以檢視下列選項：

* **複製：** 複製元件，並將其貼到互動式通訊的其他位置。
* **剪下：** 在互動式通訊中將元件從一個位置移動到另一個位置。
* **插入元件：** 在選取元件的上方插入元件。
* **貼上：** 使用上述選項貼上您剪下或複製的元件。
* **群組：** 如果要一起剪下、複製或貼上多個元件，請選取多個元件。
* **父系：** 選取元件的父件。
* **檢視SOM運算式：** 檢視 [SOM運算式](../../forms/using/using-som-expressions-adaptive-forms.md) 用於元件。

* **面板中的群組物件：** 將面板中的元件分組，以便同時對這些元件執行操作。 如需詳細資訊，請參閱 [面板中的群組物件](#groupobjectspanel).

* **取消繼承：** [取消繼承](#cancelinheritance) 元件以編輯它們。

### 面板中的群組物件 {#groupobjectspanel}

Web Channel編寫介面有助於將面板中的元件分組，以便同時對這些元件執行操作。 此 **內容** 索引標籤會列出群組元件，作為內容樹狀結構中面板的子元素。

1. 點選元件並選取群組( ![群組](assets/group.jpg))操作。
1. 選取多個元件並點選 **面板中的群組物件**.

   ![群組物件](assets/component_toolbar_group_objects_new.png)

1. 在 **面板中的群組物件** 對話方塊中，輸入面板的名稱。
1. 輸入面板的選用標題和說明。
1. 按一下 ![bullet_checkmark](assets/bullet_checkmark.png).

   群組的元件會在內容樹中顯示為「面板」的子元素。

   ![content_tree_group](assets/content_tree_grouping.png)

## 列印頻道的輸出格式 {#output-format-print-channel}

使用PrintChannel API定義互動式通訊之列印頻道的輸出格式。 如果您未定義輸出格式，AEM Forms會以PDF格式產生輸出。

```javascript
//options for rendering print channel of a multi-channel document
PrintChannelRenderOptions renderOptions = new PrintChannelRenderOptions();
PrintDocument printDocument = printChannel.render(renderOptions);
```

若要以任何其他格式產生輸出，請指定輸出格式型別。 請參閱 [PrintChannel API](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/PrintConfig.html) 以取得支援的輸出格式型別清單。

例如，您可以使用下列範例將PCL定義為互動式通訊的輸出格式：

```javascript
//options for rendering print channel of a multi-channel document
PrintChannelRenderOptions renderOptions = new PrintChannelRenderOptions();
renderOptions.setRenderFormat(PrintConfig.HP_PCL_5e);
PrintDocument printDocument = printChannel.render(renderOptions);
```
