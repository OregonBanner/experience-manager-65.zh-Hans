---
title: 配置提交操作
seo-title: Configuring the Submit action
description: Forms允许您配置提交操作以定义提交后处理自适应表单的方式。 您可以使用内置的提交操作或从头开始编写自己的提交操作。
uuid: 4368d648-88ea-4f84-a051-46296a1a084e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 9d8d7044-ffce-4ab4-9543-a2d2f9da31e3
docset: aem65
feature: Adaptive Forms
exl-id: 04efb4ad-cff6-4e05-bcd2-98102f052452
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '1870'
ht-degree: 0%

---

# 配置提交操作{#configuring-the-submit-action}

## 提交操作简介 {#introduction-to-submit-actions}

当用户单击自适应表单上的提交按钮时，会触发提交操作。 您可以在自适应表单上配置提交操作。 自适应表单提供了一些开箱即用的提交操作。 您可以复制和扩展默认提交操作以创建自己的提交操作。 但是，根据您的要求，您可以编写并注册自己的提交操作，以处理已提交表单中的数据。 提交操作可以使用 [同步或异步提交](../../forms/using/asynchronous-submissions-adaptive-forms.md).

您可以在中配置提交操作 **提交** 部分（位于侧栏中）。

![配置提交操作](assets/thank-you-setting.png)

配置提交操作

自适应表单可用的默认提交操作包括：

* 提交到REST端点
* 发送电子邮件
* 通过电子邮件发送PDF
* 调用Forms Workflow
* 使用表单数据模型提交
* Forms Portal提交操作
* 调用AEM Workflow

>[!NOTE]
>
>通过电子邮件发送PDF提交操作仅适用于使用XFA模板作为表单模型的自适应表单。

>[!NOTE]
>
>确保 [AEM_Installation_Directory]\crx-quickstart\temp\datamanager\ASM文件夹
>存在. 需要目录来临时存储附件。 如果该目录不存在，请创建它。

>[!CAUTION]
>
>如果您 [预填充](../../forms/using/prepopulate-adaptive-form-fields.md) 表单模板、表单数据模型或基于架构的自适应表单，其中XML或JSON数据投诉针对的是数据不包含的架构（XML架构、JSON架构、表单模板或表单数据模型） &lt;afdata>， &lt;afbounddata>、和 &lt;/afunbounddata> 标签后，则为无界字段的数据(无界字段为自适应表单字段，不包含 [bindref](../../forms/using/prepopulate-adaptive-form-fields.md) 属性)。

您可以为自适应表单编写自定义提交操作以满足您的用例要求。 有关更多信息，请参阅 [为自适应表单编写自定义提交操作](../../forms/using/custom-submit-action-form.md).

## 提交到REST端点 {#submit-to-rest-endpoint}

此 **提交到REST端点** 提交选项将表单中填写的数据作为HTTPGET请求的一部分传递到配置的确认页面。 您可以添加要请求的字段的名称。 请求的格式为：

`{fieldName}={request parameter name}`

如下图所示， `param1` 和 `param2` 作为参数传递，其值复制自 **文本框** 和 **数值框** 用于执行下一个操作的字段。

您还可以 **启用POST请求** 并提供用于发布请求的URL。 要将数据提交到托管表单的Experience Manager服务器，请使用与Experience Manager服务器的根路径对应的相对路径。 例如，/content/forms/af/SampleForm.html。 要向任何其他服务器提交数据，请使用绝对路径。

![配置Rest端点提交操作](assets/action-config.png)

配置Rest端点提交操作

>[!NOTE]
要在REST URL中将这些字段作为参数传递，所有字段必须具有不同的元素名称，即使这些字段位于不同的面板上也是如此。

### 将提交的数据发布到资源或外部Rest端点  {#post-submitted-data-to-a-resource-or-external-rest-end-point-nbsp}

使用 **提交到REST端点** 将提交的数据发布到rest URL的操作。 URL可以是内部（渲染表单的服务器）或外部服务器。

要将数据发布到内部服务器，请提供资源的路径。 数据被发布为资源的路径。 例如，/content/restEndPoint。 对于此类post请求，使用提交请求的身份验证信息。

