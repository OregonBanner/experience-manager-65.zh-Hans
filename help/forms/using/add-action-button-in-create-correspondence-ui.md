---
title: 在建立通訊UI中新增自訂動作/按鈕
seo-title: Add custom action/button in Create Correspondence UI
description: 瞭解如何在建立通訊UI中新增自訂動作/按鈕
seo-description: Learn how to add custom action/button in Create Correspondence UI
uuid: 1b2b00bb-93ef-4bfe-9fc5-25c45e4cb4b1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 046e3314-b436-47ed-98be-43d85f576789
docset: aem65
feature: Correspondence Management
exl-id: a582ba41-83cb-46f2-9de9-3752f6a7820a
source-git-commit: ba2c753cfd041ccfcd6ba7a45648234290b99d25
workflow-type: tm+mt
source-wordcount: '1881'
ht-degree: 1%

---

# 在建立通訊UI中新增自訂動作按鈕 {#add-custom-action-button-in-create-correspondence-ui}

## 概述 {#overview}

「通訊管理」解決方案可讓您將自訂動作新增到「建立通訊」使用者介面。

本檔案中的案例說明如何在「建立通訊使用者介面」中建立按鈕，以共用信函作為附加到電子郵件的稽核PDF。

### 前提条件 {#prerequisites}

若要完成此案例，您需要下列專案：

* CRX和JavaScript的相關知識
* LiveCycle伺服器

## 案例：在「建立通訊使用者介面」中建立按鈕，以傳送信件以供複查 {#scenario-create-the-button-in-the-create-correspondence-user-interface-to-send-a-letter-for-review}

將具有動作的按鈕（在此傳送信件以供稽核）新增至「建立通訊」使用者介面包括：

1. 將按鈕新增至「建立通訊」使用者介面
1. 新增動作處理至按鈕
1. 新增LiveCycle程式以啟用動作處理

### 將按鈕新增至「建立通訊」使用者介面 {#add-the-button-to-the-create-correspondence-user-interface}

1. 前往 `https://'[server]:[port]'/[ContextPath]/crx/de` 並以管理員身分登入。
1. 在apps資料夾中，建立名為的資料夾 `defaultApp` 具有類似於defaultApp資料夾（位於config資料夾）的路徑/結構。 使用下列步驟建立資料夾：

   1. 以滑鼠右鍵按一下 **defaultApp** 資料夾並選取 **覆蓋節點**：

      /libs/fd/cm/config/defaultApp/

      ![覆蓋節點](assets/1_defaultapp.png)

   1. 確定「覆蓋節點」對話方塊具有下列值：

      **路徑：** /libs/fd/cm/config/defaultApp/

      **覆蓋位置：** /apps/

      **符合節點型別：** 已核取

      ![覆蓋節點](assets/2_defaultappoverlaynode.png)

   1. 单击&#x200B;**确定**。
   1. 按一下 **全部儲存**.

1. 複製/apps分支下的acmExtensionsConfig.xml檔案（存在於/libs分支下）。

   1. 前往「/libs/fd/cm/config/defaultApp/acmExtensionsConfig.xml」

   1. 以滑鼠右鍵按一下acmExtensionsConfig.xml檔案，然後選取 **複製**.

      ![複製acmExtensionsConfig.xml](assets/3_acmextensionsconfig_xml_copy.png)

   1. 以滑鼠右鍵按一下 **defaultApp** 資料夾「/apps/fd/cm/config/defaultApp/」，然後選取 **貼上**.
   1. 按一下 **全部儲存**.

