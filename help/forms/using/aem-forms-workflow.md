---
title: OSGi上以Forms為中心的工作流程
seo-title: Rapidly build adaptive forms-based processes, automate document services operations, and use Adobe Sign with AEM workflows
description: 使用AEM Forms工作流程自動化並快速建立稽核和核准，以啟動檔案服務
seo-description: Use AEM Forms Workflow to automate and rapidly build review and approvals, to start document services (For example, to convert a PDF document to another format), integrate with Adobe Sign signature workflow, and more.
uuid: 797ba0f7-a378-45ac-9f82-fa9a952027be
topic-tags: publish, document_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 73e63493-e821-443f-b50d-10797360f5d1
docset: aem65
exl-id: c3e5f8fc-d2b9-4f76-9a3d-4bc5733f5a5c
source-git-commit: d9608d584e822accc0c198fcf1d1b706d065938e
workflow-type: tm+mt
source-wordcount: '3681'
ht-degree: 2%

---

# OSGi上以Forms為中心的工作流程{#forms-centric-workflow-on-osgi}

![](do-not-localize/header.png)

企業會從數以百計與數以千計的表單、各種後端系統，以及線上或離線資料來源收集資料。 他們還擁有一組動態的使用者，可就資料做出決策，其中涉及反複的稽核和核准流程。

除了內部和外部對象的檢閱和核准工作流程，大型組織和企業也有重複性的任務。 例如，將PDF檔案轉換為另一種格式。 以手動方式完成這些工作會花費許多時間與資源。 企業也有法律要求以數位方式簽署檔案並封存表單資料，以供日後以預先定義的格式使用。

## OSGi上以Forms為中心的工作流程簡介 {#introduction-to-forms-centric-workflow-on-osgi}

您可以使用AEM Workflow快速建立最適化表單式工作流程。 這些工作流程可用於審查和核准、業務流程流、啟動檔案服務、與Adobe Sign簽名工作流程整合以及類似操作。 例如，信用卡申請處理、員工休假核准工作流程、將表單儲存為PDF檔案。 此外，這些工作流程也可在組織內或跨網路防火牆使用。

透過OSGi上的Forms工作流程，您可以快速在OSGi棧疊上建置和部署各種任務的工作流程，而不需要在JEE棧疊上安裝完整的流程管理功能。 工作流程的開發和管理使用熟悉的AEM Workflow和AEM Inbox功能。 工作流程構成了自動化跨越多個軟體系統、網路、部門甚至組織的真實業務流程的基礎。

設定後，這些工作流程可以手動觸發，以完成定義的流程，或在使用者提交表單或以程式設計方式執行 [通訊管理](/help/forms/using/cm-overview.md) 字母。 透過此增強的AEM Workflow功能，AEM Forms提供兩種相異但相似的功能。 作為部署策略的一部分，您需要決定哪一個適合您。 參閱 [比較](capabilities-osgi-jee-workflows.md) OSGi上的Forms中心AEM工作流程和JEE上的流程管理。 此外，如需部署拓撲，請參閱 [AEM Forms的架構和部署拓撲](/help/forms/using/aem-forms-architecture-deployment.md).

OSGi以Forms為中心的工作流程延伸 [AEM收件匣](/help/sites-authoring/inbox.md) 並提供額外的元件（步驟）供AEM Workflow編輯器使用，以新增對AEM Forms工作流程的支援。 擴充的AEM收件匣具有類似於 [AEM Forms工作區](introduction-html-workspace.md). 除了管理以人為中心的工作流程（核准、稽核等）外，您還可以使用AEM工作流程進行自動化 [檔案服務](/help/sites-developing/workflows-step-ref.md) — 相關作業(例如，產生PDF)和電子簽章(Adobe Sign)檔案。

所有AEM Forms工作流程步驟都支援使用變數。 變數可讓工作流程步驟在執行階段跨步驟保留和傳遞中繼資料。 您可以建立不同型別的變數來儲存不同型別的資料。 您也可以建立變數集合（陣列）來儲存多個相關、相同型別資料的執行個體。 通常情況下，當您需要根據其持有的值做出決定或儲存您稍後在程式中需要的資訊時，會使用變數或變數集合。 如需有關在這些以Forms為中心的工作流程元件中使用變數的詳細資訊（步驟），請參閱 [OSGi上以Forms為中心的工作流程 — 步驟參考](../../forms/using/aem-forms-workflow-step-reference.md). 如需建立和管理變數的詳細資訊，請參閱 [AEM工作流程中的變數](../../forms/using/variable-in-aem-workflows.md).

