---
title: 為最適化表單編寫自訂提交動作
seo-title: Writing custom Submit action for adaptive forms
description: AEM Forms可讓您為最適化表單建立自訂提交動作。 本文介紹為最適化表單新增自訂提交動作的程式。
seo-description: AEM Forms lets you create custom Submit action for Adaptive forms. This article describes the procedure to add custom Submit action for Adaptive forms.
uuid: fd8e1dac-b997-4e86-aaf6-3507edcb3070
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 2a2e1156-4a54-4b0a-981c-d527fe22a27e
docset: aem65
exl-id: 7c3d0dac-4e19-4eb3-a43d-909d526acd55
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: tm+mt
source-wordcount: '1616'
ht-degree: 1%

---

# 為最適化表單編寫自訂提交動作{#writing-custom-submit-action-for-adaptive-forms}

適用性表單需要提交動作來處理使用者指定的資料。 提交動作會決定使用最適化表單提交之資料所執行的工作。 Adobe Experience Manager (AEM)包含 [OOTB提交動作](../../forms/using/configuring-submit-actions.md) 會示範您可使用使用者提交的資料執行的自訂工作。 例如，您可以執行工作，例如傳送電子郵件或儲存資料。

## 提交動作的工作流程 {#workflow-for-a-submit-action}

此流程圖會說明當您按一下 **[!UICONTROL 提交]** 最適化表單中的按鈕。 檔案附件元件中的檔案會上傳至伺服器，而表單資料會以上傳檔案的URL更新。 在使用者端內，資料會以JSON格式儲存。 使用者端傳送Ajax要求至內部servlet，以按摩您指定的資料並以XML格式傳回。 使用者端會使用動作欄位整理此資料。 它會透過「表單提交」動作將資料提交至最終servlet （引導提交servlet）。 然後，此servlet會將控制項轉送給Submit動作。 提交動作可以將請求轉送至不同的Sling資源，或將瀏覽器重新導向至其他URL。

![描述「提交」動作之工作流程的流程圖](assets/diagram1.png)

### XML資料格式 {#xml-data-format}

XML資料會使用以下工具傳送至servlet： **`jcr:data`** 要求引數。 提交動作可以存取引數以處理資料。 下列程式碼說明XML資料的格式。 與表單模型繫結的欄位會出現在 **`afBoundData`** 區段。 未繫結的欄位會出現在 `afUnoundData`區段。 如需格式化的詳細資訊， `data.xml` 檔案，請參閱 [預先填入最適化表單欄位簡介](../../forms/using/prepopulate-adaptive-form-fields.md).

```xml
<?xml ?>
<afData>
<afUnboundData>
<data>
<field1>value</field2>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
</data>
</afUnboundData>
<afBoundData>
<!-- xml corresponding to the Form Model /XML Schema -->
</afBoundData>
</afData>
```

### 動作欄位 {#action-fields}

提交動作可以新增隱藏的輸入欄位(使用HTML [輸入](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Input) 標籤)，以呈現表單HTML。 這些隱藏欄位可包含處理表單提交時所需的值。 提交表單時，這些欄位值會傳回作為請求引數，提交動作可在提交處理期間使用。 輸入欄位稱為動作欄位。

例如，也可擷取填寫表單所用時間的提交動作可以新增隱藏的輸入欄位 `startTime` 和 `endTime`.

指令碼可提供 `startTime` 和 `endTime` 表單轉譯時及表單提交前的欄位。 提交ActionScript `post.jsp` 然後可以使用請求引數存取這些欄位，並計算填寫表單所需的總時間。

### 檔案附件 {#file-attachments}

