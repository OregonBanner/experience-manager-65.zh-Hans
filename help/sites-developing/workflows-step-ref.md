---
title: 工作流步骤参考
seo-title: Workflow Step Reference
description: 工作流步骤参考
seo-description: null
uuid: 88bf6997-73a1-4639-82aa-5dff08d3ef86
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e3afffd0-d90c-4bd0-b814-f7aeac6ceb6d
docset: aem65
exl-id: 8de78bde-2fcb-4221-873e-59e347ff2d74
source-git-commit: 768576e300b655962adc3e1db20fc5ec06a5ba6c
workflow-type: tm+mt
source-wordcount: '3246'
ht-degree: 2%

---

# 工作流步骤参考 {#workflow-step-reference}

工作流程模型包含一系列各種型別的步驟。 根據型別，您可以使用引數和指令碼來設定和擴展這些步驟，以提供您需要的功能和控制。

>[!NOTE]
>
>本節介紹標準工作流程步驟。
>
>如需模組特定的步驟，請參閱下列內容：
>
>* [AEM Forms工作流程步驟參考](/help/forms/using/aem-forms-workflow-step-reference.md)
>* [使用媒體處理常式和工作流程處理資產](/help/assets/media-handlers.md)
>


## 步骤属性 {#step-properties}

每個步驟元件都有 **步驟屬性** 對話方塊，可讓您定義及編輯所需的屬性。

### 步驟屬性 — 一般標籤 {#step-properties-common-tab}

下列屬性的組合適用於大多數工作流程步驟元件，位於 **通用** 屬性對話方塊的「 」標籤：

* **標題**
步驟的標題。

* **說明**
步驟的說明。

