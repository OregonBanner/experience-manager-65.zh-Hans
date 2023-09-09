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
source-git-commit: e19a7e617bdabb678bd804cab3fea228ce19acfa
workflow-type: tm+mt
source-wordcount: '2154'
ht-degree: 51%

---

# 配置提交操作 {#configuring-the-submit-action}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html) |
| AEM 6.5 | 本文 |


## 提交操作简介 {#introduction-to-submit-actions}

当用户单击自适应表单上的提交按钮时，会触发提交操作。 您可以在自适应表单上配置提交操作。 自适应表单提供了一些现成的提交操作。 您可以复制和扩展默认提交操作以创建自己的提交操作。 但是，根据您的要求，您可以编写并注册自己的提交操作，以处理已提交表单中的数据。 提交操作可以使用 [同步或异步提交](../../forms/using/asynchronous-submissions-adaptive-forms.md).

您可以在中配置提交操作 **提交** 侧边栏中的自适应表单容器属性部分。

![配置提交操作](assets/thank-you-setting.png)

配置提交操作

自适应表单可用的默认提交操作包括：

* 提交到 REST 端点
* 发送电子邮件
* 通过电子邮件发送PDF
* 调用Forms Workflow
* 使用表单数据模型提交
* Forms Portal提交操作
* 调用AEM工作流
* 提交至 Power Automate

>[!NOTE]
>
>通过电子邮件发送PDF提交操作仅适用于使用XFA模板作为表单模型的自适应表单。

>[!NOTE]
>
>确保 [AEM_Installation_Directory]\crx-quickstart\temp\datamanager\ASM文件夹
>存在. 临时存储附件需要目录。 如果该目录不存在，请创建它。

>[!CAUTION]
>
>如果您 [预填充](../../forms/using/prepopulate-adaptive-form-fields.md) 表单模板、表单数据模型或基于架构的自适应表单，针对不包含数据的架构（XML架构、JSON架构、表单模板或表单数据模型）提出XML或JSON数据投诉 &lt;afdata>， &lt;afbounddata>、和 &lt;/afunbounddata> 标记后，则无绑定字段的数据(无绑定字段是自适应表单字段，不包括 [bindref](../../forms/using/prepopulate-adaptive-form-fields.md) 属性)。

您可以为自适应表单编写自定义提交操作以满足您的用例要求。 有关更多信息，请参阅 [编写自适应表单的自定义提交操作](../../forms/using/custom-submit-action-form.md).

## 提交到 REST 端点 {#submit-to-rest-endpoint}

此 **提交到REST端点** 提交选项将表单中填写的数据作为HTTPGET请求的一部分传递到配置的确认页面。 您可以添加要请求的字段的名称。请求的格式为：

`{fieldName}={request parameter name}`

如下图所示， `param1` 和 `param2` 作为参数传递，其值复制自 **文本框** 和 **数值框** 用于执行下一个操作的字段。

您也可以&#x200B;**启用 POST 请求**&#x200B;并提供用于发布请求的 URL。要将数据提交到托管表单的Experience Manager服务器，请使用与Experience Manager服务器的根路径对应的相对路径。 例如，/content/forms/af/SampleForm.html。 要将数据提交到任何其他服务器，请使用绝对路径。

![配置 REST 端点提交操作](assets/action-config.png)

配置 REST 端点提交操作

>[!NOTE]
>
要将字段作为 REST URL 中的参数传递，所有字段都必须具有不同的元素名称，即使这些字段位于不同的面板上也是如此。

### 将提交的数据发布到资源或外部Rest端点  {#post-submitted-data-to-a-resource-or-external-rest-end-point-nbsp}

使用&#x200B;**提交到 REST 端点**&#x200B;操作将提交的数据发布到 REST URL。该 URL 可以属于内部服务器（呈现表单的服务器）或外部服务器。

要将数据发布到内部服务器，请提供资源的路径。数据将发布到资源的路径。例如，/content/restEndPoint。对于此类 POST 请求，将使用提交请求的身份验证信息。

要将数据发布到外部服务器，请提供 URL。URL的格式为https://host:port/path_to_rest_end_point。 确保配置以匿名方式处理 POST 请求的路径。

![作为感谢页面参数传递的字段值的映射](assets/post-enabled-actionconfig.png)

在上面的示例中，使用参数 `param1` 捕获用户在 `textbox` 中输入的信息。用于发布使用 `param1` 捕获的数据的语法为：

`String data=request.getParameter("param1");`

同样，用于发布 XML 数据和附件的参数为 `dataXml` 和 `attachments`。

