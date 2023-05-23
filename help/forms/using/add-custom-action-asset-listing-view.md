---
title: 新增自訂動作至資產清單檢視
seo-title: Add custom action to the Asset Listing view
description: 本文會教導如何將自訂動作新增至資產清單檢視
seo-description: This article teaches how to add custom action to the Asset Listing view
uuid: 45f25cfb-f08f-42c6-99c5-01900dd8cdee
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 6378ae30-a351-49f7-8e9a-f0bd4287b9d3
docset: aem65
feature: Correspondence Management
exl-id: bf6d3edb-6bf7-4d3e-b042-d75cb8e39e3f
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: tm+mt
source-wordcount: '1355'
ht-degree: 3%

---

# 新增自訂動作至資產清單檢視{#add-custom-action-to-the-asset-listing-view}

## 概述 {#overview}

通訊管理解決方案可讓您將自訂動作新增到「管理資產」使用者介面。

您可以將自訂動作新增至資產清單檢視，以執行下列動作：

* 一或多個資產型別或字母
* 選取單一、多個資產/字母或不選取時，執行（動作/命令變為使用中）

此自訂可透過在「資產清單」檢視中新增命令「下載平面PDF」的案例來示範。 此自訂案例可讓您的使用者下載單一選取字母的平面PDF。

### 前提条件 {#prerequisites}

若要完成下列案例或類似案例，您需要具備以下知識：

* CRX
* JavaScript
* Java™

## 情節：將命令新增至字母清單使用者介面，以下載字母的平面PDF版本 {#addcommandtoletters}

下列步驟會將「下載平面PDF」命令新增至字母的資產清單檢視，並允許使用者下載所選字母的平面PDF。 將這些步驟與適當的程式碼和引數搭配使用，您可以為不同資產新增一些其他功能，例如資料字典或文字。

若要自訂「通訊管理」，讓您的使用者下載平面信件PDF，請完成下列步驟：

1. 前往 `https://'[server]:[port]'/[ContextPath]/crx/de` 並以管理員身分登入。

1. 在apps資料夾中，使用下列步驟建立名為items的資料夾，其路徑/結構類似於selection資料夾中的items資料夾：

   1. 以滑鼠右鍵按一下 **個專案** 資料夾並選取 **覆蓋節點**：

      `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/body/content/header/items/selection/items`

      >[!NOTE]
      >
      >此路徑專用於建立可搭配選取一個或多個資產/字母的動作使用。 如果您想要建立不需選取即可運作的動作，請改為為以下路徑建立覆蓋節點，並據此完成其餘步驟：
      >
      >
      >`/libs/fd/cm/ma/gui/content/cmassets/jcr:content/body/content/header/items/default/items`

      ![建立節點](assets/1_itemscreatenode.png)

   1. 確定「覆蓋節點」對話方塊具有下列值：

      **路徑：** /libs/fd/cm/ma/gui/content/cmassets/jcr：content/body/content/header/items/selection/items

      **位置：** /apps/

      **符合節點型別：** 已選取

      ![覆蓋節點](assets/2_createnodedownloadflatpdf.png)

   1. 单击&#x200B;**确定**。資料夾結構會在apps資料夾中建立。

      按一下 **全部儲存**.

