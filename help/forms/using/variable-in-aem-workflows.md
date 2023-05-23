---
title: AEM Forms工作流程中的變數
seo-title: Variables in AEM Forms Workflows
description: 建立變數、設定變數的值，並在AEM Forms工作流程步驟中使用它。
seo-description: Create a variable, set a value for the variable, and use it in AEM Forms workflow steps.
uuid: 634a75c4-4899-478f-9e5d-a870f5efa583
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: cbf4e35a-7905-44ab-ab68-fb443443f02d
docset: aem65
exl-id: beb2b83e-e8db-40bb-915f-cb6ba3140947
source-git-commit: 936b636819eaef595fcdf9f1f3446d4ac0c28b2f
workflow-type: tm+mt
source-wordcount: '2208'
ht-degree: 0%

---

# AEM Forms工作流程中的變數{#variables-in-aem-forms-workflows}

工作流程模型中的變數是根據其資料型別儲存值的方法。 然後，您就可以在任何工作流程步驟中使用變數的名稱，來擷取儲存在變數中的值。 您也可以使用變數名稱來定義用於進行路由決定的運算式。

在AEM工作流程模型中，您可以：

* [建立變數](../../forms/using/variable-in-aem-workflows.md#create-a-variable) 根據您想要儲存在其中的資訊型別而建立的資料型別。
* [設定變數的值](../../forms/using/variable-in-aem-workflows.md#set-a-variable) 使用「設定變數」工作流程步驟。
* [使用變數](../../forms/using/variable-in-aem-workflows.md#use-a-variable) 在所有AEM Forms Workflow步驟中擷取儲存的值，並在OR Split和Goto步驟中定義路由運算式。

以下影片示範如何在AEM工作流程模型中建立、設定和使用變數：

<!-- FUTURE ERROR: YouTube and mp4 videos are not supported -->

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_introduction_1_1.mp4)

變數是現有 [中繼資料對應](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) 介面。 您可以使用 [中繼資料對應](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) 以存取使用變數儲存的中繼資料。

## 建立變數 {#create-a-variable}

您可以使用工作流程模型Sidekick中可用的變數區段來建立變數。 AEM工作流程變數支援下列資料型別：

* **基本資料型別**：長、雙、布林值、日期和字串
* **複雜的資料型別**： [檔案](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemfd/docmanager/Document.html)， [XML](https://docs.oracle.com/javase/8/docs/api/org/w3c/dom/Document.html)， [JSON](https://static.javadoc.io/com.google.code.gson/gson/2.3/com/google/gson/JsonObject.html)和表單資料模型例項。

>[!NOTE]
>
>工作流程僅支援日期型別變數的ISO8601格式。

您需要 [AEM Forms附加元件套件](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) （檔案和表單資料模型）資料型別。  使用ArrayList資料型別建立變數集合。 您可以為所有基本和複雜資料型別建立ArrayList變數。 例如，建立ArrayList變數並選取String作為子型別，以使用變數儲存多個字串值。

執行以下步驟來建立變數：

1. 在AEM執行個體上，導覽至工具 ![](/help/forms/using/assets/hammer.png) >工作流程>模型。
1. 點選 **[!UICONTROL 建立]** 和指定工作流程模型的標題和選用名稱。 選取模型並點選 **[!UICONTROL 編輯]**.
1. 點選工作流程模型Sidekick中可用的變數圖示，然後點選 **[!UICONTROL 新增變數]**.

   ![添加变量](assets/variables_add_variable_new.png)

1. 在新增變數對話方塊中，指定名稱並選取變數的型別。
1. 從中選擇資料型別 **[!UICONTROL 型別]** 下拉式清單，並指定下列值：

   * 基本資料型別 — 指定變數的選用預設值。
   * JSON或XML — 指定選用的JSON或XML結構描述路徑。 當對應並儲存此結構描述中可用的屬性至另一個變數時，系統會驗證結構描述路徑。
   * 表單資料模型 — 指定表單資料模型路徑。
   * ArrayList — 指定集合的子型別。

1. 指定變數的說明（選用），然後點選 ![done_icon](assets/done_icon.png) 以儲存變更。 變數會顯示在左窗格中的可用清單中。

建立變數時，請考量下列作法：

* 建立工作流程所需數量的變數。 不過，為了節省資料庫資源，請使用最少數目的必要變數，並儘可能重複使用變數。
* 變數會區分大小寫。 確保您在工作流程中使用相同大小寫參考變數。
* 避免在變數的名稱中使用特殊字元

## 設定變數 {#set-a-variable}

您可以使用「設定變數」步驟來設定變數的值，並定義設定值的順序。 變數的設定順序，是變數對應在設定變數步驟中列出的順序。

變數值的變更只會影響變更發生的程式例項。 例如，啟動工作流程並變更變數資料時，變更只會影響該工作流程例項。 變更不會影響先前已起始或之後已起始之工作流程的其他執行個體。

根據變數的資料型別，您可以使用下列選項來設定變數的值：

* **常值：** 知道要指定的確切值時使用選項。

* **運算式：** 根據運算式計算要使用的值時，請使用選項。 運算式會在提供的運算式編輯器中建立。

* **JSON點標籤法：** 使用選項從JSON或FDM型別變數擷取值。
* **XPATH：** 使用選項從XML型別變數擷取值。

* **相對於裝載：** 當要儲存至變數的值可在相對於承載的路徑取得時，請使用選項。

* **絕對路徑：** 當要儲存至變數的值可在絕對路徑取得時，請使用選項。

您也可以使用JSON點標籤法或XPATH標籤法來更新JSON或XML型別變數的特定元素。

### 新增變數之間的對應 {#add-mapping-between-variables}

執行以下步驟來新增變數之間的對應：

1. 在工作流程編輯頁面上，點選工作流程模型Sidekick中可用的「步驟」圖示。
1. 拖放 **設定變數** 步驟至工作流程編輯器，點選步驟並選取 ![configure_icon](assets/configure_icon.png) （設定）。
1. 在「設定變數」對話方塊中，選取 **[!UICONTROL 對應]** > **[!UICONTROL 新增對應]**.
1. 在 **對應變數** 區段，選取要儲存資料的變數、選取對應模式，然後指定要儲存在變數中的值。 對應模式會因變數型別而異。
1. 對應更多變數，以產生有意義的運算式。 點選 ![done_icon](assets/done_icon.png) 以儲存變更。

### 範例1：查詢XML變數以設定字串變數的值 {#example-query-an-xml-variable-to-set-value-for-a-string-variable}

選取XML型別的變數來儲存XML檔案。 查詢XML變數，為XML檔案中可用的屬性設定字串變數的值。 使用 **指定XML變數的XPATH** 欄位，定義要儲存在字串變數中的屬性。

在此範例中，選取 **formdata** 要儲存的XML變數 **cc-app.xml** 檔案。 查詢 **formdata** 變數來設定 **電子郵件地址** 字串變數來儲存的值 **電子郵件地址** 中可用的屬性 **cc-app.xml** 檔案。

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/set_variable_example1.mp4 "設定變數的值")

### 範例2：使用運算式來儲存根據其他變數的值 {#example2}

使用運算式來計算變數的總和，並將結果儲存在變數中。

在此範例中，使用運算式編輯器來定義運算式，以計算 **assetscost** 和 **balanceamount** 變數並儲存結果 **totalvalue** 變數。

<!-- FUTURE ERROR: YouTube and mp4 videos are not supported -->

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_expression.mp4)

## 使用運算式編輯器 {#use-expression-editor}

您也可以在執行階段使用運算式來計算變數的值。 變數提供運算式編輯器來定義運算式。

使用運算式編輯器可以：

* 使用其他工作流程變數、數字或數學運算式設定變數值。
* 在數學運算式中使用工作流程變數、字串、數字或運算式
* 新增條件以設定變數的值。
* 在條件之間新增運運算元。

![表达式编辑器](assets/variables_expression_editor_new.png)

它以適用性表單規則編輯器為基礎，有下列變更。 變數中的規則編輯器：

* 不支援函式。
* 不提供UI來檢視規則摘要
* 沒有程式碼編輯器。
* 不支援啟用和停用物件的值。
* 不支援設定物件的屬性。
* 不支援呼叫網站服務。

如需詳細資訊，請參閱 [調適型表單規則編輯器](../../forms/using/rule-editor.md).

## 使用變數 {#use-a-variable}

您可以使用變數來擷取輸入和輸出，或儲存步驟的結果。 工作流程編輯器提供兩種型別的工作流程步驟：

* 支援變數的工作流程步驟
* 不支援變數的工作流程步驟

### 支援變數的工作流程步驟 {#workflow-steps-with-support-for-variables}

「跳至」步驟、「OR分割」步驟以及所有AEM Forms工作流程步驟都支援變數。

#### OR分割步驟 {#or-split-step}

「OR分割」會在工作流程中建立分割，之後只有一個分支處於作用中狀態。 此步驟可讓您在工作流程中匯入條件式處理路徑。 您可視需要將工作流程步驟新增至每個分支。

您可以使用規則定義、ECMA指令集或外部指令集來定義分支的路由表示式。

您可以使用變數來定義使用運算式編輯器的路由運算式。 如需在「OR分割」步驟中使用路由運算式的詳細資訊，請參閱 [OR分割步驟](/help/sites-developing/workflows-step-ref.md#or-split).

在此範例中，在定義路由運算式之前，請使用 [範例2](../../forms/using/variable-in-aem-workflows.md#example2) 設定 **totalvalue** 變數。 如果下列專案的值，則分支1處於活動狀態： **totalvalue** 變數大於50000。 同樣地，您可以定義一個規則，使「分支2」成為活動狀態，如果 **totalvalue** 變數小於50000。

<!-- FUTURE ERROR: YouTube and mp4 videos are not supported -->

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_orsplit_example.mp4)

同樣地，選取外部指令碼路徑，或指定路由運算式的ECMA指令碼以評估作用中分支。 點選 **[!UICONTROL 重新命名分支]** 指定分支的替代名稱。

如需更多範例，請參閱 [建立工作流程模型](../../forms/using/aem-forms-workflow.md#create-a-workflow-model).

#### 前往步驟 {#go-to-step}

此 **移至步驟** 可讓您根據路由運算式的結果，指定工作流程模型中要執行的下一個步驟。

與「OR分割」步驟類似，您可以使用規則定義、ECMA指令集或外部指令集來定義「轉至」步驟的路由表示式。

您可以使用變數來定義使用運算式編輯器的路由運算式。 如需在「跳至」步驟中使用路由運算式的詳細資訊，請參閱 [移至步驟](/help/sites-developing/workflows-step-ref.md#goto-step).

![移至規則](assets/variables_goto_rule1_new.png)

在此範例中，如果「 」的值為「 」，則「轉至」步驟會將「複查信用卡應用程式」指定為下一個步驟。 **已執行動作** 變數等於 **需要更多資訊**.

如需在「跳至」步驟中使用規則定義的更多範例，請參閱 [模擬For循環](/help/sites-developing/workflows-step-ref.md#simulateforloop).

#### 以Forms工作流程為中心的工作流程步驟 {#forms-workflow-centric-workflow-steps}

所有AEM Forms工作流程步驟都支援變數。 如需詳細資訊，請參閱 [OSGi上以Forms為中心的工作流程](../../forms/using/aem-forms-workflow-step-reference.md).

### 不支援變數的工作流程步驟 {#workflow-steps-without-support-for-variables}

您可以使用 [中繼資料對應](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) 介面以存取工作流程步驟中不支援變數的變數。

#### 擷取變數值 {#retrieve-the-variable-value}

在ECMA指令碼中使用下列API，根據資料型別擷取現有變數的值：

| 變數資料型別 | API |
|---|---|
| 基本（長、雙、布林、日期和字串） | workItem.getWorkflowData()。getMetaDataMap()。get(variableName， type) |
| 文档 | Packages.com.adobe.aemfd.docmanager.Document doc = workItem.getWorkflowData()。getMetaDataMap()。get(&quot;docVar&quot;， Packages.com.adobe.aemfd.docmanager.Document.class)； |
| XML | Packages.org.w3c.dom.Document xmlObject = workItem.getWorkflowData()。getMetaDataMap()。get(variableName， Packages.org.w3c.dom.Document.class)； |
| 表单数据模型 | Packages.com.adobe.aem.dermis.api.FormDataModelInstance fdmObject = workItem.getWorkflowData()。getMetaDataMap()。get(variableName， Packages.com.adobe.aem.dermis.api.FormDataModelInstance.class)； |
| JSON | Packages.com.google.gson.JsonObject jsonObject = workItem.getWorkflowData()。getMetaDataMap()。get(variableName， Packages.com.google.gson.JsonObject.class)； |

您需要 [AEM Forms附加元件套件](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) （檔案和表單資料模型變數）資料型別。

**示例**

使用下列API擷取字串資料型別的值：

```javascript
workItem.getWorkflowData().getMetaDataMap().get(accname, Packages.java.lang.String)
```

#### 更新變數值 {#update-the-variable-value}

在ECMA指令碼中使用以下API來更新變數的值：

```javascript
workItem.getWorkflowData().getMetaDataMap().put(variableName, value)
```

**示例**

```javascript
workItem.getWorkflowData().getMetaDataMap().put(salary, 50000)
```

更新以下專案的值： **薪資** 變數50000。

### 設定變數以叫用工作流程 {#apiinvokeworkflow}

您可以使用API來設定變數，並傳遞它們以叫用工作流程例項。

[workflowSession.startWorkflow](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/WorkflowSession.html#startWorkflow-com.adobe.granite.workflow.model.WorkflowModel-com.adobe.granite.workflow.exec.WorkflowData-java.util.Map-) 使用model、wfData和metaData作為引數。 使用MetaDataMap設定變數的值。

在此API中， **variablename** 變數設為 **值** 使用metaData.put(variableName， value)；

```javascript
import com.adobe.granite.workflow.model.WorkflowModel;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import com.adobe.aemfd.docmanager.Document;

/*Assume that you already have a workflowSession and modelId along with the payloadType and payload*/
WorkflowData wfData = workflowSession.newWorkflowData(payloadType, payload);
MetaDataMap metaData = wfData.getMetaDataMap();
metaData.put(variableName, value); //Create a variable "variableName" in your workflow model
WorkflowModel model = workflowSession.getModel(modelId);
workflowSession.startWorkflow(model, wfData, metaData);
```

**示例**

初始化 **檔案** 檔案物件至路徑(&quot;a/b/c&quot;)，並設定 **docVar** 變數至儲存在檔案物件中的路徑。

```javascript
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkflowData;
import com.adobe.granite.workflow.model.WorkflowModel;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import com.adobe.aemfd.docmanager.Document;

/*This example assumes that you already have a workflowSession and modelId along with the payloadType and payload */
WorkflowData wfData = workflowSession.newWorkflowData(payloadType, payload);
MetaDataMap metaData = wfData.getMetaDataMap();
Document doc = new Document("/a/b/c");// initialize a document object
metaData.put("docVar",doc); //Assuming that you have created a variable "docVar" of type Document in your workflow model
WorkflowModel model = workflowSession.getModel(modelId);
workflowSession.startWorkflow(model, wfData, metaData);
```

### 使用工作流程變數將敏感使用者資料儲存在JCR以外 {#jcr-independent-persistance}

使用Forms Workflow處理的資料可能包含敏感的使用者資料，例如個人識別資訊和敏感個人資訊。 企業可以選擇將資料從JCR儲存空間儲存到由他們擁有並管理的外部資料存放區，由各種工作流程步驟處理（並使用工作流程變數傳遞）。 若要進一步瞭解如何在外部儲存空間中儲存工作流程資料，請參閱 [對客戶擁有的資料存放區使用工作流程變數](/help/sites-administering/workflows-administering.md#using-workflow-variables-customer-datastore).
[!DNL Adobe Experience Manager] 提供工作流程API [UserMetaDataPersistenceProvider](https://github.com/adobe/workflow-variable-externalizer) 以將工作流程變數儲存在外部Azure blob儲存體中。 如需有關使用API的詳細資訊，請參閱 [使用工作流程變數將敏感資料引數化，並儲存在外部資料存放區中](/help/forms/using/aem-forms-workflow.md#externalize-wf-variables).

## 編輯變數 {#edit-a-variable}

1. 在編輯工作流程頁面上，點選工作流程模型Sidekick中可用的「變數」圖示。 左窗格中的變數區段會顯示所有現有的變數。
1. 點選 ![編輯](assets/edit.png) （編輯）圖示加以選取，並位於您要編輯的變數名稱旁。
1. 編輯變數資訊並點選 ![done_icon](assets/done_icon.png) 以儲存變更。 您無法編輯 **[!UICONTROL 名稱]** 和 **[!UICONTROL 型別]** 變數的欄位。

## 刪除變數 {#delete-a-variable}

在刪除變數之前，請從工作流程中移除變數的所有參考。 確認工作流程中未使用變數。

執行以下步驟來刪除變數：

1. 在編輯工作流程頁面上，點選工作流程模型Sidekick中可用的「變數」圖示。 左窗格中的變數區段會顯示所有現有的變數。
1. 點選要刪除的變數名稱旁的「刪除」圖示。
1. 點選 ![done_icon](assets/done_icon.png) 以確認和刪除變數。

## 引用 {#references}

如需在AEM Forms工作流程步驟中使用變數的更多範例，請參閱 [AEM工作流程中的變數](https://helpx.adobe.com/experience-manager/kt/forms/using/authoring_variables_in_aem_forms-workflow1.html).
