---
title: 为自适应表单编写自定义提交操作
seo-title: Writing custom Submit action for adaptive forms
description: AEM Forms允许您为自适应表单创建自定义提交操作。 本文介绍了为自适应表单添加自定义提交操作的过程。
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

# 为自适应表单编写自定义提交操作{#writing-custom-submit-action-for-adaptive-forms}

自适应表单需要提交操作才能处理用户指定的数据。 “提交”操作确定使用自适应表单对您提交的数据执行的任务。 Adobe Experience Manager(AEM)包括 [OOTB提交操作](../../forms/using/configuring-submit-actions.md) 演示了使用用户提交的数据可以执行的自定义任务。 例如，您可以执行各种任务，如发送电子邮件或存储数据。

## 提交操作的工作流 {#workflow-for-a-submit-action}

流程图描述了在单击 **[!UICONTROL 提交]** 按钮。 文件附件组件中的文件将上传到服务器，并且表单数据会更新为已上传文件的URL。 在客户端中，数据以JSON格式存储。 客户端向内部Servlet发送Ajax请求，该Servlet按摩您指定的数据，并以XML格式返回。 客户端将此数据与操作字段进行整理。 它通过“表单提交”操作将数据提交到最终Servlet（指南提交Servlet）。 然后，Servlet将控件转发到Submit操作。 “提交”操作可以将请求转发到其他sling资源，或将浏览器重定向到其他URL。

![描述“提交”操作工作流的流程图](assets/diagram1.png)

### XML数据格式 {#xml-data-format}

XML数据将使用 **`jcr:data`** 请求参数。 提交操作可以访问参数以处理数据。 以下代码描述XML数据的格式。 绑定到表单模型的字段显示在 **`afBoundData`** 中。 未绑定字段显示在 `afUnoundData`中。 有关 `data.xml` 文件，请参阅 [预填充自适应表单字段的简介](../../forms/using/prepopulate-adaptive-form-fields.md).

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

提交操作可添加隐藏的输入字段(使用HTML [输入](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Input) 标记)到呈现的表单HTML。 这些隐藏字段可以包含处理表单提交时需要的值。 提交表单时，这些字段值将作为请求参数发回，提交操作可在提交处理过程中使用这些参数。 输入字段称为操作字段。

例如，如果“提交”操作也捕获填写表单所花费的时间，则可以添加隐藏的输入字段 `startTime` 和 `endTime`.

脚本可以提供 `startTime` 和 `endTime` 字段。 提交ActionScript `post.jsp` 然后，可以使用请求参数访问这些字段并计算填写表单所需的总时间。

### 文件附件 {#file-attachments}

