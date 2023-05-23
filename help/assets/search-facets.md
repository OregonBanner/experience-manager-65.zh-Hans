---
title: 搜尋Facet以篩選搜尋結果
description: 如何在中建立、修改和使用搜尋Facet [!DNL Adobe Experience Manager].
contentOwner: AG
role: Admin, Developer
feature: Search
exl-id: acaf46e6-ff70-4825-8922-ce8f82905a92
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '2417'
ht-degree: 17%

---

# 搜索 Facet {#search-facets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/search-facets.html?lang=en) |
| AEM 6.5 | 本文 |

全企業範圍部署 [!DNL Adobe Experience Manager Assets] 具有儲存許多資產的容量。 有時候，如果您只使用的一般搜尋功能，尋找合適的資產可能會很費時又費力 [!DNL Experience Manager].

使用「篩選器」面板中的搜尋Facet為您的搜尋體驗新增更多精細度，並讓搜尋功能更有效率且更通用。 搜尋Facet會新增多個維度（述詞），讓您執行更複雜的搜尋。 「篩選器」面板包含幾個標準Facet。 您也可以新增自訂搜尋多面向。

總而言之，搜尋Facet可讓您以多種方式搜尋資產，而非使用單一、預先決定的分類順序。 您可以輕鬆向下鑽研至所需的詳細資訊層級，以更集中地搜尋。

例如，如果您要尋找影像，您可以選擇想要點陣圖或向量影像。 您可以指定影像的MIME型別，進一步縮小搜尋範圍。 同樣地，在搜尋檔案時，您可以指定格式，例如PDF或MS Word。

## 新增述詞 {#adding-a-predicate}

「篩選器」面板中顯示的搜尋Facet是使用述詞在基礎搜尋表單中定義。 若要顯示更多或不同的Facet，您可以將述詞新增至預設表單，或使用包含您所選的Facet的自訂表單。

若要進行全文檢索，請新增 **[!UICONTROL 全文]** 表單的述詞。 使用屬性述詞來搜尋符合您指定之單一屬性的資產。 使用「選項」述詞來搜尋符合特定屬性的一個或多個值的資產。 新增日期範圍述詞，以搜尋在指定日期範圍內建立的資產。

1. 按一下 [!DNL Experience Manager] 標誌，然後前往 **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 搜尋Forms]**.
1. 從 [!UICONTROL 搜尋Forms] 頁面，選取 **[!UICONTROL 資產管理搜尋邊欄]**，然後按一下 **[!UICONTROL 編輯]** ![編輯圖示](assets/do-not-localize/aemassets_edit.png).

   >[!NOTE]
   >
   >使用預先設定的資料夾搜尋功能 [!DNL Assets] 從舊版的Admin Search Rail，執行以下步驟：
   >
   >1. 導覽至 `/conf/global/settings/dam/search/facets/assets/jcr:content/items` 在CRXDE中。
   >1. 刪除 `type` 節點。
   >1. 從路徑 `/libs/settings/dam/search/facets/assets/jcr:content/items`，複製節點 `asset`， `directory`， `typeor`， `excludepaths`、和 `searchtype` 至步驟1中提及的路徑。
   >1. 保存更改。


1. 在 [!UICONTROL 編輯搜尋Forms] 頁面，從拖曳述詞 **[!UICONTROL 選取述詞]** 標籤移至主窗格。 例如，拖曳 **[!UICONTROL 屬性述詞]**.

   ![選取並移動述詞以自訂搜尋篩選器](assets/drag_predicate.png)

   *圖：選取並移動述詞以自訂搜尋篩選器。*

1. 在 [!UICONTROL 設定] 標籤，輸入欄位標籤、預留位置文字和述詞說明。 為您要與述詞關聯的中繼資料屬性指定有效的名稱。 中的標題標籤 [!UICONTROL 設定] tab可識別所選述詞的型別。

