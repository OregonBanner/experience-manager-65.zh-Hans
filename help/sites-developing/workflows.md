---
title: 开发和扩展工作流
seo-title: Developing and Extending Workflows
description: AEM提供多種工具和資源，用於建立工作流程模型、開發工作流程步驟，以及以程式設計方式與工作流程互動
seo-description: AEM provides several tools and resources for creating workflow models, developing workflow steps, and for programmatically interacting with workflows
uuid: 5a857589-3b13-4519-bda2-b1dab6005550
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 8954e3df-3afa-4d53-a7e1-255f3b8f499f
exl-id: 041b1767-8b6c-4887-a70d-abc96a116976
source-git-commit: 768576e300b655962adc3e1db20fc5ec06a5ba6c
workflow-type: tm+mt
source-wordcount: '1473'
ht-degree: 4%

---


# 开发和扩展工作流{#developing-and-extending-workflows}

AEM提供多種工具和資源，用於建立工作流程模型、開發工作流程步驟，以及以程式設計方式與工作流程互動。

工作流程可讓您自動化在AEM環境中管理資源和發佈內容的流程。 工作流程由一系列步驟組成，每個步驟都完成一個離散的任務。 您可以使用邏輯和執行階段資料來決定程式何時可以繼續，並從多個可能的步驟之一中選取下一個步驟。

例如，建立和發佈網頁的業務流程包括不同參與者的核准和簽核任務。 這些程式可以使用AEM工作流程進行模型化，並套用至特定內容。

主要內容說明如下，下列頁面則提供更多詳細資料：

* [创建工作流模型](/help/sites-developing/workflows-models.md)
* [扩展工作流功能](/help/sites-developing/workflows-customizing-extending.md)
* [以程式設計方式與工作流程互動](/help/sites-developing/workflows-program-interaction.md)
* [工作流步骤参考](/help/sites-developing/workflows-step-ref.md)
* [工作流过程参考](/help/sites-developing/workflows-process-ref.md)
* [工作流程最佳實務](/help/sites-developing/workflows-best-practices.md)

