---
title: 编写自适应表单的自定义提交操作
seo-title: 编写自适应表单的自定义提交操作
description: AEM Forms允许您为自适应表单创建自定义提交操作。 本文介绍为自适应表单添加自定义提交操作的过程。
seo-description: AEM Forms允许您为自适应表单创建自定义提交操作。 本文介绍为自适应表单添加自定义提交操作的过程。
uuid: fd8e1dac-b997-4e86-aaf6-3507edcb3070
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 2a2e1156-4a54-4b0a-981c-d527fe22a27e
docset: aem65
translation-type: tm+mt
source-git-commit: a399b2cb2e0ae4f045f7e0fddf378fdcd80bb848
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 0%

---


# 编写自适应表单的自定义提交操作{#writing-custom-submit-action-for-adaptive-forms}

自适应表单需要提交操作来处理用户指定的数据。 “提交”操作决定对您使用自适应表单提交的数据执行的任务。 Adobe Experience Manager(AEM)包括[OOTB提交操作](../../forms/using/configuring-submit-actions.md)，这些操作演示了可以使用用户提交的数据执行的自定义任务。 例如，您可以执行任务，如发送电子邮件或存储数据。

## 提交操作{#workflow-for-a-submit-action}的工作流

流程图描述了在自适应表单中单击&#x200B;**[!UICONTROL Submit]**&#x200B;按钮时触发的“提交”操作的工作流。 文件附件组件中的文件将上传到服务器，表单数据将使用已上传文件的URL进行更新。 在客户端中，数据以JSON格式存储。 客户端向内部servlet发送Ajax请求，该Ajax请求按照您指定的数据并以XML格式返回它。 客户端将此数据与操作字段进行整理。 它通过表单提交操作将数据提交到最终的servlet（指南提交servlet）。 然后，servlet将控件转发到“提交”操作。 “提交”操作可以将请求转发到其他sling资源或将浏览器重定向到其他URL。

![描述“提交”操作工作流的流程图](assets/diagram1.png)

### XML数据格式{#xml-data-format}

使用&#x200B;**`jcr:data`**&#x200B;请求参数将XML数据发送到servlet。 提交操作可访问参数以处理数据。 以下代码描述XML数据的格式。 绑定到表单模型的字段显示在&#x200B;**`afBoundData`**&#x200B;部分。 未绑定字段显示在`afUnoundData`部分中。 有关`data.xml`文件格式的详细信息，请参见[预填充自适应表单字段的简介](../../forms/using/prepopulate-adaptive-form-fields.md)。

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

### 操作字段{#action-fields}

