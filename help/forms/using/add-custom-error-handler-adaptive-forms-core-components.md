---
title: 在基于AEM自适应Forms核心组件的自适应Forms中添加自定义错误处理程序
seo-title: Error Handlers in Adaptive Forms for AEM Adaptive Forms core components
description: AEM Forms使用配置为调用外部服务的REST端点为表单提供现成的成功和错误处理程序。 您可以在AEM自适应表单中添加默认错误处理程序和自定义错误处理程序。
seo-description: Error handler function and Rule Editor in Adaptive Forms core components helps you to effectively manage and customize error handling. You can add a default error handler as well as custom error handler in an AEM Adaptive Form.
keywords: 添加自定义错误处理程序、添加默认错误处理程序、在表单中添加错误处理程序、使用规则编辑器的调用服务添加自定义错误处理程序、配置规则编辑器添加自定义错误处理程序、使用规则编辑器添加自定义错误处理程序
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms
source-git-commit: 28cc10b79d2ac8cf12ddfd0bf7d1a8e013fe6238
workflow-type: tm+mt
source-wordcount: '2284'
ht-degree: 1%

---


# 自适应Forms中的错误处理程序（核心组件） {#error-handlers-in-adaptive-form}

AEM Forms为表单提交提供现成的成功和错误处理程序。 它还提供自定义错误处理程序函数的功能。 例如，您可以在后端为特定的错误代码调用自定义工作流，或者通知客户服务已停止。处理器是基于服务器响应执行的客户端功能。 当使用API调用外部服务时，数据将传输到服务器进行验证，服务器将响应返回到客户端，其中包含有关提交的成功或错误事件的信息。 信息将作为参数传递给相关处理程序以执行函数。 错误处理程序有助于管理和显示遇到的错误或验证问题。

![错误处理程序工作流，用于了解如何在表单中添加自定义错误处理程序](/help/forms/using/assets/error-handler-workflow.png)

自适应表单根据预设验证条件验证您在字段中提供的输入，并检查配置为调用外部服务的REST端点返回的各种错误。 您可以根据在自适应表单中使用的数据源设置验证条件。 例如，如果使用RESTful Web服务作为数据源，则可以在Swagger定义文件中定义验证条件。

如果输入值满足验证条件，则这些值将提交给数据源，否则，自适应表单将使用错误处理程序显示错误消息。 与这种方法类似，自适应Forms集成了自定义错误处理程序以执行数据验证。 如果输入值不符合验证条件，则错误消息将在自适应表单中的字段级别显示。 当服务器返回的验证错误消息采用标准消息格式时，会发生这种情况。


## 错误处理程序的使用 {#uses-of-error-handler}

错误处理程序有多种用途。 下面列出了错误处理程序函数的一些用法：

* **执行验证**：错误处理从根据预定义的规则或标准验证用户输入开始。 当用户填写自适应表单时，错误处理程序会验证输入以确保它满足所需的格式、长度或任何其他约束。

* **提供实时反馈**：检测到任何错误时，错误处理程序会立即向用户显示反馈，例如相应表单字段下的内联错误消息。 此反馈可帮助用户识别和更正错误，而无需提交表单并等待响应。


* **显示错误消息**：当自适应表单提交遇到任何验证错误时，错误处理程序会显示相应的错误消息。 错误消息应简明扼要，并突出显示需要注意的特定字段。

* **突出显示错误的字段**：为了吸引用户注意特定的不正确字段，错误处理程序会突出显示或视觉上区分相应的字段。 此操作可通过更改背景颜色、添加图标或边框或任何其他帮助用户快速找到并解决错误的可视提示来执行。


## 失败/错误响应格式 {#failure-response-format}

如果服务器验证错误消息采用以下标准格式，则自适应表单会在字段级别显示错误。
以下代码说明了现有的故障响应结构：

```javascript
   {
    errorCausedBy : "SERVER_SIDE_VALIDATION/SERVICE_INVOCATION_FAILURE"
    errors : [
        {
             errorMessage / errorMessages : <validationMsg> / [<validationMsg>, <validationMsg>]
        }
    ]
    originCode : <target error Code>
    originMessage : <unstructured error message returned by service>
    }
```


其中：

