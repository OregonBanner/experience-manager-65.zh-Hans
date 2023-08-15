---
title: 将Form Bridge与HTML5表单的自定义门户集成
seo-title: Integrating Form Bridge with custom portal for HTML5 forms
description: 您可以使用FormBridge API从“HTML”页获取或设置表单字段的值并提交表单。
seo-description: You can use the FormBridge API to get or set the values of form fields from the HTML page and submit the form.
uuid: c8911f82-1a25-47a5-9a06-19b5dce74a2c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bd9bf095-d74d-458c-afe7-fab04050849d
docset: aem65
feature: Mobile Forms
exl-id: 89118bb8-6ec8-4048-b3d6-5c73a9eea33e
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# 将Form Bridge与HTML5表单的自定义门户集成{#integrating-form-bridge-with-custom-portal-for-html-forms}

FormBridge是一个HTML5 Forms Bridge API，它允许您与表单交互。 有关FormBridge API的参考，请参阅 [FormBridge API参考](/help/forms/using/form-bridge-apis.md).

您可以使用FormBridge API从“HTML”页获取或设置表单字段的值并提交表单。 例如，您可以使用API构建类似于向导的体验。

现有的HTML应用程序可利用FormBridge API与表单进行交互并将其嵌入到HTML页面中。 您可以使用以下步骤通过Form Bridge API设置字段的值。

## 将HTML5表单集成到网页 {#integrating-html-forms-to-a-web-page}

1. **选择配置文件或创建配置文件**

   1. 在CRX DE界面中，导航到： `https://'[server]:[port]'/crx/de`.
   1. 使用管理员凭据登录。
   1. 创建配置文件或选择现有配置文件。

      有关如何创建配置文件的详细信息，请参阅 [创建新配置文件](/help/forms/using/custom-profile.md).

1. **修改HTML配置文件**

   在配置文件渲染器中包含XFA运行时、XFA区域设置库和XFA表单HTML片段，设计您的网页，并将表单放入网页中。

   例如，使用以下代码片断，创建一个包含两个输入字段的应用程序，并创建一个表单以演示表单与外部应用程序之间的交互。

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
   >此 **9号线**，包含用于设计CSS样式和JavaScript文件的其他JSP引用。
   >
   >
   >此 &lt;div id=&quot;rightdiv&quot;> 标记位于 **第18行** 包含XFA表单的HTML片段。
   >
   >
   页面将设置为两个容器： **左侧** 和 **右**. 正确的容器具有表单。 左侧容器包含两个输入字段和一个外部HTML页的一部分。
   >
   >
   以下屏幕抓图显示了表单在浏览器中的显示方式。

   ![门户](assets/portal.jpg)

   左侧是 **HTML页面**. 包含字段的右侧是 **xfa表单**.

1. **从页面访问表单字段**

   以下是示例脚本，您可以添加此脚本来设置表单字段中的值。

   例如，如果要设置 **雇员姓名** 使用字段中的值 **名字** 和 **姓氏**，调用 **window.formBridge.setFieldValue** 函数。

   同样，您可以通过调用 **window.formBridge.getFieldValue** API。

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
