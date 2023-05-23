---
title: 建立自訂工具列動作
seo-title: Creating a custom toolbar action
description: 表單開發人員可以在AEM Forms中建立最適化表單的自訂工具列動作。 使用自訂動作表單作者，可為使用者提供更多工作流程和選項。
seo-description: Form developers can create custom toolbar actions for adaptive forms in AEM Forms. Using custom actions form authors can provide more workflows and options to their end users.
uuid: cd785cfb-e1bb-4158-be9b-d99e04eccc02
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 4beca23f-dbb0-4e56-8047-93e4f1775418
docset: aem65
exl-id: 17f7f0e1-09d8-45cd-a4f6-0846bdb079b6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---

# 建立自訂工具列動作{#creating-a-custom-toolbar-action}

## 前提条件 {#prerequisite}

在建立自訂工具列動作之前，請先熟悉 [使用使用者端資料庫](/help/sites-developing/clientlibs.md) 和 [使用CRXDE Lite開發](/help/sites-developing/developing-with-crxde-lite.md).

## 什麼是動作 {#what-is-an-action-br}

最適化表單提供工具列，讓表單作者設定一組選項。 這些選項被定義為最適化表單的動作。 按一下面板工具列中的「編輯」按鈕以設定調適型表單支援的動作。

![預設工具列動作](assets/default_toolbar_actions.png)

除了預設提供的動作集之外，您還可以在工具列中建立自訂動作。 例如，您可以新增動作，讓使用者在提交表單前檢閱所有最適化表單欄位。

## 在最適化表單中建立自訂動作的步驟 {#steps}

為了說明自訂工具列動作的建立，以下步驟將指導您建立按鈕，以便終端使用者在提交填寫的表單之前檢視所有最適化表單欄位。

1. 最適化表單支援的所有預設動作都會出現在 `/libs/fd/af/components/actions` 資料夾。 在CRXDE中，複製 `fileattachmentlisting` 節點來源 `/libs/fd/af/components/actions/fileattachmentlisting` 至 `/apps/customaction`.

1. 將節點複製到之後 `apps/customaction` 資料夾，將節點名稱重新命名為 `reviewbeforesubmit`. 此外，請變更 `jcr:title` 和 `jcr:description` 節點的屬性。

   此 `jcr:title` 屬性包含工具列對話方塊中顯示的動作名稱。 此 `jcr:description` 屬性包含當使用者將指標暫留在動作上時顯示的更多資訊。

   ![用於自訂工具列的節點階層](assets/action3.png)

1. 選取 `cq:template` 中的節點 `reviewbeforesubmit` 節點。 請確定 `guideNodeClass` 屬性為 `guideButton` 和變更 `jcr:title` 屬性。
1. 變更中的型別屬性 `cq:Template` 節點。 對於目前的範例，將type屬性變更為button。

   型別值會在元件的產生HTML中新增為CSS類別。 使用者可以使用該CSS類別來設定其動作的樣式。 按鈕、提交、重設和儲存型別值都會提供行動裝置和案頭裝置的預設樣式。

1. 從最適化表單編輯工具列對話方塊中選取自訂動作。 「審閱」按鈕會顯示在面板的工具列中。

   ![自訂動作在工具列中可供使用](assets/custom_action_available_in_toolbar.png) ![顯示自訂建立的工具列動作](assets/action7.png)