1. 在新建立的專案資料夾下，使用下列步驟在特定資產中新增自訂按鈕/動作的節點（例如：downloadFlatPDF）：

   1. 以滑鼠右鍵按一下 **個專案** 資料夾並選取 **建立** > **建立節點**.

   1. 確定「建立節點」對話方塊具有下列值，然後按一下 **確定**：

      **名稱：** downloadFlatPDF （或您要為此屬性指定的名稱）

      **型別：** nt：unstructured

   1. 按一下您已建立的新節點（此處downloadFlatPDF）。 CRX會顯示節點的屬性。

   1. 將下列屬性新增至節點（此處downloadFlatPDF），然後按一下 **全部儲存**：

      <table>
        <tbody>
        <tr>
        <td><strong>名称</strong></td>
        <td><strong>类型</strong></td>
        <td><strong>价值 和說明</strong></td>
        </tr>
        <tr>
        <td>class</td>
        <td>字符串</td>
        <td>foundation-collection-action</td>
        </tr>
        <tr>
        <td>foundation-collection-action</td>
        <td>字符串</td>
        <td><p>{"target"： "。cq-manageasset-admin-childpages"， "activeSelectionCount"： "single"，"type"： "LETTER"}<br /> <br /> <br /> <strong>activeSelectionCount</strong> 可以是單一或多個，以允許選擇執行自訂動作的單一或多個資產。</p> <p><strong>type</strong> 可以是下列其中一或多個（以逗號分隔多個專案）： LETTER、TEXT、LIST、CONDITION、DATADICTIONARY</p> </td>
        </tr>
        <tr>
        <td>图标</td>
        <td>字符串</td>
        <td>圖示 — 下載<br /> <br /> 「通訊管理」顯示在指令/選單左側的圖示。 如需可用的不同圖示和設定，請參閱 <a href="https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hans" target="_blank">CoralUI圖示檔案</a>.<br /> </td>
        </tr>
        <tr>
        <td>jcr:primaryType</td>
        <td>名称</td>
        <td>nt:unstructured</td>
        </tr>
        <tr>
        <td>rel</td>
        <td>字符串</td>
        <td>download-flat-pdf-button</td>
        </tr>
        <tr>
        <td>sling:resourceType</td>
        <td>字符串</td>
        <td>granite/ui/components/endor/actionbar/button</td>
        </tr>
        <tr>
        <td>text</td>
        <td>字符串</td>
        <td>下載一般PDF（或任何其他標籤）<br /> <br /> 顯示在「資產清單」介面中的命令</td>
        </tr>
        <tr>
        <td>标题</td>
        <td>字符串</td>
        <td>下載選取字母的平面PDF（或任何其他標籤/替代文字）<br /> <br /> 標題是當使用者將滑鼠懸停在自訂命令上時，「通訊管理」顯示的替代文字。</td>
        </tr>
        </tbody>
       </table>

1. 在apps資料夾中，使用下列步驟建立名為js的資料夾，其路徑/結構類似於admin資料夾中的items資料夾：

   1. 以滑鼠右鍵按一下 **js** 資料夾並選取 **覆蓋節點**：

      `/libs/fd/cm/ma/gui/components/admin/clientlibs/admin/js`

   1. 確定「覆蓋節點」對話方塊具有下列值：

      **路徑：** /libs/fd/cm/ma/gui/components/admin/clientlibs/admin/js

      **位置：** /apps/

      **符合節點型別：** 已選取

   1. 单击&#x200B;**确定**。資料夾結構會在apps資料夾中建立。 按一下 **全部儲存**.

1. 在js資料夾中，建立名為formaction.js的檔案，其中包含按鈕的動作處理程式碼，使用下列步驟：

   1. 以滑鼠右鍵按一下 **js** 資料夾並選取 **「建立」>「建立檔案」**：

      `/apps/fd/cm/ma/gui/components/admin/clientlibs/admin/js`

      將檔案命名為formaction.js。

   1. 連按兩下檔案以在CRX中開啟。
   1. 在formaction.js檔案（在/apps分支下）中，從位於以下位置的formaction.js檔案復製程式碼：

      `/libs/fd/cm/ma/gui/components/admin/clientlibs/admin/js/formaction.js`

      然後將下列程式碼附加至formaction.js檔案的結尾（在/apps分支下），然後按一下 **全部儲存**：

      ```javascript
      /* Action url for xml file to be added.*/
      var ACTION_URL = "/apps/fd/cm/ma/gui/content/commons/actionhandlers/items/letterpdfdownloader.html";
      
      /* File upload handling*/
      var fileSelectedHandler = function(e){
          if(e && e.target && e.target.value)
              $(".downloadLetterPDFBtn").removeAttr('disabled');
          else
              $(".downloadLetterPDFBtn").attr('disabled','disabled');
      }
      
      /*Handing of Download button in pop up.*/
      var downloadClickHandler = function(){
          $('#downloadLetterPDFDilaog').modal("hide");
          var element = $('.foundation-selections-item');
          var path = $(element).data("path");
          $("#fileUploadForm").attr('action', ACTION_URL + "?letterId="+path).submit();
      }
      
      /*Click handling on action button.*/
      $(document).on("click",'.download-flat-pdf-button',function(e){
          $("#uploadSamepledata").val("");
           if($('#downloadLetterPDFDilaog').length == 0){
              $(document).on("click",".downloadLetterPDFBtn",downloadClickHandler);
              $(document).on("change","#uploadSamepledata",fileSelectedHandler);
              $("body").append(downloadLetterPDFDilaog);
          }
            $('#downloadLetterPDFDilaog').modal("show");
      });
      
      /*Download popup.*/
      var downloadLetterPDFDilaog = '<div id="downloadLetterPDFDilaog" class="coral-Modal notice " role="dialog"  aria-hidden="true">'+
          '<form id="fileUploadForm" method="POST" enctype="multipart/form-data">'+
              '<div class="coral-Modal-header">'+
                  '<h2 class="coral-Modal-title coral-Heading coral-Heading--2" id="modal-header1443020790107-label" tabindex="0">Download Letter as PDF.</h2>'+
                  '<button type="button" class="coral-MinimalButton coral-Modal-closeButton" data-dismiss="modal">×</button>'+
              '</div>'+
              '<div class="coral-Modal-body" id="modal-header1443020790107-message" role="document" tabindex="0">'+
                  '<div class="coral-Modal-message">'+
                      '<p></p>'+
                  '</div>'+
                  '<div class="coral-Modal-uploader">'+
                      '<p>Select sample data for letter.</p>'+
                      '<input type="file" id="uploadSamepledata" name="file" accept=".xml" size="70px">'+
                  '</div>'+
              '</div>'+
           '</form>'+
              '<div class="coral-Modal-footer">'+
                  '<button type="button" class="coral-Button" data-dismiss="modal">Cancel</button>'+
                  '<button type="button" class="coral-Button coral-Button--primary downloadLetterPDFBtn" disabled="disabled">Download</button>'+
              '</div>'+
      '</div>';
      ```

      您在此步驟中新增的程式碼會覆寫libs資料夾下的程式碼，因此請將先前的程式碼複製到/apps分支中的formaction.js檔案。 將程式碼從/libs分支複製到/apps分支，可確保先前的功能也能運作。

      上述程式碼適用於此程式中建立之指令的字母特定動作處理。 如需其他資產的動作處理，請修改JavaScript程式碼。

