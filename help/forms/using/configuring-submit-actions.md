---
title: 配置提交操作
seo-title: Configuring the Submit action
description: Forms允许您配置提交操作，以定义提交后如何处理自适应表单。 您可以使用内置的提交操作，也可以从头开始编写您自己的提交操作。
uuid: 4368d648-88ea-4f84-a051-46296a1a084e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 9d8d7044-ffce-4ab4-9543-a2d2f9da31e3
docset: aem65
feature: Adaptive Forms
exl-id: 04efb4ad-cff6-4e05-bcd2-98102f052452
source-git-commit: d9608d584e822accc0c198fcf1d1b706d065938e
workflow-type: tm+mt
source-wordcount: '1870'
ht-degree: 0%

---

# 配置提交操作{#configuring-the-submit-action}

## 提交操作简介 {#introduction-to-submit-actions}

当用户单击自适应表单上的“提交”按钮时，会触发提交操作。 您可以在自适应表单上配置提交操作。 自适应表单提供了一些现成的提交操作。 您可以复制和扩展默认的提交操作，以创建您自己的提交操作。 但是，根据您的要求，您可以编写并注册您自己的提交操作，以处理已提交表单中的数据。 提交操作可使用 [同步或异步提交](../../forms/using/asynchronous-submissions-adaptive-forms.md).

您可以在 **提交** 自适应表单容器属性的部分。

![配置提交操作](assets/thank-you-setting.png)

配置提交操作

自适应表单可用的默认提交操作包括：

* 提交到REST端点
* 发送电子邮件
* 通过电子邮件发送PDF
* 调用Forms Workflow
* 使用表单数据模型提交
* Forms Portal提交操作
* 调用AEM工作流

>[!NOTE]
>
>通过电子邮件提交操作发送PDF仅适用于使用XFA模板作为表单模型的自适应表单。

>[!NOTE]
>
>确保 [AEM_Installation_Directory]\crx-quickstart\temp\datamanager\ASM folder
>存在. 临时存储附件需要目录。 如果目录不存在，请创建该目录。

>[!CAUTION]
>
>如果您 [预填充](../../forms/using/prepopulate-adaptive-form-fields.md) 表单模板、表单数据模型或基于模式的自适应表单，其中包含XML或JSON数据，抱怨某个架构（XML架构、JSON架构、表单模板或表单数据模型）的数据不包含 &lt;afdata>, &lt;afbounddata>和 &lt;/afunbounddata> 标记，则无界字段的数据(无界字段是没有 [宾德雷夫](../../forms/using/prepopulate-adaptive-form-fields.md) 属性)。

您可以为自适应表单编写自定义提交操作以完成用例。 有关更多信息，请参阅 [为自适应表单编写自定义提交操作](../../forms/using/custom-submit-action-form.md).

## 提交到REST端点 {#submit-to-rest-endpoint}

的 **提交到REST端点** 提交选项会将表单中填写的数据传递到配置的确认页面，以作为HTTPGET请求的一部分。 您可以添加要请求的字段名称。 请求的格式为：

`{fieldName}={request parameter name}`

如下图所示， `param1` 和 `param2` 将作为参数进行传递，并且值复制自 **文本框** 和 **数字框** 字段。

您还可以 **启用POST请求** 和提供用于发布请求的URL。 要向托管表单的Experience Manager服务器提交数据，请使用与Experience Manager服务器的根路径对应的相对路径。 例如， /content/forms/af/SampleForm.html。 要向任何其他服务器提交数据，请使用绝对路径。

![配置Rest端点提交操作](assets/action-config.png)

配置Rest端点提交操作

>[!NOTE]
要在REST URL中将字段作为参数传递，所有字段必须具有不同的元素名称，即使这些字段放置在不同的面板上也是如此。

### 将提交的数据发布到资源或外部休息端点  {#post-submitted-data-to-a-resource-or-external-rest-end-point-nbsp}

使用 **提交到REST端点** 操作将提交的数据发布到rest URL。 URL可以是内部服务器（呈现表单的服务器）或外部服务器。