“提交”操作可以将隐藏的输入字段（使用HTML [input](https://developer.mozilla.org/en/docs/Web/HTML/Element/Input)标记）添加到呈现的HTML表单中。 这些隐藏字段可以包含处理表单提交时需要的值。 提交表单时，这些字段值将作为请求参数发回，提交操作在提交处理过程中可以使用这些参数。 输入字段称为操作字段。

例如，“提交”操作也捕获填写表单所花费的时间，可添加隐藏的输入字段`startTime`和`endTime`。

脚本可以在表单呈现时和表单提交前分别提供`startTime`和`endTime`字段的值。 然后，提交操作脚本`post.jsp`可以使用请求参数访问这些字段并计算填写表单所需的总时间。

### 文件附件{#file-attachments}

提交操作还可以使用您使用文件附件组件上传的文件附件。 提交操作脚本可以使用sling [RequestParameter API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html)访问这些文件。 API的[isFormField](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#isFormField())方法有助于确定请求参数是文件还是表单字段。 您可以在“提交”操作中对“请求”参数进行迭代，以标识“文件附件”参数。

以下示例代码标识请求中的文件附件。 然后，它使用[获取API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#get())将数据读入文件。 最后，它使用文档创建列表对象并将其附加到数据。

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

执行所需操作后，Submit servlet将请求转发到前进路径。 操作使用setForwardPath API在指南提交servlet中设置前进路径。

如果操作未提供前进路径，则提交servlet将使用重定向URL重定向浏览器。 作者使用自适应表单编辑对话框中的感谢页面配置来配置重定向URL。 您还可以通过“提交”操作或指南提交servlet中的setRedirectUrl API配置重定向URL。 您还可以使用指南提交servlet中的setRedirectParameters API配置发送到重定向URL的请求参数。

>[!NOTE]
>
>作者提供重定向URL（使用感谢页面配置）。 [OOTB提交](../../forms/using/configuring-submit-actions.md) 操作使用重定向URL从转发路径引用的资源重定向浏览器。
>
>您可以编写自定义提交操作，将请求转发到资源或servlet。 Adobe建议对前向路径执行资源处理的脚本在处理完成时将请求重定向到重定向URL。

## 提交操作{#submit-action}

“提交”操作是sling:Folder，包括以下内容：

* **addfields.jsp**:此脚本提供在再现期间添加到HTML文件的操作字段。使用此脚本在post.POST.jsp脚本中添加提交过程中所需的隐藏输入参数。
* **dialog.xml**:此脚本与“CQ组件”对话框类似。它提供作者自定义的配置信息。 当您选择提交操作时，这些字段将显示在自适应表单编辑对话框的提交操作选项卡中。
* **post.POST.jsp**:Submit servlet使用您提交的数据以及前几节中的其他数据调用此脚本。提及在此页中运行操作意味着运行post.POST.jsp脚本。 要向要在自适应表单编辑对话框中显示的自适应表单注册提交操作，请将以下属性添加到sling:Folder:

   * **guideComponentType** 类型字符串和 **值fd/af/components/guidesubmittype**
   * **指** 定适用“提交”操作的自适应表单类型的“字符串”类型的guideDataModel。**基** 于XFA的自适应表单支持xfa, **** 而基于XSD的自适应表单支持xsd。**不** 使用XDP或XSD的自适应表单支持的基本信息。要在多种类型的自适应表单上显示操作，请添加相应的字符串。 用逗号分隔每个字符串。 例如，要使操作在基于XFA和XSD的自适应表单上可见，请分别指定值&#x200B;**xfa**&#x200B;和&#x200B;**xsd**。

   * **jcr：字符串** 类型的描述。此属性的值显示在自适应表单编辑对话框的提交操作选项卡的提交操作列表中。 OOTB操作位于CRX存储库中的&#x200B;**/libs/fd/af/components/guidesubmittype**&#x200B;位置。

## 创建自定义提交操作{#creating-a-custom-submit-action}

执行以下步骤以创建将数据保存到CRX存储库中的自定义提交操作，然后向您发送电子邮件。 自适应表单包含将数据保存到CRX存储库中的OOTB提交操作存储内容（已弃用）。 此外，CQ还提供可用于发送电子邮件的[Mail](https://docs.adobe.com/docs/en/cq/current/javadoc/com/day/cq/mailer/package-summary.html) API。 在使用Mail API之前，[通过系统控制台配置](https://docs.adobe.com/docs/en/cq/current/administering/notification.html?wcmmode=disabled#Configuring配置Day CQ邮件服务)。 可以重复使用“存储内容（已弃用）”操作，将数据存储在存储库中。 存储内容（已弃用）操作可在CRX存储库中的/libs/fd/af/components/guidesubmittype/store位置执行。

1. 登录CRXDE Lite，网址为https://&lt;server>:&lt;port>/crx/de/index.jsp。 在/apps/custom_submit_action文件夹中创建具有sling:Folder属性和store_and_mail名称的节点。 创建custom_submit_action文件夹（如果它尚不存在）。

   ![描述使用属性sling:Folder创建节点的屏幕截图](assets/step1.png)

1. **提供必填配置字段。**

   添加“存储”操作所需的配置。 将“商店”操作的&#x200B;**cq:dialog**&#x200B;节点从/libs/fd/af/components/guidesubmittype/store复制到/apps/custom_submit_action/store_and_email上的操作文件夹。

   ![屏幕截图显示对话框节点复制到操作文件夹](assets/step2.png)

1. **提供配置字段以提示作者进行电子邮件配置。**

   自适应表单还提供向用户发送电子邮件的电子邮件操作。 根据您的要求自定义此操作。 导航到/libs/fd/af/components/guidesubmittype/email/dialog。 将cq:dialog节点中的节点复制到“提交”操作的cq:dialog节点(/apps/custom_submit_action/store_and_email/dialog)。

   ![自定义电子邮件操作](assets/step3.png)

1. **在自适应表单编辑对话框中使操作可用。**

   在store_and_email节点中添加以下属性：

   * **** guideComponentTypeof **** 类型 **String和值fd/af/components/guidesubmittype**

   * **** String和value xfa **** 类型 **的guideDataModel, xsd, basic**

   * **jcr:“** 字符串”类 **** 型的描 **述以及“存储”和“电子邮件”操作**

1. 打开任何自适应表单。 单击&#x200B;**开始**&#x200B;旁边的&#x200B;**编辑**&#x200B;按钮，打开自适应表单容器的&#x200B;**编辑**&#x200B;对话框。 新操作显示在&#x200B;**提交操作**&#x200B;选项卡中。 选择&#x200B;**存储和电子邮件操作**&#x200B;将显示在对话框节点中添加的配置。

   ![提交操作配置对话框](assets/store_and_email_submit_action_dialog.jpg)

1. **使用操作完成任务。**

   将post.POST.jsp脚本添加到您的操作。 (/apps/custom_submit_action/store_and_mail/)。

   运行OOTB Store操作(post.POST.jsp脚本)。 使用CQ在您的代码中提供的[FormsHelper.runAction](https://docs.adobe.com/docs/en/cq/current/javadoc/com/day/cq/wcm/foundation/forms/FormsHelper.html#runAction(java.lang.String, java.lang.String, org.apache.sling.api.resource.Resource, org.apache.sling.api.SlingHttpServletRequest, org.apache.api.SlingHttpServletResponse) API) API。运行“商店”操作。 在JSP文件中添加以下代码：

   `FormsHelper.runAction("/libs/fd/af/components/guidesubmittype/store", "post", resource, slingRequest, slingResponse);`

   要发送电子邮件，代码会从配置中读取收件人的电子邮件地址。 要在操作的脚本中获取配置值，请使用以下代码读取当前资源的属性。 同样，您也可以读取其他配置文件。

   `ValueMap properties = ResourceUtil.getValueMap(resource);`

   `String mailTo = properties.get("mailTo");`

   最后，使用CQ邮件API发送电子邮件。 使用[SimpleEmail](https://commons.apache.org/proper/commons-email/apidocs/org/apache/commons/mail/SimpleEmail.html)类创建电子邮件对象，如下所示：

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

