---
title: 自适应表单的标准验证错误消息
seo-title: Standard validation error messages for adaptive forms
description: 使用自定义错误处理程序将自适应表单的验证错误消息转换为标准格式
seo-description: Transform the validation error messages for adaptive forms into standard format using custom error handlers
uuid: 0d1f9835-3e28-41d3-a3b1-e36d95384328
contentOwner: anujkapo
content-type: reference
keywords: 添加自定义错误处理程序、添加默认错误处理程序、在表单中添加错误处理程序、使用规则编辑器的调用服务添加自定义错误处理程序、配置规则编辑器以添加自定义错误处理程序、使用规则编辑器添加自定义错误处理程序
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
discoiquuid: ec062567-1c6b-497b-a1e7-1dbac2d60852
feature: Adaptive Forms
exl-id: 54a76d5c-d19b-4026-b71c-7b9e862874bc
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '2357'
ht-degree: 86%

---

# 自适应Forms中的错误处理程序 {#error-handlers-in-adaptive-form}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/add-custom-error-handler-adaptive-forms.html) |
| AEM 6.5 | 本文 |


AEM Forms 为表单提交提供现成的成功和错误处理程序。它还提供用于自定义错误处理函数的功能。例如，可在后端为特定的错误代码调用自定义工作流或通知客户服务已停止。处理程序是根据服务器响应执行的客户端函数。在使用 API 调用外部服务时，数据会传输到服务器以进行验证，这会向客户端返回响应，其中包含有关提交的成功或错误事件的信息。该信息作为参数传递给相关处理程序以执行该函数。错误处理程序可帮助管理和显示遇到的错误或验证问题。

![错误处理程序工作流，用于了解如何在表单中添加自定义错误处理程序](/help/forms/using/assets/error-handler-workflow.png)

自适应表单根据预设验证标准验证您在字段中提供的输入，并检查为调用外部服务而配置的 REST 端点所返回的各种错误。您可以根据用于自适应表单的数据源设置验证标准。例如，如果您使用 RESTful Web 服务作为数据源，则可以在 Swagger 定义文件中定义验证标准。

如果输入值满足验证标准，则将值提交到数据源，否则自适应表单将使用错误处理程序显示错误消息。与此方法类似，自适应表单与自定义错误处理程序集成以执行数据验证。如果输入值未满足验证标准，错误消息将在自适应表单的字段级别显示。当服务器返回的验证错误消息采用标准消息格式时，会发生此情况。


## 错误处理程序的用途 {#uses-of-error-handler}

错误处理程序具有多种用途。下面列出了错误处理程序函数的一些用途：
* **执行验证**：错误处理首先根据预定义的规则或标准验证用户输入。当用户填写自适应表单时，错误处理程序会验证输入，确保其满足所需的格式、长度或任何其他约束。

* **提供实时反馈**：当检测到任何错误时，错误处理程序会立即向用户显示反馈，例如相应表单字段下方的内联错误消息。此反馈可帮助用户识别和纠正错误，而无需提交表单并等待响应。


* **显示错误信息**：当自适应表单提交遇到任何验证错误时，错误处理程序会显示相应的错误消息。错误消息应清楚、简洁，并突出显示需要注意的特定字段。

* **突出显示错误的字段**：为了吸引用户对特定的错误字段的关注，错误处理程序会突出显示或在视觉上区分相应的字段。通过更改背景颜色、添加图标或边框或任何其他有助于用户快速找到和纠正错误的视觉提示来执行此操作。


## 失败/错误响应格式 {#failure-response-format}

如果服务器验证错误消息采用以下标准格式，则自适应表单会在字段级别显示错误。
以下代码说明了现有的失败响应结构：

```javascript
   {
    errorCausedBy : "SERVER_SIDE_VALIDATION/SERVICE_INVOCATION_FAILURE"
    errors : [
        {
             somExpression  : <somexpr>
             errorMessage / errorMessages : <validationMsg> / [<validationMsg>, <validationMsg>]
        }
    ]
    originCode : <target error Code>
    originMessage : <unstructured error message returned by service>
    }
```


其中：

* `errorCausedBy` 描述失败的原因。
* `errors` 提及未能通过验证标准的字段的SOM表达式以及验证错误消息。
* `originCode` 字段由 AEM 添加，包含由外部服务返回的 http 状态代码。
* `originMessage` 字段由 AEM 添加，包含由外部服务返回的原始错误数据。

随着 AEM Forms 版本的功能改进和后续更新，现有的失败响应结构变成了基于 RFC7807 的新格式，可向后兼容现有的失败响应结构：

