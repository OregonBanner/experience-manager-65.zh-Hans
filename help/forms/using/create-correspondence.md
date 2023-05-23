---
title: 建立對應
seo-title: Create Correspondence
description: 建立信函範本後，您可以透過管理資料、內容和附件，使用它在AEM Forms中建立通訊。
seo-description: After you have created a letter template, you can use it to create correspondence in AEM Forms by managing data, content, and attachments.
uuid: 48cf2b26-c9b4-4127-9ea0-1b36addbff60
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 87742cb2-357b-421f-b79d-e355887ddec0
docset: aem65
feature: Correspondence Management
exl-id: da966787-a3b9-420f-8b7c-f00d05c61d43
source-git-commit: c47b4dcfd2fbdcb0b98ad815f5b04d8f593e4f64
workflow-type: tm+mt
source-wordcount: '3855'
ht-degree: 0%

---

# 建立對應{#create-correspondence}

## 在「建立通訊」使用者介面中建立通訊 {#create-correspondence-in-the-create-correspondence-user-interface}

晚於 [信函範本是在「通訊管理」中建立](../../forms/using/create-letter.md)，一般使用者/代理程式/索賠理算師可以在「建立通訊」使用者介面中開啟信件，並透過輸入資料、設定內容和管理附件來建立通訊。 最後，索賠理算師或代理商可以在預覽模式下管理內容並提交信件。

### 預覽通訊 {#preview-a-correspondence}

使用以下步驟選取要預覽的字母：

1. 在「字母」頁面上，點選 **選取**.
1. 點選適當的字母以選取它。

   ![選取字母](assets/1_selectletter.png)

   選取字母

