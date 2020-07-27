---
title: 自适应表单的标准验证错误消息
seo-title: 自适应表单的标准验证错误消息
description: 使用自定义错误处理程序将自适应表单的验证错误消息转换为标准格式
seo-description: 使用自定义错误处理程序将自适应表单的验证错误消息转换为标准格式
uuid: 0d1f9835-3e28-41d3-a3b1-e36d95384328
contentOwner: anujkapo
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
discoiquuid: ec062567-1c6b-497b-a1e7-1dbac2d60852
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 0%

---


# 自适应表单的标准验证错误消息 {#standard-validation-error-messages}

自适应表单根据预先设置的验证标准验证您在字段中提供的输入。 验证标准引用自适应表单中字段的可接受输入值。 您可以根据与自适应表单一起使用的数据源设置验证条件。 例如，如果您使用RESTful Web服务作为数据源，则可以在Swagger定义文件中定义验证条件。

如果输入值满足验证条件，则这些值将提交给数据源。 否则，自适应表单会显示错误消息。

与此方法类似，自适应表单现在可以与自定义服务集成以执行数据验证。 如果输入值不满足验证条件并且服务器返回的验证错误消息为标准消息格式，则错误消息在表单的字段级别显示。

如果输入值不满足验证标准并且服务器验证错误消息不是标准消息格式，自适应表单提供将验证错误消息转换为标准格式以便它们在表单的字段级显示的机制。 可以使用以下任意两种方法将错误消息转换为标准格式：

* 在自适应表单提交中添加自定义错误处理程序
* 使用规则编辑器向调用服务操作添加自定义处理程序

本文介绍了验证错误消息的标准格式以及将错误消息从自定义格式转换为标准格式的说明。

## 标准验证错误消息格式 {#standard-validation-message-format}

如果服务器验证错误消息采用以下标准格式，自适应表单将在字段级别显示错误：

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

* `errorCausedBy` 描述失败原因
* `errors` 提到验证条件失败的字段的SOM表达式以及验证错误消息
* `originCode` 包含外部服务返回的错误代码
* `originMessage` 包含外部服务返回的原始错误数据

## 配置自适应表单提交以添加自定义处理程序 {#configure-adaptive-form-submission}

如果服务器验证错误消息未以标准格式显示，您可以启用异步提交并在自适应表单提交时添加自定义错误处理程序，以将消息转换为标准格式。

### 配置异步自适应表单提交 {#configure-asynchronous-adaptive-form-submission}

在添加自定义处理程序之前，必须配置自适应表单以进行异步提交。 执行以下步骤：

1. 在自适应表单创作模式中，选择表单容器对象，然 ![后点按自适应表单](assets/configure_icon.png) 属性以打开其属性。
1. 在“提 **[!UICONTROL 交属性]** ”部分，启用 **[!UICONTROL 使用异步提交]**。
1. 在提 **[!UICONTROL 交之前]** ，选择“在服务器上重新验证”以在服务器上验证输入字段值。
1. 选择提交操作：

   * 如果 **[!UICONTROL 使用基于RESTful Web服务的表单数据模型]** ，请选择“使用表单数据模型提交”, [然后选择相应的数](work-with-form-data-model.md) 据模型（如果使用RESTful Web服务）。
   * 如果 **[!UICONTROL 您使用RESTful Web服]** 务作为数据源 **[!UICONTROL ，请选择“提交到REST端点”并指]**&#x200B;定“重定向URL/路径”。

   ![自适应表单提交属性](assets/af_submission_properties.png)

1. 点按 ![保存](assets/save_icon.png) ，以保存属性。

### 在自适应表单提交中添加自定义错误处理程序 {#add-custom-error-handler-af-submission}

AEM Forms为表单提交提供开箱即用的成功和错误处理程序。 处理函数是基于服务器响应执行的客户端函数。 提交表单时，数据会被传输到服务器进行验证，服务器会向客户端返回一个响应，其中包含有关提交成功或错误事件的信息。 信息作为参数传递给相关处理函数以执行该函数。

执行以下步骤，在自适应表单提交时添加自定义错误处理程序：

1. 在创作模式下打开自适应表单，选择任何表单对象，然 <!--![Rule Editor](assets/af_edit_rules.png)--> 后点按以打开规则编辑器。
1. 在表 **[!UICONTROL 单对]** 象树中选择表单，然后点按 **[!UICONTROL 创建]**。
1. 从 **[!UICONTROL 事件下拉列表]** ，选择提交错误。
1. 编写规则以将自定义错误结构转换为标准错误结构，然后点 **[!UICONTROL 按完成]** 以保存规则。

以下是将自定义错误结构转换为标准错误结构的示例代码：

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

列表 `var som_map` 要转换为标准格式的自适应表单字段的SOM表达式。 您可以通过点按字段并选择视图SOM表达式，以自适应形式视图任何字段 **[!UICONTROL 的SOM表达式]**。

自适应表单使用此自定义错误处理程序将所列字段转换 `var som_map` 为标准错误消息格式。 结果，验证错误消息在自适应表单的字段级别显示。

## 使用调用服务操作添加自定义处理程序

执行以下步骤，添加错误处理程序以使用规则编辑器的调用服务操作将自定 [义错误结构转换为标](rule-editor.md) 准错误结构：

1. 在创作模式下打开自适应表单，选择任何表单对象，然 ![后点按规则编辑](assets/rule_editor_icon.png) 器以打开规则编辑器。
1. 点按&#x200B;**[!UICONTROL 创建]**。
1. 在规则的When **** （时间）部分创建条件。 例如，字[段的WhenName] 已更改。 从 **[!UICONTROL 选择状]** 态下拉 **[!UICONTROL 列表]** 中进行选择，以达到此条件。
1. 在“ **[!UICONTROL Then]** ”部分，从“选 **[!UICONTROL 择操作”下]** 拉列表中选 **[!UICONTROL 择“调用服务]** ”。
1. 从“输入”部分选择Post服务及其相应的 **[!UICONTROL 数据]** 绑定。 例如，如果要验证自适应表 **单中的** Name **、ID**&#x200B;和Status字段，请选择Post服务(pet)，并在InputProidSection中选择pet.name、pet.id和pet. ******** status。

通过此规则，只要第2步中定义的字 **段发生更改**，并且您从表单中的字段中跳出，您为Name **、ID和Status****** 字段输入的值即会被验证。

1. 从 **[!UICONTROL 模式选择]** 下拉列表中选择代码编辑器。
1. 点按 **[!UICONTROL 编辑代码]**。
1. 从现有代码中删除以下行：

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
   ```

1. 编写规则以将自定义错误结构转换为标准错误结构，然后点 **[!UICONTROL 按完成]** 以保存规则。
例如，在结尾处添加以下示例代码，将自定义错误结构转换为标准错误结构：

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

   列表 `var som_map` 要转换为标准格式的自适应表单字段的SOM表达式。 您可以通过点按字段并从更多选项(...)菜单中选择 **[!UICONTROL 视图SOM视图]** , **[!UICONTROL 以自适应形]** 式对任何字段的SOM表达式进行表达式。

   确保将示例代码的以下代码行复制到自定义错误处理程序：

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   executeOperation API包括基于 `null` 新 `errorHandler` 的自定义错误处理程序的参数和参数。

   自适应表单使用此自定义错误处理程序将所列字段转换 `var som_map` 为标准错误消息格式。 结果，验证错误消息在自适应表单的字段级别显示。