1. 連按兩下您在apps資料夾中新建立的acmExtentionsConfig.xml復本。 檔案隨即開啟以進行編輯。
1. 找到下列程式碼：

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <extensionsConfig>
       <modelExtensions>
           <modelExtension type="LetterInstance">
     <customAction name="Preview" label="loc.letterInstance.preview.label" tooltip="loc.letterInstance.preview.tooltip" styleName="previewButton"/>
               <customAction name="Submit" label="loc.letterInstance.submit.label" tooltip="loc.letterInstance.submit.tooltip" styleName="submitButton" permissionName="forms-users"/>
               <customAction name="SaveAsDraft" label="loc.letterInstance.saveAsDraft.label" tooltip="loc.letterInstance.saveAsDraft.tooltip" styleName="submitButton" permissionName="forms-users"/>
               <customAction name="Close" label="loc.letterInstance.close.label" tooltip="loc.letterInstance.close.tooltip" styleName="closeButton"/>
           </modelExtension>
       </modelExtensions>
   </extensionsConfig>
   ```

1. 若要以電子郵件傳送信件，您可以使用LiveCycleForms Workflow。 在acmExtensionsConfig.xml的modelExtension標籤下新增customAction標籤，如下所示：

   ```xml
    <customAction name="Letter Review" label="Letter Review" tooltip="Letter Review" styleName="" permissionName="forms-users" actionHandler="CM.domain.CCRCustomActionHandler">
         <serviceName>Forms Workflow -> SendLetterForReview/SendLetterForReviewProcess</serviceName>
       </customAction>
   ```

   ![customAction標籤](assets/5_acmextensionsconfig_xml.png)

   modelExtension標籤有一組customAction子標籤，可用來設定動作、許可權和動作按鈕的外觀。 以下是customAction設定標籤的清單：

   | **名称** | **描述** |
   |---|---|
   | name | 要執行之動作的英數字元名稱。 此標籤的值為必要值、唯一值（在modelExtension標籤內），且必須以字母開頭。 |
   | 標籤 | 要在動作按鈕上顯示的標籤 |
   | 工具提示 | 按鈕的工具提示文字，當使用者將滑鼠懸停在按鈕上時顯示。 |
   | 樣式名稱 | 套用至動作按鈕的自訂樣式名稱。 |
   | permissionName | 只有在使用者具有permissionName所指定的許可權時，才會顯示對應的動作。 當您指定permissionName為 `forms-users`，所有使用者都能存取此選項。 |
   | actionHandler | 使用者按一下按鈕時所呼叫之ActionHandler類別的完整名稱。 |

   除了上述引數外，還可以有其他與customAction相關的設定。 這些額外的設定可透過CustomAction物件供處理常式使用。

   | **名称** | **描述** |
   |---|---|
   | serviceName | 如果customAction包含名為serviceName的子標籤，則按一下相關按鈕/連結時，會以由serviceName標籤代表的名稱呼叫程式。 確定此程式與信件PostProcess具有相同的簽章。 在服務名稱中新增「Forms Workflow->」首碼。 |
   | 標籤名稱中包含cm_首碼的引數 | 如果customAction包含以名稱cm_開頭的子標籤，則在後置處理程式中（無論是信件後置處理程式或由serviceName標籤表示的特殊處理程式），這些引數可在相關標籤下方的輸入XML程式碼中使用，並會移除cm_前置詞。 |
   | actionName | 每當因點按而需進行後處理時，提交的XML都會在標籤下包含具有名稱的特殊標籤，且帶有使用者動作的名稱。 |

1. 按一下 **全部儲存**.

#### 在/apps分支中建立具有屬性檔案的區域設定資料夾 {#create-a-locale-folder-with-properties-file-in-the-apps-branch}

ACMExtensionsMessages.properties檔案包含「建立通訊」使用者介面中各個欄位的標籤和工具提示訊息。 若要讓自訂動作/按鈕運作，請在/apps分支中製作此檔案的復本。

1. 以滑鼠右鍵按一下 **地區設定** 資料夾並選取 **覆蓋節點**：

   /libs/fd/cm/config/defaultApp/locale

1. 確定「覆蓋節點」對話方塊具有下列值：

   **路徑：** /libs/fd/cm/config/defaultApp/locale

   **覆蓋位置：** /apps/

   **符合節點型別：** 已核取

1. 单击&#x200B;**确定**。
1. 按一下 **全部儲存**.
1. 以滑鼠右鍵按一下以下檔案並選取 **複製**：

   `/libs/fd/cm/config/defaultApp/locale/ACMExtensionsMessages.properties`

1. 以滑鼠右鍵按一下 **地區設定** 資料夾並選取 **貼上**：

   `/apps/fd/cm/config/defaultApp/locale/`

   ACMExtensionsMessages.properties檔案會複製到地區設定資料夾中。

1. 若要將新加入的自訂動作/按鈕的標籤當地語系化，請在中建立相關地區設定的ACMExtensionsMessages.properties檔案 `/apps/fd/cm/config/defaultApp/locale/`.

   例如，若要將本文建立的自訂動作/按鈕當地語系化，請使用下列專案建立名為ACMExtensionsMessages_fr.properties的檔案：

   `loc.letterInstance.letterreview.label=Revue De Lettre`

   同樣地，您可以在此檔案中新增更多屬性，例如工具提示和樣式。

1. 按一下 **全部儲存**.

#### 重新啟動Adobe資產撰寫器建置區塊套件 {#restart-the-adobe-asset-composer-building-block-bundle}

進行每個伺服器端變更後，請重新啟動Adobe資產撰寫器建置區塊套件。 在此案例中，伺服器端的acmExtensionsConfig.xml和ACMExtensionsMessages.properties檔案經過編輯，因此Adobe資產撰寫器建置區塊套件組合需要重新啟動。

>[!NOTE]
>
>您可能需要清除瀏覽器快取。

1. 转到 `https://[host]:'port'/system/console/bundles`. 如有必要，請以管理員身分登入。