* **工作流暂存**

   要套用的下拉式選擇器 [階段](/help/sites-developing/workflows.md#workflow-stages) 移至步驟。

* **超时**

   步驟「逾時」之前的期間。
您可以選取： **關閉**， **立即**， **1h**， **6h**， **12h**， **24h**.

* **超时处理程序**

   控制步驟逾時時工作流程的處理常式。 例如，`Auto Advancer`

* **处理程序前进**

   選取此選項可自動將工作流程推進至執行後的下一個步驟。 如果未選取，實作指令碼必須處理工作流程推進。

### 步驟屬性 — 使用者/群組標籤 {#step-properties-user-group-tab}

下列屬性適用於許多工作流程步驟元件，位於 **使用者/群組** 屬性對話方塊的「 」標籤：

* **透過電子郵件通知使用者**

   * 當工作流程到達步驟時，您可以傳送電子郵件通知參與者。
   * 如果啟用，系統會傳送電子郵件給屬性所定義的使用者 **使用者/群組**，或至群組的每個成員（若已定義群組）。

* **用户/组**

   * 下拉式選取方塊可讓您導覽至並選取使用者或群組。
   * 如果您將步驟指派給特定使用者，則只有此使用者可以在該步驟上操作。
   * 如果您將步驟指派給整個群組，則當工作流程達到此步驟時，此群組中的所有使用者都會在其 **工作流程收件匣**.
   * 另請參閱 [參與工作流程](/help/sites-authoring/workflows-participating.md) 以取得詳細資訊。

## AND 拆分 {#and-split}

此 **AND拆分** 會在工作流程中建立分割，之後兩個分支都會啟用。 您可視需要將工作流程步驟新增至每個分支。 此步驟可讓您在工作流程中引進多個處理路徑。 例如，您可以允許同時執行某些稽核步驟，以節省時間。

![wf-26](assets/wf-26.png)

### AND拆分 — 設定 {#and-split-configuration}

若要設定分割：

* 編輯 **AND分割屬性**：

   * **分割名稱**：指派名稱以利說明
   * 選取所需的分支數；2、3、4或5。

* 視需要將工作流程步驟新增至分支。

   ![wf-27](assets/wf-27.png)

## 容器步骤 {#container-step}

容器步驟會啟動另一個作為子工作流程執行的工作流程模型。

此容器可讓您重複使用工作流程模型，以實作步驟的共同順序。 例如，翻譯工作流程模型可用於多個編輯工作流程。

![wf-28](assets/wf-28.png)

### 容器步驟 — 設定 {#container-step-configuration}

若要設定步驟，請編輯並使用下列標籤：

* [通用](#step-properties-common-tab)
* **容器**

   * **子工作流程**：選取要啟動的工作流程。

## 跳转步骤 {#goto-step}

此 **移至步驟** 可讓您指定要在工作流程模型中執行的下一個步驟。 您可以指定規則定義、外部指令集或ECMA指令集作為路由運算式，以評估工作流程模型的下一個步驟。

* 如果您指定的條件為true，則 **移至步驟** 完成，工作流程引擎就會執行指定的步驟。
* 如果您指定的條件不成立，則 **移至步驟** 完成，而一般製程邏輯會決定下一個要執行的步驟。

此 **移至步驟** 可讓您在工作流程模型中匯入進階路由結構。 例如，若要實作回圈， **移至步驟** 可定義以執行工作流程中的先前步驟，而路由運算式會評估回圈條件。

### 移至步驟 — 設定 {#goto-step-configuration}

若要設定步驟，請編輯並使用下列標籤：

* [通用](#step-properties-common-tab)
* **进程**

   * **目標步驟**：在評估路由運算式的條件後，選取要執行的步驟。
   * **路由運算式**：選取規則定義、外部指令碼或決定是否執行的ECMA指令碼 **目標步驟**.

      * **規則定義：** 使用 [運算式編輯器](/help/forms/using/variable-in-aem-workflows.md#use-expression-editor) 以定義規則。
      * **外部指令碼：** 外部指令碼的路徑。
      * **ECMA指令碼**：判斷是否要執行 **移至步驟**.

#### 模擬回圈的 {#simulating-a-for-loop}

模擬「for回圈」需要您維持已發生回圈迭代次數的計數：

* 計數通常代表工作流程中執行之專案的索引。
* 此計數會評估為回圈的退出條件。

例如，若要實作在數個JCR節點上執行動作的工作流程，您可以使用回圈計數器作為節點的索引。 若要保留計數，請儲存 `integer` 工作流程例項的資料地圖中的值。 若要遞增計數並將計數與退出條件比較，請使用 **移至步驟**.

```
function check(){
   var count=0;
   var keyname="loopcount"
   try{
      if (workflowData.getMetaDataMap().containsKey(keyname)){
        log.info("goto script: found loopcount key");
        count= parseInt(workflowData.getMetaDataMap().get(keyname))+1;
      }

     workflowData.getMetaDataMap().put(keyname,count);

     }catch(err) {
         log.info(err.message);
         return false;
    }
   if (parseInt(count) <7){
       return true;
   } else {
      return false;
   }
}
```

### 使用規則定義模擬for回圈 {#simulateforloop}

您也可以使用「規則定義」作為路由運算式來模擬for回圈。 [建立 **count** 變數](/help/forms/using/variable-in-aem-workflows.md#create-a-variable) 長資料型別的URL。 使用 **運算式** 作為中的對應模式 **[設定變數](/help/sites-developing/using-variables-in-aem-workflows.md#set-a-variable)** 設定下列專案值的步驟： **count** 變數至 **count + 1** 每次執行 **設定變數** 步驟。

![模擬for回圈](assets/variable_use_case_count_new.png)

在 **移至步驟**，使用 **設定變數** 作為 **目標步驟** 和 **計數&lt; 5** 作為路由運算式。

![模擬for回圈的條件](assets/variable_use_case_count1_new.png)

此 **設定變數** 步驟重複執行，增加 **count** 變數乘以1，直到值達到5。

## OR 拆分 {#or-split}

此 **OR分割** 會在工作流程中建立分割，之後只有一個分支處於作用中狀態。 此步驟可讓您在工作流程中匯入條件式處理路徑。 您可視需要將工作流程步驟新增至每個分支。

>[!NOTE]
>
>另請參閱 [OR分割步驟](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/using-variables-in-aem-workflows.html?lang=en#use-a-variable)

![使用OR分割來分支](assets/variables_orsplit_new.png)

### OR拆分 — 設定 {#or-split-configuration}

若要設定分割：

* 編輯 **OR拆分屬性**：

   * **通用**

      * 指定分割名稱。
   * **分支(*x)***

      * **新增分支：** 在步驟中新增更多分支。
      * **選取路由運算式**：若要評估作用中分支，請選取路由運算式。 可能的值包括：規則定義、外部指令碼和ECMA指令碼。
      * **按一下以新增運算式**：新增運算式以評估作用中分支（如果您選取） **規則定義** 作為路由運算式。
      * **指令碼路徑**：包含計算作用中分支之指令碼的檔案的路徑（如果您選取） **外部指令碼** 作為路由運算式。
      * **指令碼**：在方塊中新增指令碼，以評估活動分支（如果您選取） **ECMA指令碼** 作為路由運算式。
      * **預設路由**：如果有多個分支，則遵循預設分支。 您只能指定一個分支作為預設值。

   >[!NOTE]
   >
   >    * 系統會根據路由運算式一次評估一個分支。
   >    * 系統會從上到下評估分支。
   >    * 系統會執行第一個評估為true的指令碼。
   >    * 如果沒有分支評估為true，則工作流程不會前進。


   >[!NOTE]
   >
   >另請參閱 [定義OR分割的規則](/help/sites-developing/workflows-models.md#defineruleecmascript).

* 視需要將工作流程步驟新增至分支。

## 參與者步驟與選擇器 {#participant-steps-and-choosers}

### 参与者步骤 {#participant-step}

A **參與者步驟** 可讓您指派特定動作的所有權。 工作流程僅在使用者手動確認步驟時進行。 如果您希望某人執行工作流程，請使用此工作流程。 例如，複查步驟。

雖然不直接相關，但在指派動作時必須考慮使用者授權；使用者必須擁有工作流程有效負載頁面的存取權。

#### 參與者步驟 — 設定 {#participant-step-configuration}

若要設定步驟，請編輯並使用下列標籤：

* [通用](#step-properties-common-tab)
* [用户/组](#step-properties-user-group-tab)

>[!NOTE]
>
>當發生下列情況時，一律會通知工作流程發起人：
>
>* 工作流程已完成（完成）。
>* 工作流程已中止（已終止）。
>


>[!NOTE]
>
>必須設定部分屬性以啟用電子郵件通知。 您也可以自訂電子郵件範本，或新增新語言的電子郵件範本。 若要在AEM中設定電子郵件通知，請參閱 [設定電子郵件通知](/help/sites-administering/notification.md#configuringemailnotification).

### 对话框参与者步骤 {#dialog-participant-step}

使用 **對話方塊參與者步驟** 以向被指派工作專案的使用者收集資訊。 此步驟對於收集稍後在工作流程中使用的少量資料很有用。

完成步驟後， **完成工作專案** 對話方塊包含您在對話方塊中定義的欄位。 在欄位中收集的資料會儲存在工作流程裝載的節點中。 之後，後續的工作流程步驟可以從存放庫讀取值。

若要設定步驟，您可以指定要指派工作專案的群組或使用者，以及對話方塊的路徑。

#### 對話方塊參與者步驟 — 設定 {#dialog-participant-step-configuration}

若要設定步驟，請編輯並使用下列標籤：

* [通用](#step-properties-common-tab)
* [用户/组](#step-properties-user-group-tab)
* **对话框**

   * **對話方塊路徑**：的對話方塊節點路徑 [您建立的對話方塊](#dialog-participant-step-creating-a-dialog).

#### 對話方塊參與者步驟 — 建立對話方塊 {#dialog-participant-step-creating-a-dialog}

若要建立對話方塊，您必須建立對話方塊：

* 決定產生的資料在何處 [儲存在承載中](#dialog-participant-step-storing-data-in-the-payload).
* [定義對話方塊；包括定義用來收集和儲存資料的欄位](#dialog-participant-step-dialog-definition).

#### 對話方塊參與者步驟 — 將資料儲存在承載中 {#dialog-participant-step-storing-data-in-the-payload}

您可以將Widget資料儲存在工作流程裝載或工作專案中繼資料中。 的格式 `name` widget節點的屬性會決定資料儲存的位置。

* **使用承載儲存資料**

   * 若要將Widget資料儲存為工作流程裝載的屬性，請為Widget節點的name屬性值使用下列格式：
      `./jcr:content/nodename`

   * 資料會儲存在 `nodename` 裝載節點的屬性。 如果節點不包含該屬性，則會建立屬性。
   * 與裝載一併儲存時，後續使用具有相同裝載的對話方塊會覆寫屬性的值。

* **使用工作專案儲存資料**

   * 若要將Widget資料儲存為工作專案中繼資料的屬性，請為name屬性的值使用下列格式：
      `nodename`

   * 資料會儲存在 `nodename` 工作專案的屬性 `metadata`. 如果之後將對話方塊用於相同的裝載，則會保留資料。

#### 對話方塊參與者步驟 — 對話方塊定義 {#dialog-participant-step-dialog-definition}

1. **對話方塊結構**

   對話方塊參與者步驟對話方塊類似於您為編寫元件所建立的對話方塊。 它們儲存在下列位置：

   `/apps/myapp/workflow/dialogs`

   標準、觸控式UI的對話方塊具有下列節點結構：

   ```xml
   newComponent (cq:Component)
     |- cq:dialog (nt:unstructured)
       |- content
         |- layout
           |- items
             |- column
               |- items
                 |- component0
                 |- component1
                 |- ...
   ```

   >[!NOTE]
   >
   >另請參閱 [建立和設定對話方塊](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog).

1. **對話方塊路徑屬性**

   此 **對話方塊參與者步驟** 具有 **對話方塊路徑** 屬性(連同屬性 [參與者步驟](#participant-step))。 的值 **對話方塊路徑** property是 `dialog` 對話方塊的節點。

   例如，對話方塊包含在名為的元件中 `EmailWatch` 儲存在節點中的變數：

   `/apps/myapp/workflows/dialogs`

   對於觸控式UI，下列值會用於 **對話方塊路徑** 屬性：

   `/apps/myapp/workflow/dialogs/EmailWatch/cq:dialog`

   ![wf-30](assets/wf-30.png)

1. **對話方塊定義範例**

   下列XML程式碼片段代表儲存 `String` 中的值 `watchEmail` 裝載內容的節點。 標題節點代表 [文字欄位](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/textfield/index.html) 元件：

   ```xml
   jcr:primaryType="nt:unstructured"
       jcr:title="Watcher Email Address Dialog"
       sling:resourceType="cq/gui/components/authoring/dialog">
       <content jcr:primaryType="nt:unstructured"
           sling:resourceType="granite/ui/components/foundation/container">
           <layout jcr:primaryType="nt:unstructured"
               margin="false"
               sling:resourceType="granite/ui/components/foundation/layouts/fixedcolumns"
           />
           <items jcr:primaryType="nt:unstructured">
               <column jcr:primaryType="nt:unstructured"
                   sling:resourceType="granite/ui/components/foundation/container">
                   <items jcr:primaryType="nt:unstructured">
                       <title jcr:primaryType="nt:unstructured"
                           fieldLabel="Notification Email Address"
                           name="./jcr:content/watchEmails"
                           sling:resourceType="granite/ui/components/foundation/form/textfield"
                       />
                   </items>
               </column>
           </items>
       </content>
   </cq:dialog>
   ```

   在觸控式UI中，此範例會產生如下的對話方塊：

   ![chlimage_1-70](assets/chlimage_1-70.png)

### 动态参与者步骤 {#dynamic-participant-step}

此 **動態參與者步驟** 元件類似於 **[參與者步驟](#participant-step)** 不同之處在於，參與者會在執行階段自動選取。

若要設定步驟，請選取 **參與者選擇器** 會識別指派工作專案給的參與者，以及對話方塊。

#### 動態參與者步驟 — 設定 {#dynamic-participant-step-configuration}

若要設定步驟，請編輯並使用下列標籤：

* [通用](#step-properties-common-tab)
* **参与者选择器**

   * **參與者選擇器**：的名稱 [您建立的參與者選擇器](#developingtheparticipantchooser).
   * **引數**：任何必要的引數。
   * **電子郵件**：是否應將電子郵件通知傳送給使用者。

* **对话框**

   * **對話方塊路徑**：的對話方塊節點路徑 [您建立的對話方塊(與 **對話方塊參與者步驟**)](#dialog-participant-step-creating-a-dialog).

#### 動態參與者步驟 — 開發參與者選擇器 {#dynamic-participant-step-developing-the-participant-chooser}

您可以建立參與者選擇器。 因此，您可以使用任何選取邏輯或條件。 例如，您的參與者選擇器可以選取工作專案最少的使用者（在群組內）。 您可以建立任意數量的參與者選擇器，以搭配的不同執行個體使用 **動態參與者步驟** 元件建立的工作流程模型。

建立可選取使用者以指派工作專案的OSGi服務或ECMAScript。

* **ECMAscript**

   指令碼必須包含名為getParticipant的函式，此函式會將使用者ID傳回為 `String` 值。 將自訂指令碼儲存在中，例如 `/apps/myapp/workflow/scripts` 資料夾或子資料夾。

   範例指令碼包含在標準AEM例項中：

   `/libs/workflow/scripts/initiator-participant-chooser.ecma`

   >[!CAUTION]
   >
   >請勿變更 `/libs` 路徑。
   >
   >
   >原因是因為內容屬於 `/libs` 下次升級執行個體時會被覆寫（並在套用hotfix或feature pack時可能被覆寫）。

   此指令碼會選取工作流程發起人作為參與者：

   ```
   function getParticipant() {
       return workItem.getWorkflow().getInitiator();
   }
   ```

   >[!NOTE]
   >
   >此 **工作流程發起人參與者選擇器** 元件延伸 **動態參與者步驟** 和會使用此指令碼作為步驟實作。

* **OSGi服務**

   服務必須實作 [com.day.cq.workflow.exec.ParticipantStepChooser](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/workflow/exec/ParticipantStepChooser.html) 介面。 介面會定義下列成員：

   * `SERVICE_PROPERTY_LABEL` 欄位：使用此欄位可指定參與者選擇器的名稱。 該名稱會顯示在中可用的參與者選擇器清單中 **動態參與者步驟** 屬性。

   * `getParticipant` 方法：傳回動態解析的主體ID為 `String` 值。
   >[!CAUTION]
   >
   >此 `getParticipant` 方法會傳回動態解析的主體id。 此ID可以是群組ID或使用者ID。
   >
   >
   >不過，群組ID只能用於 **參與者步驟**，則會在傳回參與者清單時。 對於 **動態參與者步驟**，會傳回空白清單且無法用於委派。

   若要讓您的實作可供 **動態參與者步驟** 元件、將您的Java™類別新增至匯出服務的OSGi套件組合，然後將套件組合部署至AEM伺服器。

   >[!NOTE]
   >
   >**隨機參與者選擇器** 是選取隨機使用者的範例服務( `com.day.cq.workflow.impl.process.RandomParticipantChooser`)。 此 **隨機參與者選擇** r步驟元件範例延伸 **動態參與者步驟** 和會使用此服務作為步驟實作。

#### 動態參與者步驟 — 參與者選擇器服務範例 {#dynamic-participant-step-example-participant-chooser-service}

以下Java™類別實作 `ParticipantStepChooser` 介面。 類別會傳回起始工作流程的參與者名稱。 程式碼使用的邏輯與範例指令碼(`initiator-participant-chooser.ecma`)使用。

此 `@Property` annotation設定 `SERVICE_PROPERTY_LABEL` 欄位至 `Workflow Initiator Participant Chooser`.

```java
package com.adobe.example;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.osgi.framework.Constants;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.ParticipantStepChooser;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.metadata.MetaDataMap;

@Component
@Service
@Properties({
        @Property(name = Constants.SERVICE_DESCRIPTION, value = "An example implementation of a dynamic participant chooser."),
        @Property(name = ParticipantStepChooser.SERVICE_PROPERTY_LABEL, value = "Workflow Initiator Participant Chooser (service)") })
public class InitiatorParticipantChooser implements ParticipantStepChooser {

 private Logger logger = LoggerFactory.getLogger(this.getClass());

 public String getParticipant(WorkItem arg0, WorkflowSession arg1,
   MetaDataMap arg2) throws WorkflowException {

  String initiator = arg0.getWorkflow().getInitiator();
  logger.info("Assigning Dynamic Participant Step work item to {}",initiator);

  return initiator;
 }
}
```

在 **動態參與者步驟** 屬性對話方塊， **參與者選擇器** 清單包含專案 `Workflow Initiator Participant Chooser (script)`，代表此服務。

啟動工作流程模型時，記錄會指出啟動工作流程的使用者ID以及工作專案的指派者。 在此範例中， `admin` 使用者已啟動工作流程。

`13.09.2015 15:48:53.037 *INFO* [10.176.129.223 [1347565733037] POST /etc/workflow/instances HTTP/1.1] com.adobe.example.InitiatorParticipantChooser Assigning Dynamic Participant Step work item to admin`

### 表单参与者步骤 {#form-participant-step}

此 **表單參與者步驟** 在工作專案開啟時顯示表單。 當使用者填寫並提交表單時，欄位資料會儲存在工作流程裝載的節點中。

若要設定此步驟，您可以指定要指派工作專案的群組或使用者，以及表單的路徑。

>[!CAUTION]
>
>本節將說明 [用於頁面製作的基礎元件的Forms區段](/help/sites-authoring/default-components-foundation.md#form).

#### 表單參與者步驟 — 設定 {#form-participant-step-configuration}

若要設定步驟，請編輯並使用下列標籤：

* [通用](#step-properties-common-tab)
* [用户/组](#step-properties-user-group-tab)
* **表单**

   * **表單路徑**：的路徑 [您建立的表單](#form-participant-step-creating-the-form).

#### 表單參與者步驟 — 建立表單 {#form-participant-step-creating-the-form}

建立表單以用於 **表單參與者步驟** 如往常一樣。 不過，「表單參與者步驟」的表單必須具備下列設定：

* 此 **表單的開頭** 元件必須具有 **動作型別** 屬性設定為 `Edit Workflow Controlled Resource(s)`.
* 此 **表單的開頭** 元件必須有一個值 `Form Identifier` 屬性。
* 表單元件必須具備 **元素名稱** 屬性會設定為儲存欄位資料的節點的路徑。 路徑必須在工作流程裝載內容中找出節點。 值會使用以下格式：

   `./jcr:content/path_to_node`

* 表單必須包含 **工作流程提交按鈕** 元件。 您未設定元件的任何屬性。

工作流程的要求會決定您應將欄位資料儲存的位置。 例如，欄位資料可用於設定頁面內容的屬性。 下列值 **元素名稱** 屬性會將欄位資料儲存為 `redirectTarget` 的屬性 `jcr:content` 節點：

`./jcr:content/redirectTarget`

在以下範例中，欄位資料會當作 **文字** 承載頁面上的元件：

`./jcr:content/par/text_3/text`

第一個範例可用於 `cq:Page` 元件呈現。 第二個範例只能用於裝載頁面包含 **文字** ID為的元件 `text_3`.

表單可位於存放庫中的任何位置，但工作流程使用者必須獲得讀取表單的授權。

### 随机参与者选择器 {#random-participant-chooser}

此 **隨機參與者選擇器** 步驟是一個參與者選擇器，可將產生的工作專案指派給從清單中隨機選取的使用者。

![wf-31](assets/wf-31.png)

#### 隨機參與者選擇器 — 設定 {#random-participant-chooser-configuration}

若要設定步驟，請編輯並使用下列標籤：

* [通用](#step-properties-common-tab)
* **参数**

   * **參與者**：指定可供選取的使用者清單。 若要新增使用者至清單，請按一下 **新增專案** 和輸入使用者節點的主目錄路徑或使用者ID。 使用者的順序不會影響被指派工作專案的可能性。

### 工作流发起者参与人选择器 {#workflow-initiator-participant-chooser}

此 **工作流程發起人參與者選擇器** 步驟是一個參與者選擇器，可將產生的工作專案指派給啟動工作流程的使用者。 除了以下專案外，沒有可設定的屬性 **通用** 屬性。

#### 工作流程發起人參與者選擇器 — 設定 {#workflow-initiator-participant-chooser-configuration}

若要設定此步驟，請使用下列標籤進行編輯：

* [通用](#step-properties-common-tab)

## 流程步骤 {#process-step}

A **程式步驟** 執行ECMAScript或呼叫OSGi服務以執行自動處理。

![wf-32](assets/wf-32.png)

### 程式步驟 — 設定 {#process-step-configuration}

若要設定步驟，請編輯並使用下列標籤：

* [通用](#step-properties-common-tab)
* **进程**

   * **程式**：要執行的程式實作。 使用下拉式功能表選取ECMAScript或OSGi服務。 有关信息:

      * 標準ECMAScripts和OSGi服務，請參閱 [內建程式步驟流程](/help/sites-developing/workflows-process-ref.md).
      * 建立「處理」步驟的ECMAScript，請參閱 [使用ECMAScript實作流程步驟](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript).
      * 為程式步驟建立OSGi服務，請參閱 [使用Java™類別實作程式步驟](/help/sites-developing/workflows-customizing-extending.md#implementing-a-process-step-with-a-java-class).
   * **處理常式前進**：選取此選項可自動將工作流程推進至執行後的下一個步驟。 如果未選取，實作指令碼必須處理工作流程推進。
   * **引數**：要傳遞給處理序的引數。


## 设置变量 {#set-variable}

「設定變數」步驟可讓您設定變數的值，並定義設定值的順序。 變數的設定順序，是變數對應在「設定變數」步驟中列出的順序。

![新增對應以設定變數](assets/set_variable_addmappingnew.png)

### 設定變數 — 設定 {#setvariable}

若要設定步驟，請編輯並使用下列標籤：

* [通用](/help/sites-developing/workflows-step-ref.md#step-properties-common-tab)
* **映射**

   * **選取變數：** 使用此選項可選取變數以設定其值。
   * **選取對應模式：**  若要設定變數的值，請選取對應模式。 根據變數的資料型別，您可以使用下列選項來設定變數的值：

      * **常值：** 知道要指定的確切值時使用選項。
      * **運算式：** 根據運算式計算要使用的值時，請使用選項。 運算式會在提供的運算式編輯器中建立。
      * **JSON點標籤法：** 使用選項從JSON或FDM型別變數擷取值。
      * **XPATH：** 使用選項從XML型別變數擷取值。
      * **相對於裝載：** 當要儲存至變數的值可在相對於承載的路徑取得時，請使用選項。
      * **絕對路徑：** 當要儲存至變數的值可在絕對路徑取得時，請使用選項。
   * **指定值：** 若要對應至變數，請指定值。 您在此欄位中指定的值取決於對應模式。
   * **新增對應：** 使用此選項可新增更多對應，以設定變數的值。
