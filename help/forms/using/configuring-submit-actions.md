---
title: 配置提交操作
seo-title: 配置提交操作
description: AEM表单允许您配置提交操作以定义在提交后如何处理自适应表单。 您可以使用内置提交操作或从头开始编写您自己的操作。
seo-description: AEM表单允许您配置提交操作以定义在提交后如何处理自适应表单。 您可以使用内置提交操作或从头开始编写您自己的操作。
uuid: 4368d648-88ea-4f84-a051-46296a1a084e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 9d8d7044-ffce-4ab4-9543-a2d2f9da31e3
docset: aem65
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# 配置提交操作{#configuring-the-submit-action}

## 提交操作简介 {#introduction-to-submit-actions}

当用户单击自适应表单上的“提交”按钮时，将触发提交操作。 您可以在自适应表单上配置提交操作。 自适应表单提供了一些现成的提交操作。 您可以复制和扩展默认的提交操作，以创建您自己的提交操作。 但是，根据您的要求，您可以编写并注册自己的提交操作以处理提交表单中的数据。 提交操作可以使用同 [步或异步提交](../../forms/using/asynchronous-submissions-adaptive-forms.md)。

您可以在提要栏中自适应表单 **容器属性** 的“提交”部分配置提交操作。

![配置提交操作](assets/thank-you-setting.png)

配置提交操作

自适应表单的默认提交操作包括：

* 提交到REST端点
* 发送电子邮件
* 通过电子邮件发送PDF
* 调用表单工作流
* 使用表单数据模型提交
* Forms Portal提交操作
* 调用AEM工作流

>[!NOTE]
>
>通过电子邮件发送PDF提交操作仅适用于使用XFA模板作为表单模型的自适应表单。

>[!NOTE]
>
>确保 [AEM_Installation_Directory]\crx-quickstart\temp\datamanager\ASM folder
>存在. 临时存储附件时需要该目录。 如果目录不存在，请创建它。

>[!CAUTION]
>
>如果预填表 [单模板](../../forms/using/prepopulate-adaptive-form-fields.md) 、表单数据模型或基于模式的自适应表单 [，并且XML或JSON数据会向数据不包含&lt;afData>、&lt;afBoundData>和&lt;/afUnboundData>标签的模式(XML模式、JSON模式、表单模板或表单数据模型)投诉，则无界数据自适应表单的字段(无界字段是没有bindref属](../../forms/using/prepopulate-adaptive-form-fields.md) 性的自适应表单字段)将丢失。

您可以为自适应表单编写自定义提交操作以满足您的使用案例。 有关详细信息，请参 [阅编写自适应表单的自定义提交操作](../../forms/using/custom-submit-action-form.md)。

## 提交到REST端点 {#submit-to-rest-endpoint}

“提 **交到REST端点** ”提交选项将表单中填写的数据作为HTTP GET请求的一部分传递到已配置的确认页。 您可以添加要请求的字段的名称。 请求的格式为：

`{fieldName}={request parameter name}`

如下图所示，并作为参数 `param1` 传递， `param2` 这些参数的值从文本框和数字框字段中复 **制** , **** 以便执行下一个操作。

您还可以 **启用POST请求** ，并提供用于发布请求的URL。 要向承载表单的AEM服务器提交数据，请使用与AEM服务器的根路径相对应的相对路径。 例如，/content/forms/af/SampleForm.html。 要向任何其他服务器提交数据，请使用绝对路径。

![配置Rest端点提交操作](assets/action-config.png)

配置Rest端点提交操作

>[!NOTE]
要将字段作为参数传递到REST URL中，所有字段必须具有不同的元素名称，即使这些字段位于不同的面板上也是如此。

### 将提交的数据发布到资源或外部休息端点 {#post-submitted-data-to-a-resource-or-external-rest-end-point-nbsp}

使用“ **提交到REST端点** ”动作将提交的数据发布到REST URL。 该URL可以是内部（在其上渲染表单的服务器）或外部服务器。

要将数据发布到内部服务器，请提供资源的路径。 数据将发布到资源的路径。 例如，/content/restEndPoint。 对于这种发布请求，使用提交请求的验证信息。

要将数据发布到外部服务器，请提供URL。 URL的格式为https://host:port/path_to_rest_end_point。 确保配置路径以匿名处理POST请求。

![作为感谢页面参数传递的字段值的映射](assets/post-enabled-actionconfig.png)

在上面的示例中，用户在中输入的信息 `textbox` 是使用参数捕获的 `param1`。 用于发布使用以下方式捕获的数据的 `param1` 语法：

`String data=request.getParameter("param1");`

同样，用于发布XML数据和附件的参数也是 `dataXml` 和 `attachments`。

例如，您使用脚本中的这两个参数将数据解析到一个剩余端点。 使用以下语法存储和分析数据：

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

在本例中，存 `data` 储XML数据，并存储 `att` 附件数据。

## 发送电子邮件 {#send-email}

“发 **送电子邮件** ”提交操作会在表单成功提交时向一个或多个收件人发送电子邮件。 生成的电子邮件可以包含预定义格式的表单数据。