1. 找出Adobe資產撰寫器建置區塊套件。 重新啟動套件：按一下[停止]，然後按一下[啟動]。

   ![Adobe資產撰寫器建置區塊](assets/6_assetcomposerbuildingblockbundle.png)

重新啟動Adobe資產撰寫器建置區塊組合後，「建立通訊」使用者介面中會出現自訂按鈕。 您可以在建立通訊使用者介面中開啟信函以預覽自訂按鈕。

### 將動作處理新增至按鈕 {#add-action-handling-to-the-button}

根據預設，「建立通訊」使用者介面會在cm.domain.js檔案中的以下位置實施ActionHandler：

/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccr/js/cm.domain.js

若要自訂動作處理，請在CRX的/apps分支中建立cm.domain.js檔案的覆蓋。

處理按一下動作/按鈕上的動作/按鈕包含下列專案的邏輯：

* 將新增的動作設為visible/invisible：覆寫actionVisible()函式來完成。
* 啟用/停用新增的動作：覆寫actionEnabled()函式來完成。
* 使用者按一下按鈕時的實際動作處理：覆寫handleAction()函式的實作來完成。

1. 转到 `https://'[server]:[port]'/[ContextPath]/crx/de`. 如有必要，請以管理員身分登入。

1. 在apps資料夾中，建立名為的資料夾 `js` 在CRX的/apps分支中，其結構與以下資料夾類似：

   `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js`

   使用下列步驟建立資料夾：

   1. 以滑鼠右鍵按一下 **js** 資料夾並選取 **覆蓋節點**：

      `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js`

   1. 確定「覆蓋節點」對話方塊具有下列值：

      **路徑：** /libs/fd/cm/ccr/gui/components/admin/clientlibs/crui/js

      **覆蓋位置：** /apps/

      **符合節點型別：** 已核取

   1. 单击&#x200B;**确定**。
   1. 按一下 **全部儲存**.

