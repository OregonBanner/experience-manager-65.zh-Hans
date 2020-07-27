---
title: 将自定义操作添加到资产列表视图
seo-title: 将自定义操作添加到资产列表视图
description: 本文讲授如何将自定义操作添加到资产列表视图
seo-description: 本文讲授如何将自定义操作添加到资产列表视图
uuid: 45f25cfb-f08f-42c6-99c5-01900dd8cdee
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 6378ae30-a351-49f7-8e9a-f0bd4287b9d3
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1381'
ht-degree: 2%

---


# 将自定义操作添加到资产列表视图{#add-custom-action-to-the-asset-listing-view}

## 概述 {#overview}

Corresponce Management解决方案允许您向“管理资产”用户界面添加自定义操作。

您可以为以下项向资产列表视图添加自定义操作：

* 一个或多个资产类型或字母
* 在选择单个、多个资产／字母或不选择时执行（操作／命令变为活动状态）

此自定义通过向字母的资产列表视图添加“下载平面PDF”命令的方案进行演示。 此自定义方案允许用户下载单个选定字母的平面PDF。

### 前提条件 {#prerequisites}

要完成以下或类似方案，您需要了解：

* CRX
* JavaScript
* Java

## 方案： 向字母列表用户界面添加命令以下载简单的字母PDF版本 {#addcommandtoletters}

以下步骤将“下载简单PDF”命令添加到字母的资产列表视图，并允许用户下载所选字母的简单PDF。 使用这些步骤和相应的代码和参数，您可以为其他资产添加一些其他功能，如数据字典或文本。

要自定义“通信管理”以允许用户下载简单的PDF字母，请完成以下步骤：

1. 转到并 `https://'[server]:[port]'/[ContextPath]/crx/de` 以管理员身份登录。

1. 在apps文件夹中，使用以下步骤创建一个名为items的文件夹，其路径／结构与选择文件夹中的items文件夹类似：

   1. 右键单击以下路 **径的** “项目”文件夹，然后选择“ **叠加节点”**:

      `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/body/content/header/items/selection/items`

      >[!NOTE]
      >
      >此路径专门用于创建与选择多个资源／字母之一配合的操作。 如果要创建不进行选择的操作，您需要为以下路径创建一个叠加节点，然后相应地完成其余步骤：
      >
      >
      >`/libs/fd/cm/ma/gui/content/cmassets/jcr:content/body/content/header/items/default/items`

      ![创建节点](assets/1_itemscreatenode.png)

   1. 确保“叠加节点”对话框具有以下值：

      **路径：** /libs/fd/cm/ma/gui/content/cmassets/jcr:content/body/content/header/items/selection/items

      **位置：** /apps/

      **匹配节点类型：** 已选择

      ![叠加节点](assets/2_createnodedownloadflatpdf.png)

   1. 单击&#x200B;**确定**。文件夹结构将在应用程序文件夹中创建。

      单击“ **全部保存**”。

1. 在新创建的项目文件夹下，为特定资产中的自定义按钮／操作添加一个节点(示例： 下载FlatPDF)，步骤如下：

   1. 右键单击项目文 **件夹** ，然后选择 **“创建** ” **>“**&#x200B;创建节点”。

   1. 确保“创建节点”对话框具有以下值，然后单击“确 **定”**:

      **名称：** downloadFlatPDF（或要为此属性指定的名称）

      **类型：** nt：非结构化

   1. 单击您创建的新节点（此处为downloadFlatPDF）。 CRX显示节点的属性。

   1. 将以下属性添加到节点（此处为downloadFlatPDF），然后单击“全 **部保存**”:

      <table>
        <tbody>
        <tr>
        <td><strong>名称</strong></td>
        <td><strong>类型</strong></td>
        <td><strong>值和说明</strong></td>
        </tr>
        <tr>
        <td>class</td>
        <td>字符串</td>
        <td>foundation-collection-action</td>
        </tr>
        <tr>
        <td>foundation-collection-action</td>
        <td>字符串</td>
        <td><p>{"目标": "。cq-manageasset-admin-childpages", "activeSelectionCount": "single","type": “LETTER”<br /> }ActiveSelectionCount <br /><br /><strong></strong> 可以是单个或多个，以允许对执行自定义操作的单个或多个资产进行选择。</p> <p><strong>类型</strong> 可以是以下一个或多个（逗号分隔多个条目）: 字母、文本、列表、条件、自动词</p> </td>
        </tr>
        <tr>
        <td>图标</td>
        <td>字符串</td>
        <td>icon-download<br /><br /> Commanagement在命令／菜单左侧显示的图标。 有关可用的不同图标和设置，请参 <a href="https://docs.adobe.com/docs/en/aem/6-3/develop/ref/coral-ui/coralui3/Coral.Icon.html" target="_blank">阅CoralUI图标文档</a>。<br /> </td>
        </tr>
        <tr>
        <td>jcr:primaryType</td>
        <td>名称</td>
        <td>nt:unstructured</td>
        </tr>
        <tr>
        <td>rel</td>
        <td>字符串</td>
        <td>下载-flat-pdf-button</td>
        </tr>
        <tr>
        <td>sling:resourceType</td>
        <td>字符串</td>
        <td>granite/ui/components/endor/actionbar/button</td>
        </tr>
        <tr>
        <td>文本</td>
        <td>字符串</td>
        <td>下载简单PDF(或任何其他标签<br /> )资产列表 <br /> 界面中显示的命令</td>
        </tr>
        <tr>
        <td>页面</td>
        <td>字符串</td>
        <td>下载所选字母的平面PDF(或任何其他标签/Alt文本<br /> )。标题是 <br /> Corresponce Management在用户悬停在自定义命令上时显示的替代文本。</td>
        </tr>
        </tbody>
       </table>

