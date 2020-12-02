---
title: 配置提交操作
seo-title: 配置提交操作
description: AEM Forms允许您配置提交操作，以定义提交后如何处理自适应表单。 您可以使用内置提交操作或从头开始编写您自己的提交操作。
seo-description: AEM Forms允许您配置提交操作，以定义提交后如何处理自适应表单。 您可以使用内置提交操作或从头开始编写您自己的提交操作。
uuid: 4368d648-88ea-4f84-a051-46296a1a084e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 9d8d7044-ffce-4ab4-9543-a2d2f9da31e3
docset: aem65
translation-type: tm+mt
source-git-commit: c74d9e86727f2deda62b8d1eb105b28ef4b6d184
workflow-type: tm+mt
source-wordcount: '1503'
ht-degree: 1%

---


# 配置提交操作{#configuring-the-submit-action}

## 提交操作简介{#introduction-to-submit-actions}

当用户单击自适应表单上的“提交”按钮时，将触发提交操作。 您可以在自适应表单上配置提交操作。 自适应表单提供一些开箱即用的提交操作。 您可以复制和扩展默认的提交操作，以创建您自己的提交操作。 但是，根据您的要求，您可以编写并注册您自己的提交操作，以处理已提交表单中的数据。 提交操作可使用[同步或异步提交](../../forms/using/asynchronous-submissions-adaptive-forms.md)。

您可以在提要栏的自适应表单容器属性的&#x200B;**Submission**&#x200B;部分配置提交操作。

![配置提交操作](assets/thank-you-setting.png)

配置提交操作

自适应表单的默认提交操作包括：

* 提交到REST端点
* 发送电子邮件
* 通过电子邮件发送PDF
* 调用Forms Workflow
* 使用表单数据模型提交
* Forms门户提交操作
* 调用AEM工作流

>[!NOTE]
>
>“通过电子邮件发送PDF”提交操作仅适用于使用XFA模板作为表单模型的自适应表单。

>[!NOTE]
>
>确保[AEM_Installation_Directory]\crx-quickstart\temp\datamanager\ASM folder
>存在. 临时存储附件时需要该目录。 如果目录不存在，请创建它。

>[!CAUTION]
>
>如果[预填](../../forms/using/prepopulate-adaptive-form-fields.md)表单模板、表单数据模型或基于模式的自适应表单（XML或JSON数据）向模式(XML模式、JSON模式、表单模板或表单数据模型)投诉，该数据不包含&lt;afData>、&lt;afBoundData>和&lt;/afUnboundData>标签，然后，自适应表单的无界字段（无界字段是没有[bindref](../../forms/using/prepopulate-adaptive-form-fields.md)属性的自适应表单字段）的数据丢失。

您可以为自适应表单编写自定义提交操作以满足您的使用案例。 有关详细信息，请参阅[编写自适应表单的自定义提交操作](../../forms/using/custom-submit-action-form.md)。

## 提交到REST端点{#submit-to-rest-endpoint}

**提交到REST端点**&#x200B;提交选项将表单中填写的数据传递到配置的确认页，作为HTTPGET请求的一部分。 您可以添加要请求的字段的名称。 请求的格式为：

`{fieldName}={request parameter name}`

如下图所示，`param1`和`param2`作为参数传递，其值从&#x200B;**文本框**&#x200B;和&#x200B;**数字框**&#x200B;字段中复制。

您还可以&#x200B;**启用POST请求**&#x200B;并提供用于发布请求的URL。 要向托管表单的AEM服务器提交数据，请使用与AEM服务器的根路径对应的相对路径。 例如，/content/forms/af/SampleForm.html。 要向任何其他服务器提交数据，请使用绝对路径。

![配置Rest端点提交操作](assets/action-config.png)

配置Rest端点提交操作

>[!NOTE]
要将字段作为参数传递到REST URL中，所有字段必须具有不同的元素名称，即使字段位于不同的面板上也是如此。

### 将提交的数据发布到资源或外部休息端点  {#post-submitted-data-to-a-resource-or-external-rest-end-point-nbsp}

使用&#x200B;**提交到REST端点**&#x200B;操作将提交的数据发布到其余URL。 该URL可以是内部（表单所在的服务器）或外部服务器。

要将数据发布到内部服务器，请提供资源路径。 数据将发布到资源的路径。 例如，/content/restEndPoint。 对于这种帖子请求，使用提交请求的验证信息。

要向外部服务器发布数据，请提供URL。 URL的格式为https://host:port/path_to_rest_end_point。 确保配置路径以匿名处理POST请求。

![作为感谢页面参数传递的字段值的映射](assets/post-enabled-actionconfig.png)

在上面的示例中，用户在`textbox`中输入的信息是使用参数`param1`捕获的。 用于发布使用`param1`捕获的数据的语法为：

`String data=request.getParameter("param1");`

同样，用于发布XML数据和附件的参数为`dataXml`和`attachments`。

例如，您在脚本中使用这两个参数将数据解析到一个余留端点。 您使用以下语法存储和分析数据：

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

在此示例中，`data`存储XML数据，而`att`存储附件数据。

## 发送电子邮件 {#send-email}