* `errorCausedBy` 描述失败的原因。
* `errors` 提及未能通过验证标准的字段的限定字段名以及验证错误消息。
* `originCode` 字段由AEM添加，包含由外部服务返回的http状态代码。
* `originMessage` 由AEM添加的字段，其中包含外部服务返回的原始错误数据。

随着AEM Forms版本的功能改进及后续更新，现有故障响应结构在RFC7807的基础上变更为新的形式，向后兼容现有故障响应结构：

```javascript
    {
        "type": "SERVER_SIDE_VALIDATION/FORM_SUBMISSION/SERVICE_INVOCATION/FAILURE/VALIDATION_ERROR", (required)
        "title": "Server side validation failed/Third party service invocation failed", (optional)
        "detail": "", (optional)
        "instance": "", (optional)
        "validationErrors" : [ (required)
            {
                "fieldName":"<qualified fieldname of the field whose data sent is invalid>",
                "dataRef":<JSONPath (or XPath) of the data element which is invalid>
                "details": ["Error Message(s) for the field"] (required)
    
            }
        ],
        "originCode": <Origin http status code>, (optional - in case of SERVER_SIDE_VALIDATION)
        "originMessage" : "<unstructured error message returned by service>" (optional - in case of SERVER_SIDE_VALIDATION)
    }
```


>[!NOTE]
>
> * 请确保错误响应结构包含 **fieldName** 或 **dataRef**.
> * 确保 **内容类型** 标题为 **application/problem+json**.

其中：
* `type (required)` 指定失败类型。 它可以是以下值之一：
   * `SERVER_SIDE_VALIDATION` 表示由于服务器端验证而失败。
   * `FORM_SUBMISSION` 指示表单提交过程中失败
   * `SERVICE_INVOCATION` 指示在第三方服务调用期间发生故障。
   * `FAILURE` 表示一般故障。
   * `VALIDATION_ERROR` 表示由于验证错误而失败。

* `title (optional)` 提供失败的标题或简短描述。
* `detail (optional)` 提供了有关故障的其他详细信息（如有必要）。
* `instance (optional)` 表示与失败关联的实例或标识符，并有助于跟踪或识别失败的特定发生情况。
* `validationErrors (required)` 包含有关验证错误的信息。 它包括以下字段：
   * `fieldname` 提及未能通过验证标准的字段的限定字段名。
   * `dataRef` 表示验证失败的字段的JSON路径或XPath。
   * `details` 包含验证错误消息和错误字段。
* `originCode (optional)` 字段由AEM添加，包含由外部服务返回的http状态代码
* `originMessage (optional)` 由AEM添加的字段，其中包含外部服务返回的原始错误数据。

### 示例错误响应格式 {#sample-error-response-format}

显示错误响应的部分选项包括：

+++  基于自适应表单fieldName属性