1. 對於資料字典型信件，請選取 **預覽** > **預覽**. 或者，若是非資料字典型信件，請選取 **預覽**. 您也可以將滑鼠指標暫留在信函上（無需選取信函），然後點選「信函預覽」圖示以預覽。

   >[!NOTE]
   >
   >如果資料字典未與信函相關聯，信函預覽會開啟。 否則，如果信函是以資料字典為基礎，「通訊管理」會在「預覽」選單中顯示「預覽」和「自訂」選項，您可以選取兩個選項之一。 您也可以將測試資料與資料字典建立關聯。 當 [資料字典有相關的測試資料](../../forms/using/data-dictionary.md#p-working-with-test-data-p)，然後選取預覽選項時，一般預覽會開啟，並填入測試資料。

1. 若要在預覽信函時呈現信函，您必須是管理員或屬於下列群組：

   * forms-users （在作者執行個體上預覽）
   * cm-agent-users （用於發佈執行個體上的轉譯）

   如果您沒有所需的許可權，請要求管理員提供適當的存取許可權。 如需建立使用者並將其新增至群組的詳細資訊，請參閱 [新增使用者或群組至群組](/help/sites-administering/security.md). 如果您在沒有適當許可權的情況下嘗試轉譯通訊，則會出現404錯誤頁面。

1. 如果您已選取 **預覽** > **自訂**，對話方塊隨即開啟。 在對話方塊中，選取與資料字典對應的資料檔案以預覽字母，然後選取 **預覽**. 系統會根據特定字母的資料字典建立資料檔案。 如需資料檔案的詳細資訊，請參閱 [資料字典](../../forms/using/data-dictionary.md#p-working-with-test-data-p).

   ![預覽字母](assets/8_previewcustomdatafile.png)

1. 信件HTML預覽（行動表單預覽）依預設會開啟，其中的「資料」索引標籤會成為焦點。

   如需行動表單及其支援功能的詳細資訊，請參閱 [行動Forms和PDF forms之間的功能差異](https://helpx.adobe.com/livecycle/help/mobile-forms/feature-differentiation-mobile-forms-pdf.html).

   有三個標籤：資料、內容和附件。 如果沒有資料元素（預留位置變數和版面配置欄位），信函會直接在中開啟，並顯示「內容」索引標籤。 附件標籤僅在附件存在或資料庫存取權啟用時才能使用。

   >[!NOTE]
   >
   >如需在信函預覽的HTML或PDF轉譯模式之間切換的詳細資訊，請參閱 [變更信件的轉譯模式](#changerenditionmode). 如需在Correspondence Management和AEM中支援PDF的詳細資訊，請參閱 [終止NPAPI瀏覽器外掛程式及其影響](https://helpx.adobe.com/acrobat/kb/change-in-support-for-acrobat-and-reader-plug-ins-in-modern-web-.html). <!-- and [PDF Forms to HTML5 Forms](https://helpx.adobe.com/aem-forms/kb/pdf-forms-to-html5-forms.html). THIS URL IS A 404 AND NO SUITABLE REPLACEMENT TOPIC WAS FOUND. CONSIDER DELETING OR ADDING NEW LINK. COMMENTING OUT SO USERS DON'T CLICK IT. -->

### 輸入資料 {#enterdata}

在「資料」索引標籤中，填入可用的版面配置欄位和預留位置。

1. 視需要在欄位中輸入資料和內容變數。 填寫所有標示星號(&#42;)以啟用 **提交** 按鈕。

   點選HTML信函預覽中的資料欄位值，以反白顯示「資料」索引標籤中的對應資料欄位。

   ![在信函中輸入資料](assets/2_enterdata.png) ![2_1_enterdata](assets/2_1_enterdata.png)

### 管理内容 {#managecontent}

在內容索引標籤中，管理檔案片段和信件內容變數等內容。

1. 選取 **內容**. 「通訊管理」會顯示信函的內容標籤。

   ![內容標籤 — 內容中的反白顯示模組](assets/3_content.png)

1. 視需要在「內容」標籤中編輯內容模組。 若要將焦點置於內容階層中的相關內容模組，您可以點選信函預覽中的相關行或段落，或直接點選內容階層中的內容模組。

   例如，在下圖中選擇了「我們已檢閱…… 」一行，並在「內容」標籤中選取了相關的內容模組。

   ![4_highlightmoduleincontent](assets/4_highlightmoduleincontent.png)

   在「內容」或「資料」標籤中，點選「反白選取的模組」 ( ![highlightselectedmodulesincontentccr](assets/highlightselectedmodulesincontentccr.png))，您可以停用或啟用在信函預覽中選取相關文字、段落或資料欄位時，前往內容/資料模組的功能。HTML信函預覽左上角

   如需建立通訊使用者介面中各種模組可用的動作的詳細資訊，請參閱 [建立通訊使用者介面中可用的動作和資訊](#actions-and-info-available-in-the-create-correspondence-content-tab).

1. 若要尋找內容模組，請使用「尋找」欄位。 輸入內容模組的完整或部分名稱或標題，以在通訊中搜尋它。
1. 點選「顯示」圖示( ![顯示](assets/display.png))、文字、條件或目標區域前方的「 」，以在字母中顯示或隱藏它。
1. 若要編輯內嵌或可編輯的文字模組，請點選相關的 **編輯** 圖示( ![edittextmodule](assets/edittextmodule.png))或在信函預覽中連按兩下相關的文字模組。

   系統會顯示文字編輯器以編輯文字並設定其格式。

   瀏覽器中的預設拼字檢查程式會檢查文字編輯器中的拼字。 若要管理拼字和文法檢查，您可以編輯瀏覽器的拼字檢查程式設定，或安裝瀏覽器外掛程式/附加元件來檢查拼字和文法。

   您也可以在文字編輯器中使用各種鍵盤快速鍵來管理、編輯文字及設定文字格式。 如需詳細資訊，請參閱 [文字編輯器](/help/forms/using/keyboard-shortcuts.md#correspondence-management) 通訊管理鍵盤快速鍵中的鍵盤快速鍵。

   ![5_edittextmodule](assets/5_edittextmodule.png)

   您可能想要重複使用存在於另一個檔案應用程式中的多個文欄位落。 您可以直接複製並貼上文字，例如從MS Word、HTML頁面或任何其他應用程式中複製。

   您可以在可編輯的文字模組中複製並貼上文字的一或多個段落。 例如，您可能有MS Word檔案，其中包含可接受的居住證明專案符號清單，如下所示：

   ![pastetextmsword](assets/pastetextmsword.png)

   您可以直接將MS Word檔案中的文字複製並貼上至可編輯的文字模組。 專案符號清單、字型和文字顏色等格式會保留在文字模組中。

   ![pastetexteditablemodule](assets/pastetexteditablemodule.png)

   >[!NOTE]
   >
   >不過，貼上文字的格式有些 [限制](https://helpx.adobe.com/aem-forms/kb/cm-copy-paste-text-limitations.html).

   您可以使用Tab鍵縮排信函中的文字和數字。 例如，您可以使用Tab鍵將清單中的多欄文字對齊為表格格式。

   ![Tabspace](assets/tabspaces.png)

   範例：使用Tab鍵將多欄文字對齊為表格格式

   >[!NOTE]
   >
   >有關設定文字模組和字母的定位點間距的詳細資訊，請參閱 [有關使用定位點間距來排列文字的更多資訊](https://helpx.adobe.com/aem-forms/kb/cm-tab-spacing-limitations.html).

1. 如有需要，請在通訊中插入特殊字元。 例如，您可以使用「特殊字元」浮動視窗來插入：

   * 幣別符號，例如€、¥和£
   * 數學符號，例如∑、√、∂和^
   * 標點符號，例如&quot;和&quot;

   ![特殊字元](assets/specialcharacters.png)

   Correspondence Management已內建支援210個特殊字元。 管理員可以 [透過自訂新增對更多/自訂特殊字元的支援](../../forms/using/custom-special-characters.md).

1. 若要反白顯示\強調可編輯內嵌模組中的部分文字，請選取文字並點選「反白顯示色彩」。

   ![letterbackgroundcolor](assets/letterbackgroundcolor.png)

   您可以直接點選基本顏色 `**[A]**` 出現在「基本色彩」調色盤中或點選 **選取** 使用滑桿之後 `**[B]**` 以選擇適當的顏色陰影。

   或者，您也可以移至「進階」標籤，選取適當的色相、明亮度和飽和度 `**[C]**` 以建立精確顏色，然後點選「選取」 `**[D]**` 以套用顏色來反白顯示文字。

   ![textbackgroundcolor](assets/textbackgroundcolor.png)

1. 進行適當的內容和格式變更，然後點選 **儲存**. 點選( ![editnextmoduleccr](assets/editnextmoduleccr.png))以在可編輯文字模組之間移動，或點選 **儲存並下一步** 儲存變更並移至下一個可編輯的文字模組。
1. 系統也會顯示每個分支的未填變數。 當沒有未填變數時，未填變數會顯示為0。 如果存在未填滿的變數，您可以點選分支以展開該分支，然後找到未填滿的變數。 使用內容工具列來刪除內容、增加/減少內容的縮排，以及在內容之前/之後插入分頁符號。

   您可以在資料模組上方或下方插入分頁符號，即使它們屬於清單和條件的一部分亦然。

1. 點選「開啟/關閉內容變數」 ( ![opencontentvariables](assets/opencontentvariables.png))以開啟內容變數並適當地填入。
1. 正確填入未填入的變數後，未填入的變數計數會設為0。

   在「建立通訊」使用者介面中，未填入的變數計數會顯示在包含至少一個變數之任何模組階層的每個層級。 如果模組包含未填變數，則計數會顯示在變數、模組、目標區域和信函範本層級。

   未填寫的變數計數包括：

   * 僅限未受保護的資料字典和預留位置變數。 變數計數不包含配置或受保護的資料字典變數。
   * 必填欄位。
   * 配置欄位（如果欄位是必填欄位且已繫結至使用者）。
   * 僅限不重複變數例項。 如果模組、目標區域或信函範本包含兩個或多個相同變數的例項，則計數會顯示為1 （一）。 但是，對於每個執行個體，計數會顯示為1。

   未填入的變數計數不包括已取消選取的模組。 如果信函範本中包含但信函中未包含模組，則此模組中的未填變數計數不會顯示。

   對於目標區域、模組和變數，計數會顯示在信函範本中每個物件的右側。 但是，對於完整範本，計數會顯示在「建立通訊」狀態列中。

   信函範本中的模組會顯示未填入的變數計數，如下所述：

   * **文字** 顯示文字模組中所包含的不重複未填入預留位置變數和資料字典元素的總和。
   * **條件** 顯示條件中所包含的不重複未填入條件變數與結果模組中所包含變數的總和。
   * **清單** 顯示指派給清單之模組中所包含的所有不重複未填入變數的總和。
   * **目標區域** 顯示指派給目標區域的模組中所包含的所有不重複未填入變數的總和。

   關於具有預設值的變數，請注意下列事項：

   * 布林值變數欄位預設為 *false*. 不過，變數會視為未填入。 這表示變數計數包含所有布林值變數欄位 *false*.

   * 數值變數欄位預設為 *0 （零）*. 不過，變數會視為未填入。 這表示變數計數包含所有具有值的數值變數欄位 *0 （零）*.



#### 「建立通訊內容」標籤中可用的動作和資訊 {#actions-and-info-available-in-the-create-correspondence-content-tab}

**目标区域**

* 插入空白行：插入新的空白行。
* 插入內嵌文字：插入新文字模組。
* 順序鎖定（資訊）：表示無法變更內容的順序。
* 未填滿的值（資訊）：指出目標區域中未填滿的變數數目。

**模块**

* 選擇（眼睛圖示）：包含\排除字母中的模組。
* 略過專案符號（適用於清單模組及其子模組）：略過特定模組中的專案符號。
* 在之前分頁（適用於目標區域的子模組）：在模組之前插入分頁。
* 之後的分頁符號（適用於目標區域的子模組）：在模組之前插入分頁符號。
* 未填滿的值（資訊）：指出目標區域中未填滿的變數數目。
* 編輯（僅限文字模組）：開啟RTF編輯器以編輯文字模組。
* 資料面板（文字和條件模組）：開啟模組的所有變數。

**清單模組**

* 插入空白行：插入新的空白行。
* 內容庫：開啟內容庫以將模組新增至清單。
* 清單設定（僅限巢狀清單）：
* 順序鎖定（資訊）：表示無法變更清單專案的順序。

### 管理附件 {#manage-attachments}

1. 選取 **附件**. 「通訊管理」會依照建立信函範本時的設定，顯示可用的附件。
1. 點選檢檢視示可選擇不隨信件提交附件，點選附件中的十字可從信件中刪除。 對於指定的附件，在建立信函範本時，若為「必要」，「檢視」和「刪除」圖示會停用。
1. 點選「資料庫存取」 ( ![程式庫存取](assets/libraryaccess.png))圖示以存取「內容資料庫」，將DAM資產插入為附件。

   >[!NOTE]
   >
   >「資料庫存取」圖示僅在編寫信函時啟用資料庫存取權才可用。

1. 如果在建立通訊時未鎖定附件的順序，您可以選取附件並點選向下和向上箭頭來重新排序附件。

   如需詳細資訊，請參閱 [附件傳遞](#attachmentdelivery).

### 在預覽中管理內容並提交信件 {#manage-content-in-preview-and-submit-the-letter}

您可以進行版面配置和內容相關變更，以確保信件看起來如您所願，並將信件提交給各種發佈程式。

1. 若要反白顯示信函中的所有可編輯內容，請點選 **反白可編輯區段**.

   字母的可編輯內容會以灰色背景反白顯示。

   ![反白可編輯內容](assets/4_highlightmoduleincontent-1.png)

1. 視需要在「內容」標籤中編輯內容模組。 若要將焦點置於內容階層中的相關內容模組，您可以點選信函預覽中的相關行或段落，或直接點選內容階層中的內容模組。

   例如，在下圖中選取「允許我們存取……」一行，並在「內容」標籤中選取對應的內容模組。

   點選內容中的反白選取模組( ![highlightselectedmodulesincontentccr](assets/highlightselectedmodulesincontentccr.png))，您可以停用或啟用在信函預覽中點選相關文字、段落或資料欄位時，在「內容」標籤中反白標示內容模組的功能。

   如需建立通訊使用者介面中各種模組可用的動作的詳細資訊，請參閱 [建立通訊使用者介面中可用的動作和資訊](#actions-and-info-available-in-the-create-correspondence-content-tab).

1. 若要在信函中新增分頁符號，請點選您要插入分頁符號的位置，然後選取「在之前分頁符號」或「在之後分頁符號」 ( ![pagebreakbeforeafter](assets/pagebreakbeforeafter.png))。

   信函中會插入明確的分頁符號預留位置。 若要檢視明確的分頁符號如何影響字母，請參閱平面化PDF預覽。

   >[!NOTE]
   >
   >由於行動表單不支援分頁符號，頁首和頁尾只會出現一次。 不過，您可以在版面中明確設定頁首和頁尾（每頁），以顯示於行動表單預覽中。 此外，信函中的空白頁面（如果有的話）不會出現在行動表單預覽中。

   ![明確的分頁符號](assets/8_pagebreak.png)

1. 若要將信函另存為草稿（稍後可繼續處理），請點選「另存為草稿」。 若要使用此選項，您的信件必須是 [已發佈](../../forms/using/publishing-unpublishing-forms.md#publishanasset). 如需詳細資訊，請參閱下的草稿例項 [儲存草稿並提交信件例項](#savingdrafts).

   ![saveasdraft](assets/saveasdraft.png)

   草稿字母名稱對話方塊會出現，其中包含字母例項ID。 您可以選擇編輯此ID。 記下字母ID，然後點選 **完成**. 您稍後可以使用此識別碼來 [重新載入草稿字母](submit-letter-topostprocess.md#reloaddraft).

1. 若要以平面化PDF預覽信函，並在提交時具有完全相同的版面配置和分頁符號，請點選( ![預覽](assets/preview.png))預覽。

   信件會顯示為平面化PDF。 平面化PDF是字母的精確表示，因為會以正確的字型、分行符號和字母版面配置來提交。

   >[!NOTE]
   >
   >如果您使用Mozilla Firefox和HTML轉譯型別，若要將信函預覽為平面化PDF，請務必使用原生瀏覽器外掛程式，而不是Acrobat外掛程式。 若要選取原生瀏覽器外掛程式，請前往Mozilla Firefox的設定，若要進行內容型別PDF，請選取「在Firefox中預覽」。

1. 如果您認為平面化PDF預覽令人滿意，請點選 **提交** 以提交信件。 或者，若要變更信件，請點選 **退出預覽** 返回信函的建立通訊UI預覽，以在信函中進行變更。 點選「提交」時，如果「發佈」執行個體上啟用了「管理信件執行個體」設定，則會產生提交信件執行個體。

   如需詳細資訊，請參閱「儲存草稿與提交信件例項」下的「草稿例項」。

   您也可以將信函另存為草稿，以便稍後對信函進行變更。

   進行必要的變更後，您可以從HTML5預覽提交信件，或再次點選「預覽」以檢閱平面化的PDF輸出。

   如需HTML5表單與PDF forms之間差異的詳細資訊，請參閱 [HTML5表單與PDF forms之間的功能差異](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md).

## 儲存草稿並提交信件例項 {#savingdrafts}

在「建立通訊」使用者介面中轉譯信函時，您可以將信函儲存為正在檢視。

有兩種型別的信件例項可以儲存：草稿例項和提交例項。

* **草稿例項**：草稿例項會擷取您正在預覽的信件的目前狀態。 若要儲存草稿執行個體，請先確定信函及其引用的所有資產都處於「已發佈」狀態。 如需發佈信件的詳細資訊，請參閱 [發佈資產](../../forms/using/publishing-unpublishing-forms.md#publishanasset). 您必須先發佈信件，才能將其儲存為草稿，因為當您發佈信件時，會在該時間點建立信件的版本、其相依資產和資料。 您或其他使用者無法編輯信函的已發佈版本，且稍後可以還原，而不會與已發佈版本有任何非預期的差異。 您可以稍後返回此執行個體，並從您離開的地方繼續。

* **提交執行個體**：提交執行個體會在提交時擷取字母的狀態。 提交執行個體會在信件執行個體經過後處理後，連同使用者在「建立通訊」使用者介面中輸入的資料一起，儲存信件執行個體的PDF狀態。

只有正在發佈執行個體上檢視信函時，才能儲存這類執行個體。 依預設，在執行個體上儲存是關閉的。 若要啟用儲存信件例項，請執行下列步驟。

1. 在AEM中，使用下列URL開啟伺服器的Adobe Experience Manager Web Console設定： https://&lt;server>：&lt;port>/&lt;contextpath>/system/console/configMgr
1. 尋找 **[!UICONTROL 通訊管理設定]** 並按一下。
1. Check **[!UICONTROL 管理發布時的信件例項]** 設定，然後按一下 **[!UICONTROL 儲存]**.

### 啟用儲存草稿功能 {#enable-save-draft-feature}

在發佈執行個體上發佈信件或儲存草稿之前，請在作者和發佈執行個體上執行以下步驟，以啟用「另存為草稿」功能：

此 *cq：lastReplicationAction*， *cq：lastreplicated* 和 *cq：lastReplicatedBy* 依預設，屬性不會移轉至發佈執行個體。 為了結轉 *cq：lastReplicationAction*， *cq：lastreplicated* 和 *cq：lastReplicatedBy* 屬性以發佈執行個體，停用 [!UICONTROL com.day.cq.replication.impl.ReplicationPropertiesFilterFactory] 元件。 若要停用元件：

1. 在作者執行個體上，開啟Adobe Experience Manager Web主控台元件主控台。 預設URL為 `http://author-server:port/system/console/components`

1. 搜尋 **[!UICONTROL com.day.cq.replication.impl.ReplicationPropertiesFilterFactory]** 元件。

1. 按一下 ![停用按鈕](/help/forms/using/assets/enablebutton.png) 圖示以停用 [!UICONTROL com.day.cq.replication.impl.ReplicationPropertiesFilterFactory] 元件。

![作者執行個體](/help/forms/using/assets/replicationproperties.png)

若要啟用另存為草稿功能，請在以下位置取代現有URL： [!UICONTROL VersionRestoreManager作者URL] ，並使用作者例項的URL。 取代URL：

1. 在發佈執行個體上，開啟 [!UICONTROL Adode Manager Web主控台設定]. 預設URL為 `https://publish-server:port/system/console/configMgr`

1. 搜尋並開啟 **[!UICONTROL 通訊管理 — 作者執行個體版本還原設定]** 元件。

1. 找到 **[!UICONTROL VersionRestoreManager作者URL]** 欄位並指定作者例項的URL。

1. 单击“保存”。

![发布实例](/help/forms/using/assets/correspondencemanagement.png)

開啟儲存信函例項時，您可以選擇儲存信函例項的位置。 儲存信件例項有兩個選項：本機儲存或遠端儲存。

### 本機儲存 {#local-save}

信件執行個體會儲存在發佈執行個體上，並在製作執行個體上反向復寫。

### 遠端儲存 {#remote-save}

此選項適用於擔心在發佈執行個體上儲存使用者資料的人，這些執行個體通常位於公司防火牆之外。 開啟遠端儲存時，信件執行個體不會儲存在發佈執行個體上，但會遠端儲存在透過LiveCycle使用者端SDK設定指定的處理作者上。

#### 啟用遠端儲存 {#enable-remote-save}

1. 在AEM中，使用下列URL開啟伺服器的Adobe Experience Manager Web主控台設定： `https://<server>:<port>/<contextpath>/system/console/configMgr`
1. 搜尋 **[!UICONTROL 通訊管理設定]** 並按一下。
1. 找到 **[!UICONTROL 遠端儲存]** 設定、檢查並點按 **[!UICONTROL 儲存]**.

#### 指定處理作者設定 {#specify-processing-author-settings}

1. 在AEM中，使用下列URL開啟伺服器的Adobe Experience Manager Web主控台設定： `https://<server>:<port>/system/console/configMgr`

   ![Adobe Experience Manager Web主控台設定](assets/2configmanager.png)

1. 在此頁面中，找到AdobeLiveCycle使用者端SDK設定，然後按一下以展開它。

1. 在處理伺服器URL中，輸入LiveCycle伺服器的名稱、提供登入資訊，然後按一下 **儲存**.

   ![輸入LiveCycle伺服器的名稱和登入資訊](assets/3configmanager.png)

1. 必要時，請設定您要用來存取伺服器的使用者名稱和密碼。

#### 附件傳遞 {#attachmentdelivery}

* 信函附件可在PDF中後處理，在信函提交後建立。
* 使用伺服器端API以互動式或非互動式PDF轉譯信函時，轉譯的PDF會包含附件作為PDF附件。
* 當使用「建立通訊」使用者介面將與信件範本相關聯的貼文處理載入為「提交」或「完成通訊」操作的一部分時，附件會作為「清單」傳遞&lt;com.adobe.idp.document> 在AttachmentDocs引數中。
* 現成可用的傳遞機制（例如電子郵件和列印）也會傳遞附件以及產生的信件的PDF。

## 信件預覽的轉譯模式：行動表單預覽和PDF預覽 {#rendition-modes-of-letter-preview-mobile-forms-preview-and-pdf-preview}

AEM Forms Correspondence Management在建立通訊UI中將信件顯示為HTML。 不過，「通訊管理」仍支援恢復為PDF預覽，而不是HTML預覽。 如需有關在預覽的HTML和PDF模式之間切換的詳細資訊，請參閱 [變更信件的轉譯模式](#changerenditionmode).

以下是HTML和PDF預覽中可用的優點和功能。

**行動表單/HTML預覽的優點**

* **點選資料欄位值以反白顯示對應的資料欄位**：在建立通訊使用者介面中，您可以點選信函中的資料欄位值，以反白顯示「資料」索引標籤中的對應資料欄位。 如需詳細資訊，請參閱 [輸入資料](#enterdata).

* **瀏覽器支援**：瀏覽器會逐步撤銷對NPAPI的支援，而這會影響信件的PDF預覽。 信件的HTML/行動表單預覽不受此影響。
* **反白顯示字母中的可編輯內容**：在「建立通訊」使用者介面中，您可以點選「反白可編輯內容」 ，以灰色反白信函中的所有可編輯內容。 如需詳細資訊，請參閱 [管理內容](#managecontent).

`<li>` `<li>Benefits of HTML preview  <ul>   <li>Right to left</li>   <li>NPAPI</li>   <li>Highlight Editable Content</li>  </ul> </li>` `<li>Benefits of PDF preview  <ul>   <li>Page Break</li>   <li>Final Preview</li>  </ul> </li>`
`<li>` `<li>Benefits of HTML preview  <ul>   <li>Right to left</li>   <li>NPAPI</li>   <li>Highlight Editable Content</li>  </ul> </li>` `<li>Benefits of PDF preview  <ul>   <li>Page Break</li>   <li>Final Preview</li>  </ul> </li>`  **PDF預覽的優點**

* **分頁符號**：在PDF預覽中，您可以檢視分頁字母對其輸出的確切影響。
* **最終預覽**：在PDF預覽中，您可以檢視字母的確切格式和外觀，因為字母會出現在輸出中。

如需PDF forms中指令碼支援的相關資訊，請參閱 [指令碼支援](https://help.adobe.com/en_US/livecycle/11.0/ScriptingSupport/index.html).

如需HTML5表單中指令碼支援的詳細資訊，請參閱 [HTML5表單的指令碼支援](/help/forms/using/scripting-support.md).

### 變更信件的轉譯模式 {#changerenditionmode}

依預設，建立通訊UI使用HTML或行動表單來呈現信件預覽。 行動表單預覽不會在任何瀏覽器中呈現問題，因為它使用瀏覽器的原生外掛程式，不需要其他外掛程式。 您可以將字母預覽模式變更為PDF。 但是，瀏覽器限制可能會造成信函的互動PDF預覽的不同功能問題。

如需瀏覽器與信函預覽相容性的詳細資訊，請參閱 [終止NPAPI瀏覽器外掛程式及其影響](https://helpx.adobe.com/acrobat/kb/change-in-support-for-acrobat-and-reader-plug-ins-in-modern-web-.html).

若要變更信函的預覽模式，請完成下列步驟：

1. 前往 `https://[system]:'port'/system/console/configMgr` 並視需要以管理員身分登入。
1. 前往 **[!UICONTROL 通訊管理設定]** > **[!UICONTROL 轉譯型別]** 並選取 **HTML轉譯** （預設）或 **PDF轉譯**.
1. 单击“**[!UICONTROL 保存]**”。