>[!NOTE]
所有表单字段必须具有不同的元素名称（即使它们位于不同的面板上），以便在电子邮件中包含表单数据。

## Send PDF via Email {#send-pdf-via-email}

“通 **过电子邮件发送PDF** ”提交操作会在成功提交表单时向一个或多个收件人发送一封包含表单数据的PDF的电子邮件。

>[!NOTE]
此提交操作适用于具有“记录”模板文档的基于XFA的自适应表单和基于XSD的自适应表单。

## Invoke a forms workflow {#invoke-a-forms-workflow}

“提 **交到表单”工作流程提交选项** ，可将数据xml和文件附件（如果有）发送到JEE上的现有Adobe LiveCycle或AEM Forms进程。

有关如何配置提交到表单工作流提交操作的信息，请参阅 [使用表单工作流提交和处理表单数据](../../forms/using/submit-form-data-livecycle-process.md)。

## 使用表单数据模型提交 {#submit-using-form-data-model}

“使 **用表单数据模型提交** ”动作将指定数据模型对象在表单数据模型中提交的自适应表单数据写入其数据源。 在配置提交操作时，您可以选择其提交数据要写回其数据源的数据模型对象。

此外，您还可以使用表单数据模型和记录文档(DoR)向数据源提交表单附件。

有关表单数据模型的信息，请参 [阅AEM表单数据集成](../../forms/using/data-integration.md)。

## Forms Portal提交操作 {#forms-portal-submit-action}

“表 **单门户提交操作** ”选项使表单数据可通过AEM Forms门户访问。

有关Forms Portal和提交操作的详细信息，请参阅草 [稿和提交组件](../../forms/using/draft-submission-component.md)。

## Invoke an AEM Workflow {#invoke-an-aem-workflow}

调用 **** AEM工作流提交操作将自适应表单与AEM工作流相关联。 提交表单后，关联的工作流会自动开始到处理节点。 此外，它还会将数据文件、附件和记录文档（如果适用）放在工作流的有效负荷位置。

在使用调 **用AEM Workflow提交操作之前** ，请 [配置AEM DS设置](../../forms/using/configuring-the-processing-server-url-.md)。 有关创建AEM工作流的信息，请参 [阅OSGi上以表单为中心的工作流](../../forms/using/aem-forms-workflow.md)。

## 自适应表单中的服务器端重新验证 {#server-side-revalidation-in-adaptive-form}

通常，在任何在线数据捕获系统中，开发人员都会在客户端放置一些javascript验证以执行一些业务规则。 但在现代浏览器中，最终用户可以绕过这些验证，使用各种技术手动执行提交，如Web浏览器开发工具控制台。 这些技术也适用于自适应表单。 表单开发者可以创建各种验证逻辑，但从技术上讲，终端用户可以绕过这些验证逻辑，将无效数据提交到服务器。 无效数据将破坏表单作者已实施的业务规则。

服务器端重新验证功能还允许运行自适应表单作者在服务器上设计自适应表单时提供的验证。 它防止了在表单验证中表示的数据提交和违反业务规则的任何可能的折衷。

### 在服务器上验证什么？ {#what-to-validate-on-server-br}

自适应表单的所有开箱即用(OOTB)字段验证在服务器上重新运行：

* 必填
* 验证图片子句
* 验证表达式

### 启用服务器端验证 {#enabling-server-side-validation-br}

使用提要 **栏中自适应表单容器下的“在服务器上重新验证** ”，启用或禁用当前表单的服务器端验证。

![启用服务器端验证](assets/revalidate-on-server.png)

启用服务器端验证

如果最终用户绕过了这些验证并提交了表单，服务器将再次执行验证。 如果验证在服务器端失败，则会停止提交事务。 最终用户再次呈现原始表单。 捕获的数据和提交的数据将作为错误呈现给用户。

### 在验证表达式中支持自定义功能 {#supporting-custom-functions-in-validation-expressions-br}

有时，如果存在复杂的验 **证规则**，则精确验证脚本驻留在自定义函数中，作者从字段验证表达式调用这些自定义函数。 要在执行服务器端验证时使此自定义函数库为已知和可用，表单作者可以在自适应表单容器属性的“基本 **** ”选项卡下配置AEM客户端库的名称，如下所示。

![在验证表达式中支持自定义功能](assets/clientlib-cat.png)

在验证表达式中支持自定义功能

作者可以根据自适应表单配置自定义javascript库。 在库中，只保留可重用的函数，该函数依赖于jquery和endworker.js第三方库。

## 提交操作时出错处理 {#error-handling-on-submit-action}

作为AEM安全性和强化准则的一部分，请配置自定义错误页面，如404.jsp和500.jsp。 在提交表单时，将调用这些处理函数404或500个错误。 当在“发布”节点上触发这些错误代码时，也会调用处理函数。

有关详细信息，请参 [阅自定义由错误处理程序显示的页面](/help/sites-developing/customizing-errorhandler-pages.md)。