1. 在js資料夾中，使用按鈕的動作處理程式碼，建立名為ccrcustomization.js的檔案，步驟如下：

   1. 以滑鼠右鍵按一下 **js** 資料夾並選取 **「建立」>「建立檔案」**：

      `/apps/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js`

      將檔案命名為ccrcustomization.js。

   1. 連按兩下ccrcustomization.js檔案，以在CRX中開啟。
   1. 在檔案中貼上下列程式碼，然後按一下 **全部儲存**：

      ```javascript
      /* for adding and handling custom actions in Extensible Toolbar.
        * One instance of handler will be created for each action.
        * CM.domain.CCRCustomActionHandler is actionHandler class.
        */
      var CCRCustomActionHandler;
          CCRCustomActionHandler = CM.domain.CCRCustomActionHandler = new Class({
              className: 'CCRCustomActionHandler',
              extend: CCRDefaultActionHandler,
              construct : function(action,model){
              }
          });
          /**
           * Called when user user click an action
           * @param extraParams additional arguments that may be passed to handler (For future use)
           */
          CCRCustomActionHandler.prototype.handleAction = function(extraParams){
              if (this.action.name == CCRCustomActionHandler.SEND_FOR_REVIEW) {
                  var sendForReview = function(){
                      var serviceName = this.action.actionConfig["serviceName"];
                      var inputParams = {};
                      inputParams["dataXML"] = this.model.iccData.data;
                      inputParams["letterId"] = this.letterVO.id;
                      inputParams["letterName"] = this.letterVO.name;
                      inputParams["mailId"] = $('#email').val();
                      /*function to invoke the LivecyleService */
                      ServiceDelegate.callJSONService(this,"lc.icc.renderlib.serviceInvoker.json","invokeProcess",[serviceName,inputParams],this.onProcessInvokeComplete,this.onProcessInvokeFail);
                      $('#ccraction').modal("hide");
                  }
                  if($('#ccraction').length == 0){
                      /*For first click adding popup & setting letterName.*/
                      $("body").append(popUp);
                      $("input[id*='letterName']").val(this.letterVO.name);
                      $(document).on('click',"#submitLetter",$.proxy( sendForReview, this ));
                  }
                  $('#ccraction').modal("show");
              }
          };
          /**
           * Should the action be enabled in toolbar
           * @param extraParams additional arguements that may be passed to handler (For future use)
           * @return flag indicating whether the action should be enabled
           */
         CCRCustomActionHandler.prototype.actionEnabled = function(extraParams){
                  /*can be customized as per user requirement*/
                  return true;
          };
          /**
           * Should the action be visible in toolbar
           * @param extraParams additional arguments that may be passed to handler (For future use)
           * @return flag indicating whether the action should be enabled
           */
          CCRCustomActionHandler.prototype.actionVisible = function(extraParams){
              /*Check can be enabled for Non-Preview Mode.*/
              return true;
          };
          /*SuccessHandler*/
          CCRCustomActionHandler.prototype.onProcessInvokeComplete = function(response) {
              ErrorHandler.showSuccess("Letter Sent for Review");
          };
          /*FaultHandler*/
          CCRCustomActionHandler.prototype.onProcessInvokeFail = function(event) {
              ErrorHandler.showError(event.message);
          };
          CCRCustomActionHandler.SEND_FOR_REVIEW  = "Letter Review";
      /*For PopUp*/
          var popUp = '<div class="modal fade" id="ccraction" tabindex="-1" role="dialog" aria-hidden="true">'+
          '<div class="modal-dialog modal-sm">'+
              '<div class="modal-content">' +
                  '<div class="modal-header">'+
                      '<button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</code></button>'+
                      '<h4 class="modal-title"> Send Review </h4>'+
                  '</div>'+
                  '<div class="modal-body">'+
                      '<form>'+
                          '<div class="form-group">'+
                              '<label class="control-label">Email Id</label>'+
                              '<input type="text" class="form-control" id="email">'+
                          '</div>'+
                          '<div class="form-group">'+
                              '<label  class="control-label">Letter Name</label>'+
                              '<input id="letterName" type="text" class="form-control" readonly>'+
                          '</div>'+
                          '<div class="form-group">'+
                              '<input id="letterData" type="text" class="form-control hide" readonly>'+
                          '</div>'+
                      '</form>'+
                  '</div>'+
                  '<div class="modal-footer">'+
                     '<button type="button" class="btn btn-default" data-dismiss="modal"> Cancel </button>'+
                     '<button type="button" class="btn btn-primary" id="submitLetter"> Submit </button>'+
                  '</div>'+
              '</div>'+
          '</div>'+
      '</div>';
      ```

### 新增LiveCycle程式以啟用動作 <span class="acrolinxCursorMarker"></code>處理 {#add-the-livecycle-process-to-enable-action-span-class-acrolinxcursormarker-span-handling}

在此案例中，請啟用下列元件，這些元件是附加的components.zip檔案的一部分：

* DSC元件jar (DSCSample.jar)
* 傳送信件以供複查程式LCA (SendLetterForReview.lca)

下載並解壓縮components.zip檔案，以取得DSCSample.jar和SendLetterForReview.lca檔案。 請依照下列程式使用這些檔案。
[获取文件](assets/components.zip)

#### 設定LiveCycle伺服器以執行LCA程式 {#configure-the-livecycle-server-to-run-the-lca-process}

>[!NOTE]
>
>只有在您進行OSGI設定時才需要此步驟，而且您正在實作的自訂型別需要LC整合。

LCA程式會在LiveCycle伺服器上執行，而且需要伺服器位址和登入認證。

1. 前往 `https://'[server]:[port]'/system/console/configMgr` 並以管理員身分登入。
1. 找到AdobeLiveCycle使用者端SDK設定，然後按一下 **編輯** （編輯圖示）。 「組態」面板隨即開啟。

1. 輸入下列詳細資料，然後按一下 **儲存**：

   * **伺服器Url**：動作處理常式程式碼使用其「傳送以供稽核」服務的LC伺服器URL。
   * **使用者名稱**：LC伺服器的管理員使用者名稱
   * **密碼**：管理員使用者名稱的密碼

   ![AdobeLiveCycle使用者端SDK設定](assets/3_clientsdkconfiguration.png)

#### 安裝LiveCycle封存(LCA) {#install-livecycle-archive-lca}

啟用電子郵件服務程式的必要LiveCycle程式。

>[!NOTE]
>
>若要檢視此處理作業或建立您自己的類似處理，您需要Workbench。

1. 以管理員身分登入LiveCycle®伺服器管理ui，網址為 `https:/[lc server]/:[lc port]/adminui`.

1. 導覽至 **首頁>服務>應用程式和服務>應用程式管理**.