1. 在apps資料夾中，使用下列步驟建立名為items的資料夾，其路徑/結構類似於actionhandlers資料夾中的items資料夾：

   1. 以滑鼠右鍵按一下 **個專案** 資料夾並選取 **覆蓋節點**：

      `/libs/fd/cm/ma/gui/content/commons/actionhandlers/items/`

   1. 確定「覆蓋節點」對話方塊具有下列值：

      **路徑：** /libs/fd/cm/ma/gui/content/commons/actionhandlers/items/

      **位置：** /apps/

      **符合節點型別：** 已選取

   1. 单击&#x200B;**确定**。資料夾結構會在apps資料夾中建立。

   1. 按一下 **全部儲存**.

1. 在新建立的專案節點下，使用下列步驟為特定資產（例如：letterpdfdownloader）中的自訂按鈕/動作新增節點：

   1. 以滑鼠右鍵按一下專案資料夾並選取 **建立>建立節點**.

   1. 確定「建立節點」對話方塊具有下列值，然後按一下 **確定**：

      **名稱：** letterpdfdownloader (或您要指定給此屬性的名稱 — 必須是唯一的。 如果您在此處使用不同的名稱，請在formaction.js檔案的ACTION_URL變數中指定相同的名稱。)

      **型別：** nt：unstructured

   1. 按一下您已建立的新節點（此處downloadFlatPDF）。 CRX會顯示節點的屬性。

   1. 將下列屬性新增至節點（此處為letterpdfdownloader），然後按一下 **全部儲存**：

      | **名称** | **类型** | **值** |
      |---|---|---|
      | sling:resourceType | 字符串 | fd/cm/ma/gui/components/admin/clientlibs/admin |