1. 在apps文件夹中，使用以下步骤创建一个名为js的文件夹，其路径／结构与管理文件夹中的项目文件夹类似：

   1. 右键单击以 **下路径** 的js文件夹，然后选择 **叠加节点**:

      `/libs/fd/cm/ma/gui/components/admin/clientlibs/admin/js`

   1. 确保“叠加节点”对话框具有以下值：

      **路径：** /libs/fd/cm/ma/gui/components/admin/clientlibs/admin/js

      **位置：** /apps/

      **匹配节点类型：** 已选择

   1. 单击&#x200B;**确定**。文件夹结构将在应用程序文件夹中创建。 单击“ **全部保存**”。

1. 在js文件夹中，使用用于按钮操作处理的代码使用以下步骤创建一个名为formaction.js的文件：

   1. 右键单击以下路 **径的** js文件夹，然后选择 **创建>创建文件**:

      `/apps/fd/cm/ma/gui/components/admin/clientlibs/admin/js`

      将文件命名为formaction.js。

   1. 多次-单击文件以在CRX中打开它。
   1. 在formaction.js文件（/apps分支下）中，从位于以下位置的formaction.js文件复制代码：

      `/libs/fd/cm/ma/gui/components/admin/clientlibs/admin/js/formaction.js`

      然后，在formaction.js文件（/apps分支下）的末尾附加以下代码，并单击“全部 **保存**:

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

      此步骤中添加的代码将覆盖libs文件夹下的代码，因此将之前的代码复制到/apps分支中的formaction.js文件。 将代码从/libs分支复制到/apps分支可确保以前的功能也能正常工作。

      上述代码用于对此过程中创建的命令执行字母特定的操作处理。 要对其他资源执行操作，请修改JavaScript代码。

1. 在apps文件夹中，使用以下步骤创建一个名为items的文件夹，其路径／结构与actionhandlers文件夹中的items文件夹类似：

   1. 右键单击以下路 **径的** “项目”文件夹，然后选择“ **叠加节点”**:

      `/libs/fd/cm/ma/gui/content/commons/actionhandlers/items/`

   1. 确保“叠加节点”对话框具有以下值：

      **路径：** /libs/fd/cm/ma/gui/content/commons/actionhandlers/items/

      **位置：** /apps/

      **匹配节点类型：** 已选择

   1. 单击&#x200B;**确定**。文件夹结构将在应用程序文件夹中创建。

   1. 单击“ **全部保存**”。

1. 在新创建的项目节点下，为特定资产中的自定义按钮／操作添加一个节点(示例： letterpdfdownloader)。

   1. 右键单击项目文件夹，然后选择“ **创建”>“创建节点**”。

   1. 确保“创建节点”对话框具有以下值，然后单击“确 **定”**:

      **名称：** letterpdfdownloader（或要为此属性指定的名称）必须是唯一的。 如果在此处使用其他名称，也可在formaction.js文件的ACTION_URL变量中指定相同的名称。)

      **类型：** nt：非结构化

   1. 单击您创建的新节点（此处为downloadFlatPDF）。 CRX显示节点的属性。

   1. 将以下属性添加到节点（此处为letterpdfdownloader），然后单击“全 **部保存**”:

      | **名称** | **类型** | **值** |
      |---|---|---|
      | sling:resourceType | 字符串 | fd/cm/ma/gui/components/admin/clientlibs/admin |

1. 在以下位置使用命令的操作处理代码创建名为POST.jsp的文件：

   /apps/fd/cm/ma/gui/components/admin/clientlibs/admin

   1. 右键单击以下路 **径的** admin文件夹，然后选择 **创建>创建文件**:

      /apps/fd/cm/ma/gui/components/admin/clientlibs/admin

      将文件命名为POST.jsp。 （文件名只需为POST.jsp。）

   1. 多次单 **击POST.jsp** 文件，在CRX中打开它。
   1. 将以下代码添加到POST.jsp文件，然后单击“全 **部保存**”:

      此代码特定于字母渲染服务。 对于任何其他资源，请将该资源的java库添加到此代码中。 有关AEM FormsAPI的详细信息，请参阅 [AEM FormsAPI](https://adobe.com/go/learn_aemforms_javadocs_63_en)。

      有关AEM库的更多信息，请参阅AEM [组件](/help/sites-developing/components.md)。

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

## 使用自定义功能下载简单的字母PDF {#download-flat-pdf-of-a-letter-using-the-custom-functionality}

添加自定义功能下载字母的平面PDF后，您可以使用以下步骤下载所选字母的平面PDF版本：

1. 转到 `https://'[server]:[port]'/[ContextPath]/projects.html` 并登录。

1. 选择“ **表单”>“字母**”。 通信管理列表系统中可用的信函。
1. 单击 **选择** ，然后单击字母将其选中。
1. 选择 **更多** > **&lt;下载平面PDF>** （使用本文中的说明创建的自定义功能）。 将显示“将信函下载为PDF”对话框。

   菜单项名称、功能和替代文本根据在方案中创建的自定义 [进行： 向字母列表用户界面添加一个命令，以下载简单的字母PDF版本。](#addcommandtoletters)

   ![自定义功能： 下载简单PDF](assets/5_downloadflatpdf.png)

1. 在“以PDF形式下载信函”对话框中，选择要从中填充PDF中数据的相关XML。

   >[!NOTE]
   >
   >在将字母下载为平面PDF之前，您可以使用“创建报告”选项创建包含字母中数据 **的XML** 文件。

   ![将信件下载为PDF](assets/6_downloadflatpdf.png)

   该信件将作为平面PDF下载到您的计算机。

