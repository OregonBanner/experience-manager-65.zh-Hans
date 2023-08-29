---
title: 自适应表单的标准验证错误消息
seo-title: Standard validation error messages for adaptive forms
description: 使用自定义错误处理程序将自适应表单的验证错误消息转换为标准格式
seo-description: Transform the validation error messages for adaptive forms into standard format using custom error handlers
uuid: 0d1f9835-3e28-41d3-a3b1-e36d95384328
contentOwner: anujkapo
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
discoiquuid: ec062567-1c6b-497b-a1e7-1dbac2d60852
source-git-commit: 34be3b4695679a9b5e8001d28f05ed804f929e61
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 0%

---


# 自适应表单的标准验证错误消息 {#standard-validation-error-messages}

自适应表单根据预设的验证条件验证您在字段中提供的输入。 验证标准是指自适应表单中字段的可接受输入值。 您可以基于在自适应表单中使用的数据源设置验证条件。 例如，如果使用RESTful Web服务作为数据源，则可以在Swagger定义文件中定义验证条件。

如果输入值满足验证条件，则会将值提交到数据源。 否则，自适应表单会显示错误消息。

与这种方法类似，自适应表单现在可与自定义服务集成以执行数据验证。 如果输入值不符合验证条件，并且服务器返回的验证错误消息采用标准消息格式，则错误消息将在表单的字段级别显示。

如果输入值不符合验证条件，并且服务器验证错误消息不是标准消息格式，则自适应表单提供一种机制，将验证错误消息转换为标准格式，以便它们在表单的字段级显示。 您可以使用以下两种方法中的任意一种将错误消息转换为标准格式：

* 在自适应表单提交中添加自定义错误处理程序
* 添加自定义处理程序以使用规则编辑器调用服务操作

本文介绍了验证错误消息的标准格式，以及将错误消息从自定义格式转换为标准格式的说明。

## 标准验证错误消息格式 {#standard-validation-message-format}

如果服务器验证错误消息采用以下标准格式，则自适应表单在字段级别显示错误：

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

* `errorCausedBy` 描述失败的原因
* `errors` 提及未能通过验证标准的字段的SOM表达式以及验证错误消息
* `originCode` 包含外部服务返回的错误代码
* `originMessage` 包含外部服务返回的原始错误数据

## 配置自适应表单提交以添加自定义处理程序 {#configure-adaptive-form-submission}

如果服务器验证错误消息未以标准格式显示，您可以启用异步提交，并在自适应表单提交中添加自定义错误处理程序，以将消息转换为标准格式。

### 配置异步自适应表单提交 {#configure-asynchronous-adaptive-form-submission}

添加自定义处理程序之前，必须为异步提交配置自适应表单。 执行以下步骤：

<!-- 1. In adaptive form authoring mode, select the Form Container object and tap ![adaptive form properties](assets/af_properties.png) to open its properties.
1. In the **[!UICONTROL Submission]** properties section, enable **[!UICONTROL Use asynchronous submission]**.
1. Select **[!UICONTROL Revalidate on server]** to validate the input field values on server before submission.
1. Select the Submit Action:

    * Select **[!UICONTROL Submit using Form Data Model]** and select the appropriate data model, if you are using RESTful web service based [form data model](work-with-form-data-model.md) as the data source.
    * Select **[!UICONTROL Submit to REST endpoint]** and specify the **[!UICONTROL Redirect URL/Path]**, if you are using RESTful web services as the data source.

    ![adaptive form submission properties](assets/af_submission_properties.png)

1. Tap ![Save](assets/af_save.png) to save the properties.-->

### 在自适应表单提交中添加自定义错误处理程序 {#add-custom-error-handler-af-submission}

AEM Forms为表单提交提供现成的成功和错误处理程序。 处理器是基于服务器响应执行的客户端功能。 在提交表单时，数据被传输到服务器进行验证，服务器将响应返回到客户端，其中包含有关提交的成功或错误事件的信息。 信息将作为参数传递给相关处理程序以执行函数。

执行以下步骤以对自适应表单提交添加自定义错误处理程序：

1. 在创作模式下打开自适应表单，选择任意表单对象，然后点击 <!--![Rule Editor](assets/af_edit_rules.png)--> 以打开规则编辑器。
1. 选择 **[!UICONTROL 表单]** 在表单对象树中，然后点按 **[!UICONTROL 创建]**.
1. 选择 **[!UICONTROL 提交时出错]** 从“事件”下拉列表中。
1. 编写规则以将自定义错误结构转换为标准错误结构，然后点击 **[!UICONTROL 完成]** 以保存规则。

下面是将自定义错误结构转换为标准错误结构的示例代码：

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

此 `var som_map` 列出要转换为标准格式的自适应表单字段的SOM表达式。 您可以通过点按任意字段并选择 **[!UICONTROL 查看SOM表达式]**.

使用此自定义错误处理程序，自适应表单转换 `var som_map` 更改为标准错误消息格式。 因此，验证错误消息会在自适应表单的字段级别显示。

## 使用“调用服务”操作添加自定义处理程序

执行以下步骤可添加错误处理程序，以使用将自定义错误结构转换为标准错误结构 [规则编辑器的](rule-editor.md) 调用服务操作：

<!-- 1. Open the adaptive form in authoring mode, select any form object, and tap ![Rule Editor](assets/af_edit_rules.png) to open the rule editor.
1. Tap **[!UICONTROL Create]**.
1. Create a condition in the **[!UICONTROL When]** section of the rule. For example, When[Name of field] is changed. Select **[!UICONTROL is changed]** from the **[!UICONTROL Select State]** drop-down list to achieve this condition.
1. In the **[!UICONTROL Then]** section, select **[!UICONTROL Invoke Service]** from the **[!UICONTROL Select Action]** drop-down list.
1. Select a Post service and its corresponding data bindings from the **[!UICONTROL Input]** section. For example, if you want to validate **Name**, **ID**, and **Status** fields in the adaptive form, select a Post service (pet) and select pet.name, pet.id, and pet.status in the **[!UICONTROL Input]** section.-->

    作为该规则的结果，您在步骤2中定义的字段发生更改并且您从表单中的字段跳出后，就会验证您为**Name**、**ID**和**Status**字段输入的值。

1. 选择 **[!UICONTROL 代码编辑器]** 从模式选择下拉列表中。
1. 点按 **[!UICONTROL 编辑代码]**.
1. 从现有代码中删除以下行：

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
   ```

1. 编写规则以将自定义错误结构转换为标准错误结构，然后点击 **[!UICONTROL 完成]** 以保存规则。
例如，在末尾添加以下示例代码以将自定义错误结构转换为标准错误结构：

   ```javascript
   var errorHandler = function(jqXHR, data) {
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
   };
   
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   此 `var som_map` 列出要转换为标准格式的自适应表单字段的SOM表达式。 您可以通过点按任意字段并选择 **[!UICONTROL 查看SOM表达式]** 从 **[!UICONTROL 更多选项]** (...)菜单。

   请确保将以下一行示例代码复制到自定义错误处理程序中：

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   executeOperation API包含 `null` 和 `errorHandler` 基于新的自定义错误处理程序的参数。

   使用此自定义错误处理程序，自适应表单转换 `var som_map` 更改为标准错误消息格式。 因此，验证错误消息会在自适应表单的字段级别显示。