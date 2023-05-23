---
title: 创建工作流模型
seo-title: Creating Workflow Models
description: 您可以建立工作流程模型，以定義使用者啟動工作流程時所執行的一系列步驟。
seo-description: You create a workflow model to define the series of steps executed when a user starts the workflow.
uuid: 31071d3a-d6d5-4476-9ac0-7b335de406d9
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c097b60f-bcdf-45de-babe-b4c2e2b746a1
docset: aem65
exl-id: 6790202f-0542-4779-b3ce-d394cdba77b4
source-git-commit: 840ea373537799af995c3b8ce0c8bf575752775b
workflow-type: tm+mt
source-wordcount: '2464'
ht-degree: 2%

---

# 创建工作流模型{#creating-workflow-models}

>[!CAUTION]
>
>若要使用傳統UI，請參閱 [AEM 6.3檔案](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/workflows-models.html) 以供參考。

您建立 [工作流程模型](/help/sites-developing/workflows.md#model) 定義使用者啟動工作流程時執行的一系列步驟。 您也可以定義模型屬性，例如工作流程是暫時的或使用多個資源。

當使用者啟動工作流程時，會啟動執行個體；這是對應的執行階段模型，當您建立 [同步](#sync-your-workflow-generate-a-runtime-model) 您的變更。

## 建立新工作流程 {#creating-a-new-workflow}

第一次建立新的工作流程模型時，模型會包含：

* 步驟、 **流程開始** 和 **流程結束**.
這些代表工作流程的開始和結束。 這些步驟為必要步驟，無法編輯/移除。
* 範例 **參與者** 步驟已命名 **步驟1**.
此步驟設定為指派工作專案給工作流程發起人。 編輯或刪除此步驟，並視需要新增步驟。

使用編輯器建立新工作流程：

1. 開啟 **工作流程模型** 主控台；透過 **工具**， **工作流程**， **模型** 或者，例如： [https://localhost:4502/aem/workflow](https://localhost:4502/aem/workflow)
1. 選取 **建立**，則 **建立模型**.
1. 此 **新增工作流程模型** 對話方塊隨即顯示。 輸入 **標題** 和 **名稱** （選擇性）在選取之前 **完成**.
1. 新模型會列於 **工作流程模型** 主控台。
1. 選取您的新工作流程，然後使用 [**編輯** 以開啟以進行設定](#editinganexistingworkflow)：
   ![wf-01](assets/wf-01.png)

>[!NOTE]
>
>如果以程式設計方式建立模型（使用crx套件），您也可以在中建立子資料夾：
>
>`/var/workflow/models`
>
>例如，`/var/workflow/models/prototypes`
>
>然後，此資料夾可用於 [管理對該資料夾中模型的存取權](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that).

## 編輯工作流程 {#editing-a-workflow}

您可以編輯任何現有的工作流程模型，以便：

* [定義步驟](#addingasteptoamodel-) 及其 [引數](#configuring-a-workflow-step)
* 設定工作流程屬性，包括 [階段](#configuring-workflow-stages-that-show-workflow-progress)， [工作流程是否為暫時性](#creatingatransientworkflow-) 和/或 [使用多個資源](#configuring-a-workflow-for-multi-resource-support)

編輯 [**預設及/或舊版** （現成可用）工作流程](#editing-a-default-or-legacy-workflow-for-the-first-time) 有額外步驟，以確保 [安全複製](/help/sites-developing/workflows-best-practices.md#locations-workflow-models) 會在您進行變更前完成。

工作流程更新完成後，您必須使用 **同步** 至 **產生執行階段模型**. 另請參閱 [同步處理您的工作流程](#sync-your-workflow-generate-a-runtime-model) 以取得詳細資訊。

### 同步工作流程 — 產生執行階段模型 {#sync-your-workflow-generate-a-runtime-model}

**同步** （在編輯器工具列中的右側）產生 [執行階段模型](/help/sites-developing/workflows.md#runtime-model). 執行階段模型是使用者啟動工作流程時實際使用的模型。 如果您沒有 **同步** 如此一來，您所做的變更將無法在執行階段使用。

當您（或任何其他使用者）對您必須使用的工作流程進行變更時 **同步** 產生執行階段模型 — 即使個別對話方塊（例如，步驟）有自己的儲存選項。

當變更與執行階段（儲存的）模型同步化時， **已同步** 會改為顯示。

某些步驟具有必填欄位和/或內建驗證。 當這些條件不滿足時，當您嘗試 **同步** 模型。 例如，當尚未為定義參與者時 **參與者** 步驟：

![wf-21](assets/wf-21.png)

### 首次編輯預設或舊版工作流程 {#editing-a-default-or-legacy-workflow-for-the-first-time}

當您開啟 [預設和/或舊版模型](/help/sites-developing/workflows.md#workflow-types) 進行編輯：

* 步驟瀏覽器無法使用（左側）。
* 有一個 **編輯** 動作（右側）。
* 最初，模型及其屬性會以唯讀模式呈現為：
   * 預設工作流程位於 `/libs`
   * 舊版工作流程位於 `/etc`
選取 
**編輯** 將：
* 將工作流程副本帶入 `/conf`
* 讓步驟瀏覽器可供使用
* 讓您進行變更

>[!NOTE]
>
>另請參閱 [工作流程模型的位置](/help/sites-developing/workflows-best-practices.md#locations-workflow-models) 以取得進一步資訊。

![wf-22](assets/wf-22.png)

### 將步驟新增至模型 {#adding-a-step-to-a-model}

您需要將步驟新增至模型，以表示要執行的活動 — 每個步驟都會執行特定活動。 標準AEM例項中提供一系列步驟元件。

當您編輯模型時，可用的步驟會出現在 **步驟瀏覽器**. 例如：

![wf-10](assets/wf-10.png)

>[!NOTE]
>
>如需搭配AEM安裝之主要步驟元件的相關資訊，請參閱 [工作流程步驟參考](/help/sites-developing/workflows-step-ref.md).

若要將步驟新增至工作流程模型：

1. 開啟現有的工作流程模型以進行編輯。 從 **工作流程模型** 主控台，選取所需的模式，然後 **編輯**.
1. 開啟「步驟」瀏覽器；使用 **切換側面板**，位於頂端工具列的最左側。 在此编辑器中，您可以：

   * **篩選** 以取得特定步驟。
   * 使用下拉式選擇器，將選取範圍限制在特定的步驟群組中。
   * 選取顯示說明圖示 ![wf-stepinfo-icon](assets/wf-stepinfo-icon.png) 以顯示適當步驟的詳細資訊。

   ![wf-02](assets/wf-02.png)

1. 將適當的步驟拖曳到模型中的所需位置。

   例如， **參與者步驟**.

   新增至流量後，您可以 [設定步驟](#configuring-a-workflow-step).

   ![wf-03](assets/wf-03.png)

1. 視需要新增任意數量的步驟或其他更新。

   在執行階段，步驟會依照它們在模型中出現的順序執行。 新增步驟元件後，可將它們拖曳至模型中的不同位置。

   您也可以複製、剪下、貼上、分組或刪除現有步驟；就像使用 [頁面編輯器。](/help/sites-authoring/editing-content.md)

   也可以使用工具列選項摺疊/展開分割步驟： ![wf-collapseexpand-toolbar-icon](assets/wf-collapseexpand-toolbar-icon.png)

1. 確認變更，透過 **同步** （編輯器工具列）以產生執行階段模型。

   另請參閱 [同步處理您的工作流程](#sync-your-workflow-generate-a-runtime-model) 以取得詳細資訊。

### 設定工作流程步驟 {#configuring-a-workflow-step}

您可以 **設定** 並使用自訂工作流程步驟的行為 **步驟屬性** 對話方塊。

1. 若要開啟 **步驟屬性** 步驟的對話方塊：

   * 按一下/點選工作流程模型中的* *步驟，然後選取 **設定** 元件工具列中的。

   * 在步驟上按兩下。
   >[!NOTE]
   >
   >如需搭配AEM安裝之主要步驟元件的相關資訊，請參閱 [工作流程步驟參考](/help/sites-developing/workflows-step-ref.md).

1. 設定 **步驟屬性** 視需要；可用的屬性取決於步驟型別，可能也有幾個可用的標籤。 例如，預設值 **參與者步驟**，在新工作流程中顯示為 `Step 1`：

   ![wf-11](assets/wf-11.png)

1. 使用勾號確認您的更新。
1. 確認變更，透過 **同步** （編輯器工具列）以產生執行階段模型。

   另請參閱 [同步處理您的工作流程](#sync-your-workflow-generate-a-runtime-model) 以取得詳細資訊。

### 建立暫時性工作流程 {#creating-a-transient-workflow}

您可以建立 [暫時性](/help/sites-developing/workflows.md#transient-workflows) 建立新模型或編輯現有模型時的工作流程模型：

1. 開啟的工作流程模型 [編輯](#editinganexistingworkflow).
1. 選取 **工作流程模型屬性** （從工具列）。
1. 在對話方塊中啟動 **暫時性工作流程** （或視需要停用）：

   ![wf-07](assets/wf-07.png)

1. 確認變更，透過 **儲存並關閉**；後面接著 **同步** （編輯器工具列）以產生執行階段模型。

   另請參閱 [同步處理您的工作流程](#sync-your-workflow-generate-a-runtime-model) 以取得詳細資訊。

>[!NOTE]
>
>當您在中執行工作流程時 [暫時性](/help/sites-developing/workflows.md#transient-workflows) 模式AEM不會儲存任何工作流程歷史記錄。 因此， [時間表](/help/sites-authoring/basic-handling.md#timeline) 不會顯示與該工作流程相關的任何資訊。

## 讓工作流程模型可在觸控式UI中使用 {#classic2touchui}

如果傳統UI中出現工作流程模型，但在的選取彈出式選單中遺失 **[!UICONTROL 時間表]** 觸控式UI的邊欄，然後依照設定使其可用。 下列步驟說明如何使用名為的工作流程模型 **[!UICONTROL 請求啟用]**.

1. 確認模型不適用於觸控式UI。 使用存取資產 `/assets.html/content/dam` 路徑。 選取資產。 開啟 **[!UICONTROL 時間表]** 在左側邊欄中。 按一下 **[!UICONTROL 開始工作流程]** 並確認 **[!UICONTROL 請求啟用]** 模型不存在於彈出式清單中。

1. 瀏覽至 **[!UICONTROL 「工具」>「一般」>「標籤」]**. 選取 **[!UICONTROL 工作流程]**.

1. 選取 **[!UICONTROL 「建立」>「建立標籤」]**. 設定 **[!UICONTROL 標題]** 作為 `DAM` 和 **[!UICONTROL 名稱]** 作為 `dam`. 選取 **[!UICONTROL 提交]**.
   ![在工作流程模型中建立標籤](assets/workflow_create_tag.png)

1. 導覽至 **[!UICONTROL 「工具」>「工作流程」>「模型」]**. 選取 **[!UICONTROL 請求啟用]**，然後選取 **[!UICONTROL 編輯]**.

1. 選取 **[!UICONTROL 編輯]**，開啟 **[!UICONTROL 頁面資訊]** 功能表，然後從那裡選取 **[!UICONTROL 開啟屬性]** 並前往 **[!UICONTROL 基本]** 標籤（如果尚未開啟）。

1. 新增 `Workflow : DAM` 至 **[!UICONTROL 標籤]** 欄位。 使用核取方塊（勾號）確認選取範圍。

1. 確認新增標籤，使用 **[!UICONTROL 儲存並關閉]**.
   ![編輯模型的頁面屬性](assets/workflow_model_edit_activation1.png)

1. 使用完成此程式 **[!UICONTROL 同步]**. 觸控式UI現在提供工作流程。

### 設定多資源支援的工作流程 {#configuring-a-workflow-for-multi-resource-support}

您可以為以下專案設定工作流程模型 [多重資源支援](/help/sites-developing/workflows.md#multi-resource-support) 建立新模型或編輯現有模型時：

1. 開啟的工作流程模型 [編輯](#editinganexistingworkflow).
1. 選取 **工作流程模型屬性** （從工具列）。

1. 在對話方塊中啟動 **多重資源支援** （或視需要停用）：

   ![wf-08](assets/wf-08.png)

1. 確認變更，透過 **儲存並關閉**；後面接著 **同步** （編輯器工具列）以產生執行階段模型。

   另請參閱 [同步處理您的工作流程](#sync-your-workflow-generate-a-runtime-model) 以取得詳細資訊。

### 設定工作流程階段（顯示工作流程進度） {#configuring-workflow-stages-that-show-workflow-progress}

[工作流程階段](/help/sites-developing/workflows.md#workflow-stages) 協助在處理任務時以視覺效果呈現工作流程的進度。

>[!CAUTION]
>
>如果工作流程階段定義於 **頁面屬性**，但不用於任何工作流程步驟，則進度列不會顯示任何進度（無論目前的工作流程步驟為何）。

可用的階段會在工作流程模型中定義；現有的工作流程模型可以更新以包含階段定義。 您可以為工作流程模型定義任意數量的階段。

若要定義 **階段** 針對您的工作流程：

1. 開啟工作流程模型以進行編輯。
1. 選取 **工作流程模型屬性** （從工具列）。 然後開啟 **階段** 標籤。
1. 新增（和定位）您的必要專案 **階段**. 您可以為工作流程模型定義任意數量的階段。

   例如：

   ![wf-08-1](assets/wf-08-1.png)

1. 按一下 **儲存並關閉** 以儲存屬性。
1. 將階段指派給工作流程模型中的每個步驟。 例如：

   ![wf-09](assets/wf-09.png)

   一個階段可指派給多個步驟。 例如：

   | **步骤** | **暂存** |
   |---|---|
   | 步骤 1 | 创建 |
   | 步骤 2 | 创建 |
   | 步骤 3 | 审核 |
   | 步骤 4 | 批准 |
   | 步骤 5 | 批准 |
   | 步骤 6 | 完成 |

1. 確認變更，透過 **同步** （編輯器工具列）以產生執行階段模型。

   另請參閱 [同步處理您的工作流程](#sync-your-workflow-generate-a-runtime-model) 以取得詳細資訊。

## 在封裝中匯出工作流程模型 {#exporting-a-workflow-model-in-a-package}

若要匯出封裝中的工作流程模型：

1. 使用建立新套件 [封裝管理員](/help/sites-administering/package-manager.md#package-manager)：

   1. 透過以下方式瀏覽至封裝管理員： **工具**， **部署**， **套件**.

   1. 按一下 **建立封裝**.
   1. 指定 **封裝名稱**，以及任何其他需要的詳細資訊。
   1. 单击&#x200B;**确定**。

1. 按一下 **編輯** （在新封裝的工具列上）。

1. 開啟 **篩選器** 標籤。

1. 選取 **新增篩選器** 並指定工作流程模型的路徑 *設計*：

   `/conf/global/settings/workflow/models/<*your-model-name*>`

   按一下 **完成**.

1. 選取 **新增篩選器** 並指定 *執行階段* 工作流程模型：

   `/var/workflow/models/<*your-model-name*>`

   按一下 **完成**.

1. 為您的模型使用的任何自訂指令碼新增其他篩選器。
1. 按一下 **儲存** 以確認您的篩選定義。
1. 選取 **建置** 從封裝定義的工具列。
1. 選取 **下載** 從封裝工具列。

## 使用工作流程處理表單提交 {#using-workflows-to-process-form-submissions}

您可以設定要由所選工作流程處理的表單。 使用者提交表單時，會建立新的工作流程例項，並將表單提交的資料當作其裝載。

若要設定要與表單搭配使用的工作流程：

1. 建立新頁面並開啟它以進行編輯。
1. 新增 **表單** 元件至頁面。
1. **設定** 此 **表單開始** 出現在頁面中的元件。
1. 使用 **開始工作流程** 若要從可用的工作流程中選取所需的工作流程：

   ![wf-12](assets/wf-12.png)

1. 使用勾號確認新表單設定。

## 測試工作流程 {#testing-workflows}

測試工作流程時，好的做法是使用各種裝載型別；包括與為其開發工作流程的型別不同的型別。 例如，如果您打算讓工作流程處理資產，請將頁面設定為裝載以進行測試，並確保其不會擲回錯誤。

例如，測試您的新工作流程，如下所示：

1. [開始您的工作流程模型](/help/sites-administering/workflows-starting.md) 從主控台。
1. 定義 **裝載** 並確認。

1. 視需要執行動作，以便進行工作流程。
1. 在工作流程執行時監視記錄檔。

您也可以設定AEM以顯示 **偵錯** 記錄檔中的訊息。 另請參閱 [記錄](/help/sites-deploying/configure-logging.md) 如需詳細資訊以及開發完成時，請將 **記錄層級** 返回 **資訊**.

## 示例 {#examples}

### 範例：建立（簡單）工作流程以接受或拒絕發佈請求 {#example-creating-a-simple-workflow-to-accept-or-reject-a-request-for-publication}

為了說明建立工作流程的一些可能性，以下範例建立 `Publish Example` 工作流程。

1. [建立新的工作流程模型](#creating-a-new-workflow).

   新工作流程將包含：

   * **流程开始**
   * `Step 1`
   * **流程结束**

1. 刪除 `Step 1` （因為此範例中的步驟型別錯誤）：

   * 按一下步驟並選取 **刪除** 元件工具列中的。 確認動作。

1. 從 **工作流程** 選取步驟瀏覽器，拖曳 **參與者步驟** 放到工作流程上，並將其放置在 **流程開始** 和 **流程結束**.
1. 若要開啟屬性對話方塊，請執行下列其中一種動作：

   * 按一下參與者步驟並選取 **設定** 元件工具列中的。
   * 連按兩下參與者步驟。

1. 在 **通用** tab enter `Validate Content` 針對兩個 **標題** 和 **說明**.
1. 開啟 **使用者/群組** 標籤：

   * 啟動 **透過電子郵件通知使用者**.
   * 選取 `Administrator` ( `admin`)，適用於 **使用者/群組** 欄位。

   >[!NOTE]
   >
   >若要傳送電子郵件， [需要設定郵件服務和使用者帳戶詳細資料](/help/sites-administering/notification.md).

1. 使用勾號確認更新。

   您將會返回工作流程模型的概觀，在此參與者步驟將重新命名為 `Validate Content`.

1. 拖曳 **Or分割** 放到工作流程上，並將其放置在 `Validate Content` 和 **流程結束**.
1. 開啟 **Or分割** 進行設定。
1. 配置：

   * **通用**：指定分割名稱。
   * **分支1**：選取 **預設路由**.

   * **分支2**：確保 **預設路由** 未選取。

1. 確認您對的更新 **OR分割**.
1. 拖曳 **參與者步驟** 在左側分支中，開啟屬性，指定下列值，然後確認變更：

   * **标题**: `Reject Publish Request`

   * **使用者/群組**：例如， `projects-administrators`

   * **透過電子郵件通知使用者**：啟動以透過電子郵件通知使用者。

1. 拖曳 **程式步驟** 在右側分支中，開啟屬性，指定下列值，然後確認變更：

   * **标题**: `Publish Page as Requested`

   * **程式**：選取 `Activate Page`. 此程式會將選取的頁面發佈至發行者執行處理。

1. 按一下 **同步** （編輯器工具列）以產生執行階段模型。

   另請參閱 [同步處理您的工作流程](#sync-your-workflow-generate-a-runtime-model) 以取得詳細資訊。

   您的新工作流程模型看起來會像這樣：

   ![wf-13](assets/wf-13.png)

1. 將此工作流程套用至您的頁面，以便在使用者移至 **完成** 此 **驗證內容** 步驟，他們可以選取是否要 **依要求發佈頁面**，或 **拒絕發佈請求**.

   ![chlimage_1-72](assets/chlimage_1-72.png)

### 範例：使用ECMA指令碼定義OR分割的規則 {#defineruleecmascript}

**OR分割** 步驟可讓您在工作流程中匯入條件式處理路徑。

若要定義OR規則，請依照下列步驟進行：

1. 建立兩個指令碼並將它們儲存在存放庫中，例如在下方：

   `/apps/myapp/workflow/scripts`

   >[!NOTE]
   >
   >指令碼必須具有 [函式 `check()`](#function-check) 會傳回布林值。

1. 編輯工作流程並新增 **OR分割** 至模型。
1. 編輯以下專案的屬性： **分支1** 的 **OR分割**：

   * 將此專案定義為 **預設路由** 藉由設定 **值** 至 `true`.

   * 作為 **規則**，設定指令碼的路徑。 例如：
      `/apps/myapp/workflow/scripts/myscript1.ecma`
   >[!NOTE]
   >
   >您可以視需要切換分支順序。

1. 編輯的屬性 **分支2** 的 **OR分割**.

   * 作為 **規則**，將路徑設定為其他指令碼。 例如：
      `/apps/myapp/workflow/scripts/myscript2.ecma`

1. 設定每個分支中個別步驟的屬性。 確定 **使用者/群組** 已設定。
1. 按一下 **同步** （編輯器工具列）來保留您對執行階段模型的變更。

   另請參閱 [同步處理您的工作流程](#sync-your-workflow-generate-a-runtime-model) 以取得詳細資訊。

#### 函式Check() {#function-check}

>[!NOTE]
>
>另請參閱 [使用ECMAScript](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript).

以下範例指令碼傳回 `true` 如果節點為 `JCR_PATH` 位於 `/content/we-retail/us/en`：

```
function check() {
    if (workflowData.getPayloadType() == "JCR_PATH") {
      var path = workflowData.getPayload().toString();
      var node = jcrSession.getItem(path);

      if (node.getPath().indexOf("/content/we-retail/us/en") >= 0) {
       return true;
      } else {
       return false;
      }
     } else {
      return false;
     }
}
```

### 範例：自訂的啟用請求 {#example-customized-request-for-activation}

您可以自訂任何現成的工作流程。 若要使用自訂行為，請覆蓋適當工作流程的詳細資訊。

例如， **請求啟用**. 此工作流程用於發佈中的頁面 **網站** 當內容作者沒有適當的復寫許可權時，會自動觸發和。 另請參閱 [自訂頁面編寫 — 自訂啟動請求工作流程](/help/sites-developing/customizing-page-authoring-touch.md#customizing-the-request-for-activation-workflow) 以取得更多詳細資料。
