---
title: 编写自适应表单的自定义提交操作
description: AEM Forms允许您为自适应表单创建自定义提交操作。 本文介绍了为自适应表单添加自定义提交操作的过程。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 7c3d0dac-4e19-4eb3-a43d-909d526acd55
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 1%

---

# 编写自适应表单的自定义提交操作{#writing-custom-submit-action-for-adaptive-forms}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/custom-submit-action-form.html) |
| AEM 6.5 | 本文 |

自适应表单需要提交操作来处理用户指定的数据。 提交操作确定使用自适应表单提交的数据上执行的任务。 Adobe Experience Manager (AEM)包括 [OOTB提交操作](../../forms/using/configuring-submit-actions.md) 演示您可以使用用户提交的数据执行的自定义任务。 例如，您可以执行各种任务，如发送电子邮件或存储数据。

## 提交操作的工作流 {#workflow-for-a-submit-action}

此流程图描述了在单击 **[!UICONTROL 提交]** 按钮。 文件附件组件中的文件将上载到服务器，并且表单数据将使用上载文件的URL进行更新。 在客户端中，数据以JSON格式存储。 客户端向内部servlet发送Ajax请求，后者对指定的数据进行按摩并以XML格式返回该数据。 客户端使用操作字段整理此数据。 它通过“表单提交”操作将数据提交到最终servlet（指南提交servlet）。 然后，Servlet将控件转发到Submit操作。 提交操作可以将请求转发到其他sling资源，或将浏览器重定向到其他URL。

![描述提交操作工作流的流程图](assets/diagram1.png)

### XML数据格式 {#xml-data-format}

使用将XML数据发送到servlet **`jcr:data`** 请求参数。 提交操作可以访问参数以处理数据。 以下代码描述了XML数据的格式。 绑定到表单模型的字段显示在 **`afBoundData`** 部分。 未绑定字段显示在 `afUnoundData`部分。 有关格式的详细信息 `data.xml` 文件，请参见 [预填充自适应表单字段简介](../../forms/using/prepopulate-adaptive-form-fields.md).

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

### 操作字段 {#action-fields}

提交操作可以添加隐藏的输入字段(使用HTML) [输入](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Input) 标签)到渲染的表单HTML。 这些隐藏字段可以包含处理表单提交时所需的值。 提交表单时，这些字段值作为请求参数发布回来，提交操作可在提交处理期间使用这些参数。 输入字段称为操作字段。

例如，提交操作可以添加隐藏的输入字段，该操作还会捕获填写表单所用的时间 `startTime` 和 `endTime`.

脚本可以提供 `startTime` 和 `endTime` 表单渲染时和表单提交前的字段。 提交ActionScript `post.jsp` 之后，可以使用请求参数访问这些字段，并计算填写表单所需的总时间。

### 文件附件 {#file-attachments}