* **`Header:`** `content-type:application/problem+json`
* **`Response:`**

  ```javascript
          {
              "type": "VALIDATION_ERROR",
              "validationErrors": [
              {
              "fieldName": "$form.PetId",
              "dataRef": "",
              "details": [
              "Invalid ID supplied. Provided value is not correct!"
          ]
          }
          ]}
  ```


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
              "dataRef": "$.Pet.id",
              "details": [
              "Invalid ID supplied. Provided value is not correct!"
              ]
              }
      ]}
  ```

+++

## 前提条件 {#prerequisites}

在自适应Forms中使用错误处理程序之前：

* [为您的AEM Cloud Service环境启用自适应Forms核心组件](enable-adaptive-forms-core-components.md).
* 基础知识到 [创建自定义函数](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/adaptive-forms/custom-functions-aem-forms.html?lang=en#:~:text=AEM%20Forms%206.5%20introduced%20the,use%20them%20across%20multiple%20forms.).
* 安装最新版本的 [Apache Maven](https://maven.apache.org/download.cgi).

## 使用规则编辑器添加错误处理程序 {#add-error-handler-using-rule-editor}

使用 [规则编辑器的调用服务](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke) 操作，您可以根据在自适应表单中使用的数据源定义验证条件。 如果将RESTful Web服务用作数据源，则可以在Swagger定义文件中定义验证条件。 通过使用Adaptive Forms中的错误处理程序函数和规则编辑器，您可以有效地管理和自定义错误处理。 您可以使用规则编辑器定义条件，并配置要在触发规则时执行的所需操作。 自适应表单根据预设验证条件验证您在字段中输入的输入。 如果输入值不符合验证条件，则会在自适应表单的字段级别显示错误消息。

>[!NOTE]
>
> * 要将错误处理程序与规则编辑器的调用服务操作结合使用，请使用表单数据模型配置自适应Forms 。
> * 如果错误响应位于标准架构中，则提供默认错误处理程序以在字段上显示错误消息。 您还可以从自定义错误处理程序函数中调用默认错误处理程序。

使用规则编辑器，您可以：

* [添加默认错误处理程序函数](#add-default-errror-handler)
* [添加自定义错误处理程序函数](#add-custom-errror-handler)


### 添加默认错误处理程序函数 {#add-default-errror-handler}

如果错误响应位于标准架构中或服务器端验证失败，则支持使用默认错误处理程序在字段上显示错误消息。
了解如何使用默认错误处理程序，请参见 [规则编辑器的调用服务](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke) 操作，以带有两个字段的简单自适应表单为例， **宠物Id** 和 **宠物名称** 并在以下位置使用默认错误处理程序 **宠物Id** 用于检查配置为调用外部服务的REST端点返回的各种错误的字段，例如， `200 - OK`，`404 - Not Found`， `400 - Bad Request`. 要使用规则编辑器的“调用服务”操作添加默认错误处理程序，请执行以下步骤：

1. 在创作模式下打开自适应表单，选择表单组件并点按 **[!UICONTROL 规则编辑器]** 以打开规则编辑器。
1. 点按&#x200B;**[!UICONTROL 创建]**。
1. 在中创建条件 **时间** 部分。 例如， **时间[宠物ID字段的名称]** 已更改。 Select已从 **选择状态** 下拉列表。
1. 在 **则** 部分，选择 **[!UICONTROL 调用服务]** 从 **选择操作** 下拉列表。
1. 选择 **发布服务** 及其相应的数据绑定 **输入** 部分。 例如，验证 **宠物Id**，选择一个 **发布服务** 作为 **GET/pet/{petId}** 并选择 **宠物Id** 在 **输入** 部分。
1. 从中选择数据绑定 **输出** 部分。 选择 **宠物名称** 在 **输出** 部分。
1. 选择 **[!UICONTROL 默认错误处理程序]** 从 **错误处理程序** 部分。
1. 单击&#x200B;**[!UICONTROL 完成]**。

![在表单中为字段验证检查添加默认错误处理程序](/help/forms/using/assets/default-error-handler.png)

作为此规则的结果，您输入的值 **宠物Id** 检查验证 **宠物名称** 使用REST端点调用的外部服务。 如果基于数据源的验证标准失败，则错误消息将在字段级别显示。

![在表单中添加默认错误处理程序以处理错误响应时，显示默认错误消息](/help/forms/using/assets/default-error-message.png)

### 添加自定义错误处理程序函数 {#add-custom-errror-handler}

您可以添加自定义错误处理程序函数以执行某些操作，例如：

* 处理使用非标准或标准错误响应的错误响应。 请务必注意，这些非标准错误响应不符合 [错误响应的标准架构](#failure-response-format).
* 将analytics事件发送到任何analytics平台。 例如，Adobe Analytics.
* 显示带有错误消息的模式对话框。

除了上述操作之外，还可使用自定义错误处理程序来执行符合特定用户要求的自定义函数。

自定义错误处理程序是一个函数（客户端库），旨在响应外部服务返回的错误，并向最终用户提供自定义响应。 任何带注释的客户端库 `@errorHandler` 被视为自定义错误处理程序函数。 此注释有助于识别 `.js` 文件。

要了解如何使用创建和使用自定义错误处理程序，请执行以下操作 [规则编辑器的调用服务](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke) 操作，我们以带有两个字段的自适应表单为例， **宠物Id** 和 **宠物名称** 并在中使用自定义错误处理程序 **宠物Id** 用于检查配置为调用外部服务的REST端点返回的各种错误的字段，例如， `200 - OK`，`404 - Not Found`， `400 - Bad Request`.

要在自适应表单中添加和使用自定义错误处理程序，请执行以下步骤：

1. [创建自定义错误处理程序](#create-custom-error-message)
1. [使用规则编辑器配置自定义错误处理程序](#use-custom-error-handler)

#### 1.创建自定义错误处理程序 {#create-custom-error-message}

要创建自定义错误函数，请执行以下步骤：

1. 登录 `http://server:port/crx/de/index.jsp#`.
1. 在下创建文件夹 `/apps` 文件夹。 例如，创建一个名为的文件夹 `experience-league`.
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

   ![已创建客户端库文件夹结构](/help/forms/using/assets/customclientlibrary_folderstructure.png)