1. 若要為「複查」按鈕提供功能，請在init.jsp檔案中新增一些JavaScript和CSS程式碼以及伺服器端程式碼，這些程式碼會出現在內部 `reviewbeforesubmit` 節點。

   在中新增下列程式碼 `init.jsp`.

   ```jsp
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <guide:initializeBean name="guideField" className="com.adobe.aemds.guide.common.GuideButton"/>
   
   <c:if test="${not isEditMode}">
           <cq:includeClientLib categories="reviewsubmitclientlibruntime" />
   </c:if>
   
   <%--- BootStrap Modal Dialog  --------------%>
   <div class="modal fade" id="reviewSubmit" tabindex="-1">
       <div class="modal-dialog">
           <div class="modal-content">
               <div class="modal-header">
                   <h3>Review the Form Fields</h3>
               </div>
               <div class="modal-body">
                   <div class="modal-list">
                       <table class="table table-bordered">
                           <tr class="name">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Name is: </label>
                               </td>
                           </tr>
                           <tr class="pan">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Pan Number is: </label>
                               </td>
                           </tr>
                           <tr class="dob">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Date Of Birth is: </label>
                               </td>
                           </tr>
                           <tr class="80cdeclaration">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Total 80C Declaration Amount is: </label>
                               </td>
                           </tr>
                           <tr class="rentpaid">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Total HRA Amount is: </label>
                               </td>
                           </tr>
                       </table>
                   </div>
               </div><!-- /.modal-body -->
               <div class="modal-footer">
                   <div class="fileAttachmentListingCloseButton col-md-2 col-xs-2 col-sm-2">
                       <button data-dismiss="modal">Close</button>
                   </div>
               </div>
           </div><!-- /.modal-content -->
       </div><!-- /.modal-dialog -->
   </div><!-- /.modal -->
   ```

   將下列程式碼新增至 `ReviewBeforeSubmit.js` 檔案。

   ```javascript
   /*anonymous function to handle show of review before submit view */
   $(function () {
       if($("div.reviewbeforesubmit button[id*=reviewbeforesubmit]").length > 0) {
           $("div.reviewbeforesubmit button[id*=reviewbeforesubmit]").click(function(){
               // Create the options object to be passed to the getElementProperty API
               var options = {},
                   result = [];
               options.somExpressions = [];
               options.propertyName = "value";
               guideBridge.visit(function(model){
                   if(model.name === "name" || model.name === "pan" || model.name === "dateofbirth" || model.name === "total" || model.name === "totalmonthlyrent"){
                           options.somExpressions.push(model.somExpression);
                   }
               }, this);
               result = guideBridge.getElementProperty(options);
   
               $('#reviewSubmit .reviewlabel').each(function(index, item){
                   var data = ((result.data[index] == null) ? "No Data Filled" : result.data[index]);
                   if($(this).next().hasClass("reviewlabelvalue")){
                       $(this).next().html(data);
                   } else {
                       $(this).after($("<td></td>").addClass("reviewlabelvalue col-md-6 active").html(data));
                   }
               });
               // added because in mobile devices it was causing problem of backdrop
               $("#reviewSubmit").appendTo('body');
               $("#reviewSubmit").modal("show");
           });
       }
   });
   ```

   將下列程式碼新增至 `ReviewBeforeSubmit.css` 檔案。

   ```css
   .modal-list .reviewlabel {
       white-space: normal;
       text-align: right;
       padding:2px;
   }
   
   .modal-list .reviewlabelvalue {
       border: #cde0ec 1px solid;
       padding:2px;
   }
   
   /* Adding icon for this action in mobile devices */
   /* This is the glyphicon provided by bootstrap eye-open */
   /* .<type> .iconButton-icon */
   .reviewbeforesubmit .iconButton-icon {
       position: relative;
       top: -8px;
       font-family: 'Glyphicons Halflings';
       font-style: normal;
   }
   
   .reviewbeforesubmit .iconButton-icon:before {
       content: "\e105"
   }
   ```

1. 若要驗證自訂動作的功能，請在預覽模式下開啟最適化表單，然後按一下工具列中的「檢閱」 。

   >[!NOTE]
   >
   >此 `GuideBridge` 程式庫未以編寫模式載入。 因此，此自訂動作無法在編寫模式下運作。

   ![自訂評論按鈕的動作示範](assets/action9.png)

## 範例 {#samples}

以下封存包含內容套件。 此套件包含與上述自訂工具列動作示範相關的最適化表單。

[获取文件](assets/customtoolbaractiondemo.zip)