要将数据发布到内部服务器，请提供资源的路径。 数据将发布到资源的路径中。 例如， /content/restEndPoint。 对于这种帖子请求，使用提交请求的验证信息。

要将数据发布到外部服务器，请提供URL。 URL的格式为https://host:port/path_to_rest_end_point。 确保以匿名方式配置路径以处理POST请求。

![作为感谢页面参数传递的字段值的映射](assets/post-enabled-actionconfig.png)

在上例中，用户在 `textbox` 使用参数捕获 `param1`. 用于发布使用 `param1` 为：

`String data=request.getParameter("param1");`

同样，用于发布XML数据和附件的参数也是 `dataXml` 和 `attachments`.

例如，在脚本中使用这两个参数将数据解析到其余的端点。 使用以下语法来存储和解析数据：

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

在本例中， `data` 存储XML数据， `att` 存储附件数据。

## 发送电子邮件 {#send-email}

的 **发送电子邮件** 成功提交表单后，提交操作会向一个或多个收件人发送电子邮件。 生成的电子邮件可以包含预定义格式的表单数据。

>[!NOTE]
所有表单字段必须具有不同的元素名称，即使它们位于不同的面板中也是如此)，以便在电子邮件中包含表单数据。

## 通过电子邮件发送PDF {#send-pdf-via-email}

的 **通过电子邮件发送PDF** 提交操作会在成功提交表单时，向一个或多个收件人发送一封包含表单数据的PDF的电子邮件。

>[!NOTE]
此提交操作适用于基于XFA的自适应表单和具有记录文档模板的基于XSD的自适应表单。

## 调用Forms Workflow {#invoke-a-forms-workflow}

的 **提交到Forms Workflow** 提交选项会向JEE进程上的现有AdobeLiveCycle或AEM Forms发送数据xml和文件附件（如果有）。

有关如何配置提交到Forms Workflow提交操作的信息，请参阅 [使用表单工作流提交和处理表单数据](../../forms/using/submit-form-data-livecycle-process.md).

## 使用表单数据模型提交 {#submit-using-form-data-model}

的 **使用表单数据模型提交** 提交操作将表单数据模型中指定数据模型对象提交的自适应表单数据写入其数据源。 在配置提交操作时，您可以选择要将其提交的数据写回其数据源的数据模型对象。

此外，您还可以使用表单数据模型和记录文档(DoR)将表单附件提交到数据源。

有关表单数据模型的信息，请参阅 [AEM Forms数据集成](../../forms/using/data-integration.md).

## Forms Portal提交操作 {#forms-portal-submit-action}

的 **Forms Portal提交操作** 选项可通过AEM Forms门户使表单数据可用。

有关Forms Portal和提交操作的更多信息，请参阅 [草稿和提交组件](../../forms/using/draft-submission-component.md).

## 调用AEM工作流 {#invoke-an-aem-workflow}

的 **[!UICONTROL 调用AEM工作流]** 提交操作将自适应表单与 [AEM Workflow](/help/sites-developing/workflows-models.md). 提交表单后，关联的工作流将自动在创作实例上启动。 您可以将数据文件、附件和记录文档保存到相对文件夹或工作流有效负荷下的文件夹或变量中。 如果为外部数据存储标记了工作流，则变量选项将可用，而不是有效负荷选项。 您可以从可用于工作流模型的变量列表中进行选择。 如果在以后阶段而不是在创建工作流时将工作流标记为外部数据存储，请确保已设置所需的变量配置。

在使用 **调用AEM工作流** 提交操作， [配置Experience ManagerDS设置](../../forms/using/configuring-the-processing-server-url-.md). 有关创建AEM工作流的信息，请参阅 [OSGi上以表单为中心的工作流](../../forms/using/aem-forms-workflow.md).

提交操作会将以下内容放在工作流的有效负荷位置。 但是，请注意，如果为外部数据存储标记了工作流模型，而不是有效负荷选项，则仅会显示“变量”选项。