1. 在[!UICONTROL 属性名称]字段中，为要与谓词关联的元数据属性指定有效名称。该名称是执行搜索时所依据的名称。例如，输入 `jcr:content/metadata/dc:description` 或 `./jcr:content/metadata/dc:description`。

   您也可以從選取對話方塊中選取現有節點。

   ![在「屬性名稱」欄位中將中繼資料屬性與述詞建立關聯](assets/property_settings.png)

   在「屬性名稱」欄位中將中繼資料屬性與述詞建立關聯

1. 按一下 **[!UICONTROL 預覽]** ![預覽](assets/do-not-localize/preview_icon.png) 以產生「篩選器」面板在新增述詞後的預覽。
1. 在預覽模式中檢閱述詞的配置。

   ![在提交變更之前預覽搜尋表單](assets/preview-1.png)

   在提交變更之前預覽搜尋表單

1. 若要關閉預覽，請按一下 **[!UICONTROL 關閉]** ![關閉](assets/do-not-localize/close.png) 在預覽的右上角。
1. 按一下 **[!UICONTROL 完成]** 以儲存設定。
1. 導覽至「 」中的「搜尋」面板 [!DNL Assets] 使用者介面。 屬性述詞會新增至面板。
1. 在文字方塊中輸入要搜尋之資產的說明。 例如，輸入 `Adobe`. 當您執行搜尋時，資產與說明相符 `Adobe` 會列在搜尋結果中。

## 新增選項述詞 {#adding-an-options-predicate}

選項述詞可讓您在「篩選器」面板中新增多個搜尋選項。 您可以在「篩選器」面板中選取這些選項中的一個或多個來搜尋資產。 例如，若要根據檔案型別搜尋資產，請在搜尋表單中設定選項，例如「影像」、「多媒體」、「檔案」和「封存」。 設定這些選項後，當您在「濾鏡」面板中選取「影像」選項時，會對GIF、JPEG、PNG等型別的資產執行搜尋。

若要將選項對應至個別屬性，請建立選項的節點結構，並在Options述詞的Property Name屬性中提供父節點的路徑。 父節點應為型別 `sling`： `OrderedFolder`. 選項應為型別 `nt:unstructured`. 選項節點應具有屬性 `jcr:title` 和 `value` 已設定。

此 `jcr:title` 屬性是顯示在「篩選器」面板上之選項的使用者易記名稱。 此 `value` 欄位用於查詢，以符合指定的屬性。

當您選取選項時，會根據 `value` 選項節點及其子節點的屬性（如果有）。 系統會遍歷option節點下的整個樹狀結構， `value` 每個子節點的屬性會使用OR運算來組合，以形成搜尋查詢。

例如，如果您为文件类型选择“图像”，则资产的搜索查询将通过使用 OR 操作组合 `value` 属性来构建。**********`jcr:content/metadata/dc:format`

![檔案型別的值屬性（如CRXDE中所見）可用於搜尋查詢](assets/filetype-value-property.png)

檔案型別的值屬性（如CRXDE中所見）可用於搜尋查詢

您不必在CRXDE存放庫中手動建立選項的節點結構，而是可以透過指定對應的索引鍵值配對，在JSON檔案中定義選項。 在&#x200B;**[!UICONTROL 属性名称]**&#x200B;字段中指定 JSON 文件的路径。例如，您可以定义键值对、`image/bmp`、`image/gif`、`image/jpeg` 和 `image/png`，并指定它们的值，如以下示例 JSON 文件中所示。在 **[!UICONTROL 屬性名稱]** 欄位中，您可以指定此檔案的CRXDE路徑。

```json
{
    "options" :
 [
          {"value" : "image/bmp","text" : "BMP"},
          {"value" : "image/gif","text" : "GIF"},
          {"value" : "image/jpeg","text" : "JPEG"},
          {"value" : "image/png","text" : "PNG"}
 ]
}
```

如果要使用現有節點，請使用選取對話方塊來指定它。

>[!NOTE]
>
>Options述詞是包含屬性述詞的自訂包裝函式，用於示範所描述的行為。 目前沒有可用的REST端點可原生支援此功能。