例如，您在脚本中使用这两个参数来解析传输到 REST 端点的数据。您使用以下语法来存储和解析数据：

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

在此示例中，`data` 存储 XML 数据，`att` 存储附件数据。

## 发送电子邮件 {#send-email}

此 **发送电子邮件** 提交操作会在成功提交表单时向一个或多个收件人发送电子邮件。 生成的电子邮件可以包含预定义格式的表单数据。

>[!NOTE]
>
所有表单字段必须具有不同的元素名称（即使它们位于不同的面板上），才能在电子邮件中包含表单数据。

## 通过电子邮件发送PDF {#send-pdf-via-email}

此 **通过电子邮件发送PDF** 提交操作会在成功提交表单时，向一个或多个收件人发送一封包含表单数据PDF的电子邮件。

>[!NOTE]
>
此提交操作适用于具有记录文档模板的基于XFA的自适应表单和基于XSD的自适应表单。

## 调用Forms Workflow {#invoke-a-forms-workflow}

此 **提交到Forms Workflow** 提交选项会将数据xml和文件附件（如果有）发送到JEE流程中的现有AdobeLiveCycle或AEM Forms。

有关如何配置“提交至Forms Workflow”提交操作的信息，请参阅 [使用表单工作流提交和处理表单数据](../../forms/using/submit-form-data-livecycle-process.md).

## 使用表单数据模型提交 {#submit-using-form-data-model}

此 **使用表单数据模型提交** 提交操作将表单数据模型中指定数据模型对象的已提交自适应表单数据写入其数据源。 配置提交操作时，您可以选择提交的数据要写回其数据源的数据模型对象。

此外，您可以使用表单数据模型和记录文档(DoR)将表单附件提交到数据源。

有关表单数据模型的信息，请参阅 [AEM Forms数据集成](../../forms/using/data-integration.md).

## Forms Portal提交操作 {#forms-portal-submit-action}

此 **Forms Portal提交操作** 选项通过AEM Forms门户提供表单数据。

有关Forms门户和提交操作的更多信息，请参阅 [草稿和提交组件](../../forms/using/draft-submission-component.md).

## 调用 AEM 工作流 {#invoke-an-aem-workflow}

**[!UICONTROL 调用 AEM 工作流]**&#x200B;提交操作将自适应表单与 [AEM 工作流](/help/sites-developing/workflows-models.md)相关联。在提交表单时，关联的工作流将在创作实例上自动启动。可将数据文件、附件和记录文档保存到相对于工作流的文件夹，或工作流有效负荷下的文件夹，或保存到变量中。 如果工作流标记为外部数据存储，则变量选项可用，而不是有效负载选项。 您可以从可用于工作流模型的变量的列表中进行选择。如果在稍后阶段而不是在创建工作流时为外部数据存储标记了工作流，请确保所需的变量配置已到位。

在使用之前 **调用AEM工作流** 提交操作， [配置Experience ManagerDS设置](../../forms/using/configuring-the-processing-server-url-.md). 有关创建AEM工作流的信息，请参阅 [OSGi上以表单为中心的工作流](../../forms/using/aem-forms-workflow.md).

提交操作将以下内容置于工作流的有效负荷位置。 但是，请注意，如果工作流模型标记为外部数据存储，则仅显示“变量”选项，而不显示“有效负载”选项。

* **数据文件**：它包含已提交到自适应表单的数据。您可以使用&#x200B;**[!UICONTROL 数据文件路径]**&#x200B;选项来指定文件名和相对于负载的文件路径。例如，`/addresschange/data.xml` 路径会创建一个名为 `addresschange` 的文件夹，并将它放置在负载的相对位置。您也可以仅指定 `data.xml` 以仅发送提交的数据而不创建文件夹层次结构。使用变量选项，并从可用于工作流模型的变量列表中选择变量。

>[!NOTE]
>
无论是否将工作流模型标记为外部数据存储，都可以使用变量。

* **附件**：您可以使用&#x200B;**[!UICONTROL 附件路径]**&#x200B;选项指定用于存储已上传到自适应表单的附件的文件夹名称。该文件夹是相对于负载创建的。如果为外部数据存储标记了工作流，请使用变量选项，并从对工作流模型可用的变量列表中选择变量。

* **记录文档**：它包含为自适应表单生成的记录文档。您可以使用&#x200B;**[!UICONTROL 记录文档路径]**&#x200B;选项来指定记录文档的文件名以及相对于负载的文件路径。例如，`/addresschange/DoR.pdf` 路径将创建一个相对于负载的名为 `addresschange` 的文件夹，并相对于负载放置 `DoR.pdf`。您也可以仅指定 `DoR.pdf` 以仅保存记录文档而不创建文件夹层次结构。如果为外部数据存储标记了工作流，请使用变量选项，并从对工作流模型可用的变量列表中选择变量。