要向外部服务器发布数据，请提供URL。 URL的格式为https://host:port/path_to_rest_end_point。 确保将路径配置为匿名处理POST请求。

![作为感谢页面参数传递的字段值的映射](assets/post-enabled-actionconfig.png)

在上面的示例中，用户在 `textbox` 使用参数捕获 `param1`. 用于发布使用捕获的数据的语法 `param1` 为：

`String data=request.getParameter("param1");`

同样，用于发布XML数据和附件的参数包括 `dataXml` 和 `attachments`.

例如，在脚本中使用这两个参数将数据解析到rest端点。 您可以使用以下语法来存储和解析数据：

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

在此示例中， `data` 存储XML数据，以及 `att` 存储附件数据。

## 发送电子邮件 {#send-email}

此 **发送电子邮件** 提交操作会在成功提交表单时向一个或多个收件人发送电子邮件。 生成的电子邮件可以包含预定义格式的表单数据。

>[!NOTE]
所有表单字段必须具有不同的元素名称（即使它们位于不同的面板上），才能在电子邮件中包含表单数据。

## 通过电子邮件发送PDF {#send-pdf-via-email}

此 **通过电子邮件发送PDF** 提交操作会在成功提交表单时，向一个或多个收件人发送一封包含表单数据PDF的电子邮件。

>[!NOTE]
此提交操作适用于具有记录文档模板的基于XFA的自适应表单和基于XSD的自适应表单。

## 调用Forms Workflow {#invoke-a-forms-workflow}

此 **提交到Forms Workflow** 提交选项会将数据xml和文件附件（如果有）发送到JEE流程中的现有AdobeLiveCycle或AEM Forms。

有关如何配置“提交至Forms Workflow”提交操作的信息，请参阅 [使用表单工作流提交和处理表单数据](../../forms/using/submit-form-data-livecycle-process.md).

## 使用表单数据模型提交 {#submit-using-form-data-model}

此 **使用表单数据模型提交** 提交操作将表单数据模型中指定数据模型对象的已提交自适应表单数据写入其数据源。 配置提交操作时，您可以选择提交的数据要写回其数据源的数据模型对象。

此外，您还可以使用表单数据模型和记录文档(DoR)将表单附件提交到数据源。

有关表单数据模型的信息，请参阅 [AEM Forms数据集成](../../forms/using/data-integration.md).

## Forms Portal提交操作 {#forms-portal-submit-action}

此 **Forms Portal提交操作** 选项使表单数据可通过AEM Forms门户使用。

有关Forms门户和提交操作的更多信息，请参阅 [草稿和提交组件](../../forms/using/draft-submission-component.md).

## 调用AEM Workflow {#invoke-an-aem-workflow}

此 **[!UICONTROL 调用AEM Workflow]** 提交操作将自适应表单与 [AEM Workflow](/help/sites-developing/workflows-models.md). 提交表单时，关联的工作流会在创作实例上自动启动。 可将数据文件、附件和记录文档保存到相对于工作流的文件夹，或工作流有效负荷下的文件夹，或保存到变量。 如果工作流标记为外部数据存储，则变量选项可用，而不是有效负载选项。 您可以从可用于工作流模型的变量列表中进行选择。 如果工作流在稍后阶段标记为外部数据存储，而不是在创建工作流时标记为外部数据存储，则请确保已设置所需的变量配置。

使用之前 **调用AEM Workflow** 提交操作， [配置Experience ManagerDS设置](../../forms/using/configuring-the-processing-server-url-.md). 有关创建AEM工作流的信息，请参阅 [OSGi上以表单为中心的工作流](../../forms/using/aem-forms-workflow.md).

提交操作将以下内容置于工作流的有效负荷位置。 但是，请注意，如果工作流模型标记为外部数据存储，则仅显示“变量”选项，而不显示“有效负载”选项。

* **数据文件**：它包含提交到自适应表单的数据。 您可以使用 **[!UICONTROL 数据文件路径]** 选项，用于指定文件的名称以及相对于有效负荷的文件路径。 例如， `/addresschange/data.xml` path创建一个名为的文件夹 `addresschange` 并将其相对于有效负荷放置。 您也可仅指定 `data.xml` 只发送已提交的数据而不创建文件夹层次结构。 使用变量选项，然后从可用于工作流模型的变量列表中选择变量。