提交操作还可以使用您使用文件附件组件上传的文件附件。 提交操作脚本可以使用sling访问这些文件 [RequestParameter API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html). 的 [isFormField](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#isFormField()) API的方法可帮助识别请求参数是文件还是表单字段。 您可以在“提交”操作中迭代请求参数，以标识“文件附件”参数。

以下示例代码标识请求中的文件附件。 接下来，它使用 [获取API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#get()). 最后，它使用数据创建一个Document对象并将其附加到列表。

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

执行所需操作后，Submit servlet会将请求转发到转发路径。 操作使用setForwardPath API在指南提交Servlet中设置前进路径。

如果操作未提供转发路径，则提交Servlet会使用重定向URL重定向浏览器。 作者使用自适应表单编辑对话框中的感谢页面配置来配置重定向URL。 您还可以通过提交操作或指南提交servlet中的setRedirectUrl API来配置重定向URL。 您还可以使用指南提交servlet中的setRedirectParameters API配置发送到重定向URL的请求参数。

>[!NOTE]
>
>作者提供了重定向URL（使用感谢页面配置）。 [OOTB提交操作](../../forms/using/configuring-submit-actions.md) 使用重定向URL从转发路径引用的资源中重定向浏览器。
>
>您可以编写一个自定义的Submit操作，将请求转发到资源或Servlet。 Adobe建议负责对前向路径执行资源处理的脚本在处理完成时将请求重定向到重定向URL。

## 提交操作 {#submit-action}

“提交”操作是一个sling:Folder，其中包含以下内容：

* **addfields.jsp**:此脚本提供在呈现期间添加到HTML文件的操作字段。 使用此脚本在post.POST.jsp脚本中添加提交期间所需的隐藏输入参数。
* **dialog.xml**:此脚本类似于CQ组件对话框。 它提供作者自定义的配置信息。 当您选择提交操作时，这些字段会显示在自适应表单编辑对话框的提交操作选项卡中。
* **post.POST.jsp**:提交Servlet会使用您提交的数据以及前几节中的附加数据调用此脚本。 在此页中提及运行操作意味着运行post.POST.jsp脚本。 要在自适应表单中注册“提交”操作以在“自适应表单编辑”对话框中显示，请将这些属性添加到sling:Folder:

   * **guideComponentType** 字符串类型和值 **fd/af/components/guidesubmittype**
   * **guideDataModel** “字符串”类型，指定适用“提交”操作的自适应表单类型。 **xfa** 支持基于XFA的自适应表单，而 **xd** 基于XSD的自适应表单支持。 **基本** 不使用XDP或XSD的自适应表单支持。 要对多种类型的自适应表单显示操作，请添加相应的字符串。 用逗号分隔每个字符串。 例如，要使操作在基于XFA和XSD的自适应表单上可见，请指定值 **xfa** 和 **xd** 分别进行。

   * **jcr:description** 类型为“字符串”。 此属性的值显示在“自适应表单编辑”对话框的“提交操作”选项卡的“提交操作”列表中。 OOTB操作存在于位于的CRX存储库中 **/libs/fd/af/components/guidesubmittype**.

## 创建自定义提交操作 {#creating-a-custom-submit-action}

执行以下步骤以创建一个自定义提交操作，该操作将数据保存在CRX存储库中，然后向您发送电子邮件。 自适应表单包含将数据保存到CRX存储库的OOTB提交操作存储内容（已弃用）。 此外，CQ还提供 [邮件](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hans) 可用于发送电子邮件的API。 在使用邮件API之前， [配置](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hans&amp;wcmmode=disabled) Day CQ Mail服务。 您可以重复使用“存储内容（已弃用）”操作将数据存储在存储库中。 “存储内容（已弃用）”操作可在CRX存储库的/libs/fd/af/components/guidesubmittype/store位置执行。

1. 登录到CRXDE Lite，网址为https://&lt;server>:&lt;port>/crx/de/index.jsp。 在/apps/custom_submit_action文件夹中创建一个具有属性sling:Folder和名称store_and_mail的节点。 创建custom_submit_action文件夹（如果文件夹不存在）。

   ![描述使用属性sling:Folder创建节点的屏幕截图](assets/step1.png)

1. **提供必填配置字段。**

   添加Store操作所需的配置。 复制 **cq:dialog** 从/libs/fd/af/components/guidesubmittype/store到/apps/custom_submit_action/store_and_email上的action文件夹的“存储”操作节点。

   ![屏幕截图显示将对话框节点复制到操作文件夹](assets/step2.png)

1. **提供配置字段以提示作者进行电子邮件配置。**

   自适应表单还提供了向用户发送电子邮件的“电子邮件”操作。 根据您的要求自定义此操作。 导航至/libs/fd/af/components/guidesubmittype/email/dialog。 将cq:dialog节点中的节点复制到“提交”操作的cq:dialog节点(/apps/custom_submit_action/store_and_email/dialog)。

   ![自定义电子邮件操作](assets/step3.png)

1. **使该操作在自适应表单编辑对话框中可用。**

   在store_and_email节点中添加以下属性：

   * **guideComponentType** 类型 **字符串** 和值 **fd/af/components/guidesubmittype**

   * **guideDataModel** 类型 **字符串** 和值 **xfa、xsd、基本**

   * **jcr:description** 类型 **字符串** 和值 **存储和电子邮件操作**

1. 打开任何自适应表单。 单击 **编辑** 按钮 **开始** 打开 **编辑** 自适应表单容器对话框。 新操作将显示在 **提交操作** 选项卡。 选择 **存储和电子邮件操作** 显示在对话框节点中添加的配置。

   ![提交操作配置对话框](assets/store_and_email_submit_action_dialog.jpg)

1. **使用操作完成任务。**

   将post.POST.jsp脚本添加到您的操作。 (/apps/custom_submit_action/store_and_mail/)。

   运行OOTB存储操作(post.POST.jsp脚本)。 使用 [FormsHelper.runAction](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hans)(java.lang.String， java.lang.String， org.apache.sling.api.resource.Resource， org.apache.sling.api.SlingHttpServletRequest， org.apache.sling.api.SlingHttpServletResponse)API（CQ在您的代码中提供以运行存储操作）。 在JSP文件中添加以下代码：

   `FormsHelper.runAction("/libs/fd/af/components/guidesubmittype/store", "post", resource, slingRequest, slingResponse);`

   要发送电子邮件，此代码会从配置中读取收件人的电子邮件地址。 要在操作的脚本中获取配置值，请使用以下代码读取当前资源的属性。 同样，您也可以读取其他配置文件。

   `ValueMap properties = ResourceUtil.getValueMap(resource);`

   `String mailTo = properties.get("mailTo");`

   最后，使用CQ Mail API发送电子邮件。 使用 [SimpleEmail](https://commons.apache.org/proper/commons-email/apidocs/org/apache/commons/mail/SimpleEmail.html) 类创建电子邮件对象，如下所示：

   >[!NOTE]
   >
   >确保JSP文件的名称为post.POST.jsp。

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

   在自适应表单中选择操作。 操作会发送电子邮件并存储数据。