## 提交至 Power Automate {#microsoft-power-automate}

您可以配置自适应表单以在提交时运行Microsoft® Power Automate Cloud Flow。 配置的自适应表单将捕获的数据、附件和记录文档发送到 Power Automate Cloud Flow 进行处理。它可帮助您构建自定义数据捕获体验，同时利用 Microsoft® Power Automate 的强大功能围绕捕获的数据构建业务逻辑并自动执行客户工作流。以下几个示例说明了在将自适应表单与 Microsoft® Power Automate 集成后可执行的操作：

* 在 Power Automate 业务流程中使用自适应表单数据
* 使用 Power Automate 将捕获的数据发送到 500 多个数据源或任何公开可用的 API
* 对捕获的数据执行复杂计算
* 按预定义的计划将自适应表单数据保存到存储系统

自适应Forms编辑器提供 **调用Microsoft® Power Automate流** 提交操作以将自适应表单数据、附件和记录文档发送到Power Automate Cloud Flow。 要使用Submit操作将捕获的数据发送到Microsoft®Power Automate， [将AEM Forms实例与Microsoft®Power Automate连接](/help/forms/using/forms-microsoft-power-automate-integration.md)

在成功配置后，使用[调用 Microsoft® Power Automate 流程](/help/forms/using/forms-microsoft-power-automate-integration.md#use-the-invoke-a-microsoft&reg;-power-automate-flow-submit-action-to-send-data-to-a-power-automate-flow-use-the-invoke-microsoft-power-automate-flow-submit-action)提交操作将数据发送到 Power Automate Flow。

## 自适应表单中的服务器端重新验证 {#server-side-revalidation-in-adaptive-form}

通常，在任何在线数据捕获系统中，开发人员都会在客户端放置一些 JavaScript 验证来强制实施一些业务规则。但在现代浏览器中，最终用户有办法绕过这些验证，并使用各种技术（例如，Web Browser DevTools Console）手动进行提交。此类技术对于自适应表单也是有效的。 尽管表单开发人员可以创建各种验证逻辑，但从技术上讲，最终用户可以绕过这些验证逻辑并向服务器提交无效数据。无效数据会破坏表单作者强制实施的业务规则。

服务器端重新验证功能还支持在服务器上设计自适应表单时运行自适应表单作者提供的验证。 这可防止任何可能的数据提交损害和与表单验证相关的业务规则违反情况。

### 在服务器上进行哪些验证？ {#what-to-validate-on-server-br}

在服务器上重新运行的自适应表单的所有现成(OOTB)字段验证包括：

* 必填
* 验证图片子句
* 验证表达式

### 启用服务器端验证 {#enabling-server-side-validation-br}

使用边栏中自适应表单容器下方的&#x200B;**在服务器上重新验证**，可以为当前表单启用或禁用服务器端验证。

![启用服务器端验证](assets/revalidate-on-server.png)

启用服务器端验证

如果最终用户绕过这些验证并提交表单，服务器将重新执行验证。如果服务器端验证失败，则将停止提交事务。最终用户将再次看到原始表单。捕获的数据和提交的数据将作为错误呈现给用户。

>[!NOTE]
>
服务器端验证将验证表单模型。建议为验证创建单独的客户端库，不要将其与同一客户端库中的HTML样式和DOM操作等其他内容混合。

### 支持验证表达式中的自定义函数 {#supporting-custom-functions-in-validation-expressions-br}

有时，如果存在复杂的验证规则，则准确的验证脚本驻留在自定义函数中，并且作者从字段验证表达式中调用这些自定义函数。要在执行服务器端验证时使此自定义函数库已知并可用，表单作者可以在自适应表单容器属性的&#x200B;**基本**&#x200B;选项卡下配置 AEM 客户端库的名称，如下所示。

![支持验证表达式中的自定义函数](assets/clientlib-cat.png)

支持验证表达式中的自定义函数

作者可以按自适应表单配置customJavaScript库。 该库中只保留可重用的函数，这些函数依赖 jquery 和 underscore.js 第三方库。

## 提交操作的错误处理 {#error-handling-on-submit-action}

作为Experience Manager安全和强化指南的一部分，请配置自定义错误页面，如404.jsp和500.jsp。 提交表单时出现404或500错误时，将调用这些处理程序。 在发布节点上触发这些错误代码时，也将调用处理程序。

有关更多信息，请参阅 [自定义错误处理程序显示的页面](/help/sites-developing/customizing-errorhandler-pages.md).
