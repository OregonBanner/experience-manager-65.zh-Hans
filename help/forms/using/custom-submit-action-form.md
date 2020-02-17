---
title: 为自适应表单编写自定义提交操作
seo-title: 为自适应表单编写自定义提交操作
description: 通过AEM Forms，您可以为自适应表单创建自定义提交操作。 本文描述为自适应表单添加自定义提交操作的过程。
seo-description: 通过AEM Forms，您可以为自适应表单创建自定义提交操作。 本文描述为自适应表单添加自定义提交操作的过程。
uuid: fd8e1dac-b997-4e86-aaf6-3507edcb3070
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 2a2e1156-4a54-4b0a-981c-d527fe22a27e
docset: aem65
translation-type: tm+mt
source-git-commit: dfa983db4446cbb0cbdeb42297248aba55b3dffd

---


# 为自适应表单编写自定义提交操作{#writing-custom-submit-action-for-adaptive-forms}

自适应表单要求提交操作以处理用户指定的数据。 “提交”操作可确定使用自适应表单对提交的数据执行的任务。 Adobe Experience Manager(AEM)包括 [OOTB提交操作](../../forms/using/configuring-submit-actions.md) ，这些操作演示了可以使用用户提交的数据执行的自定义任务。 例如，您可以执行诸如发送电子邮件或存储数据等任务。

## “提交”操作的工作流 {#workflow-for-a-submit-action}

流程图描述了在自适应表单中单击“提交”按钮时触发的“提 **[!UICONTROL 交]** ”操作的工作流。 文件附件组件中的文件将上传到服务器，并且表单数据将更新为已上传文件的URL。 在客户端中，数据以JSON格式存储。 客户端将Ajax请求发送到内部servlet，该servlet按摩您指定的数据并以XML格式返回它。 客户端将此数据与操作字段进行整理。 它通过表单提交操作将数据提交到最终的servlet（指南提交servlet）。 然后，Servlet将控件转发到“提交”操作。 “提交”操作可以将请求转发到其他sling资源，或将浏览器重定向到其他URL。

![描述“提交”操作工作流的流程图](assets/diagram1.png)

### XML数据格式 {#xml-data-format}

XML数据使用request参数发送到 **`jcr:data`** servlet。 提交操作可以访问参数以处理数据。 以下代码描述XML数据的格式。 绑定到表单模型的字段显示在部 **`afBoundData`** 分。 未绑定的字段显示在部 `afUnoundData`分中。 有关文件格式的详细信息，请参 `data.xml` 阅预填充自 [适应表单字段的简介](../../forms/using/prepopulate-adaptive-form-fields.md)。

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

