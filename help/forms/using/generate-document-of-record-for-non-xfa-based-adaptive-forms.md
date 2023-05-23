---
title: 產生最適化表單的記錄檔案
seo-title: Generate Document of Record for adaptive forms
description: 說明如何為最適化表單的記錄檔案(DoR)產生範本。
seo-description: Explains how you can generate a template for a document of record (DoR) for adaptive forms.
uuid: 2dc7e0de-fff9-43fa-9426-e9b047eb2595
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ce65cb5f-94ec-4423-9fa9-d617e9703091
docset: aem65
feature: Adaptive Forms
exl-id: 7240897f-6b3a-427a-abc6-66310c2998f3
source-git-commit: 85189a4c35d1409690cbb93946369244e8848340
workflow-type: tm+mt
source-wordcount: '3466'
ht-degree: 2%

---

# 產生最適化表單的記錄檔案{#generate-document-of-record-for-adaptive-forms}

## 概述 {#overview}

提交表單後，您的客戶通常希望以列印或檔案格式來記錄他們在表單中填寫的資訊，以供日後參考。 這稱為記錄檔案。

本文說明如何產生最適化表單的記錄檔案。

>[!NOTE]
>
>XFA型調適型表單不支援自動產生記錄檔案。 不過，您可以使用用來建立最適化表單作為記錄檔案的XDP。

## 最適化表單型別及其記錄檔案 {#adaptive-form-types-and-their-documents-of-record}

建立最適化表單時，您可以選取表單模型。 您的选项包括：

* [表單範本](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-an-xfa-form-template)
可讓您為最適化表單選取XFA範本。 當您選取XFA範本時，您可以使用關聯的XDP檔案來記錄檔案，如上所述。

* [XML結構描述](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-xml-or-json-schema)
可讓您選取最適化表單的XML結構描述定義。 當您為最適化表單選取XML結構描述時，您可以：

   * 為記錄檔案關聯XFA範本。 確保關聯的XFA範本使用與您的最適化表單相同的XML結構描述
   * 自動產生記錄檔案

* 無讓您建立無表單模型的最適化表單。 系統會自動為您的最適化表單產生記錄檔案。