* **数据文件**:它包含提交到自适应表单的数据。 您可以使用 **[!UICONTROL 数据文件路径]** 选项，以指定文件的名称和相对于有效负载的文件路径。 例如， `/addresschange/data.xml` 路径会创建名为 `addresschange` 并将其放置在有效载荷上。 您还可以仅指定 `data.xml` ，以便在不创建文件夹层次结构的情况下仅发送提交的数据。 使用变量选项，然后从可用于工作流模型的变量列表中选择变量。

>[!NOTE]
无论是否标记了工作流模型以用于外部数据存储，都可以使用变量。

* **附件**:您可以使用 **[!UICONTROL 附件路径]** 选项，以指定用于存储上传到自适应表单的附件的文件夹名称。 文件夹是相对于有效负载创建的。 如果工作流标记为外部数据存储，请使用变量选项，然后从可用于工作流模型的变量列表中选择变量。

* **记录文档**:它包含为自适应表单生成的记录文档。 您可以使用 **[!UICONTROL 记录路径文档]** 选项，指定记录文档的名称和相对于有效负荷的文件路径。 例如， `/addresschange/DoR.pdf` 路径会创建名为 `addresschange` 相对于有效负载，并将 `DoR.pdf` 相对于有效载荷。 您还可以仅指定 `DoR.pdf` 以仅保存记录文档，而不创建文件夹层次结构。 如果工作流标记为外部数据存储，请使用变量选项，然后从可用于工作流模型的变量列表中选择变量。

## 自适应表单中的服务器端重新验证 {#server-side-revalidation-in-adaptive-form}

通常，在任何在线数据捕获系统中，开发人员会在客户端放置一些JavaScript验证，以强制执行一些业务规则。 但在现代浏览器中，最终用户可以绕过这些验证，使用各种技术（如Web浏览器开发工具控制台）手动执行提交。 这种技术对于自适应表单也是有效的。 表单开发人员可以创建各种验证逻辑，但从技术上讲，最终用户可以绕过这些验证逻辑，将无效数据提交到服务器。 无效数据会破坏表单作者强制执行的业务规则。

服务器端重新验证功能还允许运行自适应表单作者在服务器上设计自适应表单时提供的验证。 它可防止在表单验证中表示的数据提交和业务规则违规的任何潜在危害。

### 在服务器上验证什么？ {#what-to-validate-on-server-br}

自适应表单的开箱即用(OOTB)字段验证（将在服务器中重新运行）包括：

* 必填
* 验证图片子句
* 验证表达式

### 启用服务器端验证 {#enabling-server-side-validation-br}

使用 **在服务器上重新验证** 在侧栏的自适应表单容器下，启用或禁用当前表单的服务器端验证。

![启用服务器端验证](assets/revalidate-on-server.png)

启用服务器端验证

如果最终用户绕过这些验证并提交表单，服务器将再次执行验证。 如果验证在服务器端失败，则提交事务将停止。 最终用户将再次看到原始表单。 捕获的数据和提交的数据将作为错误呈现给用户。

>[!NOTE]
服务器端验证可验证表单模型。 建议为验证创建单独的客户端库，但不要将其与HTML样式和DOM操作等其他内容混合到同一客户端库中。

### 在验证表达式中支持自定义函数 {#supporting-custom-functions-in-validation-expressions-br}

有时，如果存在复杂的验证规则，则确切的验证脚本将驻留在自定义函数中，并且作者会从字段验证表达式中调用这些自定义函数。 要在执行服务器端验证时将此自定义函数库知晓并可用，表单作者可以在 **基本** 自适应表单容器属性的选项卡，如下所示。

![在验证表达式中支持自定义函数](assets/clientlib-cat.png)

在验证表达式中支持自定义函数

作者可以根据自适应表单配置customJavaScript库。 在库中，仅保留依赖于jquery和undersore.js第三方库的可重用函数。

## 处理提交操作时出错 {#error-handling-on-submit-action}

作为Experience Manager安全和强化准则的一部分，请配置自定义错误页，如404.jsp和500.jsp。 在提交表单时，会调用这些处理程序404或500错误。 当在“发布”节点上触发这些错误代码时，也会调用处理程序。

有关更多信息，请参阅 [自定义错误处理程序显示的页面](/help/sites-developing/customizing-errorhandler-pages.md).
