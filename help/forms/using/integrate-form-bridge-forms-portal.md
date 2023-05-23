---
title: 針對HTML5表單整合Form Bridge與自訂入口網站
seo-title: Integrating Form Bridge with custom portal for HTML5 forms
description: 您可以使用FormBridge API從HTML頁面取得或設定表單欄位的值，並提交表單。
seo-description: You can use the FormBridge API to get or set the values of form fields from the HTML page and submit the form.
uuid: c8911f82-1a25-47a5-9a06-19b5dce74a2c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bd9bf095-d74d-458c-afe7-fab04050849d
docset: aem65
feature: Mobile Forms
exl-id: 89118bb8-6ec8-4048-b3d6-5c73a9eea33e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%

---

# 針對HTML5表單整合Form Bridge與自訂入口網站{#integrating-form-bridge-with-custom-portal-for-html-forms}

FormBridge是HTML5 forms bridge API，可讓您與表單互動。 如需FormBridge API的參考資料，請參閱 [FormBridge API參考](/help/forms/using/form-bridge-apis.md).

您可以使用FormBridge API從HTML頁面取得或設定表單欄位的值，並提交表單。 例如，您可以使用API來建置精靈般的體驗。

現有的HTML應用程式可運用FormBridge API與表單互動，並將其內嵌於HTML頁面中。 您可以使用下列步驟，透過Form Bridge API設定欄位的值。

## 將HTML5表單整合至網頁 {#integrating-html-forms-to-a-web-page}

1. **選擇設定檔或建立設定檔**

   1. 在CRX DE介面中，導覽至： `https://'[server]:[port]'/crx/de`.
   1. 使用管理員認證登入。
   1. 建立設定檔或選擇現有的設定檔。

      如需如何建立設定檔的詳細資訊，請參閱 [建立新的設定檔](/help/forms/using/custom-profile.md).

1. **修改HTML設定檔**

   在設定檔轉譯器中包含XFA執行階段、XFA地區設定程式庫和XFA表單HTML程式碼片段、設計您的網頁，並將表單放入網頁中。

   例如，使用以下程式碼片段，建立包含兩個輸入欄位的應用程式，以及示範表單與外部應用程式之間互動的表單。

   ```xml
   <%@ page session="false"
                  contentType="text/html; charset=utf-8"%><%
   %><%@ taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
   %><!DOCTYPE html>
   <html manifest="${param.offlineSpec}">
       <head>
          <cq:include script="formRuntime.jsp"/>
           <!-- Portal Scripts and Styles -->
          <cq:include script="portalheader.jsp"/>
       </head>
       <body>
           <div id="leftdiv" >
               <div id="leftdivcontentarea">
                   <!-- Portal Body -->
                 <cq:include script="portalbody.jsp"/>
               </div>
           </div>
           <div id="rightdiv">
               <div id="formBody">
               <cq:include script="config.jsp"/>
               <!-- Form body -->
               <cq:include script="formBody.jsp"/>
               <!  --To assist in page transitions -- add navigation, based on scrolling -->
               <cq:include  script="../nav/scroll/nav_footer.jsp"/>
               <cq:include script="footer.jsp"/>
               </div>
           </div>
       </body>
   </html>
   ```

   >[!NOTE]
   >
   >此 **第9行**，包含其他CSS樣式的JSP參考和用來設計頁面的JavaScript檔案。
   >
   >
   >此 &lt;div id=&quot;rightdiv&quot;> 標籤於 **第18行** 包含XFA表單的HTML片段。
   頁面會設定為兩個容器的樣式： **left** 和 **右側**. 正確的容器有表單。 左側容器有兩個輸入欄位和部分外部HTML頁面。
   以下熒幕擷圖顯示表單在瀏覽器中的顯示方式。

   ![入口網站](assets/portal.jpg)

   左側是 **HTML頁面**. 包含欄位的右側是 **xfa表單**.

1. **從頁面存取表單欄位**

   以下是範例指令碼，您可以新增此指令碼以在表單欄位中設定值。

   例如，如果您想要設定 **員工姓名** 使用欄位中的值 **名字** 和 **姓氏**，呼叫 **window.formBridge.setFieldValue** 函式。

   同樣地，您可以呼叫以讀取值 **window.formBridge.getFieldValue** API。

   ```javascript
   $(function() {
               $(".input").blur(function() {
                   window.formBridge.setFieldValue(
                               'xfa.form.form1.#subform[0].EmployeeName',
                                $("#lname").val()+' '+$("#fname").val()
                              )
                   });
           });
   ```