提交動作也可以使用您使用「檔案附件」元件上載的檔案附件。 提交動作指令碼可使用sling存取這些檔案 [RequestParameter API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html). 此 [isFormField](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#isFormField()) api的方法有助於識別請求引數是檔案還是表單欄位。 您可以在「提交」動作中反複執行「要求」引數，以識別「檔案附件」引數。

下列範常式式碼會識別請求中的檔案附件。 接下來，它會使用 [取得API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#get()). 最後，它會使用資料建立Document物件並將其附加至清單。

```java
RequestParameterMap requestParameterMap = slingRequest.getRequestParameterMap();
for (Map.Entry<String, RequestParameter[]> param : requestParameterMap.entrySet()) {
    RequestParameter rpm = param.getValue()[0];
    if(!rpm.isFormField()) {
        fileAttachments.add(new Document(rpm.get()));
    }
}
```

### 轉送路徑和重新導向URL {#forward-path-and-redirect-url}

執行必要的動作後，Submit servlet會將要求轉送至轉送路徑。 動作會使用setForwardPath API在指南提交servlet中設定轉送路徑。

如果動作未提供轉送路徑，則提交servlet會使用重新導向URL重新導向瀏覽器。 作者會使用「最適化表單編輯」對話方塊中的「感謝您」頁面設定，來設定重新導向URL。 您也可以透過提交動作或指南提交servlet中的setRedirectUrl API來設定重新導向URL。 您也可以使用指南提交servlet中的setRedirectParameters API，設定傳送至重新導向URL的要求引數。

>[!NOTE]
>
>作者會提供重新導向URL （使用感謝頁面設定）。 [OOTB提交動作](../../forms/using/configuring-submit-actions.md) 使用重新導向URL可從轉送路徑參照的資源重新導向瀏覽器。
>
>您可以編寫自訂提交動作，將請求轉發到資源或servlet。 Adobe建議在處理完成時，為轉送路徑執行資源處理的指令碼，將要求重新導向至重新導向URL。

## 提交操作 {#submit-action}

提交動作是sling：Folder，包括下列專案：

* **addfields.jsp**：此指令碼提供在轉譯期間新增至HTML檔案的動作欄位。 使用此指令碼，在post.post.jsp.jsp指令碼中新增提交期間所需的隱藏POST引數。
* **dialog.xml**：此指令碼類似於CQ元件對話方塊。 它提供作者自訂的設定資訊。 當您選取「提交」動作時，欄位會顯示在「最適化表單編輯」對話方塊的「提交動作」標籤中。
* **post.POST.jsp**：提交servlet會呼叫此指令碼，其中包含您提交的資料以及先前章節中的其他資料。 在此頁面中只要提到執行動作，就表示要執行post.POST.jsp指令碼。 若要以最適化表單註冊提交動作以顯示於最適化表單編輯對話方塊，請將這些屬性新增至Sling:Folder:

   * **guideComponentType** 字串和值的型別 **fd/af/components/guidesubmittype**
   * **guideDataModel** 字串型別，指定適用於提交動作的最適化表單型別。 **xfa** 支援XFA型最適化表單，但 **xsd** 支援以XSD為基礎的最適化表單。 **基本** 不使用XDP或XSD的最適化表單支援。 若要顯示多種最適化表單型別的動作，請新增對應的字串。 以逗號分隔每個字串。 例如，若要讓動作顯示在XFA和XSD型最適化表單上，請指定值 **xfa** 和 **xsd** （分別）。

   * **jcr：description** 型別字串的。 此屬性的值會顯示在「最適化表單編輯」對話方塊之「提交動作」索引標籤的「提交」動作清單中。 OOTB動作會存在該位置的CRX存放庫中 **/libs/fd/af/components/guidesubmittype**.

## 建立自訂提交動作 {#creating-a-custom-submit-action}

執行以下步驟來建立自訂提交動作，將資料儲存到CRX存放庫中，然後傳送電子郵件給您。 最適化表單包含OOTB提交動作存放區內容（已棄用），可將資料儲存於CRX存放庫。 此外，CQ還提供 [郵件](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hans) 可用於傳送電子郵件的API。 使用Mail API之前， [設定](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hans&amp;wcmmode=disabled) Day CQ Mail服務透過系統主控台。 您可以重複使用「存放區內容（已棄用）」動作，將資料儲存在存放庫中。 存放區內容（已棄用）動作可在CRX存放庫中的/libs/fd/af/components/guidesubmittype/store位置使用。

1. 在URL https://登入CRXDE Lite&lt;server>：&lt;port>/crx/de/index.jsp. 在/apps/custom_submit_action資料夾中建立具有sling：Folder屬性並命名為store_and_mail的節點。 建立custom_submit_action資料夾（如果尚未存在）。

   ![描述使用屬性sling：Folder建立節點的熒幕擷圖](assets/step1.png)

1. **提供必要設定欄位。**

   新增存放區動作所需的設定。 複製 **cq：dialog** /libs/fd/af/components/guidesubmittype/store中的存放區動作節點，可移至/apps/custom_submit_action/store_and_email中的動作資料夾。

   ![顯示對話方塊節點複製到動作資料夾的熒幕擷圖](assets/step2.png)

1. **提供設定欄位以提示作者進行電子郵件設定。**

   最適化表單還提供電子郵件動作，可向使用者傳送電子郵件。 根據您的需求自訂此動作。 導覽至/libs/fd/af/components/guidesubmittype/email/dialog。 將cq：dialog節點內的節點複製到提交動作(/apps/custom_submit_action/store_and_email/dialog)的cq：dialog節點。

   ![自訂電子郵件動作](assets/step3.png)

1. **在「最適化表單編輯」對話方塊中讓動作可用。**

   在store_and_email節點中新增下列屬性：

   * **guideComponentType** 型別 **字串** 和值 **fd/af/components/guidesubmittype**

   * **guideDataModel** 型別 **字串** 和值 **xfa， xsd，基本**

   * **jcr：description** 型別 **字串** 和值 **存放區與電子郵件動作**

1. 開啟任何最適化表單。 按一下 **編輯** 按鈕旁邊 **開始** 以開啟 **編輯** 最適化表單容器的對話方塊。 新動作會顯示在 **提交動作** 標籤。 選取 **存放區與電子郵件動作** 顯示新增至對話方塊節點的設定。

   ![提交動作設定對話方塊](assets/store_and_email_submit_action_dialog.jpg)

1. **使用動作完成任務。**

   將post.post.jsp.jspPOST碼新增至您的動作。 (/apps/custom_submit_action/store_and_mail/)。

   執行OOTB存放區動作(post.POST.jsp指令碼)。 使用 [FormsHelper.runAction](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hans)(java.lang.String、java.lang.String、org.apache.sling.api.resource.Resource、org.apache.sling.api.SlingHttpServletRequest、org.apache.sling.api.SlingHttpServletResponse) API，CQ會在您的程式碼中提供，以執行存放區動作。 在JSP檔案中新增下列程式碼：

   `FormsHelper.runAction("/libs/fd/af/components/guidesubmittype/store", "post", resource, slingRequest, slingResponse);`

   若要傳送電子郵件，程式碼會從設定中讀取收件者的電子郵件地址。 若要在動作的指令碼中擷取設定值，請使用下列程式碼讀取目前資源的屬性。 同樣地，您也可以讀取其他組態檔。

   `ValueMap properties = ResourceUtil.getValueMap(resource);`

   `String mailTo = properties.get("mailTo");`

   最後，使用CQ Mail API傳送電子郵件。 使用 [Simpleemail](https://commons.apache.org/proper/commons-email/apidocs/org/apache/commons/mail/SimpleEmail.html) 類別以建立電子郵件物件，如下所述：

   >[!NOTE]
   >
   >請確定JSP檔案的名稱為post.POST.jsp。

   ```java
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <%@page import="com.day.cq.wcm.foundation.forms.FormsHelper,
          org.apache.sling.api.resource.ResourceUtil,
          org.apache.sling.api.resource.ValueMap,
                   com.day.cq.mailer.MessageGatewayService,
     com.day.cq.mailer.MessageGateway,
     org.apache.commons.mail.Email,
                   org.apache.commons.mail.SimpleEmail" %>
   <%@taglib prefix="sling"
                   uri="https://sling.apache.org/taglibs/sling/1.0" %>
   <%@taglib prefix="cq"
                   uri="https://www.day.com/taglibs/cq/1.0"
   %>
   <cq:defineObjects/>
   <sling:defineObjects/>
   <%
           String storeContent =
                       "/libs/fd/af/components/guidesubmittype/store";
           FormsHelper.runAction(storeContent, "post", resource,
                                   slingRequest, slingResponse);
    ValueMap props = ResourceUtil.getValueMap(resource);
    Email email = new SimpleEmail();
    String[] mailTo = props.get("mailto", new String[0]);
    email.setFrom((String)props.get("from"));
           for (String toAddr : mailTo) {
               email.addTo(toAddr);
      }
    email.setMsg((String)props.get("template"));
    email.setSubject((String)props.get("subject"));
    MessageGatewayService messageGatewayService =
                       sling.getService(MessageGatewayService.class);
    MessageGateway messageGateway =
                   messageGatewayService.getGateway(SimpleEmail.class);
    messageGateway.send(email);
   %>
   ```

   選取最適化表單中的動作。 動作會傳送電子郵件並儲存資料。