1. 如果SendLetterForReview應用程式已存在，請略過此程式中的其餘步驟，否則繼續後續步驟。

   ![UI中的SendLetterForReview應用程式](assets/12_applicationmanagementlc.png)

1. 按一下 **匯入**.

1. 按一下 **選擇檔案** 並選取SendLetterForReview.lca。

   ![選取SendLetterForReview.lca檔案](assets/14_sendletterforreview_lca.png)

1. 按一下 **預覽**.

1. 選取 **匯入完成時將資產部署到執行階段**.

1. 按一下 **匯入**.

#### 將ServiceName新增至允許清單服務清單 {#adding-servicename-to-the-allowlist-service-list}

在Experience Manager伺服器中提及您要存取Experience Manager伺服器的LiveCycle服務。

1. 以管理員身分登入 `https:/[host]:'port'/system/console/configMgr`.

1. 找到並按一下 **AdobeLiveCycle使用者端SDK設定**. 「AdobeLiveCycle使用者端SDK設定」面板隨即顯示。
1. 在服務名稱清單中，按一下+圖示並新增serviceName **SendLetterForReview/SendLetterForReviewProcess**.

1. 单击“**保存**”。

#### 設定電子郵件服務 {#configure-the-email-service}

在此案例中，若要讓「通訊管理」能夠傳送電子郵件，請在LiveCycle伺服器中設定電子郵件服務。

1. 使用管理員憑證登入LiveCycle伺服器管理ui，網址為 `https:/[lc server]:[lc port]/adminui`.

1. 導覽至 **首頁>服務>應用程式和服務>服務管理**.

1. 找到並按一下 **電子郵件服務**.

1. 在 **SMTP主機**，設定電子郵件服務。

1. 单击“**保存**”。

#### 設定DSC服務 {#configure-the-dsc-service}

若要使用Correspondence Management API，請下載DSCSample.jar （在本檔案中附加為components.zip的一部分）並將其上傳至LiveCycle伺服器。 將DSCSample.jar檔案上傳至LiveCycle伺服器後，Experience Manager伺服器會使用DSCSample.jar檔案來存取renderLetter API。

如需詳細資訊，請參閱 [將AEM Forms與AdobeLiveCycle連線](/help/forms/using/aem-livecycle-connector.md).

1. 在DSCSample.jar中更新cmsa.properties中的Experience Manager伺服器URL，該URL位於以下位置：

   DSCSample.jar\com\adobe\livecycle\cmsa.properties

1. 在組態檔中提供下列引數：

   * **crx.serverUrl**=https:/host:port/[內容路徑]/[AEM URL]
   * **crx.username**=Experience Manager使用者名稱
   * **crx.password**=Experience Manager密碼
   * **crx.appRoot**=/content/apps/cm

   >[!NOTE]
   >
   >每次在伺服器端進行變更時，請重新啟動LiveCycle伺服器。

   DSCSample.jar檔案使用renderLetter API。 如需renderLetter API的詳細資訊，請參閱 [介面LetterRenderService](https://www.adobe.io/experience-manager/reference-materials/6-5/forms/javadocs/index.html?com/adobe/icc/ddg/api/LetterRenderService.html).

#### 將DSC匯入LiveCycle {#import-dsc-to-livecyle}

DSCSample.jar檔案使用renderLetter API從DSC提供作為輸入的XML資料將字母轉譯為PDF位元組。 如需renderLetter和其他API的詳細資訊，請參閱 [信件轉譯服務](https://www.adobe.io/experience-manager/reference-materials/6-5/forms/javadocs/index.html?com/adobe/icc/ddg/api/LetterRenderService.html).

1. 啟動Workbench並登入。
1. 選取 **「視窗>顯示檢視>元件」**. 「元件」檢視會新增至Workbench ES2。

1. 按一下右鍵 **元件** 並選取 **安裝元件**.

1. 選取 **DSCSample.jar** 檔案瀏覽器的檔案，然後按一下 **開啟**.
1. 按一下右鍵 **RenderWrapper** 並選取 **啟動元件**. 如果元件啟動，元件名稱旁會出現綠色箭頭。

## 傳送信件以供檢閱 {#send-letter-for-review}

設定好傳送信件以供稽核的動作和按鈕後：

1. 清除瀏覽器快取。

1. 在建立通訊UI中，按一下 **信件評論** 和指定稽核者的電子郵件ID。

1. 按一下 **提交**.

![sendreview](assets/sendreview.png)

稽核者會收到來自系統的電子郵件，其中包含字母作為PDF附件。