>[!NOTE]
无论是否将工作流模型标记为外部数据存储，都可以使用变量。

* **附件**：您可以使用 **[!UICONTROL 附件路径]** 选项，用于指定用于存储已上载到自适应表单的附件的文件夹名称。 将创建相对于有效负荷的文件夹。 如果工作流标记为外部数据存储，请使用变量选项，并从工作流模型的可用变量列表中选择变量。

* **记录文档**：它包含为自适应表单生成的记录文档。 您可以使用 **[!UICONTROL 记录文档路径]** 用于指定记录文档文件的名称以及相对于有效负荷的文件路径的选项。 例如， `/addresschange/DoR.pdf` path创建一个名为的文件夹 `addresschange` 相对于有效负荷，并放置 `DoR.pdf` 相对于有效负荷。 您也可仅指定 `DoR.pdf` 仅保存记录文档，而不创建文件夹层次结构。 如果工作流标记为外部数据存储，请使用变量选项，并从工作流模型的可用变量列表中选择变量。

## 自适应表单中的服务器端重新验证 {#server-side-revalidation-in-adaptive-form}

通常，在任何在线数据捕获系统中，开发人员都会在客户端放置一些JavaScript验证，以实施一些业务规则。 但在现代浏览器中，最终用户能够绕过这些验证，并使用各种技术（如Web浏览器DevTools控制台）手动提交内容。 此类技术对于自适应表单也是有效的。 表单开发人员可以创建各种验证逻辑，但从技术上讲，最终用户可以绕过这些验证逻辑并将无效数据提交到服务器。 无效数据将破坏表单作者已强制执行的业务规则。

通过服务器端重新验证功能，还可以在服务器上设计自适应表单时运行自适应表单作者提供的验证。 它可防止在表单验证方面可能出现的任何数据提交和业务规则违规受损。

### 要在服务器上验证什么？ {#what-to-validate-on-server-br}

在服务器上重新运行的自适应表单的所有开箱即用(OOTB)字段验证包括：

* 必填
* 验证图片子句
* 验证表达式

### 启用服务器端验证 {#enabling-server-side-validation-br}

使用 **在服务器上重新验证** 在侧栏中的自适应表单容器下，启用或禁用当前表单的服务器端验证。

![启用服务器端验证](assets/revalidate-on-server.png)

启用服务器端验证

如果最终用户绕过这些验证并提交表单，服务器将再次执行验证。 如果验证在服务器端失败，则提交事务将停止。 最终用户将再次看到原始表单。 捕获的数据和提交的数据将作为错误呈现给用户。

>[!NOTE]
服务器端验证验证表单模型。 建议为验证创建单独的客户端库，并且不要在同一客户端库中将其与HTML样式和DOM操作等其他内容混合。

### 在验证表达式中支持自定义函数 {#supporting-custom-functions-in-validation-expressions-br}

有时，如果存在复杂的验证规则，则确切的验证脚本将驻留在自定义函数中，并且作者会从字段验证表达式中调用这些自定义函数。 要使此自定义函数库在执行服务器端验证时已知且可用，表单作者可以在下配置AEM客户端库的名称 **基本** “自适应表单容器”属性的选项卡，如下所示。

![在验证表达式中支持自定义函数](assets/clientlib-cat.png)

在验证表达式中支持自定义函数

作者可以按自适应表单配置customJavaScript库。 在库中，仅保留依赖于jquery和underscore.js第三方库的可重用函数。

## 提交操作的错误处理 {#error-handling-on-submit-action}

作为Experience Manager安全和强化指南的一部分，请配置自定义错误页面，如404.jsp和500.jsp。 在提交表单时出现404或500错误时，将调用这些处理程序。 在Publish节点上触发这些错误代码时，也会调用处理程序。

有关更多信息，请参阅 [自定义错误处理程序显示的页面](/help/sites-developing/customizing-errorhandler-pages.md).