**发送电子邮件**&#x200B;提交操作会在表单成功提交时向一个或多个收件人发送电子邮件。 生成的电子邮件可以包含预定义格式的表单数据。

>[!NOTE]
所有表单字段必须具有不同的元素名称，即使它们位于不同的面板上)，以便在电子邮件中包含表单数据。

## 通过电子邮件{#send-pdf-via-email}发送PDF

**通过电子邮件发送PDF**&#x200B;提交操作在成功提交表单时向一个或多个收件人发送包含表单数据的PDF的电子邮件。

>[!NOTE]
此提交操作适用于具有“记录”模板文档的基于XFA的自适应表单和基于XSD的自适应表单。

## 调用表单工作流{#invoke-a-forms-workflow}

**提交到Forms工作流**&#x200B;提交选项会向现有AdobeLiveCycle或JEE流程的AEM Forms发送数据xml和文件附件（如果有）。

有关如何配置“提交到表单”工作流提交操作的信息，请参阅[使用表单工作流](../../forms/using/submit-form-data-livecycle-process.md)提交和处理表单数据。

## 使用表单数据模型提交 {#submit-using-form-data-model}

**使用表单数据模型提交操作将指定数据模型对象提交的自适应表单数据以表单数据模型写入其数据源。**&#x200B;在配置提交操作时，您可以选择要将其提交数据回写到其数据源的数据模型对象。

此外，您可以使用表单数据模型和记录文档(DoR)将表单附件提交到数据源。

有关表单数据模型的信息，请参见[AEM Forms数据集成](../../forms/using/data-integration.md)。

## Forms门户提交操作{#forms-portal-submit-action}

**Forms门户提交操作**&#x200B;选项通过AEM Forms门户提供表单数据。

有关Forms门户网站和提交操作的详细信息，请参阅[草案和提交组件](../../forms/using/draft-submission-component.md)。

## 调用AEM工作流{#invoke-an-aem-workflow}

**调用AEM Workflow**&#x200B;提交操作将自适应表单与AEM Workflow关联。 提交表单后，关联的工作流会自动开始到处理节点。 此外，它还会将数据文件、附件和记录文档（如果适用）放在工作流的有效负荷位置。

在使用&#x200B;**调用AEM Workflow**&#x200B;提交操作之前，[配置AEM DS设置](../../forms/using/configuring-the-processing-server-url-.md)。 有关创建AEM工作流的信息，请参阅OSGi](../../forms/using/aem-forms-workflow.md)上的[以表单为中心的工作流。

## 自适应表单{#server-side-revalidation-in-adaptive-form}中的服务器端重新验证

通常，在任何在线数据捕获系统中，开发者都会在客户端放置一些JavaScript验证，以执行一些业务规则。 但在现代浏览器中，最终用户可以绕过这些验证，使用各种技术（如Web浏览器开发工具控制台）手动执行提交。 这种技术也适用于自适应表单。 表单开发者可以创建各种验证逻辑，但从技术上讲，最终用户可以绕过那些验证逻辑并将无效数据提交到服务器。 无效数据将破坏表单作者已实施的业务规则。

服务器端重新验证功能还提供了在服务器上设计自适应表单时运行自适应表单作者提供的验证功能。 它防止了以表单验证形式表示的数据提交和业务规则违规的任何可能危害。

### 在服务器上验证什么？{#what-to-validate-on-server-br}

自适应表单的所有现成(OOTB)字段验证都可在服务器上重新运行：

* 必填
* 验证图片子句
* 验证表达式

### 启用服务器端验证{#enabling-server-side-validation-br}

使用提要栏中自适应表单容器下的&#x200B;**在服务器上重新验证**&#x200B;启用或禁用当前表单的服务器端验证。

![启用服务器端验证](assets/revalidate-on-server.png)

启用服务器端验证

如果最终用户绕过这些验证并提交表单，服务器将再次执行验证。 如果验证在服务器结束时失败，则会停止提交事务。 最终用户再次呈现原始形式。 捕获的数据和提交的数据将作为错误呈现给用户。

### 在验证表达式{#supporting-custom-functions-in-validation-expressions-br}中支持自定义函数

有时，对于&#x200B;**复杂的验证规则**，确切的验证脚本驻留在自定义函数中，作者从字段验证表达式调用这些自定义函数。 要在执行服务器端验证时使此自定义函数库已知并可用，表单作者可以在自适应表单容器属性的&#x200B;**基本**&#x200B;选项卡下配置AEM客户端库的名称，如下所示。

![在验证表达式中支持自定义功能](assets/clientlib-cat.png)

在验证表达式中支持自定义功能

作者可以根据自适应表单配置customJavaScript库。 库中只保留可重用的函数，它依赖于jquery和endrower.js第三方库。

## 提交操作{#error-handling-on-submit-action}时出错处理

作为AEM安全和强化准则的一部分，请配置自定义错误页面，如404.jsp和500.jsp。 提交表单时，将调用这些处理函数404或500个错误。 当在“发布”节点上触发这些错误代码时，也会调用处理函数。

有关详细信息，请参阅[自定义由错误处理程序](/help/sites-developing/customizing-errorhandler-pages.md)显示的页面。
