---
title: 将Form Bridge与HTML5表单的自定义门户集成
seo-title: 将Form Bridge与HTML5表单的自定义门户集成
description: 您可以使用FormBridge API从HTML页面获取或设置表单字段的值并提交表单。
seo-description: 您可以使用FormBridge API从HTML页面获取或设置表单字段的值并提交表单。
uuid: c8911f82-1a25-47a5-9a06-19b5dce74a2c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bd9bf095-d74d-458c-afe7-fab04050849d
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 将Form Bridge与HTML5表单的自定义门户集成{#integrating-form-bridge-with-custom-portal-for-html-forms}

FormBridge是一个HTML5表单桥接器API，它允许您与表单交互。 有关FormBridge API参考，请参 [阅FormBridge API参考](/help/forms/using/form-bridge-apis.md)。

您可以使用FormBridge API从HTML页面获取或设置表单字段的值并提交表单。 例如，您可以使用API构建类似向导的体验。

现有HTML应用程序可以利用FormBridge API与表单交互并将其嵌入到HTML页中。 您可以使用以下步骤使用Form Bridge API设置字段的值。

## 将HTML5表单集成到网页 {#integrating-html-forms-to-a-web-page}

1. **选择用户档案或创建用户档案**

   1. 在CRX DE界面中，导航到： `https://'[server]:[port]'/crx/de`.
   1. 使用管理员凭据登录。
   1. 创建用户档案或选择现有用户档案。

      有关如何创建用户档案的详细信息，请参 [阅创建新用户档案](/help/forms/using/custom-profile.md)。

1. **修改HTML用户档案**

   将XFA运行时、XFA区域设置库和XFA表单HTML代码片断包含在用户档案渲染器中，设计网页并将表单放在网页内。

   例如，使用以下代码片断创建一个应用程序，该应用程序包含两个输入字段和一个表单，用于演示表单与外部应用程序之间的交互。

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
   >第9 **行**，包含用于设计页面的CSS样式和JavaScript文件的其他JSP参考。
   >
   >
   >第18行上的&lt;div id=&quot;rightdiv&quot;>标 **签包含** XFA表单的HTML片段。
   页面的样式设置为两个容器: **左****右**。 正确的容器具有表单。 左容器有两个输入字段，外部HTML页面的一部分。
   以下屏幕快照显示了表单在浏览器中的显示方式。

   ![门户](assets/portal.jpg)

   左侧是 **HTML页面的一部分**。 包含字段的右侧是 **xfa表单**。

1. **从页面访问表单字段**

   以下是可添加到表单字段中设置值的示例脚本。

   例如，如果要使用“字段名”和“姓”中的值设置 **EmployeeName** ，则调用 ************ window.formBridge.setFieldValue函数。

   同样，您也可以通过调用 **window.formBridge.getFieldValue** API读取值。

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