1. 按一下 [!DNL Experience Manager] 標誌，然後前往 **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 搜尋Forms]**.
1. 從 **[!UICONTROL 搜尋Forms]** 頁面，選取 **[!UICONTROL 資產管理搜尋邊欄]**，然後按一下 **[!UICONTROL 編輯]**.
1. 在“编 **[!UICONTROL 辑搜索表单]** ”页中，将“选 **[!UICONTROL 项谓词]** ”从“选 **** 择谓词”选项卡拖至主窗格。
1. 在&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中，输入属性的标签和名称。例如，要根据资产的格式搜索资产，请为标签指定用户友好名称，例如&#x200B;**[!UICONTROL 文件类型]**。在属性字段中指定执行搜索时所依据的属性，例如 `jcr:content/metadata/dc:format.`
1. 执行下列操作之一：

   * 在 **[!UICONTROL 屬性名稱]** 欄位，提及JSON檔案的路徑，您可在此定義選項的節點，並指定對應的索引鍵值配對。
   * 按一下 `+` 「選項」欄位旁的符號，用來指定您要在「濾鏡」面板中提供之選項的顯示文字和值。 若要新增其他選項，請按一下 `+` 符號並重複該步驟。

1. 确保取消选中&#x200B;**[!UICONTROL 单选]**，以允许用户一次为文件类型选择多个选项（例如，“图像”、“文档”、“多媒体”和“存档”）。如果选中&#x200B;**[!UICONTROL 单选]**，则用户一次只能为文件类型选择一个选项。

   ![選項述詞中的可用欄位](assets/options_predicate.png)

   選項述詞中的可用欄位

1. 在 **[!UICONTROL 說明]** 欄位，輸入選擇性說明，然後按一下 **[!UICONTROL 完成]**.
1. 導覽至「搜尋」面板。 「選項」述詞會新增至 **搜尋** 面板。 的選項 **[!UICONTROL 檔案型別]** 會顯示為核取方塊。

## 新增多值屬性述詞 {#adding-a-multi-value-property-predicate}

多值屬性述詞可讓您搜尋多個值的資產。 請考量您在中擁有多個產品影像的情況 [!DNL Assets] 且每個影像的中繼資料都包含與產品相關聯的SKU編號。 您可以使用此述詞來根據多個SKU編號搜尋產品影像。

1. 按一下 [!DNL Experience Manager] 標誌，然後前往 **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 搜尋Forms]**.
1. 在「搜尋Forms」頁面上，選取 **[!UICONTROL 資產管理搜尋邊欄]**，然後按一下 **[!UICONTROL 編輯]** ![編輯圖示](assets/do-not-localize/aemassets_edit.png).
1. 在“编辑搜索表单”页中，将&#x200B;**[!UICONTROL 多值属性谓词]**&#x200B;从&#x200B;**[!UICONTROL 选择谓词]**&#x200B;选项卡拖到主窗格。
1. 在 **[!UICONTROL 設定]** 索引標籤中，輸入述詞的標籤和預留位置文字。 在屬性欄位中指定搜尋所依據的屬性名稱，例如 `jcr:content/metadata/dc:value`. 您也可以使用選取對話方塊來選取節點。
1. 确保选中&#x200B;**[!UICONTROL 分隔符支持]**。在&#x200B;**[!UICONTROL 输入分隔符]**&#x200B;字段中，指定要用于分隔各个值的分隔符。默认情况下，指定逗号为分隔符。您可以指定其他分隔符。
1. 在 **說明** 欄位，輸入選擇性說明，然後按一下 **[!UICONTROL 完成]**.
1. 導覽至「 」中的「篩選器」面板 [!DNL Assets] 使用者介面。 **[!UICONTROL 多值属性]**&#x200B;谓词已添加到面板。
1. 在「多值」欄位中指定多個值（以分隔符號分隔），然後執行搜尋。 述詞會擷取與指定值完全相符的文字。