提交操作还可以使用您通过“文件附件”组件上传的文件附件。 提交操作脚本可以使用sling访问这些文件 [RequestParameter API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html). 此 [isFormField](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#isFormField()) api的方法有助于识别请求参数是文件还是表单字段。 您可以在Submit操作中对Request参数进行迭代，以标识File Attachment参数。

以下示例代码标识请求中的文件附件。 接下来，它使用 [获取API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#get()). 最后，它会使用数据创建一个Document对象，并将其附加到列表中。

```java
RequestParameterMap requestParameterMap = slingRequest.getRequestParameterMap();
for (Map.Entry<String, RequestParameter[]> param : requestParameterMap.entrySet()) {
    RequestParameter rpm = param.getValue()[0];
    if(!rpm.isFormField()) {
        fileAttachments.add(new Document(rpm.get()));
    }
}
```

### 转发路径和重定向URL {#forward-path-and-redirect-url}

执行所需的操作后，提交servlet将请求转发到转发路径。 一个操作使用setForwardPath API在指南提交servlet中设置转发路径。

如果操作不提供转发路径，则提交Servlet将使用重定向URL重定向浏览器。 作者使用“自适应表单编辑”对话框中的“感谢页面”配置来配置重定向URL。 您还可以通过提交操作或指南提交servlet中的setRedirectUrl API配置重定向URL。 您还可以使用指南提交servlet中的setRedirectParameters API配置发送到重定向URL的请求参数。

>[!NOTE]
>
>作者提供了重定向URL（使用感谢页面配置）。 [OOTB提交操作](../../forms/using/configuring-submit-actions.md) 使用重定向URL从转发路径引用的资源重定向浏览器。
>
>您可以编写自定义提交操作，将请求转发到资源或servlet。 Adobe建议在处理完成后，为转发路径执行资源处理的脚本将请求重定向到重定向URL。

## 提交操作 {#submit-action}

提交操作是一个sling：Folder操作，它包括以下内容：

* **addfields.jsp**：此脚本提供在呈现版本期间添加到HTML文件中的操作字段。 此脚本用于在post.context.jsp脚本中添加提交期间所需的POST输入参数。
* **dialog.xml**：此脚本类似于CQ组件对话框。 它提供作者自定义的配置信息。 选择提交操作后，这些字段显示在“自适应表单编辑”对话框的“提交操作”选项卡中。
* **post.POST.jsp**：提交servlet使用您提交的数据以及前面部分中的附加数据调用此脚本。 本页中有关运行操作的任何内容都表示运行post.post.jspPOST。 要将提交操作注册到自适应表单以在“自适应表单编辑”对话框中显示，请将这些属性添加到sling:Folder:

   * **guideComponentType** 字符串和值的类型 **fd/af/components/guidesubmittype**
   * **guideDataModel** 类型字符串，指定提交操作适用的自适应表单的类型。 **xfa** 支持基于XFA的自适应表单，而 **xsd** 基于XSD的自适应表单支持。 **基本** 支持用于不使用XDP或XSD的自适应表单。 要在多种类型的自适应表单上显示操作，请添加相应的字符串。 用逗号分隔每个字符串。 例如，要使某个操作在基于XFA和XSD的自适应表单中可见，请指定相应的值 **xfa** 和 **xsd** 的量度。

   * **jcr：description** 类型为String。 此属性的值显示在“自适应表单编辑”对话框的“提交操作”选项卡的“提交操作”列表中。 OOTB操作存在于该位置的CRX存储库中 **/libs/fd/af/components/guidesubmittype**.

## 创建自定义提交操作 {#creating-a-custom-submit-action}

执行以下步骤可创建自定义提交操作，将数据保存在CRX存储库中，并向您发送电子邮件。 自适应表单包含OOTB提交操作存储内容（已弃用），可将数据保存在CRX存储库中。 此外，CQ还提供 [邮件](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hans) 可用于发送电子邮件的API。 在使用Mail API之前， [配置](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=en&amp;wcmmode=disabled) Day CQ Mail服务通过系统控制台。 您可以重用“存储内容（已弃用）”操作将数据存储在存储库中。 在CRX存储库中的/libs/fd/af/components/guidesubmittype/store位置提供了“存储内容（已弃用）”操作。

1. 通过URL https://登录CRXDE Lite&lt;server>：&lt;port>/crx/de/index.jsp. 在/apps/custom_submit_action文件夹中创建具有属性sling：Folder并命名为store_and_mail的节点。 创建custom_submit_action文件夹（如果尚不存在）。

   ![描述使用属性sling：Folder创建节点的屏幕截图](assets/step1.png)

1. **提供必需的配置字段。**

   添加存储区操作所需的配置。 复制 **cq：dialog** 从/libs/fd/af/components/guidessubmittype/store到/apps/custom_submit_action/store_and_email操作文件夹的“存储”操作的节点。

   ![显示将对话框节点复制到操作文件夹的屏幕截图](assets/step2.png)

1. **提供配置字段以提示作者进行电子邮件配置。**

   自适应表单还提供向用户发送电子邮件的电子邮件操作。 根据您的要求自定义此操作。 导航到/libs/fd/af/components/guidessubmittype/email/dialog。 将cq：dialog节点中的节点复制到提交操作(/apps/custom_submit_action/store_and_email/dialog)的cq：dialog节点。

   ![自定义电子邮件操作](assets/step3.png)

1. **使操作在“自适应表单编辑”对话框中可用。**

   在store_and_email节点中添加以下属性：

   * **guideComponentType** 类型 **字符串** 和值 **fd/af/components/guidesubmittype**

   * **guideDataModel** 类型 **字符串** 和值 **xfa， xsd，基本**

   * **jcr：description** 类型 **字符串** 和值 **存储和电子邮件操作**

1. 打开任意自适应表单。 单击 **编辑** 按钮旁边 **开始** 以打开 **编辑** 自适应表单容器的对话框。 新操作将显示在 **提交操作** 选项卡。 选择 **存储和电子邮件操作** 显示对话框节点中添加的配置。

   ![提交操作配置对话框](assets/store_and_email_submit_action_dialog.jpg)

1. **使用操作完成任务。**

   将post.jsp.jspPOST添加到您的操作中。 (/apps/custom_submit_action/store_and_mail/)。

   运行OOTB Store操作(post.store.jspPOST)。 使用 [FormsHelper.runAction](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hans)(java.lang.String、java.lang.String、org.apache.sling.api.resource.Resource、org.apache.sling.api.SlingHttpServletRequest、org.apache.sling.api.SlingHttpServletResponse) CQ在您的代码中提供的API以运行存储操作。 在JSP文件中添加以下代码：

   `FormsHelper.runAction("/libs/fd/af/components/guidesubmittype/store", "post", resource, slingRequest, slingResponse);`

   要发送电子邮件，代码会从配置中读取收件人的电子邮件地址。 要获取操作脚本中的配置值，请使用以下代码读取当前资源的属性。 同样，您可以读取其他配置文件。

   `ValueMap properties = ResourceUtil.getValueMap(resource);`

   `String mailTo = properties.get("mailTo");`

   最后，使用CQ Mail API发送电子邮件。 使用 [简单电子邮件](https://commons.apache.org/proper/commons-email/apidocs/org/apache/commons/mail/SimpleEmail.html) 类以创建电子邮件对象，如下所述：

   >[!NOTE]
   >
   >确保JSP文件的名称是post.pository.jspPOST。

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

   选择自适应表单中的操作。 该操作会发送电子邮件并存储数据。