“提交”操作可以将隐藏的输入字段(使用HTML输 [入标签](https://developer.mozilla.org/en/docs/Web/HTML/Element/Input) )添加到呈现的表单HTML中。 这些隐藏字段可以包含处理表单提交时需要的值。 提交表单时，这些字段值将作为请求参数发回，提交操作可在提交处理过程中使用这些请求参数。 输入字段称为操作字段。

例如，如果“提交”操作同时捕获填写表单所花费的时间，则可以添加隐藏的输入字段 `startTime` 和 `endTime`。

脚本可在表单呈现时和表 `startTime` 单提交 `endTime` 前分别提供字段和字段的值。 然后，“提交”操 `post.jsp` 作脚本可以使用请求参数访问这些字段并计算填写表单所需的总时间。

### 文件附件 {#file-attachments}

提交操作还可以使用您使用文件附件组件上传的文件附件。 提交操作脚本可以使用sling [RequestParameter API访问这些文件](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html)。 API [](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#isFormField()) 的isFormField方法有助于识别请求参数是文件还是表单字段。 您可以在“提交”操作中对“请求”参数进行迭代，以标识“文件附件”参数。

以下示例代码标识请求中的文件附件。 接下来，它使用Get API将数据读 [入文件](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#get())。 最后，它使用数据创建一个Document对象并将其附加到列表。

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

执行所需操作后，Submit servlet将请求转发到转发路径。 操作使用setForwardPath API在指南提交servlet中设置前进路径。

如果操作不提供前向路径，则提交servlet将使用重定向URL重定向浏览器。 作者使用自适应表单编辑对话框中的感谢页面配置来配置重定向URL。 您还可以通过“提交”操作或指南提交servlet中的setRedirectUrl API配置重定向URL。 您还可以使用指南提交servlet中的setRedirectParameters API配置发送到重定向URL的请求参数。

>[!NOTE]
>
>作者提供了重定向URL（使用感谢页面配置）。 [OOTB提交操作使用](../../forms/using/configuring-submit-actions.md) “重定向URL”从转发路径引用的资源重定向浏览器。
>
>您可以编写一个自定义提交操作，将请求转发到资源或servlet。 Adobe建议为前向路径执行资源处理的脚本在处理完成时将请求重定向到重定向URL。

## Submit action {#submit-action}

“提交”操作是sling:Folder，其中包括：

* **addfields.jsp**:此脚本提供在再现期间添加到HTML文件的操作字段。 使用此脚本可在post.POST.jsp脚本中添加提交过程中所需的隐藏输入参数。
* **dialog.xml**:此脚本与“CQ组件”对话框类似。 它提供作者自定义的配置信息。 选择“提交”操作时，这些字段将显示在“自适应表单编辑”对话框的“提交操作”选项卡中。
* **post.POST.jsp**:Submit servlet将使用您提交的数据以及前面几节中的其他数据调用此脚本。 提及在此页中运行操作即意味着运行post.POST.jsp脚本。 要向“自适应表单编辑”对话框中显示的自适应表单注册“提交”操作，请将以下属性添加到sling:Folder:

   * **guideComponentType** ，类型为String, **值为fd/af/components/guidesubmittype**
   * **guideDataModel** ，类型为String，它指定适用“提交”操作的自适应表单的类型。 **基于** XFA的自适应表单支持xfa，而基于 **XSD的自适应表单支持xsd** 。 **不使** 用XDP或XSD的自适应表单支持basic。 要在多种类型的自适应表单上显示操作，请添加相应的字符串。 用逗号分隔每个字符串。 例如，要使动作在基于XFA和XSD的自适应表单上可见，请分别指 **定xfa** 和 **xsd** 值。

   * **jcr:description** of type String. 此属性的值显示在自适应表单编辑对话框的提交操作选项卡的提交操作列表中。 OOTB操作位于CRX存储库中的 **位置/libs/fd/af/components/guidesubmittype**。

## 创建自定义提交操作 {#creating-a-custom-submit-action}

执行以下步骤以创建将数据保存到CRX存储库中的自定义提交操作，然后向您发送电子邮件。 自适应表单包含将数据保存到CRX存储库的OOTB提交操作存储内容（已弃用）。 此外，CQ还提供可用 [于发送电子邮件的Mail](https://docs.adobe.com/docs/en/cq/current/javadoc/com/day/cq/mailer/package-summary.html) API。 在使用Mail API之前， [请通过系统]控制台配置Day CQ mail服务(https://docs.adobe.com/docs/en/cq/current/administering/notification.html?wcmmode=disabled#Configuring使用Mail服务)。 可以重复使用“存储内容（已弃用）”操作，将数据存储在存储库中。 “存储内容（已弃用）”操作可在CRX存储库中的/libs/fd/af/components/guidesubmittype/store位置执行。

1. 登录URL https://&lt;server>:&lt;port>/crx/de/index.jsp中的CRXDE Lite。 使用属性sling:Folder和/apps/custom_submit_action文件夹中的名称store_and_mail创建节点。 创建custom_submit_action文件夹（如果它尚不存在）。

   ![描述使用属性sling:Folder创建节点的屏幕截图](assets/step1.png)

1. **提供必填的配置字段。**

   添加“存储”操作所需的配置。 将“商店 **** ”操作的cq:dialog节点从/libs/fd/af/components/guidesubmittype/store复制到位于/apps/custom_submit_action/store_and_email的操作文件夹中。

   ![屏幕截图显示对话框节点复制到操作文件夹](assets/step2.png)

1. **提供配置字段以提示作者进行电子邮件配置。**

   自适应表单还提供向用户发送电子邮件的“电子邮件”操作。 根据您的要求自定义此操作。 导航到/libs/fd/af/components/guidesubmittype/email/dialog。 将cq:dialog节点中的节点复制到“提交”操作的cq:dialog节点(/apps/custom_submit_action/store_and_email/dialog)。

   ![自定义电子邮件操作](assets/step3.png)

1. **在自适应表单编辑对话框中使操作可用。**

   在store_and_email节点中添加以下属性：

   * **guideComponentType** of **String** and value **fd/af/components/guidesubmittype**

   * **guideDataModel** ，类型 **为String** , value **xfa, xsd, basic**

   * **jcr:Description** of type **String** and value **Store and Email Action**

1. 打开任何自适应表单。 单击“开 **始** ”旁边的“编辑”按钮，以打开自适应表 **单容器的“编辑****** ”对话框。 新操作将显示在“提交操 **作”选项卡中** 。 选择“存 **储”和“电子邮件操作** ”会显示在对话框节点中添加的配置。

   ![“提交操作配置”对话框](assets/store_and_email_submit_action_dialog.jpg)

1. **使用操作完成任务。**

   将post.POST.jsp脚本添加到您的操作中。 (/apps/custom_submit_action/store_and_mail/)。

   运行“OOTB存储”操作（post.POST.jsp脚本）。 使用 [FormsHelper.runAction](https://docs.adobe.com/docs/en/cq/current/javadoc/com/day/cq/wcm/foundation/forms/FormsHelper.html#runAction(java.lang.String, java.lang.String, org.apache.sling.api.resource.Resource, org.apache.sling.api.SlingHttpServletRequest, org.apache.sling.api.SlingHttpServletResponse)API, API在您的代码中提供该API来运行商店操作。 在JSP文件中添加以下代码：

   `FormsHelper.runAction("/libs/fd/af/components/guidesubmittype/store", "post", resource, slingRequest, slingResponse);`

   要发送电子邮件，代码将从配置中读取收件人的电子邮件地址。 要获取操作脚本中的配置值，请使用以下代码读取当前资源的属性。 同样，您也可以读取其他配置文件。

   `ValueMap properties = ResourceUtil.getValueMap(resource);`

   `String mailTo = properties.get("mailTo");`

   最后，使用CQ邮件API发送电子邮件。 使用 [SimpleEmail类创建电子邮件对象](https://commons.apache.org/proper/commons-email/apidocs/org/apache/commons/mail/SimpleEmail.html) ，如下所示：

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

   在自适应表单中选择操作。 该操作会发送电子邮件并存储数据。