1. 双击 `functions.js` 文件以打开编辑器。 文件包含自定义错误处理程序的代码。
让我们将以下代码添加到JavaScript文件中，以在浏览器控制台中显示从REST服务端点收到的响应和标头。

   ```javascript
       /** 
       Custom Error handler
       * @name customErrorHandler Custom Error Handler Function
       * @errorHandler
       */
       function customErrorHandler(response, headers, globals)
       {
           console.log("Custom Error Handler processing start...");
           console.log("response:"+JSON.stringify(response));
           console.log("headers:"+JSON.stringify(headers));
           alert("CustomErrorHandler - Please enter valid PetId.")
           globals.invoke('defaultErrorHandler',response, headers)
           console.log("Custom Error Handler processing end...");
       }
   ```

   要从自定义错误处理程序中调用默认错误处理程序，请使用下面一行示例代码：
   `globals.invoke('defaultErrorHandler',response, headers) `

1. 保存 `function.js`.
1. 导航到 `js.txt` 并添加以下代码：

   ```javascript
       #base=js
       functions.js
   ```

1. 保存 `js.txt` 文件。

现在，让我们了解如何在AEM Forms中使用规则编辑器的调用服务配置和使用自定义错误处理程序。

#### 2.使用规则编辑器配置自定义错误处理程序 {#use-custom-error-handler}

在自适应表单中实施自定义错误处理程序之前，请确保客户端库名称位于 **[!UICONTROL 客户端库类别]** 与的类别选项中指定的名称对齐 `.content.xml` 文件。

![在自适应表单容器配置中添加客户端库的名称](/help/forms/using/assets/client-library-category-name-core-component.png)

在本例中，客户端库名称提供为 `customfunctionsdemo` 在 `.content.xml` 文件。

使用自定义错误处理程序 **[!UICONTROL 规则编辑器的调用服务]** 操作：

1. 在创作模式下打开自适应表单，选择表单组件并点按 **[!UICONTROL 规则编辑器]** 以打开规则编辑器。
1. 点按&#x200B;**[!UICONTROL 创建]**。
1. 在中创建条件 **时间** 部分。 例如，当 **[宠物ID字段的名称]** 已更改，请选择 **已更改** 从 **选择状态** 下拉列表。
1. 在 **则** 部分，选择 **[!UICONTROL 调用服务]** 从 **选择操作** 下拉列表。
1. 选择 **发布服务** 及其相应的数据绑定 **输入** 部分。 例如，验证 **宠物Id**，选择一个 **发布服务** 作为 **GET/pet/{petId}** 并选择 **宠物Id** 在 **输入** 部分。
1. 从中选择数据绑定 **输出** 部分。 例如，选择 **宠物名称** 在 **输出** 部分。
1. 选择 **[!UICONTROL 自定义错误处理程序]** 从 **[!UICONTROL 错误处理程序]** 部分。
1. 单击&#x200B;**[!UICONTROL 完成]**。

![在表单中添加自定义错误处理程序以处理错误响应](/help/forms/using/assets/custom-error-handler.png)

作为此规则的结果，您输入的值 **宠物Id** 检查验证 **宠物名称** 使用REST端点调用的外部服务。 如果基于数据源的验证标准失败，则错误消息将在字段级别显示。

![在表单中添加自定义错误处理程序以处理错误响应](/help/forms/using/assets/custom-error-handler-message-core-component.png)

打开浏览器控制台并检查从REST服务端点收到的响应和标头，以查看验证错误消息。

自定义错误处理程序函数负责根据错误响应执行其他操作，如显示模式对话框或发送Analytics事件。 自定义错误处理程序函数提供了灵活性，让您可以根据特定用户要求定制错误处理。