1. 在下列位置使用命令的動作處理程式碼，建立名為POST.jsp的檔案：

   /apps/fd/cm/ma/gui/components/admin/clientlibs/admin

   1. 以滑鼠右鍵按一下 **管理員** 資料夾並選取 **「建立」>「建立檔案」**：

      /apps/fd/cm/ma/gui/components/admin/clientlibs/admin

      將檔案命名為POST.jsp。 (檔案名稱只能是POST.jsp。)

   1. 連按兩下 **POST.jsp** 檔案以在CRX中開啟。
   1. 將下列程式碼新增至POST.jsp檔案，然後按一下 **全部儲存**：

      此程式碼專用於信件轉譯服務。 對於任何其他資產，請將該資產的Java™程式庫新增至此程式碼。 如需AEM Forms API的詳細資訊，請參閱 [AEM FORMS API](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hans).

      如需AEM資料庫的詳細資訊，請參閱AEM [元件](/help/sites-developing/components.md).

      ```xml
      /*Import libraries. Here we are downloading letter flat pdf with input xml data so we require letterRender Api. For any other Module functionality we need to first import that library. */
      <%@include file="/libs/foundation/global.jsp"%>
      <!DOCTYPE html lang="en" PUBLIC "-//W3C//DTD XHTML 1.1//EN" "https://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
      <%@page import="com.adobe.icc.ddg.api.*"%>
      <%@page import="com.adobe.icc.dbforms.obj.*"%>
      <%@page import="com.adobe.icc.render.obj.*" %>
      <%@page import="com.adobe.icc.services.api.*" %>
      <%@page import="org.apache.sling.api.resource.*" %>
      <%@page import="java.io.File" %>
      <%@page import="java.util.*" %>
      <%@page import="com.adobe.livecycle.content.appcontext.AppContextManager"%>
      <%@page import=" com.adobe.icc.dbforms.exceptions.ICCException"%>
      <%@page import="java.io.InputStream" %>
      <%@page import="java.io.FileInputStream" %>
      <%@page import="org.apache.commons.io.IOUtils" %>
      <%@page session="false" contentType="text/html; charset=utf-8"%>
      <%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0"%>
      <%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %>
       <%@page session="false" contentType="text/html; charset=utf-8"%>
      <%
         AppContextManager.setCurrentAppContext("/content/apps/cm");
         /*Get letter id sent in js file.*/
          String letterId = request.getParameter("letterId");
          if(letterId.lastIndexOf("?") != -1)
              letterId = letterId.substring(0, letterId.indexOf("?"));
          String fileName = null;
          String letterName = null;
          InputStream inputStream = null;
          /*Get xml file data*/
          if (slingRequest.getRequestParameter("file") != null)
              inputStream = slingRequest.getRequestParameter("file").getInputStream();
          if(letterId != null){
              String xmlData = null;
              try{
                  xmlData = IOUtils.toString(inputStream, "UTF-8");
              }
              catch (Exception e) {
                  log.error("Xml data does not exists.");
              }
              /*letter Name from letter letter id.*/
              letterName = letterId.substring(letterId.lastIndexOf("/")+1);
              /*Invoking letter render services API.*/
              LetterRenderService letterRenderService = sling.getService(LetterRenderService.class);
              /*using CM renderLetter api to get pdfbytes.*/
              PDFResponseType  pdfResponseType= letterRenderService.renderLetter(letterId,xmlData,true,false,false,false);
              byte[] bytes = null;
              /*Downloading pdf bytes as pdf.*/
              if(pdfResponseType != null && pdfResponseType.getFile() != null){
                  bytes = pdfResponseType.getFile().getDocument();
                  /*set the response header to enable download*/
                  response.setContentType("application/OCTET-STREAM");
                  response.setHeader("Content-Disposition", "attachment;filename=\"" + letterName + ".pdf\"");
                  response.setHeader("Pragma", "cache");
                  response.setHeader("Cache-Control", "private");
                  out.clear();
                  response.getOutputStream().write(bytes);
              }
          }
          else{
              log.error("Letter id does not exists.");
          }
      %>
      ```

## 使用自訂功能下載字母的平面PDF {#download-flat-pdf-of-a-letter-using-the-custom-functionality}

新增自訂功能下載字母的平面PDF後，您可以使用以下步驟下載所選字母的平面PDF版本：

1. 前往 `https://'[server]:[port]'/[ContextPath]/projects.html` 並登入。

1. 選取 **Forms >字母**. 「通訊管理」會列出系統中可用的信件。
1. 按一下 **選取** 然後按一下字母加以選取。
1. 選取 **更多** > **&lt;download flat=&quot;&quot; pdf=&quot;&quot;>** （使用本文說明建立的自訂功能）。 下載字母為PDF對話方塊出現。

   選單專案名稱、功能和替代文字是根據中建立的自訂內容 [情節：將命令新增至字母清單使用者介面，以下載字母的平面PDF版本。](#addcommandtoletters)

   ![自訂功能：下載一般PDF](assets/5_downloadflatpdf.png)

1. 在「以PDF形式下載信件」對話方塊中，選取要填入PDF中資料的相關XML。

   >[!NOTE]
   >
   >在將信函下載為平面PDF之前，您可以使用 **建立報告** 選項。

   ![將字母下載為PDF](assets/6_downloadflatpdf.png)

   信件會以一般PDF下載到您的電腦。