```javascript
    {
        "type": "SERVER_SIDE_VALIDATION/FORM_SUBMISSION/SERVICE_INVOCATION/FAILURE/VALIDATION_ERROR", (required)
        "title": "Server side validation failed/Third party service invocation failed", (optional)
        "detail": "", (optional)
        "instance": "", (optional)
        "validationErrors" : [ (required)
            {
                "fieldName":"<SOM expression of the field whose data sent is invalid>",
                "dataRef":<JSONPath (or XPath) of the data element which is invalid>
                "details": ["Error Message(s) for the field"] (required)
    
            }
        ],
        "originCode": <Origin http status code>, (optional - if there is SERVER_SIDE_VALIDATION)
        "originMessage" : "<unstructured error message returned by service>" (optional - if there is SERVER_SIDE_VALIDATION)
    }
```


>[!NOTE]
>
> * 确保错误响应结构包括 **fieldName** 或 **dataRef**。
> * 确保 **ContentType** 标头是 **application/problem+json**。

其中：
* `type (required)` 指定失败类型。它可以是下列任一值：
   * `SERVER_SIDE_VALIDATION` 指示因服务器端验证导致的失败。
   * `FORM_SUBMISSION` 指示表单提交期间发生的失败。
   * `SERVICE_INVOCATION` 指示第三方服务调用期间发生的失败。
   * `FAILURE` 指示常见失败。
   * `VALIDATION_ERROR` 指示因验证错误导致的失败。

* `title (optional)` 提供失败的标题或简要描述。
* `detail (optional)` 提供有关失败的其他详细信息（如有必要）。
* `instance (optional)` 表示与失败相关的实例或标识符，并可帮助跟踪或识别具体发生的失败。
* `validationErrors (required)` 包含有关验证错误的信息。它包含以下字段：
   * `fieldname` 提及未能通过验证标准的字段的SOM表达式。
   * `dataRef` 表示未通过验证的字段的 JSON 路径或 XPath。
   * `details` 包含带错误字段的验证错误消息。
* `originCode (optional)` 字段由 AEM 添加，包含由外部服务返回的 http 状态代码。
* `originMessage (optional)` 字段由 AEM 添加，包含由外部服务返回的原始错误数据。

### 错误响应格式示例 {#sample-error-response-format}

用于显示错误响应的一些选项是：

+++  基于自适应表单 fieldName 属性


* **`Header:`** `content-type:application/problem+json`
* **`Response:`**

  ```javascript
          {
              "type": "VALIDATION_ERROR",
              "validationErrors": [
              {
              "fieldName": "guide[0].guide1[0].guideRootPanel[0].textbox1686647736683[0]",
              "dataRef": "",
              "details": [
              "Invalid ID supplied. Provided value is not correct!"
          ]
          }
          ]}
  ```

  您可以通过点按自适应表单中任何字段并选择 **[!UICONTROL 查看SOM表达式]**.

  ![在自定义错误处理程序中显示错误响应的自适应表单字段的SOM表达式](/help/forms/using/assets/custom-error-handler-somexpression.png)

+++


+++ 基于自适应表单dataRef属性

* **`Header:`** `content-type:application/problem+json`
* **`Response:`**

  ```javascript
      {
          "type": "VALIDATION_ERROR",
          "validationErrors": [
          {
              "fieldName": "",
              "dataRef": "/Pet/id",
              "details": [
              "Invalid ID supplied. Provided value is not correct!"
              ]
              }
      ]}
  ```

  ![在自定义错误处理程序中显示错误响应的自适应表单字段的数据引用](/help/forms/using/assets/custom-errorhandler-dataref.png)

您可以在表单组件的&#x200B;**[!UICONTROL 属性]**&#x200B;窗口中查看 dataRef 的值。

+++

## 前提条件 {#prerequisites}

在自适应Forms中使用自定义错误处理程序之前：