>[!NOTE]
>
>有关信息:
>
>* 參與工作流程，請參閱 [使用工作流程](/help/sites-authoring/workflows.md).
>* 管理工作流程和工作流程例項，請參閱 [管理工作流程](/help/sites-administering/workflows.md).
>* 如需端對端社群文章，請參閱 [使用Adobe Experience Manager工作流程修改數位資產。](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-workflow.html?lang=zh-Hans)
>* 請參閱 [詢問AEM專家工作流程網路研討會](https://communities.adobeconnect.com/p5s33iburd54/).
>* 資訊位置的變更，請參閱 [AEM 6.5中的存放庫重組](/help/sites-deploying/repository-restructuring.md) 和 [工作流程最佳實務 — 位置](/help/sites-developing/workflows-best-practices.md#locations).
>


## 模型 {#model}

A `WorkflowModel` 代表工作流程的定義（模型）。 它由下列專案組成 `WorkflowNodes` 和 `WorkflowTransitions`. 轉接會連線節點並定義 *流量*. 模型一律有開始節點和結束節點。

### 執行階段模型 {#runtime-model}

工作流程模型的版本已設定。 當您執行工作流程例項時，它會使用並保留工作流程的執行階段模型（在啟動工作流程時可用）。

執行階段模型是 [產生時間 **同步** 在工作流程模型編輯器中觸發](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model).

對發生的工作流程模型、產生的執行階段模型或兩者進行編輯， *晚於* 已啟動的特定執行個體未套用至該執行個體。

>[!CAUTION]
>
>執行的步驟由 [執行階段模型](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model)，產生於 **同步** 動作會在工作流程模型編輯器中觸發。
>
>如果在此時間點之後變更工作流程模型(不含 **同步** （即觸發），則執行階段執行個體不會反映這些變更。 只有更新後產生的執行階段模型才會反映變更。 例外情況是基礎ECMA指令碼，這些指令碼只會保留一次，以便進行這些變更。

### 步骤 {#step}

每個步驟都會完成一個離散任務。 有不同型別的工作流程步驟：

* 參與者（使用者/群組）：這些步驟會產生工作專案並將其指派給使用者或群組。 使用者必須完成工作專案才能推進工作流程。
* 程式(指令碼、Java™方法呼叫)：這些步驟由系統自動執行。 ECMA指令碼或Java™類別會實作該步驟。 可以開發服務以監聽特殊的工作流程事件，並根據商業邏輯執行任務。
* 容器（子工作流程）：此型別的步驟會啟動另一個工作流程模型。
* OR分割/結合：使用邏輯來決定要在工作流程中執行下一個步驟。
* AND分割/結合：允許多個步驟同時執行。

所有步驟共用以下通用屬性： `Autoadvance` 和 `Timeout` 警示（指令碼式）。

### 过渡 {#transition}

A `WorkflowTransition` 代表兩個之間的轉變 `WorkflowNodes` 的 `WorkflowModel`.

* 它會定義兩個連續步驟之間的連結。
* 您可以套用規則。

### 工作项 {#workitem}

A `WorkItem` 是通過 `Workflow` 例項 `WorkflowModel`. 它包含 `WorkflowData` 執行個體所作用的物件，以及對 `WorkflowNode` 說明基礎工作流程步驟。

* 它可用來識別任務並放入各自的收件匣中。
* 工作流程例項可以有一或多個 `WorkItems` 同時（視工作流程模型而定）。
* 此 `WorkItem` 會參考工作流程例項。
* 在存放庫中， `WorkItem` 會儲存在工作流程例項下方。

### 有效负荷 {#payload}

參考必須透過工作流程進行進階的資源。

裝載實作會參照存放庫中的資源（依路徑、UUID或URL）或依序列化Java™物件。 參考存放庫中的資源具有彈性，且Sling可發揮生產力。 例如，參照的節點可以呈現為表單。

### 生命週期 {#lifecycle}

在啟動新工作流程時建立（選擇個別工作流程模型並定義裝載），並在處理結束節點時結束。

可在工作流程例項上執行下列動作：

* 终止
* 暂停
* 继续
* 重新启动

已完成的和已終止的執行個體會封存。

### 收件箱 {#inbox}

每個使用者帳戶都有各自的工作流程收件匣，指派的工作流程位於這些工作流程收件匣中 `WorkItems` 可存取。

此 `WorkItems` 會直接指派給使用者帳戶，或指派給使用者所屬的群組。

### 工作流程型別 {#workflow-types}

「工作流程模型」控制檯中會指出各種型別的工作流程：

![wf-upgraded-03](assets/wf-upgraded-03.png)

* **默认**

   這些型別是標準AEM例項中包含的現成工作流程。

* 自訂工作流程（主控台中沒有指標）

   這些工作流程已建立為新工作流程，或從已覆蓋自訂功能的現成工作流程建立。

* **旧版**

   在舊版AEM中建立的工作流程。 這些工作流程可以在升級期間保留，或從先前版本匯出為工作流程套件，然後匯入新版本。

### 瞬态工作流 {#transient-workflows}

標準工作流程會在執行期間儲存執行階段（歷史記錄）資訊。 您也可以將工作流程模型定義為 **暫時性** 以避免此類歷史記錄持續存在。 此工作流程用於效能調整，因為它可節省用於儲存資訊的時間和資源。

暫時性工作流程可用於滿足以下條件的任何工作流程：

* 經常執行。
* 不需要工作流程歷史記錄。

在資產資訊很重要的情況下，載入許多資產時引入了暫時性工作流程，但沒有工作流程執行階段歷史記錄。

>[!NOTE]
>
>另請參閱 [建立暫時性工作流程](/help/sites-developing/workflows-models.md#creating-a-transient-workflow) 以取得更多詳細資料。

>[!CAUTION]
>
>當工作流程模型標示為暫時時，在少數情況下，執行階段資訊仍必須持續存在：
>
>* 裝載型別（例如視訊）需要外部步驟來處理；在這種情況下，需要執行階段歷史記錄來確認狀態。
>* 工作流程進入 **AND拆分**. 在這種情況下，需要執行階段歷史記錄以進行狀態確認。
>* 當暫時性工作流程進入參與者步驟時，會在執行階段將模式變更為非暫時性。 由於任務正在傳遞給個人，歷史記錄必須保留。
>


>[!CAUTION]
>
>在暫時性工作流程中，您不應使用 **移至步驟**.
>
>原因在於 **移至步驟** 建立sling工作以繼續在上執行工作流程 `goto` 點。 這會讓工作流程變成暫時性的目的，並在記錄檔中產生錯誤。
>
>使用 **OR分割** 以便在暫時性工作流程中進行選擇。

>[!NOTE]
>
>另請參閱 [資產最佳實務](/help/assets/performance-tuning-guidelines.md#transient-workflows) 以進一步瞭解暫時性工作流程如何影響資產效能。

### 多资源支持 {#multi-resource-support}

啟用 **多重資源支援** 對於您的工作流程模型，表示即使您選取多個資源，也會啟動單一工作流程例項。 每個檔案都以套件形式附加。

若 **多重資源支援** 不會為您的工作流程模型啟動，且已選取多個資源，然後會為每個資源啟動個別工作流程例項。

>[!NOTE]
>
>另請參閱 [設定多資源支援的工作流程](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) 以取得更多詳細資料。

### 工作流程階段 {#workflow-stages}

工作流程階段有助於在處理任務時以視覺效果呈現工作流程的進度。 它們可用於提供工作流程處理過程的概觀。 工作流程執行時，使用者可以檢視以下說明的進度 **階段** （相對於個別步驟）。

由於各個步驟名稱可以是特定的且技術性的，因此可以定義階段名稱，以提供工作流程進度的概念性檢視。

例如，對於包含六個步驟和四個階段的工作流程：

1. 您可以 [設定「工作流程階段」（顯示「工作流程進度」），然後將適當的階段指派給工作流程中的每個步驟](/help/sites-developing/workflows-models.md#configuring-workflow-stages-that-show-workflow-progress)：

   * 可以建立多個階段名稱。
   * 然後會為每個步驟指定個別的階段名稱（可以將階段名稱指定給一個或多個步驟）。

   | **步驟名稱** | **階段（指派給步驟）** |
   |---|---|
   | 步骤 1 | 创建 |
   | 步骤 2 | 创建 |
   | 步骤 3 | 审核 |
   | 步骤 4 | 批准 |
   | 步骤 5 | 完成 |
   | 步骤 6 | 完成 |

1. 執行工作流程時，使用者可以根據階段名稱（而不是步驟名稱）檢視進度。 工作流程進度會顯示在 [工作流程專案之任務詳細資訊視窗的工作流程資訊標籤](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions) 列於 [收件匣](/help/sites-authoring/inbox.md).

### 工作流程與Forms {#workflows-and-forms}

工作流程通常用於處理AEM中的表單提交。 它可以與 [核心元件表單元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-container.html?lang=en) 適用於標準AEM執行個體，或透過 [AEM Forms解決方案](/help/forms/using/aem-forms-workflow.md).

建立表單時，可輕鬆將表單提交與工作流程模型建立關聯。 例如，將內容儲存在存放庫的特定位置，或通知使用者表單提交及其內容。

### 工作流程與翻譯 {#workflows-and-translation}

工作流程也是 [翻譯](/help/sites-administering/translation.md) 程式。