## 新增標籤述詞 {#adding-a-tags-predicate}

標籤述詞可讓您對資產執行標籤式搜尋。 依預設， [!DNL Assets] 根據您指定的標籤，在資產中搜尋一或多個相符標籤。 換言之，搜尋查詢會使用指定的標籤執行OR操作。 不過，您可以使用「比對所有標籤」選項來搜尋包含您所指定之所有標籤的資產。

1. 按一下 [!DNL Experience Manager] 標誌，然後前往 **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 搜尋Forms]**.
1. 從「搜尋Forms」頁面中選取 **[!UICONTROL 資產管理搜尋邊欄]** 然後按一下 **[!UICONTROL 編輯]** ![編輯圖示](assets/do-not-localize/aemassets_edit.png).
1. 在「編輯搜尋表單」頁面中，拖曳 **[!UICONTROL 標籤述詞]** 從「選取述詞」標籤移至主窗格。
1. 在設定索引標籤中，輸入述詞的預留位置文字。 在屬性欄位中指定搜尋所依據的屬性名稱，例如 *jcr：content/metadata/cq：tags*. 或者，您也可以從選取對話方塊中選取CRXDE中的節點。
1. 設定此述詞的根標籤路徑屬性，以填入標籤清單中的各種標籤。
1. 选择&#x200B;**[!UICONTROL 显示“匹配所有标记”选项]**，以搜索包含您指定的所有标记的资产。

1. 在 **[!UICONTROL 說明]** 欄位，輸入選擇性說明，然後按一下 **[!UICONTROL 完成]**.
1. 導覽至「搜尋」面板。 此 **[!UICONTROL 標籤]** 述詞會新增至「搜尋」面板。
1. 指定您要依據其搜尋資產的標籤，或從建議清單中選取。

1. 選取 **[!UICONTROL 全部符合]** 以搜尋包含您所指定之所有標籤的相符專案。

## 新增其他述詞 {#adding-other-predicates}

與新增「屬性」述詞或「選項」述詞的方式類似，您也可以將下列其他述詞新增至「搜尋」面板：

| 述詞名稱 | 描述 | 属性 |
|---|---|---|
| [!UICONTROL 全文] | 搜尋述詞，以在整個資產節點上執行全文搜尋。 它使用jcr：contains運運算元對應。 如果要對資產節點的特定部分執行全文搜尋，您可以指定相對路徑。 | <ul><li>标签</li><li>占位符</li><li>属性名称</li><li>描述</li></ul> |
| [!UICONTROL 路径浏览器] | 搜尋述詞，以在預先設定的根路徑搜尋資料夾和子資料夾中的資產 | <ul><li>占位符</li><li>根路径</li><li>描述</li></ul> |
| [!UICONTROL 路径] | 使用它來篩選位置的結果。 您可以將不同的路徑指定為選項。 | <ul><li>标签</li><li>路径</li><li>描述</li></ul> |
| [!UICONTROL 發佈狀態] | 搜尋述詞，以根據資產的發佈狀態來搜尋資產 | <ul><li>标签</li><li>属性名称</li><li>描述</li></ul> |
| [!UICONTROL 相对日期] | 搜尋述詞，以根據資產的相對建立日期來搜尋資產。 例如，您可以設定選項，例如2個月前、3週前等。 | <ul><li>标签</li><li>属性名称</li><li>相對日期</li></ul> |
| [!UICONTROL 范围] | 搜尋述詞，可搜尋指定範圍內的資產。 在「搜尋」面板中，您可以指定範圍的最小值和最大值。 | <ul><li>标签</li><li>属性名称</li><li>描述</li></ul> |
| [!UICONTROL 日期范围] | 搜尋述詞，以搜尋在指定範圍內建立的資產，以取得日期屬性。 在「搜尋」面板中，您可以使用日期選擇器來指定開始和結束日期。 | <ul><li>标签</li><li>占位符</li><li>属性名称</li><li>範圍文字（從）</li><li>範圍文字（至）</li><li>描述</li></ul> |
| [!UICONTROL 日期] | 根據日期屬性的資產滑桿式搜尋的搜尋述詞。 | <ul><li>标签</li><li>属性名称</li><li>描述</li></ul> |
| [!UICONTROL 檔案大小] | 搜尋述詞，以根據資產的大小進行搜尋。 這是以Silder為基礎的述詞，您可以從可設定的節點選取滑桿選項。 預設選項是在CRXDE存放庫中的/libs/dam/options/predicates/filesize中定義。 檔案大小以位元組為單位。 | <ul><li>标签</li><li>属性名称</li><li>路径</li><li>描述</li></ul> |
| [!UICONTROL 上次修改的资源] | 搜尋述詞以搜尋最近修改的資產 | <ul><li>属性名称</li><li>屬性值</li><li>描述</li></ul> |
| [!UICONTROL 發佈狀態] | 搜尋述詞，以根據資產的發佈狀態來搜尋資產 | <ul><li>标签</li><li>属性名称</li><li>描述</li></ul> |
| [!UICONTROL 评分] | 根據資產的平均評等搜尋資產的述詞 | <ul><li>标签</li><li>属性名称</li><li>選項路徑</li><li>描述</li></ul> |
| [!UICONTROL 到期状态] | 搜尋述詞，以根據資產的到期狀態來搜尋資產 | <ul><li>标签</li><li>属性名称</li><li>描述</li></ul> |
| [!UICONTROL 隐藏] | 定義隱藏欄位屬性以搜尋資產的搜尋述詞 | <ul><li>属性名称</li><li>屬性值</li><li>描述</li></ul> |

