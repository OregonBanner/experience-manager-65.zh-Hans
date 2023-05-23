---
title: 扩展工作流功能
seo-title: Extending Workflow Functionality
description: 扩展工作流功能
seo-description: null
uuid: 9f4ea2a8-8b21-4e7c-ac73-dd37d9ada111
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: f23408c3-6b37-4047-9cce-0cab97bb6c5c
exl-id: 9e205912-50a6-414a-b8d4-a0865269d0e0
source-git-commit: 13f15bee38b6b4af4cd59376849810a788f0c467
workflow-type: tm+mt
source-wordcount: '3583'
ht-degree: 2%

---

# 扩展工作流功能{#extending-workflow-functionality}

本主題說明如何為工作流程開發自訂步驟元件，以及如何以程式設計方式與工作流程互動。

建立自訂工作流程步驟涉及下列活動：

* 開發工作流程步驟元件。
* 以OSGi服務或ECMA指令碼形式實作步驟功能。

您也可以 [從您的程式和指令碼與您的工作流程互動](/help/sites-developing/workflows-program-interaction.md).

## 工作流程步驟元件 — 基本知識 {#workflow-step-components-the-basics}

工作流程步驟元件會定義建立工作流程模型時步驟的外觀和行為：

* 工作流程Sidekick中的類別和步驟名稱。
* 工作流程模型中的步驟外觀。
* 用於設定元件屬性的「編輯」對話方塊。
* 在執行階段執行的服務或指令碼。

與 [所有元件](/help/sites-developing/components.md)，工作流程步驟元件繼承自為指定的元件 `sling:resourceSuperType` 屬性。 下圖顯示下列專案的階層： `cq:component` 構成所有工作流程步驟元件基礎的節點。 此圖表也包含 **程式步驟**， **參與者步驟**、和 **動態參與者步驟** 元件，因為這些是開發自訂步驟元件最常見（和基本）的起點。

![aem_wf_componentinherit](assets/aem_wf_componentinherit.png)

>[!CAUTION]
>
>您 ***必須*** 不變更中的任何專案 `/libs` 路徑。
>
>這是因為 `/libs` 下次升級執行個體時會被覆寫（而您在套用hotfix或feature pack時很可能會被覆寫）。
>
>設定和其他變更的建議方法是：
>
>1. 重新建立所需專案（即該專案存在於中） `/libs` 在 `/apps`
>2. 進行任何變更 `/apps`


此 `/libs/cq/workflow/components/model/step` component是最接近的共同祖先 **程式步驟**， **參與者步驟**、和 **動態參與者步驟**，會繼承下列專案：

* `step.jsp`

   此 `step.jsp` 指令碼在新增到模型時呈現步驟元件的標題。

   ![wf-22-1](assets/wf-22-1.png)

* [cq：dialog](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog)

   對話方塊，內含下列索引標籤：

   * **通用**：用於編輯標題和說明。
   * **進階**：用於編輯電子郵件通知屬性。

   ![wf-44](assets/wf-44.png) ![wf-45](assets/wf-45.png)

   >[!NOTE]
   >
   >當步驟元件的「編輯」對話方塊的索引標籤不符合此預設外觀時，步驟元件已定義指令碼、節點屬性或對話方塊索引標籤，以取代這些繼承的索引標籤。

### ECMA指令碼 {#ecma-scripts}

ECMA指令碼中可用的物件如下（視步驟型別而定）：

* [工作專案](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkItem.html) 工作專案
* [工作流程工作階段](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/WorkflowSession.html) workflowsession
* [工作流程資料](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkflowData.html) workflowdata
* `args`：具有處理序引數的陣列。

* `sling`：存取其他osgi服務。
* `jcrSession`

### 中繼資料地圖 {#metadatamaps}

您可以使用工作流程中繼資料來儲存工作流程期限期間所需的資訊。 工作流程步驟的常見要求是保留資料以供日後在工作流程中使用，或擷取保留的資料。

有三種型別的MetaDataMap物件 — for `Workflow`， `WorkflowData` 和 `WorkItem` 物件。 這些檔案的目的都相同：儲存中繼資料。

工作專案有自己的MetaDataMap，只能在該工作專案（例如步驟）執行時使用。

兩者 `Workflow` 和 `WorkflowData` 中繼資料地圖會在整個工作流程中共用。 對於這些情況，建議僅使用 `WorkflowData` 中繼資料對應。

## 建立自訂工作流程步驟元件 {#creating-custom-workflow-step-components}

工作流程步驟元件可以是 [以與任何其他元件相同的方式建立](/help/sites-developing/components.md).

若要繼承自其中一個（現有）基本步驟元件，請將下列屬性新增至 `cq:Component` 節點：

* 名称: `sling:resourceSuperType`
* 类型: `String`
* 值：解析為基本元件的下列路徑之一：

   * `cq/workflow/components/model/process`
   * `cq/workflow/components/model/participant`
   * `cq/workflow/components/model/dynamic_participant`

### 指定步驟例項的預設標題和說明 {#specifying-the-default-title-and-description-for-step-instances}

使用以下程式來指定 **標題** 和 **說明** 欄位 **通用** 標籤。

>[!NOTE]
>
>當滿足以下兩個要求時，欄位值會出現在步驟例項上：
>
>* 步驟的「編輯」對話方塊會將標題和說明儲存在下列位置： >
>* `./jcr:title`
>* `./jcr:description` 个位置
>
>  當「編輯」對話方塊使用「常用」索引標籤時， `/libs/cq/flow/components/step/step` 元件實作。
>
>* 步驟元件或元件的父項不會覆寫 `step.jsp` 指令碼 `/libs/cq/flow/components/step/step` 元件實作。