* 基础知识到 [创建自定义函数](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/adaptive-forms/custom-functions-aem-forms.html?lang=en#:~:text=AEM%20Forms%206.5%20introduced%20the,use%20them%20across%20multiple%20forms.).
* 安装最新版本的 [Apache Maven](https://maven.apache.org/download.cgi).


## 使用规则编辑器添加错误处理程序 {#add-error-handler-using-rule-editor}

通过使用[规则编辑器的调用服务](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke)操作，可以根据用于自适应表单的数据源来定义验证标准。如果您使用 RESTful Web 服务作为数据源，则可以在 Swagger 定义文件中定义验证标准。通过在自适应表单中使用错误处理函数和规则编辑器，可以有效地管理和自定义错误处理。可以使用规则编辑器定义条件，并配置在触发规则时要执行的所需操作。自适应表单根据预设验证标准验证您在字段中输入的信息。如果输入值未达到验证标准，则将在自适应表单的字段级别显示错误消息。

>[!NOTE]
>
> * 要将错误处理程序与规则编辑器的调用服务操作结合使用，请使用表单数据模型配置自适应表单。
> * 如果错误响应位于标准架构中，则提供默认错误处理程序以在字段上显示错误消息。还可以从自定义错误处理程序函数调用默认错误处理程序。

利用规则编辑器，您可以：

* [添加默认错误处理程序函数](#add-default-errror-handler)
* [添加自定义错误处理程序函数](#add-custom-errror-handler)


### 添加默认错误处理程序函数 {#add-default-errror-handler}

如果错误响应处于标准架构或服务器端验证失败，则支持默认错误处理程序以在字段上显示错误消息。
为了了解如何通过[规则编辑器的调用服务](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke)操作来使用默认错误处理程序，以具有&#x200B;**宠物 ID** 和&#x200B;**宠物名称**&#x200B;这两个字段的简单自适应表单为例，并在&#x200B;**宠物 ID** 字段上使用默认错误处理程序，以检查为调用外部服务而配置的 REST 端点所返回的各种错误，例如 `200 - OK`、`404 - Not Found`、`400 - Bad Request`。要使用规则编辑器的调用服务操作添加默认错误处理程序，请执行以下步骤：

1. 在创作模式下打开自适应表单，选择表单组件，然后选择 **[!UICONTROL 规则编辑器]** 以打开规则编辑器。
1. 选择&#x200B;**[!UICONTROL 创建]**。
1. 在规则的 **When** 部分中创建条件。例如，**在更改[宠物名称 ID 字段]**&#x200B;时，会从&#x200B;**选择状态**&#x200B;下拉列表中更改选择。
1. 在 **Then** 部分中，从&#x200B;**选择操作**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 调用服务]**。
1. 从&#x200B;**输入**&#x200B;部分中选择&#x200B;**发布服务**&#x200B;及其相应的数据绑定。例如，要验证&#x200B;**宠物 ID**，选择&#x200B;**发布服务**&#x200B;作为 **GET /pet/{petId}**，并在&#x200B;**输入**&#x200B;部分中选择&#x200B;**宠物 ID**。
1. 从&#x200B;**输出**&#x200B;部分中选择数据绑定。在&#x200B;**输出**&#x200B;部分中选择&#x200B;**宠物名称**。
1. 从&#x200B;**错误处理程序**&#x200B;部分中选择&#x200B;**[!UICONTROL 默认错误处理程序]**。
1. 单击&#x200B;**[!UICONTROL 完成]**。

![为表单中的字段验证检查添加默认错误处理程序](/help/forms/using/assets/default-error-handler.png)

根据此规则，将使用 REST 端点所调用的外部服务针对您为&#x200B;**宠物 ID** 输入的值来检查验证&#x200B;**宠物名称**。如果未达到基于数据源的验证标准，错误消息将在字段级别显示。

![在表单中添加默认错误处理程序来处理错误响应时显示默认错误消息](/help/forms/using/assets/default-error-message.png)

### 添加自定义错误处理程序函数 {#add-custom-errror-handler}

您可以添加自定义错误处理程序函数来执行一些操作，例如：

* 处理使用非标准或标准错误响应的错误响应。请务必注意，这些非标准错误响应不符合[错误响应的标准架构](#failure-response-format)。
* 将分析事件发送到任何分析平台。例如，Adobe Analytics。
* 显示带错误消息的模式对话框。

除了提及的操作之外，自定义错误处理程序还可用于执行满足特定用户要求的自定义函数。

自定义错误处理程序是一个函数（客户端库），旨在响应由外部服务返回的错误并向最终用户提供自定义响应。任何带注释 `@errorHandler` 的客户端库均被视为自定义错误处理程序函数。此注释有助于识别 `.js` 文件。

为了了解如何通过[规则编辑器的调用服务](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke)操作来创建和使用自定义错误处理程序，我们以具有&#x200B;**宠物 ID** 和&#x200B;**宠物名称**&#x200B;这两个字段的简单自适应表单为例，并在&#x200B;**宠物 ID** 字段上使用自定义错误处理程序，以检查为调用外部服务而配置的 REST 端点所返回的各种错误，例如 `200 - OK`、`404 - Not Found`、`400 - Bad Request`。

要在自适应表单中添加和使用自定义错误处理程序，请执行以下步骤：

1. [创建自定义错误处理程序](#create-custom-error-message)
1. [使用规则编辑器配置自定义错误处理程序](#use-custom-error-handler)

#### 1. 创建自定义错误处理程序 {#create-custom-error-message}

要创建自定义错误函数，请执行以下步骤：

1. 登录 `http://server:port/crx/de/index.jsp#`.
1. 在 `/apps` 文件夹下创建一个文件夹。例如，创建一个名为的文件夹 `experience-league`.
1. 保存更改。
1. 导航到已创建的文件夹并创建节点类型 `cq:ClientLibraryFolder` 作为 `clientlibs`.
1. 导航到新创建的 `clientlibs` 文件夹并添加 `allowProxy` 和 `categories` 属性：

   ![自定义库节点属性](/help/forms/using/assets/customlibrary-properties.png)

   >[!NOTE]
   >
   > 您可以提供任意名称来取代 `customfunctionsdemo`.

1. 保存更改。

1. 创建名为的文件夹 `js` 在 `clientlibs` 文件夹。
1. 创建名为的JavaScript文件 `functions.js` 在 `js` 文件夹
1. 创建名为的文件 `js.txt` 在 `clientlibs` 文件夹。
1. 保存更改。
创建的文件夹结构如下所示：

   ![创建的客户端库文件夹结构](/help/forms/using/assets/customclientlibrary_folderstructure.png)
1. 双击 `functions.js` 文件以打开编辑器。 该文件包含自定义错误处理程序的代码。
让我们将以下代码添加到该 JavaScript 文件中，以在浏览器控制台中显示从 REST 服务端点接收到的响应和标头。

   ```javascript
       /**
       * Custom Error handler
       * @name customErrorHandler Custom Error Handler Function
       * @errorHandler
       */
       function customErrorHandler(response, headers)
       {
           console.log("Custom Error Handler processing start...");
           console.log("response:"+JSON.stringify(response));
           console.log("headers:"+JSON.stringify(headers));
           guidelib.dataIntegrationUtils.defaultErrorHandler(response, headers);
           console.log("Custom Error Handler processing end...");
       }
   ```

   要从自定义错误处理程序调用默认错误处理程序，请使用以下示例代码行：
   `guidelib.dataIntegrationUtils.defaultErrorHandler(response, headers) `


1. 保存 `function.js`.
1. 导航到 `js.txt` 并添加以下代码：

   ```javascript
       #base=js
       functions.js
   ```

1. 保存 `js.txt` 文件。

现在，让我们了解如何使用 AEM Forms 中规则编辑器的调用服务来配置和使用自定义错误处理程序。

#### 2. 使用规则编辑器配置自定义错误处理程序 {#use-custom-error-handler}

在自适应表单中实施自定义错误处理程序之前，请确保&#x200B;**[!UICONTROL 客户端库类别]**&#x200B;中的客户端库名称与 `.content.xml` 文件的类别选项中指定的名称一致。

![在自适应表单容器配置中添加客户端库的名称](/help/forms/using/assets/client-library-category-name.png)

在本例中，客户端库名称提供为 `customfunctionsdemo` 在 `.content.xml` 文件。

要通过&#x200B;**[!UICONTROL 规则编辑器的调用服务]**&#x200B;操作使用自定义错误处理程序，请执行以下操作：

1. 在创作模式下打开自适应表单，选择表单组件，然后选择 **[!UICONTROL 规则编辑器]** 以打开规则编辑器。
1. 选择&#x200B;**[!UICONTROL 创建]**。
1. 在规则的 **When** 部分中创建条件。例如，在更改&#x200B;**[宠物名称 ID 字段]**&#x200B;时，会从&#x200B;**选择状态**&#x200B;下拉列表&#x200B;**更改**&#x200B;选择。
1. 在 **Then** 部分中，从&#x200B;**选择操作**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 调用服务]**。
1. 从&#x200B;**输入**&#x200B;部分中选择&#x200B;**发布服务**&#x200B;及其相应的数据绑定。例如，要验证&#x200B;**宠物 ID**，选择&#x200B;**发布服务**&#x200B;作为 **GET /pet/{petId}**，并在&#x200B;**输入**&#x200B;部分中选择&#x200B;**宠物 ID**。
1. 从&#x200B;**输出**&#x200B;部分中选择数据绑定。例如，在&#x200B;**输出**&#x200B;部分中选择&#x200B;**宠物名称**。
1. 从&#x200B;**[!UICONTROL 错误处理程序]**&#x200B;部分中选择&#x200B;**[!UICONTROL 自定义错误处理程序]**。
1. 单击&#x200B;**[!UICONTROL 完成]**。

![在表单中添加自定义错误处理程序以处理错误响应](/help/forms/using/assets/custom-error-handler.png)

根据此规则，将使用 REST 端点所调用的外部服务针对您为&#x200B;**宠物 ID** 输入的值来检查验证&#x200B;**宠物名称**。如果未达到基于数据源的验证标准，错误消息将在字段级别显示。

![在表单中添加自定义错误处理程序来处理错误响应](/help/forms/using/assets/custom-error-handler-message.png)

打开浏览器控制台，并检查从 REST 服务端点接收的响应和标头中是否有验证错误消息。

自定义错误处理程序函数负责根据错误响应来执行其他操作，例如显示模式对话框或发送分析事件。利用自定义错误处理程序函数，可以灵活地处理错误以满足具体用户要求。

<!-- 

## Configure Adaptive Form submission to add custom handlers {#configure-adaptive-form-submission}

If the server validation error message does not display in the standard format, you can enable asynchronous submission and add a custom error handler on Adaptive Form submission to convert the message into a standard format.

### Configure asynchronous Adaptive Form submission {#configure-asynchronous-adaptive-form-submission}

Before adding custom handler, you must configure the adaptive form for asynchronous submission. Execute the following steps:

1. In adaptive form authoring mode, select the Form Container object and select ![adaptive form properties](assets/configure_icon.png) to open its properties.
1. In the **[!UICONTROL Submission]** properties section, enable **[!UICONTROL Use asynchronous submission]**.
1. Select **[!UICONTROL Revalidate on server]** to validate the input field values on server before submission.
1. Select the Submit Action:

    * Select **[!UICONTROL Submit using Form Data Model]** and select the appropriate data model, if you are using RESTful web service based [form data model](work-with-form-data-model.md) as the data source.
    * Select **[!UICONTROL Submit to REST Service endpoint]** and specify the **[!UICONTROL Redirect URL/Path]**, if you are using RESTful web services as the data source.

    ![adaptive form submission properties](assets/af_submission_properties.png)

1. Select ![Save](assets/save_icon.png) to save the properties.

### Add custom error handler on Adaptive Form submission {#add-custom-error-handler-af-submission}

AEM Forms provides out-of-the-box success and error handlers for form submissions. Handlers are client-side functions that execute based on the server response. When an Adaptive Form is submitted, the data is transmitted to the server for validation, which returns a response to the client with information about the success or error event for the submission. The information is passed as parameters to the relevant handler to execute the function.

Execute the following steps to add custom error handler on Adaptive Form submission:

1. Open an Adaptive Form in authoring mode, select any form object, and select  to open the rule editor.
1. Select **[!UICONTROL Form]** in the Form Objects tree and select **[!UICONTROL Create]**.
1. Select **[!UICONTROL Error in Submission]** from the Event drop-down list.
1. Write a rule to convert custom error structure to the standard error structure and select **[!UICONTROL Done]** to save the rule.

The following is a sample code to convert a custom error structure to the standard error structure:

```javascript
var data = $event.data;
var som_map = {
    "id": "guide[0].guide1[0].guideRootPanel[0].Pet[0].id_1[0]",
    "name": "guide[0].guide1[0].guideRootPanel[0].Pet[0].name_2[0]",
    "status": "guide[0].guide1[0].guideRootPanel[0].Pet[0].status[0]"
};

var errorJson = {};
errorJson.errors = [];

if (data) {
    if (data.originMessage) {
        var errorData;
        try {
            errorData = JSON.parse(data.originMessage);
        } catch (err) {
            // not in json format
        }

        if (errorData) {
            Object.keys(errorData).forEach(function(key) {
                var som_key = som_map[key];
                if (som_key) {
                    var error = {};
                    error.somExpression = som_key;
                    error.errorMessage = errorData[key];
                    errorJson.errors.push(error);
                }
            });
        }
        window.guideBridge.handleServerValidationError(errorJson);
    } else {
        window.guideBridge.handleServerValidationError(data);
    }
}
```

The `var som_map` lists the SOM expression of the Adaptive Form fields that you want to transform into the standard format. You can view the SOM expression of any field in an adaptive form by tapping the field and selecting **[!UICONTROL View SOM Expression]**.

Using this custom error handler, the adaptive form converts the fields listed in `var som_map` to standard error message format. As a result, the validation error messages display at field-level in the adaptive form.

 -->


## 附加信息 {#additional-information}

* [创建基于独立核心组件的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)
* [为表单创建样式或主题](/help/forms/using/create-or-customize-themes-for-adaptive-forms-core-components.md)
* [创建自适应表单或将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)