## 還原預設搜尋Facet {#restoring-default-search-facets}

依預設，鎖定圖示 ![鎖定已關閉圖示](assets/do-not-localize/lock_closed_icon.svg) 顯示於之前 **[!UICONTROL 資產管理搜尋邊欄]** 在 **[!UICONTROL 搜尋Forms]** 頁面。 「搜尋Forms」頁面上某個選項的鎖定圖示表示預設設定完整且未自訂。 圖示 ![鎖定已關閉圖示](assets/do-not-localize/lock_closed_icon.svg) 如果您將搜尋Facet新增至表單，指出預設表單已修改，則會消失。

![鎖定圖示](assets/locked_admin_rail.png)

若要還原預設的搜尋Facet，請執行下列步驟：

1. 選取 **[!UICONTROL 資產管理搜尋邊欄]** 在 **[!UICONTROL 搜尋Forms]** 頁面。
1. 按一下 **[!UICONTROL 刪除]** ![deleteoutline](assets/do-not-localize/deleteoutline.png) （在工具列中）。
1. 在確認對話方塊中，按一下 **[!UICONTROL 刪除]** 以移除自訂變更。

   刪除搜尋Facet的自訂變更後，鎖定圖示 ![鎖定已關閉圖示](assets/do-not-localize/lock_closed_icon.svg) 在此之前重新出現 **[!UICONTROL 資產管理搜尋邊欄]** 在 **[!UICONTROL 搜尋Forms]** 頁面。

## 使用者許可權 {#user-permissions}

如果您未獲指派管理員角色，以下列出執行與搜尋Facet相關的編輯、刪除和預覽動作所需的許可權。

| 操作 | 权限 |
| ------------------- | ---------------------------------------------------------------- |
| [!UICONTROL 编辑] | 的讀取和寫入許可權 `/apps` CRXDE中的節點 |
| [!UICONTROL 删除] | 的讀取、寫入和刪除許可權 `/apps` CRXDE中的節點 |
| [!UICONTROL 预览] | 的讀取、寫入和刪除許可權 `/var/dam/content` CRXDE中的節點 此外，上的讀取和寫入許可權 `/apps` 節點。 |

>[!MORELIKETHIS]
>
>* [擴充資產搜尋功能](searchx.md)
>* [搜索资产](search-assets.md)