1. 在 `cq:Component` 節點，新增下列節點：

   * 名称: `cq:editConfig`
   * 类型: `cq:EditConfig`

   >[!NOTE]
   >
   >如需cq：editConfig節點的詳細資訊，請參閱 [設定元件的編輯行為](/help/sites-developing/developing-components.md#configuring-the-edit-behavior).

1. 在 `cq:EditConfig` 節點，新增下列節點：

   * 名称: `cq:formParameters`
   * 类型: `nt:unstructured`

1. 新增 `String` 下列名稱的屬性至 `cq:formParameters` 節點：

   * `jcr:title`：值會填滿 **標題** 的欄位 **通用** 標籤。
   * `jcr:description`：值會填滿 **說明** 的欄位 **通用** 標籤。

### 在工作流程中繼資料中儲存屬性值 {#saving-property-values-in-workflow-metadata}

>[!NOTE]
>
>另請參閱 [儲存和存取資料](#persisting-and-accessing-data). 特別是，如需有關在執行階段存取屬性值的資訊，請參閱 [在執行階段存取對話方塊屬性值](#accessing-dialog-property-values-at-runtime).

的名稱屬性 `cq:Widget` items會指定儲存介面工具集值的JCR節點。 在工作流程步驟元件的對話方塊中，當Widget將值儲存在 `./metaData` 節點，則會將值新增至工作流程 `MetaDataMap`.

例如，對話方塊中的文字欄位是 `cq:Widget` 具有下列屬性的節點：

| 名称 | 类型 | 价值 |
|---|---|---|
| `xtype` | `String` | `textarea` |
| `name` | `String` | `./metaData/subject` |
| `fieldLabel` | `String` | `Email Subject` |

此文字欄位中指定的值會新增至工作流程例項的 ` [MetaDataMap](#metadatamaps)` 物件，且已與 `subject` 金鑰。

>[!NOTE]
>
>當索引鍵為 `PROCESS_ARGS`，此值可在ECMA指令碼實作中透過以下方式取得： `args` 變數。 在此案例中，name屬性的值為 `./metaData/PROCESS_ARGS.`

### 覆寫步驟實作 {#overriding-the-step-implementation}

每個基本步驟元件都可讓工作流程模型開發人員在設計時設定以下主要功能：

* 程式步驟：要在執行階段執行的服務或ECMA指令碼。
* 參與者步驟：指派已產生工作專案之使用者的識別碼。
* 動態參與者步驟：選擇已指派工作專案之使用者ID的服務或ECMA指令碼。

若要將焦點放在特定工作流程案例中使用的元件，請在設計中設定關鍵功能，並移除模型開發人員變更該元件的功能。

1. 在cq：component節點底下，新增以下節點：

   * 名称: `cq:editConfig`
   * 类型: `cq:EditConfig`

   如需cq：editConfig節點的詳細資訊，請參閱 [設定元件的編輯行為](/help/sites-developing/developing-components.md#configuring-the-edit-behavior).

1. 在cq：EditConfig節點底下，新增以下節點：

   * 名称: `cq:formParameters`
   * 类型: `nt:unstructured`

1. 新增 `String` 屬性至 `cq:formParameters` 節點。 元件超級型別會決定屬性的名稱：

   * 流程步骤: `PROCESS`
   * 参与者步骤: `PARTICIPANT`
   * 动态参与者步骤: `DYNAMIC_PARTICIPANT`

1. 指定屬性的值：

   * `PROCESS`：實作步驟行為之ECMA指令碼或服務PID的路徑。
   * `PARTICIPANT`：指派工作專案的使用者ID。
   * `DYNAMIC_PARTICIPANT`：ECMA指令碼的路徑，或選擇使用者指派工作專案之服務的PID。

1. 若要移除模型開發人員變更屬性值的功能，請覆寫元件超級型別的對話方塊。

### 新增Forms和對話方塊至參與者步驟 {#adding-forms-and-dialogs-to-participant-steps}

自訂您的參與者步驟元件，以提供 [表單參與者步驟](/help/sites-developing/workflows-step-ref.md#form-participant-step) 和 [對話方塊參與者步驟](/help/sites-developing/workflows-step-ref.md#dialog-participant-step) 元件：

* 當使用者開啟產生的工作專案時，向他們展示表單。
* 當使用者完成產生的工作專案時，向他們顯示自訂對話方塊。

在新元件上執行下列程式(請參閱 [建立自訂工作流程步驟元件](#creating-custom-workflow-step-components))：

1. 在 `cq:Component` 節點，新增下列節點：

   * 名称: `cq:editConfig`
   * 类型: `cq:EditConfig`

   如需cq：editConfig節點的詳細資訊，請參閱 [設定元件的編輯行為](/help/sites-developing/components-basics.md#edit-behavior).

1. 在cq：EditConfig節點底下，新增以下節點：

   * 名称: `cq:formParameters`
   * 类型: `nt:unstructured`

1. 若要在使用者開啟工作專案時顯示表單，請將下列屬性新增至 `cq:formParameters` 節點：

   * 名称: `FORM_PATH`
   * 类型: `String`
   * 值：解析為表單的路徑

1. 若要在使用者完成工作專案時顯示自訂對話方塊，請將以下屬性新增至 `cq:formParameters` 節點

   * 名称: `DIALOG_PATH`
   * 类型: `String`
   * 值：解析至對話方塊的路徑

### 設定工作流程步驟執行階段行為 {#configuring-the-workflow-step-runtime-behavior}

在 `cq:Component` 節點，新增 `cq:EditConfig` 節點。 在下方新增 `nt:unstructured` 節點(必須命名為 `cq:formParameters`)並新增下列屬性至該節點：

* 名称: `PROCESS_AUTO_ADVANCE`

   * 类型: `Boolean`
   * 价值:

      * 當設定為 `true` 工作流程將執行該步驟並繼續 — 這是預設值，也建議這麼做
      * 時間 `false`，工作流程將會執行並停止；這需要額外的處理，因此 `true` 建議使用

* 名称: `DO_NOTIFY`

   * 类型: `Boolean`
   * 值：指出是否應該針對使用者參與步驟傳送電子郵件通知（並假設郵件伺服器已正確設定）

## 儲存和存取資料 {#persisting-and-accessing-data}

### 保留資料以供後續工作流程步驟使用 {#persisting-data-for-subsequent-workflow-steps}

您可以使用工作流程中繼資料來儲存工作流程存留期期間以及步驟之間所需的資訊。 工作流程步驟的常見要求是保留資料以供未來使用，或從先前步驟中擷取保留的資料。

工作流程中繼資料儲存在 [`MetaDataMap`](#metadatamaps) 物件。 Java API提供 [`Workflow.getWorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/Workflow.html) 傳回 [`WorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkflowData.html) 提供適當內容的物件 `MetaDataMap` 物件。 此 `WorkflowData` `MetaDataMap` 物件可用於步驟元件的OSGi服務或ECMA指令碼。

#### Java {#java}

的執行方法 `WorkflowProcess` 實作會傳遞給 `WorkItem` 物件。 使用此物件來取得 `WorkflowData` 物件。 下列範例會將專案新增至工作流程 `MetaDataMap` 物件，然後記錄每個專案。 （「我的金鑰」、「我的步驟值」）專案可用於工作流程中的後續步驟。

```java
public void execute(WorkItem item, WorkflowSession session, MetaDataMap args) throws WorkflowException {

    MetaDataMap wfd = item.getWorkflow().getWorkflowData().getMetaDataMap();

    wfd.put("mykey", "My Step Value");

    Set<String> keyset = wfd.keySet();
    Iterator<String> i = keyset.iterator();
    while (i.hasNext()){
     Object key = i.next();
     log.info("The workflow medata includes key {} and value {}",key.toString(),wfd.get(key).toString());
    }
}
```

#### ECMA 脚本 {#ecma-script}

此 `graniteWorkItem` 變數是目前的ECMA指令碼表示法 `WorkItem` Java物件。 因此，您可以使用 `graniteWorkItem` 變數來取得工作流程中繼資料。 以下ECMA指令碼可用來實作 **程式步驟** 將專案新增至工作流程的方式 `MetaDataMap` 物件，然後記錄每個專案。 這些專案隨後可用於工作流程中的後續步驟。

>[!NOTE]
>
>此 `metaData` 步驟指令碼可立即使用的變數是步驟的中繼資料。 步驟中繼資料與工作流程中繼資料不同。

```
var currentDateInMillis = new Date().getTime();

graniteWorkItem.getWorkflowData().getMetaDataMap().put("hardcodedKey","theKey");

graniteWorkItem.getWorkflowData().getMetaDataMap().put("currentDateInMillisKey",currentDateInMillis);

var iterator = graniteWorkItem.getWorkflowData().getMetaDataMap().keySet().iterator();
while (iterator.hasNext()){
    var key = iterator.next();
    log.info("Workflow metadata key, value = " + key.toString() + ", " + graniteWorkItem.getWorkflowData().getMetaDataMap().get(key));
}
```

### 在執行階段存取對話方塊屬性值 {#accessing-dialog-property-values-at-runtime}

此 `MetaDataMap` 工作流程例項的物件可用於在工作流程的整個生命週期中儲存和擷取資料。 對於工作流程步驟元件實作， `MetaDataMap` 尤其適合在執行階段擷取元件屬性值。

>[!NOTE]
>
>如需有關設定元件對話方塊以儲存屬性作為工作流程中繼資料的資訊，請參閱 [在工作流程中繼資料中儲存屬性值](#saving-property-values-in-workflow-metadata).

工作流程 `MetaDataMap` 適用於Java和ECMA指令碼流程實施：

* 在WorkflowProcess介面的Java實作中， `args` 引數為 `MetaDataMap` 工作流程的物件。

* 在ECMA指令碼實作中，值可使用以下變數來取得： `args` 和 `metadata` 變數。

### 範例：擷取流程步驟元件的引數 {#example-retrieving-the-arguments-of-the-process-step-component}

的「編輯」對話方塊 **程式步驟** 元件包括 **引數** 屬性。 的值 **引數** 屬性會儲存在工作流程中繼資料中，且會與 `PROCESS_ARGS` 金鑰。

在下圖中， **引數** 屬性為 `argument1, argument2`：

![wf-24](assets/wf-24.png)

#### Java {#java-1}

以下Java程式碼為 `execute` 方法 `WorkflowProcess` 實作。 方法會將值記錄在 `args` `MetaDataMap` 與 `PROCESS_ARGS` 金鑰。

```java
public void execute(WorkItem item, WorkflowSession session, MetaDataMap args) throws WorkflowException {
     if (args.containsKey("PROCESS_ARGS")){
      log.info("workflow metadata for key PROCESS_ARGS and value {}",args.get("PROCESS_ARGS","string").toString());
     }
    }
```

當使用此Java實作的程式步驟執行時，記錄會包含以下專案：

```xml
16.02.2018 12:07:39.566 *INFO* [JobHandler: /var/workflow/instances/server0/2018-02-16/model_855140139900189:/content/we-retail/de] com.adobe.example.workflow.impl.process.LogArguments workflow metadata for key PROCESS_ARGS and value argument1, argument2
```

#### ECMA 脚本 {#ecma-script-1}

下列ECMA指令碼會當作 **程式步驟**. 它會記錄引數數目和引數值：

```
var iterator = graniteWorkItem.getWorkflowData().getMetaDataMap().keySet().iterator();
while (iterator.hasNext()){
    var key = iterator.next();
    log.info("Workflow metadata key, value = " + key.toString() + ", " + graniteWorkItem.getWorkflowData().getMetaDataMap().get(key));
}
log.info("hardcodedKey "+ graniteWorkItem.getWorkflowData().getMetaDataMap().get("hardcodedKey"));
log.info("currentDateInMillisKey "+ graniteWorkItem.getWorkflowData().getMetaDataMap().get("currentDateInMillisKey"));
```

>[!NOTE]
>
>本節說明如何使用程式步驟的引數。 此資訊也會套用至動態參與者選擇器。

>[!NOTE]
>如需在工作流程中繼資料中儲存元件屬性的另一個範例，請參閱範例：建立記錄器工作流程步驟。 此範例包含將中繼資料值與PROCESS_ARGS以外的索引鍵建立關聯的對話方塊。

### 指令碼和程式引數 {#scripts-and-process-arguments}

在的指令碼內 **程式步驟** 元件，引數可透過 `args` 物件。

建立自訂步驟元件時，物件 `metaData` 可在指令碼中使用。 此物件僅限於單一字串引數。

## 開發流程步驟實作 {#developing-process-step-implementations}

在工作流程處理期間啟動處理步驟時，步驟會傳送請求至OSGi服務或執行ECMA指令碼。 開發執行工作流程所需動作的服務或ECMA指令碼。

>[!NOTE]
>
>如需將「程式步驟」元件與服務或指令碼相關聯的資訊，請參閱 [程式步驟](/help/sites-developing/workflows-step-ref.md#process-step) 或 [覆寫步驟實作](#overriding-the-step-implementation).

### 使用Java類別實作程式步驟 {#implementing-a-process-step-with-a-java-class}

若要將程式步驟定義為OSGI服務元件（Java套裝）：

1. 建立該套件組合併將其部署至OSGI容器。 請參閱有關使用建立套件組合的檔案 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) 或 [Eclipse](/help/sites-developing/howto-projects-eclipse.md).

   >[!NOTE]
   >
   >OSGI元件需要實作 `WorkflowProcess` 介面及其 `execute()` 方法。 請參閱下列範常式式碼。

   >[!NOTE]
   >
   >套件名稱需要新增至 `<*Private-Package*>` 部分 `maven-bundle-plugin` 設定。

1. 新增SCR屬性 `process.label`  並視需要設定值。 這將是在使用泛型時列出您的流程步驟的名稱 **程式步驟** 元件。 請參閱下列範例。
1. 在 **模型** 編輯器中，使用通用將流程步驟新增至工作流程 **程式步驟** 元件。
1. 在編輯對話方塊中(屬於 **程式步驟**)，前往 **程式** 標籤並選取您的流程實作。
1. 如果您在程式碼中使用引數，請設定 **程式引數**. 例如： false。
1. 儲存步驟和工作流程模型（模型編輯器的左上角）的變更。

Java方法（分別是實作可執行Java方法的類別）會註冊為OSGI服務，讓您在執行階段隨時新增方法。

下列OSGI元件新增屬性 `approved` 至頁面內容節點（當裝載為頁面時）：

```java
package com.adobe.example.workflow.impl.process;

import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.exec.WorkflowData;
import com.adobe.granite.workflow.exec.WorkflowProcess;
import com.adobe.granite.workflow.metadata.MetaDataMap;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;

import org.osgi.framework.Constants;

import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

/**
 * Sample workflow process that sets an <code>approve</code> property to the payload based on the process argument value.
 */
@Component
@Service
public class MyProcess implements WorkflowProcess {

 @Property(value = "An example workflow process implementation.")
 static final String DESCRIPTION = Constants.SERVICE_DESCRIPTION;
 @Property(value = "Adobe")
 static final String VENDOR = Constants.SERVICE_VENDOR;
 @Property(value = "My Sample Workflow Process")
 static final String LABEL="process.label";

 private static final String TYPE_JCR_PATH = "JCR_PATH";

 public void execute(WorkItem item, WorkflowSession session, MetaDataMap args) throws WorkflowException {
  WorkflowData workflowData = item.getWorkflowData();
  if (workflowData.getPayloadType().equals(TYPE_JCR_PATH)) {
   String path = workflowData.getPayload().toString() + "/jcr:content";
   try {
    Session jcrSession = session.adaptTo(Session.class);
    Node node = (Node) jcrSession.getItem(path);
    if (node != null) {
     node.setProperty("approved", readArgument(args));
     jcrSession.save();
    }
   } catch (RepositoryException e) {
    throw new WorkflowException(e.getMessage(), e);
   }
  }
 }

 private boolean readArgument(MetaDataMap args) {
  String argument = args.get("PROCESS_ARGS", "false");
  return argument.equalsIgnoreCase("true");
 }
}
```

>[!NOTE]
>
>如果流程連續失敗三次，則會將專案置於工作流程管理員的「收件匣」中。

### 使用ECMAScript {#using-ecmascript}

ECMA指令碼可讓指令碼開發人員實作程式步驟。 指令碼位於JCR存放庫中，並從那裡執行。

下表列出可立即用於處理指令碼的變數，提供工作流程Java API物件的存取權。

| Java類別 | 指令碼變數名稱 | 描述 |
|---|---|---|
| `com.adobe.granite.workflow.exec.WorkItem` | `graniteWorkItem` | 目前的步驟例項。 |
| `com.adobe.granite.workflow.WorkflowSession` | `graniteWorkflowSession` | 目前步驟例項的工作流程工作階段。 |
| `String[]` （包含程式引數） | `args` | 步驟引數。 |
| `com.adobe.granite.workflow.metadata.MetaDataMap` | `metaData` | 目前步驟例項的中繼資料。 |
| `org.apache.sling.scripting.core.impl.InternalScriptHelper` | `sling` | 提供對Sling執行階段環境的存取權。 |

以下範例指令碼示範如何存取代表工作流程裝載的JCR節點。 此 `graniteWorkflowSession` 變數會調整為JCR工作階段變數，用於從裝載路徑取得節點。

```
var workflowData = graniteWorkItem.getWorkflowData();
if (workflowData.getPayloadType() == "JCR_PATH") {
    var path = workflowData.getPayload().toString();
    var jcrsession = graniteWorkflowSession.adaptTo(Packages.javax.jcr.Session);
    var node = jcrsession.getNode(path);
    if (node.hasProperty("approved")){
     node.setProperty("approved", args[0] == "true" ? true : false);
     node.save();
 }
}
```

以下指令碼會檢查裝載是否為影像( `.png` 檔案)，從中建立黑白影像，並將其儲存為同層級節點。

```
var workflowData = graniteWorkItem.getWorkflowData();
if (workflowData.getPayloadType() == "JCR_PATH") {
    var path = workflowData.getPayload().toString();
    var jcrsession = graniteWorkflowSession.adaptTo(Packages.javax.jcr.Session);
    var node = jcrsession.getRootNode().getNode(path.substring(1));
     if (node.isNodeType("nt:file") && node.getProperty("jcr:content/jcr:mimeType").getString().indexOf("image/") == 0) {
        var is = node.getProperty("jcr:content/jcr:data").getStream();
        var layer = new Packages.com.day.image.Layer(is);
        layer.grayscale();
                var parent = node.getParent();
                var gn = parent.addNode("grey" + node.getName(), "nt:file");
        var content = gn.addNode("jcr:content", "nt:resource");
                content.setProperty("jcr:mimeType","image/png");
                var cal = Packages.java.util.Calendar.getInstance();
                content.setProperty("jcr:lastModified",cal);
                var f = Packages.java.io.File.createTempFile("test",".png");
        var tout = new Packages.java.io.FileOutputStream(f);
        layer.write("image/png", 1.0, tout);
        var fis = new Packages.java.io.FileInputStream(f);
                content.setProperty("jcr:data", fis);
                parent.save();
        tout.close();
        fis.close();
        is.close();
        f.deleteOnExit();
    }
}
```

若要使用指令碼：

1. 建立指令碼(例如使用CRXDE Lite)並將其儲存在下面的存放庫中 `//apps/workflow/scripts/`
1. 若要指定可識別中指令碼的標題 **程式步驟** 編輯對話方塊中，新增下列屬性至 `jcr:content` 指令碼的節點：

   | 名称 | 类型 | 价值 |
   |---|---|---|
   | `jcr:mixinTypes` | `Name[]` | `mix:title` |
   | `jcr:title` | `String` | 顯示在「編輯」對話方塊中的名稱。 |

1. 編輯 **程式步驟** 執行個體並指定要使用的指令碼。

## 開發參與者選擇器 {#developing-participant-choosers}

您可以開發參與者選擇器 **動態參與者步驟** 元件。

當 **動態參與者步驟** 元件在工作流程期間啟動，步驟需要確定可將產生的工作專案指派給哪個參與者。 若要執行此動作，請執行下列步驟之一：

* 傳送要求至OSGi服務
* 執行ECMA指令碼以選取參與者

您可以開發服務或ECMA指令碼，根據工作流程的要求來選取參與者。

>[!NOTE]
>
>如需建立關聯的相關資訊， **動態參與者步驟** 具有服務或指令碼的元件，請參閱 [動態參與者步驟](/help/sites-developing/workflows-step-ref.md#dynamic-participant-step) 或 [覆寫步驟實作](#persisting-and-accessing-data).

### 使用Java類別開發參與者選擇器 {#developing-a-participant-chooser-using-a-java-class}

若要將參與者步驟定義為OSGI服務元件（Java類別）：

1. OSGI元件需要實作 `ParticipantStepChooser` 介面及其 `getParticipant()` 方法。 請參閱下列範常式式碼。

   建立該套件組合併將其部署至OSGI容器。

1. 新增SCR屬性 `chooser.label` 並視需要設定值。 這會是您的參與者選擇器所列出的名稱，使用 **動態參與者步驟** 元件。 請參閱範例：

   ```java
   package com.adobe.example.workflow.impl.process;
   
   import com.adobe.granite.workflow.WorkflowException;
   import com.adobe.granite.workflow.WorkflowSession;
   import com.adobe.granite.workflow.exec.ParticipantStepChooser;
   import com.adobe.granite.workflow.exec.WorkItem;
   import com.adobe.granite.workflow.exec.WorkflowData;
   import com.adobe.granite.workflow.metadata.MetaDataMap;
   
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Property;
   import org.apache.felix.scr.annotations.Service;
   
   import org.osgi.framework.Constants;
   
   /**
    * Sample dynamic participant step that determines the participant based on a path given as argument.
    */
   @Component
   @Service
   
   public class MyDynamicParticipant implements ParticipantStepChooser {
   
    @Property(value = "An example implementation of a dynamic participant chooser.")
    static final String DESCRIPTION = Constants.SERVICE_DESCRIPTION;
       @Property(value = "Adobe")
       static final String VENDOR = Constants.SERVICE_VENDOR;
       @Property(value = "Dynamic Participant Chooser Process")
       static final String LABEL=ParticipantStepChooser.SERVICE_PROPERTY_LABEL;
   
       private static final String TYPE_JCR_PATH = "JCR_PATH";
   
       public String getParticipant(WorkItem workItem, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
           WorkflowData workflowData = workItem.getWorkflowData();
           if (workflowData.getPayloadType().equals(TYPE_JCR_PATH)) {
               String path = workflowData.getPayload().toString();
               String pathFromArgument = args.get("PROCESS_ARGS", String.class);
               if (pathFromArgument != null && path.startsWith(pathFromArgument)) {
                   return "admin";
               }
           }
           return "administrators";
       }
   }
   ```

1. 在 **模型** 編輯者，使用一般將動態參與者步驟新增至工作流程 **動態參與者步驟** 元件。
1. 在編輯對話方塊中，選取 **參與者選擇器** 標籤並選取您的選擇器實作。
1. 如果您在程式碼中使用引數，請設定 **程式引數**. 在此範例中： `/content/we-retail/de`.
1. 儲存步驟和工作流程模型的變更。

### 使用ECMA指令碼開發參與者選擇器 {#developing-a-participant-chooser-using-an-ecma-script}

您可以建立ECMA指令碼，以選取指派工作專案的使用者， **參與者步驟** 會產生。 指令碼必須包含名為的函式 `getParticipant` 不需要引數，並傳回 `String` 包含使用者或群組的ID。

指令碼位於JCR存放庫中，並從此處執行。

下表列出可讓您立即存取指令碼中工作流程Java物件的變數。

| Java類別 | 指令碼變數名稱 |
|---|---|
| `com.adobe.granite.workflow.exec.WorkItem` | `graniteWorkItem` |
| `com.adobe.granite.workflow.WorkflowSession` | `graniteWorkflowSession` |
| `String[]` （包含程式引數） | `args` |
| `com.adobe.granite.workflow.metadata.MetaDataMap` | `metaData` |
| `org.apache.sling.scripting.core.impl.InternalScriptHelper` | `sling` |

```
function getParticipant() {
    var workflowData = graniteWorkItem.getWorkflowData();
    if (workflowData.getPayloadType() == "JCR_PATH") {
        var path = workflowData.getPayload().toString();
        if (path.indexOf("/content/we-retail/de") == 0) {
            return "admin";
        } else {
            return "administrators";
        }
    }
}
```

1. 建立指令碼(例如使用CRXDE Lite)並將其儲存在下面的存放庫中 `//apps/workflow/scripts`
1. 若要指定可識別中指令碼的標題 **程式步驟** 編輯對話方塊中，新增下列屬性至 `jcr:content` 指令碼的節點：

   | 名称 | 类型 | 价值 |
   |---|---|---|
   | `jcr:mixinTypes` | `Name[]` | `mix:title` |
   | `jcr:title` | `String` | 顯示在「編輯」對話方塊中的名稱。 |

1. 編輯 [動態參與者步驟](/help/sites-developing/workflows-step-ref.md#dynamic-participant-step) 執行個體並指定要使用的指令碼。

## 處理工作流程封裝 {#handling-workflow-packages}

[工作流程封裝](/help/sites-authoring/workflows-applying.md#specifying-workflow-details-in-the-create-workflow-wizard) 可傳遞至工作流程進行處理。 工作流程套件包含對資源（如頁面和資產）的參考。

>[!NOTE]
>
>以下工作流程處理步驟接受工作流程封裝以進行大量頁面啟用：
>
>* [`com.day.cq.wcm.workflow.process.ActivatePageProcess`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/process/ActivatePageProcess.html)
>* [`com.day.cq.wcm.workflow.process.DeactivatePageProcess`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/process/DeactivatePageProcess.html)
>


您可以開發工作流程步驟來取得封裝資源並加以處理。 下列成員 `com.day.cq.workflow.collection` 封裝提供對工作流程封裝的存取權：

* `ResourceCollection`：工作流程封裝類別。
* `ResourceCollectionUtil`：用於擷取ResourceCollection物件。
* `ResourceCollectionManager`：建立和擷取集合。 實作會部署為OSGi服務。

以下範例Java類別示範如何取得套件資源：

```java
package com.adobe.example;

import java.util.ArrayList;
import java.util.List;

import com.day.cq.workflow.WorkflowException;
import com.day.cq.workflow.WorkflowSession;
import com.day.cq.workflow.collection.ResourceCollection;
import com.day.cq.workflow.collection.ResourceCollectionManager;
import com.day.cq.workflow.collection.ResourceCollectionUtil;
import com.day.cq.workflow.exec.WorkItem;
import com.day.cq.workflow.exec.WorkflowData;
import com.day.cq.workflow.exec.WorkflowProcess;
import com.day.cq.workflow.metadata.MetaDataMap;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.apache.felix.scr.annotations.Reference;
import org.osgi.framework.Constants;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import javax.jcr.Node;
import javax.jcr.PathNotFoundException;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

@Component
@Service
public class LaunchBulkActivate implements WorkflowProcess {

 private static final Logger log = LoggerFactory.getLogger(LaunchBulkActivate.class);

 @Property(value="Bulk Activate for Launches")
  static final String PROCESS_NAME ="process.label";
 @Property(value="A sample workflow process step to support Launches bulk activation of pages")
 static final String SERVICE_DESCRIPTION = Constants.SERVICE_DESCRIPTION;

 @Reference
 private ResourceCollectionManager rcManager;
public void execute(WorkItem workItem, WorkflowSession workflowSession) throws Exception {
    Session session = workflowSession.getSession();
    WorkflowData data = workItem.getWorkflowData();
    String path = null;
    String type = data.getPayloadType();
    if (type.equals(TYPE_JCR_PATH) && data.getPayload() != null) {
        String payloadData = (String) data.getPayload();
        if (session.itemExists(payloadData)) {
            path = payloadData;
        }
    } else if (data.getPayload() != null && type.equals(TYPE_JCR_UUID)) {
        Node node = session.getNodeByUUID((String) data.getPayload());
        path = node.getPath();
    }

    // CUSTOMIZED CODE IF REQUIRED....

    if (path != null) {
        // check for resource collection
        ResourceCollection rcCollection = ResourceCollectionUtil.getResourceCollection((Node)session.getItem(path), rcManager);
        // get list of paths to replicate (no resource collection: size == 1
        // otherwise size >= 1
        List<String> paths = getPaths(path, rcCollection);
        for (String aPath: paths) {

            // CUSTOMIZED CODE....

        }
    } else {
        log.warn("Cannot process because path is null for this " + "workitem: " + workItem.toString());
    }
}

/**
 * helper
 */
private List<String> getPaths(String path, ResourceCollection rcCollection) {
    List<String> paths = new ArrayList<String>();
    if (rcCollection == null) {
        paths.add(path);
    } else {
        log.debug("ResourceCollection detected " + rcCollection.getPath());
        // this is a resource collection. the collection itself is not
        // replicated. only its members
        try {
            List<Node> members = rcCollection.list(new String[]{"cq:Page", "dam:Asset"});
            for (Node member: members) {
                String mPath = member.getPath();
                paths.add(mPath);
            }
        } catch(RepositoryException re) {
            log.error("Cannot build path list out of the resource collection " + rcCollection.getPath());
        }
    }
    return paths;
}
}
```

## 範例：建立自訂步驟 {#example-creating-a-custom-step}

開始建立您自己的自訂步驟的簡單方法是從以下位置複製現有步驟：

`/libs/cq/workflow/components/model`

### 建立基本步驟 {#creating-the-basic-step}

1. 在/apps下重新建立路徑；例如：

   `/apps/cq/workflow/components/model`

   新資料夾屬於型別 `nt:folder`：

   ```xml
   - apps
     - cq
       - workflow (nt:folder)
         - components (nt:folder)
           - model (nt:folder)
   ```

   >[!NOTE]
   >
   >此步驟不適用於傳統UI模型編輯器。

1. 然後將複製的步驟放入/apps資料夾中；例如：

   `/apps/cq/workflow/components/model/myCustomStep`

   以下是自訂步驟範例的結果：

   ![wf-34](assets/wf-34.png)

   >[!CAUTION]
   >
   >因為在標準UI中，卡片上不會顯示標題而非詳細資訊， `details.jsp` 舊版UI編輯器不需要使用。

1. 將下列屬性套用至節點：

   `/apps/cq/workflow/components/model/myCustomStep`

   **興趣屬性：**

   * `sling:resourceSuperType`

      必須繼承自現有步驟。

      在此範例中，我們繼承自下列位置的基本步驟 `cq/workflow/components/model/step`，但您可以使用其他超級型別，例如 `participant`， `process`等。

   * `jcr:title`

      是元件在步驟瀏覽器中列出時顯示的標題（工作流程模型編輯器的左側面板）。

   * `cq:icon`

      用於指定 [珊瑚圖示](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html) 用於步驟。

   * `componentGroup`

      必須為下列其中一項：

      * 协作工作流
      * DAM 工作流
      * 表单工作流
      * 项目
      * WCM 工作流
      * 工作流

   ![wf-35](assets/wf-35.png)

1. 您現在可以開啟工作流程模型以進行編輯。 在步驟瀏覽器中，您可以篩選以檢視 **我的自訂步驟**：

   ![wf-36](assets/wf-36.png)

   拖曳 **我的自訂步驟** 在模型上會顯示卡片：

   ![wf-37](assets/wf-37.png)

   若否 `cq:icon` 已針對步驟定義，然後會使用標題的前兩個字母來呈現預設圖示。 例如：

   ![wf-38](assets/wf-38.png)

#### 定義步驟設定對話方塊 {#defining-the-step-configure-dialog}

晚於 [建立基本步驟](#creating-the-basic-step)，定義步驟 **設定** 對話方塊，如下所示：

1. 在節點上設定屬性 `cq:editConfig` 如下所示：

   **興趣屬性：**

   * `cq:inherit`

      當設定為 `true`，則步驟元件將會繼承您在中指定的步驟的屬性 `sling:resourceSuperType`.

   * `cq:disableTargeting`

      視需要設定。
   ![wf-39](assets/wf-39.png)

1. 在節點上設定屬性 `cq:formsParameter` 如下所示：

   **興趣屬性：**

   * `jcr:title`

      在模型圖中的步驟卡片上設定預設標題 **標題** 的欄位 **我的自訂 — 步驟屬性** 設定對話方塊。

   * 您也可以定義自己的自訂屬性。

   ![wf-40](assets/wf-40.png)

1. 在節點上設定屬性 `cq:listeners`.

   此 `cq:listener` node及其屬性可讓您設定事件處理常式，對觸控式UI模型編輯器中的事件做出反應；例如將步驟拖曳至模型頁面或編輯步驟屬性。

   **興趣屬性：**

   * `afterMove: REFRESH_PAGE`
   * `afterdelete: CQ.workflow.flow.Step.afterDelete`
   * `afteredit: CQ.workflow.flow.Step.afterEdit`
   * `afterinsert: CQ.workflow.flow.Step.afterInsert`

   此設定對於編輯器的正常運作至關重要。 在大多數情況下，不得變更此設定。

   不過，設定 `cq:inherit` 為true (于 `cq:editConfig` 節點（請參閱上文）可讓您繼承此設定，而不需要將其明確包含在步驟定義中。 如果沒有適當繼承，則您確實需要使用以下屬性和值新增此節點。

   在此範例中，繼承已啟用，因此我們可以移除 `cq:listeners` 節點和步驟仍可正常運作。

   ![wf-41](assets/wf-41.png)

1. 您現在可以將步驟的例項新增至工作流程模型。 當您 **設定** 您將會看到對話方塊的步驟：

   ![wf-42](assets/wf-42.png) ![wf-43](assets/wf-43.png)

#### 此範例中使用的範例標籤 {#sample-markup-used-in-this-example}

自訂步驟的標籤會顯示在 `.content.xml` 元件根節點的。 範例 `.content.xml` 用於此範例：

`/apps/cq/workflow/components/model/myCustomStep/.content.xml`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:icon="bell"
    jcr:primaryType="cq:Component"
    jcr:title="My Custom Step"
    sling:resourceSuperType="cq/workflow/components/model/process"
    allowedParents="[*/parsys]"
    componentGroup="Workflow"/>
```

此 `_cq_editConfig.xml` 此範例中使用的範例：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    cq:disableTargeting="{Boolean}true"
    cq:inherit="{Boolean}true"
    jcr:primaryType="cq:EditConfig">
    <cq:formParameters
        jcr:primaryType="nt:unstructured"
        jcr:title="My Custom Step Card"
        SAMPLE_PROPERY="sample value"/>
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afterdelete="CQ.workflow.flow.Step.afterDelete"
        afteredit="CQ.workflow.flow.Step.afterEdit"
        afterinsert="CQ.workflow.flow.Step.afterInsert"
        afterMove="REFRESH_PAGE"/>
</jcr:root>
```

此 `_cq_dialog/.content.xml` 此範例中使用的範例：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    jcr:title="My Custom - Step Properties"
    sling:resourceType="cq/gui/components/authoring/dialog">
    <content
        jcr:primaryType="nt:unstructured"
        sling:resourceType="granite/ui/components/coral/foundation/tabs">
        <items jcr:primaryType="nt:unstructured">
            <common
                cq:hideOnEdit="true"
                jcr:primaryType="nt:unstructured"
                jcr:title="Common"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns"/>
            <process
                cq:hideOnEdit="true"
                jcr:primaryType="nt:unstructured"
                jcr:title="Process"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns"/>
            <mycommon
                jcr:primaryType="nt:unstructured"
                jcr:title="Common"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns">
                <items jcr:primaryType="nt:unstructured">
                    <columns
                        jcr:primaryType="nt:unstructured"
                        sling:resourceType="granite/ui/components/coral/foundation/container">
                        <items jcr:primaryType="nt:unstructured">
                            <title
                                jcr:primaryType="nt:unstructured"
                                sling:resourceType="granite/ui/components/coral/foundation/form/textfield"
                                fieldLabel="Title"
                                name="./jcr:title"/>
                            <description
                                jcr:primaryType="nt:unstructured"
                                sling:resourceType="granite/ui/components/coral/foundation/form/textarea"
                                fieldLabel="Description"
                                name="./jcr:description"/>
                        </items>
                    </columns>
                </items>
            </mycommon>
            <advanced
                jcr:primaryType="nt:unstructured"
                jcr:title="Advanced"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns">
                <items jcr:primaryType="nt:unstructured">
                    <columns
                        jcr:primaryType="nt:unstructured"
                        sling:resourceType="granite/ui/components/coral/foundation/container">
                        <items jcr:primaryType="nt:unstructured">
                            <email
                                jcr:primaryType="nt:unstructured"
                                sling:resourceType="granite/ui/components/coral/foundation/form/checkbox"
                                fieldDescription="Notify user via email."
                                fieldLabel="Email"
                                name="./metaData/PROCESS_AUTO_ADVANCE"
                                text="Notify user via email."
                                value="true"/>
                        </items>
                    </columns>
                </items>
            </advanced>
        </items>
    </content>
</jcr:root>
```

>[!NOTE]
>
>請注意對話方塊定義中的通用和流程節點。 這些是從我們用作自訂步驟超級型別的程式步驟繼承而來：
>
>`sling:resourceSuperType : cq/workflow/components/model/process`

>[!NOTE]
>
>傳統UI模型編輯器對話方塊仍可與標準觸控式UI編輯器搭配使用。
>
>雖然AEM已 [現代化工具](/help/sites-developing/modernization-tools.md) 如果您要將傳統UI步驟對話方塊升級為標準UI對話方塊。 轉換後，某些情況下仍可對對話方塊進行一些手動改進。
>
>* 如果升級後的對話方塊是空的，您可以檢視下列對話方塊： `/libs` 具有類似功能，並舉例說明如何提供解決方案的客戶。 例如：
>
>* `/libs/cq/workflow/components/model`
>* `/libs/cq/workflow/components/workflow`
>* `/libs/dam/components`
>* `/libs/wcm/workflow/components/autoassign`
>* `/libs/cq/projects`
>
>  您不得修改中的任何專案 `/libs`，只需以範例方式使用。 如果您想利用任何現有步驟，請將其複製到 `/apps` 並在那裡修改它們。