當您選取表單模型時，請使用「記錄檔案範本組態」下可用的選項來設定記錄檔案。 另請參閱 [記錄範本檔案設定](#document-of-record-template-configuration).

## 自動產生的記錄檔案 {#automatically-generated-document-of-record}

記錄檔案可讓您的客戶保留已提交表單的復本以供列印。 當您自動產生記錄檔案時，每次變更表單時，其記錄檔案都會立即更新。 例如，您會為選取美國作為其國家/地區的客戶移除年齡欄位。 當這類客戶產生記錄檔案時，他們在記錄檔案中看不到年齡欄位。

自動產生的記錄檔案具有以下優點：

* 它負責資料繫結。
* 它會自動隱藏在提交時標籤為從記錄檔案中排除的欄位。 無需額外付費。
* 這樣可節省設計記錄範本檔案的時間。
* 它可讓您使用不同的基本範本嘗試不同的樣式和外觀，並為記錄檔案選擇最佳的樣式和外觀。 樣式外觀是選用的，如果您未指定樣式，系統樣式會設定為預設值。
* 它可確保表單中的任何變更都立即反映在記錄檔案中。

## 自動產生記錄檔案的元件 {#components-to-automatically-generate-a-document-of-record}

若要產生最適化表單的記錄檔案，您需要下列元件：

**最適化表單** 您要為其產生記錄檔案的最適化表單。

**基本範本（建議）** 在AEM Designer中建立的XFA範本（XDP檔案）。 基礎範本用於指定記錄檔案範本的樣式和品牌資訊。

另請參閱 [記錄檔案的基礎範本](#base-template-of-a-document-of-record)

>[!NOTE]
>
>記錄檔案的基礎範本也稱為記錄檔案的中繼範本。

**記錄範本檔案** 從最適化表單產生的XFA範本（XDP檔案）。

另請參閱 [記錄範本檔案設定](#document-of-record-template-configuration).

**表單資料** 使用者在最適化表單中填寫的資訊。 它會與記錄檔案範本合併，以產生記錄檔案。

## 最適化表單元素的對應 {#mapping-of-adaptive-form-elements}

以下各節說明最適化表單元素在記錄檔案中的顯示方式。

### 字段 {#fields}

<table>
 <tbody>
  <tr>
   <th>最適化表單元件</th>
   <th>對應的XFA元件</th>
   <th>預設包含在記錄檔案範本中？</th>
   <th>注释</th>
  </tr>
  <tr>
   <td>按钮</td>
   <td>按钮</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>复选框</td>
   <td>复选框</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>日期选取器</td>
   <td>日期/時間欄位</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>下拉列表</td>
   <td>下拉列表</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>潦草签名</td>
   <td>手寫簽名</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>数值框</td>
   <td>數值欄位</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>密码框</td>
   <td>密码字段</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>单选按钮</td>
   <td>单选按钮</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>文本框</td>
   <td>文本字段</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>“重置”按钮</td>
   <td>“重置”按钮</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>“提交”按钮</td>
   <td><p>電子郵件提交按鈕</p> <p>HTTP提交按鈕</p> </td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>條款與條件</td>
   <td> </td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>文件附件</td>
   <td> </td>
   <td>false</td>
   <td>在記錄範本檔案中無法使用。 僅可用於透過附件的記錄檔案。</td>
  </tr>
 </tbody>
</table>

### 容器 {#containers}

<table>
 <tbody>
  <tr>
   <th>最適化表單元件</th>
   <th>對應的XFA元件</th>
   <th>注释</th>
  </tr>
  <tr>
   <td>面板<br /> </td>
   <td>子表單<br /> </td>
   <td>可重複面板對應至可重複的子表單。</td>
  </tr>
 </tbody>
</table>

### 靜態元件 {#static-components}

| 最適化表單元件 | 對應的XFA元件 | 注释 |
|---|---|---|
| 图像 | 图像 | 除非使用記錄檔案設定加以排除，否則TextDraw和Image元件（無論繫結或未繫結）一律會出現在以XSD為基礎的最適化表單的記錄檔案中。 |
| 文本 | 文本 |

>[!NOTE]
>
>在傳統UI中，您會獲得不同的索引標籤來編輯欄位屬性。

### 表格 {#tables}

最適化表單元件（例如頁首、頁尾和列）對應至對應的XFA元件。 您可以將可重複面板對應至記錄檔案中的表格。

## 記錄檔案的基礎範本 {#base-template-of-a-document-of-record}

基礎範本為記錄檔案提供樣式和外觀資訊。 它可讓您自訂自動產生記錄檔案的預設外觀。 例如，您想要在記錄檔案的頁首中新增公司標誌，並在頁尾中新增版權資訊。 基底範本的主版頁面會作為記錄檔案範本的主版頁面。 主版頁面可以包含頁首、頁尾和頁碼等資訊，可套用至記錄檔案。 您可以使用基礎範本將此類資訊套用至記錄檔案，以自動產生記錄檔案。 使用基礎範本可讓您變更欄位的預設屬性。

請關注 [基礎範本慣例](#base-template-conventions) 當您設計基底範本時。

## 基礎範本慣例 {#base-template-conventions}

基礎範本用於定義記錄檔案的頁首、頁尾、樣式和外觀。 頁首和頁尾可包含公司標誌和版權文字等資訊。 基礎範本中的第一個主版頁面會被複製並用作記錄檔案的主版頁面，其中包含頁首、頁尾、頁碼或應出現在記錄檔案所有頁面上的任何其他資訊。 如果您使用不符合基礎範本慣例的基礎範本，則基礎範本中的第一個主版頁面仍會用於記錄檔案範本中。 強烈建議您依照其慣例設計基礎範本，並使用它來自動產生記錄檔案。

**主版頁面慣例**

* 在基礎範本中，您應將根子表單命名為 `AF_METATEMPLATE` 主版頁面為 `AF_MASTERPAGE`.

* 具有名稱的主版頁面 `AF_MASTERPAGE` 位於 `AF_METATEMPLATE` 根子表單會優先擷取頁首、頁尾和樣式資訊。

* 若 `AF_MASTERPAGE` 不存在，則會使用基本範本中存在的第一個主版頁面。

**欄位的樣式慣例**

* 若要在記錄檔案中的欄位上套用樣式，基本範本會提供位於 `AF_FIELDSSUBFORM` subfrom under the `AF_METATEMPLATE` 根子表單。

* 這些欄位的屬性會套用至記錄檔案中的欄位。 這些欄位應遵循 `AF_<name of field in all caps>_XFO` 命名慣例。 例如，核取方塊的欄位名稱應為 `AF_CHECKBOX_XFO`.

若要建立基礎範本，請在AEM Designer中執行下列動作。

1. 按一下 **檔案>新增**.
1. 選取 **根據範本** 選項。

1. 選取 **Forms — 記錄檔案** 類別。
1. 選取 **DoR基本範本**.
1. 按一下 **下一個** 並提供必要資訊。

1. （可選）修改要套用至記錄檔案中欄位的樣式和外觀。
1. 儲存表單。

您現在可以使用儲存的表單作為記錄檔案的基礎範本。
請勿修改或移除基底範本中存在的任何指令碼。

**修改基底範本**

* 如果您未在基礎範本的欄位上套用任何樣式，建議您從基礎範本中移除這些欄位，以便自動擷取對基礎範本的任何升級。
* 修改基底範本時，請勿移除、新增或修改指令碼。

>[!NOTE]
>
>使用慣例並嚴格遵循上述步驟來設計基礎範本。

## 记录文档模板配置 {#document-of-record-template-configuration}

設定表單的記錄檔案範本，讓客戶下載已提交表單的易列印復本。 XDP檔案可作為記錄檔案範本。 客戶下載的記錄檔案會根據XDP檔案中指定的版面進行格式化。

執行以下步驟來設定最適化表單的記錄檔案：

1. 在AEM編寫執行個體中，按一下 **Forms > Forms和檔案。**
1. 選取表單，然後按一下 **檢視屬性**.
1. 在「屬性」視窗中，點選 **表單模型**.
您也可以在建立表單時選取表單模型。

   >[!NOTE]
   >
   >在「表單模型」標籤中，確定您選取 **結構描述** 或 **無** 從 **選擇來源** 下拉式清單。 **[!UICONTROL 以表單範本作為表單模型的XFA型或調適型表單不支援記錄檔案。]**

1. 在「表單模型」標籤的「記錄檔案範本組態」區段中，選取下列其中一個選項。

   **無** 如果您不想為表單設定記錄檔案，請選取此選項。

   **建立表單範本為記錄檔案範本的關聯** 如果您有要用作記錄檔案範本的XDP檔案，請選取此選項。 選取此選項時，會顯示AEM Forms存放庫中可用的所有XDP檔案。 選取適當的檔案。

   選取的XDP檔案會與最適化表單建立關聯。

   **產生記錄檔案** 選取此選項可使用XDP檔案作為定義記錄檔案樣式和外觀的基本範本。 選取此選項時，會顯示AEM Forms存放庫中可用的所有XDP檔案。 選取適當的檔案。

   >[!NOTE]
   >
   >在下列情況下，請確定用來建立最適化表單的結構描述與XFA表單的結構描述（資料結構描述）相同：
   >
   >
   >
   >    * 您的最適化表單是以結構描述為基礎
   >    * 您正在使用 **建立表單範本為記錄檔案範本的關聯** 記錄檔案選項


1. 按一下 **完成。**

## 自訂記錄檔案中的品牌資訊 {#customize-the-branding-information-in-document-of-record}

產生記錄檔案時，您可以在記錄檔案索引標籤上變更記錄檔案的品牌資訊。 「記錄檔案」索引標籤包含標誌、外觀、版面、頁首與頁尾、免責宣告等選項，以及是否包含未選取的核取方塊和選項按鈕選項。

若要將您在「記錄檔案」標籤中輸入的品牌資訊當地語系化，您必須確保已正確設定瀏覽器的地區設定。 若要自訂記錄檔案的品牌資訊，請完成以下步驟：

1. 在記錄檔案中選取面板（根面板），然後點選 ![設定](assets/configure.png).
1. 點選 ![dortab](/help/forms/using/assets/dortab.png). 記錄檔案索引標籤隨即顯示。
1. 選取呈現記錄檔案的預設範本或自訂範本。 如果您選取預設範本，記錄檔案的縮圖預覽會顯示在「範本」下拉式清單下方。

   ![brandingtemplate](/help/forms/using/assets/brandingtemplate.png)

   如果您選擇選取自訂範本，請在AEM Forms伺服器上瀏覽並選取XDP。 如果您想要使用AEM Forms伺服器上尚未使用的範本，您必須先將XDP上傳至您的AEM Forms伺服器。

1. 根據您選取預設或自訂範本，以下部分或全部屬性會出現在「記錄檔案」標籤中。 適當地指定下列專案：

   * **標誌影像**：您可以選擇使用最適化表單中的標誌影像、從DAM中選擇影像，或從您的電腦上傳一個影像。
   * **表单标题**
   * **标题文本**
   * **免责声明标签**
   * **免责声明**
   * **免责声明文本**
   * **輔色**：在檔案或記錄PDF中呈現標頭文字和分隔線的色彩
   * **字型系列**：記錄檔案PDF中文字的字型系列
   * **對於核取方塊與選項按鈕元件，僅顯示選取的值**
   * **用于多个选定值的分隔符**
   * **包含未繫結至資料模型的表單物件**
   * **從記錄檔案排除隱藏的欄位**
   * **隐藏面板描述**

   如果您選取的自訂XDP範本包含多個主版頁面，則這些頁面的屬性會顯示在 **[!UICONTROL 內容]** 部分 **[!UICONTROL 記錄檔案]** 標籤。

   ![母版页  属性](assets/master-page-properties.png)

   主版頁面的屬性包括標誌影像、頁首文字、表單標題、免責宣告標籤和免責宣告文字。 您可以將最適化表單或XDP範本屬性套用至記錄檔案。 AEM Forms預設會將範本屬性套用至記錄檔案。 您也可以定義主版頁面屬性的自訂值。 如需如何在記錄檔案中套用多個主版頁面的詳細資訊，請參閱 [將多個主版頁面套用至記錄檔案](#apply-multiple-master-pages-dor).

   >[!NOTE]
   >
   >如果您使用以6.3版之前的Designer版本建立的調適型表單範本，為了使輔色和字型系列屬性發揮作用，請確定根子表單下的調適型表單範本中有以下內容：

   ```xml
   <proto>
   <font typeface="Arial"/>
   <fill>
   <color value="4,166,203"/>
   </fill>
   <edge>
   <color value="4,166,203"/>
   </edge>
   </proto>
   ```

1. 若要儲存品牌變更，請點選「完成」。

## 記錄檔案中面板的表格和欄配置 {#table-and-column-layouts-for-panels-in-document-of-record}

您的最適化表單可能很長，包含多個表單欄位。 您可能不想將記錄檔案儲存為最適化表單的精確副本。 現在您可以選擇表格或欄版面配置，以將一或多個最適化表單面板儲存在記錄檔案PDF中。

在產生記錄檔案之前，在面板的設定中，選取該面板的「記錄檔案配置」為「表格」或「欄」。 面板中的欄位會在記錄檔案中進行相應組織。

![面板中的欄位會以記錄檔案中的表格版面配置呈現](assets/dortablelayout.png)

面板中的欄位會以記錄檔案中的表格版面配置呈現

![面板中的欄位在記錄檔案中以欄版面配置呈現](assets/dorcolumnlayout.png)

面板中的欄位在記錄檔案中以欄版面配置呈現

## 記錄檔案設定 {#document-of-record-settings}

記錄檔案設定可讓您選擇要包含在記錄檔案中的選項。 例如，銀行接受表單中的姓名、年齡、社會安全號碼和電話號碼。 此表單會產生銀行帳號及分行詳細資訊。 您可以選擇在記錄檔案中只顯示名稱、社保號碼、銀行帳戶和分行詳細資訊。

元件的記錄檔案設定可在其「屬性」下使用。 若要存取元件的屬性，請選取元件並按一下 ![cmppr](assets/cmppr.png) 在覆蓋圖中。 屬性會列在側邊欄中，您可以在該側邊欄中找到以下設定。

**欄位層級設定**

* **從記錄檔案排除**：將屬性設定為true會從記錄檔案中排除欄位。 這是名為的指令碼屬性 `excludeFromDoR`. 其行為取決於 **若隱藏自DoR排除欄位** 表單層級屬性。

* **以表格顯示面板：** 如果面板中有少於6個欄位，設定屬性會將面板顯示為記錄檔案中的表格。 僅適用於面板。
* **從記錄檔案排除標題：** 設定屬性會從記錄檔案中排除面板/表格的標題。 僅適用於面板和表格。
* **從記錄檔案排除描述：** 設定屬性會從記錄檔案中排除面板/表格的說明。 僅適用於面板和表格。
* **[!UICONTROL 分頁]** > **[!UICONTROL 地標]**：決定您選取放置面板的位置。
   * **[!UICONTROL 地標]** > **[!UICONTROL 關註上一個]**：將面板放置在父面板中前一個物件的後面。
   * **[!UICONTROL 地標]** > **[!UICONTROL 在內容區域中]** >內容區域名稱：將面板放置在指定的內容區域中。
   * **[!UICONTROL 地標]** > **[!UICONTROL 下一個內容區域頂端]**：將面板放置在下一個內容區域的頂端。
   * **[!UICONTROL 地標]** > **[!UICONTROL 內容區域頂端]** >內容區域名稱：將面板放置在指定內容區域的頂端。
   * **[!UICONTROL 地標]** > **[!UICONTROL 在頁面上]** >主版頁面的名稱：將面板放置在指定的頁面上。 如果未自動插入分頁符號， [!DNL AEM Forms] 新增分頁符號。
   * **[!UICONTROL 地標]** > **[!UICONTROL 下一頁頂端]**：將面板放在下一頁的頂端。 如果未自動插入分頁符號， [!DNL AEM Forms] 新增分頁符號。
   * **[!UICONTROL 地標]** > **[!UICONTROL 頁面頂端]** >主版頁面名稱：轉譯指定的頁面時，將面板置於頁面頂端。 如果未自動插入分頁符號， [!DNL AEM Forms] 新增分頁符號。
* **[!UICONTROL 分頁]** > **[!UICONTROL 晚於]**：決定置入面板後要填滿的區域。下列欄位位於 **[!UICONTROL 晚於]** 區段：
   * **[!UICONTROL 晚於]** > **[!UICONTROL 繼續填寫父項]**：繼續合併所有要填入上層面板中之物件的資料。
   * **[!UICONTROL 晚於]** > **[!UICONTROL 前往下一個內容區域]**：在放置面板後開始填入下一個內容區域。
   * **[!UICONTROL 晚於]** > **[!UICONTROL 前往內容區域]** >內容區域名稱：放置面板後，開始填入指定的內容區域。
   * **[!UICONTROL 晚於]** > **[!UICONTROL 移至下一頁]**：在放置面板後開始填入下一頁。
   * **[!UICONTROL 晚於]** > **[!UICONTROL 移至頁面]** >頁面名稱：放置面板後開始填入指定的頁面。
* **[!UICONTROL 分頁]** > **[!UICONTROL 溢位]**：設定跨頁面之面板或表格的溢位。 下列欄位位於 **[!UICONTROL 溢位]** 區段：
   * **[!UICONTROL 溢位]** > **[!UICONTROL 無]**：開始填寫下一頁。 如果未自動插入分頁符號， [!DNL AEM Forms] 新增分頁符號。
   * **[!UICONTROL 溢位]** > **[!UICONTROL 移至內容區域]** >內容區域名稱：開始填入指定的內容區域。
   * **[!UICONTROL 溢位]** > **[!UICONTROL 移至頁面]** >頁面名稱：開始填入指定的頁面。

如需如何在記錄檔案中套用分頁符號和套用多個主版頁面的詳細資訊，請參閱 [在記錄檔案中套用分頁符號](#apply-page-breaks-in-dor) 和 [將多個主版頁面套用至記錄檔案](#apply-multiple-master-pages-dor).

**表單層級設定**

* **包括DoR中未繫結欄位：** 設定屬性時，記錄檔案中會包含以結構描述為基礎的最適化表單中未繫結的欄位。 預設為true。
* **若隱藏自DoR排除欄位：** 設定要從中排除隱藏欄位的屬性 [!UICONTROL 記錄檔案] 在表單提交時。 當您啟用時 [在伺服器上重新驗證](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form-server-side-revalidation-in-adaptive-form)，伺服器會先重新計算隱藏欄位，然後再將這些欄位從 [!UICONTROL 記錄檔案].

## 在記錄檔案中套用分頁符號 {#apply-page-breaks-in-dor}

您可以使用多種方法在記錄檔案中套用分頁符號。

若要將分頁套用至記錄檔案：

1. 點選面板並選取 ![設定](/help/forms/using/assets/configure.png)
1. 展開 **[!UICONTROL 記錄檔案]** 以檢視屬性。

1. 在 **[!UICONTROL 分頁]** 區段，點選 ![資料夾](/help/forms/using/assets/folder-icon.png) 在 **[!UICONTROL 地標]** 欄位。
1. 點選 **[!UICONTROL 下一頁頂端]** 並點選 **[!UICONTROL 選取]**. 您也可以點選 **[!UICONTROL 頁面頂端]**，選取主版頁面，然後點選 **[!UICONTROL 選取]** 以套用分頁符號。
1. 點選 ![儲存](/help/forms/using/assets/save_icon.png) 以儲存屬性。

選取的面板會移至下一頁。

## 將多個主版頁面套用至記錄檔案 {#apply-multiple-master-pages-dor}

如果您選取的自訂XDP範本包含多個主版頁面，則這些頁面的屬性會顯示在 [!UICONTROL 內容] 部分 [!UICONTROL 記錄檔案] 標籤。 如需詳細資訊，請參閱 [自訂記錄檔案中的品牌資訊](#customize-the-branding-information-in-document-of-record).

您可以將不同的主版頁面套用至最適化表單的元件，藉此將多個主版頁面套用至記錄檔案。 使用 [分頁](#document-of-record-settings) 區段記錄檔案屬性以套用多個主版頁面。

以下是如何將多個主版頁面套用至記錄檔案的範例：您可以將包含四個主版頁面的XDP範本上傳至 [!DNL AEM Forms] 伺服器。 [!DNL AEM Forms] 預設會將範本屬性套用至記錄檔案。 [!DNL AEM Forms] 也會將範本中的第一個主版頁面屬性套用至記錄檔案。

若要將第二個主版頁面屬性套用至面板，而將第三個主版頁面屬性套用至後續面板，請執行下列步驟：

1. 點選面板以套用第二個主版頁面，然後選取 ![設定](assets/cmppr.png).
1. 在 **[!UICONTROL 分頁]** 區段，點選 ![資料夾](/help/forms/using/assets/folder-icon.png) 在 **[!UICONTROL 地標]** 欄位。
1. 點選 **[!UICONTROL 在頁面上]**，選取第二個主版頁面並點選 **[!UICONTROL 選取]**.
AEM Forms會將第二個主版頁面套用至最適化表單中的面板和所有後續面板。
1. 在 **[!UICONTROL 分頁]** 區段，點選 ![資料夾](/help/forms/using/assets/folder-icon.png) 在 **[!UICONTROL 晚於]** 欄位。
1. 點選 **[!UICONTROL 移至頁面]**，選取第三個主版頁面並點選 **[!UICONTROL 選取]**.
1. 點選 ![儲存](/help/forms/using/assets/save_icon.png) 以儲存屬性。
AEM Forms會將第三個主版頁面套用至最適化表單中的面板和所有後續面板。


## 使用記錄檔案時的主要考量事項 {#key-considerations-when-working-with-document-of-record}

處理最適化表單的記錄檔案時，請記住以下注意事項和限制。

* 記錄範本檔案不支援RTF文字。 因此，靜態最適化表單中或一般使用者填入的資訊中的任何RTF文字都會在記錄檔案中顯示為純文字。
* 最適化表單中的檔案片段未出現在記錄檔案中。 但是，支援自適應表單片段。
* 不支援根據XML結構描述的最適化表單產生的記錄檔案中的內容繫結。
* 當使用者請求轉譯記錄檔案時，系統會根據地區設定需求建立記錄檔案的當地語系化版本。 記錄檔案的本地化與最適化表單的本地化同時發生。 如需記錄檔案和最適化表單本地化的詳細資訊，請參閱 [使用AEM翻譯工作流程將最適化表單和記錄檔案本地化](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).