下圖說明在OSGi上建立、執行及監控Forms工作流程的端對端程式。

![introduction-to-aem-forms-workflow](assets/introduction-to-aem-forms-workflow.jpg)

## 开始之前 {#before-you-start}

* 工作流程是真實世界業務流程的表示法。 讓您的真實商業程式與商業程式參與者清單隨時待命。 此外，在開始建立工作流程之前，請準備好附屬資料(調適型表單、PDF檔案等)。
* 一個工作流程可以有多個階段。 這些階段會顯示在AEM收件匣中，並協助報告工作流程的進度。 將您的業務流程劃分為邏輯階段。
* 您可以設定AEM Workflows的指派工作步驟，以傳送電子郵件通知給使用者或受指派人。 所以， [啟用電子郵件通知](#configure-email-service).
* 工作流程也可以使用Adobe符號進行數位簽名。 如果您打算在工作流程中使用Adobe Sign，請 [設定適用於AEM Forms的Adobe Sign](../../forms/using/adobe-sign-integration-adaptive-forms.md) 將其用於工作流程之前。

## 建立工作流程模型 {#create-a-workflow-model}

工作流程模型包含商業流程的邏輯和流程。 它由一系列步驟組成。 這些步驟是AEM元件。 您可以視需要使用引數和指令碼來擴充工作流程步驟，以提供更多功能和控制。 除了開箱即用的AEM步驟外，AEM Forms還提供一些步驟。 如需AEM和AEM Forms步驟的詳細清單，請參閱 [AEM工作流程步驟參考](/help/sites-developing/workflows-step-ref.md) 和 [OSGi上以Forms為中心的工作流程 — 步驟參考](../../forms/using/aem-forms-workflow.md).

AEM提供直覺式使用者介面，可使用提供的工作流程步驟建立工作流程模型。 如需建立工作流程模型的逐步指示，請參閱 [建立工作流程模型](/help/sites-developing/workflows-models.md). 下列範例提供逐步指示，讓您為核准與複查工作流程建立工作流程模型：

>[!NOTE]
>
>您必須是工作流程編輯器群組的成員，才能建立或編輯工作流程模型。

### 建立核准和稽核工作流程的模型 {#create-a-model-for-an-approval-and-review-workflow}

核准和稽核工作流程適用於需要人為干預才能做出決定的任務。 下列範例會建立由前台銀行代理填寫的按揭貸款申請的工作流程模型。 填妥應用程式後，就會傳送以進行核准。 稍後會使用Adobe Sign將核准的申請傳送給申請人以取得電子簽章。

此範例可作為以下附加的套件提供。 使用封裝管理程式匯入並安裝範例。 您也可以執行下列步驟，手動建立應用程式的工作流程模型：

此範例會建立工作流程模型，作為前台銀行代理商填寫的抵押應用程式。 填寫完畢後，就會傳送應用程式以供核准。 稍後，核准的應用程式會傳送給客戶，以使用Adobe Sign進行電子簽章。 您可以使用封裝管理程式匯入及安裝範例。

[获取文件](assets/example-mortgage-loan-application.zip)

1. 開啟「工作流程模型」主控台。 預設URL為 `https://[server]:[port]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models`
1. 選取 **建立**，則 **建立模型**. 「新增工作流程模型」對話方塊隨即顯示。
1. 輸入 **標題** 和 **名稱** （選擇性）。 例如，抵押貸款應用程式。 點選 **完成**.
1. 選取新建立的工作流程模型並點選 **編輯**. 現在，您可以新增工作流程步驟以建立商業邏輯。 第一次建立工作流程模型時，模型會包含：

   * 步驟：流程開始與流程結束。 這些步驟代表工作流程的開始和結束。 這些步驟為必要步驟，無法編輯或移除。
   * 名為步驟1的參與者步驟範例。 此步驟已設定為指派工作專案給管理員使用者。 移除此步驟。

1. 啟用電子郵件通知。 您可以在OSGi上設定以Forms為中心的工作流程，以傳送電子郵件通知給使用者或受指派人。 執行以下設定以啟用電子郵件通知：

   1. 前往AEM設定管理員，網址為 `https://[server]:[port]/system/console/configMgr`.
   1. 開啟 **[!UICONTROL Day CQ郵件服務]** 設定。 指定 **[!UICONTROL smtp伺服器主機名稱]**， **[!UICONTROL SMTP伺服器連線埠、]** 和 **[!UICONTROL 「寄件者」地址]** 欄位。 单击“**[!UICONTROL 保存]**”。
   1. 開啟 **[!UICONTROL Day CQ連結外部化器]** 設定。 在 **[!UICONTROL 網域]** 欄位中，指定本機、作者和發佈執行個體的實際主機名稱/IP位址和連線埠號碼。 单击“**[!UICONTROL 保存]**”。

1. 建立工作流程階段。 一個工作流程可以有多個階段。 這些階段會顯示在AEM收件匣中，並報告工作流程的進度。

   若要定義階段，請點選 ![資訊圈](assets/info-circle.png) 圖示若要開啟工作流程模型屬性，請開啟 **階段** 標籤，為工作流程模型新增階段，然後點選 **儲存並關閉**. 以抵押貸款申請為例，建立階段：貸款請求、貸款請求狀態、要簽署的檔案，以及已簽署的貸款檔案。

1. 拖放 **指派任務** 步驟瀏覽器至工作流程模型。 使其成為模型的第一步。

   指派任務元件會將工作流程建立的任務指派給使用者或群組。 除了指派工作之外，您也可以使用元件來指定工作的最適化表單或非互動式PDF。 最適化表單必須接受使用者的輸入，非互動式PDF或使用唯讀最適化表單進行僅稽核工作流程。

   您也可以使用步驟來控制工作的行為。 例如，建立自動記錄檔案、將任務指派給特定使用者或群組、提交資料的路徑、要預先填入的資料路徑以及預設動作。 如需指派工作步驟選項的詳細資訊，請參閱 [OSGi上以Forms為中心的工作流程 — 步驟參考](../../forms/using/aem-forms-workflow.md) 檔案。

   ![工作流程編輯器](assets/workflow-editor.png)

   以按揭應用程式為例，設定指派工作步驟以使用唯讀最適化表單，並在工作完成後顯示PDF檔案。 此外，選取可核准貸款請求的使用者群組。 於 **動作** 標籤，停用 **提交** 選項。 建立 **actionTaken** 字串資料型別的變數，並將變數指定為 **路由變數**. 例如，actionTaken。 此外，請新增「核准」和「拒絕」路由。 路由在AEM收件匣中會顯示為個別的動作（按鈕）。 工作流程會根據使用者點選的動作（按鈕）選取分支。

   您可以針對設定為例如Mortgage Application之指派工作步驟的所有欄位整組值，匯入範例套件（可在區段開頭下載）。

1. 將OR拆分元件從步驟瀏覽器拖放至工作流程模型。 「OR分割」會在工作流程中建立分割，之後只有一個分支處於作用中狀態。 此步驟可讓您在工作流程中匯入條件式處理路徑。 您可視需要將工作流程步驟新增至每個分支。

   您可以使用規則定義、ECMA指令集或外部指令集來定義分支的路由表示式。

   使用運算式編輯器建立Branch 1和Branch 2的路由運算式。 這些路由運算式可協助您根據AEM收件匣中的使用者動作選擇分支。

   **分支1的路由運算式**

   使用者點選時 **核准** 在AEM收件匣中，會啟用分支1。

   ![OR分割範例](assets/orsplit_branch1_active_new.png)

   **分支2的路由運算式**

   使用者點選時 **拒絕** 在AEM收件匣中，會啟用分支2。

   ![OR分割範例](assets/orsplit_branch2_active_new.png)

   如需使用變數建立路由運算式的詳細資訊，請參閱 [AEM Forms工作流程中的變數](../../forms/using/variable-in-aem-workflows.md).

1. 新增其他工作流程步驟以建立商業邏輯。

   在抵押範例中，新增產生記錄檔案、兩個指派任務步驟，以及一個簽署檔案步驟至模型的「分支1」，如下圖所示。 一個指派任務步驟是顯示和傳送 **將簽署給申請者的貸款檔案** 另一個指派任務元件為 **顯示已簽署的檔案**. 此外，新增指派工作元件至分支2。 當使用者點選AEM收件匣中的拒絕時，它會啟動。

   針對指派任務步驟、記錄檔案步驟和簽署檔案步驟的所有欄位之完整值集（例如抵押應用程式），匯入範例套件，可在本節開頭下載。

   工作流程模型已準備就緒。 您可以透過各種方法啟動工作流程。 如需詳細資訊，請參閱 [在OSGi上啟動以Forms為中心的工作流程](#launch).

   ![workflow-editor-mortgage](assets/workflow-editor-mortgage.png)

## 建立以Forms為中心的工作流程應用程式 {#create-a-forms-centric-workflow-application}

應用程式是與工作流程關聯的最適化表單。 透過「收件匣」提交應用程式時，它會啟動相關的工作流程。 若要讓Forms工作流程成為AEM收件匣和AEM Forms應用程式中的應用程式，請執行以下動作以建立工作流程應用程式：

>[!NOTE]
>
>您必須是fd-administrator群組的成員，才能建立和管理工作流程應用程式。

1. 在您的AEM編寫執行個體上，前往 ![tools-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL 管理工作流程應用程式]** 和點選 **[!UICONTROL 建立]**.
1. 在「建立工作流程應用程式」視窗中，為下列欄位提供輸入，然後點選 **建立**. 隨即會建立新應用程式，並列在「工作流程應用程式」畫面中。

<table>
 <tbody>
  <tr>
   <td>字段</td>
   <td>描述</td>
  </tr>
  <tr>
   <td>标题</td>
   <td>標題會顯示在AEM收件匣中，並協助使用者選擇應用程式。 保持其描述性。 例如，儲蓄帳戶開立應用程式。<br /> </td>
  </tr>
  <tr>
   <td>名称 </td>
   <td>指定應用程式的名稱。 除字母、數字、連字型大小和底線以外的所有字元都會取代為連字型大小。 </td>
  </tr>
  <tr>
   <td>描述</td>
   <td>說明會顯示在AEM收件匣中。 在說明欄位中提供應用程式的詳細資訊。 例如，應用程式的用途。<br /> </td>
  </tr>
  <tr>
   <td>最適化表單</td>
   <td><p>指定自適應表單的路徑。 當使用者啟動應用程式時，會顯示指定的最適化表單。</p> <p><strong>注意</strong>：工作流程應用程式不支援超過一頁的表單和PDF檔案，或需要在Apple iPad上捲動。 在Apple iPad上開啟應用程式，且最適化表單或PDF檔案長於頁面時，來自第二個頁面的表單欄位和內容會遺失。</p> </td>
  </tr>
  <tr>
   <td>访问组</td>
   <td><p>選取群組。 只有選取群組的成員才能在AEM收件匣中看到應用程式。 存取群組選項可讓工作流程 — 使用者群組的所有群組都可供選取。 </p> <br /> </td>
  </tr>
  <tr>
   <td>预填服务</td>
   <td>選取 <a href="../../forms/using/prepopulate-adaptive-form-fields.md#aem-forms-custom-prefill-service" target="_blank">預填服務</a> 最適化表單的預設值。<br /> </td>
  </tr>
  <tr>
   <td>工作流模型</td>
   <td>選取 <a href="../../forms/using/aem-forms-workflow.md#create-a-workflow-model">工作流程模型</a> 應用程式的。 工作流程模型包含業務處理的邏輯和流程。 </td>
  </tr>
  <tr>
   <td>数据文件路径</td>
   <td>指定crx-repository中資料檔案的路徑。 路徑是相對於最適化表單有效負載的，並包含資料檔案的名稱。 一律包含檔案的完整名稱，包括副檔名（如適用）。 例如，[payload]/data.xml。 </td>
  </tr>
  <tr>
   <td>附件路径</td>
   <td>指定crx-repository中附件資料夾的路徑。 附件路徑是相對於承載位置。 例如，[payload]/data.xml。 </td>
  </tr>
  <tr>
   <td>记录文档路径</td>
   <td>指定crx-repository中記錄檔案的路徑。 路徑是相對於最適化表單裝載位置。 一律包含檔案的完整名稱，包括副檔名（如適用）。 例如，[payload]/DOR/creditcard.pdf。</td>
  </tr>
 </tbody>
</table>

## 在OSGi上啟動以Forms為中心的工作流程 {#launch}

您可以透過以下方式啟動或觸發以Forms為中心的工作流程：

* [從AEM收件匣提交應用程式](#inbox)
* [從AEM Forms應用程式提交應用程式](#afa)

* [提交最適化表單](#af)
* [使用watched資料夾](#watched)

* [提互動動式通訊或信件](#letter)

### 從AEM收件匣提交應用程式 {#inbox}

您建立的工作流程應用程式可在「收件匣」中作為應用程式使用。 工作流程 — 使用者群組成員的使用者可以填寫並提交觸發相關工作流程的應用程式。 如需使用AEM收件匣提交應用程式和管理工作的相關資訊，請參閱 [在AEM收件匣中管理Forms應用程式和工作](../../forms/using/manage-applications-inbox.md).

### 從AEM Forms應用程式提交應用程式 {#afa}

AEM Forms應用程式會與AEM Forms伺服器同步，並可讓您變更帳戶中的表單資料、工作、工作流程應用程式和儲存的資訊（草稿/範本）。 如需詳細資訊，請參閱 [AEM Forms應用程式](/help/forms/using/aem-forms-app.md) 和相關文章。

### 提交最適化表單 {#af}

您可以設定最適化表單的提交動作，以在提交最適化表單時啟動工作流程。 調適型表單提供 **叫用AEM工作流程** 提交動作，以在提交最適化表單時啟動工作流程。 如需提交動作的詳細資訊，請參閱 [設定提交動作](../../forms/using/configuring-submit-actions.md). 若要透過AEM Forms應用程式提交調適型表單，請在調適型表單屬性中啟用「與AEM Forms應用程式同步」 。

您可以設定最適化表單，以從AEM Forms應用程式同步、提交和觸發工作流程。 如需詳細資訊，請參閱 [使用表單](/help/forms/using/working-with-form.md).

### 使用watched資料夾 {#watched}

管理員（fd-administrators群組的成員）可以設定網路資料夾，以在使用者將檔案(例如PDF檔案)放在資料夾中時執行預先設定的工作流程。 工作流程完成後，它可以將結果檔案儲存到指定的輸出資料夾。 這類資料夾稱為 [觀察資料夾](../../forms/using/watched-folder-in-aem-forms.md). 執行以下程式來設定watched資料夾以啟動工作流程：

1. 在您的AEM編寫執行個體上，前往 ![tools-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL 設定Watched資料夾]**. 顯示已設定的Watched資料夾清單。
1. 點選 **[!UICONTROL 新增]**. 隨即顯示欄位清單。 指定下列欄位的值，以設定工作流程的Watched資料夾：

<table>
 <tbody>
  <tr>
   <td>字段</td>
   <td>描述</td>
  </tr>
  <tr>
   <td><span class="uicontrol">名称</code></td>
   <td>指定Watched資料夾的名稱。 此欄位僅支援英數字元。</td>
  </tr>
  <tr>
   <td><span class="uicontrol">路径</code></td>
   <td>指定Watched資料夾的實體位置。 在叢集環境中，使用可從AEM叢集節點存取的共用網路資料夾。</td>
  </tr>
  <tr>
   <td><span class="uicontrol">文件处理方法</code></td>
   <td>選取 <span class="uicontrol">工作流程 </code>選項。 </code></td>
  </tr>
  <tr>
   <td><span class="uicontrol">工作流模型</code></td>
   <td>選取工作流程模型。<br /> </td>
  </tr>
  <tr>
   <td><span class="uicontrol">输出文件模式</code></td>
   <td>指定輸出檔案和目錄的目錄結構。 您也可以指定 <a href="/help/forms/using/admin-help/configuring-watched-folder-endpoints.md" target="_blank">輸出檔案和目錄的模式</a>.</td>
  </tr>
 </tbody>
</table>

1. 點選 **進階**. 指定下列欄位的值並點選 **建立**. Watched資料夾已設定為啟動工作流程。 現在，每當檔案放入Watched資料夾的輸入目錄時，就會觸發指定的工作流程。

   | 字段 | 描述 |
   |---|---|
   | 有效负荷映射器过滤器 | 當您建立watched資料夾時，它會在crx-repository中建立資料夾結構。 資料夾結構可作為工作流程的裝載。 您可以撰寫指令碼來對應AEM Workflow，以接受來自watched資料夾結構的輸入。 現成可用的實作，並列於裝載對應程式篩選器中。 如果您沒有自訂實作，請選取預設實作。 |

   進階索引標籤包含更多欄位。 這些欄位大多包含預設值。 若要瞭解所有欄位，請參閱 [建立或設定watched資料夾](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md) 文章。

### 提互動動式通訊或信件 {#letter}

您可以在提互動動式通訊或信函時，在OSGi上關聯並執行以Forms為中心的工作流程。 在通訊管理中，工作流程用於後處理互動式通訊和信件。 例如，寄送電子郵件、列印、傳真或封存最終信件。 如需詳細步驟，請參閱 [互動式通訊和信函的後處理](../../forms/using/submit-letter-topostprocess.md).

## 其他設定 {#additional-configurations}

### 設定電子郵件服務 {#configure-email-service}

您可以使用AEM Workflows的指派任務和傳送電子郵件步驟來傳送電子郵件。 執行以下步驟，指定傳送電子郵件所需的電子郵件伺服器和其他設定：

1. 前往AEM設定管理員，網址為 `https://[server]:[port]/system/console/configMgr`.
1. 開啟 **[!UICONTROL Day CQ郵件服務]** 設定。 指定 **[!UICONTROL smtp伺服器主機名稱]**， **[!UICONTROL SMTP伺服器連線埠、]** 和 **[!UICONTROL 「寄件者」地址]** 欄位。 单击“**[!UICONTROL 保存]**”。
1. 開啟 **[!UICONTROL Day CQ連結外部化器]** 設定。 在 **[!UICONTROL 網域]** 欄位中，指定本機、作者和發佈執行個體的實際主機名稱/IP位址和連線埠號碼。 单击“**[!UICONTROL 保存]**”。

### 清除工作流程例項 {#purge-workflow-instances}

最大限度地减少工作流实例的数量可以提高工作流引擎的性能，因此，您可以定期从存储库中清除已完成或正在运行的工作流实例。如需詳細資訊，請參閱 [定期清除工作流程例項](/help/sites-administering/workflows-administering.md#regular) 清除工作流程例項。

## 將敏感資料引數化為工作流程變數並儲存在外部資料存放區中 {#externalize-wf-variables}

從適用性表單提交到的任何資料 [!DNL Experience Manager] 工作流程可以包含您企業一般使用者的PII （個人識別資訊）或SPD （敏感個人資料）。 不過，並非強制要求將您的資料儲存在 [!DNL Adobe Experience Manager] [JCR存放庫](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-jcr.html). 您可以將資訊引數化，將一般使用者資料的儲存空間外部化至您的受管理資料儲存空間（例如Azure blob儲存空間）。 [工作流程變數](/help/forms/using/variable-in-aem-workflows.md).

在 [!DNL Adobe Experience Manager] Forms工作流程中，會透過工作流程變數，透過一系列工作流程步驟處理和傳遞資料。 這些變數稱為儲存在工作流程例項中繼資料節點中的屬性或機碼值組；例如 `/var/workflow/instances/<serverid>/<datebucket>/<uniquenameof model>_<id>/data/metaData`. 這些工作流程變數可以外部化至JCR以外的獨立存放庫，然後由處理 [!DNL Adobe Experience Manager] 工作流程。 [!DNL Adobe Experience Manager] 提供API `[!UICONTROL UserMetaDataPersistenceProvider]` 以將工作流程變數儲存在您的受管理外部儲存空間中。 進一步瞭解在中針對客戶擁有的資料存放區使用工作流程變數 [!DNL Adobe Experience Manager]，請參閱 [管理外部資料存放區的工作流程變數](/help/sites-administering/workflows-administering.md#using-workflow-variables-customer-datastore).
[!DNL Adobe] 提供下列內容 [範例](https://github.com/adobe/workflow-variable-externalizer) 若要使用API將變數從工作流程中繼資料對應儲存至Azure blob儲存體 [UserMetaDataPersistenceProvider](https://github.com/adobe/workflow-variable-externalizer/blob/master/README.md). 在類似的行上，您可以使用範例作為使用指南 [UserMetaDataPersistenceProvider] API可將任何外部資料儲存中的工作流程變數外部化 [!DNL Adobe Experience Manager] 並管理相同專案。

>[!NOTE]
>
>將工作流程變數儲存至外部資料儲存體時，請參考 [工作流程外部資料儲存的准則](#guidelines-workflows-external-data-storage).

### 安裝工作流程API範例實作

若要將工作流程變數儲存在受管理的Azure Blob儲存體中：
1. 安裝 [範例](https://github.com/adobe/workflow-variable-externalizer) 工作流程API [UserMetaDataPersistenceProvider](https://github.com/adobe/workflow-variable-externalizer/blob/master/README.md) 如下所示：

   1. 在專案根目錄中執行 `mvn clean install` 使用Maven 3執行命令。

   1. 若要將套件組合和內容套件部署給作者，請執行 `mvn clean install -PautoInstallPackage`.

   1. 若只要將套件組合部署至作者，請執行 `mvn clean install -PautoInstallBundle`.

1. 在的外部化程式OSGi設定檔案中，初始化以下屬性： `ui.config` 內容封裝：

   ```JQL
      accountKey=""
      accountName=""
      endpointSuffix=""
      containerName=""
      protocol=""
   ```

以下是這些屬性的用途（和範例）：

* **accountKey** 是授權存取的金鑰。

* **帳戶名稱** 是必須儲存資料的azure帳戶。

* **endpointsuffix**，例如 `core.windows.net`.

* **containername** 是帳戶中需要儲存資料的容器。 此範例假設容器存在。

* **通訊協定**，例如 `https` 或 `http`.

1. 在中設定工作流程模型 [!DNL Adobe Experience Manager]. 若要瞭解如何設定外部儲存的工作流程模型，請參閱 [設定工作流程模型](#configure-aem-wf-model).

### 在中設定工作流程模型 [!DNL Adobe Experience Manager] 用於外部資料儲存 {#configure-aem-wf-model}

若要設定外部資料儲存體的AEM Workflow模型：

1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**.

1. 選取模型名稱並選取 **[!UICONTROL 編輯]**.

1. 選取「頁面資訊」圖示並選取 **[!UICONTROL 開啟屬性]**.

1. 選取 **[!UICONTROL 將工作流程資料儲存區外部化]**.

1. 選取 **[!UICONTROL 儲存並關閉]** 以儲存屬性。

### 外部資料儲存的AEM工作流程准則 {#guidelines-workflows-external-data-storage}

以下是您使用時的指引 [!DNL Adobe Experience Manager] 工作流程並將資料儲存至外部資料儲存庫(例如Microsoft Azure儲存伺服器)：

* 在工作流程模型步驟中定義輸入和輸出資料檔案及附件時，使用變數來儲存資料。 不要選取 **[!UICONTROL 相對於裝載]** 和 **[!UICONTROL 在絕對路徑上可用]** 選項。 此 **[!UICONTROL 相對於裝載]** 和 **[!UICONTROL 在絕對路徑上可用]** 選項不會在您之後自動顯示 [設定 [!DNL Adobe Experience Manager] 外部資料儲存的工作流程模型](#configure-aem-wf-model).

* 將最適化表單提交至AEM Workflow時，使用變數來儲存資料檔案和附件。 不要選取 **[!UICONTROL 相對於裝載]** 選項提交最適化表單至 [!DNL Adobe Experience Manager] 工作流程。 此 **[!UICONTROL 相對於裝載]** 選項不會在您之後自動顯示 [設定 [!DNL Adobe Experience Manager] 外部資料儲存的工作流程模型](#configure-aem-wf-model).

* 不要使用自訂 [!DNL Adobe Experience Manager] 工作流程模型中的工作流程步驟，用於將資料儲存在 [!UICONTROL CRX DE] 存放庫。

* 當您 [設定 [!DNL Adobe Experience Manager] 外部資料儲存的工作流程模型](#configure-aem-wf-model)，不要建立自訂欄 [!DNL Adobe Experience Manager] [!UICONTROL 收件匣] 因為如果工作專案位於 [!DNL Adobe Experience Manager] [!UICONTROL 收件匣] 屬於標籤為外部儲存的工作流程。
